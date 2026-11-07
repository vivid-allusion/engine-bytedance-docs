---
title: "Adding a tag"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/associating_a_tag"
---

RDS for PostgreSQL supports adding tags to instances, categorizing PostgreSQL instances through tags to facilitate instance search and resource aggregation. This topic describes how to create tags and add them to instances.

<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## **Tag setting rules** The rules for setting tags are as follows.


|Limits |Note |
|---|---|
|Tag key |Supports letters or characters of any language, digits, spaces, and the following special characters: `_.:/=+-@`. `volc:` is a system\-reserved tag key. When adding tags, the tag key cannot start with any case form of `volc:`. The tag key must be 1 to 128 characters in length. |
|Tag value |Supports letters or characters of any language, digits, spaces, and the following special characters: `_.:/=+-@`. the tag value must be 0 to 256 characters in length, which means the tag value can be empty. |
|Tag quantity |The total tag quantity is unlimited, but each PostgreSQL instance can bind up to 50 tags. You can add up to 20 tags at a time. |


<span id=".5Li65Y2V5Liq5a6e5L6L6K6-572u5qCH562-"></span>
## **Add tags to a single instance**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Find the target instance in **Instances** page and click on the edit icon in the **Tag** column. You can also click the name of the target instance, and then click the edit icon in the **Tag** row of the **Basic information** area.

4. In the pop\-up **Edit tag** window, set the **tag key** and **tag value**. When setting tags, follow the tag setting rules. For details, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_a_tag#.5qCH562-6K6-572u6KeE5YiZ). Click the **Add tag** button to add more tags.

5. Click **OK**.


<span id=".5Li65aSa5Liq5a6e5L6L6K6-572u5qCH562-"></span>
## **Setting tags for multiple instances**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the key of a newly added tag is the same as a tag key already associated with the selected instance, the new tag value will overwrite the original one. Proceed with caution.</div>



1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the instances list, select all the target instances and click **Add tag** in the lower\-left corner of the page.

4. In the pop\-up **Add tag** window, set the **tag key** and **tag value**. Follow the tag setting rules when setting tags. For details, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_a_tag#.5qCH562-6K6-572u6KeE5YiZ). You can also add multiple tags by clicking the **Add tag** button.

5. Click **OK**.
