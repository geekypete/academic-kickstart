---
title: "Shell Tips and Tricks"
date: 2018-07-13T15:52:18-05:00
categories:
  - "tutorial"
tags:
  - "ssh"
  - "shell"
  - "bash"
comments: true
---


This is a simple list of tips and tricks for the shell that I discovered over
the course of many years of messing around in shell and wanted to coalesce into
a single document, partly to remember, and partly to share with others. 

Persistent SSH Sessions
--------

In order to ensure that your SSH sessions do not get disconnected after a period
of inactivity simply add the following to your `.ssh/config` file:
```  
Host *
    ServerAliveInterval 300
    ServerAliveCountMax 2
```  
Now your SSH session will persist, and not be killed by an overzealous firewall.

Mogrify with GNU Parallel
--------

Having recently needed to convert a large quantity of images to another format I stumbled upon GNU parallel, a powerful and simple utility for executing shell jobs in parallel.

Here is a simple example where I use GNU parallel to parallelize the conversion of a series of svs (a format commonly used for pathology images from digital whole slide scanners) to tiff, a much more common format for scientific images. Simply prepend parallel to your command, and GNU parallel will execute the command with the line as arguments. The triple colon indicates that the list of svs files in the directory are being passed into GNU parallel where they can be chunked out into jobs across the ten specified concurrent processes.
```  
# Using 10 cores instead the default of all possible cores 
parallel mogrify -j10 -verbose -format tif ::: *.svs
```  
Showing Diskspace Usage by Directory
--------
I often work on HPC systems where I cannot easily install my usual disk usage monitoring utilities, like the highly recommended NCDU utility. Instead I need to resort to the `du` command to accomplish this task. One of the most common questions I have is how much space is each subdirectory in my current directory consuming. To see this, we can use the command:

```
du -h --max-depth=1 | sort -hr
```
This uses the disk usage (`du`) utility to list the disk usage of each subdirectory within the current directory by restricting the search to a max depth of 1, that is, it does not recursively list the contents of each directory, only the total disk usage of each subdirectory within the current directory. The `-h` command ensures that the results are printed in a human readable format. The pipe to `sort -hr` ensures that the results are sorted by size (`-h` is used as the original sizes were also printed in a human readable format, so this argument is necessary to sort them as such), and printed in descending order (by using `-r` for reverse).
