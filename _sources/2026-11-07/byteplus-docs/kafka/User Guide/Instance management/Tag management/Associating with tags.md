---
title: "Associating with tags"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/associating-with-tags"
---

Message Queue for Kafka allows you to add tags to instances. You can classify Kafka instances by tag for simplified instance search and resource aggregation. This topic describes how to add tags to an instance.

<span id="92f58e36"></span>
## Tag setting rules

The tag setting rules are as follows:


|**Item** |**Description** |
|---|---|
|Tag key |* It can contain letters or characters in any language (such as Chinese and English), digits, spaces; and special characters: `_.:/=+-@`.<br><br>* A tag key must be 1 and 128 characters in length. |
|Tag value |* It can contain letters or characters in any language (such as Chinese and English), digits, spaces; and special characters: `_.:/=+-@`.<br><br>* A tag value must be 0 and 256 characters in length, allowing for an empty tag value. |
|Number of tags |* The total number of tags is unlimited, but each Kafka instance can be associated with a maximum of 50 tags.<br><br>* You can set up to 20 tags at a time. |


<span id="ce0798d4"></span>
## Setting tags for an instance


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, locate the instance and click the Edit icon in the **Tag** column.

   Alternatively, click the name of the instance. In the **Basic information** pane, click the Edit icon in the **Tag** row.

4. Specify **Tag Key** and **Tag Value**.

   Follow tag setting rules to set tags.

5. Click **OK**.


<span id="4898762e"></span>
## Batch setting tags

If the new tag key you want to set overlaps with an existing tag key associated with the selected instance, the new tag value overwrites the original tag value. Proceed with caution.


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. Select all target instances and click **Binding Tag** on the upper\-left corner of the page.

4. Specify **Tag Key** and **Tag Value**.

   Follow tag setting rules to set tags. For more information.

5. Click **OK**.
