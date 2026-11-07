---
title: "Embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_Embedding1"
---

<span id="8dd39241"></span>
## Overview

To convert unstructured text data into numerical feature vectors, you can use the Embedding API. This reference provides the necessary parameters and a Go code example to call the service. The service currently supports the 'bge\-large\-zh' model for text vectorization.

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The current Embedding service only supports generating text vectors.</div>


* <div data-tips="true" data-tips-type="tip">The current Embedding service interface does not support handling high concurrent requests. Requests will be discarded when the number of requests is too large.</div>



<span id="2980efff"></span>
## **Request Parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**Description** |
|---|---|---|---|---|
|EmbModel<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">EmbModel structure instance.</div><br> |ModelName |String |Yes |Specify the model name, the currently supported model is bge\-large\-zh.<br><br><br>* There is a limit to the number of tokens that different models can handle. Bge\-large\-zh can handle up to 512 tokens. If the number is too long, it will be truncated, and if the number is insufficient, it will be padded.<br><br>* The output embedding dimension is 1024 and the type is float. |
|RawData<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">List of RawData structure instances or their components, up to 100.</div><br> |DataType |String |Yes |Specifies the data type. Currently, only text is supported. |
||Text |String |Yes |When DataType = text, pass in text of type string directly. |


<span id="7d506363"></span>
## Example

<span id="1b9db38c"></span>
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
res, err := service.Embedding(vikingdb.EmbModel{ModelName: "bge_large_zh"}, list)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
    fmt.Println("------------------------------")
}
```


<span id="3498e7dd"></span>
### Return value

This Go code returns a vector of type [][]float64.
