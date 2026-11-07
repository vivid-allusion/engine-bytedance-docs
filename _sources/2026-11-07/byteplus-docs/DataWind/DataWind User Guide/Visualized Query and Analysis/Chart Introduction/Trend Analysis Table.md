---
title: "Trend Analysis Table"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Trend_Analysis_Table"
---

This article provides comprehensive guidance on using the trend analysis table to help efficiently complete data trend analysis and visualization configuration.

<span id="74137dee"></span>
# Function overview

The trend analysis table is a visualization tool focused on analyzing core metrics over the time dimension. It supports viewing data aggregated by different date granularities for core metrics, and allows further comparison, trend observation, and mean calculation for these metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/613a6ecac6df4a16b8ca8088aa773cb8~tplv-goo7wpa0wc-image.image) </span>

<span id="1e309447"></span>
# Quick start


1. Confirm the **columns** (date dimension), **rows** (dimension, optional), and **indicators** you need to view.

   * The trend analysis table requires **one column date field of type "day", zero or more row dimensions, and one or more indicators**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa502bc620a14b2989d9ac39278a4a3b~tplv-goo7wpa0wc-image.image) </span>

   * The unit of the time dimension must be day. If the date dimension is in hours, minutes, and seconds, you can first adjust the date type of this dimension to "year\-month\-day" in the table chart.

2. Select "trend analysis table" as the chart type in the chart bar.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64c3b4bc21bc4d1eba22a6bc2395b2eb~tplv-goo7wpa0wc-image.image) </span>

   Drag dimensions and indicators into the column, row, indicator, and filter boxes, and adjust their positions.

   * By moving the relative positions of custom dimensions and indicator names in the **rows**, you can change the left\-right hierarchy between custom dimensions (such as province) and indicators (such as order data).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/450f41f29cd845eea1a41ec56c621ef1~tplv-goo7wpa0wc-image.image) </span>

   * Click "Row" \- "Indicator Name" \- "Set Field Information" to modify the header of the indicator columns in the trend analysis table.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/951204e8e4e846a39d0dfaca7a0cc06b~tplv-goo7wpa0wc-image.image) </span>

3. In the chart configuration bar below the chart, configure the **time granularity, date range**, and **end date** to be displayed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the chart displays "No data available" but the dataset actually contains data, it is possible that the selected time range or end date is incorrect.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eca6ef0f3b0346989f33058db3387fd9~tplv-goo7wpa0wc-image.image) </span>

4. Select the calculation method for indicators, supporting unified or custom configuration. If you check "Show toggle button", a toggle button will appear in the upper right corner of the chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/537489514e254d5db77a8c469236b065~tplv-goo7wpa0wc-image.image) </span>

5. Configure period\-on\-period comparison, Sparklines, and other settings as needed. The chart configuration is then complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3dcb3ddfa564e3c8c2c29c07b29c8d0~tplv-goo7wpa0wc-image.image) </span>


<span id="ab485c25"></span>
# Function introduction

<span id="f465f169"></span>
## Dimension and indicator requirements

The dimensions and indicators required to create a trend analysis table are as follows:


* Column: 1 date dimension with day granularity

* Row: Any number of dimensions (optional)

* **Indicator**: 1 or more indicators


If the dimension is not a date with day granularity, but a date with hour, minute, and second granularity, an error message will be displayed when switching charts.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be5204ac7cf4494cba0fefc411819001~tplv-goo7wpa0wc-image.image) </span>

Switching charts are supported after first adjusting the date type to day granularity in the dimension bar. Because the trend analysis table does not support switching the date type, it is necessary to switch the date type in another chart first, and then switch to the trend analysis table.

<span id="666627d8"></span>
## Dimension and metric configuration


* Columns: Support editing fields, date completion, and setting field information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bdfbf735f8f43e5afd6bd51d7ec62a7~tplv-goo7wpa0wc-image.image) </span>

* Rows: Support editing fields and setting field information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6abb38762f74658a7b2396a1d961e34~tplv-goo7wpa0wc-image.image) </span>

* Metrics: Non\-aggregated fields support aggregation methods, editing fields, setting field information, setting data format, conditional formatting (icon set only), and hiding fields. Aggregated fields, unlike non\-aggregated fields, do not support selecting aggregation methods.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9ebf8553e45402c890800eff0a59764~tplv-goo7wpa0wc-image.image) </span>


<span id="2bc6bb4a"></span>
## Time granularity and end date

<span id="95f0cc0e"></span>
### Time granularity

The trend analysis table supports quickly switching the display granularity of time, and each time granularity supports setting the date range separately.


* By default, biweekly and bimonth are selected.

* The currently supported time granularities include: day, week, biweekly, month, bimonth, quarter, and year.

   * Year: Supports selecting the calculation method, for example, January to December (calendar year), February to January of the following year, March to February of the following year, and more.

   * Biweekly: Supports selecting the calculation method, for example, Monday to Sunday, Tuesday to Monday, and more.

   * Week: Supports selecting the calculation method, for example, Monday to Sunday, Tuesday to Monday, and more.

* Starting from version V2.87.0, setting the date sort order is supported, with ascending order as the default.

   * Selecting "ascending": In the same interval, the chart displays column dates from left to right in order from oldest to newest (default behavior).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/089b32ebff8e46aea00b8570d0181caf~tplv-goo7wpa0wc-image.image) </span>

   * Selecting "descending": In the same interval, the chart displays column dates from left to right in order from newest to oldest.


<span id="28b2d589"></span>
### End date

The date range can be configured within the date granularity, and the end date is the reference date from which the date range is calculated backward.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3e4511bae814c27b48588715e35937d~tplv-goo7wpa0wc-image.image) </span>

<span id="b4ef49c5"></span>
### Date range calculation


* **Year**


The default date display range: Based on the "end date" (inclusive), the default is to go back N years (that is, starting from the year containing the end date (inclusive), go back N years to determine the start date, up to the current end date). N defaults to 3. The input box is a numeric input control, and the range is integers greater than 0.

**Example:** 

If the year calculation method is the natural year from January to December, and the end date is 20221215, with a date range of 3 years, then the range is 20200101\-20221215.

If the year calculation method is from February to January of the following year, and the end date is 20221215, with a date range of 3 years, then the range is 20200201\-20221215.


* **Quarter**


The default date display range: Based on the "end date" (inclusive), the default is to go back N quarters (that is, starting from the quarter containing the end date (inclusive), go back N quarters to determine the start date, up to the current end date). N defaults to 8. The input box is a numeric input control, and the range is integers greater than 0.

**Example:**  If the end date is 20221215 and the date range is 2 quarters, then the range is 20220701\-20221215.


* **Bimonth**


The default date display range: Based on the "end date" (inclusive), the default is to go back N bimonths (that is, starting from the bimonth containing the end date (inclusive), go back N bimonths to determine the start date, up to the current end date). N defaults to 8. The input box is a numeric input control, and the range is integers greater than 0.

**Example:**  If the end date is 20221215 and the date range is 2 bimonths, then the range is 20220901\-20221215.


* **Month**


The default date display range: Based on the "end date" (inclusive), the default is to go back N months (that is, starting from the month containing the end date (inclusive), go back N months to determine the start date, up to the current end date). N defaults to 15. The input box is a numeric input control, and the range is integers greater than 0.

**Example:**  If the end date is 20221215 and the date range is 2 months, then the range is 20221101\-20221215.


* **Biweek**


The default date display range: Based on the "end date" (inclusive), the default is to go back N biweeks (that is, starting from the biweek containing the end date (inclusive), go back N biweeks to determine the start date, up to the current end date). N defaults to 8. The input box is a numeric input control, and the range is integers greater than 0.

Week calculation method: The dropdown options are as follows, with Monday to Sunday as the default.

**Example:**  For example, if the week calculation method is Monday to Sunday and the cutoff date is 20221215, the date range for 2 biweekly periods would be 20221128\-20221215.


* **Week**


The default date display range is based on the "cutoff date" (inclusive), and by default, covers the period from the start date of the week that contains the cutoff date, going back N weeks, up to and including the cutoff date. N defaults to 5. The input box is a numeric input control, and the range is integers greater than 0.

Week calculation method: The dropdown options are as follows, with Monday to Sunday as the default.

**Example:**  For example, if the week calculation method is Monday to Sunday and the cutoff date is 20221215, the date range for 2 weeks would be 20221205\-20221215.


* **Day**


The default date display range is based on the "cutoff date" (inclusive), and by default, covers the period from N days before the cutoff date up to and including the cutoff date. N defaults to 7. The input box is a numeric input control, and the range is integers greater than 0.

**Example:**  For example, if the cutoff date is 20221215, the date range for 2 days would be 20221214\-20221215.

<span id="b98a5698"></span>
## Calculation method

The trend analysis chart supports setting the calculation method for indicators on the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7f5e4c8bbbd4a92b5830ab446cf2ee7~tplv-goo7wpa0wc-image.image) </span>


* Daily average

   * For non\-division type indicators, the calculation is the sum of the daily indicator data for a given period divided by the number of days with data. If date completion is used for the number of days with data, the completed dates are also included in the number of days with data.

   * For division type indicators (A/B), the calculation is the sum of the daily division results for a given period divided by the number of days with data, that is: sum(A/B) / N, where N is the number of days with data. If date completion is used for the number of days with data, the completed dates are also included in the number of days with data.

* Total

   * For non\-division type indicators, first calculate the indicator data for each day, then sum the indicator data for each day within the statistical period.

   * For division type indicators (A/B), first sum A and B separately, then divide, that is: sum(A) / sum(B).


<span id="934310ca"></span>
## Year\-on\-year and period\-on\-period comparison

The trend analysis chart enables the year\-on\-year and period\-on\-period comparison feature by default. After selecting the "toggle display button", you can quickly switch between year\-on\-year and period\-on\-period comparison in the upper right corner of the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1eced809c71b4b9294352c9de98cafd0~tplv-goo7wpa0wc-image.image) </span>


* Supports configuring the default calculation method. Calculation methods include: year\-on\-year and month\-over\-month.

* Supports configuring the calculation type. Calculation types include: percentage difference and difference value.

* Supports configuring conditional formatting. Supported conditional formats: icon sets.


<span id="812ab9b4"></span>
## Sparkline

The trend analysis table supports configuring Sparklines.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26068c97750d4f57b610bf8e90bad23e~tplv-goo7wpa0wc-image.image) </span>


* Field name: the name displayed for the Sparkline in the chart.

* Y\-axis: defaults to the current metric.

* X\-axis: the dimension of the current chart. Supports switching date types.

* Date range: the data range displayed by the Sparkline. The range is calculated by looking back N date units from the end date. The date unit is determined by the date type of the X\-axis. For example: if the X\-axis date type is month, the date range looks back 6 months, and the end date is 2023\-04\-25, then the Sparkline displays data from 2022\-11 to 2023\-04.


<span id="9418f8a2"></span>
## Interactive analysis feature: supported.


* Analysis feature: not supported.

* Chart linkage: supported.

   * Logic description: When a metric is selected, the date range for that time granularity is passed to other charts. For example, if 2022 Q3 is selected, 20220701\-20220930 is passed.

* Jump: supported.

* Drill up and drill down: not supported.

* Attribution analysis: not supported.

* Dynamic dimensions: not supported.

* Dynamic metrics: supported.

* Global parameters: supported.


<span id="98a49d75"></span>
## Text alignment

Supports adjusting the text alignment of columns, rows, and metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a13f3a72a8c43f98a894b32fee3268e~tplv-goo7wpa0wc-image.image) </span>

<span id="64c912b8"></span>
## Table style

Supports adjusting the style of the table header and table, such as font color, background color, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1465775379124707b6a719ab47c6a2b2~tplv-goo7wpa0wc-image.image) </span>

<span id="df9b53ba"></span>
## Special values

Supports adjusting the display style of special values for dimensions and metrics.


* Display styles include: (blank), NULL, 0, \-\-.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4bf13ef8b5e46438fd3ce7882f2be35~tplv-goo7wpa0wc-image.image) </span>

<span id="38171c47"></span>
## Display mode

Supports adjusting the display mode of the entire table. Display mode configuration includes: column width, column spacing, and row spacing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e572c9958b31445e9a5acc2de1d2ef49~tplv-goo7wpa0wc-image.image) </span>
