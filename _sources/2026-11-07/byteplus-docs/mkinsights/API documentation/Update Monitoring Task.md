---
title: "Update Monitoring Task"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/UpdateMonitorTask"
---

Replace the entire configuration of a monitoring task under the current account. Use the same MonitorTaskConfig structure as the create API, without changing the task ID or its enabled/paused status.

<span id="KsRTeV69"></span>
## Request information


|**Item** |**Description** |
|---|---|
|Environment |BytePlus production |
|HTTP method |POST |
|Request body format |application/json |
|API method |UpdateMonitorTask |
|TOP Action |UpdateMonitorTask |
|Version |2026\-03\-24 |
|Service (signature) |mkt_insight |
|Region (signature) |ap\-southeast\-1 |
|Request domain |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Complete request URL |[https://mkt-insight.byteplusapi.com/?Action=UpdateMonitorTask&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=UpdateMonitorTask&Version=2026-03-24) |
|Authentication |Use a BytePlus production AK/SK pair to generate the Authorization header according to the standard signature protocol. Include Action and Version in the query string and business parameters in the JSON request body. |


<span id="n3dDP0ra"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskID` |Int64 |Yes |ID of an existing, non\-deleted monitoring task owned by the current account. The value must be greater than 0. |
|`Config` |MonitorTaskConfig |Yes |Complete replacement configuration of the task. This API does not support partial field updates. |


<span id="7FNjUJlb"></span>
### MonitorTaskConfig


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskName` |String |Yes |Task name. After leading and trailing whitespace is removed, the value must be non\-empty and shorter than 255 bytes in UTF\-8. |
|`RuleExpression` |String |Yes |Keyword expression. Supports up to two AND groups and up to 1,000 keywords across all groups. |
|`DomainSelector` |DomainSelector |No |Sources to monitor. Omit this field or pass `{}` to use all currently enabled sites. |
|`RelatedRequirement` |String |No |Natural\-language relevance evaluation requirements. Omit this field or pass `""` to perform initial filtering only. A value containing only whitespace is invalid. Do not pass a complete model prompt or output template. |
|`Description` |String |No |Task description. Omit this field or pass `""` for no description. |


<span id="dOTyzZUP"></span>
### DomainSelector


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`DomainTypeList` |Array<String\> |No |List of site types, such as `social_media`, `wforum`, `portal_website`, and `news_website`. |
|`DomainList` |Array<String\> |No |List of specific site domains, such as `twitter.com` and `reddit.com`. Pass domains, not display names. |


The following rules apply to DomainSelector:


* If both DomainTypeList and DomainList are provided, the union of the selected sites is used.

* Each value in DomainTypeList expands to all currently enabled sites belonging to that type.

* If the same site is selected through both lists, it is included only once.

* An explicitly selected type or domain that is unknown, disabled, or blank causes the request to fail.

* If both lists are omitted or empty, the behavior is equivalent to passing an empty DomainSelector object.

* Omitting DomainSelector or passing an empty object resets the task to all sites enabled at the time of the update.

* The actual source scope is determined by the service’s current enabled\-source configuration.


For the complete list of supported site types and domains, see the CreateMonitorTask API documentation.

> Because the set of enabled sources can change, omitting DomainSelector during an update may result in a source scope different from the task’s previous scope. To preserve the current source selection, retrieve the task configuration first and submit its existing DomainSelector in the update request.


<span id="LWPIOd0F"></span>
### Keyword expression

Use `/` as the OR operator within a keyword group and `+` as the AND operator between groups. 

For example, `(apple/iphone)+(battery/charging)` matches posts that contain apple or iphone and also contain battery or charging. 

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


> If `/`, `+`, `(`, or `)` can appear as literal characters in a keyword, the documentation should specify the corresponding escaping rules.


<span id="oP0B1pxR"></span>
## Update rules

Submit the complete configuration with every request. Both `TaskName` and `RuleExpression` are required. 

Updating a task:


* Does not change the task ID.

* Does not change the task’s enabled or paused status.

* Does not automatically clear posts previously retrieved for the task.

* Does not guarantee that existing posts will be reevaluated against the updated configuration.

* Does not guarantee that every in\-progress post will use the new configuration.


Posts that entered the processing pipeline before the update may finish processing using the configuration that was active when they were retrieved. Newly retrieved posts use the updated configuration after the update takes effect.

> If the service provides a defined configuration\-effective time or stronger consistency guarantee, document it here. Otherwise, avoid implying that the new configuration takes effect instantaneously for all in\-flight content.


<span id="LzyVoBX8"></span>
## Response parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Result.TaskID` |Int64 |Yes |ID of the monitoring task that was updated successfully. |


<span id="kzWhZWwc"></span>
## Request example

```JSON
{
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
  }
}
```


<span id="KaQPKRwL"></span>
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


<span id="2z7cEPTb"></span>
### Switch to initial filtering only

You must still submit the complete configuration. The following example also clears the description:

```JSON
{
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
    "RelatedRequirement": "",
    "Description": ""
  }
}
```


<span id="9GnI3rhF"></span>
## Error codes


|**Code** |**Service HTTP status** |**Description** |
|---|---|---|
|`InvalidParameter` |400 |A parameter value or business\-format definition is invalid. This error can also be returned when the JSON request body is malformed, a required field is missing, or the rule expression cannot be compiled. |
|`Unauthorized` |403 |The caller could not be authenticated or does not have permission to update the specified task. |
|`RecordNotFound` |400 |The specified task does not exist, has been deleted, or is not owned by the current account. |
|`InternalError` |500 |The service failed to process the request because of an internal error. |


Requests with missing required fields or malformed JSON are rejected. For gateway errors, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
