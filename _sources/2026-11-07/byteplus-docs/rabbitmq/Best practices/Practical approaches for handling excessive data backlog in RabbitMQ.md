---
title: "Practical approaches for handling excessive data backlog in RabbitMQ"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Practical_approaches_for_handling_excessive_data_backlog_in_RabbitMQ"
---

During actual use, the message consumption capability of a RabbitMQ instance may not keep up with the production capability, or in scenarios where messages are produced and accumulate before being consumed, a large number of messages may pile up in the RabbitMQ instance. This can cause the cluster's memory and disk to reach high watermarks, blocking message production and consumption.

<span id="9Y4GhYx9"></span>
## Use lazy queues

<span id="SY35a8Tj"></span>
### Application scenarios

If you are not particularly sensitive to data latency, you can use lazy queues. By default, data in lazy queues is written directly to disk and is only loaded into memory when it is actually consumed. Lazy queues not only ensure data reliability, but also speed up node Restart.

Currently, for RabbitMQ version 3.8 instances, users need to manually configure the lazy policy, while version 3.12 instances are lazy queues by default and do not require user configuration. Therefore, when applying for an instance, it is highly recommended to choose version 3.12.

<span id="HrkzovNp"></span>
### Configuration example

The manual configuration of a lazy queue for a RabbitMQ 3.8 instance is shown in the following figure.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_437495724597d4e458fe8cf70b2f1af8.png) </span>

<span id="6Ec300x2"></span>
## Use a lower QoS

<span id="p6VtFmNX"></span>
### Application scenarios

If you want to speed up consumption when RabbitMQ has accumulated a large number of messages, set a higher QoS value for consumers. However, when a large number of messages are pulled to the client for consumption, messages may not be acknowledged in time, resulting in accumulation in RabbitMQ's memory and causing memory overflow. Therefore, in cases where there is a large backlog of data, it is recommended to use a smaller QoS to gradually consume the backlog, thereby reducing its accumulation.

<span id="rY3nVwH1"></span>
### Configuration example

The following example sets the QoS value for consumers in a RabbitMQ instance to 5.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When both the connections number and the number of channels are low, you may consider appropriately increasing the QoS value.</div>


```Java
channel.basicQos(5); 
```


&nbsp;

<span id="WveFqXzS"></span>
## Consumption timeout settings

<span id="m0zOdlJj"></span>
### Application scenarios

Currently, the default consumption timeout for Message Queue for RabbitMQ instances is 5 minutes. It is not recommended to set this value too high, because if a consumption exception occurs, consumption may become stuck, resulting in a growing backlog of messages.

<span id="awnDItwU"></span>
## Avoid starting a large number of connections and channels at once

When there is a large backlog of unconsumed messages in RabbitMQ, you should avoid starting a large number of connections and channels (approximately 10,000) at once. Otherwise, a large volume of messages may be read from RabbitMQ into memory simultaneously, which can lead to RabbitMQ running out of memory.

&nbsp;

<span id="yM8FMwHn"></span>
## Monitoring and alarm

<span id="YuWTZWo9"></span>
### Application scenarios

To prevent a large backlog of message consumption in RabbitMQ that could impact business operations, you can configure Cloud Monitor alarm rules for relevant Message Queue for RabbitMQ metrics.

<span id="l0BDjZBm"></span>
### Configuration example

<span id="Jyz7CID4"></span>
#### **Instance dimension**


* Number of consumable messages

   If the consumption backlog continues to increase and the accumulated amount is large, you should monitor alarms.

* Unacknowledged message count

   This mainly addresses the situation where messages have already been pulled from the RabbitMQ server, but the consumer has not acknowledged them, so the messages keep accumulating in RabbitMQ's memory.


<span id="CBltAzK7"></span>
#### **Broker Dimension**


* memory high watermark

   When the memory high watermark is reached, service production and consumption may be blocked.

* Disk high water level

   When the disk high water mark is reached, the production and consumption activities of the business may be blocked.


For detailed information about alarm rule configuration, please refer to the [recommended alarm rules](https://docs.byteplus.com/en/docs/rabbitmq/Recommended_alarm_rules).

&nbsp;

<span id="F1HcRwlr"></span>
## Configure message TTL

<span id="t7rbLK0w"></span>
### Application scenarios

In RabbitMQ version 3.12, if business messages are not particularly important, you can configure the TTL parameter for messages (applicable only to version 3.12). After configuration, messages that are not consumed after a certain period will automatically expire and be cleaned up, ensuring that Cluster resource levels remain stable.

<span id="8vSvYBH5"></span>
### Configuration example

The configuration of the message TTL parameter in RabbitMQ version 3.12 is shown in the following figure.

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a6bb179f27d59e9cd7b91dc866504ab6.png" width="1280px" /></div>


<span id="j2zOzGKo"></span>
## Mirror Queue

If mirroring is configured for a classic queue, the mirrored queue will clear its local data and then perform a full synchronization after all replicas go offline abnormally at the same time, which can result in the loss of all messages in the queue. Therefore, when a significant backlog of messages has already accumulated in a mirrored queue, you should try to avoid starting too many consumers to prevent excessive message backlog, thereby causing multiple nodes to experience simultaneous memory overflow and abnormal node shutdown.
