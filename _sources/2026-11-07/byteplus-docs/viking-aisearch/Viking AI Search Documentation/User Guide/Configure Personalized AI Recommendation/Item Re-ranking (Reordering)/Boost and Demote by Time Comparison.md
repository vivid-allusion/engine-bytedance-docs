---
title: "Boost and Demote by Time Comparison"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Time-based_Boost_and_Demotion"
---

*Viking AI Search is an enterprise\-grade generative\-AI search product. It combines multimodal semantic understanding from large language models with ByteDance's long\-standing experience in information retrieval, giving you an out\-of\-the\-box platform to build multimodal image\-and\-text search and recommendation experiences. Try the full capability set: * [Viking AI Search — Unified Search, Recommendation & Q&A Engine](https://www.volcengine.com/product/viking-ai)


---



<span id="ab2f4b0b"></span>
# What This Feature Does

**Boost & Demote by Time Comparison** uses an item's **Listing Time** or **Timestamp** field to automatically reshape recommendation ranking. Two modes are supported:


* **Dynamic (until now)**  — evaluates a relative duration against the current time. Ideal for promoting new items or recent content.

* **Static (before / after)**  — evaluates against a fixed timestamp. Ideal for precise interventions around a specific launch moment or cutoff.


Typical scenarios include e\-commerce new\-arrival promotion, news recency ranking, and short\-video trend surfacing — anywhere you want freshness to dominate ordering. This capability replaces the old pattern of hand\-setting fixed dates and refreshing them on a schedule.

<span id="62880c32"></span>
## Key Benefits


* **Saves operator time** — configure once; the rule stays correct without weekly or monthly updates.

* **Higher engagement** — promote the freshest content while user interest is at its peak.

* **Healthier content lifecycle** — stale or less\-relevant items drop out of the top positions automatically.


<span id="6d6bbe97"></span>
## How It Works

Think of the feature as a **freshness rule**. On every request, the platform compares each item's time field with the reference time and applies the configured weight.

> *Example: an item published 3 days ago matches the rule "boost 30% if published within the last 7 days" → the item's ranking score rises by 30% and it moves up.* 


Items that do not match a rule are left untouched. You may configure multiple rules; each one takes effect within its recommendation scenario independently.

<span id="78dec197"></span>
# Prerequisite

The item dataset used by this recommendation scenario **must** include at least one field with the **Launch Time** or **Timestamp** attribute. 


---



<span id="ecd36581"></span>
# Configuration steps

<span id="78266d50"></span>
## Create a new rule

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">\*Note</div>


<div data-tips="true" data-tips-type="default">Rules have no priority. When an item matches multiple rules, the platform sums all weight factors to produce the final value.</div>


<div data-tips="true" data-tips-type="default">Example: Item A matches "Boost 50%" and "Demote 30%" → final effect is "Boost 20%".</div>



1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy** and click **Boost & Demote**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c8e2c0f0733543e7b24ec16206b1d3e8" width="314px" /></div>



&nbsp;

2. On the rule configuration page,  refer to the table below to complete all fields.



<columns>
<columnsItem zoneid="VfRnI7sOiV">

<div style="text-align: center">
<strong>Dynamic (up to now) time configuration</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/82949698ad474bb795ffdc9c4a3ba426) </span>



</columnsItem>
<columnsItem zoneid="UCZLl8VwRu">

<div style="text-align: center">
<strong>Static time configuration</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5044841895b24233a388cc4d92c5184f) </span>



</columnsItem>
</columns>



|**Configuration** |**Description** |
|---|---|
|**Rule Name** |A short, descriptive name for maintenance |
|**Target Field** |Pick a time attribute field. Field's attribute determines operators available. |
|**Configuration logic** |Choose an operator based on the field's attribute |
|| **"Launch Time" field:**  Supports dynamic (up to now) time configuration<br><br><br>* Dynamic (up to now) time configuration<br><br>   * Time granularity: minutes, hours, days<br><br>   * Comparison operators: within, outside |
|| **“Timestamp” field**: Supports dynamic (up to now) and static (earlier than, later than) time configurations<br><br><br>* Dynamic (up to now) time configuration<br><br>   * Time granularity: minutes, hours, days<br><br>   * Comparison operators: within, outside<br><br>* static (before, after) time configuration<br><br>   * time granularity: timestamp, second level<br><br>   * comparison operators: before, after |
|**Boost / Demote Factor** |Integer in the range  **\-100% to 100%** . The larger the absolute value, the stronger the effect |



3. Click **Confirm**. The rule takes effect on the next request in the **Experience panel**. 

4. After validation, click **Sync Configuration to API** to push the rule to production.


&nbsp;

<span id="e1eef2f5"></span>
## View existing rules


1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy → Boost & Demote**. All active rules for this scenario are listed.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c8e2c0f0733543e7b24ec16206b1d3e8" width="314px" /></div>



2. Hover over a rule and click **Edit** to view its full configuration.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9a2d669ca34547e3b3c62045fd15b68d" width="301px" /></div>


&nbsp;

<span id="6f3be6bf"></span>
## Edit existing rules


1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy → Boost & Demote**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c8e2c0f0733543e7b24ec16206b1d3e8" width="314px" /></div>



&nbsp;

2. Locate the target rule and click its **Edit** button.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9a2d669ca34547e3b3c62045fd15b68d" width="301px" /></div>



&nbsp;

3. After clicking edit, you can edit the existing rule configuration as needed.



|**Configuration** |**Description** |
|---|---|
|**Rule Name** |A short, descriptive name for maintenance |
|**Target Field** |Pick a time attribute field. Field's attribute determines operators available. |
|**Configuration logic** |Choose an operator based on the field's attribute |
|| **"Launch Time" field:**  Supports dynamic (up to now) time configuration<br><br><br>* Dynamic (up to now) time configuration<br><br>   * Time granularity: minutes, hours, days<br><br>   * Comparison operators: within, outside |
|| **“Timestamp” field**: Supports dynamic (up to now) and static (earlier than, later than) time configurations<br><br><br>* Dynamic (up to now) time configuration<br><br>   * Time granularity: minutes, hours, days<br><br>   * Comparison operators: within, outside<br><br>* static (before, after) time configuration<br><br>   * time granularity: timestamp, second level<br><br>   * comparison operators: before, after |
|**Boost / Demote Factor** |Integer in the range  **\-100% to 100%** . The larger the absolute value, the stronger the effect |



4. Click **Confirm** to save. The updated rule takes effect on the next request in the Experience panel.

5. After you verify the effect, you **must** click **Sync Configuration to API** to publish the rule to production.


&nbsp;

<span id="29131f45"></span>
## Delete rule


1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy → Boost & Demote**.

2. Click **Delete** on the target rule and confirm in the dialog.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e4817376d4fd440387548119e11aa262" width="408px" /></div>


&nbsp;

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="danger">Deletion is <strong>irreversible</strong>. The rule stops applying immediately, and will no longer influence Experience\-panel ranking from the next request onward.</div>



---



<span id="3e1d9f30"></span>
# Frequently Asked Questions

**Q1: Why do Experience\-panel results differ from production?** 

A: The Experience panel is a preview. Live results are further shaped by personalization, so some divergence is expected.

&nbsp;

**Q2: Why can't I see the effect of a rule I created?** 

A: Check, in order:


1. The **Match Scope** actually covers the items you expect.

2. The **weight factor** is large enough.

3. You have clicked **Sync Configuration to API** to publish the Experience\-panel change to production.


&nbsp;

**Q3: I picked a time field but the "Dynamic" mode is missing. Why?** 

A: Confirm that the field in the item dataset is configured with the **Listing Time** or **Timestamp** attribute. To change field attributes, contact the Volcengine technical team.

&nbsp;

**Q4: Why can I no longer edit some of my rules?** 

A: Legacy rules built on older Listing\-Time or Timestamp attributes are not compatible with the current capability. They are **read\-only** and can only be deleted. They continue to take effect until you delete them.


---



<span id="bec1de6f"></span>
# Related documentation


* Boost / demote by item attributes: [Boost and Demote by Item Attribute](https://docs.byteplus.com/docs/393/92198).

* Boost / demote by the user\-to\-item geographic distance:  [User location-based Boost and Demotion](https://docs.byteplus.com/docs/393/User_geographic_location-based_ranking_boost_and_demotion).
