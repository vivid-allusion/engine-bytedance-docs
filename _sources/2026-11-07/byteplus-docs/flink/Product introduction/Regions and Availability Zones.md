---
title: "Regions and Availability Zones"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Regions_and_Availability_Zones"
---

This article introduces the regions and availability zones supported by BytePlus Flink, to assist you in selecting them more conveniently.

<span id="13ba99a9"></span>
## **Background Information**

Before purchasing Flink resources in specific regions and availability zones, you should first understand the basic definitions and relevant characteristics of regions and availability zones.

**Region**: Refers to different geographical areas where data centers are located, usually divided by the city where the data center is located. For example, the "North China 2 (Beijing)" region indicates that the city where the data center is located is Beijing.

**Availability Zone**: Refers to physically separate areas within the same region that are independent in terms of power and network. Availability zones are isolated from failures, and a fault in one availability zone does not affect the normal use of other availability zones.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A region is usually composed of multiple availability zones. Within the same region, different availability zones in the same virtual private network can communicate over an internal network; availability zones in different regions are completely isolated from each other.</div>


* <div data-tips="true" data-tips-type="tip">When purchasing a BytePlus Flink resource pool, the selected region and availability zone cannot be changed after the resource pool is created.</div>


* <div data-tips="true" data-tips-type="tip">The resources available in different regions can be adjusted at any time based on actual business usage, and there may be situations where resources cannot be purchased due to being sold out. Please refer to the resources displayed on the purchase page of the console. When resources are sold out and cannot be purchased, you may try changing the availability zone and region to make a purchase.</div>



<span id="b9d2b007"></span>
## How to Choose


|**Consideration Factors** |**Description** |
|---|---|
|Multi\-cloud product network connectivity |When your BytePlus Flink needs network connectivity with other cloud products (upstream and downstream storage), it is recommended to deploy BytePlus Flink in the same region and availability zone as the other cloud products. To ensure intercommunication between different cloud products via the internal network, reducing access latency and increasing access speed. |
|Network latency |* To reduce access latency, we recommend buying BytePlus Flink resource pools in the region closest to you. The closer you are to the resource region, the lower the network latency and the faster the access speed.<br><br>* If you require even lower latency, it is recommended to purchase the BytePlus Flink resource pool within the same availability zone. |
|High availability and disaster recovery |If you need higher disaster recovery capability, it is recommended to deploy your business across different availability zones to ensure fault isolation between zones and to achieve cross\-zone disaster recovery.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended that you assess based on the actual needs of the business to find the optimal balance between high availability and low latency.</div><br> |


<span id="647d08d5"></span>
## Region and Availability Zone List


|**Region** |**Number of availability zones** |**RegionID** |
|---|---|---|
|China (Hong Kong) |2 |cn\-hongkong |
|Asia Pacific (Johor) |3 |ap\-southeast\-1 |
