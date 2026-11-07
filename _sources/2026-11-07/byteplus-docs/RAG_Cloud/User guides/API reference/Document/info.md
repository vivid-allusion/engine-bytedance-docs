---
title: "info"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/doc_info"
---

<span id="0a292908"></span>
# Overview

The `/api/knowledge/doc/info` endpoint is used to view document information in a knowledge base or under a specific experimental version

> You can view the document status under a specific experimental version by specifying the pipeline_name parameter.


<span id="b79ee008"></span>
# **Prerequisites**

To call this API, you must first complete account registration, real\-name authentication, and acquire your AK/SK key and signature by following the instructions on the "Signature Authentication Method" page.

<span id="463a2ff5"></span>
# **Request endpoint**


|**URI** |/api/knowledge/doc/info |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request headers** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="20018af3"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|collection_name |string |No |\-\- |**Knowledge base name** |
|project |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this field is not specified, it will be created under the default project.</div><br><br><br><div data-tips="true" data-tips-type="warning">To operate on a knowledge base within a specified project, this field must be configured correctly.</div><br> |
|resource_id |string |No |\-\- |**Unique ID of the knowledge base**<br><br>You can pass the resource_id directly, or pass both collection_name and project to uniquely identify the knowledge base. |
|doc_id |string |Yes |\-\- |**ID of the document to query** |
|return_token_usage |bool |No |false |**Whether to return the number of tokens consumed for document vectorization and summary generation** |
|pipeline_name |string |No |\-\- |**Experimental version name**<br><br><br>* By default, document information under the primary version of the knowledge base is queried.<br><br>* If specified, document information within the specified experimental version will be queried. |


<span id="c1089ad7"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Return message |
|request_id |Unique identifier for each request |
|data |Document information |


data return value


|Field |Subfield |Field type |Description |
|---|---|---|---|
|collection_name |\-\- |string |Knowledge base name |
|doc_name |\-\- |string |Document name |
|doc_hash |\-\- |string |Unique hash value of the document content |
|doc_id |\-\- |string |Unique identifier of the document |
|add_type |\-\- |string |Document import method |
|doc_type |\-\- |string |Document type |
|create_time |\-\- |number |Document creation time, as a Unix timestamp in milliseconds. |
|added_by |\-\- |string |Document uploader |
|update_time |\-\- |number |Document update time, as a Unix timestamp in milliseconds. |
|url |\-\- |string |URL of the document |
|meta |\-\- |string |Document metadata, as a JSON\-formatted string. |
|point_num |\-\- |number |Number of document slices |
|status | |object |Document processing status object |
||process_status |number |Document processing status |
|doc_summary |\-\- |string |Full document summary |
|brief_summary |\-\- |string |Brief document summary |
|title |\-\- |string |Document title |
|doc_size |\-\- |number |Document size (bytes) |
|full_directory_path |\-\- |array |Directory path of the document |
|is_wiki |\-\- |boolean |Whether the document is of wiki type |
|statistics | |object |Document statistics object |
||pages |number |Number of pages |
||lines |number |Number of lines |
||cells |number |Number of cells |
||chars |number |Number of extracted text characters |
||images |number |Number of images |
||tables |number |Number of tables |


<span id="d1594a33"></span>
## failed_code error codes


|**failed_code** |**Error description** |**Suggested solution** |
|---|---|---|
|10001 |Document download timeout |Please try the download again. If the problem persists, please contact us. |
|10003 |URL validation failed. Please check the URL. |Please ensure the URL is correct and try again. If the problem persists, please contact us. |
|30001 |Exceeded knowledge base file size limit |Exceeded knowledge base quota limit. [Knowledge base quota description](https://docs.byteplus.com/docs/209/Knowledge_base_quota_description) |
|35001 |Exceeded knowledge base slice quantity limit |Exceeded knowledge base quota limit. [Knowledge base quota description](https://docs.byteplus.com/docs/209/Knowledge_base_quota_description) |
|35002 |FAQ document parsing result is empty |The document parsing resulted in 0 slices. Please ensure the document contains valid data. |
|35004 |Exceeded knowledge base FAQ document sheet quantity limit |Exceeded knowledge base quota limit. [Knowledge base quota description](https://docs.byteplus.com/docs/RAG_Cloud/Knowledge_base_quota_description) |
|36003 |Structured document header mismatch |Structured document header mismatch. Please ensure that the header of each sheet in the uploaded document is completely consistent with the predefined knowledge base table structure. |
|36004 |Structured document data type conversion failed |Structured document data type conversion failed. Please ensure that the content format of each cell in each sheet of the uploaded document is completely consistent with the data types defined in the predefined knowledge base table structure. |
|36005 |Exceeded knowledge base structured document sheet quantity limit |Exceeded knowledge base quota limit. [Knowledge base quota description](https://docs.byteplus.com/docs/RAG_Cloud/Knowledge_base_quota_description) |
|36006 |Exceeded knowledge base structured document valid row quantity limit |Exceeded knowledge base quota limit. [Knowledge base quota description](https://docs.byteplus.com/docs/RAG_Cloud/Knowledge_base_quota_description) |
|36007 |Structured document parsing result is empty |The document parsing resulted in 0 slices. Please ensure the document contains valid data. |
|36008 |The combined text length of the columns used for embedding exceeds the limit. |Shorten the text length in the columns used for embedding |
|Other error codes |Unknown error, please contact us |Unknown error, please contact us |


<span id="f7c17e69"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return information** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Authentication failed |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |
|1000005 |400 |Collection does not exist |Collection does not exist |
|1001001 |400 |Doc does not exist |Doc does not exist |


<span id="c67794dc"></span>
# Complete example

<span id="44643635"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/doc/info \
  -d '{
    "collection_name": "test_collection_name",
    "project": "",
    "doc_id": "test123",
    "return_token_usage": true
}'
```


<span id="38fff148"></span>
## Response message

Return on success:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
  "collection_name": "test_collection",
  "doc_name": "test.pdf",
  "doc_hash": "xxxxxxxxxxxxxxxx",
  "doc_id": "_sys_auto_gen_doc_id-xxxx",
  "add_type": "tos_fe",
  "doc_type": "pdf",
  "create_time": 1768804541257,
  "added_by": "user@example.com",
  "update_time": 1768804640273,
  "meta": "[]",
  "point_num": 11,
  "status": {
    "process_status": 0
  },
  "doc_summary": "",
  "brief_summary": "",
  "title": "xxx",
  "doc_size": 29964057,
  "full_directory_path": [],
  "is_wiki": false,
  "statistics": {
    "pages": 0,
    "lines": 0,
    "cells": 0,
    "chars": 6127,
    "images": 0,
    "tables": 0
  }
}
```


Return on failure:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request: %s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
