---
title: "Service address"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/service_address"
---

APMPlus provides two sub\-products: Server\-side Monitoring and RUM. The service endpoints for different sub\-products vary slightly. To achieve low latency, it is recommended to select a service address according to the region where the resource is located.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For latency\-sensitive businesses, we recommend specifying the region in the request header. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/Public_parameters">Public parameters</a>.</div>


* <div data-tips="true" data-tips-type="default">Domain names are API access points and do not indicate the region where the service is actually provided.</div>



<span id="RwaGFGWs"></span>
### Server\-side Monitoring


|Regions |**Region names** |**Region ID** |OpenAPI endpoint |
|---|---|---|---|
|China region |China (Beijing) |cn\-beijing |https://apmplus\-server.cn\-beijing.byteplusapi.com.cn |
||China (Shanghai) |cn\-shanghai |https://apmplus\-server.cn\-shanghai.byteplusapi.com.cn |
||China (Guangzhou) |cn\-guangzhou |https://apmplus\-server.cn\-guangzhou.byteplusapi.com.cn |
||China (Hong Kong) |cn\-hongkong |https://apmplus\-server.cn\-hongkong.byteplusapi.com |
|Asia Pacific |Asia Pacific (Johor) |ap\-southeast\-1 |https://apmplus\-server.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |https://apmplus\-server.ap\-southeast\-3.byteplusapi.com |


<span id="BKDPfeUg"></span>
### RUM


|Regions |**Region names** |**Region ID** |OpenAPI endpoint |
|---|---|---|---|
|China region |China (Beijing) |cn\-beijing |https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn |
|Asia Pacific |Asia Pacific (Johor) |ap\-southeast\-1 |https://apmplus\-openapi.ap\-southeast\-1.byteplusapi.com |
