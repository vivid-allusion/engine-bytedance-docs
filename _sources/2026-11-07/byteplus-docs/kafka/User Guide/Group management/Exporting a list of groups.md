---
title: "Exporting a list of groups"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Exporting-groups"
---

In scenarios like instance backups and image instances, quickly accessing the configurations of multiple groups is essential for batch creating groups in new instances. This topic describes how to export a list of groups.

<span id="bbf3a89e"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instances**.

3. Click the name of the target instance.

4. Click the **Group Management** tab.

5. On the upper\-right corner of the page, click Export Group.

   The browser automatically downloads the configuration list of groups to your local device.

6. View the downloaded file.

   The group configuration list is in CSV format, containing the group ID and description for all groups in this instance.


<span id="06cb24da"></span>
## Related operations

Once groups are exported, you can use the configuration file to batch create groups in a new Kafka instance. For more information, refer to [Batch importing groups](https://docs.byteplus.com/en/docs/kafka/importing-groups).
