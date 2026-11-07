---
title: "Event monitoring"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/event-monitoring"
---

Cache for Redis supports viewing event monitoring information for instance via the Cloud Service Event to help you promptly identify, locate and resolve related issues. Such information includes time of event occurrence, event source, event name and event details. This article introduces the events that Redis supports monitoring and the operation steps related to event management.

<span id=".5pSv5oyB55uR5o6n55qE5LqL5Lu2"></span>
## Supported monitoring events

Cache for Redis currently supports monitoring of exceptions and scheduled maintenance. The specific event names and descriptions for each type of event are shown in the table below.


|Event type |Event name |Event code |Description |
|---|---|---|---|
|Exception |InstanceNotAvailable |redis:Exception:InstanceNotAvailable |An event is triggered when an instance becomes unavailable due to any fault. |
||InstanceFailover |redis:Exception:InstanceFailover |This event is triggered when an instance encounters a failover (failover). |
||ReadOnlyNodeDrop |redis:Exception:ReadOnlyNodeDrop |An event is triggered when a read\-only node fails and is removed from service (excluding removal caused by active changes).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only instances with the read/write splitting function enabled support this event alarm. For more details about read/write splitting, refer to <a href="https://docs.byteplus.com/en/docs/redis/set-read-write-splitting">Setting read/write splitting.</a></div><br> |
|Maintenance |InstanceSwitchover |redis:Maintenance:InstanceSwitchover |This event is triggered when an instance encounters a failover (task switchover). |


<span id=".5p-l55yL5LqL5Lu255uR5o6n"></span>
## Viewing event monitoring

You can view Redis events via [Cloud service event](https://console.byteplus.com/cloud-monitor/event/center). The information displayed includes time of event occurrence, event source, event name and event details.

For more information about how to view event monitoring, refer to [Viewing cloud service events](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When viewing monitoring event information on the <strong>Cloud service event</strong> page, you need to select the product name as <strong>Redis</strong>.</div>


* <div data-tips="true" data-tips-type="tip">On the event list page, you can locate the target time and click <strong>Details</strong> in the <strong>Actions</strong> column to view details of the event so that you can locate the reason for event triggering. To further locate the fault, please <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support.</div>



<span id=".5Yib5bu65LqL5Lu26KeE5YiZ"></span>
## Creating event rules

You can configure alarming rules for events for specified cloud services. When an event that meets the corresponding rule occurs, you will receive alarm notifications at the earliest opportunity, which helps you quickly locate faulty cloud service resources.

For specific procedures to create event rules, refer to [Creating event rule](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When configuring the <strong>Event rule</strong> on the <strong>Create event rule</strong> page, you need to select the <strong>Resource type</strong> as <strong>Redis</strong>.</div>


* <div data-tips="true" data-tips-type="tip">After the event rule is successfully created, you can manage it in the event rule list of Cloud Monitor, including modifying the event rule, or disabling, enabling, or deleting it. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule">Managing event rule</a>.</div>
