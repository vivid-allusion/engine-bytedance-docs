---
title: "Preset mirror list"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Preset_mirror_list"
---

In machine learning development, mirrors are used to provide the running environment required for development. Machine Learning Platform provides users with pre\-configured mirrors including Python, CUDA, PyTorch, TensorFlow, BytePS, and other dependencies for direct use by users.

<span id="预置镜像列表"></span>
# Preset mirror list

<span id="python"></span>
## Python

Python is one of the most commonly used programming languages in machine learning research and development, and it is highly readable and has a wealth of software libraries (e.g. scikit\-learn, numpy, etc.). The platform installs different versions of Miniconda Python (3.7 +) based on the original Ubuntu mirror, with a built\-in power builder, while pip, conda, and apt use domestic mirror sources.

This mirror is small in size and suitable for use as a basic mirror or in lightweight tasks.

<span id="cuda"></span>
## CUDA

The CUDA mirrors provided by the platform are based on the `nvidia/cuda`series of mirrors, and the CUDA versions provided include 11.7.0, 11.6.0, 11.3.0, 11.1.1. It includes a GPU\-accelerated toolkit, compiler, power builder, and CUDA runtime environment, suitable for general\-purpose high\-performance computing scenarios.

Key features of mirroring:


* The high\-performance network infrastructure that supports the platform provides nccl\-tests for testing.

* Supports different versions of Python, ranging from 3.7 to 3.10.

* Built\-in power builders such as git, rclone, vim.

* Pip, conda, and apt use domestic mirror sources.

* Built\-in CUDNN 8.


Due to lifecycle and compatibility issues, Ubuntu 18 does not support V100 RDMA models, CUDA 10 does not support Ampere series GPUs, and the platform does not provide or recommend the use of related software.

<span id="pytorch"></span>
## PyTorch

The Pytorch mirror is based on the CUDA mirror of the platform. The `pytorch`, `torchvision`and `torchaudio`software packages are added, and the built\-in Pytorch DDP multi\-machine test samples are included. For details, please refer to the Machine Learning Platform [Mirror Center] PyTorch details page. The instructions for CUDA mirrors also apply in Pytorch mirrors.

The platform currently only provides [a combination of CUDA versions officially supported by Pytorch ](https://pytorch.org/get-started/previous-versions/).

<span id="tensorflow"></span>
## TensorFlow

TensorFlow is an end\-to\-end open source platform for machine learning. It has a comprehensive and flexible ecosystem of tools, libraries, and community resources. A series of TensorFlow mirrors are pre\-installed on the platform, and GPU\-related software packages such as CUDA and cuDNN are installed in the mirrors. Users can use the mirror to easily build and deploy machine learning applications.

The versions of TensorFlow, CUDA, and cuDNN in different mirror versions are different.


|version |CUDA version |cuDNN version |
|---|---|---|
|tensorflow:2.4 |11.0 |8.0 |
|tensorflow:1.15 |10.0 |7.4 |


<span id="tfserving"></span>
## TFServing

TensorFlow Serving is a flexible and high\-performance machine learning inference engine, which is mainly used for the rapid deployment of TensorFlow models and the lifecycle management of services. The platform comes with multiple mirrors of TensorFlow Serving to enable deployment of different versions of the TensorFlow model.

Different versions of the mirror contain different versions of CUDA, and the supported versions of TensorFlow are also different. Users need to choose the mirror version on demand.


|version |CUDA version |Supported TensorFlow versions |
|---|---|---|
|tfserving:tf\-cuda11.0 |11.0 |2.4+ |
|tfserving:tf\-cuda10.1 |10.1 |1.14、1.15、2.0、2.2、2.3 |


<span id="triton-inference-server"></span>
## Triton Inference Server

Triton Inference Server is a highly optimized inference solution for CPU and GPU. It not only supports deep learning models in various formats such as SavedModel, Torchsript, ONNX, and TensorRT, but also supports XGBoost and LightGBM\-trained tree models in higher versions. The platform comes with a series of Triton mirrors for users to choose from, enabling high\-performance model inference.

Different versions of the mirror contain different versions of Triton Inference Server, and the versions corresponding to the supported model framework are also different. Users need to choose the mirror version on demand.


|version |Supported framework versions |
|---|---|
|tritonserver:22.08 |TensorFlow 1.15/2.9, PyTorch 1.13, TensorRT 8.4.2, ONNX Runtime 1.12, 0021 (XGBoost, LightGBM, sklearn trained models) |
|tritonserver:21.12 |TensorFlow 1.15/2.6, PyTorch 1.11, TensorRT 8.2.1, ONNX Runtime 1.9, 0021 (XGBoost, LightGBM, sklearn trained models) |
|tritonserver:21.04 |TensorFlow1.15 / 2.4、PyTorch1.9、TensorRT7.2.3、ONNX Runtime1.7 |
|tritonserver:21.02 |TensorFlow1.15 / 2.4、PyTorch1.8、TensorRT7.2.2、ONNX Runtime1.6 |
|tritonserver:20.09 |TensorFlow1.15 / 2.3、PyTorch1.7、TensorRT7.1.3、ONNX Runtime1.4 |


<span id="gbdt-serving"></span>
## GBDT\-Serving

Groot is BytePlus' self\-developed inference engine for GBDT models, which provides a universal and high\-performance GBDT service deployment solution. The platform encapsulates it into a preset mirror. Using the preset mirror that includes the engine can easily deploy tree models trained by frameworks such as XGBoost and LightGBM.
