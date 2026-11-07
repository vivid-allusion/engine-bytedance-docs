---
title: "Filter instances by tag"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Filter_instances_by_tag"
---

After binding tags to instances, you can filter instances by tags when searching, displaying only instances with the specified tags. This section explains the steps to filter resources by tags.

<span id="背景信息"></span>
## Background information

When searching for instances of Message Queue for RabbitMQ console, if a RabbitMQ instance has tags set, you can filter and select all instances bound with the specified tags by specifying tag keys and tag values. You can set up to 10 tag filters when filtering instances. Different tags have an OR relationship. It means that as long as any tag filtering condition is met, it will be considered a match.

The supported filtering methods include:


|Filter method |Description |Example |
|---|---|---|
|Filter by tag key |You may filter based on tag keys, that is, set only the tag keys during filtering. This indicates viewing all instances with the specified tag key and any tag value. You can also specify multiple tag keys to filter. This indicates you can view instances that meet any of the filtering conditions.<br><br>Restricting only the tag key during retrieval without limiting the tag value suits scenarios for fuzzy search. |* Scenario 1: Set the tag key as `module`, and the tag value is empty. It indicates you can view all instances with the tag key `module` in the tags.<br><br>* Scenario 2: Set the tag keys as `module` and `owner`, both with empty tag values. It indicates viewing all instances with the tag key `module` or `owner` in the tags. |
|Filter by tag key + tag value |Filter by tag key and value. It means specifying both the tag key and tag value to view all instances bound to the specified tag. You can also specify multiple tags simultaneously to filter. It will show instances that meet any of the filtering conditions.<br><br>You can specify both tag key and tag value. It suits scenarios requiring precise search. |* Scenario 1: Set the tag key as `module` and tag value as `http`. You can view all instances tagged as `module:http`.<br><br>* Scenario 2: Set the filter condition 1 as `module:http` and condition 2 as`module:tcp`. You can view all instances with the tag key `module` and tag value `http` or `tcp`. |


<span id="注意事项"></span>
## Notes


* The tag key is required for filtering, while the tag value is optional. An empty tag value means instances filtered have no tag value.

* Supports setting up to 10 tags in filter options. There is an **OR ** relationship between different filter conditions.


<span id="操作步骤"></span>
## Operation Steps


1. Log in to the [Message Queue for RabbitMQ console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located from the top menu bar.

3. On the **Instances** page, click the filter icon to the right of the **tag** column.

4. In the pop\-up textbox, set the tag keys and tag values to filter by.

   You can click **add tag** to enter multiple tag keys for filtering. Multiple filter conditions are connected by **OR ** relationship.

5. Click **Confirm.**  

   The instance list will display all instances matching the filter conditions.

   To reset filter conditions, click **Reset** to clear all filters, then set them again following step 4.
