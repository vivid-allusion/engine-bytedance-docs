---
title: "Report Summary (Old Version)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Report-Summary-Old-Version"
---

<span id="一-术语表"></span>
# 1. Glossary


* **Probability density:**  probability density, also known as probability distribution curve (Probability Curve). Taking the probability density as the ordinate and the interval as the abscissa, the integral of the probability density to the interval is the area, and the area is the probability of the event occurring in this interval, and the sum of all areas is 1.

* **P\-value:**  The probability of an extreme case occurring in a randomly selected sample if the null hypothesis is true. When the p\-value < 1 \- confidence level is considered statistically significant.

* **MDE:**  Minimum Detectable Effect Minimum Detectable Effect (test sensitivity), which can effectively detect the diff range of the metric confidence level under current conditions.

* **Absolute difference:**  The absolute difference between the current experimental version and the control version.

* **Relative Difference Value:**  The absolute difference/baseline value of the current experimental version relative to the control version.

* **Confidence interval:**  Estimate interval for population parameters constructed from sample statistics.


<span id="二-报告概览"></span>
# 2. Overview of the report

"A/B testing" is in the overview area of the experimental report, providing conclusive inferences based on hypothesis testing theory for the comparison of experimental results. The incoming user data of the report overview is the **next day T + 1 data**, that is, the incoming user data of No. 1 will be displayed in the report overview on No. 2. As follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70ea946d564f438eb4dc0f40b77f89a2~tplv-goo7wpa0wc-image.image) </span>

<span id="三-实验关注指标-留存指标"></span>
# 3. Experimental Attention Metrics & Retention Metrics

<span id="_1-添加过滤条件"></span>
## 1. Add filter criteria

Support for adding time and dimension filters. As follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e912f128ca5e4e8d88d4f5c1406cf0f5~tplv-goo7wpa0wc-image.image) </span>

Other relevant information:


* The sky level does not include today. Switch to the hour and minute levels to see today's data.

* On the day the experiment was created, real\-time data (5\-minute level) was displayed by default in the "Experiment Concern metric". On the day the experiment is over, you can still view real\-time data, even if the experiment is over.

* If the start date of the experiment = the end date of the experiment, after the experiment is over, the "attention experimental metric" defaults to real\-time data granularity (5\-minute level). When the opening day of the experiment ≠ the end day of the experiment, on the end day of the experiment, "Follow the experimental index" defaults to the heaven\-level granularity.


<span id="_2-切换视图"></span>
## 2. Switch views

<span id="_2-1-全局视图"></span>
### 2.1 Global View

Support global view of the relevant data of the experimental focus metrics, as well as the time trend of each metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e31429067dfc4cd5abecb6e3287873ea~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-详细视图"></span>
### 2.2 Detailed view

Supports drill\-down analysis for a single metric, can calculate absolute value of difference, relative value of difference, confidence interval (if computable), p\-value (if computable), MDE (if computable), supports day\-level trends, probability distributions, box snapshots, cumulative trends.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99f444ce89594261ae646d40a0a8a32e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-实验关注指标"></span>
## 3. Experimental focus metrics

The concern metric is through the code event tracking. For new events reported on the same day, the event information can be found in about 10 minutes (without backlog), and the event attribute value can be found in about 6 hours. We recommend that you add a metric to "metric Management" 6 hours after the data is reported, and add this metric as the focus metric of the experiment during the process of creating the experiment.

<span id="_3-1-时间趋势"></span>
### 3.1 Time trends

According to the time granularity of the experimental report, the "day\-level trend", "time\-level trend" and "minute trend" of a certain metric are displayed.

Take "Daily Trend" as an example:


* You can view the statistics and p\-values of the day's metrics, as well as the range of the statistics for the day. The daily average defined caliber is the metric performance of all current users who have entered the group on that day, not the new users who entered the group on that day.

* When you open the "Range Display", a range appears, which produces an overlapping effect and shows how the range of core metrics has changed over time for each version.

   * Ideally, the range would decrease over time and be reflected in the diagram.

   * If the range is expanded, it indicates fluctuations in the data.

   * If the ranges overlap, it means you are unsure which version works better.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4798aa94c25247ec920b17b26390e00e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-概率分布"></span>
### 3.2 Probability distribution

The probability distribution shows the value of the index and the probability distribution of its occurrence. The horizontal axis is the index value, and the vertical axis is the probability density of the index value. The distribution of the index is reflected by the mean and variance. Comparison of the probability distribution of the experimental group and the control group can assist in judging the difference between the experimental group and the control group.


* The default control version uses gray, while other versions use color.

* On the normal distribution curve of different experimental versions, the mouse hover will display the information of "number of entrants, p\-value, metric variance, MDE, confidence interval" for each version.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7faf74b360524a318d497bb9ccaae4c0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-盒须快照"></span>
### 3.3 Boxes of snapshots

Box whisker snapshot, also known as box graph, is the maximum, minimum, median and two quartiles of the data, reflecting the distribution characteristics of the original data source. By comparing the box whisker snapshots of the experimental group and the control group, the distribution characteristics of the two groups of data can be compared.

Application Note:


* For per capita type (PV/AU, PV/UV, SUM/AU, SUM/UV), PV type, SUM type, CTR click through rate type, PV/SUM & SUM/PV/SUM & PV/PV/PV and other types of metrics are applicable.

* The "CVR conversion rate type" does not currently support box whisker diagrams because it is a binary value for a single individual.

* Hour\-level/minute\-level granularity display, no box whisker diagram is provided.


Overlapping area description: The shaded area of each color is the overlapping area corresponding to the experimental group and the reference group, and the overlapping area indicates that it is uncertain which version works better. If your best\-performing version has a lot of uncertainty overlap, we recommend that you adjust the running time of the experiment to a longer one.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83ad88658dd644a39d8e2d4c7704604a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-累积趋势"></span>
### 3.4 Cumulative trends

Cumulative trend refers to the metric data from the start of the experiment to the current day. Taking the metrictimespan per person, experiment time = 2020.09.01~ 2020.09.07 as an example, under the cumulative trend, the 2020.09.03 data refers to the cumulative data of 2020.09.01~ 2020.09.03; under the day\-level trend, the 2020.09.03 data refers to the data of 2020.09.03 day.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c3f7ce1790e4fd289ea9b6bd5c13f91~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-留存指标"></span>
## 4. Retention metrics

<span id="_4-1-同期群留存趋势"></span>
### 4.1 Cohort retention trends

Cohort retention trend refers to splitting experimental users into the date they first entered the experiment, and observing the subsequent retention trends of users who first entered the group on different days.

Cumulative trend graphs for sub\-groups are supported, and day\-level trend graphs from 1\-day retention rate to 30\-day retention rate are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/312b7c5baa7446cabde33d7b04c3ffbb~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-n日留存日趋势"></span>
### 4.2 N\-Day Retention Day Trend

Represents the Nth\-day retention trend for users who entered the group within the filter time frame.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2172bbffd94e49cd85022c1a1f705ffb~tplv-goo7wpa0wc-image.image) </span>

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

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/681566d96b19404e80ab4b4613a1fc67~tplv-goo7wpa0wc-image.image) </span>

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


1 day later: 4.99% = (23941 \* 1.60% + 23551 \* 1.70% + 23160 \* 1.82 % + …+ 27373 \* 30.55% + 4400 \* 30.93%)/(23941 + 23551 + … + 27373 + 4400)

4 days later: 5.42% = (22725 \* 1.69% + 22391 \* 1.85% + 22014 \* 1.93% +... + 27373 \* 26.19% + 4400 \* 27.48%)/(22725 + 22391 +... + 27373 + 4400)

<span id="_5-同期群分析"></span>
## 5. Cohort analysis

**Cohort analysis:**  that is, users are divided into groups according to the time of initial behavior (i.e. **cohorts).** 


* By comparing users in the same cohort horizontally, the changes of similar groups over time are obtained, and the impact of strategies on the entire life cycle of users is observed.

* Vertical comparison of different cohorts shows whether the performance of the application is getting better and better, thus verifying whether the product improvement has achieved results.


For details, see [Advanced Analysis: Cohort Analysis](https://docs.byteplus.com/docs/DataTester/Advanced-Analysis-Cohort-Analysis).

<span id="四-转化漏斗"></span>
# 4. Conversion funnel

For details, see [Metric Analysis: Funnel Metric Analysis](https://docs.byteplus.com/docs/DataTester/Metric-Analysis-Funnel-Metric-Analysis).

<span id="五-置信度和置信区间"></span>
# 5. Confidence levels and confidence intervals

<span id="_1-置信度"></span>
## 1. The confidence level


* Confidence level (also known as confidence level, confidence coefficient, statistical significance), refers to the probability that there is a real performance difference between the experimental group and the control group, and the difference between the experimental group and the control group is not due to randomness. Confidence levels allow us to understand when the results are correct, and for most businesses, confidence levels above 95% can generally be interpreted as experimental results being correct. Therefore, by default, the "A/B test" sets the confidence level parameter value to 95%.

* In the A/B experiment, we can only do small sample experiments because we can only extract traffic. The distribution of sample traffic will not be exactly the same as the overall traffic, which means that none of the experimental results can be 100% accurate \- even if the data goes up, it may be due solely to sampling error, regardless of our strategy. In statistics, confidence levels exist to describe the reliability of experimental results.


In the process of the experiment, the sample flow we extracted will actually be slightly different from the overall flow, and these differences determine that there will be some "errors" in the conclusions we draw through the experiment.

> For example, in the experiment, I increased the purchase rate by 3% by changing the color of the landing page, but because the sample traffic does not fully represent the overall traffic, it is possible that "my strategy of changing the color was useless, and the purchase rate increased by 3% due to the sampling results."

> So what are the chances of this "my strategy didn't work" event happening? In statistics, we use "significance level (α) " to describe the probability of this event occurring. And confidence level = 1\-α.

> On the "A/B test" platform, according to industry standards, the significance level α is 0.05. In an A/B experiment, if the probability of "my strategy actually didn't work" is less than 0.05, we say the conclusion is "statistically significant/believable." This means that your new strategy has a high probability (greater than 95% in A/B experiments) of being effective. Conversely, if the probability of this event is greater than 0.05, the experimental conclusion is said to be "not significant/unbelievable."


"A/B testing" mainly uses hypothesis testing to calculate the confidence level of the metric. In fact, it is to test a pair of opposing hypotheses: the null hypothesis and the alternative hypothesis.

> A null hypothesis is a hypothesis that the experimenter wants to gather evidence against. The null hypothesis in A/B experiments is that "the new strategy has no effect."

> Alternative hypothesis: A hypothesis that the experimenter wants to collect evidence to support, with mutual exclusion from the null hypothesis. The alternative hypothesis in A/B experiments is that "the new strategy works."


To test a hypothesis by contradiction means using existing data to prove that the null hypothesis is false (false) and that the alternative hypothesis is true (true). This set of methods is known statistically as the null hypothesis significance test.

<span id="_2-置信区间的解读"></span>
## 2. Interpretation of confidence intervals

Mainly through a certain metric or retained experimental version means changing value and confidence intervals to judge whether the experimental version performs better than the control version on the current metric or user retention.


* If the confidence intervals are both positive or negative at the 95% confidence level, the experimental results are statistically significant.

* If the confidence interval is positive and negative at the 95% confidence level, the experimental results are not statistically significant.


<span id="_2-1-统计正向显著"></span>
### 2.1 Statistical positive significance

As shown in the figure below, the change rate of the sample mean in the experimental version compared to the control version is + 17.395%. At the 95% confidence level, the confidence interval is [16.86%, 17.929%], which is statistically significant positive, indicating that the experimental version has been detected to be better than the control version under the current sample size conditions.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/4122988bf4f34c7285b41b170a129790~tplv-em5hxbkur4-noop.image?width=200&height=100) </span>

<span id="_2-2-统计负向显著"></span>
### 2.2 Statistical negative significance

As shown in the figure below, the change rate of the sample mean in the experimental version compared to the control version is \-33.240%. At the 95% confidence level, the confidence interval is [\-33.575%, \-32.906%], which is statistically significant negative, indicating that the experimental version has been detected to be inferior to the control version in the core metrics under the current sample size conditions.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e4776f3fdc7d425caab12187e6b2cdd2~tplv-em5hxbkur4-noop.image?width=376&height=104) </span>

<span id="_2-3-不显著"></span>
### 2.3 Not significant

As shown in the figure below, the change rate of the sample mean in the experimental version compared to the control version is \-0.550%. At the 95% confidence level, the confidence intervals are [\-1.4595%, 0.358%], the confidence intervals are negative and positive, and the experimental results are non\-statistically significant.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ee33d1f5cf514f45ae8a2bf1f4fa6623~tplv-em5hxbkur4-noop.image?width=374&height=84) </span>

<span id="六、下载进组用户id"></span>
# 6. Download the user ID into the group


* In the experimental report page, click on the original number of people entering the group to directly download all the user IDs and corresponding group information, including user ID, experimental name, experimental group, and filter conditions (if any);

* You can download up to 50w pieces of data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50c23024ba0d4f808ce808dae330b81c~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc348482bb3b49d2b9feb69f6b55059d~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f676df5c038f419cbe8a94a4279b9bdc~tplv-goo7wpa0wc-image.image) </span>


<span id="七、指标跳转datafinder"></span>
# 7. Jump Metric DataFinder

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is limited to customers who purchase both DataTester and DataFinder.</div>


<div data-tips="true" data-tips-type="tip">Only the jump of event metrics is supported.</div>


<div data-tips="true" data-tips-type="tip">Only client\-side experimental viewing is supported.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bb61637c1304694aec9b7c71177aad4~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/767cd7b30d0542d4952564530f9fe344~tplv-goo7wpa0wc-image.image) </span>


* When the metric viewing mode is detailed view, click the button [Enter Finder]

* The system will automatically jump to the DataFinder with the selected metric and the properties of the experimental version


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bf20d2fc66f46808950f5ba2f0dac5d~tplv-goo7wpa0wc-image.image) </span>


* When the metric viewing mode is a global view, click the button [Enter Finder].

* The system will bring all the event metrics used in the experiment into the DataFinder event analysis, and select the experimental version information.
