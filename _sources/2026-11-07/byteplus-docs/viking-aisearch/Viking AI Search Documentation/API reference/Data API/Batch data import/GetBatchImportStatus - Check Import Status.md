---
title: "GetBatchImportStatus - Check Import Status"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/GetBatchImportStatus_-_Check_Import_Status"
---

***Viking AI Search*** * is an enterprise\-level AI search product based on generative AI. It uses the multimodal semantic representation and understanding of large models, combined with ByteDance's years of best practices in information retrieval, to provide an out\-of\-the\-box AI search platform. This helps customers easily build and integrate end\-to\-end multimodal search and recommendation capabilities for images and text.* 

&nbsp;


---



Check the current status and statistics of a specified batch import task.

<span id="5bb2bc1f"></span>
## Notes

**Task validity**: each batch import task is valid for 24 hours. You must import and submit the data by calling the import task completion API within 24 hours of task creation. The task automatically becomes invalid upon expiration.

**Data statistics latency**: statistics may have a latency of a few seconds. We recommend an interval of over 5s between import and query API calls.

<span id="439dab39"></span>
## Request Details


* **Request Method**: POST

* **Request URL**:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/get_batch_import_status` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/get_batch_import_status` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/dataset/{dataset_id}/get_batch_import_status` |


<span id="17019e2e"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`batch_id` |String |Yes |`6c0001b0-f696-4bfc-acda-a2ee05170485` |The unique identifier for the batch import task. |


<span id="8633f912"></span>
## Response parameters

<span id="159a1ab8"></span>
### Request response


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|`batch_id`<br><br> |String |`6c0001b0-f696-4bfc-acda-a2ee05170485` |The unique identifier for the batch import job. |
|`status` |String |`processing` |Current status of the task (`initialized`, `processing`, `completed`, `expired`). |
|`total_received` |Integer |`5000` |The total number of data entries the task has received. |
|`expired_time` |String |`2025-11-19T14:23:45Z` |The expiration time of the task. |


<span id="8dfaa12b"></span>
## Request example

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/get_batch_import_status \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "batch_id":"a8fd2b826203421bb977"
}'
```


<span id="90a6ddeb"></span>
## Response example

```Plain Text
{
    "request_id": "346c59cc-0c28-945e-b504-92d2a45cc2b7",
    "result": {
        "batch_id": "a8fd2b826203421bb977",
        "status": "completed",
        "total_received": 2,
        "expired_time": "2025-12-17T21:15:59+08:00"
    }
}
```


<span id="851beca2"></span>
## Error codes

See [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more of Viking AI's search capabilities, visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, an integrated intelligent engine for enterprise search, recommendations, and Q&A</a>.</div>
