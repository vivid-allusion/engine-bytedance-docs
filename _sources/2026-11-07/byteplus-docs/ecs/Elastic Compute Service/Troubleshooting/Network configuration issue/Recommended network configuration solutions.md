---
title: "Recommended network configuration solutions"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_network_configuration_recommendation"
---

This topic describes how to improve network performance by modifying (increasing) the number of network interface queues. In the following content, CentOS Stream 9 64 bit operating system with the multiqueue feature enabled is used as an example to illustrate modification details.

In the example provided in this topic, the primary network interface of the target instance is named "eth0".

> The multiqueue feature can distribute network interrupts of an instance across multiple CPUs. This improves network performance and response speed. Additionally, the multiqueue feature can mitigate performance degradation due to the bottleneck where one vCPU handles all network interrupts.


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Under the same network PPS and bandwidth conditions, a greater number of queues delivers more significant performance improvements. For example, compared with one queue, using two queues can increase network performance by 50% to 100%.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance type and image support the multiqueue feature. For details, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the multiqueue status of the primary network interface.

   ```Plain Text
   ethtool -l eth0
   ```
   

   If the returned information contains two `Combined` entries, this indicates that the multiqueue feature is enabled for the primary network interface. Proceed to customize the number of queues for the primary network interface based on your needs.

   ```Plain Text
   Channel parameters for eth0:
   Pre-set maximums:
   RX: 0
   TX: 0
   Other: 0
   Combined: 2 # A maximum of 2 queues are supported for configuration
   Current hardware settings:
   RX: 0
   TX: 0
   Other: 0
   Combined: 1 # A total of 1 queue is currently active
   ```
   

3. Execute the following command to configure two queues for the primary network interface.

   ```Plain Text
   sudo ethtool -L eth0 combined 2
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84fe03e73a3253045da4a21f3f0474b4.png) </span>
