---
title: "Sparkline"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Sparkline"
---

<span id="_1-概述"></span>
# 1. Overview

A sparkline is a small chart suitable for placement within a single cell of a table. Sparklines are highly compact and can be placed next to metrics to visually and concisely highlight the time trend of the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e22043ac3f254f60a44d61539cc0be89~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

Create a table and configure the dimensions and metrics to be viewed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b30660baf3240e382f8fe9048486dbf~tplv-goo7wpa0wc-image.image) </span>

Add a sparkline display to the metric. Click the arrow on the metric capsule and select Add sparkline.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/102d803ba61f4d0eb17306b0dc1edfb6~tplv-goo7wpa0wc-image.image) </span>

Select the date field. The sparkline will use the selected date field as the horizontal axis and the current metric as the vertical axis, displaying the metric trend as a line chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b02110e65cb4597b784352e095b5767~tplv-goo7wpa0wc-image.image) </span>

A sparkline field will be generated in the configuration bar, which can be dragged to adjust the field order. The sparkline field in the table will display the metric trend for each dimension.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/675da6011e534983aaafe5197e522343~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-调整字段顺序"></span>
## 3.1 Adjust field order

By dragging fields in the configuration bar, the field order can be quickly adjusted to optimize the display.

<span id="_3-2-样式设置"></span>
## 3.2 Style settings

In the chart style configuration area, you can set the sparkline color, marker points, line style, and whether to display tooltips information.

(1) Select the sparkline for which you want to configure the style

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f33b7a6a15cc416295fb805faf5401f3~tplv-goo7wpa0wc-image.image) </span>

(2) Set the style

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcd3b92d95f245c8bef8a50f846e42e3~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-修改迷你图"></span>
## 3.3 Edit sparkline

After a sparkline is created, it can be edited.

Click the arrow on the corresponding sparkline field capsule and select Edit sparkline.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f20a9b8e85a445688e9a6db691a6ea4e~tplv-goo7wpa0wc-image.image) </span>

Make modifications and adjustments in the pop\-up configuration box.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bbf4acb2a564ef6a8a758bfc44cd238~tplv-goo7wpa0wc-image.image) </span>

To delete a sparkline, click × next to the sparkline field to delete it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/019833c7a0b445ce8379f078c9df15d6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-依赖日期"></span>
## 3.4 Date dependency

In a sparkline, a date field needs to be set as the horizontal axis to view the trend over that date field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04232728975947ec8aa9b9216f13f448~tplv-goo7wpa0wc-image.image) </span>

If the selected field has already been filtered, that is, if a filter condition for the field exists in the filter bar, the date range for the sparkline can be selected as follows:

(1) According to the current table filter condition, the date range will be consistent with the current filter, displaying trend data for the current time period

(2) Use the X\-axis field in the table filter as the base and expand the date range backward by X time points. If the date range selected in the table is "2021\-12\-20–2021\-12\-31" and shifted backward by 1 day, then the date range for the sparkline will be "2021\-12\-19–2021\-12\-31".

> As shown in the figure below, the actual date range of the sparkline will also be displayed in the table header.


```Plain Text
     ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5db5e5cc99a64de3a0137f516975217d~tplv-goo7wpa0wc-image.image =2940x)
```


**You can specify the date granularity for the dependent date.**  When configuring a sparkline, after adding a date field, you can click the arrow on the date field and select "Date type" to choose the date granularity.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff4a63ec5a0f4133b87df83b0b54f068~tplv-goo7wpa0wc-image.image) </span>

The corresponding sparkline will display trends according to the specified date granularity.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ea5cd2358c44b289753f248dec17b41~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Starting from V2.56.1, up to 6 sparkline columns can be added. If there are already 6 sparkline columns, a prompt will appear when you try to add more: A maximum of 6 sparkline columns can be added.</div>
