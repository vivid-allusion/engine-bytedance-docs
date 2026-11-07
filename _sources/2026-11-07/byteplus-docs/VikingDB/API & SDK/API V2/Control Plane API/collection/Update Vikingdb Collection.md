---
title: "Update Vikingdb Collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Update_Collection_V2"
---

<span id="984a4a60"></span>
# Overview

This interface is used to update a specified collection

<span id="bc99c49d"></span>
# Interface Upgrade Notes


* Corresponding V1 interface: https://docs.byteplus.com/en/docs/VikingDB/update

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter Naming Style |CamelCase (`CollectionName`) |Underscore (`collection_name`) |


<span id="1025c23c"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the , copy the example request and fill in the necessary information.

<span id="9ae4dba5"></span>
## Request Parameters

The value for the Action parameter is UpdateVikingdbCollection

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see the [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |String |No |Project name |
|CollectionName | |String |1 of 2 |Collection name |
|ResourceId | |String ||Collection resource ID. The request must specify either ResourceId or CollectionName. |
|Description | |Map |No |Collection description |
|Fields | |List |Yes |Field list |
| |FieldName |String |Yes |Field name |
| |FieldType |String |Yes |Field type |
| |DefaultValue |Any type |No |Default value for field content |


<span id="f2333ada"></span>
## Response Parameters

The table below lists only the unique response parameters for this interface. For more information, see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |Map |success |A message indicating the result of the operation |


<span id="1bebf375"></span>
## Request Examples

```Plain
action = "UpdateVikingdbCollection",
body = {
    "ProjectName": "default",
    "CollectionName": "my_test_coll_1",
    "Fields": [
        {
            "FieldName": "float_1",
            "FieldType": "float32",
            "DefaultValue": 0.0,
        },
    ]
}
```


<span id="f30add4b"></span>
## Response Examples

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250331204547113075129206F7CB23",
    "Action": "UpdateVikingdbCollection",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="f1e930b2"></span>
## Error Codes

For common error codes, please refer to the and documentation.
