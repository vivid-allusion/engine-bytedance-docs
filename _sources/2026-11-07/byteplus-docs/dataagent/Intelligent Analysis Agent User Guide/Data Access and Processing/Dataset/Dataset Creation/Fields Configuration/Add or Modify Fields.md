---
title: "Add or Modify Fields"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Add_or_Modify_Fields"
---

When the current field content does not meet analysis requirements, you can choose to add a new field expression or modify an existing field expression to meet analysis requirements. The add or modify fields feature allows users to add new fields or modify existing fields in the field list using custom expressions. This document explains how to add and modify fields.

<span id="d244151a"></span>
# Use cases


* The current field format does not meet requirements and needs to be modified using an expression. For example: Modify a field to the date format.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6a57c8b047341b5bee473f5b5717a82~tplv-goo7wpa0wc-image.image) </span>


* New fields need to be created based on existing field information for data analysis. For example: Create a GMV field using the order quantity and order price fields.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a90bec8b0e46108f990ede8a34218f~tplv-goo7wpa0wc-image.image) </span>

<span id="4b825386"></span>
# Add fields


1. Click Data Preview and select "Add Field".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cfbdc5c41bb4faa8a5e04dbb368d1b0~tplv-goo7wpa0wc-image.image) </span>


2. Configure the parameters for the field to be added.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95ba0e97f23e46c6a68ac713d5fd9fea~tplv-goo7wpa0wc-image.image) </span>

The parameter descriptions are as follows.


|Parameters |Configuration instructions |
|---|---|
|Field name |Add a custom field name. |
|Dimension/metric |In the drop\-down list, select whether the added field is a dimension field or a metric field. See [Dimensions and Metrics](https://docs.byteplus.com/docs/dataagent/Dimensions_and_Metrics). |
|Display expression |If Display Expression is not selected, users will not be able to view the expression in any field information display area. |
|Field expression |Double\-click in the left operation area to quickly select data source fields, dataset fields, or parameters, then choose the required functions in the right area to flexibly construct field expressions. See [Parameter Management](https://docs.byteplus.com/docs/dataagent/Parameter_Management) for parameter introduction, [Introduction to Commonly Used Functions](https://docs.byteplus.com/docs/dataagent/Introduction_to_Commonly_Used_Functions) for function introduction, and for relevant references on data source fields, dataset fields, and common functions. |
|Field description |Detailed explanation of the data meaning, type, value range, constraints, and other relevant information for the field. |
|Save to dataset |If "Save to dataset" is not selected, the added field will be a personal expression field. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Personal expression fields can be used for data analysis and exploration, but differ from other fields as follows:</div>



* <div data-tips="true" data-tips-type="warning">When a field is a personal expression field, other users will not see this field when opening the dataset via "Switch dataset".</div>


* <div data-tips="true" data-tips-type="warning">When a chart contains a personal expression, sharing the link allows others to query the field, but they cannot modify the field or view its expression. Additionally, the field appears grayed out in the dimension or metric bar for other users.</div>


* <div data-tips="true" data-tips-type="warning">When a personal expression is referenced, it will be prefixed with "Personal".</div>



<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In addition to the visualization page, the field configuration page in the dataset data preview page or dataset editing page also supports adding fields.</div>


* <div data-tips="true" data-tips-type="tip">Refer to the documentation: <a href="https://docs.byteplus.com/docs/dataagent/Introduction_to_Commonly_Used_Functions">Introduction to Commonly Used Functions</a> for expressions and functions used when adding new fields.</div>


* <div data-tips="true" data-tips-type="tip">DataAgent does not support Lod functions (including linclude, lexclude, lfixed, and similar syntax), so custom fields containing such functions will not be synchronized to semantic configuration. It is recommended to use other supported functions or methods to meet requirements, and ensure re\-vectorization after completing field mapping in the dataset management module.</div>



<span id="dd7af3fb"></span>
# Modify fields

In addition to adding fields, the product also supports modifying the expressions of existing fields. On the Data Preview page, click "Modify Field" and then click "Expand Edit Box" to open the modify field page. The configuration is the same as described above for adding fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2398830c9ddc44238de23b1a0f141aeb~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e59d32066c2443ca90094e3e12cb37b0~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e068f99ce6e1490489552fe475cc8938~tplv-goo7wpa0wc-image.image) </span>

<span id="71d42396"></span>
# Batch add or modify fields

For situations where multiple fields need to be added or modified at the same time, the product supports batch modification of fields.

<span id="a92b71da"></span>
### Batch modification in Excel

On the Data Preview page, select "Batch Modify Fields", download the latest field list for modification, upload it after completing the changes, and click "Confirm" to complete the batch modification.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/950f5a0379b745409b85c716627eebb6~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8bd591099b44ec982139d3f1c3a7a9a~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="fb822ac9"></span>
### Batch modification on the Data Preview page

Open the dataset Data Preview page to directly modify or add fields on this page. Batch modification of expressions, deleting fields, adding fields, and modifying field types are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f44ed9fba6c491cb0bd81be6e592c3c~tplv-goo7wpa0wc-image.image) </span>

Click Edit in the expression options to open the add field page. For specific configuration, refer to the documentation in the section above on adding fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/849ab5aa12c0494196661bdbb6e7e369~tplv-goo7wpa0wc-image.image) </span>

Multiple fields can be configured at the same time. After configuring the fields, click Save in the upper right corner to save these fields.

<span id="65191e10"></span>
# Related references

<span id="c6f6506f"></span>
## Data source fields and dataset fields

On the left side of the Add Field or Edit Field page, a list of data source fields and dataset fields is displayed. The following table introduces both.


|Data source fields |Dataset fields |
|---|---|
|Data source fields are fields originating from upstream data sources of the dataset. On the model configuration page of the dataset, fields obtained by directly dragging in the entire upstream table or parsed through custom SQL and similar methods are considered data source fields.<br><br><br>* Data source fields can be used directly to add fields.<br><br>* Only fields selected on the model configuration page can be used in the data source field list.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc7d494696d94c6faa5f61dc30767ae1~tplv-goo7wpa0wc-image.image) </span> |Dataset fields are fields belonging to the dataset itself, including fields added by users within the dataset and personal fields.<br><br>Each data source field selected on the model configuration page automatically generates a dataset field, and the expression of these dataset fields is the data source field itself.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6be2024a76d34648ba3320b4a186ad86~tplv-goo7wpa0wc-image.image) </span><br><br>In version V2.62.0, a series of specifications and optimizations for naming dataset fields have been introduced, as follows:<br><br><br>* No duplicate field names<br><br>   * When the field length is greater than or equal to 128 characters: the first 10 valid characters of the original field plus a 16\-character MD5 code of the characters after the original rule are used as the alias.<br><br>* When field names are duplicated<br><br>   * Automatic renaming: add the [table name] suffix; field length less than 128 characters<br><br>   * Automatic renaming: add the [table name] suffix; field length greater than or equal to 128 characters: the first 10 valid characters of the original field plus a 16\-character MD5 code of the characters after the original rule are used as the alias. |


Differences between data source fields and dataset fields:


* Both data source fields and dataset fields can be used when adding or editing fields. The difference is that some dataset field expressions generated from data source fields may have been modified, so the expression is no longer the data source field itself. To use the original field in this case, use the data source field.

* For example, in the screenshot, both are payment amount fields. The dataset field's payment amount expression should originally be "`sales_price`", but it has been changed to "`sales_price`\*10". To use the original payment amount field, select "`sales_price`" from the data source fields.

* When you double\-click a data source field, the field name added to the expression is the data source field itself. When you add a dataset field, it will be enclosed in square brackets, and the field name will be displayed in green.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8a97183401b4b8f9084692f71c1840f~tplv-goo7wpa0wc-image.image) </span>

<span id="2611c0a3"></span>
## Common functions

On the right side of the Add Field or Edit Field page, the [Common Functions] area provides a function dictionary for users to consult. You can also click the usage guide to the right of Common Functions to go to the "Quick Start with Common Expression Functions" documentation for more functions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25bf1b183c944b96bcfbc28d9cf4258a~tplv-goo7wpa0wc-image.image) </span>
