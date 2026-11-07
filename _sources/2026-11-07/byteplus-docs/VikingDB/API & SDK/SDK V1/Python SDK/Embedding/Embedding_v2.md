---
title: "Embedding_v2"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_Embedding_v2"
---

<span id="overview"></span>
## Overview

The `embedding_v2` API converts unstructured data, such as text and images, into feature vectors. This document serves as a comprehensive API reference, providing the required request parameters, details on supported models like `bge-m3`, and Python code examples for both synchronous (`embedding_v2`) and asynchronous (`async_embedding_v2`) calls to facilitate your integration.

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


* The current Embedding service supports generating vectors for text and images.

* The current Embedding service interface does not support handling high\-concurrency requests. Requests will be discarded when the number of requests is too large.

* Image size: It is recommended that the image size should not exceed 1MB, because the request limit of embedding v2 interface is 4M. When the image exceeds 1MB, we recommend that users compress the image and request again to prevent the request from being truncated;

* Image compression size recommendation: After our experiment, the length and width of the image are scaled to 30% of their original size, which can get a result similar to the original image embedding. This 30% scaling factor is an inflection point. If the ratio is lower, the accuracy deterioration will be more obvious. The scaling ratio can be above the inflection point.

* The current image embedding limit is 15 images uploaded per second. If it exceeds the limit, please contact customer service in time to request a rate limit increase.


<span id="request-parameters"></span>
## **Request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**Description** |
|---|---|---|---|---|
|emb_model |model_name |String |Yes |Specify the model name, the currently supported models are:<br><br><br>* bge\-large\-zh: It can handle up to 512 tokens. It will be truncated when the number is too long, and padding will be done when the number is insufficient. The output embedding dimension is 1024 and the type is float.<br><br>* bge\-m3: Based on the m3 model, dense vectors and sparse vectors are returned by default. It can handle up to 8192 tokens. When the number is too long, it will be truncated, and when the number is insufficient, it will be padded. The output density vector dimension is 1024, and the type is float. The output sparse vector is a dictionary type, the key (k) is the token from the Tokenizer, and the value (v) is the token's weight.<br><br>* Bge\-large\-zh\-and\-m3: Based on the bge v1.5 and m3 models, using a mixed retrieval mode. Dense vectors are extracted by bge v1.5, and sparse vectors are extracted by bge m3. It can handle up to 512 tokens. It will be truncated when the number is too long, and will be padded when the number is insufficient. The output density vector dimension is 1024 and the type is float. The output sparse vector is a dictionary type, the key (k) is the token from the Tokenizer, and the value (v) is the token's weight.<br><br>* Bge\-visualized\-m3: Based on the Visualized\-BGE and m3 models, you can encode text or pictures individually, or encode text and pictures in combination, and output a 1024\-dimensional dense vector. The text token is limited to 3702. It will be truncated when the number is too long, and will be padded when the number is insufficient. |
| |Params |Map |No |return_token_usage \- Returns the number of tokens consumed by the request, Disabled by default.<br><br>return_dense \- returns a dense vector, Enabled by default.<br><br>return_sparse \- Returns a sparse vector. This is enabled by default for models that support sparse vectors. Enabling this option for models that do not support it will cause an error.<br><br>embedding_dimension \- Used for dimensionality reduction of vectorized results.<br><br>model_version \- Used to switch model versions. If there are multiple versions of the model, you can specify it, If not specified, the default version will be used. The current Skylark\-embedding model supports "240515" (default) and "240715" versions |
|raw_data<br><br>RawData instances or lists, up to 100. |data_type |String |Yes |The following types are supported:<br><br><br>* Text: Text<br><br>* Image: Image<br><br>* Text\-image: Joint encoding of a text\-image pair |
| |Text |String |Required if `data_type` is `text` or `text-image` |When `data_type` is `text`, pass the text directly as a string. |
| |Image |String |Required if `data_type` is `image` or `text-image` |When `data_type` is `image`, pass the base64\-encoded image content |


<span id="example"></span>
## Example

<span id="request-parameters"></span>
### Request parameters

```Python
list = [RawData("text", "hello1"), RawData("text", "hello2")]
res = vikingdb_service.embedding_v2(EmbModel("bge-m3", params={"return_token_usage": True}), list)
print(res)

async def embedding_v2():
    list = [RawData("text", "hello1"), RawData("text", "hello2")]
    res = await vikingdb_service.async_embedding_v2(EmbModel("bge-m3"), list)
    print(res)
asyncio.run(embedding_v2())
```


<span id="return-value"></span>
### Return value

The example Python call returns vectors of type list< float \>, list< list< float \> \>.
