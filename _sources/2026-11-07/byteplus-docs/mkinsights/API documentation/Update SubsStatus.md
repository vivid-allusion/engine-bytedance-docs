---
title: "Update SubsStatus"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/UpdateSubsStatus"
---

Enable or pause a monitoring task under the current account.

Set `Status` to `1` to enable the task or `0` to pause it. This API does not delete monitoring tasks and does not accept `-1` as a status value.

To delete a monitoring task, use the DisableSubsTask API.

<span id="ElqXEqAl"></span>
## Request information


|**Item** |**Description** |
|---|---|
|Environment |BytePlus production |
|HTTP method |POST |
|Request body format |application/json |
|API method |UpdateSubsStatus |
|TOP Action |UpdateSubsStatus |
|Version |2026\-03\-24 |
|Service (signature) |mkt_insight |
|Region (signature) |ap\-southeast\-1 |
|Request domain |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Complete request URL |[https://mkt-insight.byteplusapi.com/?Action=UpdateSubsStatus&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=UpdateSubsStatus&Version=2026-03-24) |
|Authentication |Use a BytePlus production AK/SK pair to generate the Authorization header according to the standard signature protocol. Include Action and Version in the query string and business parameters in the JSON request body. |


<span id="PL6Na7H5"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskID` |Int64 |Yes |ID of an existing monitoring task owned by the current account. The task must not have been deleted, and the value must be greater than `0`. Parameter names are case\-sensitive. |
|`Status` |Int32 |Yes |Target status of the monitoring task. Set the value to `1` to enable the task or `0` to pause it. This field must be provided explicitly and cannot be omitted, set to `null`, set to `-1`, or set to any other value. |


<span id="4hysD4j1"></span>
## Usage notes

Enabling or pausing a task preserves its configuration. Pausing is not the same as deletion and does not guarantee that posts already in the processing pipeline will be withdrawn. The API strictly validates account ownership and cannot operate on another account's tasks.

<span id="SAyE9RIv"></span>
## Response parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Result.TaskID` |Int64 |Yes |ID of the monitoring task whose status was updated successfully. |
|`Result.Status` |Int32 |Yes |Status set by this request. The value is `1`for enabled or `0` for paused. |


<span id="lGuCgxbD"></span>
## Request example

```JSON
{
  "TaskID": 123456,
  "Status": 0
}
```


<span id="uAcfCDBi"></span>
## Response example

```JSON
{
  "Result": {
    "TaskID": 123456,
    "Status": 0
  },
  "ResponseMetadata": {
    "RequestId": "example-request-id"
  }
}
```


To re\-enable the task, change Status in the request to 1.

<span id="wFars8A9"></span>
## Error codes


|**Code** |**Service HTTP status** |**Description** |
|---|---|---|
|`InvalidParameter` |400 |A parameter value or business\-format definition is invalid. This error can also be returned when the JSON request body is malformed, a required field is missing, or the rule expression cannot be compiled. |
|`Unauthorized` |403 |The caller could not be authenticated or does not have permission to update the specified task. |
|`RecordNotFound` |400 |The specified task does not exist, has been deleted, or is not owned by the current account. |
|`InternalError` |500 |The service failed to process the request because of an internal error. |


Requests with missing required fields or malformed JSON are rejected. For gateway errors, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
