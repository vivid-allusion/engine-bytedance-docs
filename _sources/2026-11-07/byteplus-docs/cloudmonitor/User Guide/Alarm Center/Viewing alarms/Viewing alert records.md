---
title: "Viewing alert records"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history"
---

After an alert of a cloud service instance is triggered, an alert record is automatically generated. The alert record records information such as the name of the faulty resource, the time when the alert is triggered, the duration of the alert, the alert level, and the name of the alert policy, which facilitates your viewing and reviewing the alert record in a centralized manner.

<span id="50ae9c2d"></span>
## Limits


* An alert record can be stored for up to 14 days.

* If the number of alert records exceeds 5,000, only the latest 5,000 alert records are displayed.

* An alert record covers the period from the time when an alert of a resource instance is triggered for the first time to the time when the alert is cleared. If the alert is triggered again after clearance, another alert record will be generated.


<span id=".5pON5L2c5q2l6aqk"></span>
## Viewing alert records


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Alert Center** \> **Alert History**.

3. You can filter for the target alert record by specifying a time period and filter conditions above the alert record list.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8da583aa7357fd60d8987a3db384baf0.png) </span>

   The following table describes the meaning of each column in the alert record list.

   
   |Column Name |Descriptions |
   |---|---|
   |Policy Name |The name of the alert policy that generated the alert record. You can click the policy name to copy the name. |
   |resource type |The type of the cloud service for which the alert record is triggered, such as ECS. |
   |Failure resource |The name of the resource for which the alert was triggered. You can click the name to view the detailed metric dashboard of the resource. |
   |Subnamespace |Select the resource namespace of the cloud service for which the alert was triggered, such as cloud service instances or storage disks. |
   |Status |The current status of the alert record. Valid values: **Threshold alert, Threshold alert has been restored**, **No data alert**, and **No data alert has been restored**. |
   |Alert rules |The metric type and trigger condition configured in the alert rule. |
   |Alert first trigger time |Indicates the time when the alert of the resource was triggered and the alert record was generated for the first time. |
   |Duration |* If an alert is in the **Restored** state, the value in the Duration column indicates the duration from the time when the alert of the resource is triggered to the time when the alert is cleared.<br><br>* If an alert is in the **Alert** state, the value in the Duration column indicates how long the alert of the resource remains active after being triggered. |
   |Alert level |The severity level of the alert. Valid values: **Critical**, **Warning**, **Notice**. |
   |Region |The region where the alert resource is located. |
   |Action |* Click **Details** to go to the details page of the alert record.<br><br>* Click **Create suppression policy** to configure a suppression policy for the alert. |
   

4. Click **Details** in the Actions column that corresponds to the target alert record to go to the details page of the alert record.

   * Overview:

      * **Basic information**: displays the occurrence time, duration, faulty resource, and other information.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8f8c9b708fa4c3b9bf61504f2cc8f90.png) </span>

      * **Alert History**: displays the trigger time, current value, trigger status, and sending status of each alert in the alert list and the corresponding trend chart on the right side.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d0260911783d8290d933de89975666f2.png) </span>

   * Contact group: displays the contact groups that receive alert record notifications.

   * Monitor: displays metric dashboards and monitoring data.
