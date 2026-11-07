---
title: "Limits"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Limits"
---

This topic describes the usage limits on account usage and product features of Cloud Monitor.

<span id="73c58d73"></span>
## Account limits

The following table describes the limits when you use Cloud Monitor by using a single  root user.


|**Limit** |**Limit Description** |
|---|---|
|Storage duration for historical monitoring data |* The data storage duration for metrics of different cloud products is 30 days, 60 days, or 90 days. For details, see [Cloud product metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).<br><br>* The data of cloud product events can be retained for 30 days. |
|Alert record |* An alert record can be stored for up to 14 days.<br><br>* Up to 5,000 alert records can be displayed. |
|Alert policy |* Up to 1,000 alert policies can be created within one account.<br><br>* If you associate all resources in a region with an alert object, the number of alert policies is not limited.<br><br>* If you associate part of the resources in a region with an alert object, the number of resources is limited by the following rules:<br><br>   * Up to 1,000 resources of the same type can be added to an alert policy.<br><br>   * Up to 5,000 resources of all types can be added to an alert policy.<br><br>* When you select resources by **resource name**, **project** and **label**, up to 1000 resources can be matched.<br><br>* Up to five alert contact groups can be associated with each alert policy.<br><br>* Each alert policy can contain up to 1,000 resources when an alert is generated during each check exception. |
|Event rule |* Up to 1,000 event rules can be created within one account. |
|Object group |* One object group can be bound to only one alert template.<br><br>* Up to 100 object groups can be created within a root user.<br><br>* Up to 100 resource types can be added to an object group.<br><br>* Up to 1,000 resources of the same type can be added to an object group.<br><br>* Up to 5,000 resources can be added to an object group.<br><br>* When you select resources by **resource name**, **project**, and **label**, up to 1000 resources can be matched. |
|Alert contact person |* Up to 100 alert contacts can be created.<br><br>* One alert contact can be associated with up to 10 alert contact groups. |
|Alert contact group |* Up to 100 alert contact groups can be created.<br><br>* Up to 100 alert contacts can be created in an alert contact group. |
|Suppression policy |* Up to 1,000 suppression policies can be created within one account. |


<span id="86d701d2"></span>
## Alert notification limit


|**Limit** |**Limit Description** |
|---|---|
|Phone call |* A phone number can receive up to 300 phone calls per day.<br><br>* A phone number can receive up to 1 phone call and 3 text messages per minute.<br><br>* A root user and its Identity and Access Management (IAM) users can receive up to 300 **phone** calls per hour and up to 100 phone calls per minute.<br><br>* Resources are not listed in phone call notifications. |
|Text message |* A phone number can receive up to 300 text message notifications per day.<br><br>* A phone number can receive up to 1 phone call notification and 3 text message notifications per minute.<br><br>* A root user and its IAM users can receive up to 300 **text message** notifications per hour and up to 100 text message notifications per minute.<br><br>* Up to three resources can be listed in an SMS notification. |
|Email |* An email address can receive up to 100 email notifications per minute.<br><br>* An account can receive up to 100 email notifications per minute.<br><br>* Up to 10 resources can be listed in an email notification. |
|Alert callback |* You can enter up to one publicly accessible URL or select up to eight created callback URLs for an alert policy.<br><br>* A root user and its IAM users can receive up to 100 **email** notifications per minute.<br><br>* A root user and its IAM users can receive up to 100 **Webhook** notifications per minute. All resources will be listed in dedicated webhooks and sent in batches. Up to 100 resources can be sent per batch.<br><br>* A root user and its IAM users can receive up to 20 **Lark**, **WeCom**, and **DingTalk** notifications per minute. Up to 10 resources can be listed in a notification.<br><br>   The number of listed resources in a WeCom notification may be less than 10 because a WeCom message can be up to 4096 bytes in length. |


<span id="2c19c5e6"></span>
## Contact limits


|**Limit** |**Limit Description** |
|---|---|
|Email |* The same email address can receive only one verification email per minute.<br><br>* An account can send up to 100 verification emails per minute.<br><br>   If the upper limit is exceeded, contacts can be created or updated, but the activation email will not be received. Wait for a while and then update the email address again to trigger the activation email. |
|Text message |* The same mobile number can receive only one verification SMS message per minute.<br><br>* An account can send up to 100 verification SMS messages per minute.<br><br>   If the upper limit is exceeded, contacts can be created or updated, but the activation SMS message will not be received. Wait for a while and then update the mobile number again to trigger the activation SMS message. |


<span id="29257a58"></span>
## Cloud product limits


|**Limit** |**Limit Description** |
|---|---|
|Conditions for resource recovery after an alert is triggered |If the monitoring data of a resource does not reach the alert threshold for five consecutive minutes, the resource returns to a **normal** status. |
|Number of disks that can be displayed on the **OperateSystemMonitor** page of an ECS instance |Monitoring data of up to 20 disks can be displayed. |
|Number of disks that can be associated with the same alert policy |* If you associate all disks, the number of disks is not limited.<br><br>* If you associate specific disk partitions, up to 50 disks can be selected. |


<span id="a8123a02"></span>
##
