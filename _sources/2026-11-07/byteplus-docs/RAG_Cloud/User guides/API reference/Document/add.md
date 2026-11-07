---
title: "add"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/doc_add"
---

<span id="6e2d83b2"></span>
# Overview

To add documents to a knowledge base, you can use the `/api/knowledge/doc/add` endpoint. This reference details all required request parameters, response formats, status codes, and provides a complete code example to guide your implementation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Refer to document type restrictions <a href="https://docs.byteplus.com/docs/209/Knowledge_base_quota_description">Knowledge base quota description</a></div>



<span id="21262b88"></span>
# **Prerequisites**

Before calling this endpoint, you must complete account registration, identity verification, and AK/SK key acquisition. You must also generate a signature as described on the "Signature Authentication Method" page.

<span id="f1b98caa"></span>
# **Request endpoint**


|**URI** |/api/knowledge/doc/add |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client from the vector database server. |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="63abb990"></span>
# **Request parameters**


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|collection_name |\-\- |string |No |\-\- |**Name of the knowledge base** |
|project |\-\- |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under a specified project, this field must be configured correctly.</div><br> |
|resource_id |\-\- |string |No |\-\- |**Unique ID of the knowledge base**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier of the knowledge base. |
|add_type |\-\- |string |Yes |\-\- |**Method for adding documents**, can be one of the following enumerated values:<br><br><br>* url: Provides a publicly downloadable URL.<br><br>* tos: Authorized directory in tos, currently only supported in North China region |
|doc_id |\-\- |string |No |\-\- |**Unique identifier of the document in the knowledge base**<br><br><br>* Only English letters, digits, and underscores _ are allowed, must start with an English letter or underscore, and cannot be empty<br><br>* Length requirement: [1, 128]<br><br><br>Note:<br><br><br>* When uploading multiple times, duplicate doc_id values will be overwritten<br><br>* This field is required when "add_type" == "url"<br><br>* This field is invalid when "add_type" == "tos"; the system will automatically obtain it from the "x\-tos\-meta\-doc_id" of the tos file |
|doc_name |\-\- |string |No |\-\- |**Document name**<br><br><br>* Length requirement: [1, 256]<br><br>* This field is required when "add_type" == "url"<br><br>* This field is invalid when "add_type" == "tos"; the system will automatically obtain it from tos, using the file name as doc_name |
|doc_type |\-\- |string |No |\-\- |**Type of document to be uploaded**<br><br><br>* Supported types for unstructured documents: txt, doc, docx, pdf, markdown, pptx, ppt, jpeg, png, webp, bmp;<br><br><br> *(For .jpg and .jpeg files, doc_type is jpeg)* <br><br><br>* Supported types for structured documents: xlsx, csv, jsonl<br><br><br>Note:<br><br><br>* This field is required when add_type is "url"<br><br>* This field is invalid when add_type is "tos"; the system will automatically obtain it from the file extension of the tos file |
|description |\-\- |string |No |\-\- |**Document description**<br><br>The description is used during image retrieval. For example, in e\-commerce scenarios, the description can be used to store detailed product information corresponding to the image, selling points, price, and more.<br><br>Note:<br><br><br>* Currently, **only supported when** doc_type is **an image\-type document**; for other document types, this setting is invalid.<br><br>* Length [0, 4000] |
|tos_path |\-\- |string |No |\-\- |**TOS directory or specified file path to be uploaded**<br><br>Authorization must be completed on the `*Console/Upload Document/TOS Upload*` page. This field is required only when "add_type" == "tos".<br><br><br>* Correct examples:<br><br>   * `tos_path="your_tos/path/"`<br><br>   * `tos_path="your_tos/path/xxx.pdf"`<br><br>* Incorrect examples:<br><br>   * `tos_path="tos://your_tos/path/"`<br><br>   * `tos_path="tos://your_tos/path/xxx.pdf"`<br><br><br>Note:<br><br><br>* Documents imported from a directory are imported only once. Subsequent changes to documents in the directory will not be automatically synchronized to the knowledge base.<br><br>* When importing a directory, only files in the current directory are scanned; subdirectories are not checked recursively.<br><br>* If the doc_id values of documents in the TOS directory are duplicated, only the last uploaded document will be retained in the knowledge base, that is, doc_id must be unique.<br><br>* There are two ways to handle changes to the contents of files in the directory:<br><br>   * Single file update: Import via URL and specify the doc_id of the document to be replaced; this method is relatively fast.<br><br>   * Batch update: Import the TOS directory again. This method will check for changes in all documents in the directory and replace the old documents with the new versions. This method takes longer because file verification is required.<br><br>* For file size limits, refer to: [Knowledge base quota description](https://docs.byteplus.com/docs/209/Knowledge_base_quota_description) |
|url |\-\- |string |No |\-\- |**URL link of the file to be uploaded**<br><br>This field is required only when "add_type" == "url". The field length range is [1, 1024].<br><br><br>* For file size limits, refer to: [Knowledge base quota description](https://docs.byteplus.com/docs/209/Knowledge_base_quota_description) |
|**meta** | |array or JSON string corresponding to the array |No |\-\- |**Tag information**<br><br><br>* This field is valid when "add_type" is "url".<br><br>* This field is invalid when "add_type" == "tos". The system will automatically obtain the file metadata on TOS. In the [Object Storage Console](https://console.byteplus.com/tos/bucket?projectName=default), you can specify metadata information for the document by setting the parameter type to "x\-tos\-meta\-", the parameter name as the tag name, and the parameter value as the tag value. Due to the type restriction of x\-tos\-meta\-\*, the tag value field type can only be **string** at this time. |
| |field_name |string |No |\-\- |**Tag name**<br><br><br>* Cannot be "doc_id"<br><br>* Must match a field_name defined when the knowledge base was created.<br><br>   * When creating a knowledge base, you must first initialize the tag index, and then assign tags when uploading documents, so that tag filtering capability can be enabled during retrieval.<br><br>   * To add new filter tags, edit the knowledge base to add tags first, and then assign tags to documents. |
| |field_type |string |No |\-\- |**Tag type**<br><br><br>* Supports "int64", "float32", "string", "bool", "list<string\>", "list<int64\>" types.<br><br>* Must be consistent with the field_type when creating the knowledge base. |
| |field_value |Consistent with the type specified by field_type. |No |\-\- |**Tag value** |
|**dedup** | | |No |\-\- |If any sub\-parameter is set to true, deduplication is required. If there are no duplicate documents in the database, the document will be imported as a new document.<br><br>When both **content_dedup** and **doc_name_dedup** are **true** :<br><br>(C and D represent the number of documents in the database with the same content and the same doc name, respectively.)<br><br><br>* C + D = 0: Import as a new document.<br><br>* C + D = 1: The handling strategy depends on the value of the auto_skip parameter.<br><br>* C = 1, D = 1, and C and D refer to the same document: Return the duplicate document ID and error code.<br><br>* In other cases, return the corresponding document list and instructs the user to resolve duplicates before re\-importing.<br><br><br>Note: Only content and doc name are checked. Changes to other information are not checked. Overwriting or importing as a new document is determined according to the above criteria. |
| |content_dedup |bool |No |false |**Content deduplication**<br><br>Overwrites documents with the same content. In this case, documents with the same doc hash in the database are searched, and the number found is C. When **content_dedup** is **true** and **doc_name_dedup** is **false** :<br><br><br>* C = 0: Import as a new document. For rules, refer to the dedup explanation.<br><br>* C = 1: Different handling strategies are provided according to the auto_skip parameter configuration.<br><br>* C \> 1: An error message is displayed. |
| |doc_name_dedup |bool |No |false |**Document name deduplication**<br><br>Overwrites documents with the same doc name. In this case, documents with the same doc name in the database are searched, and the number found is D. When **doc_name_dedup** is **true** and **content_dedup** is **false**:<br><br><br>* D = 0: Import as a new document. For rules, refer to the dedup explanation.<br><br>* D = 1: Different handling strategies are provided according to the auto_skip parameter configuration.<br><br>* D \> 1: An error message is displayed. |
| |auto_skip |bool |No |false |**Duplicate document handling strategy**<br><br>When the auto_skip parameter is set to true, the system will automatically skip duplicate documents and return the original document ID. When the auto_skip parameter is set to false, the duplicate document is overwritten, and its doc_id is returned. |


<span id="1566dd0a"></span>
# **Response message**


|**Parameter** |**Parameter description** |**Remarks** |
|---|---|---|
|code |Status code | |
|message |Return message | |
|request_id |Unique identifier for each request | |
|data |{<br><br>"collection_name": Name of the knowledge base,<br><br>"resource_id": Unique identifier of the knowledge base,<br><br>"project": Project name,<br><br>"doc_id": Document unique identifier,<br><br>"dedup_info": { // This parameter is returned when any dedup sub\-parameter is true<br><br>"skip": true,<br><br>"same_doc_ids":[ ]<br><br>}<br><br>} | |


<span id="354b075a"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |
|1000005 |400 |The specified collection does not exist. |Collection does not exist |
|1001010 |400 |The number of documents exceeds the limit. |The number of documents has reached the limit. Click to view details [Knowledge base quota description](https://docs.byteplus.com/docs/209/Knowledge_base_quota_description) |


<span id="9e5d8994"></span>
# Complete example

<span id="b8c56a8b"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/doc/add \
  -d '{
    "collection_name": "test_collection_name",
    "project": "default",
    "add_type": "url",
    "doc_id": "test0123",
    "doc_name": "xxx",
    "doc_type": "pdf",
    "url": "xxx",
    "meta":[
    {"field_name":"industry","field_type":"string", "field_value":"Enterprise Services"},
    {"field_name":"is_public","field_type":"bool", "field_value":true}
    ]
}'
```


<span id="fe4becfa"></span>
## Response message

Return on successful execution:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "request_id":"021695029537650fd001de666660000000000000000000230da93",
    "data":{
        "collection_name": "xxx",
        "resource_id": "kb-8349ef57441ab57",
        "project": "default",
        "doc_id": "_sys_auto_gen_doc_id-17691607628519396693"
        }
}
```


Return on failed execution:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request: %s", 
"request_id": "021695029757920fd001de6666600"000000000000000002569b8f"}
```
