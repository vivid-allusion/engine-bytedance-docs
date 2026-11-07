---
title: "Regions and AZs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones"
---

This topic describes the relationship between regions and availability zones (AZs), how to choose regions and AZs, and the regions where Vital Kubernetes Engine (VKE) is supported.

<span id=".5LuA5LmI5piv5Zyw5Z-f44CB5Y-v55So5Yy6"></span>
## What are regions and AZs?

Regions and AZs are commonly used to describe the geographical locations of physical data centers. Regions are independent of each other. AZs are isolated from each other but the AZs within the same region are connected through low\-latency links. The following figure displays the relationship between regions and AZs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7fda8517034e385b1fe01bbc5b4c8d6.png) </span>


* **Region**: refers to the geographic region where a physical data center resides. Once a resource is created, the region cannot be changed. Internal networks of different regions are isolated from each other to maximize stability and fault tolerance across regions.

   * From a geographical point of view, Geographically, select a region close to you or your target users to reduce network latency and improve access speed. that is close to you or the region of your target users to reduce network latency and accelerate access.

   * Resource pricing in different regions may differ. If you or your target users are in the Chinese mainland, you do not need to consider network latency in different regions. This is because the infrastructure, BGP network performance, and resource operation and configuration are largely consistent across regions in the Chinese mainland.differ slightly between regions in the Chinese mainland.

* **AZ**: refers to a physically independent area within the same region, featuring separate power and network infrastructure. Whether to deploy resources in the same AZ depends on your requirements for disaster recovery and network latency.

   * AAZs in the same region communicate over internal networks and provide fault isolation between each other. To enable disaster recovery for your services, we recommend that you deploy the services in different AZs within a region.

   * The network latency between instances in the same AZ is lower than that between instances in different AZs. For lower latency requirements, we recommend that you deploy your services within the same AZ.


<span id=".5Zyw5Z-f5ZKM5Y-v55So5Yy65YiX6KGo"></span>
## List of regions and AZs

The following displays the regions where VKE is supported, RegionIDs, and AZs.


|Region |RegionID |ZoneID |Release status |
|---|---|---|---|
|Asia Pacific (Johor) |ap\-southeast\-1 |AZ A: ap\-southeast\-1a |Commercial use |
|||AZ B: ap\-southeast\-1b |Commercial use |
|Asia Pacific (Jakarta) |ap\-southeast\-3 |AZ A: ap\-southeast\-3a |Commercial use |
|||AZ B: ap\-southeast\-3b |Commercial use |
|||AZ C: ap\-southeast\-3c |Commercial use |
|China (Hong Kong) |cn\-hongkong |AZ A: cn\-hongkong\-a |Commercial use |
|||AZ B: cn\-hongkong\-b |Commercial use |
|China (Beijing) |cn\-beijing |AZ A: cn\-beijing\-a |Commercial use |
|||AZ C: cn\-beijing\-c |Commercial use |
|||AZ D: cn\-beijing\-d |Commercial use |
|China (Guangzhou) |cn\-guangzhou |AZ A: cn\-guangzhou\-a |Commercial use |
|||AZ B: cn\-guangzhou\-b |Commercial use |
|||AZ C: cn\-guangzhou\-c |Commercial use |
|China (Shanghai) |cn\-shanghai |AZ B: cn\-shanghai\-b |Commercial use |
|||AZ C: cn\-shanghai\-c |Commercial use |
|||AZ E: cn\-shanghai\-e |Commercial use |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">How VKE features are supported may differ in different regions. View information about a feature to obtain the regions where the feature is supported.</div>
