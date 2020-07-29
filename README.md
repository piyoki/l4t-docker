# Jetson-L4T-Docker

[![License: MIT](https://img.shields.io/badge/License-MIT-red.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/static/v1?label=Device&message=Jetson(ARMv8)&color=orange)
![](https://img.shields.io/static/v1?label=Docker&message=19.03.9&color=blue)

*** Copy Right 2020 Kevin Yu. All rights reserved.

*** Author: Kevin Yu

*** Release date: 2020/07/21

*** Update date: 2020/07/21

*** Website: www.hikariai.net

This repo is a docker image hub that contains multifunctional containers tailored to the NVIDIA Jetson Platform (ARMv8) running Ubuntu 18.04 L4T. As for now, all the containers listed in this repo are only available for JetPack 4.4+, and built based on the official L4T docker image provided by [NVIDIA GPU Cloud (NGC)](https://ngc.nvidia.com/).

With [NVIDIA Docker Runtime](https://developer.nvidia.com/nvidia-container-runtime), applications relied on CUDA are able to run with Docker Engine.

The NVIDIA runtime enables graphics and video processing applications such as DeepStream to be run in containers on the Jetson platform. The purpose of this document is to provide users with steps on getting started with running Docker containers on Jetson using the NVIDIA runtime. The beta supports Jetson AGX Xavier, Jetson TX2 series, Jetson TX1, and Jetson Nano devices. For more information, you may visit the site [HERE](https://github.com/NVIDIA/nvidia-docker/wiki/NVIDIA-Container-Runtime-on-Jetson).

Table of Contents
-----------------

* [Installation](#installation)
* [Running Guide](#running-guide)
* [Available Images](#available-images)
* [License](#license)

Installation
------------

##### Install Docker Engine with Script

```bash
$ sudo wget -qO- https://get.docker.com/ | sh
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ newgrp docker 
$ sudo systemctl enable docker
$ sudo systemctl status docker
```

##### Install NVIDIA-Docker Runtime

```bash
$ sudo apt install -y nvidia-docker2
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
$ docker info | grep nvidia
```

##### Verify Nvidia-Runtime

```bash
$ docker run -it --runtime nvidia hikariai/l4t-base-r32.4.3:latest bash 
$ cd samples/1_Utilities/deviceQuery
$ make
$ ./deviceQuery
```

**Notes**: 

If everything configured correctly, you will see the similar output log as shown below in the console.

```bash
Device 0: "NVIDIA Tegra X1"
  CUDA Driver Version / Runtime Version          10.2 / 10.2
  CUDA Capability Major/Minor version number:    5.3
  Total amount of global memory:                 3964 MBytes (4156780544 bytes)
  ( 1) Multiprocessors, (128) CUDA Cores/MP:     128 CUDA Cores
  GPU Max Clock rate:                            922 MHz (0.92 GHz)
  Memory Clock rate:                             13 Mhz
  Memory Bus Width:                              64-bit
  L2 Cache Size:                                 262144 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 32768
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 1 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            Yes
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device supports Compute Preemption:            No
  Supports Cooperative Kernel Launch:            No
  Supports MultiDevice Co-op Kernel Launch:      No
  Device PCI Domain ID / Bus ID / location ID:   0 / 0 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 10.2, CUDA Runtime Version = 10.2, NumDevs = 1
Result = PASS
```

To exit the container:

```bash
$ exit
```

<a name="installation"></a>

##### Change Docker Image Path (Optional)

```bash
$ sudo systemctl stop docker
$ sudo cp -a /var/lib/docker/ /home/kev/Docker
$ sudo mv /var/lib/docker /var/lib/docker.bak
$ sudo nano /etc/docker/daemon.json
```

```json
{
    "graph":"/home/<username>/Docker"
}
```

```bash
$ sudo systemctl start docker
$ sudo systemctl status docker
$ docker info | grep Root
```

Running Guide
-------------

Run the container without display (Applications that do not require an attached screen)
```bash
$ docker run -it --net=host --runtime nvidia --name l4t hikariai/l4t-base-r32.4.3 bash
```

Allow external applications to connect to the host’s X display (Require access to X server)
```bash
$ export DISPLAY=:0
$ sudo xhost +si:localuser:root
$ docker run -it --rm --net=host --runtime nvidia -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix hikariai/l4t-base:r32.4.3 bash
```

Run the container with addtional devices (cameras):
```bash
$ export DISPLAY=:0
$ sudo xhost +si:localuser:root
$ docker run -it --rm --net=host --runtime nvidia --device /dev/video0:/dev/video0 -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix hikariai/l4t-base-r32.4.3 bash
$ cd samples/5_Simulations/nbody
$ make
$ ./n
```

Run containers in background
```bash
$ docker run -dit --net=host --runtime nvidia --name l4t hikariai/l4t-base-r32.4.3 bash
# access the container
$ docker exec -it l4t bash
```

<a name="running-guide"></a>

##### Flags Options Explained:

- -d refers to running the container in detached mode (background mode) 
- -it refers to running in interactive mode
- --rm refers to deleting the container when finished
- --runtime nvidia refers to using the NVIDIA container runtime while running the l4t-base container
- -v refers to the mounting directory, and used to mount host’s X11 display in the container filesystem to render output videos
- --name refers to the specification of the container name
- --device refers to mapping an attached device such as camera to the container with full access

Available Images
----------------

[**L4t-base**](https://github.com/yqlbu/l4t-docker/tree/master/l4t-base-r32.4.3) -- Runnning CUDA Samples on Jetson Devices

[**L4t-cv2**]() -- L4t image with OpenCV support

[**L4t-trt**]() -- Transfer Learning Toolkit deployed on Jetson Platform for Object Detection


License
-------

[MIT License](https://github.com/yqlbu/l4t-docker/blob/master/LICENSE)

<a name="license"></a>