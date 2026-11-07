---
title: "Recommended Alert Rules"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Recommended_Alert_Rules"
---

Stream Computing Flink version supports configuring cloud monitoring alarm rules to help you monitor the task status in real time. This document presents some examples of alarm rule configurations, suggesting that you configure according to these recommended alarm strategies.

<span id="5abef327"></span>
## If the job failover count is ≥ 2 within the past 10 minutes


* **Alarm Rule Configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a0859f1d554b788707ae0e4916964b~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Value retrieval** |
|---|---|
|Dimension |Job running status |
|Trigger condition |* Monitoring indicator: Number of job Failovers in the past 10 minutes<br><br>* Duration: 3<br><br>* Value retrieval method: Maximum<br><br>* Comparison method: \>=<br><br>* Threshold: 2 |
|Alert level |Warning |



* **Handling Suggestions**

   Observe if the job recovers on its own, whether the alarm persists, and check the JM & TM logs to diagnose the reasons for job restart.


<span id="933cdd47"></span>
## Job failure status ≥ 1


* **Alarm Rule Configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d1eb91198d149b7a7629759fbf85dbe~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Value Retrieval** |
|---|---|
|Dimension |Job Running Status |
|Trigger Condition |* Monitoring Indicator: Job Failure Status<br><br>* Duration: 3<br><br>* Value Retrieval Method: Maximum<br><br>* Comparison Method: \>=<br><br>* Threshold: 1 |
|Alert Level |Warning |



* **Handling Suggestions**

   View TM & JM logs. If the logs contain business\-related error stacks, you must judge whether the job can recover after automatic relaunch; otherwise, please submit a ticket to technical support for feedback.


<span id="4cc4dccc"></span>
## Job completion status ≥ 1


* **Alarm rule configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/191329754ed84019b31095d6ed74c18f~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Value** |
|---|---|
|Dimension |Job Running Status |
|Trigger Condition |* Monitoring Indicator: Job Completion Status<br><br>* Duration: 1<br><br>* Value extraction method: maximum<br><br>* Comparison method: \>=<br><br>* Threshold: 1 |
|Alarm level |Notification |



* **Processing advice**

   This alarm indicates that batch jobs have been executed completely; if it is triggered by streaming jobs, please contact technical support for troubleshooting.


<span id="872e2f23"></span>
## Automatic recovery of failed jobs ≥ 1


* **Alarm rule configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b29b2a80c87e4704a6345f1094564de0~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Value retrieval** |
|---|---|
|Dimension |Job running status |
|Trigger condition |* Monitoring Metrics: Job Failure GTS Automatic Recovery<br><br>* Duration: 1<br><br>* Value Method: Maximum<br><br>* Comparison Method: \>=<br><br>* Threshold: 1 |
|Alarm Level |Warning |



* **Processing advice**

   * View TM & JM logs. If the log contains business\-related error stacks, it is necessary to judge whether the job can recover after being automatically restarted; otherwise, please submit a ticket to the technical support staff.

   * Check if the alert is persistent. If it is only intermittent and has no impact on operations, it can be ignored; otherwise, handle as previously mentioned.


<span id="98b69d92"></span>
## Job Checkpoint failures ≥ 1


* **Alarm rule configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ef0c06497d34da9a3f4253958aceb09~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Value Retrieval** |
|---|---|
|Dimension |Job Operation Status |
|Trigger Condition |* Monitoring Indicators:<br><br>   * Number of job Checkpoint failures in the past 5 minutes<br><br>   * Number of job Checkpoint failures in the past 10 minutes<br><br>   * Number of job Checkpoint failures in the past 15 minutes<br><br>* Duration: 3<br><br>* Method of Value Retrieval: Maximum<br><br>* Comparison Method: \>=<br><br>* Threshold: 1 |
|Alert Level |Warning |
|Description |**Suggested configuration period should be longer than the job's Checkpoint interval to avoid false alarms**. For example, if the Checkpoint interval is 10min, it is recommended to configure that the number of job Checkpoint failures in the past 15 minutes is \>= 1. If the Checkpoint interval is 1min, it is recommended to configure that the number of job Checkpoint failures in the past 5 minutes is \>= 1. |



* **Handling suggestions**

   * Check if there is backpressure on operators in the Flink UI. If backpressure exists, prioritize solving the backpressure issue. After resolving, observe whether the checkpoint fails, as most checkpoint failures are caused by backpressure.

   * Check if the alert is persistent. If it is only intermittent and has no impact on operations, it can be ignored; otherwise, handle as previously mentioned.


<span id="6f468e00"></span>
## Business delay ≥ 15 min


* **Alarm Rule Configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcb5583db2a54af3adc16a2b7b833b83~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Value** |
|---|---|
|Dimension |Job Running Status |
|Trigger Condition |* Monitoring Indicator: Business Delay<br><br>* Duration: 3<br><br>* Value Method: Maximum<br><br>* Comparison Method: \>=<br><br>* Threshold: 15 (min)  **(Note: It is recommended to configure the appropriate threshold based on the real\-time requirements of the operation.)**  |
|Alarm Level |Warning |
|Description |Currently, business delay monitoring alarms are only supported in scenarios using Flink 1.16 engine with Kafka/MySQL Change Data Capture/Mongo Change Data Capture Source. |



* **Handling Suggestions**

   * Observe if resources hit a bottleneck in the data curve, consider scaling up, and monitor if the alarm continues.

   * Check TM & JM, and investigate error messages.


<span id="d3cd4fd9"></span>
## Max KafkaConsumer Records Lag \> 1 million


* **Alarm Rule Configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f5c9ba647a64b18ad87c918e1c9dc66~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Value** |
|---|---|
|Dimension |Kafka |
|Trigger Condition |* Monitoring Indicators:<br><br>   * Max KafkaConsumer Records Lag v16 (Description: Flink 1.16 Kafka lag indicator)<br><br>   * Max KafkaConsumer Records Lag v11 (Description: Flink 1.11 Kafka lag indicator)<br><br>* Duration: 3<br><br>* Value Method: Maximum<br><br>* Comparison Mode: \><br><br>* Threshold: 1 million (**Note: It is recommended to configure an appropriate threshold based on the Source QPS**) |
|Alarm Level |Warning |



* **Handling Suggestions**

   * Observe if resources hit a bottleneck in the data curve, consider scaling up, and monitor if the alarm continues.

   * Check TM & JM, and investigate error messages.
