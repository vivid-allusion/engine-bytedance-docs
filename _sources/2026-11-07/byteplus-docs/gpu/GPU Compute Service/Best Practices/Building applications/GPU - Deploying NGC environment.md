---
title: "GPU - Deploying NGC environment"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_-_Deploying_an_NGC_environment"
---

This topic describes how to deploy TensorFlow based on NGC on a Linux instance.

<span id=".TkdD5LuL57uN"></span>
## NGC overview

NVIDIA GPU CLOUD (NGC) is a deep learning container library developed by NVIDIA. It boasts powerful performance and excellent flexibility, helping scientists and researchers quickly build, train, and deploy neural network models.

The [NGC official website](https://catalog.ngc.nvidia.com/) provides images of mainstream deep learning frameworks, such as Caffe, TensorFlow, Theano, and Torch.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, Ubuntu 18.04 is used.

* NVIDIA driver:

   * GPU driver: A program used to drive NVIDIA GPU cards. In the example provided in this topic, GPU driver 470.57.02 is used.

   * CUDA: A computing platform that enables GPUs to solve complex computational problems. In the example provided in this topic, CUDA 11.4 is used.

   * cuDNN: A deep neural network library designed for high\-performance GPU acceleration. In the example provided in this topic, cuDNN 8.2.4.15 is used.

* TensorFlow: A deep learning framework.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have purchased a Linux instance and selected "Automatically install GPU driver in the background". This way, the instance automatically installs the NVIDIA driver of the specified version when it starts. The total time from instance creation to the completion of driver installation is approximately 15 to 20 minutes. Wait patiently. For more information, see [Creating GPU Accelerated instances](https://docs.byteplus.com/en/docs/gpu/Buying-GPU-Accelerated-instances).

* An EIP is associated with the Linux instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

* To use HTTPS or the DIGITS 6 service, you need to add the following inbound rules to the security group of the instance:

   * Allow TCP port 443 (for HTTPS) or TCP port 5000 (for DIGITS 6).


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


<span id=".5q2l6aqk5LqM77ya5a6J6KOFbnZpZGlhLWRvY2tlcg=="></span>
## Step 2: Install nvidia\-docker


1. Execute the following commands in sequence to configure Docker\-CE.

   ```Plain Text
   curl https://get.docker.com | sh \
     && sudo systemctl --now enable docker
   ```
   

2. Execute the following commands in sequence to configure the package repository and GPG key:

   ```Plain Text
   distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
     && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
     && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
           sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
           sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
   ```
   

3. Execute the following command to install nvidia\-docker2.

   ```Plain Text
   sudo apt-get update
   sudo apt-get install -y nvidia-docker2
   ```
   

4. Execute the following command to configure the Docker daemon to recognize the NVIDIA container runtime.

   `sudo nvidia-ctk runtime configure --runtime=docker`

5. Execute the following command to restart the Docker daemon and complete the installation.

   `sudo systemctl restart docker`

6. Execute the following command to test whether nvidia\-docker2 is installed successfully by running a basic CUDA container.

   `sudo docker run --rm --runtime=nvidia --gpus all nvidia/cuda:11.6.2-base-ubuntu20.04 nvidia-smi`

   If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b9adefad94d123c46badb82cab75da8d.png) </span>


<span id=".5q2l6aqk5LiJ77ya6I635Y-WTkdD6ZWc5YOP"></span>
## Step 3: Obtain the NGC image


1. Log in to the [NGC website](https://catalog.ngc.nvidia.com/) and register an NGC account.

2. Obtain the NGC API key and save it.

   1. Click the account name and select "Setup" from the drop\-down list.

   2. Click the "Get API Key" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94dbae891104e9baaff67071b316151e.png) </span>

   3. Click "Generate API Key" in the upper right corner of the page, and then click the "Confirm" button. The API key will be displayed at the bottom of the page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dfa24f094284013cc6d9fdbcce3fa594.png) </span>

3. Log in to the instance and execute the following command. Enter the account name (fixed as `$oauthtoken`) and API Key as prompted to log in to the NGC container environment.

   `docker login nvcr.io`

   If the following output is displayed, you are logged in to the NGC container environment.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff118868eff3c35ac31f59b4e2ce30c6.png) </span>

4. Log in to the [NGC official website](https://ngc.nvidia.com/) and select "Containers" in the left navigation pane.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d45aec504b6cd998f458134d25480af.png) </span>

5. Enter "TensorFlow" in the search box, and then click the "Copy Image Path" button on the `NVIDIA L4T TensorFlow` card to automatically copy the address of the latest version of the TensorFlow image.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ab5f7e918ab12a3cca1b46d5ea2fd2d1.png) </span>

6. Execute the following commands in sequence to pull the image and view the downloaded image file.

   ```Plain Text
   docker pull nvcr.io/nvidia/clara-agx/agx-tensorflow:21.05-tf1-py3 //Please replace the <link> with the TensorFlow <image> address copied in the previous step
   docker images //view the downloaded image, the output is as follows, indicating the pull was successful
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_962ac59a6bc478698417a60c2b77e38d.png) </span>


<span id=".5q2l6aqk5Zub77ya6YOo572yVGVuc29yRmxvd-W8gOWPkeeOr-Wigw=="></span>
## Step 4: Deploy the TensorFlow development environment

Execute the following command to run the container.

`nvidia-docker run --rm -it nvcr.io/nvidia/tensorflow:18.03-py3`

If the following output is displayed, the deployment is successful.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7764551508a1152045688970ee5f00ee.png) </span>

<span id=".5q2l6aqk5LqU77ya6aqM6K-B5rWL6K-V"></span>
## Step 5: Verify and test the environment


1. Execute the `python` command. If the environment is normal, you will directly enter the Python environment.

2. In the Python environment, execute the following commands in sequence.

   ```Plain Text
   import tensorflow as tf
   hello = tf.constant('Hello, TensorFlow!')
   sess = tf.Session()
   sess.run(hello)
   ```
   

   If the following output is displayed, the TensorFlow environment is set up successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93923e7b334f6f0d0d348fa63af5986f.png) </span>
