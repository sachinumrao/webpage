---
draft: false
title: Setting Up Ubuntu/Debian System for Deep Learning
description: A short guide on setting up ubuntu/debian system for machine learning
date:
    created: 2019-08-15
    updated: 2019-08-15
tags:
    - Ubuntu
    - Cuda
---

# Setting Up Ubuntu/Debian System for Deep Learning

![ubuntu](./../../assets/ubuntu-logo.png)
*Image Credit: https://mytechshout.com*

As I started my journey to learn coding, I was introduced to Linux by my mentors. 
Primarily Linux was used by programmers but now a days it has garnered 
popularity in all domains. There are many Linux based operating  systems 
available out there but Ubuntu has become most used UNIX based OS. 
It is widely used in industries and universities. In this blog we will 
discuss what applications and tools are required/suggested to setup in a 
fresh ubuntu installation for working on machine learning and deep 
learning projects.

### Update the System
    $ sudo apt update
    $ sudo apt upgrade

### Basic Utilities

    $ sudo apt install vim gedit-common
    $ sudo apt install ubuntu-restricted-extras
    $ sudo apt install vlc
    $ sudo apt install classicmenu-indicator
    $ sudo apt install redshift redshift-gtk
    $ sudo apt install terminator
    $ sudo apt install unity-tweak-tool

### Install Google Chrome from .deb package

### Notes and Others
    $ sudo apt install nixnote2 #(To connect with evernote)
    
### Install Simple Note from .deb package (Take notes in cross platform app)

### Download Medium Desk and extract it to /opt folder (Read blogs on medium)

### Development Tools

    $ sudo apt install gcc g++
    $ sudo apt install cmake build-essential
    $ sudo apt install python-pip python-dev (for python3 use: python3-pip , python3-dev
    $ sudo apt install openjdk-8-jre
    $ sudo apt install git
    
### Text Editors
Install Sublime Text3 from [official site](https://www.sublimetext.com/3)

Download **Menlo font** (Its my favorite font but it is not available in Ubuntu, so you have to install opensource version)

### Install VS Code [site](https://code.visualstudio.com/)

### Python for Data Science

#### 1. Make Virtual Environment

    $ sudo apt install python-virtualenv
    $ mkdir ~/env_name && cd ~/env_name
    $ virtualenv env_name
    
#### 2. Activate virtual environment

    $ source ~/env_name/bin/activate
    
#### 3. Deactivate virtual environment

    $ deactivate
    
    
### Install Python Libraries

    $ pip install numpy matplotlib pandas
    $ pip install scipy scikit-learn scikit-image pillow
    $ pip install jupyter jupyterlab
    $ pip install nltk
    $ pip install spacy
    $ pip install tensorflow keras
    $ pip install xgboost
    
### Install CUDA
#### 1. Install Nvidia Graphics Driver from Software & Updates

Download cuda_x.deb packages <br>
Download cudnn_y.deb packages <br>

    $ sudo dpkg -i cuda_x.deb
    $ sudo apt update
    $ sudo apt install cuda
    $ sudo apt upgrade
    
#### 2. Add Cuda in Path

Add following path to ~/.bashrc file

    export CUDA_HOME=/usr/local/cuda-x.y
    export LD_LIBRARY_PATH=${CUDA_HOME}/lib64
    PATH=${CUDA_HOME}/bin:${PATH}
    export PATH
(where x and y are release numbers e.g. 7.5 or 8.0)

Now we need to install Nvidia’s library for deep learning CuDNN for which 
you need to make developer’s account in Nvidia. Download the required 
cuddnn*.deb file.

    $ sudo dpkg -i cudnn*.deb
    
### Install Deep Learning Frameworks
    $ sudo apt install cuda-command-line-tools

#### Add following lines to the ~/.bashrc file

    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64

##### Install Tensorflow-GPU
    $ sudo pip install tensorflow-gpu keras
    
##### Install Pytorch from [official site](https://pytorch.org/)