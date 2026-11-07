---
title: "Restarting instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Restarting-instances"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

This topic describes how to restart one or multiple ECS instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Only ECS instances in the **Running** state can be restarted.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Restarting an instance will interrupt your business for a short period of time. Proceed with caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region to which the target instance belongs.

4. On the instance list page, check the ECS instance that you want to restart and click "... \> Instance state \> Reboot instance" in the "Actions" column.

5. In the dialog box that appears, confirm the instance name.

6. Confirm the instance to be restarted and select a restart method.

   * Reboot: the default and standard restart mode.

   * Forced restart: Forcibly power off the running instance and then restart it.

      For instances other than bare metal instances, performing a forced restart causes all cached data that has not been written to storage devices to be lost. We recommend that you do not perform this operation on instances that are running normally.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Bare metal instances currently can only be restarted in forced restart mode.      </div>
      

7. Click "Reboot" to complete the operation.


<span id=".5pON5L2c57uT5p6c"></span>
## Result

After you restart an ECS instance, the instance changes to the  ** Restarting** state. After a short period of time, it changes to the **Running** state.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [RebootInstance - Restarts an instance](https://docs.byteplus.com/en/docs/ecs/RebootInstance)

* [RebootInstances - Restarts one or more instances](https://docs.byteplus.com/en/docs/ecs/RebootInstances)
