---
title: "Configure and Adjust Recall Merge Strategy"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configure_and_Adjust_Recall_Merge_Strategy"
---

<span id="7a9212d5"></span>
# Overview

BytePlus AI Search uses a **multi\-channel recall + fusion ranking** architecture. The platform pulls candidates from multiple recall channels in parallel — user\-profile recall, similar\-user\-interest recall, multimodal item recall, item popularity recall, parent\-item recall — and merges them into the final result list according to the **merge weights** you configure.

The Recall Merge Strategy lets you:


* **Pick a merge strategy per scenario** for Home / Detail Page / Shopping Cart independently.

* **Use preset strategies out of the box** — 3\-5 presets covering *User Profile First*, *Multimodal First*, *Popularity First*, *Item Similarity First*.

* **Customize the weights** — fine\-tune per\-channel weight when presets do not fit.


<span id="d4a87aca"></span>
# Recall Channels


|Channel |Description |Needs User Events? |Applicable Scenarios |
|---|---|---|---|
|Similarity Recall |Finds items similar to the "primary item" via item embedding. |No |Product Detail Page, Shopping Cart |
|Similar\-User Recall |Collaborative filtering based on similar users. |Yes |Recommended for You, <br><br>Product Detail Page |
|User Interest Recall |Recall based on user profile. |Yes |Recommended for You, Product Detail Page, Shopping Cart |
|Multimodal Recall |Item\-to\-item recall over multimodal embeddings; new items participate from day 0. |No |Recommended for You, <br><br>Product Detail Page |
|Popularity Recall |Global hot items, used as fallback and cold\-start booster. |Yes |Recommended for You, <br><br>Product Detail Page |


<span id="7003edb5"></span>
## Preset Strategies by Scenario

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Weights of all the recall channels must sum to 100%; Popularity Item + Similar Item recall need to be ≥ 1%.</div>


<span id="a4fcdd70"></span>
### Recommended for you


|Strategy |When to Use |Similar Users |User Interest |Multimodal |Popularity |
|---|---|---|---|---|---|
|User Profile  **(Default)**  |Strengthen user interest while keeping variety |35% |35% |20% |10% |
|Multimodal |Highlight multimodal similarity, mitigate cold start |20% |20% |50% |10% |
|Popularity |Big\-sale / hero\-item push |20% |20% |10% |50% |
|Custom |Customized business requirements |Any |Any |Any |≥ 1% |


<span id="01ce0b2c"></span>
### Product Detail Page


|Strategy |When to Use |Similar Items |Similar Users |User Interest |Multimodal |Popularity |
|---|---|---|---|---|---|---|
|Item Similarity  **(Default)**  |Same\-line / Complementary items |80% |5% |5% |5% |5% |
|User Profile |Strengthen user interest |10% |35% |35% |10% |10% |
|Multimodal |Cross\-category similar items |10% |15% |15% |50% |10% |
|Popularity |Big\-sale / hero\-item push |10% |15% |15% |10% |50% |
|Custom |Customized business requirements |Any |Any |Any |Any |≥ 1% |


<span id="0776024a"></span>
### Shopping Cart


|Strategy |When to Use |Similar Items |User Interest |
|---|---|---|---|
|Item Similarity  **(Default)**  |Complementary items for the cart |90% |10% |
|Custom |Customized business requirements |Any |Any |



---



<span id="9e00f075"></span>
# Configuration

<span id="ea699e87"></span>
## Entry Point


1. Log in to the console. Go to **Experience Configuration \> Recommendation Experience**.

2. Pick the target scenario and enter its configuration view.

3. In the **Scenario Configuration** panel, locate **Recall Fusion Strategy**. Pick a preset, or choose **Custom Mode**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a139cfd4cdad4df7b19e15bc8e13d216" width="350px" /></div>


&nbsp;

<span id="8964c3f2"></span>
## Using Custom Mode


1. In **Scenario Configuration**, locate **Recall Fusion Strategy**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/657a5e2748e341d2a8d5a542df7f7e36" width="284px" /></div>



&nbsp;

2. Click the dropdown and pick  **✎ Custom Mode** at the bottom.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ca1ebb98bb034d9dbc434b87fb5c97f9" width="309px" /></div>



&nbsp;

3. Enter the weight (integer percent) for each channel.

4. The dialog footer shows a live distribution bar and a sum check — the total **must equal 100%** , otherwise saving is blocked.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7af649d5b2b44be99b98dabfcab47f43" width="434px" /></div>



5. Click **Done** to save.

6. Return to the Recommendation Experience view to verify the output.


&nbsp;

<span id="c38dd084"></span>
## Apply and Publish


|**Action** |**Scope** |
|---|---|
|Save on the Recommendation Experience view |Takes effect on the experience view only; live API is not affected. |
|Click **Update to API** in the top\-right corner |Publishes to production; the live Recommend API immediately returns results under the new strategy. Canary first before key sales events. |



---



<span id="e21ad291"></span>
# Frequently Asked Questions

<span id="ebaaeb1d"></span>
## Tuning Guide


|**Symptom** |**Suggested Adjustment** |
|---|---|
|Results look homogeneous |Decrease Item CF / Parent Item; increase Multimodal I2I and Popularity; combine with Diversity Rules. |
|New items get almost no exposure |Switch to *Multimodal First* and / or enable *New Item Cold Start*. |
|Big\-sale push |Switch to *Popularity First*; verify the Fallback Strategy time window and behavior type. |
|Product Detail Page items not similar enough to main item |Increase Parent Item; verify category / brand fields in the item dataset. |
|Personalization underperforming overall |Start with *User Profile First* default; validate user event dataset coverage. |


<span id="dc7f9fb3"></span>
## FAQ

**Q1: Can the merge strategy be switched per API request?** 

Not in the current version. The strategy is configured at the scenario level. For A/B routing, create multiple scenarios and route on the business side.

**Q2: What if I set a channel weight to 0 in Custom Mode?** 

A weight of 0 disables the channel from final fusion. Popularity and (for Detail / Cart) Parent Item are bounded at ≥ 1% and cannot be set to 0.

**Q3: How does the merge weight relate to ranking?** 

Fusion weights determine the proportion each channel contributes to the **ranking candidate pool**. Ranking then re\-scores candidates with business metrics (CTR, CVR). Fusion weights influence *which items enter ranking*, not the final ordering directly.

**Q4: With ** ***New Item Cold Start*** ** enabled, are new\-item recalls affected by fusion weights?** 

No. New\-item recalls **skip ranking and join only at the re\-rank stage**, so ranking cannot suppress them. Fusion weights apply only to the regular multi\-channel recall.
