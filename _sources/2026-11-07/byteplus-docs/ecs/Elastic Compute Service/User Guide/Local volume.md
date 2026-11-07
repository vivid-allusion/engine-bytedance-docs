---
title: "Local volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Local-volumes"
---

A local volume is a hardware device that is deployed on the physical server (host) where the ECS instance resides. Local volumes function as local storage devices for ECS instances and provide low latency, high IOPS for random reads and writes, high I/O throughput, and high cost\-efficiency. Local volumes are applicable for scenarios that require high I/O capabilities and fast data exchange and processing.

## Considerations

* Local volumes reside on a single physical server where the ECS instance is deployed. The data reliability of a local volume depends on the reliability of the physical server. Therefore, local volumes may introduce single points of failure (SPOFs).

   > **warning**

   > When the physical server of the ECS instance is down or the local volume is damaged, the data stored on the local volume may be lost. Do not store business data that requires long\-term storage on local volumes, and back it up in a timely manner.

   * > We strongly recommend that you use a high\-availability architecture, deploy your services across multiple instances, or use cloud volumes for data backup. These measures ensure high availability of your services and data reliability.

   * > We strongly recommend that you store data that needs to be retained for a long time on volumes.

* The specifications and lifecycle of local volumes are tied to the ECS instances and cannot be purchased separately. Local volumes cannot be separately mounted, unmounted, or scaled up.

* For ECS instances that have local volumes, you can not change the instance type (including vCPU and memory).

## Local volume type

> **tip**

> This topic introduces information about local volumes currently sold with ECS instances. To learn more about instance performance and applicable scenarios, refer to [Instance type overview](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

The following table describes the local volume types and the matching ECS instance type families.

|Local volume type |Matching ECS instance type family |Scenarios |
|---|---|---|
|Local NVMe SSD |Local SSD |Assume that the ECS instance type family is local SSD, local NVMe SSDs are applicable for the following scenarios:<br><br>Business scenarios involving I/O\-intensive applications that feature high\-availability architecture at the application layer, such as relational databases, NoSQL, and Elasticsearch. |
|Local SATA HDD |Big Data |Local SATA HDDs are applicable for big data services involving large\-scale data storage and offline computing tasks, such as EMR. These services are inherently insensitive to latency and can tolerate SPOFs because data redundancy is enabled on the upper layer. |

## Performance of local volume

See the following sections for the performance data of local volumes attached to instances of certain types. You can test the performance of local volumes such as throughput and IOPS by referring to the [Testing local volume performance](https://docs.byteplus.com/en/docs/ecs/Testing-local-volume-performance) document. This way, you can verify the standard performance data provided by the platform.

### Local SSD

The following tables show the performance of local SSDs attached to Local SSD ECS instances.

* **Local SSD i4**

   |NVMe SSD metric |ecs.i4.4xlarge |ecs.i4.8xlarge |ecs.i4.16xlarge |ecs.i4.32xlarge |ecs.i4.64xlarge |
   |---|---|---|---|---|---|
   |Maximum read IOPS (10,000) |320 |640 |1280 |2560 |5120 |
   |Maximum read throughput (GB/s) |14 |28 |56 |112 |224 |
   |Maximum write throughput (GB/s) |8 |16 |32 |64 |128 |

* **Local SSD i4ag**

   |NVMe SSD metric |ecs.i4ag.12xlarge |ecs.i4ag.16xlarge |ecs.i4ag.24xlarge |ecs.i4ag.32xlarge |ecs.i4ag.48xlarge |
   |---|---|---|---|---|---|
   |Maximum read IOPS (10,000) |270 |270 |540 |540 |1,080 |
   |Maximum read throughput (GB/s) |13 |13 |26 |26 |52 |
   |Maximum write throughput (GB/s) |5.5 |5.5 |11 |11 |22 |

* **Local SSD i3s**

   > **tip**

   > To use ecs.i3s.48xlarge, contact your account manager.

   |NVMe SSD metric |ecs.i3s.3xlarge |ecs.i3s.6xlarge |ecs.i3s.12xlarge |ecs.i3s.24xlarge |ecs.i3s.48xlarge |
   |---|---|---|---|---|---|
   |Maximum read IOPS (10,000) |100 |200 |400 |800 |1,600 |
   |Maximum read throughput (GB/s) |6.5 |13 |26 |52 |104 |
   |Maximum write throughput (GB/s) |3.5 |7 |14 |28 |56 |

* **Local SSD i2 (Discontinued)**

   > **tip**

   > Local SSD i2 has been discontinued. We recommend you select Local SSD i4.

   |NVMe SSD metric |ecs.i2.3xlarge |ecs.i2.4xlarge |ecs.i2.8xlarge |ecs.i2.14xlarge |ecs.i2.28xlarge |
   |---|---|---|---|---|---|
   |Maximum read IOPS (10,000) |75 |75 |150 |300 |600 |
   |Maximum read throughput (GB/s) |6.5 |6.5 |13 |26 |52 |
   |Maximum write throughput (GB/s) |3.3 |3.3 |6.6 |13.2 |26.4 |

### Local HDD

The following tables show the performance of local HDDs attached to Big Data instances.

* **Big Data d4c**

   |SATA HDD metric |ecs.d4c.4xlarge |ecs.d4c.7xlarge |* ecs.d4c.14xlarge<br><br>* ecs.d4cd.14xlarge |* ecs.d4c.28xlarge<br><br>* ecs.d4cd.28xlarge |
   |---|---|---|---|---|
   |HDD quantity (volume) |3 |6 |12 |24 |
   |Maximum throughput (MiB/s) |770 |1540 |3080 |6160 |
   |Maximum capacity (TB) |24 |48 |96 |192 |

* **Big Data d4s**

   |SATA HDD metric |ecs.d4s.4xlarge |ecs.d4s.7xlarge |* ecs.d4s.14xlarge<br><br>* ecs.d4sd.14xlarge |* ecs.d4s.28xlarge<br><br>* ecs.d4sd.28xlarge |
   |---|---|---|---|---|
   |HDD quantity (volume) |3 |6 |12 |24 |
   |Maximum throughput (MiB/s) |815 |1630 |3260 |6520 |
   |Maximum HDD capacity (TB) |72 |144 |288 |576 |

## Related documents

* Local volumes are associated with specific instance types and cannot be purchased separately. The local volume cost is included in the instance type cost. For more billing information, refer to [Billing overview](https://docs.byteplus.com/en/docs/ecs/Billing-overview).

* Online replacement of faulty disks is supported. For more information, please refer to [Operation procedure for local volume events](https://docs.byteplus.com/en/docs/ecs/Local-volume-event-auto-maintenance).
