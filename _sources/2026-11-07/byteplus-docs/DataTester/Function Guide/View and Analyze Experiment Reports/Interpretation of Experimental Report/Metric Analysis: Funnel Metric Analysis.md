---
title: "Metric Analysis: Funnel Metric Analysis"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Metric-Analysis-Funnel-Metric-Analysis"
---

<span id="一-概述"></span>
# 1.Overview

What is a conversion funnel and how do I create and use a conversion funnel?

For details, see [Create Funnel Metric](https://docs.byteplus.com/docs/DataTester/Create-Funnel-Metric).

<span id="二-如何切换视图"></span>
# 2. How to switch views

If you add a conversion funnel to your experiment, you can toggle between List View and Funnel View on the Experiment Report page to view the conversion funnel data. As follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77b37d29d2f74942bc0667f0bba4be84~tplv-goo7wpa0wc-image.image) </span>

<span id="三-如何查看视图详情"></span>
# 3. How to view view details

<span id="_1-列表视图"></span>
## 1. List view


* You can view the relevant funnels by choosing to compare different experimental versions. On the left is the compared version of the funnel, and on the right is the compared version of the funnel. As follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4a9d077bbc2435d830c4a6e9936bf8d~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-1-对比版本漏斗"></span>
### 1.1 Comparison version funnel


* **Comparison version funnel (left)** : An experimental version must be selected, with candidates for all versions of the current experiment. When choosing a control version, only the funnel is displayed, and no information such as confidence levels and confidence intervals is calculated. The default is the experimental version with the highest total conversion rate of confidence; if the experimental version has no confidence, the experimental version with the highest total conversion rate of disbelief is displayed.

   * Description: The confidence interval calculation here is based on the "compared version of the funnel", not the compared version of the funnel.


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d9c82914ccab441280139638d92797e1~tplv-em5hxbkur4-noop.image?width=1639&height=845) </span>

<span id="_1-2-被对比版本漏斗"></span>
### 1.2 Comparison version funnel


* **The funnel of the compared version (right side)** : No experimental version can be selected, the candidate is all versions of the current experiment + "No comparison version". If the compared version is not selected, the compared version is used as the compared version by default, and there is no confidence interval and other information to calculate.


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7e4232ee6e2a422bb09ee2a5edd5f30c~tplv-em5hxbkur4-noop.image?width=1628&height=848) </span>


* When the funnel of the compared version selects "No Comparison Version", it degenerates into a single\-focus presentation. As shown below:


<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/fb64da0470c141baa068f4fb2f116b2e~tplv-em5hxbkur4-noop.image?width=1644&height=801) </span>

<span id="_1-3-如何区分各个版本的数据"></span>
### 1.3 How to distinguish between different versions of data


* It can be distinguished by the color of the text. For example, the compared version is experimental version 1, which is blue; the compared version is experimental version 2, and the text color is green. As shown below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4060e1a639f444ebe4e2aa44db084a2~tplv-goo7wpa0wc-image.image) </span>


* The confidence intervals for the floating card and the comparison version funnel are calculated with reference to the comparison version funnel. As follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e96deccfda5b48c1a3a17f7caa3eea12~tplv-goo7wpa0wc-image.image) </span>


* Floating card, the following red box, the left value indicates the number of people who compared the version of the funnel triggered the event, and the right indicates the number and proportion of the compared version of the funnel that did not trigger the event. As shown below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d75c76f8de2f4cd88bf90b5d113cf918~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-漏斗视图"></span>
## 2. Funnel view

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/496fa17a73e74b3cafae6a54503f44a3~tplv-goo7wpa0wc-image.image) </span>

Funnel configuration details for the compared and compared versions, the same as the list view.

<span id="三-数据计算相关"></span>
# 4. Data calculation correlation

<span id="09735e8e"></span>
## Basic concept


|Term |Concept introduction |
|---|---|
|Transition window |Refers to the conversion period of a process, which is the set of time required to complete each layer of transformation, expressed in DataTester as the conversion window period.<br><br>In general, the shorter the conversion cycle of a process, the better, especially in some industries with longer conversion cycles, such as online education and B2B e\-commerce.<br><br>In addition, looking at the conversion time of each layer individually can also reveal some issues. For example, if it is found that the traffic imported from a certain channel takes surprisingly consistent time to convert at a certain layer, it indicates that the traffic of that channel is likely to be abnormal. |
|Funnel event |Each layer of events is a node. For nodes, the most crucial metric is the conversion rate. By analyzing the conversion rate of the entire process and the conversion rate of each layer, we can clarify the direction of optimization: find nodes with low conversion rates and find ways to improve them. |
|Traffic |The computational logic of DataTester's funnel metric is based on the number of users (UVs) to calculate crowd flow. The performance of different groups of people under the same conversion path must be different. For example, in Taobao's shopping funnel, the conversion rates of men and women are different, and the conversion rates of young people and the elderly are also different. By classifying the population, we can quickly see the conversion rate of a specific population and better identify the problem. |


<span id="e3cd9970"></span>
## Computational logic

DataTester calculates funnel metrics by headcount (UV):


* Overall conversion rate = number of people reaching the current funnel event/people at the first funnel event

* Previous conversion rate = the number of people reaching the current funnel event/the number of people in the previous funnel event


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">DataTester's funnel indicator does not need to configure the experimental exposure event when creating, but when calculating the funnel indicator result, the experimental exposure event will be used as the filter event before the first step event of the funnel indicator, and the user who triggered the experimental exposure event will participate in the calculation of the funnel indicator. And the experimental exposure event carries the corresponding experimental version VID.</div>


<span id="6a62d455"></span>
## Precautions


* Funnels support global time and multidimensional filters, but are not affected by time granularity (5 minutes, hours, days). Real\-time does not support confidence level calculations, only pure funnels.

* If you modify any of the funnel's filters, funnel events, etc., all experiments using the funnel (in any state), the experiment details page, and the report page will be updated accordingly. The funnel data is not cached, so the funnel data on the lab report page will also be updated with the latest data.
