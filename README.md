# Object-Tracking-In-Aerial-Imagery-Using-OpenCV-Trackers-On-NVIDIA-JETSON-TX2
This repository provides the implementation of Object Tracking in Aerial Imagery using OpenCV Trackers on Jetson TX2. The implementation on PC's or server is easy and usually not much problems occur while installing the pre-requisite for OpenCV Trackers but creating environment and installing dependencis for embedded systems is quite complicated. 

This repository will cover in detail the problems that occured during the installation as well as detail evaluation of OpenCV Trackers.  

### INSTALLATION PROCEDURE

### 1. NVIDIA JETSON JETPACK:

##### Step 01 Development Environment
- Download NVIDIA JETSON SDK MANAGER : https://developer.nvidia.com/nvidia-sdk-manager
- Select Product Category: Jetson
- Set Hardware Configuration as Host Machine and Target Hardware as Jetson TX2 module
- Select Target Operating System: JetPack 4.6

##### Step 02 Details and License
- Check HOST Components with status
- Check Target Components with status
- Select Download folder for image download
- Accept terms and condition and continue to next step

##### Step 03 Setup Process
- Flash the Jetson TX2

### 2. Building OpenCV, OpenCV Contrib and Installing necessary pre-requisite libraries:
Installing OpenCV on Jetson is different than installing it on a normal UBUNTU system. Jetson has arm architecture, and the wheels for packages such as OpenCV has to be built rather than pip installation. Before buidling OpenCV with CUDA, make sure that CUDA is installed properly.
- Open terminal and write the following command to check CUDA installation with its version. 
```
nvcc --version
```
- Remove all old opencv stuffs installed by JetPack (or OpenCV4Tegra)
```
$ sudo apt-get purge libopencv*
```
- It's prefered using newer version of numpy (installed with pip), so remove this python-numpy apt package as well
```
$ sudo apt-get purge python-numpy
```
- Upgrade all installed apt packages to the latest versions (optional)
```
$ sudo apt-get update
$ sudo apt-get dist-upgrade
```
- Update gcc apt package to the latest version (highly recommended)
```
$ sudo apt-get install --only-upgrade g++-5 cpp-5 gcc-5
```
- Install dependencies based on the Jetson Installing OpenCV Guide
```
$ sudo apt-get install build-essential make cmake cmake-curses-gui \
                       g++ libavformat-dev libavutil-dev \
                       libswscale-dev libv4l-dev libeigen3-dev \
                       libglew-dev libgtk2.0-dev
```
- Install dependencies for gstreamer stuffs
```
$ sudo apt-get install libdc1394-22-dev libxine2-dev \
                       libgstreamer1.0-dev \
                       libgstreamer-plugins-base1.0-dev
```
- Install Qt5 dependencies
```
$ sudo apt-get install qt5-default
```
- Install dependencies for python3
```
$ sudo apt-get install python3-dev python3-pip python3-tk
$ sudo pip3 install numpy
$ sudo pip3 install matplotlib
```
- Modify matplotlibrc (line #41) as 'backend      : TkAgg'
```
$ sudo vim /usr/local/lib/python3.6/dist-packages/matplotlib/mpl-data/matplotlibrc
```
- Also install dependencies for python2
```
$ sudo apt-get install python-dev python-pip python-tk
$ sudo pip2 install numpy
$ sudo pip2 install matplotlib
```
- Modify matplotlibrc (line #41) as 'backend      : TkAgg'
```
$ sudo vim /usr/local/lib/python2.7/dist-packages/matplotlib/mpl-data/matplotlibrc
```
-
