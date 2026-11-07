---
title: "Common Recommendation Issues"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Personalized_recommendation_scenarios"
---

*To experience more Viking AI Search capabilities, go to: * [Viking AI Search, an all-in-one intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)


---



To resolve common issues with your recommendation system, such as empty results or poor personalization performance, you can use this troubleshooting guide. It provides diagnostic logic and specific procedures to help you quickly identify the root cause and improve the effectiveness and stability of your recommendations.

This article helps you understand troubleshooting methods and specific procedures for common problems, thereby improving the effectiveness and stability of the recommendation system.

<span id="b613850f"></span>
# Recommendation scenarios

<span id="f5f40dfb"></span>
## Empty recommendation results

> For more details, refer to: [Why does the recommendation return no items?](https://www.volcengine.com/docs/85296/2124616?lang=zh#bd9b3c9f)


You can also follow the process below to troubleshoot.


|**Element** |**Troubleshooting recommendations** |
|---|---|
|User event data quality<br><br> |1. **Item ID**: Can be found in the item table<br><br>2. **User event time**: Within 7 days (events older than 7 days can also be sent, but events within the last 7 days are required).<br><br>3. **Event type**: Both exposure and non\-exposure positive user events (such as Click, Favorite, and Purchase) are required.<br><br>4. **Number of user events**: As many as possible, with a minimum of 1,000. |
|Recommendation Filters <br><br> |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7ef54ce061374780935070d34c02f1b5" width="863px" /></div><br><br><br>The main issue is that no items meet all of the above conditions. Let's break down the possible reasons:<br><br><br>* The OR logic was incorrectly configured as AND.<br><br>* A field in the item table has a data transfer issue, and the actual value does not match the defined format.<br><br>* No item meets all the conditions. |
|Remove duplicate recommendations<br><br> |Filtered out by exposure and delivery deduplication<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/50bfc646e1b348d3bad3db3994a50cb0" width="556px" /></div><br><br><br> |
|Fallback strategy |Reasonableness of the fallback strategy<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/535f9cbf5f294995bb63b06d87184f22" width="515px" /></div><br><br><br> |
|Item data quality |1. Item's tag field must have a value. The field designated for tags is inferred by the BytePlus model. If you have a more suitable field, you can contact BytePlus to request a change.<br><br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/29d5519957124463923e6db571e62cd0" width="1716px" /></div><br><br><br> |


<span id="5fafdef4"></span>
### Slow recommendations

Recommendations may be slow if a timeout occurs when requesting item attribute information during item retrieval. This can happen if an attribute value is very large.

Check the item table for fields with very large values, such as the following:


|**Element** |**Troubleshooting recommendations** |
|---|---|
|Multi\-modal reranking<br><br> |Is the number of items for multi\-modal reranking too large? A configuration of 20 is recommended.<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/802c8ba60f5a446e9b8d0631917c79cd" width="382px" /></div><br><br><br> |
|Are there large fields used for document search? |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/072cb048f99f4581ac5c21cbed9724fa" width="741px" /></div><br> |


<span id="563c8de5"></span>
### Empty user profile in recommendation scenarios

> Similar issue: test user interest tags are empty


The calculation logic for user profile tags is as follows:


1. It counts the item IDs from a user's positive behavior within the last 7 days and uses them to query the corresponding user interest tags field in the item table.

2. The user interest tags field is a field intelligently selected by the platform's large model after analyzing the item dataset.


&nbsp;

**Suggestion:** 


1. Check if the user has any positive behavior within the last 7 days.

2. Check if the item from the positive behavior can be found in the item table.

3. If both of the above is normal, contact BytePlus technical support to check if the intelligently selected item field is appropriate. If not, adjust it manually.


<span id="579c51b8"></span>
### Recommendation results are not personalized enough

> Description:

> The expected recommendation behavior is: if a user clicks or plays an item of a certain type, they should later be recommended items of the same type.

> If the recommendation content does not meet expectations, there may be an issue with the configuration.


&nbsp;

Currently, three item retrieval paths return personalized items, as shown in the table below. To achieve strong personalized recommendation results, you need to optimize the data quality according to the logic of each item retrieval path. **In particular, optimize user interest item retrieval and large model item retrieval**.


|Item retrieval channel |Item retrieval logic |Customer\-side optimizations |
|---|---|---|
|User interest item retrieval<br><br> |1. Calculate trending items under each tag based on all user event data.<br><br>2. Get the list of tags for items associated with a user's positive behavior in the last 7 days, then retrieve trending items for each tag in the list.<br><br><br>&nbsp;<br><br>**Note: The tags here are from a field that the platform's large model automatically selects after analyzing the item table fields. Customers can infer which field the tags come from by viewing the tag values displayed below.** <br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2ac2948f039c4727b149d9c451e2b91c" width="557px" /></div><br><br><br> |1. User event data<br><br>   1. Large data volume<br><br>   2. Includes Exposure and Positive behavior (e.g., Click, Purchase, Play, etc.)<br><br>   3. Items must exist in the item data.<br><br>2. Item data<br><br>   1. Criteria for evaluating the interest dimension field automatically selected by BytePlus<br><br>      1. The field value aligns with your business logic for user interest dimensions. For example, commonly selected fields include product category and information tags.<br><br>      2. The field has high coverage, meaning that most items have a value for this field.<br><br>      3. The field's enumerated values should be distinct (avoid having most or even all items share a single tag value) and not too sparse (avoid having a large number of values where most correspond to very few items).<br><br>   2. If there is a more suitable tag field, contact BytePlus technical support to make an adjustment.<br><br><br>&nbsp;<br><br>&nbsp;<br><br> |
|Large model item retrieval<br><br> |1. Creates an embedding for each item based on the information in the fields selected as Searchable (Text)<br><br>2. Retrieves a list of items with which the user has had positive behavior in the last 7 days, creates embeddings for these items, and then performs a vector search for similar items |1. Item data fields for Document search<br><br>   1. Select fields that contain core information, such as Title and categories<br><br>   2. Do not select fields with non\-core information to prevent miscellaneous data from diluting the core information and causing irrelevant items to be retrieved |
|ItemCF item retrieval<br><br> |1. Calculates item\-to\-item similarity based on the full user event data<br><br>2. Retrieves a list of items from the user's positive behaviors over the last 7 days. For each item on the list, it then retrieves other highly similar items.<br><br><br> |1. User event data<br><br>   1. Large data volume<br><br>   2. Includes Exposure and positive behavior (e.g., Click, Purchase, Play, etc.) |


<span id="6ec6f226"></span>
### Similar items for parent items are not available on detail pages


|Checklist item |Troubleshooting logic |
|---|---|
|API parameter passing |Check: whether the parameter format is correct. Correct parameter passing is as follows:<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/160c8c2850794c92aecbb947a80f0681" width="703px" /></div><br><br><br> |
|Parent item |Check: the parent item ID must exist in the item dataset. |


<span id="4ddc2087"></span>
### The recommendation returns duplicate items


|Troubleshooting module |Troubleshooting logic |
|---|---|
|Remove duplicate recommendations |If the deduplication configuration is too small, only a few recently recommended items are filtered out with each new recommendation, which can cause previously recommended items to be recommended again.<br><br>(The maximum time window for exposure deduplication is 7 days)<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/66ee23b6db25445cb3f35b65097e90d3" width="594px" /></div><br><br><br> |
|User event data timeliness |Check whether exposure user event data is synchronized to the BytePlus platform in **real time**.<br><br>If latency is high, Exposed Item Deduplication cannot retrieve exposed items, causing the process to fail (Suggestion: Improve the timeliness of user event data and add Delivered Item Deduplication). |


&nbsp;

<span id="568c2fc9"></span>
### Diversification is not taking effect


|Troubleshooting items |Troubleshooting logic and recommendations |
|---|---|
|**Confirm that diversification has not taken effect.**  |1. Place the diversification field in output_fields and use the information returned by the API to verify if diversification is not applied.<br><br>2. On the product interface, it may seem that diversification is not working even when it is effective. This is mainly caused by the cross\-batch logic. The detailed logic is as follows:<br><br>   1. The current effective scope for diversification is within each batch. For example, if one batch returns 5 items, and the configured diversification logic is<br><br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d236c43ce2da430c9989cdd8e3ec3ed8" width="577px" /></div><br><br><br><br>   2. then within each batch, the condition of displaying at most 1 item of the same type for every 4 items can be met. However, the last Item of the first batch and the first Item of the second batch might be of the same dimension. This leads to a concentration of similar items when browsing the application, which is an expected behavior according to the functional logic.<br><br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/deb0252c51d747dbaa312924db4312b7" width="845px" /></div><br><br><br> |
|**The diversification level is too high**<br><br> |If the content is too diversified, for example, by not allowing the same dimension to appear over a long consecutive sequence, diversification may fail because the items from Item retrieval do not have enough variety.<br><br>Furthermore, in personalized recommendation practice, each user has specific preferences for certain dimensions. For example, a user might recently want to buy a certain style of down jacket, or another user might like the works of a specific author. In such cases, the recommendation system will return more items of this type to the user.<br><br>Finally, because diversification is only effective within a single batch, if one batch returns 10 items and diversification is configured to display at most N items within any 20 consecutive items, it will also likely lead to unexpected results.<br><br>Suggestion:<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4e2eb65f2026426ebcd240f5c9c2da9e" width="577px" /></div><br><br><br> |
|Is the diversification field appropriate |1. Nested fields cannot be used for unwinding.<br><br>2. If a field has a null value or no unwind field, it is treated as a single dimension. Therefore, if the unwind field contains many null values, it increases the probability of unwinding failure. |


<span id="99fdc343"></span>
### The recommendation filter is not taking effect

A dynamic filter requires both platform configuration and parameters passed via the API to take effect. If either is missing, the filter will not work, and the missing component will be indicated in the `omitted_params` field of the API response.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ca88da796488424ab990f27330a14279" width="1021px" /></div>


You can use the table below to investigate the possible reasons in order:


|Cause classification |Troubleshooting logic and recommendations |
|---|---|
|Passed in the API call, but not configured in the filter policy.<br><br> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/590f5de277e94921abf3790c368871f8) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/79e2d5c87ad94ef68a723e501dbdeeb5) </span><br><br>&nbsp;<br><br> |
|A dynamic filter is configured in the filter policy, but not passed in the API parameters. |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7e85343fb22b43b698519c863ce9571d) </span><br><br> |
|Invalid dynamic filter parameters |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0d6f429fd1c041d6a580c6a71dcd3aa0" width="822px" /></div><br><br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fb9ab25a3430454d8f774c5b4fd8a8aa" width="842px" /></div><br><br><br> |
|Logical condition check |In a filter expression, the `not found in` condition is met only if the field's value does not match any of the elements in the provided list.<br><br>If you want to filter based on matching any single element, use multiple expressions.<br><br> |
|Others<br><br>Incorrect logical condition |Check if the configured logic is OR<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1eb225a0b52444b08269d54e387ffd81" width="853px" /></div><br><br><br> |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To learn more about the capabilities of Viking AI Search, see <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, the integrated intelligent engine for enterprise Search, Recommendation, and Q&A</a>.</div>
