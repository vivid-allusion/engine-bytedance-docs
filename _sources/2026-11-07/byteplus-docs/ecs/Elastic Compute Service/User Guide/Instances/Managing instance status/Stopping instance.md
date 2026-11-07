---
title: "Stopping instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Stopping-instances"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

This topic introduces how to stop one or more ECS instances.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Stopping an instance will interrupt your business operations. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">After you stop an instance, billing will not be stopped, and resources will be reserved for you. To stop billing, you need to <a href="https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances">delete the instance and the resources configured</a>.</div>


* <div data-tips="true" data-tips-type="warning">After a spot instance is stopped, you can not restart it if the inventory is insufficient.</div>


* <div data-tips="true" data-tips-type="warning">Stopping a Subscription instance does not affect the expiration time.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Only instances in the **Running** state can be stopped.

<span id=".5YGc5q2i5qih5byP"></span>
## Stop mode

The platform provides the following stop modes:


|Stop Mode |Resource Status after Stopping |Billing Status after Stopping |Resource Status after Restarting |
|---|---|---|---|
|Normal Mode |The instance and configured resources are reserved. |The instance and configured resources are still billed, and the fees are the same as before stopping. |The instance and configured resources are restored to the status before stopping. |
|Economical Mode |The computing resources (vCPU, GPU, and memory) of the instance will be reclaimed. To avoid data loss, the image, volumes, EIP, and bandwidth (fixed bandwidth mode) will be reserved. |Billing continues, and no fees are charged for computing resources (vCPU, GPU, and memory), but billing for retained resources such as Volumes and EIPs continues. |Due to the reclamation of computing resources, the stopped instance may fail to start due to insufficient inventory. You can try to restart it later or [change the instance type](https://docs.byteplus.com/en/docs/ecs/Overview-2). If the startup fails, the instance remains in Economical Mode. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only Pay\-as\-you\-go instances without local volumes mounted (excluding EBM and HPC\-optimized instances) support Economical Mode. For more information, refer to<a href="https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances"> Stop Charging for pay\-as\-you\-go instances</a>.</div>


* <div data-tips="true" data-tips-type="tip">The default stop mode of the system is "Normal Mode". To change it, please go to <a href="https://docs.byteplus.com/en/docs/ecs/Economical_mode_for_pay-as-you-go_instances-1#.5byA5ZCv6buY6K6k6IqC55yB5YGc5py65qih5byP">Stop preference settings</a>.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target instance.

4. On the Instances page, click "Stop" in the "Actions" column on the right side of the target instance.

5. In the pop\-up box, select the stop method and stop mode.

   * **Stop method**:

      * Stop: the default and regular method that follows the standard procedure for stopping ECS instances.

      * Forced stop: forces the running ECS instances to stop, which is equivalent to a power\-off operation. Bare metal instances currently only support forced stop.

         > Performing a forced stop will cause all cached data not stored to storage devices to be lost. We recommend that you do not perform this operation on instances running normally.         
         

   * **Stop mode**: Select "Normal Mode" or "Economical Mode". [Learn more](https://docs.byteplus.com/en/docs/ecs/Stopping-instances#.5YGc5q2i5qih5byP).

6. Click "Confirm" to complete the operation.


<span id=".5pON5L2c57uT5p6c"></span>
## Result

After you perform the stop operation, the instance changes to the **Stopping** state and then to the **Stopped** state after a short period.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [StopInstance - Stops an instance](https://docs.byteplus.com/en/docs/ecs/StopInstance)

* [StopInstances - Stops one or more instances](https://docs.byteplus.com/en/docs/ecs/StopInstances)
