---
title: "AI Search: Boost and Bury via API (V2)"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/boost_bury_api_v2"
---

***Viking AI Search*** * is an enterprise\-level AI search product based on generative AI. Leveraging large models' multimodal semantic representation and understanding capabilities, combined with years of best practices in ByteDance's information retrieval domain, it provides customers with an out\-of\-the\-box AI search platform service to help them easily build and integrate end\-to\-end multimodal image and text search and recommendation capabilities.* 

*To experience more Viking AI Search capabilities, go to: * [Viking AI Search BytePlus Official Website](https://www.byteplus.com/en/product/viking-ai-search?previewMode=on)


---



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Version Notice</div>


<div data-tips="true" data-tips-type="warning">To improve extensibility and flexibility, this API released the <strong>V2 format on April 18, 2026</strong>. New integrators are strongly encouraged to adopt the V2 format directly. </div>


<div data-tips="true" data-tips-type="warning">The legacy format remains supported long\-term, and mixed use of legacy and V2 formats within a single request is allowed. Existing integrators can migrate at their own pace.</div>


<span id="677d6172"></span>
# Overview

This API lets you configure boost and bury rules dynamically. Within a single request, you specify the **field, operator, condition values, and weight strength (range: −1 to 1)**  to adjust the ranking weights of search results in real time. Compared with the previous approach of adjusting weights manually in the console, this significantly improves operational efficiency and flexibility.

<span id="1bcd09e2"></span>
## Key benefits


* **Lower maintenance cost**: reduces manual effort and avoids omissions when adjusting weights.

* **Integration with your business systems**: connect boost/bury logic with your own systems (inventory, marketing, risk control, etc.) to drive dynamic adjustments.

* **Fine\-grained personalization**: supports per\-user weight configuration for stronger personalized search.


<span id="69254124"></span>
## Typical scenarios


* **E\-commerce**: after a user views a product page, the next set of search results can boost items of the same brand via the API, surfacing them to the user first.

* **Content platforms**: when a user follows a new author, the next search results can boost articles by that author to match their short\-term reading interest.

* **Marketing campaigns**: during a promotion, you can boost promotional items via the API to increase their exposure.



---



<span id="b660a919"></span>
# API Configuration

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Pre\-requisites</div>


<div data-tips="true" data-tips-type="default">This assumes you have already integrated the Viking AI Search search API. See <a href="https://docs.byteplus.com/docs/viking-aisearch/Search">Search</a>.</div>


&nbsp;

Add the top\-level field `boost_bury_rules` to the search request body. The platform automatically merges the boost/bury rules configured in the console with those provided through the API.

<span id="9ef89377"></span>
## Request Parameters


|**Parameter** |**Type** |**Required** |**Sample** |
|---|---|---|---|
|boost_bury_rules |Array <**Conds**\> |**`Required`** |See below: **Config** |


<span id="ca81d523"></span>
### Config

A single `conds` can contain multiple `BoostConfig` objects. To create nested rules, combine multiple `BoostConfig` objects.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Automatic Loss Mitigation</div>


<div data-tips="true" data-tips-type="default">If an individual boosting or demotion rule is found to be invalid (e.g., incorrect syntax, unsupported field, or out\-of\-range values), the service will <strong>automatically ignore only that specific rule</strong>. This ensures that all other valid rules continue to function normally without interrupting the search service.</div>



|**Parameter** |**Data format** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|conds |Array <**BoostConfig**\> |**`Required`** |See below: **BootConfig** |Condition configuration for boosting/burying. Applies only to items that match the conditions |
|boost |Float |**`Required`** |0.3, \-0.3 |Boost/bury strength. Range `−1 to 1` |


<span id="38cf87d9"></span>
#### BoostConfig


|**Parameter** |**Data type** |**Required** |**Sample** |**Description** |
|---|---|---|---|---|
|field |String |**`Required`** |"author" |Condition field. Use `.` to access nested fields, e.g., `category.name`. |
|op |String |**`Required`** |"must" |Operator. <br><br>For logical operators (`and`/`or`), place the sub\-conditions in the `conds` array. <br><br>Supported operators vary by field type. |
|conds |Based on the field |**`Required`** | |Set of condition values, or an array of `and`/`or` sub\-expressions. |
|gt/gte/lt/lte |String / Int |**`Conditionally`** | |Range boundary values. When using a **range** operator, at least one must be provided. |


&nbsp;


---



<span id="6fe89772"></span>
## Return Parameters

The system returns the re\-ranked search results and reports the execution status of the dynamic boost/bury rules in the `extra_info` field.

<span id="3bc10544"></span>
### ExtraInfo


|**Parameter** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|boost_status |Array<string\> |`["success", "field not found", "invalid operator"]` |**Execution status of boost and demotion rules**<br><br>Status meanings are shown below: **Status**<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Explanation</div><br><br><br><div data-tips="true" data-tips-type="default">Order <strong>strictly follows </strong><strong>Conds</strong><strong> the order within </strong><strong>BoostConfig</strong> <strong>the parameters</strong>;</div><br><br><br><div data-tips="true" data-tips-type="default">For example: the first BoostConfig configuration executed successfully, the first status within <code>boost_status</code> will be <code>"success"</code></div><br> |


<span id="49cb8580"></span>
#### Status


|**Status value** |**Result** |**Definition** |
|---|---|---|
|success |✅  Success |**Rules configuration meets expectations**<br><br>The boost/bury rule took effect on the current request. |
|field not found |❌ Failed |**Field (** **`field`** **) validation failed.** <br><br>Make sure the configured field exists in the item dataset. |
|invalid field type |❌ Failed |**Field (** **`field`** **) data format does not support boost or burying.** <br><br>Currently, Array<Float\>, Array<Object\>, and Boolean fields do not support boost/bury rules. Make sure the field type is supported. |
|invalid date field |❌ Failed |**The field (** **`field`** **) is not a time attribute.**  <br><br>The condition values (`conds`) use the time\-attribute format, but the field (`field`) is not configured as "timestamp" or "publish time". |
|invalid operator |❌ Failed |**The field (** **`field`** **) is valid, but the configured operator (** **`op`** **) is not.**  <br><br>Make sure the operator is configured correctly. |
|invalid conds |❌ Failed |**The field (** **`field`** **) and operator (** **`op`** **) are valid, but the condition values (** **`conds`** **) are not.**  <br><br>Possible causes: <br><br><br>1. Incorrect data format<br><br>2. The field is configured with the "timestamp" or "publish time" attribute.<br><br><br>Make sure the condition values are configured correctly. |
|invalid boost |❌ Failed |**The boost/bury strength is invalid.**  Make sure the value is a number in the range −1 to 1. |



---



<span id="57df8b6f"></span>
## **Field—Operator—** Condition Value **Configuration**


|**Field type (field)**  |**Supported Operators (op)**  |**Conditions (conds)**  |**Example configuration** |
|---|---|---|---|
|Int32<br><br>Int64 |* equal: Equal to<br><br>* not_equal: Not equal to |Int32<br><br>Int64<br><br><div style="text-align: center"><br></div><br> |&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "in_stock", ```<br>```      "op": "equal", ```<br>```      "conds": 1```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br> |
||* lt: Smaller than<br><br>* gt: Greater than<br><br>* lte: Smaller than or equal<br><br>* gte: Greater than or equal ||&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "sales_count", ```<br>```      "op": "gte", ```<br>```      "conds": 1000```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br><br><br> |
||* range: Open or closed interval, must be used in conjunction with gt/gte/lt/lte  ||&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "sales_count", ```<br>```      "op": "range", ```<br>```      "gte": 0,```<br>```      "lt": 10```<br>```     },```<br>```  "boost": 0.5```<br>```}```<br><br><br> |
|Float |* lt: Smaller than<br><br>* gt: Greater than |Float、Int |&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "price", ```<br>```      "op": "gt", ```<br>```      "conds": 1000.20```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br> |
||* range：Open interval, must be used in conjunction with gt/lt ||&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "price", ```<br>```      "op": "range", ```<br>```      "gt": 1000.20，```<br>```      "lt": 10000.50，```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br> |
|String |* must: contains<br><br>* must_not: does not contain |Array<String\> |&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "item_type", ```<br>```      "op": "must", ```<br>```      "conds": ["sneakers","tennis shoes"]```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br> |
||* equal: Equal to<br><br>* not_equal: Not equal to |String |&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "item_type", ```<br>```      "op": "equal", ```<br>```      "conds": "sneakers"```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br> |
|Array(String)<br><br>Array(Int) |* must: contains<br><br>* must_not: does not contain |Array<String\> or Array<Int\> |&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "item_type", ```<br>```      "op": "must", ```<br>```      "conds": ["sneakers","tennis shoes"]```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br> |
|Array(Object) |* must：all elements contain<br><br>* must_not: all elements do not contain<br><br>* any_must: at least one element contains<br><br>* any_must_not: at least one element does not contain |Array<String\> or Array<Int\> |&nbsp;<br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "item.type", ```<br>```      "op": "must", ```<br>```      "conds": ["sneakers","tennis shoes"]```<br>```      },```<br>```  "boost": 0.5```<br>```}```<br> |
|Timestamp<br><br>Release Time |* time_range：dynamic time<br><br>   * `now() +/- d/h/m` units<br><br>   * Must be used in conjunction with gt/gte/lt/lte  |Relative time expression |1. **Earlier than a given time:** <br><br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "publish_time", ```<br>```      "op": "time_range", ```<br>```      "lte": "now()-7d"```<br>```      },```<br>```  "boost": 0.8```<br>```}```<br><br><br><br>&nbsp;<br><br>2. **Later than a given time:** <br><br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "publish_time", ```<br>```      "op": "time_range", ```<br>```      "gte": "now()-1m"```<br>```      },```<br>```  "boost": 0.8```<br>```}```<br><br><br><br>&nbsp;<br><br>3. **Within a time interval:** <br><br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "publish_time", ```<br>```      "op": "time_range", ```<br>```      "gte": "now()-1h",```<br>```      "lte": "now()+1h"```<br>```      },```<br>```  "boost": 0.8```<br>```}```<br> |
||* time_range：Static time<br><br>   * UNIX timestamp |UNIX timestamp  |1. **Earlier than a given time:** <br><br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "publish_time", ```<br>```      "op": "time_range", ```<br>```      "lte": 1781107279```<br>```      },```<br>```  "boost": 0.8```<br>```}```<br><br><br><br>&nbsp;<br><br>2. **Later than a given time:** <br><br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "publish_time", ```<br>```      "op": "time_range", ```<br>```      "gte": 1781107279```<br>```      },```<br>```  "boost": 0.8```<br>```}```<br><br><br><br>&nbsp;<br><br>3. **Within a time interval:** <br><br><br>```JSON```<br>```{```<br>```  "config": {```<br>```      "field": "publish_time", ```<br>```      "op": "time_range", ```<br>```      "gte": 1781106000,```<br>```      "lte": 1781107200```<br>```      },```<br>```  "boost": 0.8```<br>```}```<br> |
|Array(Float)<br><br>Boolean |Not supported |— |— |


<span id="aca0e02a"></span>
## Logical nesting

Use the logical operators `and` and `or` in `op` to combine multiple conditions. 

Place the sub\-conditions in the `conds` array. With `and`, an item must satisfy all sub\-conditions; with `or`, it only needs to satisfy one. See **Example 4 — Nested rules** below.


---



<span id="d9dbe1d9"></span>
# Example


<Tabs>
<Tab zoneid="wmRpv5KiSc" title="Example 1: E-commerce">
<TabTitle>Example 1: E-commerce</TabTitle>

**Goal:**  Boost relevant brands and merchants; bury out\-of\-stock items.

&nbsp;

```JSON
{
  "boost_bury_rules": [
    {
      "config": {
          "field": "brand", 
          "op": "must", 
          "conds": ["apple", "samsung", "huawei"]
      },
      "boost": 0.8
    },
    {
      "config": {
          "field": "available_qty", 
          "op": "lte", 
          "conds": 0
      },
      "boost": -0.8
    }
  ]
}
```



</Tab>
<Tab zoneid="T2VGYwK5lE" title="Example 2: Content Platform">
<TabTitle>Example 2: Content Platform</TabTitle>

**Goal:**  When a user follows a new author or searches for a topic, boost articles by that author and content on that topic.

&nbsp;

```JSON
{
  "boost_bury_rules": [
    {
      "config": {
          "field": "author", 
          "op": "must", 
          "conds": ["author_1","author_2"]
      },
      "boost": 0.3
    },
    {
      "config": {
         "field": "tags",
         "op":"must",
         "conds":["topic_1"]
      },
      "boost": 0.8
    }
  ]
}
```



</Tab>
<Tab zoneid="vbC2S6169r" title="Example 3: Time-based boost/bury">
<TabTitle>Example 3: Time-based boost/bury</TabTitle>

**Goal:**  Boost items published within the last 7 days; bury items published before a specific point in time.

&nbsp;

```JSON
{
  "boost_bury_rules": [
    {
      "config": {
          "field": "publish_time", 
          "op": "time_range", 
          "gte": "now()-7d", 
          "lt": "now()"
      },
      "boost": 0.8
    },
    {
      "config": {
          "field": "publish_time", 
          "op": "time_range", 
          "lt": 1764886800
      },
      "boost": -0.8
    }
  ]
}
```



</Tab>
<Tab zoneid="dtYGWYccJ5" title="Example 4: Nested rules">
<TabTitle>Example 4: Nested rules</TabTitle>

**Goal:**  Boost items whose type is "electronics" **AND** whose rating is greater than or equal to 4.0.

```JSON
{
  "config": {
    "op": "and",
    "conds": [
      {"op": "must", "field": "category", "conds": ["electronics"]},
      {"op": "range", "field": "rating", "gte": 4.0}
    ]
  },
  "boost": 0.6
}
```


&nbsp;

**Goal:**  Boost items whose type is "electronics" **OR** whose rating is greater than or equal to 4.0.

```JSON
{
  "config": {
    "op": "or",
    "conds": [
      {"op": "must", "field": "category", "conds": ["electronics"]},
      {"op": "range", "field": "rating", "gte": 4.0}
    ]
  },
  "boost": 0.6
}
```



</Tab>
</Tabs>



---



<span id="910eb173"></span>
# Frequently Asked Questions (FAQ)

**Q: What happens if a boost/bury rule is invalid?** 

A: The system automatically ignores the invalid rule; all other valid rules still take effect as normal.

&nbsp;

**Q: How can I tell whether the dynamic boost/bury rules took effect?** 

A: The system returns the execution result for each rule in the same order as in the request body, including statuses such as success, field not found, and invalid field type. For details, see **Status**.
