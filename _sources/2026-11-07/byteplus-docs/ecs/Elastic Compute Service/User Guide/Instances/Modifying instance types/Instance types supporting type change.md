---
title: "Instance types supporting type change"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-2"
---

If the current ECS instance type does not meet your business needs, you can refer to this topic to check the type changes supported by the instance. You can then change the instance type (including vCPU and memory) to perform an upgrade or downgrade. For detailed steps, please refer to [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Modify-instance-type).

<span id=".5LiN5Y-v5Y-Y5pu055qE5a6e5L6L57G75Z6L"></span>
## Unchangeable instance types

The following instance types cannot be changed:


* Local SSD

* Big Data

* EBM

* HPC\-optimized


<span id=".5Y-v5Y-Y5pu055qE5a6e5L6L57G75Z6L"></span>
## Instance types that can be changed

Other instance types, except for the unchangeable ones listed above, support type change, but the available target instance families vary. For details, see the table below.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The supported target instance types may be affected by inventory factors. Please refer to the actual display on the type modification page. You can also refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing_regions_where_instances_are_available_for_sale">Viewing regions where instances are available for sale</a> to view the instance types that can be purchased in the current region or availability zone.</div>


&nbsp;


|Original instance type family |Target instance type family |
|---|---|
|g4i, c4i, r4i |* g4i, c4i, r4i<br><br>* e |
|g3i, c3i, r3i |* g3i, c3i, r3i<br><br>* e |
|g3a, c3a, r3a |* g3a, c3a, r3a<br><br>* e |
|g2i |* t2, e<br><br>* g2i, c2i, r2i<br><br>* g3i, c3i, r3i<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To change g2i to g3i, c3i, or r3i, the following conditions must be met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The g2i instances must be running the Linux operating system and have the Virtio 1.1 driver installed. <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo">Check whether the Virtio1.1 driver is installed</a>.</div><br> |
|c2i, r2i |* e<br><br>* g2i, c2i, r2i<br><br>* g3i, c3i, r3i<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To change c2i/r2i to g3i, c3i, or r3i, the following conditions must be met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">c2i/r2i must be running the Linux operating system and have the Virtio 1.1 driver installed. <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo">Check whether the Virtio1.1 driver is installed</a>.</div><br> |
|t2 |* t2<br><br>* e<br><br>* g2i, c2i, r2i |
|e |* e<br><br>* t2<br><br>* g3i, c3i, r3i<br><br>* g3a, c3a, r3a<br><br>* g2i, c2i, r2i<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To change the e instance type to g3i, c3i, r3i, or g3a, c3a, r3a, the following conditions must be met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The e type instances must be running the Linux operating system and have the Virtio 1.1 driver installed. <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo">Check whether the Virtio1.1 driver is installed</a>.</div><br> |
|pni3l |pni3l |
|gni3cl |gni3cl |
|gni3c |gni3c |
