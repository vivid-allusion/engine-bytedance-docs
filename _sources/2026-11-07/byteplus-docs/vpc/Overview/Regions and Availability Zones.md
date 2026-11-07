---
title: "Regions and Availability Zones"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Regions-and-Availability-Zones"
---

## Regions

### Introduction​

A region refers to a distinct geographic area where physical data centers are located, typically divided based on the city in which the data center resides.

### Related features

* Private networks between different regions are completely isolated, ensuring maximum stability and fault tolerance across regions.

* You can either use Elastic IP Addresses (EIP) for public interconnectivity across regions, or leverage Cloud Enterprise Network (CEN) for private interconnection.

### How to select a region

|Considerations |Recommended solution |
|---|---|
|Geographic location |To minimize access latency and maximize download speeds, we recommend creating your VPC in the region geographically closest to your target services. Note that the region cannot be modified after resource creation. |
|Private network connectivity |If isolating private networks is required, deploy them in different regions. If connecting private networks is required, deploy them in the same region. |

## Availability zone

### Introduction​

An Availability Zone (AZ) refers to a physically isolated location within the same region, featuring independent power and network infrastructure.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f10d7e47d58eae704eb219b7f37832f.png)

### Related features

* Within the same region and VPC, different AZs interconnect over the private network.

* Availability Zones are fault\-isolated, meaning a failure in one AZ does not impact the normal operation of others, ensuring your business remains continuously online.

### How to select an availability zone

* To ensure disaster recovery capabilities for your services, we recommend deploying them across different Availability Zones within the same region.

* If your services require lower latency, we recommend deploying them within the same Availability Zone.

* Availability Zone cannot be changed after resource creation.

## Regions and Availability Zones

The currently available Regions and Availability Zones are listed in the table below. We will gradually add more Regions and Availability Zones for your selection and use.

> **warning**

> Product features may vary by Region. The features available in the console shall prevail.

|Regions |RegionID |AZ Quantity |ZoneID |
|---|---|---|---|
|**China regions** ||||
|China (Beijing) |cn\-beijing |5 |* AZ A: cn\-beijing\-a<br><br>* AZ B: cn\-beijing\-b<br><br>* AZ C: cn\-beijing\-c<br><br>* AZ D: cn\-beijing\-d<br><br>* AZ\-E: cn\-beijing\-e |
|China (Shanghai) |cn\-shanghai |4 |* AZ A: cn\-shanghai\-a<br><br>* AZ B: cn\-shanghai\-b<br><br>* AZ C: cn\-shanghai\-c<br><br>* AZ E: cn\-shanghai\-e |
|China (Guangzhou) |cn\-guangzhou |3 |* AZ A: cn\-guangzhou\-a<br><br>* AZ B: cn\-guangzhou\-b<br><br>* AZ C: cn\-guangzhou\-c |
|China (Hong Kong) |cn\-hongkong |3 |* AZ A: cn\-hongkong\-a<br><br>* AZ B: cn\-hongkong\-b<br><br>* AZ C: cn\-hongkong\-c |
|**Other countries and regions** ||||
|Asia Pacific (Johor) |ap\-southeast\-1 |3 |* AZ A: ap\-southeast\-1a<br><br>* AZ B: ap\-southeast\-1b<br><br>* AZ C: ap\-southeast\-1c |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |3 |* AZ A: ap\-southeast\-3a<br><br>* AZ B: ap\-southeast\-3b<br><br>* AZ C: ap\-southeast\-3c |
