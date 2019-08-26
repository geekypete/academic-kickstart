---
title: "Introducing Parallel into Shell"
date: 2018-12-17T15:03:25-06:00
draft: false 
categories:
  - "tutorial"
tags:
  - "parallel"
  - "shell"
  - "bash"
---

Having recently needed to convert the format of an enormous quantity of images I stumbled upon GNU parallel, a powerful and simple utility for replacing shell loops with a parallel alternative.  

Mogrify with GNU Parallel
--------
Here is a simple example where I use GNU parallel to parallelize the conversion of a series of svs (a format commonly used for pathology images from digital whole slide scanners) to tiffs, a much more common format. Simply prepend parallel to your command, and GNU parallel will execute the command with the line as arguments. The triple colon indicates that the list of svs files in the directory are being passed into GNU parallel where they can be chunked out into jobs across the ten specified concurrent processes.
```  
# Using 10 cores instead the default of all possible cores 
parallel mogrify -j10 -verbose -format tif ::: *.svs
```  


