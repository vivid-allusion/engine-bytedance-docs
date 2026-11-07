---
title: "Filtering instances by tags"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/filtering_instances_by_tags"
---

After you succeed in adding tag to an instance, you can filter instances by tag during the instance search to display the list of instances containing the specified tag. This topic describes the procedure for filtering resources by tag.

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Background information**

When searching for instances in the RDS for PostgreSQL console, if the PostgreSQL instance has tags set, you can filter and screen all instances bound with specified tags by specifying tag key and tag value. When filtering instances, you can set up to 10 tag filters. Different tags are combined with **or** relation, meaning the condition matches if any tag filter is met. Supported filtering methods are as follows:


|Filter method |Note |Example |
|---|---|---|
|Filter by tag key |Filtering by tag key means setting only the tag key during filtering, indicating viewing all instances with the specified tag key and any tag value. You can also specify multiple tag keys simultaneously for filtering, indicating viewing instances matching any filter condition.<br><br>When searching, limiting only the tag key and not the tag value suits fuzzy search scenarios. |Scenario 1: Tag key is module and tag value is empty, meaning viewing all instances with the tag key module in tags. Scenario 2: Tag keys are module and owner, both with empty values, meaning viewing all instances with the tag key module or owner in tags. |
|Filter by tag key + tag value |Filter by tag key + tag value, which means specifying both tag key and tag value to view all instances bound with the specified tag. You can also specify multiple tags for filtering, which means viewing instances that meet any of the filter criteria.<br><br>Specifying both tag key and tag value applies to precise search scenarios. |Scenario 1: The tag key is module, and the tag value is http, indicating viewing all instances with the `module:http` tag. Scenario 2: Filter condition 1 is `module:http`, and condition 2 is `module:tcp`, indicating viewing all instances where the tag key is module and the tag value is either http or tcp. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

Tags have been added to the instance. For more information, refer to [Adding a tag](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_a_tag).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* When filtering, the tag key is required, and the tag value is optional. Leaving the tag value empty indicates filtering instances without a tag value set.

* Supports setting up to 10 tags in the filter; different filter conditions use an **or** relationship.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the filter icon on the right of the **Tag** column.

4. In the pop\-up text box, set the tag key and tag value for filtering.

5. You can click **Add field** to enter multiple tag keys for filtering; multiple filter conditions use an **or** relationship.

6. Click **OK**. The Instances list displays all instance Summary that meet the filter criteria. To reset filter conditions, click **Reset** to clear all filters, then reset the filter according to step 4.
