---
title: "Associating tag"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-tag"
---

RDS for SQL Server supports adding tags to instances, through which SQL Server instances are classified for easy instance search and resource aggregation. This document describes the steps to create a tag and add a tag to an instance.

<span id="tag-setting-rules"></span>
## Tag setting rules

The setting rules for tags are as follows:


|**restriction** |**explain** |
|---|---|
|Tag key |* Support any language letters or characters (such as Chinese, English letters, etc.), numbers, spaces; support special characters: `_ .:/=+-@`.<br><br>* `volc:` A tag key reserved for the system. When adding tags, the beginning of the tag key cannot be set to any upper or lower case `volc:`.<br><br>* The length of the tag key should be between 1 and 128 characters. |
|Tag value |* Support any language letters or characters (such as Chinese, English letters, etc.), numbers, spaces; support special characters: `_ .:/=+-@`.<br><br>* The length of the tag value should be 0 to 256 characters, that is, the tag value can be empty. |
|number of tags |* The total number of tags is unlimited, but each SQL Server instance can bind up to 50 tags.<br><br>* You can add up to 20 tags per setup. |


<span id="taging-for-a-single-instance"></span>
## Taging for a single instance


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Locate the target instance on the **Instances list** page and click the edit icon in the **tab** column. You can also click the name of the target instance and click the edit icon in the tab line of the basic area.

4. In the pop\-up **Edit tag** window, set the **tag key** and **tag value**. tag setting rules should be followed when setting tags, please refer to the [tag setting rules ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-tag#tag-setting-rules)for details. You can also add multiple tags by clicking the **Add tag** button.

5. Click **OK**.


<span id="set-tags-for-multiple-instances"></span>
## Set tags for multiple instances

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the newly bound tag key coincides with the selected instance's bound tag key, the new tag value will overwrite the original tag value, please proceed with caution.</div>



1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. In the Instances list, select all instances that need to be taged, and click **Bind tags** in the lower left corner of the page.

4. In the pop\-up **binding tag** window, set the **tag key** and **tag value**. tag setting rules should be followed when setting tags, please refer to the [tag setting rules ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-tag#tag-setting-rules)for details. You can also add multiple tags by clicking the **Add tag** button.

5. Click **OK**.
