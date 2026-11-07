---
title: "Filtering instances by tags"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/filtering_instances_by_tags"
---

After associating tags to instances, you can filter instances by tags to generate a list containing only the instances carrying the specified tags. This topic describes how to filter resources by tags.

<span id="background"></span>
## Background

If you've associated tags to RDS for MySQL instances, you can easily find instances associated with specified tags by filtering tag keys and tag values in the console. 10 tag filters can be set at the maximum for instances, with tags connected by the **OR** operator. That is, an instance meeting any one of the tag filters is regarded as a match.

Supported filters are as follows:


|**Filter Method** |**Description** |**Example** |
|---|---|---|
|Tag key |Only tag keys should be set. All instances that match the specified key string, regardless of their tag values, are regarded as a match. You can also specify multiple tag keys for filtering, so that you can view instances that meet any filter condition.<br><br>Limiting tag keys but not tag values applies to fuzzy searches. |* Scenario 1: Tag key: `module`; tag value: empty. It means to find all instances with a tag key `module`.<br><br>* Scenario 2: Tag key: `module` and `owner`; tag value: empty. It means to find all instances with a tag key of `module` or `owner`. |
|Tag key + tag value |Both a tag key and a tag value should be set. All instances that match the specified tag key and tag value—that is, all instances associated with the specified tags—are regarded as a match. You can also specify multiple tags for filtering, so that you can view instances that meet any filter condition.<br><br>Specifying both tag keys and tag values applies to exact searches. |* Scenario 1: Tag key: `module`; tag value: `http`. It means to find all instances with the tag `module:http`.<br><br>* Scenario 2: Filter 1: `module:http`; filter 2: `module:tcp`. It means to find all instances with a tag key `module` and a tag value `http` or `tcp`. |


<span id="precautions"></span>
## Precautions


* Tag key is required for filtering, while tag value is optional. If the tag value is empty, it means to find instances without a tag value set.

* 10 tags can be set as filters at the maximum. Filters are connected with the **OR** operator.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.</div>



3. On the **Instance list** page, click the filter icon to the right of the **Tag** column.

4. Enter the tag key and tag value for filtering in the text box that pops up.

   Click **Add field** to enter more tag keys as filters. Filters are connected with the **OR** operator.

5. Click **OK**.

   The instance list displays the information of all instances matching the filters.

   To reset filter conditions, click **Reset** to clear all filter conditions, and then reset filter conditions according to step 4 for filtering.
