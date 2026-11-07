---
title: "service_chat (recommended)"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_service_chat"
---

This section explains how to perform retrieval or Q&A based on an existing knowledge service.

<span id="d349a7d4"></span>
# Overview

To perform retrieval or conversational Q&A against a published knowledge service, you can use the `/api/knowledge/service/chat` API. This unified endpoint simplifies development by combining search and chat functionalities into a single call authenticated with a simple API key. This reference details the request parameters, headers, and response structures for both retrieval\-only and Q&A service types, including streaming and non\-streaming modes.

> What are the advantages of using the service/chat API?

> 1. There is no need to concatenate the search_knowledge API and the chat_completions API. After debugging parameters online in the console frontend and publishing the service, you can call this API directly to obtain results that are completely consistent with the console frontend.

> 2. There is no need to generate a complex AKSK signature; you can call the API using only an API Key.


<span id="0fa85226"></span>
# **Prerequisites**

Publish the knowledge service in your knowledge base console interface and associate the corresponding API Key (for permission verification).

<span id="f1a70ae9"></span>
# **Request API**


|**URI** |/api/knowledge/service/chat | |
|---|---|---|
|**Request method** |POST | |
|**Request headers** |Content\-Type: application/json |Request message type |
||'Authorization': 'Bearer {apikey}' |The API Key associated with this knowledge service, used for authorization |
||"Host": knowledge_base_domain |Knowledge base domain name |


<span id="d21968c9"></span>
# **Request parameters**


|**Parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|
|service_resource_id |string |Yes |\-\- |**Unique ID of the knowledge service** |
|messages |json |Yes |\-\- |**Multi\-turn conversation messages for retrieval/Q&A**<br><br>The format is a question\-and\-answer form. The role of the participant sending the message can be one of the following:<br><br><br>* user: User message<br><br>* assistant: Assistant message<br><br><br>The `content` of the last element where `role` is `user` represents the latest query<br><br>**Plain text conversation:** <br><br>For example:<br><br>```Python```<br>```[```<br>```    {```<br>```        "role": "system",```<br>```        "content": "You are an online customer service representative. Your primary task is to reply to users' questions with clever wording. You need to answer the following 'User Questions' based on the 'Reference Materials'. This information is within <context></context> XML tags. You need to provide accurate and concise answers based on the reference materials. The reference materials may contain image information, with image references within <img></img> XML tags. The order of images in the reference materials matches the order of images uploaded by the user."```<br>```    },```<br>```    {"role": "user", "content": "Hello"},```<br>```    {"role": "assistant", "content": "Hello! How can I help you?"},```<br>```    {"role": "user", "content": "Current round user question"}```<br>```]```<br><br><br>**Image and text conversation**:<br><br>For example:<br><br>```JSON```<br>```[```<br>```    {```<br>```        "role": "system",```<br>```        "content": "You are an online customer service representative. Your primary task is to reply to users' questions with clever wording. You need to answer the following 'User Questions' based on the 'Reference Materials'. This information is within <context></context> XML tags. You need to provide accurate and concise answers based on the reference materials. The reference materials may contain image information, with image references within <img></img> XML tags. The order of images in the reference materials matches the order of images uploaded by the user."```<br>```    },```<br>```    {```<br>```        "role": "user",```<br>```        "content": [```<br>```            {```<br>```                "type": "text",```<br>```                "text": "Recommend a similar toy suitable for a 3-year-old child"```<br>```            },```<br>```            {```<br>```                "type": "image_url",```<br>```                "image_url": {```<br>```                    "url": "xxx" # Image uploaded by customer, supports URL/base64 encoding. For protocol details, see: https://www.volcengine.com/docs/82379/1362931?lang=zh#477e51ce and https://www.volcengine.com/docs/82379/1362931?lang=zh#d86010f4```<br>```                }```<br>```            }```<br>```        ]```<br>```    }```<br>```]```<br> |
|query_param | |No |nil |**Search filter criteria**<br><br>If you configured filter criteria when creating the knowledge service, they are combined with these additional filter criteria using AND logic<br><br><br>* Supports filtering of document metadata and allows filtering by doc_id<br><br>* The fields used for filtering here need to be added to the fields section in index_config during collection creation<br><br><br>For example:<br><br>Single\-layer filter:<br><br>```JSON```<br>```doc_filter = {```<br>```   "op": "must", // Query operator: must/must_not/range/range_out```<br>```   "field": "doc_id",```<br>```   "conds": ["tos_doc_id_123", "tos_doc_id_456"]```<br>```}```<br>```query_param = {```<br>```    "doc_filter": doc_filter```<br>```}```<br><br><br>Multi\-layer filter:<br><br>```JSON```<br>```doc_filter = {```<br>```  "op": "and",   // Logical operator: and/or```<br>```  "conds": [     // Condition list, supports nested logical and query operators```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining any number of conditions (>=1)```<br>```    }```<br>```  ]```<br>```}```<br>```query_param = {```<br>```    "doc_filter": doc_filter```<br>```}```<br> |
|stream |bool |No |true |**Whether to stream the response**<br><br>Effective when the created knowledge service is a Q&A\-type service. |


<span id="eab4f193"></span>
# **Response message**

Currently, knowledge services are mainly divided into two types: retrieval\-type and Q&A\-type. The message format returned varies depending on the type of knowledge service.

<span id="4f5d7501"></span>
## Retrieval\-type knowledge service

If you request a retrieval\-type knowledge service, the returned result is as follows:


|Field |Subfield |Type |Remarks |
|---|---|---|---|
|code | |int |Status code |
|message | |string |Return message |
|**data** | |**json** |**Return data details** |
||count |int |Number of items returned in search results |
||rewrite_query |string |Result of query rewriting |
||token_usage |json |Token usage information |
|**result_list** | |**list** |**Returned chunk information** |
||id |string |Primary key of the index |
||content |string |Chunk content<br><br><br>1. Unstructured files: `content` returns the chunk content<br><br>2. FAQ files: content returns the answer<br><br>3. Structured files: content returns the fields and values involved in indexing, concatenated as key\-value (K:V) pairs, separated by \n |
||md_content |string |Markdown format parsing result<br><br>For table chunks in unstructured documents, this can also return Markdown format parsing results to retain more original table information<br><br>Table chunks can be identified by `chunk_type == table` |
||html_content |string |HTML format parsing result<br><br>For table chunks in unstructured documents, this can also return HTML format parsing results to retain more original table information<br><br>Table chunks can be identified by `chunk_type == table` |
||table_chunk_fields |list |Structured data search returns full single\-row data |
||original_question |string |Original question corresponding to the answer in FAQ data search |
||score |float |Score from vectorized semantic search |
||point_id |string |Chunk ID |
||chunk_title |string |Chunk title |
||chunk_id |int |Chunk position ID<br><br>Represents the position order in the original document |
||process_time |int |Search duration (s) |
||rerank_score |float |Re\-ranking score |
||doc_info |list |Document information<br><br>```JSON```<br>```{```<br>```    "doc_id": "_sys_auto_gen_doc_id-134144883689", //Document ID```<br>```    "doc_name": "2404.08817v2.pdf", //Document name```<br>```    "create_time": 1727333117, //Document creation time```<br>```    "doc_type": "pdf", //Type of the original document to which the knowledge belongs```<br>```    "doc_meta": "[{\"field_name\":\"doc_id\",\"field_type\":\"string\",\"field_value\":\"_sys_auto_gen_doc_id-13411829101044883689\"}]", //Document-related metadata (here, a string in the form of a list containing document ID information)```<br>```    "source": "url", //Knowledge source type: tos tos_fe```<br>```    "title": "Revisiting Code Similarity Evaluation with Abstract Syntax Tree Edit Distance", //Title of the document to which the knowledge belongs```<br>```    "url": "***" //Public download link of the original document```<br>```}```<br> |
||recall_position |int |Recall position in vectorized semantic search |
||rerank_position |int |Re\-ranking position |
||chunk_type |string |Chunk type<br><br>Example return value types include: doc\-image, image, table, mixed\-table, text, structured, and faq. |
||chunk_attachment |list |Temporary download links for retrieved attachments (such as original images), effective when chunk_type is image, table, or mixed\-table and get_attachment_link is True |


<span id="a92fe12b"></span>
## Q&A\-type knowledge service \- non\-streaming

If you request a Q&A\-type knowledge service and select non\-streaming response, the returned result is as follows:


|Field |Subfield |Type |Remarks |
|---|---|---|---|
|code | |int |Status code |
|message | |string |Return message |
|**data** | |**json** |**Return data details** |
||count |int |The number of returned search results |
||rewrite_query |string |Result of query rewriting |
||token_usage |json |Token usage information |
||result_list |json |Information returned by the search |
||generated_answer |string |Answer generated by the LLM |
||reasoning_content |string |Content generated by the reasoning model |


<span id="a928fc8a"></span>
## Q&A\-type knowledge service \- streaming

If you request a Q&A\-type knowledge service and select streaming response, the retrieval result will be returned in the first stream, token_usage will be returned in the last stream, and the intermediate streams will return the generated results in SSE format (refer to [chat_completions (new)](https://docs.byteplus.com/docs/209/collection_chat_completions)).


|Field | |Type |Remarks |
|---|---|---|---|
|code | |int |Status code |
|message | |string |Return message |
|**data** | |**json** |**Details of returned data** |
||count |int |The number of returned search results. Returned in the first stream. |
||rewrite_query |string |Result of query rewriting. Returned in the first stream. |
||result_list |json |Information returned by the search. Returned in the first stream. |
||generated_answer |string |Answer generated by the LLM. Returned in an intermediate stream. |
||reasoning_content |string |Content generated by the reasoning model. Returned in an intermediate stream. |
||token_usage |json |Token usage information. Returned in the final stream. |


<span id="d6cee676"></span>
# Complete example

<span id="6d2210c6"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer your_api_key' \
  http://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/service/chat \
  -d '{
    "service_resource_id": "your_service_resource_id",
    "stream": false,
    "messages": [
        {
            "role": "user",
            "content": "What are the ways to register for Douyin"
        }
    ]
}'
```


<span id="5266d589"></span>
## Response message

Response on successful execution:

```Shell
{
    "code": 0,
    "data": {
        "count": 2,
        "token_usage": {
            "embedding_token_usage": {
                "prompt_tokens": 23,
                "completion_tokens": 0,
                "total_tokens": 23
            },
            "rerank_token_usage": 62,
            "llm_token_usage": {
                "prompt_tokens": 510,
                "completion_tokens": 52,
                "total_tokens": 562,
                "prompt_tokens_details": {
                    "cached_tokens": 0
                },
                "completion_tokens_details": {
                    "reasoning_tokens": 0
                }
            }
        },
        "result_list": [
            {
                "id": "_sys_auto_gen_doc_id-8423876736290680802-0",
                "content": "Question: What are the ways to register for Douyin\nAnswer: There are methods such as phone number, email, etc.",
                "score": 0.6423748731613159,
                "point_id": "_sys_auto_gen_doc_id-8423876736290680802-0",
                "chunk_id": 0,
                "process_time": 1745475503,
                "rerank_score": 0.929823701560032,
                "doc_info": {
                    "doc_id": "_sys_auto_gen_doc_id-8423876736290680802",
                    "doc_name": "Untitled Spreadsheet.xlsx",
                    "create_time": 1745475499,
                    "doc_type": "xlsx",
                    "doc_meta":"[{\"field_name\":\"Industry\",\"field_type\":\"list<string>\",\"field_value\":[\"Healthcare\"]},{\"field_name\":\"Priority\",\"field_type\":\"float32\",\"field_value\":\"10\"}]",
                    "source": "tos_fe",
                    "url": ""
                },
                "recall_position": 1,
                "rerank_position": 1,
                "chunk_type": "structured",
                "chunk_source": "document",
                "update_time": 1745475503,
                "table_chunk_fields": [
                    {
                        "field_name": "Question",
                        "field_value": "What are the ways to register for Douyin"
                    },
                    {
                        "field_name": "Answer",
                        "field_value": "There are methods such as phone number, email, etc."
                    }
                ],
                "FromRecallQueue": "master_recall"
            },
            {
                "id": "_sys_auto_gen_doc_id-8423876736290680802-1",
                "content": "Question: Are there other ways to register for WeChat\nAnswer: Alternatively, you can register for WeChat through QQ",
                "score": 0.5205988883972168,
                "point_id": "_sys_auto_gen_doc_id-8423876736290680802-1",
                "chunk_id": 1,
                "process_time": 1745475503,
                "rerank_score": 0.3796083432458134,
                "doc_info": {
                    "doc_id": "_sys_auto_gen_doc_id-8423876736290680802",
                    "doc_name": "Untitled Spreadsheet.xlsx",
                    "create_time": 1745475499,
                    "doc_type": "xlsx",
                    "doc_meta":"[{\"field_name\":\"Industry\",\"field_type\":\"list<string>\",\"field_value\":[\"Healthcare\"]},{\"field_name\":\"Priority\",\"field_type\":\"float32\",\"field_value\":\"10\"}]",
                    "source": "tos_fe"
                },
                "recall_position": 2,
                "rerank_position": 2,
                "chunk_type": "structured",
                "chunk_source": "document",
                "update_time": 1745475503,
                "table_chunk_fields": [
                    {
                        "field_name": "Question",
                        "field_value": "Are there other ways to register for WeChat"
                    },
                    {
                        "field_name": "Answer",
                        "field_value": "Alternatively, you can register for WeChat through QQ"
                    }
                ],
                "FromRecallQueue": "master_recall"
            }
        ],
        "generated_answer": "Hello, you can register for Douyin using phone number, email, and other methods<reference data-ref=\"_sys_auto_gen_doc_id-8423876736290680802-0\" data-img-ref=\"false\"></reference>.",
    },
    "message": "success",
    "request_id": "02174581251018800000000000000000000ffff0a007412e51bff"
}
```


Response on failed execution:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
{
    "code": 1000003,
    "message": "invalid request:messsages role nil",
    "request_id": "02174581256280800000000000000000000ffff0a007412632e7a"
}
```
