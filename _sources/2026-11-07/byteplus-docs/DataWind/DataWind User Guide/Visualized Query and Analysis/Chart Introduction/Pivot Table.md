---
title: "Pivot Table"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Pivot_Table"
---

<span id="_1-概述"></span>
# 1. Overview

A pivot table aggregates, calculates, and displays data according to column dimensions and row dimensions. By simply configuring column dimensions, row dimensions, and measures, you can display a pivot table. Compared with a table, a pivot table divides [Dimension Field Configuration](https://docs.byteplus.com/docs/DataWind/Dimension_Field_Configuration) into rows and columns, making it easier to present data in tables in multi\-dimensional scenarios.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases

Pivot tables are typically used to categorize and summarize detailed tables, and to perform data calculations based on different combinations. For example: In different regions, which categories of products are sold, and what quantities.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acec21ce3ca4449585a93d4fd8977bc3~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-使用过程示例"></span>
## 2.2 Example usage process

**Step 1: Select the chart panel \- Pivot table**

After selecting the pivot table, the data panel will change to include column dimensions, row dimensions, and measures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c26983ddc50f47e9926dc9bfd724f962~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Set column dimensions, row dimensions, and measures**

See [1. Overview of dimension field configuration](https://docs.byteplus.com/docs/DataWind/Dimension_Field_Configuration#_1-%E7%BB%B4%E5%BA%A6%E5%AD%97%E6%AE%B5%E9%85%8D%E7%BD%AE%E6%A6%82%E8%BF%B0) and [Dimension Filter](https://docs.byteplus.com/docs/DataWind/Dimension_Filtering).

Select 'Region' as the column dimension, 'Category' as the row dimension, and 'Quantity' as the measure; [Overview of Field Configuration](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/096b55238d6c4f5b8c8f74d8bdbf3666~tplv-goo7wpa0wc-image.image) </span>

**Step 3: Modify the chart style as needed**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f9e3399f6634ca2909ccd410d9730d1~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-透视表图标"></span>
## 3.1 Pivot table icon

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c26983ddc50f47e9926dc9bfd724f962~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-配置规则"></span>
## 3.2 Configuration rules

**Dimension**: Supports zero or more dimensions.

**Measure**: Supports zero or more measures. When there are more than two measures, a measure name will be generated.

**Measure name**: This is a placeholder capsule, and the measure name can be freely dragged between column dimensions and row dimensions. When there are two measures in the data panel, one measure name will be generated. When there is only one measure, the measure name will automatically disappear.

**Example**: One column dimension, one row dimension, two measures


* Measure name in column dimension


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c99a3e78a934ca88a7a5e8697f556e0~tplv-goo7wpa0wc-image.image) </span>


* Measure name in row dimension


<span id="_3-3-图表配置"></span>
## 3.3 Chart configuration

<span id="_3-3-1-基本格式"></span>
### 3.3.1 Basic format


* Supports setting the data display mode to tiled or tree display.

   * When the data display mode is set to tree, you need to select the data retrieval method as either full retrieval or incremental retrieval. The following explains the data retrieval methods:

   
   |Data retrieval methods |Description of data retrieval methods |
   |---|---|
   |Full data retrieval |Each time the pivot table loads, it retrieves all data, with an upper limit of 10,000 records (can be adjusted to 50,000 after enabling the pager). |
   |Incremental data retrieval |By default, the pivot table loads the data of the first node. Each time a new node is expanded, the data of the new node is incrementally retrieved, with a single retrieval limit of 10,000 records. At the same time, the overall data display limit of the pivot table is 10,000 records; if exceeded, only the first 10,000 records are displayed in order.<br><br>Other limitations:<br><br>a. The features in the analysis only support totals and the top N entries in TopN results.<br><br>b. When downloading, all data is always downloaded in full.<br><br>c. Incremental loading does not apply to mobile devices. |
   

* Set whether the data can automatically wrap lines.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b9db260661d4901ba3bd6ae58e0f67e~tplv-goo7wpa0wc-image.image) </span>


* Supports setting the basic format to compact mode, and also supports adjusting the arrangement in compact mode.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b901725cdb24923b8662fb019074571~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-2-翻页器"></span>
### 3.3.2 Pager


* When there are many data entries, a paginator can be configured. The paginator supports a minimum of 10 items per page and a maximum of 100 items per page.

* In V2.91.0 and later versions, the upper limit for data display can be set to 1k, 2k, 5k, 10k, 20k, 30k, 40k, or 50k records, or you can manually enter a positive integer (up to 50k) records.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f896c57d0074207a8c42355bfa57046~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-3-文字对齐"></span>
### 3.3.3 Text alignment

You can set alignment (auto, left, center, or right) separately for dimensions (rows/columns) and measures. You can make overall adjustments to the alignment here according to individual needs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b188fa8266684f8db81ad8fab2dcefc7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-4-表格样式"></span>
### 3.3.4 Table style

You can configure colors for row and column headers and the value area.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27551523b6044b9690c455d4b8ffcf2c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-5-特殊值"></span>
### 3.3.5 Special values

You can customize settings for special values of dimensions or measures, and set the display style of special values as blank, NULL, 0, or \-\-.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f7a4cef664942f89325286b7d99e414~tplv-goo7wpa0wc-image.image" width="204px" /></div>


When using the "Table Calculation" feature's "Difference" or "Difference Percentage" in the "Pivot Table", you can select "Hide rows or columns with 0 or null".

<span id="_3-3-6-显示模式"></span>
### 3.3.6 Display mode

By default, the display mode sets column width and row spacing according to the content of data items, and you can adjust the column width and row spacing.

Column width: Standard, Auto, or Custom column width (must be greater than 40, in pixels)

Row spacing: Comfort, Efficient, or Custom spacing (in pixels)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08c9a27f81b6403797dfb6b72315e244~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-7-图内控件样式"></span>
### 3.3.7 In\-chart control style

In\-chart controls include in\-chart filters, dynamic dimensions/measures, and in\-chart parameters. After displaying them in the chart, you can adjust the arrangement of the title and filter content, as well as the typography settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7b98f4ef33e426dad2997b73ccea915~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-8-恢复默认设置"></span>
### 3.3.8 Restore default settings

Click Restore Default Settings to revert all of the above chart configuration content to their default settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8cb1211dcda4aa99b18cd529b6305df~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-字段设置"></span>
## 3.4 Field settings

<span id="_3-4-1-数据支持多维度-0-个指标"></span>
### 3.4.1 Data supports multiple dimensions and zero measures

Starting from V2.50.0, the pivot table supports multiple dimensions but no measures.

<span id="_3-4-2-解析文本"></span>
### 3.4.2 Parse text

See [3.4 Parse text](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-4-%E8%A7%A3%E6%9E%90%E6%96%87%E6%9C%AC)

<span id="27fca474"></span>
### 3.4.3 Conditional formatting

See [3.5 Set conditional formatting](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-5-%E8%AE%BE%E7%BD%AE%E6%9D%A1%E4%BB%B6%E6%A0%BC%E5%BC%8F).

<span id="_3-4-3-指标条件格式"></span>
### 3.4.4 Measure conditional formatting

See [3.5 Set conditional formatting](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-5-%E8%AE%BE%E7%BD%AE%E6%9D%A1%E4%BB%B6%E6%A0%BC%E5%BC%8F).

<span id="_3-4-4-行列钻取设置"></span>
### 3.4.5 Row and column drill settings

Click the downward triangle icon on the left side of the row/column capsule, select "Drill Settings" from the drop\-down list, and you can manually configure the drill path for dimensions, enabling linkage between fields without [Configure Field Hierarchy](https://docs.byteplus.com/docs/DataWind/Configure_Field_Hierarchy) in the data.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36b1cf30f834467a9489c525bfa7c160~tplv-goo7wpa0wc-image.image" width="660px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4221a73458f94391aa5bd6fb81ff44b9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-列操作"></span>
## 3.5 Column operations

<span id="_3-5-1-调整列宽"></span>
### 3.5.1 Adjust column width

You can adjust the column width of the pivot table by dragging the dividing line between two columns with the mouse.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e80ee67b3963412186d9c0a3bf855ca4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-5-2-列排序"></span>
### 3.5.2 Column sorting

When you hover the mouse over the column name in the table header, the column sorting criteria and sorting button will be displayed. Click the button to sort the column contents, and click again to cancel the sorting. **Caution: If "Top N" is used in the analysis, sorting will be based on the selected Top N data entries.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c160a0d3d7140d89b11d9d69be8bf3e~tplv-goo7wpa0wc-image.image) </span>

At the same time, the fields in the pivot table totals also support sorting.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/325a1d6b6a2249d1969d5ddeba65d1ac~tplv-goo7wpa0wc-image.image) </span>
