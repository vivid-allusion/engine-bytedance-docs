---
title: "Bind tags"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Bind_tags"
---

The Message Queue for RabbitMQ supports adding tags to instances. You can classify RabbitMQ instances using tags for convenient instance search and resource aggregation. This section describes the steps to add tags to instances.

<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## Tag settings rules

The rules for setting tags are as follows:


|Constraints |Description |
|---|---|
|Tag key |* Supports letters or characters from any language (such as Chinese, English letters, etc.), numbers, and spaces; supports special characters `_.:/=+-@`.<br><br>* Tag key length must be between 1 and 128 characters. |
|Tag value |* Supports letters or characters from any language (such as Chinese, English letters, etc.), numbers, and spaces; supports special characters `_.:/=+-@`.<br><br>* The tag value length must be between 0 and 256 characters, meaning the tag value can be empty. |
|Number of tags |* The total number of tags is unlimited, but each RabbitMQ instance can bind up to 50 tags.<br><br>* You can add up to 20 tags each time. |


<span id=".5Li65p-Q5Liq5a6e5L6L6K6-572u5qCH562-"></span>
## Set tags for an instance


1. Log in to the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq).

2. Select the region of the instance in the top menu bar.

3. On the **Instances** page, find the specified instance and click the edit icon in the **Tag** column.

   You can also click the instance name, then click the edit icon in the **Tag** column within the **Basic information** section.

4. Set the **Tag key** and **Tag value**.

   Follow the tag setting rules when setting tags. For details, see the [tag setting rules](https://docs.byteplus.com/en/docs/rabbitmq/Bind_tags#.5qCH562-6K6-572u6KeE5YiZ).

5. Click **OK**.


<span id=".5om56YeP6K6-572u5qCH562-"></span>
## Set tags in bulk

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the newly bound tag key overlaps with an existing tag key on the selected instance, the new tag value will overwrite the original tag value. Proceed with caution.</div>



1. Log in to the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq).

2. Select the region of the instance in the top menu bar.

3. Select all instances that need tags, then click **Binding Tags**.

4. Set the **Tag key** and **Tag value**.

   Follow the tag setting rules when setting tags. For details, see the [tag setting rules](https://docs.byteplus.com/en/docs/rabbitmq/Bind_tags#.5qCH562-6K6-572u6KeE5YiZ).

5. Click **OK**.
