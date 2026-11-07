---
title: "BatchImport - Batch data import"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/BatchImport_-_Batch_data_import"
---

***Viking AI Search*** * is an enterprise\-grade AI search product based on generative AI. It uses the multimodal semantic representation and understanding capabilities of large language models, combined with years of best practices from ByteDance in information retrieval. Viking AI Search provides an out\-of\-the\-box AI search platform service that helps customers easily build and integrate end\-to\-end multimodal image and text search and recommendation capabilities.* 


---



After creating a batch import task (see: [CreateBatchImport - Create Batch Import Task](https://docs.byteplus.com/docs/viking-aisearch/CreateBatchImport_-_Create_Batch_Import_Task)), use the returned `batch_id` to import the batch data sequentially.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default"><strong>You should call this API multiple times with the same </strong><strong><code>batch_id</code></strong><strong> instead of creating multiple BatchImport tasks. </strong>All uploaded data across different API requests will be collected into a single import batch. </div>


&nbsp;

**After the upload is complete, you should invoke the 'Complete Upload' API to finish the import operation for the batch. The system will then automatically start the subsequent data storage and processing workflow.** 

Currently, batch data import only supports the item dataset and includes the following data actions:


* **Batch import new data:**  Use this when you need to batch import the full set of candidate data after creating a dataset. Upload item data as a list of JSON objects. The uploaded data schema must match the one you defined in the console when you created the dataset.

* **Batch update data:**  Uploading item data with a unique identifier that already exists in the dataset triggers an update. The newly uploaded data overwrites the existing data. If you only need to update certain fields in a batch of data, you only need to upload the item's ID and the fields to be updated for each record.


&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Important</div>


<div data-tips="true" data-tips-type="warning">Avoid creating multiple BatchImport tasks to increase import speed. Due to task orchestration overhead, <strong>importing larger amounts of data through a single BatchImport task is faster than multiple smaller BatchImport tasks.</strong></div>



---



<span id="51c773eb"></span>
## Note


1. **Task validity period**: Each batch import task is valid for 24 hours. You need to complete the data import and submit this data batch by invoking the import task completion API within 24 hours of creating the task. The task automatically becomes invalid after expiration.

2. **API request body limit:**  You can successively invoke the batch import API to upload data within the same batch. The request body for each invocation cannot exceed 10MB.

3. **Batch import API rate limit:**  The batch import API is limited to a request frequency of **50 QPS**. 



---



<span id="65cc013d"></span>
## Request details


* **Request method**: `POST`

* **Request URL**:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/batch_import` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/batch_import` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/dataset/{dataset_id}/batch_import` |


<span id="5a248040"></span>
## Request parameters

<span id="5af88527"></span>
### Image and text dataset request body


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|batch_id |String |Yes |`"a8fd2b826203421bb977"` |The batch_id returned when a batch import task is created |
|fields |Array of Object |Yes |Image and text data:<br><br>```JSON```<br>```［```<br>```    { ```<br>```        "item_id": "WSHOE001", ```<br>```         "title": "舒适通勤 尖头浅口高跟鞋 - 黑色", ```<br>```         "category": "女士高跟鞋", ```<br>```         "status": 1,```<br>```         "images": [ ```<br>```         { ```<br>```             "image_url": "https://example.com/images/womens_pump_black.jpg" ```<br>```          } ```<br>```         ] ```<br>```     }```<br>```］```<br> |The data to write to the dataset. Input an array where each element is a single data entry. |


<span id="0b29143d"></span>
#### Upload image files

When uploading data, upload image file data according to the data types defined in the dataset. You must upload image files that meet the format and restrictions described below for Viking AI Search to process and index them:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Images must meet the following conditions:</div>



1. <div data-tips="true" data-tips-type="default"><strong>Supported formats:</strong> jpeg, png, webp, bmp, tiff, ico, dib, icns, sgi, jpeg2000. For images in tiff, sgi, icns, and jpeg2000 formats, ensure alignment with metadata (e.g., setting the file metadata correctly in object storage), otherwise parsing will fail.</div>


2. <div data-tips="true" data-tips-type="default"><strong>Aspect ratio (width/height):</strong> [1/100, 100].</div>


3. <div data-tips="true" data-tips-type="default"><strong>Side length:</strong> [10, 6000] px, i.e., the short side must be greater than 10 px and the long side must be less than 6000 px.</div>



&nbsp;

You can upload publicly accessible URL links or directly upload image files using Base64 encoding, according to the attributes defined in your dataset configuration:


1. **Upload using a URL link:**  Ensure your URL link is publicly accessible. If your link has access restrictions, add the [aisearch.cn-beijing.volces.com](http://aisearch.cn-beijing.volces.com/) domain to the allowlist.

2. **Upload an image file using Base64 encoding:**  Ensure the Base64 encoding follows the standard format, which includes a **data header (Data URI scheme)**  and a **Base64\-encoded body**:



<Tabs>
<Tab zoneid="kOKhqeuy33" title="Format">
<TabTitle>Format</TabTitle>

```JSON
data:<MIME Type>;base64,<Base64 Encoded String>
```



</Tab>
<Tab zoneid="awO37I2YD3" title="JPEG image">
<TabTitle>JPEG image</TabTitle>

```JSON
data:image/jpeg;base64,<Base64 Encoded String>
```



</Tab>
<Tab zoneid="DFIug4Uilv" title="PNG image">
<TabTitle>PNG image</TabTitle>

```JSON
data:image/png;base64,<Base64 Encoded String>
```



</Tab>
<Tab zoneid="EWAXrahN4X" title="WebP image">
<TabTitle>WebP image</TabTitle>

```JSON
data:image/webp;base64,<Base64 Encoded String>
```



</Tab>
</Tabs>


<span id="fa8912ae"></span>
### Video dataset request body


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|batch_id |String |Yes |`"a8fd2b826203421bb977"` |The `batch_id` returned when a batch import task is created. |
|fields |Array of Object |Yes |```JSON```<br>```[```<br>```    {```<br>```        "content_id": "video_900026",```<br>```        "content_type": "video",```<br>```        "parent_content_id": "collection_342534",```<br>```        "sequence_index": 26,```<br>```        "video_url": [```<br>```            "http://xxxx.mp4"```<br>```        ],```<br>```        "my_title": "MyVideo"```<br>```    }```<br>```]```<br> |The data to write to the dataset. Enter an array where each element is a single data record. |


<span id="923b58b2"></span>
#### Upload video files

When you upload data, upload the video data according to the data type you have defined in the dataset. In a video dataset, use video_url (Array<String\>) to upload a list of URLs for a single video (supports splicing multiple video clips into 1 video). The upload format and requirements for videos are as follows:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Video formats and requirements</div>



1. <div data-tips="true" data-tips-type="default">Before you import video download URLs, ensure that they can be accessed by the official Volcano Engine API domain. Uploading webpage links to crawl videos is not supported.</div>


2. <div data-tips="true" data-tips-type="default">Before uploading, ensure that for all video files in the list, <strong>the total size is no more than 10 GB and the total duration is no more than 3 hours</strong>.</div>


3. <div data-tips="true" data-tips-type="default">You can upload video files in the following formats:</div>


   <div data-tips="true" data-tips-type="default">mp4、flv、asf、rm、rmvb、mpeg、mov、avi、mpegts、m4s、m3u8、matroska、wmv、3gp、ts、mpg、webm、mkv、wm、asx、ram、mpe、vob、dat、mp4v、m4v、f4v、mxf、qt   </div>
   


<span id="661036fa"></span>
## Response parameters

<span id="4645d3a0"></span>
### Request response


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|`batch_id` |String |`6c0001b0-f696-4bfc-acda-a2ee05170485` |The unique identifier for the batch import task. |
|`accepted_count` |Integer |`1000` |The number of data entries successfully received for this request. |
|`total_received` |Integer |`5000` |The total number of data entries received for the task. |
|`status` |String |`processing` |The current Status of the task. |
|`expired_time` |String |`2025-11-19T14:23:45Z` |The expiration time of the task. |


<span id="0ef5d04c"></span>
## Request example


<Tabs>
<Tab zoneid="HGdfUSQtB2" title="Image and text dataset">
<TabTitle>Image and text dataset</TabTitle>

Image and text dataset batch upload example:

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/batch_import' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "batch_id":"a8fd2b826203421bb977",
    "fields": [
                {
                    "item_id": "WSHOE001",
                    "title": "MyProduct",
                    "category": "Shoes",
                    "status": 1,
                    "images": [
                        {
                            "image_url": "https://example.com/images/womens_pump_black.jpg"
                        }
                    ]
                },
                {
                    "item_id": "WSHOE002",
                    "title": "MyProduct2",
                    "category": "Clothes",
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
<Tab zoneid="YU1RwenSOe" title="Video dataset">
<TabTitle>Video dataset</TabTitle>

Video dataset batch upload example:

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/batch_import' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <火山鉴权的一系列相关header>' \
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
                    "my_title": "三体第二十六集"
                },
                {
                    "content_id": "video_900027",
                    "content_type": "video",
                    "parent_content_id": "collection_342534",
                    "sequence_index": 27,
                    "video_url": [
                        "http://xxxx.mp4"
                    ],
                    "my_title": "三体第二十七集"
                }
    ]
}'
```





</Tab>
</Tabs>


<span id="2e4d42f7"></span>
## Response example

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


<span id="aab7e956"></span>
## Error codes

See: [Common Error Messages](https://docs.byteplus.com/docs/viking-aisearch/Meaning_and_handling_of_common_error_messages)


---



*To experience more Viking AI Search capabilities, go to: * [Viking AI Search, the all-in-one intelligent engine for enterprise search, recommendations, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)
