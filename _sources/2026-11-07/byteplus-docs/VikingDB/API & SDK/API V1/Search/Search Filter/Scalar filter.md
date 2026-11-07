---
title: "Scalar filter"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Scalar_filter"
---

You can filter the results in a vector database using a scalar filter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Scalar filtering is a general\-purpose search capability that you can use in<strong>Search and Aggregation Statistics</strong>Incoming from the relevant interface<strong>Filter parameters</strong>To enable scalar filtering capabilities.</div>


<span id="96e38c3f"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/search |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |



|**URI** |/api/index/search/agg |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="ea8e9ffd"></span>
# **request parameters**

In addition to vector search and aggregation statistics, you can specify the `filter` parameter in your search request to perform scalar filtering.


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|Search |Filter |Map |Yes |*  |Filter conditions, see the Filter expression section.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions use query operators (`must`, `must_not`, `range`, `range_out`) and logical operators (`and`, `or`).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The precondition for a filter is that the corresponding field has a scalar index enabled.</div><br> |


<span id="04164d3b"></span>
## Filter expression


|**operator** |**operator description** |**field type** |**example** |
|---|---|---|---|
|Must |Matches documents where the value of the specified field is in the provided list. | |```JSON```<br>```{```<br>```  "op": "must",```<br>```  "field": "region",```<br>```  "conds": ["cn", "sg"]```<br>```}```<br> |
|must_not |Matches documents where the value of the specified field is not in the provided list. | |```JSON```<br>```{```<br>```  "op": "must_not",```<br>```  "field": "data_type",```<br>```  "conds": [1,2,3]```<br>```}```<br> |
|Range |Effective for the specified field name, the semantics must be within the specified range.<br><br>Use `gte` (greater than or equal to), `gt` (greater than), `lte` (less than or equal to), and `lt` (less than) to define a one\-dimensional range.<br><br>In addition, you can use `center` and `radius` to represent a circular range in two dimensions. | |```JSON```<br>```// Selects price values in the range of [100.0, 500.0).```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0,```<br>```  "lt": 500.0```<br>```}```<br>``````<br>```// Selects price values greater than or equal to 100.0.```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0```<br>```}```<br>``````<br>```// Selects values in a circle with a radius of 50 from the specified center.```<br>```{```<br>```  "op": "range",```<br>```  "field": ["pos_x", "pos_y"],```<br>```  "center": [100.0, 123.4],```<br>```  "radius": 50.0```<br>```}```<br> |
|range_out |Effective for the specified field name, the semantics must be outside the specified range. Configure to use`gte`(Greater than or equal to), `gt`(Greater than), `lte`(Less than or equal to), `lt`(Less than), used to delimit the one\-dimensional range. | |```JSON```<br>```// Selects price values outside the range of [100.0, 500.0).```<br>```{```<br>```  "op": "range_out",```<br>```  "field": "price",```<br>```  "gt": 500.0,```<br>```  "lt": 100.0```<br>```}```<br> |
|And |Logical operator, which intersects multiple conditions for logical query requirements. | |```JSON```<br>```{```<br>```  "op": "and",   // The operator name.```<br>```  "conds": [     // The list of conditions. You can nest logical operators and the must or must_not operator.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // You can specify one or more conditions for filtering.```<br>```    }```<br>```  ]```<br>```}```<br> |
|Or |Logical operator, for logical query requirements, takes the union of multiple conditions. | |```JSON```<br>```{```<br>```  "op": "or",   // The operator name.```<br>```  "conds": [     // The list of conditions. You can nest logical operators and the must or must_not operator.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // You can specify one or more conditions for filtering.```<br>```    }```<br>```  ]```<br>```}```<br> |


<span id="27510e4b"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Description |
|request_id |A unique identifier for each request |
|Data |Search results, scalar filter search will return the retrieved primary key, score, fields. |


<span id="06b3db44"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Search success |Index retrieved successfully. |
|1000008 |400 |Index does not exist |The specified Index does not exist. |
|1000003 |400 |Invalid request |Illegal parameter:<br><br><br>* Required parameters are missing.<br><br>* Lack of search input.<br><br>* Constraint not satisfied. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |
|1000016 |400 |Invalid vectors for index_recall |The input vector format is invalid. |
|1000029 |429 |The request has reached the upper limit, please adjust the number of CPU cores |Need to increase cpu_quota |


<span id="b3a6d8a5"></span>
# Complete example

<span id="03df9c5c"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/search \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test",
    "search": {
        "order_by_vector": {
            "vectors": [
                [0.1, 0.2, 0.3......0.9], 
                [0.01, 0.02, 0.03......0.09],
            ],
            "sparse_vectors": [
                {"what": 0.34, "is": 0.03, "B": 0.11, "M":0.32, "25": 0.03}, 
                {"one": 0.08, "of": 0.14, "information": 0.19, "retrieval": 0.63, "algorithms":0.97} 
            ]            
        }, 
        "limit": 2,   
        "dense_weight": 0.5,  
        "filter": {     // The filter condition. 
          "op": "must",    // The filter type. The result must meet the condition. 
          "field": "region",     // The field to filter. 
          "conds": ["cn", "sg"]    // The filtered values must match "cn" or "sg". 
        }
        "partition": "default"     // The name of the subindex matches the field value.
    }
}'
```


<span id="11fccd5b"></span>
## Response message

A successful request returns the following response:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "msg":"search success",
    "request_id":"021695029757920fd001de6666600000000000000000002569b8f",
    "data": [
        [
            {
                "id": 1,
                "score": 0.99,
                "fields": {
                    "time": 1690529704,
                    "author": "zhangsan"
                } 
            },
            {
                "id": 2,
                "score": 0.98,
                "fields": {
                    "time": 1690529701,
                    "author": "lisi"
                } 
            }
        ],
        [
            {
                "id": 9,
                "score": 0.95,
                "fields": {
                    "time": 1690529708,
                    "author": "wangwu"
                } 
            },
            {
                "id": 8,
                "score": 0.84,
                "fields": {
                    "time": 1690529710,
                    "author": "zhaoliu"
                } 
            }            
        ]
    ]
}
```


A failed request returns the following response:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008, "msg":"index not exist", "request_id":"021695029757920fd001de6666600000000000000000002569b8f"}
```
