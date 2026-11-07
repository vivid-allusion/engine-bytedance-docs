---
title: "Visualization of Kafka Protocol Consumption Metrics"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Visualization-of-Kafka-Protocol-Consumption-Metrics"
---

This article describes how to achieve real\-time monitoring and alarming of the consumption backlog situation of the Kafka protocol through the dashboard and alarming capabilities of Torch Log Service (TLS).

<span id="31a647df"></span>
## Before you begin

The Kafka protocol consumption log task has been created. For more information, please refer to [Use the Kafka protocol to consume logs](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs).

<span id="020a7dc4"></span>
## Background information

After starting the Kafka consumption group, due to limitations of factors such as Kafka Client configuration, performance of client consumption threads, performance of client data processing threads, and the number of Topic shards, it may lead to the situation that the amount of consumed data is lower than the amount of uploaded data (data uploaded through multiple channels such as Log Connector and Kafka protocol upload), thus resulting in data backlog. Under normal circumstances, a certain degree of backlog is normal because there is a time interval for the client to poll data. However, if the backlog keeps increasing, it indicates insufficient consumption capacity. When the consumption delay exceeds the storage duration of the topic, data will be lost. In such cases, it is necessary to improve the client's consumption capacity through means such as optimizing client parameters, expanding the client, and expanding partitions. For more information, please refer to [Consumer Configs](https://kafka.apache.org/documentation/#consumerconfigs).

TLS provides a Kafka monitoring dashboard, which is used to display the changing trends of consumption delay and consumption speed, and also supports configuring alarms for the charts, so that you can discover and handle related problems regarding consumption delay and consumption speed in a timely manner.

<span id="7b1f7e14"></span>
## Scenario 1: View the changing trends of the consumption group's delay and consumption speed


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where the TLS is located.

3. In the left\-side navigation pane, choose **Data Processing** \> **Log consumption**.

4. In the **Kafka** tab, locate and expand the project to which the target kafka consumer group belongs, and then click the specified kafka consumer group.

5. In the **Monitor Kanban** tab, view the consumer\-related dashboards.

   The dashboard displays the consumption latency, consumption speed, and related trends of the Kafka consumption group.

   * MaxPartitionLag: Among all the partitions consumed by this consumer group, it refers to the number of unconsumed data entries in the partition with the most unconsumed data.

   * TotalLag: It represents the number of unconsumed data entries of the entire consumer group at this point in time.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1097ca30182246d68689d9fea8ffc5ac~tplv-goo7wpa0wc-image.image) </span>


<span id="315f23ad"></span>
## Scenario 2: Configure alerts for the consumption delay of the consumer group


1. In the **Delay** chart, select  **···**  \> **Add Alarm**.

2. On the **Create alarm policy** page, complete the following configuration and click **Create** .

   TLS already has relevant query and analysis statements built in. The important parameter configurations are as follows. For the descriptions of other parameters, please refer to [Create alarm policies](https://docs.byteplus.com/docs/tls/create_alarm_policies).

   * Set the **Trigger condition** to **Have data** , `$1. MaxPartitionLag > 100000 | | $1. TotalLag > 500000`. The value of `MaxPartitionLag` and `TotalLag` should be evaluated in combination with the actual business.

   * Select the appropriate execution cycle, alarm cycle, and notification group.

3. Receive an alarm notification.

   When the consumption delay indicator reaches the trigger condition, you will receive an alert notification.
