---
title: "Cost analysis"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/Cost_analysis"
---

<span id="r4L9gDt5"></span>
# Feature Overview

Cost Analysis provides self\-service visualization capabilities for analyzing expense and cost bills. It supports multi\-dimensional filtering and categorized summaries to view expense trends and structures. Users can save viewing conditions as report templates for quick access.

Note:


1. Cost Analysis data is updated one day later than the bill details. Final data for the current month is available on the 4th of the following month. If there are bills with the billing mode set to "Contract Billing," the final data for the current month is available on the 5th working day of the following month. Cost bills are available one day later than the bill details.

2. The expense trend chart only displays the top 10 categorized values. The remaining amounts are summarized as "Others," and all categorized details can be viewed in the expense details.

3. When the billing criteria is "Bill," only cost data analysis from January 2022 onwards is supported. When the billing criteria is "Cost Bill," only cost data analysis from the month the cost bill was activated is supported.


<span id="QPFysgxR"></span>
# Operation Guide

**1. Activate the Cost Analysis Service:** 

Log in to the BytePlus  [Billing center- Cost analysis](https://console.byteplus.com/finance/bill/cost-analyse) , and click to activate the Cost Analysis Service when entering for the first time.

**2. View Cost Trends:** 

On the Cost Analysis page, you can filter and view cost trends under various classification dimensions and filter conditions. Supports three styles: bar chart, bar graph, and line chart.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260514090729-1269578456142.png) </span>


* Classification dimension: Supports viewing cost trends based on multiple dimensions such as product, region, project, and tags.

   * When tags are used as a classification dimension, you need to specify the tag key to view the cost trend for the corresponding tag.

   * When instance ID is used as a classification dimension, you can select up to 10 instance IDs to view cost trends; 

* Billing criteria: Supports cost analysis for two types of bills:  bills and cost bills.

* Expense type: Different expense type options will be provided based on the selected billing type.

* Time granularity: Supports viewing data within a certain time range by month or by day.

* Filter conditions: Users can view more precise cost data by using advanced filters; the filter conditions default to include all, and when selected, it supports either include only or exclude only.


**3. View cost details list:** 

The cost details list supports querying distribution details under each classification dimension. When **PoP Rate** is selected, the system will display month\-on\-month comparison data against the prior period.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260514090941-602511355766.png) </span>

&nbsp;

**4. Report Template Management:** 

Click "Save Report" or "Save As" in the upper right corner to save the current page's viewing conditions as a report template. Click "Report Management" to navigate to the report template management menu, where you can view and manage report template data.


* View Report: Click "View" to quickly access the cost analysis view under the conditions of the selected report template.

* Delete Report: Click "Delete" to remove the report template. (Note: System\-preset report templates cannot be deleted or modified.)


 <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260514084924-449435006677.png) </span>
