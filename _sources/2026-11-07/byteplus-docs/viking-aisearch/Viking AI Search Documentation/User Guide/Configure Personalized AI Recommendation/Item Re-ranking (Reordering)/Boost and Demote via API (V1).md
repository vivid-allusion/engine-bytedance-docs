---
title: "Boost and Demote via API (V1)"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/boost_demote_api_v1"
---

***Viking AI Search*** * is an enterprise\-grade AI search product based on generative AI, leveraging the multimodal semantic representation and understanding capabilities of large models, combined with years of best practices in information retrieval at ByteDance, to provide customers with an out\-of\-the\-box AI search platform service, helping them easily build and integrate end\-to\-end multimodal image and text search and recommendation capabilities. To experience more capabilities of Viking AI Search, click to go to: * [Viking AI Search engine, the integrated intelligent engine for enterprise search and recommendations](https://www.volcengine.com/product/AI-Search-Rec)


---



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Version Notice</div>


<div data-tips="true" data-tips-type="warning">To improve extensibility and flexibility, this API released the <strong>V2 format on April 18, 2026</strong>. New integrators are strongly encouraged to adopt the V2 format directly. </div>


<div data-tips="true" data-tips-type="warning">The legacy format remains supported long\-term, and mixed use of legacy and V2 formats within a single request is allowed. Existing integrators can migrate at their own pace.</div>


<div data-tips="true" data-tips-type="warning">For details of the new format, see <a href="https://docs.byteplus.com/docs/393/Recommendation_API_uplift_and_demotion_rule_configuration">Boost and Demote via API (V2)</a>.</div>


<span id="677d6172"></span>
# Overview

This API enables dynamic boost and de\-boost configuration at request time. You specify the **field, operator, condition value, and boost strength (range: \-1 to 1)**  directly in the request to adjust recommendation ranking weights in real time. Compared with the previous console\-only workflow, this approach significantly reduces operational overhead and increases flexibility.

<span id="15266d99"></span>
## Key Benefits


* **Lower maintenance cost.**  Removes manual steps and prevents oversights during weight adjustment.

* **Integration with business systems.**  Boost / de\-boost logic can be driven by your inventory, marketing, or risk\-control systems for real\-time adjustment.

* **Fine\-grained personalization.**  Per\-user weight configuration enhances personalized recommendations.


<span id="ed22cd00"></span>
## Typical Use Cases


* **E\-commerce.**  After a user clicks an electronic\-product detail page, the next recommendation request can dynamically boost items of the same brand to prioritize them.

* **Content platforms.**  When a user follows a new author, subsequent requests can boost articles by that author to match short\-term interests.

* **Marketing campaigns.**  During promotions, boost promotional items dynamically to increase their exposure.



---



<span id="b660a919"></span>
# API Configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">\*Version Notice</div>


<div data-tips="true" data-tips-type="warning">To improve extensibility and flexibility, this API released the <strong>V2 format on April 18, 2026</strong>. New integrators are strongly encouraged to adopt the V2 format directly. </div>


<div data-tips="true" data-tips-type="warning">The legacy format remains supported long\-term, and mixed use of legacy and V2 formats within a single request is allowed. Existing integrators can migrate at their own pace.</div>


<div data-tips="true" data-tips-type="warning">For details of the new format, see <a href="https://docs.byteplus.com/docs/393/Recommendation_API_uplift_and_demotion_rule_configuration">Boost and Demote via API (V2)</a>.</div>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Prerequisites</div>


<div data-tips="true" data-tips-type="default">You must have already integrated the Viking AI Search recommendation API. See <a href="https://docs.byteplus.com/docs/viking-aisearch/Recommendation">Recommendation</a></div>


<span id="42e54221"></span>
## Request

Add the top\-level field `conditional_boost` to the request body of a recommendation call. The platform automatically merges rules configured in the console with those passed via the API.

<span id="9ef89377"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`conditional_boost` |`Array<`**`Conds`**`>` |Yes |See below |List of boost / de\-boost rules |


<span id="ca81d523"></span>
### Conds

If a rule is invalid, the system automatically skips that single rule; other valid rules continue to take effect.


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`conds` |`Array<`**`BoostConfig`**`>` |Yes |See below |Rule conditions. Only items matching the conditions are boosted or de\-boosted |
|`boost` |`Float` |Yes |`0.3` / `-0.3` |Boost / de\-boost strength. Range: `-1` to `1` |


<span id="38cf87d9"></span>
### BoostConfig


|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`field` |`String` |Yes |`"author"` |The field used for condition matching. Use `.` for nested fields, e.g. `category.name` |
|`op` |`String` |Yes |`"must"` |Operator. Supported operators depend on the field type — see the table below. |
|`conds` |Depends on `field` |Yes |— |Condition values. Supported formats depend on field type and operator — see the table below. |


<span id="6099735e"></span>
### Field — Operator — Condition Value Matrix


|**Field Type** |**Field Attribute** |**Supported Operators** |**Condition Value Format** |
|---|---|---|---|
|`Int32` |None / Any |`equal`, `not_equal`, `lte`, `lt`, `gte`, `gt` |`Int32` |
|`Int64` |None / others |`equal`, `not_equal`, `lte`, `lt`, `gte`, `gt` |`Int64` |
||Timestamp / Launch time (UNIX) |`before`, `after` |UNIX timestamp |
|||`within` |`Xd` (X days) / `Xh` (X hours) / `Xm` (X minutes) |
|`Float` |None / Any |`lt`, `gt` |`Float` |
|`String` |None / others |`must`, `must_not` |`Array<String>` |
|||`equal`, `not_equal` |`String` |
||Launch time |`before`, `after` |UNIX timestamp |
|||`within` |`Xd` / `Xh` / `Xm` |
|`Array<String>` |None / Any |`must`, `must_not` |`Array<String>` |
|`Array<Int>` |None / Any |`must`, `must_not` |`Array<Int>` |
|`Array<Float>` |Not Supported |||
|`Array<Object>` |Not Supported |||
|`Boolean` |Not Supported |||


&nbsp;


---



<span id="6fe89772"></span>
## Response

The API returns the re\-ranked recommendation results after weight adjustment, along with the execution status of each rule via the `extra_info` field.

<span id="3bc10544"></span>
### ExtraInfo

> For the full schema, see the recommendation API reference: [ExtraInfo](https://docs.byteplus.com/docs/viking-aisearch/Recommendation#09fcad10)



|**Parameter** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|`boost_status` |`Array<String>` |`["success", "field not found", "invalid operator"]` |Execution status for each rule. Status meaning, see below: [Status](https://docs.byteplus.com/docs/viking-aisearch/Recommendation_API_uplift_and_demotion_rule_configuration#49cb8580)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Order</div><br><br><br><div data-tips="true" data-tips-type="default">The order <strong>strictly matche</strong>s the order of <code>BoostConfig</code> in the request — e.g., the first element corresponds to the first <code>BoostConfig</code></div><br> |


<span id="49cb8580"></span>
#### Status


|**Status** |**Result** |**Meaning and Troubleshooting** |
|---|---|---|
|`success` |✅ Success |Rule applied successfully in this request |
|`field not found` |❌ Failure |Field validation failed. Verify that the field exists in your item dataset |
|`invalid field type` |❌ Failure |The field's data type does not support boosting. `Array<Float>`, `Array<Object>`, and `Boolean` are currently not supported |
|`invalid date field` |❌ Failure |The condition value uses a time\-based format, but `field` is not configured as *Timestamp* or *New\-arrival time* |
|`invalid operator` |❌ Failure |The field is valid, but the operator is not supported for this field type. See the matrix above |
|`invalid conds` |❌ Failure |Field and operator are valid, but the condition value is malformed or does not match the required format for *Timestamp* / *New\-arrival time* attributes |
|`invalid boost` |❌ Failure |The boost strength is outside the `-1` to `1` range |


&nbsp;


---



<span id="d9dbe1d9"></span>
# Example


<Tabs>
<Tab zoneid="wmRpv5KiSc" title="Example 1 - E-commerce">
<TabTitle>Example 1 - E-commerce</TabTitle>

**Requirement:**  When the user clicks on the homepage of an electronic product, the next recommendation request:


1. **Boost** related brand products and merchants

2. **Demote ** out\-of\-stock items


```JSON
"conditional_boost": [
    {
        "conds": [
            {
                "field": "brand",
                "op":"must",
                "conds":["apple", "samsung", "huawei"]
            }
         ],
        "boost": 0.8
     },
     {
        "conds": [
            {
                "field": "seller_id",
                "op":"must",
                "conds":["123"]
            }
         ],
        "boost": 0.5
     },
     {
        "conds": [
            {
                "field": "available_qty",
                "op":"lte",
                "conds":0
            }
         ],
        "boost": -0.8
     }
 ]

```



</Tab>
<Tab zoneid="T2VGYwK5lE" title="Example 2 - Content community">
<TabTitle>Example 2 - Content community</TabTitle>

**Request:**  When a user newly follows an author or searches for a topic, the next recommendation request


1. **Boost** articles by the same author and on the same topic


&nbsp;

```JSON
"conditional_boost": [
    {
        "conds": [
            {
                "field": "author",
                "op":"must",
                "conds":["author_1","author_2"]
            }
         ],
        "boost": 0.3
     },
     {
        "conds": [
            {
                "field": "tags",
                "op":"must",
                "conds":["topic_1"]
            }
         ],
        "boost": 0.8
     }
 ]
```



</Tab>
<Tab zoneid="vbC2S6169r" title="Example 3 - Time boost and demotion">
<TabTitle>Example 3 - Time boost and demotion</TabTitle>

**Request:**  In the next recommendation request


1. **Boost ** items published within 7 days

2. **Demote** items published before a specific point in time


&nbsp;

```JSON
"conditional_boost": [
    {
        "conds": [
            {
                "field": "pub_time",
                "op":"within",
                "conds":"7d"
            }
         ],
        "boost": 0.8
     },
     {
        "conds": [
            {
                "field": "pub_time",
                "op":"before",
                "conds":1764886800
            }
         ],
        "boost": -0.8
     }
 ]
```



</Tab>
</Tabs>



---



<span id="910eb173"></span>
# Frequently asked questions (FAQ)

**Q: What happens if a boost / demote rule is invalid?** 

A: The system automatically skips the invalid rule. Other valid rules still apply, and the request as a whole does not fail.

&nbsp;

**Q: How can I verify whether my dynamic boost / demote rules took effect?** 

A: The response's `extra_info.boost_status` returns the execution status of each rule in the exact order submitted (`success`, `field not found`, `invalid field type`, etc.).
