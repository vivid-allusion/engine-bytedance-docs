---
title: "Product specification"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/product_specifications"
---

This topic describes the product specification of Database Transmission Service (DTS).

<span id=".6KeE5qC85oCn6IO96KGo"></span>
## Specification performance table


|Specification |Performance upper limit reference value (RPS) ||
|---|---|---|
||Incremental migration, incremental synchronization, or subscription rate |Full migration or full initialization |
|Compact |2,000. |The actual online performance depends on the network environment, and there is no theoretical maximum value. |
|Medium |5,000. ||
|Standard |The actual online performance depends on the network environment, and there is no theoretical maximum value. ||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The performance metric for DTS is the data rows migrated or synchronized per second (i.e., RPS).</div>


* <div data-tips="true" data-tips-type="tip">The performance ceiling for each specification can only reach the reference values listed in the table when all of the following conditions are met simultaneously.</div>


   * <div data-tips="true" data-tips-type="tip">The load on the source instance must meet or exceed the performance ceiling corresponding to each specification.</div>


   * <div data-tips="true" data-tips-type="tip">The write performance of the target instance is not a bottleneck and can support the load corresponding to each specification.</div>


   * <div data-tips="true" data-tips-type="tip">The network latency between both the source instance, the target instance, and the DTS server is less than or equal to 2ms.</div>
