---
title: "Update Vikingdb Index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Update_Index_V2"
---

<span id="6b7bf094"></span>
# Overview

Interface for updating a specified index

<span id="72ab4418"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is: https://docs.byteplus.com/en/docs/VikingDB/update1

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter naming style |CamelCase (`IndexName`) |Underscore (`index_name`) |



* Note: QPS rate limiting is calculated based on the number of data entries, and the rate limiting behavior of V1 and V2 interfaces is identical.


<span id="e784a2a5"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="75df12b5"></span>
## Request Parameters

Request parameter Action value: UpdateVikingdbIndex.

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |String |No |Project name |
|CollectionName |String |One of two |Dataset name |
|ResourceId |String ||Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|IndexName |String |Yes |Index name |
|ShardPolicy |String |No |Index sharding type<br><br>Optional values are auto/custom, where auto is automatic sharding and custom is custom sharding.<br><br>Index sharding refers to evenly dividing index data into multiple small index data blocks in large data volume scenarios, and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data, and queries will simultaneously request index data blocks on different nodes. Due to the limited capacity of a single node, it is impossible to store all index data on a single node, so it is necessary to set an appropriate number of index shards, otherwise, it will affect the timeliness of data indexing. In addition, the number of shards is related to cost, and the more shards, the higher the cost. |
|Description |String |No |Custom description of the index. |
|ScalarIndex |Array of String |No |Scalar field list, used to set fields that need to be built into the scalar index. Among them, float and int64 fields can be used for range retrieval, and non\-float fields can be used for exact match retrieval.<br><br><br>* scalar_index defaults to None, indicating that all fields are built into the scalar index.<br><br>* When scalar_index is [], it indicates no scalar index.<br><br>* When scalar_index is a non\-empty list, it indicates that the fields in the list are built into the scalar index. |
|ShardCount |Integer |No |Custom shard count.<br><br><br>* When shard_policy is auto, shard_count is ignored.<br><br>* When shard_policy is custom, shard_count is required.<br><br>   * Value range: [1, 256].<br><br>   * Defaults to 1, shard count estimation guideline: estimated data volume/30 million. |
|CpuQuota |Integer |No |CPU quota consumed by index retrieval, in the format of a positive integer.<br><br>Related to throughput, not latency. 1 CPU core is approximately 100 QPS.<br><br>N shards consume N times the CPU; if the CPU consumed by retrieval exceeds the quota, the index will be rate\-limited.<br><br>Value range: [1, 10240]. |


<span id="6306949a"></span>
## Response Parameters

The table below only lists the response parameters specific to this interface. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |Operation result information |


<span id="532d186a"></span>
## Request Example

```Plain
action = "UpdateVikingdbIndex"
body = {
  "Description": "it is a test index",
  "CpuQuota": 10,
  "CollectionName": "test_coll",
  "IndexName": "test_index_1"
}
```


<span id="104ff208"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250527175413216098005053ADD0C8",
    "Action": "UpdateVikingdbIndex",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="5495ab87"></span>
## Error Codes

For common error codes, please refer to the  API V2 Error Codes and Troubleshooting Guide.
