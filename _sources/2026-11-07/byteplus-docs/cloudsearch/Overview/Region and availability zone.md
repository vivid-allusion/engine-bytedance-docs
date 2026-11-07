---
title: "Region and availability zone"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Region_and_availability_zone"
---

This article outlines the supported regions and availability zones in BytePlus cloud search service, in an effort to facilitate optimal deployment planning.

<span id="25c82fac"></span>
## **Background**

Prior to purchasing ES instances in regions and availability zones, ensure the understanding of their fundamental definitions and associated features.

**Region**: a geographical distinct data center location, typically demarcated by city boundaries. For example, the North China 2 (Beijing) region means the data center is located in Beijing.

**Availability zone (Zone)** : a physically isolated area within a region, with independent power and network infrastructure. Availability zones are fault\-isolated. A failure in one availability zone does not impact other availability zone operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb4434ba39704479b5ed061b1946c441~tplv-goo7wpa0wc-image.image) </span>

<span id="6c493f7c"></span>
## Notice

Before selecting regions and availability zones, review the following considerations.


* A region typically consists of multiple availability zones. Within the same region, availability zones under one VPC maintain private network connectivity, while availability zones across different regions remain fully isolated.

* The selected region and availability zone for an ES instance cannot be modified after the instance is created successfully.

* Resource availability in various regions is subject to dynamic adjustment based on actual usage. Inventory depletion may occur. Refer to the available resources on the console purchase page.

   **If resources are depleted in your selected zone/region, attempt purchase in alternative availability zones and regions.** 


<span id="c51a8a60"></span>
## How to select


|**Considerations** |**Note** |
|---|---|
|Multi\-cloud product network connectivity |For optimal network connectivity between the cloud search service and other cloud products, deploy them within the same region and availability zone. Therefore, internal network connectivity between cloud products reduces access latency and improves access speed. |
|Network latency |* To minimize access latency, it is recommended to purchase your ES instance in the nearest available region. The closer you are to the resource region, the lower the network latency and the faster the access speed.<br><br>* For lower latency, it is recommended to purchase the ES instance within the same availability zone. |
|High availability and disaster recovery |For higher disaster recovery capability, it is recommended to deploy your services across multiple availability zones, thus ensuring fault isolation and enabling cross\-availability zone disaster recovery.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to evaluate your actual business needs and find the best balance between high availability and low latency.</div><br> |
