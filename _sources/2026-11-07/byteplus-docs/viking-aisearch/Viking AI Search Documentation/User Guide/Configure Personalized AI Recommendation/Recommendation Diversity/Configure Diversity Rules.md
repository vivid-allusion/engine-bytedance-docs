---
title: "Configure Diversity Rules"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Diversity_rule_configuration"
---

*Viking AI Search is an enterprise\-grade generative\-AI search product. It combines multimodal semantic understanding from large language models with ByteDance's long\-standing experience in information retrieval, giving you an out\-of\-the\-box platform to build multimodal image\-and\-text search and recommendation experiences. Try the full capability set: * [Viking AI Search — Unified Search, Recommendation & Q&A Engine](https://www.volcengine.com/product/viking-ai)


---



<span id="764345f4"></span>
# Overview

Personalized recommendation matches each user with the items most relevant to them. However, when the item pool contains many highly similar items, the system may surface them together, making results feel repetitive and hurting the user experience.

The **Item Diversity Rules** feature lets you re\-rank the recommendation list **before it is returned to the user**, ensuring the final result set is diverse. It is designed for operations teams and strategy product managers who want to improve browsing experience and content discovery.

This topic explains how to configure and manage diversity rules within a recommendation scenario.

<span id="e0d5cecc"></span>
## Rule Types


|**Rule type** |**Description** |
|---|---|
|**Sliding\-window** |Prevents similar items from being grouped together. Two modes are supported:<br><br><br>1. Limit repetitions of a specific dimension value (for example, author ID or content category) within a sliding window.<br><br>2. Apply deduplication only to items that match a filter condition (for example, `is_lottery = true`). |
|**Top N items** |Prevents similar items from being grouped together in the top N items. The same two modes are supported. |


<span id="6e5f7a8e"></span>
## Typical Use Cases


* **Content platforms — avoid consecutive homogeneous items.**  In news, short\-video, or live\-streaming feeds, prevent consecutive items from the same author, category (tech, entertainment), or topic. For example, a short\-video app can add a rule on **author ID** to stop users from seeing back\-to\-back clips from the same creator.

* **E\-commerce — keep category and brand variety.**  In product feeds, avoid concentrating items from the same brand, category (dresses, sneakers), or price band. A fashion retailer can add a rule on **category ID** to interleave categories and reduce visual fatigue.

* **Music and podcast — broaden stylistic range.**  Prevent consecutive tracks from the same artist, genre (rock, classical), or podcast series. A rule on **style tag** helps users discover more varied audio content.



---



<span id="BVW6xb1Xka"></span>
# Operational steps

All rule changes are released in two phases: your changes first take effect in the "Experience Center" to verify their effect. After confirmation, update the configuration to apply the rules to the live production environment. This design aims to provide a secure testing environment to prevent unverified rules from affecting live users.

<span id="567dfa28"></span>
## Add new rule

Follow the steps below to create and activate a diversity rule within the recommendation scenario.


1. Go to **Experience Centre → Recommendation preview → Recommendation strategy →  Diversity rules.** 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1befab26f9a64168910e6c74626f6fcf" width="340px" /></div>



&nbsp;

2. Click the “Add Rule” button in the interface to open the new rule configuration window.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8f59763bb1544b33a74f3b9a173c3518" width="554px" /></div>



&nbsp;

3. Fill in the fields based on business needs



|**Field** |**Description** |
|---|---|
|**Rule name** |A short, readable name that identifies the rule. |
|**Rule Type** |Select between the 2 supported rule types: Sliding window or Top N. |
|**Window Size** |The number of items the rule evaluates.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Example</div><br><br><br><div data-tips="true" data-tips-type="default">With window size = 10 and max duplicates = 5, any 10 consecutive items contain at most 5 items sharing the same dimension value.</div><br> |
|**Item condition** |Defines which items the rule applies to:<br><br><br>* **Deduplication dimension**: the field to dedupe on. Must already exist in the item dataset.<br><br>* **Item filter** (optional): restrict the rule to a subset of items (for example, `category = lottery`).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">You cannot save a new rule whose <strong>sliding window size</strong> and <strong>item condition</strong> are identical to those of an existing rule.</div><br> |
|**Max duplicates** |The maximum number of items that may share the same dimension value within the window. **Must not exceed the sliding window size.**  |



&nbsp;

4. Click **Confirm**. The rule is created with the **lowest priority** by default. To change its priority, see [Manage rule priority](https://docs.byteplus.com/docs/393/Diversity_rule_configuration#db920a59).

5. The rule takes effect in the **Experience Centre ** on the next recommendation request.

6. Once you are satisfied with the result, click **Sync to API** in the top\-right corner of the rule list to publish the rule to the **production API**.


&nbsp;

<span id="dc1a8981"></span>
## View and Edit a Rule


1. Go to **Experience Centre → Recommendation preview → Recommendation strategy →  Diversity rules.** 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1befab26f9a64168910e6c74626f6fcf" width="340px" /></div>



&nbsp;

2. Locate the rule and click **Edit**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f183acd6e47e4f1ca381d8f26aabf99a" width="330px" /></div>



&nbsp;

3. Modify the rule name, sliding window size, item condition, or max duplicates as needed.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f56145839c5941cba512dd458e1d87ca" width="489px" /></div>



|**Field** |**Description** |
|---|---|
|**Rule name** |A short, readable name that identifies the rule. |
|**Rule Type** |Select between the 2 supported rule types: Sliding window or Top N. |
|**Window Size** |The number of items the rule evaluates.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Example</div><br><br><br><div data-tips="true" data-tips-type="default">With window size = 10 and max duplicates = 5, any 10 consecutive items contain at most 5 items sharing the same dimension value.</div><br> |
|**Item condition** |Defines which items the rule applies to:<br><br><br>* **Deduplication dimension**: the field to dedupe on. Must already exist in the item dataset.<br><br>* **Item filter** (optional): restrict the rule to a subset of items (for example, `category = lottery`).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">You cannot save a new rule whose <strong>sliding window size</strong> and <strong>item condition</strong> are identical to those of an existing rule.</div><br> |
|**Max duplicates** |The maximum number of items that may share the same dimension value within the window. **Must not exceed the sliding window size.**  |



&nbsp;

4. Click **Confirm**. The rule is updated; **its priority is preserved**. To change priority, see [Manage rule priority](https://docs.byteplus.com/docs/393/Diversity_rule_configuration#db920a59).

5. The rule takes effect in the **Experience Centre ** on the next recommendation request.

6. Once you are satisfied with the result, click **Sync to API** in the top\-right corner of the rule list to publish the rule to the **production API**.



---



<span id="db920a59"></span>
## Manage rule priority

When a scenario contains multiple diversity rules, the platform may be unable to satisfy all of them simultaneously. Rules are therefore executed in **priority order**, from top to bottom in the rule list — the higher a rule sits, the earlier it is applied.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">\*Warning</div>


<div data-tips="true" data-tips-type="warning">A lower\-priority rule may not take effect when it conflicts with a higher\-priority rule.</div>



&nbsp;

1. Go to **Experience Centre → Recommendation preview → Recommendation strategy →  Diversity rules**.

2. Press and hold the drag handle on the left side of a rule, then drop it at the desired position. The new order is saved immediately.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0edbd5ea618948c195eab25227a1f0b8" width="384px" /></div>



&nbsp;

3. The updated diversity rule priority takes effect in the **Experience Centre ** on the next recommendation request.

4. Once you are satisfied with the result, click **Sync to API** in the top\-right corner of the rule list to publish the rule to the **production API**.


<span id="11abc7ce"></span>
## Delete rule

Follow the steps below to delete an active diversity rule configuration:


1. Go to **Experience Centre → Recommendation preview → Recommendation strategy →  Diversity rules**.

2. Click **Delete** on the target rule


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/567fa55f6f1e40c0be844c773c8de376" width="360px" /></div>



&nbsp;

3. The rule is immediately disabled in the preview environment on the next recommendation request.

4. Click **Update configuration** to remove the rule from the production API.



---



<span id="7e0682c4"></span>
# FAQ

**Q: Why do I get "Max duplicates cannot exceed the sliding window size" when saving?** 

A: **Max duplicates** value is larger than the ** window size**. Increase the window, or decrease the max duplicates, so that window ≥ max duplicates.

&nbsp;

**Q: Why does the system say the rule conflicts with an existing one?** 

A: A new rule cannot share both the same ** window size** and **item condition** with any existing rule. Change at least one of these values and try again.
