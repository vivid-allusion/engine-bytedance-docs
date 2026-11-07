---
title: "Storage types"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Storage_type"
---

Document Database for MongoDB provides two storage types, ESSD FlexPL volumes (hereinafter referred to as "FlexPL volumes") and Local SSDs (hereinafter referred to as "local disks"). This topic introduces the architectural features, performance comparison, and applicable scenarios of these two storage types, helping you make the optimal choice based on your business needs.

## Overview

* **FlexPL volume**

   Based on a distributed storage architecture, compute and storage are separated. It supports independent and elastic configuration changes for compute and storage resources. For more information on FlexPL volume performance metrics, refer to [ESSD FlexPL volumes](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume?lang=en).

   To use FlexPL volumes, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.

* **Local disk**

   Data is stored directly on the host's local disk, resulting in low I/O latency.

The main differences between the two storage types are as follows.

|**Comparison dimensions** |**FlexPL volume** |**Local disk** |
|---|---|---|
|Storage architecture |Decoupled compute and storage |Integrated compute and storage |
|Elastic expansion |Supports and completes in minutes |May involve data migration, with time taken correlating to data volume |
|Configuration flexibility |Storage space can be expanded independently |Expansion requires simultaneous adjustment of compute resources |
|Expansion impact |Configuration changes may cause 1 to 2 temporary disconnections |Configuration changes may cause 1 to 2 temporary disconnections |
|I/O Latency |Average random write latency within 0.2 ms in some availability zones |Lower than volumes |
|Performance features |Significant advantages in read\-intensive scenarios |More suitable for high\-throughput write scenarios (\>350 MiB/s) |
|Applicable scenarios |Read\-write mixed scenarios such as high\-concurrency internet applications, e\-commerce, gaming, and social media |Scenarios such as log collection, data batch import, and financial transactions |

You can view the instance's **Storage type** in the **Configuration** area of the **Instance information** tab on the [MongoDB console](https://console.byteplus.com/db/mongodb).

## Performance comparison

* Read\-intensive scenarios

   FlexPL volumes outperform local disks in high\-concurrency scenarios, **with the advantage becoming more pronounced as the proportion of read operations increases**.

* Write\-intensive scenarios

   Both perform relatively well, with volumes being slightly better.

* High\-throughput write scenarios (sustained bandwidth \> 350 MiB/s)

   Local disk data is stored on the local hard drive, and read/write operations do not require network links, offering a **significant latency advantage**. Local disks are recommended for this scenario.

## Selection recommendations

* For most business scenarios, FlexPL volumes are recommended for their superior overall performance.

* Local disks are only recommended for high\-throughput write scenarios where disk bandwidth consistently exceeds 350 MiB/s, or for businesses with extreme I/O latency requirements (e.g., financial transactions).

**Key takeaway**: For mixed read/write operations, choose volumes. For high\-throughput writes, choose local disks.
