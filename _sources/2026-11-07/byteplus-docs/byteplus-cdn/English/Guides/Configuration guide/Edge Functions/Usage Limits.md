---
title: "Usage Limits"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Usage_Limits_Functions"
---

This document introduces the usage limits of functions and Edge KV.

<span id="function-usage-limits"></span>
### Function usage limits


|Limit |Description |
|---|---|
|Programming language |Supports JavaScript (ES6). |
|Memory |Each function can use 128 MB of memory on an edge node. You can [submit a ticket](https://console.byteplus.com/workorder/create) to adjust this quota. |
|CPU time |The CPU time consumed by a function during each execution should not exceed 50 ms (excluding waiting time for IO/timers/kernel and other external events). You can [submit a ticket](https://console.byteplus.com/workorder/create) to adjust this quota. |
|Response time |The time from triggering to completion of each function execution should not exceed 30 seconds. You can [submit a ticket](https://console.byteplus.com/workorder/create) to adjust this quota. |
|.js file size |The maximum size of a single .js file should not exceed 2 MB. |
|Number of functions |Each primary account can create up to 100 functions. You can request to adjust this quota in the [Quota Center](https://console.byteplus.com/quota/productList). |
|Number of domains |Each function can be associated with up to 100 domains. Each domain can be associated with up to 50 functions. You can request to adjust this quota in the [Quota Center](https://console.byteplus.com/quota/productList). |
|Number of Cron triggers |Each function can have up to 10 Cron triggers. You can request to adjust this quota in the [Quota Center](https://console.byteplus.com/quota/productList). |
|HTTP request methods |A function can handle the following types of HTTP requests:<br><br><br>* GET<br><br>* POST<br><br>* PUT<br><br>* DELETE<br><br>* OPTIONS<br><br>* HEAD<br><br>* PURGE<br><br>* PATCH<br><br>* TRACE |
|Number of [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch) calls |The number of fetch() calls should not exceed 4 for each function execution. |


<span id="edge-kv-usage-limits"></span>
### Edge KV usage limits


|Limit |Description |
|---|---|
|Access restriction |Functions can only read and write Edge KV data under the same primary account. |
|Namespaces |Each primary account can create up to 10 namespaces. In a primary account, the name of each namespace must be unique. You can request to adjust this quota in the [Quota Center](https://console.byteplus.com/quota/productList). |
|Storage capacity |Each primary account has a maximum storage capacity of 10 GB. Each namespace has a maximum capacity of 1 GB. |
|Key\-value pairs |Key: Can only contain English letters, numbers, hyphens (\-), and underscores (_), and cannot exceed 512 Bytes.<br><br>Value: Cannot exceed 128KB. |
|Synchronization time |Edge KV data synchronization is completed across all edge nodes within a maximum of 60 seconds. |
|Number of [KV.set()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI#kv-set), [KV.get()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI#kv-get), and [KV.delete()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI#kv-delete) calls |The total number of KV.set(), KV.get(), and KV.delete() calls should not exceed 10 for each function execution. |
