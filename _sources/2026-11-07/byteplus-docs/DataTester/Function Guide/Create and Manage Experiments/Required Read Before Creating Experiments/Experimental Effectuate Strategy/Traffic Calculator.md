---
title: "Traffic Calculator"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Traffic-Calculator"
---

<span id="一-概述"></span>
# Overview

For beginners, there is often a lack of empirical judgment on how much online traffic to allocate when conducting an experiment, which affects the experimental results.

"A/B Testing" provides an experimental traffic recommendation tool that recommends the proportion of online traffic allocation by setting a series of target parameters. Assuming that the new strategy can improve core metrics in real\-world scenarios, using traffic recommendation tools can help users achieve significant results in a single experiment.

<span id="二-为什么开实验时需要先计算实验流量"></span>
# Application scenario


* The larger the experimental traffic, the greater the statistical power, that is, if an experiment has a real improvement in the index, then the sufficient traffic has a higher probability of achieving significant results in one experiment.

* However, for greater statistical efficacy, it is not advisable to use too much traffic in the experiment. The default statistical power is 80% because:

   * **Waste traffic:**  online traffic is precious, usually the same mutual exclusion group will have multiple iterations at the same time, an experiment that occupies 10% of the traffic can meet statistical efficiency, if the traffic is opened to 100% obviously wasted.

   * **If the test/experiment shows negative results, bring unnecessary online losses:**  New strategies are often tested in experiments, and new strategies usually have greater risks than old strategies. If there is a problem, the low\-traffic test has a smaller impact.

   * **Significance is more sensitive, but the actual benefits of the experiment may not equal the cost of the feature:**  Although the results are slightly positive, the experimental ROI is low, which is not good for the product in the long run. It is equivalent to observing the experimental group and the control group with a microscope. They are different after all. If you get a statistical significance of 0.001%, is this really meaningful? Therefore, when starting the experiment, it is recommended that you calculate the required experimental traffic rate according to the expected index income of the experiment, and convert it into the experimental traffic rate according to the MAU. Start the experiment and set the experimental traffic size according to this suggestion.


<span id="三-如何使用"></span>
# Use the traffic calculator

In the second step of the new experiment, "Set the effective policy", click "Traffic Calculator" to pop up the Experiment Traffic Suggestion Tool page, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0dc9c9bb7d914e6d98665e2911efc7ba~tplv-goo7wpa0wc-image.image) </span>

<span id="c40134bc"></span>
## Enter metric information

DataTester will calculate the historical mean for you in advance based on the historical performance of the metric. If it is not possible to automatically generate pre\-calculation results based on recent data, or if you need more flexible configuration of calculation data, you can fill in manually.


* Select Precomputed Metrics

   
   |Parameter |Configuration instructions |
   |---|---|
   |Select metrics |Select the experimental metric in the drop\-down box. You can choose the core metrics and attention metrics of the experiment according to the purpose of the experiment, and use the traffic calculator to estimate the required sample size. The final traffic is taken as the maximum value, so as to ensure that the core metrics and attention metrics of the experiment have enough traffic. |
   |Estimated number of experimental days |The current default is 7 days. |
   |Precomputed data |According to the historical operation of the selected index, DataTester calculates the estimated total sample size, index mean and index variance based on the accumulated data of multiple days.<br><br><br>* Estimated total sample size (cumulative): Estimated test schedule (currently 7 days), the metric calculates the corresponding deduplicate cumulative sample size.<br><br>* metric mean (cumulative): The average of the metrics in the expected test schedule, calculated based on the accumulated data.<br><br>* metric variance (cumulative): The index variance value of the user granularity in the expected test schedule, calculated based on the accumulated data. |
   

* Fill in manually

   
   |Parameter |Configuration instructions |
   |---|---|
   |Metric type |According to the metric type of the follow\-up experiment, select the corresponding metric type. The variance and sample size calculation formulas corresponding to different metric types will be different. Currently:<br><br><br>* Average: cumulative value/number of people, such as amount per person, number of times per person<br><br>* Retention: retention/number of people, also as a uv_ctr, same as uv_ctr formula<br><br>* uv_ctr: the conversion rate of the number of people, for example, the number of people converted/the number of people entering the group<br><br>* pv_ctr: cumulative value/cumulative value, e.g. conversions/clicks<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Summation\-type metrics are proposed to be converted into per capita metrics.</div><br> |
   |Estimated total sample size (cumulative) |The estimated cumulative sample size (number of people entering the group) in the test schedule is actually mainly used to calculate the proportion of "total recommended experimental traffic". |
   |Metric mean (cumulative) |Expect the average of the metrics in the test period.<br><br><br>* Estimate the cumulative mean of the metric over the test period.<br><br>* The cumulative mean of retention metrics can be calculated by splitting them into groups, or they can be estimated directly from the overall retention. |
   |Metric Variance (Cumulative) |The metric variance of the expected user granularity in the test period. See below for more details on metric variance [Reference: related concepts](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator#0093b876). |
   


<span id="df512068"></span>
## Set test accuracy


|Parameter |Configuration instructions |
|---|---|
|Minimal change in expected detection metrics |That is, MDE (minimum detectable effect), which is the sensitivity of the experiment. If an experimental business expects an increase of x%, the MDE can be set to x%, or a smaller value, to obtain the sample size required to verify the increase. Supports setting relative or absolute values.<br><br>A detailed description of MDE can be found in the conceptual reference documentation [Calibration Sensitivity MDE](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator#32f045db)section below. |
|Number of Experimental Versions & Fixed Multiple Comparisons |* Configure according to the number of experimental versions (including control groups) required for subsequent experiments. The range of values is 2 to 20.<br><br>* When the number of experimental versions is more than 2, the metric will increase due to multiple comparisons. At this time, you can turn on the correction multiple comparisons switch. After turning it on, the problems caused by multiple comparisons will be automatically corrected for you. See below for more information on multiple comparisons [Multiple comparisons](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator#1e5ce32a). |
|Default parameters |Default parameters can use platform defaults.<br><br><br>* Statistical power (1\-β): How likely is it to detect version differences. Assuming that the two groups are actually different, what is the probability that the statistical results can detect significance? Default 80%, support adjusting to 50%, 80%, 90%, 99%, 99.99%.<br><br>* Statistical significance (α): the probability that the indifference version is judged to be insignificant. Assuming that there is no actual difference between the two groups, what is the probability that the statistical results will incorrectly give a significant conclusion (i.e. the probability of making a Type I error)? The default is 5%, and 1%, 10%, and 20% are also supported.<br><br>* Traffic filter ratio: refers to `the number of users who can pass the filter conditions /the number of users who do not enter the experimental group without filter conditions`. When not filtered, the traffic rate is 100%.<br><br><br>For more information on statistical power and statistical significance, see [Reference: related concepts](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator#0093b876). |


<span id="acef333f"></span>
## View calculation results


* Sample size required for a single group: Based on the input data related to the metrics you configure, the traffic calculator calculates the sample size required for a single experimental group.

   For example: the metric selects the retention class table, selects 80% statistical efficacy, fills in 1% absolute difference, inputs 100 variance, and finally the sample size output by the calculator is xxxx.

   The implication behind this is that if the retained **true difference (absolute difference A \- B) between AB versions is 1%**  and the variance is 100, and it is hoped that this difference will be detected experimentally with a probability of 80% or more, the required **minimum sample size is xxxx**.

* It is recommended that the total experimental traffic: the proportion of the total experimental traffic = the sample size required for a single group \* the number of experimental groups (including control groups)/the estimated total number of users reached within the experimental time.


<span id="0093b876"></span>
# Reference: related concepts

<span id="a27a6216"></span>
## Index variance

Metric variance, the recent metric variance at the user granularity level in the experimental version.

**How to calculate the index variance?** 


* For metrics of the per value class, such as pv/uv, you can calculate the variance of the metrics using the SQL standard function (click [here ](https://www.w3resource.com/mysql/aggregate-functions-and-grouping/aggregate-functions-and-grouping-std().php)for MySQL help instructions).

   ```SQL
   select  STD(total_cost)** 2
   from purchase_table
   group by user_id;
   ```
   

* pv_ctr class of metrics, for example, pv_ctr = sum(y)/sum(x), x and y need to have been aggregated by user granularity, such as sum(read)/sum(impr), you can calculate the metric variance according to the following formula:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e0fedf58b3e4dc4898710a1e6d1f272~tplv-goo7wpa0wc-image.image) </span>

   The expectation (μ), variance (var), and covariance (cov) of x and y are replaced by the sample mean, sample variance, and sample covariance between impr and read, respectively.


<span id="32f045db"></span>
## Calibration Sensitivity MDE


* **What is MDE:**  Minimum Detectable Effect (MDE), that is, test sensitivity, is a metric diff amplitude that can be **effectively detected** by experiments **under current conditions**.

   * Current conditions refer to the current sample size, metric value, and metric distribution, and assume that the sample variance is close enough to the overall metric variance.

   * Valid detection, indicating a detection probability greater than or equal to 80% (type II error less than or equal to 20%).

* **What MDE can be used for:**  By comparing the target improvement rate of the metric MDE and the metric to determine whether the insignificant metric conclusion is credible, the experiment can be avoided in the case of insufficient sensitivity, to end prematurely by making non\-significant conclusions, resulting missing potential features.

   Suppose your expected target improvement rate for a metric is 1%.

   * If MDE = 0.5% at this time, MDE < the expected improvement value, in the case of statistical insignificance, indicating that the metric change is really not significant, please combine business ROI and other dimensions such as user experience, long\-term strategic value, etc. to comprehensively judge whether it is worth going online;

   * If MDE = 2% at this time, MDE \> the expected increase value, indicating that the current minimum difference that can be detected as significant is 2%, which cannot be detected due to insufficient sensitivity (i.e., calibration effectiveness). In this case, it is recommended to increase the sample size, such as expanding the traffic and observing the accumulation of more users over a period of time. There is still a possibility of confidence in the metric.

* **How to set it:**  The smaller the MDE, the higher the sensitivity you require for the test and the larger the sample size required.

   * If the MDE setting is too detailed, not only will unnecessary traffic be wasted, but the actual benefits may not make up for the development and promotion costs of the new strategy.

   * Insufficient sensitivity (e.g. 1% is expected to meet the standard, but the experimental sensitivity can only detect 5% or more) may lead to missing potential features.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Usually the experimental metric is to increase/decrease the value of xx (a certain business metric value), then the MDE is recommended to be less than this metric value for estimation, so as to avoid the MDE value being too large to detect the real experimental results.   </div>
   

<span id="4b4636d8"></span>
## Statistical power (1\-β)

<span id="e5d330da"></span>
### **Sampling error**


* In order to avoid the impact of the wrong strategy on users as much as possible, we will only take a small proportion of the overall traffic when conducting experiments. Therefore, there is a sampling step in A/B experiments. Although we try our best to keep the sample traffic and the overall traffic distribution consistent, sampling errors are inevitable. This means that we can't test the "null hypothesis" and "alternative hypothesis" with 100% accuracy by sampling data.

* With the help of statistical theory, we can learn what mistakes we are likely to make during testing, and how likely we are to make mistakes. Statistics tell us that in the process of hypothesis testing, we can make two kinds of errors, which are called type I errors (discarding truth) and type II errors (taking falsification).


<span id="16fd5e29"></span>
### Type II error

The second type of error refers to the null hypothesis being wrong (false), but the conclusion of our hypothesis test shows that "the null hypothesis is correct (true) and the alternative hypothesis is wrong", in the process we accept the wrong (false) null hypothesis, **so the second type of error is "taking falsification"** .


* In practice, it shows that my new strategy actually works, but the experiment failed to detect it.


In statistics, we use β to describe the probability that an experimenter will make a Type II error.

<span id="4b6ed774"></span>
### Statistical power

Statistical power = 1 \- probability of type II error (β), statistical power is expressed in reality as: If my new strategy is effective, how likely am I to detect it in experiment.

<span id="47e6e7e0"></span>
## Statistical significance (1\-α)

<span id="458a6e15"></span>
### Type I error

From the above, it can be seen that there is inevitable sampling error in A/B experiments. We put \- the null hypothesis is correct (true), but the conclusion of our hypothesis test shows that "the null hypothesis is wrong (false), the alternative hypothesis is correct" \- such errors are defined as the first type of errors. In the process, we reject the correct (true) null hypothesis. **So the first type of error is "discarding truth"** .


* In practice, it appears that the experimental conclusion shows that my new strategy is effective, but in reality, my new strategy is ineffective.


In statistics, we use the significance level (α) to describe the probability that an experimenter will make a Type I error.

When the metrics of a certain experimental group are significant, it indicates that the experimental results are reliable to a certain extent. For example, the significance level is 95%, which means that the system has 95% confidence that the experimental result is accurate.

<span id="147146fe"></span>
### Statistical significance

Statistical significance = 1 \- Probability of Type I error (α), also known as "confidence, confidence level, confidence coefficient", existing to describe the reliability of experimental results.

"A/B Testing" sets the default value of the confidence level parameter to 95%, and group management and app administrators can adjust it according to their needs in "System Settings \- Confidence Level".

<span id="2d397191"></span>
### Meaning of significance level

For example, if a button changes from blue to red and a window moves from left to right, will the user experience get better or worse? We're not sure, so we're trying to transform this uncertainty by using A/B experiments, monitoring how old and new strategies perform in low\-traffic tests to determine their strengths and weaknesses.

But would that eliminate the uncertainty entirely?

The answer is no, because of sampling error. For example, if the average income of people in country X is ten times that of country Y, then randomly selecting three X people and three Y people can guarantee that the average income of these three X people in the sample is ten times that of three Y people? Obviously, the answer is uncertain. It is possible that the three Y people randomly selected are the top three richest people in Y country. This error caused by sampling is the sampling error.

On the other hand, suppose that at 1% of the traffic, Group A (buttons are red) has a higher purchase rate than Group B (buttons are blue), and expanding the traffic to 100% guarantees that Strategy A will still perform better than Strategy B? \- Apparently the answer is still uncertain.

The uncertainty caused by sampling error makes it impossible to guarantee that the conclusion is completely correct when doing a low\-traffic test. Fortunately, for the uncertainty of sampling, in statistics, we have a way to quantify the degree of uncertainty.

<span id="1e5ce32a"></span>
## Multiple comparisons

A/B experiments based on hypothesis testing are suitable for scenarios where two groups of A and B are compared, which can help you choose a better one between strategy A and strategy B: at a 95% confidence level, assuming that the new strategy is useless, if we do a comparison, the probability of making the type I error (that is, my strategy is useless, but the experimental conclusion shows that my strategy is useful) is 5%. But if the experiment is an AABB experiment, or an ABCD experiment, or an ABCDEFG experiment, etc., then the situation is very different \-\- we will face multiple comparison problems: when there are more than two groups, the probability that we are wrong increases greatly, no longer 5%.

Take the ABCD experiment as an example: assuming that there is no significant difference between strategies A, B, C, and D, we compare ABCD in pairs, with a total of 6 combinations, and 6 comparisons are required. As long as one of the six comparisons is wrong, our conclusion is wrong, so the probability of error for each statistical metric becomes **1\- (1\-5%) ^ 6 = 26.5%**  , **much greater than 5%** .

Another thing to note is that the hypothesis test uses "AB is not significantly different" as the null hypothesis, and the p\-value obtained by B relative to A does not mean that the probability that B is better than A is 1\- (p\-value). It is precisely because of this that when there are multiple comparisons (especially when there is no obvious difference or even equivalence between groups of policies), hypothesis testing is difficult to provide a criterion for judging which policy is the best. The above two questions greatly increase the difficulty of assessing who is better at ABCD and the risk of making wrong decisions.

Overall, hypothesis testing does not work in a "multi\-group meritocracy" scenario, and cannot tell you who is better or at greater risk of making mistakes.
