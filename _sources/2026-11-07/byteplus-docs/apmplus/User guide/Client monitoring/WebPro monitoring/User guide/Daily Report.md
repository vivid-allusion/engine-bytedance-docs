---
title: "Daily Report"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/daily_Report"
---

The daily Report presents performance scores and trend charts for each core metric at a daily granularity over the selected time period. It is commonly used to observe whether metrics have improved after a period of optimization or for routine monitoring.

<span id=".562b6YCJ57u05bqm"></span>
## Filter dimensions

Supports filtering data by time.

Time: Select **last day**, **last 7 days**, **last 15 days**, **last 30 days**, **last 60 days**. All time periods have a time granularity of one day.

<span id=".5aSn55uY"></span>
## Dashboard

The dashboard is divided into two parts: the left part displays filtered data performance scores, and the right part displays the trend chart for each metric.

<span id=".6KGo546w5YiG"></span>
### Performance score

The calculation rules for the pageload performance score include six metrics: JavaScript error rate, request time, request error rate, static resource error rate, blank screen error count, and pageload performance score. In the radar chart, the three levels—poor, good, and excellent—are displayed using different colors. Determination criteria:


|**Performance scores** |**Levels** |**Color** |
|---|---|---|
|0 <= performance score < 60 |Poor |Red |
|60 <= performance score < 80 |Good |Yellow |
|80 <= performance score <= 100 |Excellent |Green |


<span id=".5p2D6YeN"></span>
#### Weight


|**Metric** |**Default weight** |
|---|---|
|JavaScript error rate |0.2 |
|request time |0.15 |
|request error rate |0.15 |
|Static resource error rate |0.2 |
|Blank screen error rate |0.1 |
|pageload performance score |0.2 |


When a metric is not turned on for reporting, the weights of all metrics are allocated according to the current proportions. At the same time, the corresponding area of the radar chart is grayed out, and it is indicated that metrics not reported do not participate in scoring.

For example, if static resource error rate reporting is not turned on, the performance score will be composed of five metrics, and the weights of these metrics will be redistributed according to their current proportions.

<span id=".5b6X5YiG6K6h566X5YWs5byP"></span>
#### The score calculation formula


1. Calculate metrics.

   Rules for calculating metric scores:

   
   |**Metric value range** |**Scoring** |Levels |Scope |Score |
   |---|---|---|---|---|
   |metric value <= Y |100 |Satisfied |0~Y |1 |
   |Y <= metric value <= 4Y |100 \- 100 \* (metric value \- Y) / 3Y |Tolerable |Y~4Y |0.5 |
   |metric value \> 4Y |0 |Not satisfied |Greater than 4Y |0 |
   

   Y is the threshold. The thresholds and weights for each metric can be configured in the [project setting](https://docs.byteplus.com/en/docs/apmplus/project_setting).

2. Calculate the performance score.

   Performance score = ∑ (score of metric i × weight of metric i)

   
   |**Performance score** |**Level** |**Colors** |
   |---|---|---|
   |0 <= performance score < 60 |Relatively poor |Red |
   |Performance score: 60 <= score < 80 |Good |yellow |
   |80 <= performance score <= 100 |Excellent |Green |
   


<span id=".5aSn55uY6LaL5Yq_"></span>
### Dashboard trends


|**Metric** |**Calculation rules or description** |
|---|---|
|JavaScript error rate |Number of page views with JavaScript errors / total page views |
|request error rate |Request error count / total error count |
|Complete load time |The time for the page to fully load |
|blank screen count |Number of blank screen occurrences |


<span id=".6LaL5Yq_5Zu-"></span>
### Trend charts


* The metrics displayed in the trend chart include **JavaScript error rate**, **affected user rate**; **request error rate**, **proportion of users affected by request errors**; **complete load time**, **slow page load count**; **blank screen count**, **blank screen affected users**; **static resource error rate**, **proportion of users affected by static resource errors**; **page PV**, **page UV**.

* Each chart includes data: the average metric value for the current time period, the metric value for the previous period, and the fluctuation relative to the previous period.

   The value of the previous period refers to the value within the time period selected by the previous user. For example, if you select a cycle of 7 days, the previous cycle refers to the preceding 7 days.

* You can click the "Go to a certain page" option in the upper right corner to navigate to a specific page and view more detailed information.
