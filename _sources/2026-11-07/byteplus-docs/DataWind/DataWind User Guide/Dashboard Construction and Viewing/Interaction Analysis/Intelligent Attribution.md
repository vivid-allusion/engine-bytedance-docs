---
title: "Intelligent Attribution"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Intelligent_Attribution"
---

Intelligent attribution refers to the attribution analysis feature with built\-in attribution algorithms in visualization dashboards, which helps users gain insights into the causes of business anomalies. By performing multidimensional attribution analysis, users can examine data results in depth, identify the influencing factors and root causes of metrics, and gain intelligent attribution insights. This article introduces how to use the intelligent attribution feature.

<span id="f4e01e39"></span>
# Notes

Intelligent attribution is only available for extracted datasets and does not currently support direct connection datasets. For the differences between direct connection and extraction, refer to [Connection methods](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview#0b15f366).

<span id="34509668"></span>
# Application scenarios

Over time, users often observe significant increases or sharp decreases in values and want to understand the reasons behind such fluctuations. With intelligent attribution, the reasons can be identified with just a few clicks. Specific business scenario examples are as follows. The actual application results depend on the business data.

<span id="e84e2636"></span>
## Attribution for sudden increase in average latency

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa4b8b8b0d4b4ec484b38cd9a1985f19~tplv-goo7wpa0wc-image.image) </span>

Through attribution analysis, it can be found that the increase in latency may be caused by the Rexxx project.

<span id="74efc170"></span>
## Attribution for sudden increase in payment amount

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac0129942fd04a5aa39d5dcd36844022~tplv-goo7wpa0wc-image.image) </span>

Through attribution analysis, it is found that the sudden increase is mainly due to growth in the Beijing region.

<span id="_2-快速入门"></span>
# Quick start

**The basic trigger conditions for attribution analysis are as follows:** 


* The X\-axis must be a date\-type field. Currently, the supported aggregation granularities are day, week, and month.

* There must be at least one metric in the chart that meets the expression requirements. For details, see the supported expressions for attribution analysis described later.

* The current analysis point or comparison time point must not be empty, null, or 0.

* The dataset used for attribution analysis must be an **extracted dataset**. Direct connection datasets are not currently supported.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Attribution analysis requires a certain amount of continuous data; otherwise, fluctuations cannot be determined.</div>



* <div data-tips="true" data-tips-type="warning">Daily level: At least 14 consecutive days of data are required.</div>


* <div data-tips="true" data-tips-type="warning">Weekly level: At least 8 consecutive weeks of data are required.</div>


* <div data-tips="true" data-tips-type="warning">Monthly level: At least 24 consecutive months of data are required.</div>


1. In the line chart, if a sudden drop in GMV is observed on the most recent day, click the data point where the drop occurs to perform attribution analysis (select "Default Attribution Analysis" here).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/375eb49eb6494838b5489c319a4ecf41~tplv-goo7wpa0wc-image.image) </span>


2. After the attribution analysis is completed, click to view the attribution results.

3. View the attribution results. Recently, GMV has exhibited abnormal fluctuations. By default, the data is compared with that of the previous month, showing a decrease of 22.61%. The dimensions are ranked by their contribution to the decline, and it is found that the coefficient for sale_city is 0.56, making it a significant influencing factor. You can filter and further analyze the sales performance in this region.


<span id="_3-使用场景"></span>
# Feature overview

<span id="_4-1-归因分析对比时间选择"></span>
## Selecting comparison time for attribution analysis


* Default attribution analysis

   * Daily level: By default, compares the date 7 days ago with the current date.

   * Weekly level: By default, compares the previous week with the current week.

   * Monthly level: By default, compares the previous month with the current month.

* Custom comparison period: You can customize the comparison period.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a087cfe8b1b84139aaafe7c200764992~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-解读归因分析报告"></span>
## Interpreting the attribution analysis report

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61e1f7cec0390b757599643e8f34f637.png) </span>

A: Fluctuation status. Based on recent data, determine whether the indicator is fluctuating normally.

B: Indicator change. The change in the indicator compared to a previous point in time.

C: Dimension contribution ranking, for a single dimension:


* Dimension name

* Gini coefficient, used to indicate the degree of impact on indicator changes.

* Top 3 dimension items by overall contribution.

* When used with CDP, you can also create new groups here.


D: Analysis of specific dimension items.

<span id="_4-3-归因分析配置"></span>
## Attribution analysis configuration.

Supports attribution analysis configuration at the dataset level. When attribution analysis is performed on this dataset, attribution will be performed based on the configured attribution basis and display dimensions, and the specified number of results will be displayed.

<span id="_4-3-1-入口"></span>
### Entry

**Entry 1 Visual Query**: Click the ⋮ in the upper right corner of the dataset information on the left, and select "Attribution Analysis Configuration"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/136955d8677349109a0a83a5e43016fc~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44855a33196249f787554ca0d8fcdc68~tplv-goo7wpa0wc-image.image) </span>

**Entry 2 Dataset**: Open the dataset to be queried, and select "Attribution Analysis Configuration" in the upper right corner

<span id="_4-3-2-全局配置与个性配置"></span>
### Global configuration and personalized configuration

In attribution analysis configuration, you can preset the attribution basis, display dimensions, and number of results to display.

A dataset often contains multiple metrics. When different metrics require different attribution configuration settings, click "Custom configuration" to select metrics for individual configuration. The global configuration applies to metrics other than those with individual configuration.

If no individual configuration is set, the global configuration applies to all metrics.

<span id="_4-3-3-异常判断依据"></span>
### Criteria for anomaly detection


* Time series prediction: The system automatically determines anomalies based on whether the result falls within the default time series prediction range.

* Fluctuation greater than: Anomalies are determined based on period\-over\-period fluctuation. If the fluctuation exceeds the specified value, it is considered an anomaly.


<span id="_4-3-4-归因维度限制"></span>
### Attribution dimension restrictions

After enabling attribution dimension restrictions, not all dimensions will be included in attribution analysis, which helps avoid including meaningless analysis dimensions that could cause misunderstanding or increase computational load.


* Only dimensions with fewer than 1,000 items participate in attribution: The number can be set freely. If the dataset contains dimensions such as id or device number with a large number of items and no attribution significance, this option can be selected.

* Exclude certain dimensions: Manually exclude specific dimensions so that they do not participate in attribution.


<span id="_4-3-5-结果展示限制"></span>
### Result display restrictions

By default, the attribution analysis report displays analysis results for all dimensions in descending order of their impact on the Gini coefficient. After selecting this option, the number of displayed dimensions can be limited. After selecting this option, some impactful dimensions may not be fully displayed.

<span id="_4-4-支持的表达式"></span>
## Supported expressions


* Expressions supported by attribution analysis

   
   |**Expression** |**Example** |
   |---|---|
   |count(distinct XXX) |count(distinct user_id) |
   |sum(XXX) |sum(col), sum(col/100), sum(1/col), sum(case when result = 'failed' then 1/result_count else 0 end) |
   |avg(XXX) |avg(col) |
   |sum(XXX)/sum(XXX) |sum(col1) / sum(col2), sum(case when result='failed' then 1 / result_count else 0 end) / sum(1 / result_count) |
   |sum(XXX)/count(XXX) |sum(vv)/count(uid) |
   |count(XXX) |count(col1) |
   |sum(XXX)/100 |sum(col)/100, |
   |100/sum(XXX) |100/sum(col) |
   |XXX/XXX |col/1, col1/col2 |
   |XXX |col |
   

* Expressions not supported by attribution analysis

   
   |Expression |Example |
   |---|---|
   |count(distinct XXX) / count(distinct XXX) |count(distinct pid) / count(distinct uid) |
   |uniq(XXX) / uniq(XXX) | |
   |sum(XXX) / count(distinct XXX) |sum(vv) / count(distinct uid) |
   |sum(XXX) / sum(XXX) / sum(XXX) | |
   |sum(XXX) / sum(XXX) / 1 | |
   |XXX \- YYY |profit \- cost |
   

* Support will be added in the future

   
   |Expression |Example |
   |---|---|
   |uniq(XXX) |uniq(XXX) |
   |uniq(XXX)/100 |uniq(XXX)/100 |
   


<span id="_4-5-归因的维度范围"></span>
## Scope of attribution dimensions

The following types of dimensions will not appear in the dimension list on the left side of the attribution analysis report list:


* Any dimension whose expression is id or date;

* If the top item of a dimension has too small a contribution value, it will not be displayed. For example, for the dimension "Province", if the item "Shanghai" has the highest contribution value but its contribution percentage is less than 1%, it will not be displayed;

* If a dimension has only one item, it will not be displayed;

* The partition field dimension will not be displayed.

* If there are no dimension items under a dimension, it will not be displayed.

* In time period analysis, if the number of dimension items for a dimension is too large (\>10K), it will not be displayed.

* If there are too many dimensions (\>15), only some of the dimensions selected by the user will be included in the calculation (those with a high Gini coefficient and those most frequently used by the current user).
