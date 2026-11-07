---
title: "Pull posts"
product: "Market Insights"
product_code: "mkinsights"
source: "https://docs.byteplus.com/en/docs/mkinsights/PullPosts"
---

Retrieves, by page, posts associated with the monitoring task specified by `TaskID`.

By default, the API returns all posts associated with the task through initial filtering. You can use `IsSelect=true` to return only posts explicitly identified as relevant. Results can be filtered either by post publish time or by the time when each post was first associated with the specified task through initial filtering.

The API uses cursor\-based pagination and does not return a total item count.Request information


|**Item** |**Description** |
|---|---|
|Environment |BytePlus production |
|HTTP method |POST |
|Request body format |application/json |
|API method |PullPosts |
|TOP Action |PullPosts |
|Version |2026\-03\-24 |
|Service (signature) |mkt_insight |
|Region (signature) |ap\-southeast\-1 |
|Request domain |[https://mkt-insight.byteplusapi.com/](https://mkt-insight.byteplusapi.com/) |
|Complete request URL |[https://mkt-insight.byteplusapi.com/?Action=PullPosts&Version=2026-03-24](https://mkt-insight.byteplusapi.com/?Action=PullPosts&Version=2026-03-24) |
|Authentication |Use a BytePlus production AK/SK pair to generate the Authorization header according to the standard signature protocol. Include Action and Version in the query string and business parameters in the JSON request body. |


The public TOP Action is `PullPosts`, including the trailing `s`, and matches the IDL method name.

<span id="LGxMZfm8"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`TaskID` |Int64 |Yes |ID of an existing, non\-deleted monitoring task owned by the current account.  |
|`StartTime` |String |No |Inclusive start of the post publish\-time range. Use UTC (UTC+0) and the format yyyy\-MM\-dd HH:mm:ss. If publish\-time filtering is used, provide both StartTime and EndTime. StartTime cannot be earlier than 90 days before the time of the request. This field is ignored when ingestion\-time filtering is used. |
|`EndTime` |String |No |Inclusive end of the post publish\-time range. Use UTC (UTC+0) and the format yyyy\-MM\-dd HH:mm:ss. If publish\-time filtering is used, provide both StartTime and EndTime, and make sure EndTime is not earlier than StartTime. This field is ignored when ingestion\-time filtering is used. |
|`PageToken` |String |No |Opaque pagination cursor. Omit this field in the first request. To retrieve the next page, pass the NextPageToken returned by the preceding response unchanged. |
|`Size` |Int64 |No |Number of posts requested per page. If omitted or less than or equal to 0, the default value is 20. Values greater than 100 are treated as 100. |
|`CreateStartTime` |Int64 |No |Inclusive lower bound of the time when a post was first associated with the specified task through initial filtering, expressed as a Unix timestamp in UTC milliseconds. The value must be non\-negative. If ingestion\-time filtering is used, provide both CreateStartTime and CreateEndTime. |
|`CreateEndTime` |Int64 |No |Exclusive upper bound of the ingestion\-time range, expressed as a Unix timestamp in UTC milliseconds. It must be provided with CreateStartTime and must be greater than CreateStartTime. |
|`IsSelect` |Boolean |No |If `true`, returns only posts explicitly identified as relevant for the specified task. If omitted or set to `false`, returns all posts associated with the task through initial filtering. false does not mean that only irrelevant posts are returned. |


<span id="Ha80clUh"></span>
## Filtering and pagination

The ingestion\-time interval is [CreateStartTime, CreateEndTime). When these parameters are provided, StartTime and EndTime are ignored completely; publish\-time restrictions are not combined with the ingestion\-time filter. Ingestion time belongs to the association between the current task subscription and a post. The same post can have different ingestion times under different subscriptions. Subsequent relevance evaluation updates do not refresh this time.

For ingestion\-time queries, posts are sorted first by ingestion time for the current subscription in descending order, then by post ID in ascending order when ingestion times are equal. Without ingestion\-time parameters, posts remain sorted by publish time in descending order. Pagination does not provide a fixed data snapshot. Concurrent additions or updates can affect subsequent pages; deterministic ordering does not mean that the data remains unchanged during traversal.

Omit PageToken on the first request. When HasMore=true, pass NextPageToken unchanged in the next request and keep the task, time, relevance, and page\-size parameters identical. Do not parse, concatenate, or construct the token. Do not use a page containing fewer than Size items as a substitute for checking HasMore. This API does not return a total item count.

If an older post lacks an ingestion time for the current subscription, the response does not fabricate CreateTime, and the post does not match an ingestion\-time interval. A task that performs only initial filtering does not generate new relevance decisions, so IsSelect=true is not guaranteed to return results. Clearing the relevance requirements does not delete historical relevant results.

For time parameters, StartTime and EndTime are UTC (UTC+0) strings, and you must provide explicit start and end values. Omitting these fields does not mean “the last 24 hours.” For example, 22:00:00–23:00:00 on September 20, 2026 in China Standard Time (UTC+8) corresponds to StartTime="2026\-09\-20 14:00:00" and EndTime="2026\-09\-20 15:00:00". CreateStartTime and CreateEndTime are Unix timestamps in milliseconds; do not add or subtract eight hours. The publish\-time interval is [StartTime, EndTime], including both endpoints. The ingestion\-time interval is [CreateStartTime, CreateEndTime), including the start and excluding the end.

<span id="Y0BrG0W0"></span>
## Response parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`Result.ItemDocs` |Array<PullPost\> |No |Posts returned on the current page. When no posts are available, this field may be returned as an empty array or omitted. Clients must support both forms. |
|`Result.HasMore` |Boolean |Yes |Indicates whether another page is available. |
|`Result.NextPageToken` |String |No |Opaque cursor for retrieving the next page. Use this value only when HasMore=true. The field may be omitted or returned as an empty string when HasMore=false. |


<span id="e1dA4A9i"></span>
### PullPost


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`PostID` |String |Yes |Unique identifier of the post in the Market Insights service. |
|`Title` |String |No |Post title. |
|`Content` |String |No |Post content. |
|`Summary` |String |No |Existing summary of the post. This field may be empty or omitted when no summary is available. |
|`Ocr` |String |No |Text extracted from images through OCR. |
|`Asr` |String |No |Text transcribed from audio or video through speech recognition. |
|`Url` |String |Yes |Link to the original post. |
|`PublishTime` |String |Yes |Post publish\-time string. |
|`MainDomain` |String |Yes |Primary domain of the post. |
|`IsFollow` |Boolean |No |Whether the post is a repost. |
|`MediaName` |String |No |Media outlet or author name. |
|`FansCount` |Int64 |No |Follower count associated with the source account. This field is not guaranteed to be returned. |
|`locations` |Array |No |Location information extracted from the post. The field name begins with a lowercase `l` and is case\-sensitive. This field is not guaranteed to be returned. |
|`RiskType` |Array |No |Existing content or risk labels for the current subscription. These labels are not guaranteed to be generated. |
|`Emotion` |String |No |Existing sentiment result for the current subscription. This result is not guaranteed to be generated. |
|`Reason` |String |No |Reason for the relevance decision under the current subscription. The field might be empty when the post has not been processed or no result is available. |
|`DedupID` |String |No |Deduplication ID; currently not guaranteed to be returned. |
|`UpdateTime` |String |No |Post update\-time string. This is not the time when the post was first ingested for the current subscription. |
|`OcrHigh` |String |No |Output from the existing OCR field. |
|`CreateTime` |Int64 |No |The time when the current subscription first passed preliminary filtering and was stored, in UTC milliseconds. This field is not returned for legacy associations where the value is unavailable. |


<span id="L09OZFcW"></span>
### MentionLocation

All fields are strings. `Name` is the location name. Optional fields are `Region`, `Province`, `City`, `District`, `Town`, `RegionCode`, `CityCode`, `DistrictCode`, `TownCode`, and `Location`. This structure preserves the existing protocol and does not add new location recognition capabilities.

<span id="IDasxORv"></span>
## Request example

```JSON
{
  "TaskID": 123456,
  "CreateStartTime": 1789776000000,
  "CreateEndTime": 1789862400000,
  "IsSelect": true,
  "Size": 20
}
```


<span id="1JYLUueN"></span>
## Response example

```JSON
{
  "Result": {
    "ItemDocs": [
      {
        "PostID": "example-post-001",
        "Title": "Mobile phone battery usage experience",
        "Content": "A user shares their battery life and charging experience.",
        "Url": "https://example.com/posts/001",
        "PublishTime": "2026-09-19 10:00:00",
        "MainDomain": "example.com",
        "Reason": "The content describes a genuine battery usage experience.",
        "CreateTime": 1789786800000
      }
    ],
    "HasMore": false,
    "NextPageToken": ""
  },
  "ResponseMetadata": {
    "RequestId": "example-request-id"
  }
}
```


<span id="6oQ1G2s6"></span>
## Error codes


|**Code** |**Service HTTP status** |**Description** |
|---|---|---|
|`InvalidParameter` |400 |A parameter value or business\-format definition is invalid. This error can also be returned when the JSON request body is malformed, a required field is missing, or the rule expression cannot be compiled. |
|`Unauthorized` |403 |The caller could not be authenticated or does not have permission to update the specified task. |
|`RecordNotFound` |400 |The specified task does not exist, has been deleted, or is not owned by the current account. |
|`InternalError` |500 |The service failed to process the request because of an internal error. |


Requests with missing required fields or malformed JSON are rejected. For gateway errors, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

&nbsp;

<span id="oDrDPgVg"></span>
## **Data availability**

Ingestion\-time filtering covers only data that has a searchable ingestion time for the current subscription. Historical associations might not have this time, so the filter is not guaranteed to cover all historical posts. Data is retrieved by polling; no webhook is sent.

&nbsp;

<span id="BEpIpi5u"></span>
## Next\-page request example

When the previous response has HasMore=true, keep all filter parameters and Size unchanged, and pass NextPageToken unchanged as PageToken:

```JSON
{
  "TaskID": 123456,
  "CreateStartTime": 1789776000000,
  "CreateEndTime": 1789862400000,
  "IsSelect": true,
  "Size": 20,
  "PageToken": "<NextPageToken returned on the previous page>"
}
```


Continue until HasMore=false. The token in the example is an explanatory placeholder and cannot be used directly as a request value.
