---
title: "Create Vikingdb Collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Create_Collection_V2"
---

<span id="overview"></span>
# Overview

This interface is used to create a vector database

<span id="interface-upgrade-notes"></span>
# Interface Upgrade Notes


* Corresponding V1 interface: https://docs.byteplus.com/en/docs/VikingDB/create

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |CamelCase (`CollectionName`) |Underscore (`collection_name`) |
|Parameter Type |Vectorize type is map |Vectorize data type is []map. |
|Primary Key Parameter Location |Sub\-parameter IsPrimaryKey of Fields |primary_key |


<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2), copy the calling example and fill in the necessary information.

<span id="request-parameters"></span>
## Request Parameters

Request parameter Action value: CreateVikingdbCollection

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Level 1 Parameter |Level 2 Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|---|---|
|ProjectName | | |String |No |default |Project name |
|CollectionName | | |String |Yes | |Collection name |
|Description | | |String |No | |Collection description |
|Fields | | |List |Yes | |Field list |
| |FieldName | |String |Yes | |Field name |
| |FieldType | |String |Yes | |Field type |
| |Dim | |Integer |No | |If the field type is vector, this parameter specifies the dimension of the dense vector |
| |IsPrimaryKey | |Boolean |No | |Specifies whether this is the primary key field. You can specify 1 primary key field (string or int64 type) for the collection. If not specified, an auto\-generated primary key will be used with the field name "**AUTO_ID**". |
| |DefaultValue | |Any type |No | |Default value for field content |
|Vectorize | | |Map |No | |Vectorization model settings. Fill in only when the collection needs vectorization. |
| |Dense | |Map |Yes | |Dense vectorization model configuration |
| | |ModelName |String |Yes | |Model name |
| | |ModelVersion |String |No | |Model version |
| | |TextField |String |No | |Text vectorization field name |
| | |ImageField |String |No | |Image vectorization field name |
| | |Dim |Integer |No | |If dense vectors need to be generated, specify the vector dimension. By default, the model's default dimension is used. |
| | |VideoField |String |No | |Video vectorization field |
| |Sparse | |Map |No | |Sparse vectorization configuration |
| | |ModelName |String |Yes | |Model name |
| | |ModelVersion |String |No | |Model version |
| | |TextField |String |No | |Text vectorization field name |
|FullText | | |List |No | |FullTextConfig structure is shown below.<br><br>You can configure up to two text fields as full\-text search fields. |


`FullTextConfig` structure:


|Parameter |Required |Type |Description |
|---|---|---|---|
|Field |Yes |String |Must be an existing text field in Fields. |
|Analyzer |Yes |AnalyzerConfig |AnalyzerConfig structure is shown below. |


`AnalyzerConfig` structure:


|Parameter |Required |Type |Description |
|---|---|---|---|
|Tokenizer |Yes |String |Tokenizer. Valid values:<br><br><br>* `standard`: Supports Chinese/English/mixed content with better performance.<br><br>* `zh`: Better Chinese tokenization with slightly lower performance.<br><br>* `whitespace`: Split by whitespace characters (space, `\t`, `\n`, `\r`, `\v`, `\f`). |


<span id="example-response"></span>
## Example Response

The table below lists only the unique response parameters for this interface. For more information, see [Control Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Control_Plane_API_V2)


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|ResourceId |String | |Resource ID |
|Message |String |success |Operation result information |


<span id="request-examples"></span>
## Request Examples

<span id="create-a-collection-with-vector-field"></span>
### Create a collection with vector field

```Plain
action="CreateVikingdbCollection",
body = {
  "ProjectName": "default",
  "CollectionName": "my_test_coll_1",
  "Description": "this is my test collection",
  "Fields": [
    {
      "FieldName": "f_id",
      "FieldType": "string",
      "IsPrimaryKey": true,
    },
    {
      "FieldName": "f_int64",
      "FieldType": "int64",
      "DefaultValue": -1
    },
    {
      "FieldName": "f_vector",
      "FieldType": "vector",
      "Dim": 1024
    }
  ]
}
```


<span id="create-a-collection-with-vectorize-field"></span>
### Create a collection with vectorize field

```Python
action = "CreateVikingdbCollection"
body = {
    "ProjectName": "default",
    "CollectionName": "my_test_coll_2",
    "Description": "",
    "Fields": [
        {"FieldName": "f_id", "FieldType": "int64", "IsPrimaryKey": True},
        {"FieldName": "f_text", "FieldType": "text", },
        {"FieldName": "f_image", "FieldType": "image", },
        {"FieldName": "f_video", "FieldType": "video", },
    ],
    "Vectorize": {
        "Dense": {
            "ModelName": "Skylark-embedding-vision",
            "ModelVersion": "250615",
            "TextField": "f_text",
            "ImageField": "f_image",
            "Dimension": 1024,
        },
    }
}
```


Example Response

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250331173619111231152071D44F42",
    "Action": "CreateCollection",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="error-codes"></span>
# Error codes

For common error codes, please refer to the [Common Error Codes](https://docs.byteplus.com/en/docs/VikingDB/FAQ_common) and [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/en/docs/VikingDB/FAQnew).
