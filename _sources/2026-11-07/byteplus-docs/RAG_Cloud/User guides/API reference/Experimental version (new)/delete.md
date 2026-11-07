---
title: "delete"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/pipeline_delete"
---

The `api/knowledge/pipeline/delete` endpoint is used to delete an experimental version.

<span id="9cae6bd9"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, AK/SK key acquisition, and signature retrieval on the 'Signature Authentication Method' page, you can call the API endpoint to delete a specific experimental version.

<span id="73d1466a"></span>
# **Request endpoint**


|**URI** |/api/knowledge/pipeline/delete |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="2ed980ae"></span>
# **Request parameters**


|Parameter |Type |Required |Default value |Remarks |
|---|---|---|---|---|
|collection_name |string |No |*  |**Knowledge base name** |
|project |string |No |default |**Project** |
|resource_id |string |No |*  |**Unique knowledge base ID**<br><br><br>* You can choose to directly pass resource_id, or pass both name and project as the unique identifier for the knowledge base. |
|name |string |Yes |*  |**Experimental version name**<br><br><br>* Cannot use the system's existing default value.<br><br>* Must consist of letters, numbers, and underscores, and can only begin with a letter.<br><br>* Length must not exceed 32 characters. |


<span id="beac0da0"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |


<span id="f6359f9f"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* Collection naming does not conform to specifications<br><br>* Field type and related field attributes do not meet constraint conditions |


<span id="1e61f75d"></span>
# Complete example

<span id="4aa26e25"></span>
## Request message

```Shell
curl -i -X POST \
-H 'Content-Type: application/json' \
-H 'Authorization: token=****' \
https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/pipeline/delete \
-d '{
"collection_name": "test_collection_name",
"project": "default",
"name": "custom_pipeline_01"
}'
```


<span id="bdc6d5d3"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 78
Content-Type: application/json

{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failed execution:

```Shell
HTTP/1.1 400 Bad Request
Content-Length: 120
Content-Type: application/json

{
"code": 1000003,
"message": "invalid request: cannot delete default pipeline",
"request_id": "021695029757920fd001de6666600000000000000000002569b8f"
}
```
