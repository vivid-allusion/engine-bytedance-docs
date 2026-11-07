---
title: "Get Monitoring Task"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/GetMonitorTask"
---

Retrieves the details of an existing, non\-deleted monitoring task owned by the current account.

The response includes the task configuration shared with the CreateMonitorTask and UpdateMonitorTask APIs, the task’s enabled or paused status, and its creation and update times.

<span id="y067MRJV"></span>
## Request information


|**Item** |**Description** |
|---|---|
|Environment |BytePlus production |
|HTTP method |POST |
|Request body format |application/json |
|API method |GetMonitorTask |
|TOP Action |GetMonitorTask |
|Version |2026\-03\-24 |
|Service (signature) |mkt_insight |
|Region (signature) |ap\-southeast\-1 |
|Request domain |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Complete request URL |[https://mkt-insight.byteplusapi.com/?Action=GetMonitorTask&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=GetMonitorTask&Version=2026-03-24) |
|Authentication |Use a BytePlus production AK/SK pair to generate the Authorization header according to the standard signature protocol. Include Action and Version in the query string and business parameters in the JSON request body. |


<span id="nRdUy05X"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskID` |Int64 |Yes |ID of an existing, non\-deleted monitoring task owned by the current account. The value must be greater than 0. |


<span id="sHp8uhUg"></span>
## Response parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Result.Task` |MonitorTaskDetail |Yes |Details of the specified monitoring task. |
|`Result.Task.TaskID` |Int64 |Yes |Task ID. |
|`Result.Task.Config` |MonitorTaskConfig |Yes |Current task configuration represented by the unified configuration protocol. It can be used as the basis for a complete configuration update, subject to the source\-representation considerations described on this page. |
|`Result.Task.Status` |Int32 |Yes |Current task status. Supported values are 1 for enabled and 0 for paused. Details are not returned for a deleted task. |
|`Result.Task.CreatedAt` |String |No |Task creation time in RFC 3339 format, including the time\-zone offset. |
|`Result.Task.UpdatedAt` |String |No |Time of the most recent task update in RFC 3339 format, including the time\-zone offset. |


<span id="B5CVtvcu"></span>
### MonitorTaskConfig


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskName` |String |Yes |Currently saved task name. |
|`RuleExpression` |String |Yes |Keyword expression reconstructed from the task's saved retrieval configuration. See the expression format below. |
|`DomainSelector` |DomainSelector |No |The monitoring source scope saved for the task. It is not recalculated using the default sources at query time. |
|`RelatedRequirement` |String |No |The relevance evaluation requirements currently saved for the task. If relevance evaluation is not configured, an empty string "" is returned, indicating that the task currently performs initial filtering only. This field represents a relevance requirement rather than a complete model prompt.  |
|`Description` |String |No |The description currently saved for the task. If no description is configured, an empty string "" is returned. |


<span id="MRvJIznn"></span>
### DomainSelector


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`DomainTypeList` |Array<String\> |No |Site types saved for the task. This field may be omitted if the task stores its source scope as specific domains. |
|`DomainList` |Array<String\> |No |Specific site domains saved for the task. For a task originally configured using site types, this field may contain the expanded list of domains resolved when the configuration was saved. |


The returned source fields reflect the source scope saved for the task.

&nbsp;

The following rules apply:


* Retrieving task details does not recalculate the source scope using the service’s current enabled\-source configuration.

* The returned DomainSelector is not guaranteed to preserve the exact representation submitted when the task was created or last updated.

* A task created using DomainTypeList may be returned with an expanded DomainList.

* The returned domain list represents the saved source scope and does not automatically include sites added to the corresponding site type after the configuration was saved.

* Disabled or no\-longer\-supported domains may still appear if they are part of the task’s saved historical configuration.


> Important: If a returned DomainTypeList has been converted into an expanded DomainList, submitting the returned Config directly to UpdateMonitorTask may save the task as a fixed domain selection. The task may therefore stop automatically following later changes to that site type. Review DomainSelector before using the returned configuration in a full update.


<span id="nIlS1u2j"></span>
### Keyword expression

Use `/` as the OR operator within a keyword group and `+` as the AND operator between groups. 

For example, `(apple/iphone)+(battery/charging) `matches posts that contain apple or iphone and also contain battery or charging. 

The following rules apply:


* An expression can contain no more than two AND groups.

* Use / to separate alternative keywords within a group.

* Use + to connect AND groups.

* Each group can be enclosed in one level of parentheses.

* Nested parentheses are not supported.

* Empty keywords and empty groups are not supported.

* Leading and trailing whitespace is removed from each keyword.

* The expression can contain no more than 1,000 keywords in total across all groups.

* Duplicate keywords are not automatically removed and still count toward the 1,000\-keyword limit.


The returned expression is reconstructed from the retrieval configuration currently saved for the task. Its formatting may differ from the original submitted text while retaining equivalent retrieval semantics.

> If `/`, `+`, `(`, or `)` can appear as literal characters in a keyword, the API documentation should also specify the corresponding escaping rules.


<span id="mGHOtSDS"></span>
## Usage notes

Using the returned configuration for an update

Result.Task.Config represents the task’s current configuration and can be used as the basis for a complete update through UpdateMonitorTask.

&nbsp;

Before submitting it:


* Review all fields because UpdateMonitorTask replaces the complete configuration.

* Review DomainSelector in particular because the returned representation may differ from the representation originally submitted.

* Modify the required fields.

* Submit the complete Config object.


Do not submit only the field that you want to change.

**Empty optional fields**

When RelatedRequirement or Description is not configured, the corresponding field is returned as an empty string.

&nbsp;

An empty RelatedRequirement means that the task currently performs initial filtering only. It does not mean that:


* Existing post results have been deleted.

* Previously processed posts have been reevaluated.

* Posts currently in the processing pipeline have been cleared.


**Historical task compatibility**

This API returns tasks that can be represented by the current unified configuration protocol.

**Task status**

Status indicates only whether the monitoring task is enabled or paused:


* 1: Enabled

* 0: Paused


**Request example**

```JSON
{
  "TaskID": 123456
}
```


<span id="Pjq7xKhy"></span>
## Response example

```JSON
{
  "Result": {
    "Task": {
      "TaskID": 123456,
      "Config": {
        "TaskName": "Mobile Phone Battery Monitoring",
        "RuleExpression": "(apple/iphone)+(battery/charging)",
        "DomainSelector": {
          "DomainList": [
            "twitter.com",
            "reddit.com"
          ]
        },
        "RelatedRequirement": "Focus on users’ real-world battery life and charging experience when using their phones, excluding purely promotional ads.",
        "Description": "Monitor product usage feedback"
      },
      "Status": 1,
      "CreatedAt": "2026-09-19T10:00:00+08:00",
      "UpdatedAt": "2026-09-19T11:00:00+08:00"
    }
  },
  "ResponseMetadata": {
    "RequestId": "example-request-id"
  }
}
```


<span id="JM65isNI"></span>
## Error codes


|**Code** |**Service HTTP status** |**Description** |
|---|---|---|
|`InvalidParameter` |400 |A parameter value or business\-format definition is invalid. This error can also be returned when the JSON request body is malformed, a required field is missing, or the rule expression cannot be compiled. |
|`Unauthorized` |403 |The caller could not be authenticated or does not have permission to update the specified task. |
|`RecordNotFound` |400 |The specified task does not exist, has been deleted, or is not owned by the current account. |
|`InternalError` |500 |The service failed to process the request because of an internal error. |


Requests with missing required fields or malformed JSON are rejected. For gateway errors, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
