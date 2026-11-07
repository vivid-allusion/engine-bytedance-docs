---
title: "Initial Configuration of Item Pool"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Initial_Configuration_of_Item_Pool"
---

<span id="98941071"></span>
# Background

**Item pool ** is the set of active items within an application that are eligible for search, recommendation, and conversational search. By configuring pre\-filters at the application level, you can define which items from your item dataset qualify for the item pool. Items that do not meet the filter conditions are excluded from indexing and the retrieval pipeline.

This article covers the concept of the item pool, how to configure it, and important considerations during setup and updates.


---



<span id="65207557"></span>
# Overview

<span id="41f72de4"></span>
## Key concepts

In Viking AI Search, the relationship between the item pool and item dataset is as follows:


* **Item dataset** — The complete set of item data you have imported into the platform.

* **Pre\-filter conditions** — A set of filter rules configured at the application level.

* **Item pool** — The subset of items in the item dataset that match the pre\-filter conditions. Only items in the item pool participate in vectorization, index building, and retrieval.


<span id="bbf321ff"></span>
## **Use Cases**

The item pool is well\-suited for the following scenarios:


* **Vertical content delivery** — When the target items represent a small fraction of the dataset (for example, only recommending content with specific tags), using an item pool reduces empty retrieval results.

* **State\-aware visibility control** — Display only items that are listed, in stock, and approved.

* **Time\-window restrictions** — Display items only within their copyright validity period or active availability window.

* **Compliance and safety** — Exclude items that must not be shown publicly, preventing them from entering the index.


<span id="33e844fd"></span>
## **Scope**

The item pool applies uniformly across the following pipelines within an application: search, conversational search, and personalized recommendation.


---



<span id="b9344fff"></span>
# Configuration steps

<span id="a23a5f0b"></span>
## Prerequisites

Before configuring the item pool, ensure the following conditions are met:


* An application has been created and the item dataset association process has been initiated. See [Create and link item dataset](https://docs.byteplus.com/docs/viking-aisearch/Create_an_Application_and_Link_Item_Datasets), [Link existing item dataset](https://docs.byteplus.com/docs/viking-aisearch/98550).


<span id="cc51e1c1"></span>
## Pre\-filter vs. Request\-level Filter

The item pool's pre\-filter and the `filter` parameter in search and recommendation API requests (request\-level filter) can be used simultaneously. When both are active, they are combined with logical `AND`.


| |**Item pool (Pre\-filter)**  |**Request\-level filter (Post\-filter)**  |
|---|---|---|
|Applied at |Index building and retrieval stage |Query stage |
|Configured via |Console, applied at the application level |Passed per API request |
|Cost |Items that don't match are not indexed or computed. |All items participate in indexing |
|Typical use cases |Long\-term, stable visibility rules |Dynamic per\-request or per\-user conditions |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Recommendation</div>


<div data-tips="true" data-tips-type="default">We recommend configuring stable business rules as item pool pre\-filters, and handling dynamic conditions through request\-level filters.</div>



---



<span id="454eb2e0"></span>
## Initial Item Pool Configuration

<span id="0f70a0f3"></span>
### Step 1: Create an application

See [Create Application](https://docs.byteplus.com/docs/viking-aisearch/98549).

<span id="247f24a8"></span>
### Step 2: Link item dataset

See [Link existing item dataset](https://docs.byteplus.com/docs/viking-aisearch/98550)details. Ensure that any fields you intend to use for filtering have the **Filterable** attribute enabled.

&nbsp;

<span id="9fb8bad7"></span>
### Step 3: Configure Item Pool Filter Condition

Click **Add** to begin configuring your pre\-filter rules. You can combine multiple conditions using AND or OR logical operators. The platform supports one level of nested logic.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Only fields marked as <strong>Filterable</strong> can be used in filter conditions. The console does not validate filter expressions — ensure that the item pool contains items that satisfy your filter conditions.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b98eb3178757466b85afd9bc5465cde9) </span>

<span id="456ed33f"></span>
### Step 4: Preview Item Pool

After completing the filter expression, click **Preview Valid Data** to see which items in the dataset match the item pool conditions.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e95818346d9b408aac7ad4fd9c94c2f3) </span>

&nbsp;

If the matched count is 0, the console displays:  *"No valid data matches this filter. Please update the filter conditions."* 


<columns>
<columnsItem zoneid="TWo3ezL8lT">

<div style="text-align: center">
<strong>Items matching the filter conditions</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c345b36671ee4b7f8db1934fbddf202c) </span>



</columnsItem>
<columnsItem zoneid="Jt95tE4qn8">

<div style="text-align: center">
<strong>No items matching the filter conditions</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9bdae17bd256497cb22992011abd4aba) </span>



</columnsItem>
</columns>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default"><strong>Special note if you </strong><a href="https://docs.byteplus.com/docs/viking-aisearch/Create_an_Application_and_Link_Item_Datasets"><strong>Create and link item dataset</strong></a><strong> in the application.</strong></div>


<div data-tips="true" data-tips-type="default">If no item dataset has been created before you click <strong>Preview Valid Data</strong>, the platform will prompt you to create one. Before proceeding, confirm the field names, types, and attributes, as these cannot be modified after the dataset is created. After the dataset is created, the platform automatically refreshes the preview results in approximately 20 seconds. </div>


<div data-tips="true" data-tips-type="default">If there are still no matches, click <strong>Recalculate</strong>.</div>


<div style="text-align: center">
<div data-tips="true" data-tips-type="default"><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/46242c88797641b3be7ab27a20a38f34" width="348px" /></div>
</div>


<div data-tips="true" data-tips-type="default"></div>


&nbsp;

<span id="01de8527"></span>
### Step 5: Activate Dataset

Click **Complete**. The platform will associate and activate the item data. During the data backfill phase, the platform performs the following:


* Items that do not meet the filter conditions are not vectorized and are not written to the index (no item data processing fees are charged for these items).

* Items that do not meet the filter conditions are marked as non\-searchable and non\-recommendable.


&nbsp;

<span id="35a62293"></span>
## Update Item Pool Configuration

See [Change application item scope (pre-filter)](https://docs.byteplus.com/docs/viking-aisearch/98551)


---



<span id="e8bbbff7"></span>
# Billing


1. The platform charges item processing fees only for items that satisfy the pre\-filter conditions.

2. If an item's field values change such that the item now meets the item scope conditions, the platform automatically adds it to the item pool. No additional API call costs are incurred, but item processing fees apply.

3. Updating the item scope configuration triggers a data backfill. Item data processing fees are charged based on the number of items that satisfy the new item scope conditions after backfill


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For detailed billing items, see <a href="https://docs.byteplus.com/docs/viking-aisearch/Standard_plan">Viking AI Search (Standard plan) billing details</a></div>



---



<span id="fff656ab"></span>
# FAQ


1. **Will live requests be affected while the item pool is being updated?**  

   No. During backfill, live requests continue to use the original item pool. The platform automatically switches to the new configuration once backfill is complete.

2. **Why does the preview count differ from the actual index count?**  

   The preview count reflects items that match the pre\-filter conditions. The actual index count may be lower due to processing failures or errors on individual items. Hover over the tool tip icon next to the data count for details.

3. **How do the item pool and the ** **`filter`** ** parameter in API requests interact?**  

   They are combined with logical AND. Items returned by a request must satisfy both the item pool conditions and the request\-level filter.

4. **If a dataset is deleted or replaced, are the item pool settings retained?**  

   Item pool settings are tied to the association between an application and a dataset. Settings become inactive when the association is removed and must be reconfigured after re\-association.

5. **Can I configure an item pool using fields that are not marked as Filterable?**  

   No. You must first mark the target field as **Filterable** in the dataset before using it in item scope configuration.



---



***Related Documents***


* [Create and link item dataset](https://docs.byteplus.com/docs/viking-aisearch/Create_an_Application_and_Link_Item_Datasets)

* [AI Search: Filter](https://docs.byteplus.com/docs/viking-aisearch/AI_search_filter)

* [Configure Static Filter Rules](https://docs.byteplus.com/docs/viking-aisearch/Static_Recommendation_Scope_Configuration)

* [Configure Dynamic Filter Conditions](https://docs.byteplus.com/docs/viking-aisearch/Dynamic_recommendation_scope_configuration)

* [Why did the recommendation not return any items?](https://docs.byteplus.com/docs/viking-aisearch/empty_recommendation)
