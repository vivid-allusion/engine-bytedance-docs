---
title: "Daily Report"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/daily_Report_minipro"
---

The daily report presents the performance scores and trend charts for each core metric of the Mini Program, displayed at a daily granularity over the selected time period. It is commonly used to observe whether metrics have improved after a period of optimization or for routine inspection.

<span id="b1177eca"></span>
## Filter dimensions

Support filtering data by time, mini program type, and operating system.


* Time: Allows selection of **the last 7 days**, **the last 15 days**, **the last 30 days**, and **the last 60 days**. The time granularity for all time cycles is 1 day.

* Mini program type: Supports selecting **All**, **TikTok Mini Program**, **WeChat Mini Program**, **Alipay Mini Program**, **Baidu Mini Program**, and **Lark Mini Program**.

* Operating system: Supports selecting **all**, **iOS**, **Android**, **Mac**, and **Windows**.


<span id="220b563e"></span>
## Dashboard

The dashboard is divided into two sections: the left side displays data performance scores based on filter conditions, while the right side shows trend charts for each metric.

<span id="7f520143"></span>
### Performance scores

The calculation rules for the performance score include six metrics: JavaScript error rate, request error rate, request time, callback time, setData time, and pageload performance score. The radar chart uses different colors to represent the three levels: poor, good, and excellent. Determination criteria.


|**Performance score** |**Level** |**Colors** |
|---|---|---|
|0 <= performance score < 60 |Poor |Red |
|Performance score is at least 60 but less than 80 |Good |yellow |
|80 <= Performance score <= 100 |Excellent |Green |


<span id="7084b699"></span>
#### Weight


|**Metric** |**Default weight** |
|---|---|
|JavaScript error rate |0.15 |
|request error rate |0.15 |
|request time |0.15 |
|callback time |0.2 |
|setData Time |0.15 |
|pageload performance score |0.2 |


When a metric is not turned on for reporting, the weights of all metrics are allocated according to the current proportions. At the same time, the corresponding area in the radar chart is grayed out, and it is indicated that metrics not reported do not participate in scoring.

For example, if reporting is not turned on for setData, the performance score consists of five metrics, and the weights of these five metrics are redistributed according to the current weight proportions.

<span id="3d1fd220"></span>
#### The score calculation formula


1. Calculate metric score.

   Rules for calculating metric scores:

   
   |**Metric value range** |**Rating** |Level |Scope |Score |
   |---|---|---|---|---|
   |Metric value <= Y |100 |Satisfaction |0~Y |1 |
   |Y <= metric value <= 4Y |100 \- 100 \* (metric value \- Y) / 3Y |Tolerable |Y~4Y |0.5 |
   |metric value \> 4Y |0 |Dissatisfied |Greater than 4Y |0 |
   

   Y is the threshold. Each metric's threshold and weight can be configured in the [project setting](https://docs.byteplus.com/en/docs/apmplus/project_setting_minipro).

2. Calculate the performance score.

   Performance score = ∑ (score of metric i × weight)


<span id="ce114279"></span>
### Dashboard trends


|**Metric** |**Calculation rules** |**DescriptionS** |
|---|---|---|
|PV(Page View) |Deduplicate reported pageviews based on view_id. |Page views |
|UV(User View) |Deduplicate reported pageviews based on user_id. |Number of unique visitors |
|page time on site |Subtract the timestamps of two pageviews with the same view_id. |The duration from when users enter the page until they leave the page |
|average time on site |Page time on site / unique visitors |Average time each user spends on a page |


<span id="4987cdd8"></span>
### Trend charts


* Metrics displayed in the trend chart include **JavaScript error rate**, **JavaScript error user impact rate**; **request error rate**, **request error user impact rate**; **first screen total load time**, **slow startup count**; **total page navigation time**, **slow\-pageload count**.

* Each chart contains the following data: the average metric value for the current time period, the metric value for the previous period, and the fluctuation relative to the previous period.

   The value of the previous period refers to the value within the time period selected by the previous user. For example, if you select a cycle of 7 days, the previous period is the previous 7\-day period.

* Click 'Go to a page' in the upper right corner on any page to jump to a specific page and view more detailed information.
