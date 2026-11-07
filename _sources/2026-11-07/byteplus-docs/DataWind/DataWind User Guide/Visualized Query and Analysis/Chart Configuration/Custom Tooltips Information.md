---
title: "Custom Tooltips Information"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Custom_Tooltips_Information"
---

<span id="_1-概述"></span>
# 1. Overview

When displaying a chart, moving the mouse over the value area, such as over a specific bar in a column chart, will display a tooltip.

By default, dimension and metric information is displayed automatically. Users can also customize the settings to display more information, or even enable interactivity by inserting other related charts into the tooltip.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cba1efa6df604471b16443a293521d7c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

After creating a chart, click "tooltips" in the chart editing area to disable or enable the tooltips, edit the trigger mode, and configure the display content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18334d27c97f42ab98b5f2348812cfb1~tplv-goo7wpa0wc-image.image) </span>

Select the trigger mode: by default, both dimension and item are enabled. For example, in a column chart, if the dimension trigger is selected, the tooltips will appear only when the mouse is moved to the blank area above a bar (selecting the entire dimension). If the item trigger is selected, the tooltips will appear only when the mouse is moved to a specific bar (selecting a single item).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aee170f106b6430e9d5e502ac92c0490~tplv-goo7wpa0wc-image.image) </span>

Edit display content: By default, the current dimension and metric values are displayed. You can drag other metrics into the display content box and edit them for custom configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffaa52f26b5d4ca58d0c21191921967b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f291eb460c3c49f5b75d313d26720c47~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-支持的图表类型"></span>
## 3.1 Supported chart types

Column chart, bar chart, line chart, area chart, dual\-axis chart, pie chart, map, bidirectional bar chart, combination chart, scatter plot

<span id="_3-2-默认提示信息"></span>
## 3.2 Default tooltips information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7ba98625ad44130b45d2df275826c5b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-插入和编辑文字与字段"></span>
## 3.3 Insert and edit text and fields

You can add other metrics from the dataset to supplement the tooltips information.

(1) Drag metrics into "tooltips" – "Display content". Click the arrow on the field to edit the displayed field name, format, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49aee769273149ab9ab797b0470d3a36~tplv-goo7wpa0wc-image.image) </span>

(2) Click the edit button to further configure custom tooltips information in the pop\-up edit box. Supports **entering text, inserting fields, and inserting charts**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ff8f57634634acdbd20838dd40ad2cd~tplv-goo7wpa0wc-image.image) </span>

Derived metrics can also be used for tooltips annotations. For example, if a derived field for year\-on\-year or period\-on\-period comparison is added, this field can be applied in the tooltips.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/630d7cdaa0a34274a5ddc8f0e59e1956~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d50ee83f69447f0bbfa9848221012a3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b09d8e4bb53455f8348aa6d3abf732c~tplv-goo7wpa0wc-image.image) </span>

After editing text and fields and adjusting the layout, you can achieve a customized effect. Click Preview to preview the effect.

> As shown in the figure, in the editing box:

> Text content with a gray background enclosed by <\> symbols represents inserted fields, such as <订单状态\> <订单状态\>. After saving, the dimension item name or metric value will be displayed.

> Text content with a gray background enclosed by [] symbols represents field names, such as [付款金额] [订单数]. After saving, the field names will be displayed.

> Text without a background is manually entered information and will not change based on actual field information or selected data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34be2ea1b6cb4680aadf351f31502759~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-插入图表"></span>
## 3.4 Insert charts

You can insert saved charts from the currently used dataset.

> Only charts from the currently used dataset can be inserted. After insertion, the prompt message will indicate that the chart will synchronize the current chart's filters. In other words, this method enables quick linkage effects.

> Only charts can be inserted; tables cannot be inserted.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/530c62ed33dc4664a565cf7367fefb09~tplv-goo7wpa0wc-image.image) </span>

Click "OK" to apply to the chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e007165f269b41c38017484434e88a39~tplv-goo7wpa0wc-image.image) </span>
