---
title: "Creating a Kafka trigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_a_Kafka_trigger"
---

FaaS supports integration with [Message Queue Kafka ](https://docs.byteplus.com/en/docs/kafka/what-is-message-queue-for-kafka). By creating a Kafka trigger, FaaS will act as a consumer to consume messages from Kafka and deliver these messages to the user function, thereby triggering function code logic. You don't need to worry about the details of how functions consume messages, just focus on writing the function to process messages. This article explains how to create a Kafka trigger.

<span id="prerequisites"></span>
## Prerequisites


* The function must have VPC access enabled, and the function must be in the same VPC as the Kafka instance to be consumed. For detailed actions, refer to [Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration).

* After enabling or modifying VPC access configurations, a full release must be completed again. For detailed operations, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

* A Kafka instance and Topic have been created, and a SASL user has been established for the current Kafka instance. The SASL user must have at least read permission for the target Topic. For detailed operations, refer to [Kafka Getting Started](https://docs.byteplus.com/en/docs/kafka/started-overview).


<span id="usage-limit"></span>
## Usage limit


* A maximum of 20 triggers can be created for each function.

* The Kafka instance and function must be in the same VPC.

* If you need to modify the function's VPC or subnet, you must first disable or delete all MQ triggers.

* Once a Kafka trigger is successfully created, it does not support changes to the Kafka instance, Topic, or consumption location.


<span id="procedures"></span>
## Procedures


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Function** page, select the function you need to create a trigger for, then click the function name.

4. In the function details page, under the **Triggers** tab, click **Create trigger**.

5. In the **Create trigger** panel, set the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Trigger type |Choose Kafka trigger for this scenario. |
   |Trigger name |Custom trigger name. Under the same function, trigger names cannot be duplicated. Trigger names cannot be modified after being successfully created. |
   |Instance |Kafka instance, where FaaS will act as the consumer, consuming messages from the specified Kafka instance under the specified Topic. Please select the Kafka instance and Topic prepared in the prerequisites.<br><br><br>* **Topic**: a message subject, representing a collection of a certain type of messages and the basic unit for subscription in Kafka Message Queue.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only Kafka instances located in the same VPC as the function can be selected.</div><br> |
   |Number of retries |The maximum number of retries when a function encounters a runtime error, including user code errors and Runtime errors. |
   |Consumer offset |Specify the position to start consuming messages in the Topic, supporting two types: consuming from the beginning and from the latest. Please choose according to business needs; once the consumption position is specified, it cannot be changed.<br><br><br>* **Consuming from the beginning**: Starts consuming from the first message produced in the Topic.<br><br>* **Consuming from the latest**: Consumes only the messages produced after subscribing to the Topic. |
   |Enable immediately |Whether to enable the trigger at the same time it is created. Only the triggers that are enabled can function properly. |
   |Authentication |Prepare the SASL username and password required to access the Kafka instance specified in the prerequisites. FaaS will authorize message consumption for SASL users of PLAIN and SCRAM types through Kafka ACL permission policies.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Please enter the correct SASL username and password, as incorrect credentials will prevent the function from consuming Kafka messages.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Ensure that the configured SASL user has at least read permission for the target Topic.</div><br> |
   |Description |Enter remarks as needed. |
   

6. Click **Confirm** to complete the creation of the Kafka trigger.


<span id="what-to-do-next"></span>
## What to do next


* If you need to modify the Kafka trigger, refer to [Managing triggers](https://docs.byteplus.com/en/docs/faas/Managing_triggers).

* If you need to monitor the operational status of the function, refer to [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs).
