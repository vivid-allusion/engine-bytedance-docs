---
title: "Dynamic Dimensions and Dynamic Metrics"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dynamic_Dimensions_and_Dynamic_Metrics"
---

<span id="_1-概述"></span>
# 1. Overview

The dynamic dimensions/dynamic metrics feature has been added, making it simpler and faster to switch between multiple dimensions or metrics to meet the needs of different users for different dimensions or metrics.

<span id="_2-快速入门"></span>
# 2. Quick start

**Step 1**: Drag a dynamic dimension into the dimensions section of the data panel

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15cf5e64fd334961b2ae37a2af87e024~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Drag the date field into the dynamic dimension configuration popup. You can drag two identical date fields and set different date granularities for each

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1fddedf69bc4d95a76917270d6bae7c~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Click Confirm to generate a dynamic dimension. By default, the first dimension in the dynamic dimension is displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24a18d635b104506a762214dd9d74580~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Drag the dynamic dimension field into the data panel again to generate a new dynamic dimension: sale_province/sale_city, and select the option to allow the dimension to be empty; similarly, add a dynamic metric, and check the dimension option to leave it blank; Similarly, add another dynamic indicator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4983835ee717407a95e7e8e70e2f2afb~tplv-goo7wpa0wc-image.image) </span>

**Step 5**: Once added, you can change the selection in the dimension/metric selector to switch between multiple dimensions or metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb8b26a565394b63a8eafc0c1e901a24~tplv-goo7wpa0wc-image.image) </span>

**Step 6**: Save the chart to the dashboard to dynamically switch dimensions or metrics in the dashboard

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf9121d9692d4206901f7096c4c7e2f4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-配置动态维度-指标"></span>
## 3.1 Configure dynamic dimensions/metrics


* You can add multiple dynamic dimensions/dynamic metrics to the data panel. Multiple dimensions or metrics can be added to a single dynamic field

* Dynamic dimensions add an option: the dimension option can be empty; the dynamic metric option cannot be empty

* Interaction: Dropdowns and dragging fields are supported to adjust the order


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9054a51725e848ca81a2ce4e66b43d9d~tplv-goo7wpa0wc-image.image) </span>

Editing dynamic dimensions/metrics:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/383b17346a764c5a810b6f2e9d68e10b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-选择器"></span>
## 3.2 Selector


* When a dynamic field is added to the data panel, a corresponding dimension/metric selector is generated

* All selectors are single\-select


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4063cbed051414b9e8d06bb4c5264a1~tplv-goo7wpa0wc-image.image) </span>
