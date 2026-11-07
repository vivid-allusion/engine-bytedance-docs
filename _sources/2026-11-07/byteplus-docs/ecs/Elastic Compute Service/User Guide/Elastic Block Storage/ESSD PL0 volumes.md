---
title: "ESSD PL0 volumes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/esd_pl0_volume"
---

EBS offers ESSD PL0 volumes. This topic provides the use cases and performance details about these volumes.

<span id=".6K6h6LS56K-05piO"></span>
## Billing notes

ESSD PL0 volumes are billed based on their capacity. Billing begins when you create an ESSD PL0 volume. For more information, see [Volume billing](https://docs.byteplus.com/en/docs/ecs/Volume-billing).

<span id=".5LqR55uY5oCn6IO9"></span>
## Volume performance

ESSD PL0 volumes provide only baseline performance and do not support additional performance. Specifically:


|Performance metrics |**Value** |
|---|---|
|Maximum IOPS per volume |10,000 |
|Formula to calculate IOPS per volume |IOPS = min{1,800 + 12 × Capacity (GiB), 10,000} |
|Maximum throughput per volume (MB/s) |180 |
|Formula to calculate throughput per volume |Throughput = min{100 + 0.25 × Capacity (GiB), 180} |
|Average latency of single\-path random writes (block size = 4K) |0.3–0.5 ms |
|Maximum capacity per volume (GiB) |* System volume: 20–2,048<br><br>* Data volume: 10–65,536 |
|Data reliability |99.9999999% (9 nines) |
|API name |ESSD_PL0 |


<span id=".5Yib5bu6RVNTRCBQTDDkupHnm5g="></span>
## Creating an ESSD PL0 volume

EBS lets you create an ESSD PL0 volume as either a system or data volume. Steps:


* Creating an ESSD PL0 system volume

   When creating an instance, set the system volume type to ESSD PL0. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).



&nbsp;

* Creating an ESSD PL0 data volume

   When creating a volume, set the data volume type to ESSD PL0. For more information, see [Creating a volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume). Alternatively, set the data volume type to ESSD PL0 when creating an instance. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e86aee5b2587258a4718656c49c3fd9.png) </span>


&nbsp;

&nbsp;
