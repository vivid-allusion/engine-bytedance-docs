---
title: "GPU - Deploying PyTorch applications"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_-_Deploying_PyTorch_applications"
---

This topic describes how to deploy PyTorch applications on a Linux instance.

<span id=".UHl0b3JjaOeugOS7iw=="></span>
## PyTorch overview

PyTorch is an open\-source Python machine learning library used for applications such as natural language processing (NLP). It not only enables powerful GPU acceleration but also supports dynamic neural networks.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, Ubuntu 18.04 is used.

* NVIDIA driver:

   * GPU driver: A program used to drive NVIDIA GPU cards. In the example provided in this topic, GPU driver 470.57.02 is used.

   * CUDA toolkit: A computing platform that enables GPUs to solve complex computational problems. In the example provided in this topic, CUDA 11.4 is used.

   * cuDNN Library: A deep neural network library designed for high\-performance GPU acceleration. In the example provided in this topic, cuDNN Library 8.2.4.15 is used.

* Anaconda: A package acquisition and management tool. It comes pre\-installed with over 180 scientific computing packages and their dependencies, including Conda and Python, and enables the creation of isolated Python virtual environments. In the example provided in this topic, Anaconda 3 and Python 3.8.3 are used.


> When PyTorch uses CUDA for GPU acceleration, if it still fails to work when ​CUDA and the GPU driver are installed, the issue is most likely a version mismatch. Strictly ensure the version compatibility of the aforementioned software.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have purchased a GPU Accelerated Linux instance and selected "Automatically install GPU driver in the background". This way, the instance automatically installs the NVIDIA driver of the specified version when it starts. For more information, see [Creating GPU Accelerated instances](https://docs.byteplus.com/en/docs/gpu/Buying-GPU-Accelerated-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5q2l6aqk5LiA77ya5p-l55yL6amx5Yqo54mI5pys5bey5a6J6KOF5oiQ5Yqf"></span>
## Step 1: Verify that the driver version is installed successfully


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the GPU driver.

   `nvidia-smi`

   If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9cf12d051419d3e7fe35fb035c934f4f.png) </span>

3. Execute the following command to view the CUDA driver.

   `/usr/local/cuda/bin/nvcc -V`

   If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2ca4a02a0bc450bca0f81aea02371662.png) </span>


<span id=".5q2l6aqk5LqM77ya5Yib5bu66Jma5ouf546v5aKD"></span>
## Step 2: Create a virtual environment


1. Execute the following command to download the Anaconda installation package.

   `wget https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh`

2. Execute the following command to install Anaconda.

   `bash Anaconda3-2022.05-Linux-x86_64.sh`

   1. Keep pressing the "Enter" key to continue the installation.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9b1511b6ccc837c96f0835a0cd0d916c.png) </span>

   2. Enter "yes" to confirm the information.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_790ab5464c6fc47ce2d8b98ca2870415.png) </span>

   3. Press the "Enter" key once. After a short wait, the installation will complete. Record the Anaconda installation path `/root/anaconda3`.

      <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_09ccff292fb63a6d645b4ca0b44b4ef2.png) </span>

   4. Enter "yes" to confirm initialization of Anaconda.

      <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_20ad9424b84e37ff2294fe6227ec20a9.png) </span>

3. Execute the `source ~/.bashrc` command to apply the configuration file.

   If the following output is displayed, the configuration is successful and you have entered the base environment.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ab46d5d0808d1eb9916638936422b434.png) </span>

4. Create a virtual environment and specify the Python version.

   1. Execute the `conda create -n cuda11.4 python=3.8.3` command. In the command, `cuda11.4` is the name of the virtual environment, which you can change based on your needs.

   2. When `Proceed ([y]/n)?` is displayed, enter "y" to confirm the creation.

   3. Execute the following command to activate the virtual environment.

      `conda activate cuda11.4`

      If the following output is displayed, the activation is successful.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_070a4a3724059360bd1d7a29fb7059b2.png) </span>


<span id=".5q2l6aqk5LiJ77ya5a6J6KOFUHl0b3JjaA=="></span>
## Step 3: Install PyTorch


1. Visit the [PyTorch official website](https://pytorch.org/get-started/previous-versions/), find the installation command that matches your CUDA version in Conda. For CUDA 11.4, select the installation package corresponding to CUDA 11.3.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_42cea3c4b131b27dff0773c97be7665d.png) </span>

2. Log in to the instance and continue to execute the installation command in the "cuda11.4" virtual environment. Enter "y" to confirm the installation.

   `conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch`

3. Execute the `pip list` command. If the following output is displayed, PyTorch is installed successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff9d9d6e4f4ca188cbc57c00fffd642a.png) </span>


<span id=".5q2l6aqk5Zub77ya6aqM6K-B546v5aKD"></span>
## Step 4: Verify the environment


1. Execute the following commands in sequence to test whether CUDA is available.

   ```Plain Text
   python
   >>>import torch
   >>>torch.cuda.is_available()
   ```
   

   If the following output is displayed, PyTorch is deployed successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cde566dbe153dea147865dc1b4ea747b.png) </span>

2. Enter `conda deactivate` to exit the virtual environment.
