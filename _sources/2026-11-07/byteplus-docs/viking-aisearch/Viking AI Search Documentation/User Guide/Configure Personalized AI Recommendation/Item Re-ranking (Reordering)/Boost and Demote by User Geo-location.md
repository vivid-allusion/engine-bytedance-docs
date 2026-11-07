---
title: "Boost and Demote by User Geo-location"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/User_geographic_location-based_ranking_boost_and_demotion"
---

*Viking AI Search is an enterprise\-grade generative\-AI search product. It combines multimodal semantic understanding from large language models with ByteDance's long\-standing experience in information retrieval, giving you an out\-of\-the\-box platform to build multimodal image\-and\-text search and recommendation experiences. Try the full capability set: * [Viking AI Search — Unified Search, Recommendation & Q&A Engine](https://www.volcengine.com/product/viking-ai)


---



<span id="92887b24"></span>
# What This Feature Does

**Boost & Demote by User Geo\-location** is a location\-based operator\-override capability. The platform uses the **distance between the user and each item** as a condition to reshape recommendation ranking, enabling new\-item promotion, inventory clearance, suppression of low\-quality items, or region\-aware distribution.

<span id="KVIz1aZ2Jh"></span>
## Key Capabilities


* **Boost** — raise the weight of matched items so they appear more often.

* **Demote** — lower the weight of matched items so they appear less often; can be triggered by a distance threshold.

* **Weight factor** — integer in the range  **\-100% to 100%** . The larger the absolute value, the stronger the effect.

* **Distance dimension** — configure weight rules using the real\-world distance between user and item for region\-aware boosting or demotion.


<span id="564ec1df"></span>
## Typical Use Cases


* **Demote far\-away items** — demote items with cross\-region inventory or restricted delivery to improve geographic relevance and fulfillment experience.

* **Boost nearby items** — boost items from nearby stores or warehouses to lift conversion and timeliness.


<span id="0b845616"></span>
# Prerequisite

Before enabling this capability, you **must** ensure the item dataset used by the recommendation scenario has both `longitude` and `latitude` field attributes configured. Otherwise, the **User\-to\-Item Distance** option will not appear in the rule configuration page.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ee7f1bab58de4cfba040df23b6c84dc8) </span>


---



<span id="wxQnE81rOx"></span>
# Configuration steps

<span id="PTDr528UXv"></span>
## Create a Geo\-location Rule

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Rules have no priority. When an item matches multiple rules, the platform sums all weight factors to produce the final value.</div>


<div data-tips="true" data-tips-type="default">Example: Item A matches "Boost 50%" and "Demote 30%" → final effect is "Boost 20%".</div>



&nbsp;

1. Go to **Experience Configuration → Recommendation Experience → Recommendation Strategy** and click **Boost & Demote**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/12411cf694ff46daa528c4aa99d00a79" width="305px" /></div>



&nbsp;

2. After entering the rule configuration page, fill in the following information:



|**Field** |**Description** |
|---|---|
|Rule Name |A short, descriptive name, e.g., "Demote items \>20 km from Singapore users" |
|Scope |1. Navigate to "calculated fields" and select "distance between user and item".<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/77916254f79c4767a7dfdfa843731e27) </span><br><br><br>2. In the condition settings, select "Within" or "Beyond" from the dropdown, enter the distance value (e.g., 20) in the input box, and choose the unit.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/022e738c9cd945e09ae4a6d58a552415) </span><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">What if an item has multiple coordinates?</div><br><br><br><div data-tips="true" data-tips-type="default"><em>If an item carries multiple </em><code><em>(longitude, latitude)</em></code><em> pairs, the platform automatically picks the pair </em><strong><em>closest to the user</em></strong><em> when computing distance.</em></div><br> |
|Boost / Demote Factor |Integer in the range  **\-100% to 100%**  |



3. Click **Confirm**. The rule takes effect on the next request in the **Experience panel**. We recommend validating with [Experience location rules](https://docs.byteplus.com/docs/393/User_geographic_location-based_ranking_boost_and_demotion#b8ff614f)before publishing.

4. After validation, click **Sync Configuration to API** to push the rule to production.


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">API Request</div>


<div data-tips="true" data-tips-type="default">Live API requests <strong>must</strong> include a <code>location</code> object inside <code>context</code>. Without it, geo\-based rules cannot be evaluated. See <a href="https://docs.byteplus.com/docs/393/Recommendation#65900099">Context</a> for details.</div>


<div data-tips="true" data-tips-type="default">```JSON
{
  "context": {
    "location": {
      "longitude": 116.4,
      "latitude": 39.9
    }
  }
}
```
</div>


&nbsp;

<span id="b8ff614f"></span>
## Experience location rules

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Prerequisites</div>


<div data-tips="true" data-tips-type="default">You must have completed <a href="https://docs.byteplus.com/docs/viking-aisearch/User_geographic_location-based_ranking_boost_and_demotion#PTDr528UXv">Create a Geo\-location Rule</a>.</div>



1. Go to **Experience Configuration → Recommendation Experience** and select the target scenario (for example, home feed or product list page).

2. In the **Test User** panel on the left, specify test coordinates in one of two ways:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d23fc40d94b64fa99da2cfac85cb9999" width="376px" /></div>




|**Option** |**Description** |
|---|---|
|Use my location |Ask the browser for the current location. Requires browser geolocation permission.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Fail to retrieve location</div><br><br><br><div data-tips="true" data-tips-type="default">If <strong>Use my location</strong> fails to populate the coordinates, check the following in order:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">System\-level location services are enabled.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">The browser is permitted to access location.</div><br><br><br>3. <div data-tips="true" data-tips-type="default">If you previously denied the permission, <strong>restart the computer</strong> to clear permission restrictions.</div><br> |
|Specify user location |Enter longitude and latitude manually, e.g., `longitude 116.4°, latitude 39.9°`. |


3. Click **Refresh Recommendations**. The platform computes distance from the simulated user coordinate to each item's coordinate and applies the configured rules. Examples:

   1. **Nearby boost** — Rule "Within 5 km of user, boost 50%" → matching items rank higher.

   2. **Far\-away demote** — Rule "Beyond 20 km from user, demote 80%" → matching items rank lower.



---



<span id="99f2aff8"></span>
# Frequently Asked Questions

**Q1: Why do Experience\-panel results differ from production?** 

A: The Experience panel previews with the test coordinates you supplied. In production, the rule evaluates against the user's real location, so some divergence is expected.

**Q2: Why can't I see the effect of a rule I created?** 

A: Check, in order:


1. The item dataset has `longitude` and `latitude` fields correctly configured.

2. The **distance condition** in the rule aligns with the test coordinates.

3. The **weight factor** is large enough.

4. You have clicked **Sync Configuration to API** to publish the change.


**Q3: Why is the "User\-to\-Item Distance" option missing?** 

A: Confirm the item dataset used by this scenario has `longitude` and `latitude` field attributes. To change field attributes, contact the BytePlus technical team.

<span id="d352c821"></span>
## Related documents


* Boost / demote by item attributes:[Boost and Demote by Item Attribute](https://docs.byteplus.com/docs/viking-aisearch/92198)

* Boost / demote by `publish_time` or `listing_time`: [Boost and Demote by Time Comparison](https://docs.byteplus.com/docs/viking-aisearch/Time-based_Boost_and_Demotion)
