---
title: "LAS job development"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/LAS_job_development"
---

This article describes how to use [the development machine](https://www.volcengine.com/docs/6492/1738923) for job development.

The typical practice for job development is to start a development machine for remote job development. After job development is complete, package the job and use the LAS [task management](https://www.volcengine.com/docs/6492/1747868) feature to run the job online. Users can also choose to develop jobs locally, but due to issues with operating system compatibility, model support, and Python package support, it is still recommended to use the LAS pre\-configured development machine for job development.

<span id="680442eb"></span>
## Prerequisites


* The development machine has been created. For detailed instructions, please refer to [Create a development machine](https://docs.byteplus.com/docs/Byteplus_LAS/create_a_development_machine).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to mount file storage vePFS or object storage TOS when creating a development machine. The reasons are as follows:</div>



* <div data-tips="true" data-tips-type="tip">The development machine may need to be rebuilt, and using vePFS/TOS allows code to be preserved.</div>


* <div data-tips="true" data-tips-type="tip">The development machine can share vePFS/TOS with distributed task containers, so jobs can be run without packaging images or job packages (details will be explained below).</div>


* ve\-daft has been installed and updated to the latest version. When creating a development machine, if the ve\-daft image is selected, ve\-daft, its Python dependencies, and model dependencies are already installed.

   The method for updating ve\-daft within the development machine is as follows:

   1. [Click to download the update package](https://las-ai-cn-beijing.tos-cn-beijing.volces.com/qa/whl/ve_daft-0.5.10.post8-cp39-abi3-manylinux_2_35_x86_64.whl).

   2. Install ve\-daft and the operator package provided by LAS.

   ```Python
   # Install ve-daft and the operator package provided by LAS
   pip install {Installation package name}[las]
   pip install {Installation package name}[flash-attn] # Model acceleration tools
   ```
   

* The development machine has been connected remotely via SSH. For detailed instructions, please refer to: [Remote connection to the development machine](https://docs.byteplus.com/docs/Byteplus_LAS/92509).


<span id="ab212637"></span>
## Job development and online execution

<span id="e409ece1"></span>
### Job development

<span id="548dfc95"></span>
#### Method 1: Use vePFS/TOS mounting

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9a96794359d4f4eaba5c495bf30e5de~tplv-goo7wpa0wc-image.image) </span>

<span id="c986cbe4"></span>
#### Method 2: Use an image

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c68d5855bf834306a813d6672475a9d6~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Method two has obvious drawbacks during the development phase due to the need to frequently package and download images, but it offers significant advantages in runtime by ensuring environment stability through images.</div>


<span id="8ff87048"></span>
#### Code development

Once the environment is ready, you can develop code in TRAE, VSCode, or the terminal.

<span id="cab21c26"></span>
### Online execution

Refer to [Task management](https://docs.byteplus.com/docs/Byteplus_LAS/Task_manage) to submit the developed job to task management for execution.

<span id="a057d8c6"></span>
#### Method 1: Use vePFS/TOS mounting

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e9ff060fcaa4efd98239afeddc39d90~tplv-goo7wpa0wc-image.image) </span>


1. Fill in the same base image as the development machine, or at least a newer image from the same series.

2. Specify the command to invoke the main Python script. Whenever possible, use absolute paths for Python commands.

3. Fill in environment variables. Common environment variables are typically as follows.


```Bash
export ACCESS_KEY=xxx
export SECRET_KEY=xxx
export TOS_ENDPOINT=https://tos-cn-beijing.volces.com  # Use https://tos-cn-beijing.ivolces.com for internal network
export TOS_REGION=cn-beijing
```



4. Specify the mounted vePFS/TOS path. Make sure the mount path is consistent with the development machine.


<span id="fd2e0122"></span>
#### Method 2: Use an image


1. First, save the development machine image on the development machine page.

2. As with Method 1, select the newly created image on the task management page, fill in the startup command and environment variables (mounting vePFS/TOS is not required).
