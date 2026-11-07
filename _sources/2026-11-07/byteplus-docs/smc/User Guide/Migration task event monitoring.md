---
title: "Migration task event monitoring"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Migration-Job-Incident-Monitoring"
---

To help you track task status changes and reduce manual monitoring overheads in high\-volume or slow\-migration scenarios, BytePlus supports viewing migration task status and receiving task status change notifications through the event monitoring feature. Supported migration task events can be viewed in [status change events](https://docs.byteplus.com/en/docs/ecs/Event-type-overview#.54q25oCB5Y-Y5YyW5LqL5Lu2).

<span id=".5p-l6K-i6L-B56e75Lu75Yqh5LqL5Lu2"></span>
## Query migration task event

You can query migration task event information through ECS console, OpenAPI, and Cloud Monitor console. For details on operations, see [Querying and handling events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events).


* ECS console example

* Cloud Monitor console example


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a177f9ca72ed24cd356523b48baedba9.png) </span>

<span id=".6K6i6ZiF6L-B56e75Lu75Yqh5LqL5Lu26YCa55-l"></span>
## Subscribe to migration task event notification

For monitoring events triggered by a migration task, you can receive task\-related notifications via the message center and Cloud Monitor. For details, see [Receiving event notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications).


<Tabs>
<Tab zoneid="lSQqlsDkn0" title="Message center notification">
<TabTitle>Message center notification</TabTitle>

After you subscribe to specified event messages, when an instance triggers the target event, BytePlus automatically sends you notification messages via internal message, email, SMS, or other channels. The notification conveys information such as the instance name and event name. For details, see [Subscribing to event notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#.6K6i6ZiF5LqL5Lu26YCa55-l).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_98c80526ea91c8c9252a402f71ba9f91.png) </span>


</Tab>
<Tab zoneid="nRU7N1NmiM" title="Cloud Monitor notification">
<TabTitle>Cloud Monitor notification</TabTitle>

For created event rules, Cloud Monitor supports sending alert notifications to you via email, phone, SMS, alert callback, logs, and other channels. For details, see [Creating an event rule](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Select "SMC" for the parameter "Resource type".</div>



</Tab>
</Tabs>
