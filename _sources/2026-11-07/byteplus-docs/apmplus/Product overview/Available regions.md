---
title: "Available regions"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/server-launching_region"
---

This topic describes the concept of regions, methods of selecting regions, and the regions where APMPlus is available.

<span id="7z8HeeZr"></span>
## Region overview

Regions refer to the different geographical locations of physical data centers. They are typically categorized based on the city where each physical data center is located. The internal networks of different regions are isolated. This ensures the highest stability and fault tolerance between regions. Different regions can communicate with each other via EIPs or through private network connections such as CEN.

<span id="pMtlt5YY"></span>
## Method of selecting a region

After resources are created, you cannot change their regions. Therefore, when you select a region, consider the following factors:


* From the perspective of geographical location, we recommend that you select the region close to you or your target users to reduce network latency and accelerate access.

* From the perspective of private network connectivity, if your services require isolation, deploy them in different regions. If not, deploy them in the same region.

* From the perspective of resource pricing, resource prices may vary based on different regions. If you or your target users are located in the Chinese mainland, you do not need to consider network latencies caused by different regions. This is because differences between regions in the Chinese mainland are small in terms of infrastructure, BGP network quality, and resource operations and configurations.


<span id="NqrnvZTE"></span>
## Available regions

APMPlus supports two sub\-products: Server\-side Monitoring and RUM. The service regions and service addresses for each sub\-product slightly differ. The following table lists service regions and their related information.

<span id="yyRUFJxO"></span>
### Server\-side Monitoring


|Area |**Region names** |**Region ID** |OpenAPI endpoint |
|---|---|---|---|
|China |China (Beijing) |cn\-beijing |https://apmplus\-server.cn\-beijing.byteplusapi.com.cn |
||China (Shanghai) |cn\-shanghai |https://apmplus\-server.cn\-shanghai.byteplusapi.com.cn |
||China (Guangzhou) |cn\-guangzhou |https://apmplus\-server.cn\-guangzhou.byteplusapi.com.cn |
||China (Hong Kong) |cn\-hongkong |https://apmplus\-server.cn\-hongkong.byteplusapi.com |
|Asia Pacific |Asia Pacific (Johor) |ap\-southeast\-1 |https://apmplus\-server.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |https://apmplus\-server.ap\-southeast\-3.byteplusapi.com |


<span id="keu2tEyg"></span>
### RUM


|Area |**Region names** |**Region ID** |service address ||
|---|---|---|---|---|
|China |China (Beijing) |cn\-beijing |OpenAPI endpoint |https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn |
||||SDK endpoint |https://apmplus.bytepluses.com |
||||Symbol table request URL |https://open.apmplus.cn\-beijing.bytepluses.com/apmplus_api/eue/guest/app/mapping/upload |
|Asia Pacific |Asia Pacific (Johor) |ap\-southeast\-1 |OpenAPI endpoint |https://apmplus\-openapi.ap\-southeast\-1.byteplusapi.com |
||||SDK endpoint |https://apmplus.ap\-southeast\-1.bytepluses.com |
||||Symbol table request URL |https://open.apmplus.ap\-southeast\-1.bytepluses.com/apmplus_api/eue/guest/app/mapping/upload |
