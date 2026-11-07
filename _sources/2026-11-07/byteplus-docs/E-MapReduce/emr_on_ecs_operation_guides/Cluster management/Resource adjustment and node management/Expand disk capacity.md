---
title: "Expand disk capacity"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_expand_disk_capacity"
---

When the data storage space of an E\-MapReduce (EMR) cluster is insufficient, you can expand the disk (data disk) capacity by following the instructions in this document.

<span id="_1-使用限制"></span>
## Limits

The EMR console only supports expansion of **data disks** and does not support expansion of **system disks**. To expand **system disks**, go to the ECS console. For details, see [Cloud Disk Expansion Overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume).

<span id="操作步骤"></span>
## Procedure


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)

2. In the left navigation pane, click **Resources \> on ECS \> Cluster Details \> Nodes,**  and go to the **Nodes** page.

3. Click the **Disk expansion** button in the operation column of the target node group.

4. In the disk expansion dialog box, set the expanded capacity for the data disk.

5. Select the checkbox to agree to the E\-MapReduce service terms, and click OK to submit.
