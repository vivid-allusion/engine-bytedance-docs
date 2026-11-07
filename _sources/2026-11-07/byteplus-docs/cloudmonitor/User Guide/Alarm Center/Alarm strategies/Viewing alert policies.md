---
title: "Viewing alert policies"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy"
---

You can view detailed information about existing alert policies in the Cloud Monitor console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

At least one alert policy has been created. For details, see [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

<span id=".5pON5L2c5q2l6aqk"></span>
## Querying alert policies


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert Policy**.

3. On the **Alert policy** page, view the list of alert policies.

   The following table describes the column fields in the alert policy list.

   
   |Parameter |Descriptions |
   |---|---|
   |Name |The name and ID of the alert policy.<br><br>Click the name of an alert policy to go to the alert policy details page to view **Basic information**, **Alert object**, **Alert rules**, and **Notification method**. |
   |Status |The status of the alert policy.<br><br>When a cloud service resource triggers the specified alert policy, the strategy will be in the **Alert** state. Otherwise, it will be in the **Normal** state. |
   |resource type |The monitored cloud service. |
   |Subnamespace |The resource dimension of the monitored cloud service. |
   |Trigger condition |The details of the conditions that trigger the alert policy. |
   |Alert level |The alert level specified in the alert policy. Available levels include **Notification**, **Warning**, and **Critical**.<br><br>You can filter the alert list by alert level. |
   |Notification method |If you set the alert method to email, phone call, or SMS message for an alert policy, the number of alert contact groups will be displayed in the Notification method column. |
   |Enable status |* If **Enabled** is displayed in the Enable status column, it indicates that the specified cloud service resource is being monitored in real time.<br><br>* If **Disabled** is displayed in the Enable status column, it indicates that the specified cloud service resource is not being monitored in real time. |
   |Project |The project to which the alert policy belongs. |
   |Modified at |After you enable, disable, or edit an alert policy, the time displayed in the Modified at column will be updated. |
   |Action |You can enable, disable, edit, or delete an alert policy. For related operations, refer to the following topics:<br><br><br>* [Editing alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Modifying-an-alarm-strategy)<br><br>* [Enabling an alert policy](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-an-alarm-strategy)<br><br>* [Disabling an alert policy](https://docs.byteplus.com/en/docs/cloudmonitor/Disabling-an-alarm-strategy)<br><br>* [Deleting alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Deleting-an-alarm-strategy) |
   


<span id="RMDG3Dbq"></span>
## Viewing alert policy details


1. In the alert policy list, click the target policy name to enter the alert policy details page, where you can view details about the alert policy, such as the **basic information**, **alert object**, **alert rule**, and **notification method**. In the upper\-right corner of the alert policy details page, you can click the corresponding button to edit, disassociate, enable, disable, or delete the alert policy.

2. In the **Alert object** section of the alert policy details page, you can click **Details** next to the **Resource scope** field to query details of resource instances covered by the current alert policy. The details include the instance name, status, and region.


&nbsp;

&nbsp;
