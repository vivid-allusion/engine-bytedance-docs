---
title: "Viewing migration progress and results"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-migration-progress-results"
---

During the migration of business data, the original cluster can be stopped only after all subscribed messages in the original cluster are consumed. This topic introduces how to view the migration progress and results.

<span id="通过云监控查看"></span>
## Viewing in the Vitality Cloud Monitor (VCM) console

Make sure that Message Queue for Kafka is integrated with VCM. Then, you can view the metrics related to message production and consumption traffic in the VCM console and analyze the running status of your instance.


1. Log on to the CloudMonitor console.

2. In the left\-side navigation pane, click **Cloud Service Monitor**, find the **Middleware** pane, and select **Kafka**.

3. Click your instance name to go to the **Monitor** page of the instance.

   After specifying a time range, you can determine the message production and consumption status in your instance based on the following metrics.

   * **message producer rate**: the message production traffic rate in the cluster per second, based on which the current message production rate can be determined.

   * **message consumer rate**: the message consumption traffic rate in the cluster per second, based on which the current message consumption rate can be determined.

      If 0 is displayed for these metrics, no persistent message production and consumption occurs. In this case, confirm whether producers and consumers are connected.


<span id="通过命令行查看"></span>
## Viewing by using a command line

You can refer to the following steps to view the consumption progress in each consumer group.


1. Run the following command to query the consumer group list in the Kafka cluster:


```undefined
./bin/kafka-consumer-groups.sh --bootstrap-server {kafkaAddress} --list
```


<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a9bf9c5d35253f718986000486928711) </span>


2. Run the following command to query the consumption progress of a specified consumer group in the cluster:


```undefined
./bin/kafka-consumer-groups.sh --bootstrap-server {kafkaAddress} --describe --group {group-name}
```


The LAG column indicates the number of remaining messages that can be consumed. As displayed in the following figure, if 0 is displayed in the LAG column, all messages have been consumed.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_76c706b4aab8b4d8c6a523c952f4efd5) </span>
