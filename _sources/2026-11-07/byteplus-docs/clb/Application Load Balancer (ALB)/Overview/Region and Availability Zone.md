---
title: "Region and Availability Zone"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Regions-and-Availability-Zones"
---

<span id=".5Zyw5Z-f5LiO5Y-v55So5Yy6"></span>
## Regions and Availability Zones

<span id=".5Z-65pys5qaC5b-1"></span>
### Terms


* A region is a geographic area where BytePlus data centers are located. BytePlus divides regions based on the geographical position of data centers. Once an ALB instance is created, its region cannot be changed.

* An availability zone (AZ) is a group of one or more physical data centers. Within the same region, the power and network infrastructure of availability zones are independent, so a failure in one AZ does not affect other AZs in the same region. An availability zone in one region is completely isolated from an availability zone in another region, but availability zones within the same region can connect with each other.


<span id=".5aaC5L2V6YCJ5oup5Zyw5Z-f"></span>
### How to select a region

It is recommended to choose the region closest to your users to reduce network latency and improve access speed.

<span id=".5aaC5L2V6YCJ5oup5Y-v55So5Yy6"></span>
### How to select an availability zone


* If there is only one availability zone in a region, you can only select that availability zone.

* If there are two or more availability zones in a region, it is recommended to select at least two availability zones to create instances and improve service availability.


<span id=".YWxi55qE5Zyw5Z-f5LiO5Y-v55So5Yy6"></span>
## Regions and availability zones of ALB

Multi\-availability zone deployment of ALB provides more stable and reliable traffic load balancing services.


* ALB instances support multi\-availability zone functionality, allowing you to select multiple availability zones for one ALB instance. Under normal circumstances, traffic is forwarded by the same ALB instance to multiple availability zones within the same region. No duplicate instance fees occur due to multiple availability zones.

* If one availability zone fails, ALB will still forward traffic to other availability zones within the same region.

* You can deploy backend servers of the same server group across different availability zones. The ALB instance routes traffic to these backend servers in different availability zones based on the specified forwarding rules.

* When an availability zone fails, ALB isolates instances and backend servers within that zone and reallocates traffic to the remaining healthy servers based on the load balancing algorithm and load allocation ratio.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once the failed availability zone recovers, the load balancing service resumes immediately.   </div>
   

<span id=".YWxi55qE5Zyw5Z-f5LiO5Y-v55So5Yy65YiX6KGo"></span>
## ALB regions and availability zones

The currently available Regions and Availability Zones are listed in the table below. We will gradually add more Regions and Availability Zones for your selection and use.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please refer to the actual regions and availability zones supported by the console.</div>



|**Regions** |**Region ID** |**AZ Quantity** |**Availability zone ID** |**Status** |
|---|---|---|---|---|
|China (Beijing） |cn\-beijing |5 |* AZ A: cn\-beijing\-a<br><br>* AZ B: cn\-beijing\-b<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Availability Zone B in China (Beijing) was discontinued as of August 1, 2026. Following this discontinuation, ALB instances can no longer be created in this availability zone.   </div><br>   <br><br>   * AZ C: cn\-beijing\-c<br><br>* AZ D: cn\-beijing\-d<br><br>* AZ\-E: cn\-beijing\-e |GA |
|China (Shanghai) |cn\-shanghai |4 |* AZ A: cn\-shanghai\-a<br><br>* AZ B: cn\-shanghai\-b<br><br>* AZ C: cn\-shanghai\-c<br><br>* AZ E: cn\-shanghai\-e |GA |
|China (Guangzhou) |cn\-guangzhou |3 |* AZ A: cn\-guangzhou\-a<br><br>* AZ B: cn\-guangzhou\-b<br><br>* AZ C: cn\-guangzhou\-c |GA |
|China (Hong Kong) |cn\-hongkong |2 |* AZ A: cn\-hongkong\-a<br><br>* AZ B: cn\-hongkong\-b |GA |
|Asia Pacific (Johor) |ap\-southeast\-1 |3 |* AZ A: ap\-southeast\-1a<br><br>* AZ B: ap\-southeast\-1b<br><br>* AZ C: ap\-southeast\-1c |GA |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |3 |* AZ A: ap\-southeast\-3a<br><br>* AZ B: ap\-southeast\-3b<br><br>* AZ C: ap\-southeast\-3c |GA |
