---
title: "Configure Static Filter Rules"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Static_Recommendation_Scope_Configuration"
---

<span id="ba0b063a"></span>
# Introduction

Static recommendation scope configuration defines **fixed filtering rules for recommendation results. ** Its primary value is helping businesses quickly exclude items that do not meet basic requirements, such as out\-of\-stock products or blocked categories. To meet complex enterprise requirements, this feature supports sophisticated static filtering logic to ensure every recommended item strictly adheres to your business standards.

**<ins>Suitable scenarios</ins>**


1. **Often\-changing business rules**, such as short\-term restrictions on particular products or items.

2. Items filtered out are a **small percentage of the item pool, ** with majority of items in the item dataset fulfill the filter condition. 


This article describes the configuration steps and logic of static recommendation scope.

<span id="9825450f"></span>
# Important Note

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>



1. <div data-tips="true" data-tips-type="warning">The platform does not perform mutual exclusion checks. Ensure the filtering logic is correct during configuration. If mutually exclusive conditions exist, the system returns empty results without reporting an error.</div>


2. <div data-tips="true" data-tips-type="warning">If an item is missing a specific field used in a filter, the system automatically ignores that filtering condition for that item. For more information, see <a href="https://docs.byteplus.com/docs/viking-aisearch/Static_Recommendation_Scope_Configuration#545109f8">Automatic Degradation</a>.</div>




---



<span id="d16960e2"></span>
# Create a filter rule


1. In the left navigation bar, select ** Scope** \> **Define Recommendable Items** to open the static recommendation scope configuration page.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/756f02cdaed2413e86b5e5e797adaab0" width="500px" /></div>



2. Click **Add Rule** and configure filter rules based on your business needs. Each filter rule supports condition groups to achieve compound logic, such as (A and B) or C, **with up to one level of nesting.** 

   
   |**Configuration** |**Description** |
   |---|---|
   |Outer logical operator |In nested filters, it defines the top\-level logical relationship between condition groups (AND/OR). |
   |Logical operator |Defines condition combination logic. AND requires all conditions to be met; OR requires any one condition to be met. |
   |Filter field |Select an item field from the dropdown list. **Only fields marked as Filterable are supported.**  |
   |Condition type |Select a matching rule, such as `found in`, `not found in`, or numerical range comparison. |
   |Condition value |Enter the matching value. |
   

   **For a detailed demonstration, view the video below. ** 

   <video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9aa1a295fe5a4348bb069a679a88c5b1" controls></video>
   


<span id="9bc2218b"></span>
## Supported Operators


|**Operators / Data Type** |<div style="text-align: center"><br><strong>String</strong></div><br> |<div style="text-align: center"><br><strong>Integer</strong></div><br> |<div style="text-align: center"><br><strong>Float</strong></div><br> |<div style="text-align: center"><br><strong>Array<X\></strong></div><br> |<div style="text-align: center"><br><strong>Boolean</strong></div><br> |<div style="text-align: center"><br><strong>Publish time</strong></div><br> |<div style="text-align: center"><br><strong>Timestamp</strong></div><br> |<div style="text-align: center"><br><strong>Object</strong></div><br> |
|---|---|---|---|---|---|---|---|---|
|**Found in** |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Not found in** |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**In range** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Less than / Earlier than** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Less than or equal to** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Greater than / Later than** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Greater than or equal to** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Equals** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Not equal to** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |
|**Dynamic time range** |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>\-</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>✅</div><br> |<div style="text-align: center"><br>\-</div><br> |


<span id="545109f8"></span>
# Automatic Degradation

When an item is missing a field required by a filtering condition, the system automatically ignores that condition for the affected item.

**For example,**  if an item is missing the field required for filter condition A, the platform applies the following logic:


|**Filter Rule** |**Final output** |
|---|---|
|A AND B |Item does not meet filter conditions |
|A OR B |The result depends on **filter condition B**. |
|A AND (B AND C) |Item does not meet filter conditions |
|A AND (B OR C) |Item does not meet filter conditions |
|A OR (B AND C) |The result depends on the ** (B AND C) filter conditions.**  |
|A OR (B OR C) |The result depends on the  **(B OR C) filter conditions.**  |
|B AND (A OR C) |The result depends on the  **(B AND C) filter conditions.**  |
|A AND (A AND C) |Item does not meet filter conditions |
|A OR (A AND C) |Item does not meet the filter conditions |



---



<span id="2b654529"></span>
## Dynamic filters

In some recommendation scenarios, users may want to add additional varied filter conditions based on personal preferences. For these use cases, use the dynamic filtering feature.  

For more details, refer to: [Configure Dynamic Filter Conditions](https://docs.byteplus.com/docs/viking-aisearch/Dynamic_recommendation_scope_configuration).
