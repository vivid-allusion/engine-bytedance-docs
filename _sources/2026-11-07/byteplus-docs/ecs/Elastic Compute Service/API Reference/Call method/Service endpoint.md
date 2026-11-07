---
title: "Service endpoint"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Service_address"
---

For lower latency, select the appropriate service endpoint based on the region where your resource is located.


|**Region** ||**RegionId** |**Service endpoint (new)**  |**Service endpoint (old)**  |
|---|---|---|---|---|
|China regions |China (Beijing) |cn\-beijing |ecs.cn\-beijing.byteplusapi.com.cn |open.ap\-southeast\-1.byteplusapi.com |
||China (Shanghai) |cn\-shanghai |ecs.cn\-shanghai.byteplusapi.com.cn ||
||China (Guangzhou) |cn\-guangzhou |ecs.cn\-guangzhou.byteplusapi.com.cn ||
||China (Hong Kong) |cn\-hongkong |ecs.cn\-hongkong.byteplusapi.com ||
|Other regions |Asia Pacific (Johor) |ap\-southeast\-1 |ecs.ap\-southeast\-1.byteplusapi.com ||
||Asia Pacific (Jakarta) |ap\-southeast\-3 |ecs.ap\-southeast\-3.byteplusapi.com ||


<span id="OYvP0gJp"></span>
### <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For latency\-sensitive businesses, it is recommended to specify the region in the request header. For detailed information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Public-parameters">common parameters</a>.</div>


* <div data-tips="true" data-tips-type="default">The domain name is the access point of the API and does not represent the region where the product provides services.</div>
