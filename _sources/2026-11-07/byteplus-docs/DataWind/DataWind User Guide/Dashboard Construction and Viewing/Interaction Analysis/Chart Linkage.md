---
title: "Chart Linkage"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Chart_Linkage"
---

Chart linkage allows you to use a chart as a filter. By clicking a data item in the chart, the associated charts will filter and display the data corresponding to the selected item. This article introduces how to use the chart linkage feature.

<span id="_1-概述"></span>
# Feature overview

The chart linkage feature enables users to quickly locate data in other charts that correspond to a specific factor.

Example usage scenarios:


* Real\-time linkage between summary and detail tables: In the regional sales summary table, you can view the overall sales situation for each region, and link to the detail table to view the sales performance of each sales representative within the region.


<span id="_2-快速入门"></span>
# Quick start


1. Go to the dashboard editing page, click the options in the upper right corner of the chart you want to configure for linkage, and select "Linkage settings".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1a8b9f894eb48719b8c4632482782da~tplv-goo7wpa0wc-image.image) </span>


2. Select the charts to link with the current chart, click "OK" to enable chart linkage.

* If the chart to be linked uses the same dataset as the current chart, simply select the chart name. In the example below, select "Chart linkage detail table".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52f6c6b7d09d457685d4b41766967207~tplv-goo7wpa0wc-image.image) </span>


* If the chart to be linked uses a different dataset from the current chart, you need to associate the fields.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbf2a945b69b4673b50f1c35e953a54f~tplv-goo7wpa0wc-image.image) </span>


3. Click any data item to view the chart linkage effect.


<span id="_3-2-设置联动"></span>
# Configure linkage


* If the chart to be linked uses the same dataset as the current chart, simply click "OK".

* If the chart to be linked uses a different dataset from the current chart, you need to configure the mapping between fields.

   * At least one field must be associated. Once this condition is met, the field configuration box will turn from red to green.

   * Caution: When the field value is null (empty), linkage will not take effect.

   * If there are drill\-down fields under the current primary field (see [Drill Up and Drill Down](https://docs.byteplus.com/docs/DataWind/Drill_Up_and_Drill_Down)), drill\-down fields also support linkage configuration.


<span id="_3-3-图表联动"></span>
# View linkage

<span id="890a61ce"></span>
## Single data point linkage


* Click the dimension field "Jilin" in the source chart, and the linked chart will display the data corresponding to "Jilin".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9048dd09b09f41deb5fe8184274d7cdf~tplv-goo7wpa0wc-image.image) </span>

* Click the value "197,203" in the "Revenue" metric field of the source chart. All dimension field values in that row will be passed to the linked chart, which will then display the corresponding data for "Henan\-Nanyang".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/958bf883adba4fe7a847400b4c7e46df~tplv-goo7wpa0wc-image.image) </span>


<span id="5d9e521d"></span>
## Multiple data point linking

Selecting multiple data points in the linked chart allows you to link multiple data points.

<span id="74b6f0e9"></span>
# Cancel linking

Click the previously linked single field or multiple data points again, or click a blank area of the chart, to cancel the linking state.

<span id="_3-4-删除联动"></span>
# Remove linking

In dashboard edit mode, clicking "Cancel linking" on the chart will clear the linking configuration for that chart.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b709f50e5404cb0a082d54fde74f270~tplv-goo7wpa0wc-image.image) </span>
