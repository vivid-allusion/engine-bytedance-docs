---
title: "Region and availability zone"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Regions-and-Availability-Zones"
---

## Regions and availability zones

When creating a scaling group, you are required to select the region and availability zone. The scaling group only supports managing cloud resources in the same region and availability zone. After being selected, the region and availability zone cannot be changed.

## Region

#### Overview

Region refers to a geographic area where physical data centers are located. Typically, regions are divided by the city where the data centers reside.

#### Notes

* Private networks between different regions are completely isolated, which ensures maximum stability and fault tolerance across regions.

* Resources in different regions can mutually connect through Elastic IP Address (EIP). Private networks in different regions can mutually connect through Cloud Enterprise Network (CEN).

#### How to select a region?

|Consideration |Selection suggestion |
|---|---|
|Geographical area |For good download performance and short latency, we recommend that you select a region closest to your desired service when you buy an ECS instance. Note that once you have paid for an instance, you can not change the region. |
|Private network connectivity |If isolating VPCs is required, deploy VPCs in different regions. If connecting VPCs is required, deploy VPCs in the same region. |
|Resource price |Resource prices may vary based on regions. When selecting a region, please refer to the prices listed on the purchase page and consider your budget. |

## Availability zone

#### Overview

Availability zones (AZs) are physical areas that use separate power sources and networks in a region.

#### Notes

* Within the same region and VPC, different AZs interconnect over the private network.

* Availability Zones are fault\-isolated, meaning a failure in one AZ does not impact the normal operation of others, ensuring your business remains continuously online.

#### How to select an availability zone?

* If your services require disaster recovery, we recommend that you deploy resources in different availability zones of a region.

* If low latency between your services is required, we recommend that you deploy resources in the same availability zone.

* After the resource is purchased, the availability zone cannot be changed.

## Regions and availability zones​

> **tip**

> The regions available for different products may vary. Please refer to the regions actually supported by each product.

|Region |City |Number of AZs |RegionID |ZoneID |Release status |
|---|---|---|---|---|---|
|**Regions in China** ||||||
|China (Beijing) |Beijing |4 |cn\-beijing |* Availability zone A: cn\-beijing\-a<br><br>* Availability zone B: cn\-beijing\-b<br><br>* Availability zone C: cn\-beijing\-c<br><br>* Availability zone D: cn\-beijing\-d |GA |
|China (Shanghai) |Shanghai |3 |cn\-shanghai |* Availability zone A: cn\-shanghai\-a<br><br>* Availability zone B: cn\-shanghai\-b<br><br>* Availability zone C: cn\-shanghai\-c<br><br>* Availability zone E: cn\-shanghai\-e |GA |
|China (Guangzhou) |Guangzhou |3 |cn\-guangzhou |* Availability zone A: cn\-guangzhou\-a<br><br>* Availability zone B: cn\-guangzhou\-b<br><br>* Availability zone C: cn\-guangzhou\-c |GA |
|China (Hong Kong) ||2 |cn\-hongkong |* Availability zone A: cn\-hongkong\-a<br><br>* Availability zone B: cn\-hongkong\-b<br><br>* Availability zone C: cn\-hongkong\-c |GA |
|**Regions in other countries** ||||||
|Asia Pacific |Johor |2 |ap\-southeast\-1 |* Availability zone A: ap\-southeast\-1a<br><br>* Availability zone B: ap\-southeast\-1b |GA |
|Asia Pacific |Jakarta |2 |ap\-southeast\-3 |* Availability zone A: ap\-southeast\-3a<br><br>* Availability zone B: ap\-southeast\-3b<br><br>* Availability zone C: ap\-southeast\-3c |GA |
