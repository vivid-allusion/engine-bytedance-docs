---
title: "Regions and availability zones"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Regions_and_availability_zones"
---

This article introduces the regions and availability zones supported by Milvus for VectorDB to help you select regions and availability zones more easily.

<span id="25c82fac"></span>
## **Background**

Before selecting a region and availability zone to purchase a Milvus for VectorDB instance, you should first understand the basic definitions and related features of regions and availability zones.

**Region**: a geographical distinct data center location, typically demarcated by city boundaries. For example, the North China 2 (Beijing) region means the data center is located in Beijing.

**Availability zone**: refers to a physically independent area within the same region with separate power and network. Availability zones are fault\-isolated. A failure in one availability zone does not impact other availability zone operations.

<span id="6c493f7c"></span>
## Precautions


* A region typically consists of multiple availability zones. Within the same region, availability zones under one VPC maintain private network connectivity, while availability zones across different regions remain fully isolated.

* The region and availability zone selected when purchasing a Milvus for VectorDB instance cannot be changed after the instance is created.

* Resource availability in various regions is subject to dynamic adjustment based on actual usage. Inventory depletion may occur. Refer to the available resources on the console purchase page. If resources are depleted in your selected zone/region, attempt purchase in alternative availability zones and regions.


<span id="c51a8a60"></span>
## How to select


|**Considerations** |**Description** |
|---|---|
|Multi\-cloud product network connectivity |When your Milvus for VectorDB needs network connectivity with other cloud products, it is recommended to deploy them within the same region and availability zone. Therefore, internal network connectivity between cloud products reduces access latency and improves access speed. |
|Network latency |* To reduce network latency and improve access speed, we recommend purchasing Milvus for VectorDB instances in the region closest to your business.<br><br>* If your business requires lower latency, deploy the instance in the same availability zone as your business servers. |
|High availability and disaster recovery |For higher disaster recovery capability, it is recommended to deploy your services across multiple availability zones, thus ensuring fault isolation and enabling cross\-availability zone disaster recovery.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to evaluate your actual business needs and find the best balance between high availability and low latency.</div><br> |
