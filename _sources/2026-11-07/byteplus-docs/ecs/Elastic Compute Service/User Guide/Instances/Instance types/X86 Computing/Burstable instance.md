---
title: "Burstable instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Burstable-performance-instances"
---

<span id=".5qaC6L-w"></span>
## Overview

Burstable instances are the only instance type that use CPU credits to ensure CPU utilization. They are suitable for lightweight computing scenarios where CPU utilization is generally low under normal conditions, but higher CPU performance is required during specific periods.

A burstable instance provides baseline CPU performance, which represents the minimum level of performance that the instance can continuously and stably deliver. If an instance's runtime performance falls below the baseline performance, CPU credits will accumulate at a fixed rate. When baseline performance cannot meet actual requirements, accumulated CPU credits are consumed to increase performance above the baseline level, without affecting the environment or applications deployed on the instance. The CPU credits earned or consumed depend on the CPU utilization of the instance:


* If CPU usage is lower than the baseline performance, the points earned will exceed the points consumed, and the CPU points balance will increase.

* If CPU usage equals the benchmark performance, the points earned will be equal to the points consumed, and the CPU points balance will remain unchanged.

* If CPU usage exceeds the baseline performance, the points earned will be less than the points consumed, resulting in a decrease in the CPU points balance.


After the CPU credit balance is depleted, the instance will gradually drop to baseline performance and will not burst above the baseline until it accumulates more credits. Therefore, **burstable instances have an availability SLA guarantee, but no performance SLA guarantee** (that is, their performance cannot be guaranteed under all circumstances), and computing performance may fluctuate and become unstable under high load. If you find that the burstable instance type does not meet or exceed your application requirements, you can modify the instance type at any time to adapt to changes in business scenarios.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To learn about instance types, estimate instance fees, view instance spec modification status, and understand instance naming rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance types and specifications overview</a>.</div>


<span id=".5Z-65pys5qaC5b-1"></span>
## Basic concepts


|Basic concepts |Description |
|---|---|
|Benchmark performance |The minimum sustained and stable CPU performance that an instance can provide is determined by the instance type. For details, see the "Average Baseline CPU Performance" column in the instance type metrics table. |
|Initial CPU points |After you create a burstable instance, you receive a one\-off allocation of CPU credits, which is fixed at 30 credits per vCPU. |
|Point acquisition speed |After an instance is started, it accrues CPU credits at a fixed rate. The rate at which CPU credits are earned is determined by the instance type. For details, refer to the "CPU credits/hour" column in the specification and metric details table. This metric indicates the number of CPU credits that all vCPUs of a single instance can earn per hour. The calculation formula is as follows:<br><br>**CPU credits earned per hour by a single instance = number of vCPUs × baseline performance × 60 minutes**<br><br>For example, for ecs.t2\-c1m2.large (2 vCPUs) with a baseline performance of 20%, the instance earns 24 CPU credits per hour (2 × 60 × 20%). |
|Consume CPU credits |After a burstable instance is started, it immediately begins consuming CPU credits to maintain computing performance. Initial CPU credits are consumed first. Once the initial CPU credits are depleted, they cannot be restored, and only earned CPU credits can be used thereafter.<br><br>The rate at which CPU credits are consumed is related to the burstable instance's number of vCPUs, CPU utilization, and working time. The calculation formula is as follows:<br><br>**CPU credits consumed per hour by a single instance = number of vCPUs × CPU utilization × 60 minutes**<br><br>For example, each of the following three scenarios will consume one CPU credit:<br><br><br>* One vCPU runs at 100% utilization for one minute<br><br>* A vCPU runs at 50% utilization for 2 minutes<br><br>* Two vCPUs operating at 25% utilization for 2 minutes |
|CPU points balance |If a burstable instance earns more CPU credits than it consumes, the excess is accumulated as the CPU credit balance, which can be used to increase CPU utilization above the baseline performance.<br><br>**Points balance equals (points earned minus points spent) when this value is below the baseline.** <br><br>For example, if an ecs.t2\-c1m2.large instance (2 vCPUs) runs at 5% CPU utilization for one hour, which is 20% below the baseline performance, then the instance's points balance per hour = points earned (2 × 60 × 20%) \- points consumed (2 × 60 × 5%) = 18. |
|Maximum CPU points balance |For a specified instance type, the rate at which CPU credits are earned is fixed; therefore, the CPU credit balance has an upper limit. The maximum CPU credit balance is equal to the amount of CPU credits that can be earned by the specified instance type in 24 hours. For details, see the “Maximum CPU Credit Balance” column in the instance type metrics table. |


<span id=".5Lqn5ZOB54m554K5"></span>
## Product features

**Good value for money**

Burstable instances are more cost\-effective than regular instances. Unlike regular instances, which provide fixed CPU resources, burstable instances offer a baseline level of CPU utilization and can temporarily exceed this baseline through a CPU credit mechanism. This ensures that you only pay for the baseline CPU usage, helping to reduce computing costs.

**Predictable performance**

A burstable instance has a performance baseline, that is, a CPU baseline. Compared to Shared instances, it offers a more reliable guarantee of baseline performance. Burst performance is supported, allowing you to estimate the burst performance an instance can provide based on its baseline performance and available CPU credits. You can independently select computing power according to your business needs.

**Highly flexible specifications**

A variety of burstable instance types are available with different processor\-to\-memory ratios, such as 1:1, 1:2, and 1:4. The smallest instance type is ecs.t2\-c2m1.large (2 vCPU, 1 GiB). You can combine instance types more flexibly to meet requirements with finer granularity.

<span id="BuPqqP53"></span>
## Burstable instance t2

**Specifications and features**


|Type |Performance |
|---|---|
|Compute |* Use Intel third\-generation or second\-generation processors:<br><br>   * 3rd Gen Intel<sup>®</sup> Xeon<sup>®</sup> Scalable Processor (Ice Lake): processor base frequency of 2.3 GHz, all\-core turbo frequency of 3.0 GHz<br><br>   * 2nd generation Intel<sup>®</sup> Xeon<sup>®</sup> Scalable processors (Cascade Lake): processor base frequency 2.4 GHz, all\-core turbo frequency 3.1 GHz<br><br>* Support for multiple processor\-to\-memory ratios, such as 1:1, 1:2, and 1:4<br><br>* Maximum supported: 8 vCPUs and 32 GiB |
|Storage |* Supports Enhanced SSD volumes and TSSD volumes. You can mount up to four volumes (including one system volume).<br><br>* Storage I/O performance is related to computing specifications; the higher the specifications, the better the performance. |
|Network |* Maximum throughput: 400,000 PPS<br><br>* Network performance depends on computing specifications; the higher the specifications, the better the performance. |


**Scenarios**

Burstable instances are suitable for scenarios where CPU usage remains very low most of the time but occasionally experiences a sudden spike in CPU usage. For example:


* Web application server

* Light\-load applications and microservices

* Develop, test, and stress test service applications


**Specification and metric details**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Due to differences in business scenarios, maximum throughput (PPS) can vary significantly. Therefore, it is recommended that you conduct a business stress test to understand the performance of the instance, so that you can select the appropriate instance type.</div>



|Instance type |vCPU |Memory (GiB) |Average benchmark CPU computing performance |Initial points |CPU points per hour |Maximum CPU points balance |Outbound and inbound network bandwidth capacity (Gbit/s) |Maximum throughput (inbound + outbound) (10,000 PPS) |Number of connections (in ten thousands) |Maximum queues per network interface |elastic network interface (including a primary network interface) |Private IP of a single network interface |Volume IOPS (×10,000) |Volume bandwidth (Gbit/s) |Number of volumes (including one system volume) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ecs.t2\-c2m1.large |2 |1 |10% |60 |12 |288 |1 |10 |4 |1 |2 |2 |1 |1 |4 |
|ecs.t2\-c1m1.large |2 |2 |20% |60 |24 |576 |1 |10 |4 |1 |2 |2 |1 |1 |4 |
|ecs.t2\-c1m2.large |2 |4 |20% |60 |24 |576 |1 |10 |4 |1 |2 |2 |1 |1 |4 |
|ecs.t2\-c1m4.large |2 |8 |30% |60 |36 |864 |1 |10 |6 |1 |2 |2 |1 |1 |4 |
|ecs.t2\-c1m4.xlarge |4 |16 |40% |120 |96 |2304 |2 |20 |12 |1 |2 |6 |2 |2 |4 |
|ecs.t2\-c1m4.2xlarge |8 |32 |40% |240 |192 |4608 |4 |40 |24 |1 |2 |6 |3 |3 |4 |


<span id="bXFJrtHH"></span>
## Example of CPU points calculation

The CPU credits of a burstable instance fluctuate based on the relationship between CPU utilization and baseline performance. The following diagram uses ecs.t2\-c1m2.large as an example to illustrate changes in the CPU credit balance. Basic information for ecs.t2\-c1m2.large can be found in the specification metric details and is summarized as follows:


* vCPU：2

* Baseline performance: 20%

* Initial points: 60

* Points earned per hour: 24

* Maximum points balance: 576


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The examples in this document are designed solely to illustrate concepts such as CPU performance and CPU points. They are for reference only and cannot be fully equated to actual conditions. Real\-world business scenarios are more complex and variable, and CPU usage fluctuates continuously.</div>


* <div data-tips="true" data-tips-type="warning">CPU usage refers to out\-of\-band CPU usage collected at the physical machine level. You can view CPU usage and CPU credit data on the <strong>Basic monitoring</strong> tab of the instance details page. <a href="https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data">Learn more</a>.</div>



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ccc825b0bccb4c268068b7687843661e.png) </span>

The following explains the reasons for changes in CPU points at each stage in the diagram.


* P1 (0–24 hours): After instance creation, a one\-off award of 60 initial points is granted. During this stage, CPU usage is zero and it is in an idle status. Points will continue to accumulate, and the accumulated points will exceed the points that can be earned within 24 hours.

   At the end of this stage, the CPU points balance = initial CPU points (60) + maximum CPU points balance (576) = 636

   > In real\-world scenarios, an instance consumes a small amount of points when it starts and runs, and the CPU point balance will not reach the maximum theoretical value shown in this example.   
   

   * P2 (25–36 hours): Initial points are consumed first. Once the initial points are depleted, they will not be restored. During this phase, when CPU utilization is less than or equal to 20% of the baseline performance, the instance earns more credits than it consumes. However, after the initial credits are depleted, the CPU credit balance cannot exceed its maximum value of 576; any credits beyond this limit will be discarded.

   At the end, the CPU points balance is equal to the CPU points balance for P1 at the end (636) minus the initial points consumed (60), which equals 576.

* P3 (37–48 hours): Operated at 30% CPU utilization for 12 hours. Baseline performance was insufficient to meet requirements, so the system began consuming the CPU credit balance, using 36 credits per hour and earning 24 credits per hour.

   At the end, the CPU points balance = CPU points balance at the end of P2 (576) – points consumed (36 × 12) + points earned (24 × 12) = 432

* P4 (49–52 hours): CPU utilization is 90%. The instance runs for 4 hours, consuming 108 points per hour.

   At the end, the CPU points balance = CPU points balance at the end of P3 (432) \- points consumed (108 \* 4) + points earned (24 \* 4) = 96

* P5 (53–54 hours): CPU utilization is 60%, the instance runs for 2 hours, and consumes 72 points per hour.

   At the end, the CPU points balance = CPU points balance of P4 at the end (96) – points consumed (72 × 2) + points earned (24 × 2) = 0

   > When the CPU credit balance is low, the instance's performance will gradually decrease to the baseline performance level. This ensures that, after the CPU credit balance is depleted, the instance's performance does not drop sharply. When the CPU credit balance is depleted and no CPU credits are available, the instance cannot exceed baseline performance.   
   

   * P6 (55–60 hours): The CPU operated at baseline performance for 6 hours. The points consumed were equal to the points earned, so the CPU points balance remained unchanged.

   At the end, the CPU points balance is calculated as P5's CPU points balance at the end (0) minus the points consumed (24 × 6) plus the points earned (24 × 6), resulting in 0.

   * P7 (61–72 hours): The instance remains idle for 12 hours, earning 24 points per hour with no consumption, and begins accumulating points.

   At the end, the CPU points balance is the CPU points balance at the end of P6 (0) plus the points earned (24 \* 12), totaling 288.

   <span id=".5a6e5L6L5YGc5py65a-5Q1BV56ev5YiG55qE5b2x5ZON"></span>
   ## Impact of instance shutdown on CPU credits


|**Shutdown methods** |**Changes in CPU points** |
|---|---|
|[Keep Charging](https://docs.byteplus.com/en/docs/ecs/Stopping-instances#.5YGc5q2i5qih5byP) |The current CPU points balance will be retained, and you will continue to earn CPU points. |
|[Stop Charging](https://docs.byteplus.com/en/docs/ecs/Stopping-instances#.5YGc5q2i5qih5byP) |The current CPU points balance will be retained, but no further CPU points will be earned. Only pay\-as\-you\-go instances support Economical Mode. [Learn more](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances). |
|[Service suspension after overdue payment](https://docs.byteplus.com/en/docs/ecs/Arrears) |The current CPU points balance will be retained for 15 days, but no additional CPU points will be earned. If you recharge and settle the bill before forced resource reclaim, you can continue to earn CPU points. |
|[Stop the service after expiration](https://docs.byteplus.com/en/docs/ecs/Expiration) |The current CPU points balance will be retained for 15 days, but no additional CPU points will be accrued. If you promptly complete the renewal and restart the machine within 15 days after expiration, you will continue to receive CPU credits. |


<span id=".Q1BV56ev5YiG6K6h566X56S65L6L"></span>
## 

&nbsp;

&nbsp;
