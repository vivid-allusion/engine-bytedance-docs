---
title: "Overview - Search Summary"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Overview-Search-Summary"
---

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">Due to HTTP body size limits, a single request body cannot exceed 10 MB.</div>


* <div data-tips="true" data-tips-type="warning">Only the first 20 entries in <code>items</code> are processed. If you pass more, sort them by relevance or business priority first.</div>




---



<span id="83a1c377"></span>
## Prerequisites

Make sure the **Search Summary** configuration is complete and active for your application, the datasets used in the request are linked to the application, and the item data has finished processing.

<span id="f2651d75"></span>
## Request

<span id="e30b32be"></span>
### Overview

This API generates a summary, comparison, or buying advice based on the user's question and the items you specify. You decide which items go into the summary, and the API streams the result back over SSE.


|**Parameter** |**Description** |
|---|---|
|Method |`POST` |
|Path |`{REGION_URL}/api/v1/application/{APPLICATION_ID}/overview/{SCENE_ID}` |
|Content\-Type |`application/json` |
|Authentication |`Authorization: Bearer <API_KEY>` |
|Response format |SSE stream |


<span id="e49dbb86"></span>
### Endpoints


|**Service** |**Region** |**URL** |
|---|---|---|
|Volcano Engine |China North (Beijing) |`https://aisearch.cn-beijing.volces.com` |
|Volcano Engine |Southeast Asia (Johor) |`https://aisearch.ap-southeast-1.volces.com` |
|BytePlus |Southeast Asia (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com` |


<span id="56dfdf4a"></span>
### Path parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`APPLICATION_ID` |String |Yes |Unique application ID. |
|`SCENE_ID` |String |Yes |Unique search scenario ID. |


<span id="d1703bbc"></span>
### Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`session_id` |String |Yes |Unique ID for this summary session. We recommend generating a new ID for each new session. |
|`query` |String |Yes |The question the user wants the summary to answer. |
|`user` |Object |No |User information, used to provide personalized context. |
|`user._user_id` |String |No |Unique user ID. |
|`user.nickname` |String |No |User nickname. |
|`user.user_profile` |String |No |Description of the user's preferences relevant to the current question. |
|`items` |Array<Object\> |Yes |Items to include in the summary. Pass at least 1; only the first 20 are processed. |
|`items[].dataset_id` |String |Yes |ID of the dataset the item belongs to. The dataset must be linked to the current application. |
|`items[]._id` |String |Yes |The item's primary key value in the dataset. |


<span id="a196ec59"></span>
### Request example

```Bash
curl --request POST 'https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/<application_id>/overview/<scene_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'Content-Type: application/json' \
  --data '{
    "session_id": "overview_session_001",
    "query": "Compare these two sports earbuds on noise cancellation, battery life, and comfort",
    "user": {
      "_user_id": "user_123",
      "nickname": "Alex",
      "user_profile": "Travels long distances often; cares most about battery life and comfort"
    },
    "items": [
      {
        "dataset_id": "<dataset_id>",
        "_id": "item_001"
      },
      {
        "dataset_id": "<dataset_id>",
        "_id": "item_002"
      }
    ]
  }'
```


&nbsp;

<span id="0037fbc5"></span>
## Response

The API returns `application/event-stream`. Parse events in the order they arrive and append `result.content` incrementally.

<span id="e3c6fe8e"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`request_id` |String |Unique request ID, used for troubleshooting. |
|`result` |Object |Response result for the current stream chunk. |
|`result.content` |String |The current chunk of summary text. Append chunks in order. |
|`result.payload` |Object |Extended information such as summary status, related items, and suggested follow\-up questions. |
|`result.payload.overview` |Object |Status of this search summary. |
|`result.payload.overview.enabled` |Boolean |Whether a search summary was generated. |
|`result.payload.overview.session_id` |String |ID of this summary session. |
|`result.payload.related_items` |Array<Object\> |Information about the items referenced in the summary. |
|`result.payload.suggestions` |Array<String\> |Suggested follow\-up questions based on the current summary. |
|`result.stop_reason` |String |Why the stream ended. `stop` means it finished normally. |


<span id="07b218e4"></span>
### Response example

```JSON
{"request_id":"68631400-6f90-4ab2-9881-b87bfc4b8f12","result":{"payload":{"overview":{"enabled":true,"session_id":"overview_session_001"}}}}
{"request_id":"68631400-6f90-4ab2-9881-b87bfc4b8f12","result":{"content":"Both earbuds support active noise cancellation, "}}
{"request_id":"68631400-6f90-4ab2-9881-b87bfc4b8f12","result":{"content":"and item_001 has longer battery life."}}
{"request_id":"68631400-6f90-4ab2-9881-b87bfc4b8f12","result":{"payload":{"suggestions":["What's the price difference between them?","Which one is better for commuting?"]}}}
{"request_id":"68631400-6f90-4ab2-9881-b87bfc4b8f12","result":{"stop_reason":"stop"}}
```


&nbsp;

Different fields may arrive in different events. Display text incrementally as `content` arrives, and stop reading once you receive `stop_reason=stop`.

<span id="9a9bfe55"></span>
### When no summary is generated

If the request doesn't trigger a search summary, `result.payload.overview.enabled` is `false` and no summary text is returned.

```JSON
{"request_id":"68631400-6f90-4ab2-9881-b87bfc4b8f12","result":{"payload":{"overview":{"enabled":false,"session_id":"overview_session_001"}},"stop_reason":"stop"}}
```


&nbsp;

<span id="dbed3e47"></span>
## FAQ

**Why are some items missing from the summary?** 

Check whether you passed more than 20 items, whether the dataset is linked to the current application, whether the item's primary key exists, and whether the data has finished processing. Only the first 20 entries in `items` are processed.

**Why is the response incomplete?** 

Search summaries are streamed over SSE. The client must keep reading until it receives `stop_reason=stop`. If the connection is closed early, you only get part of the text.

**How do I adjust the summary content and response style?** 

Adjust the output language, focus dimensions, and generation prompt in the **Search Summary** configuration in the console. For production, we recommend managing configuration centrally in the console.
