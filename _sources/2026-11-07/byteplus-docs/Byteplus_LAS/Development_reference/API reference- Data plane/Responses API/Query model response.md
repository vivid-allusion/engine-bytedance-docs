---
title: "Query model response"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Query_the_model_response"
---

Obtain the model response using the response ID.

# Request description

* **Base URL**: In Asia Pacific (Johor), the Base URL is `https://operator.las.ap-southeast-1.bytepluses.com`. When using the API, use the Base URL for the region where your LAS service is deployed. For details, see [Usage methods](https://docs.byteplus.com/docs/Byteplus_LAS/Usage_methods).

* **Path**：/api/v1/responses/

* **Method**: GET

* **Content\-type**: application/json

# Request parameters

### Path parameters

|Parameter name |Data type |Required |Parameter description |
|---|---|---|---|
|response_id |string |Required |The response ID to be retrieved. |

## Response parameters

* If the response you called has been completed, the model will return the corresponding [The response object](https://docs.byteplus.com/docs/Byteplus_LAS/The_response_object).

* If the response you called has not been completed, the model will return an error code.

# Example

* request

   ```Bash
   curl --location 'https://operator.las.ap-southeast-1.bytepluses.com/api/v1/responses/resp_0217******' \
   --header "Authorization: Bearer $LAS_API_KEY" \
   --header 'Content-Type: application/json'
   ```

* response

   ```JSON
   {
       "created_at": 1754571515,
       "id": "resp_0217******",
       "max_output_tokens": 32768,
       "model": "seed-1-6-250615",
       "object": "response",
       "output": [
           {
               "type": "message",
               "role": "assistant",
               "content": [
                   {
                       "type": "output_text",
                       "text": "The image shows a red-haired girl resting her cheek against a red fox in a quiet meadow. The girl's auburn hair echoes the fox's warm coat, while the fox's white chest, dark ears, and amber eyes stand out in the soft light. Their relaxed posture conveys trust and companionship, creating a calm and comforting scene."
                   }
               ],
               "status": "completed",
               "id": "msg_0217******"
           }
       ],
       "thinking": {
           "type": "enabled"
       },
       "status": "completed",
       "usage": {
           "input_tokens": 1377,
           "output_tokens": 910,
           "total_tokens": 2287,
           "input_tokens_details": {
               "cached_tokens": 0
           },
           "output_tokens_details": {
               "reasoning_tokens": 552
           }
       },
       "caching": {
           "type": "disabled"
       },
       "store": true,
       "expire_at": 1754830715
   }
   ```
