---
title: "Drill Up and Drill Down"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Drill_Up_and_Drill_Down"
---

Drill up and drill down refers to creating a hierarchical structure based on fields (for example: province \-\> city \-\> channel), allowing users to quickly move up or down between levels during visual analysis by clicking. This article introduces two methods for implementing drill up and drill down: by creating a hierarchy and by configuring drill settings.

<span id="e568d7ae"></span>
# Prerequisites


* To implement drill up and drill down by **creating a hierarchy**, dataset edit permission is required.

* To implement drill up and drill down by **drill settings**, only dataset view permission is required.


<span id="_1-概述"></span>
# Overview

<span id="c9d729f3"></span>
## Supported chart types


* Table, pivot table

* Clustered column chart, stacked column chart, 100% stacked column chart

* Clustered bar chart, stacked bar chart, 100% stacked bar chart

* Line chart

* Area chart, 100% stacked area chart

* Dual\-axis chart

* Pie chart, donut chart, Nightingale rose chart

* Filled map, symbol map

* Bidirectional bar chart

* Combo chart

* Scatter plot, bubble chart

* Word cloud

* Radar chart

* Waterfall chart


<span id="_2-1-通过创建层级实现上钻下钻"></span>
# Implementing drill up and drill down by creating a hierarchy


1. Create a hierarchical structure, for example, a geographic hierarchy: region \-\> province \-\> city. For more details, see [Configure Field Hierarchy](https://docs.byteplus.com/docs/DataWind/Configure_Field_Hierarchy).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e912d07c5f664e968e33ce6e50bbc775~tplv-goo7wpa0wc-image.image) </span>

2. Add province and city to the hierarchy.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dd36c1e08c44c1ebd39d5c730e9aca7~tplv-goo7wpa0wc-image.image) </span>


3. Add the region field to the dimensions. A "+" sign appears before the hierarchy that supports drilling down. Then, specify the metrics and chart type for visual analysis to start interactive drill up and drill down analysis.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3737743b1da8472dbcbe75108a1462ae~tplv-goo7wpa0wc-image.image) </span>


4. Click a data item in the chart and select "Drill down" to perform a drill down operation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76c0b9fa3e6a4933bf12f7e5dcf05c27~tplv-goo7wpa0wc-image.image) </span>


5. Click Northeast, then click Heilongjiang. The data for all cities in Heilongjiang Province, Northeast region, will be displayed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54616034919f46ea8c4e465d7cb3a563~tplv-goo7wpa0wc-image.image) </span>


6. In the drill\-down hierarchy breadcrumb, click the corresponding field name to perform a drill up operation and return to the previous level.

7. Save the chart to the dashboard to perform drill up and drill down in the dashboard.


<span id="_2-2-通过钻取设置快速实现上钻下钻"></span>
# Implementing drill up and drill down by configuring drill settings


1. Select the required metrics and the dimensions to drill down.

2. Click the downward triangle icon in front of the dimension capsule to expand the field configuration page for the dimension, and select "Drill\-down settings".

3. On the drill\-down settings page, select Add dimension, then check the dimensions to drill down to, and click OK.

4. Next, specify the metrics and chart type you want to visualize to start drill\-up and drill\-down interactive analysis. For detailed steps, see steps 4–7 of **Implement drill\-up and drill\-down by creating hierarchies**.
