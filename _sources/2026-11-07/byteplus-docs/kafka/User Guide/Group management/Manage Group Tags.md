---
title: "Manage Group Tags"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/group-tags"
---

Tags are used to identify and classify cloud resources. Kafka supports adding tags to groups. You can classify groups by tags, which is beneficial for identifying and managing groups.

<span id="42c78b0c"></span>
## Tag setting rules

The tag setting rules are as follows:


|**Item** |**Description** |
|---|---|
|Tag key |* It can contain letters or characters in any language (such as Chinese and English), digits, spaces; and special characters: `_.:/=+-@`.<br><br>* A tag key must be 1 and 128 characters in length. |
|Tag value |* It can contain letters or characters in any language (such as Chinese and English), digits, spaces; and special characters: `_.:/=+-@`.<br><br>* A tag value must be 0 and 256 characters in length, allowing for an empty tag value. |
|Number of tags |* The total number of tags is unlimited, but each Kafka instance can be associated with a maximum of 50 tags.<br><br>* You can set up to 20 tags at a time. |


<span id="c13da2d0"></span>
## Edit Tags

After the group tag is added, it supports editing capabilities, including modifying tag key value information, adding tags, unbinding tags, and other operations.


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. In the left\-side navigation pane, click **Instances**. Click the name of the target instance.

4. Click the **Group Management** tab.

5. On the Group list page, select the target Group, and then click the edit icon below the **Tag** column.

6. In the **Edit Tag** dialog box, edit, add, and unbind tags as needed, and then click **OK**.


<span id="c1ed9ff9"></span>
## Filter Group by tag

When searching for groups, if groups have been tagged, you can filter them by specifying the tag key and tag value to find all groups bound to the specified tag.


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. In the left\-side navigation pane, click **Instances**. Click the name of the target instance.

4. Click the **Group Management** tab.

5. On the Group list page, click the filter icon behind the tag.

6. In the pop\-up text box, enter the tag name and tag value, and then click **OK**.

   * During screening, the tag key is required, and the tag value is optional. If the tag value is empty, only Group will be filtered based on the tag.

   * Support inputting up to 10 tags for filtering, and the relationship between different filtering conditions is **OR**, that is, if any tag filtering condition is met, the matching is successful.


<span id="95aea838"></span>
## Batch binding tag

If you need to add the same tag to multiple groups, you can use batch binding. When adding tags in batches, if the new bound tag key coincides with the bound tag key of the selected group, the new tag value will overwrite the original tag value. Please be careful.


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. In the left\-side navigation pane, click **Instances**. Click the name of the target instance.

4. Click the **Group Management** tab.

5. On the Group list page, check the groups that need to be bound with tags in batches, and then click **Binding Tag**.

6. In the **Binding Tag** dialog box, review the prompt message, then set multiple tag keys and tag values as needed, and click **OK**.


<span id="71ff4f1d"></span>
## Batch Remove tag

If multiple groups need to remove tags, batch unbinding can be used. When batch unbinding tags, select the tag key you want to unbind, and all tags corresponding to the tag key will be unbound. Please operate with caution.


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. In the left\-side navigation pane, click **Instances**. Click the name of the target instance.

4. Click the **Group Management** tab.

5. On the Group list page, check the groups that need to be untagged in batches, and then click **Remove Tag**.

6. In the **Remove Tag** dialog box, view the prompt message, select the multiple tag keys that need to be unbound, and then click **OK**.
