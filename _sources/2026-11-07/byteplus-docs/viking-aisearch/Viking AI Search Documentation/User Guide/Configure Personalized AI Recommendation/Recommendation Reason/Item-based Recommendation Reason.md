---
title: "Item-based Recommendation Reason"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Item-based_Recommendation_Reason"
---

<span id="f3f5021b"></span>
# Overview

Personalized recommendations can feel like a black box to end users — they see "You May Like" but have no idea why a particular item showed up, and often swipe away without a second thought. Operations teams face a similar problem: tuning strategy usually means running broad A/B tests, with no easy way to see why a specific recommendation was shown (or wasn't clicked).

**Recommendation Reason** lets you configure a short (roughly 20\-character) reason template per recall channel — for example, "Similar to items you recently viewed" or "Recently popular Top 3" — which is returned synchronously in the Recommend / Predict API response. End users get an explanation they can understand at a glance, and operations teams can fine\-tune wording through the console instead of relying solely on A/B experiments. This article covers what the feature does, how to configure it, and the API response format.

<span id="3b76f9ac"></span>
## Scope

Recommendation Reason is configured per recommendation scenario. Before you start, make sure you have:


* Completed [Prerequisites and setup](https://docs.byteplus.com/docs/viking-aisearch/Configuration_Setup)

* Understand the recall channels currently used by the scene


<span id="74ace32f"></span>
## Terminology


|<div style="text-align: top"><br><strong>Term</strong></div><br> |<div style="text-align: top"><br><strong>Description</strong></div><br> |<div style="text-align: top"><br><strong>Example</strong></div><br> |
|---|---|---|
|<div style="text-align: top"><br>Recall channel</div><br> |<div style="text-align: top"><br>The path the recommendation system uses to surface candidate items</div><br> |<div style="text-align: top"><br>Hot item recall, multimodal recall, similar\-user\-interest recall (ItemCF), user profile recall, parent item recall, item cold start recall</div><br> |
|<div style="text-align: top"><br>Variable</div><br> |<div style="text-align: top"><br>A placeholder inserted into a reason template that the system substitutes with an actual value at request time</div><br> |<div style="text-align: top"><br><code>{{rank}}</code>, <code>{{category}}</code>, <code>{{item}}</code></div><br> |
|<div style="text-align: top"><br>Fallback reason</div><br> |<div style="text-align: top"><br>The generic text used when a recommendation doesn't match any configured template, or the matched template is empty</div><br> |<div style="text-align: top"><br>"Recommended for you"</div><br> |



---



<span id="8c0fb0cc"></span>
# Platform Configuration

The console automatically lists the configurable reason channels based on which recall channels your scenario uses:


* **Homepage recommendation**: hot item recall, multimodal recall, similar\-user\-interest recall, user profile recall, item cold start recall

* **Detail page / cart recommendation**: parent item recall, hot item recall, multimodal recall, similar\-user\-interest recall, user profile recall, item cold start recall


Newly created scenarios enable all applicable channels by default, using built\-in multi\-language templates (Chinese, English, Japanese, Korean, Hindi, etc.) that follow the application's language setting. 

**Existing scenarios do not enable this feature automatically — you need to turn it on manually.** 


|**Type of scenarios** |**Status** |
|---|---|
|Newly created |All applicable recall channels are enabled by default  |
|Historical scenarios |Not automatically activated. Manually enable feature. |


<span id="7470e84e"></span>
## Recall channels


|<div style="text-align: top"><br><strong>recall_channel</strong></div><br> |<div style="text-align: top"><br><strong>Channel</strong></div><br> |<div style="text-align: top"><br><strong>Default template (English)</strong></div><br> |<div style="text-align: top"><br><strong>Variables</strong></div><br> |
|---|---|---|---|
|<div style="text-align: top"><br><code>multimodal</code></div><br> |<div style="text-align: top"><br>Multimodal recall</div><br> |<div style="text-align: top"><br>Similar to items you've interacted with</div><br> |<div style="text-align: top"><br>—</div><br> |
|<div style="text-align: top"><br><code>user_profile</code></div><br> |<div style="text-align: top"><br>User profile recall</div><br> |<div style="text-align: top"><br>Matches your interest in {{category}}</div><br> |<div style="text-align: top"><br><code>category</code></div><br> |
|<div style="text-align: top"><br><code>item_cf</code></div><br> |<div style="text-align: top"><br>Similar\-user\-interest recall</div><br> |<div style="text-align: top"><br>Has a similar audience to {{item}}</div><br> |<div style="text-align: top"><br><code>item</code></div><br> |
|<div style="text-align: top"><br><code>hot_item</code></div><br> |<div style="text-align: top"><br>Hot item recall</div><br> |<div style="text-align: top"><br>Recently popular top {{rank}}</div><br> |<div style="text-align: top"><br><code>rank</code></div><br> |
|<div style="text-align: top"><br><code>item_similarity</code></div><br> |<div style="text-align: top"><br>Parent item recall</div><br> |<div style="text-align: top"><br>Similar to {{item}}</div><br> |<div style="text-align: top"><br><code>item</code></div><br> |
|<div style="text-align: top"><br><code>cold_start</code></div><br> |<div style="text-align: top"><br>Item cold start recall</div><br> |<div style="text-align: top"><br>Recently added</div><br> |<div style="text-align: top"><br>—</div><br> |
|<div style="text-align: top"><br>(fallback)</div><br> |<div style="text-align: top"><br>—</div><br> |<div style="text-align: top"><br>Recommended for you</div><br> |<div style="text-align: top"><br>—</div><br> |


<span id="52b4b2d3"></span>
## Configuration steps


1. In the console, go to **Experience center \> Recommendation**, select the target scenario, and open the **Recommendation strategy** tab.

2. Under the **Recommendation Reason** group on the left, expand **Single\-item recommendation reason** and click **Add reason**.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a3c4736d1e3f4e179d154ea37fd8a18c) </span>


3. The panel lists the recall channels supported by this scenario, each with its own toggle: 

* All channels are on by default, pre\-filled with the built\-in template text.

* Click **Use template** below the text box to restore the default wording at any time.

* To customize, edit the text directly. 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/81a29afb26c74c7c9ade0ec602922052) </span>


&nbsp;

4. Click the buttons under **Variables** to insert a placeholder: 

   1. `+{{rank}}`: automatically pulls the recommended item's popularity rank

   2. `+{{category}}`: automatically pulls the recommended item's category

   3. `+{{item}}`: after inserting, click the variable to choose a specific item field from the dropdown (e.g., `title`, `genre`); it resolves to `item.{field name}`. You can insert multiple variables in one template.

   4. Note: 


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default"><code>array<object></code> fields and their nested fields are not selectable. Array\-type field values are rendered as a comma\-separated list.</div>



&nbsp;

5. To hide the reason for a specific recall channel, turn off its toggle and that channel will no longer appear in `rec_info`. 

   If a template is left blank while the toggle stays on, the channel still appears in `rec_info`, but with an empty `reason` string.

6. Click **Confirm** to save. Changes apply to the console first — test them in the preview panel in the middle of the page.


&nbsp;

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e12fbdb988c84635a286560ecbeac53e" width="673px" /></div>



&nbsp;

7. Once verified, click **Update configuration** in the top\-right corner to publish the changes to production so they take effect on live API requests.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip!</div>


<div data-tips="true" data-tips-type="default">Hover over a variable button to see where its value comes from (for example, the item variable is described as "automatically pulls a field from the recommended item").</div>


<div data-tips="true" data-tips-type="default">Templates are independent per channel. If the same item is surfaced by multiple recall channels, <code>rec_info</code> will contain multiple reason entries for it.</div>


 &nbsp;

<span id="fa9878a7"></span>
# API Request

&nbsp;

<span id="15f71c15"></span>
## API Response

Once enabled, the [Recommend](https://docs.byteplus.com/docs/viking-aisearch/Recommendation) response includes a new `rec_info` field for each recommended item — no extra API call required, and no added latency.


|<div style="text-align: top"><br><strong>Parameter</strong></div><br> |<div style="text-align: top"><br><strong>Type</strong></div><br> |<div style="text-align: top"><br><strong>Description</strong></div><br> |
|---|---|---|
|<div style="text-align: top"><br><code>rec_info</code></div><br> |<div style="text-align: top"><br><code>Array<Object></code></div><br> |<div style="text-align: top"><br>List of recommendation reasons</div><br> |
|<div style="text-align: top"><br><code>rec_info.recall_channel</code></div><br> |<div style="text-align: top"><br><code>string</code></div><br> |<div style="text-align: top"><br>The recall channel that matched</div><br> |
|<div style="text-align: top"><br><code>rec_info.reason</code></div><br> |<div style="text-align: top"><br><code>string</code></div><br> |<div style="text-align: top"><br>The generated reason text for that channel</div><br> |


<span id="8ede5d14"></span>
### Sample Response

```JSON
{
  "result": {
    "rec_results": [
      {
        "_id": "688932914577129760",
        "display_fields": {
          "item_id": "item_1004"
        },
        "rec_info": [
          { "recall_channel": "hot_item", "reason": "Recently popular Top 3" },
          { "recall_channel": "item_cf", "reason": "Has a similar audience to Limited Edition Sneakers" }
        ]
      }
    ]
  }
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For the full field reference, see <a href="https://docs.byteplus.com/docs/viking-aisearch/Recommendation">Recommend</a>.</div>


&nbsp;

<span id="d45b7937"></span>
## Billing and performance


* This capability is **not separately billed**.

* It has **no significant impact** on Recommendation API endpoint latency.



---



<span id="1ce7ea56"></span>
# FAQ

**Q: Why doesn't a recommendation include ** **`rec_info`** **, or why is ** **`reason`** ** an empty string?**  

A: Check whether the channel's toggle is off (no entry is returned in that case), whether its template is blank (an empty string is returned), or whether this is an existing scenario where Recommendation Reason hasn't been manually enabled yet.

**Q: How long does it take for template changes to go live?**  

A: Edits apply immediately in the console preview, but live API requests only return the new text after you click **Update configuration** to publish.

**Q: What languages are supported?**  

A: Default templates ship in Chinese, English, Japanese, Korean, and Hindi, and follow the application's language setting automatically. You can also edit them directly to use your own wording.
