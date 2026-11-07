---
title: "Overview of Field Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Overview_of_Field_Configuration"
---

<span id="_1-概述"></span>
# 1. Overview

In the **visual query** module of Intelligent Data Insight, **fields are divided into two concepts: "dimension" and "measure"** . Text or time data is recognized by default as dimension fields, while numeric data is recognized by default as measure fields. In actual use, dimension and measure fields can also be converted to each other. A field is a concept used to describe and store data.

After selecting the dimension and measure fields to query, users can click a specific field for further configuration. Intelligent Data Insight supports a wide range of field configuration options. For example, for all fields, modifying the display name is supported; for date fields, setting the date type is supported; for measure fields, the aggregation method can be changed; for numeric fields, the data format can be modified, and more.

This article will help you understand the **general configuration of field settings**. For specific configurations of dimensions and measures, refer to separate documentation.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-单个字段修改"></span>
## 2.1 Modify a single field

To change the display name of a field in the chart, follow these steps to modify the display name.

<span id="_2-2-点击字段呼出字段设置选项"></span>
## 2.2 Click the field to open field settings options

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11257cecf6024c368c5115eb17c6684b~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-选择设置字段信息-格式等"></span>
## 2.3 Select to configure field information, format, and more

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4165dcb4e4644e79b671bb1e1b6e77c9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-在弹出窗口中进行修改并确认"></span>
## 2.4 Modify and confirm in the pop\-up window

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2effc983bccc465dafe1fe547d486192~tplv-goo7wpa0wc-image.image" width="504px" /></div>


<span id="_2-5-字段批量修改"></span>
## 2.5 Batch modify fields

You can batch adjust the format and information of configured dimensions or measures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64eedbe8bca04de89db43687e9b22e7a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-点击配置栏的设置按钮"></span>
## 2.6 Click the settings button in the configuration bar

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99e7d18b803841389d2ea5339d0040bd~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-7-在弹出窗口中批量修改字段信息并确认"></span>
## 2.7 Batch modify field information and confirm in the pop\-up window

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64eedbe8bca04de89db43687e9b22e7a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-字段通用配置介绍"></span>
# 3. Introduction to general field configuration

<span id="_3-1-设置字段信息"></span>
## 3.1 Configure field information

**Feature description**: The display name of a field defaults to the field name. To modify the display name, click "Change display name". Additionally, you can add remarks to a field to help viewers understand the field definition. **Scope of use**: All fields **Operation steps**:


* Click the field and select "Configure field information"

* Enter the new name you want to use, and click "OK" to apply the change, such as changing the field name to "Date".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bef345af1c3b489a8a0767c8a85a32c7~tplv-goo7wpa0wc-image.image" width="504px" /></div>



* After modification, the field name in the chart will become "Date".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ef4ab1f14494a368fce0843b2be7611~tplv-goo7wpa0wc-image.image) </span>


* To restore the default, click "Restore default" in the lower left corner and then click "OK" to confirm.

* Check "Display field description", enter the description information, and confirm.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd6a77846d8d464f829d080a727410a0~tplv-goo7wpa0wc-image.image" width="442px" /></div>



* After modification, an underline will appear under the field in the chart, and hovering the mouse over the field will display the description information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a54244d4ee6647ffbc3b5b0a76a766b6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-维度字段配置"></span>
## 3.2 Dimension field configuration

For details, see [Dimension Field Configuration](https://docs.byteplus.com/docs/DataWind/Dimension_Field_Configuration).

<span id="_3-3-指标字段配置"></span>
## 3.3 Metric field configuration

For details, see [Metric Field Configuration](https://docs.byteplus.com/docs/DataWind/Metric_Field_Configuration).

<span id="_3-4-解析文本"></span>
## 3.4 Parse text

Fields support parsing content in specific formats.


* When the field content is an image or video link, parsing it as an image or video enables online preview.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/593ebe168cd54842b9dac5c305df85d5~tplv-goo7wpa0wc-image.image) </span>

Note: If the image link is cross\-domain, an error may occur as shown in the following figure.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ab3f987479548ddb142334c04d7e464~tplv-goo7wpa0wc-image.image) </span>


* When the field content is parsed as a link, clicking the cell opens a new tab and accesses the cell content as a link.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a552c088a84e34a7416722fe820936~tplv-goo7wpa0wc-image.image) </span>


* The original template link feature has been replaced by the chart jump feature, which must be configured on the dashboard. See [Chart Redirect](https://docs.byteplus.com/docs/DataWind/Chart_Redirect) for instructions.


<span id="_3-5-设置条件格式"></span>
## 3.5 Set conditional format

Conditional format allows you to mark cells with colors or icons, making important or abnormal data more prominent. The platform supports four types of conditional format for tables: single color, icon set, color scale, and data bar.

**Supported tables: table, detail table, pivot table (currently only single color is supported).** 

**Operation steps**:


* Click the field

* Click "Conditional format"


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03c73517e5ad42ef98cc103f5bc64bd3~tplv-goo7wpa0wc-image.image) </span>

**Caution**: The configuration of icon set, color scale, and data bar conditional format for dimension fields is based on the metric fields dragged into the query.


* Single color:

   * The single color feature allows you to set the text and background color of cells that meet the conditions individually. It supports multiple condition settings and the addition of multiple rules to meet more business needs.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5ca1346d2ce443eb31129c03d2c8adc~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a61539a1c98742ec8612f29b682d3753~tplv-goo7wpa0wc-image.image) </span>


* Fields available for monochrome are dimensions or metrics in the table; time data cannot be used as a condition for monochrome configuration.

* The default scope of monochrome is a cell. Starting from version V2.42, the scope can be set to either a cell or the entire row.



|Monochrome scope selection: [Cell] |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99359ae3fec34b87b0a3f66125b623f6~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4146c465b1a64266b2008c4ee4979cda~tplv-goo7wpa0wc-image.image) </span> |
|---|---|---|
|**Monochrome scope selection: [Entire row]**  |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ad45b1c83d34408942ecb4249af6173~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5aeebb814810484bb23ad46bf42dd075~tplv-goo7wpa0wc-image.image) </span> |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If a cell has both cell\-level and entire\-row monochrome conditional format conflicts, the cell\-level priority is higher than the entire\-row priority.</div>


* <div data-tips="true" data-tips-type="warning">If a cell has multiple entire\-row monochrome conditional format conflicts, the field order in the table determines priority, with earlier fields taking precedence. As shown in the figure below, with the same settings, adjusting the field order will result in different display outcomes.</div>



<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/650b5bd0436f4217aa5e8eb429f59c1e~tplv-goo7wpa0wc-image.image" width="1464px" /></div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab3262374e394de4b207d444e0bc715f~tplv-goo7wpa0wc-image.image" width="1482px" /></div>


<div style="text-align: center">
<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8df5fbf3a773443085f214a1583929f0~tplv-goo7wpa0wc-image.image" width="358px" /></div>
</div>



* Icon sets: Icon sets provide a more intuitive way to categorize and display data. Data is divided into several major categories based on thresholds, and data in the same category is displayed using the same icon set.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a630992b98474565bc7fbc7c0aaed9bb~tplv-goo7wpa0wc-image.image) </span>


* Color scales: Color scales help users better understand the distribution of data. The larger the value, the closer the cell color is to the color corresponding to the maximum value; the smaller the value, the closer the cell color is to the color corresponding to the minimum value.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9202ed9f21e8452396464e5987c792f0~tplv-goo7wpa0wc-image.image) </span>


* For scenarios with outliers or requiring customized color scales, users can configure the maximum and minimum values themselves.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97251604db6948738d58d6473ea1e81b~tplv-goo7wpa0wc-image.image" width="475px" /></div>



* Data bars: Data bars help users identify larger or smaller values. The longer the data bar, the larger the value; the shorter the data bar, the smaller the value.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f52db4092706499697bfc799c30338ef~tplv-goo7wpa0wc-image.image) </span>


* This is effective for the total function. When [Total](https://docs.byteplus.com/docs/DataWind/Total) is used in the table and there is a total row, you can configure whether conditional format applies to the total row. By default, it applies to the total row.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/194b1ec17d8a43f28db1120cd9788721~tplv-goo7wpa0wc-image.image) </span>


* Click the corresponding conditional format setting to select or deselect "Apply to total". If you apply the setting after deselecting, the conditional format will not be displayed in the total row.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b93e24271a654279a28dfae4ea6c1f87~tplv-goo7wpa0wc-image.image" width="575px" /></div>


<span id="_3-6-视觉样式"></span>
## 3.6 Visual styles

To make the table display style richer, you can set the header text, header background color, body text, and alternating row text.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a285cfa755e42febf1db8a564d6c8ac~tplv-goo7wpa0wc-image.image) </span>

**Supported scope**: Table, detail table


|**Edit visual style module** |**Function** |**Effect** |
|---|---|---|
|Table header text |You can set the font size, bold, italic, and color of the table header text. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79b5a573d16d45d2b8b38b628d5851d9~tplv-goo7wpa0wc-image.image) </span> |
|Table header background color |You can change the table header background color. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57421ca09642427bb1c53f23f415c718~tplv-goo7wpa0wc-image.image) </span> |
|Table body text |Set the text font size, bold, italic, and color for the actual data in the table body |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/905f9b17129c4f199ff79b894f681852~tplv-goo7wpa0wc-image.image) </span> |
|Alternating row color in the table body |Set the background color for alternating rows of actual data in the table body |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c8405b531de4096a2fdff5ac7fd3b9d~tplv-goo7wpa0wc-image.image) </span> |
|Restore defaults |One\-click reset: restores the table header and table settings to default | |


<span id="_3-7-隐藏字段"></span>
## 3.7 Hide fields

**Feature description**: Columns or fields that are required in the chart but not displayed can be hidden to avoid displaying redundant information.

**Scope of use**: Any field in a table or detail table can be hidden; metric fields in pivot tables or other charts can also be hidden.

**Operation steps**:


* Click the field and select "Hide field".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bd5557aca774172b79748e2dcc67728~tplv-goo7wpa0wc-image.image) </span>


* The field is hidden. If the chart type is table, the fields are hidden; if the chart type is graph, the corresponding metrics are not displayed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/526ed290b7214beb92b7452cfcbf59f7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-批量配置字段"></span>
## 3.8 Batch configure fields

**Function description**: Allows batch configuration of dimension/metric fields to reduce configuration operation costs.

**Scope of use**: Supports batch configuration of dimension and metric fields; filtering is not supported.

**Operation steps**:


* Click the configuration button to open the batch configuration panel.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99e7d18b803841389d2ea5339d0040bd~tplv-goo7wpa0wc-image.image) </span>


* Select the fields to be batch configured, choose the configuration format or restore the default configuration, and click Confirm to complete the operation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1feadaf341f2489a8280bfc252b566a6~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-常见问题"></span>
# 4. Frequently asked questions

(1) Question: What is p_date?

Answer: p_date is the partition date field of the dataset. It is supported in extraction mode for dataset usage, but not available in direct connection mode. p_date represents the date when data is synchronized to the product dataset (if the upstream data does not have a date partition), or the date when data is generated in the upstream data table (the original date/p_date partition fields in the Hive table will be renamed to p_date). In visual queries, p_date can be used for selecting and filtering by date dimension according to analysis needs. By default, it is set to the most recent day with data.

(2) Question: Why is the field gray?

When the mouse hovers over the gray field capsule in the field configuration area, a prompt will display the reason why the field is gray.
