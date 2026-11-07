---
title: "Associating or adding tag"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/associate-tag"
---

Cache for Redis supports tag management. Tags can be used to identify cloud resources, helping you label and classify similar instances based on different criteria (such as usage, type, owner and environment), making it easier to filter and manage the tags. This topic describes how to associate tags with instances.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Tag setting rules

The tag setting rules in Cache for Redis service are specified in the table below.

|Limits |Description |
|---|---|
|Tag key |* Letters of any alphabetic language (such as English) or characters (such as Chinese), numbers, spaces, and the following special characters are supported: `_.:/=+-@`.<br><br>* The tag key must be 1 to 128 characters in length.<br><br>* Tag keys are case\-sensitive. For example, `Type` and `type` are two different tag keys.<br><br>* `volc:` is a system\-reserved tag key. When adding tags, you cannot set any case variation of `volc:` as the beginning of a tag key. |
|Tag value |* Letters of any alphabetic language (such as English) or characters (such as Chinese), numbers, spaces, and the following special characters are supported:<br><br>    `_.:/=+-@`.<br><br>* Tag values are case\-sensitive. For example, `Shard` and `shard` are two different tag values.<br><br>* The tag value should be 0 to 256 characters in length, meaning that tag values can be empty. |
|Quantity |* The total number of tags is unlimited, but each Redis instance can associate up to 50 tags.<br><br>* You can add up to 20 tags at a time. |

## Precautions

* Each tag key must be unique for instance, and can have only one tag value.

* If the key of a newly added tag is the same as a tag key already associated with instance, the new tag value will overwrite the original one. Proceed with caution.

## Procedure

> **tip**

> Associating tags has no impact on instance operation.

### Associate tag for individual instance

* **Method 1**

   Associate tags directly when creating instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* **Method 2**

   1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

   2. In the top menu bar, select the project and region to which the instance belongs.

   3. On the **Instances** page, locate the target instance and click the icon in the **Tag** column.

      You can click the target instance to enter the **Summary** page, and in the **Basic information** pane, click  ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) in the **Tag** column.

   4. In the pop\-up dialog box, confirm the instance information and select existing tag keys and values from the drop\-down list according to business needs, or enter new tag keys and values.

      > **tip**

      * > If IAM users use tag resources in Redis instances, the main account needs to add the `TagFullAccess` permission policy for the IAM users globally first. Only then can the existing tags under the main account be seen in the drop\-down list. Otherwise, the drop\-down list will be empty. However, even if IAM users do not have `TagFullAccess` permission, they can still add new tags to instances. For more details, refer to [Using Redis with IAM users](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).

      * > For the tag key and tag value setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).

   5. Click **OK**.

### Associate tag for multiple instances

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, select the target instances with which tags will be associated in batch, and select  **... \> Add tag** at the lower left corner of the instance list.

4. In the pop\-up dialog box, confirm the instance information and select existing tag keys and values from the drop\-down list according to business needs, or enter new tag keys and values.

   > **tip**

   * > If IAM users use tag resources in Redis instances, the main account needs to add the `TagFullAccess` permission policy for the IAM users globally first. Only then can the existing tags under the main account be seen in the drop\-down list. Otherwise, the drop\-down list will be empty. However, even if IAM users do not have `TagFullAccess` permission, they can still add new tags to instances. For more details, refer to [Using Redis with IAM users](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).

   * > For the tag key and tag value setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).

5. Click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/redis/addtagstoresource) |Call the AddTagsToResource API to associate tags with a specified instance. |
