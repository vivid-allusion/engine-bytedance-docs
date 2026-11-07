---
title: "TSSD volumes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume"
---

EBS offers TSSD volumes. This topic provides important notes, use cases, and performance details about TSSD volumes.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


|Category |Considerations |
|---|---|
|Supported instance types |You can attach TSSD volumes to the following instance types:<br><br><br>* X86 Computing: c3il, g3il, r3il, c3al, g3al, r3al, c2a, g2a, r2a, c2i, g2i, r2i, hfc2, hfg2, hfr2, g2ine, d2s, d2c, t2, s2, c1ie, g1ie, r1ie, g4i, g4ie, g4il, g4al, c4i, c4ie, c4il, c4al, r4i, r4ie, r4il, hfg4i, hfc4i, and hfr4i.<br><br>* Elastic Bare Metal (EBM): ebmg4id.<br><br>* Heterogeneous Computing: ecs.gni3cl. |
|Supported regions |Currently, you can create TSSD volumes in the following availability zones:<br><br><br>* China (Beijing) Availability Zone A/C/D<br><br>* China (Shanghai) Availability Zone A/B/C<br><br>* Asia Pacific (Johor) Availability Zone B |
|Unsupported operations |Currently, after you create a TSSD volume, you cannot change its specifications. |
|Extending a volume |The throughput of a TSSD volume is limited by its capacity. When you extend a TSSD volume and the sum of the baseline and additional throughput after expansion exceeds the limit for that capacity, EBS automatically [cancels](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management) the excess provisioned performance.<br><br>For example, you create a TSSD volume with a capacity of 500 GiB and an additional throughput of 100 MB/s. Then, you increase the volume's capacity to 2,000 GiB. Since the baseline throughput for a 2,000 GiB volume is 1,000 MB/s, which is the limit of that capacity, EBS automatically cancels the extra 100 MB/s of throughput. |


<span id=".6K6h6LS56K-05piO"></span>
## Billing notes

You are charged for the capacity and additional performance of TSSD volumes. Specifically:


* Capacity cost: Billing begins when you create a TSSD volume. For more information, see [Volume billing](https://docs.byteplus.com/en/docs/ecs/Volume-billing).

* Additional performance cost: Billing begins when you provision additional performance. For more information, see [Additional performance billing - TSSD TL0 volumes](https://docs.byteplus.com/en/docs/ecs/extra-performance-billing-tssd-tl0-volume).


<span id=".5LqR55uY5oCn6IO9"></span>
## Volume performance

TSSD volumes offer both baseline and additional performance. If the baseline performance does not meet your needs, you can provision additional performance. The formula for calculating volume performance is as follows:

**TSSD performance = Baseline performance + Additional performance**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The minimum capacity for a TSSD volume is 40 GiB.</div>


* <div data-tips="true" data-tips-type="warning">Additional performance is only possible when your TSSD volume capacity is at least 100 GiB.</div>



**Performance metrics**


|**Type** |**Performance metrics** |**Value** |
|---|---|---|
|Baseline performance |Maximum throughput per volume (MB/s) |1,000 MB/s |
||Formula to calculate throughput per volume |min {120 + 0.5 × Capacity (GiB), 1,000} |
||Maximum IOPS per volume |20,000 |
||Formula to calculate IOPS per volume |Min {1,800 + 12 × Capacity (GiB), 20,000} |
||Average latency of single\-path random writes (block size = 4K) |1–2 ms |
||Maximum capacity per volume (GiB) |* System volume: 40–2,048 (GiB)<br><br>* Data volume: 40–65,536 (GiB)<br><br><br>Expansion step size: 1 GiB |
||API name |TSSD_TL0 |
|Additional performance |Configurable maximum throughput (MB/s) |* 100 GiB < Volume capacity ≤ 500 GiB: min {Additional throughput, 2× Volume capacity \- Baseline throughput}<br><br>* Volume capacity \> 500 GiB: min {Additional throughput, 1,000 \- Baseline throughput} |
||Formula to calculate IOPS per volume |Additional throughput (MB/s) × 1,024 / 64 KB |


**Throughput limits**

The throughput of TSSD volumes is determined by their capacity. The maximum throughput for TSSD volumes, which includes baseline and additional performance, is calculated as follows:


|**Volume capacity (GiB)**  |**Maximum throughput (MB/s)**  |
|---|---|
|40 ≤ Capacity < 100 |120 + 0.5 × Capacity (GiB) |
|Capacity ≥ 100 |Min (2 × Capacity (GiB), 1,000) |


The changes in maximum throughput relative to volume capacity are described below:


* You cannot provision additional performance when the volume capacity is between 40 and 100 GiB. In this case, the maximum throughput is the baseline throughput, which increases linearly with capacity at a rate of 0.5 MB/s per GiB.

* When the volume capacity is between 100 and 500 GiB, the maximum throughput increases linearly with capacity at a rate of 2 MB/s per GiB.

* The maximum throughput reaches its limit of 1,000 MB/s once the volume capacity reaches 500 GiB. If the capacity exceeds 500 GiB, the maximum throughput stabilizes at 1,000 MB/s and will not increase further.


The maximum baseline throughput of a volume increases linearly with capacity and cannot be adjusted independently. The baseline throughput reaches its limit of 1,000 MB/s when the capacity reaches 1,760 GiB. Even if the capacity exceeds 1,760 GiB, the baseline throughput remains at 1,000 MB/s.

The maximum additional provisionable throughput is the difference between the volume throughput limit and the maximum baseline throughput. As the volume capacity changes, so does the maximum additional throughput that can be provisioned. When the volume capacity is 1,760 GiB or greater, the maximum baseline throughput is 1,000 MB/s. This hits the volume throughput limit, so you cannot provision additional throughput. The figure below shows the changes in capacity and throughput.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fae01953c0471b8f2083792beade136.png) </span>

&nbsp;

<span id=".5Yib5bu65ZCe5ZCQ5Z6LU1NE5LqR55uY"></span>
## Creating a TSSD volume

EBS lets you create a TSSD volume as either a system or data volume. Steps:


* When creating an instance, set the system volume type to TSSD. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd6ce758f7be4062f8fda933c5957b64.png) </span>



&nbsp;

* When creating a volume, set the data volume type to TSSD. For more information, see [Creating a volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume).

   Alternatively, set the data volume type to TSSD when creating an instance. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7f0e992c34d303debe169965f39ecf5.png) </span>


&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Additional performance is only possible when the volume capacity is at least 100 GiB.</div>


* <div data-tips="true" data-tips-type="warning">The maximum throughput of a TSSD volume (the sum of the baseline and additional performance throughputs) depends on the volume capacity. TSSD volumes with different capacities support different amounts of additional throughput that can be provisioned. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume#.5LqR55uY5oCn6IO9">Volume performance</a>.</div>



**Related operations**


* **View volume details**

   On the Volumes page, click the name of the volume that you want to check. In the "Volume information" section, you can view details such as specifications and additional performance.

* **Adjust additional performance**

   EBS lets you modify the additional performance settings of one or more volumes with identical specifications in a batch. Steps:

   * Modify a single volume: On the Volumes page, click "... \> Adjust extra performance" in the Actions column of the volume that you want to manage. In the box that appears, enter the desired additional performance, and click "Adjust extra performance".

   * Modify multiple volumes: On the Volumes page, check the boxes next to the volumes that you want to manage. The selected volumes must have the same specifications. Next, click "... \> Adjust extra performance" in the lower\-left corner of the page. Finally, set the desired additional performance type and value, and click "Adjust extra performance".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also use the <a href="https://docs.byteplus.com/en/docs/ecs/ModifyVolumeExtraPerformance">ModifyVolumeExtraPerformance</a> API to provision additional performance for TSSD volumes.   </div>
   

* **Cancel additional performance**

   On the Volumes page, click "... \> Adjust extra performance" in the Actions column of the volume that you want to manage. In the box that appears, set the additional performance value to 0, and click "Adjust extra performance".

* **Extend a volume**

   On the Volumes page, click "... \> Extend volume" in the Actions column of the volume that you want to manage. For more information, see [Extending a volume](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux).
