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

### 2. Building OpenCV and OpenCV Contrib:
- Installing OpenCV on Jetson is different than installing it on a normal UBUNTU system. Jetson has arm architecture, and the wheels for packages such as OpenCV has to be built rather than pip installation. 
- Before buidling OpenCV with CUDA, make sure that CUDA is installed properly using the following command in terminal. 
  nvcc --version
