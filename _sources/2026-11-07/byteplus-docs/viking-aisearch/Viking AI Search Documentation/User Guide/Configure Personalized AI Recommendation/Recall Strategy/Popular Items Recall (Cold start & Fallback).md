---
title: "Popular Items Recall (Cold start & Fallback)"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Recommended_Fallback_Strategy"
---

*Viking AI Search is a Large\-Language\-Model and AI\-based enterprise search product. It uses multimodal semantic understanding from large language models, combined with ByteDance's experience in information retrieval, to provide a ready\-to\-use platform for building and integrating end\-to\-end multimodal search and recommendation capabilities.* 

<span id="2765eab0"></span>
# Popular Items Recall (New users cold start & Fallback strategy)

**Popular items Recall** is a recommendation strategy that ranks items either by global user behavior statistics or by a selected item field, and recommends whichever items are currently most popular. It is the underlying implementation of what this article calls the "fallback strategy."

<span id="16c9cfe9"></span>
## Applicable scenarios

Popular items Recall addresses two problems:


1. **Recommendation fallback:**  When other personalized recommendation strategies (for example, a "similar items" or "recommended for you" strategy) do not recall enough items, Popular items Recall adds globally popular items so the recommendation result is never empty. This improves the user experience.

2. **New user cold start: ** For new users, or users with little behavior history, the system cannot generate effective personalized recommendations. In this case, Popular items Recall suggests generally popular items as a starting point for discovery.


<span id="411a6bfd"></span>
## Prerequisites

Before you configure Popular items Recall, make sure that:


* You have linked at least one item dataset.

* You have created a recommendation scenario.

* If you plan to use the **User event data** method, you have ingested behavior data for a behavior type that reflects genuine popularity (for example, `purchase`, `collect`, or `share`).

* If you plan to use the **Sort by item field** method, your item dataset already includes a field suitable for ranking (for example, a sales count or a popularity score).



---



<span id="dead59a1"></span>
# Configuration steps

<span id="61252a9e"></span>
## Step 1: Open the configuration entry point

In the **Recall section ** on the left, find **Popular items recall.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/553080ffc0ce4cce81943ead5be0200b" width="400px" /></div>


&nbsp;

<span id="f2e10d52"></span>
## Step 2: Choose a rule type and set parameters

Expand **Popular items Recall**, then select **Add Rule** (or select an existing rule to edit it) to open the configuration panel. The panel offers two mutually exclusive configuration methods, choose one:

<span id="a53c7982"></span>
### Method A: User event data

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/308a6b01e6bf4f3ca3d1f613a359e071) </span>


|**Setting** |**Input constraints** |**Description** |
|---|---|---|
|Event type |At least 1 rule; select **Add behavior** to add more |Each rule follows the pattern "When the item occurs [behavior type], when the item is hot, add [X] point(s)." You can add multiple behavior types, each with its own point value; the platform sums them into one popularity score. |
|Statistical past (time window) |Minimum 5 minutes, maximum 14 days. Units: minutes, hours, or days. |The time range the platform uses to calculate item popularity from user event data. For example, if you set this to 7 days, the platform counts behavior data from the past 7 days only. |
|Use the item field when there are not enough popular items |Toggle, off by default |When enabled, if item interactions are too low to produce enough popular items under the rules above, the platform supplements the result by sorting on an item field instead (see Method B). <br><br>**This setting takes effect the next day (T+1), not immediately.**  Plan your rollout timing accordingly. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Recommendation</div>



1. <div data-tips="true" data-tips-type="default">Choose user event types that strongly indicate genuine user preference, such as <code>purchase</code>, <code>collect</code>, or <code>share</code>. Avoid relying only on weakly related behaviors like <code>impression</code> (view), since these can lower the quality of the popularity ranking.</div>


2. <div data-tips="true" data-tips-type="default">Avoid only choosing user event types that occur rarely to prevent the case where there are insufficient popular items due to lack of user events. </div>



<span id="b39954d2"></span>
### Method B: Sort by item field

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bad671bec5c247c5b4aa5086d8e56151) </span>


|<div style="text-align: top"><br><strong>Setting</strong></div><br> |<div style="text-align: top"><br><strong>Input constraints</strong></div><br> |<div style="text-align: top"><br><strong>Description</strong></div><br> |
|---|---|---|
|<div style="text-align: top"><br>Item field sorting rule</div><br> |<div style="text-align: top"><br>Select one item field, plus a sort direction (descending or ascending order)</div><br> |<div style="text-align: top"><br>Ranks items directly by the selected field to produce the popularity list, without relying on user event data. Useful when behavior data is too sparse for Method A, but the item dataset already has a usable popularity or sales field.</div><br> |


<span id="c46e23a5"></span>
## Step 3: Confirm and save configuration


1. When you are done, select **Confirm** to save the configuration.

2. In the **Recall section ** on the left, find **Popular** ** items recall ** and select the new recall strategy


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/553080ffc0ce4cce81943ead5be0200b" width="400px" /></div>



3. Preview the rule to confirm it fits your business scenario.

4. In the top\-right corner, select Update online configuration to publish the change.


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>



1. <div data-tips="true" data-tips-type="default">Popular item strategy does not retroactively recalculate against historical data in real time — it accumulates user event data incrementally instead. A new configuration needs new user event data and time to accumulate before it can determine popular items.</div>


2. <div data-tips="true" data-tips-type="default">Item field sorting output is only produced on a T+1 (next\-day) basis. After configuring it, wait for the T+1 output to confirm the sorting matches your expectations.</div>



&nbsp;

<span id="95050f24"></span>
### How this relates to the Recall Merge Strategy

Popular items Recall corresponds to the "item popularity recall" channel in **Recall fusion Strategy**. When you configure fusion weights there, **the popular items recall weight must be at least 1%** , or popular items may not be available for fallback and cold\-start scenarios. 

To adjust this channel's share of the final recommendation result, see [Configure and Adjust Recall Merge Strategy](https://docs.byteplus.com/docs/viking-aisearch/Configure_and_Adjust_Recall_Merge_Strategy).


---



<span id="bc48296f"></span>
# Best practices


|<div style="text-align: top"><br><strong>Scenario</strong></div><br> |<div style="text-align: top"><br><strong>Recommended method</strong></div><br> |<div style="text-align: top"><br><strong>Suggested time window</strong></div><br> |<div style="text-align: top"><br><strong>Suggested behavior types</strong></div><br> |
|---|---|---|---|
|<div style="text-align: top"><br>E\-commerce promotions / best\-seller\-driven periods</div><br> |<div style="text-align: top"><br>User event data</div><br> |<div style="text-align: top"><br>24 hours \- 48 hours</div><br> |<div style="text-align: top"><br><code>purchase</code>, <code>collect</code></div><br> |
|<div style="text-align: top"><br>Everyday content platform recommendations</div><br> |<div style="text-align: top"><br>User event data</div><br> |<div style="text-align: top"><br>2 days \- 7 days</div><br> |<div style="text-align: top"><br><code>share</code>, <code>collect</code></div><br> |
|<div style="text-align: top"><br>Sparse behavior data</div><br> |User event data |7 days \- 14 days |`click` |
|Early cold start |<div style="text-align: top"><br>Sort by item field</div><br> | | |


<span id="89a822f5"></span>
## FAQ


* **Can I use both methods (User event data and Sort by item field) at the same time?**  

   * Both methods are mutually exclusive, only 1 can be active at any point in time. 

* **Why does the item\-field Fall\-back toggle (and Method B) take effect the next day (T+1) instead of immediately?**  

   * Item field sorting, whether used as the Method A fallback or configured directly as Method B, is produced on a T+1 (next\-day) cycle. Wait for the T+1 output before evaluating the result. 

* **Why don't I see updated hot items immediately after saving a Method A (User event data) rule?** 

   * Method A does not retroactively recalculate against historical data. It accumulates behavior data incrementally, starting from when you save the rule, so a new or changed rule needs new behavior data — and time for it to accumulate — before it produces results.

* **Can Popular items Recall and Item cold start recall be enabled at the same time? If so, which one takes priority?**  

   * They can be enabled at the same time. Item cold start recall takes priority and is merged after all other recall channels are merged and undergo fine\-ranking, in order to ensure new items are not outcompeted by established high\-traffic items and can get sufficient exposure opportunities to accumulate initial interaction data.

* **What happens if I only select ** **`impression`** ** as my behavior type?**  

   * The popularity ranking may be lower quality, because `impression` (a view) is only weakly correlated with genuine user interest. We recommend combining it with stronger signals such as `purchase` or `collect` rather than using it alone.
