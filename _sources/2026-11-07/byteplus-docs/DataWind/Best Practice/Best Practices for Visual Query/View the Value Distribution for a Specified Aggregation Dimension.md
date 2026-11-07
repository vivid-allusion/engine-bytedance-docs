---
title: "View the Value Distribution for a Specified Aggregation Dimension"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/View_the_Value_Distribution_for_a_Specified_Aggregation_Dimension"
---

<span id="_1-场景示例"></span>
# 1. Scenario example

**Background**: As shown in the figure, this is a dataset at the order level, containing detailed data for each order, including order ID, the province where the order occurred, order amount, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c624f9b28e554937acf57c8e8d6a1b13~tplv-goo7wpa0wc-image.image) </span>

**Requirement**: Aggregate by province to calculate the total sales amount (sum of payment amounts) for each province, and view the distribution of this data (that is, the sales amount for each province). Distribution: View the distribution within the following ranges: 0–200,000, 200,000–400,000, 400,000–600,000, 600,000–800,000, 800,000–1,000,000, and above 1,000,000, that is, the number of provinces whose sales amount falls within each range.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1f67995aeb643fea9b8b744fa16273f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-设计思路"></span>
# 2. Design approach

The challenge in this case is that the dataset is at the order level, while the required distribution data is at the province level. Therefore, it is necessary to first aggregate by province, and then perform further processing to view the distribution data.

The aggregation approach is as follows:

(1) Specify aggregation by province, calculate the sum of payment amounts, and create a "payment amount by province" field

(2) Use the grouping function to segment the payment amount by province: 0–200,000, 200,000–400,000, 400,000–600,000, 600,000–800,000, 800,000–1,000,000, 1,000,000 and above

(3) Use the segmented payment amount by province field as a dimension, and calculate the distinct count of provinces, that is, the number of provinces

<span id="_3-操作步骤"></span>
# 3. Operation steps

(1) Create the "payment amount by province" field

Specify aggregation by the [province] dimension, calculate the sum of [payment amount], **and save as a dimension**. The expression is:

{fixed [province]: sum([payment amount])}

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9221f08209b64ff3b1fc522dbf824fbf~tplv-goo7wpa0wc-image.image) </span>

(2) Segment the payment amount by province

Select the field and [Configure Field Grouping](https://docs.byteplus.com/docs/DataWind/Configure_Field_Grouping)

Group by step size, and set the name and condition for each group according to requirements

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/146be23da6b9404bbff6a7c41f4ee2e8~tplv-goo7wpa0wc-image.image) </span>

(3) Calculate the number of provinces in each segment

Use the above grouping field as a dimension, drag the "province" field to the metrics area, and select "distinct count" as the aggregation method.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a34264691c664b7fa612df7b514398ef~tplv-goo7wpa0wc-image.image) </span>

Select the bar chart as the chart type, and set the sorting accordingly.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98adb9838f2b4436918f91e29e028855~tplv-goo7wpa0wc-image.image) </span>
