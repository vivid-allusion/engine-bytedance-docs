---
title: "Overview of volume operations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-of-volume-operations"
---

This topic describes common operations in the lifecycle of volumes and the applicable scenarios.


|Operation |Applicable Scenario |
|---|---|
|[Create a volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume) |This operation can be applied in scenarios in which you want to create an empty volume for an Elastic Compute Service (ECS) instance. |
|[Attach a volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume) |This operation can be applied in scenarios in which you want to mount a created empty volume on an ECS instance. |
|[Partitioning and initialize a volume](https://docs.byteplus.com/en/docs/ecs/Initialize-volume-overview) |After you create a volume, you are required to initialize the data volume and create a file system. |
|[Reinitialize a volume](https://docs.byteplus.com/en/docs/ecs/Reinitialize-volume) |You can restore the volume to its state at the time of creation. |
|[Detach a volume](https://docs.byteplus.com/en/docs/ecs/Detach-volume) |If you no longer want to use a volume, you can detach it from its ECS instance. |
|[Delete a volume](https://docs.byteplus.com/en/docs/ecs/Delete-volume) |If you no longer want to use a volume to store data, you can delete it. |
|[Modify a volume property](https://docs.byteplus.com/en/docs/ecs/Modify-volume-attribute) |This operation can be applied in the following scenario: You want to modify the name and description of a volume and specify whether your data volume is deleted when you delete its instance. |
|[View a disk serial number](https://docs.byteplus.com/en/docs/ecs/View-a-volume-serial-number) |This operation can be applied in scenarios in which you want to view disk serial numbers in a Linux or Windows instance. |
|[Extend a volume](https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume) |If you want to increase the storage of a volume, you can extend its capacity. |
