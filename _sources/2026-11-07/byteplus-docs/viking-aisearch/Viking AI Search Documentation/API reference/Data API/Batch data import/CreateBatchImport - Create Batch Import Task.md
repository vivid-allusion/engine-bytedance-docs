---
title: "CreateBatchImport - Create Batch Import Task"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/CreateBatchImport_-_Create_Batch_Import_Task"
---

***Viking AI Search*** * is an enterprise\-grade AI search product based on generative AI. It combines the multimodal semantic representation and understanding capabilities of large models with ByteDance's years of best practices in information retrieval. The platform offers an out\-of\-the\-box service for customers to easily build and integrate end\-to\-end multimodal search and recommendation capabilities for images and text.* 


---



Call this API to create a batch data import task and get a unique task ID. You can then use this ID to batch import item data or check the task status.

We currently support batch import tasks for item data.

<span id="59b78b96"></span>
## Notes


1. **Task Validity Period**: Each batch import task is valid for 24 hours. You must complete the data import and submit the data by calling the complete import task API within 24 hours of creating the task. The task automatically becomes invalid upon expiration.

2. **Task Creation Request Frequency**: You can create up to one batch import task per minute. Avoid frequently creating multiple batch import tasks.


<span id="c4a5d7ef"></span>
## Request Description


* **Request Method**: `POST`

* **Request URL**:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/create_batch_import` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/create_batch_import` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/dataset/{dataset_id}/create_batch_import` |


<span id="2534c944"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`estimated_count`<br><br> |Integer<br><br> |Optional |`1000000` |Estimated total number of data entries for this bulk import. |


<span id="7db1f2f8"></span>
## Response parameters

<span id="3ac28b12"></span>
### Request response


|Parameter |Type |Example |Description |
|---|---|---|---|
|`batch_id` |String |`6c0001b0-f696-4bfc-acda-a2ee05170485` |The unique identifier for the batch import task. |
|`status` |String |initialized |Task status: the initial status of the task returned upon creation. |
|`expired_time`<br><br> |String |`2025-11-19T14:23:45Z`<br><br> |The task's expiration time (ISO 8601 UTC). |


<span id="6a127e66"></span>
## Request example

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/create_batch_import' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "estimated_count":1500000
}'
```


<span id="091e8a5f"></span>
## Response example

&nbsp;

```Plain Text
{
    "request_id": "a8207cf1-2230-9f9b-a819-324b5b325c19",
    "result": {
        "batch_id": "a8fd2b826203421bb977",
        "status": "initialized",
        "expired_time": "2025-12-17T21:15:59+08:00"
    }
}
```


<span id="4a70ba74"></span>
## Error codes

See [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more of Viking AI's search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, an integrated intelligent engine for enterprise search, recommendation, and question answering</a>.</div>
