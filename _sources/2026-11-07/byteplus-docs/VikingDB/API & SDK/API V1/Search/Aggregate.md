---
title: "Aggregate"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Aggregate"
---

<span id="662ca44e"></span>
# Overview

/index/search/agg interface is used to implement aggregation. This page mainly describes how to perform aggregation statistics on the specified index search results.

You can perform aggregate statistics by specifying fields for grouping and adding filter conditions. This can help you understand your data distribution.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An index requires a scalar index field that contains at least one enumeration type (string, int64, or bool).</div>


<span id="ceaf0870"></span>
# **Request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/search/agg |Uniform Resource Identifier |
|---|---|---|
|**Request method** |POST |The HTTP method for the operation. |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="df3fa2d7"></span>
# **request parameters**


|Parameter name |Type |Required |Note |Sub\-parameter |Type |Note |Required |
|---|---|---|---|---|---|---|---|
|collection_name/collection_alias |String |Yes |Collection name | | | | |
|index_name |String |Yes |Index name | | | | |
|Search |Map |No |Search parameters |Filter |Map |Filter conditions, used in the same way as the index search interface |No |
|||||||||
|||||||||
|||||Partition |Int64/string |The sub\-index name. Its type must be consistent with the partition_by field's type, and its value must correspond to the partition_by field's value.<br><br><br>* If field_type is int64 or list, the partition input type is int64.<br><br>* field_type string, list, partition input type is string, and must match the format `^[a-zA-Z0-9-_]+$`<br><br><br>If this parameter is not set, the default value is "default". |No |
|Agg |Map |Yes |Aggregation parameter |Op |String |Currently, only the count operator is supported. To use it, the index must contain at least one scalar index field of type string, int64, or bool. |Yes |
|||||Field |String |The name of the field to aggregate. The field must be a scalar index field of type string, int64, or bool. |No |
|||||Cond |Map |Similar to the GROUP BY HAVING clause in SQL. This parameter only takes effect if the field parameter is also specified. For the count operator, gt is supported, which returns only groups with a count greater than the specified value. |No |


<span id="f03377f1"></span>
# Complete example

<span id="a9aff30e"></span>
## Request message

Example 1: Get a total count of the data in the specified index.

```Shell
{
    "collection_name": "coll_name",
    "index_name": "idx_name",
    "search": {},
    "agg": {
        "op": "count"
    }
}
```


Example 2: Filter data in the specified index, aggregate by a specific field, and return only groups with a count greater than 5.

```TypeScript
{
    "collection_name": "coll_name",
    "index_name": "idx_name",
    "search": {
        "filter": {
            "op": "must_not",
            "field": "f_string",
            "conds": ["doc1"]
        }
    },
    "agg": {
        "op": "count",
        "field": "f_string",
        "cond": {
            "gt": 5
        }
    }
}
```


<span id="cfea4e42"></span>
## Return example

Example 1

```Shell
{
    "code":0,
    "msg":"success",
    "request_id":"02173373312268600000000000000000000ffff0a0048d51718ba"
    "data": {
        "agg_op": "count",
        "group_by_field": "__NONE__",
        "agg_result": {
            "__TOTAL__": 10001
        }
    }
}
```


Example 2

```TypeScript
{
    "code":0,
    "msg":"success",
    "request_id":"02173373312268600000000000000000000ffff0a0048d51718ba"
    "data": {
        "agg_op": "count",
        "group_by_field": "f_doc",
        "agg_result": {
            "doc1": 234,
            "doc2": 221
        }
    }
}
```
