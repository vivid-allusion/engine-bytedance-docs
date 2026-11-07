---
title: "Metric Field Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Metric_Field_Configuration"
---

<span id="_1-指标字段配置概述"></span>
# 1. Overview of metric field configuration

In the **visual query** module of Intelligent Data Insight, **fields are categorized into two concepts: "dimension" and "metric"** . Text or time data is recognized as dimension fields by default, while numeric data is recognized as metric fields by default. In actual use, dimension and metric fields can be converted to each other. This article introduces the specific capabilities of **metric field configuration**.

<span id="_2-指标字段配置具体介绍"></span>
# 2. Detailed introduction to metric field configuration

<span id="_2-1-设置聚合方式"></span>
## 2.1 Set aggregation method

**Function description**: Metric fields display aggregated results in charts. The aggregation method of metric fields (the field itself must not contain an aggregation function) can be modified.

**Default state**: Metric fields are aggregated by "sum" by default.

**Scope of use**: Metric fields without aggregation functions in the expression.

**Example:** 


* If the metric field is `Order Amount`, the aggregation method can be set.

* If the metric field is count(`Order ID`), which contains the aggregation function count, then the aggregation method for this field is "count" and cannot be set to other aggregation methods.


**Aggregation methods**: The system supports the following aggregation methods. Among them, "count distinct (fast)" is supported from version V2.50.0 and later.


* Sum (default state)

* Count


Example: For the Name field, if the detailed results are "Zhang", "Li", "Zhang", the "count" aggregation result is 3.


* Count distinct (fast): Uses the uniq function for fast calculation, resulting in an approximate value. Performance is better when querying large amounts of data.

* Count distinct:


Example: For the Name field, if the detailed results are "Zhang", "Li", "Zhang", the "count distinct" aggregation result is 2.


* Average

* Maximum

* Minimum

* Variance

* Standard deviation

* Quantile: Supports 1%, 5%, 10%, 25%, 50% (median), 75%, 90%, 95%, and 99% quantiles.


\*Quantile meaning: Sort the data in ascending order. The data at the nth percentile position is the nth percentile of the dataset. For example, among the five data points 1, 3, 5, 7, and 9, the 50% quantile is the third number, 5.

**Operation steps**:


* Click the field

* Select "Aggregation method"

* Select the required aggregation method, such as "maximum"


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/913e464898f84945a498bba9c278ae96~tplv-goo7wpa0wc-image.image) </span>


* Modification completed


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c6966c9150040108e3ba11978b4f6bf~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Caution** : The current version does not support changing the aggregation method for metrics that already contain aggregation functions.

<span id="_2-2-设置数据格式"></span>
## 2.2 Set data format

**Note** : You can set the numeric format for numeric fields.

**Scope of use** : Numeric fields (either original numeric fields or fields whose expression results are numeric)

**Default state** : The default format for integers is the original value; the default format for decimals is to retain 4 significant digits, include thousand separators, and display numbers without units

**Data format** :


* Number (default option for decimals):

   * Numeric unit: Supports thousand, ten thousand, million, ten million, hundred million; K (Thousand), M (Million), B (Billion)

   * Decimal places: Default is 4

   * Significant digits for decimal places: If this option is selected, the number of significant digits after the decimal point equals the set number of decimal places. Not selected by default

      * Example: 12345.0012345

         * Decimal places set to 3, "Significant digits for decimal places" not selected, result is 12345.001

         * Decimal places set to 3, "Significant digits for decimal places" selected, result is 12345.00123

   * Thousand separator

      * Example: 123456789.123456789

         * "Include thousand separator" selected, result is 123,456,789.123456789

         * "Include thousand separator" not selected, 123456789.123456789

* Percentage:

   * Decimal places: Default is 2

   * Significant digits for decimal places: If this option is selected, the number of significant digits after the decimal point equals the set number of decimal places. Not selected by default

      * Example: 12345.0012345%

         * Decimal places set to 3, "Significant digits for decimal places" not selected, result is 12345.001%

         * Decimal places set to 3, "Significant digits for decimal places" selected, result is 12345.00123%

* Per mille: Configurable options are similar to percentage

* Original value (default option for integers): Uses the data format from the database

* Number, percentage, and per mille support prefix/suffix for data


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/525a099999964756b11294ae6595d713~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eff1d38552cb4cd3a7dccbd281239a64~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is available in version V2.42 and later.</div>



* The data format of fields supports customization


In the field settings of visual queries, users can configure different data formats for the same field data based on conditions. In customization, set the required conditions and define the rules for displaying data from different time ranges as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36f92c4eb8824afbb6268b6249cd1b76~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is available in version V2.56 and later.</div>


**Operation steps** :


* Click the field to bring up options

* Select "Set data format"


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/525a099999964756b11294ae6595d713~tplv-goo7wpa0wc-image.image) </span>


* Switch the data format in the pop\-up window and configure as needed. For example, change the number of decimal places to 2.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b120225d0794c8aab4e80df9687f868~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* After configuration is complete


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0b2656758a74db9b8401a818a86f926~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-3-解析文本"></span>
## 2.3 Parse text

Fields support parsing content in specific formats.


* Images, videos: When the field content is a link to an image or video, parsing as an image or video allows you to preview the image or video online.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3936e7183fe421cb70dbeef50cae9b2~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ab3f987479548ddb142334c04d7e464~tplv-goo7wpa0wc-image.image" width="2938px" /></div>



* Links: When parsing field content as a link, clicking the cell opens a new tab and accesses the cell content as a link.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a552c088a84e34a7416722fe820936~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-设置条件格式"></span>
## 2.4 Set conditional formatting

Conditional formatting allows you to mark cells with colors or icons, making important or abnormal data more prominent. The platform supports four types of conditional formatting for tables: single color, icon set, color scale, and data bar. Date fields also support conditional formatting configuration.

**Supported scope: tables and detail tables.** 

**Operation steps**:


* Click the field

* Click "Conditional formatting"


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03c73517e5ad42ef98cc103f5bc64bd3~tplv-goo7wpa0wc-image.image) </span>

**Caution**: The configuration of icon set, color scale, and data bar conditional formatting for dimension fields is based on the metric fields dragged into the query.


* Single color:

   * The single color feature allows you to set the text and background color of cells that meet the conditions individually. It supports multiple condition settings and rule additions to meet more business needs.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2902814eb0a544358ddfd3df455f4d2c~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* The selectable fields for single color are dimensions or metrics in the table. Time\-type data cannot be used as conditions for single color configuration.

* The default scope of single color is the cell. Starting from version V2.42, you can choose to apply it to either the cell or the entire row.



|Monochrome applies to: [Cell] |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99359ae3fec34b87b0a3f66125b623f6~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4146c465b1a64266b2008c4ee4979cda~tplv-goo7wpa0wc-image.image) </span> |
|---|---|---|
|**Monochrome applies to: [Entire row]**  |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ad45b1c83d34408942ecb4249af6173~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5aeebb814810484bb23ad46bf42dd075~tplv-goo7wpa0wc-image.image) </span> |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When the same cell contains both cell\-level and entire\-row single\-color conditional formatting rules that conflict, the cell\-level rule takes precedence over the entire\-row rule.</div>


* <div data-tips="true" data-tips-type="warning">When the same cell has multiple conflicting entire\-row single\-color conditional formatting rules, the rule corresponding to the field that appears earlier in the table takes precedence. As shown in the figure below, with the same settings, changing the field order will result in different display outcomes.</div>



<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/650b5bd0436f4217aa5e8eb429f59c1e~tplv-goo7wpa0wc-image.image" width="1464px" /></div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab3262374e394de4b207d444e0bc715f~tplv-goo7wpa0wc-image.image" width="1482px" /></div>


<div style="text-align: center">
<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8df5fbf3a773443085f214a1583929f0~tplv-goo7wpa0wc-image.image" width="358px" /></div>
</div>



* Icon set: Icon sets allow for more intuitive categorization and display of data. Data is divided into several categories by thresholds, and data in the same category is displayed with the same icon set.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a630992b98474565bc7fbc7c0aaed9bb~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8fc2e6968d84af48be62ddc95ae1f70~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Color scale: Color scales help users better understand the distribution of data. The larger the value, the closer the cell color is to the color corresponding to the maximum value; the smaller the value, the closer the cell color is to the color corresponding to the minimum value.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae12b30bcecb4af2b56980d5ed78905b~tplv-goo7wpa0wc-image.image) </span>


* For scenarios with outliers or where a customized color scale is needed, users can configure the maximum and minimum values themselves.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67f53b05635a4e09a48deb8ad63cd445~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

* Data bar: Data bars help users identify larger or smaller values. The longer the data bar, the larger the value; the shorter the data bar, the smaller the value. You can set the minimum value (the starting position of the data bar) and the maximum value (the end position of the data bar) to make the data bar better adapt to different data distributions.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc7241b0875b4dadac0e97df572c4a04~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fe899fffec74a03b57d860049169534~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Effective for the total function. When [Total](https://docs.byteplus.com/docs/DataWind/Total) is used in the table and there is a total row, you can configure whether the conditional formatting applies to the total row. By default, conditional formatting applies to the total row.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63ba1355361e46efaa52985873979c3c~tplv-goo7wpa0wc-image.image) </span>


* Click the corresponding conditional formatting setting to select or deselect "Apply to total". If you apply after deselecting "Apply to total", the conditional formatting will not be displayed in the total row.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b93e24271a654279a28dfae4ea6c1f87~tplv-goo7wpa0wc-image.image" width="575px" /></div>



* You can customize the display style and direction of the data bar.


<span id="_2-5-视觉样式"></span>
## 2.5 Visual style

To make the table display style more diverse, you can set the header text, header background color, body text, and alternating row text.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a285cfa755e42febf1db8a564d6c8ac~tplv-goo7wpa0wc-image.image) </span>

**Supported scope**: Table, detailed table


|**Edit visual style function module** |**Function** |**Achieved effect** |
|---|---|---|
|Header text |You can set the font size, bold, italic, and color of the header text. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79b5a573d16d45d2b8b38b628d5851d9~tplv-goo7wpa0wc-image.image) </span> |
|Header background color |You can change the header background color. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57421ca09642427bb1c53f23f415c718~tplv-goo7wpa0wc-image.image) </span> |
|Body text |You can set the font size, bold, italic, and color of the actual data in the table body. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/905f9b17129c4f199ff79b894f681852~tplv-goo7wpa0wc-image.image) </span> |
|Body alternating row color |You can set the background color for alternating rows of actual data in the table body. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c8405b531de4096a2fdff5ac7fd3b9d~tplv-goo7wpa0wc-image.image) </span> |
|Restore default |Reset with one click, restoring the header and table settings to default. | |


<span id="_2-6-隐藏字段"></span>
## 2.6 Hide fields

**Function description**: You can hide columns or fields that are required for the chart but should not be displayed, to avoid showing redundant information.

**Scope of use**: Any field in a table or detailed table can be hidden; indicator fields in pivot tables or other charts can also be hidden.

**Operation steps**:


* Click the field and select "Hide field".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bd5557aca774172b79748e2dcc67728~tplv-goo7wpa0wc-image.image) </span>

* The field is hidden. If the chart type is a table, the field is hidden; if the chart type is not a table, the corresponding indicator is not displayed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/526ed290b7214beb92b7452cfcbf59f7~tplv-goo7wpa0wc-image.image) </span>
