---
title: "BrowseIndex"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/browseindex"
---

***Viking AI Search*** * is an enterprise\-grade AI search product based on generative AI. Leveraging the multimodal semantic representation and understanding capabilities of large models and ByteDance's years of best practices in information retrieval, it provides customers with an out\-of\-the\-box AI search platform service to help them easily build and integrate end\-to\-end multimodal image\-text search and recommendation capabilities. * 


---



You can use this interface to browse and query **data from datasets that are associated with the application and have an active index:** 

<span>![图片](blob:https://arcosite.bytedance.net/ec6eeda4-bd83-4861-8175-efd725c6992e) </span>

&nbsp;

<span id="b5ae4987"></span>
## Note


* **Scope: ** This API only supports item dataset type. Document datasets and user event datasets are not supported

   * This can be used only for datasets of the item dataset type. Document datasets and user event datasets do not support retrieval via the browse interface.

* **Request body limit: ** Due to the HTTP body size limit, the body of a single request cannot exceed 10 MB.

   * Due to the HTTP body size limit, the body of a single request cannot exceed 10 MB.

* **items quantity limit:** 

   * A single index (dataset associated in the application) can only page query up to **10,000** data records.


<span id="c91b7050"></span>
## Request details


* Request method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/browse_index` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/browse_index` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/browse_index` |


`{application_id}:` The unique identifier for the application, assigned by the system when you create a new application in the console. You can view this ID in the console.

<span id="7e0954ce"></span>
## API rate limiting

Limit per tenant: 20 QPS.

Calls that exceed the API rate limit return a 429 status code.

<span id="54c00e21"></span>
## Authentication method

You can use an API Key or Access Key for authentication. For details, refer to the [API authentication guide](https://www.volcengine.com/docs/85296/1544950).

<span id="4b40e480"></span>
## Request parameters

<span id="2f4e41dd"></span>
### Path parameters


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`application_id` |String |<span data-api-tag="require\|ar4Wdbcwj">必选</span> |76414365027 |Your application's unique identifier. |


<span id="6eecdc1e"></span>
### Body parameters


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`dataset_id` |String |<span data-api-tag="require\|aTBuM4BiC">必选</span> |"14365027" |The unique ID of the dataset. You can find this ID on the Datasets page of the platform. Each request must explicitly specify the dataset to browse. |
|`page_number` |Integer |<span data-api-tag="require\|a8hoCsZ3a">必选</span> |`1` |The page number used to retrieve data for a specific page. The value starts from `1`. |
|`page_size` |Integer |<span data-api-tag="require\|aqszNw1Zq">必选</span> |`20` |The number of Items to return per page. The default value is `10`, and the maximum value is `1000`. |
|`filter` |[Filter structure](https://docs.byteplus.com/docs/viking-aisearch/browseindex#7e072dc5) |Optional |See request example |The search filter object. You can use fields configured as "Filterable" in the data source to filter results. For the detailed structure and usage of the `Filter` object, refer to the relevant documentation. |
|`sort_by` |String |Optional |`metrics.score` |The field name for sorting. **The field must exist in the dataset and be checked as "Filterable" in the application**. It supports the following types:<br><br><br>* **Basic types**: `int32`, `int64`, `float`, `bool`, `string`<br><br>* **Complex types**: For the `Sorting` of sub\-level fields of a `Field` of the `object` `type`, use `.` The connector references its internal Fields in the format `object.field`, for example, `product.price`. |
|`sort_order` |String |Optional |`desc` |Sort order. Supports the following enum values:<br><br><br>* `desc`: Descending order (default value)<br><br>* `asc`: Ascending order |
|`output_fields` |Array<String\> |Optional |`["item_id", "title", "image_url"]` |Specifies which fields to return in the response's `display_fields`. If this parameter is empty or omitted, all fields in the data source are returned by default.<br><br>**Note**: For nested objects (such as `object` or `array<object>`), only top\-level field names are currently supported. Non\-existent fields or fields within nested objects are ignored. |
|`facet` |[Facet](https://docs.byteplus.com/docs/viking-aisearch/browseindex#be80f5ee) |Optional |See the data structure below \- [Facet](https://docs.byteplus.com/docs/viking-aisearch/browseindex#be80f5ee) |Used to specify the field for results grouping and filtering.<br><br><br>* The default value is empty. |


<span id="7e072dc5"></span>
### Filter structure


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|`op` |string |Yes |"must" |Operator type. Supports:<br><br>"must"、"must_not"、"range"、"and"、"or"<br><br>For details on how to use operators, see the Filter operator description below. |
|`field` |string |Conditionally required |"status" |The field to which the filter conditions apply.<br><br><br>* Required for "must", "must_not", and "range" operators.<br><br>* This parameter is ignored for "and" and "or" operators. |
|`gte` |Float |No |100.0 |The filter range of the "range" operator, which filters data where the "field" Field value is `greater than or equal to` the specified Value. |
|`gt` |Float |No |100.0 |The filter range of the "range" operator, which filters data where the "field" Field value is `greater than` the specified Value. |
|`lte` |Float |No |500.0 |The filtering scope for the "range" operator. Semantically, it filters data where the "field" field value is `less than or equal to` a specified value. |
|`lt` |Float |No |500.0 |The filtering scope for the "range" operator. Semantically, it filters data where the "field" field value is `less than` a specified value. |
|`conds` |array |Conditionally required |See the example below |Except for the "range" operator, all other operators must specify the conds condition.<br><br><br>* The "must" and "must_not" operators require specifying a set of filter values.<br><br>* The "and" and "or" operators require specifying nested filter conditions. |


<span id="9319f9c1"></span>
#### Filter operators


|**Operator** |**Filtered field type** |**Description** |**Example** |
|---|---|---|---|
|`must` |* int32<br><br>* int64<br><br>* string<br><br>* Bool<br><br>* array(int32)<br><br>* array(int64)<br><br>* array(string) |Conditional expression parameter syntax:<br><br><br>* `op`: Pass "must"<br><br>* `field`: Pass in the target filter Field<br><br>* `conds`: Pass in a list of filter values. The list elements must have the same type as the field.<br><br><br>When `field` is a single integer or String element, the meaning is  **"in"** , i.e., "the Field value is in the provided filter list".<br><br>When `field` is a list of integers or Strings, the meaning is  **"has intersection"** , i.e., "the target Field and the filter list have overlapping elements". |**Example One:**  The region must be one of "cn" OR "sg".<br><br>```JSON```<br>```{```<br>```    "op": "must",```<br>```    "field": "region",```<br>```    "conds": ["cn", "sg"]```<br>```}```<br><br><br>**Example Two:**  The status Value must be one of 1, 2, or 3.<br><br>```JSON```<br>```{```<br>```    "op": "must",```<br>```    "field": "status",```<br>```    "conds": [1, 2, 3]```<br>```}```<br><br><br> |
|`must_not` |* int32<br><br>* int64<br><br>* string<br><br>* Bool<br><br>* array(int32)<br><br>* array(int64)<br><br>* array(string) |Conditional expression parameter syntax:<br><br><br>* `op`: Pass in "must_not"<br><br>* `field`: Pass in the target filter Field<br><br>* `conds`: Pass in a list of filter values. The list elements must have the same type as the field.<br><br><br>When `field` is a single integer or string element, it means  **"not in"** , i.e., the target field value is not in the filter list.<br><br>When `field` is a list of integers or strings, it means  **"no intersection"** , i.e., the target field and the elements in the filter list do not overlap. |The status value must not be 1, 2, or 3<br><br>```JSON```<br>```{```<br>```    "op": "must_not",```<br>```    "field": "status",```<br>```    "conds": [1, 2, 3]```<br>```}```<br><br><br> |
|`range` |* int32<br><br>* int64<br><br>* Float |Conditional expression parameter syntax:<br><br><br>* `op`: Enter "range"<br><br>* `field`: Pass in the target filter Field<br><br>* `gt`: Greater than<br><br>* `gte`: Greater than or equal to (valid for integers)<br><br>* `lt`: less than<br><br>* `lte`: less than or equal to (valid for integers)<br><br><br>This means the target numerical Field value is required to be within the specified range.<br><br>Configure using `gte` (greater than or equal to), `gt` (greater than), `lte` (less than or equal to), `lt` (less than), to select the Value range. |**price \>= 100.0**<br><br>```JSON```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0```<br>```}```<br><br><br>**price is between 100.0 and 500.0**<br><br>```JSON```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0,```<br>```  "lt": 500.0```<br>```}```<br> |
|`time_range`<br><br> |The filtered Field is required to be an uploaded Field marked with the "Release time" attribute, supporting the following:<br><br><br>* int64: UNIX Timestamp<br><br>* string: ISO8601 time format; or "YYYY\-Mm\-DD hh:mm:ss.sss" format<br><br><br>For details, see [Review Reserved Field Attributes](https://docs.byteplus.com/docs/viking-aisearch/Introduction_Image_Text_Dataset#bb64f3ff) |Conditional expression parameter syntax:<br><br><br>* `op`: Pass in "time_range"<br><br>* `field`: Pass in the target filter Field<br><br>* `gt`: Later than<br><br>* `lt`: Earlier than<br><br><br>The target filter Field must be a time\-based Field. Supported values for `gt` and `lt`:<br><br><br>* Absolute time condition (fixed time period): Use a UNIX **millisecond\-precision** Timestamp (int).<br><br>* Relative time condition (a relative time period relative to the request time): Use the expression "now[+/\-][Value][d/h/m/s]", passed as a String. Relative time expression examples:<br><br>   * `now+2d`: 2 days after the current time<br><br>   * `now-24h`: 24 hours before the current time<br><br><br> |**Release time after 2026**<br><br>```JSON```<br>```{```<br>```  "op": "time_range",```<br>```  "field": "publish_time",```<br>```  "gt": 1767196800000,```<br>```}```<br><br><br>**Release time within the last month**<br><br>```JSON```<br>```{```<br>```  "op": "time_range",```<br>```  "field": "publish_time",```<br>```  "gt": "now-30d",```<br>```}```<br> |
|geo_distance |this field in your items datasets must be an **object** type and `includes` two subfields named `latitude` and `longitude`. list of object is not supported. |Conditional expression parameter syntax:<br><br><br>* `op`: pass in "geo_distance"<br><br>* `field`: field name to apply geographic filtering. the type of this field must be an object `including` `latitude` and `longitude` subfields.<br><br>* `center`: the reference point for distance calculation, formatted as a `"{longitude},{latitude}"` string. If this parameter is not provided, the value of `context.location` in the Search interface request is used as the reference point by default.<br><br>* `radius`: distance range, a string in the format of `"{Number}{Unit}"`. For example: `"5km"`, `"10000m"`. |**Example one: use the user's current location as the reference point**<br><br>This example filters all Items whose `store_location` field is within 5 kilometers of the user's current location (passed via `context.location`).<br><br>```JSON```<br>``````<br><br><br>**Example two: use specified latitude and longitude as the reference point**<br><br>This example filters all Items whose `store_location` field is within 10,000 meters of the specific latitude and longitude coordinates (`121.4737,31.2304`).<br><br>```JSON```<br>``````<br> |
|`and` |Not applicable |A logical operator that returns the intersection of multiple conditions for logical queries. |&nbsp;<br><br>```JSON```<br>```{```<br>```  "op": "and",```<br>```  "conds": [     // A list of conditions, supporting nested and/or/must/must_not/range operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "status",```<br>```      "conds": [1, 2, 3]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining any number of conditions (>=1).```<br>```    }```<br>```  ]```<br>```}```<br> |
|`or` |Not applicable |A logical operator that returns the union of multiple conditions for logical queries. |&nbsp;<br><br>```JSON```<br>```{```<br>```  "op": "or",```<br>```  "conds": [ // A list of conditions, supporting nested and/or/must/must_not/range operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "status",```<br>```      "conds": [1, 2, 3]```<br>```    },```<br>```    {```<br>```        ...      // Supports combining any number of conditions (>=1).```<br>```    }```<br>```  ]```<br>```}```<br> |


<span id="be80f5ee"></span>
### Facet


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`facets` |Array <facets\> |Optional<br><br> |```Plain Text```<br>```"facets": [```<br>``` {  ```<br>``` "field": "tags",        ```<br>``` "max_facet_buckets": 10     ```<br>``` },```<br>``` {```<br>``` "field": "price",      ```<br>``` "number_ranges": [```<br>``` { "gte": 0, "lt": 19},{ "gte": 10, "lt": 100},{"gte": 200, "lt": 999}```<br>``` // Configurable value range```<br>``` ]```<br>``` }```<br>``` ]```<br> |Specify the facet fields, value ranges, and the maximum number of Enum values to return for aggregation of search results.<br><br>If not passed in, the fields already configured in Console \- Experience center \- **Facet** will be used by default<br><br>Parameter Details can be viewed at: [facets](https://docs.byteplus.com/docs/viking-aisearch/browseindex#1891cb01)<br><br> |
|`facet_filter`<br><br> |facet_filter<br><br> |Optional<br><br> |&nbsp;<br><br>```Plain Text```<br>```"facet_filter":{```<br>```{```<br>```    "op": "must",```<br>```    "field": "region",```<br>```    "conds": ["cn", "sg"]```<br>```},```<br>```{```<br>```    "op": "must_not",```<br>```    "field": "status",```<br>```    "conds": [1, 2, 3]```<br>```}```<br>```}```<br> |This parameter specifies the facet filter for the current search request.<br><br>If not passed in, no facet filter will be applied, the initial search results will be returned.<br><br>Same as [Filter](https://docs.byteplus.com/docs/viking-aisearch/Search#aead416b)<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/595f3eaf3e19437d95b484d1af5ab716) </span><br><br> |


<span id="1891cb01"></span>
#### facets


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`field` |String |<span data-api-tag="require\|ayIPtcXVN">必选</span> |"brand" |Field name used for aggregate statistics |
|`number_ranges` |Array<NumberRange\><br><br>`NumberRange` is of OBJECT type |Optional<br><br>Defaults to empty |"{ "gte": 0, "lt": 19}" |If a field of numeric type (int, float, Array<int\>, Array<float\>) is designated as the category statistics field, it is suggested to preset the value range to aggregate statistics on the results based on the value range.<br><br>Currently, **4** operators for defining value ranges are supported:<br><br><br>* gte: semantics filter data where the \"field\" field value is `greater than or equal to` the specified value.<br><br>* gt: semantics filter data where the \"field\" field value is `greater than` the specified value.<br><br>* lte: semantics filter data where the \"field\" field value is `less than or equal to` the specified value.<br><br>* lt: semantics filter data where the \"field\" field value is `less than` the specified value.<br><br><br>If not passed in, facet would be performed by default based on the original field values. |
|`max_facet_buckets` |Int |Optional<br><br>the default value is 10 |10<br><br> |Used to set how many enums each field would be returned at most, the default is 10, and the upper limit is 50.<br><br>If not passed, it will be processed according to the default value 10. |


&nbsp;

&nbsp;

<span id="40d81141"></span>
## Response structure

The response body is a JSON object that includes the unique ID of the request and the result data.


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`request_id` |String |The unique identifier for this request. Use this ID to quickly locate request logs for troubleshooting. |
|`result` |Object |The result object returned when the request is successful. See below for the detailed structure. |


<span id="81122c6c"></span>
### Result object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|result |Object |Object that includes content |
|* total_items |Integer |The total number of items that meet the current filter conditions. |
|* items |Array<Object\> |The list of items returned for this page. This is an array of objects, and each object represents an item. |


<span id="b8c13e4c"></span>
### Item object

Each object in the `items` array represents a single Item. Its structure is as follows:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`_id` |String |The primary key of the item in data storage, usually originating from the field value marked as "Unique identifier" when you upload data. |
|`display_fields` |Object |A collection of key\-value pairs containing other fields of the item. The request parameter `output_fields` controls which fields are returned. If `output_fields` is not specified, all fields are returned. |


<span id="2c1ffa33"></span>
## Example

<span id="f0f3a2f4"></span>
### Sample request

Return 200 items per page

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/browse_index' \
--header 'Authorization: Bearer your_api_key' \
--header 'Content-Type: application/json' \
--data-raw '{
    "dataset_id": "your-dataset-id",
    "page_number": 1,
    "page_size": 200,
    "filter": {
        "op":"and",
        "conds":
        [
            {
                "field": "tag",
                "op": "must",
                "conds": ["Outdoor"]
            },
            {
                "field": "quality_score",
                "gte":80
            }
        ]
    },
    "sort_by": "upload_timestamp",
    "sort_order": "desc",
    "output_fields": [
        "asset_id",
        "photographer",
        "thumbnail_url"
    ]
}'
```


<span id="abbe1c34"></span>
### Sample response

```JSON
{
    "request_id": "req-a1b2c3d4-e5f6-7890-1234-567890abcdef",
    "result": {
        "result": {
            "total_items": 1532,
            "items": [
                {
                    "_id": "doc001",
                    "display_fields": {
                        "asset_id": "asset-001",
                        "photographer": "James",
                        "thumbnail_url": "https://example.com/thumbnails/asset-001.jpg"
                    }
                },
                {
                    "_id": "doc002",
                    "display_fields": {
                        "asset_id": "asset-002",
                        "photographer": "Monica",
                        "thumbnail_url": "https://example.com/thumbnails/asset-002.jpg"
                    }
                }
                // ... more items
            ]
        }
    }
}
```


<span id="f260c8d3"></span>
## Error codes


|**HTTP status code** |**Error code** |**Error message** |**Meaning** |
|---|---|---|---|
|400 |`MissingParameter` |The request is missing the following parameter: {parameters} |Missing parameter error, such as when a required parameter is not provided. |
|400 |`InvalidParameter` |A parameter in the request is not valid: {parameters} |The parameter is invalid, for example, the parameter type is incorrect, the length is invalid, the enum value is invalid, or the value does not satisfy the regex rule. |
|400 |`InvalidRequestFormat` |The request cannot be parsed in JSON format. |Failed to parse the request body. This typically occurs when the request body has an invalid format, is not a legal JSON format, or does not match the defined request structure. Refer to the corresponding API documentation to check the request structure. |
|400 |`InvalidAction` |The specified action is invalid: {Action} |When the Action in the request path does not exist or is temporarily unavailable for request:<br><br><br>* `browse_index`: Unable to browse the dataset index. This may be because the index has not taken effect after the dataset was linked, or the dataset corresponding to the `dataset_id` is not linked in the application. |


For other common error codes, see the [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)documentation.


---



To experience more Viking AI Search capabilities, go to: [Viking AI Search, the integrated intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)
