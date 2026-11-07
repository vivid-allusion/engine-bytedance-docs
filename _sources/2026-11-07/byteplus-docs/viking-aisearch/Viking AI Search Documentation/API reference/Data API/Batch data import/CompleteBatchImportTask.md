---
title: "CompleteBatchImportTask"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/CompleteBatchImportTask_-_Complete_Batch_Import"
---

***Viking AI Search*** * is an enterprise\-grade AI search product powered by generative AI. It leverages the multimodal semantic representation and understanding of large models, combined with Bytedance's years of best practices in information retrieval. Viking AI Search provides an out\-of\-the\-box platform that allows customers to easily build and integrate end\-to\-end multimodal search and recommendation capabilities for text and images.* 


---



Call this API to complete a batch item data upload. Pass in the `batch_id` for the completed upload to start writing the data to the database and processing it.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">You must call this API to mark the batch upload task as complete. Otherwise, the upload task will remain in the "processing" state and will not be written to the database or undergo subsequent processing.</div>


<span id="6e69a36e"></span>
## Note


1. **Task Validity Period**: Each batch import task is valid for 24 hours. You must complete the data import and call the complete import task API to submit the data within 24 hours of creating the task. The task will automatically become invalid upon expiration.


<span id="fd18d367"></span>
## Request Details


* **Request Method**: `POST`

* **Request URL**:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/complete_batch_import_task` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/complete_batch_import_task` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/dataset/{dataset_id}/complete_batch_import_task` |


<span id="052b320b"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`batch_id` |String |Required |`6c0001b0-f696-4bfc-acda-a2ee05170485` |The unique identifier for the batch import task. |


<span id="83d650c9"></span>
## Response parameters

<span id="a75f0284"></span>
### Request and response


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|`batch_id` |String |`6c0001b0-f696-4bfc-acda-a2ee05170485` |A unique identifier for the batch import task. |
|`status` |String |`completed` |The upload is complete. |


<span id="607571d6"></span>
## Request example

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/complete_batch_import_task \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "batch_id":"a8fd2b826203421bb977"
}'
```


<span id="94a49ee4"></span>
## Response example

&nbsp;

```Plain Text
{
    "request_id": "c7e10e6a-9764-9ada-b361-6aa642c76514",
    "result": {
        "batch_id": "a8fd2b826203421bb977",
        "status": "completed"
    }
}
```


<span id="b7ad3b5c"></span>
## Error code

See [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more Viking AI search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, the all\-in\-one intelligent engine for enterprise search, recommendations, and Q&A</a></div>
