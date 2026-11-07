---
title: "update"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/doc_update"
---

<span id="fa28e54d"></span>
# Overview

The `/api/knowledge/doc/update` endpoint is used to update information for a document, such as the document title. Updating document information will automatically trigger data updates in the index.

<span id="1e40ffce"></span>
# **Prerequisites**

To update document information, complete account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page, then call the API.

<span id="1f719e85"></span>
# **Request endpoint**


|**URI** |/api/knowledge/doc/update |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client from the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="d3633eee"></span>
# **Request parameters**


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|collection_name |\-\- |string |No |\-\- |**Name of the knowledge base** |
|project |\-\- |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |\-\- |string |No |\-\- |**Unique ID of the knowledge base**<br><br>Specify resource_id directly, or specify both collection_name and project as the unique identifier of the knowledge base. |
|doc_id |\-\- |string |Yes |\-\- |**ID of the document to be updated** |
|doc_name |\-\- |string |Yes |\-\- |**Updated document name.**  |


<span id="bdf6ea56"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |```JSON```<br>```{```<br>```    "doc_id": "1234567890",```<br>```    "doc_name": "Updated Document Name.docx", // Other updated document-related information```<br>```}```<br> |


<span id="b12c0720"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |
|1001001 |400 |doc not exist |Document does not exist |
|1000028 |500 |internal error |Internal error |


<span id="70af546e"></span>
# Complete example

```JSON
{
    "message": "success",
    "code": 200, // Assuming errorhandlers.VolcanoOK is 200
    "request_id": "abc1234567890",
    "data": {
        "doc_id": "1234567890",
        "doc_name": "Updated Document Name.docx", // Other updated document-related information
    }
}
```
