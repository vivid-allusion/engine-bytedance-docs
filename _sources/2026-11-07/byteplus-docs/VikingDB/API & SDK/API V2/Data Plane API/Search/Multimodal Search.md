---
title: "Multimodal Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Multimodal_Search_V2"
---

<span id="overview"></span>
# Overview

Multimodal data search refers to the vector database's support for direct search through multimodal data types such as text and images, and supports modal combinations, such as text\-to\-image search, image\-to\-image search, image\-to\-text + image search, etc.

<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process, copy the calling example and fill in the necessary information.


|URI |/api/vikingdb/data/search/multi_modal |Uniform Resource Identifier |
|---|---|---|
|Method |POST |Client operation type for the vector database server |
|Headers |Content\-Type: application/json |Request message type |
| |Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="request-body-parameters"></span>
# Request Body Parameters

Only parameters specific to this interface are listed. For more information, refer to the linked documentation.

https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process


|Parameter |Required |Type |Description |
|---|---|---|---|
|text |at least one |string |Text content for search |
|image | |string |* Image TOS link. `tos://{bucket}/{object}`<br><br>* http/https URL |
|video | |map |{<br><br>"value": A TOS link or an http/https URL (required)<br><br>"fps": 2.0 (0.2\-5 optional)<br><br>} |
|need_instruction |Required if the model supports instruction capability. |bool |For text\-based search, you can view the actual effective search statement in the real_text_query parameter in the response. |
|rerank |No |map |Rerank parameter: After retrieval, rerank can be optionally used to reorder data. |
|tensor_rerank |No |map |Tensor rerank parameter. |


<span id="rerank-sub-parameter-list"></span>
### Rerank Sub\-parameter List


|Parameter Name |Required |Type |Description |
|---|---|---|---|
|model_name |Yes |string |Name of the rerank model. |
|model_version |Yes |string |Version of the rerank model. |
|input_limit |No |int |The number of data entries that enter the rerank phase after retrieval. The value defaults to the limit parameter in the search request, and must not exceed 100. Requirement: `search.limit <= search.rerank.input_limit <= 100`. When a search request is executed, the system first retrieves the amount of data specified by `rerank.input_limit` for reranking, and finally returns the top `search.limit` entries from the reranked results. |
|instruction |No |string |Rerank instruction. It is not filled in by default. In specific usage scenarios, filling in the instruction can improve reranking performance. Below are some reference examples:<br><br>Whether the Document answers the Query or matches the content retrieval intent<br><br>Whether the Document and Query represent duplicate questions<br><br>Find images that are exactly the same as the Query image. The query image may have been edited (for example, scaled, cropped, or watermarked). Ignore these modifications and find the original, unedited image.<br><br>Determine if the sequence of video screenshots in the document matches the video description in the query. The document contains keyframe screenshots from the video, arranged chronologically. Consider elements such as the scene, characters, actions, objects, and emotional expression to determine if the document and query refer to the same video content. |
|score_threshold |No |float |Optional, filters results by rerank score threshold. Data with a score lower than `score_threshold` will not be returned. Default value is 0, recommended value range is 0.01\-0.1, common reference value is 0.5. |
|fail_strategy |No |string |Processing strategy when the rerank call fails:<br><br>`fallback`: Default, fall back to returning the sorting results from vector retrieval, and display the error in the `rerank_error` field of the returned result.<br><br>`fail_fast`: Fail fast. If reranking fails for any data entry, the entire request will fail. |
|timeout_ms |No |int |Rerank timeout period. A timeout will be counted as a rerank failure and trigger the configured `fail_strategy`. |


<span id="tensor-rerank-sub-parameter-list"></span>
### Tensor_rerank Sub\-parameter List


|Parameter Name |Type |Required |Description |
|---|---|---|---|
|input_limit |int |Yes |The number of candidates entering tensor rerank, value range: [1, 1000], default value: 100 |


<span id="instruction"></span>
### Instruction


|Parameter |Top\-level Parameter |Type |Required |Default Value |Description |
|---|---|---|---|---|---|
|instruction |*  |Map |No |*  |Instruction configuration<br><br>By setting instructions, the model is guided to more accurately focus on the key information of the input content to improve the accuracy of vector representation<br><br>If this field is not filled, it is equivalent to `AutoFill = true` |
|*  |auto_fill |Boolean |Yes |true |Automatically fills the instruction content<br><br>When writing data, the instruction content is automatically filled based on the modality information. If the model does not support the `instruction` parameter, no error is reported, but the setting has no effect. See the model list in the table below for the filling rules of each model. |


<span id="model-list"></span>
### Model List


|Model Name |Model Version |Supported Vectorization Types |Default Dense Vector Dimension |Optional Dense Vector Dimensions |Text Truncation Length |Sparse Vector Support |Tensor Support |Instruction Support |Supported Storage Instruction Auto\-fill Content |Supported Retrieval Instruction Auto\-fill Content |
|---|---|---|---|---|---|---|---|---|---|---|
|bge\-large\-zh |(default) |text |1024 |1024 |512 |No |No |Yes |null |`Generate an embedding for this sentence for retrieving relevant articles:`<br><br>Prepended to the text |
|bge\-m3 |(default) |text |1024 |1024 |8192 |Yes |No |No |null |null |
|bge\-visualized\-m3 |(default) |text, image and their combinations |1024 |1024 |8192 |No |No |No |null |null |
|Skylark\-embedding |240715 |text |2048 |512, 1024, 2048 |4096 |No |No |Yes |null |`Generate an embedding for this sentence for retrieving relevant articles:`<br><br>Prepended to the text |
|Skylark\-embedding\-large |240915 |text |2048 |512, 1024, 2048, 4096 |4096 |No |No |Yes |null |`Generate an embedding for this sentence for retrieving relevant articles:`<br><br>Prepended to the text |
|Skylark\-embedding\-vision |250615 |Compatible with the usage of 241215. In addition, supports full_modal_seq (text/image/video sequence) |2048 |2048, 1024 |128k |No |No |Yes |null |`According to this question, find the corresponding text or image that can answer the question:`<br><br>Prepended to the text |
|Skylark\-embedding\-vision |251215 |Compatible with the usage of 241215, supports full_modal_seq (text/image/video sequence). Additionally supports tensor |2048 |2048, 1024 |128k |Yes |Yes |Yes |`Instruction:Compress the {} into one word. Query:`<br><br>The placeholder is automatically filled according to the dataset modality information (such as text; text and image; or text, image, and video) |`Target_modality: {}. Instruction:According to this question, find the corresponding text or image that can answer the question Query:`<br><br>The placeholder is automatically filled according to the dataset modality information (such as text; text and image; or text, image, and video) |


<span id="request-response-example"></span>
# Request Response Example

<span id="_1-text-search"></span>
#### 1. Text Search

<span id="request-parameters"></span>
##### Request Parameters

```JSON

req_path = "/api/vikingdb/data/search/multi_modal"
req_body = {
    "collection_name": "test_coll_with_vectorize",
    "index_name": "idx_1",
    "text": "A vector is a quantity with a certain magnitude and direction in mathematics, unstructured data such as text, images, audio and video",
    "instruction": {
        "auto_fill": true
    },
    "output_fields": [
        "f_text"
    ],
    "limit": 2
}
```


<span id="response-parameters"></span>
##### Response Parameters

```JSON

{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "id": "uid_001",
                "fields": {
                    "f_text": "A vector is a quantity with a certain magnitude and direction in mathematics"
                },
                "score": 9.899999618530273,
                "ann_score": 9.899999618530273
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_text": "Vector is an important concept in high school mathematics"
                },
                "score": 8.324234999961,
                "ann_score": 8.324234999961
            }
        ],
        "total_return_count": 2,
        "real_text_query": "According to this question, find the corresponding text or image that can answer the question: A vector is a quantity with a certain magnitude and direction in mathematics, unstructured data such as text, images, audio and video",
        "token_usage": {
            "skylark-embedding-vision__251215": {
                "prompt_tokens":53,
                "completion_tokens":0,
                "image_tokens":0,
                "total_tokens":53
            }
        }
    }
}
```


<span id="_2-text-image-search"></span>
#### 2. Text + Image Search

<span id="request-parameters"></span>
##### Request Parameters

```JSON

req_path = "/api/vikingdb/data/search/multi_modal"
req_body = {
    "collection_name": "test_coll_with_vectorize",
    "index_name": "idx_1",
    "text": "A vector is a quantity with a certain magnitude and direction in mathematics, unstructured data such as text, images, audio and video",
    "image": "tos://my_bucket/vector_icon.jpg",
    "output_fields": [
        "f_text", "f_image"
    ],
    "instruction": {
        "auto_fill": true
    },
    "limit": 2
}
```


<span id="response-parameters"></span>
##### Response Parameters

```JSON

{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "id": "uid_001",
                "fields": {
                    "f_text": "A vector is a quantity with a certain magnitude and direction in mathematics", "f_image": "tos://my_bucket/vector_1.jpg"
                },
                "score": 9.899999618530273,
                "ann_score": 9.899999618530273
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_text": "Vector is an important concept in high school mathematics", "f_image": "tos://my_bucket/vector_2.jpg"
                },
                "score": 8.324234999961,
                "ann_score": 8.324234999961
            }
        ],
        "total_return_count": 2,
        "real_text_query": "According to this question, find the corresponding text or image that can answer the question: A vector is a quantity with a certain magnitude and direction in mathematics, unstructured data such as text, images, audio and video",
        "token_usage": {
            "skylark-embedding-vision__251215": {
                "prompt_tokens":53,
                "completion_tokens":0,
                "image_tokens":0,
                "total_tokens":53
            }
        }
    }
}
```


<span id="_3-video-search"></span>
#### 3. Video Search

Video tokens are counted as image_tokens.

<span id="request-parameters"></span>
##### Request Parameters

```SQL

req_path = "/api/vikingdb/data/search/multi_modal"
req_body = {
        "collection_name": "jiangyuan_video_collection",
        "index_name": "jiangyuan_video_index",
        "text": "cat",
        "video": 
            {   
                "value": "tos://data-import/2101858484/2025_08_19_10_51_40Oheg6Pua9jaD33cVl2GhcKyjumEM7aXy/cat_video.mp4",
                "fps": 1.0,
            },
        "output_fields": [
                "f_id", "f_video"
            ],
        "instruction": {
            "auto_fill": false
        },
        "limit": 2
 }
```


<span id="response-parameters"></span>
##### Response Parameters

```JSON

{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175574557162300000000000000000000ffff0a007af7628242",
    "result": {
        "data": [
            {
                "id": "4",
                "fields": {
                    "f_id": "4",
                    "f_video": {
                         "value": "tos://my_bucket/xxxx1.mp4",
                         "fps": 1.0,
                     }
                },
                "score": 0.9932262897491455,
                "ann_score": 0.9932262897491455
            },
            {
                "id": "1",
                "fields": {
                    "f_id": "1",
                    "f_video": {
                         "value": "tos://my_bucket/xxxx2.mp4",
                         "fps": 1.0,
                     }
                },
                "score": 0.41645175218582153,
                "ann_score": 0.41645175218582153
            }
        ],
        "total_return_count": 2,
        "real_text_query": "cat",
        "token_usage": {
            "Skylark-embedding-vision__250615": {
                "prompt_tokens": 18146,
                "completion_tokens": 0,
                "image_tokens": 17892,
                "total_tokens": 18146
            }
        }
    }
}
```


<span id="_4-image-text-search-with-rerank"></span>
#### 4. Image\-text Search with rerank

<span id="request-parameters"></span>
##### Request Parameters

```JSON


{
    "collection_name": "test_coll_with_vectorize",
    "index_name": "idx_1",
    "text": "A vector is a quantity with a certain magnitude and direction in mathematics, unstructured data such as text, images, audio and video",
    "image": "tos://my_bucket/vector_icon.jpg",
    "output_fields": [
        "f_text", "f_image"
    ],
    "instruction": {
        "auto_fill": true
    },
    "limit": 2,
    "rerank": {
        "model_name": "doubao-seed-rerank",
        "model_version": "251028",
        "instruction": "Whether the Document and Query represent duplicate questions"
    }
}
```


<span id="response-parameters"></span>
##### Response Parameters

```JSON

{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "id": "uid_001",
                "fields": {
                    "f_text": "A vector is a quantity with a certain magnitude and direction in mathematics", "f_image": "tos://my_bucket/vector_1.jpg"
                },
                "score": 0.51,
                "ann_score": 9.899999618530273
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_text": "Vector is an important concept in high school mathematics", "f_image": "tos://my_bucket/vector_2.jpg"
                },
                "score": 0.11,
                "ann_score": 8.324234999961
            }
        ],
        "total_return_count": 2,
        "real_text_query": "According to this question, find the corresponding text or image that can answer the question: A vector is a quantity with a certain magnitude and direction in mathematics, unstructured data such as text, images, audio and video",
        "token_usage": {
            "skylark-embedding-vision__251215": {
                "prompt_tokens":1335,
                "completion_tokens":0,
                "image_tokens":1231,
                "total_tokens":1335
            },
            "Skylark-seed-rerank__251028": {
                "prompt_tokens":1335,
                "completion_tokens":0,
                "image_tokens":1231,
                "total_tokens":1335
            }
        }
    }
}
```


<span id="_5-image-text-search-with-tensor-rerank"></span>
#### 5. Image\-text Search with tensor_rerank

<span id="request-parameters"></span>
##### Request Parameters

```JSON

{
    "collection_name": collection_name,
    "index_name": index_name,
    "limit": 3,
    "output_fields": ["id", "name", "dense_text_vector", "sparse_text_vector", "tensor_text_vector"],
    "text": "sky is very blue",
    "instruction": {
        "auto_fill": false
    },
    "tensor_rerank" : {
        "input_limit" : 50
    },
    "advance": {
        "dense_weight": 0.7
    }
}
```


<span id="response-parameters"></span>
##### Response Parameters

```JSON

req http status code:  200
req result: 
 {
  "code": "Success",
  "message": "The API call was executed successfully.",
  "request_id": "02176373667508300000000000000000000ffff0a00730abcf2fa",
  "result": {
    "data": [
      {
        "id": 85,
        "fields": {
          "dense_text_vector": "OUmJbeyyyplieGsPHTft",
          "id": 85,
          "name": "FxkdlaxJEe",
          "sparse_text_vector": "ImUZkmTZLxXVLJEwEIDr",
          "tensor_text_vector": "KIEdrgNtIjKmAPdgoNdS"
        },
        "score": 225083.109375,
        "ann_score": 0.18097847700119019
      },
      {
        "id": 40,
        "fields": {
          "dense_text_vector": "BvUISeyzoEBxduVUPfhO",
          "id": 40,
          "name": "hItTJqQtbJ",
          "sparse_text_vector": "NlNAvNyOJDXZFHiJLyeD",
          "tensor_text_vector": "IIVuNrxYInoebjVGTLCf"
        },
        "score": 224653.296875,
        "ann_score": 0.18653953075408936
      },
      {
        "id": 90,
        "fields": {
          "dense_text_vector": "EGEoGsKBLexTzLXfcFAz",
          "id": 90,
          "name": "jLwxYLXUzv",
          "sparse_text_vector": "KAgXCPHqBQYyXUlpTKkk",
          "tensor_text_vector": "PggVnXHcaNucUPSWnSRy"
        },
        "score": 224428.125,
        "ann_score": 0.21451199054718018
      }
    ],
    "total_return_count": 3,
    "real_text_query": "sky is very blue",
    "token_usage": {
      "Skylark-embedding-vision__250615": {
        "prompt_tokens": 29,
        "completion_tokens": 0,
        "image_tokens": 0,
        "total_tokens": 29
      }
    }
  }
}
```


<span id="request-template"></span>
### Request Template

```Python

"""
pip3 install volcengine
"""

from volcengine.base.Request import Request
import requests, json


class ClientForDataApi:
    def __init__(self, api_key=None, host=None):
        """
        Initializes the ClientForDataApi class
        :param api_key: API Key of VikingDB
        :param host: API Host of VikingDB
        """
        if not api_key or not host:
            raise ValueError("api_key and host are required")
        self.api_key = api_key
        self.host = host

    def prepare_request(self, method, path, params=None, data=None):
        r = Request()
        r.set_shema("https")
        r.set_method(method)
        r.set_connection_timeout(10)
        r.set_socket_timeout(10)
        mheaders = {
            "Accept": "application/json",
            "Content-Type": "application/json",
            "Host": self.host,
            "Authorization": f"Bearer {self.api_key}",
        }
        r.set_headers(mheaders)
        if params:
            r.set_query(params)
        r.set_host(self.host)
        r.set_path(path)
        if data is not None:
            r.set_body(json.dumps(data))
        return r

    def do_req(self, req_method, req_path, req_params, req_body):
        req = self.prepare_request(
            method=req_method, path=req_path, params=req_params, data=req_body
        )
        return requests.request(
            method=req.method,
            url="http://{}{}".format(self.host, req.path),
            headers=req.headers,
            data=req.body,
            timeout=10000,
        )


if __name__ == "__main__":
    import os
    client = ClientForDataApi(
        api_key=os.environ.get("VIKINGDB_API_KEY", "***"), # Get API Key from environment variables, use default value if not set
        host="api-vikingdb.vikingdb.cn-beijing.volces.com",  # Replace with your domain name
    )
    req_method = "POST"
    req_params = None
    req_path = "/api/vikingdb/data/search/multi_modal"
    req_body = {
        "collection_name": "test_coll_with_vectorize",
        "index_name": "idx_1",
        "text": "A vector is a quantity with a certain magnitude and direction in mathematics, unstructured data such as text, images, audio and video",
        "instruction": {
            "auto_fill": true
        },
        "output_fields": [
            "f_text"
        ],
        "limit": 2
    }
    result = client.do_req(
        req_method=req_method, req_path=req_path, req_params=req_params, req_body=req_body
    )
    print("req http status code: ", result.status_code)
    print("req result: \n", result.text)
```
