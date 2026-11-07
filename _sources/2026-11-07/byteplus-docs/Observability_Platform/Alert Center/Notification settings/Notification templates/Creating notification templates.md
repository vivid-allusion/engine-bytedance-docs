---
title: "Creating notification templates"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_templates"
---

The Alert Center provides a custom notification template feature, which allows you to define the notification type, channel, template content, and other information in a notification template. This topic describes how to create a notification template.

<span id="SF1oOHTz"></span>
## Limits


* Each root user can have up to 1,000 notification templates.

* Do not include links, IP addresses, or contacts in an SMS template. 

* The template length and rendered length vary for different templates. Details are shown in the following table.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When your template content exceeds the <strong>rendered length</strong>, the excess part will be truncated, and only the truncated notification text will be displayed.   </div>
   

   
   |Template type |Template length |Rendered length |
   |---|---|---|
   |Email |* Title: 400 bytes<br><br>* Content: 10 KB |* Title: 512 bytes<br><br>* Content: 2 MB |
   |Text message |2,000 bytes |1,024 byte |
   |Phone call |400 bytes |1,024 byte |
   |Feishu |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 512 bytes<br><br>* Content: 16,384 bytes |
   |DingTalk |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 512 bytes<br><br>* Content: 8,192 bytes |
   |WeCom |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 256 bytes<br><br>* Content: 3,600 bytes |
   |Slack |* Title: 400 bytes<br><br>* Content: 4,000 bytes |* Title: 512 bytes<br><br>* Content: 4,096 bytes |
   |General callback address |10 KB |None |
   


<span id="fZtk4DHC"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, select "**Alert Center \-\> Notification configuration**" to go to the "Notification configuration" page.

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
