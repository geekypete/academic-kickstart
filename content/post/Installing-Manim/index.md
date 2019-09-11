---
title: "Installing Manim"
date: 2019-08-24T16:21:26-05:00
categories: 
 - "tutorial"
draft: false 
tags:
  - "manim"
  - "visualization"
comments: true
lastmod: false
---
I was hoping to generate some explanatory math videos in the style of [3blue1brown](https://www.3blue1brown.com/) and fortunately the creator Grant Sanderson made his **m**athematical **anima**tion library (Manim) available at [3bib/manim](https://github.com/3b1b/manim). The repo has instructions for installation on Linux, but as I use Arch it was not as intuitive as I would have liked. As such I am throwing my installation process up here for anyone to duplicate that is running into trouble.

Manim Installation
--------
These installation instructions assume you have Python3 installed and are using Anaconda/Miniconda conda environments
```shell
git clone git@github.com:3b1b/manim.git
cd manim
conda env create --file=environment.yml
sudo pacman -S python-cairo
pip install manimlib
# It is necessary to install ffmpeg with x264 support 
conda install x264=='1!152.20180717' ffmpeg=4.0.2 -c conda-forge
# Run an example manim which should write output SquareToCircle.mp4 to .media
python -m manim example_scenes.py SquareToCircle -pl 
```
