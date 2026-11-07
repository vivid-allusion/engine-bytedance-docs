---
title: "Overview of Cloud Monitor alert configurations"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Cloud_Monitor_alerting_principles"
---

The Cloud Monitor alert configuration consists of four key configurations: resource type, alert object, trigger condition, and notification policy, along with other configurations such as notification cycle, notification aggregation policy, alert recovery notification, and project. These configurations form a complete Cloud Monitor alert rule, defining the entire logic of "which objects to monitor, which metrics to track, what conditions trigger an alert, who to notify after triggering, and through which channels."

<span id="U4y1MzgS"></span>
## Glossary


* **Resource type**: Specifies the type of cloud service that can be monitored via Cloud Monitor alerts, such as ECS and TOS. It categorizes alert objects at the top level and provides different alert rules and alert template configurations for different cloud services. This improves configuration efficiency and maintainability.

* **Alert object**: Specifies the specific instances being monitored in the alert rule, determining the effective scope of the alert. This eliminates alert blind spots and prevents irrelevant alerts.

* **Trigger condition**: Defines the rule that determines when an alert is triggered, including key information such as metrics, thresholds, periods, and severity levels.

* **Notification policy**: Specifies the methods, channels, contacts, and alert content display formats for receiving notifications when alerts of different severity levels occur and when alerts are resolved.


<span id="hffItxbj"></span>
## Resource relationships

Alert templates, preset alert templates, and object groups contain only partial alert configurations. These resources not only consolidate scattered alert settings into reusable standards but also enable quick batch creation of alert rules, reuse of best practices, and improved configuration efficiency. The key alert configuration differences across various resources are as follows:


|Key settings |Alert rules |Preset alert templates |Alert templates |Resource group |
|---|---|---|---|---|
|Resource type |✅ |✅ |✅ |✅ |
|Alert object |✅ (Some or all resources) |✅ (All resources) |❌ |✅ (Some resources) |
|Trigger condition |✅ |✅ |✅ |❌ |
|Notification policy |✅ |❌ |❌ |❌ |


<span id="UiJlBP9U"></span>
## Alert rule creation methods

Cloud Monitor provides multiple alert rule creation methods, allowing you to select the most suitable one based on your business requirements.


* **Custom creation of alert rules**: If you wish to customize alert rules for specific scenarios or have only a small number of alert rules, we recommend manually creating alert rules. This does not compromise usage efficiency and allows for fine\-grained tuning of alert configurations. For procedure and configuration details, see Method 1 in [Creating Cloud Monitor alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Cloud_Monitor_alert_rules).

* **Enable preset alert templates**: If you lack established experience in alert configuration and want to set up an alert monitoring system quickly, we recommend using the standardized alert templates officially provided for rapid implementation. When enabling preset alert templates, you only need to provide the notification policy to complete all settings in the alert rule, allowing you to create alert rules quickly based on the preset alert templates. For procedure and configuration details, see [Enabling preset alert templates of Cloud Monitor](https://docs.byteplus.com/en/docs/Observability_Platform/Enabling_Cloud_Monitor_preset_alert_templates).

* **Use custom alert templates**: If you already have established experience in alert configuration and want to reuse configurations within the same account while reducing duplicate creation of alert rules, we recommend following the steps below to create alert templates and apply them to object groups, standardizing and operationalizing the relevant experience.

   1. [Create alert templates](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Cloud_Monitor_alert_templates): Create an alert template by resource type, consolidating configurations such as alert trigger conditions into an alert template for quick reuse.

   2. [Create object groups](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_object_groups): Add alert objects from multiple services and regions to the same group for batch management of alert resources.

   3. [Apply alert templates to object groups](https://docs.byteplus.com/en/docs/Observability_Platform/Applying_alert_templates_to_object_groups): Combine an alert template and an object group that share the same resource type, and supplement a notification policy when applying the template to complete all configurations of the alert rule.

* **Import/export alert rules via JSON**: If suitable alert rules already exist in other projects and you wish to batch copy alert rules across accounts, regions, or projects, we recommend using the import/export feature to export Cloud Monitor alert rules from other projects and then import them into the Cloud Monitor alert rules of the current project. For procedure and configuration details, see Method 2 in [Creating Cloud Monitor alert rules](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_Cloud_Monitor_alert_rules).


<span id="6PtkD8wU"></span>
## Alert principles

The detailed process of alert triggering, execution, and recovery after a Cloud Monitor alert rule is created is as follows.

<span id="yOKJfFvU"></span>
### Metric thresholds reached

For example, the alert trigger conditions in an alert policy are as follows:


* Average disk read/write bandwidth exceeds 58 MiB/s for one cycle.

* Maximum disk read/write bandwidth exceeds 58 MiB/s for one cycle.

* Minimum disk read/write bandwidth exceeds 58 MiB/s for one cycle.


Raw metric values are reported at 30\-second intervals and alert detection is performed once per minute. During alert detection, raw data from the past 1 minute is aggregated using max, avg, and min functions to generate the corresponding maximum, average, and minimum values.

For example, the average value at 12:06 is calculated by averaging the two data points collected at 12:05:30 and 12:06:00. The maximum and minimum values follow the same calculation logic.

The alert process details are as follows:


|Trigger condition |Metric |<div style="text-align: center"><br>Alert detection time</div><br> ||||||||||Alert recovery |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|||12:04 |12:05 |12:06 |12:07 |12:08 |12:09 |12:10 |12:11 |··· |12:15 ||
|Maximum disk read/write bandwidth exceeds 58 MiB/s for one cycle |Maximum |Not higher than the threshold |Exceeds the threshold, triggering an alert |||||||||The metric remains above the threshold, keeping the alert from recovery |
|Average disk read/write bandwidth exceeds 58 MiB/s for one cycle |Average |Not higher than the threshold ||Exceeds the threshold, triggering an alert |||||Below the threshold ||No subsequent alert is triggered for five consecutive cycles, leading to alert recovery. |A recovery notification is sent using the specified method at 12:15 |
|Minimum disk read/write bandwidth exceeds 58 MiB/s for one cycle |Minimum |Not higher than the threshold ||||||||||No alert triggered |


<span id="xOlEAji5"></span>
### Cycle\-over\-cycle comparison thresholds reached

For example, the trigger conditions configured by the user in an alert policy are: Average disk read/write bandwidth has a 10% cycle\-over\-cycle rise or drop for three consecutive cycles.

Raw metric values are reported at 30\-second intervals and alert detection is performed once per minute. During alert detection, raw data from the current cycle (past 1 minute) is aggregated using the avg function to calculate the average value. The average value is then used to calculate the cycle\-over\-cycle change rate against the average value from the previous cycle.

The alert process details are as follows:


|Trigger condition |Metric |<div style="text-align: center"><br>Alert detection time</div><br> |||||||Alert recovery |
|---|---|---|---|---|---|---|---|---|---|
|||12:04 |12:05 |12:06 |12:07 |12:08 |... |12:12 ||
|Average disk read/write bandwidth has a 10% cycle\-over\-cycle rise or drop for three consecutive cycles. |Cycle\-over\-cycle average comparison |The metric meets the alert threshold for fewer than three consecutive cycles, failing to trigger an alert. ||The metric reaches the alert threshold for three consecutive cycles, triggering an alert. ||Does not reach the alert threshold. ||No subsequent alert is triggered for five consecutive cycles, leading to alert recovery. |Send recovery notifications using the specified method. |


<span id="PePCc7CQ"></span>
### Edge cases

Cycle\-over\-cycle change = (nth cycle \- (n\-1)th cycle) / (n\-1)th cycle


|Data for cycle n\-1 |Data for cycle n |Description |
|---|---|---|
|0 |Not 0 |The cycle\-over\-cycle change is infinite and exceeds any threshold setting. The trigger condition is met in this cycle. |
|No data reported |No data reported or any value reported |Unable to calculate the cycle\-over\-cycle change. The trigger condition is not met in this cycle. |
|No data reported or any value reported |No data reported |Unable to calculate the cycle\-over\-cycle change. The trigger condition is not met in this cycle. |
|n |0 |The cycle\-over\-cycle change is \-1 (\-100%). The trigger condition is not met in this cycle. |
|0 |0 |No cycle\-over\-cycle change. The trigger condition is not met in this cycle. |


Period\-over\-period change from yesterday = (Value for the current cycle \- Value for the same cycle of yesterday) / Value for the same cycle of yesterday

Period\-over\-period change from the last week = (Value for the current cycle \- Value for the same cycle last week) / Value for the same cycle last week


|Data for the same cycle yesterday / the same cycle last week / the previous cycle |Data within the current cycle |Description |
|---|---|---|
|0 |Not 0 |The period\-over\-period change is infinite and exceeds any threshold setting. The trigger condition is met in this cycle. |
|No data reported |No data reported or any value reported |Unable to calculate the period\-over\-period change. The trigger condition is not met in this cycle. |
|No data reported or any value reported |No data reported |Unable to calculate the period\-over\-period change. The trigger condition is not met in this cycle. |
|n |0 |The period\-over\-period change is \-1 (\-100%). The trigger condition is not met in this cycle. |
|0 |0 |No change from the period\-over\-period comparison. The trigger condition is not met in this cycle. |


<span id="xok5tgNt"></span>
##
