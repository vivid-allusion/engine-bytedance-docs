---
title: "Scaling solution guide"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/scaling-solution-guide"
---

Cache for Redis supports modifications to instance configurations, including horizontal scaling (increasing or decreasing the number of instance shards) and vertical scaling (upgrading or downgrading node specifications). You can determine when changes are needed and how to select the appropriate action based on the information below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification">Modifying instance specifications</a>.</div>



|Reconfiguration ||Supported instance or architecture types ||||Scenario |
|---|---|---|---|---|---|---|
|||Primary\-secondary instance ||Single\-node instance |||
|||Sharding cluster enabled |Sharding cluster disabled |Sharding cluster enabled |Sharding cluster disabled ||
|Upscaling |Horizontal upscaling<br><br>(increasing the number of shards) |✔️ |❌ |✔️ |❌ |You can perform upscaling, if the CPU load of the instance server node is relatively high or the total memory capacity is insufficient.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend that you perform upscaling tasks during off\-peak hours to reduce the impact on business operations.</div><br> |
||Vertical upscaling<br><br>(upgrading node specifications) |✔️ |✔️ |✔️ |✔️ ||
|Downscaling |Horizontal downscaling<br><br>(decreasing the number of shards) |✔️ |❌ |✔️ |❌ |Free up surplus memory capacity through downscaling.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend that you perform downscaling tasks during off\-peak hours to reduce the impact on business operations.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Before downscaling, it is necessary to ensure that the memory used for instance does not exceed 85% of the total capacity of the new memory.</div><br> |
||Vertical downscaling<br><br>(downgrading node specifications) |✔️ |✔️ |✔️ |✔️ ||
