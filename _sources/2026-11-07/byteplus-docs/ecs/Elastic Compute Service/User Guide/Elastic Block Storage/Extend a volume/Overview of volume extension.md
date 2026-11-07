---
title: "Overview of volume extension"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume"
---

<span id="operation-scenario"></span>
## Operation scenario

As your businesses develop and application data increases, your current volume capacity may not meet the requirements for storing massive amounts of business data. To solve this issue, we recommend that you expand volume capacity to increase the storage of a single Elastic Compute Service (ECS) instance without losing the existing data. This topic describes how to expand the capacity of system and data volumes.

The system allows you to perform hot volume expansion online. This type of expansion does not affect your business or require you to restart your ECS instance.

<span id="before-you-begin"></span>
## Before you begin


* Make sure you prepare a subscription or pay\-as\-you\-go volume.

* Make sure the instance on which your volume is attached is in the **running** status or the **stopped** status. You can expand your data volume offline or online.

* Make sure your account does not have overdue payments.


<span id="precautions"></span>
## Precautions


* The maximum capacity of a volume varies based on its type. For more information, refer to [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).

* After a volume is expanded, a billing rule takes effect based on the new capacity.

* A Master Boot Record (MBR) partition supports a maximum volume capacity of 2 TiB. Assume that you already set MBR as the format of your volume partition and want to expand the partition to larger than 2 TiB. In this case, we recommend that you recreate and attach a data volume, partition the volume using GUID partition table (GPT), and replicate the data of the MBR partition to the GPT volume.

* After you expand a partitioned volume again, only the capacity of the volume is expanded. In this case, you are required to partition the expanded part. You can log on to the ECS instance to expand or create partitions and file systems as needed.

* You cannot attach or detach a volume in the **Extending** status. Perform either operation after the expansion task is complete.
