---
title: "Raw-Data Table"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Raw-Data_Table"
---

<span id="_1-概述"></span>
# 1. Overview

A raw\-data table is a table used to display detailed data. Users can click the raw\-data table, select the required fields, and the corresponding detailed data will be automatically associated and displayed.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

Typically used in scenarios where detailed data needs to be displayed.

**Table example:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61eaec2d8d7c4f358c6b949a15390601~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Usage process example

**Step 1: Select Chart Panel \- Raw\-data Table**

**Step 2: Set the dimensions and metrics to be displayed, and configure filter conditions**

Select the dimensions "Province", "City", "Transaction Date", "type", and "sale_order"

**Step 3: Modify the chart format as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/814cffeb080a4e149c3cfa07b3493378~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-明细表图标"></span>
## 3.1 Raw\-data table icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aeff0bd1c9945b9979e0f1df1452832~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

**Dimension**: Supports zero or more dimensions.

**Metric**: Supports zero or more metrics.

Dimensions and metrics are displayed in the raw\-data table according to the order in the data panel. Metrics are not aggregated.

<span id="_3-3-图表配置"></span>
## 3.3 Chart configuration

<span id="_3-3-1-基本格式"></span>
### 3.3.1 Basic format


* Serial number: Adds a serial number before each data entry, allowing users to quickly locate a specific row when there are many entries.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e59c307cc2041e6993575675e7a963e~tplv-goo7wpa0wc-image.image) </span>


* Row\-column transpose: By default, data is displayed horizontally. After selecting "Row\-column transpose", data is displayed vertically.

* **Caution: Row\-column transpose is available only when the number of data entries is 100 or fewer. If there are more than 100 entries, this option cannot be configured.** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f44a70c168d14e6ca2683ae593d24170~tplv-goo7wpa0wc-image.image) </span>


* Auto wrap: When the text exceeds the table width, the text is abbreviated by default. To display more or all text, extend the table width or enable auto wrap.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/600e389f3f8a4f929c39a9ac20eb546e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-2-翻页器"></span>
### 3.3.2 Paginator

When there are many data entries, a paginator can be configured for the table. The paginator supports a minimum of 10 entries per page and a maximum of 100 entries per page. In V2.91.0 and later versions, after configuring the paginator, the table supports displaying 1k, 2k, 5k, 10k, 20k, 30k, 40k, and 50k entries, or manually entering a positive integer (up to 50k) for the number of entries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5569e8b3e43340208d86e8970e01545d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-3-文字对齐"></span>
### 3.3.3 Text alignment

The default alignment is "AUTO", which means text and dates are left\-aligned, and numbers are right\-aligned. The overall alignment can be adjusted as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1b2c65df4e944feb829d9cd7d51e2c2~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-4-表格样式"></span>
### 3.3.4 Table style

The color of the table header, cell text, and grid lines can be configured.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56dfd9e2fe764353933c3b9b1464eaf7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-5-网格线"></span>
### 3.3.5 Gridlines

You can adjust the color, line width, and line style for the table's outer border, as well as for horizontal and vertical gridlines.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcb170e6a1c94d1c9415894d74520293~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-6-特殊值"></span>
### 3.3.6 Special values

You can customize settings for special values of dimensions or measures. If the field originates from a dimension, it is processed as a dimension; if it originates from a measure, it is processed as a measure. You can set the display style for special values as blank, NULL, 0, or \-\-.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cdef8ec341d4039abc845bde4fbe049~tplv-goo7wpa0wc-image.image) </span>

Caution: When the parsed text of a raw\-data table is an image, if the image can be displayed, the corresponding image will be shown in the raw\-data table; if the image cannot be displayed, the raw\-data table will show a blank.

<span id="_3-3-7-显示模式"></span>
### 3.3.7 Display mode

The display mode can be customized to adjust the table's appearance according to actual needs, including:


* Column width: Fit to content, fit to container, or custom

* Row spacing/column spacing: Comfortable (default spacing, 8 pixels), efficient (narrower, 4 pixels), or custom

> Manually set column width: each column will have the specified width, in pixels.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91998822f93e4fa783fc13b8b47b8413~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-8-图内控件样式"></span>
### 3.3.8 In\-chart control style

In\-chart controls include in\-chart filters, dynamic dimensions/measures, and in\-chart parameters. After displaying them in the chart, you can adjust the arrangement of titles and filter content, as well as the layout settings. The following figure shows dynamic dimensions arranged vertically.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/230517dbc6ca4a78bc531dc386360375~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-9-恢复默认设置"></span>
### 3.3.9 Restore default settings

Click Restore Default Settings to revert all the above chart configuration items to their default values.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c64b37e222bc4f6fbaf77bc2c09bf4d0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-字段配置"></span>
## 3.4 Field configuration

<span id="_3-4-1-解析文本"></span>
### [3.4 Parse text](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-4-%E8%A7%A3%E6%9E%90%E6%96%87%E6%9C%AC)

<span id="_3-4-2-条件格式"></span>
### [3.5 Set conditional formatting](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-5-%E8%AE%BE%E7%BD%AE%E6%9D%A1%E4%BB%B6%E6%A0%BC%E5%BC%8F)

<span id="_3-4-3-编辑视觉样式"></span>
### [3.6 Visual styles](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-6-%E8%A7%86%E8%A7%89%E6%A0%B7%E5%BC%8F)

<span id="_3-5-表格"></span>
## 3.5 Table

<span id="_3-5-1-调整列宽"></span>
### 3.5.1 Adjust column width

Drag the divider between two columns in the table with the mouse to adjust the column width.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8dad1eab85542a8817e1664692afa67~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-2-列排序"></span>
### 3.5.2 Column sorting

When you hover the mouse over the column name in the table header, the column sorting button will appear. Click the button to sort the column content; click again to cancel sorting.

**Caution: If "Top N" is used in the analysis, the "Top N" operation takes precedence over column sorting in the table.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/925d001120ad4d218a8f174bd067c2c8~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-3-冻结列"></span>
### 3.5.3 Freeze columns

When there are many columns, you can fix the position of a column you are particularly interested in. When scrolling left or right to view other columns, the frozen column and columns to its left will remain stationary.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fca0586c818a4226b8eeebef772f2219~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-图表切换"></span>
## 3.6 Chart switching

<span id="_3-6-1-从表格切换到明细表"></span>
### 3.6.1 Switch from table to raw\-data table


* Place the fields of dimensions and metrics into columns in the order of dimensions and metrics.

* Filter out metrics that are not present in the filter criteria/results; retain detail filters for metrics and filters for dimensions.

* Clear the configuration of the analysis panel.

   **Before switching: table**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b631dbfa44f24a288e54faa418f881db~tplv-goo7wpa0wc-image.image) </span>

**After switching: raw\-data table**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55c55dfe1bcb4d4b98f77fe766a858ab~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-2-从明细表切换到表格"></span>
### 3.6.2 Switch from raw\-data table to table


* Place the fields in the columns into the dimensions or metrics of the table according to whether they are dimensions or metrics, and assign the default aggregation method to metrics.

* Restore the filter content as is.

* Clear the configuration of the analysis panel.

   **Before switching: raw\-data table**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55c55dfe1bcb4d4b98f77fe766a858ab~tplv-goo7wpa0wc-image.image) </span>

   **After switching: table**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b631dbfa44f24a288e54faa418f881db~tplv-goo7wpa0wc-image.image) </span>
