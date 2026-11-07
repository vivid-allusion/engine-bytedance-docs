---
title: "Embedding"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Embedding1"
---

<span id="42fa5f46"></span>
## Embedding interface

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The embedding interface is upgraded to the v2 version, with a new long text window model and sparse vector output, and supports usage statistics. It is recommended to migrate to the v2 interface to use the embedding function.</div>


To convert unstructured text data into feature vectors, you can use the `/api/data/embedding` endpoint. This API leverages deep learning neural networks to extract the content and semantics of your text, representing it as a numerical vector. Note that the v2 interface is now available with enhanced features and is the recommended version for all embedding tasks.

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The current Embedding service only supports generating text vectors.</div>


* <div data-tips="true" data-tips-type="tip">Currently, the call limit of TPM (Tokens Per Minute, the number of tokens per minute) is set for the Embedding model, and the TPM of each account (including all sub\-accounts under the main account, combined calculation) does not exceed 120,000/model.</div>



<span id="2a189472"></span>
### **Request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the Embedding service, you need to construct a signature for authentication. For detailed OpenAPI signature invocation methods, please refer to <a href="https://www.volcengine.com/docs/84313/1392480">API Signature Call Guide</a>.</div>



|**URI** |/api/data/embedding |Uniform Resource Identifier |
|---|---|---|
|**method** |POST/GET |The type of operation requested by the client on the Embedding service |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="0e73971c"></span>
### **Request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**Description** |
|---|---|---|---|---|
|Model |model_name |String |Yes |Specify the model name, the currently supported models are bge\-large\-zh.<br><br><br>* bge\-large\-zh: It can handle up to 512 tokens. Inputs longer than 512 tokens are truncated, and shorter inputs are padded. The output embedding dimension is 1024 and the type is float. |
|Data<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Maximum 100 objects.</div><br> |data_type |String |Yes |Specifies the data type, currently only text is supported. |
||Text |String |Yes |If data_type is text, provide the text directly as a string. |


<span id="4754eb39"></span>
### Response message


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique identifier for each request |
|Data |Embedding result. |


<span id="cdbfae5c"></span>
### **Status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |The Embedding service was successfully requested. |
|1000003 |400 |Invalid request:% s |Illegal parameter:<br><br><br>* Missing required parameters, such as model_name.<br><br>* The field value does not match the field type. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000025 |404 |Failed to calcTextEmbedding |Request for model service failed:<br><br><br>* The model name is incorrect.<br><br>* The input type does not correspond to the model. |


<span id="2e63dc2d"></span>
## Complete example

<span id="90eae9b2"></span>
### Embedding request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/data/embedding \
  -d '{
        "model": {
                "model_name": "bge-large-zh"
        },
        "data": [
                {
                        "data_type": "text",
                        "text": "How to deploy a model using torchserve"
                },
                {
                        "data_type": "text",
                        "text": "How to train a machine learning model"
                }
        ]
}'
```


<span id="6ab252d1"></span>
### Embedding response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "request_id":"021695029736548fd001de66666000000000000000000029aa917",
    "data": [ // The output is a 2D array, [batch_size, model_output_dimension]
        [
            0.014988808892667294,
            -0.025562003254890442,
            -0.039532456547021866,
            ...
        ],
        ...
    ]
}
```


On failure, the following is returned:

```Shell
HTTP/1.1 404 OK
Content-Length: 43
Content-Type: application/json
 
{"message":"failed to calcTextEmbedding, ModelNotFoundException: Model not found: bge-large-zh","code":1000025, "request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```
