---
title: "Regions and availability zones"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones"
---

<span id=".5Zyw5Z-f77yIUmVnaW9u77yJ"></span>
## Region

<span id=".566A5LuL"></span>
#### Overview

Region refers to a geographic area where physical data centers are located. Typically, regions are divided by the city where the data centers reside.

<span id=".55u45YWz54m55oCn"></span>
#### Notes


* Private networks between different regions are completely isolated, which ensures maximum stability and fault tolerance across regions.

* Resources in different regions can connect through Elastic IP Address (EIP). Private networks in different regions can connect through Cloud Enterprise Network (CEN).


<span id=".5aaC5L2V6YCJ5oup5Zyw5Z-f77yf"></span>
#### How to select a region?


|Consideration |Recommendation |
|---|---|
|Geographical area |For good download performance and low latency, we recommend that you select a region closest to your desired service when you buy an ECS instance. Note that once you have paid for an instance, you cannot change the region. |
|Private network connectivity |If isolating VPCs is required, deploy VPCs in different regions. If connecting VPCs is required, deploy VPCs in the same region. |
|Resource price |Resource prices may vary based on regions. When selecting a region, please refer to the prices listed on the purchase page and consider your budget. |


<span id=".5Y-v55So5Yy677yIQVrvvIk="></span>
## Availability zone

<span id=".566A5LuL"></span>
#### Overview

Availability zones (AZs) are physical areas that use separate power sources and networks in a region.

<span id=".55u45YWz54m55oCn"></span>
#### Notes


* Within the same region and VPC, different AZs interconnect over the private network.

* Availability Zones are fault\-isolated, meaning a failure in one AZ does not impact the normal operation of others, ensuring your business remains continuously online.


<span id=".5aaC5L2V6YCJ5oup5Y-v55So5Yy677yf"></span>
#### How to select an availability zone?


* If your services require disaster recovery, we recommend that you deploy resources in different availability zones of a region.

* If your services require low latency, we recommend that you deploy resources in the same availability zone.

* After the resource is purchased, the availability zone cannot be changed.


<span id=".5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo"></span>
## Regions and availability zones​

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The regions available for different products may vary.</div>



|**Region** |**City** |**Number of AZs** |**RegionID** |**ZoneID** |**Release status** |
|---|---|---|---|---|---|
|China |Beijing |3 |cn\-beijing |* Availability zone A: cn\-beijing\-a<br><br>* Availability zone C: cn\-beijing\-c<br><br>* Availability zone D: cn\-beijing\-d |GA |
|China |Shanghai |2 |cn\-shanghai |* Availability zone A: cn\-shanghai\-a<br><br>* Availability zone B: cn\-shanghai\-b |GA |
|China |Guangzhou |1 |cn\-guangzhou |* Availability zone A: cn\-guangzhou\-a |GA |
|China |Hong Kong |3 |cn\-hongkong |* Availability zone A: cn\-hongkong\-a<br><br>* Availability zone B: cn\-hongkong\-b<br><br>* Availability zone C: cn\-hongkong\-c |GA |
|Asia Pacific |Johor |3 |ap\-southeast\-1 |* Availability zone A: ap\-southeast\-1a<br><br>* Availability zone B: ap\-southeast\-1b<br><br>* Availability zone C: ap\-southeast\-1c |GA |
|Asia Pacific |Jakarta |3 |ap\-southeast\-3 |* Availability zone A: ap\-southeast\-3a<br><br>* Availability zone B: ap\-southeast\-3b<br><br>* Availability zone C: ap\-southeast\-3c |GA |
