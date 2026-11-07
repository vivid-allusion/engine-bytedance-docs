---
title: "Recommendation Overview"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Feature_Overview"
---

Personalized recommendation services use user behavior data to provide accurate item suggestions, aiming to increase user engagement and conversion rates. This feature is widely applied in business scenarios such as "You May Like" on e\-commerce homepages and "Related Recommendations" on content detail pages. This article guides you through the initialization and use of personalized recommendation services.

<span id="r7DekaWdHQ"></span>
# Prerequisites

Before configuring, you must complete the necessary prerequisites to ensure the **user event dataset** is linked and active. Without linking the user event dataset, creating recommendation scenarios is restricted. To learn how to link and activate the user event dataset, please refer to [Prerequisites and setup](https://docs.byteplus.com/docs/viking-aisearch/Configuration_Setup).


---



<span id="G4Bt2PrBs4"></span>
# Create Recommendation Scenario


1. Navigate to the ** Experience center** \> **Recommendation** module.

2. **If no scenarios existing were found: ** Click on **Create recommendation configuration** to create a new scenario. 


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">The platform will automatically create two recommendation configurations after the first user event dataset has been initialized. Feel free to click on <strong>create configuration</strong> to add more recommendation configurations</div>


&nbsp;


<columns>
<columnsItem zoneid="eaQDz7i0gh">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0831be270ce4490ca75e258f63c160e1" width="700px" /></div>




</columnsItem>
<columnsItem zoneid="yYknF4qdwf">

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/feb2de065be04c4cb67f9f7f5793de5e) </span>



</columnsItem>
</columns>



3. Configure basic information



|**Configuration** |**Description** |
|---|---|
|Configuration name |Customize the recommended scenario name (up to 50 characters, we recommend including business scenario keywords for easier management).<br><br>**Preconfigured for auto\-created scenarios.**  |
|Recommendation scene |Select recommendation scene type<br><br><br>1. Recommended for you: Recommendation based on user profile. <br><br>2. Related items: Recommendation based on item relevance and user profile. <br><br><br>**Preconfigured for auto\-created scenarios.**  |
|Recommendation scene name |**Identify the "Interaction Interface" for this scenario:** <br><br>This setting drives the **automatic exposure data extraction task**, which tracks which items a user has already seen. Ensure that this configuration is accurate. <br><br>For more information, refer to [Exposure Deduplication](https://docs.byteplus.com/docs/viking-aisearch/Remove_items_exposed_to_users).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Not seeing any options?</div><br><br><br><div data-tips="true" data-tips-type="default">Selections are automatically extracted from the field tagged with the <code>scene name</code> attribute in the user event dataset. Ensure this field is accurately populated in the user event data. </div><br> |
|Item dataset for recommendation |**Source item dataset for recommendations**<br><br>Link a specific item dataset to this scenario to define the pool of items available for recommendation. In the "Item Dataset" dropdown menu, select an **already active** item dataset. |



4. After creating the recommendation scenario, you should be automatically redirected to the recommendation experience page.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/12fd9cdc363246fca82bfe0e73a4e2d6) </span>

&nbsp;


---



<span id="383c999b"></span>
# Experience Centre

<span id="c852d79f"></span>
## Interface

**The interface consists of two main parts:** 


* Left: Recall and Business Strategy, and Recommendation Reason

* Middle: Recommendation results and inputs


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5d273ce9047b4638a5fbe57de09eb46b) </span>

<span id="b7737829"></span>
## Recall and Business Strategy

<span id="58652e52"></span>
### Scope


|**Feature** | ** Description** |**Learn more** |
|---|---|---|
|Related user event scenes |**Identify the "Interaction Interface" for this scenario.** <br><br>This setting drives the **automatic exposure data extraction task**, which tracks which items a user has already seen. Ensure that this configuration is accurate. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Missing options?</div><br><br><br><div data-tips="true" data-tips-type="default">Selections are automatically extracted from the field tagged with the <code>scene name</code> attribute in the user event dataset. Ensure this field is accurately populated in the user event data. </div><br> |* [Exposure Deduplication](https://docs.byteplus.com/docs/viking-aisearch/Remove_items_exposed_to_users) |
|Recommendable items |Configure item **filter rules** to ensure returned items meet business requirements.  |* [Configure Static Filter Rules](https://docs.byteplus.com/docs/viking-aisearch/Static_Recommendation_Scope_Configuration)<br><br>* [Configure Dynamic Filter Conditions](https://docs.byteplus.com/docs/viking-aisearch/Dynamic_recommendation_scope_configuration) |
|Fallback strategy |Configure fallback strategy that is to be used on users **without any user profile**. The platform automatically calculates hot items based on user interactions to serve new users (Cold Start). |* [Popular Items Recall (Cold start & Fallback)](https://docs.byteplus.com/docs/viking-aisearch/Recommended_Fallback_Strategy) |
|Recommendation rationale statements |[Does not affect API return]<br><br>Role settings for personalized recommendation reasons (such as friendly shopper, professional analyst, etc.) | |


<span id="41c504f2"></span>
### Result limits


|**Feature** | ** Description** |**Learn more** |
|---|---|---|
|Maximum number of results |**Upper limit** for the number of recommended items returned each time.<br><br><br>* Default: 10 items<br><br>* Maximum: 400 items | |


<span id="c8f166e9"></span>
### Recall


|**Feature** | ** Description** |**Learn more** |
|---|---|---|
|Item cold start recall |**Item cold start recall** provides a dedicated recall channel for new items, ensuring they receive baseline exposure and can accumulate user event data to transition into mature items. |[Configure Item Cold Start Recall](https://docs.byteplus.com/docs/viking-aisearch/Configure_Item_Cold_Start_Recall) |
|Recall merge strategy |**Configure fusion weights across multiple recall channels. ** <br><br>Decide how much each channel contributes to the final result, so you can fine\-tune the recommendation balance for different business scenarios. |[Configure and Adjust Recall Merge Strategy](https://docs.byteplus.com/docs/viking-aisearch/Configure_and_Adjust_Recall_Merge_Strategy) |


&nbsp;

<span id="b4facf1b"></span>
### Sorting


|**Feature** | ** Description** |**Learn more** |
|---|---|---|
|Boost and demotion |Adjust the weight of certain items in recommendations through boosting and demotion rules to achieve business\-driven ranking results. |* [Boost and Demote by Item Attribute](https://docs.byteplus.com/docs/viking-aisearch/Item_Attribute_Boost_and_Demotion)<br><br>* [Boost and Demote by User Geo-location](https://docs.byteplus.com/docs/viking-aisearch/User_geographic_location-based_ranking_boost_and_demotion)<br><br>* [Boost and Demote by Time Comparison](https://docs.byteplus.com/docs/viking-aisearch/Time-based_Boost_and_Demotion) |
|Deduplication rules |Automatically remove items that have already been displayed when personalized recommendations retrieve the same items. |* [Exposure Deduplication](https://docs.byteplus.com/docs/viking-aisearch/Remove_items_exposed_to_users) |
|Diversity rules |Control the distribution density of similar items in recommendations using diversity rules to avoid excessive homogenization, enhancing result richness and user browsing experience. |* [Configure Diversity Rules](https://docs.byteplus.com/docs/viking-aisearch/Diversity_rule_configuration) |
|Pin items |Force specific items to be displayed in the corresponding position within the final returned items according to the pinned items list configuration. |* [Pinned Recommendation](https://docs.byteplus.com/docs/viking-aisearch/Pinned_Recommended_Items) |


&nbsp;

<span id="c91d52d4"></span>
## Recommendation Reason


|**Feature** | ** Description** |**Learn more** |
|---|---|---|
|Item\-based recommendation reason |Configure a short reason template per recall channel to explain why each item was recommended. The text is returned synchronously in the Recommend API response.<br><br>Newly created scenarios enable all applicable channels by default with built\-in, multi\-language templates that follow the app language; existing scenarios do not enable this automatically and must be turned on manually. |* [Item-based Recommendation Reason](https://docs.byteplus.com/docs/viking-aisearch/118535) |
|Recommendation Assistant |***Does not affect API response***<br><br>Role settings for personalized recommendation reasons (such as friendly shopper, professional analyst, etc.) | |


&nbsp;

<span id="45868ea2"></span>
## Recommendation Results and Input


|**Feature** |**Feature description** |
|---|---|
|Recommended items |**Recommendation** ** result:**  Display recommended items and preview the recommendation effect |
|Recommendation reason |**Explainable recommendation:**  Use large language model (LLM) capabilities to infer recommendation reasons based on recommended items, user profiles, and role settings. |


&nbsp;

<span id="04620aad"></span>
## Recommendation Input


|**Feature** |**Feature description** |**Learn more** |
|---|---|---|
|Test user |* **Specified user**: Generate recommendations based on a custom user ID and profile<br><br>* **Random user**: The system randomly selects a user ID by default and generates recommendations based on that profile for quick recall testing |* [Configure test users](https://docs.byteplus.com/docs/viking-aisearch/Recommended_Input#fb2bca40) |
|Test item |This feature is only available in **related item scenarios.** <br><br><br>* **Specified item**: Generate related recommendations based on a custom item ID<br><br>* **Random item**: The system randomly selects an item ID by default and generates related recommendations for quick recall testing |* [Configure test items](https://docs.byteplus.com/docs/viking-aisearch/Recommended_Input#8e0a7bde) |
|Configure user location |Only visible when the "Distance between user and item" boosting and demotion conditions are configured.<br><br><br>* **Specify user location**: Manually enter latitude and longitude coordinates (e.g., `Longitude: 39.9°`, `Latitude: 116.4°`)<br><br>* **Get my location:**  Obtain your current location to simulate user testing. This requires granting location permissions in your browser.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">If you click on "Obtain my location" and the platform is unable to <strong>automatically obtain </strong><strong>your </strong><strong>latitude and longitude</strong>, please check:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="warning">Whether the computer’s location service is enabled</div><br><br><br>2. <div data-tips="true" data-tips-type="warning">Whether the computer or browser restricts browser location access permissions</div><br><br><br><br><div data-tips="true" data-tips-type="warning">If you previously denied location access for your browser, you may need to reset this permission in your browser's settings.</div><br> |* [Experience location rules](https://docs.byteplus.com/docs/viking-aisearch/User_geographic_location-based_ranking_boost_and_demotion#b8ff614f) |


&nbsp;


---



<span id="cf121540"></span>
## Mapping Business Requirements to Features

The product supports multiple business configurations, allowing you to configure business logic, including recommendation limit, duplicate item removal, filter configuration, and popular item calculation logic.


|**Business requirements** |**Related features** |**Learn more** |
|---|---|---|
|Set the number of items returned per request |1. Configure recommendation scenarios and set maximum number of results<br><br>2. Customize the `page_size` parameter through API requests |* [Recommend](https://docs.byteplus.com/docs/viking-aisearch/Recommendation) |
|Ensure that repeated user requests do not return the same items |Configure rules to remove duplicate recommended items |* [Exposure Deduplication](https://docs.byteplus.com/docs/viking-aisearch/Remove_items_exposed_to_users) |
|Ensure recommended items meet business requirements |Configure "**static**" or "**dynamic**" recommendation **scope** rules based on business needs |* [Configure Static Filter Rules](https://docs.byteplus.com/docs/viking-aisearch/Static_Recommendation_Scope_Configuration)<br><br>* [Configure Dynamic Filter Conditions](https://docs.byteplus.com/docs/viking-aisearch/Dynamic_recommendation_scope_configuration) |
|Different user requests have different filtering conditions |Configure **dynamic** recommendation scope rules according to business requirements |* [Configure Dynamic Filter Conditions](https://docs.byteplus.com/docs/viking-aisearch/Dynamic_recommendation_scope_configuration) |
|Different user requests have different weighting conditions |Configure **dynamic** boosting and demoting rules according to business requirements |* [Boost and Bury via API (V2)](https://docs.byteplus.com/docs/viking-aisearch/Recommendation_API_uplift_and_demotion_rule_configuration) |
|New users and cold start users handling logic |Display popular items as fallback |* [Popular Items Recall (Cold start & Fallback)](https://docs.byteplus.com/docs/viking-aisearch/Recommended_Fallback_Strategy) |
|Handling logic for personalized recommendation exceptions |||


<span id="Uu1Erfdhhc"></span>
##
