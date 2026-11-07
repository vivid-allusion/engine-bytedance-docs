---
title: "Exporting a list of topics"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/exporting-topics"
---

In scenarios like instance backups and image instances, quickly accessing the configurations of multiple topics is essential for batch creating topics in new instances. This topic describes how to export a list of topics.

<span id="bbf3a89e"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Topic management** tab.

5. On the upper\-right corner of the page, click Export Topic.

   The browser automatically downloads the configuration list of topics to your local device.

6. View the downloaded file.

   The topic configuration list is in CSV format, containing the following configurations for all topics in this instance: Topic name, description, partition count, replica count, minimum in\-sync replica count, message retention period, maximum message size, and user permissions.


<span id="06cb24da"></span>
## Related operations

Once topics are exported, you can use the configuration file to batch create topics in a new Kafka instance. For more information, refer to [Batch importing topics](https://docs.byteplus.com/en/docs/kafka/batch-importing-topics).
