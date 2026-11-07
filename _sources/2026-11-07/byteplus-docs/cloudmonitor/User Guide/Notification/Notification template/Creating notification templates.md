---
title: "Creating notification templates"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Creating_a_notification_template"
---

Cloud Monitor supports custom notification templates, where you can define the structure and fields of alert notifications or event notifications. This topic describes how to create a notification template.

<span id="wSpzrqpr"></span>
## Limits


* Each root user can have up to 1,000 notification templates.

* Do not include links, IP addresses, or contacts in an SMS template. 

* The template length and rendered length vary for different templates. Details are shown in the following table.



|Template type |Template length |Rendered length |
|---|---|---|
|Text message |2,000 bytes |1,024 bytes |
|Phone call |400 bytes |1,024 byte |
|Email |* Title: 400 bytes<br><br>* Content: 10 KB |* Title: 512 bytes<br><br>* Content: 2 MB |
|Feishu |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 512 bytes<br><br>* Content: 16,384 bytes |
|WeCom |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 256 bytes<br><br>* Content: 3,600 bytes |
|DingTalk |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 512 bytes<br><br>* Content: 8,192 bytes |
|Slack |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 512 bytes<br><br>* Content: 4,096 bytes |
|Custom callback |10 KB |None |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When your template content exceeds the <strong>rendered length</strong>, the excess part will be truncated, and only the truncated notification text will be displayed.</div>


<span id="X0KTw6ej"></span>
## Procedure


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview). 

2. In the left navigation pane, click **Notification \> Notification policy**.

3. Click the **Notification template** tab and the **Create notification template** button, and configure the relevant notification template parameters as needed.

   
   |Parameter |Description |
   |---|---|
   |Template name |Specify a name for the notification template as a unique identifier. Duplicate names are not allowed. |
   |Notification type |The product type for the notification template. Multiple types can be selected. Currently supported product types include Cloud Monitor, cloud service events, VMP, and Server\-side Monitoring. |
   |Notification method |The notification channel for the template. Each template supports only one channel. Currently supported notification channels include email, SMS, phone, Feishu group bot, Feishu application bot, DingTalk, WeCom, and notification callback URL. |
   |Template content |The notification title and content must comply with Markdown and Go Template syntax. For SMS and phone channels, only the notification content needs to be configured. For other channels, the notification title and content need to be configured.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">VMP supports configuring alert templates and recovery templates. Other notification types currently support configuring alert templates only.</div><br><br><br>The system provides a preset notification title and content for each notification type by default. If the preset templates do not meet your requirements, you can customize a notification template based on your actual scenario. The template writing syntax is universal, but the supported extension functions and variables vary by notification type. For more information, see:<br><br><br>* [Notification template syntax](https://docs.byteplus.com/en/docs/Observability_Platform/Notification_template_syntax)<br><br>* [Cloud Monitor & cloud product event extension functions and variables](https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_Cloud_Monitor)<br><br>* [Extension functions and variables for VMP](https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_VMP)<br><br>* [Extension functions and variables for Server-side Monitoring](https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_Server-side_Monitoring) |
   

4. Click **Preview notification template** in the lower\-right corner of the template content section to preview the notification template. After you confirm that everything is correct, click **Confirm** to complete the notification template creation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Click <strong>Restore default</strong> in the lower\-right corner of the template content section to restore the notification title and template content to the system preset content.   </div>
   

<span id="JnJpGPhZ"></span>
## What to do next

After the notification template is created, you can reference this template in alert policies, notification policies, or event rules. For details, see [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules), [Creating notification policies](https://docs.byteplus.com/en/docs/cloudmonitor/Create_a_notification_policy), and [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).

<span id="aFTgHSyt"></span>
## Validate results

<span id="t11INUaD"></span>
### View settings

After the configuration is complete, you can filter and view the specified template in the notification template list.

After the notification template is created, the following operation and maintenance actions are supported:


* Click the template name to enter the details page and view template details.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Delete** in the **Actions** column to delete the task.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the notification template is deleted, the alert policies and event rules associated with the notification template will generate notifications using the default notification content.</div>
