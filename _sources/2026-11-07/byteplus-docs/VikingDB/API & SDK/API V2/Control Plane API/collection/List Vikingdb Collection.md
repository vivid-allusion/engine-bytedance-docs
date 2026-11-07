---
title: "List Vikingdb Collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/List_Collection_V2"
---

<span id="9cc2eae5"></span>
# Overview

This interface is used to query the list of specified collections

<span id="b7f108bd"></span>
# Interface Upgrade Notes


* Corresponding V1 interface: https://docs.byteplus.com/en/docs/VikingDB/list1

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |CamelCase (`CollectionName`) |Underscore (`collection_name`) |


<span id="4eb8f722"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="8068a6ad"></span>
## Request Parameters

Request parameter Action value: ListVikingdbCollection

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |String |No |Project name |
|PageNumber | |Integer |No |Page number for pagination. Starting from 1. |
|PageSize | |Integer |No |Page size for pagination. |
|Filter | |Map |No |Filter conditions |
||CollectionNameKeyword |String |No |Keywords contained in the collection name |


<span id="81fa98ce"></span>
## Response Parameters

The table below lists only the unique response parameters for this interface. For more information, see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2)


|Parameter |Level 1 Parameter |Level 2 Parameter |Level 3 Parameter |Type |Description | |
|---|---|---|---|---|---|---|
|TotalCount | | | |Integer |Total count of query results | |
|PageSize | | | |Integer |PageSize value in the request. If not specified in the request, it will be the default value. | |
|PageNumber | | | |Integer |PageNumber value in the request. If not specified in the request, it will be the default value. | |
|Collections | | | |Map |Vector database collection list | |
||CollectionName | | |String |Collection name | |
||ResourceId | | |String |Resource ID | |
||ProjectName | | |String |Project name | |
||Vectorize | | |Map |Vectorization configuration | |
|||Dense | |Map |Dense vectorization model configuration | |
||||ModelName |String |Model name | |
||||ModelVersion |String |Model version | |
||||TextField |String |Text vectorization field name | |
||||ImageField |String |Image vectorization model | |
||||Dim |Integer |If dense vectors need to be generated, specify the vector dimension. By default, the model's default dimension is used. | |
|||Sparse | |Map |Sparse vectorization configuration | |
||||ModelName |String |Model name | |
||||ModelVersion |String |Model version | |
||||TextField |String |Text vectorization field name | |
||Tags | | |Map |Tags | |
|||Key | |String |Tag key | |
|||Value | |String |Tag value | |
||Description | | |String |Collection description | |
||Fields | | |Map |Field list | |
|||FieldName | |String |Field name | |
|||FieldType | |String |Field type | |
|||Dim | |Integer |If the field type is vector, this parameter specifies the dimension of the dense vector | |
|||IsPrimaryKey | |Boolean |Whether it is a primary key field. You can specify one primary key field (string or int64 type) for the dataset. If not specified, an auto\-generated primary key will be used with the field name "AUTO_ID". | |
|||DefaultValue | |Any |Default value of field content | |
||CreateTime | | |Map |Creation time | |
||UpdateTime | | |Map |Update time | |
||UpdatePerson | | |Map |Updater | |
||CollectionStats | | |Map |Statistical information | |
|||DataCount | |Long |Number of data entries | |
|||DataStorage | |Long |Data storage size (bytes) | |
||EnableKeywordsSearch | | |Boolean |Whether keyword search is supported | |
||IndexNames | | |Array of String |List of index names under the dataset | |
||IndexCount | | |Integer |Number of indexes under the dataset | |


<span id="7149973f"></span>
## Request example

```Plain
action = "ListVikingdbCollection"
body = {
  "PageNumber": 1,
  "PageSize": 10,
  "Filter": {
    "CollectionNameKeyword": "test"
  }
}
```


<span id="4eb85693"></span>
## Return example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "202504151652000192410360866607FF",
    "Action": "ListVikingdbCollection",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Collections": [
      {
        "CollectionName": "test_coll",
        "ResourceId": "vdb-abcabc",
        "ProjectName": "default",
        "Description": "",
        "Fields": [
          {
            "FieldName": "f_v",
            "FieldType": "vector",
            "Dim": 1024
          },
          {
            "FieldName": "f_s",
            "FieldType": "string"
          }
        ],
        "CreateTime": "2023-11-21 12:22:57",
        "UpdateTime": "2023-11-22 13:15:45",
        "UpdatePersion": "xiaoming",
        "CollectionStats": {
          "DataCount": 887,
          "DataStorage": 475000
        },
        "IndexCount": 1,
        "IndexNames": [
          "idx1"
        ]
      }
    ]
  }
}
```


<span id="bcb561a8"></span>
## Error code

For common error codes, please refer to the [Common Error Codes](https://docs.byteplus.com/docs/VikingDB/FAQ_common) and [API V2 Error Codes and Troubleshooting Guide](https://docs.byteplus.com/docs/VikingDB/FAQnew)
