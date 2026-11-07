---
title: "Embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_Embedding"
---

<span id="c2ef854e"></span>
## Overview

The Embedding API allows you to convert unstructured text data into a numerical vector representation. This document provides the necessary parameters, such as `modelName` and `RawData`, and a code example to help you call the service. By using this API, you can obtain high\-dimensional feature vectors from your text, which are essential for downstream tasks like semantic search and text analysis. Please note that the current service only supports text input.

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The current Embedding service only supports generating text vectors.</div>


* <div data-tips="true" data-tips-type="tip">The current Embedding service interface does not support high\-concurrency requests. Requests will be discarded when the number of requests is too large.</div>



<span id="e53ddc77"></span>
## **Request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required?**  |**Description** |
|---|---|---|---|---|
|EmbModel<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">EmbModel instance.</div><br> |modelName |String |Yes |Specify the model name, the only currently supported model is bge\-large\-zh.<br><br><br>* There is a limit to the number of tokens that different models can handle. Bge\-large\-zh can handle up to 512 tokens. Inputs exceeding this token limit are truncated, while shorter inputs are padded.<br><br>* The output embedding dimension is 1024 and the type is float. |
|RawData<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A RawData instance or a list of up to 100 instances.</div><br> |dataType |String |Yes |Specifies the data type, currently only text is supported. |
||Text |String |Yes |When dataType = text, Pass the text directly as a string. |


<span id="9e244efc"></span>
## Example

<span id="95ea4c8e"></span>
### Request parameters

```Java
List res = vikingDBService.embedding(new EmbModel().setModelName("bge-large-zh").build(), new RawData().setDataType("text").setText("hello1").build());
```


<span id="6c433601"></span>
### Return value

The Java call performs the above task, returning vectors of type list, list<list\>.
