---
title: "How to Interpret the Experiment Report"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/How-to-Interpret-the-Experiment-Report"
---

This document will follow the analysis logic of the "A/B testing" experiment report and gradually explain to you: what are the statistics on the "A/B testing", how to look at them, what to do in case of insignificant situations, and how to write an experiment report.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The number of participants in the experiment was counted in real time on the day of the experiment. After the second day of opening, it will be updated according to the T\-1 daily day level, and the specific criteria is the cumulative number of people entering the group in the experiment as of 0:00 on the day.</div>


<span id="一-为什么要用多天累计数据评估实验"></span>
# 1. Why use multi\-day cumulative data to evaluate experiments?


* First of all, the number of users accumulated over multiple days, that is, the number of users accumulated into groups and **deduplicated** during the experiment period, the cumulative users can better ensure that the samples of each group are "homogeneous and comparable" than the users of a single day;

* Secondly, the multi\-day accumulation makes the experiment obtain more samples, which means that with the progress of the experiment, the test sensitivity of the experiment is constantly improving, and it is easier to detect the significance of the affected metrics than the multi\-day average.

* At the same time, the index calculated statistically according to the multi\-day accumulation logic can directly calculate the confidence level of the index change rate during the experiment, and the experimental conclusion is more scientific and reliable.


<span id="二-解读多天累计数据报告"></span>
# 2. Interpreting multi\-day cumulative data reports

In the new feature project stage, I presume that the students have made very clear the optimization goals and evaluation metrics of the feature, and designed experiments based on this goal and evaluation criteria while developing the feature. I want to verify your answer through A/B experiments: Is my feature effective? And if so, how much of an improvement in the target metric?

<span id="_1-确定评估指标"></span>
## 1. Identify evaluation metrics

Since you want to obtain qualitative and quantitative answers through A/B experiments, it is natural to develop your evaluation criteria according to the optimization goals of your features before evaluating the experiment: the evaluation metrics and expected improvement value of the experiment, that is, the new feature has a direct or indirect causal relationship with it, and the expected impact. Instead of being foolish and doing the experiment and completely judging by the data results.

In "A/B Testing", you can set the "core metrics" for a certain experiment and the "must\-see metrics" for each experiment.


* Core metrics: "direct effect metrics" or "success metrics" used to determine whether the experimental function meets expectations. For example, in an experiment on copy optimization of a guide page button, the "conversion rate" of the button click can be used as a decision\-making metric for the experiment.

* Must\-see metrics: Business line metrics that must be guarded. Experimental functions may not have a direct causal relationship with them and cannot directly improve them, but generally they cannot have a significant negative impact on them.


<span id="_2-分析指标的数据表现"></span>
## 2. Analyze the data performance of the metrics

<span id="_2-1-何时来看？"></span>
### 2.1 When is it suggested to see it?

In general, we recommend running the experiment for at least a full natural cycle (7 days) before observing the data, of course the test schedule depends on the duration of the experiment to produce results.

For example, features that are more sensitive to the impact of metrics and can see immediate results in a short time (such as some recommendation strategies) can obtain experimental results faster; while some experimental features designed to improve long\-term retention require longer test schedules to evaluate the effect.

<span id="_2-2-有哪些数据？"></span>
### 2.2 What data is available?

The following detailed view is taken as an example, and the following basic information is provided in the data report shown in the figure below, which can help us understand the basic situation of metric changes:


* Number of participants: The number of participants in this experimental version.

* Absolute value: The absolute value of the metric in each group.

* Absolute difference: The absolute difference between the current experimental version and the baseline (control) version.

* Difference Relative Value: The absolute difference/baseline value between the current experimental version and the baseline version (control version).

* Confidence interval: An estimated interval for a population parameter composed of sample statistics.

* P\-value: The probability of extreme cases in a randomly selected sample, provided that the null hypothesis is true. When the p\-value < 1 \- confidence level is considered statistically significant.

* MDE: Minimum Detectable Effect Minimum Detectable Effect, which can effectively detect the diff of the confidence level under current conditions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a99d5897ea8458e888ae4e2278be3c4~tplv-goo7wpa0wc-image.image) </span>

It also supports viewing probability distributions, box snapshots, and sky\-level trends, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/915124b3be0f43ac888b03f8c4322f29~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-指标变化符合预期吗？"></span>
### 2.3 Is the metric change in line with expectations?

Compare it to your expected improvement:


* If it does not meet expectations, whether the ROI is worth it requires a comprehensive business assessment.

* If it meets expectations, continue to evaluate the credibility of the results.


<span id="_2-4-指标提升是显著的吗？"></span>
### 2.4 Is metric improvement significant?


* **Qualitative judgment:**  To make it easier to judge, the "A/B testing" directly gives the significance in the data table with base color. Green means that the metric is positively significant relative to the control group, red is negatively significant, and black is insignificant.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2825622b7f0a49f098064047bcd848f1~tplv-goo7wpa0wc-image.image) </span>


* **Quantitative analysis:**  If you want to know the quantitative confidence level, you can click on the grid where the data is located to wake up the statistical card, and perform quantitative analysis by P\-value size and confidence interval.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b0e265c034a4b059ac0673b52dc33b5~tplv-goo7wpa0wc-image.image) </span>

**No.1 Level of confidence**


* The P\-value shows the probability of making the first type of error in this experiment. Generally, we will make the probability of making the first type of error less than the significance level (usually take the significance level α = 0.05), that is, when the p\-value < 0.05 is statistically defined as significant, the confidence level is (1\-significance level) = 95%.

* The smaller the p\-value, the more reliable it is. For metrics with significant differences, the confidence of P\-value = 0.01 is higher than that of P\-value = 0.05.


**No.2 Confidence interval**

The confidence interval [16.801%, 23.297%] in the statistical card above gives the interval estimate of the expected change of the metric after the experimental group goes online, and the interval estimate is more likely to cover the true value of the relative change of the metric (assuming that after 100 experiments, 95 of the calculated confidence intervals contain the true value).


* Confidence intervals can be interpreted simply but loosely as follows: assuming the strategy rolls out 100%, you are 95% sure that you will see the true metric return in the range [16.801%, 23.297%].

* The narrower the confidence interval, the higher the confidence.


<span id="_2-5-不显著怎么办？"></span>
### 2.5 What should I do if it is not significant?

What if the metrics I focus on are not significant? Is the feature really useless? Don't worry, there might still be a reversal. Especially in the following situations, don't rush to conclusions:


* The total experimental sample is relatively small

* Low penetration rate of user behavior corresponding to metrics

* The experiment duration is short

* Metrics are not sensitive to experimental function.


**How is MDE used?** 

By comparing the index **MDE and the target improvement rate of the index to** determine whether the insignificant conclusion is solid, the experiment can be avoided in the case of insufficient sensitivity to make a non\-significant conclusion prematurely and end, missing potential features.

Suppose your target improvement rate for this metric is 1%.


* If MDE = 0.5% at this time, **MDE < expected improvement value**, indicating that the metric change is really not significant, please combine business ROI and other dimensions such as user experience, long\-term strategic value, etc. to comprehensively judge whether it is worth going online;

* If MDE = 2% at this time, and **MDE \> expected increase value**, it means that the minimum difference value that can currently detect significance is 2%, which cannot be detected due to insufficient sensitivity (that is, verification effectiveness). In this case, it is recommended to increase the sample size, such as expanding the traffic and observing the accumulation of more users over a period of time. There is still a possibility of confidence in the metric.


<span id="_3-解读指标变化原因"></span>
## 3. Interpret the reasons for the changes in the metrics

Getting the data results is actually only 80% complete. What's more important is to explore the unknown between the real data and your hypothesis through A/B experiments.


* If the data is growing, is the real reason consistent with your expectations?

* If there is no effect or even worse, have you found the problem and cause, and how to optimize it next?


At this point, business students need to conduct further analysis of the experimental data, such as multi\-dimensional drill\-down analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94026336060940959bad9d26b12c393b~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-实验结论"></span>
## 4. Experimental conclusions

In the experimental overview area, "A/B testing" is based on hypothesis testing theory to provide conclusive inferences about the comparison of experimental results. As follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32b5171dc5744c178cd40f40750222b2~tplv-goo7wpa0wc-image.image) </span>

If there is no conclusion, it is actually a conclusion. It can only mean that the test sensitivity under the current time, number of users, etc. cannot verify the difference. The increase in the index during the experiment period does not represent the increase after rolling out 100%.


* Testing can only determine whether there are significant differences, but cannot guarantee the magnitude of the differences. Roll out 100% and the time variable is actually inconsistent during the experiment.

* We can only assume that if the sample size is large enough, the statistical value is close to the "true value" (the law of large numbers).


Do not be limited to data, user feedback, user research, vendor evaluation, can assist in judging the value of features, experiments are just a way to avoid turning AB test reports into statistical reports, for the gain of features, it is necessary to refine the disassembly research and understand its deep\-seated reasons.

<span id="三-相关视频"></span>
# 3. Related videos

<video src="https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/44f54d76e25b42b282de20da1fed125d.mp4" controls></video>
