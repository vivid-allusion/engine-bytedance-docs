---
title: "Embedding v2"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Embedding_v2"
---

<span id="embedding-v2-interface"></span>
## Embedding v2 interface

The embedding interface is upgraded to the v2 version, with a new long text window model and sparse vector output, and supports usage statistics. It is recommended to migrate to the v2 interface to use the embedding function.

The data/embedding/version/2 interface uses deep learning neural networks to extract the content and semantics of unstructured data (such as text, images, audio, and video) and convert it into feature vectors.

> When you use the embedding models to create vectorized data, your uploaded data may be transmitted to BytePlus servers in Malaysia for processing. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


* The current Embedding service supports generating vectors of text/images.

* The Embedding model has a call limit measured in Tokens Per Minute (TPM). The TPM for each account, which includes all its sub\-accounts combined, cannot exceed 120,000 per model.

* Image size: It is recommended that the image size should not exceed 1MB, because the request limit of embedding v2 interface is 4M. If an image exceeds 1 MB, we recommend compressing it and resubmitting the request to prevent the request payload from being truncated.

* Image compression size recommendation: Our experiments show that scaling the image's length and width to 30% of their original size can yield embedding results similar to the original image. A scaling factor of 0.3 is the inflection point. If the ratio is lower, the accuracy will degrade more significantly. The scaling ratio can be above the inflection point.

* The current image embedding limit is 15 images uploaded per second. If you exceed this limit, please contact customer service to request a limit increase.


<span id="request-interface"></span>
### **request interface**

When requesting the OpenAPI interface of the Embedding service, you need to construct a signature for authentication. For detailed OpenAPI signature invocation methods, please refer to [API Signature Call Guide](https://docs.byteplus.com/en/docs/VikingDB/Preparation).


|**URI** |/api/data/embedding/version/2 |Uniform Resource Identifier |
|---|---|---|
|**method** |POST/GET |The type of operation requested by the client side on the Embedding service |
|**request header** |Content\-Type: application/json |Request message type |
| |Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="request-parameters"></span>
### **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**optional value** |**explain** |
|---|---|---|---|---|---|
|Model |model_name |String |Yes |Bge\-large\-zh |The semantic vectorization model developed by ByteDance supports both Chinese and English. When the TPM exceeds 5000, please go to [Model Ark](https://www.byteplus.com/en/product/modelark) Use.<br><br><br>* **Output dense vector dimension: 2048, supports dimensionality reduction to 512 or 1024**<br><br>   \*\*\* Whether to return a sparse vector: No\*\*<br><br>   \*\*\* Supported Modes: text\*\*<br><br>   \*\*\* longest context length: 4K\*\*<br><br><br>**The model's billing rules can be viewed in** [vector library billing.](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database)<br><br>[Skylark-embedding includes two versions, 240515 and 240715, which can be accessed by setting the model_version parameter.](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database)<br><br>[The Chinese and English retrieval performance of the 240715 version is greatly improved compared to the 240515 version.](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database) |
| | | | |BGE\-M3 |* **Output dense vector dimension: 2048, supports dimensionality reduction to 512 or 1024**<br><br>   \*\*\* Whether to return a sparse vector: Yes\*\*<br><br>   \*\*\* Supported Modes: text\*\*<br><br>   \*\*\* longest context length: 4K\*\*<br><br><br>**The model's billing rules can be viewed in** [vector library billing.](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database) |
| | | | |bge\-large\-zh\-and\-m3 |The latest upgrade of ByteDance's semantic vectorization model, using a more capable bean bag language model as a base, supports both Chinese and English. When the TPM exceeds 5000, please go to [model Ark](https://console.volcengine.com/ark/region:ark+cn-beijing/model/detail?Id=Skylark-embedding) Use<br><br><br>* **Output dense vector dimension: 4096, supports dimensionality reduction to 2048, 1024, or 512**<br><br>   \*\*\* Whether to return a sparse vector: No\*\*<br><br>   \*\*\* Supported Modes: Text\*\*<br><br>   \*\*\* longest context length: 4K\*\*<br><br><br>**The model's billing rules can be viewed in** [vector library billing.](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_a_vector_database) |
| | | | |bge\-visualized\-m3 |* **Output dense vector dimension: 4096, supports dimensionality reduction to 2048, 1024, or 512**<br><br>   \*\*\* Whether to return a sparse vector: Yes\*\*<br><br>   \*\*\* Supported Modes: text\*\*<br><br>   \*\*\* longest context length: 4K\*\*<br><br><br>**The billing rules of the model can be viewed at**[vector library billing](https://www.volcengine.com/docs/84313/1414459)**View** |
| |Params |Map |No |return_token_usage |Returns the number of tokens consumed by the request, disabled by default. |
| | | | |return_dense |Returns a dense vector, enabled by default. |
| | | | |return_sparse |Returns a sparse vector. This is enabled by default for models that support sparse vector extraction. Enabling this for other models will cause an error. |
| | | | |embedding_dimension |Used for dimensionality reduction of vectorization results. |
| | | | |model_version |Used to switch model versions. If there are multiple versions of the model, you can specify it. If you don't fill it in, the default version will be used. The current Skylark\-embedding model supports "240515" (default) and "240715" versions. |
|Data<br><br>Maximum 100. |data_type |String |Yes |Text |Text |
| | | | |Image |Picture |
| | | | |Text\-image |Text\-image pair joint encoding |
| |Text |String |Required if data_type is text or text\-image. |data_type = text, directly pass in the text string |*  |
| |Image |String |Required if data_type is image or text\-image. |If data_type is image, pass the base64\-encoded image content. |*  |


<span id="response-message"></span>
### Response message


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Message |
|request_id |A unique identifier for each request |
|Data |Dictionary type, now contains<br><br>{<br><br>"sentence_dense_embedding": [<br><br>[0.23, 0.54, 0.76],<br><br>...<br><br>],<br><br>"sentence_sparse_embedding": [<br><br>{'De': 0.05005, 'fin': 0.1368, 'ation': 0.04498, 'of': 0.0633, 'BM': 0.2515, '25': 0.3335},<br><br>...<br><br>],<br><br>"token_usage": {<br><br>"prompt_tokens": 8,<br><br>"completion_tokens": 0,<br><br>"total_tokens": 8//Number of tokens consumed<br><br>}<br><br>}<br><br>sentence_dense_embedding is a two\-dimensional vector with a shape of [batch_size, embedding_size]<br><br>The value of sentence_sparse_embedding is a list, the shape is [batch_size], and the elements in the list are dictionaries {"token": value}<br><br>Dense and sparse vectors with consistent subscripts correspond to the same text<br><br>token_usage: The number of tokens consumed by the request. |


<span id="status-code-description"></span>
### **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |The Embedding service was successfully requested. |
|1000003 |400 |Invalid request:% s |Invalid parameter:<br><br><br>* Missing required parameters, such as model_name.<br><br>* The field value does not match the field type. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000025 |404 |Failed to calcTextEmbedding |Request to the model service failed:<br><br><br>* The model name is incorrect.<br><br>* The input type does not correspond to the model. |


<span id="complete-example"></span>
## Complete example

<span id="embedding-v2-request-message"></span>
### Embedding v2 request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/data/embedding/version/2 \
  -d '{
        "model": {
                "model_name": "bge-large-zh-and-m3",
                "params":{
                    "return_dense":true,
                    "return_sparse":true,
                    "return_token_usage":true,
                }
        },
        "data": [
                {
                        "data_type": "text",
                        "text": "How to deploy models using torchserve"
                },
                {
                        "data_type": "text",
                        "text": "How to train machine learning models"
                }
        ]
}'
```


<span id="embedding-v2-response-message"></span>
### Embedding v2 response message

Example of a successful response:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
        "code": 0,
        "data": {
                "sentence_dense_embedding": [[0.005996500349661112, 0.01326021542580391, -0.00757963274399552, -0.022116572232986055, ...], [0.013724524677071628, 0.013717792739791143, 0.005816815453880527, -0.014414478409530515, ...]],
                "sentence_sparse_embedding": [{
                        "ch": 0.13818359375,
                        "serve": 0.3193359375,
                        "tor": 0.1937255859375,
                        "how": 0.1217041015625,
                        "to": 0.1177978515625,
                        "model": 0.258544921875,
                        "deploy": 0.2318115234375
                },
                {
                        "use": 0.168212890625,
                        "learn": 0.1473388671875,
                        "how": 0.1380615234375,
                        "machine": 0.1451416015625,
                        "model": 0.2425537109375,
                        "train": 0.275390625
                }],
                "token_usage": {
                        "prompt_tokens": 32,
                        "completion_tokens": 0,
                        "image_tokens": 0,
                        "total_tokens": 32
                }
        },
        "message": "success",
        "request_id": "02174159237407500000000000000000000ffff0a005875459994"
}
```


Example of a failed response:

```Shell
HTTP/1.1 404 OK
Content-Length: 43
Content-Type: application/json
 
{"message":"failed to calcTextEmbedding, ModelNotFoundException: Model not found: bge-large-zh","code":1000025, "request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```
