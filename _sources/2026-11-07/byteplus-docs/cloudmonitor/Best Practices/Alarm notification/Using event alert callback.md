---
title: "Using event alert callback"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Generating-alarm-strategies-based-on-alarm-templates"
---

Beyond phone, SMS, email, DingTalk, Feishu, and WeCom alerts, Cloud Monitor offers alert callbacks for more flexible event handling.

<span id="25d62398"></span>
## Prerequisites


* A publicly accessible URL is ready. This URL is the address of your O&M system or message notification system.

* A callback address has been created. For details, see [Create callback address](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address#414fd7c7).


<span id="f939c3bc"></span>
## Background

Alert notifications are sent to your specified URL via HTTP/HTTPS POST. You can then process the alert based on the content.

<span id="1f6bff30"></span>
## Creating an event rule

The following example shows how to use the alert callback feature for cloud product events. It uses a scenario where ECS events configured in an event rule are pushed to a webhook, demonstrating how to integrate alert notifications from Cloud Monitor into your existing O&M or message notification system.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Event Center \> Event Rule**.

3. On the **Event Rule** page, click **Create event rule**.

4. On the **Create event rule** page, specify the related parameters, and then click **OK**.

   
   |**Section** |**Parameter** |**Description** |**Sample value** |
   |---|---|---|---|
   |**Basic information** |Name |Specify a custom name to identify the event rule. |ECS system failure: instance stopped. |
   ||Description |Specify a custom description for the event rule. |test |
   |**Event rule** |resource type |Specify the cloud service to be monitored. |Elastic Compute Service (ECS) |
   ||Event name |Selecting a **Resource Type** automatically shows this drop\-down list. You need to select one or more event names. |System failure, causing instance to stop: In progress |
   ||Effective time |Specify the effective period of the event rule by day. Event Center only monitors whether the cloud service triggers the event rule during the specified effective period. |00:00\-23:59 |
   ||Level |Used to indicate the severity level of the event. Valid values: **Critical**, **Warning**, **Notice**. |Warning |
   |**Delivery method** |Delivery channel |Select one or more channels. |Alert callback |
   ||Alert callback |When **Alert callback** is selected as the **Delivery channel**, the **Alert callback** text box will appear, and you need to specify a valid URL. Later, when a resource triggers the event rule, the event details will be sent to this URL via POST for further data analysis.<br><br><br>* We recommend using a server that has HTTP enabled and can connect to the Cloud Monitor console. Set its HTTP URL as the alert callback URL.<br><br>* For more information about alert callback, refer to [Alert callback usage](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions). |Doc |
   

5. View alert notifications.

   You will receive alert notifications at your URL when an event rule is triggered by a cloud product. The notification content is shown in the following figure.

   ```JSON
   {
     "Type": "Event",
     "AccountId": "210****353",
     "Source": "ecs",
     "Id": "1777*****43520",
     "EventType": "ecs:Instance:SystemFailure.Stop.Executing",
     "HappenedAt": 1712635880,
     "Region": "cn-beijing",
     "Details": {
       "data": {
         "EventType": "RebootInstance",
         "ExtraInfo": {},
         "InstanceId": "i-yd218*****r2s",
         "InstanceName": "ECS-cloudmonitor-test",
         "PrivateIpAddress": [
           "192.168.xxx.xxx"
         ]
       },
       "id": "1777*****43520",
       "project": "default",
       "source": "ecs",
       "specversion": "1.0",
       "subject": "trn:ecs:cn-beijing:210****353:instance/i-ycs*****ok3",
       "time": "2024-04-09T12:11:20+08:00",
       "type": "ecs:Instance:SystemFailure.Stop.Executing",
       "volcaccountid": "210****353",
       "volceventbusname": "default",
       "volcpublishtime": "2024-04-09T12:11:20+08:00",
       "volcregion": "cn-beijing",
       "volcresourcename": "test_eventgateway"
     },
     "Rules": [
       {
         "RuleId": "1749*****07328",
         "RuleName": "demo",
         "Level": "warning"
       }
     ]
   }
   ```
