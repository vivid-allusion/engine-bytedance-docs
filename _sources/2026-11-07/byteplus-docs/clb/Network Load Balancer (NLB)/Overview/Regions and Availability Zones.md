---
title: "Regions and Availability Zones"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Regions-and-availability-zones"
---

## Regions

#### Introduction​

A region refers to a distinct geographic area where physical data centers are located, typically divided based on the city in which the data center resides.

#### Related features

* Private networks between different regions are completely isolated, ensuring maximum stability and fault tolerance across regions.

* You can either use Elastic IP Addresses (EIP) for public interconnectivity across regions, or leverage Cloud Enterprise Network (CEN) for private interconnection.

#### How to select a region?

|Considerations |Recommended solution |
|---|---|
|Geographic location |To minimize access latency and optimize download speed, create your cloud resources in the region closest to your target service. Once provisioned, the region cannot be modified. |
|Private network connectivity |If isolating private networks is required, deploy them in different regions. If connecting private networks is required, deploy them in the same region. |
|Resource pricing |Resource prices vary by region. Please select based on your budget and the reference price on the purchase page. |

## Availability zone

#### Introduction​

An Availability Zone (AZ) refers to a physically isolated location within the same region, featuring independent power and network infrastructure.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dca3ce456b73a87b20fddd585204925c.png)

#### Related features

* Within the same region and VPC, different AZs interconnect over the private network.

* Availability Zones are fault\-isolated, meaning a failure in one AZ does not impact the normal operation of others, ensuring your business remains continuously online.

#### How to select an availability zone

* To ensure disaster recovery capabilities for your services, we recommend deploying them across different Availability Zones within the same region.

* If your services require lower latency, we recommend deploying them within the same Availability Zone.

## Regions and Availability Zones

The currently available Regions and Availability Zones are listed in the table below. We will gradually add more Regions and Availability Zones for your selection and use.

> **warning**

> Product features may vary by Region. The features available in the console shall prevail.

|Regions |RegionID |AZ Quantity |ZoneID |
|---|---|---|---|
|**China regions** ||||
|China (Beijing) |cn\-beijing |4 |* AZ A: cn\-beijing\-a<br><br>* AZ B: cn\-beijing\-b<br><br>* AZ C: cn\-beijing\-c<br><br>* AZ D: cn\-beijing\-d |
|China (Shanghai) |cn\-shanghai |4 |* AZ A: cn\-shanghai\-a<br><br>* AZ B: cn\-shanghai\-b<br><br>* AZ C: cn\-shanghai\-c<br><br>* AZ E: cn\-shanghai\-e |
|China (Guangzhou) |cn\-guangzhou |2 |* AZ B: cn\-guangzhou\-b<br><br>* AZ C: cn\-guangzhou\-c |
|China (Hong Kong) |cn\-hongkong |2 |* AZ A: cn\-hongkong\-a<br><br>* AZ B: cn\-hongkong\-b |
|**Other countries and regions** ||||
|Asia Pacific (Johor) |ap\-southeast\-1 |2 |* AZ A: ap\-southeast\-1a<br><br>* AZ B: ap\-southeast\-1b |
