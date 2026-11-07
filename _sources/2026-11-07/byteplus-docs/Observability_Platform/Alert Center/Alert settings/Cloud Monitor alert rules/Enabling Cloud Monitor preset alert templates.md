---
title: "Enabling Cloud Monitor preset alert templates"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Enabling_Cloud_Monitor_preset_alert_templates"
---

Alert templates can be preset for various cloud products. They include basic information, alert objects, and alert rules, but do not include notification policies. Preset alert templates can be applied to all regions and all resources with a few clicks to streamline the process.

<span id="dGl5y9Nv"></span>
## Prerequisites

You have created a notification policy that specifies the contacts who receive notification messages, the notification template, and other information. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

<span id="Rw0eVpWA"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the Alert Configuration page.

3. In the alert configuration section on the left, select **Cloud Monitor** and click the **Preset alert template** tab.

4. In the Actions column that corresponds to the target preset alert template, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89d5221ec75c7cea9f937fbbf811e437.png) </span>icon and configure the required information in the pop\-up dialog box. After completing the configuration, click **Confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After a preset alert template is enabled, alert rules are automatically created based on the template and applied to all resources in all regions.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Notification policy |Select the notification policy that matches the preset alert template. A notification policy is a collection of notification methods. For details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Select a notification policy that includes notification methods supported by Cloud Monitor. Otherwise, although the alert rules can be created, you will not receive alert notifications because the notification methods are not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Cloud Monitor supports the following notification methods: phone call, SMS, email, Feishu, WeCom, DingTalk, Slack, alert callback, Feishu app, and Orchestration.</div><br> |
   |Project |Select the project it belongs to. The default project is "default".<br><br>Project management is a resource management method that allows you to manage cloud resources in groups based on different businesses or projects. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
   


<span id="LmG1Y7zy"></span>
## Validate results

After a preset alert template is enabled, the alert rules created from the template will be applied to all resources in all regions. Click the "Alert Rule" tab to view the alert rules automatically generated from this preset template. You can also view the alert templates and notification policies associated with these alert rules.

&nbsp;
