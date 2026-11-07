---
title: "Create Funnel Metric"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Create-Funnel-Metric"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Only one funnel metric can be created per metric group.</strong></div>


<div data-tips="true" data-tips-type="tip">Reason: The conversion link of funnel metrics also contains multiple conversion rate metrics, so compared to other event metrics, it is a concept of a set of metrics in itself, and funnel data and charts are presented according to the granularity of the metrics on the report page.</div>


<span id="一、概述"></span>
# 1. Overview

The conversion funnel model is essentially decomposed and quantified to find the conversion efficiency of each link in the target process, so as to help operations and product personnel find weak links and tune abnormal steps. Funnel models can be widely used in traffic monitoring, user operation, product target conversion, marketing advertising and other daily data operations, called conversion funnel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06c3c35eda93476283255e0e00c6d7c1~tplv-goo7wpa0wc-image.image) </span>

<span id="相关名词解释："></span>
#### **Explanation of related terms:** 


* CVR: Conversion rate, which is usually used to measure the effectiveness of CPA advertising, is later generalized to the situation of initiating crowd achievement for a specific goal.

* Conversion Time Window: Events of the funnel must be completed within the Conversion Time Window time limit in the configured order to count as a successful conversion. Subsequent target events later than the conversion time window are excluded from conversion.

* Query Time Interval: A funnel for long\-term observations. By querying the time interval, the funnel formed by filtering the conversion events in the target time region.


<span id="二、常见的漏斗类型"></span>
# 2. Common types of funnels

**In AB test scenarios, there are three common types of funnels:** 


* Customer acquisition: This type mainly attracts new potential customers and converts them into customers.

   * Some advertising agencies often use offers or gifts to attract potential customers to provide email addresses or other contact information, etc., to form customer conversions.

* Activation: This type is targeted at new customers who have not yet started using the product at a high frequency.

* Profitability: This type is designed to increase the CLV of existing customers.


<span id="三、新建留存指标"></span>
# 3. New retention metrics

Entry: List Page Click "Create Metric Group" \- Metric Group Type: Funnel Metric

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac219c66b1ce4ae992967e75181bcd07~tplv-goo7wpa0wc-image.image) </span>

<span id="基本信息："></span>
### **Basic information:** 


* **Metric Group Type:**  Select Funnel Metric

* **Belonging metric group:**  By default, the first metric group of the **same type** created by the current user history will be selected. Support re\-select the metric group & create a new metric group and select it.


<span id="指标设置："></span>
### Metric **settings:** 


* **Metric name:**  It is recommended to take a name related to the conversion funnel. The name is unique within the metric group, with a maximum of 50 characters.

* **Metric description:**  Briefly describe the meaning and purpose of the metric, etc., so that business\-related personnel can use the metric more reasonably.

* calculation aperture

   * **Conversion time window period:**  refers to the time when the user completes the conversion, and the user completes the complete conversion process within the set window period to be considered a successful conversion. You can choose minutes, hours, and days.

   * **Funnel event:** 

      * Virtual events, general events, and circled events can all be used as funnel conversion events.

      * Minimum 2 funnel events and maximum 10 funnel events.

      * Strictly adhere to the order of occurrence of events, if the experimental visitor does not complete all events in the order of the conversion funnel within the conversion time window, it will not be counted in the conversion data statistics.

   * **Global filter conditions:**  support user grouping, public attributes (including preset attributes and custom attributes). Filter criteria support public attributes and event attributes, but user grouping is not currently supported.


**Once the funnel metric starts collecting, counting, and analyzing data, it is not recommended to edit the funnel. Modifying the funnel will trigger an automatic update of all data.** 

<span id="使用指标"></span>
### Usage metrics

In the second step of creating the experiment \- select the follow metric, you can add the set conversion funnel metric to the follow metric. As shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66549971664d48939b2dea5c9a4c039b~tplv-goo7wpa0wc-image.image) </span>

In an experiment, only one conversion funnel metric can be added at most, and it cannot be set as the core metric for the time being, and monitoring and alarming are not supported.
