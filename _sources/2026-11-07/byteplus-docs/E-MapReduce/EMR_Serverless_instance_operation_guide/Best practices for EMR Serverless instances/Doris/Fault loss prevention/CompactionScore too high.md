---
title: "CompactionScore too high"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_doris_compactionscore_too_high"
---

<span id="4c7ccdb1"></span>
## Use cases


* Applicable to scenarios where a cluster's CompactionScore is too high, resulting in degraded read and write performance. This can be mitigated by manually forcing a Compact operation.

* The mitigation strategy should be determined by considering the cluster's resource utilization, the customer's write model, and write frequency. This document only provides the procedure for manually triggering a Compact operation.


<span id="9cd49534"></span>
## Applicable versions


|**Product type** |**Engine** |**Deployment method** |**Applicable versions** |
|---|---|---|---|
|Serverless instance<br><br>(fully managed) |Doris |Integrated storage and compute |Supported only in version 2.1.8. |
