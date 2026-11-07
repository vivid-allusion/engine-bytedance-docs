---
title: "QueryRecommendation"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/QueryRecommendation"
---

***Viking AI Search*** * is an enterprise\-level AI search product based on generative AI, leveraging the multimodal semantic representation and understanding capabilities of large models, combined with years of best practices in information retrieval from ByteDance. It provides customers with an out\-of\-the\-box AI search platform service to help them easily build and integrate end\-to\-end multimodal image and text search and recommendation capabilities.* 


---



Without relying on the user input query prefix, recommend a list of query keywords based on the user's personalized interests, search keyword popularity, and other information. Mainly applicable to scenarios such as search box background keyword rotation and Recommended for you lists.

<span id="f2efd9aa"></span>
## Request description


* **Request Type:**  POST

* **Request URL**:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/search/{scene_id}/query_recommendation` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{scene_id}/query_recommendation` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/search/{scene_id}/query_recommendation` |


`{scene_id}` is the search strategy ID and `{application_id}` is the application ID.

<span id="23e89361"></span>
## Authentication method

Authentication can use API Key or Access Key. For details, refer to [API authentication mechanism description](https://www.volcengine.com/docs/85296/1544950)

<span id="3344dde6"></span>
## **Request parameters**

<span id="97558d92"></span>
### Request body


|**Parameter** |**Data Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|user |**User** |Yes |'user_xxxx' |**User information**<br><br>Used to specify which user triggered this API call. |
|page_size<br><br> |Integer<br><br> |No<br><br> |5 |**Configure the maximum result limits**<br><br>If not provided, the result limits configured in the current policy on the console will be used. Paging is not supported; results return in a single batch.<br><br>Note: result limits do not necessarily equal the `page_size` parameter. If after deduplication and filtering, the number of recommended queries is less than `page_size`, the result limits may be less than configured.<br><br>The default value is 5. |
|min_length |Integer |No |2 |**Configure the minimum value of acceptable query character length**<br><br>If not provided, the limit configured in the current policy on the console is used.<br><br>The default value is 2. |
|max_length |Integer |No |10 |**Configure the maximum value of acceptable query character length**<br><br>If not provided, the limit configured in the current policy on the console is used.<br><br>The default value is 10. |
|related_item |String<br><br> |No |'400408' |**Parent Item ID**<br><br>When you need to recommend related query keywords based on a specific Item, you must provide the unique identifier of that Item. |
|dataset_id |String |Partially |'38759234' |**Parent item dataset ID**<br><br>When the parent item ID is passed in, you must also pass in the dataset ID where the parent item is located; otherwise, it is not possible to recommend related query keywords based on the parent item |


&nbsp;

<span id="9111ffac"></span>
## **Response parameters**


|**Parameter** |**Data type** |**Example** |**Description** |
|---|---|---|---|
|request_id |String |`"25ee998a-5462-9385-9f18-035f1da7a6e5"` |**Request ID**<br><br>Unique identifier for a request, supports quick location of a request |
|recommendation_queries |Array<String\> |&nbsp;<br><br>```Plain Text```<br>```{```<br>```"recommendation_queries":[```<br>```    {"query":"adizero shoes"},```<br>```    {"query":"shorts"},```<br>```    {"query":"fitted shirts"}```<br>```    ]```<br>```}```<br><br><br> |**List of recommended queries** |


&nbsp;


---



<span id="8464e176"></span>
## Example 

<span id="4e8d5d3e"></span>
### Search Query Recommendation Request

```Plain Text
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/search/${scene_id}/query_recommendation' \
  -H 'Content-Type: application/json' \
  -H 'X-Account-Id: account_id' \   //input your account_id
  -H 'Authorization: Bearer <API Key>' \
  -d '{
  "user": { 
        "_user_id": ""
     }, 
  "page_size":
  "min_length": ""
  "max_length": ""
  "related_item": ""
  "dataset_id": ""
}'
```


&nbsp;

<span id="2afa019d"></span>
### Recommend Related Search Query Based on Items

```Plain Text
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/search/${scene_id}/query_recommendation' \
  -H 'Content-Type: application/json' \
  -H 'X-Account-Id: account_id' \  //input your account_id
  -H 'Authorization: Bearer <API Key>' \
  -d '{
  "user": { 
        "_user_id": ""
     }, 
  "page_size": 
  "min_length": "" 
  "max_length": ""
  "related_item": ""
  "dataset_id": "" 
}'
```
