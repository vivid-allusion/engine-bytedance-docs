---
title: "RecReason - Recommendation Assistant"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/RecReason-Recommendation-Assistant"
---

<span id="970d22a8"></span>
# Overview

The Recommendation Assistant API takes the items already returned by the [Recommend](https://docs.byteplus.com/docs/viking-aisearch/Recommendation) API, along with their recall information, and combines them with the user profile and the assistant persona prompt configured in the console (assistant identity, response style, and follow\-up tendency). A large language model then streams back an analysis explaining why this batch of items was recommended, followed by 3 progressive follow\-up questions.

This is an SSE (Server\-Sent Events) streaming API. The response body is pushed in chunks, so clients can render the text token by token.

The Recommendation Assistant does not add items or re\-rank them. It only explains the items passed in the request. Item sources and ordering are always those returned by the Recommend API.

<span id="1a14224e"></span>
## Typical call sequence


1. Call the Recommend API to get recommended items and render the item cards (milliseconds).

2. Call this API asynchronously to stream the analysis and follow\-up questions (seconds).

3. When the user taps a follow\-up question, call the ChatSearch API.


<span id="57e45954"></span>
## Notes

**Limits**


* Due to HTTP body size limits, a single request body cannot exceed 10 MB.

* We recommend passing the items returned by the current Recommend call straight through to `context.items`. Up to 400 items are processed per request; any items beyond that are ignored.

* This API only explains the items passed in. It does not recall new items or change their order.


**Prerequisites**


* Before calling this API, create a recommendation scenario in the console and turn on **Trigger Recommendation Assistant**.

* `context.items._id` must be an item ID that exists in the item dataset and matches the ID returned by the Recommend API.

* The `rec_info` of each item can be passed through directly from the `rec_info` returned by the Recommend API (recall channel + recommendation reason).


&nbsp;

<span id="3d3d9fb8"></span>
## **Billing**

Billed per conversation. One conversation is counted as soon as the model starts streaming output. Requests that produce no content because of rate limiting or timeouts are not charged. See [Viking AI Search Billing and Pricing](https://docs.byteplus.com/docs/viking-aisearch/Billing_and_Pricing) for details.


---



<span id="ebe27535"></span>
# Request

**Method:**  `POST`

<span id="94a5a4ca"></span>
## Endpoints


|**Service** |**Region** |**URL** |
|---|---|---|
|Volcano Engine |China North (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/rec_reason/{scene_id}` |
|Volcano Engine |Southeast Asia (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/rec_reason/{scene_id}` |
|BytePlus |Southeast Asia (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/rec_reason/{scene_id}` |


<span id="095eafc4"></span>
## Headers


|**Header** |**Value** |**Description** |
|---|---|---|
|`Content-Type` |`application/json` |The request body is JSON. |
|`Authorization` |`Bearer {API Key}` |Authentication credentials. |


<span id="ac51bed3"></span>
## Authentication

You can authenticate with either an API Key or an Access Key. For details, see [API Authentication](https://docs.byteplus.com/docs/viking-aisearch/API_Authentication).

<span id="9f26e878"></span>
## Path parameters


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`application_id` |String |Yes |`76414365027` |Unique application ID assigned by the system when you create an application. You can find it in the console. |
|`scene_id` |String |Yes |`scene-R01asDfs` |Unique ID of the recommendation scenario, prefixed with `scene-`. You can find it on the Recommendation Strategy page in the console. The persona configuration (assistant identity, response style, follow\-up tendency) and the feature toggle are both read from this scenario. |


<span id="643e8c79"></span>
## Request body


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`user` |Object<User\> |Yes |User information. Used to fetch the user profile and to identify who the call belongs to. |
|`context` |Object<RecReasonContext\> |Yes |Per\-request context containing the recommended items and their recall information. It is merged with the assistant persona configured in the console. |


<span id="17134fe0"></span>
## Data structures

<span id="5eef7fef"></span>
### User


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`_user_id` |String |Yes |`"user_199432"` |Unique user ID. The user profile (interest tags and a summary of past behavior) is retrieved by this ID. For users who are not logged in, you can use a virtual user ID as long as it is globally unique. |


<span id="1147a3ef"></span>
### RecReasonContext


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`items` |Array<RecReasonItem\> |Yes |Items recommended in this round. <br><br>We recommend passing through the `rec_results` returned by the Recommend API (including each item's `rec_info`). <br><br>Up to 400 items per request. |
|`additional_context` |String |No |Extra per\-request context for the assistant, such as the current channel, campaign theme, or marketing messaging. Applies to this request only. <br><br>The content must meet your compliance requirements. The assistant will not use it to introduce facts beyond the items themselves. |


<span id="e72f9550"></span>
### RecReasonItem


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`_id` |String |Yes |`"688930"` |Unique item ID. Must match the `_id` returned by the Recommend API and exist in the item dataset. |
|`rec_info` |Array<RecallReason\> |Yes |See below |Recommendation info for the item: the recall channels it matched and the corresponding reasons. <br><br>Can be passed through directly from the Recommend API response. |


<span id="c5a72b9f"></span>
### RecallReason


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|`recall_channel` |String |Yes |`"hot_item"` |Recall channel ID, using the same values as the Recommend API. <br><br>e.g. `hot_item` (trending), `user_profile` (user profile), `multimodal` (multimodal), `item_cf` (similar users), `item_similarity` (parent item / item similarity), `cold_start` (item cold start). |
|`reason` |String |Yes |`"Top 3 trending recently"` |Per\-item recommendation reason for this recall channel (generated in template mode). <br><br>Used as factual input for the model's analysis. |


<span id="05d5d168"></span>
# Response

The response is an SSE event stream. Each event is a single line in the form `data: {JSON payload}` (the `data:` prefix is omitted in the examples below). Every payload carries a `request_id`. Events are pushed in the following order:


|**Order** |**Event** |**Payload signature** |**Description** |
|---|---|---|---|
|1 |Session init |`result.payload.rec_reason.session_id` |Returns the session ID, used for troubleshooting and follow\-up questions. |
|2 |Reply start |`result.step_info.step = "reply"` |Marks the start of the response body. |
|3 |Content chunks |`result.content` is non\-empty |The model's recommendation analysis, pushed token by token. Concatenate chunks in arrival order. |
|4 |Follow\-up suggestions |`result.payload.suggestions` |Array of suggested follow\-up questions. <br><br>Normally 3, progressing from category/scenario → specific attributes → comparison/decision. <br><br>In fallback cases, only 1 generic follow\-up is returned. |
|5 |End marker |`result.stop_reason = "stop"` |Marks the end of the response. The server then closes the stream. |


<span id="c8485869"></span>
## Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`request_id` |String |Request ID, unique across the full call chain. Used for troubleshooting. |
|`result` |Object |Response container. Different events carry different fields. |
|`result.step_info` |Object |Response step information. |
|`result.step_info.step` |String |Response step: `reply` (starting / generating the body) or `stop` (response complete). |
|`result.content` |String |Streaming chunk of the response body. Concatenate in arrival order to get the full analysis. May contain inline item references in the form `<ref>_id</ref>`. In fallback or content\-moderation cases, this contains the corresponding fallback text. |
|`result.payload` |Object |Extended payload. |
|`result.payload.rec_reason` |Object |Recommendation Assistant session info (returned in the session init event). |
|`result.payload.rec_reason.session_id` |String |Session ID. Pass it to the ChatSearch API to continue the conversation with this recommendation context. |
|`result.payload.suggestions` |Array<String\> |Suggested follow\-up questions. 3 normally, 1 in fallback cases. The question text never contains reference tags. |
|`result.stop_reason` |String |End marker. Set to `"stop"` when the response is complete. |


<span id="b0e4c103"></span>
# Examples

<span id="92dec628"></span>
## Request example

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/rec_reason/${scene_id}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: text/event-stream' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "user": {
      "_user_id": "user_199432"
    },
    "context": {
      "items": [
        {
          "_id": "688932914577129760",
          "rec_info": [
            { "recall_channel": "user_profile", "reason": "Matches your interest in \"work tote bags\"" },
            { "recall_channel": "item_similarity", "reason": "Similar to \"item_1002\"" }
          ]
        },
        {
          "_id": "528424731470549718",
          "rec_info": [
            { "recall_channel": "hot_item", "reason": "Top 3 trending recently" }
          ]
        }
      ],
      "additional_context": "This is the \"You may also like\" slot on the home page of an e-commerce app. The user recently browsed ladylike shoulder handbags."
    }
  }'
```


&nbsp;

<span id="036a53c8"></span>
## Response example

The stream below is shown in event order, split across lines for readability. In practice, each event is a single line.

```JSON
// 1. Session init
{"request_id":"b1c2d3e4-...","result":{"payload":{"rec_reason":{"session_id":"rr_20260916_0001"}}}}
// 2. Reply start
{"request_id":"b1c2d3e4-...","result":{"step_info":{"step":"reply"}}}
// 3. Content chunks (token by token, pushed multiple times, concatenate in order)
{"request_id":"b1c2d3e4-...","result":{"content":"These are all roomy, minimalist bags "}}
{"request_id":"b1c2d3e4-...","result":{"content":"made for the office commute, "}}
{"request_id":"b1c2d3e4-...","result":{"content":"in the same ladylike handbag style you've been browsing lately, mostly priced around 200 CNY.\n\n"}}
{"request_id":"b1c2d3e4-...","result":{"content":"- If you need to fit a laptop and folders, go for the large canvas or cowhide leather options;\n"}}
{"request_id":"b1c2d3e4-...","result":{"content":"- If you prefer a white ladylike bag for dates or casual outings, most styles in this batch fit.\n"}}
// 4. Follow-up suggestions
{"request_id":"b1c2d3e4-...","result":{"payload":{"suggestions":["Show more ladylike work bags","Cowhide leather work bags","Compare bags by material"]}}}
// 5. End marker
{"request_id":"b1c2d3e4-...","result":{"stop_reason":"stop"}}
```


&nbsp;

<span id="97fc7c28"></span>
## Client handling tips


* Keep a string buffer, append every `content` chunk in arrival order, then render.

* When `suggestions` arrives, render them as tappable follow\-up buttons. When `stop_reason=stop` arrives, end the loading state.


&nbsp;

<span id="37456af3"></span>
# Follow\-up questions (via the ChatSearch API)

When the user taps a follow\-up question, call the ChatSearch API to continue a multi\-turn conversation:

```Plain Text
POST /api/v1/application/{application_id}/chat_search
```


&nbsp;

Follow\-up questions extend the existing ChatSearch request body with the parameters below.

<span id="2d98dd98"></span>
## Extended request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`query` |String |Yes |Text of the follow\-up question the user tapped (same definition as in ChatSearch). |
|`is_recommend` |Boolean |No |Always pass `true` to mark this as a recommendation follow\-up: search recall is skipped and `items` is used to build context. <br><br>When `is_recommend=true`, the chat API skips search recall and uses the recommended items passed in as the reference source, so answers always stay focused on this batch of recommendations. |
|`dataset_id` |String |Yes |ID of the item dataset the recommended items belong to. Used to fetch item details. |
|`items` |Array<ChatSearchRecommendItem\> |No |Items recommended in this round (the same items passed to `rec_reason`), including the recommendation reason for each recall channel. |


<span id="1e6a0231"></span>
### ChatSearchRecommendItem


|Parameter |Type |Required |Description |
|---|---|---|---|
|`_id` |String |Yes |Item ID, e.g. `"WSHOE001"`. |
|`rec_info` |Array<RecallReason\> |Yes |Recommendation info. Same structure as **RecallReason** above (`recall_channel` + `reason`). |


<span id="11e60c39"></span>
### Request example

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/chat_search' \
  -H 'Content-Type: application/json' \
  -H 'Accept: text/event-stream' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "session_id": "rr_20260916_0001",
    "input_message": {
      "content": [
        { "type": "text", "text": "Cowhide leather work bags" }
      ]
    },
    "user": {
      "_user_id": "user_199432"
    },
    "enable_suggestions": true,
    "is_recommend": true,
    "dataset_id": "106264990",
    "items": [
      {
        "_id": "688932914577129760",
        "rec_info": [
          { "recall_channel": "user_profile", "reason": "Matches your interest in \"work tote bags\"" },
          { "recall_channel": "item_similarity", "reason": "Similar to \"item_1002\"" }
        ]
      },
      {
        "_id": "528424731470549718",
        "rec_info": [
          { "recall_channel": "hot_item", "reason": "Top 3 trending recently" }
        ]
      }
    ]
  }'
```


&nbsp;

> **Note:**  For the full list of fields and the streaming response format of the chat API, see [ChatSearch](https://docs.byteplus.com/docs/viking-aisearch/ChatSearch). They are not repeated here.


<span id="7a0f17bf"></span>
## Billing


* **Billing model:**  Billed per conversation, not per token.

* **When a charge applies:**  One conversation is counted as soon as the model starts streaming output (the first content chunk is returned). Usage is reported when the request ends.

* **Not charged:**  Requests where the model produces no content, for example because the feature toggle is off, quota pre\-check fails, the model is rate\-limited, or the request times out.


<span id="a1ed6736"></span>
## Error codes

For common error codes, see [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)
