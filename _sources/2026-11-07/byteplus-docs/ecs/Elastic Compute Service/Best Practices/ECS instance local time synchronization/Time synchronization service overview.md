---
title: "Time synchronization service overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/BytePlus-NTP-server"
---

If the system time of your ECS instance is incorrect, or if you need to keep the time consistent across multiple instances in different regions, you can configure the time synchronization service for them.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios


* **Troubleshooting**

   When an ECS instance fails, the timestamp in the log is critical for troubleshooting. If the server time is inaccurate, it will increase the difficulty of fault diagnosis and may even prolong the system downtime caused by the fault.

* **Transaction processing**

   For an ECS instance used in payment and transaction scenarios, any time deviation is highly likely to alter the transaction order, trigger transaction disputes, and result in economic losses.

* **Scheduled tasks**

   If time synchronization of an ECS instance is exceptional, scheduled tasks deployed on the instance will not be triggered and executed at the preset accurate time. In the case of a time deviation, some tasks may start earlier or later than expected, disrupting the overall business workflow.


<span id=".5pe26Ze05LiN5ZCM5q2l55qE5Yik5pat5pa55rOV"></span>
## Determine whether the instance time is synchronized

If you suspect that the instance time is not synchronized with the actual time, you can refer to the following methods for assessment:


* **Compare system time and authoritative time source**


     You can obtain the accurate time from professional time reference channels, such as authoritative websites, TV broadcasts, and mobile devices, and compare it with the system time of the instance. If the system time of the instance is significantly different from the accurate time you obtain, the system time of the instance may not be synchronized.


* **Monitor scheduled tasks in instances**


     You can monitor the execution status of scheduled tasks specified in the instance. If you find that scheduled tasks are not executed at the expected time, the system time of the instance may not be synchronized.


* **Check Tracking logs**


     In distributed systems, Tracking logs are crucial for ensuring the correct execution of transactions and the consistency of data. Tracking logs record the processing order and status changes of transactions across different nodes. When link confusion such as record order reversal or exceptional timestamps occurs, the system time of the instance may not be synchronized.

<span id=".5pe26Ze05ZCM5q2l5pyN5Yqh"></span>
## Time synchronization service

Generally, you can use the NTP service or the Chrony tool to implement the time synchronization service for the instance.


|Tool |Description |Applicable scenario |Operation guide |
|---|---|---|---|
|NTP service |The NTP service is an implementation of NTP. The NTP server retrieves accurate time from an authoritative time source, while the client sends a time synchronization request to the server. The client then calibrates its own clock incrementally to maintain a low error margin. The entire synchronization process is periodic and progressive. |Applicable to business scenarios where time accuracy is not critical, the network is relatively stable, and compatibility is prioritized. |* [Configuring NTP service for Linux instances (Ubuntu 18)](https://docs.byteplus.com/en/docs/ecs/Configure-the-NTP-service-for-Linux)<br><br>* [Configuring NTP service for Windows instances](https://docs.byteplus.com/en/docs/ecs/Configuring-the-NTP-service-for-Windows) |
|Chrony |Chrony is another implementation of NTP, and its time synchronization algorithm is more advanced. It can quickly estimate the deviation between the local clock and the server clock. By using intelligent filtering technology, it enables the clocks to achieve more accurate synchronization even under unstable network conditions, reducing the number of synchronization rounds required. |Applicable to business scenarios that require high time accuracy, high stability, and adaptability to changes in the network environment. |[Configuring Chrony service for Linux instances (CentOS 7)](https://docs.byteplus.com/en/docs/ecs/Configure-the-Chrony-service-for-Linux) |
