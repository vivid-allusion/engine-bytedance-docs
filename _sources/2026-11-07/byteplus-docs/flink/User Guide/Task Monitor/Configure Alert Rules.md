---
title: "Configure Alert Rules"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Configure_Alert_Rules"
---

BytePlus Flink has been integrated with the cloud monitoring service, where you can configure alert policies on the cloud monitoring platform to identify resource anomalies promptly and send alert notifications, thereby enhancing operational efficiency. This article introduces how to configure alert policies on the cloud monitoring platform, and the details of the Metric supported for alert configuration in BytePlus Flink.

<span id="42514f01"></span>
## Metric Introduction

The table below introduces the monitoring indicators for alert configuration supported by BytePlus Flink.


|**Dimension** |**Metric Name** |**Supported Aggregation Dimensions** |**Meaning and Calculation of Metrics** |**Corresponding Open Source BytePlus Flink Metrics (Scope:MetricName)**  |**Usage Instructions** |
|---|---|---|---|---|---|
|Job Running Status |Duration of Job Failure or Recovery |Maximum Value |Deprecated, Time from Failure to Running During Failover |job:downtime |Only supports 1.11, not recommended for use |
||Number of Job Failovers in the Past 30s |Maximum, minimum, average values |Number of job Failovers in the past 30s |job:fullRestarts |Not recommended due to the long intervals of Flink Failovers; it's suggested to use the subsequent 5/10/15 minutes Failover count metrics instead |
||Job failure status (a value of 1 indicates failure) |Maximum value |Job ends in a failure state |None |This alert only notifies once and does not support alarm recovery features |
||Job Failover QPS |Maximum Value |QPS when job experiences a Failover |job:fullRestarts |Not recommended for use, as the Flink Failover interval is relatively long, making the QPS calculation not intuitive. It is recommended to use subsequent Failover count metrics for the past 5/10/15 minutes instead |
||Job successfully ends status (a value of 1 indicates a successful conclusion) |Maximum Value |Job ends in a success state |None |This alarm notifies only once and does not support alarm recovery function |
||Number of times the job is automatically restarted after failing |Maximum Value |Number of times the job was automatically restarted after a failure |None |Effective only when the task failover restart configuration is enabled |
||Business Delay |Maximum Value |The time taken for Source to process data minus the time to write the data into upstream storage. Currently supports only the new KafkaSource |operator:currentEmitEventTimeLag |Supported only in version 1.16 using the new KafkaSource |
||Number of job failovers in the past 5 minutes |Total |Number of Failovers in the Past 5 Minutes |job:fullRestarts |Recommended to configure an alarm after 3/5 consecutive periods exceed the threshold to prevent false alarms |
||Number of Failovers in the Past 10 Minutes |Total |Number of Failovers in the Past 10 Minutes |job:fullRestarts |Recommended to configure an alarm after 3/5 consecutive periods exceed the threshold to prevent false alarms |
||Number of Failovers in the Past 15 Minutes |Total |Failover count in the past 15 minutes |job:fullRestarts |Recommended configuration: Trigger an alarm only if the value exceeds the threshold for 3 out of 5 periods consecutively to prevent false alarms |
|checkpoint |Duration of the most recent checkpoint |Maximum, minimum, and average values |Duration of the most recent checkpoint |job:lastCheckpointDuration |It is not recommended to use this alert since a long checkpoint duration might trigger a timeout, making it difficult to configure thresholds. Set a reasonable checkpoint timeout along with a configuration for issuing alerts upon checkpoint failure occurrences |
||Consecutive checkpoint failure count |Maximum, minimum, and average values |Consecutive failure count, reset to zero after a successful checkpoint Do not count the instances of checkpoint failures triggered (e.g., during job failover) |None | |
||Number of job checkpoints failed in the past 5 minutes |Total |Number of job failovers in the past 5 minutes |job:numberOfFailedCheckpoints |Recommend configuring a trigger for alerts only if 3 out of 5 cycles exceed the threshold to prevent false alarms |
||Number of job Checkpoint failures in the past 10 minutes |Total |Number of job Failover instances in the past 10 minutes |job:numberOfFailedCheckpoints |Recommend configuring a trigger for alerts only if 3 out of 5 cycles exceed the threshold to prevent false alarms |
||Number of job Checkpoint failures in the past 15 minutes |Total |Number of job Failover instances in the past 15 minutes |job:numberOfFailedCheckpoints |It is recommended to trigger an alarm only if the value exceeds the threshold for 3/5 consecutive cycles to prevent false alarms. |
|Kafka |Max KafkaConsumer Records Lag V11 |Maximum, minimum, average values |The number of data records in Kafka awaiting consumption indicates maximum values across multiple partitions; a high value suggests inadequate consumption capacity. |None |This metric is only effective when using OldKafkaSource and will not be recorded in the event of abnormal job execution. |
||Max KafkaConsumer Records Lag V16 |Maximum, minimum, average values |The number of data records in Kafka awaiting consumption indicates maximum values across multiple partitions; a high value suggests inadequate consumption capacity. |None |Effective only when using NewKafkaSource, and this metric is not tracked when there are job anomalies |
|flinkFiveMinsCounter |Number of job Failovers in the past 5 minutes |Total |Number of job Failovers in the past 5 minutes |job:fullRestarts |Not recommended; this alert metric is repetitive and will be deprecated.<br><br>Recommended to use the metric of Failover counts on job operation status dimension for alerts |


<span id="f02e2ee8"></span>
## Prerequisites


* Before creating alert policies on the cloud monitoring service, you need to clearly define the resource object and obtain the ID of the Flink job in advance.

* When creating alert policies, choose **email**, **phone**, or **text message** as the notification method. You need to create alert contacts and contact groups in advance, please see [creating alert contacts and contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group).


<span id="9125fb84"></span>
## Create Alert Policies


1. Login to the [cloud monitoring console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, select **Alarm Center \> Alarm Policy**, then click **Create Alarm Policy**.

3. In the **Basic Information** section, set the alarm policy name and description.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_20805cde1d4fa15886a5999a4fee2a89.png) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Noun |Custom alarm policy name, used to identify the alarm policy.<br><br>Required length range is 1~128 characters, and it must not start with a number or a hyphen (\-). |
   |Description |Description of the alarm policy. |
   

4. In the **Alarm Object** area, select the resource type as **Data Platform \> BytePlus Flink**, then choose the region, dimension, and resources based on the actual situation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da81091f7d6648ea8c7ddb4b69e9eb94~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Resource Type |Select **BytePlus Data Mid\-End \> BytePlus Flink**. |
   |Region |Select based on the region of your resource object. |
   |Dimension |Create alert policies based on dimensions, currently supporting four dimensions: **job running status**, **checkpoint**, **Kafka**, and **flinkFiveMinsCounter**. |
   |Resource |Define the scope of the resource (job) for which alert policies are set, supporting the following two settings:<br><br><br>* All: Indicates setting alert policies for all jobs under the current account. Note, all refers to current jobs being affected; manually configure subsequent newly created jobs.<br><br>* Partial: Manually select one or more jobs, indicating that the alert policy is set only for the selected jobs. |
   

5. In the **Alarm Rules** area, select the metric type, set alarm trigger conditions, alarm levels, policy effective time, alarm sending frequency, and more.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ae4a62e9a33f0f55292f8de8f15d30b.png) </span>

   
   |**Configure** |**Description** |
   |---|---|
   |Use preset trigger conditions |Preset trigger conditions according to alarm dimensions make it easy to quickly fill in alarm strategies. However, BytePlus Flink does not have preset trigger conditions for any dimension, so there is no need to focus on this parameter. |
   |Metric type |Supports selecting either **single metric** or **multiple metrics**. If you need to monitor multiple metrics of a resource, you can directly configure the multi\-metric type. |
   |Trigger conditions |Set the monitoring metrics, duration period, statistical type, comparison relation, and threshold for the alarm. When the monitored resource metric meets the trigger conditions, the system will send an alarm notification.<br><br>The method for triggering an alarm involves collecting statistical values of the current cycle indicator for continuous N cycles. If all meet the alarm threshold, an alarm is triggered.<br><br>For example, consider "Failover occurrences in the past 5 minutes". If configured for 3 consecutive cycles (1 cycle = 1 minute) with a total that is greater than or equal to 5. Then every minute, the system calculates the sum of Failover counts for the past 5 minutes. If the value calculated continuously for 3 minutes is \>=5, an alarm is triggered. |
   |Alarm Level |Used to indicate the severity of an alarm. Supports setting **critical**, **warning**, **notification** levels. |
   |Effective Time |The effective time of the alarm policy. The alarm policy only monitors resource data to meet triggering conditions within the effective time. |
   |Alarm Sending Cycle |After a monitoring strategy triggers an alert, if the monitored resource continues to trigger alerts, the system will periodically send alert notifications. |
   |Alert Recovery Notification |Whether to send alert recovery notifications when the criteria for triggering alerts are no longer met. Current BytePlus Flink does not support alert recovery; do not enable it. |
   

6. In the **Alarm Method** area, choose the alarm notification method and alarm notification group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee74db8945a4416ba5e1622f12fcfd06.png) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Alert Channel |Select one or multiple channels. Supports **email**, **phone**, **SMS**, and **alert callback**. |
   |Alert Contact Group |When **alert channels** are selected, which include **email**, **phone** or **SMS**, you must set one or more contact groups to receive alert notifications. |
   |Alert Callback |When selecting alert callback, the page will display a text box for alert callbacks, and you must specify a valid URL.<br><br>If an alert is triggered later, the system will send the detailed information of the alert to this URL via a POST request to facilitate in\-depth data analysis. |
   

7. After configuring the alarm policy, click **OK** at the bottom right corner of the page.

   Once the alarm policy is successfully created, it will automatically start.
