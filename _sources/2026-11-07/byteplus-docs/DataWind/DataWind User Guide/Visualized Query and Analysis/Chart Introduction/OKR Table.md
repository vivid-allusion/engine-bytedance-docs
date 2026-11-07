---
title: "OKR Table"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/OKR_Table"
---

The OKR table supports configuring targets for metrics, viewing the monthly, quarterly, and annual target completion rates of business metrics in the chart, the time progress within the current cycle, as well as the year\-on\-year and period\-on\-period comparisons for each metric, enabling users to track the completion status of business objectives in real time. This article introduces how to use the OKR table.

<span id="_1-概述"></span>
# Feature overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1e14c81536245c89f433b156b252e5b~tplv-goo7wpa0wc-image.image) </span>


* Field configuration area: Includes settings for date, dimension, and metric fields to meet various data presentation needs

* Filter configuration area: Includes filter settings to help users quickly locate key data

* Chart preview area: Visually presents data visualization effects, allowing users to view chart content in real time

* Chart configuration area: Allows users to customize various chart details

   
   |Chart configuration |Feature introduction |
   |---|---|
   |Basic format |Set the dimension display mode and default expansion level |
   |Deadline |Determine the data calculation deadline and configure the date filter box |
   |Table columns |Select preset or custom columns, edit column content and display mode. |
   |Calculation method |Configure indicator calculation rules |
   |Year\-on\-year and period\-on\-period comparison |Adjust the calculation type for year\-on\-year and period\-on\-period comparison columns |
   |Conditional formatting |Configure conditional formatting for year\-on\-year and period\-on\-period comparison columns |
   |Data format |Configure data format for year\-on\-year and period\-on\-period comparison columns |
   |Time progress |Display data progress for different periods |
   |Sparkline |Add and customize indicator trend Sparklines |
   |Dimension sorting |Adjust the display order of dimension fields |
   |Text alignment |Set the arrangement of table text |
   |Table style |Customize the appearance of the table and table header |
   |Special values |Set the display format for special data |
   |Display mode |Adjust chart column width and spacing |
   


<span id="_2-快速入门"></span>
# Quick start


1. Go to the visualization query page and select OKR table in the chart options.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42f06b9c61224db281170cd30a8de283~tplv-goo7wpa0wc-image.image) </span>

2. Select the target configuration option in the chart configuration area below the OKR table to configure targets for metrics. For detailed steps, refer to the documentation: [Measure Targets](https://docs.byteplus.com/docs/DataWind/109951).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The user's operation account must have dataset editing permissions to <strong>configure metric targets</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To query a metric that already has a target configured, this step can be skipped.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d41c6b89f714b79bc34c5564c32115a~tplv-goo7wpa0wc-image.image) </span>

3. Add date, dimension, and metric fields as required by the chart.

   * One date field with daily granularity, zero to five dimensions, and one or more metrics

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e6c1dca01694ac28a9c5faaa85311e5~tplv-goo7wpa0wc-image.image) </span>

4. Adjust the data and cutoff date to be displayed in the chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97c43f52509748ed97ffb48d62d2efda~tplv-goo7wpa0wc-image.image) </span>

5. After creating the chart, you can further adjust the calculation method for year\-on\-year and period\-on\-period comparisons, modify the granularity of time progress, and add sparklines in the chart configuration area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e152c24f02404812975b742b649fb4cf~tplv-goo7wpa0wc-image.image) </span>


<span id="f8b19e07"></span>
# Configure fields

<span id="5e2c3e62"></span>
## Set field information

The date, dimension, and metric fields in the field configuration area all support setting field information.


1. Select a field and click "Set field information."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07c185942f7e4e4696ad7234bfccebf5~tplv-goo7wpa0wc-image.image) </span>

2. You can set the chart display name and the content and style of the field description. After configuration, click "OK" to confirm.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a9c375a4a694921a75de9bd6e472f31~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration instructions |
   |---|---|
   |Chart display name |You can set the display name of the field in the chart. |
   |Display field description |You can choose whether to display the description of the field. After selecting this option, you can add a description for the field.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Field descriptions can be displayed for date and metric fields, but not for dimension fields.</div><br> |
   |Display style |The display style of the field description content. You can choose underline or icon.<br><br><br>* Underline<br><br>* Icon |
   


<span id="1473ef62"></span>
# Configure chart

<span id="5ac5ad46"></span>
## Basic format

Supports setting the dimension expansion style and expansion level for the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9df2b3c475f443ea8e97dac3a7425000~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Configuration instructions |
|---|---|
|Basic format |You can choose "flat display" or "tree display".<br><br><br>* Flat display<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93eba611dd6d4949991d946eac2c9f93~tplv-goo7wpa0wc-image.image) </span><br><br>* Tree display<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abc759b42fc545cbb5d3ff9ad5196568~tplv-goo7wpa0wc-image.image) </span> |
|Default expand level |You can set the default expand level of the OKR table according to the number of dimensions. |


<span id="_3-1-截止日期"></span>
## Cutoff date

Support configuring a data cutoff date for charts. After setting the cutoff date, the data in the OKR table will use the selected cutoff date to calculate time progress and target completion progress.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/272679b558864da09c50629e5ef19b8e~tplv-goo7wpa0wc-image.image) </span>


* Support selecting whether to display the date filter box in the chart.

* Support configuring the most recent day with data, T\-1, or custom (fixed date).

* Support selecting the display position as either the far right or the far left.


<span id="_3-2-表格列"></span>
## Table columns

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/843117719d90402bb22caf8954f18ada~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-1-选择列"></span>
### Select columns

Support selecting which columns' data to display in the OKR table. Users can choose from system\-provided column options or customize columns.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d0222f683f44fa89f0f2ddb981d85a8~tplv-goo7wpa0wc-image.image) </span>


* The columns currently supported by the OKR table include:

   
   |**Date granularity** |**Column type** |
   |---|---|
   |Last 1 day |Metric value, month\-on\-month, week\-on\-week, year\-on\-year |
   |Last 7 days |Metric value, month\-on\-month, week\-on\-week, year\-on\-year |
   |Last 1 month |Metric value, month\-on\-month, week\-on\-week, year\-on\-year, target value, target completion rate |
   |Last 1 quarter |Metric value, month\-on\-month, week\-on\-week, year\-onear, target value, target completion rate |
   |Last 1 year |Metric value, month\-on\-month, week\-on\-week, year\-on\-year, target value, target completion rate |
   

* If the currently supported columns do not meet visualization requirements, users can customize columns as follows:

   1. Click "Customize", then click "Add custom period\-on\-period comparison".

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d05ee3e7c50148fd85864c88fc7c5524~tplv-goo7wpa0wc-image.image) </span>

   2. Set the calculation method. Both dynamic time and fixed time are supported.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05c4ac24a36449c0b0532592b27f9ae3~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-2-2-目标配置"></span>
### Target configuration

Indicators in the OKR table must have targets configured before they can be used. Otherwise, target completion cannot be viewed. For details, see [Measure Targets](https://docs.byteplus.com/docs/DataWind/109951).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0984c0a112974ca7b42fdb73dbfd1a57~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-3-编辑列"></span>
### Edit columns

Use the edit columns feature to adjust the order of indicators, modify column names or add column descriptions, and set the date display position. Users can flexibly configure three display options: "Show in table header", "Show in tooltip", or "Do not show".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60f6618f3d6e4dd5b8113c1c0c3aa441~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-计算方式"></span>
## Calculation method

Support adjusting the calculation method for indicators in the OKR table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e010e6bcb1145e2b0733f85ffa706c3~tplv-goo7wpa0wc-image.image) </span>


|Calculation method |Introduction |
|---|---|
|Daily average |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/589125a4a2cf4c6ab7e2346bbeae38ea~tplv-goo7wpa0wc-image.image) </span> |
|Cumulative |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fee92b1c6afe433b8b368672d6109022~tplv-goo7wpa0wc-image.image) </span> |
|Automatic |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9afe0c020df247b58ee9bbdffc9705ee~tplv-goo7wpa0wc-image.image) </span> |



* The default calculation method is cumulative.

* Support selecting indicators first and then columns to configure the calculation method for each cell.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76fc3977229c486ab99ab038f25651f6~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-4-同环比"></span>
## Period\-on\-period comparison

Support adjusting the calculation type for period\-on\-period comparison columns.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/711730ca8b6f4deba3ad3329cea9b99c~tplv-goo7wpa0wc-image.image) </span>


* Calculation types include difference percentage, difference value, or original value.

   
   |Calculation type |Example |
   |---|---|
   |Difference percentage |(Today \- Yesterday) / Yesterday \* 100% |
   |Difference value |Today \- Yesterday |
   |Original value |Yesterday |
   


<span id="_3-5-时间进展"></span>
## Conditional formatting

Support configuring conditional formatting for period\-on\-period comparison columns.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d98eb0a86b5b4d559f8383ca410fa7e9~tplv-goo7wpa0wc-image.image) </span>


* Select the required conditional formatting and the applicable indicators for it to take effect.


<span id="1cfbc9c0"></span>
## Data format

Support configuring the data format for period\-on\-period comparison columns, including auto, number, percentage, per mille, original value, pp, and custom features. For details, see [2.2 Set data format](https://docs.byteplus.com/docs/DataWind/Metric_Field_Configuration#_2-2-%E8%AE%BE%E7%BD%AE%E6%95%B0%E6%8D%AE%E6%A0%BC%E5%BC%8F).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84396129042a45afb06e36f5f4f64fcd~tplv-goo7wpa0wc-image.image) </span>

<span id="99747cab"></span>
## Time progress

You can select whether to display time progress and which granularity to show. Currently, monthly, quarterly, and annual time progress are supported.


* The calculation method for time progress is: **number of days elapsed in the current period as of the deadline / total number of days in the current period**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e38b75440fba4b8887c3b1f710183123~tplv-goo7wpa0wc-image.image) </span>


<span id="616ef4ec"></span>
## Sparkline

The OKR table allows you to add Sparklines, which display the trend of indicator changes in the last N days before the deadline within the table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/927a396b5cbc4ecd884b400b0c868e3c~tplv-goo7wpa0wc-image.image) </span>

The parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|Field name |Custom Sparkline field names are supported. |
|Y\-axis |No configuration required; defaults to the current metric. |
|X\-axis |This is a date field. You can set the date type and date completion.<br><br><br>* Date types: year, year\-quarter, year\-bimonth, year\-month, year\-biweek, year\-week, year\-month\-day. Among these, year, year\-biweek, and year\-week support custom intervals.<br><br>* Date completion: display or not display.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For the Year\-Biweek date type, the week calculation logic in the filter will take precedence over the currently configured week calculation logic.</div><br> |
|Date range |You can set the Sparkline date range, for example, by going back 7 days from the "end date". |
|Data color |You can define the Sparkline line color. |
|Line style |You can choose whether to have marker points, and whether the line is straight or smooth. |
|Display tooltip |You can choose whether to display the tooltip. Display is enabled by default.<br><br><br>* If the option to display the tooltip is selected, when the user moves the mouse over a Sparkline marker, the corresponding date and value for the marker will be displayed.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1a9a9def9bd4143827193b8ffb48a9d~tplv-goo7wpa0wc-image.image) </span> |


<span id="a14363c5"></span>
## Dimension sorting

You can sort dimension fields, including ascending, descending, and manual sorting.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d1ca22efd534dd78129fe6904bc7dc3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-文字对齐"></span>
## Text alignment

You can adjust the text alignment in the table, including automatic, left, center, and right alignment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06fbe4262ec74878a8cad041d89ae067~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-表格样式"></span>
## Table style

You can adjust the overall table style, as well as the text, fill color, and fill display mode of the table header.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/699645cba9184a50935552aef7a64e2a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-9-特殊值"></span>
## Special values

When there are special values in the table, such as empty values, you can adjust the display mode for these values. The default for dimensions is NULL; the default for indicators is blank.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b38de53c77654daa9b681bb7f52b9fbf~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-10-显示模式"></span>
## Display mode

You can adjust the column width, column spacing, and row spacing of the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9754580252674552b3d3867cd8443097~tplv-goo7wpa0wc-image.image) </span>
