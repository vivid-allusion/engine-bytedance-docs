---
title: "Using AI container images"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-AI-container-images"
---

AI container images are a series of Docker images provided by BytePlus, which are pre\-installed with common AI frameworks, tools, and related dependencies. They offer a quick\-start and highly consistent AI development environment. This topic describes how to use AI container images.

## Background information

In the preliminary stages of AI model training and inference, you typically work with specific combinations of AI frameworks and tools (for example, the PyTorch framework and DeepSpeed library). After performing algorithm tuning, model injection, or script development in a basic environment, you need to submit repackaged images to the job queue of the training or inference platform.

AI container images accelerate the setup of AI development, training, and inference environments. Together with other tools and product capabilities in the AI Suite, they provide services covering the entire lifecycle of AI applications.

## Prerequisites

A basic environment for AI training or inference has already been set up with VKE resources such as clusters, VPCs, and GPU nodes.

## Limit

* VKE AI container images can only be pulled within a VPC and cannot be pulled from the public network. You need to pull images from the VKE cluster or ECS instance in the corresponding region of BytePlus.

* The following document mainly introduces the practices officially tested and verified. In order to achieve the expected results and comply with the Vital Kubernetes Engine (VKE) [Limits](https://docs.byteplus.com/en/docs/vke/Limits), you must strictly follow the procedures (or the recommended resources) in this document. If you need to modify the procedures to suit your service requirements, contact the customer manager for consultation.

## Procedure

### Step 1: Obtain the address of the desired AI container image

BytePlus provides a series of pre\-built AI container images, enabling rapid deployment and consistent AI development environments. The following table contains the supported versions, support status, and image addresses of AI container images.

> **tip**

* > You need to replace **{regionID}** in an image address with the actual region ID. For regions where AI container images are available and their region IDs, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones).

* > Pay attention to the following information about pre\-built AI container images:

   * > The software and dependencies in pre\-built AI container images are limited to versions officially compiled and made generally available by NVIDIA.

   * > Pre\-built AI container images are updated quarterly, following the update cycle of official software versions from NVIDIA. The updated images will use the latest generally available software versions released by NVIDIA.

|Machine learning framework version |Other software and dependency version |Operating system version |Still supported |Image address |
|---|---|---|---|---|
|\- |* CUDA 11.8.0<br><br>* Python 3.10 |Ubuntu 22.04 |Yes |ai\-containers\-{regionID}.cr.volces.com/deeplearning/cuda11.8.0\-py3.10\-ubuntu22.04:latest |
|Pytorch 2.0.1 |* CUDA 11.8.0<br><br>* Python 3.10 |Ubuntu 22.04 |Yes |ai\-containers\-{regionID}.cr.volces.com/deeplearning/torch2.0.1\-cuda11.8.0\-py3.10\-ubuntu22.04:latest |
|Tensorflow 2.13.0 |* CUDA 11.8.0<br><br>* Python 3.10 |Ubuntu 22.04 |Yes |ai\-containers\-{regionID}.cr.volces.com/deeplearning/tensorflow2.13.0\-cuda11.8.0\-py3.10\-ubuntu22.04:latest |
|Pytorch 2.0.1 |* Megatron 23.05<br><br>* CUDA 11.8.0<br><br>* Python 3.10 |Ubuntu 22.04 |Yes |ai\-containers\-{regionID}.cr.volces.com/deeplearning/megatron23.05\-torch2.0.1\-cuda11.8.0\-py3.10\-ubuntu22.04:latest |
|Pytorch 2.0.1 |* Deepspeed 0.10.0<br><br>* CUDA 11.8.0<br><br>* Python 3.10 |Ubuntu 22.04 |Yes |ai\-containers\-{regionID}.cr.volces.com/deeplearning/deepspeed0.10.0\-torch2.0.1\-cuda11.8.0\-py3.10\-ubuntu22.04:latest |

### Step 2: Pull the AI container image to start a container

Obtain the AI container image, pull it into VKE, and use it to start a container. This AI container image is used to create a basic training environment.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster that is available for AI training or inference. The management page of the cluster opens.

3. In the left navigation bar, click **Workload** \> **Pod** to enter the pod management page.

4. Click ** Create with Yaml** to create a pod that uses a pulled pre\-built AI container image. The following sample code shows the YAML content.

```Yaml
apiVersion: v1
kind: Pod
metadata:
  name: ai-env      # Pod name.
  namespace: default# The namespace to which the pod belongs
spec:
  containers:
  - name: pytorch      # Container name.
    image: ai-containers-cn-beijing.cr.volces.com/deeplearning/torch2.0.1-cuda11.8.0-py3.10-ubuntu22.04:latest# Pre-built AI container image and its version. Use the image address obtained from Step 1 and use the 'latest' image tag.
    command: [ "/bin/bash", "-c", "--" ]
    args: [ "while true; do sleep 3600; done;" ]
    resources:
      limits:
        nvidia.com/gpu: "1"# The number of GPU graphics cards.
```

### Step 3: Prepare the training environment

After the pod enters the Running status, log in to the pod console via VKE to further prepare the environment as needed. For example, you can use development tools to develop algorithms and scripts, or import model files.

### Step 4: Package the image and push it to CR

1. Use the AI container image as the base image to build a custom AI development environment via a Dockerfile. The following Dockerfile provides an example:

```dockerfile
# The address and version of the pre-built container image. This setting must be consistent with the AI container image pulled in Step 2.
FROM ai-containers-cn-beijing.cr.volces.com/deeplearning/torch2.0.1-cuda11.8.0-py3.10-ubuntu22.04:latest
# Set the working directory for subsequent commands in the Dockerfile.
WORKDIR /home
# Import files (such as model files) from the local file system into the image.
COPY chatglm2-6b.tar /chatglm2-6b.tar
# Preinstall other required AI tools for the image, such as jupyterlab.
RUN pip install "jupyterlab"
# Add other required environment variables to the image environment.
ARG VARNAME="value"
ENV PATH=$VARNAME
```

2. Push the derived image to the BytePlus CR service. For details, see [Pulling images from and pushing images to a standard CR instance](https://docs.byteplus.com/en/docs/cr/push-and-pull-images-in-an-enterprise-instance).

## What to do next

At this point, the derived image packaged based on the AI container image has been pushed to BytePlus CR. You can deploy model training or inference jobs in the VKE cluster.
