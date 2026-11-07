---
title: "Daily trend"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/daily_trend"
---

The daily trend is a method for displaying trend charts of core metrics at a daily granularity, commonly used to observe whether metrics have improved after a period of optimization or for routine inspection.

<span id="24672585"></span>
## Filter dimensions

Support filtering data by time and Operating System.


|**Subnamespace** |**DescriptionS** |
|---|---|
|time |Filter data by the time range.<br><br><br>* **Recent**: View data from the past X days. By default, data for the most recent 7 days is displayed. You can configure it to display data for the most recent **1 day**, **7 days**, **30 days**, or **60 days**.<br><br>* **Scope**: View the data between yyyy\-mm\-dd and yyyy\-mm\-dd. The platform retains data for up to 90 days, so the earliest start time you can select is 90 days ago. |
|System |Select an operating system.<br><br><br>* **All**<br><br>* **iOS**<br><br>* **Android** |


<span id="cf8dcd31"></span>
## Dashboard

The dashboard is divided into two sections: the left side displays the data performance score under the filter conditions, while the right side shows the trend chart for each metric.


* Data performance score

   The Android operating system and the iOS operating system calculate performance scores based on six different metrics:

   * Android: OOM impacted users rate, Cold Start, disk usage, network error rate, total crash impacted users rate, ANR impacted users rate, and smoothness

   * iOS: OOM user ratio, disk usage, Cold Start, network error rate, hang ratio, frame loss rate

* Metric trend chart

   
   |**Metric** |**DescriptionS** |
   |---|---|
   |alert count |Alert count under filter conditions |
   |Crash alert count |Crash alert count under filter conditions |
   |Error alert count |Error alert count under filter conditions |
   |PV |Page views under filter conditions (page view) |
   |UV |Unique visitor count under filter conditions (Unique Visitor) |
   |new user count |Number of first\-time application users under filter conditions<br><br>Calculation method: The set difference between the users who reported data within the reporting period (according to the filter criteria) and those who reported data before the reporting period. The smallest unit for new user count display data is the day. Because the platform only retains data from the past 90 days, the platform approximates the new user count by calculating the user count that has not reported any data within the past 90 days.<br><br>For example: On June 15, 2023, view the new user count for the past seven days (from June 9, 2023 to June 15, 2023).<br><br>The platform obtains the user count for data reported within the most recent seven days, from 2023\-06\-09 to 2023\-06\-15, and then obtains the user count for data reported from 2023\-03\-15 to 2023\-06\-08. The difference between these two sets yields the new user count. |
   |Top 3 tasks that trigger alerts |Alert task with the highest alert count under filter conditions |
   


<span id="fc6cc786"></span>
### Performance scores

Performance scores are calculated based on six metrics, and the radar chart uses different colors to display excellent, qualified, and unqualified. The criteria are as follows:


* **Excellent**: For each metric, the mean is calculated based on internal business data. The means are then sorted in ascending order, and the 90th quantile (PCT90) is used as the excellent value.

* **Qualified**: The mean value for each metric is calculated based on internal business calculations. The means are then sorted in ascending order, and the 60th quantile (PCT60) is set as the qualified value.

* **Non\-compliant**: The mean value of each metric is calculated based on internal business logic. After sorting these means in ascending order, the 0th to 59th quantiles (PCT0~PCT59) are designated as non\-compliant values.


<span id="22e89105"></span>
### Weight

There are six metrics on the dashboard, each with a different weight, which indicates the proportion of each metric in the total score.

The empirically determined acceptable and excellent values, as well as the description of weights for Android metrics, are shown in the following table:


|**Metric** |**DescriptionS** |**Pass (60 points)**  |**Excellent (90 points)**  |**Weight** |
|---|---|---|---|---|
|Network error rate |Network error count/total network count |0.01 |0.006 |0.1 |
|Crash impacted users rate |Crash unique user count (UV)<br><br>Includes Java crash, Java startup crash, and Native crash. |0.012 |0.002 |0.3 |
|ANR user proportion |Deduplicated user count/unique visitors (UV) for ANR crashes |0.002 |0.0002 |0.2 |
|Cold Start |Average cold start duration |1100 milliseconds |500 milliseconds |0.1 |
|Fluency |Percentage of FPS in the range 0–50 frames<br><br>The sum of the proportions of FPS_NORMAL and FPS_BAD on the platform |0.06 |0.03 |0.1 |
|Disk usage |Average app storage usage |300M |50M |0.1 |
|Proportion of OOM users |OOM user count/UV |0.7‰ |0.04‰ |0.1 |


The following table shows the qualified values, excellent values, and weight descriptions for iOS metrics, which are provided based on experience:


|**Metric** |**DescriptionS** |**Pass (60 points)**  |**Excellent (90 points)**  |**Weight** |
|---|---|---|---|---|
|Network error rate |Network error count/total network count |0.04 |0.02 |0.1 |
|crash Impacted users rate |Crash unique user count/UV<br><br>Only ordinary crashes are included; hang, OOM crash, and Extension crash are not included. |0.0118 |0.0034 |0.2 |
|Crash impacted users rate |OOM crash deduplicated user count/UV |0.001 |0.0003 |0.2 |
|Startup duration (cold start) |Average cold start duration |1000ms |600ms |0.1 |
|Proportion of users experiencing hang |Watch_dog lag user count per unique visitor |0.0014 |0.0008 |0.2 |
|Frame loss rate |(minor frame loss + moderate frame loss + severe frame loss) / (minor frame loss + moderate frame loss + severe frame loss + no frame loss)<br><br>> Frame loss description: [Smoothness and frame loss](https://docs.byteplus.com/en/docs/apmplus/User_experience#.5rWB55WF5oCn5ZKM5Lii5bin) |0.0015 |0.0006 |0.1 |
|Disk usage |Average app storage usage |300MB |100MB |0.1 |


<span id="f730811b"></span>
### Score calculation formula


1. For each metric, two standard values—qualified value M and excellent value N—are determined based on internal business application data.

2. The score for this metric is calculated in segments based on the score range [0,100]. Where X is the zero score value and Y is the full score value.

3. Calculate metric score [K]

   As shown in the figure, when the metric value K falls within different ranges, it corresponds to different metric scores [K].

4. Calculate scores

   Score = ∑ (score of metric i × weight)


<span id="898771e7"></span>
### Dashboard trend

The trend chart displays five metrics—alert count, crash alert count, error alert count, PV, and UV—along with their change ratios compared to the previous period and the corresponding trend lines. Metric data helps you view changes relative to the previous period. The metric chart uses different colors to show the trends of six dimensions within the filtered time range.

&nbsp;
