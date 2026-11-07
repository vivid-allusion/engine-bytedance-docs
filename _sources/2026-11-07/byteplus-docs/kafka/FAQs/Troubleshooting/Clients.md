---
title: "Clients"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/clients-faq"
---

This topic provides answers to frequently asked questions (FAQs) related to clients in Message Queue for Kafka.

<span id="23edf2e5"></span>
## How do I troubleshoot issues when I connect a client to Message Queue for Kafka for the first time?

When you connect a client to Message Queue for Kafka for the first time, issues such as connection failures may occur. To troubleshoot such an issue:


1. Verify the network connection.

   If you fail to connect to the endpoint of a Kafka instance from the client, the client cannot be connected to the brokers of the Kafka instance. This issue is caused by the following reasons:

   * The client is deployed in an Elastic Compute Service (ECS) instance. The ECS instance and the Kafka instance are not in the same Region or virtual private cloud (VPC). In this case, if the Kafka instance is connected via the default endpoint, a connection failure occurs. To ensure a successful connection, connect the client to a public endpoint of the instance. For more information, refer to [Connecting to an instance by using a SASL_SSL endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL).

   * The client is deployed in the data center or a third\-party environment. If you connect the client to a private endpoint of the Kafka instance, a connection failure occurs. To ensure a successful connection, connect the client to a public endpoint of the instance. For more information, refer to [Connecting to an instance by using a SASL_SSL endpoint](https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL).

   * The client IP address is not included in the allowlist associated with the Kafka instance. For information on how to modify an allowlist, refer to [Associating an instance with an allowlist](https://docs.byteplus.com/en/docs/kafka/associating-allowlist).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For information on how to select a correct endpoint for connection, refer to <a href="https://docs.byteplus.com/en/docs/kafka/viewing-endpoints">Viewing endpoints</a>, which helps you understand the network and authentication requirements for different instance endpoints.   </div>
   

2. Verify that a correct client version is used.

   We recommend that you use a client version that is compatible with the version of the Kafka instance. If the Kafka version of your client is outdated, a connection exception may occur. To resolve such issues, log on to the Message Queue for Kafka console, view the Message Queue for Kafka version of the specified instance on the **Instances** page, then update the client version accordingly.

3. Verify the connection configurations.

   A connection failure may occur if the account, password, or permission of a SASL_SSL user is configured incorrectly. In this case, rectify the relevant parameters by referring to the message production and consumption demos available for Message Queue for Kafka.


<span id="a26c16f2"></span>
## Why do partition rebalance events frequently occur on the consumer client?

After you connect your client to a Kafka instance, partition rebalance events frequently occur on the consumer client. The main reason is that the consumer does not maintain heartbeat status in an independent thread and fails to send the heartbeat status in a timely manner. As a result, the consumer times out and leaves the consumer group, which leads to a partition rebalance.

You can set the `max.poll.interval.ms` parameter on the client. This parameter specifies the maximum interval between two polls for the consumer. If the consumer fails to consume all messages that have been pulled within the specified period and polls messages again, Message Queue for Kafka determines that an issue occurs on the consumer client. This makes the client proactively leave the message queue and causes a partition rebalance.

To prevent the frequent occurrence of partition rebalance events, use the following methods:


1. Adjust poll\-related parameters.

   
   |Parameter |Description |
   |---|---|
   |[session.timeout.ms](https://kafka.apache.org/documentation/#connectconfigs_session.timeout.ms) |Specifies the timeout period of consumer heartbeats. This parameter can be set on the client.<br><br>We recommend that you keep the default value of 10 seconds. |
   |[max.poll.records](https://kafka.apache.org/documentation/#consumerconfigs_max.poll.records) |Specifies the maximum number of messages to return for each poll initiated by the consumer.<br><br>We recommend that you reduce the value of this parameter to far smaller than the product of the following formula: `Number of consumed messages per thread per second * Number of threads * Value of the max.poll.interval.ms parameter`. |
   |[max.poll.interval.ms](https://kafka.apache.org/documentation/#consumerconfigs_max.poll.interval.ms) |Specifies the maximum interval between two polls for the consumer. The default value is 5 minutes.<br><br>We recommend that you set the value of this parameter to be larger than the value of the following formula: `Value of the max.poll.records parameter / (Number of consumed messages per thread per second * Number of threads)`. |
   

2. Improve the consumption speed of the client. For example, start a separate thread to process the consumption logic.

3. Control the number of topics subscribed to by the group to a reasonable range.

   We recommend that you control the number of topics subscribed to by a single group to 1 or no greater than 5.


<span id="d1aca627"></span>
## Why does a consumer slowly poll messages or fail to poll messages?

Although a topic subscribed to by a group contains messages, the consumer in the group has not consumed messages at the latest consumer offset and slowly polls messages or fails to poll messages from the brokers. This issue is caused by the following reasons: The message consumption traffic reaches the bandwidth limit; the size of a single message exceeds the limit; the consumer requests an excessively large volume of messages in each poll.

To resolve such an issue, use the following methods.


|Cause |Troubleshooting Method |Solution |
|---|---|---|
|The message consumption traffic reaches the network bandwidth limit of the instance. |Verify whether the **message consumer rate** of the instance is close to that of the instance specifications in the Vitality Cloud Monitor (VCM) console. For more information, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/kafka/viewing-monitoring-data). |Upgrade the instance type. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).<br><br>Alternatively, limit the number of messages to return in each poll by using the parameters given in the following table. |
|The bandwidth limit of the associated elastic IP address (EIP) is reached. |Verify the EIP bandwidth associated with the instance to see if the maximum EIP bandwidth is far smaller than the **message consumer rate** of the instance. |Increase the EIP bandwidth. |


Message Queue for Kafka allows you to set the volume of messages to return in each poll by using the following parameters.


|Parameter |Description |
|---|---|
|**max.poll.records** |Specifies the maximum number of messages to return in each poll. |
|**fetch.max.bytes** |Specifies the total size of messages to return in each poll. Unit: bytes. We recommend that you set this parameter to a value less than the current network bandwidth. |
|**max.partition.fetch.bytes** |Specifies the total size of messages to return from each partition in each poll. Unit: bytes. We recommend that the product of `the value of the max.partition.fetch.bytes parameter multiplied by the number of total subscribed partitions` is less than the current network bandwidth. |
