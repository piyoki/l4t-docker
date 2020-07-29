# l4t-cv2

[![License: MIT](https://img.shields.io/badge/License-MIT-red.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/static/v1?label=Device&message=Jetson(ARMv8)&color=orange)
![](https://img.shields.io/static/v1?label=Docker&message=19.03.9&color=blue)

*** Copy Right 2020 Kevin Yu. All rights reserved.

*** Author: Kevin Yu

*** Release date: 2020/07/21

*** Update Time: 2020/07/29

*** Website: www.hikariai.net

The l4t-cv2 docker image enables a CV2 CUDA-compiled environment for further AI  applications development. This container is compatible with Jetson Nano, TX1/TX2, Xavier NX, and AGX Xavier with the latest JetPack 4.4(L4T R32.4.3) Release.

Package Versions
----------------

* CUDA 10.2
* TensorRT 7.1.3
* OpenCV 4.1.1

Suported Architecture
---------------------

ARMv8 Nvidia Jetson Platform

Supported Device
---------------------

NVIDIA Jetson Nano

**Notes:** 

- This image also works with Jetson Xavier but it will be only using 4 CPU cores.

Application Setup
-----------------

Use the Pre-Built Image from DockerHub

```bash
$ docker pull l4t-cv2-r44.4.1
```

Usage
-----

Run the container without display (Applications that do not require an attached screen)

```bash
$ docker run -it --runtime nvidia l4t-cv2-r44.4.1:nano bash 
```

Verify the OpenCV version

```bash
$ python3 -c "import cv2 ; print(cv2.__version__)"
```

Run the container with display (Require access to X server)

```bash
$ export DISPLAY=:0
$ sudo xhost +si:localuser:root
$ docker run -it --rm --net=host --runtime nvidia --device /dev/video0:/dev/video0 -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix hikariai/l4t-cv2-r44.4.1:nano bash
$ python3 base.py
```

**Notes:**

- The container will open /dev/video0 USB WebCam by default, and stream the content in 640*480 resolution.

Parameters
----------

|    FLAG   |                                              USAGE                                              |
|:---------:|:-----------------------------------------------------------------------------------------------:|
|     -d    |                       run the container in detached mode (background mode)                      |
|    -it    |                              run the container in interactive mode                              |
|    --rm   |                        delete the container when it finishes its process                        |
| --runtime |                use a specify runtime (NVIDIA runtime) while running the container               |
|     -v    | add a mounting directory from the host to access and save files inside or outside the container |
|   --name  |                                specify the name of the container                                |
|  --device |                                map a host device to the container                               |
|     -p    |                               map the container port to host port                               |

Version Tags
------------

|       NAME      |     VERSION    |
|:---------------:|:--------------:|
| l4t-cv2-r44.4.1 | latest (4.1.1) |

License
-------

[MIT License](https://github.com/yqlbu/l4t-docker/blob/master/LICENSE)

<a name="license"></a>