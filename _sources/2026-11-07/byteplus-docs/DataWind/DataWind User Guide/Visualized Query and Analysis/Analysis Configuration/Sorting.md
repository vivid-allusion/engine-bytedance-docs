---
title: "Sorting"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Sorting"
---

<span id="_1-概述"></span>
# 1. Overview

The sorting component supports sorting the horizontal axis, vertical axis, and dimension fields within charts. DataWind provides components with sorting functionality, offering three sorting methods: ascending, descending, and manual sorting. Date fields only support ascending and descending order, while other fields allow custom ordering of field values.

**Example**:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3525535517dd46b28c910736455a1b76~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-表格排序"></span>
## 2.1 Table sorting

**Step 1**: Use the dropdown to select the field to sort by, and choose the sorting method.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97cd2bdecada49eeb999260a1b1de16a~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click "Apply".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84d66d894bea4418909c0620f1630bd3~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-图表排序"></span>
## 2.2 Chart sorting

**Step 1**: Use the dropdown to select the field to sort by, and select the sorting method.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/915aad821f7f4b38b7206f06184d4913~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click "Apply".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fae3b38b10044e8a5535157382df966~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-表格排序"></span>
## 3.1 Table sorting

<span id="_3-1-1-表头排序"></span>
### 3.1.1 Header sorting

The table provides header sorting for single\-condition sorting. Hover the mouse over the field in the header and click the sort button to easily configure sorting.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6453a78236264264bedf6b2fd949c7af~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-排序配置"></span>
### 3.1.2 Sorting configuration

Header sorting is equivalent to a quick sorting configuration. Clicking the sort button in the header will automatically generate a sorting rule in "Sorting" by default. At the same time, "Sorting" supports multi\-condition sorting, allowing multiple sorting rules to take effect simultaneously. Example: Sort order types in ascending order, and within the same order type, sort payment dates in descending order. Then modify it to first sort by payment date in descending order, and then by order type in ascending order.

**Step 1**: Sort product types in descending order.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f6bdfa227a94c74a1c707404a43ae3d~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Add a sorting rule to sort order dates in descending order.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13e20435b8af4b3e87950a49ef84c2ba~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Use the order adjustment buttons to change the order of the above sorting rules. Move "product_type ascending" down or "order_date descending" up; here, the first method is used.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/454b592ee3e2444499e6e730e868da8d~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Click "Apply".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3bb40c0fa5c4f62bed2b1cf3899f71a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-图表排序"></span>
## 3.2 Chart sorting

<span id="_3-2-1-数值排序"></span>
### 3.2.1 Value sorting

For X and Y axis charts, when there is only one dimension field in the data panel, value sorting can be performed. The sorting basis can be the axis dimension field itself or any metric field in the data panel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96c90dafd88a4a0bb22592e346b3988d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-2-维度轴排序"></span>
### 3.2.2 Dimension axis sorting

For X\- and Y\-axis charts, when there are multiple dimension fields on the data panel, dimension axis sorting can be performed. The sorting basis can be the axis dimension field itself or any metric field on the data panel.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c74f3c849a084622a903ab1644be815a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-3-图例排序"></span>
### 3.2.3 Legend sorting

For XY\-axis charts, when there are multiple dimension fields on the data panel, or for charts without axis dimensions such as pie charts and scatter plots, legend sorting can be performed. The sorting basis can be "dimension\-legend" or any metric field on the data panel. Each data point within a dimension will be sorted according to a unified legend order.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f97e58757de74ea8946220ceed5a419e~tplv-goo7wpa0wc-image.image) </span>

**Legend sorting calculation logic**: The calculation is performed based on the legend's dimension according to the metric calculation logic, and after calculation, the sorting is applied directly, as shown in the figure below:


|**Horizontal axis dimension** |BU name |
|---|---|
|**Legend** |Product name |
|**Metric calculation** |sum (revenue) |
|**Legend sorting calculation logic** |**Product name** is **sorted in ascending order** based on the **sum of revenue** data |
| |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/859f73a0f6df41aa916e1274e94511ac~tplv-goo7wpa0wc-image.image) </span> |
|**Example** |The product names in the chart below are sorted as described above. For each dimension (BU name), multiple product names are displayed on a single bar. The order follows the table above and matches the top\-to\-bottom sequence of the legend on the right. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/439fa4cf800147e59d552d137e1e7532~tplv-goo7wpa0wc-image.image) </span>

<span id="e14d903e"></span>
## 3.3 Pivot table sorting

By default, there are two options to select for pivot table sorting: the first is to select the sorting field, and the second is to select the sorting basis.

**The sorting field determines the calculation scope for sorting, while the sorting basis determines which field's result is used for sorting. Only the currently selected sorting field will be sorted, and the order of other dimensions will not be affected.** 

<span id="afc97627"></span>
#### Scenario 1: Sorting by row dimension

**Example 1:**  If "Primary Channel" is selected as the sorting field and "Payment Amount" is selected as the sorting basis, the sorting will first calculate the sum of payment amounts for each "Primary Channel" enumeration value, and then sort the "Primary Channel" accordingly.

For example, the sum of "Payment Amount" for all "Marketing Activities" and the sum of "Payment Amount" for all "Official Website and App Store"; the sorting will only affect the order of "Primary Channel" enumeration values, not the order of other dimensions, so after sorting, the "Payment Amount" within each "Primary Channel" will still be unordered.

**Example 2:**  When the sorting field is set to "secondary channel" and the sorting basis is set to "payment amount", the sorting will first calculate the sum of the "payment amount" for each "secondary channel". Then, the "secondary channels" under each "primary channel" will be sorted accordingly.

In this case, the sorting only adjusts the order of the "secondary channels" under each "primary channel". Therefore, whether you choose ascending or descending order, it will not affect the order of the "primary channels".

**Example 3:**  When the sorting field is set to "payment method" and the sorting basis is set to "payment amount", the sum of the "payment amount" for each "payment method" will be calculated first. Then, the "payment methods" under each "secondary channel" will be sorted accordingly (since "payment method" does not have a lower\-level dimension, the sum of the "payment amount" corresponds to its own value).

At the same time, the sorting will only affect the order of the "payment methods" under each "secondary channel" and will not affect the order of the enumeration values for "primary channel" and "secondary channel".

**Summary:**  Based on the three examples above, the logic of pivot table sorting can be summarized as follows: Pivot table sorting calculates the **sum of the sorting basis field** at the **enumeration value granularity** of the **sorting field**, and then sorts the **enumeration values of the sorting field** within the **upper\-level dimension of the sorting field**.

<span id="52c2854f"></span>
#### Scenario 2: Sorting by column dimension

When a column dimension is added to the pivot table, you can select the column dimension field as the sorting field. The sorting rules for column dimension fields are the same as those for row dimensions.

For example, if the sorting field is set to "payment method" and the sorting basis is set to "payment amount", the sum of the "payment amount" for each "payment method" will be calculated first, and then sorting will be performed based on this sum. This can be observed by adding a column total, that is, first calculate the total for each column, and then sort according to the total.

<span id="0688ee31"></span>
#### Scenario 3: Quick sort

The quick sort feature in pivot tables differs from sorting in regular tables. Once quick sort is applied, a sorting configuration is automatically added in the "Analysis \- Sort" feature, where you can view the status of the sorting configuration:

**Quick sort when only row dimensions are present**

When sorting by a metric or the last row dimension, the sorting result is based on sorting the last row dimension. For details, refer to **Example 3 in Scenario 1** above.

When sorting by other dimensions, refer to **Example 1 and Example 2 in Scenario 1** above for the sorting result.

**Quick sort when column dimensions are present**

When column dimensions are added to the pivot table, multiple columns may be generated. When using quick sort, sorting is performed based on the currently selected column. Therefore, the sorting configuration generated in "Analysis \- Sort" will include an additional filter criteria field, indicating which column the sorting is based on.

**When the selected sorting field is a metric**, as shown in the figure below, the "Alipay APP" column under "Payment Method" is selected for quick sort. In this case, the generated sorting configuration will include a filter criterion for "Alipay APP", and the final sorting result will also be based on this column.

For the sorting method, refer to **Example 3 in Scenario 1** above; that is, for each "Secondary Channel" under every "Primary Channel", sorting is performed based on the "Payment Amount" in the "Alipay APP" column.

When the selected sorting field is a dimension, the sorting result is the same as in **Example 1 and Example 2 in Scenario 1** above, and sorting is performed based on the total result of the selected dimension's corresponding row.
