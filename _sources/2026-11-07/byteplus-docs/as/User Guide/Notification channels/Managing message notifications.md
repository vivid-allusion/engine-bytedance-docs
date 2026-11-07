---
title: "Managing message notifications"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Managing_message_notifications"
---

The Auto Scaling service supports notifications of scaling results via internal messages, SMS, or email. This way, you can promptly learn about changes in the scaling group and keep track of scaling group states.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only the root user can manage the event message feature. For related operations, log in to BytePlus with the root user.</div>


* <div data-tips="true" data-tips-type="tip">Each scaling group only supports creating one message notification.</div>



<span id=".5raI5oGv6YCa55-l57G75Z6L"></span>
## Message notification type

Currently, message notifications are sent only when the following scaling activities occur:


|Scaling activity |Description |
|---|---|
|Scaling activity succeeded |An adjustment was triggered, and all target instances were added or removed. |
|Scaling activity failed |An adjustment was triggered, and not all target instances were added or removed. |
|Scaling activity denied |A scaling request was received. The trigger conditions for the adjustment were not met, so the request was denied. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Scaling groups created before July 26, 2022, have default message notifications for scaling activity success/failure. You can <a href="https://docs.byteplus.com/en/docs/as/Managing_message_notifications#.5L-u5pS55raI5oGv6YCa55-l">modify message notification settings</a> based on your needs.</div>


<span id=".566h55CG5raI5oGv6YCa55-l"></span>
## Manage message notifications

<span id=".6YWN572u5raI5oGv5o6l5pS2"></span>
### Configure message reception

To use the message notification feature, you need to configure the message delivery method and recipients on the BytePlus platform. Otherwise, message notifications may not be delivered.


1. Access BytePlus [Message center](https://console.byteplus.com/message/setting).

2. Select "Product\-Product Status Remind" and choose one or multiple notification methods based on your business requirements (internal message, email, SMS).

3. Click the "Edit" button on the right side of the "Product\-Product Status Remind" list to change message recipients.

   * Add a new recipient: Click the "Add recipient" button, enter the information of the new recipient, then click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e21c7df933d3d957b7b21e3952b34694.png) </span> button to select the contact, and click the "Confirm" button to complete the addition.

   * Remove a recipient: Uncheck the contact you want to remove, and click the "OK" button to complete the addition.

   * Modify account contact: To modify the email and password of the account contact,.


<span id=".5Yib5bu65raI5oGv6YCa55-l"></span>
### Create message notifications

Currently, you can create message notifications by using one of the following methods based on your business requirements.


* Method 1: You can select one or multiple message notification methods when [creating a scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group). Once the group is created, the configured notifications take effect immediately.

* Method 2: If you did not select any message notification method when [creating a scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group), you can refer to the following steps to enable message notifications.

   1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

   2. In the top menu bar, select the project and region of the target resource.

   3. Click the name of the scaling group and select the "Notify" tab.

   4. Click the "Create message notification" button to select one or multiple notification events.

   5. Click the "Confirm" button to complete the operation.


<span id=".5L-u5pS55raI5oGv6YCa55-l"></span>
### Modify message notifications

Modify message notification events of a scaling group based on your needs. The changes take effect immediately.


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Notify" tab.

4. Click the "Modify" button on the right side of the message notification list and reselect notification events.

5. Click the "Confirm" button to complete the operation.


<span id=".5Yig6Zmk5raI5oGv6YCa55-l"></span>
### Delete message notifications

To disable the message notification feature, refer to the following steps.


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of the target resource.

3. Click the name of the scaling group and select the "Notify" tab.

4. Click the "Delete" button on the right side of the message notification list.

5. Click the "Confirm" button to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DescribeScalingActivities](https://docs.byteplus.com/en/docs/as/DescribeScalingActivities)
