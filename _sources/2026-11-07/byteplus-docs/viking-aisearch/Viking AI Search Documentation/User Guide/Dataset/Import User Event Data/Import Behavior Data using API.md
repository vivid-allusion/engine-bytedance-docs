---
title: "Import Behavior Data using API"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Import_Behavior_Data_using_API"
---

<span id="a4430615"></span>
## Use case

After creating a behavior dataset, you can import behavior data via the API for the following scenarios:


* **Import historical behavior data:**  call the write API to import historical behavior data from the past 7 days, 30 days, or other specific periods.

* **Upload behavior data in real time:**  call the write API to synchronize immediate user behaviors such as exposures, clicks, purchases, or views from your system in real\-time. 


<span id="6e326241"></span>
## API Calls

You can call the Write API for real\-time item data import (see API details: [Write - real-time import/update data](https://docs.byteplus.com/docs/viking-aisearch/Write_-_Import_and_update_data_in_real_time)). Behavior data can only be imported incrementally:

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/dataset/{dataset_id}/write' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "fields": [
            {
                "user_id": "user134",
                "item_id": "1235",
                "event_type": "exposure",
                "event_timestamp": 1678886400000,
                "event_scene": "home"
            }，
            {
                "user_id": "user134",
                "item_id": "1235",
                "event_type": "click",
                "event_timestamp": 1678886400300,
                "event_scene": "home"
            }，
        ]
}'
```



* API Key: You can create a valid API Key by following the workflow described in [鉴权机制](https://docs.byteplus.com/docs/undefined/67c52c0142e9c20551c0aee0)

* dataset_id: Specify the behavior dataset ID in the API path where the data is to be written.

* fields: A list of JSON objects, where multiple behavior records are uploaded in JSON object format.


&nbsp;

Each API call accepts a request body of **up to 10MB**. We recommend splitting large volumes of data into multiple batches to avoid timeouts or transmission failures.
