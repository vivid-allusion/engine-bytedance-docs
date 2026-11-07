---
title: "Create Monitoring Task"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/CreateMonitorTask"
---

Creates a monitoring task that initially filters content by keyword and source and can optionally evaluate the relevance of matched content.

A successful request returns the task ID and its initial status. After creating the task, call the content retrieval API to retrieve posts associated with it.

<span id="y5PZz4Ld"></span>
## Request information


|**Item** |**Description** |
|---|---|
|Environment |BytePlus production |
|HTTP method |POST |
|Request body format |application/json |
|API method |CreateMonitorTask |
|TOP Action |CreateMonitorTask |
|Version |2026\-03\-24 |
|Service (signature) |mkt_insight |
|Region (signature) |ap\-southeast\-1 |
|Request domain |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Complete request URL |[https://mkt-insight.byteplusapi.com/?Action=CreateMonitorTask&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=CreateMonitorTask&Version=2026-03-24) |
|Authentication |Use a BytePlus production AK/SK pair to generate the `Authorization` header according to the standard signature protocol. Include` Action `and Version in the query string and business parameters in the JSON request body. |


<span id="53yTwUmn"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Config` |MonitorTaskConfig |Yes |Complete task configuration. |
|`ClientToken` |String |Yes |Deduplication token for the create request. The value must be 1–128 UTF\-8 bytes and cannot contain only whitespace. |


<span id="1dlidfLk"></span>
### MonitorTaskConfig


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskName` |String |Yes |Task name. After leading and trailing whitespace is removed, the value must be non\-empty and shorter than 255 bytes in UTF\-8. |
|`RuleExpression` |String |Yes |Keyword expression. Supports up to two AND groups and up to 1,000 keywords across all groups. |
|`DomainSelector` |DomainSelector |No |Sources to monitor. Omit this field or pass {} to use all currently enabled sites. |
|`RelatedRequirement` |String |No |Natural\-language relevance evaluation requirements. Omit this field or pass "" to perform initial filtering only. A value containing only whitespace is invalid. Do not pass a complete model prompt or output template. |
|`Description` |String |No |Task description. Omit this field or pass "" for no description. |


<span id="5UqGlKTF"></span>
### DomainSelector


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`DomainTypeList` |Array<String\> |No |List of site types, such as `social_media`, `wforum`, `portal_website`, and `news_website`. |
|`DomainList` |Array<String\> |No |List of specific site domains, such as [twitter.com](http://twitter.com/) and[reddit.com](http://reddit.com/). Pass domains, not display names. |


If both lists are provided, their union is used. Each type expands to the sites of that type that are currently enabled. An explicitly selected value that is unknown, disabled, or blank causes an error. If both lists are empty, the behavior is equivalent to passing an empty object. The available scope is determined by the service's current enabled\-source configuration.

```JSON
{
  "DomainSelector": {
    "DomainTypeList": ["wforum"],
    "DomainList": ["twitter.com"]
  }
}
```


&nbsp;

<span id="BgNqPV5N"></span>
### `RuleExpression` keyword expression

`/` means OR within a group, and `+` means AND between groups. For example, `(apple/iphone)+(battery/charging)` matches posts that contain apple or iphone and also contain battery or charging. Each group can use one level of parentheses. Nested parentheses, empty keywords, and more than two AND groups are not supported. Leading and trailing whitespace is removed from each keyword, and duplicate keywords still count toward the 1,000\-keyword limit.

<span id="ejlvtjNZ"></span>
## Usage notes

After a task is created successfully, `Status=1` indicates that the task is enabled. It does not indicate that post results are already available. Use the content retrieval API to pull posts.

Deduplication applies to the same account, create endpoint, and `ClientToken`. A deduplication record is created only after parameter validation and rule compilation succeed, and remains valid for 10 minutes from creation.

If parameter validation or rule compilation fails, no deduplication record is created. You can correct the parameters and retry with the same `ClientToken`. After a deduplication record is created, it remains until it expires, regardless of whether task creation subsequently succeeds or fails. If another request with the same `ClientToken` passes validation and compilation during the validity period, the API returns OperationDenied rather than the result of the first request.

`ClientToken` is not a permanent idempotency key. If a request times out or the creation result is unknown, do not immediately switch to a different ClientToken and create the task again.

<span id="ah1VonEy"></span>
## Response parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Result.TaskID` |Int64 |Yes |ID of the new task. |
|`Result.Status` |Int32 |Yes |Task status. A newly created task has status 1. Status values: 1 for enabled, 0 for paused, and \-1 for deleted. |


<span id="Qqpm8OlD"></span>
## Request example

```JSON
{
  "Config": {
    "TaskName": "Mobile phone battery monitoring",
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
  "ClientToken": "monitor-create-example-001"
}
```


<span id="uwX5EK2c"></span>
## Response example

```JSON
{
  "Result": {
    "TaskID": 123456,
    "Status": 1
  },
  "ResponseMetadata": {
    "RequestId": "example-request-id"
  }
}
```


<span id="t80ab19M"></span>
## Error codes


|**Code** |**Service HTTP status** |**Description** |
|---|---|---|
|`InvalidParameter` |400 |A parameter value or business\-format definition is invalid. This error can also be returned when the JSON request body is malformed or a required field is missing. |
|`Unauthorized` |403 |The caller could not be authenticated or does not have permission to perform the operation. |
|`OperationDenied` |403 |A duplicate create request was submitted using the same `ClientToken` during the 10\-minute deduplication period, or the business operation was otherwise denied. |
|`QuotaExceeded` |429 |The account does not have sufficient monitoring\-task quota to create another task. |
|`InternalError` |500 |The service failed to process the request because of an internal error. |


Requests with missing required fields or malformed JSON are rejected. For signature, authentication, authorization, throttling, and other gateway errors, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
