---
title: "QuestionSuggestions"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/QuestionSuggestions"
---

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Due to HTTP body size limits, the package size for a single request must not exceed 10MB</div>


<span id="2aeab828"></span>
# Prerequisite

Ensure that this application has enabled  **"Starter questions"** . For more details, see [Configure Conversation Opening](https://docs.byteplus.com/docs/viking-aisearch/Configure_Conversation_Opening).

<span id="44a4e292"></span>
# Description

<span id="d3b02c65"></span>
## API overview

This interface independently returns questions users can directly ask. It does not generate greetings or create/read conversational search sessions.


|**Parameters** |**Description** |
|---|---|
|Request method |POST |
|Request path |`{REGION_URL}/api/v1/application/{APPLICATION_ID}/question_suggestions` |
|Content\-Type |`application/json` |
|Authentication |`Authorization: Bearer <API_KEY>` |
|Response format |Standard JSON response |


<span id="2763c771"></span>
## **Region URL**


|**Service** |**Region** |**Region URL** |
|---|---|---|
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com` |
|Volcano Engine |Southeast Asia (Johor) |`https://aisearch.ap-southeast-1.volces.com` |
|BytePlus |Southeast Asia (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com` |


<span id="6d7b07fe"></span>
## Path parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`APPLICATION_ID` |String |Yes |Application unique identifier. |


<span id="e1ec0745"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`user` |Object |No |User information used to generate personalized referral questions. |
|`user._user_id` |String |No |Unique identifier for the user. It will be used as the basis for personalized Recommendation after being passed in. |
|`user.nickname` |String |No |User nickname. |


<span id="b7e439bd"></span>
## Sample Request

```Bash
curl--request POST 'https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/<application_id>/question_suggestions' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'Content-Type: application/json' \
  --data '{
    "user": {
      "_user_id": "user_123"
    }
  }'
```


&nbsp;

**If personalization is not required:**  Pass an empty object in the request body.

```Bash
curl --request POST 'https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/<application_id>/question_suggestions' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'Content-Type: application/json' \
  --data '{}'
```


<span id="43822ca3"></span>
## Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`request_id` |String |Request unique identifier . |
|`result` |Object |Successful response result. |
|`result.suggestions` |Array<String\> |Recommendation question list. <br><br>Returns an empty array when no recommendations are available or Starter Question configuration is disabled. |


<span id="68a63c4d"></span>
## Sample Response

```JSON
{
  "request_id": "68631400-6f90-4ab2-9881-b87bfc4b8f12",
  "result": {
    "suggestions": [
      "What are some popular items today?",
      "Recommend me some dramas that I can watch during my commute.",
      "What are the latest news in tech?"
    ]
  }
}
```


&nbsp;

**If Starter Questions is disabled in this application,**  this API will return an empty list.

```JSON
{
  "request_id": "68631400-6f90-4ab2-9881-b87bfc4b8f12",
  "result": {
    "suggestions": []
  }
}
```
