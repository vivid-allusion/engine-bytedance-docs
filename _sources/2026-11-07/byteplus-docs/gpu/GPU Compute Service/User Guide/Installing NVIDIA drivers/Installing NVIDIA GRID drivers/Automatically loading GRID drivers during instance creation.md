---
title: "Automatically loading GRID drivers during instance creation"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Automatically_loading_GRID_drivers_during_instance_creation"
---

<span id="sVF9l5c1"></span>
## Applicable scenarios

For a GPU Rendering instance, you can configure a GRID driver to be automatically loaded when creating an instance of the corresponding types. Or, you can apply for a License and then manually install the GRID driver after creating a GPU instance. To optimize the computing performance and graphics rendering capabilities provided by a GPU instance, GRID driver is recommended.

This topic describes how to automatically load the GRID driver based on an image with a pre\-installed GRID driver when you create a [GPU Rendering instance](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types#FZuiXLTc). If you need OpenGL graphics and image processing capabilities for a GPU Accelerated instance, manually install the NVIDIA GRID driver and purchase the GRID License officially released by NVIDIA.

<span id="16bHCkin"></span>
## Procedure


1. Go to the [instance creation page](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance?). 

2. Select the GPU Rendering instance you need to purchase.

3. When you configure the parameter **Image**, select **Public Images** first, and then the public image version.

4. Then, follow the interface instructions to create the instance.


<span id="YQkESYma"></span>
## Image list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If provided driver versions can not meet your business requirements, you can <a href="https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-GRID-drivers">uninstall the GRID driver</a> and then <a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers">install a new one</a>.</div>


* <div data-tips="true" data-tips-type="tip">Images available for selection vary slightly by instance type. Please refer to the actual instance creation page.</div>




|Public image name |Applicable instance family |GRID driver version (installed by default) |
|---|---|---|
|Ubuntu Server 20.04 with GRID 13.1 |GPU Rendering |13.1 |
|veLinux 1.0 with GRID 13.1 |GPU Rendering |13.1 |
|Windows Server 2022 Datacenter Edition with GRID 13.1 |GPU Rendering |13.1 |
|Windows Server 2019 Datacenter Edition with GRID 13.1 |GPU Rendering |13.1 |
|Windows Server 2016 Datacenter Edition with GRID 13.1 |GPU Rendering |13.1 |


<span id="IXgmH56m"></span>
## Related documents


* If you have not configured the GRID driver to be automatically loaded when creating the instance, install the driver manually after you create the instance. For specific steps, refer to [Installing NVIDIA GRID drivers](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers).

* To upgrade the GRID driver version, refer to [How do I upgrade NVIDIA Tesla driver?](https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-FAQs#.5aaC5L2V5Y2H57qnTlZJRElBIEdSSUTpqbHliqjvvJ8=)
