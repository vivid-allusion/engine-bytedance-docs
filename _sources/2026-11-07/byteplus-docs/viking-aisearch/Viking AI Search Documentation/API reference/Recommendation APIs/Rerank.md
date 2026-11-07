---
title: "Rerank"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Rerank"
---

<span id="f78b3cf0"></span>
## Overview

A standalone ranking endpoint that scores and re\-orders a caller\-supplied candidate list using the platform's rerank model. Use it when you want the platform to act as a pure ranking service on top of your own retrieval pipeline.

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Availability</div>


<div data-tips="true" data-tips-type="default">This is a <strong>white\-list capability</strong> and is not enabled by default. To request access, contact BytePlus technical support or your account manager. If you want to pass recall items directly into a recommendation request instead, see <a href="https://docs.byteplus.com/docs/viking-aisearch/Recommendation#3b41d1cd">InputItems</a>.</div>


&nbsp;

<span id="c13c1889"></span>
## When to Use

Choose the Rerank API when any of the following applies:


* You maintain your own recall candidate pool and only need the platform's rerank model for final ordering.

* You want to consume the platform as a **pure ranking service**, decoupled from recall and filtering.

* You need personalized ranking scores for a **specific, bounded set of items** (for example, a curated shortlist or A/B test cohort).


&nbsp;

**Rerank API vs. Recommendation API**

The Recommendation API runs the full **recall → ranking → rerank ** pipeline. The Rerank API runs ranking only against the candidate list you supply — no recall, no filtering, no deduplication.

&nbsp;


---



<span id="fbf82606"></span>
## API information


* Request Method: POST

* Request URL:



|**Service** |**Region** |**URL** |
|---|---|---|
|BytePlus |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.bytepluses.com/api/v1/application/{application_id}/{scene_id}/rerank` |
|Volcano Engine |North China (Beijing) |`https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/{scene_id}/rerank` |
|Volcano Engine |Asia\-Pacific (Johor) |`https://aisearch.ap-southeast-1.volces.com/api/v1/application/{application_id}/{scene_id}/rerank` |


<span id="cf1375bc"></span>
### **Path parameters**


|**Parameters** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`application_id` |String |Yes |Application ID |
|`scene_id` |String |Yes |The unique identifier for a recommendation scene, assigned by the system after creation. |


<span id="40042cc3"></span>
## Request parameter


|**Parameters** |**Type** |**Required** |**Default value** |**Description** |
|---|---|---|---|---|
|`items` |Object |Yes |— |Wrapper for the candidate list. |
|`items.items` |Array<Object\> |Yes |— |Candidate items. **Maximum 400 per request.**  |
|`items.items._id` |String<br><br> |Yes |— |Item ID. Must exist in the system's forward index. |
|`user` |Object |Yes |— |User context used for personalized ranking. |
|`user._user_id` |String |Yes |— |User ID |
|`page_size` |Int |No | |Number of items to return. If omitted, all scored items are returned. |
|`output_fields` |Array<String\> |No<br><br> |All fields |Item fields to include in the response (for example, `item_id`, `title`, `category`). |
|`strategy_switch` |Object |No |— |Optional ranking strategy toggles. |
|`strategy_switch.enable_boost_bury_rule` |Boolean |No |`false` |When `true`, the returned score incorporates boost and bury rule effects. |
|`strategy_switch.enable_diversity_rule` |Boolean |No |`false` |When `true`, applies the diversity (scattering) rule to the final order. |
|`strategy_switch.enable_force_recommend` |Boolean |No |`true` |When `true`, applies the pinned items rule to the final list of returned items. |
|`session_id` |String |No |— |**A unique identifier for a user session.** <br><br>Use a custom and unique value for each session, such as a UUID.<br><br>> Learn more: [Pinned Recommendation](https://docs.byteplus.com/docs/viking-aisearch/Pinned_Recommended_Items)<br><br><br>When pinned items are configured for a recommendation scene and 'Repeat recommendations on each refresh' is disabled, the platform uses the session_id to check if the pinned configuration has been applied to a visit within **24 hours**.<br><br><br>* If this parameter is not provided, repeated pinning will occur for the **same visit within 24 hours**. |


<span id="c46068ea"></span>
### Constraints


* A single request accepts at most **400 items**. For larger candidate pools, batch the calls and merge the results client\-side.

* Items whose `_id` is not found in the forward index are **silently dropped** from the response — no error is raised.


&nbsp;

<span id="f6e59aa0"></span>
## Response parameter


|**Field** |**Type** |**Description** |
|---|---|---|
|`request_id` |String |Unique request identifier. Include this when reporting issues. |
|`results` |Object |Ranking result wrapper. |
|`results.rec_results` |Array<Object\> |Ranked items, sorted by `score` in descending order. |
|`results.rec_results._id` |String |Item ID |
|`results.rec_results.display_fields` |Object |Item fields selected via `output_fields`. |
|`results.rec_results.score` |Float |Rerank score. Includes boost/bury effects when `enable_boost_bury_rule` is `true`. |
|`extra_info` |Object |**Additional information about request processing**<br><br>Use this to check the recommendation request processing logic, which helps you understand and troubleshoot the validity of your configuration and whether the processing logic meets business requirements. |
|`extra_info.forced_item_info`<br><br> |Object |**Pinned Item Processing Logic**<br><br>When the pinned item configuration is enabled for a recommendation scene, the parameter returns the pinned item ID and effective status, allowing you to check if it works as expected. |
|`extra_info.forced_item_info.item_ids` |Array<String\> |**Successfully pinned item IDs**<br><br>If an item ID is not in the item dataset, the platform automatically removes the item. |
|`extra_info.forced_item_info.skipped`<br><br> |Boolean<br><br> |**Pin status**<br><br><br>* true: The session_id has appeared within the last 24 hours, and the pin is inactive.<br><br>* false: The session_id has not appeared within the last 24 hours, and the pin is active. |



---



<span id="d6bbbb03"></span>
## Example

<span id="d88bbc83"></span>
### Request

```JSON
curl -X POST 'https://aisearch.ap-southeast-1.volces.com/api/v1/application/\${application_id}/\${scene_id}/rerank' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "items": {
        "items": [
            {"_id": "KJ3873"},
            {"_id": "KU8746"},
            {"_id": "LF8635"},
            {"_id": "LF8632"},
            {"_id": "LF8618"},
            {"_id": "LF8613"}
        ]
    },
    "user": {
        "_user_id": "user_001"
    },
    "page_size": 10,
    "output_fields": ["item_id", "title", "category"],
    "strategy_switch": {
        "enable_boost_bury_rule": true,
        "enable_diversity_rule": false,
        "enable_force_recommend": true
    }
}
```


<span id="b09053f4"></span>
### Response

```JSON
{
    "request_id": "25ee998a-5462-9385-9f18-035f1da7a6e5",
    "results": {
        "rec_results": [
            {
                "_id": "688932914577129760",
                "display_fields": {
                    "item_count": "1234",
                    "update_time": 1752238692193,
                    "item_id": "item_1004"
                },
                "score": 0.877
            }
        ]
    },
        "extra_info": {
                    "forced_item_info": {
                        "item_ids": ["60493","52937"],
                        "skipped": false
                    }        
         }
     }
}
```


<span id="2d71c30d"></span>
### Notes


* **No deduplication.**  The Rerank API does **not** participate in exposure deduplication or delivery deduplication. Returned items are **not** written to the delivery dedup table — you are responsible for any client\-side dedup logic.

* **No filtering.**  Filtering rules configured for the recommendation pipeline are **not** applied here.

* **Score semantics.**  With `enable_boost_bury_rule = false`, the score reflects the rerank model only. With `enable_boost_bury_rule = true`, the score is the combined output of the rerank model and the boost/bury rules.



---



<span id="bb8eb124"></span>
## Errors

This endpoint uses the platform's standard error code set. See [Common Error Codes](https://docs.byteplus.com/docs/viking-aisearch/Common_Error_Codes)for the full reference, including authentication, quota, and validation errors.

&nbsp;

<span id="3c9d586e"></span>
## Frequently asked questions (FAQ)

**Q: How many items can a single request contain?** 

A: Up to 400. For larger pools, call the endpoint in batches and merge results client\-side.

&nbsp;

**Q: What happens if I pass an unknown item ID?** 

A: The item is silently omitted from `rec_results`. No error is returned, so verify counts on the caller's side if completeness matters.

&nbsp;

**Q: Does Rerank trigger exposure or delivery deduplication?** 

A: No. The Rerank API is outside the dedup pipeline and does not update the delivery dedup table.

&nbsp;

**Q: How does ** **`enable_boost_bury_rule`** ** change the score?** 

A: When enabled, the returned `score` is the composite of the rerank model output and the configured boost/bury rules, rather than the raw model score.

&nbsp;

**Q: How is Rerank different from the Recommendation API?** 

A: The Recommendation API runs the full **recall → ranking → rerank** pipeline against the platform's candidate pool. The Rerank API runs **ranking only** against the candidate list you provide; recall and filtering are your responsibility.
