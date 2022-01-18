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
- In this repository I will be using OpenCV 3.4.2, so downloading and using 3.4.2 in my steps
```
cd ~/Downloads  
wget https://github.com/opencv/opencv/archive/3.4.2.zip
unzip 3.4.2.zip 
mv opencv-3.4.2 ~/
cd ~/opencv-3.4.2
mkdir build
cd ~/Downloads
rm 3.4.2.zip
wget https://github.com/opencv/opencv_contrib/archive/3.4.2.zip
unzip 3.4.2.zip
mv opencv_contrib-3.4.2 ~/
cd ~/opencv-3.4.2/build
```
- Run the following cmake commands in the build directory:
```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D WITH_CUDA=ON -D CUDA_ARCH_BIN="6.2" -D CUDA_ARCH_PTX="" \
      -D WITH_CUBLAS=ON -D ENABLE_FAST_MATH=ON -D CUDA_FAST_MATH=ON \
      -D ENABLE_NEON=ON -D WITH_LIBV4L=ON -D BUILD_TESTS=OFF \
      -D BUILD_PERF_TESTS=OFF -D BUILD_EXAMPLES=OFF \
      -D WITH_QT=ON -D WITH_OPENGL=ON \       
      -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.2/modules ..
```
```
make -j4
sudo make install
```

#### ISSUES  
##### While building OpenCV issues occur, some due to pre-requisite libraries versions and other randomly. Below mentioned are some of the issues that I had while buidling OpenCV 3.4.2.

```
1. While installing "libjasper-dev, libpng12-dev" they are often missing from the apt get repositries. 
Since these packages are not compulsory, you can skip installing them.
```

```
2. *** No rule to make target '/usr/lib/aarch64-linux-gnu/libGL.so', needed by...
This issue arsises when you run the make command to build openCV. The problem is, the
file required lies in the path "/usr/lib/aarch64-linux-gnu/", however to make it 
available to the build process, a symbolic link needs to be created for that.

Steps to resolve this issue:
cd /usr/lib/aarch64-linux-gnu/
sudo rm libGL.so
sudo ln -sf libGL.so.1.0 libGL.so

In case the issue persists, try repeating the above steps but changing the libGL.so.1.0
to libGL.so.1 or libGL.so.1.0.0
```

```
3. While installing matplotlib using pip3, there are often issues encountered.
Googling the issues suggest to upgrade the setuptools, however the issues persists.
In order to resolve this issue, try installing matplotlib using apt-get method as:

$ sudo apt-get install matplotlib
```

```
4. "error Please include the appropriate gl headers before including cuda_gl_interop.h"

sudo vim /usr/local/cuda/include/cuda_gl_interop.h
cd /usr/lib/aarch64-linux-gnu/
sudo ln -sf tegra/libGL.so libGL.so

```

