---
title: "Delete model response"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Delete_model_responses"
---

This document describes how to delete a model response with a specified ID.

<span id="8d8b5607"></span>
# Request description


* **Base URL**: Using North China 2 (Beijing) as an example, the Base URL is: https://operator.las.ap\-southeast\-1.bytepluses.com In actual use, you need to use the Base URL for your current service region. For details, see [Usage methods](https://docs.byteplus.com/docs/Byteplus_LAS/Usage_methods).

* **Path**：/api/v1/responses/

* **Method**: DELETE

* **Content\-type**: application/json


<span id="a37e0c5b"></span>
# Request parameters

<span id="119f285e"></span>
## Path parameters


|Parameter name |Data type |Required |Parameter description |
|---|---|---|---|
|response_id |string |Required |The response ID to be deleted. |


<span id="a065ceeb"></span>
# Response parameters


|Parameter name |Data type |Parameter description |
|---|---|---|
|id |string |ID of the request to be deleted. |
|object |string |Fixed as response. |
|deleted |boolean |Value range:<br><br><br>* true: Deleted successfully.<br><br>* false: Deletion failed. |


<span id="71b21aea"></span>
# Example


* request

   ```Bash
   curl -X DELETE https://operator.las.ap-southeast-1.bytepluses.com/api/v1/responses/resp_0217****** \
       -H "Content-Type: application/json" \
       -H "Authorization: Bearer $LAS_API_KEY"
   ```
   

* response

   ```Bash
   {
     "id": "resp_0217******",
     "object": "response",
     "deleted": true
   }
   ```
