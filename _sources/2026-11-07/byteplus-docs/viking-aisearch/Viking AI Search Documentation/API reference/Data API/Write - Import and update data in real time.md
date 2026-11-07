---
title: "Write - Import and update data in real time"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Write_-_Import_and_update_data_in_real_time"
---

***Viking AI Search*** * is an enterprise\-level AI search product powered by generative AI. It combines the multimodal semantic understanding of large models with ByteDance's best practices in information retrieval. This out\-of\-the\-box platform helps customers easily build and integrate end\-to\-end multimodal search and recommendation capabilities for text and images.* 


---



Call this API to write item and user event data to a specified dataset **in real time**. Data processing and indexing start immediately.

Use this API to write item and user event datasets:


* **Item dataset:**  Stores structured data for searchable items in the AI engine, uploaded as a list of JSON objects. The schema of the uploaded data must match the schema you defined for the item dataset in the console.

* **User event dataset:**  Stores historical and incremental user behavior data as structured data, which is uploaded as a list of JSON objects. The schema of the uploaded data must match the schema you defined for the behavior dataset in the console.


&nbsp;

You can also use this API to update data in the datasets:


* **Item dataset: ** Uploading item data with a unique identifier that already exists in the dataset triggers a data update. The newly uploaded data will overwrite the existing data.

* **User event dataset**: Updating historical behavior data is not supported.


&nbsp;

<span id="998280aa"></span>
## Note


* **Usage limits:** 

   * The body of a single request cannot exceed 10 MB due to the HTTP body size limit.

* **Import rate limiting: ** To ensure the stability of real\-time data imports and processing, we apply rate limiting for real\-time data imports. The logic is as follows:



|**Dataset type** |**Rate limit** |**Description** |
|---|---|---|
|Item dataset |2,000 items/min |If more than 2,000 data entries are sent within 1 minute, the API returns a 429 status code and the WriteDataLimitExceeded rate limit error code.<br><br>To upload or update a large volume of item data in a short time, use the Bulk Import Data API. View [Batch Import Item Data](https://docs.byteplus.com/docs/viking-aisearch/Batch_Import_Item_Data). |
|User event dataset |500,000 entries/minute |If more than 500,000 data entries are sent within 1 minute, the API returns a 429 status code and the WriteDataLimitExceeded rate limit error code.<br><br>The bulk import API is not available for behavioral data. Contact us if the real\-time import rate for your behavioral data exceeds the limit. |



---



<span id="53507199"></span>
## Request description


* Request method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/dataset/{dataset_id}/write` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/write` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/dataset/{dataset_id}/write` |


 *{dataset_id}*  *: The unique ID assigned to a dataset after it is created in the console. You can find it in the console.* 

<span id="a710b8e2"></span>
## Request Parameters

<span id="ae68862e"></span>
### Image\-Text Dataset Request Body


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|fields |Array of Object |<span data-api-tag="require\|ahWEyYTEB">必选</span> |&nbsp;<br><br>```JSON```<br>```［```<br>```    { ```<br>```        "item_id": "SHOE001", ```<br>```         "title": "MyProduct", ```<br>```         "category": "Shoes", ```<br>```         "status": 1,```<br>```         "images": [ ```<br>```         { ```<br>```             "image_url": "https://example.com/images/womens_pump_black.jpg" ```<br>```          } ```<br>```         ] ```<br>```     }```<br>```］```<br> |Data to write to the dataset. Input an array where each element is a single record. |


<span id="df57f0fd"></span>
#### Upload Image Files

When uploading data, upload the image file data according to the field types defined in your dataset. To allow AI Search Engine to process and index images, you must upload image files that comply with the formats and restrictions outlined below:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">The provided images must meet the following conditions:</div>



1. <div data-tips="true" data-tips-type="default"><strong>Supported formats:</strong> jpeg, png, webp, bmp, tiff, and icns. For TIFF and ICNS images, ensure they are aligned with their metadata by correctly setting it in object storage. Otherwise, parsing will fail.</div>


2. <div data-tips="true" data-tips-type="default"><strong>Aspect ratio (width/height):</strong> In the range of [1/100, 100].</div>


3. <div data-tips="true" data-tips-type="default"><strong>Side length:</strong> [10, 6000] px, i.e., the shorter side must be greater than 10 px and the longer side must be less than 6000 px.</div>



&nbsp;

Based on the attributes defined in your dataset configuration, you can upload images via publicly accessible URLs or by using Base64 encoding:


1. **Upload via URL:**  Ensure your URL remains publicly accessible. If your link has access restrictions, add the [aisearch.cn-beijing.volces.com](http://aisearch.cn-beijing.volces.com/) domain to your allowlist.

2. **Upload via Base64 encoding:**  Ensure the Base64 encoding follows the standard format, which includes both a **data header (Data URI scheme)**  and a **Base64\-encoded body**:


&nbsp;


<Tabs>
<Tab zoneid="MmT1fHb4Bu" title="Format">
<TabTitle>Format</TabTitle>

```JSON
data:<MIME类型>;base64,<Base64 Encoded String>
```



</Tab>
<Tab zoneid="naez3vdpTx" title="JPEG image">
<TabTitle>JPEG image</TabTitle>

```JSON
data:image/jpeg;base64,<Base64 Encoded String>
```



</Tab>
<Tab zoneid="VNGUlGmXeQ" title="PNG image">
<TabTitle>PNG image</TabTitle>

```JSON
data:image/png;base64,<Base64 Encoded String>
```



</Tab>
<Tab zoneid="h0QGc6laZb" title="WebP image">
<TabTitle>WebP image</TabTitle>

```JSON
data:image/webp;base64,<Base64 Encoded String>
```



</Tab>
</Tabs>



|**Components** |**Format requirements** |**Description** |
|---|---|---|
|Data header prefix |Set to `data:` |Indicates that the string is in the Data URI format and cannot be omitted or modified. |
|MIME type |Must strictly match the image's actual format. |Used by the server to identify the image type. Do not enter an incorrect value, such as using a PNG MIME type for a JPG image. |
|Separator |Must be `;base64,` |Connects the MIME type with the Base64\-encoded body. The semicolon, "base64," and comma cannot be omitted or replaced. |
|Base64\-encoded body |A Base64\-encoded string compliant with the RFC 4648 standard. |Directly encoded from the binary data of the image file. **It must not contain spaces, newlines, or special characters** and must be a continuous ASCII string. |


<span id="baee1e98"></span>
### Video Dataset Request Body


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|fields |Array of Object |<span data-api-tag="require\|a0WNiafv8">必选</span> |```JSON```<br>```[```<br>```    {```<br>```        "content_id": "video_900026",```<br>```        "content_type": "video",```<br>```        "parent_content_id": "collection_342534",```<br>```        "sequence_index": 26,```<br>```        "video_url": [```<br>```            "http://xxxx.mp4"```<br>```        ],```<br>```        "my_title": "MyVideo"```<br>```    }```<br>```]```<br> |The data to write to the dataset. The input is an array, where each element is a single record. |


<span id="4d637d33"></span>
#### Upload Video File

Upload video data according to the field types you have defined in the dataset. In a video dataset, use `video_url` (Array<String\>) to upload a list of URLs for a single video. This supports combining multiple video clips into one video. The upload format and requirements for videos are as follows:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Video Formats and Requirements</div>



1. <div data-tips="true" data-tips-type="default">Before importing video download links, ensure their download URLs are accessible to the official Volcano Engine API domain. Uploading webpage links to crawl for videos is not supported.</div>


2. <div data-tips="true" data-tips-type="default">Before uploading, ensure all video files in the list <strong>do not exceed a total of 10 GB in size and 3 hours in duration</strong>.</div>


3. <div data-tips="true" data-tips-type="default">The following video formats are supported:</div>


   <div data-tips="true" data-tips-type="default">mp4、flv、asf、rm、rmvb、mpeg、mov、avi、mpegts、m4s、m3u8、matroska、wmv、3gp、ts、mpg、webm、mkv、wm、asx、ram、mpe、vob、dat、mp4v、m4v、f4v、mxf、qt   </div>
   


&nbsp;

<span id="b2a1fe08"></span>
### User Behavior Dataset Request Body


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|fields |Array of Object |<span data-api-tag="require\|aowpkLAWa">必选</span> |```JSON```<br>```[```<br>```    {```<br>```        "user_id": "user134",```<br>```        "item_id": "1235",```<br>```        "event_type": "impression",```<br>```        "event_timestamp": 1678886400000,```<br>```        "event_scene": "home"```<br>```    }```<br>```]```<br> |1. The data to be written to the dataset. Input an array where each element represents a single data entry.<br><br><br>&nbsp;<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">Each behavioral data entry must include: User ID, Item ID, Behavior Type, Behavior Time, and Behavior Scene. If required fields are missing, downstream data processing automatically ignores invalid behavioral data.</div><br><br><br> |


<span id="5d548669"></span>
## Response Parameters

<span id="55d1dea4"></span>
### Response


|**Parameter** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|request_id |String |25ee998a\-5462\-9385\-9f18\-035f1da7a6e5 |A unique identifier for a request that allows you to quickly locate its execution. |


<span id="5c86e898"></span>
## Request Example


<Tabs>
<Tab zoneid="oVPTqhFiWx" title="Image-Text Dataset">
<TabTitle>Image-Text Dataset</TabTitle>

<span id="c5cdac3d"></span>
### Image\-Text Dataset Request Example

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/write' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
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
            "category": "Shoes",
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
<Tab zoneid="LGzTERmKje" title="Video Dataset">
<TabTitle>Video Dataset</TabTitle>

<span id="5a94e783"></span>
### Video Dataset Request Example

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/write' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <火山鉴权的一系列相关header>' \
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
<Tab zoneid="cNy7rJPzUm" title="User Behavior Dataset">
<TabTitle>User Behavior Dataset</TabTitle>

<span id="c1958b47"></span>
### User Behavior Dataset Request Example

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/write' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <火山鉴权的一系列相关header>' \
  -d '{
    "fields": [
            {
                "user_id": "user134",
                "item_id": "1235",
                "event_type": "曝光",
                "event_timestamp": 1678886400000,
                "event_scene": "home"
            },
            {
                "user_id": "user134",
                "item_id": "1235",
                "event_type": "点击",
                "event_timestamp": 1678886400300,
                "event_scene": "home"
            }
        ]
}'
```



</Tab>
</Tabs>


<span id="c2d1410f"></span>
## Response Example

```Plain Text
{
    "request_id": "25ee998a-5462-9385-9f18-035f1da7a6e5"
}
```


&nbsp;

<span id="6082e63e"></span>
## Error handling

<span id="5f76fd39"></span>
### Error code


|**HTTP Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|429 |WriteDataLimitExceeded |The specified data write limit has been exceeded: **items per minute** |The rate limit for real\-time item data writes has been exceeded. |
|429 |WriteDataLimitExceeded |The specified data write limit has been exceeded: **events per minute** |Real\-time writes for behavioral data have exceeded the rate limit. |


For other common error codes, see the [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes) documentation.


---



*To experience more of Viking AI's search capabilities, go to * [Viking AI Search Engine, the all-in-one intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec) *.*
