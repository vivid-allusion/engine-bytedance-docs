---
title: "Edit Item Pool"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Edit_Item_Pool"
---

<span id="2a7219f8"></span>
# Background

**Item pool ** is the set of active items within an application that are eligible for search, recommendation, and conversational search. By configuring pre\-filters at the application level, you can define which items from your item dataset qualify for the item pool. Items that do not meet the filter conditions are excluded from indexing and the retrieval pipeline.

This article covers the concept of the item pool, how to configure it, and important considerations during setup and updates.


---



<span id="77ecd333"></span>
# Overview

<span id="a5512804"></span>
## Key concepts

In Viking AI Search, the relationship between the item pool and item dataset is as follows:


* **Item dataset** — The complete set of item data you have imported into the platform.

* **Pre\-filter conditions** — A set of filter rules configured at the application level.

* **Item pool** — The subset of items in the item dataset that match the pre\-filter conditions. Only items in the item pool participate in vectorization, index building, and retrieval.


<span id="2a51869f"></span>
## **Use Cases**

The item pool is well\-suited for the following scenarios:


* **Vertical content delivery** — When the target items represent a small fraction of the dataset (for example, only recommending content with specific tags), using an item pool reduces empty retrieval results.

* **State\-aware visibility control** — Display only items that are listed, in stock, and approved.

* **Time\-window restrictions** — Display items only within their copyright validity period or active availability window.

* **Compliance and safety** — Exclude items that must not be shown publicly, preventing them from entering the index.


<span id="407bb401"></span>
## **Scope**

The item pool applies uniformly across the following pipelines within an application: search, conversational search, and personalized recommendation.


---



<span id="577c5ba9"></span>
# Configuration steps

<span id="9d6bb77a"></span>
## Prerequisites

Before configuring the item pool, ensure the following condition is met:


* An application has been created and an item dataset has been completed. See[Create and link item dataset](https://docs.byteplus.com/docs/viking-aisearch/Create_an_Application_and_Link_Item_Datasets), [Link existing item dataset](https://docs.byteplus.com/docs/viking-aisearch/98550).


<span id="b45a8b7f"></span>
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



<span id="d5c6dc5d"></span>
## Update Item Pool Configuration

<span id="4d295dee"></span>
### Step 1: Access Item Pool settings

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ff83d862c9da4b45a4f0a6fb8d31ba42) </span>

&nbsp;

<span id="1f99168d"></span>
### Step 2: Modify item pool conditions

Update the filter conditions for the item scope. You can combine multiple conditions using AND or OR logical operators. The platform supports one level of nested logic.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">\*Note</div>


<div data-tips="true" data-tips-type="default">Only fields marked as <strong>Filterable</strong> can be used in filter conditions. The console does not validate filter expressions — ensure that the item pool contains items that satisfy your filter conditions.</div>


&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3661c84e49d64d7fbf8289e7fd15025d) </span>

&nbsp;

<span id="ef3320fc"></span>
### Step 3: Preview Item Pool

After completing the filter expression, click **Preview Valid Data** to see which items in the dataset match the item pool conditions.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/068f9bcdc84a40598a74d64e7b61aaad) </span>

&nbsp;

<span id="2d202d89"></span>
### Step 4: Confirm changes

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/35b9c0123d3f420d9c3ea3e553016f0b) </span>


---



<span id="da5b6162"></span>
# Billing


1. The platform charges item processing fees only for items that satisfy the pre\-filter conditions.

2. If an item's field values change such that the item now meets the item scope conditions, the platform automatically adds it to the item pool. No additional API call costs are incurred, but item processing fees apply.

3. Updating the item scope configuration triggers a data backfill. Item data processing fees are charged based on the number of items that satisfy the new item scope conditions after backfill


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For detailed billing items, see <a href="https://docs.byteplus.com/docs/viking-aisearch/Standard_plan">Viking AI Search (Standard plan) billing details</a></div>



---



<span id="233c1f9f"></span>
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
