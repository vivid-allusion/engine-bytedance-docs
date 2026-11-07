---
title: "Creating aggregation policies"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_aggregation_policies"
---

An aggregation policy is primarily used to configure the aggregation cycle for alerts. It groups a batch of alerts for notification, preventing alert storms caused by a large number of alert messages generated in a short period when alerts are triggered frequently. This topic describes how to create an aggregation policy.

<span id="graXdcZR"></span>
## Background

If you have not created an aggregation policy, the system applies the default policy. The aggregation parameters for each severity level are listed below.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The default policy built in by the system cannot be modified or deleted.</div>



|Level |Aggregate dimension |Alert group first wait time |Alert grouping follow\-up wait time |Recurring notification interval |Notification down |
|---|---|---|---|---|---|
|Critical |`rule_id`, `region` |30 seconds |1 minute |1 hour |Disabled |
|Warning |`rule_id`, `region` |1 minute |3 minutes |2 hours |Disabled |
|Notification |`rule_id`, `region` |1 minute |5 minutes |4 hours |Disabled |


<span id="EleRGv6q"></span>
## Limits


* Aggregation policies currently apply only to the VMP service.

* You can create up to 1,000 aggregation policies. Each policy can contain up to 30 aggregation groups, and up to 30 grouping fields are supported.


<span id="xThT3JoZ"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select "**Alert Center \-\> Aggregation Policy**" to go to the "Aggregation Policy" page.

3. Click **Create an aggregation strategy ** and configure the aggregation policy parameters as needed.

   
   |Parameter |Description |
   |---|---|
   |Policy name |Specify a name for the aggregation policy, which serves as a unique identifier. Duplicate names are not allowed. |
   |Level |Currently, you can configure separate aggregation policies for alerts of three severity levels (Critical, Warning, and Notice). You can also configure an "All" level as a fallback. For example, if you configure an aggregation policy only for alerts of the "Critical" and "All" severity levels, the system still aggregates the "Warning" and "Notice" alerts and sends the notification with the highest level.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you do not configure aggregation policies for alerts of all three severity levels (Critical, Warning, and Notice), you are required to configure an aggregation policy for the "All" level.</div><br> |
   |Aggregate dimension |The aggregation dimensions of alert notifications. You configure this parameter via alert Label Keys. For example, if you set `rule_id `and `region`, alerts are aggregated by rule and region.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><code>rule_id</code> and <code>region</code> are required and cannot be deleted. During actual use, you can add other dimensions as needed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the aggregation dimension configuration is completed, when alert notifications are received, the system will create a group to aggregate notifications with the same Key for management. <strong>This process completes in the system background and is not visible to you</strong>.</div><br> |
   |Alert group first wait time |The waiting time of the first alert after the group is created in the system background. For example, if you set this parameter to 10 seconds, the first notification is sent 10 seconds after the group is created. |
   |Alert grouping follow\-up wait time |The waiting time before a notification is sent for the second and subsequent alerts after a group is created in the system background. For example, if you set this parameter to 20 seconds, the second and subsequent notifications within the same alert group will be sent after a 20\-second delay. |
   |Recurring notification interval |Restricts the reporting interval of repeatedly received notifications. For example, if the recurring notification interval is 1 minute, notifications for alert A are sent once per minute.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">New notifications are not subject to this configuration. Specifically, the first generated alert is not regarded as a duplicate notification and will be reported directly after the initial waiting period and the subsequent waiting period of the alert group.</div><br> |
   |Notification down |Disabled by default. After you enable this feature, you can configure the frequency reduction mode and the maximum notification interval in this mode.<br><br><br>* **Down mode**: The mode of notification frequency reduction. Currently, only doubling the interval is supported. When you select this mode, the actual notification interval is equal to twice the repeat notification interval.<br><br>* **Maximum notification interval after frequency reduction**: The upper limit of the notification interval when frequency reduction is enabled. With frequency reduction enabled, the maximum notification interval cannot exceed the specified value of this parameter.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Notification frequency reduction is not supported for "Critical" alerts.</div><br> |
