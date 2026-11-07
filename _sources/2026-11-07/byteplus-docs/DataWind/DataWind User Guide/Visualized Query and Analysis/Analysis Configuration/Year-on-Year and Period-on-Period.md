---
title: "Year-on-Year and Period-on-Period"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Year-on-Year_and_Period-on-Period"
---

<span id="_1-概述"></span>
# 1. Overview

Year\-on\-year and period\-on\-period calculations compare two metrics of the same dimension based on a specified time interval.

The product provides a year\-on\-year and period\-on\-period analysis component, which supports rapid calculation of year\-on\-year and period\-on\-period data for metrics.

**Year\-on\-year**: The ratio of the metric value during the reporting period to the metric value at the same stage in the previous statistical cycle, indicating the degree of development of the phenomenon at the same stage in each statistical cycle.

Year\-on\-year growth rate = (current period value \- value in the same period last year) / value in the same period last year × 100%.

**Period\-on\-period**: Period\-on\-period refers to the ratio of the metric value during the reporting period to the value in the previous period, indicating the degree of development of the phenomenon in each period.

Period\-on\-period growth rate = (current period value \- previous period value) / previous period value × 100%.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3b0ddc243e94ac59240a3ec851160c5~tplv-goo7wpa0wc-image.image) </span>

**Common application scenarios**

(1) View the increase or decrease in data between two time periods

a. Metric card: The primary metric is the value for the time period selected by the filter, and the secondary metric is the percentage difference for year\-on\-year and period\-on\-period.

b. Table: Place a categorical field on the dimension, and display the value for the time period selected by the filter and the percentage difference for year\-on\-year and period\-on\-period for the metric.

(2) View the increase or decrease in data for each time period.

Line chart: Place the 'date' field on the dimension, and display the value for the time period selected by the filter and the difference for year\-on\-year and period\-on\-period for the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d0062bb63ad4e5aaa83706535ebb5cb~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

**Step 1**: Select the analysis tab and click the year\-on\-year and period\-on\-period icon.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff6e481dc52b43719851f34bcd72de94~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Select the date as the basis. By default, the first date field in the dimension is used. If the dimension does not contain a date field, the default is "p_date".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2398271bd434b658e056f9c21415eae~tplv-goo7wpa0wc-image.image) </span>

Multiple metrics can be selected for calculation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08746b27411243579c69432bac7a9b59~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Select the calculation basis. The default is "period\-on\-period".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3618cf085134b28b47d677fd89c3ed4~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Select the calculation type. There are three types: "percentage difference", "difference value", and "original value". The following examples illustrate the differences among the three types. The default is "percentage difference".

Percentage difference: (today \- yesterday) / yesterday

Difference value: today \- yesterday

Original value: yesterday

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4470a26bafb342a083df2dfb5d2c1d7e~tplv-goo7wpa0wc-image.image) </span>

**Step 5:**  Click to view the calculation rules  **.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/131a77cc8702464288bf85bb07d12c29~tplv-goo7wpa0wc-image.image) </span>

**Step 6**: Click "Apply" to add a new value to the metric. To set different calculation methods for different metrics, continue adding additional period\-on\-period comparisons.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e18db2a93a394eb2ba4786ce79ae1a08~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-依据日期"></span>
## 3.1 Date field

The date field serves as the reference time field for calculating year\-on\-year and month\-on\-month comparisons, and only supports fields of the date type.

**The selectable range includes date fields in dimensions, filters, and "p_date"** , with the first date field in the dimensions used by default. If there is no date field in the dimensions, "p_date" is used by default.

**Advanced configuration:**  Supports shifting the date by year as the time granularity, enabling calculation of metrics for the same period N years ago using year\-on\-year and month\-on\-month comparisons.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf63a12de265480c9433e4b3579c92f4~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the required field is not in the dropdown menu, please confirm the following:</div>


<div data-tips="true" data-tips-type="warning">(1) Whether the field has been changed to date type;</div>


<div data-tips="true" data-tips-type="warning">(2) Whether the field has been configured in the dimension or filter panel.</div>


<span id="_3-2-计算指标"></span>
## 3.2 Calculated metrics

Calculated metrics are the metric fields that require year\-on\-year or month\-on\-month calculation. By default, all metric fields are included. If there are no metric fields, period\-on\-period comparisons cannot be configured.

<span id="_3-3-计算方式"></span>
## 3.3 Calculation methods

The calculation method sets the comparison period for period\-on\-period analysis, including five options: month\-on\-month, week\-on\-week, month\-on\-month for the previous month, and so on.


* **Month\-on\-month**: Month\-on\-month analysis compares the data of a given period with that of the previous period, and does not have special requirements for the type of the date field. For example, if the date field type is day, today's data is compared with yesterday's data; if the date field type is month, this month's data is compared with last month's data.

* **Week\-on\-week**: When the date field type is day, week\-on\-week comparison can be set. For example, the data for this Thursday is compared with the data for last Thursday.

* **Month\-on\-month for the previous month**: When the date field type is day, month\-on\-month for the previous month can be set. For example, the data for the 12th of this month is compared with the data for the 12th of last month.

   Note: Special case for daily year\-on\-year calculation—when this month has 30 days and last month has 31 days, the calculation logic compares the 30th of this month with the 30th of last month.

* **Year\-on\-year**: When the date field type is day, year\-on\-year comparison can be set. For example, today's data this year is compared with today's data last year.

* **Fixed date**: The configured fixed time interval must match the granularity of the reference date. For example, when the dimension is set to a quarterly level, you need to select data from a specific quarter as the fixed baseline, and all dates are compared against this date.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a1e62e9c7c4b378d0822fa8ae18918~tplv-goo7wpa0wc-image.image) </span>


* **Dynamic date**: The comparison date for "dynamic date" is a relative time based on the reference date, and you can select a time before or after the reference date. For example, 1 day before or 2 months after. There are no special requirements for the type of the reference date field. For example, when "Custom" is set to 3 days before, the data for July 5 is compared with the data for July 2.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9b9aedcf5a8458bbad94fc14a938bb8~tplv-goo7wpa0wc-image.image) </span>


* **Advanced configuration**: Through advanced configuration, you can set each dimension date value to be compared with the beginning or end of its current or previous year, quarter, or month for year\-on\-year or period\-on\-period analysis.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cb32aeca7d143499019a4fbbbe8ad6f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-计算类型"></span>
## 3.4 Calculation types


* **Difference percentage:**  Difference percentage = (Current data \- Baseline data) / Baseline data.


For example: The year\-on\-year difference percentage for this Thursday compared to last Thursday = (Data for this Thursday \- Data for last Thursday) / Data for last Thursday.


* **Difference value:**  Difference value = Current data \- Baseline data.


For example: The year\-on\-year difference value for this Thursday compared to last Thursday = Data for this Thursday \- Data for last Thursday.


* **Original value:**  Original value = Baseline data.


For example: The year\-on\-year original value for this Thursday compared to last Thursday = Data for last Thursday.

<span id="_3-5-快捷配置"></span>
## 3.5 Quick configuration

<span id="_3-5-1-快速同环比"></span>
### 3.5.1 Quick year\-on\-year and period\-on\-period comparison

For the year\-on\-year and period\-on\-period comparison feature, the system supports quick configuration. You can use **Quick year\-on\-year and period\-on\-period comparisons** to improve operational efficiency. The steps are as follows:

**Step 1**: Configure the relevant metrics on the visual query page.

**Step 2**: Click the dropdown button on the left side of the metric dimension.

**Step 3**: Click Quick year\-on\-year and period\-on\-period comparison and complete the relevant configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19d64da2303c4b02926a03bbd27c2f25~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-2-差异值贡献"></span>
### 3.5.2 Difference value contribution

Quick year\-on\-year and period\-on\-period comparison adds the ability to calculate difference value contribution. Difference value contribution = Current difference value / Total difference value.

To quickly calculate the difference value contribution, follow the steps below.

**Step 1**: In Quick year\-on\-year and period\-on\-period comparison, click the **Difference value contribution** button.

**Step 2**: Create period\-on\-period analysis for the difference value, and hide this capsule.

**Step 3**: Configure table calculation for the derived capsule of this difference value as follows:

(1) Calculation type: Percentage of total

(2) Calculation metric: Derived capsule of the difference value

(3) Unit calculation area: The default value of 'unit calculation area' when creating a table calculation in the current chart.

(4) Addressing direction: The default value of 'addressing direction' when creating a table calculation in the current chart.

(5) Do not enable secondary table calculation.

**Caution**: If the calculation type of quick period\-on\-period analysis includes both 'difference value contribution' and 'difference value', only one derived capsule for the difference value is generated, not two. And because you selected the difference value, the capsule for the difference value will not be hidden this time.

<span id="_4-使用实例"></span>
# 4. Usage example

When using the period\-on\-period analysis feature in practice, there is a scenario where the current month is not yet complete. For example, today is 2022\-5\-20, and the cumulative data for this month is from 2022\-5\-1 to 2022\-5\-19. To view the year\-on\-year data range from 2022\-4\-1 to 2022\-4\-19, proceed as follows:

(1) The data is as follows: the total for April is 30, and the total for May is 19.

(2) Drag the date into the filter, and set the time to 'This Month'.

(3) Select Analysis – Period\-on\-period, and you can view the data from the previous month (2022\-4\-1 to 2022\-4\-19) for comparison.
