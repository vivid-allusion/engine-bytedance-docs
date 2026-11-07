---
title: "Create a TLS trigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Create_a_TLS_trigger"
---

Function Service supports connecting to [Torch Log Service](https://docs.byteplus.com/en/docs/tls/What_is_TLS). By creating a TLS trigger, the Function Service will act as a consumer to process messages from the corresponding log topics and pass these messages to user functions, thus triggering code logic. This article introduces how to create a TLS trigger.

<span id="background-information"></span>
## Background information


* **Use Cases**

   Perform ETL processing on massive log data. Simple configuration and event triggering mechanism allow for processing event source data, enhancing the log service with one\-stop collection, processing, analysis, alert visualization, and delivery features, providing an end\-to\-end solution between cloud services.

* **Consumption rules**

   * If there are multiple shards in the log topic, the consumption order is not guaranteed, and it is recommended to use the load balancing mode to upload logs.

   * Initial consumption defaults to starting from "Latest".

   * For non\-initial consumption, it continues from the offset by default.

   * During a brief restart of the TLS trigger, log data can be consumed, but log data collected more than 2 hours after the interruption is not supported for consumption.

   * The retention time for log data on the TLS server side is 2 hours; it will be deleted after 2 hours or when the Kafka protocol consumption is disabled on the TLS side.


<span id="prerequisites"></span>
## Prerequisites


* Torch Log Service has been activated, and log projects and topics have been created in the function's region, with log data successfully collected. For detailed information, refer to [TLS Getting started](https://docs.byteplus.com/en/docs/tls/getting_started_overview).

* Kafka consumption feature has been enabled for the specified log topic. For detailed operations, refer to [Enable Kafka consumption feature](https://docs.byteplus.com/en/docs/tls/use_the_kafka_protocol_to_consume_logs#_1-enable-the-feature-of-using-the-kafka-protocol-for-consumption).

* BytePlus AccessKey ID (AK) and Secret Access Key (SK), have been obtained. It is recommended to use the IAM user's access key for authentication. Before using the IAM user, ensure that the BytePlus account has created an IAM user and that they have been granted permissions related to consuming TLS (at least with tls:ConsumeLogs permission). For details, refer to [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys) and [TLS authorizable actions](https://docs.byteplus.com/en/docs/tls/Authorizable_actions).

* The function must have been fully released at least once. For detailed operations, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).


<span id="usage-limit"></span>
## Usage limit


* A maximum of 20 triggers can be created for each function.

* Once a TLS trigger is created, it does not support changing the consumed log project and log topic.


<span id="procedures"></span>
## Procedures


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Function** page, select the function for which you need to create a trigger and click the function name.

4. In the function details page, under the **Triggers** tab, click **Create trigger**.

5. In the **Create trigger** panel, set the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Trigger type |This scenario selects a TLS trigger. |
   |Trigger name |Custom trigger name. Under the same function, trigger names cannot be duplicated. Trigger names cannot be modified after being successfully created. |
   |Log project and topic |Select the **log project** and **log topic** you need to consume. |
   |Number of retries |The maximum number of retries when a function run error occurs (including user code errors and runtime errors). Default is 100 times, the value range is 0~100. The retry policy is fixed interval retry, with an interval of 5 seconds. |
   |Enable immediately |Whether to enable the trigger at the same time it is created. Only triggers in the enabled state can function properly. |
   |Authentication |Prepare the BytePlus access keys AK and SK required in the prerequisites.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">It is recommended to use the IAM user access keys which should include permissions related to consuming TLS (with a minimum requirement of tls:ConsumeLogs permission).</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The access keys are only used for identity verification and veFaaS will not store your keys.</div><br> |
   |Description |Enter remarks as needed. |
   

6. Click **Confirm** to complete the creation of the TLS trigger.

   Once created, you can view the newly created TLS trigger details under the **Triggers** tab of the current function.


<span id="what-to-do-next"></span>
## What to do next


* If you need to modify the TLS trigger, refer to [Managing triggers](https://docs.byteplus.com/en/docs/faas/Managing_triggers).

* If you need to monitor the operational status of the function, refer to [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs).

* TLS provides Kafka protocol consumption operational capabilities, including viewing consumer group information, resetting consumption points, and monitoring consumption progress. You can observe the TLS trigger consumption details on the TLS side. For more details, refer to [Use the Kafka protocol to consume logs](https://docs.byteplus.com/en/docs/tls/use_the_kafka_protocol_to_consume_logs).
