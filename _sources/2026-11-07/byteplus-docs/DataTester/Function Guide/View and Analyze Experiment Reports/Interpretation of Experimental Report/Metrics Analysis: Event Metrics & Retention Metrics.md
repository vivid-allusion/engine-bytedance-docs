---
title: "Metrics Analysis: Event Metrics & Retention Metrics"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Metrics-Analysis-Event-Metrics-Retention-Metrics"
---

<span id="9499c525"></span>
# Event metrics


1. Log into the A/B test console.

2. In the left navigation bar, select **A/B Testing** \> **Experiment List**.

3. Select the specified experiment in the experiment list to enter the experiment details page.

4. On the experiment details page, click the **data metrics** tab and select **event metrics** on the left side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52462b8b5ae94f93bd179629cc3aca61~tplv-goo7wpa0wc-image.image) </span>

5. Select the specified metric on the left side of the page and complete the following configuration to query.

   
   |Configuration item |Description |
   |---|---|
   |Set query time period |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35fe29f991cf488397c22fc19d9dea43~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. Choose **from start\-to\-date accumulation**, **flexible accumulation**<br><br>   * **Start\-to\-date accumulation**<br><br>      * Number of users entering the group: accumulated from the first day of the experiment to the current date<br><br>      * Other metrics: cumulative by filter time<br><br>   * **Flexible accumulation**<br><br>      * Number of incoming users: accumulated by filter time<br><br>      * Other metrics: cumulative by filter time<br><br>2. Select **day level**, **hour level**, **5 minute level**<br><br>3. Specify a specific time period. |
   |Attribute filtering |Build an attribute filter by selecting an attribute, adding a condition, and setting a range of values.<br><br><br>* Click **Add and condition** to add multiple attribute filter conditions, and the relationship between multiple conditions is and.<br><br>* Click **Add cluster** to add a user cluster as a filter condition, and the relationship between it and other conditions is and.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4953c13e8e844a9fae0e5d519c71904c~tplv-goo7wpa0wc-image.image) </span> |
   |Attribute grouping |After selecting the specified attribute, the query results will be displayed in groups according to the different values of the attribute. For example, if the attribute group selects a city, the query results will be displayed in groups according to cities such as Beijing and Shanghai.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53626d0be012409b80a4fc85edee3d9f~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Switching preAA data, viewing data distribution, and box plots are not supported after attribute grouping.</div><br> |
   

6. Click **Query** to see the view.

   See below for a detailed description of the various types of views.


<span id="12ff4e5e"></span>
## Metric group view

Experimental metrics support viewing data in a single metric or metric group dimension. In the metric group view, the **metric value** of the control group will be displayed, as well as the **change rate** and confidence interval of the metrics of each experimental group relative to the control group. You can view the details of the metrics by hovering the confidence interval

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c3f5601345b48feaf9fda0355be8d7d~tplv-goo7wpa0wc-image.image) </span>

<span id="fdb47dd7"></span>
## Metric View

Experimental metrics support viewing data in a single metric or metric group dimension. The single metric view displays information such as the number of people entering the group, the metric value, the diff value of the experimental version relative to the metric, and the relative change and confidence interval. It also supports viewing sky\-level trends, probability distributions, and box charts, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44cff0f03c5a4fb3a031545d91a3486b~tplv-goo7wpa0wc-image.image) </span>

<span id="b755abae"></span>
### Time trend

According to the time granularity of the experimental report, the "sky\-level trend", "time\-level trend" and "minute trend" of a certain metric are displayed. Take "Sky Trends" as an example:


* You can view the actual value and p\-value of the metric for the day, as well as the range of values for the day. The daily average defined caliber is the metric performance of all current users who have entered the group on that day, not the new users who entered the group on that day.

* When you open the "Range Display", a range appears, which produces an overlapping effect and shows how the range of core metrics has changed over time for each version.

   * Ideally, the range would decrease over time and be reflected in the diagram.

   * If the range is expanded, it indicates fluctuations in the data.

   * If the ranges overlap, it means you are unsure which version works better.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/024b3e65e80540d4a4baca5eb9c2981d~tplv-goo7wpa0wc-image.image) </span>


<span id="fb09ca98"></span>
### **Probability distribution**

The probability distribution shows the value of the index and the probability distribution of its occurrence. The horizontal axis is the index value, and the vertical axis is the probability density of the index value. The distribution of the index is reflected by the mean and variance. Comparison of the probability distribution of the experimental group and the control group can assist in judging the difference between the experimental group and the control group.


* The default control version uses gray, while other versions use color.

* On the normal distribution curve of different experimental versions, the mouse hover will display the information of "number of entrants, p\-value, metric variance, MDE, confidence interval" for each version.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/279fdaee921b41d49883438390340ff6~tplv-goo7wpa0wc-image.image) </span>

<span id="0e12f6c4"></span>
### Distribution analysis(Box Plot)

Box and whisker snapshot, also known as box graph, is the maximum, minimum, median and two quartiles of the data, reflecting the distribution characteristics of the original data source. By comparing the box whisker snapshots of the experimental group and the control group, the distribution characteristics of the two groups of data can be compared.

Application Note:


* For per capita type (PV/AU, PV/UV, SUM/AU, SUM/UV), PV type, SUM type, CTR click through rate type, PV/SUM & SUM/PV/SUM & PV/PV/PV and other types of metrics are applicable.

* The "CVR conversion rate type" does not currently support box whisker diagrams because it is a binary value for a single individual (i.e. only 0 or 1).

* Hour\-level/minute\-level granularity display, no box whisker diagram is provided.


Overlapping area description: The shaded areas of each color are the overlapping areas corresponding to the experimental group and the benchmark group. The overlapping areas represent the experimental versions with overlapping parts. The metrics perform similarly, and it is impossible to determine which version works better. If your best\-performing version has a lot of uncertainty overlap, we recommend that you adjust the running time of the experiment to a longer one.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c07d5c0b8554a1fb77dd5c3ade4f4aa~tplv-goo7wpa0wc-image.image) </span>

<span id="65d83bfb"></span>
# Retention metric


1. Log into the A/B test console.

2. In the left navigation bar, select **A/B Testing** \> **Experiment List**.

3. Select the specified experiment in the experiment list to enter the experiment details page.

4. On the Experiment details page, click the **Data metrics** tab and select **Retention metrics** on the left side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7e1b134871e4ea8a35916783437d9e6~tplv-goo7wpa0wc-image.image) </span>

5. Select the specified metric on the left side of the page and complete the following configuration to query.

   
   |Configuration item |Description |
   |---|---|
   |Set query time period |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35fe29f991cf488397c22fc19d9dea43~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. Choose **from start\-to\-date accumulation**, **flexible accumulation**<br><br>   * **Start\-to\-date accumulation**<br><br>      * Number of users entering the group: accumulated from the first day of the experiment to the current date<br><br>      * Other metrics: cumulative by filter time<br><br>   * **Flexible accumulation**<br><br>      * Number of incoming users: accumulated by filter time<br><br>      * Other metrics: cumulative by filter time<br><br>2. Select **day level**, **hour level**, **5 minute level**<br><br>3. Specify a specific time period. |
   |Attribute filtering |Build an attribute filter by selecting an attribute, adding a condition, and setting a range of values.<br><br><br>* Click **Add and condition** to add multiple attribute filter conditions, and the relationship between multiple conditions is and.<br><br>* Click **Add cluster** to add a user cluster as a filter condition, and the relationship between it and other conditions is and.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4953c13e8e844a9fae0e5d519c71904c~tplv-goo7wpa0wc-image.image) </span> |
   |Group comparison |Support adding multiple groups, and set attribute filter conditions for groups to compare groups.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ca0e17907dc4e76864e951f7894798b~tplv-goo7wpa0wc-image.image) </span> |
   |retention caliber |Select the **starting event** and **return visit event** to query respectively, and support adding multiple filter conditions. |
   

6. Click **Query** to see the view.

   See below for a detailed description of the various types of views.


<span id="ddcd0631"></span>
## Cohort retention trend

Cohort retention trend refers to splitting experimental users into the date they first entered the experiment, and observing the subsequent retention trends of users who first entered the group on different days. Cumulative trend graphs for sub\-groups are supported, and sky\-level trend graphs from 1\-day retention rate to 30\-day retention rate are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dd20ee5367842c49791b0b2f413c025~tplv-goo7wpa0wc-image.image) </span>

<span id="fb07a9e8"></span>
### N\-Day Retention Day Trend

Represents the Nth\-day retention trend for users who entered the group within the filter timeframe.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be714b33884a497cbceef86cd8025d51~tplv-goo7wpa0wc-image.image) </span>

<span id="0af1c3b6"></span>
# Common problem

<span id="c981fd92"></span>
## **The retention rate is the default configuration of the system. How to calculate the retention rate?** 


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


<span id="dbaa8aee"></span>
## **How to calculate detailed data for each experimental version of "Cohort Retention Trends" every day?** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/675a9b951c564d6d86083a804f4546cc~tplv-goo7wpa0wc-image.image) </span>

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


1 day later: 4.99% = (23941 \* 1.60% + 23551 \* 1.70% + 23160 \* 1.82 % + … + 27373 \* 30.55% + 4400 \* 30.93%)/(23941 + 23551 + … + 27373 + 4400)

4 days later: 5.42% = (22725 \* 1.69% + 22391 \* 1.85% + 22014 \* 1.93 % + … + 27373 \* 26.19% + 4400 \* 27.48%)/(22725 + 22391 +... + 27373 + 4400)
