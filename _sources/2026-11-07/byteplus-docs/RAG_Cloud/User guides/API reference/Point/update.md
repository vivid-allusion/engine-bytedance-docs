---
title: "update"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/point_update"
---

<span id="26f12174"></span>
# **Overview**

The `/api/knowledge/point/update` endpoint is used to update the content of a slice in the knowledge base or under a specific experimental version

> Supports updating slice content within a specific experimental version by specifying the pipeline_name parameter.


<span id="d04d4d91"></span>
# **Prerequisites**

Before calling this API endpoint, you must register an account, complete real\-name authentication, acquire your AK/SK keys, and retrieve your signature from the "Signature Authentication Method" page.

<span id="f509173c"></span>
# **Request endpoint**


|URI |/api/knowledge/point/update |Uniform resource identifier |
|---|---|---|
|Request method |POST |Operation type requested by the client to the vector database server |
|Request headers |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="a738779b"></span>
# **Request parameters**


|Parameter |Type |Required |Default value |Remarks |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, the operation applies to the knowledge base in the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To update a knowledge base in a specified project, this field must be correctly configured.</div><br> |
|resource_id |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier of the knowledge base |
|point_id |string |Yes |\-\- |**ID of the slice to be updated** |
|chunk_title |string |No |\-\- |**Slice title**<br><br>Only unstructured documents support modifying the title of a slice. |
|content |string |Provide either content or fields, but not both. |\-\- |**Content of the slice in the unstructured document to be updated**<br><br><br>* Unstructured file: content corresponds to the original text of the slice<br><br>* FAQ file: content corresponds to the answer field<br><br>* Structured file: content corresponds to the indexed fields and values, concatenated as 'Key:Value' pairs and separated by \n. |
|fields |list ||\-\- |**Content of the slice in the structured document to be updated**<br><br>Full update of one row of data<br><br>[<br><br>{ "field_name": "xxx" // Field name<br><br>"field_value": xxxx // Field value<br><br>},<br><br>]<br><br>The field_name must be configured in the fields of the corresponding knowledge base; otherwise, an error will occur |
|question |string |No |\-\- |**Question field of the slice in the unstructured FAQ document to be updated** |
|pipeline_name |string |No |\-\- |**Experimental version name**<br><br><br>* Specifying this parameter allows updating slices under a specific experimental version<br><br>* If not specified, slices under the primary version of the knowledge base are updated by default |


<span id="a07fab59"></span>
# **Response message**


|Field |Remarks |
|---|---|
|code |Status code |
|message |Description |
|request_id |Unique identifier for each request |


<span id="3ac4e800"></span>
## **Status code description**


|code |message |Remarks |http status_code |
|---|---|---|---|
|0 |success |Success |200 |
|1000001 |unauthorized |Missing authentication information |401 |
|1000002 |no permission |Insufficient permissions |403 |
|1000003 |invalid request：%s |Invalid parameter |400 |
|1000005 |collection not exist |Collection does not exist |400 |


<span id="e4976fdb"></span>
# **Complete example**

<span id="73cceca0"></span>
## Request message

```Shell
curl -i -X POST \ 
  -H 'Content-Type: application/json' \ 
  -H 'Authorization: HMAC-SHA256 ***' \ 
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/point/update \ 
  -d '{ 
    "resource_id": "kb_xxxxx", 
    "point_id": "_sys_xxxx",
    "content": "test content" 
}'
```


<span id="1a3f5494"></span>
## Response message

Return on successful execution:

```JSON
HTTP/1.1 200 OK 
Content-Length: 43 
Content-Type: application/json 
  
{"code":0,"message":"success","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```


Return on failed execution:

```JSON
HTTP/1.1 400 OK 
Content-Length: 43 
Content-Type: application/json 
  
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"} 
```
