---
title: "Top N"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Top_N"
---

<span id="_1-概述"></span>
# 1. Overview

The Top N component provided by DataWind supports quickly extracting the top or bottom entries of data values for each category.

When using incremental data retrieval in chart pivot tables, only Top N is supported.

**Example**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/387caf0fb62b4f7a9a0c913ebe7cffc9~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_2-快速入门"></span>
# 2. Quick start

**Step 1**: Select the calculation type. The default is "Top N result data"; here, select "Top N dimension items".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6e8b356804743eca177fe527abaf35f~tplv-goo7wpa0wc-image.image" width="735px" /></div>


**Step 2**: Select the dimension and sorting basis. Here, select "Customer Name" as the dimension and "Sum (Fixed Cost)" as the sorting basis.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2245973605946afa7bf597f7f99fc6a~tplv-goo7wpa0wc-image.image" width="735px" /></div>


**Step 3:**  Select the calculation method. The default is "Top"; here, select "Bottom".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ba0b741e39347ffad098dd479c17f61~tplv-goo7wpa0wc-image.image" width="735px" /></div>


**Step 4**: Select the calculation metric from the dropdown. The default is empty. Here, select "Sum (Profit)".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11c6f61058614579a9f4a344eae3c32e~tplv-goo7wpa0wc-image.image" width="735px" /></div>


**Step 5**: Configure the number for Top N. The default is "10". Set this to "2".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9dea9c5fabb4376bc4dc15011a5ab1b~tplv-goo7wpa0wc-image.image" width="735px" /></div>


**Step 6**: Click "Apply". This will retrieve the two entries with the lowest sum (fixed cost) under each customer name.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b0a43b6e7074e95833bad3ede3684c0~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-结果数据的前n条"></span>
## 3.1 Top N result data


* TOP N is the default calculation type.

* You can sort the result data based on any dimension or metric.

* After selecting this calculation type, options for sorting basis and TOP N quantity will appear.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88ca3084a3e4465593550830846d65e2~tplv-goo7wpa0wc-image.image" width="735px" /></div>



* Sorting basis: All fields of dimensions and metrics will be listed for selection. After selecting a dimension, you can choose ascending or descending order, or manual sorting; for metric fields, only ascending or descending order can be selected.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e45cd73e5b0441888c9f4cdd53b0a631~tplv-goo7wpa0wc-image.image) </span>


* TOP N quantity: You can select a specific number (entries) or a percentage (%).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b1ec5b472224514b253130ca7c2db76~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-前-n-条维度项"></span>
## 3.2 Top N dimension items


* **Usage restriction:**  At least one dimension must be configured to use this option.

* You can sort based on the number of result entries corresponding to any dimension item.

* After selecting this calculation type, options for selecting dimension, sorting basis, calculation method, and TOP N/Bottom N quantity will appear.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6368fe83a4e347718ffe5dc0a119955a~tplv-goo7wpa0wc-image.image" width="735px" /></div>



* Select dimension: All dimensions will be listed for selection.

* Sorting basis: The sorting basis will list the current dimension and all metrics. For example, if the dimensions are "Marital Status" and "Lead Source", and you select "Lead Source" as the dimension, the sorting basis will include "Lead Source" and all metrics.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd3815e832594aa799159ff75be9739f~tplv-goo7wpa0wc-image.image" width="735px" /></div>



* Calculation method: You can select either the top or bottom. After selecting the top, the next option will be TOP N; after selecting the bottom, the next option will be Bottom N.

* TOP N/Bottom N quantity: The display of TOP N/Bottom N changes according to the calculation method. You can select a specific quantity (number of items) or a percentage (%).

* For example, the following option refers to **the top two lead channels with the highest number of orders**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce5a21046b5544529257e99fe764e7f9~tplv-goo7wpa0wc-image.image" width="735px" /></div>


<span id="_3-3-每个维度下的前-n-条"></span>
## 3.3 Top N items under each dimension


* At least two dimensions must be configured to use this option.

* You can sort based on the number of results corresponding to any dimension item (the sorting criterion can be another dimension item).

* After selecting this calculation type, options for selecting dimension, sorting criterion, calculation method, and TOP N/Bottom N quantity will appear.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6648886619e4e04afb057753cf5898b~tplv-goo7wpa0wc-image.image" width="735px" /></div>



* Select dimension: All dimensions will be listed for selection.

* Sorting criterion: The sorting criterion will list the current dimension and all metrics. For example, if the dimensions are "marital status" and "lead channel", and you select "lead channel" as the dimension, the sorting criterion will list all dimensions and metrics, so you can select "marital status" as the sorting criterion.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1468819fe86439ab27dcd48a9c678d7~tplv-goo7wpa0wc-image.image" width="735px" /></div>



* Calculation method: You can select either the top or bottom. After selecting the top, the next option will be TOP N; after selecting the bottom, the next option will be Bottom N.

* TOP N/Bottom N quantity: The display of TOP N/Bottom N changes according to the calculation method. You can select a specific quantity (number of items) or a percentage (%).

* For example, the following option refers to viewing the first data result of the lead channel in each marital status category.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dab775205424446babe4421f0457ef5a~tplv-goo7wpa0wc-image.image" width="735px" /></div>
