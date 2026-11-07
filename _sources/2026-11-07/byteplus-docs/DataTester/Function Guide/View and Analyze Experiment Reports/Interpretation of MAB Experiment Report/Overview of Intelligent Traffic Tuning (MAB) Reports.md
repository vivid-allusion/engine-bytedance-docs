---
title: "Overview of Intelligent Traffic Tuning (MAB) Reports"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Overview-of-Intelligent-Traffic-Tuning-MAB-Reports"
---

<span id="_1-术语表"></span>
# 1. Glossary


* **MAB experiment revenue improvement:**  MAB(Multi\-Armed Bandit) intelligent tuning experiment compared to the average split ordinary A/B experiment, the overall improvement ratio of core metrics.

* **Probability of becoming the best group Probability\-to\-beat\-all (P2BA):**  The probability of winning this version relative to all versions, the calculation logic is to use the Monte Carlo method to calculate the probability of winning each group.

* **Metric Distribution Interval Estimate:**  Shows the range of the probability distribution of random changes in the core metric, i.e. all tuning rounds under the metrics 25, 50 (i.e. median) and 75 points check point.

* **Experimental traffic allocation:**  The proportion of traffic assigned by the MAB algorithm to each version during each round of tuning.

* **Evaluate traffic:**  Take a portion of the total traffic for normal AB test, and the data results are used for algorithm tuning and revenue calculation.


<span id="_2-报告概览"></span>
# 2. Overview of the report

<span id="_2-1-mab实验整体收益提升"></span>
## **2.1 Overall revenue improvement of MAB experiment**

Conventional experiments pay more attention to the selection of the winning group, while MAB experiments pay more attention to the optimization of the core metrics **on the overall flow** during the entire experiment. Therefore, in the MAB report page, overall earnings improvement is given top priority as the most important part.


* Cumulative return: The return of the core metrics increases when doing the MAB experiment compared to the average diversion to each experimental version.

   * Revenue Summary: Shows the improvement in target optimization metrics by the deadline.

   * The abscissa refers to the tuning time, and the ordinate is the cumulative improvement value of the core metrics. You need to see the specific time of each round of adjustment and the improvement value of each node. You can move the mouse into the line chart to show it.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a64018eb2fa4717befe4d7a50a30cc1~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf4a00fd11704901a155241b04b5b43b~tplv-goo7wpa0wc-image.image) </span>

* Detailed benefits: Focusing on the proportion of each new user entering the group, its core metrics will increase in the current round.

   * The abscissa refers to the tuning time, and the ordinate is the cumulative improvement value of the core metrics. You need to see the specific time of each round of adjustment and the improvement value of each node. You can move the mouse into the line chart to show it.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/005b0edd0b7b4da8b04987e704766842~tplv-goo7wpa0wc-image.image) </span>

* Intelligent tuning of processes and assessment of traffic metrics trends

   * The horizontal axis refers to the tuning time, and the vertical axis refers to the core metric

   * The green curve is the index trend of the intelligent optimization flow group, and the gray curve is the index trend of the evaluation flow group, which can be displayed by moving the mouse into the line chart.

      Note: The data displayed on the front end is accurate to 4 decimal places

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c03dd69b6714468ae6b4a005c7c5b4d~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-核心指标明细表"></span>
## **2.2 List of core metrics**

In the current version, the MAB experiment provides core metric data. Here are the details of the core metrics in each experimental group, and the table shows the cumulative data.


* Metric value: the current cumulative value of the core metric

* Number of incoming users: The number of incoming users accumulated in this experimental version

* Probability of being the best group: the probability that this version will win against all versions


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74e692b9bc6d4ed29036a019bdf267ce~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-核心指标明细图"></span>
## **2.3 Detailed chart of core metrics**

The detailed chart of the core metrics shows the changes of the core metrics in each round of tuning, divided into absolute trends and relative trends.


* **Absolute Trend:**  Shows how the metric has changed over time, with each tuning, and the 95th percentile range (shaded).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e508a4bc5f9b49359ca95574d9ee56f1~tplv-goo7wpa0wc-image.image) </span>

* **Relative trend:**  Based on version 1, analyze the trend chart of the core metrics in each tuning result of all versions relative to version 1 over time. The metrics include the 95th percentile interval (shaded part) of the improvement ratio and improvement degree of the metrics according to the round comparison.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b1acccef9e245b69a5540b361b5f934~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-4-实验流量分配"></span>
## **2.4 Experimental traffic allocation**

Shows the distribution of flow over time after each adjustment. Used for traffic monitoring and observation.


* **Accumulated data:**  show the traffic ratio of each group of traffic participating in intelligent tuning from the beginning of the experiment to the present, and move the mouse into the chart to query the distribution of the cumulative traffic ratio in each round of intelligent tuning experiment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b577364cac0b43149ce6cf342d842eff~tplv-goo7wpa0wc-image.image) </span>

* **Detailed Data \- Actual Allocation:**  Shows the proportion of traffic actually participating in intelligent tuning online at a certain time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8208fa4f6547470e976e227e52af8ea1~tplv-goo7wpa0wc-image.image) </span>

* **Detailed data \- theoretical allocation** : More used for algorithm/technical monitoring and troubleshooting problems, showing the weight ratio given by the algorithm for a certain time line.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98389741dfdd423c99929e46a5163ccd~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-报告解读"></span>
# 3. Interpretation of the report

<span id="_3-1-核心指标明细图与流量分配之间的关系"></span>
## 3.1 Relationship between core metrics and traffic allocation

In the absolute trend chart of the core metrics at time t, the size relationship between the version metrics corresponds to the traffic distribution at time t on the traffic distribution chart. The larger the version of the core metrics at time t, the more traffic will be presented on the traffic distribution chart at time t.

<span id="_3-2-流量最高的实验版本与版本优胜"></span>
## 3.2 The experimental version with the highest traffic and the winning version

Under the current version, the experimental version with the highest traffic is not necessarily the optimal version, but the high probability is the sub\-optimal and optimal version. The longer the experiment time and the more samples, the more likely the version with high traffic is to be the optimal version.
