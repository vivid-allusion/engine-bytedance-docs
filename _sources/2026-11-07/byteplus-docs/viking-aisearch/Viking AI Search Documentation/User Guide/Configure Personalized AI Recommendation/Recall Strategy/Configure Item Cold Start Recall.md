---
title: "Configure Item Cold Start Recall"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configure_Item_Cold_Start_Recall"
---

<span id="32a6f907"></span>
## Overview

Item cold start recall addresses a fundamental challenge in recommendation systems: Newly uploaded items lack user interaction history (such as clicks, purchases, or views), making them invisible to recommendation models. 

This results in:


* New items being unable to enter standard recall channels

* Reduced content freshness in recommendation results

* Slower item turnover affecting business growth


&nbsp;

By enabling **Item Cold Start Recall**, the platform provides a dedicated recall channel for new items, ensuring they receive baseline exposure and can accumulate user event data to transition into mature items.

<span id="9504dbb7"></span>
## How It Works

The Item Cold Start Recall operates within the recommendation pipeline as follows:


1. **New Item Pool Definition**: You define criteria to identify which items qualify as "new items" (e.g., items imported within the last 24 hours).

2. **Dedicated Recall Channel**: New items matching the criteria are recalled through a separate channel, bypassing the requirement for historical behavior data.

3. **Ranking Bypass**: Cold start items skip the fine\-ranking stage and are directly merged at the re\-ranking stage, preventing score suppression due to lack of interaction signals.

4. **Automatic Graduation**: Once a new item exceeds the configured exposure threshold, it automatically exits the new item pool and enters standard recall channels.


<span id="958c7315"></span>
## Use Cases

**Content Platforms**

For platforms with high daily content uploads (short videos, user\-generated content, community posts), cold start ensures new creator content gets initial visibility, avoiding the "Matthew Effect" where only established content receives exposure.

**E\-commerce**

For marketplaces with frequent product additions, cold start helps new products gain initial traction, supporting healthy inventory turnover and seller onboarding.

**Time\-sensitive Content**

For news, live streaming, or event\-based recommendations, cold start ensures the latest content is surfaced promptly.


---



<span id="9d24f88b"></span>
## Prerequisites

Before configuring Item Cold Start Recall, ensure the following:


* At least one item dataset is associated with your application.

* A recommendation scenario has been created.

* User event data is being uploaded (Real\-time upload is recommended for optimal results).



---



<span id="55e57792"></span>
## Configuration

<span id="c637fc60"></span>
### Step 1: Accessing the Configuration


1. Navigate to your application in the console.

2. Select the target recommendation **Scene**.

3. In the left panel under **Recall**, locate **Item cold start recall**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f4fc8b1b6c684bad8123d69499773afe" width="390px" /></div>



4. Toggle the switch to **Enable**.


&nbsp;

<span id="b37e24cd"></span>
### Step 2: Define New Items

Configure which items qualify for the new item pool. 


1. Click **Edit** next to "Filter New Item Scope".

2. Configure the filter rule for new items. The platform currently supports two methods.


<span id="232b3c4a"></span>
#### Method 1: By Item Import Time

Define new items based on when they were first imported to the item dataset.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/06f7b19b888445fcb55b657477f023a3) </span>


|**Parameter** |**Description** |**Default** |**Minimum** |**Maximum (Recommended)**  |
|---|---|---|---|---|
|Time window |Items first imported within X hours are considered new |24 hours |1 hour |168 hours |


<span id="a156edbe"></span>
#### Method 2: By Item Fields

Define new items using custom filter conditions based on item dataset fields.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ad1f51d1963e44409dac8b25d8474b22) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Only fields marked as "filterable" in your item dataset schema can be selected as part of the filter conditions.</div>



|**Parameter** |**Description** |
|---|---|
|Field |Select a field from the item dataset. The field must be configured as filterable.  |
|Operator |Configure comparison operators.  |
|Value |Match value. |


<span id="28d45109"></span>
### Step 3: Configure Exposure Limit

The platform selects new items based on user preferences and profiles. When eligible new items exist, the system prioritizes recommending them up to the configured limit.


|**Parameter** |**Default** |**Supported Range** |**Description** |
|---|---|---|---|
|New Item Exposure Limit |100 |1 \- 1000 |If a new item exposure count exceeds the limit, the item exits the new item pool and enters standard recommendation channels.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">The platform will only compute exposure events that occurred in the past 7 days.</div><br> |
|New Items Per Request |1 |1 \- Maximum number of results |Controls the **maximum number of new items ** returned per recommendation request. <br><br>This value cannot exceed the scene's total return limit. |


<span id="99a53bce"></span>
### Step 4: API Parameter (Optional)

When calling the recommendation API, you can dynamically override the new item count per request. For more details on the Recommendation API, refer to [Recommend](https://docs.byteplus.com/docs/viking-aisearch/Recommendation)


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|new_items_size |Integer |**Maximum number of new items ** returned in this recommendation request. <br><br>This will override the configuration on the platform. |


<span id="38e8f387"></span>
## Best Practices


|**Scenario** |**Recommended Configuration** |
|---|---|
|High\-volume content platform <br><br>(e.g., short video, social feeds) |New item definition: Imported in the past 24 hours<br><br>Exposure Limit: 100\-500<br><br>New Items Limit: 1\-3 per request |
|E\-commerce with frequent product launches |New item definition: Imported in the past 48 hours<br><br>Exposure Limit: 200\-1000<br><br>New Items Limit: 1\-2 per request |
|News/real\-time content |New item definition: Imported in the past 12 hours<br><br>Exposure Limit: 50\-100<br><br>New Items Limit: 2\-5 per request |


<span id="fa31ca84"></span>
## FAQ

**Q: What happens if I disable Item Cold Start Recall?** 

A: New items will only be discoverable through standard recall channels that require some historical interaction data. Items with zero interactions may not appear in recommendations.

&nbsp;

**Q: Can I change the new item definition after enabling the feature?** 

A: Yes. You can modify the filter criteria at any time. Changes take effect on the next recommendation request.

&nbsp;

**Q: How does the exposure cap interact with multiple scenes?** 

A: The exposure cap is counted globally across all scenes. Once an item reaches the cap in any scene, it exits the new item pool for all scenes.

&nbsp;

**Q: Does the new item recommendation limit guarantee that many items will be returned?** 

A: No. The limit is an upper bound and fewer items may be returned. Below are some reasons for a lower than expected number of new items: 


* Insufficient items that fulfil the definition of new items and match user interest.

* Boost and bury rules or diversity rules negatively affect new item position.
