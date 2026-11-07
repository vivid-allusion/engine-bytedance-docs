---
title: "GPU - Building AIGC capabilities (Linux)"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_-_Building_AIGC_capabilities_Linux"
---

This topic describes how to deploy the Stable Diffusion WebUI frontend tool and Stable Diffusion training model to generate high\-quality AI images. It helps you master the entire AI image generation inference process and the impact of key parameters on image output.

## AIGC overview

AI Generated Content (AIGC) refers to a content production method that automatically generates content using AI technology. It signifies that AI has evolved from understanding language, text, images, and videos to generating content, representing a new "human\-machine co\-creation" model.

## Software version

* NVIDIA driver: In the example provided in this topic, Tesla 470.57.02 is used with Cuda 11.4.1.

* Python: A programming language that provides machine learning libraries such as NumPy. In the example provided in this topic, Python 3.11.3 is used.

* PIP: A universal Python package management tool. In the example provided in this topic, PIP 20.0.2 is used.

* Git: A distributed version control system. In the example provided in this topic, Git 2.25.1 is used.

## Usage notes

* To ensure the smooth operation of Stable Diffusion WebUI and the associated model, we recommend that you specify **12 GB** of video memory and more than **16 GiB** of memory for the instance. This enables support for larger images and higher preprocessing efficiency.

   In the example provided in this topic, the ecs.ini2.7xlarge instance type is used, equipped with an NVIDIA A30 GPU card, 24 GB of video memory, and 234 GiB of memory.

* Downloading the software required for this example may require access to websites outside the Chinese mainland. We recommend that you add a network proxy, such as FlexGW, to improve access speed. Alternatively, you can download the required software to your local device and upload the software to the GPU instance by referring to [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).

## Step 1: Create a GPU Accelerated instance

Create an instance that meets the following conditions. For more information, see [Purchasing instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Instance type: ecs.ini2.7xlarge

* Image: Ubuntu 20.04. Specify that the following GPU driver is automatically installed in the background.

* EIP: Select "Assign Elastic IP (EIP)".

## Step 2: Install Python and PIP

1. Log in to the [Python website](https://www.python.org/downloads/source/).

2. Find and click Python 3.11.3 to enter the version 3.11.3 download page.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c00a024a74e95b457a0610fd21dd8a79.png)

3. Scroll to the bottom of the page, right\-click "Gzipped source tarball", and select "Copy link address" to copy the download address of the Python installation package. In this example, the download address is `https://www.python.org/ftp/python/3.11.3/Python-3.11.3.tgz`.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0682c0d5bc68e4d194da08ff60c9b09a.png)

4. Remotely connect to and log in to the instance. For more information, see [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

5. Execute the following command to pull and install the Python installation package.

   ```Plain Text
   apt update
   apt -y upgrade
   wget https://www.python.org/ftp/python/3.11.3/Python-3.11.3.tgz
   tar -zxvf Python-3.11.3.tgz
   cd Python-3.11.3/
   ./configure --prefix=/usr/local/python3.11.3
   make && make install
   ```

6. Execute the following command to install PIP.

   ```Plain Text
   cd
   apt install python3-pip
   ```

7. Execute the `pip --version` command. If the following output is displayed, the installation is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e8da50b8e9b56264b9456871d28ed5e.png)

## Step 3: Install Git

1. Execute the following command to install Git.

   `apt -y install git`

2. Execute the `git --version` command. If the following output is displayed, the installation is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a5855f25510e659eb84fec5bf20f62d.png)

## Step 4: Confirm the NVIDIA driver

1. Execute the `nvidia-smi` command. If the GPU version is displayed, the GPU driver is installed.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cdc7ec468851f6d9aa6496ac626ecf9a.png)

2. Execute the `/usr/local/cuda/bin/nvcc -V` command. If the CUDA version is displayed, CUDA is installed.

## Step 5: Install Stable Diffusion UI

Execute the following command to install Stable Diffusion UI.

```Plain Text
cd 
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

If the following output is displayed, the download is successful.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0db598b877d2ec6d391bd3490cea17fa.png)

## Step 6: Download the Stable Diffusion training model

1. Log in to the [Stable Diffusion code repository](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/tree/main) and click the "Files and versions" tab.

2. Right\-click the "sd\-v1\-4.ckpt" training model to copy the download link. In this example, the download link is `https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/blob/main/sd-v1-4.ckpt`.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83c5dfe903d016a16b1c69dc927af910.png)

3. Execute the following commands in sequence to navigate to the training model storage directory and download the model to the directory.

   ```Plain Text
   cd stable-diffusion-webui/models/Stable-diffusion/
   wget https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/blob/main/sd-v1-4.ckpt
   ```

4. Execute the following command to navigate to the training model webui directory.

   `cd && cd stable-diffusion-webui/`

5. Execute the following command to add the Tsinghua University mirror site.

   1. Execute the `vi launch_utils.py` command.

   2. Search for the code `run(f'"{python}" -m {torch_command}` and add the Tsinghua University mirror site `-i https://pypi.tuna.tsinghua.edu.cn/simple`.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_290636a9dcc62e2db76e41f5d52eff5f.jpeg)

   3. Search for the code `return run(f'"{python}" -m pip {command}` and add the Tsinghua University mirror site `-i https://pypi.tuna.tsinghua.edu.cn/simple`.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51a1e397482e4b668d12263fabc6bde5.jpeg)

6. Execute the following commands in sequence to enter and activate the python\-venv virtual environment.

   ```Plain Text
   apt -y install python3.8-venv
   python3 -m venv venv_name
   source venv_name/bin/activate
   ```

   If the following output is displayed, you have entered the virtual environment.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f53e4d9e785e6db74beb43d192e47a0.png)

7. Execute the following command to install gfpgan.

   ```Plain Text
   git clone https://github.com/TencentARC/GFPGAN.git
   pip install gfpgan
   ```

8. Execute the following commands in sequence to run the `webui.sh` file.

   `./webui.sh --share -f`

   Depending on your network speed, the process may take 20 minutes to 2 hours. Be patient and **do not close the remote connection window. ** If the run fails during the process, retry later or troubleshoot as needed.

9. If the following output is displayed, the download is complete.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90c129006dc50e7ea8bf77b9cdc8552d.png)

10. Open http://127.0.0.1:7860 in your browser. Do not close the remote connection window.

## Step 7: Generate images

1. Configure the relevant parameters in http://127.0.0.1:7860.

   |**Parameter​**  |**Description** |Sample value |
   |---|---|---|
   |Sampling Steps |The number of steps for AI inference. More steps result in richer details in the image but require more time. Typically, this parameter is set to a value ranging from 20 to 30. |20 |
   |Sampling method |The algorithm for AI generation. Common options include Euler a, Euler, and DDIM. |Euler a |
   |Image resolution |Image resolution depends on the graphics card. Images below 512 x 512 lack significant details. |512\*512 |
   |Extended options |* Restore faces: Generates more realistic facial features. When you select this option for the first time, several gigabytes of runtime libraries need to be downloaded first.<br><br>* Tiling: Creates tileable images (similar to ceramic tiles) with seamless horizontal/vertical alignment.<br><br>* Highres. fix: Enables AI to fill in content at a higher resolution. |Do not configure |
   |Batch count |The number of generation rounds. |1 |
   |Batch size |The number of images generated simultaneously per round. |1 |
   |CFG Scale |Higher values make the AI strictly adhere to the prompt but reduce creativity. Lower values increase creativity but may deviate from the prompt. This parameter is typically set to approximately 7. |7 |
   |Seed |A random seed that determines the initial state of diffusion for each image generation. In most cases, retain the default setting. |\-1 |

2. After clicking the "Generate" button, you will obtain an AI\-generated image stored locally, along with the image generation time and GPU utilization, as shown in the following figure.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eab05263481f93c26286ab1d3aa90123.png)
