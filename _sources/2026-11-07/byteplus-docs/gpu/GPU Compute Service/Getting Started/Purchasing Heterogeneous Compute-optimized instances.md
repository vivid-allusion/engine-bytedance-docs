---
title: "Purchasing Heterogeneous Compute-optimized instances"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Buying-GPU-Accelerated-instances"
---

You can purchase GPU Heterogeneous Compute\-optimized instances based on your business scenario.

<span id=".56ys5LiA5q2l77ya6LSt5LmwR1BV6K6h566X5Z6L5a6e5L6L"></span>
## Step 1: Purchase a Heterogeneous Compute\-optimized instance

The purchase process for Heterogeneous Compute\-optimized instances is the same as that for ECS instances. Select the appropriate instance type that meets your business scenario under **GPU Accelerated ** . For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types">Instance types</a>.</div>


* <div data-tips="true" data-tips-type="tip">For information related to the GPU driver, see <a href="https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide">Installation guide of NVIDIA drivers</a>.</div>



<span id=".5q2l6aqk5LqM77ya5ZCv5YqoRmFicmljIE1hbmFnZXLmnI3liqE="></span>
## Step 2: Start the Fabric Manager service

The NVIDIA\-Fabric Manager service enables interconnection between multiple graphics cards via NVSwitch. After you use a public image to purchase an instance equipped with multiple graphics cards and NVSwitch support, the service will be installed by default. You need to start the service manually. Otherwise, the instance does not work as expected.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For instances that support NVSwitch, refer to the feature overview of <a href="https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types">each instance type</a>.</div>


* <div data-tips="true" data-tips-type="warning">In the pni3l instance type family, instances equipped with two or more GPU cards are configured with an NVLink device by default. If the <code>nvidia-fabricmanager.service</code> status is <code>failed</code>, this is normal and does not affect business operations.</div>


* <div data-tips="true" data-tips-type="warning">If you select an image in which the service is not installed, manually install the service by referring to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager">Installing NVIDIA\-Fabric Manager packages</a>.</div>


1. Execute the following command to start the Fabric Manager service.

   `sudo systemctl start nvidia-fabricmanager`

2. Execute the following command to check whether the Fabric Manager service starts as expected. If the output is `active (running)`, the service starts as expected.

   `sudo systemctl status nvidia-fabricmanager`

3. (Optional) Execute the following command to specify that the Fabric Manager service starts automatically when the instance starts.

   `sudo systemctl enable nvidia-fabricmanager`


<span id=".55u45YWz5paH5qGj"></span>
## Related document

For information about how to create GPU instances by calling an API operation, see [RunInstances - Creates instances](https://docs.byteplus.com/en/docs/ecs/RunInstances).
