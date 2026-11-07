---
title: "delete"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/point_delete"
---

<span id="0bb37fed"></span>
# **Overview**

To delete a specific data slice from a knowledge base, you can use the `/api/knowledge/point/delete` endpoint. This API allows you to remove a slice from either the primary version or a specified experiment version of the knowledge base by providing its point_id.

> By specifying pipeline_name, you can delete a slice within a specified experiment version under the knowledge base.


<span id="5395592a"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page, you can call the API to delete a specific slice under a knowledge base.

<span id="fa37f0b6"></span>
# **Request endpoint**


|**URI** |/api/knowledge/point/delete |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="1cf0412e"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Remarks** |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Knowledge base name**<br><br><br>* Only English letters, digits, and underscores (_) are allowed. The name must start with an English letter and cannot be empty<br><br>* Length requirement: [1, 64] |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, the operation targets a knowledge base in the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate on a knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique ID of the knowledge base**<br><br><br>* You can choose to pass resource_id directly, or pass both collection_name and project together as the unique identifier for the knowledge base. |
|point_id |string |Yes |\-\- |**ID of the slice to be deleted** |
|pipeline_name |string |No |\-\- |**Experiment version name**<br><br><br>* Specifying this parameter allows deletion of a slice under a specific experiment version.<br><br>* If not specified, the slice is deleted from the primary version of the knowledge base by default. |


<span id="45a275f0"></span>
# **Response message**


|Field |Remarks |
|---|---|
|code |Status code |
|message |Response message |
|request_id |Unique identifier for each request |


<span id="440f9e82"></span>
# **Complete example**

<span id="0c83896f"></span>
## Request message

```Shell
curl -i -X POST \ 
  -H 'Content-Type: application/json' \ 
  -H 'Authorization: HMAC-SHA256 ***' \ 
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/point/delete \ 
  -d '{ 
    "resource_id": "kb_xxxxxx", 
    "point_id": "_sys_xxxxx"
}'
```


<span id="6701689d"></span>
## Response message

Successful response:

```JSON
HTTP/1.1 200 OK 
Content-Length: 43 
Content-Type: application/json 
  
{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Failed response:

```Plain
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request: <reason>", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
