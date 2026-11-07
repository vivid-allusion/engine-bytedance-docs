---
title: "Service Address"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Service_address"
---

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located.


|**Available Regions** ||**RegionId** |**New Service Access Address** |**Legacy Service Access Address** |
|---|---|---|---|---|
|China Regions |China (Beijing) |cn\-beijing |cr.cn\-beijing.byteplusapi.com.cn |open.volcengineapi.com |
||China (Shanghai) |cn\-shanghai |cr.cn\-shanghai.byteplusapi.com.cn ||
||China (Guangzhou) |cn\-guangzhou |cr.cn\-guangzhou.byteplusapi.com.cn ||
||China (Hong Kong) |cn\-hongkong |cr.cn\-hongkong.byteplusapi.com ||
|<div style="text-align: center"><br>Other Regions</div><br> |Asia Pacific (Johor) |ap\-southeast\-1 |cr.ap\-southeast\-1.byteplusapi.com ||
||Asia Pacific (Jakarta) |ap\-southeast\-3 |cr.ap\-southeast\-3.byteplusapi.com |\- |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For latency\-sensitive operations, it is recommended to specify the Region in the request Header. For more details, please refer to the <a href="https://docs.byteplus.com/en/docs/cr/common-parameters">Public parameters</a> documentation.</div>


* <div data-tips="true" data-tips-type="default">The domain name serves as the access point for the API and does not necessarily represent the actual region where the service is provisioned.</div>
