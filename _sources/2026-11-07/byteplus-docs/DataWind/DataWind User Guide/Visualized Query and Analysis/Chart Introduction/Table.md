---
title: "Table"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Table"
---

A table is both a visual communication method and a means of organizing and managing data. It consists of one or more rows of cells and is used to display numbers and other items for quick reference and analysis. This article introduces the specific functions of tables in visual charts.

<span id="_1-概述"></span>
# Feature overview

Users can display detailed data by simply configuring dimensions and metrics. Additionally, tables support chart configuration, field configuration, column operations, and other features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f87781c6fb174015a254cd762c17fc80~tplv-goo7wpa0wc-image.image) </span>

<span id="a1b02c18"></span>
# Application scenarios

Typically used in scenarios where users focus on detailed data or need to display multiple directly related values.

For example: Within a specific time period, what products did regional managers sell, and what was the profit?

<span id="_2-快速入门"></span>
# Quick start


1. Set [Dimension Field Configuration](https://docs.byteplus.com/docs/DataWind/Dimension_Field_Configuration), [Metric Field Configuration](https://docs.byteplus.com/docs/DataWind/Metric_Field_Configuration), and [Overview of Field Configuration](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration). Select "Province" and "Transaction date" as dimensions, select 'order_count' and 'price' as metrics; filter the date as "the most recent day with available data".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5447a1bcb06f422b9c512f5e17ad9c11~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">p_date is the partition date field of the dataset. It is supported in extraction mode, but not available in direct connection mode.</div>


<div data-tips="true" data-tips-type="tip">p_date represents the date when data is synchronized to the product dataset (if the upstream data does not have date partitions), or the date when data is generated in the upstream data table (the original Hive table's date/p_date partition fields will both be renamed to p_date).</div>


<div data-tips="true" data-tips-type="tip">In visual queries, you can select and filter the date dimension according to analysis requirements. By default, the most recent day with data is selected.</div>



2. Select the chart panel \- table. Table is selected by default.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f49f232a10bf44df85b7f0c6d4f0a8f2~tplv-goo7wpa0wc-image.image) </span>


3. Modify the chart style in the chart configuration area as needed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c25c0a956467442badbf00d8bc5c685d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-配置规则"></span>
# Configuration rules

**Dimensions**: Supports zero or more dimensions.

**Metrics**: Supports zero or more metrics.

**Combination rules**: One or more dimensions with zero or more metrics; zero or more dimensions with one or more metrics.

**Example**: One dimension, three metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9167e137cece4187815f33030c6590e5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-图表配置"></span>
# Chart configuration

<span id="_3-2-1-基本格式"></span>
## Basic format

Supports serial numbers, automatic line wrapping, row and column transposition, metrics displayed before dimensions, and merging dimension cells, among other configurations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2814d1491c74305a308c12c2a041e9f~tplv-goo7wpa0wc-image.image) </span>


|Configuration |Example |
|---|---|
|Serial number |Add a serial number before each data entry to quickly locate a specific row when there are many data entries.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/182f7976d36142b5a892c1a0a93820fe~tplv-goo7wpa0wc-image.image) </span> |
|Automatic line wrapping |When the text exceeds the table width, it is truncated with an ellipsis by default. To display more or all of the text, extend the table width or enable automatic line wrapping.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bcbc9013ba3450a8906061a97bd5213~tplv-goo7wpa0wc-image.image) </span> |
|Transpose rows and columns |By default, data is displayed horizontally. After selecting "Transpose rows and columns", data is displayed vertically.<br><br><br>* Before transposing<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e93acb4c3c649ca8f4be0300adbbc45~tplv-goo7wpa0wc-image.image) </span><br><br><br>* After transposing<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/317c6fecae734c839cb8963ed496b321~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the number of data entries is within 100, row and column transposition can be performed. If there are more than 100 entries, the configuration is invalid.</div><br> |
|Metrics first |The table columns are displayed in the order: dimensions + metrics. After selecting "Metrics first", the table columns are displayed in the order: metrics + dimensions.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/218829ccf64149ee97cb1df5aecdbfab~tplv-goo7wpa0wc-image.image) </span> |
|Merge dimension column cells |Supports merging identical values in the same column.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/387ae06d140f4de5a2862678032ee409~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After enabling this feature, when the data volume is large, table rendering time will increase, affecting page performance.</div><br> |


<span id="876d291b"></span>
## Pager

When there are many data entries, you can configure a pager for the table. The pager supports a minimum of 10 items per page and a maximum of 100 items per page. After configuring the pager, in version V2.91.0 and above, the table supports displaying 1k, 2k, 5k, 10k, 20k, 30k, 40k, and 50k entries, or manually entering a positive integer (up to 50k) for the number of entries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2bdb5fcbd9c4faca302aa3c44cc5429~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">From version V2.44 onwards, after selecting the pagination control, the number of data entries and the current page range will be displayed.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/600a3b07a9414092be1b7704d2e65365~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="_3-2-3-文字对齐"></span>
## Text alignment

You can set the text alignment for dimensions and metrics separately. Currently, there are three alignment options: left, center, and right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6224da89b82349f29d9a9ab053e936d3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-4-表格样式"></span>
## Table style


* You can modify the table style and switch between minimalist and standard styles.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35faa0ee4b8e4647b5c9aad85fe4ff81~tplv-goo7wpa0wc-image.image) </span>


* The row headers can be shown or hidden.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb928ecfa4064a12b2803e36594c3650~tplv-goo7wpa0wc-image.image) </span>


* You can configure the colors of the table headers, cell text, and gridlines.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f0cb036298146829f751c5f863b27af~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-5-网格线"></span>
## Gridlines

You can adjust the color, line width, and line style for the table's outer border, horizontal gridlines, and vertical gridlines.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3305d665ae16494e9abfbbfb47050fd1~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-6-迷你图"></span>
## Sparkline

Starting from version V2.44, tables support inserting Sparklines. For details, see [Sparkline](https://docs.byteplus.com/docs/DataWind/Sparkline).

<span id="_3-2-7-特殊值"></span>
## Special values

You can customize the display of special values for dimensions or metrics, and set the style for special values to appear as blank, NULL, 0, or \-\-.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3fa792de9f64439a84527050c598b75~tplv-goo7wpa0wc-image.image) </span>

<span id="5b462348"></span>
## Custom fields

After enabling, this chart will enable the custom field feature in the dashboard.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0007875f36904a458206a6cdc4831201~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-8-显示模式"></span>
## Display mode

The display mode can be customized to adjust the table's appearance according to actual needs, including:


* Column width: Fit to content, fit to container, or custom.

* Row spacing/column spacing: Comfortable (default spacing, 8 pixels), efficient (narrower, 4 pixels), or custom.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b47b3b26ac8046f0a074fe37c6b39558~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-9-图内控件样式"></span>
## In\-chart control style

In\-chart controls include in\-chart filters, dynamic dimensions/metrics, and in\-chart parameters. After displaying them in the chart, you can adjust the layout of the title and filter content, as well as the typography settings. The following figure shows dynamic dimensions arranged vertically.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/666062bbdb6c4eef814c6ffa8df424fd~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-10-恢复默认设置"></span>
## Restore default settings

Click Restore Default Settings to revert all the above chart configurations to their default values.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/285172659a084f1baaf198562a082fa0~tplv-goo7wpa0wc-image.image) </span>

<span id="9bf375e2"></span>
# Field configuration

<span id="4b679f29"></span>
## Parse text

See [3.4 Parse text](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-4-%E8%A7%A3%E6%9E%90%E6%96%87%E6%9C%AC) for details.

<span id="aff9f5b5"></span>
## Conditional formatting

See [3.5 Set conditional formatting](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-5-%E8%AE%BE%E7%BD%AE%E6%9D%A1%E4%BB%B6%E6%A0%BC%E5%BC%8F) for details.

<span id="710bb4e9"></span>
## Edit visual style

See [3.6 Visual styles](https://docs.byteplus.com/docs/DataWind/Overview_of_Field_Configuration#_3-6-%E8%A7%86%E8%A7%89%E6%A0%B7%E5%BC%8F) for details.

<span id="_3-3-4-配置指标组"></span>
## Configure metric groups

The table supports configuring metric groups, allowing you to view metrics by category.


1. In the visualization query interface, click the metrics button to open a dropdown, then click "Configure Metric Groups".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/955e05f5be12408988df87edd58feea3~tplv-goo7wpa0wc-image.image) </span>


2. On the pop\-up page, click "Create Group", then name the group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd6f078d8fd7448fb3c4c6ef54400416~tplv-goo7wpa0wc-image.image) </span>


3. Then, drag the metrics you want to include in this group into the group using the mouse.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/682d6e4b8afb44618c15b1c29553161d~tplv-goo7wpa0wc-image.image) </span>


4. Click OK to save, and you can view these metrics by category


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1f1923aefe64074969763bf385582bd~tplv-goo7wpa0wc-image.image) </span>

<span id="77133b09"></span>
# Column operations

<span id="_3-4-1-调整列宽"></span>
## Adjust column width

Drag the divider between two columns in the table with the mouse to adjust the column width.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60c14cc395774ad98188334c39d224b4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-2-列排序"></span>
## Column sorting

When you hover the mouse over the column name in the table header, the column sorting button will appear. Click the button to sort the column contents; click again to cancel sorting.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36779cb07724474798a138ffcabb5f42~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If "Top N" is used in the analysis, sorting will be performed based on the selected Top N data entries.</div>


<span id="_3-4-3-冻结列"></span>
## Freeze columns

When there are many columns, you can fix the position of a column you want to focus on. When scrolling left or right to view other columns, the frozen column and the columns to its left will remain stationary. Click the dropdown list in the corresponding column header, select Freeze column, and click again to unfreeze the column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7762d6de01164f1f8543f1998aca4e36~tplv-goo7wpa0wc-image.image) </span>
