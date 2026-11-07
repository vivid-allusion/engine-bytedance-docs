---
title: "Trigger overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Trigger_overview"
---

Triggers are the gateways for function logic execution, activating functions by defining a set of rules. FaaS currently supports the following triggers:

<span id="timer-trigger"></span>
## Timer trigger

Based on Crontab syntax, this trigger schedules the execution of function logic.

<span id="api-gateway-trigger"></span>
## API Gateway trigger

Using public or private network HTTP/HTTPS traffic through API Gateway to trigger function logic.

<span id="tos-trigger"></span>
## TOS trigger

FaaS allows users to write functions to handle event changes in Torch Object Storage. Using the TOS trigger, FaaS will monitor events in the specified TOS Bucket and deliver eligible events to the user function to trigger function logic.

<span id="mq-trigger"></span>
## MQ trigger

FaaS supports users writing functions to handle messages received in the message queue. FaaS acts as a consumer to consume messages from a specified MQ Topic and delivers these messages to the user function, triggering function logic. FaaS currently offers the following three MQ triggers, which you can choose based on business characteristics and user habits.


* **Kafka trigger**: connect to BytePlus [Message Queue for Kafka](https://docs.byteplus.com/en/docs/kafka/what-is-message-queue-for-kafka).

* **RocketMQ trigger**: connect to BytePlus RocketMQ.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">RocketMQ Service is in <strong>beta</strong>. To use RocketMQ Service and RocketMQ trigger, contact your BytePlus costomer manager.   </div>
   

<span id="tls-trigger"></span>
## TLS trigger

FaaS supports users in writing functions to consume data from Torch Log Service TLS. FaaS will act as a consumer to consume messages from specified log projects and pass the messages to user functions, triggering function code logic.
