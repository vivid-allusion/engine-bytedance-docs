---
title: "Mandatory Metric Dashboard"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Mandatory-Metric-Dashboard"
---

<span id="一-概述"></span>
# 1. Overview

Mandatory metrics refer to the business line metrics that must be guarded. Experimental functions may not have a direct causal relationship with them and cannot directly improve them, but generally they cannot have a significant negative impact on them.


* If a certain metric is set as a mandatory metric, then each experiment under the application will default to selecting the mandatory metric as the experimental attention metric.


Mandatory metric dashboard, this function mainly provides users with an "application perspective", on the one hand, you can view the trend of each mandatory metric under the application; on the other hand, through the reverse correlation experiment of mandatory metrics, in order to timely and accurately understand which experiments have affected the trend of mandatory metrics.

<span id="二-应用场景"></span>
# 2. Application scenario


* When we seek to maximize the benefits of our experimental core metrics, where can we see the impact of our experiments on the mandatory metrics?

* As a business leader, my concern may not be the situation of individual experiments, but the overall performance of the entire application. Where can I view the overall data of the "Application Perspective"?

* What experiments are related to the fluctuation of metrics, and how to filter and view them through the time dimension?


<span id="三-如何设置必看指标"></span>
# 3. How to set mandatory metrics

<span id="_1-操作入口"></span>
## 1. Operation entrance

Entrance: metric management \- metric list \- mandatory metric dashboard. **Only group administrators and app administrators can create mandatory metrics.** 

<span id="_2-操作方法"></span>
## 2. Operation method


* Click metric management;

* Locate the metric you want to set as a mandatory by means of list search or direct search;

* Set the corresponding metric as a mandatory metric.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e11ca2e79e794e6b8a9402e3d3ccb282~tplv-goo7wpa0wc-image.image) </span>


<span id="四-必看指标看板"></span>
# 4. Mandatory metric dashboard

<span id="_1-设置筛选条件"></span>
## Step 1 Set filter criteria

The dimensions supported by the filter criteria are as follows:


|**Dimension name** |**Support content** |
|---|---|
|Time |Support "day\-level, hour\-level, 5\-minute\-level" data aggregation granularity, and provide "recent" and "range" filtering methods |
|Experimental mode |It is divided into two categories: active trigger experiment (other experiments) and passive acceptance experiment (push experiment). After selecting the experimental mode, you can select "experiment and version" for data review |
|Experiments and versions |Adopt a double\-layer structure of "Experiment Name\-Experiment Version", which is convenient for locating the experimental details |
|Filter dimension |Support two categories of filtering: "public attributes, user grouping" |



* Experiment and version screening, as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61ee68e907a146e8a464975d09ae8a3a~tplv-goo7wpa0wc-image.image) </span>


* Filter dimensions as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4231a7039f34ea3af06d6829f1e639c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-查看指标趋势"></span>
## 2. Check the metric trend


* Support viewing "Event Metrics, Technical Metrics" Trends.

* If the event or attribute to which the metric belongs is offline, the corresponding metric trend chart has no data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2a04b891e7a4617853183880a351e14~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-一键查看指标关联的实验"></span>
## 3. One\-click to view the experiment of metric association


* The mouse hover metric trend chart shows the specific metric value.

* When the time filter is "day\-on\-day", the trend of "day\-on\-day ratio" and "week\-on\-week ratio" is displayed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80f63f17e82f4c6387d37c7ab0eab4b5~tplv-goo7wpa0wc-image.image) </span>


* Click "View new experiments at that time" and "View running experiments at that time", and you will jump to the "Experiment List" page with specific time information, and check all experiments associated with the mandatory metrics with one click.
