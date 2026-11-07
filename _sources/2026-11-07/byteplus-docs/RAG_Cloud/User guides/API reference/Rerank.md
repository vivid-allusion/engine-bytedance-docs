---
title: "Rerank"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Rerank"
---

<span id="1aa6a399"></span>
## **Overview**

`/api/knowledge/service/rerank` API endpoint helps you improve the relevance of your search results. You can submit a query and a list of retrieved documents, and it will return new relevance scores to help you reorder the retrieved results more accurately. The score is based on the probability that a text chunk can answer the query. A higher score indicates that the model considers it more likely that this text chunk can answer the query.

<span id="6b8bc056"></span>
## **Request interface**


|**URI** |/api/knowledge/service/rerank |Uniform resource identifier |
|---|---|---|
|**Method** |POST |The HTTP method for the request. |
|**Request header** |Content\-Type: application/json |The media type of the request body. |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="fc0e9bb2"></span>
## **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|datas |list[map] |Yes |\-\- |**List of data to be reordered**<br><br>Each element is a map, with an array length not exceeding 200, supporting the following parameters:<br><br><br>* query (required): Query content for sorting, string or object<br><br>   * string: Plain text query content, applicable to general rerank models<br><br>* content (optional): Text content to be sorted, string<br><br>* title (optional): Title of the document |
|rerank_model |string |No |"base\-multilingual\-rerank" |**Rerank model**<br><br>Optional models:<br><br><br>* "base\-multilingual\-rerank": Fast, supports long texts, supports more than 70 languages.<br><br>* "m3\-v2\-rerank": For regular texts, supports more than 100 languages. |


<span id="1fbd7aa4"></span>
## **Response message**


|**Field** |**Type** |**Subfield** |**Subfield type** |**Description** |
|---|---|---|---|---|
|code |integer |\-\- |\-\- |Status code |
|message |string |\-\- |\-\- |Error message |
|request_id |string |\-\- |\-\- |Unique identifier for the request |
|data |object |scores |array |float64 array, corresponds one\-to\-one with the input datas array, representing the relevance score between each document and the query |
|||token_usage |integer |Total number of tokens consumed by this rerank call |


<span id="1efbc14b"></span>
### **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |ErrUnauthorized |Authentication failed |
|1000002 |400 |ErrInvalidRequest |Invalid request parameters (triggered when query is missing or none of the documents in the datas array contain any text or media content) |
|300004 |429 |ErrQuotaLimiter |The account's rerank calls have reached the quota limit |
|1000028 |500 |ErrInternal |Internal service error, rerank model overloaded |


<span id="0f5f620a"></span>
## Complete example

<span id="9763c4a0"></span>
### Request message

```Shell
curl
--location --request POST 'http://<your-host>/api/knowledge/service/rerank' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <your-auth-token>' \
--data-raw '{
    "rerank_model": "base-multilingual-rerank",
    "datas": [
        {
            "query": "Show a system architecture diagram",
            "title": "System Architecture Design Document",
            "image": "https://<your-domain>/path/to/arch-diagram.png"
        },
        {
            "query": "Show a system architecture diagram",
            "title": "Meeting Minutes",
            "content": "Discussed the OKRs for next quarter."
        }
    ]
}'
```


<span id="77b1f0b4"></span>
### Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
{
    "message":"success",
    "code":0,
    "request_id":"02170427320284800000000000000000000ffff0a0060861f847c",
    "data":[0.17574862881497047,0.7583029228400268]
}
```


Return on failed execution:

```JSON
HTTP/1.1 403 OK
Content-Length: 43
Content-Type: application/json
 
{
    "message":"Signature verification failed. Please check your AK and SK.",
    "code":1000001,
    "request_id":"02170427372421200000000000000000000ffff0a006086784460"
}
```
