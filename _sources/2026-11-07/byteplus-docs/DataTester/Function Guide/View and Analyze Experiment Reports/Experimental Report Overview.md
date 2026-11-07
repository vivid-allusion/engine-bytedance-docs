---
title: "Experimental Report Overview"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Experimental-Report-Overview"
---

<span id="一-术语表"></span>
# 1. Glossary


* **Absolute difference:**  The absolute difference between the current experimental version and the control version.

* **Relative Difference Value:**  The absolute difference/baseline value of the current experimental version relative to the control version.

* **p\-value:**  The probability of an extreme case occurring in a randomly selected sample if the null hypothesis is true. When the p\-value < 1 \- confidence level is considered statistically significant.

* **Confidence interval:**  Estimate interval for population parameters constructed from sample statistics.

* **MDE:**  Minimum Detectable Effect Minimum Detectable Effect (test sensitivity), which can effectively detect the diff range of the metric confidence level under current conditions.

* **Probability density:**  probability density, also known as probability distribution curve (Probability Curve). Taking the probability density as the ordinate and the interval as the abscissa, the integral of the probability density to the interval is the area, and the area is the probability of the event occurring in this interval, and the sum of all areas is 1.


<span id="二-实验报告"></span>
# 2. Experimental report

The experimental report module of "A/B Testing" provides conclusive inferences based on hypothesis testing theory for comparing experimental results.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The number of participants in the experiment was counted in real time on the day of the experiment. After the second day of opening, it will be updated according to the T\-1 daily day level, and the specific caliber is the cumulative number of people entering the group in the experiment as of 0:00 on the day.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93befdcdaecb4016859287fca15eb53e~tplv-goo7wpa0wc-image.image) </span>

The experimental report page not only shows the basic conclusions of the experiment, but also includes the specific performance of the core metrics and the corresponding day\-level trend map, probability distribution map and box chart (snapshot of the original box).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11c5533e19c745fe90fe8e707fae2a2e~tplv-goo7wpa0wc-image.image) </span>

<span id="三-数据指标"></span>
# 3. Data metrics

Data metrics include three categories: event metrics, retention metrics, and funnel metrics

<span id="_3-1-事件指标"></span>
## 3.1 Event metrics

<span id="_3-1-1-指标导航"></span>
### 3.1.1 Metric navigation

The metric navigation on the left side of the experimental data will display all the "focus metric groups" of this experiment in groups, and it is recommended to place a set of related metrics in one metric group. By default, the metric group where the "core metric" is located is displayed. After a certain metric is selected in the navigation, the right view will automatically anchor to the metric group \- the location of the metric

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b350fac065f4bbdb9a7530c21296eef~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-指标信息"></span>
### 3.1.2 Metric information


* The default view is "Metric Group View", and switching to "Metric View" is supported.

* Each metric in the table shows the "relative difference value", "confidence interval", "index value" in turn, and the significant test results of Diff are colored.

* Hover the data table to show a detailed interpretation of the metric performance


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7525cd2b09064691a4dee3f37dedf29b~tplv-goo7wpa0wc-image.image) </span>


* The single metric view displays information such as the number of people entering the version, the metric value, the diff value of the experimental version relative to the metric, and the relative change and confidence interval, and supports viewing day\-level trends, probability distributions, and box charts


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6437a331c74240fcbfcabfc0f724db65~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-3-添加过滤条件"></span>
### 3.1.3 Add filters


* **Support for adding time and dimension filters. As follows:** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38ca0de191184bb4be25357c64ff6461~tplv-goo7wpa0wc-image.image) </span>

Other relevant information:


* The day level does not include today. Switch to the hour and minute levels to see today's data.

* On the day the experiment was created, real\-time data (5\-minute level) was displayed by default in the "Experiment Concern metric". On the day the experiment is over, you can still view real\-time data, even if the experiment is over.

* If the start date of the experiment = the end date of the experiment, after the experiment is over, the "attention experimental metric" defaults to real\-time data granularity (5\-minute level). When the opening day of the experiment ≠ the end day of the experiment, on the end day of the experiment, "Follow the experimental index" defaults to the heaven\-level granularity.


<span id="_3-1-4-时间趋势"></span>
### 3.1.4 **Time Trend**

According to the time granularity of the experimental report, the "day\-level trend", "time\-level trend" and "minute trend" of a certain metric are displayed. Take "Sky Trends" as an example:


* You can view the statistics and p\-values of the day's metrics, as well as the range of the statistics for the day. The daily average defined caliber is the metric performance of all current users who have entered the group on that day, not the new users who entered the group on that day.

* When you open the "Range Display", a range appears, which produces an overlapping effect and shows how the range of core metrics has changed over time for each version.

   * Ideally, the range would decrease over time and be reflected in the diagram.

   * If the range is expanded, it indicates fluctuations in the data.

   * If the ranges overlap, it means you are unsure which version works better.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc5a13b0530a4d5a941c601275981b5e~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-1-5-概率分布"></span>
### 3.1.5 Probability distribution

The probability distribution shows the value of the index and the probability distribution of its occurrence. The horizontal axis is the index value, and the vertical axis is the probability density of the index value. The distribution of the index is reflected by the mean and variance. Comparison of the probability distribution of the experimental group and the control group can assist in judging the difference between the experimental group and the control group.


* The default control version uses gray, while other versions use color.

* On the normal distribution curve of different experimental versions, the mouse hover will display the information of "number of entrants, p\-value, metric variance, MDE, confidence interval" for each version.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d69b5d2ec8fc4ac194b46eef2576640c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-6-箱型图"></span>
### 3.1.6 B**ox drawing**

Box whisker snapshot, also known as box graph, is the maximum, minimum, median and two quartiles of the data, reflecting the distribution characteristics of the original data source. By comparing the box whisker snapshots of the experimental group and the control group, the distribution characteristics of the two groups of data can be compared.

Application Note:


* For per capita type (PV/AU, PV/UV, SUM/AU, SUM/UV), PV type, SUM type, CTR click through rate type, PV/SUM & SUM/PV/SUM & PV/PV/PV and other types of metrics are applicable.

* The "CVR conversion rate type" does not currently support box whisker diagrams because it is a binary value for a single individual.

* Hour\-level/minute\-level granularity display, no box whisker diagram is provided.


Overlapping area description: The shaded area of each color is the overlapping area corresponding to the experimental group and the reference group, and the overlapping area indicates that it is uncertain which version works better. If your best\-performing version has a lot of uncertainty overlap, we recommend that you adjust the running time of the experiment to a longer one.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99faf43ab68c45ad817daac9dea38644~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-7-自选指标视图"></span>
### 3.1.7 Optional metrics view

Added "Optional Metric Summary" view to support metrics summary display across metric groups

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd9795a3d50049728e60e447050dcb8b~tplv-goo7wpa0wc-image.image) </span>


* Tag the metric in the "Follow Metrics Group" to add it to the "Optional Metrics Summary".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7749744eb8d548f4b2904f658714fad4~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f607ca890784af29717b36d0cb4e6a5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-留存指标"></span>
## 3.2 Retention metrics

<span id="_3-2-1-同期群留存趋势"></span>
### 3.2.1 Cohort retention trends

Cohort retention trend refers to splitting experimental users into the date they first entered the experiment, and observing the subsequent retention trends of users who first entered the group on different days. Cumulative trend graphs for sub\-groups are supported, and day\-level trend graphs from 1\-day retention rate to 30\-day retention rate are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b49750519634f47a7862790c2119ff3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-n日留存日趋势"></span>
### 3.2.2 N\-Day Retention Day Trends

Represents the Nth\-day retention trend for users who entered the group within the filter timeframe.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6026591081d440590d1a706a82a0bf4~tplv-goo7wpa0wc-image.image) </span>

**The retention rate is the default configuration of the system. How to calculate the retention rate?** 


|Rule |Processing logic |
|---|---|
|Grouping |Users entering the experimental group for the first time (not necessarily new users) |
|Attribution method |The retained users are divided according to the time of entering the group and attributed to the time of first entering the group |
|Return visit rule |Returning to the APP is regarded as a return visit. |


Let me give you an example.


* The number of users in experimental group A on the first day is: 10000, and the base_user on the first day is 10000;

* The number of users in experimental group A on the second day is: 10400, of which 9200 users are already in A on the first day, and 1200 users are new users on the same day; the base_user is 1200 on the second day, and the retention on the next day of the first day is 9200/10000 = 92%;

* The number of users in experimental group A on the third day is: 10200, of which 8000 users are already in A on the first day, 1100 users are users who enter A on the second day, and 1100 is users who enter A on the third day; The base_user of the third day is 1100, the retention of the second day of the first day is 8000/10000 = 80%, and the retention of the next day of the second day is 1100/1200 = 91.67%;

* Then, the index of each entry date is weighted and averaged with base_user to obtain the Day Retention Ratio at Day 1 and Day 2.


**How to calculate detailed data for each experimental version of "Cohort Retention Trends" every day?** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fd2d5db7665401d8ab3e4814e9e56b4~tplv-goo7wpa0wc-image.image) </span>

Examples are as follows:


|Date |Number of new entrants |1 day later |2 days later |3 days later |4 days later |5 days later |6 days later |7 days later |8 days later |9 days later |10 days later |11 days later |12 days later |13 days later |14 days later |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|All new users |317907 |4.99% |5.11% |5.24% |5.42% |5.58% |5.81% |6.11% |6.49% |6.93% |7.44% |8.48% |10.06% |13.77% |15.96% |
|20200715 |24,230 | | | | | | | | | | | | | | |
|20200714 |23,941 |1.60% | | | | | | | | | | | | | |
|20200713 |23,551 |1.70% |1.70% | | | | | | | | | | | | |
|20200712 |23,160 |1.82% |1.85% |1.89% | | | | | | | | | | | |
|20200711 |22,725 |1.74% |1.64% |1.70% |1.69% | | | | | | | | | | |
|20200710 |22,391 |1.79% |1.87% |1.73% |1.85% |1.76% | | | | | | | | | |
|20200709 |22,014 |1.83% |1.91% |1.86% |1.93% |1.89% |1.84% | | | | | | | | |
|20200708 |21,631 |1.89% |1.83% |1.90% |1.75% |1.87% |1.76% |1.90% | | | | | | | |
|20200707 |21,237 |1.93% |1.96% |1.87% |1.90% |1.86% |1.80% |1.91% |1.92% | | | | | | |
|20200706 |20,857 |1.97% |1.80% |1.87% |1.84% |1.86% |1.84% |1.78% |1.91% |1.90% | | | | | |
|20200705 |20,480 |1.98% |1.98% |1.90% |2.01% |2.01% |2.02% |2.06% |2.03% |1.97% |1.91% | | | | |
|20200704 |20,104 |2.01% |2.04% |2.05% |2.05% |2.06% |2.20% |2.21% |2.23% |2.12% |1.88% |2.09% | | | |
|20200703 |19,813 |2.44% |2.40% |2.47% |2.51% |2.27% |2.17% |2.17% |2.29% |2.24% |2.06% |2.04% |1.96% | | |
|20200702 |27,373 |30.55% |29.08% |27.47% |26.19% |24.61% |23.36% |21.84% |20.36% |18.99% |17.42% |16.04% |14.56% |13.16% | |
|20200701 |4,400 |30.93% |29.73% |28.70% |27.48% |26.59% |25.32% |24.25% |23.23% |21.89% |20.77% |19.68% |18.57% |17.52% |15.95% |


After 1 day: 4.99% = (23941 \* 1.60% + 23551 \* 1.70% + 23160 \* 1.82 % + …+ 27373 \* 30.55% + 4400 \* 30.93%)/(23941 + 23551 + … + 27373 + 4400) After 4 days: 5.42% = (22725 \* 1.69% + 22391 \* 1.85% + 22014 \* 1.93% +... + 27373 \* 26.19% + 4400 \* 27.48%)/(22725 + 22391 +... + 27373 + 4400)

<span id="_3-3-转化漏斗"></span>
## 3.3 The conversion funnel

For details, see [Metric Analysis: Funnel Metric Analysis](https://docs.byteplus.com/docs/DataTester/Metric-Analysis-Funnel-Metric-Analysis).

<span id="四、高级分析"></span>
# 4. Advanced Analytics

<span id="_4-1-同期群分析"></span>
### 4.1 **Cohort analysis**

**Cohort analysis:**  that is, users are divided into groups (i.e. cohorts) according to the time when the initial behavior occurred.


* By comparing users in the same cohort horizontally, the changes of similar groups over time are obtained, and the impact of strategies on the entire life cycle of users is observed.

* Vertical comparison of different cohorts shows whether the performance of the application is getting better and better, thus verifying whether the product improvement has achieved results.


For details, see [Advanced Analysis: Cohort Analysis](https://docs.byteplus.com/docs/DataTester/Advanced-Analysis-Cohort-Analysis).

<span id="_4-2-差异分析"></span>
### 4.2 Analysis of differences

After the experiment is completed, the experimental results are for all the audience groups of the experiment, and the conclusion that the corresponding strategy has positive or negative effects can be obtained through the data. However, a strategy that reaches positive or negative conclusions for all users is not the same as reaching the same conclusion for subdivided users. At this time, we can use group comparison and difference analysis to obtain a conclusion that the experimental strategy is positive/negative for a certain segment of the population.

For details see:[Advanced Analysis: Difference Analysis and Group Comparison](https://docs.byteplus.com/docs/DataTester/Advanced-Analysis-Difference-Analysis-and-Group-Comparison)

<span id="五-置信度和置信区间"></span>
# 5. Confidence levels and confidence intervals

<span id="_5-1-概念解读"></span>
### 5.1 Concept interpretation

**Confidence level**


* Confidence level (also known as confidence level, confidence coefficient, statistical significance), refers to the probability that there is a real performance difference between the experimental group and the control group, and the difference between the experimental group and the control group is not due to randomness. Confidence levels allow us to understand when the results are correct, and for most businesses, confidence levels above 95% can generally be interpreted as experimental results being correct. Therefore, by default, the "A/B test" sets the confidence level parameter value to 95%.

* In the A/B experiment, we can only do small sample experiments because we can only extract traffic. The distribution of sample traffic will not be exactly the same as the overall traffic, which means that none of the experimental results can be 100% accurate \- even if the data goes up, it may be due solely to sampling error, regardless of our strategy. In statistics, confidence levels exist to describe the reliability of experimental results.


In the process of the experiment, the sample flow we extracted will actually be slightly different from the overall flow, and these differences determine that there will be some "errors" in the conclusions we draw through the experiment.

> For example, in the experiment, I increased the purchase rate by 3% by changing the color of the landing page, but because the sample traffic does not fully represent the overall traffic, it is possible that "my strategy of changing the color was useless, and the purchase rate increased by 3% due to the sampling results." So what are the chances of this "my strategy didn't work" event happening? In statistics, we use "significance level (α) " to describe the probability of this event occurring. And confidence level = 1\-α. On the "A/B test" platform, according to industry standards, the significance level α is 0.05. In an A/B experiment, if the probability of "my strategy actually didn't work" is less than 0.05, we say the conclusion is "statistically significant/believable." This means that your new strategy has a high probability (greater than 95% in A/B experiments) of being effective. Conversely, if the probability of this event is greater than 0.05, the experimental conclusion is said to be "not significant/unbelievable."


"A/B testing" mainly uses hypothesis testing to calculate the confidence level of the metric. In fact, it is to test a pair of opposing hypotheses: the null hypothesis and the alternative hypothesis.

> A null hypothesis is a hypothesis that the experimenter wants to gather evidence against. The null hypothesis in A/B experiments is that "the new strategy has no effect." Alternative hypothesis: A hypothesis that the experimenter wants to collect evidence to support, with mutual exclusion from the null hypothesis. The alternative hypothesis in A/B experiments is that "the new strategy works."


To test a hypothesis by contradiction means using existing data to prove that the null hypothesis is false (false) and that the alternative hypothesis is true (true). This set of methods is known statistically as the null hypothesis significance test.

**Confidence interval**

Mainly through a certain metric or retained experimental version means changing value and confidence intervals to judge whether the experimental version performs better than the control version on the current metric or user retention.


* If the confidence intervals are both positive or negative at the 95% confidence level, the experimental results are statistically significant.

* If the confidence interval is positive and negative at the 95% confidence level, the experimental results are not statistically significant.


<span id="_5-2-示例"></span>
### 5.2 Examples

**Statistical positive significance**

As shown in the figure below, the change rate of the sample mean in the experimental version compared to the control version is + 46.822%. At the 95% confidence level, the confidence interval is [46.589%, 47.055%], which is statistically significant positive, indicating that the experimental version has been detected to be better than the control version under the current sample size conditions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f0a01395ff94688bf46e32528e5dc56~tplv-goo7wpa0wc-image.image" width="800px" /></div>


**Statistically negatively significant**

As shown in the figure below, the change rate of the sample mean in the experimental version compared to the control version is \-26.553%. At the 95% confidence level, the confidence interval is [\-26.786%, \-26.320%], which is statistically significantly negative, indicating that the experimental version has been detected to be inferior to the control version in core metrics under the current sample size conditions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ba21078696d49049e79016be0166aae~tplv-goo7wpa0wc-image.image" width="800px" /></div>


**Insignificant**

As shown in the figure below, the change rate of the sample mean in the experimental version compared to the control version is \-0.941%. At the 95% confidence level, the confidence intervals are [\-3.552%, 1.670%], the confidence intervals are negative and positive, and the experimental results are non\-statistically significant.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5631f207a5c74b869c9a457c271b2b74~tplv-goo7wpa0wc-image.image" width="800px" /></div>


<span id="六、下载进组用户id"></span>
# Download the user ID into the group


* In the experimental report page, click on the original number of people entering the group to directly download all the user IDs and corresponding group information, including user ID, experimental name, experimental group, and filter conditions (if any);

* You can download up to 5 million pieces of data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdc6eb85c93d4f08a6c006733dc8654c~tplv-goo7wpa0wc-image.image) </span>
