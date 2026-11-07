---
title: "info"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/point_info"
---

<span id="c6970127"></span>
# Overview

The `/api/knowledge/point/info` endpoint is used to view information about a specified chunk in the knowledge base or under a particular experiment version.

> By specifying pipeline_name, you can view information about chunks under a specific experiment version in the knowledge base.


<span id="32f9233d"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature retrieval on the 'Signature Authentication Method' page, you can call the API endpoint to view information about a specified chunk in the knowledge base.

<span id="499c37e2"></span>
# **Request endpoint**


|**URI** |/api/knowledge/point/info |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Operation type requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="6fc75b44"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique knowledge base ID**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier for the knowledge base. |
|point_id |string |Yes |\-\- |**Unique chunk ID** |
|get_attachment_link |bool |No |False |**Whether to obtain a temporary download link for images in the chunk**<br><br>Valid for 10 minutes |
|pipeline_name |string |No |\-\- |**Experiment version name**<br><br><br>* Specifying this parameter allows querying chunk information under a specific experiment version.<br><br>* If not specified, chunk information under the primary version of the knowledge base is queried by default. |


<span id="a1f9406d"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |Returned content |


data return value


|Field |Subfield |Field type |Description |
|---|---|---|---|
|collection_name |\-\- |string |Knowledge base name |
|point_id |\-\- |string |Unique chunk ID |
|doc_info |\-\- |list | |
| |doc_id |string |ID of the associated document |
| |doc_name |string |Document name |
| |create_time |int |Time when the document was created |
| |doc_type |string |Document type |
| |doc_meta |string |Document meta information |
| |source |string |Document import source |
|process_time |\-\- |int |Time when knowledge processing was completed |
|chunk_title |\-\- |string |The parent title of this text chunk, which is the previous\-level title identified by the parsing model. If there is no previous\-level title, this field is empty. |
|chunk_type |\-\- |string |**Chunk type**<br><br>Some return value types include: doc\-image, image, table, text, structured, FAQ, mixed\-table, and more. |
|description |\-\- |string |**Document description**<br><br>Note:<br><br><br>* Note: Currently, **only supported** when doc_type is **an image\-type document**; settings for other document types are invalid.<br><br>* Length [0, 4000] |
|content |\-\- |string |Chunk content<br><br><br>1. Unstructured file: content returns the original text of the chunk<br><br>2. FAQ file: content returns the content of the answer field<br><br>3. Structured file: content returns the fields and values involved in indexing, concatenated as K:V pairs and separated by \n |
|md_content |\-\- |string |Parsing result in markdown format<br><br>For table chunks in unstructured documents, an additional parsing result in markdown format can be returned to retain more original table information<br><br>Table chunks can be identified by chunk_type == table |
|html_content |\-\- |string |Parsing result in HTML format<br><br>For table chunks in unstructured documents, an additional parsing result in HTML format can be returned to retain more original table information<br><br>Table chunks can be identified by chunk_type == table |
|chunk_id |\-\- |int |The sequential position of the chunk in the original document |
|table_chunk_fields |\-\- |list |Structured data retrieval returns all data for a single row |
|chunk_attachment |\-\- |list |Retrieves attachments recalled during search; valid when chunk_type is image |
|update_time |\-\- |int |Update time |
|original_coordinate |\-\- |\-\- |Original coordinate information of the knowledge point; only supported for PDF and PPT documents |
||page_no |list |Pages containing the coordinates of the knowledge point |
||bbox |list<list\> |Bounding box coordinates of the knowledge point on the original page |
|chunk_source |\-\- |string |Chunk source<br><br>Originates from document parsing chunk or manually added chunk; the corresponding values are document and user, respectively |


chunk_attachment return value


|Field |Field type |Description |
|---|---|---|
|uuid |string |Unique identifier of the attachment |
|caption |string |Title to which the image belongs; if no title is recognized, the value is "\n" |
|type |string |image, mixed\-table, table, and more |
|link |string |When "get_attachment_link" == True, returns a temporary download link for the extracted image frame or images contained in the table; valid for 10 minutes |


<span id="2a0b5890"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request：%s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |
|1001001 |400 |doc not exist |Document does not exist |
|1002001 |400 |point not exist |point_id does not exist |


<span id="4be82583"></span>
# Complete example

<span id="87d81c62"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/point/info \
  -d '{
    "resource_id": "xxx",
    "point_id": "_sys_auto_gen_doc_id-29175896809570851-0"
}'
```


<span id="65dd9082"></span>
## Response message

Return on successful execution:

```JSON
{
    "code":0,
    "data":{
        "collection_name":"test",
        "point_id":"_sys_auto_gen_doc_id-29175896809570851-0",
        "process_time":1731054363,
        "content":"a:4\nb:5\nc:6",
        "chunk_id":0,
        "doc_info":{
            "doc_id":"_sys_auto_gen_doc_id-29175896809570851",
            "doc_name":"table_case",
            "create_time":1731054262,
            "doc_type":"table",
            "doc_meta":"[{\"field_name\":\"doc_id\",\"field_type\":\"string\",\"field_value\":\"_sys_auto_gen_doc_id-291758968095705851\"}]",
            "source":"url"
            },
        "chunk_type":"structured",
        "table_chunk_fields":[{"field_name":"a","field_value":"4"},{"field_name":"b","field_value":"5"},{"field_name":"c","field_value":"6"}]
        },
    "message":"success",
    "request_id":"02173217505951900000000000000000000ffff0a00787e6d6662"
}
```


Return on failed execution:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
