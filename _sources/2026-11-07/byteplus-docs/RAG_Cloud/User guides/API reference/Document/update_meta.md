---
title: "update_meta"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/doc_update_meta"
---

<span id="a57af64a"></span>
# Overview

The `/api/knowledge/doc/update_meta` endpoint is used to update document information in the knowledge base or a specific experimental version. Updating document meta information will automatically trigger data updates in the index.

> Editing document meta information in a specific experimental version is supported by specifying the pipeline_name parameter.


<span id="552094ae"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature retrieval on the 'Signature Authentication Method' page, you can call the API endpoint to update document information.

<span id="4311c46e"></span>
# **Request endpoint**


|**URI** |/api/knowledge/doc/update_meta |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="491921df"></span>
# **Request parameters**


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|collection_name |\-\- |string |No |\-\- |**Knowledge base name** |
|project |\-\- |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under the specified project, this field must be configured correctly.</div><br> |
|resource_id |\-\- |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier for the knowledge base. |
|doc_id |\-\- |string |Yes |\-\- |**ID of the document to be updated** |
|meta | |array or JSON string corresponding to the array |No |\-\- |**Meta information** |
| |field_name |string |No |\-\- |**Name of the field to be updated** |
| |field_type |string |No |\-\- |**Type of the field to be updated**<br><br><br>* Effective only when adding a label field that has not been configured in the knowledge base. The newly added field cannot be used for scalar filtering and can only be stored as descriptive information for the current document.<br><br>* Supports types such as "int64", "float32", "string", "bool", "list", and more. |
| |field_value |Consistent with the type specified by field_type |No |\-\- |**Value of the field to be updated**<br><br>The field value must ensure that the type matches the field definition, such as "int64", "float32", "string", and so on. |
|pipeline_name |\-\- |string |No |\-\- |**Experimental version name**<br><br><br>* If not specified, document information in the primary version of the knowledge base is updated by default.<br><br>* If specified, document information in the specified experimental version is updated. |


<span id="5965c4a3"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |


<span id="94bbf930"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |
|1001001 |400 |doc not exist |Document does not exist |


<span id="c2bfa30a"></span>
# Complete example

<span id="5509cb33"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/doc/update_meta \
  -d '{
    "collection_name": "test_collection_name",
    "project": "",
    "doc_id": "test123",
    "meta": [
      {"field_name": "industry", "field_type": "string", "field_value": "Enterprise Services"},
      {"field_name": "is_public", "field_type": "bool", "field_value": true}
    ]
  }'
```


<span id="fe6d72c7"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failed execution:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
