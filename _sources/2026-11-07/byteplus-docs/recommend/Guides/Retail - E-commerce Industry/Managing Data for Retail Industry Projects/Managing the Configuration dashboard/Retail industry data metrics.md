---
title: "Retail industry data metrics "
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-retail_industry_data_metrics"
---

The Data Configuration dashboard has a Metrics section with some default metrics. Metrics are the quantitative measurement to reckon the success of recommendations.

The metrics used in BytePlus Recommend are as follows:


|**Categories** |**Purpose** |**Metrics** |**Description** |
|---|---|---|---|
|Join rate |To check if two sets of data align with each other by the sync percentage. |userevent\-to\-product |* Equals the total number of UserEvents containing a `product_id` in User data divided by the total number of User Events.<br><br>* Equals the total number of UserEvents containing a `root_product_id` in User data divided by the total number of User Events. |
|||userevent\-to\-user |Equals the total number of UserEvents containing a `user_id` in User data divided by the total number of User Events. |
|Attribution rate |To check if associated user events are attributed to the inherited user event. |attribution rate of click |This ratio is utilized to assess the contribution of the recommendation toward the desired outcomes, such as clicks or purchases.<br><br>Attribution rate of click is calculated through the following: total number of clicks that are attributed to the recommendation/total number of clicks. |
|||attribution rate of purchase |Attribution rate of purchase is calculated through the following: total number of purchases that are attributed to the recommendation/total number of purchases. |
|Core metrics |To check if the optimization metrics are aligned |click\-through rate |Click\-through rate refers to the rate of how likely users will click on a product after seeing it.<br><br>Click\-through rate is calculated through the following: number of clicks/number of unique visitors. |
|||click per user |Click per user is calculated through the following: number of clicks/number of unique visitors. |
|||purchase per user |Purchase per user is calculated through the following: number of purchase/number of unique visitors. |
|||conversion rate |Conversion rate measures how likely users will buy a product after clicking on it.<br><br>Conversion rate is calculated through the following: number of purchases/numnber of unique visitors. |
|||impression per user |Impression per user is calculated through the following: number of impressions/number of unique visitors. |
