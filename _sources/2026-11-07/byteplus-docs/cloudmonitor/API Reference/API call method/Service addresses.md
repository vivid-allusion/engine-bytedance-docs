---
title: "Service addresses"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Service_address"
---

To achieve low latency, it is recommended to select a service address according to the region where the resource is located.


|**Enabled regions** ||**RegionId** |**Service access address (new)**  |**Service access address (old)**  |
|---|---|---|---|---|
|China region |China (Beijing) |cn\-beijing |cloudmonitor.cn\-beijing.byteplusapi.com.cn |open.volcengineapi.com |
||China (Shanghai) |cn\-shanghai |cloudmonitor.cn\-shanghai.byteplusapi.com.cn ||
||China (Guangzhou) |cn\-guangzhou |cloudmonitor.cn\-guangzhou.byteplusapi.com.cn ||
||China (Hong Kong) |cn\-hongkong |cloudmonitor.cn\-hongkong.byteplusapi.com ||
|Other regions |Asia Pacific (Johor) |ap\-southeast\-1 |cloudmonitor.ap\-southeast\-1.byteplusapi.com ||
||Asia Pacific (Jakarta) |ap\-southeast\-3 |cloudmonitor.ap\-southeast\-3.byteplusapi.com ||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For latency\-sensitive business, it is recommended to specify regions in the request headers. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Common-parameters">Public parameters</a>.</div>


* <div data-tips="true" data-tips-type="tip">Domain names only represent access points of APIs and have nothing to do with the actual region where products deliver services.</div>
