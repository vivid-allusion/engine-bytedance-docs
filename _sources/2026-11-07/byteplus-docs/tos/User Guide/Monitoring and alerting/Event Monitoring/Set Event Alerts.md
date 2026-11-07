---
title: "Set Event Alerts"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-event-alerts"
---

You can set up alerts for TOS\-related events based on your business needs. When an event occurs, the system will send notification alerts in the manner you specify, allowing you to promptly detect any abnormalities. This article explains how to set up event alerts.

<span id="d2603f3c"></span>
## Prerequisites

Alarm contacts and contact groups have been created, or an alarm callback address has been set up. For details, see [Creating an alarm contact and an alarm contact group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group) and [Create a callback address](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address#create-a-callback-address).

<span id="18fafca4"></span>
## Procedure


1. Log in to [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left sidebar, select **Event Center \> Event Rules**.

3. On the **Event Rule** page, click **Create event rule**.

4. On the **Create event rule** page, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |The name of the alarm rule. The naming rules are as follows:<br><br><br>* Length must be between 1 to 128 characters.<br><br>* Cannot start with a number, hyphen, or special character. |
   |Description |Instructions for custom alert rules. |
   |Resource type |Select **object storage**. |
   |Event description |Select the alert event. For detailed information about TOS alert events, please refer to [Flow Control Event Metrics Description](https://docs.byteplus.com/docs/tos/Flow-control-event-metrics-description). |
   |Level |Indicates the severity of the alert event. Supports setting **Critical**, **Warning**, and **Notice**. |
   |Project selection |Select the project to which the alarm resource belongs, supporting the choice between **All projects** and **part of the project**. |
   |Delivery channel |Select one or multiple channels. Supports **Email** and **Webhook**.<br><br><br>* If you select **Email** in **Delivery** **channel**, **Alarm contact group** appears on the page. In this case, you must specify one or multiple alarm contact groups for receiving alarm notifications.<br><br>* If you select **Webhook**in **Delivery channel**, the **Webhook** text box appears on the page. In this case, you must specify an accessible URL.<br><br><br>For a detailed introduction, please see [Creating an event rule](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule). |
   |Effective time |Set specific active periods for alarm rules based on a daily cycle. Once configured, monitoring for TOS is only active within the designated effective times. |
   

5. After setting the parameters, click **OK**.

   The alarm event is enabled by default, and you can manage its status later as needed. For specific operations, please see [Managing an event rule](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-an-event-rule).


&nbsp;
