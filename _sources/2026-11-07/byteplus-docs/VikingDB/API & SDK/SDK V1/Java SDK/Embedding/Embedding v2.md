---
title: "Embedding v2"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_Embedding_v2"
---

<span id="overview"></span>
## Overview

The embedding_v2 API allows you to convert unstructured data like text and images into feature vectors. This reference details the required request parameters, lists available models such as Skylark\-embedding and bge\-m3, and provides a Java code example to help you quickly integrate the vectorization capability into your applications.

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


The asynchronous call uses the async_embedding_v2 interface, and the parameters remain unchanged.


* The current Embedding service supports generating vectors of text/images.

* The current Embedding service interface does not support high\-concurrency requests. Requests will be discarded when the number of requests is too large.

* Image size: We recommend that image sizes do not exceed 1 MB. The total request size limit is 4 MB, so for images larger than 1 MB, we recommend compressing them and retrying the request to prevent it from being truncated.

* Image compression size recommendation: After our experiment, the length and width of the image are scaled to 0.3 times their original size, which can get a result similar to the original image embedding. This scaling ratio is the inflection point; if the ratio is lower, the accuracy deterioration will be more obvious. The scaling ratio can be above the inflection point.

* The current image embedding limit is 15 images uploaded per second. If it exceeds the limit, please contact customer service in time to request a quota increase.


<span id="request-parameters"></span>
## **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**explain** |
|---|---|---|---|---|
|EmbModel<br><br>EmbModel instance. |modelName |String |Yes |Specify the model name, the currently supported models are:<br><br><br>* Skylark\-embedding: A semantic vectorization model developed by ByteDance, which supports both Chinese and English, and has a maximum context length of 4K. Output dense vectors with the highest dimension of 2048, and support 512,1024 dimensionality reduction. If your TPM exceeds 5000, please use Model Ark.<br><br><br>Skylark\-embedding includes two versions, 240515 and 240715, which can be accessed using the `model_version` parameter.<br><br>The Chinese and English retrieval performance of the 240715 version is greatly improved compared with the 240515 version.<br><br><br>* Skylark\-embedding\-large: The latest upgrade of the ByteDance semantic vectorization model, using the more capable Doubao language model as its base, supports Chinese and English bilingualism, and the longest 4K context length. Output dense vectors with the highest dimension of 4096, support 2048, 1024, 512 dimensionality reduction. If your TPM exceeds 5000, please use Model Ark.<br><br>* Skylark\-embedding\-vision: Byte's self\-developed multimodal vectorization model, mainly for the use of multimodal vector retrieval, supports image input and Chinese and English bilingual text input, with a maximum context length of 8K. Output 3072\-dimensional dense vectors. If your TPM exceeds 5000, please use Model Ark.<br><br>* bge\-large\-zh: It can handle up to 512 tokens. Inputs that are too long will be truncated, and inputs that are too short will be padded. The output embedding dimension is 1024 and the type is float.<br><br>* bge\-m3: Based on the m3 model, dense vectors and sparse vectors are returned by default. It can handle up to 8192 tokens. Inputs that are too long will be truncated, and inputs that are too short will be padded. The output dense vector dimension is 1024, and the type is float. The output sparse vector is a dictionary type, k is the token output by Tokenizer, and v is the weight of this token.<br><br>* Bge\-large\-zh\-and\-m3: Based on the bge v1.5 and m3 models, using a mixed retrieval mode. Dense vectors are extracted by bge v1.5, and sparse vectors are extracted by bge m3. It can handle up to 512 tokens. Inputs that are too long will be truncated, and inputs that are too short will be padded. The output dense vector dimension is 1024 and the type is float. The output sparse vector is a dictionary type, k is the token output by the Tokenizer, and v is the weight of this token.<br><br>* Bge\-visualized\-m3: Based on the Visualized\-BGE and m3 models, you can encode text or images individually, or encode text and images in combination, and output a 1024\-dimensional dense vector. The text token is limited to 3702. Inputs that are too long will be truncated, and inputs that are too short will be padded. |
| |Params |Map |No |return_token_usage \- returns the number of tokens consumed by the request, disabled by default.<br><br>return_dense \- returns a dense vector, enabled by default.<br><br>return_sparse \- Returns a sparse vector. This is enabled by default for models that support it. Enabling this for unsupported models will cause an error.<br><br>embedding_dimension \- used for dimensionality reduction of vectorized results.<br><br>model_version \- Used to switch model versions. If there are multiple versions of the model, you can specify it, if you don't fill it in, the default version will be used. The current Skylark\-embedding model supports "240515" (default) and "240715" versions |
|RawData<br><br>RawData instances or lists, up to 100. |dataType |String |Yes |The following types are supported:<br><br><br>* Text: text<br><br>* Image: image<br><br>* Text\-image: joint encoding of a text\-image pair |
| |Text |String |data_type text or text\-image, required |When data_type = text, pass in text of type string directly. |
| |Image |String |data_type image or text\-image, required |data_type = image, pass in the base64 encoding of the image content |


<span id="example"></span>
## Example

<span id="request-parameters"></span>
### Request parameters

```Java
HashMap params = new HashMap<>();
params.put("return_token_usage", true);
ArrayList rawDatas = new ArrayList<>();
rawDatas.add(new RawData().setDataType("text").setText("hello1").build());
rawDatas.add(new RawData().setDataType("text").setText("hello2").build());
Map res = vikingDBService.embeddingV2(new EmbModel().setModelName("bge-m3").setParams(params).build(), rawDatas);
System.out.println(res);
```


<span id="return-value"></span>
### Return value

The Python call performs the above task, returning vectors of type listor list.
