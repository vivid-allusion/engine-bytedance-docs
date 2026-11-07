---
title: "Pinned Recommendation"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Pinned_Recommended_Items"
---

*Viking AI Search is an enterprise\-grade generative\-AI search product. It combines multimodal semantic understanding from large language models with ByteDance's long\-standing experience in information retrieval, giving you an out\-of\-the\-box platform to build multimodal image\-and\-text search and recommendation experiences. Try the full capability set: * [Viking AI Search — Unified Search, Recommendation & Q&A Engine](https://www.volcengine.com/product/viking-ai)


---



<span id="jXgtGWIfWd"></span>
# Background

**Pinned Recommendation** lets you fix specific items at the top of the recommendation feed to meet high\-exposure needs for marketing campaigns, promotions, and other operational use cases. By concentrating traffic on a small set of priority items during a defined period, you can materially lift conversion.

This document explains how to create and manage pinned recommendations.

<span id="A4HzmSBfB8"></span>
# What This Feature Does

Pinned Recommendation is an **operator\-override capability**. An operator manually selects one or more items and fixes them at the top of the feed. Those items bypass the personalized ranking algorithm and are guaranteed priority exposure under the configured conditions.

<span id="F7BgdppvWj"></span>
## Key Features


* **Manual pinning** — fix one or more items at the top of the feed.

* **Priority management** — when multiple items are pinned, you define their display order.


<span id="SF6sXJV7gF"></span>
## Usage Limits


* Pinned items occupy regular recommendation slots, and their display logic **takes precedence over** all personalized algorithms.

* The platform automatically drops pinned items that have been deleted.


<span id="e0b9c926"></span>
## Additional Notes


* If the recommendation response for a request is empty, the platform **does not** surface pinned items on their own.

* If the recommendation response returns **fewer** items than the number of pinned items, only the portion that fits is returned.


<span id="AzN8xI6n2C"></span>
# Configuration Steps


1. In the **Recommendation Experience** console, go to **Recommendation Strategy → Ranking → Pinned Items** and click **Add Item**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2c3507b4de5f491db1225530d051fec8" width="374px" /></div>



2. In the dialog, search by **Item ID or keyword** in the top search box, then select one or more target items from the result list. The platform automatically tries, in order:

   * Exact match on Item ID;

   * Exact match on item keyword;

   * Fuzzy match on item keyword.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a16eb186ad9d4aa7943d46cbef0fc36d" width="412px" /></div>



&nbsp;

3. Click **Confirm**. Selected items are written to the **Pinned Items** list.

4. Manage ordering from the Pinned Items list:

   * **Drag** rows to reorder.

   * Click the **delete icon** to remove a single item.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6a7de011faa244cdba154aedfa67af14" width="388px" /></div>



5. Use the **Repeat Pinned Items on Every Refresh** toggle to control refresh behavior — see [Pin on Every Refresh](https://docs.byteplus.com/docs/393/92193#c05becd3).

6. In the right\-hand **Experience panel**, click "**Recommend again"**  to simulate multiple refresh requests from the same user and validate the pinning effect.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f799fc02c1ab4e77b99578554ba02500" width="298px" /></div>



&nbsp;

7. Once validation passes, click **Sync Changes to API** to publish the change to the live endpoint.


&nbsp;

<span id="c05becd3"></span>
## Pin on Every Refresh

This toggle decides whether pinned items continue to appear across multiple requests from the same user. In some product shapes (for example, infinite scroll feeds), returning pinned items on every request conflicts with the client UX and causes the same item to be exposed multiple times within one session. 

Turn the toggle off to avoid this.


|**State** |**Behavior** |
|---|---|
|On (Default) |Pinned items are returned on every recommendation request. |
|Off |The platform consults the `session_id` in the request:<br><br><br>* If pinned items were **already returned** to the same `session_id` within the last **24 hours** → the pinning config is ignored for this request.<br><br>* If pinned items were **not** returned to the same `session_id` within the last **24 hours** → the pinning config applies and pinned items are returned. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">When <strong>Pin on Every Refresh</strong> is off, you <strong>must</strong> include the <code>session_id</code> parameter on every recommendation request. Without it, the platform cannot determine repeat state. See <a href="https://docs.byteplus.com/docs/393/Recommendation#4fa39169">Request Body</a> for the field definition.</div>


&nbsp;

<span id="gAAIbQPZSX"></span>
# Frequently Asked Questions

**Q: I get "Item ID not found" when adding a pinned item.** 

A: Verify that the Item ID is correct and that the item exists in the item dataset linked to the current application.

&nbsp;

**Q: I can't find my item by keyword search.** 

A: Try a different keyword. The platform searches only across fields configured with the **Used for Filter** or **Used for Text Search** attribute. Fields without those attributes will not be searchable.
