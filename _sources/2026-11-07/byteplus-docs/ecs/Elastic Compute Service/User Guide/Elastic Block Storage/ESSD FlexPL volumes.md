---
title: "ESSD FlexPL volumes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume"
---

EBS offers ESSD FlexPL volumes. This topic provides the use cases and performance details about these volumes.

<span id=".6K6h6LS56K-05piO"></span>
## Billing notes

You are charged for the capacity, additional performance, and burst performance of your ESSD FlexPL volumes. Specifically:


* Capacity cost: Billing begins when you create an ESSD FlexPL volume. For more information, see [Volume billing](https://docs.byteplus.com/en/docs/ecs/Volume-billing).

* Additional performance cost: Billing begins when you provision additional performance. For more information, see [Additional performance billing - ESSD FlexPL volumes](https://docs.byteplus.com/en/docs/ecs/Extra-performance-of-volume-billing).


<span id=".5LqR55uY5oCn6IO9"></span>
## Volume performance

ESSD FlexPL volumes offer baseline, additional and burst performance. If the baseline performance does not meet your needs, you can provision additional or burst performance. The formula for calculating volume performance is as follows:

**ESSD FlexPL volume performance = Baseline performance + Additional performance + Burst performance**

<span id="sczUWYP8"></span>
### Total performance


|**Performance metric** |Value |
|---|---|
|Maximum IOPS per volume<br><br> |Min{1,000 × Capacity (GiB), 200,000}<br><br> |
|Maximum throughput per volume (MB/s) |Min{Actual IOPS × 16 KB ÷ 1,024, 2,000} |
|Average latency of single\-path random writes (block size = 4K) |The average random write latency for newly created ESSD FlexPL volumes is 0.2 ms in some availability zones and 0.3 to 0.5 ms in others. For more information, see the **Latency** section below. |
|Maximum capacity per volume (GiB) |* System volume: 20–2,048<br><br>* Data volume: 10–65,536 |
|Promised data reliability |99.9999999% (9 nines) |
|API name |ESSD_FlexPL |


<span id="aoEayUv2"></span>
### Baseline performance

Baseline performance is built into the volume and is not customizable. For FlexPL ESSD volumes, baseline performance increases with capacity until it reaches the volume type's limit. Specifically:


|**Performance metric** |Value |
|---|---|
|Maximum IOPS per volume |50,000 |
|Formula to calculate IOPS per volume |IOPS = min{1,800 + 50 × Capacity (GiB), 50,000} |
|Maximum throughput per volume (MB/s) |350 |
|Formula to calculate throughput per volume |Throughput = min{120 + 0.5 × Capacity (GiB), 350} |
|Average latency of single\-path random writes (block size = 4K) |The average random write latency for newly created ESSD FlexPL volumes is 0.2 ms in some availability zones and 0.3 to 0.5 ms in others. For more information, see the **Latency** section below. |
|Maximum capacity per volume (GiB) |* System volume: 20–2,048<br><br>* Data volume: 10–65,536 |
|Promised data reliability |99.9999999% (9 nines) |
|API name |ESSD_FlexPL |


**Latency**

Starting November 1, 2025, the average random write latency for newly created ESSD FlexPL volumes in certain availability zones will be within 0.2 ms by default. The average random write latency for existing ESSD FlexPL volumes and volumes changed from ESSD PL0 to ESSD FlexPL remains 0.3 to 0.5 ms. The availability zones that support 0.2 ms latency are as follows:


* China (Beijing) Availability Zone A/B/C/D/E.

* China (Shanghai) Availability Zone A/B.

* Asia Pacific (Johor) Availability Zone A/B.


<span id=".6aKd5aSW5oCn6IO9"></span>
### Additional performance

EBS lets you provision additional performance for ESSD FlexPL volumes. You can increase the performance of a volume without increasing its capacity. There are three types of additional performance that you can provision:


* **Balanced type**: You can provision additional IOPS for your volume. The provisionable range is 1 to 50,000 IOPS. For every IOPS added, the throughput increases by 8 KB/s. This option is ideal for workloads with high IOPS and throughput demands.

* **IOPS type**: You can provision additional IOPS for your volume. The provisionable range is 1 to 50,000 IOPS. For every IOPS added, the throughput increases by 4 KB/s. This option is ideal for IOPS‑intensive workloads, such as OLTP databases.

* **Throughput type**: You can provision additional throughput for your volume. The provisionable range is 1 to 650 MB/s. For every 1 MB/s added, the IOPS increases by 16. This option is ideal for throughput\-intensive workloads such as video offloading, transcoding, machine learning, media rendering, log storage, and large\-scale offline data processing.


Specifically:


|**Performance metric** |**Balanced type** |**IOPS type** |**Throughput type** |
|---|---|---|---|
|Maximum additional IOPS per volume |50,000 |50,000 |10,400 |
|Formula to calculate additional IOPS per volume |Min{Provisioned additional IOPS, 50,000} |Min{Provisioned additional IOPS, 50,000} |Provisioned additional throughput \* 16 |
|Maximum additional throughput per volume (MB/s) |390 |195 |650 |
|Formula to calculate additional throughput per volume (MB/s) |Min{Provisioned additional IOPS \* 8 KB / 1,024, 390} |Min{Provisioned additional IOPS \* 4 KB / 1,024, 195} |min{Provisioned additional throughput, 650} |
|API name |Balance |IOPS |Throughput |


<span id=".5Yib5bu6IEVTU0QgRmxleFBMIOS6keebmA=="></span>
### Burst performance

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Burst performance is currently in closed beta. Please contact your account manager for access.</div>


* <div data-tips="true" data-tips-type="default">Burst performance is essentially additional performance provided based on the available resources. It depends on the current load of the cluster in which the volume resides. Burst performance is not guaranteed and may fail if the system is overloaded.</div>



This feature allows for dynamic performance adjustments based on workloads and does not require pre\-configuration. When enabled for a volume, burst performance provides extra capacity when baseline and additional performance are insufficient. It increases IOPS or throughput within performance limits to handle short\-term traffic spikes. Burst performance automatically scales down when the workload returns to normal levels. This is suitable for burst workloads or scenarios that require processing large amounts of data in a short time. The formula for calculating burst performance is as follows:


* **Burst IOPS for a given volume = Actual IOPS − Baseline IOPS − Additional IOPS**

* **Burst throughput for a given volume (MB/s) = Actual throughput − Baseline throughput − Additional throughput**


<span id="jUio1aFm"></span>
## Creating an ESSD FlexPL volume

EBS lets you create an ESSD FlexPL volume as either a system or data volume. Steps:


* Creating an ESSD FlexPL system volume

   When creating an instance, set the system volume type to "ESSD" with a performance level of "FlexPL (basic IOPS limit for one volume: 50,000)". If your volume has a capacity of 500 GiB or more, you can provision additional performance by dragging the horizontal scroll bar to the far right and selecting "Extra performance". For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3362e18ec4f23668720829c42d5baf1e.png) </span>



&nbsp;

* Creating an ESSD FlexPL data volume

   * When creating an instance, set the data volume type to "ESSD" with a performance level of "FlexPL (basic IOPS limit for one volume: 50,000)". If your volume has a capacity of 500 GiB or more, you can provision additional performance by dragging the horizontal scroll bar to the far right and selecting "Extra performance". For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * Alternatively, set the data volume type to ESSD FlexPL when creating a volume. For more information, see [Creating a volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume).

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Description   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Additional performance is available only if your ESSD FlexPL volume is at least 500 GiB.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only select one additional performance type for each volume. If necessary, you can change the type of additional performance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you delete a volume, the additional performance configuration is also deleted.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9523343e444ddf360c3c6fb98a55283.png) </span>


&nbsp;

<span id="ZyL9pTy1"></span>
## **Related operations**


* **View volume details**

   On the "Volumes" page, click the name of the volume that you want to check. In the "Volume information" section, you can view details such as specifications, additional performance and burst performance.

* **Additional performance**

   * **Provision additional performance for your volume**

      On the "Volumes" page, click "... \> Adjust extra performance" in the "Actions" column of the volume that you want to manage. In the box that appears, set the desired additional performance type and value, and click "Adjust extra performance".

   * **Adjust additional performance**

      On the "Volumes" page, click "... \> Adjust extra performance" in the "Actions" column of the volume that you want to manage. In the box that appears, modify the additional performance type and value, and click "Adjust extra performance".

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When you modify additional performance, its billing changes immediately. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Extra-performance-of-volume-billing">Additional performance billing</a>.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also use the <code>ModifyVolumeExtraPerformance</code> API to provision additional performance for ESSD FlexPL volumes. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/ModifyVolumeExtraPerformance">ModifyVolumeExtraPerformance</a>.      </div>
      

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can only adjust the additional performance when the volume is in the Available, Attaching, Attached, Detaching, Snapshotting, or Rolling Back state.      </div>
      

   * **Cancel additional performance**

      On the "Volumes" page, click "... \> Adjust extra performance" in the "Actions" column of the volume that you want to manage. In the box that appears, set the additional performance value to 0, and click "Adjust extra performance".

* **Burst performance**

   * **Enable burst performance**

      * When creating a volume, select the "Enable performance burst" option. Under "Order details", check the box that says "I have read and agree to Elastic Compute Service Terms of Service", and click "Create volume" to submit your order.

      * You can also enable burst performance for an existing volume. On the "Volumes" page, click "... \> Modify attributes" in the "Actions" column of the volume. In the "Modify volume attributes" dialog, select "Enable performance burst", and click "Save".

   * **Disable burst performance**

      On the "Volumes" page, click "... \> Modify attributes" in the "Actions" column of the volume that you want to manage. In the "Modify volume attributes" dialog, deselect "Enable performance burst", and click "Save".
