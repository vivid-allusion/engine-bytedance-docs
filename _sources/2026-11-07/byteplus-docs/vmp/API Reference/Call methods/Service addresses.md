---
title: "Service addresses"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Service_address"
---

To achieve low latency, it is recommended to select a service address according to the region where the resource is located.


|**Enabled regions** ||**RegionId** |**Service access address (new)**  |**Service access address (old)**  |
|---|---|---|---|---|
|China region |China (Beijing) |cn\-beijing |vmp.cn\-beijing.byteplusapi.com.cn |open.volcengineapi.com |
||China (Shanghai) |cn\-shanghai |vmp.cn\-shanghai.byteplusapi.com.cn ||
||China (Guangzhou) |cn\-guangzhou |vmp.cn\-guangzhou.byteplusapi.com.cn ||
||China (Hong Kong) |cn\-hongkong |vmp.cn\-hongkong.byteplusapi.com ||
|Other regions |Asia Pacific (Johor) |ap\-southeast\-1 |vmp.ap\-southeast\-1.byteplusapi.com ||
||Asia Pacific (Jakarta) |ap\-southeast\-3 |vmp.ap\-southeast\-3.byteplusapi.com ||


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For latency\-sensitive workloads, we recommend specifying a region in the request header. See <a href="https://docs.byteplus.com/en/docs/vmp/Common-parameters">Default parameters</a> for details.</div>


* <div data-tips="true" data-tips-type="default">Domain names are API access points and do not indicate the region where the service is actually provided.</div>
