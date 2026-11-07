---
title: "Search"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Search"
---

***Viking AI Search*** * is an enterprise\-level AI search product powered by generative AI. It leverages the multimodal semantic understanding of large models and ByteDance's extensive experience in information retrieval to offer an out\-of\-the\-box platform. This service allows customers to easily build and integrate end\-to\-end multimodal search and recommendation capabilities for both images and text. * 


---



Searches for content related to the user's input query or image within the item data source bound to the application.

<span id="013d18cf"></span>
## Request description


* Request method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/search/{scene_id}` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{scene_id}` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/search/{scene_id}` |


`{application_id}:` the unique identifier for an application, assigned by the system after creation. You can view this ID in the console.

`{scene_id}:` the unique policy identifier assigned by the system after a new search policy is created on the experience configuration page in the console. You can find it by navigating to "Search Experience" in the console, hovering over the policy name, and copying the policy ID.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a9ceb28a289347e19ac0f4df665f6347) </span>

&nbsp;

<span id="56d4d3f1"></span>
## Notes


* **Scope of Use:** 

   * Only available for Item datasets. Search is not supported for Document and User Behavior datasets.

* **Request Body Limit:** 

   * The body of a single request cannot exceed 10 MB.


<span id="323cb778"></span>
## API Rate Limiting

The call rate limit is 20 QPS per tenant.

Calls that exceed the API rate limit will return a 429 status code.

<span id="a020560d"></span>
## Authentication Method

Use an API Key or Access Key for authentication. For details, refer to the [API Authentication Guide](https://www.volcengine.com/docs/85296/1544950).

<span id="886126fa"></span>
## Request Parameters

<span id="a89eee90"></span>
### Path Parameters


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|application_id |String |<span data-api-tag="require\|aKyz1BVo9">必选</span> |76414365027 |Your unique application identifier. |
|scene_id |String |<span data-api-tag="require\|aMasiXdB9">必选</span> |1024 |The unique identifier of the scenario. |


<span id="7408d8c7"></span>
### Body Parameters


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`query` |[Query](https://docs.byteplus.com/docs/viking-aisearch/Search#7d914235) |<span data-api-tag="require\|aKyz1BVo9">必选</span> |&nbsp;<br><br>```Plain Text```<br>```{```<br>```    "text":"同款鞋",```<br>```    "image_url":{base64图片文件}```<br>```}```<br> |The text or image information for the search query passed in the Query object. Options:<br><br><br>* Text search only<br><br>* Image search only<br><br>* Image and text search<br><br><br>For parameter details, see: [Query](https://docs.byteplus.com/docs/viking-aisearch/Search#7d914235) |
|`dataset_id` |string |<span data-api-tag="require\|aMasiXdB9">必选</span> |"106265704" |The dataset ID can be viewed in the dataset list or on the dataset details page. When using the direct search feature, you must explicitly specify the dataset ID in each request. |
|`page_number` |int |<span data-api-tag="require\|a35KR2QyB">必选</span> |1 |The page number for search results, used for list pagination, starting from 1. For example: "page_number": 1 returns the first page of search results. |
|`page_size` |int |<span data-api-tag="require\|aSkF39i9s">必选</span> |20 |The number of search results per page. You can enter a value from 1 to the maximum number of results you set in the console.<br><br>To ensure optimal performance and reduce loading times on the client side, we recommend setting the page size to a maximum of 100 and loading additional data through pagination.<br><br>Default: 10 |
|`user` |[User](https://docs.byteplus.com/docs/viking-aisearch/Search#9dc80774) |Optional |```JSON```<br>```{```<br>```    "_user_id":"U90E89FF8045"```<br>```}```<br> |Enter the User object with the searching user's information. You can upload the user's pseudo ID to specify which user triggered this API call. |
|`filter` |[Filter](https://docs.byteplus.com/docs/viking-aisearch/Search#aead416b) |Optional |See the data structure below\-[Filter](https://docs.byteplus.com/docs/viking-aisearch/Search#aead416b) |A search filter object that filters search results based on the filterable fields configured in the application's data source.<br><br><br>* The default value is empty, meaning no filter is applied to the search results.<br><br>* Filter conditions support the `must`, `must_not`, and `range` query operators, as well as the `and` and `or` logical operators. You can combine these query operators. |
|`sort_by` |string |Optional |"create_at" |The name of the field used for sorting. **The field must exist in the dataset and have "Used for filtering" selected in the application.**  The following types are supported:<br><br><br>* **Basic types**: `int32`, `int64`, `float`, `bool`, `string`<br><br>* **Complex types**: To sort the sub\-fields of an `object` type, use a `.` The connector references internal fields using the format `object.field`, for example, `product.price`. |
|`sort_order` |string |Optional |"desc" |Sort order. Supported enumerated values: "desc"\|"asc":<br><br><br>* "desc": Descending order (default if not specified)<br><br>* "asc": Ascending order |
|`output_fields` |array(string) |Optional |["title", "price", "category"]<br><br> |Specify which fields from the item dataset to return for display in 'display_fields'. If this parameter is not provided, all fields will be returned.<br><br>> If the dataset contains nested objects (object or array<object\>), you can only pass top\-level field names.<br><br>> Fields that do not exist or are nested within an object will be ignored. |
|`context` |object(context) |Optional |See the data structure below: [Context](https://docs.byteplus.com/docs/viking-aisearch/Search#7f9aa6e1) |Configures the request context. It currently supports passing the geographic location of the user initiating the search. |
|`conditional_boost` |array(conds) |Optional |See: [Conds](https://docs.byteplus.com/docs/viking-aisearch/AI_Search_Boost_Demotion#ca81d523) |Request\-level promotion and demotion configuration<br><br>> Learn more: [AI Search: Boost and Demotion](https://docs.byteplus.com/docs/viking-aisearch/AI_Search_Boost_Demotion)<br><br><br>The platform automatically merges promotion and demotion rule configurations from the console and API, and they take effect simultaneously. |
|`disable_personalize` |Boolean |Optional |false |**Whether to Close Search "Personalized Retrieval" Ability**<br><br>Defaults to false.<br><br>When the input parameter is true, search results are sorted only according to the following two aspects:<br><br><br>1. Item relevance (default logic, cannot be removed)<br><br>2. Item popularity (premised on having enabled this feature in the console; if not enabled, it has no effect. For feature details, see [Configure item heat rank participation](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#294a09ed))<br><br><br>&nbsp;<br><br>When the input parameter is false, in addition to the above, search results can also be adjusted based on the following aspects:<br><br><br>1. user personalized retrieval (the prerequisite is that this function is enabled on the console; if not enabled, it will not take effect; function details see [Enable Personalized Retrieval](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#b1e67f28)) |
|`query_keyword_match_percent` |float |Optional |0.8 |Used to specify the match degree threshold of the query keyword in ES item retrieval, **the value range is [0,1]** , the example explanation is as follows:<br><br><br>* when set to 1, the search query's tokenized results must match the text information in the item 100% accurately for the item to be retrieved by ES;<br><br>* when set to 0.8, after the search query is tokenized, only 80% of the tokens need to hit for the item to be retrieved; suppose a search query is tokenized into three tokens, 3\*80%=2.4, which will be rounded down to needing to match two query tokens for the item to be retrieved.<br><br><br>**Default: 1** |
|`facet` |[Facet](https://docs.byteplus.com/docs/viking-aisearch/Search#951b95a9) |Optional |See the data structure below \-[Facet](https://docs.byteplus.com/docs/viking-aisearch/Search#951b95a9) |Used to specify the field for search results grouping and filtering.<br><br><br>* The default value is empty. |
|`sort_rules` |[SortRules](https://docs.byteplus.com/docs/viking-aisearch/Search#5222cd88) |Optional |&nbsp;<br><br>```Plain Text```<br>```"sort_rules": {```<br>```    "mode": "merge",```<br>```    "rules": [```<br>```     {```<br>```     "field": "updated_at", ```<br>```     "order": "desc"```<br>```      }```<br>```     ]```<br>```  }```<br> |Sort results with similar search relevance using the sorting rules defined by this parameter.<br><br>This parameter corresponds to the [Configure customized Sorting rules](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#39776d7b) feature on the Viking AI Search console:<br><br>The main difference between this parameter and `sort_by`, `sort_order` is:<br><br>`sort_by` does not consider search relevance and globally sorts by field directly. If you want to ensure search result relevance while partially controlling the result sorting, you can use `sort_rules`.<br><br>**When using**`sort_rules` **, search results are first sorted by relevance, then results with the same relevance level are sorted by the rules**. This ensures low\-relevance items do not appear before high\-relevance items due to sorting rules. |


<span id="d055ad90"></span>
### Data Structure

<span id="7d914235"></span>
#### Query


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|text |string |At least one is required |"Women's shoes spring/summer" "The Three\-Body Problem" |Text query |
|image_url |string ||"data:image/jpeg;base64,iVBUAAAA..."<br><br>"www.example.com/image.png" |Image Search<br><br>**Applications linked to video datasets do not support ** **image search.**  |
|image_query_instruction |string |Optional when the `image_url` field is provided |"Retrieve similar images based on their overall content, rather than focusing on specific details within the image" |An instruction for image search used to enhance search performance in search\-by\-image scenarios |


<span id="f9bdf529"></span>
##### **Uploading Images in Query**

For the image passed in `query.image_url`, we support either an **image URL (recommended)**  or a **base64\-encoded** image file.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Limits</div>


<div data-tips="true" data-tips-type="default"><strong>Input images must meet the following conditions</strong><strong>:</strong></div>


<div data-tips="true" data-tips-type="default"><strong>Supported formats:</strong> jpeg, png, webp, bmp, tiff, icns. For tiff and icns images, ensure they align with their metadata by correctly setting the file metadata in object storage. Otherwise, parsing will fail.</div>


<div data-tips="true" data-tips-type="default"><strong>Aspect ratio (width/height):</strong> Within the range [1/100, 100].</div>


<div data-tips="true" data-tips-type="default"><strong>Side length:</strong> [10, 6000] px. The shorter side must be greater than 10 px, and the longer side must be less than 6000 px.</div>


&nbsp;

**Option 1: Image URL (Recommended)** 

Ensure the image URL is publicly accessible and triggers a preview instead of a download when accessed.

&nbsp;

**Option 2: Base64 Format**

Ensure the Base64 encoding is in the standard format, including two parts: **a data header (Data URI Scheme)**  and **a Base64\-encoded body**.

```Plain Text
data:[<MIME type>];base64,<Base64 encoded string>
```



|**Components** |**Format requirements** |**Description** |**Example** |
|---|---|---|---|
|Data header prefix |Must be `data:` |Indicates the string is in Data URI format and cannot be omitted or modified |\- |
|MIME Type |Must strictly match the actual image format. |Used by the server to identify the image type. Do not enter incorrect information, such as using the PNG MIME type for a JPG image. |JPG/JPEG：`image/jpeg`；PNG：`image/png`；WebP：`image/webp` |
|Separator |Always `;base64,` |Connects the MIME type with the Base64 encoded body. The semicolon, "base64", and comma cannot be omitted or replaced. |\- |
|Base64 Encoded Body |A Base64\-encoded string that complies with the RFC 4648 standard. |Generated by directly encoding the binary data of an image file. **It cannot contain spaces, line breaks, or special characters** and must be a continuous ASCII string. | |


<span id="9dc80774"></span>
#### User


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`_user_id` |string |Optional |"ldy_199432" |This represents **a unique identifier for the end\-user**.<br><br>This field specifies the user who triggered the API call, which is crucial for distinguishing between different users from the same organization.<br><br>For example, it can help you record detailed operation logs, provide personalized recommendations, or analyze different user behavior patterns. We recommend assigning and passing a unique ID for each end\-user. |


<span id="aead416b"></span>
#### Filter


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`op` |string |<span data-api-tag="require\|abhTKcjeG">必选</span> |"must" |The supported operator types are:<br><br>"must"、"must_not"、"range"、"and"、"or" |
|`field` |string |Condition required |"status" |The field to which the filter condition is applied.<br><br><br>* Required for the "must", "must_not", and "range" operators.<br><br>* The "and" and "or" operators ignore this parameter. |
|`gte` |Float |Optional |100.0 |The filter range for the "range" operator, which filters data where the "field" value is `greater than or equal to` the specified value. |
|`gt` |Float |Optional |100.0 |The filter range for the "range" operator, filtering data where the "field" value is `greater than` the specified value. |
|`lte` |Float |Optional |500.0 |The filter range for the "range" operator, filtering data where the "field" value is `less than or equal to` the specified value. |
|`lt` |Float |Optional |500.0 |The filtering range of the "range" operator. It filters data where the "field" value is `less than` a specified value. |
|`conds` |array |Condition required |See the example below. |All operators except "range" require the conds condition.<br><br><br>* The "must" and "must_not" operators require a set of filter values.<br><br>* The "and" and "or" operators require nested filtering conditions. |


**Filter Operator (op) Examples**


|**Operator** |**Filtered field (field) type** |**Operator Description** |**Example** |
|---|---|---|---|
|must |* int32<br><br>* int64<br><br>* string<br><br>* Bool<br><br>* array(int32)<br><br>* array(int64)<br><br>* array(string) |Conditional expression parameter syntax:<br><br><br>* `op`: pass in "must"<br><br>* `field`: pass the target field for filtering<br><br>* `conds`: Enter a list of filter values. The element type must match the field type.<br><br><br>When `field` is a single integer or string, it means  **"is in"** , i.e., the field's value is in the provided filter list.<br><br>When `field` is a list of integers or strings, it means  **"intersects with"** , i.e., the target field and the filter list have common elements. |**Example 1:**  the region must be "cn" or "sg".<br><br>```JSON```<br>```{```<br>```    "op": "must",```<br>```    "field": "region",```<br>```    "conds": ["cn", "sg"]```<br>```}```<br><br><br>**Example 2:**  the status value must be one of 1, 2, or 3.<br><br>```JSON```<br>```{```<br>```    "op": "must",```<br>```    "field": "status",```<br>```    "conds": [1, 2, 3]```<br>```}```<br><br><br> |
|must_not |* int32<br><br>* int64<br><br>* string<br><br>* Bool<br><br>* array(int32)<br><br>* array(int64)<br><br>* array(string) |Conditional expression parameter syntax:<br><br><br>* `op`: Enter "must_not"<br><br>* `field`: pass the target field for filtering<br><br>* `conds`: Enter a list of filter values. The element type must match the field type.<br><br><br>When `field` is a single integer or string element, it means  **"does not belong to"** , i.e., the target field value is not in the filter list.<br><br>When `field` is a list of integers or strings, it means  **"no intersection"** , i.e., the elements in the target field and the filter list do not overlap. |The status value cannot be 1, 2, or 3.<br><br>```JSON```<br>```{```<br>```    "op": "must_not",```<br>```    "field": "status",```<br>```    "conds": [1, 2, 3]```<br>```}```<br><br><br> |
|range |* int32<br><br>* int64<br><br>* Float |Conditional expression parameter syntax:<br><br><br>* `op`: enter "range"<br><br>* `field`: pass the target field for filtering<br><br>* `gt`: Greater than<br><br>* `gte`: Greater than or equal to (for integers only)<br><br>* `lt`: Less than<br><br>* `lte`: Less than or equal to (for integers only)<br><br><br>The value of the target numeric field must be within the specified range.<br><br>Use `gte` (greater than or equal to), `gt` (greater than), `lte` (less than or equal to), and `lt` (less than) to define a numeric range. |**price \>= 100.0**<br><br>```JSON```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0```<br>```}```<br><br><br>**price is between 100.0 and 500.0**<br><br>```JSON```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0,```<br>```  "lt": 500.0```<br>```}```<br> |
|time_range<br><br> |The filtered field must have the 'New Arrival Time' property. Supported:<br><br><br>* Int64: UNIX timestamp<br><br>* String: ISO 8601 time format; or "YYYY\-Mm\-DD hh:mm:ss.sss" format<br><br><br>For details, see [Review Reserved Field Attributes](https://docs.byteplus.com/docs/viking-aisearch/Introduction_Image_Text_Dataset#bb64f3ff) |Conditional expression parameter syntax:<br><br><br>* `op`: pass "time_range"<br><br>* `field`: pass the target field for filtering<br><br>* `gt`: later than<br><br>* `lt`: earlier than<br><br><br>The target filter field must be within a time range. Supported input values for `gt` and `lt`:<br><br><br>* Absolute time condition (fixed period): Pass in a UNIX timestamp (int) **accurate to the millisecond**.<br><br>* Relative time condition (relative to the request time): Pass in the expression "now[+/\-][value][d/h/m/s]" as a string. Relative time expression examples:<br><br>   * `now+2d`: A point in time 2 days after the current time.<br><br>   * `now-24h`: A point in time 24 hours before the current time.<br><br><br> |**Published after 2026**<br><br>```JSON```<br>```{```<br>```  "op": "time_range",```<br>```  "field": "publish_time",```<br>```  "gt": 1767196800000,```<br>```}```<br><br><br>**Published within the last month**<br><br>```JSON```<br>```{```<br>```  "op": "time_range",```<br>```  "field": "publish_time",```<br>```  "gt": "now-30d",```<br>```}```<br> |
|geo_distance |This Field in your item dataset must be an **Object** type, and it must `Include` `latitude` and `longitude` two subfields. List of Object is not supported. |Conditional expression parameter syntax:<br><br><br>* `op`: input "geo_distance"<br><br>* `field`: field name requiring geographical location Filter. This Field type must be an Object containing `latitude` and `longitude` subfields.<br><br>* `center`: the reference point for distance calculation, formatted as a `"{longitude},{latitude}"` string. if this parameter is not provided, the default reference point is the value of `context.location` in the search interface request.<br><br>* `radius`: distance range, formatted as a `"{Value}{unit}"` string. for example: `"5km"`, `"10000m"`. |**example one: use the user's current location as the reference point**<br><br>this example filters all items with the `store_location` field within 5 kilometers of the user's current location (passed through `context.location`).<br><br>```JSON```<br>```{```<br>```    "query": {```<br>```        "text": "mexican food nearby"```<br>```    },```<br>```    "context": {```<br>```        "location": {```<br>```            "longitude": "116.412138",```<br>```            "latitude": "39.914912"```<br>```        }```<br>```    },```<br>```    "filter": {```<br>```        "op": "geo_distance",```<br>```        "field": "store_location",```<br>```        "radius": "5km"```<br>```    }```<br>```}```<br><br><br>**example two: use a specified latitude and longitude as the reference point**<br><br>this example filters all items with the `store_location` field within 10,000 meters of the specific latitude and longitude coordinates (`121.4737,31.2304`).<br><br>```JSON```<br>```{```<br>```    "query": {```<br>```        "text": "hotel near Times Square"```<br>```    },```<br>```    "filter": {```<br>```        "op": "geo_distance",```<br>```        "field": "store_location",```<br>```        "center": "121.4737,31.2304",```<br>```        "radius": "10000m"```<br>```    }```<br>```}```<br> |
|and |Not applicable |Logical operator: Finds the intersection of multiple conditions for logical queries. |&nbsp;<br><br>```JSON```<br>```{```<br>```  "op": "and",```<br>```  "conds": [     // Condition list, supports nested and/or/must/must_not/range operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "status",```<br>```      "conds": [1, 2, 3]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining any number of conditions (>=1).```<br>```    }```<br>```  ]```<br>```}```<br><br><br> |
|or |Not applicable |A logical operator that finds the union of multiple conditions for logical queries. |&nbsp;<br><br>```JSON```<br>```{```<br>```  "op": "or",```<br>```  "conds": [ // Condition list, supports nested and/or/must/must_not/range operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "status",```<br>```      "conds": [1, 2, 3]```<br>```    },```<br>```    {```<br>```        ...      // Supports combining any number of conditions (>=1).```<br>```    }```<br>```  ]```<br>```}```<br><br><br> |


<span id="7f9aa6e1"></span>
#### Context


|**Parameter** |**Example Value** |**Description** |
|---|---|---|
|`location` |```JSON```<br>```{```<br>```    "latitude": "12.12",```<br>```    "longitude": "-13.43"```<br>```}```<br> |1. Accepts user location data for configuring item boosting and de\-boosting based on geography. The input data must be a string.<br><br>2. If the input is invalid, the platform ignores the LBS configuration. |


<span id="951b95a9"></span>
#### Facet


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`facets` |Array <facets\> |Optional<br><br> |```Plain Text```<br>```"facets": [```<br>``` {  ```<br>``` "field": "tags",        ```<br>``` "max_facet_buckets": 10     ```<br>``` },```<br>``` {```<br>``` "field": "price",      ```<br>``` "number_ranges": [```<br>``` { "gte": 0, "lt": 19},{ "gte": 10, "lt": 100},{"gte": 200, "lt": 999}```<br>``` // Configurable value range```<br>``` ]```<br>``` }```<br>``` ]```<br> |Specify the facet fields, value ranges, and the maximum number of Enum values to return for aggregation of search results.<br><br>If not passed in, the fields already configured in Console \- Experience center \- **Facet** will be used by default<br><br>Parameter Details can be viewed at: [facets](https://docs.byteplus.com/docs/viking-aisearch/Search#39369208)<br><br> |
|`facet_filter`<br><br> |facet_filter<br><br> |Optional<br><br> |&nbsp;<br><br>```Plain Text```<br>```"facet_filter":{```<br>```{```<br>```    "op": "must",```<br>```    "field": "region",```<br>```    "conds": ["cn", "sg"]```<br>```},```<br>```{```<br>```    "op": "must_not",```<br>```    "field": "status",```<br>```    "conds": [1, 2, 3]```<br>```}```<br>```}```<br> |This parameter specifies the facet filter for the current search request.<br><br>If not passed in, no facet filter will be applied, the initial search results will be returned.<br><br>Same as [Filter](https://docs.byteplus.com/docs/viking-aisearch/Search#aead416b)<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/697f45ca273d400e8d178ef1c619b776) </span><br><br> |


<span id="39369208"></span>
##### facets


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|field |String |<span data-api-tag="require\|aR1cRq5eN">必选</span> |"brand" |Field name used for aggregate statistics |
|number_ranges |Array<NumberRange\><br><br>`NumberRange` is of OBJECT type |Optional<br><br>Defaults to empty |"{ "gte": 0, "lt": 19}" |If a field of numeric type (int, float, Array<int\>, Array<float\>) is designated as the category statistics field, it is suggested to preset the value range to aggregate statistics on search results based on the value range.<br><br>Currently, **4** operators for defining value ranges are supported:<br><br><br>* gte: semantics filter data where the \"field\" field value is `greater than or equal to` the specified value.<br><br>* gt: semantics filter data where the \"field\" field value is `greater than` the specified value.<br><br>* lte: semantics filter data where the \"field\" field value is `less than or equal to` the specified value.<br><br>* lt: semantics filter data where the \"field\" field value is `less than` the specified value.<br><br><br>If not passed in, facet would be performed by default based on the original field values. |
|max_facet_buckets |Int |Optional<br><br>the default value is 10 |10<br><br> |used to set how many enums each field would be returned at most, the default is 10, and the upper limit is 50.<br><br>if not passed, it will be processed according to the default value 10. |


&nbsp;

<span id="5222cd88"></span>
#### SortRules


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|mode<br><br> |String |Optional |merge |String enumeration: `merge` / `override`.<br><br><br>* merge: both the API\-defined rule and the console\-configured rule take effect, with API\-configured rules taking priority<br><br>* override: the sorting rule defined by the API directly overrides the console\-configured rule, only API configuration takes effect<br><br>* Empty value defaults to `merge`.<br><br>* Invalid value: server returns parameter error (InvalidParameter). |
|rules |repeated SortRule |required |see the details below |the sorting rule list specified via API.<br><br>parameter details are in the notes below. |


<span id="ba5be231"></span>
##### **repeated SortRule**


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|field<br><br> |String<br><br> |required |"price" |specify the field to use for the sorting rule, supporting the following types:<br><br><br>* **basic types**: int32, int64, float, bool, string<br><br>* **complex types**: for sorting sub\-level fields of object type fields, use "." the connector references internal fields, in the format object.field, such as product.price. |
|order |String |required |"desc" |Sort order. Supported enumerated values: "desc"\|"asc":<br><br><br>* "desc": Descending order (default if not specified)<br><br>* "asc": Ascending order |


&nbsp;

&nbsp;


---



&nbsp;

<span id="b985afcd"></span>
## Response Parameters

<span id="6b7c4144"></span>
#### Request and Response


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|`request_id` |string |25ee998a\-5462\-9385\-9f18\-035f1da7a6e5 |A unique identifier for a request. Use this ID to quickly track its execution. |
|`spell_correction` |SpellCorrection |{"mode": "auto",<br><br>  "corrected_query": "Three\-Body TV series episodes"} |Returns the correction mode configuration and the corrected search term suggestion when search term correction is triggered. |
|`result` |Result |{"search_results": [...], "spell_correction": {...}, <br><br>"total_items": 300} |Search result. |
|`total_items` |int |300 |The total number of search results returned |
|`facet_results` |Array<[FacetResult](https://docs.byteplus.com/docs/viking-aisearch/Search#0c32f585)\> |{<br><br>"field": "content_type",<br><br>    "counts": [<br><br>      {"value": "video", "count": 260},<br><br>      {"value": "collection", "count": 40}<br><br>]<br><br>} |results of breakdown results by category for search results |


<span id="5c47a38b"></span>
#### Data Structure

<span id="e18cd336"></span>
##### SpellCorrection


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|`mode` |string |"suggestion_only" |The search correction mode configured in the console, which returns two enumerated values:<br><br><br>* "suggestion_only": Only returns suggested search terms, and uses the original user\-uploaded term for the search.<br><br>* "auto": Automatically uses the corrected search term for the search.<br><br>* "off": The search term correction feature is not enabled in the console. |
|`corrected_query` |string |"4K display TV" |The corrected search query. An empty value indicates that no search terms needed correction. |


&nbsp;

<span id="b4a611ca"></span>
##### Result


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|`search_results` |array<[SearchResult](https://docs.byteplus.com/docs/viking-aisearch/Search#7a70ec00)\> |&nbsp;<br><br>```JSON```<br>```[```<br>```  {```<br>```    "_id": "ITEM0001",```<br>```    "display_fields": {```<br>```      "multi_modal_id": "ITEM0001",```<br>```      "multi_modal_content": "Sample content for the 2026 Year of the Horse Spring Festival gift box.",```<br>```      "multi_modal_image_url": [```<br>```        "https://example.com/images/detail_1.jpg"```<br>```      ]```<br>```    }```<br>```  }```<br>```]```<br><br><br> |List of search results. |
|`total_items` |int |300 |The total number of search results, which is the number of candidates. You can adjust the maximum number of items to recall in the application configuration, but the final count depends on the total amount of relevant data in the data source. |


<span id="7a70ec00"></span>
##### SearchResult


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|`_id` |string |"WSHOE001"<br><br>"video_900026" |The primary key for this data in data storage is the value from the field with the **unique identifier** attribute in your uploaded content. |
|`display_fields` |object |Image and text data:<br><br>```Plain Text```<br>```{ ```<br>```    "item_id": "WSHOE001", ```<br>```    "title": "Comfort Commuter Pointed-Toe Shallow Heels - Black", ```<br>```    "category": "Women's High Heels", ```<br>```    "status": 1```<br>```}```<br><br><br>Video data:<br><br>```JSON```<br>```{```<br>```  "_video_generated_summary": "To prevent Lei Zhicheng from reporting the signal transmission, Ye Wenjie staged an accident to lure him and Yang Weining off a cliff, then cut the rope and killed them. Shi Qiang was hospitalized due to radiation exposure. Ye Wenjie recalled the warmth she experienced in Qijiatun and her later experiences. Meanwhile, the operations center intercepted information from the Trisolarans, and Wang Miao and Shi Qiang entered the Three-Body game and encountered Listener No. 1379.",```<br>```  "video_generated_title": "Ye Wenjie Admits to Killing Lei Zhicheng",```<br>```  "content_id": "video_900026",```<br>```  "content_type": "video",```<br>```  "parent_content_id": "collection_342534",```<br>```  "sequence_index": 26,```<br>```  "video_url": ["http://xxxx.mp4"],```<br>```  "my_title": "Three-Body Episode 26"```<br>```}```<br> |Other fields in the dataset are the same as the fields from the data import. |
|`score` |Float |0.852 |The merged score from multiple recall channels |
|`recall_info`<br><br> |array<object\><br><br> |```JSON```<br>```[```<br>```    {```<br>```        "recall_reason": "text'",```<br>```        "recall_score": 0.7```<br>```    },```<br>```    {```<br>```        "recall_reason": "vlm'",```<br>```        "recall_score": 0.5```<br>```    }```<br>```]```<br> |Records the information for each recall path.<br><br>recall_reason indicates the recall method. It currently supports "text" for text recall and "vlm" for image recall.<br><br>recall_score indicates the relevance score for the recall path. |
|`rerank_info`<br><br> |object |```JSON```<br>```{```<br>```    "is_reranked": true,```<br>```    "rerank_score":0.993242```<br>```}```<br><br><br> |Reranking information for recalled data, which indicates whether the data has been reranked and its rerank score. The `rerank_score` field does not exist for data that has not been reranked. |


<span id="0c32f585"></span>
##### FacetResult


|**Parameter** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|field |string<br><br> |"category" |facet field |
|buckets |Array<buckets\> |[<br><br> { "value": "iphone", "count": 2345 },<br><br> { "value": "vivo", "count":230},<br><br> { "value": "xiaomi", "count": 100}<br><br> ] |results of faceting |


&nbsp;

<span id="9a2cd0f2"></span>
## API Example

<span id="6fa5ee84"></span>
### Using the Associated Image\-Text Dataset

<span id="aac4fbf5"></span>
#### Request Example

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/search/${scene_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "query": {
        "text": "women shoes summer"
    },
    "page_number": 1,
    "page_size": 5,
    "user": {
        "_user_id": "ldy_199432"
    },
    "filter": {
        "op": "must",
        "field": "status",
        "conds": [1, 2]
    },
    "dataset_id": "106265704",
    "context": {
        "location":{
            "latitude": "12.12",
            "longitude": "-13.43"
        }
    }
}'
```


<span id="346c1b3b"></span>
#### Response Example

```JSON
{
  "request_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",
  "result": {
    "search_results": [
      {
        "_id": "WSHOE001",
        "display_fields": {
          "item_id": "WSHOE001",
          "title": "Comfort Commuter Pointed-Toe Shallow Heels - Black",
          "category": "Women's High Heels",
          "status": 1,
          "images": [
            {
              "image_url": "https://example.com/images/womens_pump_black.jpg"
            }
          ]
        }
      },
      {
        "_id": "WSHOE002",
        "display_fields": {
          "item_id": "WSHOE002",
          "title": "Lightweight Mesh Running Sneakers - Pink/Grey",
          "category": "Women's Athletic Shoes",
          "status": 1,
          "images": [
            {
              "image_url": "https://example.com/images/womens_sneaker_pink.jpg"
            }
          ]
        }
      },
      {
        "_id": "WSHOE003",
        "display_fields": {
          "item_id": "WSHOE003",
          "title": "Bohemian Style Wedge Sandals - Beige",
          "category": "Women's Sandals",
          "status": 2,
          "images": [
            {
              "image_url": "https://example.com/images/womens_sandal_beige.jpg"
            }
          ]
        }
      }
    ],
    "spell_correction": {
      "mode": "off"
    },
    "total_items": 300
  }
}
```


&nbsp;

<span id="c9700cd8"></span>
### Using the Associated Video Dataset

<span id="98dd32cb"></span>
#### Request Example

```JSON
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/${application_id}/search/${scene_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: <Volcengine_Auth_Headers>' \
  -d '{ 
    "query": { 
        "text": "Sci-Fi Movies" 
    }, 
    "page_number": 1, 
    "page_size": 5, 
    "user": { 
        "_user_id": "ldy_199432" 
    }, 
    "filter": {
        "op": "must",
        "field": "director",
        "conds": ["Christopher Nolan"]
    },
    "dataset_id": "106265704",
    "context": {
        "location":{
            "latitude": "12.12",
            "longitude": "-13.43"
        }
    }
}'
```


<span id="96905c72"></span>
#### Response Example

```JSON
{
  "request_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",
  "result": {
    "search_results": [
      {
        "_id": "video_900026",
        "display_fields": {
          "content_id": "video_900026",
          "content_type": "video",
          "parent_content_id": "collection_342534",
          "sequence_index": 26,
          "video_url": [
            "http://xxxx.mp4"
          ],
          "my_title": "Stranger Things Episode 26"
        }
      },
      {
        "_id": "video_900027",
        "display_fields": {
          "content_id": "video_900027",
          "content_type": "video",
          "parent_content_id": "collection_342534",
          "sequence_index": 27,
          "video_url": [
            "http://xxxx.mp4"
          ],
          "my_title": "Stranger Things Episode 27"
        }
      },
      {
        "_id": "video_900028",
        "display_fields": {
          "content_id": "video_900028",
          "content_type": "video",
          "parent_content_id": "collection_342534",
          "sequence_index": 28,
          "video_url": [
            "http://xxxx.mp4"
          ],
          "my_title": "Stranger Things Episode 28"
        }
      }
    ],
    "spell_correction": {
      "mode": "auto",
      "corrected_query": "Stranger Things TV Series"
    },
    "total_items": 300
  }
}
```


&nbsp;

<span id="a6e18099"></span>
## Error Handling

<span id="b886a808"></span>
### Error Code


|**HTTP Status Code** |**Error Code** |**Error Message** |**Meaning** |
|---|---|---|---|
|400 |`MissingParameter` |The request is missing the following parameter: {parameters} |A required parameter is missing in the request. |
|400 |`InvalidParameter` |A parameter in the request is not valid: {parameters} |The parameter is invalid, for reasons such as an incorrect data type, invalid length, an invalid enum value, or failure to match a regular expression. |
|400 |`InvalidRequestFormat` |The request cannot be parsed in JSON format. |Failed to parse the request body. This usually occurs when the request body has an invalid format, such as an illegal JSON format or a structure that does not match the request definition. Refer to the corresponding API documentation to check the request structure. |
|400 |`InvalidAction` |The specified action is invalid: {Action} |The Action in the request path does not exist or is temporarily unavailable:<br><br><br>* `search`: Unable to perform a search. This may occur if the index has not taken effect after the dataset was associated, or if the application is not associated with a dataset for the corresponding dataset_id. |


For other common error codes, see the [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)documentation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To explore more Viking AI search capabilities, visit the <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, an all\-in\-one intelligent engine for enterprise search, recommendation, and Q&A</a>.</div>
