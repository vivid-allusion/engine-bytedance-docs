---
title: "Filtering instances by tag"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/filtering-instances-by-tag"
---

Once tags are associated with an instance, you can filter a list of instances by tag when retrieving instances. This topic describes how to filter resources by tag.

<span id="背景信息"></span>
## Background information

In the Message Queue for Kafka console, if Kafka instances are tagged, you can filter instances associated with a tag by specifying the tag key and tag value. A maximum of 10 tag filters can be set when filtering instances, with different tags having an **OR** relationship, meaning a match with any one of the filtering conditions counts as a successful match.

The following filtering methods are supported:


|**Filtering Method** |**Description** |**Example** |
|---|---|---|
|Filtering by tag key |Filtering by tag key involves only setting a tag key to filter all instances with a specified string as the tag key and any value as the tag value. You can also specify multiple tag keys for filtering, indicating that instances meeting one of the filtering conditions are filtered.<br><br>During the search, only a tag key must be specified, not a tag value. This method is suitable for fuzzy search scenarios. |Scenario 1: Specify the tag key as `module` and leave the tag value empty to filter all instances with the tag key `module`.<br><br>Scenario 2: Specify tag keys as `module` and `owner` and leave the tag values empty to filter all instances with the tag key `module` or `owner`. |
|Filtering by tag key and tag value |Filtering by tag key and tag value involves specifying both the tag key and tag value to filter all instances associated with the specified tag. You can also specify multiple tags for filtering, indicating that instances meeting one of the filtering conditions are filtered.<br><br>Both tag keys and tag values must be specified. This method is suitable for exact search scenarios. |Scenario 1: Specify the tag key as `module` and the tag value as `http` to filter all instances with the tag `module:http`.<br><br>Scenario 2: Specify `module:http` as filtering condition 1 and `module:tcp` as filtering condition 2 to filter instances with the tag key as `module` and the tag value as `http` or `tcp`. |


<span id="注意事项"></span>
## Precautions


* During filtering, the tag key is required, and the tag value is optional. If you leave the tag value empty, instances without a tag value are filtered.

* You can set up to 10 tags in the filter options. The relationship between different filtering conditions is logical **OR**.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, click the filter icon on the right of the **Tag** column.

4. In the pop\-up textbox, set a tag key and a tag value.

   You can click **Add Label** to type multiple tag keys for filtering. The relationship between different filtering conditions is logical **OR**.

5. Click **OK**.

   The instance list displays all instances that meet the filtering conditions.

   To reset filtering conditions, click **Reset** to clear all filtering conditions, then repeat Step 4 to reset filtering conditions.
