---
title: "NVIDIA driver installation guide"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide"
---

<span id="gY3vaJ3w"></span>
## Driver introduction

NVIDIA drivers are programs used to drive NVIDIA GPU cards. As the software corresponding to the hardware, they enhance the operating system's compatibility with the GPU chipset. Currently, all GPU instances provided by BytePlus are Compute\-optimized, which is a GPU pass\-through type, requiring GPU drivers to be installed to drive the physical GPU cards and unleash their capabilities.

Currently, GPU instances support the following two types of NVIDIA drivers (the latest driver version is recommended):


|Driver type |Description |Fee |
|---|---|---|
|Tesla driver |Used to drive physical GPU cards, enabling general computing capabilities on GPU instances. This type is applicable for deep learning, inference, AI, and other scenarios.<br><br>We recommended using Tesla drivers with CUDA and cuDNN libraries to utilize GPU cards more efficiently. |Free |
|GRID driver |Used to obtain graphics acceleration capabilities of GPU cards, applicable for graphics computing scenarios like OpenGL. |You need to purchase an NVIDIA GRID License. |


<span id=".5YWs5YWx6ZWc5YOP5a6J6KOFVGVzbGHpqbHliqg="></span>
## Operation guide

Select the required driver type and installation method based on instance type and operating system. For instance types, refer to [GPU instance family list](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types#FZuiXLTc).


|Instance type |Recommended driver type |Supported installation methods |
|---|---|---|
|Compute\-optimized instance |Tesla driver |* During instance creation:<br><br>   * [(Recommended) Configure the driver to be automatically installed after you select a public image (Linux) of the standard version](https://docs.byteplus.com/en/docs/gpu/Automatically_installing_Tesla_drivers_during_instance_creation#.5pa55byP5LiA77ya5ZCO5Y-w6Ieq5Yqo5a6J6KOFR1BV6amx5Yqo)<br><br>   * [(Recommended) Use a public image of the GPU version with a pre-installed Tesla driver](https://docs.byteplus.com/en/docs/gpu/Automatically_installing_Tesla_drivers_during_instance_creation#vQ1gg8oI)<br><br>* After you create an instance:<br><br>   * [Manually install the GPU driver](https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers), [the CUDA toolkit](https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits), and then [the Fabric Manager package](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager)<br><br>   * [(Recommended) Use the cloud assistant to batch install Tesla drivers](https://docs.byteplus.com/en/docs/gpu/Quickly_installing_Tesla_drivers_in_created_instances#cNqrNWRv)<br><br>   * [Select a public image with a pre-installed driver when you change the instance operating system](https://docs.byteplus.com/en/docs/gpu/Quickly_installing_Tesla_drivers_in_created_instances#q16oLGbp) |
|Rendering instance |GRID driver |* When you are creating an instance:<br><br>   [(Recommended) Use a public image with the GRID driver pre-installed to automatically load the GRID driver](https://docs.byteplus.com/en/docs/gpu/Automatically_loading_GRID_drivers_during_instance_creation)<br><br>* After you create an instance:<br><br>   [Apply for License and manually install the GRID driver](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers) |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When creating a rendering instance, you can select a public image with a pre\-installed GRID driver. This enables the GRID driver with an activated License to be loaded automatically. Thus, no need to install the driver manually. If you need a Compute\-optimized instance for graphics acceleration scenarios, <a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers">apply for a License</a> <a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers">from the official NVIDIA website</a>.</div>


<span id="F1nMPtDD"></span>
## Related documents


* If the driver version does not match your current scenario, or if you can not access your instance due to an inappropriate type or version of the installed driver, you can uninstall the current driver and then install a new one. For more details, refer to [Uninstalling NVIDIA Tesla drivers](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers), [Uninstalling NVIDIA-Fabric Manager packages](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Fabric-Manager), and [Uninstalling NVIDIA GRID drivers](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-GRID-drivers).

* For NVIDIA driver\-related issues, refer to [NVIDIA driver FAQs](https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-FAQs).
