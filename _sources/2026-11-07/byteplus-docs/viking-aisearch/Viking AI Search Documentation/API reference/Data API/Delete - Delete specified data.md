---
title: "Delete - Delete specified data"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Delete_-_Delete_specified_data"
---

***Viking AI Search*** * is an enterprise\-level AI search product powered by generative AI. Based on the multimodal semantic representation and understanding of large models and ByteDance's best practices in information retrieval, it provides an out\-of\-the\-box platform for customers to easily build and integrate end\-to\-end multimodal search and recommendation capabilities for images and text.* 

*To explore more Viking AI Search capabilities, visit: * [Viking AI Search Engine, an integrated intelligent engine for enterprise search, recommendation, and question-answering](https://www.volcengine.com/product/AI-Search-Rec)


---



This API deletes existing data from a specified item dataset. The delete request only requires the unique identifiers of the data.

<span id="b6acb193"></span>
## Notes


* **Limitations:** 

   * A single request can include up to 10,000 unique identifiers for items to be deleted.


<span id="ef11ea08"></span>
## Request Details


* Request Method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/delete` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/delete` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/dataset/{dataset_id}/d`elete |


 *{dataset_id}*  *: The unique ID for a dataset. The system assigns this ID after you create a dataset in the console. You can view this ID in the console.* 

<span id="231557aa"></span>
## Request Parameters

<span id="bf05d86a"></span>
### Request Body


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|_ids |Array of Object<br><br>The object is of the String or Int type. |Yes |["WSHOE001", "WSHOE002", "WSHOE003"] |A list of primary keys for the data to be deleted. The values in this list must directly correspond to the values of the field used as the **unique identifier** in your data. |


<span id="413d1114"></span>
## Response Parameters

<span id="ee4f7ee2"></span>
### Request and Response


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|request_id |String |25ee998a\-5462\-9385\-9f18\-035f1da7a6e5 |Uniquely identifies a request. You can use the request_id to quickly locate its execution. |


&nbsp;

<span id="52fd0e30"></span>
## Request Example

```Plain Text
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/delete'
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <Header set for Signature/Auth>' \
  -d '{
    "_ids": [
        "WSHOE001",
        "WSHOE002",
        "WSHOE003"
    ]
}'
```


&nbsp;

<span id="4af02739"></span>
## Response Example

```Plain Text
{
    "request_id": "25ee998a-5462-9385-9f18-035f1da7a6e5"
}
```


&nbsp;

<span id="fbaf314a"></span>
## Error Handling

<span id="5f87a1e2"></span>
### Error Codes

See the [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)documentation</a\> for this API's error codes.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more of Viking AI's search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, the all\-in\-one intelligent engine for enterprise search, recommendations, and Q&A</a></div>
