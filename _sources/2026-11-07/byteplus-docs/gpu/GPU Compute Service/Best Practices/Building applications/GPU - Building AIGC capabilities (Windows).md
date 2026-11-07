---
title: "GPU - Building AIGC capabilities (Windows)"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_-_Building_AIGC_capabilities_Windows"
---

This topic describes how to deploy the Stable Diffusion WebUI frontend tool and Stable Diffusion training model to generate high\-quality AI images. It helps you master the entire AI image generation inference process and the impact of key parameters on image output.

<span id=".QUlHQ-eugOS7iw=="></span>
## AIGC overview

AI Generated Content (AIGC) refers to a content production method that automatically generates content using AI technology. It signifies that AI has evolved from understanding language, text, images, and videos to generating content, representing a new "human\-machine co\-creation" model.

<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* NVIDIA driver: In the example provided in this topic, Tesla 571.71 is used with Cuda 11.7.

* Python: A programming language that provides machine learning libraries such as NumPy. In the example provided in this topic, Python 3.10.6 is used.

* PIP: A universal Python package management tool. In the example provided in this topic, PIP 22.3.1 is used.

* Git: A distributed version control system. In the example provided in this topic, Git 2.38.1 is used.


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* To ensure the smooth operation of Stable Diffusion WebUI and the associated model, we recommend that you specify **12 GB** of video memory and more than **16 GiB** of memory for the instance. This enables support for larger images and higher preprocessing efficiency.

   In the example provided in this topic, the ecs.ini2.7xlarge instance type is used, equipped with an NVIDIA A30 GPU card, 24 GB of video memory, and 234 GiB of memory.

* Downloading the software required for this example may require access to websites outside the Chinese mainland. We recommend that you add a network proxy, such as FlexGW, to improve access speed. Alternatively, you can download the required software to your local device and upload the software to the GPU instance by referring to [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).


<span id=".5q2l6aqk5LiA77ya5Yib5bu6R1BV6K6h566X5Z6L5a6e5L6L"></span>
## Step 1: Create a GPU Accelerated instance

Create an instance that meets the following conditions. For more information, see [Purchasing instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


* Instance type: ecs.ini2.7xlarge

* Image: Windows Server 2019 Datacenter Edition 64 bit (GPU)

* EIP: Select "Assign Elastic IP (EIP)".


<span id=".5q2l6aqk5LqM77ya5a6J6KOFUHl0aG9u5ZKMUElQ"></span>
## Step 2: Install Python and PIP


1. Remotely connect to and log in to the instance. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Log in to the [Python website](https://www.python.org/downloads/release/python-3106/).

3. Scroll to the bottom of the page and click "Windows installer (64\-bit)" to download the Python installation package, which already includes PIP.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d8afa2477774b849b155f19261778b4.png) </span>

4. Double\-click the installation package to start the installation process. On the following page, select "Add Python to PATH", and then click "Install Now".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a332238bb0313e1741dc6ceeb77575b.png) </span>

5. Open "Command Prompt" and execute the `Python -V` command. If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_207bdb97e72932cc009126bf7bc0115b.png) </span>

6. Execute the `python -m pip install --upgrade pip -i https://mirrors.ivolces.com/pypi/simple/` command to upgrade PIP to the latest version.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28432e5ece7eefffb236990e37ce0793.png) </span>


<span id=".5q2l6aqk5LiJ77ya5a6J6KOFR2l0"></span>
## Step 3: Install Git


1. Log in to the [Git website](https://git-scm.com/download).

2. Select "Windows" and click "64\-bit Git for Windows Setup" to download the Git installation package.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_958ac29abc135db50d467cd853eb04bf.png) </span>

3. Double\-click the installation package to start the installation process, and repeatedly click the "Next" button to complete the installation.

4. Open "Git CMD" and execute the `git --version` command. If the following output is displayed, the installation is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_def8bab6a86cc82532c425ba1700315e.png) </span>


<span id=".5q2l6aqk5Zub77ya5LiL6L29TlZJRElB6amx5Yqo"></span>
## Step 4: Download the NVIDIA driver


1. Uninstall the GPU driver pre\-installed in the image. For more information, see [Uninstalling NVIDIA driver (Windows)](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers?lang=en#.5Y246L29TlZJRElBIFRlc2xh6amx5Yqo77yIV2luZG93c--8iQ==).

2. Install the GPU driver Tesla 571.71 compatible with Cuda 11.7. For more information, see [Installing GPU driver (Windows)](https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers?lang=en#.5a6J6KOFR1BV6amx5Yqo77yIV2luZG93c--8iQ==).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76612512e7afcf364b59c4158a33431f.png) </span>

3. Install the Cuda driver 11.7. For more information, see [Installing CUDA toolkit (Windows)](https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits?lang=en#.5a6J6KOFQ1VEQeW3peWFt-WMhe-8iFdpbmRvd3PvvIk=).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d999f0b73b67a005479a070e13886a94.png) </span>


<span id=".5q2l6aqk5LqU77ya5a6J6KOFU3RhYmxlIERpZmZ1c2lvbiBVSQ=="></span>
## Step 5: Install Stable Diffusion UI

Open "Git cmd" and execute the `git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git` command.

If the following output is displayed, the download is successful.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1379d33f30a5990549c57a17ac72e5c5.png) </span>

<span id=".5q2l6aqk5YWt77ya5LiL6L296K6t57uD5qih5Z6LU3RhYmxlIERpZmZ1c2lvbg=="></span>
## Step 6: Download the Stable Diffusion training model


1. Log in to the [Stable Diffusion code repository](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/tree/main) and click the "Files and versions" tab.

2. Download the "sd\-v1\-4.ckpt" training model to the `\stable-diffusion-webui\models\Stable-diffusion\` directory.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83c5dfe903d016a16b1c69dc927af910.png) </span>

3. Go to the `\stable-diffusion-webui\` directory and double\-click the `webui-user.bat` file to run the file.

4. After you double\-click the file, the script download begins. The process typically takes 20 minutes to 2 hours, depending on your network speed. The status may remain unchanged as shown in the following figure for an extended period. Be patient and **do not close the CMD window**. As long as the bottom of the window does not display a prompt like "Press any key to close this window", the script is still running as expected.

5. If the following output is displayed, the download is complete.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8bba412e65c8af211548a9a2a4e08a97.png) </span>

6. Open http://127.0.0.1:7860 in your browser. Do not close the CMD window.


<span id=".5q2l6aqk5LiD77ya55Sf5oiQ5Zu-54mH"></span>
## Step 7: Generate images


1. Configure the relevant parameters in http://127.0.0.1:7860.

   
   |**Parameter​**  |**Description** |Sample value |
   |---|---|---|
   |Sampling Steps |The number of steps for AI inference. More steps result in richer details in the image but require more time. Typically, this parameter is set to a value ranging from 20 to 30. |20 |
   |Sampling method |The algorithm for AI generation. Common options include Euler a, Euler, and DDIM. |Euler a |
   |Image resolution |Image resolution depends on the graphics card. Images below 512 x 512 lack significant details. |512\*512 |
   |Extended options |* Restore faces: Generates more realistic facial features. When you select this option for the first time, several gigabytes of runtime libraries need to be downloaded first.<br><br>* Tiling: Creates tileable images (similar to ceramic tiles) with seamless horizontal/vertical alignment.<br><br>* Highres. fix: Enables AI to fill in content at a higher resolution. |Do not configure. |
   |Batch count |The number of generation rounds. |1 |
   |Batch size |The number of images generated simultaneously per round. |1 |
   |CFG Scale |Higher values make the AI strictly adhere to the prompt but reduce creativity. Lower values increase creativity but may deviate from the prompt. This parameter is typically set to approximately 7. |7 |
   |Seed |A random seed that determines the initial state of diffusion for each image generation. In most cases, retain the default setting. |\-1 |
   

2. After clicking the "Generate" button, you will obtain an AI\-generated image stored locally, along with the image generation time and GPU utilization, as shown in the following figure.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eab05263481f93c26286ab1d3aa90123.png) </span>
