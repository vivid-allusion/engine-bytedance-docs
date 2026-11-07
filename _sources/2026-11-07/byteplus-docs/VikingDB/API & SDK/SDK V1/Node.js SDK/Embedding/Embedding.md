---
title: "Embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_Embedding"
---

To convert unstructured data like text and images into feature vectors, you can use the Embedding API. This reference provides the complete request and response parameters, data models, and a code example to guide your implementation.

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The Embedding service currently supports generating vectors for text and images.</div>


* <div data-tips="true" data-tips-type="tip">The Embedding service interface does not support a high volume of concurrent requests. Requests will be discarded when the number of requests is too large.</div>


* <div data-tips="true" data-tips-type="tip">If an image exceeds 1 MB, we recommend compressing it and submitting the request again to prevent the request payload from being truncated.</div>


* <div data-tips="true" data-tips-type="tip">Our experiments show that scaling an image's length and width to 30% of the original size produces embedding results comparable to those from the uncompressed image. This 30% scale factor is an inflection point; scaling below this ratio causes a more significant drop in accuracy. For best results, use a scaling ratio at or above 30%.</div>



<span id="2e56e84f"></span>
# Request parameters

`Embedding` There are two parameters, namely `ModelParams` and `DataParams[]`.

<span id="11b5bc78"></span>
## ModelParams


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|ModelName |`ModelName` |Yes |Use the model name |
|ReturnTokenUsage |`boolean` |No |Specifies whether to return the number of consumed tokens. |
|ReturnDense |`boolean` |No |Specifies whether to return a dense vector. |
|ReturnSparse |`boolean` |No |Specifies whether to return a sparse vector. |


<span id="1e5a8c81"></span>
### ModelName

```TypeScript
type ModelName = "bge-large-zh" | "bge-m3" | "bge-large-zh-and-m3" | "bge-visualized-m3"
```


<span id="9bf73c71"></span>
## DataParams

```TypeScript
type DataParams = TextDataParams | ImageDataParams | TextImageDataParams

enum DataType {
  Text = "text",
  Image = "image",
  TextImage = "text-image",
}
```


```TypeScript
type DataParams = TextDataParams | ImageDataParams | TextImageDataParams

enum DataType {
  Text = "text",
  Image = "image",
  TextImage = "text-image",
}
```


<span id="216c2d6f"></span>
### TextDataParams


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|DataType |`DataType.Text` |Yes |Data type |
|Text |`string` |Yes |Text data |


<span id="99cbd5f8"></span>
### ImageDataParams


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|DataType |`DataType.Image` |Yes |Data type |
|Image |`string` |Yes |Image base64 encoding |


<span id="88acd6ab"></span>
### TextImageDataParams


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|DataType |`DataType.TextImage` |Yes |Data type |
|Image |`string` |Yes |Image base64 encoding |
|Text |`string` |Yes |Text data |


<span id="cac771fc"></span>
# response parameters

```TypeScript
declare class EmbeddingResponse {
  readonly Result: EmbeddingResult[];
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    Result: EmbeddingResult[],
    OriginalRequest: string,
    LogId: string
  );
}
```


<span id="434f3a91"></span>
## EmbeddingResult

The returned fields depend on the provided ModelParams.


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|SentenceDenseEmbedding |`number[][]` |No |Dense vector |
|SentenceSparseEmbedding |`Record[]` |No |Sparse vector |
|TokenUsage |`TokenUsage` |No |Resource usage |


<span id="03c39060"></span>
### TokenUsage


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|PromptTokens |`number` |Yes |*  |
|CompletionTokens |`number` |Yes |*  |
|TotalTokens |`number` |Yes |*  |


<span id="095a3210"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

const response await service.embedding.Embedding({ 
  ModelName: 'bge-large-zh', 
  ReturnTokenUsage: true, // Optional. If you set this parameter to true, token usage is returned. 
  ReturnDense: true, // Optional. If you set this parameter to true, dense vectors are returned. 
  ReturnSparse: true, // Optional. If you set this parameter to true, sparse vectors are returned. 
}) 

console.log(response.Result) // Get the embedding result.
```
