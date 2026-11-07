---
title: "Alert principles"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-mechanism"
---

This topic describes the detailed process of alert triggering, execution, and recovery after an alert policy is created.

<span id="4687a9a8"></span>
## Alerting process

<span id="1f829541"></span>
### Metric thresholds reached

For example, the alert trigger conditions in an alert policy are as follows:


* Average disk read/write bandwidth exceeds 58 MiB/s for one cycle.

* Maximum disk read/write bandwidth exceeds 58 MiB/s for one cycle.

* Minimum disk read/write bandwidth exceeds 58 MiB/s for one cycle.


The alert process details are as follows:


|Trigger condition |Metric |<div style="text-align: center"><br>Alert detection time</div><br> ||||||||||Alert recovery |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|||12:04 |12:05 |12:06 |12:07 |12:08 |12:09 |12:10 |12:11 |··· |12:15 ||
|Maximum disk read/write bandwidth exceeds 58 MiB/s for one cycle |Maximum |Not higher than the threshold |Exceeds the threshold, triggering an alert |||||||||The metric remains above the threshold, keeping the alert from recovery |
|Average disk read/write bandwidth exceeds 58 MiB/s for one cycle |Average |Not higher than the threshold ||Exceeds the threshold, triggering an alert |||||Below the threshold ||No subsequent alert is triggered for five consecutive cycles, leading to alert recovery |A recovery notification is sent using the specified method at 12:15 |
|Minimum disk read/write bandwidth exceeds 58 MiB/s for one cycle |Minimum |Not higher than the threshold ||||||||||No alert triggered |


<span id="9c4f7f6f"></span>
### Cycle\-over\-cycle comparison thresholds reached

For example, the alert trigger conditions in an alert policy are as follows:


* Average disk read/write bandwidth has a 10% cycle\-over\-cycle rise or drop for three consecutive cycles.


The alert process details are as follows:


|Trigger condition |Metric |<div style="text-align: center"><br>Alert detection time</div><br> |||||||Alert recovery |
|---|---|---|---|---|---|---|---|---|---|
|||12:04 |12:05 |12:06 |12:07 |12:08 |... |12:12 ||
|Average disk read/write bandwidth has a 10% cycle\-over\-cycle rise or drop for three consecutive cycles. |Cycle\-over\-cycle average comparison |The metric meets the alert threshold for fewer than three consecutive cycles, failing to trigger an alert ||The metric reaches the alert threshold for three consecutive cycles, triggering an alert. ||Does not reach the alert threshold. ||No subsequent alert is triggered for five consecutive cycles, leading to alert recovery. |Send recovery notifications using the specified method. |


<span id=".5p6B56uv5Zy65pmv6K-05piO"></span>
## Edge cases

Cycle\-over\-cycle change = (nth cycle \- (n\-1)th cycle) / (n\-1)th cycle


|Data for cycle n\-1 |Data for cycle n |Descriptions |
|---|---|---|
|0 |Not zero |The cycle\-over\-cycle change is infinite and exceeds any threshold setting. The trigger condition is met in this cycle. |
|No data reported |No data reported or any value reported |Unable to calculate the cycle\-over\-cycle change. The trigger condition is not met in this cycle. |
|No data reported or any value reported |No data reported |Unable to calculate the cycle\-over\-cycle change. The trigger condition is not met in this cycle. |
|n |0 |The cycle\-over\-cycle change is \-1 (\-100%). The trigger condition is not met in this cycle. |
|0 |0 |No cycle\-over\-cycle change. The trigger condition is not met in this cycle. |


Period\-over\-period change from yesterday = (Value for the current cycle \- Value for the same cycle of yesterday) / Value for the same cycle of yesterday

Period\-over\-period change from the last week = (Value for the current cycle \- Value for the same cycle last week) / Value for the same cycle last week


|Data for the same cycle yesterday / the same cycle last week / the previous cycle |Data within the current cycle |Descriptions |
|---|---|---|
|0 |Not zero |The period\-over\-period change is infinite and exceeds any threshold setting. The trigger condition is met in this cycle. |
|No data reported |No data reported or any value reported |Unable to calculate the period\-over\-period change. The trigger condition is not met in this cycle. |
|No data reported or any value reported |No data reported |Unable to calculate the period\-over\-period change. The trigger condition is not met in this cycle. |
|n |0 |The period\-over\-period change is \-1 (\-100%). The trigger condition is not met in this cycle. |
|0 |0 |No change from the period\-over\-period comparison. The trigger condition is not met in this cycle. |
