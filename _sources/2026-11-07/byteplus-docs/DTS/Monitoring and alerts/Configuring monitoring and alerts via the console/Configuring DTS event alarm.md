---
title: "Configuring DTS event alarm"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Configuring_DTS_event_alarm"
---

Database Transfer Service (DTS) supports the monitoring of events and anomalies during data transmission, and can set up alarm rules. During data transmission, you will be notified immediately once an event reaches the set trigger rules, so that you can take timely measures to ensure the normal operation of the business. This topic describes how to create event alarm rules for DTS in the Cloud Monitor console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The cloud monitor has already been activated. For more details, refer to [Enabling pay-as-you-go for cloud monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling_pay-as-you-go).

<span id=".5Yib5bu6LWR0cy3nmoTkuovku7blkYrorabop4TliJk="></span>
## Creating event alarm rules for DTS


1. Log on to the [Cloud monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, choose **Event center** \> **Event rules**.

3. On the **Event policy** page, click **Create event policy**.

4. On the **Create event policy** page, configure the following information.

   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Name** |The name of the custom event policy. The naming convention is as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* The length must be between 1 and 128 characters. |
   ||**Description** |Description of the custom event rule. The description specifications are as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* Can only contain Chinese, letters, digits, underscores(_) and hyphens(\-).<br><br>* The length must be between 0 and 255 characters. |
   |<div style="text-align: center"><br><strong>Event policy</strong></div><br> |**Resource type** |Select **Database Transmission Service** from the drop\-down list of resource types. |
   ||**Event name** |Select trigger events as needed. Event types include **Migration task abnormal**, **Migration task incremental start**, **Migration task recovery**, **Synchronization task abnormal**, **Synchronization task incremental start**, **Synchronization task recovery**, **Subscription task abnormal**, **Subscription task recovery** , and **PG logical replication slot deletion failed**. |
   ||**Severity** |Indicates the severity of the event. You can set the level to **Critical**, **Warning**, or **Notice**. |
   ||**Event details matching** |Click **add** to allow finer\-grained event matching based on the field after `Data` in the DTS event details. For example, you can implement event matching based on the instance ID of DTS.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more DTS event details, refer to <a href="https://docs.byteplus.com/en/docs/DTS/Viewing_DTS_event_information">Viewing DTS events</a>.</div><br> |
   |**Delivery method** |**Delivery channel** |Select one or more channels. Supports **email**, **phone**, **SMS**, **Alarm** callback, **log Service**, and **message queue kafka**. |
   ||**Alarm contact group** |When you select one or more **delivery channels** from **Email**, **Phone**, or **SMS**, the page displays the **Alarm contact group,**  and you must set one or more contact groups to receive alarm notifications. You can set up to 5 contact groups as recipients. |
   ||**Alarm callback** |When you select **Delivery channel** as **Alarm callback**, the **Alarm callback** text box is displayed on the page, and you must specify an available URL. If a resource triggers the event policy, the system sends the details of the event to this URL via a POST request for in\-depth data analysis.<br><br><br>* We recommend that you prepare a server with an opened HTTP service and interconnected with the Cloud monitor (VCM) console network, and then set the server's HTTP URL as the alarm callback URL.<br><br>* For more information about warning callbacks, refer to [Warning callback usage instructions](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions). |
   ||Message queue |When the **Delivery channel** selects **Message Queue for Kafka**, the **Add delivery message queue** button is displayed on the page, and you need to specify an available delivery topic.<br><br><br>* Delivery to topics or instances of Message Queue for Kafka is currently supported only in **China (Beijing)**  and **China (Shanghai)** .<br><br>* For an instance associated with an allowlist, only the IP addresses configured in the allowlist can access the corresponding Kafka instance. Note the following:<br><br>   * When pushing messages to Message Queue for Kafka, do not select an instance that is associated with an allowlist.<br><br>   * After you configure pushing to an instance, do not add that instance to an allowlist.<br><br>* When you select a topic in Message Queue for Kafka as the destination in a **User management** event rule for the first time, a user named __volcevent_xxxvolc is automatically created under User Management for the topic. Do not delete this user; otherwise, Cloud monitor (VCM) can not deliver messages to the topic properly. |
   ||**Topic** |When **Delivery channel** is set to **Log Service**, the **Add delivery topic** button is displayed. You must specify an available delivery topic.<br><br><br>* Only delivery to Log Service topics is currently supported in **China (Beijing)** .<br><br>* You can add up to 10 topics.<br><br>* For more information about log topics, refer to [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you choose to deliver to the log service, Cloud monitor (VCM) does not charge for the data, but the log service will charge for the data after Cloud monitor (VCM) delivers the data to the log service.</div><br> |
   ||Orchestration plan |When **Alarm channel** is set to **Operation orchestration**, the **Orchestration plan** drop\-down list is displayed on the page.<br><br>Configure the operation orchestration plan to be executed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Operation orchestration is a cloud\-based, workflow\-driven automated operations service offered by BytePlus. It allows you to orchestrate task flows and execute them automatically based on your requirements. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview_of_Process_Orchestration">Operation orchestration</a>.</div><br> |
   ||Notification template configuration |When one or more channels are selected for **Delivery channel**, such as **Email**, **Phone**, or **SMS**, you can specify a notification template for the event delivery channel. If not configured, the system uses the default notification template for event delivery. For how to configure a notification template, refer to [Creating a notification template](https://docs.byteplus.com/en/docs/cloudmonitor/Creating_a_notification_template). |
   ||Effective time |Configure the effective time of the event rule. The system delivers events based on the event rule configuration only during the effective time. |
   

5. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Manage event policies: after an event policy is created, you can enable, disable, or delete the event policy in the Cloud Monitor console. For details, refer to [Manage event policies](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule).
