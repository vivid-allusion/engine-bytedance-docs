---
title: "System Settings"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/System-Settings"
---

In the System Administration \- System Settings module, BytePlus A/B Testing provides you with the ability to set up [Experiment Creation/Editing], [Confidence Level], and [System Tips]. If the parameters in the system settings are successfully set, it will take effect on the new experiment in the current application and the experiment in the history of "draft + debugging + running", and the history of "ended" will not change.

<span id="二-功能介绍"></span>
# Function introduction

<span id="_1-实验创建-编辑"></span>
## 1. Experiment creation/editing

<span id="_1-1-支持去除被动事件"></span>
### 1.1 Support for removing passive events

In BytePlus A/B testing, the experimental entry conditions can be distinguished by [Active Arbitrary Events and Passive Events], and you can set [Passive Events] to not be used as the entry criteria to make the experimental data meet your real business situation.

You can set the option of [Incoming users remove passive event triggering conditions], the system defaults to "No", if changed to "Yes", users who only trigger passive events will be excluded from the incoming users.

For active and passive events, please refer to: [Passive and Relational Events](https://docs.byteplus.com/docs/DataTester/Passive-and-Relational-Events).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25703e2788cf4d5193e5612c0a08ec36~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-2-置信水平"></span>
### 1.2 Confidence level

<span id="_1-2-1-置信水平概述"></span>
#### 1.2.1 Confidence Levels Overview

Confidence level (also known as confidence level, confidence coefficient, statistical significance), refers to the probability that there is a real difference in performance between the experimental group and the control group, and the difference between the experimental group and the control group is not due to randomness. Confidence levels allow us to understand when the results are correct, and **for most businesses, generally speaking, a confidence level higher than 95% can be understood as the experimental results are correct.**  **Therefore, by default, the "A/B Test" product sets the confidence level parameter value to 95%, and you can also set it on demand.** 

In the A/B experiment, since we can only take a small sample of the traffic, the distribution of the sample traffic will not be exactly the same as the overall traffic. As a result, none of the experimental results can be 100% accurate \- and even if the data goes up, it may be due to sampling error alone, regardless of the strategy we adopted. In statistics, the **confidence level exists to describe the reliability of experimental results.** 

<span id="_1-2-2-置信水平与实验结果"></span>
#### 1.2.2 Confidence level and experimental results

The experimental results need to be evaluated from two aspects: the first is the rise and fall of the data results; the second is to determine whether the data results can be trusted, that is, whether the results are "significant".

**How can we understand whether the data is significant?** 


* An A/B experiment is a low\-traffic test where we need to take a certain amount of samples from the overall traffic to verify whether the new strategy is effective. During the sampling process, the sample does not fully represent the whole. The uneven distribution of the sample leads to a situation where the experimental results may be \- "the strategy I took didn't work, but the experimental results show that the strategy worked".

* Statistics tells us that such errors cannot be completely avoided, but we can use some statistical methods to calculate the probability of such errors occurring in the process of obtaining the results of experimental data. In other words, we can determine what percentage of our experiments are reliable.


According to the accepted standards in the industry, in A/B experiments, if the experimental data results are statistically reliable with a probability of more than 95%, we shall say that the data results are significant. Such data can be used to determine whether the experimental hypothesis is valid.

<span id="_1-2-3-使用场景"></span>
#### 1.2.3 Usage case

**The confidence level parameter value can be understood as a standard and a threshold. In the same experiment, the higher the threshold, the fewer significant indicators, and the lower the threshold, the more significant indicators. The higher the confidence level parameter value is, the more reliable the experimental results are.** 


* If you want to increase the number of significant indicators, you can set a lower confidence level parameter value, but the reliability of the experimental results will decrease.

* If you want to increase the credibility of the experimental results, you can set a higher confidence level parameter value, but the fewer significant indicators will be.


<span id="_1-2-4-如何操作"></span>
#### 1.2.4 How to operate

The default confidence level parameter value of BytePlus AB test is 95%. You can set it as needed. The parameter values that can be set are 99%, 95%, 90%, 80%. Click on the percentage number and save it.


* Permissions: Only group administrators and app administrators can set this parameter value.

* Description: If the confidence level parameter is successfully set, it will take effect on the new experiment in the current application and the experiment in the history of "draft + debugging + running". The history of "ended" will not change.


As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0f837b6264f4280914192c6e7d63c74~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-3-系统设置"></span>
### 1.3 System Settings

In the system settings, you can set the maximum number of metrics supported for a single experiment, up to a maximum of 1000.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7483af7d1fb428e92b5147ef8e2d16a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-系统提示"></span>
## 2. System prompt

BytePlus AB testing supports you to customize the no\-permission prompt information. You can prompt and guide users/colleagues who do not have permission by modifying the copy. The specific location is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae032bd837834d43bf4becaf526496b4~tplv-goo7wpa0wc-image.image) </span>

<span id="d82b7ef5"></span>
## 3. Open Settings in a new tab of the browser

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f58f4c0ae7544edb264d319647b684d~tplv-goo7wpa0wc-image.image) </span>

Configure whether a new page needs to be opened when each list page enters the data page.
