# ------------------------------------------------------------------------------
# Simple PyTorch Docker image for use as research base image.
#
# Author: Ryan Eloff
# Contact: ryan.peter.eloff@gmail.com
# Date: November 2018
# ------------------------------------------------------------------------------
# Based on the deep learning Docker images from https://github.com/ufoym/deepo.
# Usage with nvidia-docker:
#   $ nvidia-docker run -it --name my_container <image-build-tag> bash
# ------------------------------------------------------------------------------
# NOTE: Specify the PyTorch release version with TORCH_VERSION:
#   $ docker build --build-arg TORCH_VERSION=0.4.1 -t reloff/kaldi:latest .
# ------------------------------------------------------------------------------
FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
LABEL author="Ryan Eloff" date="19-11-2018"
# ------------------------------------------------------------------------------
# Install Python 3.6 from the deadsnakes PPA and link as default python
# ------------------------------------------------------------------------------
RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils \
    curl \
    software-properties-common \
&& add-apt-repository ppa:deadsnakes/ppa \
&& apt-get update && apt-get install -y --no-install-recommends \
    python3.6 \
    python3.6-dev \
&& curl https://bootstrap.pypa.io/get-pip.py | python3.6 \
&& ln -s /usr/bin/python3.6 /usr/local/bin/python3 \
&& ln -s /usr/bin/python3.6 /usr/local/bin/python \
&& python -m pip --no-cache-dir install --upgrade \
    setuptools \
&& apt-get clean \
&& apt-get autoremove \
&& rm -rf /var/lib/apt/lists/* \
          /etc/apt/sources.list.d/*
# ------------------------------------------------------------------------------
# Define TensorFlow GPU release version to install (defaults to latest release)
# ------------------------------------------------------------------------------
ARG TORCH_VERSION
# ------------------------------------------------------------------------------
# Install PyTorch (==${TORCH_VERSION} if specified)
# ------------------------------------------------------------------------------
RUN python -m pip --no-cache-dir install --upgrade \
    torch${TORCH_VERSION:+\=\=${TORCH_VERSION}} \
    torchvision
# ------------------------------------------------------------------------------
# Set default command to '/bin/sh -c bash'
# ------------------------------------------------------------------------------
CMD ["bash"]
