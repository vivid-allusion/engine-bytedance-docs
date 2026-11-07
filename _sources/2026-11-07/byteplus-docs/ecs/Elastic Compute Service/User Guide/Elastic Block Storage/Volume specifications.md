---
title: "Volume specifications"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Volume-specifications"
---

EBS currently offers ESSD and TSSD volumes. This topic describes the performance metrics and baseline performance of these volumes to help you quickly understand how they perform.

<span id=".5LqR55uY5oCn6IO9"></span>
## Volume performance

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">PTSSD volumes have been discontinued. You can continue using your existing volumes, but you cannot create new ones.</div>


* <div data-tips="true" data-tips-type="warning">The maximum IOPS and maximum throughput values represent the sum of read and write operations. For example, maximum IOPS equals read IOPS plus write IOPS.</div>


* <div data-tips="true" data-tips-type="warning">Burst performance is currently in closed beta. Please contact your account manager for access.</div>




|**Performance metric** |**ESSD** ||**TSSD TL0** |**PTSSD (discontinued)**  |
|---|---|---|---|---|
||**FlexPL** |**PL0** |||
|Maximum IOPS per volume |200,000 |10,000 |20,000 |30,000 |
|Formula to calculate IOPS |* Baseline performance: IOPS = min{1,800 + 50 × Capacity (GiB), 50,000}<br><br>* Additional performance: Three types of additional performance are available. For more information, see [Volume type - ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).<br><br>* Burst performance: Actual IOPS \- Baseline IOPS \- Additional IOPS. For more information, see [Volume type - ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume). |IOPS = min{1,800 + 12 × Capacity (GiB), 10,000} |* Baseline performance: IOPS = min{1,800 + 12 × Capacity (GiB), 20,000}<br><br>* Additional performance: Additional IOPS = Additional throughput (MB/s) × 1,024 / 64 KB |Not applicable. |
|Maximum throughput per volume (MB/s) |2,000 |180 |1,000 |350 |
|Formula to calculate throughput |* Baseline performance: Throughput = min{120 + 0.5 × Capacity (GiB), 350}<br><br>* Additional performance: Three types of additional performance are available. For more information, see [Volume type - ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).<br><br>* Burst performance: Actual throughput \- Baseline throughput \- Additional throughput. For more information, see [Volume type - ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume). |Throughput = min{100 + 0.25 × Capacity (GiB), 180} |* Baseline performance: Throughput = min {120 + 0.5 × Capacity (GiB), 1,000}<br><br>* Additional performance: Only one type of additional performance is available. For more information, see [Volume type - TSSD](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume). |Not applicable. |
|Average latency of single\-path random writes (block size = 4K) |The average random write latency for newly created ESSD_FlexPL volumes is 0.2 ms in some availability zones and 0.3 to 0.5 ms in others. For more information, see [Latency](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume). |0.3–0.5 ms |1–2 ms |0.3–0.5 ms |
|Maximum capacity per volume (GiB) |* System volume: 20–2,048<br><br>* Data volume: 10–65,536 |* System volume: 20–2,048<br><br>* Data volume: 10–65,536 |* System volume: 40–2,048<br><br>* Data volume: 40–65,536 |* System volume: 40–500<br><br>* Data volume: 20–8,192 |
|Promised data reliability |99.9999999% (9 nines) |99.9999999% (9 nines) |99.9999999% (9 nines) |99.99999% (7 nines) |
|API name |ESSD_FlexPL |ESSD_PL0 |TSSD_TL0 |PTSSD |


<span id=".5bqU55So5Zy65pmv"></span>
## Use cases


|**Type** |Characteristics and u**se cases** |
|---|---|
|ESSD FlexPL |* Characteristics: High throughput, high IOPS, and low latency, with multiple additional performance options. Resource provisioning is flexible, as you can provision performance and capacity separately.<br><br>* Use cases: Ideal for I/O\-intensive workloads, such as large\-scale databases and NewSQL databases. |
|ESSD PL0 |* Characteristics: Balanced IOPS and throughput, low latency, and cost‑effective.<br><br>* Use cases: Ideal for workloads requiring moderate I/O performance, such as small to medium\-sized databases. |
|TSSD TL0 |* Characteristics: High throughput, moderate IOPS, and latency\-insensitive. Up to an additional 1,000 MB/s throughput can be provisioned for this type of volume.<br><br>* Use cases: Ideal for workloads requiring high bandwidth and not sensitive to latency. Examples include offline big data processing, training large AI models, processing large batches of log data, and transferring or streaming HD video content. |


<span id=".55u45YWz5paH5qGj"></span>
## Performance optimization

<span id="hYJIj5rE"></span>
### Troubleshooting slow read/write speeds and high I/O on volumes

You can use the ECS console to view various monitoring metrics of your volumes and determine whether their performance meets your business requirements. For more information, see [Viewing basic monitoring data/operating system monitoring data](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data). If you notice that a volume has slow read/write speeds or high I/O usage, follow these troubleshooting steps:


1. Check whether your volume is billed on a pay\-as\-you\-go basis. If so, and if your account has an outstanding balance, your volume I/O performance will be restricted. It will return to normal once you recharge your account and settle the outstanding balance.

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If your account falls behind by 2 hours, the volume service will be suspended. 15 days and 2 hours later, the system will release your volume resources and permanently delete all your data, which cannot be recovered.   </div>
   

2. Check for programs that are consuming high IOPS based on your operating system. For instructions, see [Troubleshooting and solution for high disk load of ECS instance with Linux system](https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_solution_for_high_disk_load_issues_on_Linux_system_ECS_instances) and [Troubleshooting and solution for high disk load of ECS instance with Windows system](https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_Solution_for_High-Disk_Load_Issues_on_Windows_System_ECS_Instances).

3. If the volume performance does not meet your business requirements, we recommend extending the volume or provisioning additional performance. For more information, see [Improving volume performance](https://docs.byteplus.com/en/docs/ecs/Volume-specifications?lang=en#tjhrxcIt).


<span id="tjhrxcIt"></span>
### Improving volume performance

To keep your business running smoothly, you can check if your volume performs as expected using FIO. For more information, see [Testing storage performance](https://docs.byteplus.com/en/docs/ecs/Testing-storage-performance). If the actual performance does not meet your business requirements, you can use the following methods to improve it.


|Method |Use cases |Related documentation |
|---|---|---|
|Change the type of your volume |If you are using an ESSD PL0 volume, you can switch to an ESSD FlexPL volume to meet growing performance needs. This method is useful when your business experiences significant growth and has strict performance requirements for its volumes. |[Modifying volume type](https://docs.byteplus.com/en/docs/ecs/Modify-volume-type) |
|Provision additional performance for your volume |You can provision additional performance for an ESSD FlexPL or a TSSD TL0 volume. This method offers on\-demand usage and flexibility and is ideal for scenarios with fluctuating storage performance needs. |* [ESSD FlexPL volumes](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume)<br><br>* [TSSD volumes](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume) |
|Enable burst performance |You can enable burst performance for an ESSD FlexPL volume. This feature temporarily increases IOPS or throughput within performance limits in order to handle short\-term traffic spikes. Burst performance automatically scales down when the workload returns to normal levels. This is suitable for burst workloads or scenarios that require processing large amounts of data in a short time. |[ESSD FlexPL volumes](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume) |
|Extend your volume |Volume performance increases with capacity. If you encounter an I/O bottleneck due to business growth, and the volume is low on storage space but has not yet reached its performance limit, consider extending the volume to improve performance. |[Extending a volume](https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume) |


<span id="m8GfFZei"></span>
### Relationship between instance specifications and volume performance

A volume's performance depends on the specifications of the ECS instance to which it is attached. Different ECS instances have different maximum performance limits for volumes. Higher instance specification tiers support higher limits. For a detailed introduction to the maximum volume performance supported by ECS instance specifications, see [X86 Computing](https://docs.byteplus.com/en/docs/ecs/X86_computing). In real use cases, however, a volume may perform below its maximum due to these limits.


* Scenario 1: The final storage performance is determined by the performance of the volumes themselves if the total performance of the volumes does not exceed the maximum limit supported by the ECS instance.

   For example, an ecs.g4i.4xlarge instance supports up to 80,000 IOPS and 5 Gbit/s of throughput. This instance has one attached ESSD FlexPL volume with a capacity of 1,000 GiB. This volume has a maximum of 50,000 IOPS and a maximum throughput of 2.8 Gbit/s. Since the total volume performance does not exceed the maximum supported by the ECS instance, the final storage performance is determined by the volume's performance. Therefore, the volume's achievable performance limit is 50,000 IOPS and 2.8 Gbit/s throughput.

* Scenario 2: If the total performance of the volumes exceeds the maximum supported by the ECS instance, the final storage performance is capped at that limit. When multiple volumes are attached to an instance, the system dynamically allocates performance based on a resource contention mechanism.

   For example, an ecs.g4i.4xlarge instance supports up to 80,000 IOPS and 5 Gbit/s of throughput. Three ESSD FlexPL volumes, each with a capacity of 1,000 GiB, are attached to this instance. Each volume supports a maximum of 50,000 IOPS and 2.8 Gbit/s of throughput. The total performance of the three volumes is a maximum of 150,000 IOPS and 8.4 Gbit/s of throughput. If the workload I/O or throughput of the three volumes simultaneously reaches its performance limit, the instance’s processing capacity limits the overall actual performance. Consequently, the combined performance of the three volumes is capped at 80,000 IOPS and 5 Gbit/s throughput. The system dynamically allocates the performance of each volume based on a resource contention mechanism.


To maximize volume performance and prevent waste, select an instance whose specifications match those of your volumes.

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [Volume type - ESSD PL0](https://docs.byteplus.com/en/docs/ecs/esd_pl0_volume)

* [Volume type - ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume)

* [Volume type - TSSD](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume)
