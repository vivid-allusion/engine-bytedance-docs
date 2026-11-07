---
title: "Viewing node information"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-broker-information"
---

This topic describes how to view broker information about an instance in the console, facilitating the daily operations and monitoring of the instance.

<span id="700ca59f"></span>
## Background information

Message Queue for Kafka offers a broker list for instances. You can view the number of partitions and leader partitions for each broker of a specified instance in the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The number of brokers in an instance depends on the instance type. Typically, a more advanced instance type supports more brokers. The <strong>Node information</strong> tab of an instance displays the number of brokers for the corresponding instance type.</div>


<span id="becc4c12"></span>
## Viewing the broker list of an instance

To view the broker information about a Kafka instance in the console:


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, click the name of the instance.

4. On the **Node information** tab, view the broker list of the current instance.

   The items are described as follows:

   
   |Item |Description |
   |---|---|
   |Broker ID |The broker ID of the current Kafka instance.<br><br>In cases of abnormal broker status, the back\-end service automatically replaces the faulty broker and swiftly redirects traffic. Broker switching leads to changes in the broker ID but does not affect service stability. |
   |No. of Partitions |The number of partitions in the specified broker.<br><br>If the number of partitions varies greatly among brokers, those with more partitions may have higher business traffic and disk utilization, leading to a higher disk skew rate. We recommend that you use a suitable data writing method and set the number of partitions properly. For example, set the number of partitions for a topic to be a multiple of the number of brokers, ensuring that data is evenly written to the brokers of the instance. |
   |No. of Leaders |The number of leader partitions. The leader handles all read and write requests for the partition, and followers automatically replicate data from the leader. |
   

   Example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdfd0d59f8d74d8fa84bfc9b09c81dad~tplv-goo7wpa0wc-image.image) </span>
