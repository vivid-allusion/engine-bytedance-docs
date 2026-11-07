---
title: "Configuring event monitoring notifications"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications"
---

When ECS instances and dedicated hosts trigger monitoring events, you can receive event notifications via the message center and Cloud Monitor.


> * Whether you have configured to receive event notifications or not, this does not affect events being displayed in the ECS console. For information about querying and handling events in the console, refer to [Querying and handling events​](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events).

> * You can receive event notifications via the message center and Cloud Monitor in a more timely and convenient manner than in the console.


<span id=".6YCa55-l5pa55byP"></span>
## Notification method

The comparisons of message notifications via the message center and Cloud Monitor are as follows. You can choose one notification method as needed or enable both methods.


|Notification method |Notification channels |Description |
|---|---|---|
|[Message center notification](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications?lang=zh&TagIDs=2,288,70,69#2iPm0nJi) |* Internal message<br><br>* email<br><br>* SMS<br><br>* Voice message<br><br>* Feishu message<br><br>* WeCom<br><br>* DingTalk |This method is simple and user\-friendly. It covers common notification channels and meets your daily needs to receive notifications. |
|[Cloud Monitor notification](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#.5LqR55uR5o6n6YCa55-l) |* Email<br><br>* Phone call<br><br>* SMS<br><br>* Alert callback<br><br>* Message queue Kafka<br><br>* Log service<br><br>* Orchestration |This method involves a longer configuration process, but offers more notification channels. Through this method, you can also configure rules such as notification severity levels and effective time periods. This can meet your needs for integrating event notifications and quickly locating cloud product resources with exceptions. |


<span id="2iPm0nJi"></span>
## Message center notification

[Certain events](https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature?lang=zh#DW3MsTFY) are subscribed to by default with notification methods preconfigured. For other events, access the [Message Center](https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods) to subscribe to event messages and configure notification methods. After this, you can receive event notifications.


* Relation between event and message type

   
   |Event type |Level 1 event type |Level 2 event type |
   |---|---|---|
   |Status change event |Product message |Product Release Notification |
   ||Operation message |Operation Notification |
   |Scheduled operations events |Operation message |Operation Notification |
   |Unexpected operation and maintenance events |Operation message |Operation Notification |
   |Task status class event |Product message |Product Status Remind |
   |Fees warning |Operation message |Operation Notification |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For event categories and event descriptions, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Event-type-overview?lang=zh">Event type summary</a>.   </div>
   

* [Configure the message recipient](https://docs.byteplus.com/en/docs/message_center/How-to-Configure-Message-Recipients): This allows notification messages to be automatically sent to you via internal message, email, SMS, and other channels when an instance triggers a target event.

* Configure message robots: This allows notification messages to be automatically sent to you via Feishu robots, WeCom robots, DingTalk group robots, and other channels when an instance triggers a target event.


<span id=".5LqR55uR5o6n6YCa55-l"></span>
## Cloud Monitor notification

To push alerts to designated personnel via custom channels when an instance triggers a specified monitoring event, you can use Cloud Monitor event alerts. Specifically, you can configure alert rules, recipients, and notification methods to improve configuration granularity. For more information, refer to [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule) and [Managing event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule).

<span id="1GNvfNAF"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> System Events".

3. In the top menu bar, select the region and project of your business.

4. Click the "Cloud Monitor Notification" button to configure relevant event alert rules, recipients, and notification channels. For more information, refer to [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule) and [Managing event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Select "ecs" for "Resource type".   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateSubscription](https://docs.byteplus.com/en/docs/ecs/CreateSubscription)

* [ModifySubscriptionEventTypes](https://docs.byteplus.com/en/docs/ecs/ModifySubscriptionEventTypes)

* [DescribeSubscriptions](https://docs.byteplus.com/en/docs/ecs/DescribeSubscriptions)
