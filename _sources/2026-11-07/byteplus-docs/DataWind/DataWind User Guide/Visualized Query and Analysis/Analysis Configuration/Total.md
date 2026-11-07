---
title: "Total"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Total"
---

<span id="_1-概述"></span>
# 1. Overview

Total refers to the sum or aggregate, which is the total of a set of values. The product provides a total analysis component that supports summing the values of specified areas in a chart.

**Example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d1b8c1fa9440a683a289d9e0cdd6d5~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-表格合计"></span>
## 2.1 Table total

**Step 1**: At the top, select "In\-chart total item" and modify the display name (the default is Total); for display position, select one (the default is Top); for calculation basis, select one (the default is All data).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d733fa93e83456b91c8d0caac79189b~tplv-goo7wpa0wc-image.image" width="735px" /></div>


**Step 2**: In the table, you can set different calculation methods for different columns; set Calculation Card 1, select Sum as the calculation method, and select Revenue as the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74d8603a0dc5401f83e0de69e37efcf7~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Add a calculation card, select Average as the calculation method for Calculation Card 2, and select Expenditure as the metric.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aebfec123bb24a06b890721907e9f63f~tplv-goo7wpa0wc-image.image" width="735px" /></div>


**Step 4**: Click Apply.

<span id="_2-2-透视表合计"></span>
## 2.2 Pivot table total

**Step 1**: Pivot table total supports grand totals and subtotals for rows and columns. At the top, select "In\-chart total item".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ca6b0529a6343a193a7ccc99c8f83ed~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Check Column Total, Column Subtotal, Row Total, and Row Subtotal. Select Sum as the calculation method.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1be9ff627bbe4202a7013d11e2e3d5e9~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Click Apply.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f99025764a2e4f68ac2c5e949067480e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-图表合计"></span>
## 2.3 Chart total

<span id="f17c2f46"></span>
### 2.3.1 Total by legend


* **Step 1**: At the top, select "In\-chart total item". The calculation basis can be set to All data or Current displayed data; the calculation method is set to Sum, and all metrics must use the same calculation method.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd5960e73fdf497aa42d16771e973582~tplv-goo7wpa0wc-image.image) </span>


* **Step 2**: Click "Apply".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed7bf14cf3ac42d5aa5a3b2e7347599c~tplv-goo7wpa0wc-image.image) </span>

<span id="c4257f3f"></span>
### 2.3.2 Total by axis


* **Step 1**: In "Chart", select Line Chart.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37449810c94a4ca3abe316b4d6a4d7ee~tplv-goo7wpa0wc-image.image" width="749px" /></div>



* **Step 2**: At the top of the chart, select "In\-chart total item". For total type, select "By axis". The calculation basis can be set to All data or Current displayed data. The calculation method is set to Sum, and all metrics must use the same calculation method.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6698c2d3b12549249f2756e049d3713b~tplv-goo7wpa0wc-image.image) </span>


* **Step 3**: Click "Apply".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/913d2598e0d74b39b313c0a616325175~tplv-goo7wpa0wc-image.image" width="2938px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-图外汇总指标"></span>
## 3.1 Out\-of\-chart summary metrics

To allow users to quickly understand an overview of current summary data, the product supports quick presentation of data summary results in addition to detailed data analysis, for example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0136ef2d4f1946aaa071f6be124a094a~tplv-goo7wpa0wc-image.image) </span>


* **Implementation process:**  Select "Total", then select "external summary indicator". Next, configure the total display mode, calculation basis, calculation settings, and other relevant information. After selecting Apply, the corresponding summary results will be displayed on the chart.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d350e8e2dddf4f9d831b3e39d153632e~tplv-goo7wpa0wc-image.image) </span>


* **Function description:** 

   * Supported chart types: Most charts, including trend charts, bar charts, and tables, are supported.

   * Total display: You can configure the combined display of text and values. After clicking, you can select as prompted.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a63d44ab40b94991bffcc5ce0ecf961b~tplv-goo7wpa0wc-image.image" width="497px" /></div>



* **Calculation basis:** 

   * All data: The calculation result includes all data and is not affected by TOP N or the number of rows displayed in the chart.

   * Currently displayed data: The total is calculated only for the data within the visible range of the chart.

* **Calculation settings:** 

   * Calculation method: You can choose the default calculation method for the indicator or adjust it as needed. Currently, sum, average, maximum, and minimum are supported.

   * Calculation indicator: You can choose to apply to all indicators or to specific indicators.


<span id="_3-2-表格合计"></span>
## 3.2 Table total

<span id="_3-2-1-显示名称设置"></span>
### 3.2.1 Display name settings

Modify the display name. This applies to the name of the newly added total row.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57eeb3ec992e4969a50f3660c45eb961~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_3-2-2-显示位置设置"></span>
### 3.2.2 Display position settings

Modify the display position. You can set the total result to be displayed at the top or bottom.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28ec8c165b70490ba9d83046ed69647a~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_3-2-3-计算依据"></span>
### 3.2.3 Calculation basis

You can set the calculation basis to all data or currently displayed data.


* All data: The total is calculated based on all data and is not limited by top N or N (if the table data exceeds 1,000 rows, only 1,000 rows are displayed by default).

* Currently displayed data: In tables, this refers to calculating based on the data range visible to the user. The calculation is affected by the maximum number of displayed rows. If the user selects to display 1k/50k rows in the pager, the total for currently displayed data is calculated based on these 1k/50k rows. The calculation range is also affected by TOP N. For example, if TOP 5 is selected based on revenue, the calculation is performed on the 5 rows after applying TOP N.


<span id="_3-2-4-计算卡片"></span>
### 3.2.4 Calculation card

**Calculation method:**  Six calculation methods are supported, with sum as the default.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b120a4fe55dc4a478e865a4d629d9156~tplv-goo7wpa0wc-image.image" width="243px" /></div>


**Calculation metrics:**  You can select all calculation metrics or a specific calculation metric. If you select all calculation metrics, you cannot select any individual calculation metric, and the calculation method applies to all calculation metrics. When selecting specific calculation metrics, multiple selections are supported.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48ac92b258c342b484b4b42467eed347~tplv-goo7wpa0wc-image.image" width="735px" /></div>


If you select specific calculation metrics, you can continue to add calculation cards.

You can set different calculation methods for different calculation metrics, and each calculation metric can only correspond to one calculation method.

<span id="_3-3-透视表合计"></span>
## 3.3 Pivot table totals

<span id="_3-3-1-显示名称设置"></span>
### 3.3.1 Display name settings

Modify the display name, which applies to the names of newly added total items.

<span id="_3-3-2-列总计、行总计"></span>
### 3.3.2 Column totals and row totals

You can set the total for an entire column or row.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/476b87cf0c63480988b371fb376632b3~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_3-3-3-列小计、行小计"></span>
### 3.3.3 Column subtotals and row subtotals

Set the subtotal for a column or row, and you can specify the dimension on which the subtotal calculation is based.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/320b9ccc986c4f9db6142a87a16517e7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-4-位置设置"></span>
### 3.3.4 Position settings

You can set the position of newly added total items.

<span id="_3-4-图表合计"></span>
## 3.4 Chart totals

<span id="_3-4-1-显示名称设置"></span>
### 3.4.1 Display name settings

Modify the display name, which applies to the names of newly added total items.

<span id="_3-4-2-显示位置设置"></span>
### 3.4.2 Display position settings

Modify the display position; you can set the total result to be displayed at the top or bottom.

<span id="_3-4-3-计算依据"></span>
### 3.4.3 Calculation basis

You can set the calculation basis to be either all data or the currently displayed data.


* **All data:**  Calculate the total based on all data, not limited by top N and N (if the chart data exceeds 10,000 rows, only the first 10,000 rows are displayed by default);

* **Currently displayed data:**  Calculation is based on the corresponding data used for online plotting and is affected by top N and N.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b287d9242f0448f976f48a1eebc8525~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_3-4-4-计算方式"></span>
### 3.4.4 Calculation method

You can choose from multiple calculation methods; the default is sum.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bfc7e3904b64ac9a773a2a23578b108~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_3-5-自动与求和"></span>
## 3.5 Auto and sum

Calculation is based on the underlying unaggregated data, rather than aggregated data. As shown in the figure below, the expression for the average product price is sum([价格])/count([产品id]), which calculates "the sum of product prices across all provinces divided by the total number of product IDs (that is, the number of products)", meaning the table data details are calculated according to the field expression to obtain the national average product price.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b86ad96d67ce4292a32a49b46c28ee32~tplv-goo7wpa0wc-image.image) </span>

In this case, it is distinguished from "average value". The calculation logic for "Auto" is total price divided by total number of products, while "Average" refers to the average of (total price divided by number of products) for each province. You can select different calculation methods based on actual calculation requirements.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00e4c3fd3118423aacae9081ed8ca9a8~tplv-goo7wpa0wc-image.image" width="735px" /></div>


There is a fundamental difference between "Auto" and "Sum". "Auto" is calculated based on the metric's field expression, whereas "Sum" calculates the total sum of the corresponding metric. As shown in the figure below, summing the metric "Average Price" yields the sum of the average prices for each province, rather than the "total price divided by total number of products" as calculated by "Auto".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18cd506ea21149d1b11338b70b68cee9~tplv-goo7wpa0wc-image.image" width="735px" /></div>
