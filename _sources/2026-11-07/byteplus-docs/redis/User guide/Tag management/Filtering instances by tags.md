---
title: "Filtering instances by tags"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/filter-by-tag"
---

After associating tags with instances, you can filter instances by tags in the instance list of the Redis console to quickly find instances with specified tags. This topic describes the detailed procedure for filtering instances by tags.

## Precautions

* When filtering, the tag key is required and the tag value is optional. Not entering a tag value means no restrictions are placed on the tag value, and all instances associated with the specified tag key will be searched.

* A maximum of 10 tags can be set for filtering at one time, and the different filtering conditions are an **OR** relationship.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, on the right side of **Tag** column click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64d3d8547df5760a41a50d1a2f6b6f49.png) icon.

4. In the pop\-up box, set the tag keys and tag values to be filtered.

   You can click **Add tag** to enter multiple tag keys for filtering. The different filtering conditions are an OR relationship.

5. After clicking **OK**, you can view all instance information matching the filter criteria in the instance list below.

   To reset filter conditions, first click **Reset** to clear all existing conditions. Then, follow Step 4 to set new conditions for filtering.

## Tag filtering example

|Filtering method |Description |Example |
|---|---|---|
|Filter by tag key |* When filtering, if only tag keys are specified, all instances with tag keys containing the specified string of characters are viewed, regardless of the tag values.<br><br>* You can also specify multiple tag keys for filtering, which means that you want to view instances that meet any of the filtering criteria.<br><br>* When searching, restricting only the tag key and not the tag value is suitable for fuzzy search scenarios. |* Filter example 1<br><br>   * Filtering conditions<br><br>      Set tag key `department`, with an empty tag value.<br><br>   * Filter results<br><br>      All Redis instances containing `department` tag key will be filtered out.<br><br>* Filter example 2<br><br>   * Filtering conditions<br><br>      Set tag keys `department` and `owner`, with both tag values empty.<br><br>   * Filter results<br><br>      All Redis instances containing either `department` or `owner` tag keys will be filtered. |
|Filter by tag key and tag value |* When filtering, specifying both the tag key and tag value displays all instances associated with the specified tag.<br><br>* You can also specify multiple tags simultaneously for filtering to view instances that meet any of the filter conditions.<br><br>* Specifying both the tag key and tag value is suitable for precise search scenarios. |* Filter example 1<br><br>   * Filtering conditions<br><br>      Set tag `department:game`.<br><br>   * Filter results<br><br>      All Redis instances containing `department:game` tag will be filtered out.<br><br>* Filter example 2<br><br>   * Filtering conditions<br><br>      Set tag keys `department:game` and `owner:Bob`.<br><br>   * Filter results<br><br>      All Redis instances containing `department:game` or `owner:Bob` tags will be filtered out. |

## Relevant APIs

|API |Description |
|---|---|
|[DescribeTagsByResource](https://docs.byteplus.com/en/docs/redis/describetagsbyresource) |Call the DescribeTagsByResource API to query the information of tags associated with instance. |
