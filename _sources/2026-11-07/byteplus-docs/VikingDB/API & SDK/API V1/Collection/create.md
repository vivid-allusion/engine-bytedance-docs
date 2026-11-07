---
title: "create"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/create"
---

<span id="99db8b05"></span>
# Overview

/collection/create interface is used to create a new dataset Collection. After successful creation, data can be written.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each Collection must specify a primary key field. When adding a field of type <code>vector</code> to the <code>fields</code> definition, you cannot select the vector type for subsequent new fields. Because only one vector field is supported, multiple vector fields cannot be added.</div>


* <div data-tips="true" data-tips-type="tip">It is recommended to vectorize image and text data through the vectorize parameter. If you use a pipeline for text vectorization, you must also provide the <code>pipeline_name</code> sub\-parameter.</div>


* <div data-tips="true" data-tips-type="tip">When adding a text field with a <code>pipeline_name</code>, you cannot add <code>vector</code> or <code>sparse_vector</code> fields, and only one such text field is allowed. When adding a text field without a <code>pipeline_name</code>, you can add <code>vector</code> and <code>sparse_vector</code> fields, as well as multiple text fields (up to the 200\-field limit).</div>



<span id="544c4d82"></span>
# **Request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/collection/create |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="0eefd1b9"></span>
# **Request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name |\-\- |String |Yes |\-\- |Specifies the name of the Collection created.<br><br><br>* Must begin with an English letter and can only contain English letters, numbers, and underscores (_). Cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|collection_aliases |\-\- |Array |No |\-\- |Alias for the custom dataset.<br><br><br>* Multiple aliases can be set, and each alias is entered for confirmation.<br><br>* The same dataset alias cannot be repeated.<br><br>* If an alias is already mapped to another dataset, setting it here remaps it to the current dataset.<br><br>* Only use English letters, numbers, underscores _ and start with English letters.<br><br>* Length requirements: [1,128]. |
|Description |\-\- |String |No |" |Description of Custom Collection.<br><br><br>* Length requirement: [0,65535]. |
|primary_key |\-\- |String |Yes |\-\- |* The primary key uniquely identifies a row of data. For a custom primary key, you can select an existing field of type `int64` or `string` from the `fields` list.<br><br>* For automatic primary key generation, set this parameter to `__AUTO_ID__`. The system will then automatically generate an `int64` value for the primary key. |
|Fields<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum number of fields in a Collection is 200.</div><br> |field_name |String |Yes |\-\- |Specify the name of the custom field.<br><br><br>* Only English letters, numbers, underscores _, and begin with English letters, cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Field names cannot be repeated. |
| |field_type |String |Yes |\-\- |Specify a custom field type, see optional values for details **field_type optional values**Explanation. |
| |default_val |Consistent with field_type |No |\-\- |Specify the default value of the custom field, see the default value for details **field_type optional values**Explanation.<br><br><br>* When `field_name` is the primary key, `default_val` has no effect and is not validated. |
| |dim |Int |Required when field_type is a vector |\-\- |Specify a custom field vector dimension.<br><br><br>* Value range: [4, 4096], and must be a multiple of 4.<br><br>* Vector dimension refers to the number of elements contained in a vector. |
|Vectorize |Dense |Map |No (fill in<br><br>Required when vectorizing) |\-\- |Vectorization parameters of dense vectors. See below for sub\-parameters\*\*"Vectorized parameter"\*\*Table. |
||Sparse |Map |No |\-\- |The vectorization parameter of the sparse vector. If you don't need a sparse vector, you don't have to fill it in. See below for sub\-parameters\*\*"Vectorized parameter"\*\*Table. |


<span id="77f49e0e"></span>
## field_type optional value


|**field type** |**Available index types** |**Default value** |**When data is written**<br><br>**value range** |**default_val**<br><br>**value range** |**Can be the primary key** |**Description** |
|---|---|---|---|---|---|---|
|int64 |Range |0 |Int64 range |Int64 range |Yes |Integer |
|Float32 |Range |0.0 |Float32 range |Float32 range |No |Floating\-point number |
|String |Enumeration |"Default" |\-\- |Length < = 128 |Yes |String |
|Bool |Enumeration |False |True/false |True/false |No |Boolean type |
|list |Enumeration |["Default"] |List length < = 32 |List length < = 32 |No |String array |
|list |Enumeration |[0] |List length < = 32 |List length < = 32 |No |Integer array |
|Vector |Vector |\-\- |Dimension 4\-2048 |\-\- |No |Dense vector.<br><br><br>* When `field_type` is set to `vector`, the `dim` parameter is required for that field. |
|sparse_vector |Sparse vector |\-\- |Non\-zero subscript Unlimited<br><br>Non\-zero values are in the float32 range |\-\- |No |Sparse vector.<br><br><br>* sparse_vector cannot be set separately, it must be set in combination with the vector field.<br><br>* Accepts a JSON object where keys are strings representing keywords and values are their corresponding float32 weights.<br><br>> Example:<br><br>> sparse_vector = |
|Text |\-\- |\-\- |\-\- |\-\- |No |Text, which can be vectorized |
|Image |\-\- |\-\- |\-\- |\-\- |No |* Currently, writing to the tos path is supported. The format is:`tos://{bucket}/{object_key}`.<br><br>* Image, can be used for vectorization. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If <code>field_type</code> is set to <code>text</code> or <code>image</code>, the <code>pipeline_name</code> parameter is optional.</div>


* <div data-tips="true" data-tips-type="warning">When the definition field fields adds a text field with pipeline_name, it is not allowed to add vector fields or sparse_vector fields, there is a text field with pipeline_name can only have one; when the definition field fields adds a text field without pipeline_name, it is allowed to add vector and sparse_vector fields, and allow to add multiple text fields without pipeline_name, up to 200 fields.</div>



<span id="e6fe6bd9"></span>
### Vectorization parameter


|Parameter name |Type |Required |Default value |Note |
|---|---|---|---|---|
|text_field |String |No |/ |Text field to be vectorized |
|image_field |String |No |/ |Image field to be vectorized |
|model_name |String |Yes |/ |The name of the model. This must correspond to a model name in the "Model list" table below. |
|model_version |String |No |/ |Model version. If there are multiple versions of a model, you can specify a specific version. If the default version of the model is used or the model does not have multiple versions, this field is not required. |
|Dimming |Int |No |/ |If you need to generate dense vectors, specify the vector dimension; otherwise, the model's default dimension is used. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">text_field and image_field settings need to correspond to model selection. For example, if <code>model_name</code> is a plain text embedding model, the <code>image_field</code> parameter is not allowed.</div>


<span id="06f12f88"></span>
### Model list

> In utilizing the embedding models for the creation of vectorized data, it may be necessary for your uploaded data to be transmitted to BytePlus's servers located in Malaysia for processing purposes. Please be advised that BytePlus does not store your data, inclusive of any processed data, on our Malaysian servers.



|Model name |Supports vectorization type |Introduction |Default dense vector dimension |Optional dense vector dimension |Support for sparse vectors |Need instructions |Default version |Optional version |
|---|---|---|---|---|---|---|---|---|
|Bge\-large\-zh |Text |Only supports Chinese, outputs dense vectors of 1024 dimensions, suitable for short text |1024 |1024 |No |No | | |
|BGE\-M3 |Text |Supports over 100 languages with cross\-lingual vectorization capabilities. It can output dense and sparse vectors and is suitable for long\-text, multilingual use cases. |1024 |1024 |Yes |No | | |
|bge\-visualized\-m3 |Text, text_image, image |You can encode text or images individually, or encode text and images in combination to output a dense vector of 1024 dimensions |1024 |1024 |No |No | | |


<span id="23fd0783"></span>
# **Response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Message |
|request_id |A unique identifier for each request |


<span id="fa041922"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |Collection created successfully. |
|1000004 |400 |Collection exists |Collection already exists. |
|1000003 |400 |Invalid request:% s |Illegal parameter:<br><br><br>* Required parameters are missing.<br><br>* Collection naming does not conform to the specification.<br><br>* Field types and related field properties do not satisfy constraints. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="f611a279"></span>
# Complete example

<span id="95db3540"></span>
## Request message

For example, creating a Collection with dense vectors, sparse vector fields, and scalar fields:

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/create \
  -d '{
    "collection_name": "test_name",
    "description": "test dataset",
    "primary_key": "id",            
    "fields": [                               
        {
            "field_name": "id",       
            "field_type": "int64"
        },
        {
            "field_name": "text",                     
            "field_type": "string", 
            "default_val": ""
        },
        {
            "field_name": "vector_field",
            "field_type": "vector",      
            "dim": 768
        },
        {
            "field_name": "sparse_vector_field",
            "field_type": "sparse_vector"
        },
        {
            "field_name": "time",
            "field_type": "int64",       
            "default_val": 0
        },
        {
            "field_name": "author",
            "field_type": "string",      
            "default_val": "null"
        },
    ]
}'
```


Create a Collection with a text field as an example:

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/collection/create \
  -d '{
        "collection_name": "test_raw_data_collection",
        "description": "test_raw_data_collection",
        "primary_key": "id",  
        "fields": [{
                "field_name": "id",
                "field_type": "int64",
                "default_val": 0
        }, {
                "field_name": "gap",
                "field_type": "float32",
                "default_val": 3.1
        }, {
                "field_name": "content",
                "field_type": "text",
        }],
        "vectorize":[{
            "dense": {
                "text_field": "content", 
                "model_name": "bge-visualized-m3",
                "dim": 1024
            },
            "sparse": {
                "text_field": "content",
                "model_name": "bge_m3"
            }
        }]
    }'
```


<span id="ed9e24be"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


If execution fails, the response is:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000004,"message":"collection exist","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```
