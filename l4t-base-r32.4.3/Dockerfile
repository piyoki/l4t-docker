FROM nvcr.io/nvidia/l4t-base:r32.4.3

ENV CUDA_HOME="/usr/local/cuda"
ENV PATH="/usr/local/cuda/bin:${PATH}"
ENV LD_LIBRARY_PATH="/usr/local/cuda/lib64:${LD_LIBRARY_PATH}"
    
RUN apt-get update && apt-get install -y --no-install-recommends \
    sudo make g++ git cmake wget nano curl zip unzip\
    python3-pip \
    python3-dev \
    python3-setuptools
    
RUN pip3 install --upgrade pip setuptools --user 

WORKDIR /root/

COPY . .

RUN mv ./tensorrt-7.1.3.0.dist-info /root/.local/lib/python3.6/site-packages/tensorrt-7.1.3.0.dist-info