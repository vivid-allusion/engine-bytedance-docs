---
title: "Filter resources by tag"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Filter_resources_by_tag"
---

After you attach tags to cloud resources, you can search for cloud resources by tag. For example, you specify a tag as a condition to search for projects. This topic describes how to search for projects based on tags.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

You have attached tags to your projects on Torch Log Service (TLS). When you search for projects in the TLS console, you can specify tag keys and tag values for filtering projects. You can specify up to 10 tags when searching for projects. The logical relationship among the specified tags is **OR**, that is, the projects to which any one of the specified tags are attached are displayed in the search result list.

The following filter methods are supported:


|Filter Method |Description |Example |
|---|---|---|
|Filter by tag key |TLS allows you to specify only a tag key as a condition to search for projects. If you use this filter method, the projects with the specified tag key and any tag values are displayed in the search result list. You can specify multiple tag keys to search for the projects that meet any of the filter conditions.<br><br>When using this method, the search results are determined only by tag keys, not tag values. This method is suitable for fuzzy matching scenarios. |* Example 1: Specify the tag key `module` and leave the tag value column empty to search for all projects that have tags with the `module` key.<br><br>* Example 2: Specify the tag keys `module` and `owner` and leave the tag value column empty to search for all projects that have tags with the `module` or `owner` key. |
|Filter by tag key and tag value |TLS allows you to specify a tag key and tag value as one condition to search for projects. If you use this filter method, the projects with the specified tag key and tag value are displayed in the search result list. You can specify multiple tags to search for the projects that meet any of the filter conditions.<br><br>This method is suitable for exact matching scenarios. |* Example 1: Specify a condition with `module` as the tag key and `http` as the tag value to search for all projects that have the `module:http` tag.<br><br>* Example 2: Specify `module:http` and `module:tcp` as two conditions to search for all projects that have a tag with `module` as the tag key and `http` or `tcp` as the tag value. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* For filter conditions, tag keys are required and tag values are optional. If the label value is empty, it means filtering all log items under that label key.

* You can specify up to 10 tags as conditions in each search, and the logical relationship among the conditions is **OR**.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

3. Select the target project, then click the project name.

4. In the **Tag** column of **Topic** area, click **Filter** icon. Then specify the tag keys and tag values that you want to use as conditions.

   To specify multiple conditions, click **Add tag** to add tags as conditions. The logical relationship among multiple filter conditions is **OR**.

5. Click **OK**.
