---
title: "Determining Proton cache size"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Determining_Proton_cache_size"
---

<span id="_1-利用空闲ssd"></span>
## 1 **Utilize idle SSDs**

By monitoring Node metrics, you can observe local disk utilization. Unused disk space can be allocated to Proton's cache to achieve acceleration. When configuring space for Proton, do not allocate all idle space to the Proton cache; ensure that disk utilization does not exceed 90%.

<span id="_2-提升缓存命中率"></span>
## 2 **Improve cache hit rate**

In cache\-enabled mode, the higher the cache hit rate, the better the acceleration effect. By monitoring Proton metrics, you can calculate the current cache hit rate. Adjust the cache size to maintain the cache hit rate at around 80% for optimal performance.

Cache hit rate = Hit Ops / (Hit Ops + Miss Ops).
