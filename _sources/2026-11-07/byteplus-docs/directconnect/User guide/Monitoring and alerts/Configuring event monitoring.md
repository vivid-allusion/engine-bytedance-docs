---
title: "Configuring event monitoring"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Configuring-event-monitoring-alerts"
---

You can configure event alarm rules for Direct Connect on the Cloud Monitor platform to promptly monitor key events occurring on your connections. After configuring alarm rules, whenever an event matching the rule occurs, personnel in the contact groups will receive alert notifications promptly. This facilitates quickly pinpointing the affected Direct Connect resource and ensures business stability.

For an introduction to specific event metrics of Direct Connect, see [Direct Connect event metrics](https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=event&namespace=directconnect%2C%E4%B8%93%E7%BA%BF%E8%BF%9E%E6%8E%A5).

<span id=".5Yib5bu65LqL5Lu26KeE5YiZ"></span>
## Create an event rule

<span id=".5pON5L2c6K-05piO"></span>
### Instructions


* A maximum of 1,000 event rules can be saved under a single account.

* Events that have occurred on the Cloud Monitor platform are saved for 30 days by default. If you cannot find Direct Connect event information via the Event Center, it indicates either that no events have occurred for Direct Connect or that the events occurred more than 30 days ago.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

You have created alarm contacts and groups on the Cloud Monitor platform. For specific procedure, see [Creating an alarm contact and group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, select **Event Center \> Event rule**.

3. On the Event Rules page, click **Create event rule**.

4. On the Create Event Rule page, configure the event rules for Direct Connect.

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Name |Name of the event rule. |DC\-Rule |
   |**Event rule** |||
   |Resource type |Specify the monitored cloud product, here select "Direct Connect". |Direct Connect |
   |Event name |This parameter appears after selecting the resource type. Select one or more event names.<br><br>Supported events for Direct Connect are as follows:<br><br><br>* **BFD session down**: Indicates a line failure.<br><br>* **BGP routes exceed limit**: A single BGP session supports a maximum of 100 BGP routes by default. Any BGP routes exceeding this limit will be discarded.<br><br>* **BGP session down**: Indicates a failure in the BGP Peer session. |BFD session down |
   |Effective on |The time period when the event rule is active is specified on a daily cycle. The Cloud Monitor Event Center only monitors whether the Direct Connect triggers the event rule during the specified effective time. |00:00\-23:59 |
   |Severity level |Severity level of the event. Severity levels supported: Severe, Warning, Notification. |Severe |
   |**Delivery method** |||
   |Delivery channel |The method of alarm notification after an event rule is triggered. Multiple methods can be set simultaneously. Supported channels include: Email, Phone, SMS, Alarm Callback, Torch Log Service (TLS), and Message Queue Kafka. |Phone |
   |Alert contact group |When selecting one or more of the following delivery channels: **Email**, **Phone**, or **SMS**, the page will display the Alarm Contact Group field. You must specify one or more contact groups as recipients for alarm notifications. A maximum of 5 contact groups can be set as recipients. |DC O&M contact group |
   |Alarm callback |When the delivery channel is set to "Alarm Callback", the page will display the Alarm Callback text box, and you must specify a valid URL. Subsequently, if a resource triggers the event rule, the system will send the detailed event information via a POST request to this URL, enabling you to perform in\-depth data analysis.<br><br><br>* It is recommended that you prepare a server with the HTTP service enabled and network connectivity to the Cloud Monitor console, then set the server's HTTP URL as the alarm callback URL.<br><br>* For more information about alarm callbacks, see [Alert callback usage notes](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions). |\- |
   |Topic |When the delivery channel is set to TLS, the page will display the Add Delivery Topic button, and you need to specify a usable Delivery Topic. |\- |
   |Message queue |When the delivery channel is set to Message Queue Kafka, the page will display the Add Delivery Message Queue button, and you need to specify a usable Delivery Topic. |\- |
   

5. Click **Confirm** to complete the action.


<span id=".5YGc55SoL-WQr-eUqOS6i-S7tuinhOWImQ=="></span>
## Disable or enable event rules

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

The successfully created event rule is enabled by default. You can manage the status of the event rule based on your actual needs.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, select **Event Center \> Event rule**.

3. In the event rules list, see the diagram to disable or enable rules.


<span id=".5p-l6K-i5bey5Y-R55Sf5LqL5Lu2"></span>
## Query occurred events

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

Currently, only Direct Connect event alerts that have occurred can be viewed in the Cloud Monitor console.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, select **Event Center \> Cloud product event**.

3. On the Cloud Product Events page, you can filter for target events based on time, cloud product name, and event name.

4. Click **Details** in the Actions column on the right side of the target event to view detailed information.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/CreateEventRule): Create an event rule.

* [ListEventRules](https://docs.byteplus.com/en/docs/cloudmonitor/ListEventRules): Query event rule information.

* [EnableEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/EnableEventRule): Enable one or more event rules.

* [DisableEventRule](https://docs.byteplus.com/en/docs/cloudmonitor/DisableEventRule): Disable one or more event rules.
