---
title: "OpenAPI"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/OpenAPI_"
---

<span id="bec39a18"></span>
# Use consultation

<span id="c645a66e"></span>
## What is the QPS of OpenAPI's interface for obtaining the number of groups, and is there any pressure test data?


* The interface recommends no more than 1 million pieces of data.

* Using streaming grouping export interface, support grouping query within 300w. It is recommended to call uniformly to avoid concurrent use of this interface.


Please see for details [Get the User List Information for the Specified Cohorts](https://docs.byteplus.com/docs/DataFinder/Get_the_User_List_Information_for_the_Specified_Cohorts).

<span id="9f7170aa"></span>
## Use cluster OpenAPI to get the user list information of the specified cluster. Can you set paging to get data?

There is currently no paging function.

<span id="d77427af"></span>
## What are the meanings of the beginTime and endTime parameters when using DSL statements for data queries?

The actual meaning of the beginTime and endTime parameters depends on the time granularity chosen. For example, if the time granularity is "by day", beginTime and endTime should be date ranges.

<span id="1a20278a"></span>
## What state of clustered data can be returned when using OpenAPI that fetches clustered data?

If the "status" status is refresh, error, timeout, grouping pending, data can be retrieved, but the data may not be accurate. If the "status" status is an error or a timeout, the previous day's result is obtained.

<span id="239e2e11"></span>
## When using OpenAPI for getting clustered data, is downloading user clustered data real\-time?

The user grouping user list data downloaded by OpenAPI is the latest refresh data.

<span id="e064b4bb"></span>
## Dashboard query function related to OpenAPI, can I refresh the cache?

No, no parameters can trigger to refresh the cache, and the calculated Dashboard data is obtained.

<span id="ddbe2994"></span>
## What is the difference between the csv file downloaded by OpenAPI download and the csv file downloaded by page event analysis?

There is no difference. If the query conditions are consistent, then the exported data is also consistent.

<span id="072005e8"></span>
## Does OpenAPI's javaSDK have maven? Where is Maven's dependency address?

OpenAPI javaSDK is not placed in the maven repository, you can get the jar package in the official website documentation: [Call Method](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52).

<span id="8a1dc884"></span>
# Call error

<span id="78d19481"></span>
## Returns "code": 400, "message": "User is not in this group", "fmt_params": {}

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14783894de064e30b32a9c4a9e429fb6~tplv-goo7wpa0wc-image.image) </span>

Solution: Confirm whether the aksk used is correct, and ensure that the account applied for by the aksk is there, the corresponding user is under the group and has the corresponding project authority

<span id="3b8cdc20"></span>
## Error "Expecting value: line 1 column 2 (char 10" when calling the user to analyze OpenAPI

Check if the body json format is normal


1. Body key with double quotes

2. JS can be converted by methods such as JSON.stringify


<span id="01bca7a3"></span>
# Abnormal query result

<span id="d88331c7"></span>
## After calling OpenAPI to get Bitable data, the data is incorrect?

Bitable Dashboard cannot be checked by OpenAPI to check the report, because Bitable's DSL is very complicated, and the return format is also different from event analysis, so it cannot be queried by OpenAPI to check the report.

<span id="2c4f22fd"></span>
## When calling the report API (Query Report Information API), the event occurrence time parameter does not take effect?

When using the report API interface, if a date range is included in the filter criteria, the date range of the actual query is subject to the time filter parameter passed in.

If the event filter parameter does not take effect, it may be caused by the inconsistency between the set filter time granularity and the query time granularity. For example, if you set the granularity of the time filter parameter period to be monthly ("granularity": "month"), the DataFinder will automatically complete the data for the current month. If the time granularity when querying the data is sky\-granularity, there may be more data than expected due to automatic completion. At this point, you need to change the time filter granularity to the day granularity ("granularity": "day"), which is consistent with the time granularity at the time of the query.

<span id="5ed1c31f"></span>
## No data returned when calling the "Get Custom Export Data File Inventory" API/Submitted the export task but could not query the file?

Solution:


1. Confirm whether the application has enabled the data export function. If not, you need to open it first and then operate it.

2. Confirm whether the currently used DataFinder environment is the same as the interface environment. DataFinder distinguishes between different types of environments such as SaaS\-cloud\-native, SaaS\-non\-cloud\-native, and privatization. The interfaces of different environments are different, and it is necessary to confirm whether the correct environment interface is used.

3. Check whether a task with the date of this query has been submitted. If data on the same date has not been submitted before, the file may not be queried.

4. It is recommended to use the query API (/openapi/v1/analysis) for data queries rather than the get file manifest interface.

5. Verify that Event Query (query_type) is selected.

6. If the query API returns empty data, it is possible that the data export task was not successfully submitted or the task was closed.

7. If the data export task is not successfully submitted, you can try resubmitting the task.


<span id="1b2fb35a"></span>
## In SaaS\-cloud\-native\-cloud hosting environment, there is an exception when calling the user grouping API to query more than 1 million user IDs, prompting request timed out: 504 Gateway Time\-out?

In this scenario, you need to use the streaming interface to query, for details, see [Download the Specified Cohorts User List Information (Streaming)](https://docs.byteplus.com/docs/DataFinder/Download_the_Specified_Cohorts_User_List_Information_Streaming).
