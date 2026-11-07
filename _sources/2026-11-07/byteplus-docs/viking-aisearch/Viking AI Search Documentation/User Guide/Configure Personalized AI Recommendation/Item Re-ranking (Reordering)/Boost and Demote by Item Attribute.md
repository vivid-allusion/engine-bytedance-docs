---
title: "Boost and Demote by Item Attribute"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Item_Attribute_Boost_and_Demotion"
---

*Viking AI Search is an enterprise\-grade generative\-AI search product. It combines multimodal semantic understanding from large language models with ByteDance's long\-standing experience in information retrieval, giving you an out\-of\-the\-box platform to build multimodal image\-and\-text search and recommendation experiences. Try the full capability set: * [Viking AI Search — Unified Search, Recommendation & Q&A Engine](https://www.volcengine.com/product/viking-ai)


---



<span id="49743877"></span>
# What This Feature Does

**Boost & Demote by Item Attribute** is an operator\-override capability. By adjusting a **weight factor**, an operator can raise or lower the ranking priority of specific items in the recommendation feed, providing a direct lever to shape results in line with business objectives.

<span id="KVIz1aZ2Jh"></span>
## Key Capabilities


* **Boost** — raise the weight of matched items so they appear more often.

* **Demote** — lower the weight of matched items so they appear less often.

* **Weight factor** — integer in the range  **\-100% to 100%** . The larger the absolute value, the stronger the effect.


<span id="bae38207"></span>
## Typical Use Cases


* **New\-item promotion** — boost newly listed items to accelerate exposure.

* **Inventory clearance** — boost overstocked items to speed up sell\-through.

* **Suppression of low\-quality items** — demote items with negative feedback or quality issues.



---



<span id="wxQnE81rOx"></span>
# Configuration steps

<span id="PTDr528UXv"></span>
## Create a Rule

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Rules have <strong>no priority</strong>. When an item matches multiple rules, the platform sums all weight factors to produce the final value.</div>


<div data-tips="true" data-tips-type="default">Example: Item A matches "Boost 50%" and "Demote 30%" → final effect is "Boost 20%".</div>



1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy** and click **Boost & Demote**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c8e2c0f0733543e7b24ec16206b1d3e8" width="314px" /></div>



&nbsp;

2. After entering the rule configuration page,  fill in the following information:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/be2d54afe5e542e693a40d0271625e2b" width="525px" /></div>



|**Field** |**Description** |
|---|---|
|Rule name |Enter a simple and clear name. |
|Scope |Pick a target field from the item dataset plus a match operator. <br><br>Additional clauses may be added as needed.<br><br>Example: boost all items in the Shoes category → field `category`, operator `Equals`, value `Shoes` |
|Boost/demotion Factor |Integer in the range  **\-100% to 100%** The larger the number, the more significant the boost or demotion effect. |



3. Click **Confirm**. The new rule takes effect on the next recommendation request in the **Experience panel**.

4. After you verify the effect, you **must** click **Sync Configuration to API** to publish the rule to production.


&nbsp;

<span id="0959b519"></span>
## View existing rules


1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy → Boost & Demote**. All active rules for this scenario are listed.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c8e2c0f0733543e7b24ec16206b1d3e8" width="314px" /></div>



2. Hover over a rule and click **Edit** to view its full configuration.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9a2d669ca34547e3b3c62045fd15b68d" width="301px" /></div>


&nbsp;

<span id="4be6d9b2"></span>
## Edit existing rules


1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy → Boost & Demote**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c8e2c0f0733543e7b24ec16206b1d3e8" width="314px" /></div>



&nbsp;

2. Locate the target rule and click its **Edit** button.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9a2d669ca34547e3b3c62045fd15b68d" width="301px" /></div>



&nbsp;

3. On the rule editing page, you can modify the following information:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/be2d54afe5e542e693a40d0271625e2b" width="525px" /></div>



|**Field** |**Description** |
|---|---|
|Rule name |Enter a simple and clear name. |
|Scope |Pick a target field from the item dataset plus a match operator. <br><br>Additional clauses may be added as needed.<br><br>Example: boost all items in the Shoes category → field `category`, operator `Equals`, value `Shoes` |
|Boost/demotion Factor |Integer in the range  **\-100% to 100%** The larger the number, the more significant the boost or demotion effect. |



4. Click **Confirm** to save. The updated rule takes effect on the next request in the Experience panel.

5. After you verify the effect, you **must** click **Sync Configuration to API** to publish the rule to production.


&nbsp;

<span id="9e72c7be"></span>
## Delete rule


1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy → Boost & Demote**.

2. Click **Delete** on the target rule and confirm in the dialog.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e4817376d4fd440387548119e11aa262" width="408px" /></div>


&nbsp;

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="danger">Deletion is <strong>irreversible</strong>. The rule stops applying immediately, and will no longer influence Experience\-panel ranking from the next request onward.</div>


&nbsp;


---



<span id="365cdc44"></span>
# Frequently Asked Questions

**Q1: Why do Experience\-panel results differ from production?** 

A: The Experience panel is a preview. Live results are additionally shaped by personalization, so some divergence is expected.

**Q2: Why can't I see the effect of a rule I created?** 

A: Check, in order:


1. The **Match Scope** actually covers the items you expect.

2. The **weight factor** is large enough (effect scales with absolute value).

3. You have clicked **Sync Configuration to API** to publish the Experience\-panel change to production.


**Q3: Why can I no longer edit some of my rules?** 

A: Legacy rules built on the `listing_time` or `timestamp` attributes are not compatible with the new capability. They are **read\-only** and can only be deleted. They continue to take effect until you delete them.

&nbsp;

<span id="f28cda10"></span>
## **Related documents**


* Boost / demote items by the user\-to\-item geographic distance: [User location-based Boost and Demotion](https://docs.byteplus.com/docs/393/User_geographic_location-based_ranking_boost_and_demotion).

* Boost / demote items by `publish_time` or `listing_time`:  [Boost and Demote by Time Comparison](https://docs.byteplus.com/docs/393/Time-based_Boost_and_Demotion).
