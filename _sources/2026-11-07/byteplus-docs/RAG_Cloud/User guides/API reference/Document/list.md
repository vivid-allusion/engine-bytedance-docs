---
title: "list"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/doc_list"
---

<span id="3578d6b0"></span>
# Overview

The `/api/knowledge/doc/list` endpoint is used to query the list of documents in a knowledge base or in a specific experimental version, sorted by document upload time in descending order by default.

> You can query the list of documents in a specific experimental version by specifying the pipeline_name parameter.


<span id="15968d4f"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature generation on the "Signature authentication method" page, you can call the API endpoint to query all document information in a knowledge base.

<span id="3384ec9f"></span>
# **Request endpoint**


|**URI** |/api/knowledge/doc/list |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="9e05e3e3"></span>
# **Request parameters**


|**Parameter** |Sub\-parameter |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|collection_name |\-\- |string |No |\-\- |**Name of the knowledge base** |
|project |\-\- |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, the system searches for the knowledge base in the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To query documents from a knowledge base in a specified project, this field must be configured correctly.</div><br> |
|resource_id |\-\- |string |No |\-\- |**Unique ID of the knowledge base**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project together to uniquely identify the knowledge base. |
|filter | |json |No |\-\- |**Filter conditions**<br><br>Used to filter the returned results; supports filtering by doc_id. |
||doc_id_list |list |No |\-\- |**A list of document IDs to filter by.** <br><br>Only the information of the documents specified in the list will be returned. |
|offset |\-\- |int |No |0 |**Query starting position**<br><br>Indicates the starting position in the result set; must be greater than or equal to 0.<br><br>Note: If offset ≥ 100 is set, the limit parameter must also be provided for it to take effect. |
|limit |\-\- |int |No |\-1 |**Number of documents to query**<br><br>\-1 means to retrieve all documents, but the maximum number returned per request is 100. |
|doc_type |\-\- |list |No |\-\- |**Document type filter** |
|return_token_usage |\-\- |bool |No |false |**Whether to return the number of tokens consumed for document vectorization and document summary generation** |
|pipeline_name |\-\- |string |No |\-\- |**Name of the experimental version**<br><br><br>* If not specified, the list of documents in the primary version of the knowledge base is queried by default.<br><br>* If specified, the list of documents in the specified experimental version is queried. |
|detailed |\-\- |bool |No |false |**Whether to display detailed document information**<br><br>Detailed information: document summary<br><br>Note: The summary\-related fields return a large amount of content, which may result in longer request times. It is recommended to call the doc/info endpoint separately only when necessary. |


**Response message**


|**Parameters** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |* collection_name: Name of the knowledge base<br><br>* total_num: Total number of documents in the knowledge base<br><br>* count: Total number of documents returned in this query<br><br>* doc_list: List of queried document information, where each element represents the information of a single document. For the format of a single document's information, refer to [info](https://docs.byteplus.com/docs/209/doc_info) |


<span id="c79eb0fe"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |


<span id="4646ba60"></span>
# Complete example

<span id="9344dab7"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/doc/list \
  -d '{
    "collection_name": "test_collection_name",
    "project": "",
    "filter": {
            "doc_id_list": ["test0123", "test1111"]
        },
    "return_token_usage": true
}'
```


<span id="1108db4f"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
{
    "code": 0,
    "data": {
        "collection_name": "test_collection_name",
        "total_num": 2,
        "count": 2,
        "doc_list":[
            {
                "collection_name": "test_collection_name",
                "doc_name" :"Zhang XX Theft Case",
                "doc_id": "test0123",
                "add_type": "url",
                "doc_type": "pdf",
                "doc_summary": "This paper proposes a Transformer model based on attention mechanism,...", // Full document summary
                "brief_summary": "This paper proposes a Transformer model based on attention mechanism,...", // Brief summary
                "create_time": 1711367027,
                "added_by": "username",
                "update_time": 1711367030,
                "url": "xxx",
                "point_num": 53,
                "status":{
                    "process_status":0
                },
                "total_tokens":345390,
                "doc_summary_tokens": 120742,
                "doc_premium_status":{
                "doc_summary_status_code":0  // Summary generation status code
            },
            {
                "collection_name": "test_collection_name",
                "doc_name" :"Test Document",
                "doc_id": "test1111",
                "add_type": "url",
                "doc_type": "doc",
                "create_time": 1711367010,
                "added_by": "username",
                "update_time": 1711367010,
                "url": "xxx",
                "point_num": 100,
                "status":{
                    "process_status":0
                },
                "total_tokens":345390
            }
        ]
    },
    "message": "success",
    "request_id": "02171136497331800000000000000000000ffff0a00601688694f"
}
```


Failed execution returns:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request: %s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
