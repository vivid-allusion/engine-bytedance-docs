---
title: "Embedding v2"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_Embedding_v2"
---

<span id="overview"></span>
## Overview

To convert unstructured data like text and images into feature vectors, you can use the embedding_v2 interface. This API reference provides detailed descriptions of all request parameters, supported models, and includes a Go code example to help you get started quickly.

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


The asynchronous call uses the async_embedding_v2 interface, and the parameters remain unchanged.


* The current Embedding service supports generating vectors of text/images.

* The current Embedding service interface does not support high\-concurrency requests. Requests will be discarded when the number of requests is too large.

* Image size: It is recommended that the image size should not exceed 1MB, because the request limit of embedding v2 interface is 4M. When the image exceeds 1MB, we recommend that users compress the image and request again to prevent the request from being truncated;

* Image compression size recommendation: Our experiments show that scaling an image's dimensions by a factor of 0.3 produces embedding results similar to those of the original image. This 0.3 factor is an inflection point; scaling by a lower ratio causes a more significant drop in accuracy. The scaling ratio should be kept at or above this point.

* The current image embedding limit is 15 images uploaded per second. If it exceeds the limit, please contact customer service to request a limit increase.


<span id="request-parameters"></span>
## **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**Description** |
|---|---|---|---|---|
|EmbModel<br><br>EmbModel structure instance. |ModelName |String |Yes |Specify the model name, the currently supported models are:<br><br><br>* bge\-large\-zh: It can handle up to 512 tokens. It will be truncated when the number is too long, and padding will be done when the number is insufficient. The output embedding dimension is 1024 and the type is float.<br><br>* bge\-m3: Based on the m3 model, dense vectors and sparse vectors are returned by default. It can handle up to 8192 tokens. When the number is too long, it will be truncated, and when the number is insufficient, it will be padded. The output dense vector dimension is 1024, and the type is float. The output sparse vector is a dictionary type, k is the token output by Tokenizer, and v is the weight of this token.<br><br>* Bge\-large\-zh\-and\-m3: Based on the bge v1.5 and m3 models, using a mixed retrieval mode. Dense vectors are extracted by bge v1.5, and sparse vectors are extracted by bge m3. It can handle up to 512 tokens. It will be truncated when the number is too long, and will be padded when the number is insufficient. The output dense vector dimension is 1024 and the type is float. The output sparse vector is a dictionary type, k is the token output by the Tokenizer, and v is the weight of this token.<br><br>* Bge\-visualized\-m3: Based on the Visualized\-BGE and m3 models, you can encode text or pictures individually, or encode text and pictures in combination, and output a 1024\-dimensional dense vector. The text token is limited to 3702. It will be truncated when the number is too long, and will be padded when the number is insufficient. |
| |Params |Map |No |return_token_usage \- Returns the number of tokens consumed by the request, Disabled by default.<br><br>return_dense \- returns a dense vector, Enabled by default.<br><br>return_sparse \- Returns a sparse vector. This is enabled by default for models that support sparse vector extraction; enabling it for other models will cause an error.<br><br>embedding_dimension \- used for dimensionality reduction of vectorized results.<br><br>model_version \- Used to switch model versions. If there are multiple versions of the model, you can specify it. If not specified, the default version is used. The current Skylark\-embedding model supports "240515" (default) and "240715" versions |
|RawData<br><br>List of RawData structure instances or their components, up to 100. |DataType |String |Yes |The following types are supported:<br><br><br>* Text: text<br><br>* Image: image<br><br>* Text\-image: joint encoding of a text\-image pair |
| |Text |String |Required if data_type is 'text' or 'text\-image'. |When data_type = text, pass the text directly as a string. |
| |Image |String |Required if data_type is 'image' or 'text\-image'. |If data_type is 'image', pass the base64\-encoded image content. |


<span id="example"></span>
## Example

<span id="request-parameters"></span>
### Request parameters

```Go
list := []vikingdb.RawData{
    {
       DataType: "text",
       Text:     "hello1",
    },
    {
       DataType: "text",
       Text:     "hello2",
    },
}
res, err := service.EmbeddingV2(vikingdb.EmbModel{ModelName: "bge-m3", Params: map[string]interface{}{"return_token_usage": true}}, list)
if err != nil {
    fmt.Println(err)
}
for key, item := range res {
    fmt.Println(key,item)
    fmt.Println("------------------------------")
}
```


<span id="return-value"></span>
### Return value

The Go call performs the above task and returns the result as a JSON object, including both dense and sparse vectors (if any).
