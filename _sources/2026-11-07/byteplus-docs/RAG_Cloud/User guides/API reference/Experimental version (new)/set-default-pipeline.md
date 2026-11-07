---
title: "set-default-pipeline"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/set-default-pipeline"
---

<span id="e25569ad"></span>
# Overview

To promote a tested, experimental knowledge base pipeline to the official production version, use the `api/knowledge/collection/set-default-pipeline` endpoint. This API reference provides the necessary parameters and prerequisites for this operation, which is intended for frontend calls only.

**Prerequisites**


1. After completing account registration, identity verification, AK/SK key acquisition, and signature retrieval on the 'Signature Authentication Method' page, you can call this API endpoint.

2. **The number of documents in the experimental version must match that of the official version before it can be set as the official version.** 


<span id="f5b4ff1c"></span>
# **Request endpoint**


|**URI** |/api/knowledge/collection/set\-default\-pipeline |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: token=\*\*\*\*\*\*\*\*\*\* |Authentication |


<span id="ea00e437"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|name |string |No | |**Knowledge base name** |
|project |string |No |default |**Name of the project to which the knowledge base belongs** |
|resource_id |string |No | |**Unique ID of the knowledge base**<br><br>You can choose to pass resource_id directly, or pass both name and project as the unique identifier of the knowledge base |
|new_default_pipeline_name |string |Yes | |The name of the experimental version to set as the official version. |
|old_pipeline_name |string |No | |A new name for the original official version.<br><br><br>* The new name cannot be set to the system default value "default"<br><br>* The experimental version name must consist of letters, numbers, and underscores, and can only begin with a letter<br><br>* Length must not exceed 128 characters |


<span id="d1df14bf"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Description |


<span id="17cf811e"></span>
## **Status code description**


|**Status code** |**Return information** |**Status code description** |
|---|---|---|
|0 |success |Success |
|1000001 |unauthorized |Authentication failed |
|1000002 |no permission |Insufficient permissions |
|1000003 |invalid request: %s |**Invalid parameter**<br><br><br>* Missing required parameter<br><br>* Collection name does not conform to the specification<br><br>* The field type and its attributes do not meet the constraints. |
