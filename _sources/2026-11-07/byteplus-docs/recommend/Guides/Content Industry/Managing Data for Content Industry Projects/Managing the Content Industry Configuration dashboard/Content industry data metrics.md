---
title: "Content industry data metrics"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-content_industry_data_metrics"
---

The Data Configuration dashboard has a Metrics section with some default metrics. Metrics are the quantitative measurement to reckon the success of recommendations.

The metrics used in BytePlus Recommend are as follows:


|**Categories** |**Purpose** |**Metrics** |**Description** |
|---|---|---|---|
|Join rate |To check if two sets of data align with each other by the sync percentage. |userevent\-to\-user |Equals the total number of UserEvents containing a `user_id` in User data divided by the total number of User Events. |
|||userevent\-to\-content |* Equals the total number of UserEvents containing a `content_id` in User data divided by the total number of User Events. |
|Attribution rate |To check if associated user events are attributed to the inherited user event. |attribution rate of stay |Attribution rate of stay is calculated through the following: total stay duration that are attributed to the recommendation/total time of stay. |
|||attribution rate of click |This ratio is utilized to assess the contribution of the recommendation toward the desired outcomes, such as clicks or duration of stay.<br><br>Attribution rate of click is calculated through the following: total number of clicks that are attributed to the recommendation/total number of clicks. |
|Core metrics |To check if the optimization metrics are aligned |impression per user |Impression per user is calculated through the following: number of impressions/number of unique visitors. |
|||duration per user |Duration per user is calculated through the following: duration of stay/number of unique visitors. |
|||click per user |Click per user is calculated through the following: number of clicks/number of unique visitors. |
|||click through rate |Click\-through rate refers to the rate of how likely users will click on a content after seeing it.<br><br>Click\-through rate is calculated through the following: number of clicks/number of unique visitors. |
