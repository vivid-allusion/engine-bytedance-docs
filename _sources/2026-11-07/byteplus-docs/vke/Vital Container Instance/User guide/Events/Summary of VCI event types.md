---
title: "Summary of VCI event types"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-event-types"
---

This topic summarizes the types of events that can be monitored by VCI, their descriptions, and other information.

<span id=".6K6h5YiS5YaF6L-Q57u05LqL5Lu2"></span>
## Scheduled operation and maintenance events


|Event category |Event type |Event description |Event name |Recommended operations for users |
|---|---|---|---|---|
|VCI |SystemMaintenance.PodEvicted |Pods are evicted due to system operation and maintenance tasks.<br><br><br>* Scheduled<br><br>* Executed |* SystemMaintenance.PodEvicted.Scheduled<br><br>* SystemMaintenance.PodEvicted.Executed |No action is required. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For VCI workloads, you also need to monitor the event types and event names of Vital Kubernetes Engine (VKE). For detailed information, see <a href="https://docs.byteplus.com/en/docs/vke/Event-types">Summary of VKE event types</a>.</div>
