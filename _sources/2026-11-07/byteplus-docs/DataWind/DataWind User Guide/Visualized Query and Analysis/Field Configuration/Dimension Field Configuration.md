---
title: "Dimension Field Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dimension_Field_Configuration"
---

<span id="_1-维度字段配置概述"></span>
# 1. Overview of dimension field configuration

In the **visual query** module of Intelligent Data Insight, **fields are divided into two concepts: "dimension" and "measure"** . Text/time data is recognized as dimension fields by default, while numeric data is recognized as measure fields by default; in actual use, dimension and measure fields can be converted to each other. This article introduces the specific capabilities of dimension field configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b54a5988c0bd45cf9026c6a7fa4b8fd0~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-设置日期类型"></span>
## 2.1 Set date type

**Feature description**: For date fields, setting the date type is supported. By default, data is displayed by "day". Supports truncated dates (for example, if "month" is selected, measures from 2020\-01\-01 to 2020\-01\-30 will be aggregated and displayed under the 2020\-01 dimension) and extracted dates (for example, if "week" is selected, 2020\-01\-01 is a Wednesday and will be displayed as 3).

**Default state**: Displayed by "day". For example, 2020\-01\-01.

**Scope of use**: Date\-type fields. The system will identify fields that meet the criteria as date fields based on the field expression.

**Operation steps**:


* Click the field

* Select "Date type"

* Select the required date type to configure


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4468f3b2a9f4d8086514e1127d71c63~tplv-goo7wpa0wc-image.image) </span>

**Date types**:


* Year: Supports custom fiscal years. For example: When the year is set from April to March of the following year, 2013\-07\-01 will be displayed as 2013.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bc5527210844209b4c2133c05d2981b~tplv-goo7wpa0wc-image.image) </span>


* Year\-month\-day (day): For example, 2020\-01\-01

* Year\-bimonth: Supports aggregation by bimonth. For example, 2013\-11\-15 will be displayed as 2013\-11/12

* Year\-biweek: Supports aggregation by biweek. The start date of the biweek can be adjusted as needed (Monday to Sunday, Tuesday to Monday, and so on). For example, 2013\-11\-26 will be displayed as 2013\-W47/48. Click Advanced Settings to configure the aggregation method for the starting week of the biweek.

> The week containing the first Thursday of each year is considered the first week of that year (for example, if January 1 is a Friday, the following week is the first week; if January 1 is a Thursday, the week containing January 1 is the first week).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d9ff855029142d18cc408e5894101c8~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32e0ffd4fa3345888586b12653cbf750~tplv-goo7wpa0wc-image.image" width="614px" /></div>



* Year\-week (custom week): Supports custom weeks, displayed as year\-week number. For example, 2021\-08\-01 will be displayed as 2021\-30 (07/26\-08/01)

* Custom week: Select as needed from Monday to Sunday, Tuesday to Monday, Wednesday to Tuesday, and so on, or Sunday to Saturday


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b493d5f654c74fd79bfe49d5c23ce756~tplv-goo7wpa0wc-image.image) </span>


* Month: That is, from the 1st to the last day of each month

* Week: A date extraction type. For example, 2020\-01\-01 is Wednesday, displayed as the number 3.


<span id="_2-2-日期显示格式"></span>
## 2.2 Date display format

**Function description**: When selecting a date, you can customize how the date data is displayed.

**Scope of use**: Date\-type fields

**Default state**: The default display format is YYYY\-MM\-DD

**Operation steps**:


* Click the field

* Select "Date display format"

* Select the required date format


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc88ef0fda26445881be4ad531fff5dc~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-日期补全"></span>
## 2.3 Date completion

**Function description**: When there is no data for certain days' indicators in the selected date range, you can use the date completion feature to display those dates.

**Scope of use**: Date\-type fields. The product will identify fields that meet the criteria as date fields based on the field expression

**Default state**: Off, that is, dates without data are not displayed by default

**Operation steps**: In the following charts


* Click the field, select "Date completion" \- "Show", and dates without data will also be displayed.
