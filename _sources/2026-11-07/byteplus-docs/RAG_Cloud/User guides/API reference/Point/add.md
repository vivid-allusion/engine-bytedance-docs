---
title: "add"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/add"
---

<span id="f158c074"></span>
# **Overview**

The `/api/knowledge/point/add` endpoint is used to add a chunk to a knowledge base or to a document under a specific experimental version.

> By specifying pipeline_name, you can add a chunk to a specified experimental version within the knowledge base.


<span id="67b9d318"></span>
# **Prerequisites**

After completing account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page, you can call the API to add a chunk to a document under a knowledge base.

<span id="74857c2d"></span>
# **Request endpoint**


|**URI** |/api/knowledge/point/add |Uniform Resource Identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="211fab95"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Remarks** |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Name of the knowledge base** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique ID of the knowledge base**<br><br><br>* You can choose to pass resource_id directly, or pass both collection_name and project to uniquely identify the knowledge base. |
|doc_id |string |Yes |\-\- |**Indicates the document to which the new chunk belongs**<br><br><br>* An error will be reported if it does not exist. |
|chunk_type |string |Yes |\-\- |**Type of chunk to add**<br><br><br>* An error will be reported if the chunk type does not match the types supported by the knowledge base.<br><br>* Structured knowledge base: "structured",<br><br>* Unstructured knowledge base:<br><br>   * "text": plain text chunk<br><br>   * "faq": FAQ chunk |
|content |string ||\-\- |**Text content of the new chunk**<br><br>Required when chunk_type is text or faq<br><br><br>1. text: content corresponds to the original text of the chunk<br><br>2. faq: content corresponds to the content of the **answer field** |
|chunk_title |string |No |\-\- |**Chunk title**<br><br>Only unstructured documents support modifying the chunk title. |
|question |string |No |\-\- |**The question field in the new FAQ chunk**<br><br>Required when chunk_type is faq<br><br><br>* The length of this field must be between 1 and {maximum length supported by the Embedding model}. |
|fields |list |No |\-\- |**Represents the structured data passed in**<br><br>Required when chunk_type is structured.<br><br>[<br><br>{ "field_name": "xxx" // Field name<br><br>"field_value": xxxx // Field value<br><br>},<br><br>]<br><br><br>* field_name must be configured in the table fields of the corresponding knowledge base, otherwise an error will be reported<br><br>* After concatenation, the text length for embedding must not exceed 65535, consistent with the vector field length check during document import. |
|pipeline_name |string |No |\-\- |**Name of the experimental version**<br><br><br>* Specifying this parameter allows adding a chunk to a specific experimental version<br><br>* If not specified, new chunks are added by default under the main version of the knowledge base |


<span id="c3e9c215"></span>
# **Response message**


|**Field** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |{<br><br>"collection_name": Name of the knowledge base,<br><br>"resource_id": Unique identifier of the knowledge base,<br><br>"project": Project name,<br><br>"doc_id": Document ID,<br><br>"chunk_id": Integer, ID of the chunk under the document, unique within the document,<br><br>"point_id": Chunk ID, unique within the knowledge base<br><br>} |


<span id="2ed6a8da"></span>
# **Complete example**

<span id="4acd8055"></span>
## Request message

```Shell
curl -i -X POST \ 
  -H 'Content-Type: application/json' \ 
  -H 'Authorization: HMAC-SHA256 ***' \ 
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/point/add \ 
  -d '{ 
    "resource_id": "kb_XXX", 
    "doc_id": "_sys_XXXX",
    "chunk_type": "text",
    "content": "test content"
}'
```


<span id="da707c14"></span>
## Response message

Returned on successful execution:

```JSON
HTTP/1.1 200 OK 
Content-Length: 43 
Content-Type: application/json 
  
{
    "code": 0,
    "data": {
        "collection_name": "lzm_test2",
        "project": "default",
        "resource_id": "kb-a638e4045e9708f0",
        "doc_id": "_sys_auto_gen_doc_id-9744689384778553745",
        "chunk_id": 7,
        "point_id": "_sys_auto_gen_doc_id-9744689384778553745-7"
    },
    "message": "success",
    "request_id": "02173431739184000000000000000000000ffff0a0078dc15a2fe"
}
```


Returned on failed execution:

```Plain
HTTP/1.1 400 OK 
Content-Length: 43 
Content-Type: application/json 
  
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"} 
```
