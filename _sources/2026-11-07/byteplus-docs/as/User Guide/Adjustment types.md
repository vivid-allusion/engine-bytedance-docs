---
title: "Adjustment types"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Adjustment-types"
---

Auto Scaling provides you with multiple adjustment types, such as manual scaling and automatic scaling. This topic describes the trigger conditions, applicable scenarios, and implementation methods for each type.


|Adjustment type |Trigger condition |Applicable scenarios |Implementation method |
|---|---|---|---|
|Triggered manually |Manually add, remove, or delete instances in the scaling group. |Applicable to scenarios where business changes are irregular and instances need to be added or removed at any time. |[Adding instances](https://docs.byteplus.com/en/docs/as/Adding-instances-manually)<br><br>[Removing](https://docs.byteplus.com/en/docs/as/Removing-instances-automatically)/[Deleting](https://docs.byteplus.com/en/docs/as/Deleting-instances-manually) instances |
|Scaling rule \- Timed execution/Periodic execution |Create scheduled or periodic tasks using scaling rules to automatically trigger adjustments at fixed times. |Applicable to business scenarios involving predictable or regular changes, such as holiday promotions or daily scheduled releases. |[Creating scheduled scaling rules](https://docs.byteplus.com/en/docs/as/Creating-a-scheduled-scaling-policy)<br><br>[Creating periodic scaling rules](https://docs.byteplus.com/en/docs/as/Creating-a-recurring-scaling-policy) |
|Scaling rule \- Alert task |Create alert tasks by using scaling rules, and dynamically adjust the number of instances by monitoring the metric data (such as the CPU usage) of instances. |Applicable to sudden or unpredictable business scenarios, such as breaking news. |[Creating alert-driven scaling rules](https://docs.byteplus.com/en/docs/as/Creating-an-alarm-scaling-policy) |
|Scaling rule \- Target tracking task |Create a target tracking task by using scaling rules. Specifically, select a monitoring metric and specify its target value. The platform will automatically calculate the number of instances to add or remove for scaling, thereby maintaining the specified monitoring metric around the target value. |Applicable to business scenarios prioritizing operational health. For example, maintain the average CPU usage of instances in the scaling group at or below 80%. |[Creating target tracking-driven scaling rules](https://docs.byteplus.com/en/docs/as/Creating-a-target-tracking-scaling-policy) |
|Health Check |When the health check feature of Auto Scaling identifies an instance exception, it automatically triggers an adjustment. |Applicable to scenarios requiring regular monitoring of instance operational status, it automatically replaces abnormal instances and prevents business disruptions caused by failure to detect abnormal instances in a timely manner. |[Instance health check](https://docs.byteplus.com/en/docs/as/Health-checks) |
|Instance count check |When the number of instances in the scaling group deviates from the configured minimum, maximum, or desired instance count, an automatic adjustment is triggered. |Applicable to scenarios with clear business performance expectations. It helps avoid continuous scaling (either scaling out or in) when trigger conditions are met, preventing high costs from excessive resource waste or business operational disruptions due to insufficient resources. |[Creating scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group) |


<span id=".6KGM5Li657G75Z6L5LyY5YWI57qn"></span>
## Adjustment type priority

Within the same scaling group, you can enable multiple adjustment types simultaneously. When the condition for any type is met, the adjustment will be executed. However, when multiple adjustment types are triggered at the same time, the adjustment triggered manually will be executed first.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All adjustment types other than those triggered manually are mutually competitive. Only the one triggered first will be executed.</div>
