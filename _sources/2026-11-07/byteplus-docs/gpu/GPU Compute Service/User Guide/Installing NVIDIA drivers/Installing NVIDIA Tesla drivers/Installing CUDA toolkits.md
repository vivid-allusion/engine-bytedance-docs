---
title: "Installing CUDA toolkits"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits"
---

<span id=".Q1VEQeW3peWFt-WMheS7i-e7jQ=="></span>
## CUDA toolkit introduction

CUDA (Compute Unified Device Architecture) is a computing platform launched by NVIDIA. This platform enables GPUs to solve complex computational problems based on CUDA Instruction Set Architecture (ISA) and the parallel computing engines built into GPUs.

Since GPU instances use NVIDIA graphics cards, installing the CUDA development and runtime environment is required. We recommend installing the CUDA driver of the latest version, as it is compatible with various Linux and Windows operating systems, including CentOS, Ubuntu, Debian, Windows, and many others.

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

If CUDA is not installed when you create a GPU instance, follow this topic to manually install the CUDA toolkit for the created instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For ease of use, when creating a GPU instance, you can select a public image that either supports auto\-installation of specific versions of the GPU driver and CUDA or is pre\-installed with them. For details, refer to <a href="https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide">NVIDIA driver installation guide</a>.</div>


* <div data-tips="true" data-tips-type="tip">If you install the GPU driver and CUDA toolkit manually, ensure that their versions are compatible with each other. <a href="https://docs.nvidia.com/deploy/cuda-compatibility/index.html#binary-compatibility__table-toolkit-driver">Learn more</a>.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have purchased a GPU instance and associated an EIP with it, enabling the instance to connect to the Internet.

<span id=".5a6J6KOFQ1VEQeW3peWFt-WMhe-8iExpbnV477yJ"></span>
## Install CUDA toolkit (Linux)


1. Log in to the [website to download the CUDA toolkit](https://developer.nvidia.com/cuda-toolkit-archive), and select the appropriate operating system and version based on the GPU instance configuration. In this topic, downloading CUDA 12.3 on Ubuntu 20.04 64 bit is used as an example, as displayed below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Two methods are supported to install CUDA: runfile and deb. runfile is recommended, as it does not require handling dependency packages and is simpler and faster.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f91a98fa2dc45f1febe23e4fbf65edf1.png) </span>

2. After you select the required options, the following page appears. Then, copy the installation commands.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6ae9414900c579d5338739da2752f1e.png) </span>

3. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

4. Execute the commands obtained in step 2. When you execute the second command, refer to the following instructions to complete the operations in sequence.

   1. In the installation interface, enter "accept" and press Enter to proceed to the next step.

   2. Use the up and down arrow keys on the keyboard to select "Install", and press Enter to confirm and start the installation.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If your ECS instance has the GPU driver installed, press Enter as shown in the following picture to uncheck the GPU driver option before proceeding with the installation.      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6733b7ea22fadd8eb3fd0ae1bfa99b5.png" width="400px" />      </div>
      

5. After installation is complete, execute the following command to view the CUDA version. This indicates that CUDA is installed successfully.

   ```Plain Text
   /usr/local/cuda/bin/nvcc -V
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ab9a0c60956faf58fab38f0df7d2f2d6.png) </span>


<span id=".5a6J6KOFQ1VEQeW3peWFt-WMhe-8iFdpbmRvd3PvvIk="></span>
## Install CUDA toolkit (Windows)


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. In the remote desktop, use a browser to access [CUDA download link](https://developer.nvidia.com/cuda-toolkit-archive), and select the appropriate operating system and version based on the GPU instance configuration.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bafa62507df592128d79b9f812e062a1.png) </span>

3. After you select the required options, the following page appears. Then, click the "Download" button to the right of "Base Installer" to download CUDA.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c4bba0b454248b33034be7cf3a584d3.png) </span>

4. After the download is complete, open the folder where the toolkit installation file is stored, double\-click it, and follow the prompts to complete the installation.

5. After installation is complete, right\-click on the desktop and select NVIDIA Control Panel from the context menu. Click "NVIDIA Control Panel", and select the "System Information" button in the lower left corner of the Control Panel. Select the "Components" tab to view the CUDA version.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_282ea941ce8946e69a403f10001b57db.png) </span>
