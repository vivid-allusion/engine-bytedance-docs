---
title: "Why does the recommendation return no items?"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/empty_recommendation"
---

This document applies to developers or administrators who encounter empty recommendation results when integrating or operating AI search engine recommendation services. The AI search engine's recommendation service tries to return items. Through multiple recall methods and fallback strategies, we aim to ensure each recommendation request returns personalized items. Typical use cases include product recommendations on e\-commerce websites and content feeds in news applications. However, in some scenarios, the recommendation system cannot return personalized content, resulting in empty returns in the recommendation interface and experience. Since the possible causes vary, you can follow the troubleshooting steps below to identify the issue:

<span id="16882d73"></span>
## No recommended items in all responses

If **every** recommendation interface request or recommendation experience refresh returns no items, it is likely your uploaded data does not meet expectations. Please check the following configurations:

<span id="bd9b3c9f"></span>
### Behavior data issues


|**Checkpoint** |**Issue** |**Impact** |**Solution** |
|---|---|---|---|
|Upload behavior data volume |Too low |Insufficient historical data, unable to build user profiles |Upload more historical behavior data, at least several thousand records. Actions other than exposure must exist.<br><br>**Data Volume:**  The more data, the better. At a minimum, the dataset should contain **at least 1,000 records** to allow the model to initialize and begin learning user preferences. |
|Matching rate of item IDs between item dataset and user behavior dataset |Low |Unable to obtain attributes of items interacted by users |Upload missing items.<br><br>**Item ID Validation:**  Every `item_id` in your behavior logs **must exist** in your Item Metadata table. If the ID cannot be found, the behavior is considered "orphaned" and will be ignored. |
|Action occurrence time |Earlier than within 7 days |Unable to extract profile |Upload user behavior data from within 7 days.<br><br>**Time Window (Last 7 Days):**  You must provide behavior data from within the **last 7 days**. While you can upload older historical data, the system strictly requires recent data (last 7 days) to power real\-time features like exposure de\-duplication. |
|Behavior type distribution |Only exposure behavior |Exposure is not a positive behavior and cannot extract user preferences |Upload more positive behaviors, such as clicks, views, and follows.<br><br>**Behavior Type Diversity:**  Your dataset must include both **Exposure (Impression)**  events and **Positive Interactions** (e.g., clicks, favorites, shares, or purchases). |


<span id="c9325032"></span>
### Scenario configuration issues


|**Checkpoint** |**Problem** |**Impact** |**Fix plan** |
|---|---|---|---|
|Filter conditions |Does not meet expectations |All recalled items are filtered out by the filter conditions |On the 'Strategy' page in the console, locate the 'Define Recommendable Items' setting and check to ensure that some items meet the filter criteria. |
|Fallback Strategy configuration |Time window, behavior type |If the configuration is inconsistent with actual business scenarios, the system will fail to **recall popular items** for **cold\-start users**, hindering initial engagement. |After ensuring alignment with business needs, try extending the time window (for example, from '24 hours' to '72 hours') or changing the behavior type.<br><br>Reference: [Feature Overview](https://docs.byteplus.com/docs/viking-aisearch/92194) |


&nbsp;


---



&nbsp;

<span id="64736d21"></span>
## Some requests have no recommended items

If only some "recommendation API" requests or the "recommendation experience" interface refresh do not return items, it is likely due to business rules causing no available recommended items. You can check the following configurations:


|**Checkpoint** |**Problem** |**Impact** |**Fix plan** |
|---|---|---|---|
|"Deduplication Rules" configuration |The time window is too large |All recommendable items are returned to the user, and the platform cannot obtain items meeting the return conditions |Ensure configuration aligns with business needs and consider shortening the time window (for example, from "7 days" to "3 days")<br><br>Reference: [Feature Overview](https://docs.byteplus.com/docs/viking-aisearch/92194) |
||The number of items is too large ||Ensure configuration aligns with business needs and consider reducing the number of deduplicated items (for example, from 500 to 200)<br><br>Reference: [Feature Overview](https://docs.byteplus.com/docs/viking-aisearch/92194) |
|Filter conditions |Does not meet expectations |No items match the filter criteria |On the console's "Scene Configuration" page, locate the "Filter Conditions" setting and check to ensure items meet the filter criteria. |
|Filter conditions |Set too strictly |Recalled items are all filtered out by the filter conditions |Loosen the filter conditions while ensuring business compliance |
