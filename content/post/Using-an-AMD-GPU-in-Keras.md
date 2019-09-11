---
title: "Using an AMD GPU in Keras"
date: 2019-04-04T12:42:08-05:00
categories:
  - "tutorial"
tags:
  - "Keras"
  - "deep learning"
  - "OpenCV"
  - "PlaidML"
draft: false 
comments: true
---

A while ago my research lab acquired a new workstation, but my PI, well meaning as he is, purchased a system with an AMD GPU (FirePro W7100) rather than an Nvidia card, so CUDA is not an option. For the longest time I thought deep learning was not going to happen with TensorFlow using an OpenCV library, but I recently stumbled on a library `PlaidML`, a tensor compiler that allows for the use of OpenCL devices, and sits as a layer underneath common machine learning frameworks. I use an Arch based distro (Manjaro) so this guide is specific to Arch, but it's likely that this process is not too different for other distros. 

First check what GPU you have installed on your system.

``` bash
lspci | grep VGA
```

And you should see output something like:

``` bash
03:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Tonga PRO GL 
[FirePro W7100]                                                                       
```

Now make sure you have a graphics driver installed:
```bash
glxinfo | grep -i vendor
```
which yields: 
```bash
server glx vendor string: SGI
client glx vendor string: Mesa Project and SGI
   Vendor: X.Org (0x1002)
OpenGL vendor string: X.Org
```
In my case I am using the AMD Mesa open driver rather than the proprietary AMD Pro driver. 

Now I need to install the OpenCL library. I used the proprietary library from the AMD pro driver which you can install, without installing the full driver, using:
```bash
yaourt -S opencl-amd
```
To make sure that got installed you can use clinfo, after installing it of course:
```bash
sudo pacman -S clinfo
clinfo
```
If you get `Number of Platforms 0` you have done something wrong. If you get a long list of details that include the `Device Board Name (AMD)` with the name of your GPU, in my case AMD FirePro W7100, then you should be good to move onto the next step and install the PlaidML library!

PlaidML is a Python library which I recommend installing in a virtual environment as that is just good practice, but its up to you. To install:

```bash
pip install plaidml-keras plaidbench
```

Then choose the accelerator you would like to use (most likely the AMD GPU you have configured). PlaidML will offer a series of numbered devices after running the following command, select the one corresponding to the GPU you would like to use.

```bash
plaidml-setup
```

Now you should be good to go! The next time you build/run a model in Keras import PlaidML first.

```python
import os
os.environ["KERAS_BACKEND"] = "plaidml.keras.backend"
import keras
```
