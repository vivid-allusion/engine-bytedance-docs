---
title: "search_knowledge (new)"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/collection_search_knowledge"
---

This section explains how to perform semantic retrieval based on an existing knowledge base or a specific [experimental version](https://www.volcengine.com/docs/84313/1510752).

> To retrieve slices only from a specific experimental version, specify the pipeline_name parameter.


<span id="978bbe6c"></span>
# Overview

To perform advanced semantic searches against your knowledge base, you can use the /api/knowledge/collection/search_knowledge endpoint. This API provides powerful pre\-processing and post\-processing capabilities, including query rewriting for multi\-turn conversations, result reranking for improved relevance, and flexible filtering. It supports both dense and hybrid retrieval to optimize search performance and accuracy.

<span id="feb71bf9"></span>
# **Prerequisites**


* Once the knowledge base is created and documents are imported and processed, online retrieval is available.

* Before calling the API, complete account registration, identity verification, AK/SK key acquisition, and signature acquisition on the [Signature authentication and examples](https://docs.byteplus.com/docs/209/Signature_authentication_and_examples) page.

* Difference between the search and search_knowledge endpoints: The search_knowledge endpoint is the latest version of the interface, upgraded from the original search endpoint. Based on the original search endpoint, it supports new features such as multi\-turn rewriting and document aggregation sorting. In conjunction with the chat_completions endpoint, it enables a standard retrieval\-generation workflow.


<span id="db487ec9"></span>
# **Request endpoint**


|**URI** |/api/knowledge/collection/search_knowledge |Uniform resource identifier |
|---|---|---|
|**Request method** |POST |Type of operation requested by the client to the vector database server |
|**Request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="9155f052"></span>
# **Request parameters**


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Default value** |**Parameter description** |
|---|---|---|---|---|---|
|name |\-\- |string |No |\-\- |**Name of the knowledge base** |
|project |\-\- |string |No |default |**Project to which the knowledge base belongs**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To create the knowledge base in the default project, do not specify this field.</div><br><br><br><div data-tips="true" data-tips-type="warning">To manage a knowledge base in a specified project, set this parameter correctly.</div><br> |
|resource_id |\-\- |string |No |\-\- |**Unique ID of the knowledge base**<br><br>You can choose to pass resource_id directly, or pass both name and project as the unique identifier of the knowledge base. |
|query |\-\- |string |Yes |\-\- |**Text to retrieve**<br><br><br>* The maximum input length is 8000. If the query length exceeds 8000, the endpoint returns an error.<br><br>* If the query length is greater than the selected embedding model's maximum input length but less than 8000, the query is automatically truncated according to the selected model.<br><br>* If the query length is less than the selected embedding model's maximum input length, the retrieval returns the target slice as expected. |
|image_query |\-\- |string |No |\-\- |**Image to retrieve**<br><br>Image URL or Base64 encoding is supported. For detailed requirements, see [Image pixel specifications](https://www.volcengine.com/docs/82379/1409291?lang=zh#7a10f532) and [Image file format](https://www.volcengine.com/docs/82379/1409291?lang=zh#5c068efa).<br><br><br>* Image URL input: Suitable for scenarios where the image file already has a publicly accessible URL, with each image less than 10 MB.<br><br>* Base64 encoding input: Suitable for scenarios with smaller image files, with each image less than 3 MB and the request body not exceeding 4 MB. |
|limit |\-\- |int |No |10 |**Number of retrieval results**<br><br><br>* Valid range: [1, 1000] |
|query_param | |json |No | |**Retrieval filter and return settings** |
||doc_filter |map |No |\-\- |**Retrieval filter conditions**<br><br><br>* Supports filtering by document metadata.<br><br>* For detailed usage and supported fields, see [filter expression](https://www.volcengine.com/docs/84313/1419289#filter-%E8%A1%A8%E8%BE%BE%E5%BC%8F). Filtering by doc_id is supported.<br><br>* Fields used for filtering here must be added to the fields of index_config during collection/create.<br><br><br>For example:<br><br>Single\-layer filter:<br><br>```JSON```<br>```doc_filter = {```<br>```    "op": "must", // Query operators must/must_not/range/range_out```<br>```    "field": "doc_id",```<br>```    "conds": ["tos_doc_id_123", "tos_doc_id_456"]```<br>```}```<br>```query_param = {```<br>```    "doc_filter": doc_filter```<br>```}```<br><br><br>Multi\-layer filter:<br><br>```JSON```<br>```doc_filter = {```<br>```  "op": "and",   // Logical operators and/or```<br>```  "conds": [     // Condition list, supports nested logical and query operators```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // Supports any combination of one or more conditions```<br>```    }```<br>```  ]```<br>```}```<br>``````<br>```query_param = {```<br>```    "doc_filter": doc_filter```<br>```}```<br> |
|dense_weight |\-\- |float |No |0.5 |**Weight of dense vectors in hybrid retrieval**<br><br><br>* A value of 1 means pure dense retrieval, and 0 means pure lexical retrieval. The valid range is [0.2, 1].<br><br>* Effective only when the requested knowledge base uses hybrid retrieval, that is, when the index algorithm is hnsw_hybrid. |
|pre_processing | |json | | |**Retrieval preprocessing** |
||need_instruction |bool |No |False |**Whether to concatenate instruction for retrieval** |
||return_token_usage |bool |No |False |**Whether to return token usage at each stage of the search process** |
||rewrite |bool |No |False |**Whether to rewrite the query**<br><br>Rewrites the query based on historical conversation information passed in the messages field, for up to 3 rounds.<br><br>Note: A valid rewrite_query is returned only if the messages field contains more than two messages and this parameter is set to True.<br><br>```JSON```<br>```"messages": [```<br>```    {"role": "user", "content": "prompt 1"},```<br>```    {"role": "assistant", "content": "prompt2"},```<br>```    {"role": "user", "content": "prompt 3"},```<br>```]```<br> |
||messages |json |Yes |\-\- |**Multi\-turn conversation information**<br><br>Only required when **rewrite** is enabled. The question can be rewritten based on historical conversation content. Note that the number of conversation rounds uploaded must be \>= 1.<br><br>Roles of conversation participants sending messages. Optional values include:<br><br><br>* user: User Message (user message)<br><br>* assistant: Assistant Message (assistant message)<br><br><br>```JSON```<br>```[```<br>```    {"role": "user", "content": "What document formats does the knowledge base support?"},```<br>```    {"role": "assistant", "content": "The knowledge base supports structured and unstructured documents. Structured documents support common formats such as Excel, CSV, JSONL, etc. Unstructured documents support common formats such as PDF, DOCX, PPT, etc."},```<br>```    {"role": "user", "content": "What about the size?"}```<br>```]```<br> |
|post_processing | |json | | |**Retrieval post\-processing** |
||rerank_switch |bool |No |False |**Automatically rerank results**<br><br>When enabled, the rerank model is automatically used to sort the results. |
||retrieve_count |int |No |25 |Number of slices to be reranked. The default is 25<br><br>Effective only when rerank_switch is True. retrieve_count must be greater than or equal to limit, otherwise an error will be thrown. |
||chunk_diffusion_count |int |No |0 |The number of preceding and succeeding slices to return alongside the matched slice.<br><br>Default is 0, which means chunk diffusion is not performed. Range [0, 5] |
||chunk_group |bool |No |False |**Text aggregation**<br><br>Aggregation is disabled by default. For unstructured files, you can enable text aggregation to preserve the original document order, which can improve comprehension for large language models. After this is enabled, slices are re\-aggregated and sorted by document and document order before being returned. |
||rerank_model |string |No |"base\-multilingual\-rerank" |**Rerank model selection**<br><br>Only takes effect when "rerank_switch" == True<br><br>Optional models:<br><br><br>* "base\-multilingual\-rerank": High speed, supports long text, and supports over 70 languages<br><br>* "m3\-v2\-rerank": Suitable for general text and supports over 100 languages |
||rerank_only_chunk |bool |No |False |**Whether to calculate rerank score based only on chunk content**<br><br>Optional values:<br><br><br>* True: Score is calculated only based on chunk content<br><br>* False: Sorting score is calculated based on chunk title and content together |
||get_attachment_link |bool |No |False |**Whether to obtain a temporary download link for images in the slice** |
|pipeline_name |\-\- |string |No |\-\- |**Experiment version name**<br><br><br>* Specifies the experiment version from which to query slices<br><br>* If not specified, the default is to query the slice list under the primary version of the knowledge base |


<span id="043d7f03"></span>
# **Response message**


|**Parameter** |**Parameter description** |
|---|---|
|code |Status code |
|message |Status message |
|request_id |Unique identifier for each request |
|data |Retrieved slice information |


data return value


|**Field** |**Subfield** |**Field type** |**Description** |
|---|---|---|---|
|collection_name |\-\- |string |Name of the knowledge base that was searched. |
|count |\-\- |int |Number of slices returned by retrieval |
|rewrite_query |\-\- |string |Rewritten query |
|token_usage | |list |Token usage information |
||embedding_token_usage | |Token usage during the vectorization retrieval stage<br><br>```JSON```<br>```{```<br>```    "prompt_tokens": 16,```<br>```    "completion_tokens": 0,```<br>```    "total_tokens": 16```<br>```}```<br> |
||rerank_token_usage |int |Token usage during the rerank stage |
||rewrite_token_usage |int |Token usage for query rewriting |
|result_list | |list |Returned slice information |
||id |string |Primary key of the index |
||content |string |Slice content<br><br><br>1. Unstructured file: content returns the slice content<br><br>2. FAQ file: content returns the answer<br><br>3. Structured file: content returns the fields and values involved in indexing, concatenated as K:V pairs, separated by \n |
||md_content |string |Parsing result in markdown format<br><br>For table slices in unstructured documents, an additional markdown\-formatted parsing result can be returned to retain more original table information<br><br>Table slices can be identified by chunk_type == table |
||html_content |string |Parsing result in HTML format<br><br>For table slices in unstructured documents, the HTML format parsing result can be returned additionally to retain more original table information<br><br>Table slices can be identified by chunk_type == table |
||description |string |If slice content analysis is enabled when creating the knowledge base, that is, enable_slice_analysis=true, this field returns the slice content analysis result |
||table_chunk_fields |list |Structured data retrieval returns the complete data of a single row |
||original_question |string |Original question corresponding to the answer retrieved from FAQ data |
||score |float |Vectorized semantic retrieval score |
||point_id |string |Slice ID |
||chunk_title |string |Slice title |
||chunk_id |int |Slice position ID<br><br>Represents the ordinal position in the original document |
||process_time |int |Retrieval time (s) |
||rerank_score |float |Rerank score |
||doc_info |list |Information about the document to which the chunk belongs<br><br>```JSON```<br>```{```<br>```    "doc_id": "_sys_auto_gen_doc_id-134144883689", // Document id```<br>```    "doc_name": "2404.08817v2.pdf", // Document name```<br>```    "create_time": 1727333117, // Document creation time```<br>```    "doc_type": "pdf", // Type of the original document to which the knowledge belongs```<br>```    "doc_meta": "[{\"field_name\":\"doc_id\",\"field_type\":\"string\",\"field_value\":\"_sys_auto_gen_doc_id-13411829101044883689\"}]", // Document-related metadata (this is a string in the form of a list containing document id information)```<br>```    "source": "url", // Knowledge source type: tos tos_fe```<br>```    "title": "Revisiting Code Similarity Evaluation with Abstract Syntax Tree Edit Distance", // Title of the document to which the knowledge belongs```<br>```    "url": "***" // Public download link of the original document```<br>```}```<br> |
||recall_position |int |Recall position in vectorized semantic retrieval |
||rerank_position |int |Rerank position |
||chunk_type |string |Chunk type<br><br>Possible values include: doc\-image, image, table, mixed\-table, text, structured, and faq. |
||chunk_attachment |list |Temporary download link for retrieved attachments, valid for 10 minutes<br><br>When chunk_type is image/doc_image and get_attachment_link is True, returns the original image download link<br><br>When chunk_type is table/mixed\-table and get_attachment_link is True, this field returns the image of the table or a list of images contained in the table |
||original_coordinate | |Position coordinates of the chunk in the original document<br><br>Currently only pdf and ppt documents are supported. An example of the returned value is as follows:<br><br>```Plain```<br>```{```<br>```  "page_no": [0, 2],```<br>```  "bbox": [```<br>```              [0.43075400818407467, 0.05201688247011952, 0.8814365734218823, 0.06268848178713717],```<br>```              [0.1144293768909557, 0.08121951665355412, 0.8790083028120703, 0.7626920876297637]```<br>```  ]```<br>```}```<br> |


table_chunk_fields return value


|Field |Field type |Description |
|---|---|---|
|field_name |string |Table field name of the structured data |
|field_value |\-\- |Table field value of the structured data<br><br>The field type is subject to the table field definition when creating the knowledge base |


chunk_attachment return value


|Field |Field type |Description |
|---|---|---|
|uuid |string |Unique identifier of the attachment |
|caption |string |Title to which the image belongs; if no title is recognized, the value is "\n" |
|type |string |Attachment type, such as image. |
|link |string |When "get_attachment_link" == True, returns a temporary download link for the image or table containing the image, valid for 10 minutes |


<span id="4c7b835c"></span>
## **Status code description**


|**Status code** |**HTTP status code** |**Return message** |**Status code description** |
|---|---|---|---|
|0 |200 |success |Success |
|1000001 |401 |unauthorized |Missing authentication information. |
|1000002 |403 |no permission |Insufficient permissions |
|1000003 |400 |invalid request: %s |Invalid parameter |
|1000005 |400 |collection not exist |Collection does not exist |


<span id="a7757ca9"></span>
# Complete example

<span id="18f6343c"></span>
## Request message

```Shell
curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-knowledgebase.mlp.cn-hongkong.bytepluses.com/api/knowledge/collection/search_knowledge \
  -d '{
        "name": "your_collection",
        "query": "test",
        "limit": 2,
        "query_param": {
            "doc_filter": {
                "op": "must",
                "field": "doc_id",
                "conds": ["tos_doc_id_123", "tos_doc_id_456"]
            }
        },
        "dense_weight": 0.5,
        "pre_processing": {
            "need_instruction": True,
            "rewrite": True,
            "messages": [
                {
                    "role": "system",
                    "content": "prompt template"
                },
                {
                    "role": "user",
                    "content": "history content"
                }
                {
                    "role": "assistant",
                    "content": "history content"
                },
                {
                    "role": "user",
                    "content": "history content"
                },
                ...
           
                {
                    "role": "assistant",
                    "content": "history content"
                }
                
            ],
            "return_token_usage": True
        },
        "post_processing": {
            "rerank_switch": False,
            "rerank_model": "base-multilingual-rerank",
            "rerank_only_chunk": False,
            "retrieve_count": 25,
            "endpoint_id": "ep",
            "chunk_group": False,
            "get_attachment_link": False
        }
    }
  }
}'
```


<span id="2164ae88"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 209
Content-Type: application/json
 
{
    "code": 0,
    "data": {
        "collection_name": "example",
        "count": 2,
        "rewrite_query": "xxx",
        "token_usage": {
            "embedding_token_usage": {
                "prompt_tokens": 16,
                "completion_tokens": 0,
                "total_tokens": 16
            },
            "rerank_token_usage": 0
        },
        "result_list": [
            {
                "id": "_sys_auto_gen_doc_id-13411829101044883689-15",
                "content": "content",
                "score": 0.2639991044998169,
                "point_id": "_sys_auto_gen_doc_id-13411829101044883689-15",
                "chunk_title": "title",
                "chunk_id": 15,
                "process_time": 1727333127,
                "doc_info": {
                    "doc_id": "_sys_auto_gen_doc_id-13411829101044883689",
                    "doc_name": "2404.08817v2.pdf",
                    "create_time": 1727333117,
                    "doc_type": "pdf",
                    "doc_meta": "[{\"field_name\":\"doc_id\",\"field_type\":\"string\",\"field_value\":\"_sys_auto_gen_doc_id-13411829101044883689\"}]",
                    "source": "tos_fe",
                    "title": "title"
                },
                "recall_position": 1,
                "chunk_type": "text"
            },
            {
                "id": "_sys_auto_gen_doc_id-13411829101044883689-7",
                "content": "content",
                "score": 0.2583845257759094,
                "point_id": "_sys_auto_gen_doc_id-13411829101044883689-7",
                "chunk_title": "title",
                "chunk_id": 7,
                "process_time": 1727333127,
                "doc_info": {
                    "doc_id": "_sys_auto_gen_doc_id-13411829101044883689",
                    "doc_name": "2404.08817v2.pdf",
                    "create_time": 1727333117,
                    "doc_type": "pdf",
                    "doc_meta": "[{\"field_name\":\"doc_id\",\"field_type\":\"string\",\"field_value\":\"_sys_auto_gen_doc_id-13411829101044883689\"}]",
                    "source": "tos_fe",
                    "title": "title"
                },
                "recall_position": 2,
                "chunk_type": "text"
            }
        ]
    },
    "message": "success",
    "request_id": "02172740884343900000000000000000000ffff0a00406f8a8861"
}
```


Failed execution returns:

```JSON
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000003, "message":"invalid request：%s", "request_id": "021695029757920fd001de6666600000000000000000002569b8f"}
```
