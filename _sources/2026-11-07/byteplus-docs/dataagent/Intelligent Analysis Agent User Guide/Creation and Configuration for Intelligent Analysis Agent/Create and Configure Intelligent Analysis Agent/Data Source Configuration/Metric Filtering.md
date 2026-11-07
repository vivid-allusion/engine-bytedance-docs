---
title: "Metric Filtering"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Metric_Filtering"
---

This article introduces multiple methods for filtering metrics in a dataset.

<span id="63e6310d"></span>
# Quick start


1. Click "Filter configuration" to enter the dataset filter configuration interface, then click "Add" to set the filter conditions for the metric fields used by the agent.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8df6b6e8304f44e784112634c9c703a0~tplv-goo7wpa0wc-image.image) </span>


2. For metric fields, two methods are provided: "Result filtering" and "Detail filtering". Set the relevant filter parameters according to actual data requirements, then click "Confirm" to execute the filtering.


<span id="89f7d62c"></span>
# Applicable scenarios


|Metric filtering methods |Applicable scenarios |
|---|---|
|Result filtering |Filtering is performed based on the aggregated results of metrics, targeting metric aggregate values. For example: filter data where **sum (order quantity)**  is greater than 2,000. |
|Detail filtering |Filtering is performed based on the original values of metrics, targeting the initial detail data in the dataset. For example: filter data where **order quantity** is less than 5. |


<span id="be9a8973"></span>
# Feature overview


1. Select the filter type as "Result filtering" or "Detail filtering".

2. Select an operator and enter the filter value.

3. Click "Confirm" to complete the data filtering.


The relevant parameter configuration is explained as follows:


|Parameters |Configuration description |
|---|---|
|Type |* Result filtering: Filtering based on the aggregated results of metrics<br><br>* Detail filtering: Filtering based on the original values of metrics |
|Operator |Supports =, ≠, \>, ≥, <, ≤, (not in) range, (NOT) IN, (not) empty, (not) NaN and other operators<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For range and not in range operators, you also need to specify whether the left and right boundaries are open or closed.</div><br> |
|Filter value |Enter the filter value for the filter condition |
