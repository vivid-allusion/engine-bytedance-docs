---
title: "update"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/pipeline_update"
---

The `api/knowledge/pipeline/update` is used to modify experimental version configuration.

<span id="d8d1db68"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, AK/SK key acquisition, and signature retrieval on the "Signature authentication method" page, you can call the API to update experimental version information.

<span id="5692d18f"></span>
# **Request endpoint**


|**URI** |/api/knowledge/pipeline/update |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="f84ab534"></span>
# **Request parameters**


|Parameter |Type |Required |Default value |Remarks |
|---|---|---|---|---|
|collection_name |string |No |*  |**Knowledge base name** |
|project |string |No |default |**Project name** |
|resource_id |string |No |*  |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both name and project as the unique identifier for the knowledge base |
|name |string |Yes |*  |**Experimental version name**<br><br><br>* Cannot use the existing system default value "default"<br><br>* The experimental version name must consist of letters, numbers, and underscores, and can only begin with a letter<br><br>* Length must not exceed 32 characters |
|cpu_quota |int |No |*  |**CPU quota** |
|auto_sync_doc |bool |No |*  |**Whether to automatically synchronize newly added documents**<br><br>When enabled, documents uploaded to the knowledge base via the add_doc API are automatically synchronized to the current experimental version |


<span id="9ba9beaa"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return information |


<span id="8f6728c7"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |403 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter<br><br><br>* Missing required parameter<br><br>* Collection naming does not conform to specifications<br><br>* Field type and related field attributes do not meet constraint conditions |


<span id="c69448ae"></span>
# Complete example

<span id="e08f5d8c"></span>
## Request message

```Shell
curl -i -X POST \
-H 'Content-Type: application/json' \
-H 'Authorization: token=****' \
https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/pipeline/update \
-d '{
  "collection_name": "test_collection_name",
  "project": "default",
  "name": "custom_pipeline_01",
  "cpu_quota": 2,
  "auto_sync_doc": true
}'
```


<span id="c8efdfbe"></span>
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
