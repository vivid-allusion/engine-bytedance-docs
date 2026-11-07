---
title: "Configuring resource capacity alerts"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Configure_resource_capacity_alerts"
---

You can configure quota alerts for your CR resources based on usage quantity or percentage. These alerts provide early warnings, allowing you to manage resource capacity proactively and prevent task failures due to resource exhaustion.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Currently, only <strong>Standard Edition </strong>instances support this feature.</div>


* <div data-tips="true" data-tips-type="default">For standard quota details of each type of resource, see <a href="https://docs.byteplus.com/en/docs/cr/limits">Limits</a>.</div>



<span id="siy6YBda"></span>
## Background

Currently, capacity alerts are supported only for the following resources. If the quantity or percentage of **namespaces** or **OCI artifact repositories** in any Standard Edition instance under your account reaches the threshold defined in an alert rule, alert notifications can be sent via email, SMS, site message, or other channels.


|Resource type |Alert configuration parameter |
|---|---|
|OCI artifact repository |repoMaxRatioEnterpriseStandard |
|Namespace |namespaceMaxRatioEnterpriseStandard |


<span id="IsMKaFAo"></span>
## Procedure

The following example shows how to configure an alert for 85% quota usage of OCI artifact repositories within an instance.


1. Log in to the [Quota Center console](https://console.byteplus.com/quota/productList).

2. On the Product list page, select **cr**.

3. Select the target alert configuration parameter and region and click **Create alarm**.

4. Configure alert parameters.

   
   |Configuration item |Description |
   |---|---|
   |Alarm name |The name of the custom alert. |
   |Alarm type |Two types are supported: usage alert and balance alert In this example, **usage alert** is selected.<br><br><br>* Usage alert: Sets an alert based on the quantity or percentage of resources already used.<br><br>* Balance alert: Sets an alert based on the remaining quantity or percentage of resources. |
   |Alarm threshold |You can set the threshold using either a numerical value or a percentage. In this example, the **Percentage** option is selected. |
   |Notification type |By default, notifications are sent via email, SMS, and site message.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure that the corresponding notification channels are enabled in <a href="https://console.byteplus.com/message/setting">Message center \> Message receive configuration</a> \> <strong>Quota Center Alarm</strong>. For details, see <a href="https://docs.byteplus.com/en/docs/message_center/Message-Subscription-and-Notification-Methods">Subscribing to messages and notification methods</a>.</div><br> |
   

5. Click **Submit** to complete creation.



&nbsp;

&nbsp;


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
