---
title: "update"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/update1"
---

<span id="bc583163"></span>
# Overview

/index/update interface is used to update the description, cpu_quota, scalar_index of the specified Index.

<span id="f73657eb"></span>
# **Request format**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/update |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="e75cf0e0"></span>
# **Request parameters**


|**parameter** |**type** |**Required** |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |The name of the Collection that contains the index to be updated.<br><br><br>* Must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|index_name |String |Yes |The name of the index to update.<br><br><br>* Must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|cpu_quota |Int |No |CPU quota consumed by index retrieval, in the form of a positive integer.<br><br><br>* As a general estimate that prioritizes throughput over latency, 1 CPU core can handle approximately 100 QPS.<br><br>* The total CPU consumption is proportional to the number of shards; if retrieval consumption exceeds the quota, requests will be throttled.<br><br>* Value range: [1,10240]. |
|Description |String |No |Update the description of the index. |
|scalar_index |Array |No |Updates the list of fields to build into the scalar index. Among them, float and int64 fields can be used for range retrieval, and non\-float fields can be used for enumeration retrieval.<br><br><br>* scalar_index defaults to None, meaning all fields are built into a scalar index.<br><br>* An empty array (`[]`) specifies that no scalar index should be built.<br><br>* If you provide a non\-empty list, only the fields in the list are built into the scalar index. |
|shard_policy |String |No |Index sharding type<br><br><br>* Possible values are `auto` (for automatic sharding) and `custom` (for custom sharding).<br><br><br>For large datasets, index sharding divides index data into multiple smaller blocks (shards) and distributes them across different nodes in a cluster. Each node stores and processes a subset of the index data. Queries are executed in parallel across the shards on different nodes. Since a single node has limited storage capacity, you must set an appropriate number of shards to avoid impacting indexing performance. Additionally, a higher number of shards results in a higher cost. |
|shard_count |Int |No |The number of custom shards.<br><br><br>* shard_count does not take effect when shard_policy is auto.<br><br>* This parameter is required when `shard_policy` is set to `custom`.<br><br>   * Value range: [1,256].<br><br>   * The default value is 1. To estimate the required number of shards, you can use the formula: (estimated data volume) / 30 million. |


<span id="034a30b7"></span>
# **Response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique identifier for each request. |


<span id="90c3f74f"></span>
## **Status code descriptions**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |Index updated successfully. |
|1000005 |400 |Collection does not exist |The specified Collection does not exist. |
|1000008 |400 |Index does not exist |The specified Index does not exist. |
|1000003 |400 |Invalid request:% s |Invalid argument. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="84d8648c"></span>
# Complete example

<span id="8c1b7fb9"></span>
## Request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/update \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test",
    "description": "update for index",
    "cpu_quota": 10,
    "scalar_index": ["city", "date"]
}'
```


<span id="c3fc4f06"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success","request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```


An example of a failed execution response is as follows:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000005, "message":"collection not exist", "request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```
