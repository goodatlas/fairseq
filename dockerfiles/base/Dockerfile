FROM nvidia/cuda:10.1-devel-ubuntu18.04

MAINTAINER tom tom@atlaslabs.ai

ENV LANG=C.UTF-8

ENV TZ=Asia/Seoul
ENV DEBIAN_FRONTEND=noninteractive
RUN ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# TensorFlow version is tightly coupled to CUDA and cuDNN so it should be selected carefully
ENV PYTORCH_VERSION=1.5.0
ENV CUDNN_VERSION=7.6.5.32-1+cuda10.1
ENV NCCL_VERSION=2.7.8-1+cuda10.1

ENV PYSPARK_PACKAGE=pyspark==2.4.7
ENV SPARK_PACKAGE=spark-2.4.7/spark-2.4.7-bin-hadoop2.7.tgz

# Python 3.7 is supported by Ubuntu Bionic out of the box
ARG python=3.7
ENV PYTHON_VERSION=${python}

# Set default shell to /bin/bash
SHELL ["/bin/bash", "-cu"]

RUN apt-get update && apt-get install -y --allow-downgrades --allow-change-held-packages --no-install-recommends \
        build-essential \
        cmake \
        g++-7 \
        git \
        curl \
        vim \
        wget \
        ca-certificates \
        libcudnn7=${CUDNN_VERSION} \
        libnccl2=${NCCL_VERSION} \
        libnccl-dev=${NCCL_VERSION} \
        libjpeg-dev \
        libpng-dev \
        python${PYTHON_VERSION} \
        python${PYTHON_VERSION}-dev \
        python${PYTHON_VERSION}-distutils \
        librdmacm1 \
        libibverbs1 \
        ibverbs-providers

RUN ln -s /usr/bin/python${PYTHON_VERSION} /usr/bin/python

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    rm get-pip.py



RUN pip install torch==${PYTORCH_VERSION}+cu101 -f https://download.pytorch.org/whl/torch_stable.html

RUN pip install soundfile




