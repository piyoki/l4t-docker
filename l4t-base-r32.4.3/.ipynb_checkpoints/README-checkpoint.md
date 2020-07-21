# l4t-base

[![License: MIT](https://img.shields.io/badge/License-MIT-red.svg)](https://opensource.org/licenses/MIT)
![](https://img.shields.io/static/v1?label=Device&message=Jetson(ARMv8)&color=orange)
![](https://img.shields.io/static/v1?label=Docker&message=19.03.9&color=blue)

*** Copy Right 2020 Kevin Yu. All rights reserved.

*** Author: Kevin Yu

*** Update Time: 2020/07/21

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

Usage
-----

Parameters
----------

Version Tags
------------

|            NAME           | VERSION |
|:-------------------------:|:-------:|
| hikariai/l4t-base-r32.4.3 |  latest |

License
-------

[MIT License](https://github.com/yqlbu/l4t-docker/blob/master/LICENSE)

<a name="license"></a>