---
title: "searchByMultiModal"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByMultiModal_v2"
---

<span id="overview"></span>
# Overview

`search_by_multi_modal` is used for multi\-modal data retrieval. Multi\-modal data retrieval means that the vector database supports direct retrieval using multi\-modal data types such as images and text, and supports combinations of modalities, such as text\-to\-image search, image\-to\-image search, image\-to\-text+image search, etc.


* Currently supports unstructured data of text, image, and video types.

* After Collection data is written/deleted, Index data update time is approximately 20s, so it cannot be immediately retrieved in the Index.


<span id="prerequisites"></span>
# Prerequisites


* You have selected the database type starting from vectorization from the console and configured vectorization fields when creating the dataset; or configured the Collection's vectorization function by setting the vectorize parameter when creating a dataset through the create_collection interface.

* When writing data through the upsert_data interface, you have written the field names and field values of text or image types.

* When creating an index through create_index, you have created the vector_index vector index.


Applicable when selecting "Need vectorization" when creating a vector library: When the imported data is raw data, you can input text, images, etc. through this interface for retrieval.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByMultiModalRequest`, and its fields are shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|text |Optional[str] |At least 1 required |Input text for retrieval. |
|image |Optional[Any] | |Input image for retrieval, supports:<br><br><br>* TOS link, in the form `tos://{bucket}/{object_key}`.<br><br>* Base64 encoding, in the form `base64://{Base64 encoding}`. |
|video |Optional[Any] | |JSON structure, such as:<br><br>{<br><br>"value": "http/https/TOS link (required)",<br><br>"fps": 2.0 (0.2\-5, optional)<br><br>} |
|filter |Optional[Dict[str, Any]] |No |Scalar filter conditions, see **Scalar Filtering** for details.<br><br><br>* Not filling in means pure multi\-modal retrieval.<br><br>* Supports operators such as must, must_not, range, range_out, which can be combined with and / or. |
|output_fields |Optional[List[str]] |No |List of scalar fields to return.<br><br><br>1. When not set, returns all scalar fields in the collection.<br><br>2. Passing an empty list means not returning any scalar fields.<br><br>3. The field name must exist in the collection schema, otherwise the request will report an error. |
|limit |Optional[int] |No |Limit the number of returned items, maximum 5000. |
|offset |Optional[int] |No |Pagination offset, default 0, deep pagination performance overhead will occur when it is too large. |
|partition |Optional[str] |No |Specify the partition name for retrieval. |
|advance |Optional[SearchAdvance] |No |Advanced parameter set (post_process_ops, ids_in, etc.), see [Common Retrieval Parameters](https://docs.byteplus.com/docs/84313/1927082) for details. |
|need_instruction |Optional[bool] |No |Controls whether to let the model automatically complete the instruction, default True for Doubao series, default False for other models. |


<span id="return-parameters"></span>
# Return Parameters


|Name |Type |Description |
|---|---|---|
|request_id |Optional[str] |Request link ID. |
|code |Optional[str] |Service return code, Success indicates success. |
|message |Optional[str] |Error or prompt information. |
|api |Optional[str] |The specific API name called. |
|result |Optional[SearchResult] |Retrieval result body, see the structure below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|data |List[SearchItemResult] |List of recalled results, see the structure below. |
|filter_matched_count |Optional[int] |Total number of documents that meet the filter conditions. |
|total_return_count |Optional[int] |Number of results returned this time. |
|real_text_query |Optional[str] |The real query string after possible correction by the model. |
|token_usage |Dict[str, Any] |Token metering information. |



* SearchItemResult



|Name |Type |Description |
|---|---|---|
|id |Any |Primary key value. |
|fields |Dict[str, Any] |Content of returned scalar fields. |
|score |Optional[float] |Final similarity score. |
|ann_score |Optional[float] |ANN coarse ranking score. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```python
import os

from vikingdb import IAM
from vikingdb.vector import SearchByMultiModalRequest, VikingVector

auth = IAM(
    ak=os.environ["VIKINGDB_AK"],
    sk=os.environ["VIKINGDB_SK"],
)
client = VikingVector(
    host=os.environ["VIKINGDB_HOST"],
    region=os.environ["VIKINGDB_REGION"],
    auth=auth,
    scheme="https",
)

index_client = client.index(
    collection_name=os.environ["VIKINGDB_COLLECTION"],
    index_name=os.environ["VIKINGDB_INDEX"],
)
request = SearchByMultiModalRequest(
    text="找下类似品种",
    need_instruction=True,                  # need instruction improves prompt
    image="tos://zayn-viking/kind_dog.png", # upload to tos first
    limit=3,
)
response = index_client.search_by_multi_modal(request)
if response.result:
    for item in response.result.data:
        print(item.id, item.fields.get("image"), item.score)
```
