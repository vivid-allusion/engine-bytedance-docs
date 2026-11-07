---
title: "Embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_Embedding"
---

<span id="74cfa176"></span>
## Overview

The embedding API converts unstructured text data into feature vectors. This document provides details on the synchronous `embedding` and asynchronous `async_embedding` interfaces, including required parameters and code examples. Please note that the service currently supports only text vectorization and is not designed for high\-concurrency requests.

The asynchronous call uses the async_embedding interface, and the parameters remain unchanged.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The current Embedding service only supports generating text vectors.</div>


* <div data-tips="true" data-tips-type="tip">The current Embedding service interface does not support high\-concurrency requests. Requests will be discarded when the number of requests is too large.</div>



<span id="8fbc9fa1"></span>
## **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**Description** |
|---|---|---|---|---|
|emb_model<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">EmbModel instance.</div><br> |model_name |String |Yes |Specify the model name, the currently supported models are bge\-large\-zh.<br><br><br>* There is a limit to the number of tokens that different models can handle. Bge\-large\-zh can handle up to 512 tokens. If the number is too long, it will be truncated, and if the number is insufficient, it will be padded.<br><br>* For bge\-large\-zh, the output embedding dimension is 1024 and the type is float. |
|raw_data<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A list of up to 100 RawData instances.</div><br> |data_type |String |Yes |Specifies the data type, currently only text is supported. |
||Text |String |Yes |When data_type = text, pass in text of type string directly. |


<span id="512e9a5a"></span>
## Example

<span id="b9f5c09a"></span>
### Request parameters

```Python
list = [RawData("text","hello1"), RawData("text","hello2")]
res = vikingdb_service.embedding(EmbModel("bge-large-zh"), list)

# Asynchronous call
async def embedding():
    list = [RawData("text", "hello1"), RawData("text", "hello2")]
    res = await vikingdb_service.async_embedding(EmbModel("bge_large_zh"), list)
    print(res)
asyncio.run(embedding())
```


<span id="b5b70a5a"></span>
### Return value

The Python call returns a list of vectors with the type list<list\>.
