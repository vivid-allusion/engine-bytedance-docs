---
title: "Disable SubsTask"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/DisableSubsTask"
---

Deletes an existing monitoring task owned by the current account.

Although the API is named DisableSubsTask, it performs a deletion rather than temporarily pausing the task. The operation cannot be undone through the current API version.

<span id="68s9mjt4"></span>
## Request information


|**Item** |**Description** |
|---|---|
|Environment |BytePlus production |
|HTTP method |POST |
|Request body format |application/json |
|API method |DisableSubsTask |
|TOP Action |DisableSubsTask |
|Version |2026\-03\-24 |
|Service (signature) |mkt_insight |
|Region (signature) |ap\-southeast\-1 |
|Request domain |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Complete request URL |[https://mkt-insight.byteplusapi.com/?Action=DisableSubsTask&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=DisableSubsTask&Version=2026-03-24) |
|Authentication |Use a BytePlus production AK/SK pair to generate the Authorization header according to the standard signature protocol. Include Action and Version in the query string and business parameters in the JSON request body. |


<span id="jv45QInB"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskID` |Int64 |Yes |ID of an existing monitoring task to delete. The task must be owned by the current account, and the value must be greater than 0. |


<span id="7uZc80Ta"></span>
## Usage notes

After deletion, the task can no longer be accessed through the current\-version task details, update, enable/pause, or data retrieval APIs. To disable a task temporarily, call the enable/pause API with `Status=0`. Deletion does not mean that all stored posts are immediately erased from physical storage, and no recovery API is provided.

Deleting an already deleted task returns RecordNotFound rather than another success response. A request can delete only a task owned by the current account.

<span id="REm0H3Bu"></span>
## Response parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Result.TaskID` |Int64 |Yes |ID of the task deleted successfully. |


The response contains only the task ID and does not include Status.

<span id="2JjVymcN"></span>
## Request example

```JSON
{
  "TaskID": 123456
}
```


<span id="DRnoH4gA"></span>
## Response example

```JSON
{
  "Result": {
    "TaskID": 123456
  },
  "ResponseMetadata": {
    "RequestId": "example-request-id"
  }
}
```


<span id="UG26xj89"></span>
## Error codes


|**Code** |**Service HTTP status** |**Description** |
|---|---|---|
|`InvalidParameter` |400 |A parameter value or business\-format definition is invalid. This error can also be returned when the JSON request body is malformed, a required field is missing, or the rule expression cannot be compiled. |
|`Unauthorized` |403 |The caller could not be authenticated or does not have permission to update the specified task. |
|`RecordNotFound` |400 |The specified task does not exist, has been deleted, or is not owned by the current account. |
|`InternalError` |500 |The service failed to process the request because of an internal error. |


Requests with missing required fields or malformed JSON are rejected. For gateway errors, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
