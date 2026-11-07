---
title: "Create an Alarm Strategy"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/2hG26c"
---

This document introduces how to add alarm strategies in BytePlus GTM and associate the alarm strategies with GTM instances.

<span id="prerequisites"></span>
## Prerequisites

You have already activated BytePlus Cloud Monitor. If you need to use notification channels such as email or webhook, you also need to create an alarm contact group in BytePlus Cloud Monitor.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can refer to <a href="https://docs.byteplus.com/en/docs/CloudMonitor/Creating-an-alarm-contact-and-an-alarm-contact-group">Creating an alarm contact and an alarm contact group</a> to learn how to create and use alarm contact groups.</div>


<span id="steps"></span>
## Steps

Follow the steps below to create an alarm strategy and associate the alarm strategy with GTM instances.


1. On the [Alarm notification page](https://console.byteplus.com/dns-suite/gtm/alarm), click **Create alarm strategy**.

2. On the **Create alarm strategy** page, you will be prompted to create and authorize the service\-linked role ServiceRoleForGTM to BytePlus GTM. This role will allow BytePlus GTM to manage event rules in BytePlus Cloud Monitor. You need to follow the prompted steps to complete the authorization.

3. After authorization, configure the following parameters on the **Create alarm strategy** page:

   **Basic information**

   
   |Parameter |Description |
   |---|---|
   |**Name** |The name of the alarm strategy. |
   |**Remark** |Remarks for the alarm strategy. |
   |**Enabled** |Whether to enable the alarm strategy. The alarm strategy will only take effect if enabled. |
   |**Alarm level** |The severity level of the alarm strategy, including **Critical**, **Warning**, and **Info**. |
   

   **Alarm events**

   You can select the following alarm events.

   **Instance**

   
   |Parameter |Description |
   |---|---|
   |**Instance state changes** |The GTM instance undergoes one or more of the following changes:<br><br><br>* The state of the GTM instance changes from **running** to **stopped**.<br><br>* The state of the GTM instance changes from **stopped** to **running**.<br><br>* The GTM instance is deleted. |
   |**Instance configuration changes** |The GTM instance undergoes one or more of the following changes:<br><br><br>* The basic information of the GTM instance changes.<br><br>* The health check parameters of the GTM instance change. |
   |**Rule changes** |The rule configuration changes. |
   

   **Pool Set**

   
   |Parameter |Description |
   |---|---|
   |**Pool set activation status changes** |Another pool set in the rule becomes active. |
   |**Pool set becomes unavailable** |The status of the pool set changes from available to unavailable. |
   |**Pool set becomes available** |The status of the pool set changes from unavailable to available. |
   

   **Address**

   
   |Parameter |Description |
   |---|---|
   |**Address becomes unavailable** |The status of the address changes from available to unavailable. |
   |**Address becomes available** |The status of the address changes from unavailable to available. |
   

   **Notification method**

   
   |Parameter |Description |
   |---|---|
   |**Notification channel** |The method of alarm notification. You can select one or more notification channels. You need to select at least one notification channel. |
   |**Contact group** |The alarm contact group you created in BytePlus Cloud Monitor. This parameter will only appear if you select one or more of **Email** and **Webhook** as the notification channel. |
   |**Webhook** |The webhook in BytePlus Cloud Monitor. This parameter will only appear if you select **Webhook** in the notification channel.<br><br>&nbsp;<br><br>You need to enter a URL that is accessible from the internet. BytePlus Cloud Monitor will push the alarm information to this address through a POST request. See [Webhook Instructions](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions) to learn about the content of the POST request sent by BytePlus Cloud Monitor. You do not need to create this webhook in BytePlus Cloud Monitor. |
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the <strong>Webhook</strong> parameter, you cannot enter the webhook address of a Lark bot.</div>


<div data-tips="true" data-tips-type="warning">If you want a Lark bot to receive the alarm callback, you need to first receive the alarm callback from BytePlus Cloud Monitor, transform the JSON data of the alarm callback into the data structure supported by the Lark bot, and then send the transformed JSON data to the webhook address of the Lark bot.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following example shows the request body of a POST request that BytePlus Cloud Monitor sends to the webhook URL when BytePlus Cloud Monitor detects a GTM instance status change event.</div>


<div data-tips="true" data-tips-type="tip">```JSON
{
    "Type": "Event",
    "AccountId": "21*****11",
    "Source": "trafficroute_gtm",
    "Id": "1836*****04000",
    "EventType": "trafficroute_gtm:Instance:StateChange",
    "Description": "StateChange",
    "HappenedAt": 1664332705,
    "Details": {
        "data": null,
        "datacontenttype": "application/json",
        "id": "1836*****04000",
        "resourceid": "",
        "source": "trafficroute_gtm",
        "specversion": "1.0",
        "subject": "trafficroute_gtm:a.example.com",
        "time": "2023-05-16T14:23:26+08:00",
        "type": "trafficroute_gtm:Instance:StateChange",
        "volcaccountid": "21*****11",
        "volceventbusname": "default",
        "volcprojectname": "",
        "volcpublishtime": "2023-05-16T14:23:26+08:00",
        "volcresourcename": ""
    },
    "Rules": [
        {
            "RuleId": "1836**********8880",
            "RuleName": "webhook",
            "Level": "notice"
        }
    ]
}
```
</div>


<div data-tips="true" data-tips-type="tip">The <code>type</code> parameter refers to the event type. The values are as follows:</div>



* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:Instance:StateChange</code>: Instance state changes</div>


* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:Instance:ConfigChange</code>: Instance configuration changes</div>


* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:Instance:ViewChange</code>: Rule changes</div>


* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:View:PoolSetFailover</code>: Pool set activation status changes</div>


* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:View:PoolSetInactive</code>: Pool set becomes unavailable</div>


* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:View:PoolSetActive</code>: Pool set becomes available</div>


* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:Address:AddressInactive</code>: Address becomes unavailable</div>


* <div data-tips="true" data-tips-type="tip"><code>trafficroute_gtm:Address:AddressActive</code>: Address becomes available</div>



**Associated instance**

Select the GTM instances associated with the alarm strategy. An alarm strategy can be associated with one or more GTM instances. Each GTM instance can only be associated with one alarm strategy.

After configuration, click **Confirm**. You can see the alarm strategy you added on the **Alarm notification** page.
