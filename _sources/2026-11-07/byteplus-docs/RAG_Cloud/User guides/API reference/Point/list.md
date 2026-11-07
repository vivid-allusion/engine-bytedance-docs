---
title: "list"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/point_list"
---

<span id="93cfc7be"></span>
# Overview

The `/api/knowledge/point/list` endpoint is used to view the list of slices under the knowledge base or a specific experiment version, sorted by point_id in ascending order by default.

> By specifying the pipeline_name parameter, it is possible to query only the list of slices under a specific experiment version.


<span id="5687c89e"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page, the API can be called to view the list of slices under the knowledge base.

<span id="660ccaf0"></span>
# **Request endpoint**


|**URI** |/api/knowledge/point/list |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="6ff17136"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Name of the knowledge base** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique ID of the knowledge base**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier of the knowledge base. |
|offset |int |No |0 |**Used for pagination**<br><br>Indicates the starting position in the result set; must be greater than or equal to 0. |
|limit |int |No |\-1 |**Number of slices to return**<br><br>\-1 means to retrieve all; the maximum value does not exceed 100, and each response returns no more than 100. |
|doc_ids |list |No |\-\- |**Filter by document ID**<br><br>Specify a document to return the corresponding slice list. If not provided or set to null, no filtering is applied. If the input size is 0, an empty result will be returned. Limit the list length; the maximum length is 100. |
|point_ids |list |No |\-\- |**Filter by slice ID**<br><br>Specify one or more slice IDs to return the corresponding slice content. If not provided or set to null, no filtering is applied. If the input size is 0, an empty result will be returned. The maximum length of slice IDs is 100. |
|get_attachment_link |bool |No |False |**Whether to obtain a temporary download link for images in the slice**<br><br>Valid for 10 minutes |
|pipeline_name |string |No |\-\- |**Experiment version name**<br><br><br>* Specifying this parameter allows querying the list of slices under a specific experiment version.<br><br>* If not specified, the list of slices under the primary version of the knowledge base is queried by default. |


<span id="b6ce9114"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |Slice content. The return value description is the same as the info API.<br><br>```JSON```<br>```{```<br>```    "collection_name": "Knowledge base name",```<br>```    "total_num": "Total number of results",```<br>```    "count": "Number of results returned this time",```<br>```    "point_list": [```<br>```        {```<br>```          "collection_name": "Knowledge base name",```<br>```          "point_id": "Chunk ID // Unique within each knowledge base version",```<br>```          "doc_info": {```<br>```              "doc_id": "Document ID to which it belongs",```<br>```              "doc_name": "Document name to which it belongs",```<br>```              "create_time": "Chunk creation time",```<br>```              "doc_type": "Original document type to which it belongs",```<br>```              "description": "Document description (currently only supports image documents)",```<br>```              "doc_meta": "Meta information of the document to which it belongs",```<br>```              "source": "Knowledge source of the document to which it belongs (url, tos, etc.)",```<br>```              "title": "Document title to which it belongs",```<br>```              "original_coordinate": "Original position coordinates of the chunk in the document // Only PDF and PPT documents are supported"```<br>```          },```<br>```        "process_time": "Time when chunk processing was completed",```<br>```        "chunk_title": "Chunk title, which is the upper-level title identified by the parsing model. Empty if there is no upper-level title",```<br>```        "content": "Chunk content",```<br>```        "md_content": "Chunk markdown parsing result, preserving more original table information, currently only chunks with chunk_type as table will return this field",```<br>```        "html_content": "Chunk HTML parsing result, preserving more original table information, currently only chunks with chunk_type as table will return this field"```<br>```      }```<br>```  ]```<br>```}```<br> |


<span id="528433bf"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |


<span id="619aaa2a"></span>
# Complete example

<span id="31dff5f4"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/point/list \
  -d '{
    "collection_name": "test_collection_name",
    "project": ""
}'
```


<span id="e21583b5"></span>
## Response message

Return on success:

```Shell
{
    "code": 0,
    "data": {
        "collection_name": "api0828",
        "total_num": 1,
        "count": 1,
        "point_list": [
            {
                "collection_name": "api0828",
                "point_id": "_sys_auto_gen_doc_id-17691607628519396693-0",
                "process_time": 1724848725,
                "content": "xxx",
                "chunk_id": 0,
                "doc_info": {
                    "doc_id": "_sys_auto_gen_doc_id-17691607628519396693",
                    "doc_name": "xxx.xlsx",
                    "create_time": 1724848720,
                    "doc_type": "xlsx",
                    "source": "tos_fe"
                },
                "chunk_type": "structured",
                "table_chunk_fields": [
                    {
                        "field_name": "Explanation Module",
                        "field_value": "Explanation Module: xxxxxx"
                    },
                    {
                        "field_name": "Sub-module",
                        "field_value": "Sub-module: xxxxx"
                    },
                    {
                        "field_name": "Question Example",
                        "field_value": "Question Example: xxxxxx"
                    },
                    {
                        "field_name": "Memorization - Key Points",
                        "field_value": ""
                    }
                ]
            }
        ]
    },
    "message": "success",
    "request_id": "02172484891424400000000000000000000ffff0a00705414b331"
}
```


Return on failure:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
