---
title: "Embedding Calculation"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Embedding_Calculation_V2"
---

<span id="interface-upgrade-notes"></span>
# Interface Upgrade Notes


* Corresponding old interface: [Embedding v2](https://docs.byteplus.com/lwxm71ps/myp4bm1t)

* Usage differences:



| |New Interface |Old Interface |
|---|---|---|
|Model Combination |Dense and sparse models can be specified independently. Supports dense+sparse, dense\-only, or sparse\-only embedding calculation. |Dense and sparse models are specified through the same model_name parameter. |
|Data Limit Per Write Request |No more than 10, with lower latency. |No more than 100 |
|Returns Model Token Usage |Yes |Requires setting an additional parameter for the value to be returned |



* Note: Rate limiting is calculated based on token usage. The rate limiting behavior of V1 and V2 interfaces is exactly the same.


<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the [Data Plane API Calling Process](https://docs.byteplus.com/lwxm71ps/gk6oc6no), copy the code example and fill in the required information.


|URI |/api/vikingdb/embedding |Uniform Resource Identifier |
|---|---|---|
|Method |POST |The type of operation the client requests from the server |
|Request Header |Content\-Type: application/json |Request message type |
| |Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="request-body-parameters"></span>
# Request Body Parameters


|Parameter |Type |Required |Sub\-parameters |Type |Required |Description |
|---|---|---|---|---|---|---|
|dense_model |map |At least 1 of 2 |name |string |Yes |Model name |
| | | |version |string |No, but required for Doubao models |Model version |
| | | |dim |int |No |Dimension. If this parameter is not provided, the default dimension for the model version is used. |
|sparse_model |map | |name |string |Yes |Model name |
| | | |version |string |No |Model version |
|data |list |Yes | | | |Data. Detailed fields are shown below. The maximum list length is 10. If the data type is 'full_modal_seq', the length must be 1 |


Data structure:


|Parameter |Type |Required |Description |
|---|---|---|---|
|text |string |Provide either 'full_modal_seq', or at least one of 'text', 'image', or 'video'. |Text string content. If too long, it will be truncated. Truncation thresholds for each model are shown below. |
|image |string | |Format specifications are provided in the MediaData description below. |
|video |map[string] | |{<br><br>"value": TOS link, HTTP/HTTPS format link (this field is required)<br><br>"fps": 2.0 (this field is optional)<br><br>} |
|full_modal_seq |list | |FullModalData structure is shown below |



* MediaData (e.g., image, video) format specifications:



|Choose 1 of 2 |* TOS resource address within the same region. `tos://{bucket}/{object_key}` |
|---|---|
| |* Publicly accessible http/https link. `http://` or `https://` |



* FullModalData structure:



|Choose 1 of 3 |Field Name |Type |Remarks |
|---|---|---|---|
| |text |string |Plain text |
| |image |string or map |If there are no special configuration parameters, provide the image resource address as a string, according to the MediaData specification;<br><br>If there are special configuration parameters, you can use map type with sub\-parameters including:<br><br><br>* value: Use string type to fill in image resource address, refer to MediaData specification. |
| |video |string or map |If there are no special configuration parameters, provide the video resource address as a string, according to the MediaData specification;<br><br>If there are special configuration parameters, you can use map type with sub\-parameters including:<br><br><br>* value: Use string type to fill in video resource address, refer to MediaData specification.<br><br>* fps: The frame extraction frequency. If not set, the default is 1, and the valid range is 0.2–5.0. However, the server extracts a minimum of 16 frames by default. A higher value results in more extracted frames, which consumes more tokens and increases latency. |


<span id="model-list"></span>
## Model List


|Model Name |Model Version |Supported Vectorization Types |Default Dense Vector Dimension |Optional Dense Vector Dimensions |Text Truncation Length |Supports Sparse Vector |Supports Instruction |
|---|---|---|---|---|---|---|---|
|bge\-large\-zh |(default) |text |1024 |1024 |512 |No |Yes |
|bge\-m3 |(default) |text |1024 |1024 |8192 |Yes |No |
|bge\-visualized\-m3 |(default) |text, image and their combinations |1024 |1024 |8192 |No |No |
|skylark\-embedding\-vision |250615 |Text, image, video, and their combinations. Supports 'full_modal_seq', which is a sequence of text, images, and videos. |2048 |2048, 1024 |128k |No |Yes |


<span id="response-body-parameters"></span>
# Response Body Parameters

For public response body parameters, see

[Data Plane API Calling Process](https://docs.byteplus.com/lwxm71ps/gk6oc6no)


|Parameter Name |Type |Sub\-parameter | |Description |
|---|---|---|---|---|
|result |map |data |list |Data list |
| | |token_usage |map |Token statistics for each model.<br><br>Includes 'prompt_tokens', 'completion_tokens', 'image_tokens', and 'total_tokens'. |


EmbeddingResult structure:


|Parameter Name |Type |Description |
|---|---|---|
|dense |list |Dense vector result |
|sparse |map |Sparse vector result |


<span id="request-response-examples"></span>
# Request Response Examples

<span id="_1-text-dense-sparse"></span>
## 1. Text Dense+Sparse


* Request Parameters


```JSON
req_path = "/api/vikingdb/embedding"
req_body = {
    "dense_model": {
        "name": "Skylark-embedding-large",
        "version": "240915",
        "dim": 1024,
    },
    "sparse_model": {
        "name": "bge-m3",
        "version": "default",
    },
    "data": [
        {
            "text": "The sky is blue."
        },
        {
            "text": "The sea is deep."
        }
    ]
}
```



* Response Parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "dense": [0.05149054509186956,0.034275332726816786, ......],
                "sparse": {
                    "sky": 0.263671875,
                    "is": 0.18603515625,
                    "blue": 0.3046875
                }
            },
            {
                "dense": [0.0076801463728645375,0.034275332726816786, ......],
                "sparse": {
                    "is": 0.2010498046875,
                    "sea": 0.32958984375,
                    "deep": 0.32373046875
                }
            }
        ],
        "token_usage": {
            "bge-m3__default": {
                "prompt_tokens": 14,
                "completion_tokens": 0,
                "image_tokens": 0,
                "total_tokens": 14
            },
            "Skylark-embedding-large__240915": {
                "prompt_tokens": 9,
                "completion_tokens": 0,
                "image_tokens": 0,
                "total_tokens": 9
            }
        }
    }
}
```


<span id="_2-text-image-multimodal"></span>
## 2. Text+Image Multimodal


* Request Parameters


```JSON
req_path = "/api/vikingdb/embedding"
req_body = {
    "dense_model": {
        "name": "bge-visualized-m3",
        "version": "default",
        "dim": 1024
    },
    "data": [
        {"text": "The sky is blue"},
        {"text": "tos://my_bucket/sky_1.jpeg"}
    ]
}
```



* Response Parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "dense": [0.013657506555318832,0.034275332726816786, ......]
            }
        ],
        "token_usage": {
            "bge-visualized-m3__default": {
                "prompt_tokens": 926,
                "completion_tokens": 0,
                "image_tokens": 926,
                "total_tokens": 926
            }
        }
    }
}
```


<span id="_3-text-image-video-multimodal"></span>
## 3. Text+Image+Video Multimodal


* Request Parameters


```JSON
req_path = "/api/vikingdb/embedding"
req_body = {
    "dense_model": {
        "name": "Skylark-embedding-vision",
        "version": "250615",
        "dim": 1024,
    },
    "data": [
        {
            "full_modal_seq":[
                {
                    "text": "haha haha"
                },
                {
                    "image": "tos://my_bucket/images/dogs/5.jpeg"
                },
                {
                    "video": "tos://my_bucket/videos/1.mp4"
                },
                {
                    "video":
                    //If you need custom processing for the video, you can define the video value as JSON to set advanced parameters:
                    //value represents video content;
                    //fps represents frame extraction frequency. If not set, defaults to 1, range is 0.2-5.0. However, the server defaults to extracting at least 16 frames. The higher the value, the more frames extracted, and the more tokens consumed and higher latency.
                        {
                            "value": "tos://my_bucket/videos/2.mp4",
                            "fps": 0.4, 
                        }
                }
            ]
        }
    ]
}
```



* Response Parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "dense": [0.05149054509186956,0.034275332726816786, ......]
            }
        ],
        "token_usage": {
            "Skylark-embedding-vision__250615": {
                "prompt_tokens": 1325,
                "completion_tokens": 0,
                "image_tokens": 1312,
                "total_tokens": 1325
            }
        }
    }
}
```
