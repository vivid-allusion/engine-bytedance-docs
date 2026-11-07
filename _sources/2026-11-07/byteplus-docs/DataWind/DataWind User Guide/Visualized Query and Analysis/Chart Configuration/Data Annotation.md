---
title: "Data Annotation"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Annotation"
---

<span id="_1-概述"></span>
# 1. Overview

The visualization query module provides a data annotation feature, which supports annotating a specific data point or a specific time period on a chart.

**Applicable scenarios**: When a data anomaly occurs at a certain data point or during a certain time period for some reason, users can add a data annotation at the corresponding position to inform other users of the reason for the data anomaly. This reduces the need for oral or written explanations and improves readability and communication efficiency.

<span id="_2-快速入门"></span>
# 2. Quick start

(1) Select the required dimensions, metrics, filter conditions, and chart type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10a526daff3f445da58467c77779dea2~tplv-goo7wpa0wc-image.image) </span>

(2) Locate the data point or time period to be annotated and click the corresponding position on the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85c5d261952b4be08ebe884fa5ee6791~tplv-goo7wpa0wc-image.image) </span>

(3) Select data point annotation or time period annotation as needed, and enter the annotation content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345ae2b0887f4dc2b2c98324f4282902~tplv-goo7wpa0wc-image.image) </span>

(4) After entering the annotation content, click Confirm. The annotation card can be dragged to an appropriate position.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d241d9c601b43f88fdc817d3500746c~tplv-goo7wpa0wc-image.image) </span>

(5) By clicking the data point again, you can configure multiple data point annotations and time period annotations simultaneously.


* For data point annotations, click the icon above the data point to toggle display on or off.

* For time period annotations, click the time period text box at the top of the corresponding date dimension to toggle display on or off.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb9598c6b7e47af8e58b4b67317a678~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-功能介绍"></span>
# 3. Feature description

<span id="_3-1-支持的图表类型"></span>
## 3.1 Supported chart types

The current version supports the following chart types: stacked column chart, percentage column chart, grouped column chart, stacked bar chart, percentage bar chart, grouped bar chart, line chart, stacked area chart, percentage area chart, dual\-axis chart, bidirectional bar chart, combination chart, table view, scatter plot, change waterfall chart, and composition waterfall chart.

<span id="_3-2-数据标注的类型"></span>
## 3.2 Types of data annotation

 **(1) Data point annotation**


* You can annotate a specific data point. After setting the annotation, a thin gray line will connect the annotation card and the data point, making it easier to identify the corresponding data point.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d241d9c601b43f88fdc817d3500746c~tplv-goo7wpa0wc-image.image) </span>

 **(2) Time period annotation**


* Time period annotation can only be set when the first dimension is a date\-type field.

* Annotations can be added to a specific time period. After setting the annotation, a thin gray line perpendicular to the date axis will appear at the start date of the time period on the chart, and the annotation card will be connected to this gray line, making it easier to distinguish the corresponding time period.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb9598c6b7e47af8e58b4b67317a678~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-数据标注配置页面"></span>
## 3.3 Data annotation configuration page

 **(1) Font configuration**


* The font supports configuration of font type, font size, bold, italic, underline, and font color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33097ad7c4f146dcb88e4a3a53cc64d2~tplv-goo7wpa0wc-image.image) </span>

 **(2) Insert field**


* When initially configuring data annotations, the current chart's dimensions and metrics are automatically added. You can choose to delete them or click "Insert Field" to re\-add the current chart's dimensions and metrics.


 **(3) Preview**


* After clicking, you can preview the content and style of the data annotation as displayed on the chart.


 **(4) Other options**


* You can choose whether to expand the "Data Annotation" details panel by default. If you clear the checkbox, the configured data annotation will not be displayed directly on the chart.

* You can choose whether to display the "Annotation Content" by default. If you clear the checkbox, the configured data annotation will not display the annotation content (this option is only available for time period annotations).


<span id="_3-4-数据标注展示页面"></span>
## 3.4 Data annotation display page

 **(1) Data point annotation**


* In the data point annotation card, the left side displays the avatar of the user who set the data point annotation. When you hover over the avatar, the user's personal information will be shown.

* You can close the data annotation by clicking the icon in the upper right corner. Clicking the annotation icon on the data point again will reopen it.

* The lower right corner provides buttons for editing and deleting the data annotation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f45b5e46d9554587afea1870b3feb56f~tplv-goo7wpa0wc-image.image) </span>

 **(2) Time period annotation**


* The overall page functionality for time period annotations is the same as for data point annotations. The annotated time period is additionally displayed above the content.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84f849fa8d11425090ea1771bfae81dd~tplv-goo7wpa0wc-image.image) </span>
