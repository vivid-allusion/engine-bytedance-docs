---
title: "Creating a RocketMQ trigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_a_RocketMQ_trigger"
---

Function Service supports connecting to Message Queue for RocketMQ. By creating a RocketMQ Trigger, Function Service acts as a consumer to consume messages from RocketMQ, and passes the messages to user functions, triggering function code logic. You do not need to worry about the details of how Function Service consumes messages; just focus on writing the function that processes the messages. This article introduces how to create a RocketMQ Trigger.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">RocketMQ Service and RocketMQ trigger are in <strong>beta</strong>. To use them, contact your BytePlus costomer manager.</div>


<span id="prerequisites"></span>
## Prerequisites


* The function must have the VPC access feature enabled, and the function and the RocketMQ instance to be consumed must be in the same VPC. For detailed actions, refer to [Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration).

* After enabling or modifying the VPC access configuration for the function, you must complete a full release again. For detailed actions, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

* RocketMQ instance, Topic, Consumer Group, and access keys have been created. The access key is the key for RocketMQ ACL permission control and must include subscription permissions.


<span id="usage-limit"></span>
## Usage limit


* A maximum of 20 triggers can be created for each function.

* RocketMQ instances and functions must be in the same VPC.

* If you need to modify the function's VPC or subnet, you must first disable or delete all MQ triggers.

* Once a RocketMQ trigger is created, it does not support changes to the RocketMQ instance, Topic, or Consumer Group.


<span id="procedures"></span>
## Procedures


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Function** page, select the function you want to create a trigger for and click the function name.

4. In the function details page, under the **Triggers** tab, click **Create trigger**.

5. In the **Create trigger** panel, set the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Trigger type |Select the RocketMQ trigger for this scenario. |
   |Trigger name |Custom trigger name. Under the same function, trigger names cannot be duplicated. Trigger names cannot be modified after being successfully created. |
   |Instance |The instance, that is, the RocketMQ instance, the function service will play the role of the designated Consumer Group to consume messages from the specified topic under the RocketMQ instance. Please select the RocketMQ instance, Topic, and Consumer Group that you have prepared under the prerequisites.<br><br><br>* **Topic**: Message topic, representing a collection of a type of messages, is the basic unit for subscribing to messages in Message Queue for RocketMQ.<br><br>* **Consumer Group**: A consumer group is a group of consumers with the same Group ID. Through consumer groups, messages in a Topic can be consumed in parallel.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only instances of RocketMQ in the same VPC as the function are supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To ensure that the trigger can consume all the messages of a Topic, it is recommended that one Consumer Group corresponds exclusively to one trigger.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The Consumer Group begins consuming from the latest position in the Topic.</div><br> |
   |Number of retries |The maximum number of retries when a function encounters a runtime error, including user code errors and runtime errors. |
   |Message order |Select whether to strictly consume messages in the order they are published based on business needs.<br><br><br>* **Message ordering**: Ensure all messages are consumed in the order delivered by the producer (i.e., first in, first out, FIFO).<br><br>* **Message disorder**: Consumption does not strictly follow the first\-in\-first\-out principle, suitable for scenarios where message order is unimportant. |
   |Enable immediately |Whether to enable the trigger at the same time it is created. Only triggers that are enabled can function properly. |
   |Authentication |Enter the access key ID and access key secret prepared in the prerequisites to access the RocketMQ instance. The access key is only used for message subscription authentication, and the veFaaS will not store your access key.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The access key is for the RocketMQ ACL permission control, not the key for the BytePlus account.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The access key must include subscription permissions.</div><br> |
   |Description |Enter remarks as needed. |
   

6. Click **Confirm** to start creating the RocketMQ Trigger.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The creation process may take 1 to 2 minutes. Please be patient. Once successfully created, you can find the corresponding Consumer client information in the RocketMQ Console.   </div>
   

<span id="result-validation"></span>
## Result validation


* Function Service console

   Under the **Trigger** tab of the current function, you can view the information of the newly created RMQ Trigger.

* Message Queue for RocketMQ console

   You can view the newly added consumer client information under the details of the corresponding Consumer Group in the RMQ instance. This client is the current function.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Status synchronization may have a minute\-level delay, please be patient.   </div>
   

<span id="what-to-do-next"></span>
## What to do next


* If you need to modify the trigger, refer to [Managing triggers](https://docs.byteplus.com/en/docs/faas/Managing_triggers).

* If you need to monitor the operational status of the function, refer to [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs).
