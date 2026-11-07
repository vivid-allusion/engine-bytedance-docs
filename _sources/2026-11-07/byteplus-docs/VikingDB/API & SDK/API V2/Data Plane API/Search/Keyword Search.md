---
title: "Keyword Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Keyword_Search_V2"
---

<span id="overview"></span>
# Overview

The multi\-keyword search API allows you to perform a hybrid search that combines exact keyword matching with semantic retrieval. This method precisely recalls content containing specified keywords while also retrieving semantically relevant results. This document details the API endpoint, parameters, and provides examples for implementing various search modes, such as `semantic_then_match` or `bm25` for full\-text search, to help you achieve more accurate ranking.

For scenarios with weak semantics but strong keyword/phrase constraints, VikingDB introduces full\-text search. Enable it by configuring the **FullText parameter** when creating a collection. Up to two text fields can be configured for tokenization and keyword retrieval. Full\-text search complements pure semantic vector retrieval and can be seamlessly combined with vector search and filtering to achieve more accurate ranking in a “semantic + keyword” hybrid recall mode.

<span id="request-api"></span>
# Request API

When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the [Data Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process), copy the calling example and fill in the necessary information.


|URI |/api/vikingdb/data/search/keywords |Uniform Resource Identifier |
|---|---|---|
|Method |POST |Client operation type for the vector database server |
|Headers |Content\-Type: application/json |Request message type |
| |Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="request-body-parameters"></span>
# Request Body Parameters

Only parameters specific to this interface are listed. For more information, please refer to

[Data Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process)

To use the keyword search, at least one of the following prerequisites must be satisfied:


* The dataset is configured with **Vectorize** to vectorize the `text` field.

* The dataset is configured with **FullText**.



|Parameter |Required |Type |Description |
|---|---|---|---|
|mode |No |string |Specifies one of two modes:<br><br><br>1. semantic_then_match: The collection must have Vectorize configured.<br><br>2. bm25: Prerequisite: The collection must have FullText configured.<br><br>   If this parameter is omitted, the mode is selected automatically based on the collection configuration:<br><br>* If **FullText** is configured, bm25 is used.<br><br>* If Vectorize is configured, semantic_then_match is used.<br><br>* If both are configured, bm25 is used by default.<br><br>* If neither is configured, this API cannot be used. |
|keywords |Yes<br><br>Required if 'query' is not provided |list |Keyword list with 1\-10 elements. Elements cannot be empty strings. The total length of elements must not exceed 512 bytes. |
|query | |string |Query string with a maximum length of 512 bytes.<br><br>For semantic search, separate multiple keywords with spaces, and the backend tokenizes by spaces (up to the first 10 keywords).<br><br>For bm25 search, the query is parsed by the analyzer (up to the first 10 keywords). |
|case_sensitive |No |bool |Takes effect only for semantic_then_match mode. Specifies whether the search is case\-sensitive. Default is false. For bm25 mode, the analyzer is used. |
|fields |No |list |Takes effect only for bm25 mode. If multiple FullText fields are configured, specify which fields to search in. |
|During actual retrieval, up to the first 10 keywords are extracted. The total length of keyword content does not exceed 512 bytes. | | | |


<span id="request-response-example"></span>
# Request Response Example


* Request Parameters


```JSON
req_path = "/api/vikingdb/data/search/keywords"
req_body = {
    "collection_name": "test_coll_with_vectorize",
    "index_name": "idx_1",
    "keywords": ["Volcano", "Vector", "Search", "Billion"],
    "output_fields": [
        "f_text"
    ],
    "limit": 5
}
```



* Response Parameters


```JSON
{
    "code": "Success",
    "message": "The API call was executed successfully.",
    "request_id": "02175438839168500000000000000000000ffff0a003ee4fc3499",
    "result": {
        "data": [
            {
                "id": "uid_001",
                "fields": {
                    "f_text": "Supports billion-scale vector search"
                },
                "score": 3.605649671017216,
                "ann_score": 0.34465837478637695
            },
            {
                "id": "uid_002",
                "fields": {
                    "f_text": "Vector similarity search is a retrieval method based on vector space models"
                },
                "score": 2.583801264623392,
                "ann_score": 0.269525408744812,
            },
            {
                "id": "uid_001",
                "fields": {
                    "f_text": "A vector is a quantity in mathematics with magnitude and direction. Unstructured data such as text, images, audio and video"
                },
                "score": 0.269525408744812,
                "ann_score": 0.31852447986602783
            },
            {
                "id": "uid_001",
                "fields": {
                    "f_text": "The database has multiple proprietary index algorithms developed by Volcano Engine"
                },
                "score": 1.5971799596522382,
                "ann_score": 0.3151528239250183
            },
            {
                "id": "uid_001",
                "fields": {
                    "f_text": "Can be widely applied to intelligent question answering, intelligent search, recommendation systems and data deduplication"
                },
```
