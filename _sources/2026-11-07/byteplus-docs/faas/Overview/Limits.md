---
title: "Limits"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Limits"
---

This topic outlines some of the constraints and limits when using the Function Service (FaaS) product.


|Limit item |Description |Limit |
|---|---|---|
|Function memory specification |The configurable memory size for a function instance. |512 ～ 3072 MiB |
|Maximum number of instances |The maximum number of instances a function can automatically scale. |100 |
|Instance concurrency |The maximum number of concurrent request that a single instance can support.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Asynchronous tasks do not support instance concurrency features.</div><br> |10 ~ 1000 |
|Number of triggers |The maximum number of triggers that can be created for a function. |20 |
|Function execution timeout |Time limit for single\-request execution, exceeding which terminates the process and returns an error. |* Synchronous call: 1 s ~ 15 min<br><br>* Asynchronous task: 10 s ~ 3 h |
|Temporary storage capacity |The maximum temporary storage space that a function instance can write to (/tmp directory). |10 GiB |
|Size of the valid payload in function call request |The maximum supported request payload size for a function instance. |* Synchronous call: 16 MiB<br><br>* Asynchronous task: 128 KiB |
|Instance log collection volume |The maximum log capacity that a single function Instance can collect. |2048 Bytes/s |
|Number of GPU instances |Quota of GPU Instances for each BytePlus Account. |5 |
|Function Instance Network Requests |For function instances with network requests in a single\-tenant single\-availability zone, if the function is bound to a VPC, all functions share the quota for a specific VPC subnet. When the limit is exceeded, requests from functions accessing the VPC network may encounter errors or be throttled.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The limit values are default settings. If you have usage requirements that exceed these limits, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001272">submit a ticket</a> to apply for higher quotas.</div><br> |* New connections per second: 10,000<br><br>* Concurrent connections: 100,000<br><br>* Bandwidth: 1 Gbps |
