# l4t-base

[![License: MIT](https://img.shields.io/badge/License-MIT-red.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/static/v1?label=Device&message=Jetson(ARMv8)&color=orange)
![](https://img.shields.io/static/v1?label=Docker&message=19.03.9&color=blue)

*** Copy Right 2020 Kevin Yu. All rights reserved.

*** Author: Kevin Yu

*** Release date: 2020/07/21

*** Update Time: 2020/07/29

*** Website: www.hikariai.net

The l4t-base docker image is used for testing the CUDA environment with NVIDIA Docker Runtime. It contains the cuda samples for testing. This container is compatible with Jetson Nano, TX1/TX2, Xavier NX, and AGX Xavier with the latest JetPack 4.4(L4T R32.4.3) Release.

Package Versions
----------------

* TensorFlow 1.15
* PyTorch v1.5.0
* onnx 1.6.0
* numpy 1.18.2
* pandas 1.0.3
* scipy 1.4.1
* scikit-learn 0.22.2
* JupyterLab 2.0.1

Suported Architecture
---------------------

ARMv8 Nvidia Jetson Platform

Application Setup
-----------------

Build Image Manually

```bash
$ docker build -t [TAG] .
```

Use the Pre-Built Image from DockerHub

```bash
$ docker pull hikariai/l4t-base-r32.4.3
```

Usage
-----

Run the container without display (Applications that do not require an attached screen)

```bash
$ docker run -it --runtime nvidia hikariai/l4t-base-r32.4.3:latest bash 
$ cd samples/1_Utilities/deviceQuery
$ make
$ ./deviceQuery
```

Run the container with display (Require access to X server)

```bash
$ export DISPLAY=:0
$ sudo xhost +si:localuser:root
$ docker run -it --rm --net=host --runtime nvidia --device /dev/video0:/dev/video0 -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix hikariai/l4t-base-r32.4.3 bash
$ cd samples/5_Simulations/nbody
$ make
$ ./nbody
```

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

Version Tags
------------

|            NAME           | VERSION |
|:-------------------------:|:-------:|
| hikariai/l4t-base-r32.4.3 |  latest |

License
-------

[MIT License](https://github.com/yqlbu/l4t-docker/blob/master/LICENSE)

<a name="license"></a>