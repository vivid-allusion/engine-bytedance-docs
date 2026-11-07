---
title: "Post-processing operators"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Post-processing_operators"
---

Postprocessing operator is one provided by VikingDB**post\-retrieval processing capability**, used in**Vector recall**After that, the candidate data is further filtered and optimized to ensure that the final returned search results are more accurate and efficient.

In VikingDB, postprocessing operators can be used to:


* **Precise screening of results**: Set filtering rules through regular matching based on business requirements, such as filtering products that contain certain characteristic text information, to ensure that users get valid search results.

* **Data quality improvement**: Use regular matching to check the format of search results, filter data containing special characters, illegal content or advertising information, ensure that the returned content meets standards, and improve data standardization.

* **Search Results Equalization**Set frequency limits on specific fields to prevent certain values from occupying too many search results, such as popular brands, popular authors, or overexposure of specific categories, and ensure the diversity and fairness of search results.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Postprocessing operators are general\-purpose search capabilities that you can apply to<strong>Vector Nearest Neighbor Search</strong>,<strong>dense sparse hybrid nearest neighbor retrieval</strong>In.</div>


<span id="8a15016b"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/search |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="ea39ffa4"></span>
# **request parameters**

On the basis of a vector search request, you can specify in the search request parameters \*\*`post_process_ops`,`post_process_input_limit`\*\*Subparameter setting post\-processing operator.


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|Search |post_process_ops |List\ < map \> |No |*  |List of postprocessing operators. After the vector or scalar recall phase, further filtering processing is performed on the candidate data, such as string matching, frequency control, etc. Each operator is a map and is executed serially. Default is empty. See postprocessing operators below for details. |
||post_process_input_limit |Int |No |*  |When post_process_ops is set, the number of candidates to enter the post\-processing phase. The default value is 1000, and the maximum value is min (1600, limit \* 10). |


<span id="66dc3f22"></span>
## Postprocessing operator


|Operator |**explain** |Example |
|---|---|---|
|string_match |Regular matching operator. Only for fields of type string.<br><br>For regular matching rules, please refer to:[Syntax](https://github.com/google/re2/wiki/syntax) |```JSON```<br>```{```<br>```   "op": "string_match",```<br>```   "field": "name",```<br>```   "pattern": "^[0-9A-Za-z_]+$"```<br>```}```<br> |
|string_contain |Keyword matching operator. Only for fields of type string.<br><br>Indicates that the field content contains a pattern. |```JSON```<br>```{```<br>```   "op": "string_contain",```<br>```   "field": "name",```<br>```   "pattern": "bar"```<br>```}```<br> |
|enum_freq_limiter |Frequency operator. Only for fields of type string.<br><br>Used to ensure that the total number of occurrences of a particular value in a recall does not exceed `threshold` Times. |```JSON```<br>```{```<br>```  "op": "enum_freq_limiter",```<br>```  "field": "city"```<br>```  "threshold": 5```<br>```}```<br> |


<span id="dc60f747"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique device identifier for each request |
|Data |Search results, scalar filter search will return the retrieved primary key, score, fields. |


<span id="425e0630"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Drop index success |Index retrieved successfully. |
|1000008 |400 |Index not exists |The specified Index does not exist. |
|1000003 |400 |Invalid request |Illegal parameter:<br><br><br>* Required parameters are missing.<br><br>* Lack of search input.<br><br>* Constraint not satisfied. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |
|1000016 |400 |Invalid vectors for index_recall |The input vector format is invalid. |
|1000029 |429 |The request has reached the upper limit, please adjust the number of CPU cores |Need to increase cpu_quota |


<span id="cdf75d92"></span>
# Complete example

<span id="fcb7d501"></span>
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
                [0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9], 
                [0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 0.07, 0.08, 0.09]
            ],
            "sparse_vectors": [
                {"what": 0.34, "is": 0.03, "B": 0.11, "M": 0.32, "25": 0.03}, 
                {"one": 0.08, "of": 0.14, "information": 0.19, "retrieval": 0.63, "algorithms": 0.97} 
            ]            
        }, 
        "limit": 2,
        "dense_weight": 0.5,
        "partition": "default"
    },
    "post_process_ops": [           // A list of post-processing operators applied after initial retrieval. 
        { 
            "op": "string_match",   // Apply string matching to string fields. 
            "field": "name",        // Filter the `name` field by using a regular expression. 
            "pattern": "^[0-9A-Za-z_]+$" // Retain only values that match the regular expression pattern. 
            // Example: Remove candidates with `name` values that include characters other than letters, digits, or underscores. 
        }, 
        { 
            "op": "enum_freq_limiter", // Limit the frequency of a specific field value in the results. 
            "field": "city",        // Apply frequency control to the `city` field. 
            "threshold": 5          // Allow each unique `city` value to appear no more than 5 times. 
            // Example: If candidates from the same city exceed 5, the list is trimmed to 5. 
        } 
    ], 
    "post_process_input_limit": 1000 // The maximum number of candidates processed in the post-processing stage. The default value is 1000. This improves performance by limiting processing to the top 1000 retrieved candidate results. 
}'
```


<span id="e0b6320b"></span>
## Response message

Successful execution returns:

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


Execution fails to return:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008, "msg":"index not exist", "request_id":"021695029757920fd001de6666600000000000000000002569b8f"}
```
