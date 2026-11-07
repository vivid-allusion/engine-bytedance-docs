---
title: "Add multiple instances to a scaling group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Add_multiple_instances_to_the_scaling_group"
---

A scaling group is a concept in [Auto Scaling (AS),](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling?lang=en) used to manage a group of ECS instances. You can batch add instances to a scaling group. With the elasticity offered by the scaling group, you can make full use of existing computing resources.

<span id="j1fa6btd"></span>
## Prerequisites

When adding instances in a batch to the scaling group, the selected instances must meet the following conditions:


* All instances must be Linux or Windows instances.

* This action is supported by the orchestration service, which by default uses the CustomerRoleForOOS role to submit operations. If you have not yet created this role, please refer to [Orchestration permission management](https://docs.byteplus.com/en/docs/ecs/Preparation) to enable it.

* The current scaling group only supports adding the primary network interfaces of instances. Before adding instances, please first read [Manually adding instances to a scaling group](https://docs.byteplus.com/en/docs/as/Adding-instances-manually) to understand the prerequisites, operation instructions, and policies on the resource association after instance addition.


<span id="W9jD73UQ"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project where the target instance resides.

4. On the Instances page, select one or more instances and click the "··· \> Add scaling group" button at the bottom of the list.

5. Select the target scaling group and select the "Entrusted instance to scaling group" checkbox.

   > * Mark "Entrusted" for instances in the scaling group. This determines whether their lifecycle is managed by the scaling group.

   > * Mark **Entrusted**: When the scaling group scales down, the instances will be automatically deleted along with the associated resources (such as EIP, volumes, network interfaces). For more information on entrustment, please refer to [Instance lifecycle](https://docs.byteplus.com/en/docs/as/Instance-lifecycle).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once entrusted, the action cannot be revoked.   </div>
   

6. Click the "Complete" button and then click the "Go Now" button in the upper\-right corner of the page to view execution details.

7. After successful execution, you can [view the details of the added instances](https://docs.byteplus.com/en/docs/as/Viewing-instance-details) in the scaling group console.


<span id="89byGmCq"></span>
## Related documents


* [Orchestration overview](https://docs.byteplus.com/en/docs/ecs/Overview_of_Process_Orchestration)

* [Introduction to Auto Scaling (AS) and scaling groups](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling)

* [Manually adding instances in a scaling group](https://docs.byteplus.com/en/docs/as/Adding-instances-manually)
