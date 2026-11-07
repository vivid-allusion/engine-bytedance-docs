---
title: "Common Search Parameters"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Common_Search_Parameters_V2"
---

Search functionality consists of multiple interfaces, each corresponding to different search modes and business scenarios.

<span id="interface-upgrade-notes"></span>
# Interface Upgrade Notes


* The V1 interface combined various search modes into a single interface, distinguished by different parameter combinations. The V2 interface maps different search modes to different interfaces, making it clearer and easier for you to choose the appropriate search method for your business scenario.

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Vector Search, Dense\-Sparse Vector Hybrid Search |SearchByVector<br><br>dense_vector parameter |https://docs.byteplus.com/en/docs/VikingDB/Vector_Search<br><br>Set order_by_vector.vectors parameter |
|Dense\-Sparse Vector Hybrid Search |SearchByVector,<br><br>Set sparse_vector parameter |https://docs.byteplus.com/en/docs/VikingDB/Hybrid_dense\-sparse_vector_retrieval<br><br>Set order_by_vector.sparse_vectors parameter |
|Support for tensor reranking under vector search |SearchByVector<br><br>Set the `tensor_rerank` parameter. For more details, refer to:<br><br>[Tensor Rerank Structure](https://docs.byteplus.com/en/docs/VikingDB/Common_Search_Parameters_V2#post-processing-structure:~:text=5%20%3Cbr%3E%20%7D%20%3Cbr%3E-,Tensor%20Rerank%20structure,-Note%3A%20This%20parameter) |Not supported |
|Multimodal Search |SearchByMultiModal<br><br>For models that support instruction, you must explicitly set whether to add an instruction to refine the search results. The query statement, with the instruction concatenated, will be returned in the response. |https://docs.byteplus.com/en/docs/VikingDB/Multimodal_Retrieval<br><br>Set order_by_raw parameter |
|Tensor reranking support in multimodal search |SearchByMultiModal<br><br>Configure the `tensor_rerank` parameter. For more details, refer to: [Tensor Rerank Structure](https://docs.byteplus.com/en/docs/VikingDB/Common_Search_Parameters_V2#post-processing-structure:~:text=5%20%3Cbr%3E%20%7D%20%3Cbr%3E-,Tensor%20Rerank%20structure,-Note%3A%20This%20parameter) |Not supported |
|Primary Key Search |SearchByID |https://docs.byteplus.com/en/docs/VikingDB/Vector_Search<br><br>Set order_by_vector.primary_keys parameter |
|Scalar Sort Search |SearchByScalar |Set order_by_scalar parameter |
|Random Search |SearchByRandom |Do not set any order_by_xxx parameter |
|Keyword Search |SearchByKeywords |Not supported |
|Primary Key Filtering |ids_in, ids_not_in parameters |https://docs.byteplus.com/en/docs/VikingDB/primary_key_filter<br><br>primary_key_in, primary_key_not_in parameters |
|Sub\-index |Partitioning with better performance and usability is under development. Please stay tuned. |Specified by partition parameter |
|Response Fields |Primary key values will be listed separately for easy data location |All fields are returned at the same level in the response object |


<span id="common-request-body-parameters-for-search-interfaces"></span>
# Common Request Body Parameters for Search Interfaces


|Parameter Name |Type |Required |Sub\-parameter |Type |Description |
|---|---|---|---|---|---|
|resource_id |string |Choose 1 of 2 | | |Resource ID |
|collection_name |string | | | |Collection name |
|index_name |string |Yes | | |Index name |
|output_fields |list |No | | |List of scalar fields to return.<br><br><br>1. When users do not provide output_fields, all scalar fields are returned<br><br>2. When users provide an empty list, no scalar fields are returned<br><br>   If the format of output_fields is incorrect or if the specified fields are not in the collection, the interface returns an error |
|filter |map |No | | |Filter conditions. See below for the format. The default is empty, which means no filtering is applied. |
|limit |int |No | | |Number of search results, default is 10, upper limit is 100000 |
|offset |int |No | | |Offset. Only used in pagination scenarios, it is not recommended to set a large value to avoid deep pagination impact. Default value is 0. The value should be at least 0, with the same semantics as MySQL's offset. |
|advance (some advanced parameters, not needed for ordinary scenarios) |map |No |dense_weight |float32 |If the collection has a sparse vector field, you can specify the weight of dense and sparse vectors during search. Default value is 0.5, optional range [0.2, 1] |
| | | |ids_in |listor list |Setting this parameter limits the search to the specified list of primary keys. Default is empty. |
| | | |ids_not_in |listor list |Setting this parameter excludes items with the specified primary keys from the search results. Default is empty. |
| | | |post_process_ops |list |Post\-processing operator list. After the vector or scalar recall phase, further filter processing is performed on candidate data, such as string matching, frequency control, etc. Each operator is a map, executed serially. Default is empty. See below for post\-processing operators. |
| | | |post_process_input_limit |int |This parameter specifies the number of candidates that enter the post\-processing stage when post_process_ops is set.<br><br>The default value is three times the value of the limit parameter. If explicitly set, it should not be less than the limit value, but not exceed 100000. |
| | | |scale_k |float64 |The sef value for the search is calculated by multiplying the index's sef parameter by scale_k. Default 1, range [0.1, 100], the larger the value, the more accurate the search results, but correspondingly degrades performance. |


<span id="filter-structure"></span>
## filter Structure

To use a filter, the corresponding field must be configured as a scalar field by setting ScalarIndex.


|Operator |Applicable Field Types | |Example |
|---|---|---|---|
|must |string, int64, bool, list, list |This operator is effective for the specified field name. Its semantics are "must be in [...]" (i.e., "must in"). |`JSON <br> { <br> "op": "must", <br> "field": "region", <br> "conds": ["cn", "sg"] <br> } <br>` |
|must_not |string, int64, bool, list, list |This operator is effective for the specified field name. Its semantics are "must not be in [...]" (i.e., "must not in"). |`JSON <br> { <br> "op": "must_not", <br> "field": "data_type", <br> "conds": [1,2,3] <br> } <br>` |
|and |/ |This is a logical operator that takes the intersection of multiple conditions. |`JSON <br> { <br> "op": "and", // Operator name <br> "conds": [ // Condition list, supports nested logical operators and must/must_not operators <br> { <br> "op": "must", <br> "field": "type", <br> "conds": [1] <br> }, <br> { <br> ... // Supports one or more conditions to be combined. <br> } <br> ] <br> } <br>` |
|or |/ |This is a logical operator that takes the union of multiple conditions. |`JSON <br> { <br> "op": "or", // Operator name <br>` |
|range |int64, float32 |This option is valid for a specific field name and must be within a specified range. Use gte (greater than or equal to), gt (greater than), lte (less than or equal to), and lt (less than) to define a one\-dimensional range. |`Python <br> // price is in the range [100.0, 500.0) <br> { <br> "op": "range", <br> "field": "price", <br> "gte": 100.0, <br> "lt": 500.0 <br> } <br> <br> //price >= 100.0 <br> { <br> "op": "range", <br> "field": "price", <br> "gte": 100.0 <br> } <br>` |


<span id="post-processing-structure"></span>
## Post\-processing structure


|Operator |Applicable field types | |Example |
|---|---|---|---|
|string_contain |string |This is a keyword\-matching filter operator. It indicates that the field content contains the specified pattern. |`JSON <br> { <br> "op": "string_contain", <br> "field": "name", <br> "pattern": "bar" <br> } <br>` |
|string_match |string |This is a regular expression matching filter operator. |`JSON <br> { <br> "op": "string_match", <br> "field": "name", <br> "pattern": "^[0-9A-Za-z_]+$" <br> } <br>` |
|enum_freq_limiter |string |Frequency control operator. Used to ensure that the total number of occurrences of a specific value in a recall result does not exceed threshold. |`JSON <br> { <br> "op": "enum_freq_limiter", <br> "field": "city" <br> "threshold": 5 <br> } <br>` |


<span id="tensor-rerank-structure"></span>
## Tensor Rerank structure

Note: This parameter is supported only in SearchByVector and SearchByMultiModal.


|Parameter |Type |Required |Description |
|---|---|---|---|
|tensor |list |Required in SearchByVector; not allowed in SearchByMultiModal |Tensor input used to compute similarity with stored tensors.<br><br><br>* Required in SearchByVector<br><br>* Automatically generated by the model in SearchByMultiModal |
|input_limit |int |Yes |Number of candidates entering tensor rerank. Range: [1, 1000] |


<span id="retrieve-common-response-body-parameters-of-the-class-interface"></span>
# Common response body parameters for search interfaces


|Parameter Name |Type |Subparameter | |Description |
|---|---|---|---|---|
|result |map |data |list |This is the list of queried data. The structure of each item (SearchItem) is shown below. |
| | |filter_matched_count |int |If a filter is used, this returns the number of items that match the filter conditions. |
| | |total_return_count |int |Returns the number of data items in the actual search results |
| | |real_text_query |string |Optional. If it is a text search, returns the search statement (including instruction) when it is actually executed. |
| | |token_usage |map |This contains information about token usage, including prompt_tokens, completion_tokens, image_tokens, and total_tokens. |


<span id="searchitem"></span>
## SearchItem


|Parameter name |type |Other |
|---|---|---|
|id |string/int64 |The primary key field value of the data. |
|fields |map<string,any\> |key is the field name, value is the field value |
|score |float |Required. Final score. Results returned by the search API are sorted by score. |
|ann_score |float |This is not required. If the result has been processed by operators such as full\-text search and score calculation, the original score value of the vector search (ANN) will be returned. |
