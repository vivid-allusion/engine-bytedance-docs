---
title: "Search Common Parameters"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Search_Common_Parameters_v2"
---

The search function consists of multiple interfaces, each corresponding to different search modes and business scenarios.

<span id="interface-description"></span>
# Interface Description

The V2 API maps different search modes to different interfaces, making it clearer and easier for you to select the appropriate search method for your business scenario.

<span id="common-request-body-parameters-for-search-interfaces"></span>
# Common Request Body Parameters for Search Interfaces


|Name |Type |Required |Sub\-parameter |Type |Description |
|---|---|---|---|---|---|
|resource_id |str |Either one is required | | |Collection resource ID. |
|collection_name |str | | | |Collection name. |
|index_name |str |Yes | | |Index name. |
|output_fields |List[str] |No | | |List of scalar fields to return.<br><br><br>1. Returns all scalar fields in the collection when not set.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. Field names must exist in the collection schema, otherwise the request will return an error. |
|filter |Dict[str, Any] |No | | |Scalar filter conditions, see format below, not set by default. |
|limit |int |No | | |Maximum number of results to return, default 10, maximum value 100000. |
|offset |int |No | | |Pagination offset, default 0. Large values will trigger deep pagination performance degradation. |
|Advance |SearchAdvance |No |dense_weight |Optional[float] |Dense/sparse weight in hybrid vector scenarios, default 0.5, range [0.2, 1]. |
| | | |ids_in |Optional[List[Any]] |Search only within this primary key collection range. |
| | | |ids_not_in |Optional[List[Any]] |Exclude specified primary key list. |
| | | |post_process_ops |Optional[List[Dict[str, Any]]] |List of post\-processing operators, executed serially. See "Post\-Processing Operators \- PostProcess" for details. |
| | | |post_process_input_limit |Optional[int] |Number of candidates entering the post\-processing stage. |
| | | |scale_k |Optional[float] |Candidate ratio allocated for subsequent rerank. |
| | | |filter_pre_ann_limit |Optional[int] |Maximum number of candidates when performing scalar filtering first. |
| | | |filter_pre_ann_ratio |Optional[float] |Candidate ratio when performing scalar filtering first. |


<span id="filter-structure"></span>
## filter Structure

The prerequisite for using filter is that the corresponding scalar field has been set as a scalar index (scalar_index).


|Operator |Applicable Field Types |Description |Example |
|---|---|---|---|
|must |string, int64, bool, list, list |Takes effect on the specified field name, semantic meaning is "must be in [...]" |`JSON <br> { <br> "op": "must", <br> "field": "region", <br> "conds": ["cn", "sg"] <br> } <br>` |
|must_not |string, int64, bool, list, list |Takes effect on the specified field name, semantic meaning is "must not be in [...]" |`JSON <br> { <br> "op": "must_not", <br> "field": "data_type", <br> "conds": [1,2,3] <br> } <br>` |
|and |/ |Logical operator, for logical query requirements, takes intersection of multiple conditions |`JSON <br> { <br> "op": "and", // Operator name <br> "conds": [ // Condition list, supports nested logical operators and must/must_not operators <br> { <br> "op": "must", <br> "field": "type", <br> "conds": [1] <br> }, <br> { <br> ... // Supports combination of any number >=1 conditions <br> } <br> ] <br> } <br>` |
|or |/ |Logical operator, for logical query requirements, takes union of multiple conditions |`JSON <br> { <br> "op": "or", // Operator name <br> "conds": [ // Condition list, supports nested logical operators and must/must_not operators <br> { <br> "op": "must", <br> "field": "type", <br> "conds": [1] <br> }, <br> { <br> ... // Supports combination of any number >=1 conditions <br> } <br> ] <br> } <br>` |
|range |int64, float32 |Takes effect on the specified field name, semantic meaning is "must be in the specified range". Configure using `gte` (greater than or equal), `gt` (greater than), `lte` (less than or equal), `lt` (less than) to define a one\-dimensional range. |`Python <br> // price is in [100.0, 500.0) <br> { <br> "op": "range", <br> "field": "price", <br> "gte": 100.0, <br> "lt": 500.0 <br> } <br> <br> // price >= 100.0 <br> { <br> "op": "range", <br> "field": "price", <br> "gte": 100.0 <br> } <br>` |
|time_range |date_time |Time point filtering, configure using `gte` (greater than or equal), `gt` (greater than), `lte` (less than or equal), `lt` (less than) to define a one\-dimensional range. |`JSON <br> { <br> // Search for data between Beijing time 2025-08-12 00:00:00 ~ 2025-08-13 00:00:00 <br> "op": "time_range", <br> "field": "f_date_time", <br> "gt": "2025-08-12T00:00:00+08:00", <br> "lt": "2025-08-13T00:00:00+08:00", <br> } <br>` |
|geo_range |geo_point |Geographic distance filtering, uses `center` as the center point and `radius` as the distance radius. |`JSON <br> { <br> "op": "geo_range", <br> "field": "f_geo_point", <br> "center": "116.412138,39.914912", <br> "radius": "10000m" <br> } <br>` |


<span id="post-processing-structure"></span>
## Post\-Processing Structure


|Operator |Applicable Field Types |Introduction |Example |
|---|---|---|---|
|score_fusion |string |Score fusion operator, used to fuse scores of specified spatiotemporal scalars. |`JSON <br> { <br> "op": "score_fusion", <br> "fusion_by": "add", <br> "addition_score_weight": 0.6, // Additional score weight is 0.6, ANN score weight is 1-0.6=0.4 <br> "addition_score": [ <br> { <br> "factor": 1.0, <br> "base_value_from": "scalar_field", <br> "field": "f_sales" <br> }, <br> { <br> "factor": -10.0, // Products with many complaints should have lower score <br> "base_value_from": "scalar_field", <br> "field": "f_complain" <br> } <br> ] <br> } <br>` |
|string_contain |string |Keyword matching filter operator. Indicates the field content contains the pattern. |`JSON <br> { <br> "op": "string_contain", <br> "field": "name", <br> "pattern": "bar" <br> } <br>` |
|string_match |string |Regex matching filter operator. |`JSON <br> { <br> "op": "string_match", <br> "field": "name", <br> "pattern": "^[0-9A-Za-z_]+$" <br> } <br>` |
|enum_freq_limiter |string |Frequency control operator. Used to ensure that in one recall result, the total number of occurrences of a specific value does not exceed `threshold` times. |`JSON <br> { <br> "op": "enum_freq_limiter", <br> "field": "city", <br> "threshold": 5 <br> } <br>` |
