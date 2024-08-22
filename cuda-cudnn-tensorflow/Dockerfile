# Use the base image from NVIDIA with CUDA, cuDNN, and Ubuntu 22.04
ARG IMAGE_NAME=nvidia/cuda
FROM ${IMAGE_NAME}:11.8.0-devel-ubuntu22.04 AS base

# Set environment variables for cuDNN
ENV NV_CUDNN_VERSION 8.9.6.50
ENV NV_CUDNN_PACKAGE_NAME "libcudnn8"
ENV NV_CUDNN_PACKAGE "libcudnn8=$NV_CUDNN_VERSION-1+cuda11.8"
ENV NV_CUDNN_PACKAGE_DEV "libcudnn8-dev=$NV_CUDNN_VERSION-1+cuda11.8"

# Install cuDNN, Python 3, pip, and other dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    ${NV_CUDNN_PACKAGE} \
    ${NV_CUDNN_PACKAGE_DEV} \
    python3 python3-pip \
    && apt-mark hold ${NV_CUDNN_PACKAGE_NAME} \
    && rm -rf /var/lib/apt/lists/*

# Install Python packages
RUN pip3 install \
    tensorflow==2.13.0 \
    matplotlib \
    scipy \
    scikit-learn \
    pandas \
    cupy-cuda11x
