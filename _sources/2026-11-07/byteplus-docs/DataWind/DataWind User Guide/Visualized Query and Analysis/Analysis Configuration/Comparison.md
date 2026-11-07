---
title: "Comparison"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Comparison"
---

<span id="_1-概述"></span>
# 1. Overview

Comparative analysis refers to data differences caused by other influencing factors (comparison conditions) under the same data standards (the same dimensional metrics). The purpose of comparative analysis is to discover these differences and further explore the underlying causes, thereby finding optimization methods. DataWind provides a comparative analysis component that supports comparing two or more groups of data under the same dimension.

**Example**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/750c4b56460040579b19a2ea7722ee41~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios

In a single chart, compare prices and price differences across various categories for different regions simultaneously.

<span id="_2-2-使用过程示例"></span>
## 2.2 Usage process example

After configuring a table, the dimension is "type" and the metric is "price".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afffa36be56f468dafa56df6759f6b5b~tplv-goo7wpa0wc-image.image) </span>

**Step 1: Click the "Analysis" tab in the middle panel and select "Comparison".** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/145c35ff00cd47208b286e06445c2396~tplv-goo7wpa0wc-image.image) </span>

**Step 2: Drag the dimension field used as the comparison condition and configure it.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/326df84b0bb04c55bc52acfdcf224951~tplv-goo7wpa0wc-image.image) </span>

**Step 3: After specifying the calculation type, click "Apply".** 

To display only the prices for "Shanghai" and "Beijing", simply check "Original value".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd3713ce2bfb4101959510031d2c706a~tplv-goo7wpa0wc-image.image) </span>

This completes a basic comparative analysis workflow. To adjust the style, you can modify the display name and data format in the capsule UI element, or convert the chart style to another chart type.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4deaa62e7b814b179c4dbe7b0f4e12c7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-添加对比条件"></span>
## 3.1 Add comparison conditions

Multiple dimensions can be added to a comparison condition, and they have an "and" relationship.

By default, we provide two comparison condition configurations. To add more comparison conditions, click the add button to continue adding.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c743e9043ec448fda809b7ff364acdb8~tplv-goo7wpa0wc-image.image) </span>

By default, "Comparison condition 1" serves as the baseline condition, and there is an icon next to the title.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1afdfd852d4b4e7d9ca7118f1db71202~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-复制对比条件"></span>
## 3.2 Copy comparison conditions

If your comparison conditions are similar, you can use the copy function to quickly add comparison conditions. When the mouse hovers over the panel, a "Copy" button appears in the upper right corner of the title. Click it to directly copy the current comparison condition.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/571b5a3a82f74d1aa9e31e010b4a877f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-设置生效指标"></span>
## 3.3 Set effective metrics

By default, all indicators in the indicator bar are treated as effective indicators. To modify the effective indicators, click the dropdown list to reselect them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d3a93fa711a402381c711f2833f232e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-切换基准条件"></span>
## 3.4 Switch the benchmark condition

By default, "Comparison Condition 1" is set as the benchmark condition. To change the benchmark condition, click the dropdown list. After switching, a "Benchmark" label will appear next to the title of the corresponding comparison condition.

<span id="_3-5-选择计算类型"></span>
## 3.5 Select the calculation type

We provide four calculation types:


* Original value: The indicator value under the comparison condition.

* Difference value: Comparison condition value \- benchmark condition value.

* Difference percentage: (Comparison condition value \- benchmark condition value) / benchmark condition value \* 100%.

* Ratio: Comparison condition value / benchmark condition value.

* Confidence interval: An interval defined by the upper and lower confidence limits of the statistic.


The conditions for triggering the confidence interval are relatively strict:


* Confidence interval calculation is only supported when there are two comparison conditions.

* A field for calculating the confidence interval must be specified, and this field must be a numeric dimension.

* When entering the field, it must be an expression, not a field name.


<span id="_3-6-原始字段胶囊与衍生字段胶囊"></span>
## 3.6 Original field capsules and derived field capsules

After applying the comparison condition, the effective indicators will **split** into a series of derived indicators as required.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ac7122cb0dd4376912d6209da7cdf4d~tplv-goo7wpa0wc-image.image) </span>

Unlike original indicators, derived indicator capsules have a lighter color and a dashed border. They cannot be deleted individually. To delete derived indicators, deselect them in the configuration bar on the left.

At this point, the original indicator capsule serves only as a placeholder and is not displayed in the chart. (Because it has already been split into the original values for comparison)

Each derived indicator supports modifying the display name, data format, and more.

Capsules can be reordered by dragging and dropping between them.
