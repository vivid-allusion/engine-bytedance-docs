---
title: "Replace Dataset"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Replace_Dataset"
---

<span id="815dd339"></span>
# 1. Overview

The replace dataset feature allows you to quickly switch datasets for a dashboard after it is created, updating the dashboard with the new dataset. In addition, after applying a dashboard template, you can retain the template's refined style while replacing the original dashboard data with your own business data.

**Common use cases**


* When the underlying dataset changes, you can replace the underlying data while keeping the charts in the dashboard unchanged.

* When creating a dashboard with general applicability, you may want to reuse it across multiple business lines. By copying dashboards and replacing their datasets, you can quickly complete the workflow from dataset creation to chart building and dashboard assembly.


**Current methods supported for replacing datasets in charts**


* Project Center Chart Management page: Allows you to batch replace datasets for charts under a project.

* Dashboard page: Allows you to batch replace datasets for charts on the dashboard (currently, replacing the dataset for a single chart on the dashboard is not supported).

* Visualization Query page: Allows you to replace the dataset for a single saved chart.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="dafc684d"></span>
## **Step 1: Entry point for replacement**

**Path 1: In the Project Center \- Chart Management module**, after filtering for the dataset to be replaced, click the icon for the chart whose dataset you want to replace, then click the [Replace dataset] icon on the right.

> Note: Only project administrators, chart owners, and dashboard administrators where the chart resides can perform dataset replacement.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14907da192c94385ad247f0dd3ecb89e~tplv-goo7wpa0wc-image.image) </span>

Users can also select multiple chart names to batch replace datasets. Caution: Only batch replacement for a single dataset is supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d9b464fa5de4d2ca68d5445a3170da9~tplv-goo7wpa0wc-image.image) </span>

**Path 2: In the dashboard editing interface, click "Replace dataset" in the upper right corner to batch replace datasets for charts on the dashboard.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74b86cdb4a6e4336b79507b6cb9503d6~tplv-goo7wpa0wc-image.image) </span>

<span id="2a1182cf"></span>
## **Step 2: Replacement configuration**

Fill in and complete the dataset replacement configuration. After selecting the target dataset for replacement, perform model field mapping, which includes data source field mapping (required) and dataset field mapping (optional). For a detailed explanation of data source fields and dataset fields, refer to [Fields and Field Expressions FAQs](https://docs.byteplus.com/docs/DataWind/Fields_and_Field_Expressions_FAQs). For the specific mapping results, see the feature introduction below.

Caution: The system automatically matches fields based on the model field names by default. If there is a data type mismatch, the model will be highlighted in red. Please ensure the types are consistent before proceeding to the next step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cebcb0f42b5b43a2bc33f641f7d26900~tplv-goo7wpa0wc-image.image) </span>

<span id="3a958ede"></span>
## **Step 3: Complete the replacement**

After confirming the mapping information, click "Next" to open the field confirmation page. If the original dataset fields used by the chart do not have fields with the same name in the target dataset, and no dataset field mapping is configured, the corresponding fields will be automatically added to the new dataset.

<span id="7d5d6056"></span>
# 3. Feature introduction

<span id="_3-1-支持替换的数据集类型"></span>
## **3.1 Dataset field mapping feature**

When configuring chart dataset replacement, since each data source field requires a mapping relationship, if the current chart contains many fields and chart dataset replacement is frequently performed,

manually configuring field mapping for each dataset replacement can be very cumbersome and incurs high operational costs.

To address this, field mapping configuration is provided, allowing you to pre\-configure mapping relationships between datasets. When performing chart dataset replacement for these mapped datasets, the mapping relationships will be automatically populated according to the configuration, reducing operational costs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/124472c6e0fb4bfa948930649b04c746~tplv-goo7wpa0wc-image.image) </span>

For detailed operation instructions, see [Field Configuration](https://docs.byteplus.com/docs/DataWind/Fields_Configuration).

<span id="_3-2-替换的匹配依据"></span>
## 3.2 Supported dataset types for replacement

Specific conditions for dataset replacement: Direct connection and extracted datasets from the same data source can be replaced; datasets from different data sources cannot be replaced. Replacement between different query engines (such as replacing Doris with ClickHouse) is currently not supported.


* Supported:

   * Standard datasets (including conventional extraction and direct connection datasets), mirror datasets

* Not supported:

   * Tag datasets, group datasets

   * Charts created based on visual JOIN


<span id="f0aeffd6"></span>
## 3.3 Replacement effects

**Data source field matching** mainly refers to replacing the fields on the chart and the **data source fields from the old dataset** referenced in expressions with **data source fields from the new dataset**.


* If the old dataset's field has **a field with the same name** in the new dataset, it will be directly replaced with the new dataset's field, and will **use the calculation logic of the new dataset's field** directly.

* If the old dataset's field does **not have a field with the same name** in the new dataset, the corresponding field will be automatically added to the new dataset during replacement, and the logic of the new field will **inherit the logic of the old dataset's field.** 


**Dataset field matching** allows **the current chart's field** to be **completely replaced with a field from the new dataset.** 


* This applies to scenarios where **the new and old datasets have fields with the same name**, but you need to replace field A from the old dataset with field B from the new dataset.


<span id="e78d4b03"></span>
## 3.4 Other impacts

<span id="64482d13"></span>
### 3.4.1 Dataset parameters


* There is no impact on project\-level "personal parameters".

* For dataset\-level "public parameters", if they were previously applied to the original dataset, after replacement, the scope of application will include the new dataset.


<span id="e5c13751"></span>
### 3.4.2 Hierarchy and categories

The hierarchy and categories of the original dataset will not be copied to the new dataset, and the hierarchy and categories of the new dataset remain unchanged.

<span id="7f03e87f"></span>
### 3.4.3 Permissions

After replacement, whether the permissions of the original dataset are appended or inherited to the new dataset depends on the settings.

<span id="02a69d9b"></span>
### 3.4.4 Dashboard

For charts that have replaced the dataset, or dashboards containing charts after dataset replacement, in principle, all components and configurations remain unchanged. This includes public filter components, linkage/jump configurations, chart colors, legend configurations, and other configurations.

<span id="_4-常见报错提示解析"></span>
# 4. Analysis of common error messages

<span id="_4-1-数据类型不匹配"></span>
## 4.1 Field data type mismatch

The datasets before and after chart replacement need to ensure that the model field data types are consistent.


* As shown in the screenshot below, "order_date" is a date\-type field, while "GMV" is a numeric\-type field, which will result in a field data type mismatch error.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14d5ceb53bfb4408b17cd1abc9068b84~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**When the above error message appears, the user can choose the following actions to adjust and optimize:** 


* Confirm whether the field type of the target dataset for replacement meets expectations; if modification is needed, the field type of the upstream table in the dataset must be modified;

* Caution: The field to be modified here is the model field of the dataset, not the dataset field.

   * If the dataset uses a Feishu table as its data source, modify the data type of the corresponding column in the Feishu table.

   * If the dataset uses a Hive data source, modify the data type of the corresponding field in the Hive table.

   * If the dataset uses a custom SQL model, you can perform the conversion in SQL using the CAST function.


<span id="_4-2-强制转换字段类型后，图表查询报错"></span>
## 4.2 Failed to retrieve field information

The following reasons may cause a failure to retrieve field information:


* Charts in the current dashboard are not only placed on this dashboard, but also on other dashboards, and the person making the replacement does not have edit permissions for those dashboards;

* There are too many charts on the current dashboard.
