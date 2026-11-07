---
title: "Search Common Parameters"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/search_common_parameters"
---

Search functionality consists of multiple interfaces, each corresponding to different search modes and business scenarios.

<span id="interface-description"></span>
# Interface Description

V2 interfaces map different search modes to different endpoints, making it clearer for you to select the appropriate search method based on your business scenarios.

<span id="common-request-body-parameters-for-search-interfaces"></span>
# Common Request Body Parameters for Search Interfaces


|Parameter Name |Type |Required |Sub\-parameter |Type |Remarks |
|---|---|---|---|---|---|
|resourceId |string |2 out of 1 required | | |Resource ID |
|collectionName |String | | | |Collection name |
|indexName |String |Yes | | |Index name |
|outputFields |List[string] |No | | |List of scalar fields to return.<br><br><br>1. When user does not pass outputFields, all scalar fields are returned<br><br>2. When user passes an empty list, no scalar fields are returned<br><br>3. If outputFields format is incorrect or the field is not in the collection, the interface returns an error |
|filter |Map[String, Object] |No | | |Filter conditions, see format below. Default is empty, no filtering |
|limit |Integer |No | | |Number of search results, default is 10, upper limit is 100000 |
|offset |Integer |No | | |Offset. Only used in pagination scenarios. Setting too large a value is not recommended as it may cause deep pagination performance impact. Default value is 0. Value must be at least 0, semantics are the same as mysql offset. |
|advance (advanced parameter, infrequently used) |SearchAdvance |No |denseWeight |float32 |If the collection has sparse vector fields, you can specify the weights for dense and sparse during search. Default value is 0.5, optional range [0.2, 1] |
| | | |idsIn |List[Object] |Setting this parameter will limit the search to only within the primary key list. Default is empty. |
| | | |idsNotIn |List[Object] |Setting this parameter will exclude data within the primary key list from the search results. Default is empty. |
| | | |postProcessOps |List[Map[String, Object]] |Post\-processing operator list. After the vector or scalar recall phase, further filtering is performed on candidate data, such as string matching, frequency control, etc. Each operator is a map, executed serially. Default is empty. See post\-processing operators below for details. |
| | | |postProcessInputLimit |Int |When postProcessOps is set, the number of candidates entering the post\-processing phase.<br><br>Default value is the above limit parameter value \* 3. If explicitly set, it should not be less than the limit value. |
| | | |scaleK |float64 |The search `sef` is `scale_k` times the index parameter `sef`. Default value is 1, value range [0.1, 100]. The larger the value, the more accurate the search results, but performance will decrease accordingly. |
| | | |filterPreAnnLimit |Integer | |
| | | |filterPreAnnRatio |Double | |


<span id="filter-structure"></span>
## filter Structure

The prerequisite for using filter is that the corresponding scalar field has scalar index (scalarIndex) set.


|Operator |Applicable Field Types |Description |Example |
|---|---|---|---|
|must |string、int64、bool、list[string]、list[int64] |Effective for specified field name, semantics is must be in [...], i.e. "must in" |`JSON <br> { <br> "op": "must", <br> "field": "region", <br> "conds": ["cn", "sg"] <br> } <br>` |
|must_not |string、int64、bool、list[string]、list[int64] |Effective for specified field name, semantics is must not be in [...], i.e. "must not in" |`JSON <br> { <br> "op": "must_not", <br> "field": "data_type", <br> "conds": [1,2,3] <br> } <br>` |
|and |/ |Logical operator, for logical query requirements, takes intersection of multiple conditions |`JSON <br> { <br> "op": "and", // Operator name <br> "conds": [ // Condition list, supports nested logical operators and must/must_not operators <br> { <br> "op": "must", <br> "field": "type", <br> "conds": [1] <br> }, <br> { <br> ... // Supports any number of conditions >= 1 for combination <br> } <br> ] <br> } <br>` |
|or |/ |Logical operator, for logical query requirements, takes union of multiple conditions |`JSON <br> { <br> "op": "or", // Operator name <br> "conds": [ // Condition list, supports nested logical operators and must/must_not operators <br> { <br> "op": "must", <br> "field": "type", <br> "conds": [1] <br> }, <br> { <br> ... // Supports any number of conditions >= 1 for combination <br> } <br> ] <br> } <br>` |
|range |int64、float32 |Effective for specified field name, semantics is must be within specified range. Configured using `gte` (greater than or equal), `gt` (greater than), `lte` (less than or equal), `lt` (less than), to define a one\-dimensional range. |`Python <br> // price is in [100.0, 500.0) <br> { <br> "op": "range", <br> "field": "price", <br> "gte": 100.0, <br> "lt": 500.0 <br> } <br> <br> // price >= 100.0 <br> { <br> "op": "range", <br> "field": "price", <br> "gte": 100.0 <br> } <br>` |
|time_range |date_time |Time point filtering, configured using `gte` (greater than or equal), `gt` (greater than), `lte` (less than or equal), `lt` (less than), to define a one\-dimensional range. |`JSON <br> { <br> // Search data between Beijing time 2025-08-12 00:00:00 ~ 2025-08-13 00:00:00 <br> "op": "time_range", <br> "field": "f_date_time", <br> "gt": "2025-08-12T00:00:00+08:00", <br> "lt": "2025-08-13T00:00:00+08:00", <br> } <br>` |
|geo_range |geo_point |Geographic distance filtering, uses `center` as the center point, `radius` as the distance radius. |`JSON <br> { <br> "op": "geo_range", <br> "field": "f_geo_point", <br> "center": "116.412138,39.914912", <br> "radius": "10000m" <br> } <br>` |


<span id="post-processing-structure"></span>
## Post\-processing Structure


|Operator |Applicable Field Types |Description |Example |
|---|---|---|---|
|score_fusion |string |Score fusion operator, used to fuse scores from specified spatiotemporal scalars. |`JSON <br> { <br> "op": "score_fusion", <br> "fusion_by": "add", <br> "addition_score_weight": 0.6, // Additional score weight is 0.6 ann score weight is 1-0.6=0.4 <br> "addition_score": [ <br> { <br> "factor": 1.0, <br> "base_value_from": "scalar_field", <br> "field": "f_sales" <br> }, <br> { <br> "factor": -10.0, // Products with more complaints should have lower scores <br> "base_value_from": "scalar_field", <br> "field": "f_complain" <br> } <br> ] <br> } <br>` |
|string_contain |string |Keyword matching filter operator. Indicates that the field content contains pattern. |`JSON <br> { <br> "op": "string_contain", <br> "field": "name", <br> "pattern": "bar" <br> } <br>` |
|string_match |string |Regular matching filter operator. |`JSON <br> { <br> "op": "string_match", <br> "field": "name", <br> "pattern": "^[0-9A-Za-z_]+$" <br> } <br>` |
|enum_freq_limiter |string |Frequency control operator. Used to ensure that in the results of one recall, the total number of occurrences of a specific value does not exceed `threshold` times. |`JSON <br> { <br> "op": "enum_freq_limiter", <br> "field": "city", <br> "threshold": 5 <br> } <br>` |
