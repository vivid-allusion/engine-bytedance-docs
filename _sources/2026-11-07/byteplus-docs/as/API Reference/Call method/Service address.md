---
title: "Service address"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Service-URL"
---

To achieve low latency, it is recommended to select the corresponding service URL based on the region where the resource is located.


|**Region name** ||**Region ID** |**Service address** |
|---|---|---|---|
|**China regions**<br><br> |China (Beijing) |cn\-beijing |`IPv4` auto\-scaling.cn\-beijing.byteplusapi.com.cn<br><br>`Dual-stack` auto\-scaling.cn\-beijing.byteplus\-api.com.cn |
||China (Shanghai) |cn\-shanghai |`IPv4` auto\-scaling.cn\-shanghai.byteplusapi.com.cn<br><br>`Dual-stack` auto\-scaling.cn\-shanghai.byteplus\-api.com.cn |
||China (Guangzhou) |cn\-guangzhou |`IPv4` auto\-scaling.cn\-guangzhou.byteplusapi.com.cn<br><br>`Dual-stack` auto\-scaling.cn\-guangzhou.byteplus\-api.com.cn |
||China (Hong Kong) |cn\-hongkong |`IPv4` auto\-scaling.cn\-hongkong.byteplusapi.com |
|**Overseas regions** |Asia Pacific (Johor) |ap\-southeast\-1 |`IPv4` auto\-scaling.ap\-southeast\-1.byteplusapi.com |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |`IPv4` auto\-scaling.ap\-southeast\-3.byteplusapi.com |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For latency\-sensitive businesses, it is recommended to specify the region in the request header. For detailed information, refer to <a href="https://docs.byteplus.com/en/docs/as/Public-parameters">common parameters</a>.</div>


* <div data-tips="true" data-tips-type="default">The domain name is the access point of the API and does not represent the region where the product provides services.</div>
