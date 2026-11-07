---
title: "Creating event rule"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-event-rule"
---

RDS for SQL Server has connected to the Cloud Monitoring Event Center and registered the corresponding events. To stay informed of events and resolve issues as quickly as possible, you can create rules for events and send alert notifications to designated contacts after the event occurs and the event rule is triggered. This article describes how to create event rules for a RDS for SQL Server.

<span id="usage-restrictions"></span>
## **usage restrictions**

A maximum of 1000 event rules can be saved under the same main account.

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [the cloud monitoring console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, select **Event Hub** \> **Event Rules** .

3. On the **Event Rules** page, click **Create Event Rule** .

4. On the **Create Event Rule** page, complete the following configuration and click **OK** .

   
   |**area** |**explain** |
   |---|---|
   |**Basic information** |Sets the basic identification information for the event rule.<br><br><br>* **Name** : Required. Custom name to identify the event rule. When creating a name, the following rules should be followed:<br><br>* Cannot start with a number or a dash.<br><br>* The length is limited to between 1 and 128 characters.<br><br>* **Description** : Optional. Description information for custom event rules. When adding a description, the following rules should be followed:<br><br>* Cannot start with a number or a dash.<br><br>* Can only contain Chinese, letters, numbers, underscores (_), underscores (\-).<br><br>* The length is limited to between 0 and 255 characters. |
   |**event rules** |Set up detailed rules for cloud product events that need to be monitored.<br><br><br>* **Resource Type** : RDS for SQL Server.<br><br>* **Event name** : After selecting the resource type, the page will automatically display the drop\-down list. You need to manually select one or more event names.<br><br>* **Effective time** : On a daily basis, specify the effective time period of the event rule. Event Hubs only monitor whether cloud products have triggered event rules for a specified effective time.<br><br>* **Severity** : Used to identify the severity of the incident. Support setting severe, warning, notification. |
   |**Delivery method** |Set the way for alarm notifications after triggering event rules.<br><br><br>* **Delivery channels** : Select one or more channels. Support email, phone, SMS, alarm callback and log services.<br><br>* **Alarm Contact Groups** : When one or more of the channels in the mail, phone or text message is selected for the delivery channel, the page will display the alarm contact group, and you must set up one or more contact groups as the recipient of the alarm notification. Set up to 6, with the contact group as the recipient.<br><br>* **Alarm Callback** : When the delivery channel selects an alarm callback, the page will display the alarm callback text box and you must specify an available URL. In the future, if the resource triggers an event rule, the system will send the event details to the URL via a POST request, allowing you to perform in\-depth data analytics.<br><br>* It is recommended that you prepare a server that has the HTTP service turned on and interacts with the cloud monitoring console network, and then set the server's HTTP URL to the alarm callback URL.<br><br>* For more information about alarm callbacks, see the [alarm callback instructions](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions).<br><br>* **Themes** : When the delivery channel selects the log service, the page will display the new delivery theme button, you need to specify the available delivery themes.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you choose to post to the logging service, cloud monitoring does not charge for the data, but after cloud monitoring delivers the data to the logging service, the logging service charges for the data.</div><br> |
   


<span id="next-steps"></span>
## **Next steps**

Successfully created event rules default to the **enabled** state, and you can manage the state of the event rules later according to the actual request. For details, see [Managing Event Rules](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule).
