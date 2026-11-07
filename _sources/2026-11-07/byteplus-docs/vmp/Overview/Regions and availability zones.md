---
title: "Regions and availability zones"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Regions-and-availability-zones"
---

This topic describes the relationship between regions and availability zones, how to select regions and availability zones, and the available regions of Vital Managed Service for Prometheus (VMP).

<span id=".5LuA5LmI5piv5Zyw5Z-f44CB5Y-v55So5Yy6"></span>
## Basic concept

Regions and availability zones are usually used to describe the locations of physical data centers. Regions are independent of each other, and availability zones are isolated from each other. However, availability zones within the same region are connected by low\-latency links. The following figure shows the relationship between regions and availability zones.


* **Regions**: the geographical locations of physical data centers. After resource creation, you cannot change the corresponding region. The internal networks of different regions are isolated. This ensures the highest stability and fault tolerance between regions.


From the perspective of geographical location, it is recommended to select the region close to you or your target users to reduce network latency and accelerate access.


* **Availability zone**: the physical locations, which have their own independent power supply and network in a region. Whether to deploy resources in the same availability zone mainly depends on your requirements for disaster recovery and network latency.

   * Availability zones in the same region are connected over an internal network, and fault isolation can be achieved between availability zones. If you want to achieve disaster recovery for your service, it is recommended to deploy the service in different availability zones within the same region.

   * The network latency between instances within the same availability zone is smaller. If your services require lower latency, it is recommended to deploy the service within the same availability zone.


<span id=".5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo"></span>
## List of regions and availability zones

The following table shows the available regions and region IDs of VMP.


|**Region** |**City** |**Region ID** |Release Status |
|---|---|---|---|
|**China** ||||
|China (Beijing) |Beijing |cn\-beijing |General availability |
|China (Shanghai) |Shanghai |cn\-shanghai |General availability |
|China (Guangzhou) |Guangzhou |cn\-guangzhou |General availability |
|China (Hong Kong) |China (Hong Kong) |cn\-hongkong |General availability |
|**Other countries and regions** ||||
|Asia Pacific (Johor) |Johor |ap\-southeast\-1 |General availability |
||Jakarta |ap\-southeast\-3 |General availability |
