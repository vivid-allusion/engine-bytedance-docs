---
title: "VCI event monitoring overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-event-monitoring-overview"
---

Event monitoring is used to record and display VCI information. When a VCI triggers a system event, you can promptly view the event details and process it.

<span id=".5LqL5Lu254q25oCB"></span>
## Event status


|Status |Displayed in the console |Attribute |Description |
|---|---|---|---|
|Scheduled |Scheduled |Intermediate status |The operation and maintenance task is scheduled but has not been executed. |
|Executed |Completed |Stable status |The operation and maintenance task has been executed. |


<span id=".5ZG95ZCN6KeE5YiZ"></span>
## Naming rules

VCI event types and event names always follow the naming rules below. Once you know these rules, you can quickly understand an event's meaning from its name.


* Event type: `<Event cause>.<Impact on resource>`

   For example, SystemMaintenance.PodEvicted indicates that a VCI pod has been evicted due to system O&M tasks.

* Event content: `<Event cause>.<Impact on resource>.<Event status>`

   For example, `SystemMaintenance.PodEvicted.Executed` indicates that a VCI pod has been evicted due to operation and maintenance tasks, and the event is in the executed state.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For event types and event names supported by VCI, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-event-types">Summary of VCI event types</a>.</div>
