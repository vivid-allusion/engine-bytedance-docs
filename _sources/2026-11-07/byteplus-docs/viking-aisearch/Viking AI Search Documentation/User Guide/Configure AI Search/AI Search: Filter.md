---
title: "AI Search: Filter"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/AI_search_filter"
---

<span id="8a270e9f"></span>
# Feature Overview

Viking AI Search supports **pre\-filtering** of candidate data during a search call. This allows you to restrict the search scope to a specific subset of items, ensuring that the results retrieved are relevant both to the user's query and your business constraints.

The filtering logic is controlled via the **Search API** and is executed during the **Recall Phase**. By performing pre\-filtering at the point of retrieval, the system identifies matches only from items that satisfy the filter criteria. This prevents "zero\-result" scenarios (empty search results) that often occur when filtering is applied *after* the initial recall.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">See full API documentation: <a href="https://www.volcengine.com/docs/85296/1544974">API Reference \> Search</a></div>


<span id="79213890"></span>
# Implementation Guide

To perform a filtered search, use the `filter` parameter to pass your filtering syntax when calling the Search API, as shown in the example below:

```HTTP
curl -X POST 'https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/search/{scene_id}' \ 
 -H 'Content-Type: application/json' \ 
 -H 'Authorization: Bearer <API_KEY>' \ 
 -d '{ 
 "query": { 
 "text": "query text string", 
 "image_url": "https://example.com/image.jpg" 
 }, 
 "page_number": "search page number", 
 "page_size": "number of search results per page", 
 "user": { 
 "user_id": "user ID" 
 }, 
 "filter": "search filter conditions", 
 "dataset_id": "target dataset id" 
 }'
```


<span id="f298c6c7"></span>
## Filter parameter description

The `filter` parameter is a JSON object that contains one or more filtering conditions. Each condition consists of a field name, an operator, and a value to specify the filtering rules to be met.

**Basic structure:** 

```JSON
{
    ...
    "filter": {
        "op": "Operator Type",
        "field": "Field Name",
        "conds": ["Value List"]
    }
    ...
}
```



|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`op` |String |<span data-api-tag="require\|ajWjofLsu">必选</span> |Operator type: `must` / `must_not` / `range` / `and` / `or`/`time_range`/`geo_distance` |
|`field` |String |Conditionally required |Name of the field to filter <br><br>**Required** **when the operator type is ** `must`, `must_not`, or `range`,<br><br>**Not required when operator type is ** `and`, `or` |
|`conds` |Array |Conditionally required |Condition value array <br><br>*This parameter is not used by the * `*range*` * operator.*  |
|`gte` |Float |No |Greater than or equal to (used only by the `range` operator as a condition) |
|`gt` |Float |No |Greater than (used only by the `range` operator as a condition) |
|`lte` |Float |No |Less than or equal to (used only by the `range` operator as a condition) |
|`lt` |Float |No |Less than (used only by the `range` operator as a condition) |


&nbsp;

<span id="72aa92f8"></span>
## Filter operators

<span id="405e8858"></span>
### Quick reference

**<ins>Operators</ins>**


|**Operator** |**Definition** |**Requires field** |**Requires ** **conds** |**Supported Data Types** |
|---|---|---|---|---|
|`must` |In list/include |✓ |✓ |Integer, String, Boolean, Array<String\>, Array<Int\>. |
|`must_not` |Not in list/do not include |✓ |✓ |Integer, String, Boolean, Array<String\>, Array<Int\>. |
|`range` |Numeric range |✓ |✗ |Integer, Float |
|`time_range` |Time range |✓ |✗ |Integer, String fields that have been previously configured with the time attributes |
|`geo_distance` |Within a certain distance to a geo\-center |✓ |✓ |An object field with longitude and latitude sub\-fields |
|`and` |Logical and (intersection) |✗ |✓ |Any nested operator |
|`or` |Logical or (union) |✗ |✓ |Any nested operator |


**<ins>Range parameters</ins>**


|**Parameter** |**Mathematical Symbol** |**Definition** |**example** |
|---|---|---|---|
|`gte` |\>= |Greater than or equal to |`"gte": 100` →  \>= 100 |
|`gt` |\> |Greater than/later than |`"gt": 100` →  \> 100<br><br>`"gt": 1767196800000` → after 0:00 on January 1, 2026 (UTC +8) |
|`lte` |<= |Less than or equal to |`"lte": 500` →  <= 500 |
|`lt` |< |Less than / earlier than |`"lt": 500` →  < 500<br><br>`\"lt\": now+7d` → within 7 days from now |



---



<span id="79c3f23b"></span>
### 1. `must` operator (must include/intersection)


<columns>
<columnsItem zoneid="dN7zX3P7Oi">

**Condition expression parameter format:** 


* `op`: Set to "must"

* `field`: The target field to filter

* `conds`: A list of filter values, with elements that match the field's type


&nbsp;

**Meaning:** 

When `field` is a single integer or string element, it means  **"belongs to"** , i.e., "the field's value is in the provided filter list."

When `field` is a list of integers or strings, it means  **"has intersection"** , i.e., "the target field overlaps with elements in the filter list."

&nbsp;

**Supported field types**:


* `Int32` / `Int64` / `String` / `Bool`

* `Array<int32>` / `Array<int64>` / `Array<string>`


&nbsp;

**Use cases**:


* Filtering Products by Specific Status

* Restricting Results to Specific Regions

* Selecting Content from Specific Categories

</columnsItem>
<columnsItem zoneid="hQk1Gmc5yF">

**Example 1: Filter products for sale**

```JSON
{
  "filter": {
    "op": "must",
    "field": "status",
    "conds": [1, 2]
  }
}
```


**Explanation**: Only return products with status values 1 or 2 (e.g., 1 = for sale, 2 = pre\-sale)

**Example 2: Filter specific categories**

```JSON
{
  "filter": {
    "op": "must",
    "field": "category",
    "conds": ["Women's High Heels", "Women's Sneakers", "Women's Sandals"]
  }
}
```


**Explanation**: The search results will only include products whose `category` field matches any of the values provided in the list: **Women's High Heels**, **Women's Sneakers**, or **Women's Sandals**. This effectively narrows the search scope to these specific product types.

</columnsItem>
</columns>


&nbsp;


---



<span id="723149e0"></span>
### 2. `must_not` operator (must exclude)


<columns>
<columnsItem zoneid="NFy5LZbSZJ">

**Conditional expression parameter format:** 


* `op`: Set to "must_not"

* `field`: The target field for filtering

* `conds`: A list of filter values where elements must match the field's type


&nbsp;

**Semantics:** 

When `field` is a single integer or string element, it means  **"not belonging to"** , meaning the item is excluded if its field value is in the provided filter list.

When `field` is a list of integers or strings, it means  **“no intersection”** , that is, the search result is excluded if there is any overlap (shared elements) between the target field array and the filter list.

**Supported field types**:


* `Int32` / `Int64` / `String` / `Bool`

* `Array<int32>` / `Array<int64>` / `Array<string>`


&nbsp;

**Use cases**:


* **Exclude Delisted Products:**  Prevent items that are no longer for sale from appearing in search results.

* **Filter Disabled Accounts:**  In social or community apps, ensure content from banned or deactivated users is hidden.

* **Remove Specific Content Types:**  Allow users to filter out types of content they are not interested in, such as excluding "Short Videos" from a general media search.

</columnsItem>
<columnsItem zoneid="y3kKs0L7TY">

**Example 1: Exclude delisted and sold\-out products**

```JSON
{
  "filter": {
    "op": "must_not",
    "field": "status",
    "conds": [0, 3]
  }
}
```


**Explanation**: This filter ensures that products with a `status` of **0** (removed/delisted) or **3** (sold out) are excluded from the search results. Only products that do not match these specific status codes will be returned to the user.

<span id="d71828dc"></span>
### 

</columnsItem>
</columns>


&nbsp;


---



<span id="d2139bb5"></span>
### 3. `range` operator (range filtering)


<columns>
<columnsItem zoneid="NKFfuwRMzO">

**Condition expression parameter syntax:** 


* `op`: Set to "range"

* `field`: pass in the target field to filter

* `gt`: greater than

* `gte`: greater than or equal to (valid for integers)

* `lt`: less than

* `lte`: less than or equal to (valid for integers)


This means the target numeric field's value must be within the specified range.

**Semantics**: The numeric field's value must be within the specified range

**Supported field types**:


* `Int32` / `Int64` / `Float`


**Range parameters**:


* `gte`: greater than or equal to (\>=)

* `gt`: greater than (\>)

* `lte`: less than or equal to (<=)

* `lt`: less than (<)


**Use cases**:


* Price range filtering

* Rating range filtering

* Time range filter

</columnsItem>
<columnsItem zoneid="lqfCY5RtDx">

**Example 1: Filter products with a price greater than or equal to 100**

```JSON
{
  "filter": {
    "op": "range",
    "field": "price",
    "gte": 100.0
  }
}
```


**Example 2: Filter products with a price between 100 and 500**

```JSON
{
  "filter": {
    "op": "range",
    "field": "price",
    "gte": 100.0,
    "lt": 500.0
  }
}
```


&nbsp;

<span id="432ed7c2"></span>
### 

</columnsItem>
</columns>



---



<span id="ba9a42a1"></span>
### 4. `time_range` operator (Time\-based filtering)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div>


<div data-tips="true" data-tips-type="default">This operator can be used to filter fields with the <strong>"publish time"</strong> attribute and supports the following types:</div>



* <div data-tips="true" data-tips-type="default">int64: UNIX timestamp (seconds or milliseconds)</div>


* <div data-tips="true" data-tips-type="default">string: ISO8601 time format; or "YYYY\-Mm\-DD hh:mm:ss.sss" format</div>



<div data-tips="true" data-tips-type="default">See details at <a href="https://docs.byteplus.com/docs/viking-aisearch/Introduction_Image_Text_Dataset#bb64f3ff">Review Reserved Field Attributes</a></div>



<columns>
<columnsItem zoneid="aEIOMrKKdo">

**Conditional expression parameter syntax:** 


* `op`: Set to "time_range"

* `field`: pass in the target field for filtering

* `gt`: later than

* `lt`: earlier than


**Semantics:**  the time must fall within a specific range. The time range is defined by the gt and lt parameters. `gt` indicates the lower time limit (must be later than this value), and `lt` indicates the upper time limit (must be earlier than this value). Together, they form an open interval.

**`lt`** ** and ** **`gt`** ** parameter values support two formats:** 


* **Absolute time condition (fixed time period):**  UNIX timestamps (integer) in milliseconds.

* **Relative time condition (relative time period based on request time):**  Expressions in the string format "now[+/\-][value][d/h/m/s]". Examples of relative time expressions:

   * `now+2d`: A point in time 2 days from now.

   * `now-24h`: A point in time 24 hours ago.

</columnsItem>
<columnsItem zoneid="aWYYE9Z7Y5">

**Example 1: Filtering based on a fixed point in time**

```JSON
{
  "op": "time_range",
  "field": "publish_time",
  "gt": 1767196800000
}
```


**Meaning:**  Search only for content published after 2026

**Example 2: Filtering based on relative time conditions from the current time**

```JSON
{
  "op": "time_range",
  "field": "publish_time",
  "gt": "now-30d"
}
```


**Meaning:**  Search only for content published within the last 30 days

</columnsItem>
</columns>


&nbsp;


---



<span id="0cc43162"></span>
### 5.`geo_distance` operator


<columns>
<columnsItem zoneid="mHcGM1iTLz">

**Parameter format for condition expressions:** 


* `op`: Pass in "geo_distance".

* `field`: The name of the field to apply geolocation filtering to. The field type must be an object (Object) that contains the `latitude` and `longitude` subfields.

* `center`: The reference point for distance calculation, in the form of a `"{longitude},{latitude}"` string. If this parameter is not provided, the system uses `context.location` in the Search API request as the reference point by default.

* `radius`: The distance range, in the form of a `"{value}{unit}"` string. For example, `"5km"` or `"10000m"`.


**Semantics:** 

Return all content whose distance between the target field coordinates and the specified reference point (`center`) is within the given radius (`radius`).

**Parameter details:** 


* **`field`**

   * **Field type requirements**: In your item dataset, this field must be an **object (Object)**  and must contain two subfields named `latitude` (latitude) and `longitude` (longitude). A list of objects (List of Object) is not supported.


```JSON
// Example of a correct field structure
"store_location":{
"latitude":39.914912,
"longitude":116.412138
}
```



* **`center`** (optional)

   * **Format**: A string composed of longitude and latitude, in the form of `"{longitude},{latitude}"`.

   * **Default behavior**: If the request does not include the `center` parameter, the system automatically uses the user location provided in `context.location` as the reference point. To use this feature, you must pass valid `location` information in the request `context` object.


```JSON
"context":{
    "location":{
        "longitude":"116.404",
        "latitude":"39.915"
    }
}
```



* **`radius`**

   * **Format**: A string composed of a value and a unit, in the form of `"{value}{unit}"`.

   * **Supported units**: `m` (meters) and `km` (kilometers).

   * **Value precision**: The value supports integers and decimals. To ensure calculation accuracy, the decimal portion supports up to **7** digits. If the input exceeds 7 decimal digits, the system automatically truncates it.

</columnsItem>
<columnsItem zoneid="vJRMs9mYgZ">

**Example 1: Use the user’s current location as the reference point**

This example filters all items whose `store_location` field is within 5 km of the user’s current location (passed via `context.location`).

```JSON
{
    "query":{
        "text":"local restaurant"
    },
    "context":{
        "location":{
            "longitude":"116.412138",
            "latitude":"39.914912"
        }
    },
    "filter":{
        "op":"geo_distance",
        "field":"store_location",
        "radius":"5km"
    }
}
```


&nbsp;

**Example 2: Use the specified latitude and longitude as the reference point**

This example filters all items whose `store_location` field is within 10000 m of the specified latitude and longitude coordinates (`121.4737,31.2304`).

```JSON
{
    "query":{
        "text":"hotels near this location"
    },
    "filter":{
        "op":"geo_distance",
        "field":"store_location",
        "center":"121.4737,31.2304",
        "radius":"10000m"
    }
}
```




</columnsItem>
</columns>


<span id="3e1bf9cf"></span>
### 6. `and` operator (logical AND)


<columns>
<columnsItem zoneid="OD4NIB4Q9y">

**Semantics**: all subconditions must be met simultaneously (intersection)

**Features**:


* No `field` parameter required

* Multiple filter conditions nested through the `conds` array

* Supports nesting any operators (`must`/`must_not`/`range`/`and`/`or`)


**Use cases**:


* Meeting multiple conditions simultaneously

* Composite filter logic

</columnsItem>
<columnsItem zoneid="Df8aJtBbEt">

**Example 1: Filter by status and price together**

```JSON
{
  "filter": {
    "op": "and",
    "conds": [
      {
        "op": "must",
        "field": "status",
        "conds": [1, 2]
      },
      {
        "op": "range",
        "field": "price",
        "gte": 100.0,
        "lte": 500.0
      }
    ]
  }
}
```


**Explanation**: Returns items that are on sale (status is 1 or 2) and priced between 100 and 500.

**Example 2: Combination of three conditions**

```JSON
{
  "filter": {
    "op": "and",
    "conds": [
      {
        "op": "must",
        "field": "category",
        "conds": ["Women's High Heels"]
      },
      {
        "op": "must_not",
        "field": "brand",
        "conds": ["BrandX"]
      },
      {
        "op": "range",
        "field": "price",
        "lt": 1000.0
      }
    ]
  }
}
```


**Explanation**: Returns items classified as women's high heels, with a brand other than BrandX, and priced under 1000.

</columnsItem>
</columns>


&nbsp;


---



<span id="74d03245"></span>
### 7. `or` operator (logical OR)


<columns>
<columnsItem zoneid="LsZpMDG2az">

**Semantics**: any subcondition met (union)

**Features**:


* No `field` parameter required

* Use multiple filter conditions nested in the `conds` array

* Supports nested arbitrary operators


**Use cases**:


* Meeting any one condition

* Multiple optional filtering paths

</columnsItem>
<columnsItem zoneid="C2DlQkcNBh">

Example 1: filter popular regions or VIP users

```JSON
{
  "filter": {
    "op": "or",
    "conds": [
      {
        "op": "must",
        "field": "region",
        "conds": ["cn", "us"]
      },
      {
        "op": "must",
        "field": "is_vip",
        "conds": [true]
      }
    ]
  }
}
```


**Explanation**: Returns data where the region is China or the US **OR** the user is VIP

</columnsItem>
</columns>


&nbsp;

<span id="cd314f5a"></span>
## Sample API requests

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">See full API documentation: <a href="https://www.volcengine.com/docs/85296/1544974">API Reference \> Search</a></div>


<span id="7a8940ee"></span>
### Example 1: Single\-condition filter

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{your_app_id}/search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API_KEY>' \
  -d '{
    "query": {
        "text": "Women Shoes Spring/Summer"
    },
    "dataset_id": "106265704",
    "page_number": 1,
    "page_size": 20,
    "filter": {
        "op": "must",
        "field": "status",
        "conds": [1, 2]
    }
}'
```


<span id="3f3e7762"></span>
### Placeholder replacement instructions:


1.  **{your_app_id}** : Replace with the actual `app_id` of the target AI Search application. You can find it on the application details page in the Volcengine AI Search console.

2.  **<API_KEY\>:**  Replace with your API Key. You can create and view API Keys in the AI Search service section of the Cloud Search Service console.

* Create an API Key: https://www.volcengine.com/docs/6465/1359479

*  View an API Key: https://www.volcengine.com/docs/6465/1359481


<span id="6UuIzNaD"></span>
### Example 2: Nested filters

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{configuration_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API_KEY>' \
  -d '{
    "query": {
        "text": "Sneakers"
    },
    "dataset_id": "<your_dataset_id>",
    "page_number": 1,
    "page_size": 20,
    "filter": {
        "op": "and",
        "conds": [
            {
                "op": "must",
                "field": "category",
                "conds": ["Women Sneakers", "Men Sneakers""]
            },
            {
                "op": "range",
                "field": "price",
                "gte": 200.0,
                "lte": 1000.0
            },
            {
                "op": "must_not",
                "field": "status",
                "conds": [0, 3]
            },
            {
                "op":"time_range",
                "field":"online_date",
                "gt":"now-90d"
            }
        ]
    }
}'
```
