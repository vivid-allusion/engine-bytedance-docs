---
title: "Adding a tag"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_a_tag"
---

You can classify MySQL instances by tags to facilitate instance search and resource aggregation. This topic describes how to create tags and add them to instances.

<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## Tagging rules

The tagging rules are as follows.


|Limits |Note |
|---|---|
|Tag key |* Supports letters or characters of any language, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* `volc:` is a system\-reserved tag key. When adding tags, the tag key cannot start with `volc:`, regardless of the case.<br><br>* The tag key must be 1 to 128 characters in length. |
|Tag value |* Supports letters or characters of any language, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>* The tag value must be 0 to 256 characters in length. A length of 0 indicates that the tag value is empty. |
|Tag quantity |* The total number of tags is unlimited, but you can bind up to 50 tags to each MySQL instance.<br><br>* You can add up to 20 tags at a time. |


<span id=".5Li65Y2V5Liq5a6e5L6L6K6-572u5qCH562-"></span>
## **Add tags to a single instance**


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. In the left navigation bar, choose **MySQL** \> **Instances**.

4. Find the target instance in **Instances** page and click on the edit icon in the **Tag** column. You can also click the name of the target instance, and then click the edit icon in the **Tag** row of the **Summary** area.

5. In the pop\-up **Edit tag** window, enter a new **Tag key** and **Tag value**, or select an existing tag from the drop\-down list. When setting tags, follow the tag setting rules. For more information, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_a_tag#.5qCH562-6K6-572u6KeE5YiZ). Click the **Add tag** button to add more tags.

6. Click **OK**.


<span id=".5Li65aSa5Liq5a6e5L6L6K6-572u5qCH562-"></span>
## Setting tags for multiple instances

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the key of a newly added tag is the same as a tag key already associated with the selected instance, the new tag value will overwrite the original one. Proceed with caution.</div>



1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the region where the instance is located.

3. In the left navigation bar, choose **MySQL** \> **Instances**.

4. On the Instances page, select all the instances to which you want to add a tag, and in the lower\-left corner of the page, click  **...**  \> **Add tag**.

5. In the **Add tag** window, enter a new **tag key** and **tag value**, or select an existing Tag from the drop\-down list. Follow the rules for adding tags. For details, refer to [Rules for adding tags](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_a_tag#.5qCH562-6K6-572u6KeE5YiZ). Click the **Add tag** button to add more tags.

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Note |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/RDS_for_MySQL/addtagstoresource) |Call the AddTagsToResource API to bind tags to one or more MySQL instances. |


&nbsp;
