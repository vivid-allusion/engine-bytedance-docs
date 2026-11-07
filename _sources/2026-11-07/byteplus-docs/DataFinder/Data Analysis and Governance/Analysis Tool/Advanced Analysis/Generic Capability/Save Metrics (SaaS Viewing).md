---
title: "Save Metrics (SaaS Viewing)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Save_Metrics_SaaS_Viewing"
---

<span id="_1-概述"></span>
# 1. Overview

<span id="_1-1-使用场景"></span>
## 1.1 Scenarios of use

**Indicators** can reflect the current situation of business development, identify business problems and focus on solutions, and promote orderly growth of business.

For example, in an e\-commerce C2C enterprise, the essence of the business is to solve the problem of demand "matching" and "matching efficiency", which is a process of continuously enriching supply and meeting needs. The goal will be to pursue the bilateral relationship needs of more users, and corresponding to the data, strategic indicators such as "DAU", "orders", and "GMV" will be derived.

The growth analysis product supports the preservation of the indicators that the business continues to focus on in the advanced analysis module, so as to realize the unified management of indicators.

<span id="_1-2-名词解释"></span>
## 1.2 Explanation of terms

<span id="_1-2-1-什么是指标？"></span>
### 1.2.1 What are indicators?

Indicators: It is a **quantitative value** , including UV, PV, number of times per capita, click through rate, retention rate, etc., to measure business performance.

Metrics can be divided into attributes data and composite metrics:


* Such as UV, PV, and order amount are all simple attributes data.

* And like bounce rate, purchase conversion rate, etc., involving four operations, it belongs to the composite index.


<span id="_1-2-2-指标和事件的区别是什么？"></span>
### 1.2.2. What is the difference between indicators and events?

Events are user actions or business actions defined through event tracking. Such as "play video", "buy goods", etc., to mark user behavior.

Metrics are composed of events and operators, such as the number of UVs app_launch an event that constitutes the DAU metric.

Operator: refers to the metrics supported during analysis, such as total number of people, total number of times.

<span id="_1-2-3-当前支持的分析模型范围"></span>
### 1.2.3 Scope of currently supported analytical models


|**Advanced Analytical Model** |**Support** |
|---|---|
|Event analysis |✔️ |
|Retention analysis |❌ |
|Conversion analysis |✔️ |
|Distribution analysis |❌ |
|Component analysis |❌ |
|User path |❌ |
|Attribution analysis |❌ |
|User lifecycle |❌ |
|Heat map analysis |❌ |
|LTV analysis |❌ |
|Business Object Analysis |❌ |


<span id="_2-功能介绍"></span>
# 2. Function introduction

Growth Analysis Current event analysis models can support saving metrics, as illustrated by event analysis as an example below.

<span id="_2-1-创建指标"></span>
## 2.1 Creating metrics

You can create metrics by clicking "Save Metrics" on the Advanced Analytics \- Event Analytics page. Anyone can create a metric. If the metric you create does not need to be used by other members, please select "Only yourself" for the visible range.

The operation method is:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/722dc446da8143eba650bc82c9a67b59~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cd303cbfb594aedbab3e24cf653a1ce~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用指标"></span>
## 2.2 Use of metrics

Metrics are only supported in the Advanced Analytics \- Event Analysis module. Unlike events, query metrics do not need to be paired with operators (e.g. PV, UV, etc.), and metrics directly correspond to numerical results.

Special note: The indicator does not support the use of "ring chart" type display for the time being.

The operation method is:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aec0d733b05747d0b848644a12591536~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a875575ccef14dcb8f4790925762da00~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-编辑指标"></span>
## 2.3 Editing metrics

The creator or administrator of the indicator can edit the indicator, modify the indicator calculation criteria or describe the information.

Attention should be paid to the fact that the indicator modification calculation criteria is effective for saved charts, and the data will be changed.

The operation method is:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a7430384c6042488bc344d1b9029f35~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-删除指标"></span>
## 2.4 Delete metrics

The creator or administrator of the indicator can delete the indicator. Attention: Charts that have been saved after the indicator is deleted will not be able to continue searching for results.

The operation method is:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba2af0f96b594be793febb768ea864e7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-常见问题faq"></span>
# 3. Frequently Asked Questions

<span id="_3-1-事件、虚拟事件、指标的差异是什么？"></span>
## 3.1 What are the differences between events, virtual events, and metrics?

An event marks a user action, such as a user watching a video.

Virtual events are a combination of multiple events, for example, user interaction events are composed of retweeting or commenting or liking events, and any one of the events occurring by the user is counted as interaction.

Metrics are quantified values of events or virtual events, for example, the DAU metric is the result of a UV calculation of app_launch events.

<span id="_3-2-什么是组合指标？"></span>
## 3.2 What are portfolio metrics?

Composite metrics are complex metrics that consist of addition, subtraction, multiplication and division of multiple events, such as login rate = number of logged\-in users/total number of users.

<span id="_3-3-指标可以在哪些地方使用？"></span>
## 3.3 Where can indicators be used?

Save metrics are currently only supported in the event analysis module, and more analysis functions will be supported in the future.
