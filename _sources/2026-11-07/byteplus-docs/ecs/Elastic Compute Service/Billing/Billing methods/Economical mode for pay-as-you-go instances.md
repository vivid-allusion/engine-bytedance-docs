---
title: "Economical mode for pay-as-you-go instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances"
---

Economical Mode refers to putting the instance into a **stopped** status by **selecting Economical Mode** when stopping a pay\-as\-you\-go instance. After an instance is stopped, its computing resources (vCPU, GPU, and memory) will stop incurring fees, but the mounted volumes (system volume, data volume), images, Elastic IP (EIP), and bandwidth (fixed bandwidth mode) continue to incur fees. This topic describes the conditions for enabling Economical Mode and the billing situation of resources after Economical Mode is enabled.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When Economical Mode is enabled, only billing for certain instance resources (compute resources) stops. If you want to terminate instance billing, <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances">delete the instance and the resources (volume and EIP) associated with it</a>.</div>


* <div data-tips="true" data-tips-type="warning">For information on how to enable Economical Mode and how to set the default shutdown mode for instances on the platform, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Economical_mode_for_pay-as-you-go_instances-1">Economical Mode for Pay\-as\-you\-go</a>.</div>



<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Instances to be enabled in Economical Mode must meet the following conditions:


|Condition |Description |
|---|---|
|The billing method is pay\-as\-you\-go or spot instance |If it is a subscription instance, you can [change it to a pay-as-you-go instance](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go). |
|The instances do not have local volumes |This mode is not available for instances with local volumes, such as local SSDs or big data instances. For information on how to query the instance types that include local volumes, refer to the "local storage" column of each [instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types#.5a6e5L6L6KeE5qC85peP5YiX6KGo). |
|Non\-elastic bare metal or HPC\-optimized instances |Economical Mode is not available for Elastic Bare Metal (EBM) instances and HPC\-optimized instances. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Account arrears have the following impact on instances in Economical Mode:

   * If arrears exceed 2 hours, the EIP attached to instances in Economical Mode becomes unavailable.

   * If arrears exceed 15 days, billing for the volumes and EIPs attached to instances in Economical Mode will stop, and the purchased instances, volumes, and EIPs will be forcibly released.

* In scenarios where instances need to be started again in a short period of time, Economical Mode is not recommended, as it may lead to start failures. For example, the scenario of [changing the operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS).


<span id=".6IqC55yB5YGc5py65ZCO6LWE5rqQ5oOF5Ya1"></span>
## Resource status after Economical Mode is enabled

Once Economical Mode is enabled, the instance will be in the "stopped `Economical Mode`" state. The resources will be in status as shown in the following table.


|Resources |After instance stop |After instance restart |
|---|---|---|
|Compute resources (vCPUs, GPUs, and memory) |The resources will be reclaimed and billing ends. |Due to the reclamation of compute resources, the instance may fail to start if there is insufficient inventory when starting. You can try again later or [change the instance type](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type). If the start fails, the instance remains in Economical Mode. |
|* Volumes (system volumes and data volumes)<br><br>* Image<br><br>* Elastic IP (EIP) and bandwidth (fixed bandwidth mode) |To avoid data loss, these resources will still be retained and billed based on billing rules. |* The private IP address and the EIP associated with the instance before shutdown remain unchanged.<br><br>* The data on the volume and the image configuration remain unchanged. |
