---
title: "AI Search: Boost and Bury via API (V1)"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/AI_Search_Boost_Demotion"
---

<span id="677d6172"></span>
# Function overview

To dynamically adjust search result rankings in real\-time, you can use the API\-based boosting and demotion feature. This reference explains how to specify conditional rules (fields, operators, values) and weight intensity directly within a search request, allowing you to bypass the limitations of manual console configurations and implement dynamic, business\-driven ranking strategies.

<span id="1bcd09e2"></span>
# Core values


1. **Reduced Manual Maintenance:**  Eliminates the risk of human error or omissions during manual weight adjustments, empowering more efficient business operations.

2. **Dynamic Business Integration:**  Enables customers to integrate boosting/demotion logic with their own business systems (such as inventory, marketing, or risk control) for real\-time adjustments and faster response times.

3. **User\-Level Personalization:**  Supports weight configurations at the individual user level, significantly enhancing the personalized search experience.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Version Notice</div>


<div data-tips="true" data-tips-type="warning">To improve extensibility and flexibility, this API released the <strong>V2 format on April 18, 2026</strong>. New integrators are strongly encouraged to adopt the V2 format directly. </div>


<div data-tips="true" data-tips-type="warning">The legacy format remains supported long\-term, and mixed use of legacy and V2 formats within a single request is allowed. Existing integrators can migrate at their own pace.</div>


<div data-tips="true" data-tips-type="warning">For details of the new format, see <a href="https://docs.byteplus.com/docs/viking-aisearch/112797">AI Search: Boost and Bury via API (V2)</a>.</div>



---



<span id="b660a919"></span>
# API configuration

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Preconditions</div>


<div data-tips="true" data-tips-type="default">You must have already successfully integrated the AI Search Engine <strong>Search API</strong>. Please refer to <a href="https://docs.byteplus.com/docs/viking-aisearch/Search">Search</a>.</div>


&nbsp;

When sending a search request, simply add the relevant boosting and demotion parameters. The platform will automatically merge the weight rules configured in the **Console** with those provided via the **API**.

<span id="9ef89377"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Example value** |
|---|---|---|---|
|conditional_boost |Array <**Conds**\> |**`Required`** |See below: [Conds](https://docs.byteplus.com/docs/viking-aisearch/AI_Search_Boost_Demotion#ca81d523) |


<span id="ca81d523"></span>
### Conds

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">If a rule is invalid, the service will automatically ignore individual boosting or demotion rules to ensure other valid rules remain effective.</div>



|**Parameter name** |**Data format** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|conds |Array <**BoostConfig**\> |**`Required`** |See below: [BoostConfig](https://docs.byteplus.com/docs/viking-aisearch/AI_Search_Boost_Demotion#38cf87d9) |**Boost and Demotion Configuration**<br><br>The platform only boosts or demotes items that meet the criteria. |
|boost |Float |**`Required`** |0.3, \-0.3 |**Boost and Demotion Intensity**<br><br>Supports any value between \-1 and 1. |


<span id="38cf87d9"></span>
### BoostConfig


|**Parameter Name** |**Data Format** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|field |String |**`Required`** |`"author"` |**Conditional field**<br><br>Field used for boosting or demotion condition.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip for nested field</div><br><br><br><div data-tips="true" data-tips-type="default">Fields can be configured using "."; for example: "category.name"</div><br> |
|op |String |**`Required`** |`"must"` |**operator**<br><br>Operators supported by each field type are as follows: [Field–Operator–Condition value configuration] |
|conds |Based on the field |**`Required`** | |**Condition value**<br><br>A set of conditions for boosting and demotion. Supported values for each field type and operator are as follows: [Field–Operator–Condition value configuration](https://docs.byteplus.com/docs/viking-aisearch/AI_Search_Boost_Demotion#6099735e) |


<span id="6099735e"></span>
### **Field–Operator–** Condition value **configuration**


|**Field type (field)**  |**Field attribute** |**Supported operator (op)**  |**Condition value input (conds)**  |
|---|---|---|---|
|**Int32** |No attribute, other attributes |* `equal` (equals)<br><br>* `not_equal` (not equals)<br><br>* `lte` (less than or equal to)<br><br>* `lt` (less than)<br><br>* `gte` (greater than or equal to)<br><br>* `gt` (greater than) |Int32 format data |
|**Int64** |no attribute, other attributes |* `equal` (equal to)<br><br>* `not_equal` (not equal to)<br><br>* `lte` (less than or equal to)<br><br>* `lt` (less than)<br><br>* `gte` (greater than or equal to)<br><br>* `gt` (greater than) |Int64 format data |
||timestamp<br><br>release time \- UNIX format |* `before`<br><br>* `after` |UNIX timestamp |
|||* `within` (in range) |* `Xd` (X days)<br><br>* `Xh` (X hours)<br><br>* `Xm` (X minutes) |
|**Float** |Unsupported attribute |* `lt` (less than)<br><br>* `gt` (greater than) |Float format data |
|**String** |No attribute, other attributes |* `must` (include)<br><br>* `must_not` (exclude) |Array<String\> format data |
|||* `equal` (equals)<br><br>* `not_equal` (not equals) |String format data |
||release time |* `before` (earlier than)<br><br>* `after` (later than) |UNIX timestamp |
|||* `within` (within range) |* `Xd` (X days)<br><br>* `Xh` (X hours)<br><br>* `Xm` (X minutes) |
|**Array(String)**  |no special attributes |* `must` (include)<br><br>* `must_not` (exclude) |Array<String\> format data |
|**Array(Int)**  |No special attributes |* `must` (include)<br><br>* `must_not` (exclude) |Array<Int\> format data |
|**Array(Float)**  |<div style="text-align: center"><br><strong>Not supported temporarily</strong></div><br> |||
|**Array(Object)**  |<div style="text-align: center"><br><strong>Not supported temporarily</strong></div><br> |||
|**Boolean** |<div style="text-align: center"><br><strong>Not supported temporarily</strong></div><br> |||


&nbsp;


---



<span id="6fe89772"></span>
## Response parameters

The system returns the search results after weight adjustment. Additionally, the extra_info field provides the execution status of your dynamic boosting and demotion rules.

&nbsp;

<span id="3bc10544"></span>
### ExtraInfo

> For more information, see the search interface: [Search](https://docs.byteplus.com/docs/viking-aisearch/Search)



|**parameter** |**type** |**example value** |**description** |
|---|---|---|---|
|`boost_status` |Array <String\> |`["success", "field not found", "invalid operator"]` |The execution status of each boosting/demotion rule. status meanings. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">The statuses strictly follow the order of the <strong>BoostConfig</strong><strong> </strong>parameters specified in the <strong>Conds</strong> parameters.</div><br><br><br><div data-tips="true" data-tips-type="default">For example: the first configuration executes successfully, boost_status's first status will be "success".</div><br> |


<span id="49cb8580"></span>
### Status


|**Status value** |**Execution status** |**Meaning** |
|---|---|---|
|success |✅  success |**The rule configuration meets expectations**<br><br>The boosting and demotion rules are successfully applied to this request. |
|field not found |❌  failure |**The field (** **`field`** **) validation failed**<br><br>Ensure the configured field exists in the item dataset. |
|invalid field type |❌  failure |**The data type of the field (** **`field`** **) does not support boosting or demotion**<br><br>Currently, Array<float\>, Array<object\>, and Boolean fields do not support boosting or demotion rules.<br><br>Ensure the field type matches the expectation.  |
|invalid date field |❌  failure |**The field (** **`field`** **) is not a time attribute**<br><br>The condition value input (`conds`) uses the time attribute configuration format, but the field (`field`) is not configured as "timestamp" or "publish time". |
|invalid operator |❌  failed |**The field (** **`field`** **) is valid but the configured operator (** **`op`** **) is invalid**<br><br>Please ensure operator configuration meets expectations.  |
|invalid conds |❌  failed |**The field (** **`field`** **) and operator (** **`op`** **) are valid, but the condition value input (** **`conds`** **) is invalid**<br><br>possible reasons include:<br><br><br>1. incorrect data format<br><br>2. The value provided is invalid for a field configured with the “timestamp” or “publish time” attribute.<br><br><br>Please ensure the condition value input meets expectations. |
|invalid boost |❌  failure |**The configuration for boost and demotion intensity is invalid.** <br><br>Make sure the input is a number between \-1 and 1. |


&nbsp;


---



<span id="d9dbe1d9"></span>
# Example


<Tabs>
<Tab zoneid="wmRpv5KiSc" title="Example 1 - e-commerce">
<TabTitle>Example 1 - e-commerce</TabTitle>

Requirement: When a user searches,


1. **Boost** popular brand products and the weight of specified merchants

2. **Demote** the weight of out\-of\-stock items


&nbsp;

```JSON
"conditional_boost": [
    {
        "conds": [
            {
                "field": "brand",
                "op":"must",
                "conds":["apple", "samsung", "huawei"],
            }
         ],
        "boost": 0.8
     },
     {
        "conds": [
            {
                "field": "seller_id",
                "op":"must",
                "conds":["123"],
            }
         ],
        "boost": 0.5
     },
     {
        "conds": [
            {
                "field": "available_qty",
                "op":"lte",
                "conds":0,
            }
         ],
        "boost": -0.8
     }
 ]

```



</Tab>
<Tab zoneid="T2VGYwK5lE" title="Example 2 - content community">
<TabTitle>Example 2 - content community</TabTitle>

Requirement: When a user searches,


1. **Boost** the weight of popular authors' articles and topics


&nbsp;

```JSON
"conditional_boost": [
    {
        "conds": [
            {
                "field": "author",
                "op":"must",
                "conds":["author_1","author_2"],
            }
         ],
        "boost": 0.3
     },
     {
        "conds": [
            {
                "field": "tags",
                "op":"must",
                "conds":["topic_1"],
            }
         ],
        "boost": 0.8
     }
 ]
```



</Tab>
<Tab zoneid="vbC2S6169r" title="Example 3 - time-based boost and demote">
<TabTitle>Example 3 - time-based boost and demote</TabTitle>

Requirement: When a user searches,


1. **Boost** the weight of items published within 7 days

2. **Demote** the weight of items published more than 30 days ago


&nbsp;

```JSON
"conditional_boost": [
    {
        "conds": [
            {
                "field": "pub_time",
                "op":"within",
                "conds":"7d",
            }
         ],
        "boost": 0.8
     },
     {
        "conds": [
            {
                "field": "pub_time",
                "op":"before",
                "conds":1764886800,
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
# FAQ

**Q: What happens if a boost or demotion rule is invalid?** 

A: The system automatically ignores invalid boost and demotion rules; other valid rules remain effective.

&nbsp;

**Q: How can users know the execution results of dynamic boost and demotion rules?** 

A: The system returns the execution results of dynamic boost and demotion rules in the order of the request body parameters, including success, field not found, invalid field type, and other information.
