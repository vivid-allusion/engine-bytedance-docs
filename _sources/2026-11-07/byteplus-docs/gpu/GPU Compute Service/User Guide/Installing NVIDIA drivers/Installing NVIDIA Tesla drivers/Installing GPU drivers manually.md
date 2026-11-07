---
title: "Installing GPU drivers manually"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers"
---

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

To ensure that a GPU instance runs properly, you need to install the appropriate infrastructure software in advance. For NVIDIA Tesla series GPUs, the following software packages are needed:


* Hardware driver program: used to drive GPUs.

* Libraries: required by upper\-layer applications.


For general\-purpose computation scenarios, like deep learning and AI, or graphics acceleration scenarios like OpenGL, Direct3D, and cloud gaming, GPU instances can offer high\-performance computing capabilities or display smoother graphics only with the Tesla driver installed.

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

If the Tesla driver is not installed when you create a GPU instance, follow this topic or refer to [Installing CUDA toolkits](https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits) to install the driver manually for the created GPU instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you install the GPU driver and CUDA Toolkit manually, ensure that their versions are compatible with each other. <a href="https://docs.nvidia.com/deploy/cuda-compatibility/index.html#binary-compatibility__table-toolkit-driver">Learn more</a>.</div>


* <div data-tips="true" data-tips-type="tip">For ease of use, when creating a GPU instance, you can select a public image that either supports auto\-installation of specific versions of the GPU driver and CUDA toolkit or is pre\-installed with them. <a href="https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide">Learn more</a>.</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager">Installing the NVIDIA\-Fabric Manager service</a> is required when the GPU instance is equipped with A100/A800 graphics cards. Otherwise, you may fail to use the instance normally.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have purchased a GPU instance and associated an EIP with it, enabling the instance to connect to the Internet.

<span id=".5a6J6KOFR1BV6amx5Yqo77yITGludXjvvIk="></span>
## Install GPU driver (Linux)

The driver installation for Linux operating systems uses a Shell script, which is applicable to any Linux operating system, such as CentOS and Ubuntu.


1.   Visit [the Nvidia driver download page](https://www.nvidia.com/en-us/drivers/).

2. Set the search conditions and click the "Find" button to find the driver version that matches the specified conditions.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7be8d0286888c00bb1e319df510dadd6.png) </span>

   
   |Configuration item |Description |Example |
   |---|---|---|
   |* Product type<br><br>* Product series<br><br>* Product family |Select based on GPU card configuration of the target instance type. For details, refer to [Instance types](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types). |* Data Center / Tesla<br><br>* T\-Series<br><br>* Tesla T4 |
   |Operating systems |Select the Linux operating system version corresponding to the instance image.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select Linux 64\-bit for the operating system, this indicates downloading the Shell script installer. If you select a specific platform version, the file that you download is the corresponding installation package.</div><br> |Linux 64\-bit |
   |CUDA Toolkit |Select the CUDA Toolkit version. |12.2 |
   |Language |Select the driver language. |Chinese (Simplified) |
   

3. Select a specific version and click the "View" button.

4. On the driver download page, right\-click the "Download" button and select "Copy link address" from the pop\-up menu.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_217f93206929fe40951bdc91be3be209.png) </span>

5. [Log in to the GPU instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

6. Use the `wget` command, paste the link address obtained in step 4, and download the installation package (note: the GPU instance must have internet access). Example:

   ```Plain Text
   wget https://cn.download.nvidia.com/tesla/535.216.03/NVIDIA-Linux-x86_64-535.216.03.run
   ```
   

7.  **(Conditionally required​)**  If you use the "veLinux 1.0 CentOS compatible edition with 5.10 kernel" or "veLinux 1.0 CentOS Compatible Edition" image for the instance, execute the following command to modify the default version of the GNU Compiler Collection (GCC).

   ```Plain Text
   source /opt/rh/devtoolset-8/enable
   ```
   

8. Execute the `sh` command to run the driver installation program, and follow the prompts to perform subsequent operations.

   ```Plain Text
   sh NVIDIA-Linux-x86_64-535.216.03.run
   ```
   

9. After installation is complete, execute the following command to verify.

   ```Plain Text
   nvidia-smi
   ```
   

   If GPU information similar to the following output is returned, the GPU driver is installed successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c526f9c8dd6c725b65ac0aa80252c5a1.png) </span>


<span id=".5a6J6KOFR1BV6amx5Yqo77yIV2luZG93c--8iQ=="></span>
## Install GPU driver (Windows)


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. In the remote desktop, use the browser to   Visit [the Nvidia driver download page](https://www.nvidia.com/en-us/drivers/).

3. Set the search conditions and click the "Find" button to find the driver version that matches the specified conditions.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a6d20663e77f64202bf3d9b755b1101.png) </span>

4. Select a specific version and click the "View" button.

5. Click the "Download" button to download the driver.

6. Click the "Run" and "View download" buttons in sequence. After the download is complete, click the "OK" button and follow the prompts to complete the installation.

7. After installation is complete, right\-click on the desktop and select NVIDIA Control Panel from the context menu. Click "NVIDIA Control Panel", and select the "System Information" button in the lower left corner of the Control Panel to view the driver version.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1268ddb1510a9555d36727a023de683.png) </span>
