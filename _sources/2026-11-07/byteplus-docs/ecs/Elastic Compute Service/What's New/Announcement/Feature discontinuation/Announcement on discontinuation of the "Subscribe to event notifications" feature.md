---
title: "Announcement on discontinuation of the \"Subscribe to event notifications\" feature"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature"
---

Dear BytePlus users, to optimize product experience, BytePlus will officially discontinue the "Subscribe to event notifications" feature of ECS service at **00:00 on December 9, 2025** (UTC+8).

> After this feature is discontinued, you will no longer be able to access, subscribe to, or cancel event notifications on the ECS console.


<span id="Yd4e0pXY"></span>
## Reason for discontinuation

The current configuration process for the "Subscribe to event notifications" feature of ECS is complex, and its core capabilities overlap with the subscription configurations of message center and Cloud Monitor. To simplify the configuration logic and improve usage efficiency, BytePlus has decided to discontinue this feature.


|Original and current processes |Description |
|---|---|
|Original process for subscribing to event notifications |1. Subscribe to event notifications in the ECS console.<br><br>2. Subscribe to messaging and notification methods in the message center console, or configure event notification methods and channels in the Cloud Monitor console. |
|Current process for subscribing to event notifications |Subscribe to messaging and notification methods in the message center console, or configure event notification methods and channels in the Cloud Monitor console. |


<span id="grtQAKXl"></span>
## Current policy and operation guide for subscribing to event notifications

After the "Subscribe to event notifications" feature of ECS is discontinued, the handling of previously subscribed event notifications, subsequent subscription policy, and operation guide are as follows:

<span id="oOsITW9l"></span>
### **Policy on subscribing to event notifications**


|Event |Policy on subscribing to event notifications |Policy on cancelling event notification |
|---|---|---|
|Subscribed events |After this feature is discontinued, the policies for the original subscribed event are adjusted as follows:<br><br><br>* For [default subscribed events](https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature?lang=zh#DW3MsTFY), event notifications will continue to be sent normally. For non\-default subscribed events, subsequent event notifications will be automatically canceled, and you need to go to [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule) to resubscribe to such events.<br><br>* For events other than the [default subscribed events](https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature?lang=zh#DW3MsTFY), you need to go to [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule) to subscribe to messaging and notification methods. Only after this, you can receive event notifications. |<div style="text-align: center"><br></div><br><br><br>Go to message center or [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule) to cancel event notification. |
|Unsubscribed events |After this feature is discontinued, you must go to message center or [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule) to subscribe to messaging and notification methods. Only after this, you can receive event notifications.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For some events, the notification methods of SMS, email, and internal message are enabled by default. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature?lang=zh#DW3MsTFY">Default subscribed events</a>.</div><br> ||


<span id="V95jzTtZ"></span>
### **Operation guide**


* Subscription in Message center: recommended for scenarios requiring daily notifications. Learn more.

* Subscription in Cloud Monitor: recommended for scenarios requiring refined configurations. For specific operations, refer to [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).


<span id="DW3MsTFY"></span>
## Default subscribed events

In the message center, subscription methods for the following events have been enabled by default. You can change the subscription status or notification channel in the message center based on your needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The "\*" in the table below indicates the default notification method subscribed in the message center.</div>


* <div data-tips="true" data-tips-type="default">For events other than the default subscriptions, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Event-type-overview">Event type overview</a>.</div>




|**Event type** |Event name |**ECS event & status** |**Level 1 event type** |**Level 2 event type** |**Event notification methods (\* indicates default method)**  |
|---|---|---|---|---|---|
|Status change event |SpotInstanceInterruption.Delete (Spot instance interrupted, instance released) |SpotInstanceInterruption_Delete:Scheduled |Product message<br><br> |Product Release Notification<br><br> |SMS\*, email\*, internal message\*, voice message, external Feishu, internal Feishu<br><br> |
||ServerMigrationTask (Server migration task) |* ServerMigrationTask:Executing<br><br>* ServerMigrationTask:Pending<br><br>* ServerMigrationTask:Recovered<br><br>* ServerMigrationTask:Succeeded<br><br>* ServerMigrationTask:Failed |Operation message |Operation Notification |SMS\*, email\*, internal message\*, external Feishu, WeCom, DingTalk, Slack, internal Feishu |
||ServerMigration.FirstSync (Server migration, full data synchronization) |* ServerMigration.FirstSync.Succeeded<br><br>* ServerMigration.FirstSync.Failed ||||
||ServerMigration.AdditionalSync (Server migration, incremental data synchronization) |* ServerMigration.AdditionalSync:Succeeded<br><br>* ServerMigration.AdditionalSync:Failed ||||
|Scheduled operations events |SystemMaintenance.Redeploy (Instance redeployment due to system maintenance) |* SystemMaintenance.Redeploy:Inquiring<br><br>* SystemMaintenance.Redeploy:Succeeded<br><br>* SystemMaintenance.Redeploy:Failed |Operation message |Operation Notification |SMS\*, email\*, internal message\*, external Feishu, WeCom, DingTalk, Slack, internal Feishu |
||InfrastructureUpgrade.Redeploy (Instance redeployment due to infrastructure upgrade) |* InfrastructureUpgrade.Redeploy:Inquiring<br><br>* InfrastructureUpgrade.Redeploy:Succeeded ||||
|Unexpected operation and maintenance events |SystemFailure.Reboot (Instance restart due to system failures) |* SystemFailure.Reboot:Succeeded<br><br>* SystemFailure.Reboot:Failed ||||
||SystemFailure.Redeploy (Instance redeployment due to system failures) |* SystemFailure.Redeploy:Failed<br><br>* SystemFailure.Redeploy:Succeeded<br><br>* SystemFailure.Redeploy:Inquiring ||||
||SystemFailure.Stop (Instance stop due to system failure) |SystemFailure.Stop:Succeeded ||||
||DiskErrorDetected (Hard disk error) |DiskErrorDetected:Inquiring ||||
||DiskError.Redeploy (Instance redeployment due to hard disk error) |DiskError.Redeploy:Succeeded ||||
||DiskError.ReplaceDisk (Hard disk replacement due to exception) |DiskError.ReplaceDisk:Succeeded ||||
||GpuRiskDetected (GPU risk detected) |GpuRiskDetected:Succeeded ||||
||InstanceFileSystemFailure.StopAndRepair (Downtime repair due to file system exception) |* InstanceFileSystemFailure.StopAndRepair:Inquiring<br><br>* InstanceFileSystemFailure.StopAndRepair:Succeeded<br><br>* InstanceFileSystemFailure.StopAndRepair:Failed ||||
||InstanceFailure (Instance exception due to operating system errors) |InstanceFailure:Succeeded ||||
||InstanceOOM (Instance memory OOM) |InstanceOOM:Succeeded ||||
|Fees warning |AccountUnbalanced.Stop (Instance stop due to account arrears) |AccountUnbalanced.Stop:Succeeded ||||
||AccountUnbalanced.Delete (Instance release due to account arrears) |AccountUnbalanced.Delete:Succeeded ||||
|Task status class event |ElasticScheduledInstance.Create (Creation of ESI order) |* ElasticScheduledInstance.Create:Failed<br><br>* ElasticScheduledInstance.Create:Succeeded |Product message |Product Status Remind |SMS\*, email\*, internal message\*, voice message, external Feishu\*, WeCom, DingTalk, internal Feishu |
||ElasticScheduledInstance.Deliver (Delivery of ESI order) |* ElasticScheduleInstance.Deliver:Scheduled<br><br>* ElasticScheduledInstance.Deliver:Failed<br><br>* ElasticScheduledInstance.Deliver:Executing<br><br>* ElasticScheduledInstance.Deliver:Succeeded<br><br>* ElasticScheduledInstance.Deliver:Pending ||||
||ElasticScheduledInstance.AutoReleaseAt (Auto release of ESI) |* ElasticScheduledInstance.AutoRelease:Scheduled<br><br>* ElasticScheduledInstance.AutoRelease:Executing<br><br>* ElasticScheduledInstance.AutoRelease:Succeeded ||||


<span id="50cUfYLo"></span>
## Impact on you

The discontinuation of this feature is primarily for simplifying the operational logic of event subscription. This does not affect the normal use of ECS instance event feature, but may affect message notifications for previously subscribed non\-[default events](https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature?lang=zh#DW3MsTFY) .  For previously subscribed non\-default events, resubscription is required. For details, refer to the [Policy on subscribing to event notifications](https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature#oOsITW9l). We sincerely apologize for any inconvenience this may cause and appreciate your understanding.

<span id="V82tmZhP"></span>
## Questions and feedback

For any questions or assistance, please contact your account manager or [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000240). Thank you for your support and understanding of BytePlus!
