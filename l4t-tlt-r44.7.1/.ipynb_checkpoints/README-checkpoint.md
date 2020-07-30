# l4t-tlt

[![License: MIT](https://img.shields.io/badge/License-MIT-red.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/static/v1?label=Device&message=Jetson(ARMv8)&color=orange)
![](https://img.shields.io/static/v1?label=Docker&message=19.03.9&color=blue)

*** Copy Right 2020 Kevin Yu. All rights reserved.

*** Author: Kevin Yu

*** Release date: 2020/07/29

*** Update Time: 2020/07/29

*** Website: www.hikariai.net

The l4t-tlt docker image integrates the [Transfer Learning ToolKit](https://developer.nvidia.com/transfer-learning-toolkit) developed by NVIDIA with CUDA support. It may help you quickly run inference based on the custom-trained SSD model on the Jetson Devices. This container is compatible with Jetson Nano, TX1/TX2, Xavier NX, and AGX Xavier with the latest JetPack 4.4(L4T R32.4.3) Release.

Package Versions
----------------

* CUDA 10.2
* TensorRT 7.1.3
* OpenCV 4.1.1
* TensorRT-OSS 7.1.3
* Tensorflow 1.15
* Pycuda 2019.1.2
* jupyterlab 2.2
* ipykernel 5.3.3

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
$ docker pull hikariai/l4t-tlt-r44.7.1:nano
```

Use the Pre-Built Image from AliCloud (Users from China ONLY)

```bash
$ docker run --name tlt -it --runtime nvidia -p 3001:8888 registry.cn-hangzhou.aliyuncs.com/hikariai/l4t-tlt-r44.7.1 bash
```

Usage
-----

Run the container

```bash
$ sudo docker run --name tlt -it --runtime nvidia -p 3001:8888 hikariai/l4t-tlt-r44.7.1:nano bash
$ jupyter lab --ip 0.0.0.0 --port 8888 --allow-root
```

**Notes:**

- Open up a new browser and visit **http://localhost:3001**, and you should be able to log into JupyterLab with the token displayed in your console.
- The detailed usage instruction of the tool, including all the setup steps, is available in the notebook



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
|     -p    |                             map the container port to the host port                             |

Version Tags
------------

|           NAME           |    VERSION   |
|:------------------------:|:------------:|
| hikariai/l4t-tlt-r44.7.1 | latest (7.1) |

License
-------

[MIT License](https://github.com/yqlbu/l4t-docker/blob/master/LICENSE)

<a name="license"></a>