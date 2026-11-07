---
title: "Solutions for modification of instance specifications"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification"
---

You can flexibly adjust Redis instance configurations based on business volume changes. This includes horizontal scaling (increasing or decreasing the number of instance shards), vertical scaling (upgrading or downgrading node specifications), and adjusting the number of nodes per shard. This topic describes the configuration adjustment solutions supported by Redis.

## Precautions

* For sharding cluster enabled instances with an applied direct connection address, the instance's shard count cannot exceed 8 during configuration changes. If you need to increase the number of shards while direct connection is enabled, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

* The completion time for configuration changes is influenced by various factors (such as network, task queue, current instance load, and data volume). Perform configuration adjustments during off\-peak business hours.

## Specification modification solutions

Different modification operations apply to different Redis instance types. The specific applicable scenarios are shown in the table below.

> **tip**

> In the table below, ✔️ indicates that the current instance or architecture type supports this configuration modification solution, while ❌ indicates it does not.

|Specification modification operation ||Scenario |Impact |Supported instance or architecture types ||||
|---|---|---|---|---|---|---|---|
|||||Primary\-secondary instance ||Single\-node instance ||
|||||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled |
|[Modifying number of nodes](https://docs.byteplus.com/en/docs/redis/modify-node-number) ||Each shard in the Redis primary\-secondary instances contains one primary node and at least one secondary node. There is a replication relationship between the primary and secondary nodes. Redis supports changing the scalability and high availability of instances by increasing or decreasing the number of secondary nodes. For more details, refer to [Core components](https://docs.byteplus.com/en/docs/redis/about-redis#.5qC45b-D57uE5Lu2). |* Adding nodes has no impact on the instance or services.<br><br>* When reducing nodes, the instance might experience up to 1 connection interruption, lasting within 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism. |✔️ |✔️ |❌ |❌ |
|[Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec) |Vertical upscaling<br><br>(Upgrading node specifications) |You can perform upscaling, if the CPU load of the instance server node is relatively high or the total memory capacity is insufficient. |During the node specification change, the instance may experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism. |✔️ |✔️ |✔️ |✔️ |
||Vertical downscaling<br><br>(Downgrading node specifications) |Free up surplus memory capacity through downscaling.<br><br>> **tip**<br><br><br>> If you want to downgrade the node specification, you need to ensure that the current **Used memory** of the instance does not exceed 85% of the total new memory capacity, where total new memory capacity = modified single shard memory \* shard number.<br> ||✔️ |✔️ |✔️ |✔️ |
|[Modifying number of shards](https://docs.byteplus.com/en/docs/redis/modify-shard--number) |Horizontal upscaling<br><br>(Increasing shard) |You can perform upscaling, if the CPU load of the instance server node is relatively high or the total memory capacity is insufficient. |During the process of adding shards, the instance might prompt error `-TRYAGAIN The specific keys are being migrated.\r\n`. |✔️ |❌ |✔️ |❌ |
||Horizontal downscaling<br><br>(Reducing shard) |Free up surplus memory capacity through downscaling.<br><br>> **tip**<br><br><br>> If you need to reduce the number of shards, make sure that the **Used memory** of each single shard in the instance after reducing the shards does not exceed 85% of the memory specification of a single shard. Otherwise, the configuration change will fail.<br> |During the process of reducing shards or changing sharding cluster configuration of instance, the instance might prompt the error `-TRYAGAIN The specific keys are being migrated.\r\n`, or experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism. |✔️ |❌ |✔️ |❌ |
|[Modifying sharding cluster configuration](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config) ||Change instances with sharding cluster disabled to instances with sharding cluster enabled to meet business horizontal scaling requirements. ||❌ |✔️ |❌ |✔️ |
|[Switching to primary-secondary instance](https://docs.byteplus.com/en/docs/redis/switch_to_high_availability_instance)<br><br> ||Cache for Redis offers single\-node and primary\-secondary instance types. Primary\-secondary instances offer enterprise\-grade high\-availability capabilities such as persistent storage, automatic backup, cross\-availability zone disaster recovery, and read/write splitting, effectively ensuring data persistence, availability, and security. You can switch a single\-node instance to a primary\-secondary instance to meet business growth demands for a high\-availability architecture.<br><br>> **tip**<br><br><br>> During the process of switching to a primary\-secondary instance, if you also reduce the number of shards or downgrade node specifications, ensure that the current **Used memory** of the instance does not exceed the total new memory capacity, where total new memory capacity = modified single shard memory \* shard number.<br> |During the change process, the instance might prompt the error `-TRYAGAIN The specific keys are being migrated.\r\n`, or experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.<br><br> |❌ |❌ |✔️ |✔️ |

## Billing information

For details on the billing rules for changing instance configurations, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription#.5Y-Y5pu06YWN572u).
