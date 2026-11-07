---
title: "Experimental Metric"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Experimental-Metric"
---

<span id="一-概述"></span>
# 1. Overview

<span id="指标是什么？"></span>
### **What are the metrics?** 

In the Internet industry, a metric refers to a concept that reflects a certain thing or phenomenon, describes the scale, degree, proportion, structure, and other concepts at a certain time and under certain conditions, and is usually composed of a metric name and a metric value. **Metrics can be divided into simple counting metrics and composite metrics.** 


1. Simple counting metrics are metrics that can be obtained numerically by repeatedly adding 1, such as UV (Unique Visit, unique visitor), PV (Page View).

2. Composite metrics are derived from four simple counting metrics operations, such as bounce rate and purchase conversion rate.


<span id="指标组"></span>
### **Metric group**

As the name suggests, it is a collection of multiple metrics. We usually place highly relevant metrics in the same group for easy search, use, and management, such as: XX project revenue metrics group, order metrics group, XX page conversion metrics group, etc.

Note: Only **the same type**(Type: Event/Retention/Funnel Metrics) can belong to the same group, that is, all metrics in the same metrics group have the same type.

> **The new version of metric management displays and manages metrics according to the granularity of the metric group by default**

> * For metrics that have been created in history, data migration and grouping will be carried out according to [metric owner \* metric type \* public/private], that is, public metrics of the same type with the same owner will be grouped into the same group; private metrics Each metric will generate a metric group separately.


<span id="二-指标组列表"></span>
# 2. List of metric groups

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/837e83f127174cbfb5ef04f43fbd9db4~tplv-goo7wpa0wc-image.image) </span>

**The actionable content is as follows:** 


* **Filter:**  All metrics in use are displayed by default. Click the "Filter icon" in the status bar to toggle the display of offline metric groups or all status metrics.

* **Search:**  Support entering "metric group name, description, creator" to search for metrics.

* **New metric group:**  Click "Create metric group" in the upper right corner of the page to start creating a new metric group.

* **Merge metric groups:**  Multiple metric supports of the same type can be combined into a new metric group.

* **Import from Growth Analysis:**  Supports importing metrics from Finder Kanban to quickly create evaluation metrics for experiments.

* **View metric group:**  Click "Metric name" to jump to the metric group details page to view the basic information of the metric group, metric caliber, metric group permissions, etc.

* **Modify metric group:**  Click the "Edit icon" in the operation column to jump to the editing status of the metric group to modify.

   * Note: Only metric group owners and administrators can edit metric groups, and non\-administrators cannot edit other people's metric groups.

* **Other operations:** 

   * **Offline:**  The current metric group can be offline. Offline Premise: None of the metrics in the current metric group are associated with running experiments.

   * **Replication:**  The current metric group can be replicated.


<span id="三-实验关注指标"></span>
# 3. Experimental attention metric

<span id="核心指标"></span>
### **Core metrics**

Core metrics, which are used to determine whether the experimental function meets the expected "direct effect metrics", are also called "success metrics". Only one metric can be set as the core metric of an experiment, and the experimental data can be viewed in the experiment report. For example, to open an optimization experiment of "button copy", then "button click through rate" is the core metric of the experiment.

Common core metrics are divided into different classes as follows: ① conversion rate, uv/au class; ② per capita frequency class, such as pv/au, pv/uv, sum/au, sum/uv; ③ average class, such as sum/pv;

You can choose or create new core metrics based on your current business.

<span id="必看指标"></span>
### **Mandatory metrics**

Mandatory metrics refer to the business line metrics that must be guarded. Experimental functions may not have a direct causal relationship with them and cannot directly improve them, but generally they cannot have a significant negative impact on them.


* If a certain metric is set as a mandatory metric, then each experiment under the application will default to selecting the mandatory metric as the experimental attention metric.
