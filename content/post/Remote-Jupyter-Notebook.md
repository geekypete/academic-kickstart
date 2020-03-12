---
title: "Using a Jupyter Notebook on a Remote Host"
date: 2020-03-11T10:16:22-05:00
draft: false 
---

It is often desirable to connect to a remote Jupyter notebook instance in order to leverage the computational resources of a remote workstation while working from a less powerful system, such as a laptop. Jupyter notebook, in combination with SSH, makes this process quite simple.

Configuring a Remote Jupyter Session
--------
- First, ensure Jupyter notebook is installed on both the host system (the remote workstation you would like the Jupyter session to execute on) and the local system (the laptop or other computer you would like to interactively run the Jupyter session in a browser while it runs on the host).
- SSH into your remote host, and execute the following command:
```
jupyter notebook --no-browser --port=8889
```
You should see output similar to that below:
```
[I 10:25:19.448 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 10:25:19.451 NotebookApp] 
    
    To access the notebook, open this file in a browser:
        file:///home/username/.local/share/jupyter/runtime/nbserver-26769-open.html
    Or copy and paste one of these URLs:
        http://localhost:8889/?token=7f666b19a0ce0b0d7c39070361337adfcb8324f70dcff6bc
     or http://127.0.0.1:8889/?token=7f666b19a0ce0b0d7c39070361337adfcb8324f70dcff6bc
```
- In your local computer open a terminal and execute the following command:
```
ssh -N -f -L localhost:8888:localhost:8889 username@your_remote_host_ip
# Update `username` to your username on your remote host
# Update `your_remote_host_ip` to the ip address or alias of your remote host
```
- Now open your web browser of choice, and enter the following into the address bar:
```
localhost:8888
```
You will be presented with a list of Jupyter notebooks present in the working directory of the remote host. Select the one you would like to work on. You should be able to work just as you would locally, except your code will be executed on the remote host, and any changes to your Jupyter notebook will be saved on the remote host.

Configuring a Remote Jupyter Session on a High Performance Computer (HPC)
------
What if you would like to run a remote Jupyter instance on your institutional HPC? If you have the `idev` (`I`nteractive `DEV`elopment) application, developed by the Texas Advanced Computing Center (TACC) and deployed on many supercomputers, you will be able to do just that!

First we will need to login to our HPC with port forwarding enabled:
```
ssh -L 8888:127.0.01:7000 userID@hpc.address.edu
```
Replace the `userID` with your institutional userID for accessing your particular HPC system. Replace the `hpc.address.edu` with the address you use to ssh into your HPC.

Now start an idev session with port forwarding enabled. Feel free to configure your idev session as you see fit. If you are not familiar with idev, please refer to the guide here: https://portal.tacc.utexas.edu/software/idev#how-to-use-idev.
