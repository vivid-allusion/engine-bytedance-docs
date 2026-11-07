---
title: "LOD Expression"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/LOD_Expression"
---

This article introduces how to use LOD expressions.

<span id="8f16c5f0"></span>
# Function overview

LOD stands for Level of Detail and refers to the detail level expression functionality. Detail level refers to the hierarchy of data aggregation granularity; different levels represent varying degrees of aggregation and granularity in the data.

LOD expressions can address issues involving multiple data detail levels within a single visualization view. To add a dimension during analysis whose detail level is higher or lower than the visualization detail level of the existing view, without changing the current chart display, use the detail level expression functionality.

**How to reference fields within LOD expressions**

The product supports the following two field reference formats, and users can choose according to actual needs. For more information, see [Data source fields and dataset fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields#d510d1e1).


* Use 'field name' for data source fields, as shown below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f0fa4a65ffb49ff9cdfa31f6f89da5a~tplv-goo7wpa0wc-image.image) </span>

* Use [field name] for dataset fields, as shown below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29a01cac4f8d45088090f3cf8d32b62c~tplv-goo7wpa0wc-image.image) </span>


<span id="dacbbb4d"></span>
# Caution

Because queries using LOD functions have a significant impact on performance, a single chart can query up to five fields containing LOD functions at the same time. If the number of LOD function fields in the chart exceeds five, the chart cannot be saved.

<span id="05fcb6df"></span>
# Quick start


1. Click Settings to the right of the dataset name and select "Add field".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6883604f3230400589484c034ae8ae98~tplv-goo7wpa0wc-image.image) </span>

2. Enter the display name for the field, specify the dimension or metric category, edit the expression, and then click Save.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc6c65ab7dd24b69869f4ca06a4d12a8~tplv-goo7wpa0wc-image.image) </span>

3. When using the newly added field for visualization queries, you can see that the aggregated original price for the same province remains the same, regardless of changes in order type.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d007e0c16a294fc681d53076776b3175~tplv-goo7wpa0wc-image.image) </span>


<span id="2ce76cc0"></span>
# Expression syntax

LOD expressions have the following structure:

`{[FIXED | INCLUDE | EXCLUDE]< dimension declaration >` **`:`** `< aggregation expression >}`


* The fixed function supports dimension filtering and introduces a new filter parameter: `{filter=true:fixed <dimension declaration> : <aggregation expression>}`

   * `filter=true`: Optional parameter. If this parameter is added, the dimension filter conditions set in the filter (such as region, color, and so on) and metric filter conditions (such as sales \> 1000 and so on) will be applied to the aggregation calculation process of the fixed function.

   * If `filter=true` is not added, the calculation of the fixed function will ignore all filters and be performed directly on all original data.

* < Dimension declaration \>: Specifies one or more dimensions to which the aggregate expression will be joined. Separate each dimension with a comma. For example: [Segment], [Category], [Region].

* < Aggregate expression \>: An aggregate expression is the calculation performed, resulting in an aggregate value.


<span id="dd1dc2e6"></span>
# Currently supported expressions

<span id="b0f0005f"></span>
## LOD functions as measures


|Expression |
|---|
|sum({include `Region`:sum(`Sales amount`)}) |
|sum({include [Region]:sum([Sales amount])}) |
|sum({include [Region]:avg([Sales amount])}) |
|sum({fixed [Region]:avg([Sales amount])}) |
|sum({exclude [Region]:avg([Sales amount])}) |
|sum({avg(`Sales amount`)}) |
|sum({fixed:avg(`Sales amount`)}) |
|sum({include [Region]:sum([Sales amount])+sum([Quantity])}) |
|sum({fixed [Region]:sum([Sales amount])+avg([Quantity])}) |
|avg({ include case when [Segment]='Company' then 1 else 0 end: sum([Sales amount])+max([Quantity])}) |
|sum({fixed [Region]:avg([Sales amount])}+[Discount]) |
|sum({include [Region]:avg([Sales amount])}+[Discount]) |


<span id="91f60712"></span>
## Fixed as a dimension


|Expression |
|---|
| |
| |
| |
| |


<span id="d05dc650"></span>
# Application examples

<span id="e3fac2c5"></span>
## FIXED

The FIXED level of detail expression calculates values using the specified dimensions, without referencing the dimensions in the view.

<span id="73a9284d"></span>
### Example 1: Calculate the total profit for each province

{fixed `**sale_province**`:sum(`**profit**`)}

The dimensions are `**sale_province**` plus `**sale_city**`, but since the FIXED level of detail expression does not consider the level of detail in the view, only the dimensions referenced in the calculation are used, which in this case is `**sale_province**`. For this reason, you may see that the value for a single city within each province is the same.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d69ff2b86ad84c1c81dcaea04520cf73~tplv-goo7wpa0wc-image.image) </span>

<span id="ad1a0227"></span>
### Example 2: Fixed as a dimension, customer purchase frequency

We often encounter customer purchase frequency analysis, where we analyze customer loyalty by examining the number and distribution of customer purchases.

Proposition: The distribution of customer purchase frequency, that is, how many customers have purchased once, twice, three times, and so on.


* Visualization focus: The number of customers for each purchase frequency.

* Visualization dimension: Purchase frequency (1, 2, 3, N)

* Background information to reference: The number of purchases for each customer

* {fixed `customer id`:uniq(`order id`)}


In the view, we used purchase frequency and customer count. This is an example of using one value to distinguish another value. LOD fixed can easily convert a measure into a dimension, which cannot be done by include or exclude.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/454658474ae44843a82e476fdf925b4d~tplv-goo7wpa0wc-image.image) </span>

<span id="d08f912b"></span>
### Example 3: Table\-scoped level of detail expression

A "table\-scoped level of detail expression" simply omits the dimension qualifier; in fact, it is a fixed level of detail expression without a dimension declaration. Therefore, we can regard a "table\-scoped level of detail expression" as the simplest level of detail expression.


* {avg([quantity])} Returns the average value over the entire range of quantity in the detailed data

* {sum([quantity])} Returns the sum over the entire range of quantity in the detailed data


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/480a0df0dc004463ad592c7c522c666f~tplv-goo7wpa0wc-image.image) </span>

<span id="a244a1f7"></span>
## INCLUDE

The INCLUDE function allows for further refinement of aggregate functions, enabling more precise calculations. It takes two parameters, with the expression formatted as {INCLUDE [Dimension a]:aggregate function([Metric b])}, meaning that metric b is aggregated based on dimension a.

For example, the expression `{INCLUDE [Customer id]:avg([Sales amount])}` means calculating the average sales amount by customer id. In application scenarios, when [Region] is placed as a dimension, the three metrics shown in the figure below represent the following meanings respectively:


* Sum(Sales amount): The total sales amount for each region

* Average(Sales amount): The average sales amount for each region (total sales amount divided by total number of orders)

* Average({INCLUDE [Customer id]:avg([Sales amount])}): The average customer sales amount for each region.


During the calculation process, first calculate the average sales amount for each customer (that customer's total sales amount divided by the number of orders for that customer), then calculate the arithmetic mean of the sales amounts for all customers in the region (sum of average sales amounts divided by the number of customers).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8748d6e6782d4cabb9cd97681abc8330~tplv-goo7wpa0wc-image.image) </span>

Taking Northeast as an example, first calculate the average sales amount corresponding to each customer id in Northeast, then calculate the average value of all customer average sales amounts in Northeast, which is 1547.5217.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f676598469242cc9319218fd198ba01~tplv-goo7wpa0wc-image.image" width="487px" /></div>


<span id="8d992793"></span>
## EXCLUDE

The EXCLUDE level of detail expression specifies the dimensions to be ignored from the view's level of detail.

The EXCLUDE level of detail expression is very useful for scenarios such as "percentage of total" or "difference from overall average".

The following level of detail expression excludes [Province/Autonomous Region] from the sum calculation of [Sales amount]:`{exclude [Province/Autonomous Region]:sum([Sales amount])}`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59989977a2474722b63fb5882a0100c2~tplv-goo7wpa0wc-image.image) </span>

{exclude [Province/Autonomous Region]:sum([Sales amount])} is the total sales amount for the corresponding region.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ef0679675054ec4b85851f8a5bbc294~tplv-goo7wpa0wc-image.image) </span>

<span id="0291febe"></span>
# Practical cases

<span id="0236b5f6"></span>
## Case 1: Calculating the sum of maximum values

<span id="8d6f7e14"></span>
### Scenario example

In data center quota management, it is necessary to group by psm, obtain the maximum capacity value of each data center under psm for the past 7 days, then group by psm to calculate the sum of these maximum values, and display the total sum of maximum values to assess the total quota capacity for each psm and data center.

For scenarios that require secondary aggregation, the LOD function can be used for processing.

<span id="1a251686"></span>
### Design approach

In this case, daily quota data for each psm and each data center is already available. However, since resource usage fluctuates daily, to be on the safe side, the actual quota allocated should be greater than the maximum resource quota in the past 7 days (there are multiple data centers under each psm).

Therefore, in this case, the aggregation approach is as follows:


1. Filter the data from the past 7 days, aggregate by psm and data center, and calculate the maximum quota at the data center granularity within the 7\-day period.

2. Aggregate by psm to calculate the quota for each psm, that is, the sum of the maximum values mentioned above.

3. Use the total function to calculate the overall quota.


<span id="ebd27a25"></span>
### Operation steps


1. Calculate the maximum quota at the data center granularity within the 7\-day period

   With the fields for data center, psm, and daily quota already available, use the LOD function, set the date filter to the most recent 7 days with data, calculate the maximum quota at the data center granularity within the 7\-day period, and save it as a metric field.

   The expression is as follows: `{fixed [机房-演示],[psm-演示]:max([cpu配额])}`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Aggregate based on the data center and psm fields, and calculate the maximum value of the cpu quota field. Since the filter selects the last 7 days, the result is the maximum value for the last 7 days.   </div>
   

2. Set as metric

   Select psm as the dimension, drag the above field to the metrics bar, select "Sum" as the aggregation method, and calculate the required quota for each psm.

3. Calculate the total quota

   Use the [Total](https://docs.byteplus.com/docs/DataWind/Total) function to sum the total quota for each psm and display it at the top of the chart.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ffaf261c46b48f7915d8abb0b2e97e2~tplv-goo7wpa0wc-image.image) </span>

<span id="e5656fea"></span>
## Case 2: Specify aggregation dimension and view value distribution

<span id="74e99373"></span>
### Scenario example

**Background**: As shown in the figure, this is a dataset at the order granularity, containing detailed data for each order, including order ID, the province where the order occurred, order amount, and more.

**Requirement**: Aggregate by province to calculate the total sales amount for each province (the sum of payment amounts), and view the distribution of this data (that is, the sales amount for each province). Distribution: View the distribution within the following ranges: 0–20w, 20–40w, 40–60w, 60–80w, 80–100w, and above 100w, that is, the number of provinces whose sales amount falls within each range.

<span id="770520fe"></span>
### Design approach

The challenge in this case is that the dataset is at the order granularity, while the required distribution data is at the province granularity. Therefore, it is necessary to first aggregate by province, and then perform a secondary process to view the distribution data.

The aggregation approach is as follows:


1. Specify the province dimension, sum the payment amounts, and create a "payment amount by province" field.

2. Use the grouping function to segment provincial payment amounts: 0(20w, 20)40w, 40(60w, 60)80w, 80~100w, 100w

3. Take the segmented provincial payment amount field as a dimension and calculate the distinct count of provinces, that is, the number of provinces.


<span id="69effcb2"></span>
### Operation steps


1. Create a new "Provincial payment amount" field

   Specify the [Province] dimension, calculate the sum of [Payment amount], and save it as a dimension.

   The expression is:  **{fixed [Province]: sum([Payment amount])}** 

2. Segment provincial payment amounts

   Select the field and [Configure Field Grouping](https://docs.byteplus.com/docs/DataWind/Configure_Field_Grouping).

   Group by step size, and set the name and condition for each group as needed.

3. Calculate the number of provinces in each segment.

   Use the above grouping field as a dimension, drag the "Province" field to the metrics bar, and select "distinct count" as the aggregation method for the metric.

   Select bar chart as the chart type and set the sorting.
