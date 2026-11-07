---
title: "Filtering instances by tag"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Filtering_instances_by_tag"
---

After associating tags with instances, you can filter instances by tags in the instance list of the console to quickly find instances that contain the specified tags. This topic contains instructions on how to filter instances by tags.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A tag is identified by a set of key\-value pairs. When filtering, the tag key is required and the tag value can be empty. When the tag value is empty, only the instances with empty tag values corresponding to the specified tag key are filtered out.

* 10 tags can be set as filters at the maximum. Filters are connected with the **OR** operator.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the **Filter** icon for the **Tag** column.

4. In the pop\-up text box, select the tag key and tag value to be filtered from the drop\-down list. Multiple filtering conditions are in an **OR** relationship.

5. After clicking **OK**, you can view all the instance information that meets the filter criteria in the instance list below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To reset the filter criteria, first click <strong>Reset</strong> to clear all filter criteria, and then reset the conditions to filter.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) |Call the DescribeDBInstances to query the instance list. |
