---
title: "Get Vikingdb Collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Get_Collection_V2"
---

<span id="f866c2a3"></span>
# Overview

This interface is used to query the details of a specified collection

<span id="8498f0db"></span>
# Interface Upgrade Notes


* Corresponding V1 interface: https://docs.byteplus.com/en/docs/VikingDB/info

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |CamelCase (`CollectionName`) |Underscore (`collection_name`) |


<span id="74d18a99"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="58894477"></span>
## Request Parameters

Request parameter Action value: GetVikingdbCollection

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see[Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |String |No |Project name |
|CollectionName |String |1 of 2 |Collection name |
|ResourceId |String ||Collection resource ID. The request must specify either ResourceId or CollectionName. |


<span id="50b9fd8e"></span>
## Response Parameters

The table below lists only the unique response parameters for this interface. For more information, see[Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2)


|Parameter |Level 1 Parameter |Level 2 Parameter |Type |Description |
|---|---|---|---|---|
|ProjectName | | |String |Project name |
|ResourceId | | |String |Resource ID |
|CollectionName | | |String |Collection name |
|Description | | |String |Collection description |
|Fields | | |Map |Field list |
| |FieldName | |String |Field name |
||FieldType | |String |Field type |
||Dim | |Integer |If the field type is vector, this parameter specifies the dimension of the dense vector |
||IsPrimaryKey | |Boolean |Whether it is a primary key field. You can specify 1 primary key field (string or int64 type) for the collection. If not specified, an auto\-generated primary key will be used with the field name "**AUTO_ID**". |
||DefaultValue | |Any type |Default value for field content |
|Vectorize | | |Map |Vectorization configuration |
||Dense | |Map |Dense vectorization model configuration |
|||ModelName |String |Model name |
|||ModelVersion |String |Model version |
|||TextField |String |Text vectorization field name |
|||ImageField |String |Image vectorization field name |
|||Dim |Integer |If dense vectors need to be generated, specify the vector dimension. By default, the model's default dimension is used. |
||Sparse | |Map |Sparse vectorization configuration |
|||ModelName |String |Model name |
|||ModelVersion |String |Model version |
|||TextField |String |Text vectorization field name |
|CreateTime | | |String |Creation time |
|UpdateTime | | |String |Update time |
|UpdatePerson | | |String |Updater |
|CollectionStats | | |Map |Statistics |
||DataCount | |Long |Data count |
||DataStorage | |Long |Data storage (byte) |
|EnableKeywordsSearch | | |Boolean |Whether keyword search is supported |
|IndexNames | | |Array of String |Index name list in the collection |
|IndexCount | | |Integer |Number of indexes in the collection |


<span id="673f05d3"></span>
## Request Examples

```Plain
action = "GetVikingdbCollection",
body = {
  "ProjectName": "default",
  "CollectionName": "my_test_coll_1"
}
```


<span id="10647794"></span>
## Response Examples

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250331165519111117128071B54F6E",
    "Action": "GetVikingdbCollection",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "ProjectName": "default",
    "ResourceId": "vc_m720250331165459221712807139*****",
    "CollectionName": "my_test_coll_1",
    "Description": "",
    "Fields": [
      {
        "FieldName": "f_id",
        "FieldType": "string",
        "IsPrimaryKey": true,
        "DefaultValue": null
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
    ],
    "Vectorize": {},
    "CreateTime": "2025-03-31T16:54:59+08:00",
    "UpdateTime": "2025-03-31T16:54:59+08:00",
    "UpdatePerson": "Volcengine API",
    "CollectionStats": {
      "DataCount": 0,
      "DataStorage": 0
    },
    "EnableKeywordsSearch": false,
    "IndexNames": [],
    "IndexCount": 0
  }
}
```


<span id="64550969"></span>
## Error Codes

For common error codes, please refer to the [Common Error Codes](https://docs.byteplus.com/docs/VikingDB/FAQ_common) documentation.
