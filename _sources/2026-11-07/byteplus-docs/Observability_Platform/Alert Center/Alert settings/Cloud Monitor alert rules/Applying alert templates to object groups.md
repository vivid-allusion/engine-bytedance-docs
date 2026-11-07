---
title: "Applying alert templates to object groups"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Applying_alert_templates_to_object_groups"
---

Apply an alert template to an object group. Alert rules will be automatically generated based on this template for resource monitoring. This topic describes how to apply an alert template to an object group.

<span id="zL2Ug89N"></span>
## Prerequisites


* You have created an object group to specify the resource scope for alert rules. For details, see [Creating object groups](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_object_groups).

* You have created a notification policy that specifies the contacts who receive notification messages, the notification template, and other information. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).


<span id="OfBb0re6"></span>
## Limits


* Each alert template can be associated with at most 100 object groups.

* Each object group can be bound to up to 20 alert templates.


<span id="WvkwIPtu"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration page.

3. In the alert configuration section on the left, select **Cloud Monitor** and click the **Alert template** tab.

4. Click **Apply to object group** in the Actions column that corresponds to the target alert template, configure information such as the object group and notification policy, and then click **Apply**.

   
   |Parameter |Description |
   |---|---|
   |Resource group |Select the object group that matches the alert template. An object group is a collection of resources for alert objects. For details, see [Object groups](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_object_groups).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Make sure that the object group matches the resource type specified in the alert template. Otherwise, although the alert rules can be created, they cannot work as expected because no resources are matched.</div><br><br><br><br>* If the resource types in the alert template and the object group overlap, Cloud Monitor generates corresponding alert rules based on the overlapping resource types and dimensions. The generated alert rule name is `{alert rule name}&{object group name}`.<br><br>* You cannot edit or delete the alert rule generated through the alert template. |
   |Notification policy |Select the notification policy that matches the alert template. A notification policy is a collection of notification methods. For detailed descriptions of notification policies, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Select a notification policy that includes notification methods supported by Cloud Monitor. Otherwise, although the alert rules can be created, you will not receive alert notifications because the notification methods are not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Cloud Monitor supports the following notification methods: phone call, SMS, email, Feishu, WeCom, DingTalk, Slack, alert callback, Feishu app, and Orchestration.</div><br> |
   |Project |Select the project it belongs to. The default project is "default".<br><br>Project management is a resource management method that allows you to manage cloud resources in groups based on different businesses or projects. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
   


<span id="gbGJjdtP"></span>
## Validate results


* After the template is applied, you can view the alert policies and object groups associated with the current alert template in the alert template list.

* Switch to the "Alert Rule" tab to view the alert rules automatically generated based on this template, as well as the alert templates and notification policies associated with the alert rules.
