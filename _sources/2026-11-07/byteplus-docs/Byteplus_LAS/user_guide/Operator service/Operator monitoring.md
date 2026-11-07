---
title: "Operator monitoring"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/las_operator_service"
---

LAS AI provides monitoring and management capabilities for common operator metrics through the operator monitoring page. On this page, you can view usage data, usage trends, and detailed core metrics for each operator (such as Token rate, request error count, and more). This article introduces the details of the operator monitoring feature.

<span id="31289554"></span>
# Notes


* Currently, operator monitoring supports only online operators; offline operators are not supported at this time.

* Currently, you can view monitoring metric data for up to the past 30 days.


<span id="14cbea0a"></span>
# User guide

<span id="620f8ad5"></span>
## Access point

After logging in and entering [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home?), click "Operator service \> operator monitoring" in the left navigation of the console page for the supported region to access the operator monitoring page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cd54cb220e04202b5beee1e82a1ebbc~tplv-goo7wpa0wc-image.image) </span>


* You can use the filter box at the top to select the range of operator types to view (all operators, video operators, image operators, and so on).

* Filtering by the LAS API Key used for invocation is also supported. You can select the LAS API Key to view from the dropdown box.

* You can also select the time range to query in the upper right corner. Currently, usage data for the past 30 days is supported.


<span id="b00cc850"></span>
## Global usage statistics

After accessing the operator monitoring page, you can conveniently view the current global operator usage on the page, such as the number of successful operator calls, total consumption, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2428ce0e889d4b088caea3644e1389f0~tplv-goo7wpa0wc-image.image) </span>

<span id="be075748"></span>
## View operator monitoring metrics

After accessing the operator monitoring page, you can view basic information for each operator (operator ID, billing method, and so on) on the page. You can also:


* Click the "Monitor" button in the "Actions" column to view the monitoring metrics for the current operator, including Token rate, request error count, and more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/139a44a8203749c8a23a5a8a4c5a51c9~tplv-goo7wpa0wc-image.image) </span>

   * You can flexibly select the time range for viewing monitoring data (1 hour, 6 hours, 12 hours, and so on), and you can also customize the time range. Currently, you can view monitoring data for up to the past 30 days.

   * Token rate, number of request errors, and several other monitoring metrics are preconfigured for display. You can hover the mouse over the tooltip button next to each metric to view detailed definitions of the metrics.

   * When there are multiple detailed monitoring metrics in the monitoring chart, you can also flexibly select specific metrics to view.

* Click the operator name to jump to the operator details page, where you can view detailed information about the operator's core capabilities, API invocation instructions, and examples.
