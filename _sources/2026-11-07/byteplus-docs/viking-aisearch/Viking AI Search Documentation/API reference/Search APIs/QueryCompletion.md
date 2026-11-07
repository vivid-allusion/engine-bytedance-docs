---
title: "QueryCompletion"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Query_Autocomplete"
---

***Viking AI Search*** * is an enterprise\-level AI search product powered by generative AI. It leverages the multimodal semantic representation and understanding of large models and combines it with ByteDance's years of best practices in information retrieval. Viking AI Search offers an out\-of\-the\-box platform that helps customers easily build and integrate end\-to\-end, multimodal search and recommendation capabilities for images and text.* 


---



Returns suggested query terms based on partial search input.

<span id="99ef8729"></span>
## Request description


* Request method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/search/{scene_id}/query_completion` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{scene_id}/query_completion` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/search/{scene_id}/query_completion` |


`{application_id}`: The unique identifier for an application. This ID is assigned by the system after the application is created in the console and can be viewed there.

`{scene_id}`: The ID of the search policy. The system assigns a unique ID after a new search policy is created on the experience configuration page. You can copy the policy ID in the console under "Search Experience" by hovering over the policy name.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d1ab6c06946e48d8a93f859090bbdd69) </span>

&nbsp;

&nbsp;

<span id="d7d4ee03"></span>
## Authentication method

Use an API Key or Access Key for authentication. For details, see [API Authentication](https://www.volcengine.com/docs/85296/1544950).

<span id="07253871"></span>
## Request Parameters

<span id="4b24c81b"></span>
### Request Body


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|query |String |Yes |"At the seaside" |The query term for which to generate suggestions. The length of the query term must be greater than or equal to the minimum character count for suggestions configured in the application. |


<span id="fbdcd877"></span>
## Response Parameters

<span id="a7582bad"></span>
### Request and Response


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|request_id |String |25ee998a\-5462\-9385\-9f18\-035f1da7a6e5 |A unique request identifier used to quickly locate the execution of a request. |
|result |Result |See below: Result |Search suggestion results |


<span id="ea2c7c5e"></span>
### Data Structure

<span id="13a68e68"></span>
#### Result


|**Parameter** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|suggestions |Array of[Suggestion](https://docs.byteplus.com/docs/viking-aisearch/Query_Autocomplete#b804b340) |See Suggestion below. |A list of search suggestions. 10 items are returned by default. To adjust this, modify the maximum number of recalled suggestions in the application configuration. |


<span id="b804b340"></span>
#### Suggestion


|**Parameter** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|suggestion |String |"Camping by the sea" |Single search suggestion |


<span id="87551b8a"></span>
## Request Example

```Plain Text
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/60590835675/search/g0BAC4BM/query_completion' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
  "query": "red"
}'
```


&nbsp;

<span id="0d353761"></span>
## Response Example

```Plain Text
{
  "request_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",
  "result": {
    "suggestions": [
      {
        "suggestion": "red dress"
      },
      {
        "suggestion": "red shoes"
      },
      {
        "suggestion": "red watch"
      },
      {
        "suggestion": "red skirt"
      },
      {
        "suggestion": "red socks"
      }
    ]
  }
}
```


&nbsp;

<span id="22e36686"></span>
## Error Handling

<span id="57c10b19"></span>
### Error Code

For the error codes for this API, refer to the [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)documentation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more Viking AI search capabilities, go to: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine: The All\-in\-One Intelligent Engine for Enterprise Search, Recommendations, and Q&A</a></div>
