---
title: "Batch Import Item Data"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Batch_Import_Item_Data"
---

<span id="5ea804d6"></span>
## Use Cases

After creating an item dataset, you may encounter scenarios requiring large\-scale data imports:


* Batch importing all product or content data for the first time for a full test or production environment.

* Performing high\-volume updates (over 100,000 records), such as bulk changes to "listing/unlisting" status.

* Adding new data fields and writing new field values in bulk for all existing products or content.


In such scenarios, if the volume of data to be updated exceeds 10,000 records per operation, real\-time write APIs may not meet your needs. You can use the Batch Import Item Data API to perform the operations.

&nbsp;

Currently, batch import only supports **Item Datasets** and allows the following operations:


* **Batch Import New Data:**  Suitable for importing the entire candidate data pool after a dataset is created. Item data is uploaded as a list of JSON Objects. The schema must strictly follow the schema you configured in the console.

* **Batch Update Data:**  Triggered by re\-uploading data with a unique ID that already exists in the dataset. The most recently uploaded data will overwrite existing data. If you only need to update specific fields, each record only requires the **Item ID** and the **fields to be updated**.


&nbsp;

<span id="4970c8b5"></span>
## Applicable Dataset Types


|**Dataset type** |**Supports batch import** |
|---|---|
|Image and text item dataset |✅ |
|video item dataset |✅ |
|document dataset |❌ not supported yet |


<span id="923936ab"></span>
## Batch Import Process Overview

Use the following set of APIs to complete the batch import process. Please execute the steps in the order listed below:


* API authentication: [API Authentication](https://docs.byteplus.com/docs/393/API_Authentication)

* Create bulk import task: [CreateBatchImport - Create Batch Import Task](https://docs.byteplus.com/docs/393/92192)

* Batch import data: [BatchImport - Batch data import](https://docs.byteplus.com/docs/viking-aisearch/92260)

* Complete batch import task: [CompleteBatchImportTask - Complete Batch Import](https://docs.byteplus.com/docs/viking-aisearch/CompleteBatchImportTask_-_Complete_Batch_Import)

* Check batch import task status: [GetBatchImportStatus - Check Import Status](https://docs.byteplus.com/docs/viking-aisearch/GetBatchImportStatus_-_Check_Import_Status)


&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5b96dda5bdd546eb9be86c2929dbe709) </span>

&nbsp;

<span id="9dcb44c7"></span>
### Step 1: create a batch import task

Call the *create_batch_import* API under the dataset path to create a batch import task. For API details, see: [CreateBatchImport - Create Batch Import Task](https://docs.byteplus.com/docs/viking-aisearch/CreateBatchImport_-_Create_Batch_Import_Task)

You can upload `estimated_count` to provide the expected import data volume, which will be returned during status queries for verification:

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/create_batch_import \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "estimated_count":1500000
}'
```



* `dataset_id`: The ID of the target dataset must be passed in the URL path.

* `API Key`: You can create a valid API Key by following the process in the [鉴权机制](https://docs.byteplus.com/docs/undefined/67c52c0142e9c20551c0aee0)


The interface will return the `batch_id` corresponding to this import task, which can be used with `batch_id` to call subsequent batch upload and status query interfaces.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">The <code>batch_id</code> has an expiration period. If no data is imported and the <em>CompleteBatchImportTask</em> interface is not called to complete the task within <strong>24 hours</strong> of obtaining the <code>batch_id</code>, it will become invalid. An error will occur when calling the interface to upload, query, or complete tasks.</div>


**Response Example:** 

```Bash
{
    "request_id": "a8207cf1-2230-9f9b-a819-324b5b325c19",
    "result": {
        "batch_id": "a8fd2b826203421bb977",
        "status": "initialized",
        "expired_time": "2025-12-17T21:15:59+08:00"
    }
}
```


<span id="4033e8a1"></span>
### Step 2: upload batch data

You can call the *batch_import* interface multiple times by passing `batch_id` and batch data. For API details, please see: [BatchImport - Batch data import](https://docs.byteplus.com/docs/viking-aisearch/92260)


<Tabs>
<Tab zoneid="uYeM2rz23B" title="Image & Text dataset">
<TabTitle>Image & Text dataset</TabTitle>

**Batch Upload Example for Image & Text Dataset**

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/batch_import' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "batch_id":"a8fd2b826203421bb977",
    "fields": [
                {
                    "item_id": "WSHOE001",
                    "title": "Comfortable Commuter Pointed-Toe Pumps - Black",
                    "category": "Women High Heels",
                    "status": 1,
                    "images": [
                        {
                            "image_url": "https://example.com/images/womens_pump_black.jpg"
                        }
                    ]
                },
                {
                    "item_id": "WSHOE002",
                    "title": "Lightweight Mesh Running Sneakers - Pink/Grey",
                    "category": "Women Sports Shoes",
                    "status": 1,
                    "images": [
                        {
                            "image_url": "https://example.com/images/womens_sneaker_pink.jpg"
                        }
                    ]
                }
            ]
}'
```



</Tab>
<Tab zoneid="R5jo1O1WVE" title="Video dataset">
<TabTitle>Video dataset</TabTitle>

**Batch Upload Example for Video Dataset**

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/batch_import' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <Series of relevant Volcengine authentication headers>' \
  -d '{
    "fields": [
        {
            "content_id": "video_900026",
            "content_type": "video",
            "parent_content_id": "collection_342534",
            "sequence_index": 26,
            "video_url": [
                "http://xxxx.mp4"
            ],
            "my_title": "Three-Body Episode 26"
        },
        {
            "content_id": "video_900027",
            "content_type": "video",
            "parent_content_id": "collection_342534",
            "sequence_index": 27,
            "video_url": [
                "http://xxxx.mp4"
            ],
            "my_title": "Three-Body Episode 27"
        }
    ]
}'
```





</Tab>
</Tabs>


As long as the total request body does not exceed the **10MB** size limit, you can pass multiple item data objects using an Array of Objects in each request. All objects uploaded will be processed within the same batch import task. For example, using the same `batch_id` for a single item dataset, you could upload 5,000 item objects per call and repeat this 100 times until all 500,000 records are uploaded.

Each API call will return the number of records uploaded in that specific request as well as the total accumulated count for the current batch:

```Plain Text
{
    "request_id": "41feb961-6b21-94e0-ba4e-c063aaff0784",
    "result": {
        "batch_id": "a8fd2b826203421bb977",
        "accepted_count": 2,
        "total_received": 2,
        "status": "processing",
        "expired_time": "2025-12-17T21:15:59+08:00"
    }
}
```


<span id="0e1294c5"></span>
### Step 3: confirm batch upload completion

After you have finished uploading all your data, call the *complete_batch_import_task* interface to indicate completion. This will trigger the system to start the storage, parsing, and processing of the batch. For API details, please refer to:  [CompleteBatchImportTask - Complete Batch Import](https://docs.byteplus.com/docs/viking-aisearch/CompleteBatchImportTask_-_Complete_Batch_Import)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">If you do not call the <em>complete</em> interface, the system will not initiate the data storage and processing workflow; the uploaded data will remain in a <strong>"processing"</strong> (uploading) status. Once the task times out, the uploaded data will be discarded and will not be stored or processed. </div>


```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/complete_batch_import_task \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "batch_id":"a8fd2b826203421bb977"
}'
```


The interface will return a final task status of "completed".

```Plain Text
{
    "request_id": "c7e10e6a-9764-9ada-b361-6aa642c76514",
    "result": {
        "batch_id": "a8fd2b826203421bb977",
        "status": "completed"
    }
}
```


<span id="2978d8ae"></span>
### **Query Batch Upload Task Status**

You can call the *get_batch_import_status* interface at any time during the import process to check the current task status and the volume of imported data. For API details, please refer to [GetBatchImportStatus - Check Import Status](https://docs.byteplus.com/docs/viking-aisearch/GetBatchImportStatus_-_Check_Import_Status)

```Bash
curl -X GET 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/batch_import_status \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "batch_id":"6c0001b0-f696-4bfc-acda-a2ee05170485"
}'
```


The interface will return the current status of the task and the total number of records imported:

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
