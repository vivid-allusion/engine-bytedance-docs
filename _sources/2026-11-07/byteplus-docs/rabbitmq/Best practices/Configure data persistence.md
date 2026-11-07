---
title: "Configure data persistence"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Configure_data_persistence"
---

In scenarios such as toggling extensions that may cause an instance to restart, or in rare cases of service exceptions, there is a risk of data loss if data persistence is not configured. This document demonstrates how to configure data persistence.

<span id="169d6e5d"></span>
## Application scenarios

Data persistence refers to writing data stored in memory to disk for long\-term storage. In Message Queue for RabbitMQ, both persistent and non\-persistent messages are written to the instance disk. However, in scenarios such as instance restart, reconfiguration, or service exceptions, non\-persistent messages may be accidentally deleted. Configuring data persistence can improve the reliability of Message Queue for RabbitMQ instances and prevent accidental data loss in abnormal scenarios. In scenarios where data reliability is critical, such as financial services, it is recommended to configure data persistence to enhance data reliability.

RabbitMQ data persistence methods include Exchange persistence, Queue persistence, and Message persistence. It is recommended to enable all configurations to ensure that messages are not lost in the vast majority of abnormal scenarios.

<span id="a8519aa7"></span>
## Configuration methods

<span id="c1197bc8"></span>
### Configure Exchange persistence settings

The persistence settings of Queue and Message ensure the reliability of messages. The persistence of Exchange ensures that Exchange still exists after an instance restart. If Exchange persistence is not configured, restarting the service may result in loss of Exchange information and cause message producers to be unable to send messages normally.

When creating an Exchange in the RabbitMQ WebUI, set the **durable** parameter to true. This enables Exchange persistence.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6dcea95cf7264d1e9857b21b17539ddc~tplv-goo7wpa0wc-image.image) </span>

After completing the configuration, the parameter attributes are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/219aba5d8611408daa5e51b0faa291cb~tplv-goo7wpa0wc-image.image) </span>

<span id="46b1e27a"></span>
### Configure Queue Persistence

The persistence flag of a Queue is durable. When the Queue **durable** parameter is set to true, it will enable persistence for the queue. After configuration, the backend service stores persistent queues on the instance disk. When the RabbitMQ instance restarts, the backend service reloads these queues, so the persistent queues will still exist.

When creating a Queue in the RabbitMQ WebUI, set the **durable** parameter to true to enable persistence for the queue.

A configuration example:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is strongly recommended to use <strong>Lazy mode</strong> for durable queues to avoid excessive memory consumption and potential slow startup problems caused by large backlogs. RabbitMQ\-3.8 must be manually configured, while RabbitMQ\-3.12 is enabled by default.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83c57dfbbdea4258bacbb53269750887~tplv-goo7wpa0wc-image.image) </span>

After completing the configuration, the parameter attributes are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e00df7e5dd6407f8c6cf5a56ac8e722~tplv-goo7wpa0wc-image.image) </span>

<span id="d281a354"></span>
### Configure message persistence

If there are still unsent messages in the queue before Restart, whether these messages remain in the queue after Restart depends on the message persistence settings at the time the messages are sent. Therefore, after configuring queue persistence, you also need to configure message persistence.

Caution: Because writing data to disk is slower than writing to memory, persisting a large number of messages will affect the performance of the RabbitMQ instance. When sending persistent messages, it is recommended to make a trade\-off between data reliability and throughput according to business requirements.

When sending a message, set the message persistence flag to make the message persistent. For details on configuring message persistence, refer to the official RabbitMQ documentation.

The following code shows how to send persistent messages via the client Java SDK:

```C++
channel.basicPublish("", "test-queue", MessageProperties.PERSISTENT_TEXT_PLAIN, messageBytes);
```
