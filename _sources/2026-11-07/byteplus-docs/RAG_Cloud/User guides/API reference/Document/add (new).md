---
title: "add (new)"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/add_new"
---

<span id="fb29ef65"></span>
# Overview

The /api/knowledge/doc/v2/add API allows you to add documents to an existing knowledge base. This endpoint features a simplified interface and uses a unified `uri` parameter to specify the document source from either a URL or a TOS path. It also supports setting tags when importing files and includes built\-in content deduplication to prevent duplicate entries.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For document type restrictions, refer to <a href="https://docs.byteplus.com/docs/RAG_Cloud/Knowledge_base_quota_description">Knowledge base quota description</a></div>


* <div data-tips="true" data-tips-type="tip">Improvements to the doc/v2/add API</div>


   * <div data-tips="true" data-tips-type="tip">Simplified interface parameters to improve usability</div>


   * <div data-tips="true" data-tips-type="tip">Unified use of the <code>uri</code> parameter to specify the document source (supports URL or TOS path)</div>


   * <div data-tips="true" data-tips-type="tip">Supports setting tag information when importing files via TOS</div>


   * <div data-tips="true" data-tips-type="tip">Adopts a unified content deduplication rule. No additional configuration is required. An error will be reported if a duplicate document is detected.</div>



<span id="9e448cb4"></span>
# **Prerequisites**

After completing account registration, identity verification, AK/SK key acquisition, and signature acquisition on the "Signature Authentication Method" page, you can call the API to import documents into the knowledge base.

<span id="794028fc"></span>
# **Request API**


|**URI** |/api/knowledge/doc/v2/add |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="a6247fd0"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|collection_name |string |No |\-\- |Knowledge base name |
|project |string |No |default |Project to which the knowledge base belongs<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate the knowledge base under a specified project, this field must be configured correctly</div><br> |
|resource_id |string |No |\-\- |**Unique ID of the knowledge base**<br><br>You can choose to pass resource_id directly, or pass both collection_name and project as the unique identifier of the knowledge base. |
|doc_id |string |Yes |\-\- |**Unique identifier of the document in the knowledge base**<br><br><br>* Only English letters, digits, and underscores (_) are allowed. It must start with a letter or underscore and cannot be empty.<br><br>* Length requirement: [1, 128] |
|doc_name |string |No |\-\- |**Document name**<br><br><br>* For TOS import, if not provided, the document name under the TOS path is used directly.<br><br>* For URL import, the document name with a suffix is extracted from the URL. If not available, error code 400 is returned, and the user is required to provide doc_name.<br><br><br>Format requirements:<br><br><br>* Cannot contain special\-purpose characters (< \> : " / \<br><br>* Length requirement: [1, 255] |
|doc_type |string |No |\-\- |**Type of document to upload**<br><br><br>* Supported unstructured document types: txt, doc, docx, pdf, markdown, pptx, ppt, jpeg, png, webp, bmp, mp4, mp3, wav, aac, flac, ogg<br><br>   * For .jpg and .jpeg files, doc_type is jpeg<br><br>   * For .markdown and .md files, doc_type is markdown<br><br>* Supported structured document types: xlsx, csv, jsonl<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The provided value is used first. If a value is not provided, the system attempts to extract it automatically. If automatic extraction fails, the interface returns an error.</div><br> |
|description |string |No |\-\- |**Document description**<br><br>The description is used in image retrieval. For example, in e\-commerce scenarios, the description can be used to store detailed product information corresponding to the image, selling points, price, and more.<br><br>Note:<br><br><br>* This is currently supported only when doc_type is an image\-type document; settings for other document types are invalid.<br><br>* Length [0, 4000] |
|tag_list |list |No |\-\- |Tag is a struct and includes:<br><br><br>* field_name: Tag name, type is string<br><br>   * Cannot be "doc_id"<br><br>   * Must align with the field_name specified when creating the knowledge base<br><br>      * Initialize the tag index when creating the knowledge base, then apply tags when uploading documents to enable tag filtering during retrieval<br><br>      * To add new filtering tags, edit the knowledge base to add tags first, then tag the documents<br><br>* field_type: Tag type<br><br>   * Supports "int64", "float32", "string", "bool", "list", "list", "date_time", and "geo_point" types<br><br>   * Must align with the field_type specified when creating the knowledge base<br><br>* field_value: Tag value<br><br>   * Must match the type specified by field_type |
|uri |string |Yes |\-\- |URI of the file to be uploaded, for example:<br><br><br>* http://a/b/c.pdf<br><br>* tos://a/b/c.pdf |


<span id="9338bedc"></span>
# **Response message**


|**Parameter** |**Parameter description** |**Remarks** |
|---|---|---|
|code |Status code | |
|message |Return information | |
|request_id |Unique identifier for each request | |
|data |{<br><br>"collection_name": Name of the knowledge base,<br><br>"resource_id": Unique identifier of the knowledge base,<br><br>"project": Project name,<br><br>"doc_id": Unique identifier of the document<br><br>} | |


<span id="e474aec5"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |
|1001002 |400 |invalid request: doc_id:xxx is duplicated with doc_ids:xxx |The document content is duplicated with an existing document |
|1001010 |400 |doc num is exceed 3000000 |The number of documents has reached the limit. For more information, see [Knowledge base quota description](https://docs.byteplus.com/docs/RAG_Cloud/Knowledge_base_quota_description) |


<span id="27e77518"></span>
# Complete example

<span id="df21f314"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/doc/v2/add \
  -d '{
    "collection_name": "test_collection_name",
    "project": "default",
    "doc_id": "test0123",
    "doc_name": "test.mp4",
    "uri": "xxx",
    "tag_list": [
        {"field_name":"Industry","field_type":"string", "field_value":"Enterprise Service"},
        {"field_name":"IsPublic","field_type":"bool", "field_value":true}
        ]
}'
```


<span id="e617ca18"></span>
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
        "collection_name": "video_collection",
        "resource_id": "kb-8349ef57441ab57",
        "project": "default",
        "doc_id": "test0123"
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
