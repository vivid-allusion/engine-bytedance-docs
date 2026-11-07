---
title: "RFM Tags"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/RFM_Tags"
---

<span id="_1-产品概述"></span>
# 1. Product Overview

Supports the creation of RFM model labels, allowing users to customize the R, F, and M indicators to determine customer value. In this function module, companies can flexibly create RFM labels to measure customer value based on customer transaction frequency and transaction amount, develop refined operation strategies, and promote user purchase decisions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">RFM tags do not support real\-time calculation</div>


<span id="_2-名词解释"></span>
# 2. Glossary

This model evaluates the high and low values of R, F, and M for each user, categorizing them into different intervals to divide users into 8 types of customer value: Important Value Customers, Important Return Customers, Important Cultivation Customers, Important Retention Customers, Potential Customers, New Customers, General Maintenance Customers, and Lost Customers.


* R: Recency (last purchase), reflecting a customer's activity level

* F: The frequency of consumption (Frequency), reflects a customer's loyalty

* M: The consumption amount (Monetary), reflects a customer's contribution


<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_37cf224e32f905a910781fd9d0c071eb) </span>

In the RFM model, the closer the user's most recent consumption, the better, as such users are more sensitive, resulting in more significant marketing effects; The frequency of consumption should be higher, indicating higher customer satisfaction and stronger repurchase intentions; The higher the consumption amount, the better, as users with higher transaction amounts contribute more to the product and belong to high\-value users.

<span id="_3-操作步骤"></span>
# 3. Operation Steps

Go to the **Labeling System** module, click the **Create Label** button, and select **RFM Label** to enter this functional module.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1575122c5f6edd5edadb25259021ea0a.png) </span>

<span id="_3-1-配置基础信息"></span>
## 3.1 Configure Basic Information


* Label Name: The name of the new label (within 100 characters; under the same project, label names cannot be repeated)

* Path: Select the folder category where the label is located


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Creating a tag \- involving two switches in the path:</div>



1. <div data-tips="true" data-tips-type="tip">Group switch: In the project center \- group configuration \- function configuration section, there is a <strong>label directory permission control</strong> switch, which is off by default. When turned on, strict permission control will be applied to the "directory" when creating a tag, allowing only users with no <strong>edit tag tree</strong> permission to place tags under "Uncategorized".</div>


2. <div data-tips="true" data-tips-type="tip">Module switch: After turning on the <strong>label directory permission control</strong> switch, users without <strong>edit tag tree</strong> permission will default to the "Uncategorized" path when <strong>creating a new tag</strong> (project administrators can authorize users in <strong>project center \- permission</strong>).</div>


* Description: Enter the label description for reference by other label users

* Calculation Type: Optional offline calculation or real\-time calculation

* Update Type: Optional Scheduled Update or Manual Update

* Execution Frequency: When scheduling updates, you need to set the update frequency and time, supporting daily/weekly/monthly synchronization

* Calculation Result Storage Rules: When scheduling updates, you can set the number of historical versions to retain. Excess versions will be deleted the next day

   * If **Unlimited** is chosen here, the default value set by the group will be used

   * If **Specified Duration,**  specify the number of recent result versions to retain. For example, entering 4 \- Daily: retain the latest 4 days; Weekly: retain the latest 4 weeks; Monthly: retain the latest 4 months of results. The smaller value between the group settings will prevail.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TTL (Time To Live): The data lifecycle, i.e., the time to make stored data invalid;</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6dacc487bedff96eb7b7f8a41f0ba47b.png) </span>

<span id="_3-2-配置标签规则"></span>
## 3.2 Configuration Tag Rules

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_de0209992d86b21668601c125466dbf8) </span>

**1) Select Date & Time.**  Support selecting detailed data/attribute data/tag data sources. The corresponding application scenarios and RFM calculation logic are as follows:


|**Data Source** |**Use Case** |**How to obtain RFM** |
|---|---|---|
|Detailed Data |The detailed table records order data (by order ID, recording user ID, consumption amount, and consumption time for each purchase) |Aggregate order data according to the user ID for calculating R (the number of days from the most recent consumption to today), F (consumption frequency), M (consumption amount) |
|Attribute data |Aggregate data according to the user ID to obtain R (the number of days from the most recent consumption to today), F (consumption frequency), M (consumption amount) as independent fields stored in the attribute table |Match the three independent fields with R, F, M, and use the field results as the calculation results |
|Label |Three existing labels match the calculation logic of R (the number of days from the most recent consumption to today), F (consumption frequency), M (consumption amount) |Match the three labels with R, F, M, and use the label results as the calculation results |


\*Note: When there is partitioned detailed data, you need to select the data calculation period; no need to select the data calculation period for attribute and label data, default calculation scope is the full data in the partition for the previous day.

**2) Define the values of R, F, M, and comparison values.** 


|**Data source** |**R value** |**F value** |**M value** |**Comparison value of parameters** |
|---|---|---|---|---|
|Detailed data |Date field displayed in the table |Numerical field displayed in the table, supporting aggregation configuration |Numerical field displayed in the table, supporting aggregation configurations for summation and averages |Average, median, or custom |
|Attribute data |Numerical field displayed in the table |Numerical field displayed in the table |Display numeric fields in the table |Average, median, or custom |
|Label |Display existing labels, text type labels display text label values, and require segmented assignment |Display existing labels, text type labels display text label values, and require segmented assignment |Display existing labels, text type labels display text label values, and require segmented assignment |Average, median, or custom |



* Numerical fields support using original values or assigning values by interval, which means dividing the original values into intervals and assigning scores. For example, in a 5\-point system, 0\-max is divided into 5 intervals and assigned 1, 2, 3, 4, 5 points respectively. Attention: The upper limit of intervals is 20.

* Support R, F, M switches. For example, in an enterprise scenario, if R values are not needed, you can toggle the button off, and obtain the four label values based on the rules of F and M values' superiority. Note that at least two indicators must be retained to create RFM labels.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_438b3e6253e5bb5e874fd08fb7a582c6) </span>

**3) Naming of label values.**  Display default names for 8 label values, allowing users to customize them.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5b5728a4aba8be8d6ddcf991068d1181) </span>

<span id="_3-3-查看标签详情页"></span>
## 3.3 View the details page of labels

Click on "Estimated Number" in the upper right corner to view the coverage of each label value. Click **Complete Creation** to finish creating the current label. You can view the distribution of current label people, historical details, operation records, etc., on the label details page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28ec5f407ef425b76efb3e91c45cb5ac.png) </span>
