---
title: "CompactionScore too high"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_compactionscore_too_high"
---

<span id="aa8fc185"></span>
## Use cases


* Applicable when the cluster CompactionScore is too high, resulting in degraded read and write performance. This can be mitigated by manually forcing a Compact operation.

* The stop\-loss approach should be determined based on a comprehensive assessment of cluster resource utilization, customer write model, and frequency. This document only provides the procedure for manually triggering Compact.


<span id="69498efb"></span>
## Applicable versions


|**Product type** |**Engine** |**Deployment method** |**Applicable versions** |
|---|---|---|---|
|Serverless instance<br><br>(fully managed) |StarRocks |Storage and compute separation |Only supported in version 3.2.12 |
|||Integrated storage and compute |— |


<span id="a7337744"></span>
## Procedure
