---
title: "Scheduled maintenance window overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview_of_Planned_Maintenance_Windows"
---

Scheduled maintenance window is a flexible, automated O&M feature for ECS instances offered by BytePlus. It is specifically designed for [scheduled O&M events](https://docs.byteplus.com/en/docs/ecs/Event-type-overview#.6K6h5YiS5YaF6L-Q57u05LqL5Lu2), allowing automatic handling of O&M events during your off\-peak hours.

As a long\-term rule configuration, this feature supports batch selection of resources by tag or project, flexible maintenance cycle configuration (daily or weekly), and automated authorization triggered by events. This enables unified management of O&M periods, effectively addressing issues such as delayed manual authorization, instance downtime, and inefficient configuration. This enhances ECS instance stability while minimizing the O&M impact on your business.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This feature is in Beta. If you need a trial, <a href="https://console.byteplus.com/workorder/create">submit a ticket </a>or contact your account manager.</div>


* <div data-tips="true" data-tips-type="default">Without a scheduled maintenance window, when an event is generated and in the <strong>Inquiring</strong> state, you need to authorize BytePlus to perform the O&M operation manually. For specific steps.</div>



<span id="1WxVOi17"></span>
## Concepts


|Concept |Description |
|---|---|
|O&M operation |The scheduled operation (such as instance redeployment) for the target event during the scheduled maintenance period. |
|Automatic authorization |By creating a scheduled maintenance window, you authorize BytePlus to perform O&M operations for corresponding scheduled O&M events. After configuration, manual authorization is no longer required when an event is triggered. |


<span id="LQjyQQCF"></span>
## How a scheduled maintenance window works

<span id="BzyQ4xuf"></span>
### Event generated before the scheduled window cycle starts

If an event is generated **before** the start time of the scheduled maintenance window, the system defers instance redeployment until the scheduled window cycle starts. The cycle can be configured as "Weekly" or "Daily". The logic is consistent across both options. We use "Weekly" as an example below:

For example, if an event is generated on `Monday`, and the scheduled maintenance window cycle is from `Friday 00:00` to `Saturday 02:00`, BytePlus will perform the O&M operation (instance redeployment) for that event between `Friday 00:00` and `Saturday 02:00`.

<span id="EsYJDRbr"></span>
### Event generated **within** the scheduled window cycle

If an event is generated within the current window cycle, the O&M operation (instance redeployment) will be executed within the current window. For example, if an event is generated between **00:00 and 01:30**, the operation will be performed during **that day's** maintenance period of **00:00\-01:30**.

<span id="7yGrysZD"></span>
## **Maintenance action and O&M event of a scheduled maintenance window**

For maintenance action and O&M event details of a scheduled maintenance window, see [Scheduled O&M events](https://docs.byteplus.com/en/docs/ecs/Event-type-overview#.6K6h5YiS5YaF6L-Q57u05LqL5Lu2).
