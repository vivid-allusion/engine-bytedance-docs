---
title: "Advanced Analysis: Cohort Analysis"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Advanced-Analysis-Cohort-Analysis"
---

<span id="一-概述"></span>
# 1. Overview

**Why is cohort analysis necessary?** 

The user behavior of most products changes in stages over time, that is, the user's use of the product/function has a life cycle: after the user comes into contact with the new product or new function, they will experience the process from initial use to frequent use to become a loyal user, or reduced interest to become a lapsed user.

What product operation needs to do is to manage and change the user life cycle and improve the stickiness and active level of users. The basis for decision\-making here is cohort analysis.

**What is cohort analysis?** 

**Cohort analysis:**  that is, the user is divided into groups according to the time of the initial behavior (i.e. **cohorts)** , and then:


* By comparing users in the same cohort horizontally, the changes of similar groups over time are obtained, and the impact of strategies on the entire life cycle of users is observed.

* Vertical comparison of different cohorts shows whether the performance of the application is getting better and better, thus verifying whether the product improvement has achieved results.


<span id="二-名词解释"></span>
# 2. Term explanation


* **Cohort:**  belongs to a subdivision in the user subgroup, which refers to the grouping of users with common behavioral characteristics within a specified time.

* **Common behavioral characteristics:**  refers to similar behaviors in a certain time period, which can be classified according to different behaviors in addition to new users at different times, such as entering the experiment for the first time.

* **New users:**  Users who entered the experiment for the first time that day.


<span id="三-应用场景"></span>
# 3. Application scenario

**1. Does the experimental strategy have long\-term effects on users?** 

Douyin developed a new function of playing time for rewards, first open an A/B experiment to verify the experimental effect, looking at the data and finding that the user data performance of the new function is significantly better than that of the control group, wondering whether the experimental strategy can have a long\-term impact on the user: for example, let the user develop a habit, even if the experiment is closed without rewards, the user still maintains the habit of playing.

Then you can use cohort analysis to observe whether the user has seen the new function since entering the experimental group for the first time, and whether the metric performance is still better than that of the control group after 1 day/2 days/n days, so as to determine whether the experimental strategy is effective in the short term or has a long\-term impact on the user.

**2. Analyze the impact of experiments on users with different active levels**

After the experiment is launched, if you want to compare the follow\-up performance of users who experienced the experimental strategy at different stages of the experiment to analyze the differences between the groups of "new users" on different dates, you can use cohort analysis to analyze the performance of "new users" on different days. Check the metric performance after 1 day/2 days/n days.

<span id="四-同期群分析"></span>
# 4. Cohort analysis

<span id="_1-操作入口"></span>
## 1. Operation entrance

On the "Experiment Reports Page \- \> Cohort Analysis", view the cohort analysis report of the experiment. As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1c6672410c04ab4b71dfdacd49cf88c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-按进组时间拆分指标趋势"></span>
## 2. Split metric trends by group entry time

Metric trend display, the metric trend chart of the first\-time user in the selected time since the first entry day, 1 day later, 2 days later... 30 days later.


* By default, aggregated data from the start date of the experiment to yesterday is displayed.

* Add a dimension above to observe a cohort analysis for a client base (e.g., "System Language = en").

* You can toggle the metric in the upper left corner of the trend chart:

   * Support: per capita class (pv/au, pv/uv, sum/au, sum/uv), conversion rate class (uv/au), ctr click through rate class (pv/sum, sum/pv, pv/pv, sum/sum), and meet the type of combination metrics;

   * Not supported: pv type, sum type.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba918ed91f38495eaef9ef0f35d882f4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-按进组时间拆分详细数据"></span>
## 3. Split detailed data by group entry time

Detailed data, showing the metrics data of the first\-time users in the selected time since the first day, 1 day later, 2 days later... 30 days later.


* For each experimental group, show the increase or decrease and confidence interval relative to the control group;

* Click the arrow icon next to the detailed data experiment group to view the daily data, that is, the metric data of the new group users on the same day, 1 day later, 2 days later... 30 days later.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65c724ae7bb34267bde6e7601a1a5c0d~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-同期群报告如何解读"></span>
## 4. How to interpret cohort reports

Taking the metric purchase conversion rate as an example, the following figure shows the purchase conversion rate (that is, the proportion of people who have purchased) trend and detailed data of new users since they first entered the experiment. You can see:

(1) After the user enters the group for the first time, the purchase conversion rate (the proportion of the number of people who have purchased) is on a downward trend. For example, there are 433 new users in the experimental version. The purchase conversion rate on the day of entering the group for the first time is about 10%. After entering the group for 3 days, the purchase conversion rate is about 6%. After 20 days, it tends to be 0.

(2) From the detailed data, the comparison of the purchase conversion rate by group split between the experimental version and the control version is not significant, that is, the experimental strategy has no positive effect on the long\-term trend of purchase conversion rate.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1930ff96d57465eacccebd1c67449c2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9718f97dc9d841be9e510b3818647c00~tplv-goo7wpa0wc-image.image) </span>
