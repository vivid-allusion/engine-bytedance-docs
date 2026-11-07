---
title: "Import and Update Item Data in Real Time"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Import_and_Update_Item_Data_in_Real_Time"
---

<span id="2c8488f1"></span>
## Use Cases

After creating an item dataset and importing the initial batch of data, you may encounter requirements for real\-time data writing or updates in the following scenarios:


* **Real\-time Field Updates:**  Filtering fields such as product "in\-stock" status or content interaction metrics (likes, comments) may need real\-time synchronization to ensure the timeliness of search and recommendation strategies.

* **Real\-time Addition of New Items:**  For scenarios like new product listings or newly published content, data must be synced to the search and recommendation candidate pools immediately to guarantee content freshness.


In these scenarios, you need to continuously synchronize new data or updated fields from your business database to the AI Search item dataset. Data updates require high timeliness, but the data volume uploaded per minute is relatively small. Real\-time Write API is suitable for such operations.

<span id="73029554"></span>
## **Applicable Dataset Types ** 


|**Dataset type** |**Supports Real\-time Writing** |
|---|---|
|Image & text item dataset |✅ |
|Video item dataset |✅ |
|Document dataset |❌ Not supported currently, only console upload is allowed |


<span id="aa55a8ab"></span>
## API Calls

You can call the Write API to perform real\-time data imports for items (for API details, see: [Write - real-time import/update data](https://docs.byteplus.com/docs/viking-aisearch/Write_-_Import_and_update_data_in_real_time)). You can use the Write API to perform the following operations:


* **Real\-time Addition of Item Data:**  Call the interface to upload new data to the dataset in real\-time. If the dataset is already associated with an active application, the new data will be automatically imported, stored, processed, and indexed. Processing each record may take from a few seconds to dozens of seconds; a large number of images may extend processing time. Video data processing may take longer (processing approximately 1–2 hours of video per hour), depending on video duration and resolution.

* **Real\-time Update of Item Data:**  Call the interface to upload updated data. If you only need to update specific fields, you can include only the Item ID and the specific fields/values to be updated, rather than including all fields. If the updated fields are used only for filtering and not for retrieval, the update will take effect within seconds. If images or video data are updated, processing time will be longer.


Each API call can upload multiple JSON objects (Array of Objects), and multiple records will be written simultaneously.


<Tabs>
<Tab zoneid="BMjuHrP5bf" title="Image & Text dataset">
<TabTitle>Image & Text dataset</TabTitle>

<span id="4c5635cd"></span>
### **Image& Text Dataset Request Example ** 

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/write' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
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
    ]}'
```



</Tab>
<Tab zoneid="IBOH4nr9wD" title="Video dataset">
<TabTitle>Video dataset</TabTitle>

<span id="abe44456"></span>
### Video **Dataset Request Example ** 

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/142460036/write' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
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


<span id="15f71154"></span>
## API Rate Limiting

**To ensure stable real\-time data import and processing,**  we impose rate limits on real\-time data import. The import volume is capped at a maximum of 2,000 records per minute. If this limit is exceeded, the system will return a 429 status code.
