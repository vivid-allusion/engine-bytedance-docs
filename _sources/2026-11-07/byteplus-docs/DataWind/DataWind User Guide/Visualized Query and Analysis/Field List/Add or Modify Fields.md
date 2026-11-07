---
title: "Add or Modify Fields"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Add_or_Modify_Fields"
---

When the current field content does not meet analysis requirements, you can choose to add a new field expression or modify an existing field expression to meet the analysis requirements. The add or modify fields feature allows users to add new fields or modify existing fields in the field list using custom expressions. This document describes how to add and modify fields.

<span id="159f7cf9"></span>
# Application scenarios


* When the current field format does not meet requirements, you need to modify the format using an expression. For example, modify a timestamp to a date format.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce43270f3a294be09dc72bbccb32c8b5~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/871fd51f28fd4485968cfdb5dd1e4606~tplv-goo7wpa0wc-image.image) </span>

* You need to create a new field based on existing field information for data analysis. For example, create a GMV field using the order quantity and order price fields.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09c63cff06ed44b9908c0a80230b4a78~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c5bee802ba64caf93e3c737c0e3af42~tplv-goo7wpa0wc-image.image) </span>


<span id="efe08e1f"></span>
# Add field


1. Click Settings to the right of the dataset name and select "Add field".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fe39f53e411443c87d91c273776be7c~tplv-goo7wpa0wc-image.image) </span>

2. Configure the parameters for the field to be added.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce6eb97be9d14152a695e4137639592d~tplv-goo7wpa0wc-image.image) </span>

   The parameter descriptions are as follows.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Field name |Customize the field name to be added. |
   |Dimension/Metric |In the drop\-down list, select whether the field to be added is a dimension field or a metric field. |
   |Display expression |If Display Expression is not selected, users will not be able to view the expression in any field information display area. |
   |Field expression |Double\-click to quickly select data source fields, dataset fields, or parameters in the left operation area, and select the required function in the right area to flexibly build the field expression. For parameter descriptions, see [Parameter Management](https://docs.byteplus.com/docs/DataWind/109997). For function descriptions, see [Introduction to Commonly Used Functions](https://docs.byteplus.com/docs/DataWind/Introduction_to_Commonly_Used_Functions). For information on data source fields, dataset fields, and common functions, see **related references**. |
   |Field description |A detailed explanation of the data meaning, type, value range, constraints, and other relevant information for the field. |
   |Save to dataset |If "Save to Dataset" is not selected, the added field will be a personal expression field. |
   

   Caution: Personal expression fields can be used for data analysis and exploration, but differ from other fields in the following ways.

   * When a field is a personal expression field, other users will not see this field when they open the dataset via "Switch dataset".

   * When a chart contains a personal expression, if you share the link with others, they can query this field but cannot modify the field or view the field expression. At the same time, this field will appear grayed out in the dimension or metric bar for other users.

   * When a personal expression is referenced, it will be prefixed with "Personal".


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In addition to the visualization page, the field configuration page in the dataset's data preview page or dataset editing page also supports adding fields.</div>


* <div data-tips="true" data-tips-type="tip">The expressions and functions used when adding new fields can be referenced in the document: <a href="https://docs.byteplus.com/docs/DataWind/Introduction_to_Commonly_Used_Functions">Introduction to Commonly Used Functions</a>.</div>



<span id="c505053a"></span>
# Modify field

In addition to adding fields, the product also supports modifying the expressions of existing fields. In the dimension and metric bar on the left side of the visualization page, find the field you want to modify, click the option after the field, and the modify field page will pop up. The configuration is the same as described above for adding a field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e43e19270fec4ed3b27cbd6231b18a60~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4c1491d6bc043869f1f84a4a76796d0~tplv-goo7wpa0wc-image.image) </span>

<span id="b01ecfbd"></span>
# Batch add/modify fields

For situations where you need to add or modify multiple fields at once, the product supports batch modification of fields.


1. On the visual query page, click Settings to the right of the dataset name and select "Batch edit fields".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/028eaf19cf6a492a8c4dc8022278219c~tplv-goo7wpa0wc-image.image) </span>

2. After clicking, you will be redirected to the dataset data preview page, where you can directly modify or add fields. This page supports batch editing expressions, deleting fields, adding fields, changing field types, and more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eebd331647f5477fa6ec9b98b33483f9~tplv-goo7wpa0wc-image.image) </span>

3. Click Edit in the Expression option to open the Add Field page. For detailed configuration, refer to the Add Field section above.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15474203e01445c8890c5dbfc676f8cc~tplv-goo7wpa0wc-image.image) </span>

4. You can configure multiple fields at the same time. After configuring the fields, click Save in the upper right corner to save these fields.


<span id="9909be65"></span>
# Related references

<span id="d510d1e1"></span>
## Data source fields and dataset fields

On the left side of the Add Field or Edit Field page, lists of data source fields and dataset fields are displayed. The following table introduces both.


|Data source field |Dataset field |
|---|---|
|Data source fields are fields from the upstream data source of the dataset. On the model configuration page of the dataset, fields obtained by directly dragging the entire upstream table or parsing through custom SQL and other methods are considered data source fields.<br><br><br>* Data source fields can be used directly when adding fields.<br><br>* Only fields selected on the model configuration page can be used in the data source field list.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61956f1624bc4013b3b7266565826600~tplv-goo7wpa0wc-image.image) </span> |Dataset fields refer to the fields within the dataset itself, including fields added by the user in the dataset and personal fields.<br><br>For each data source field selected on the model configuration page, a dataset field is automatically generated, and the expression of these dataset fields is the data source field itself.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17903e88572b46dbb898c9514d8e5f45~tplv-goo7wpa0wc-image.image) </span><br><br>In version V2.62.0, a series of specifications and optimizations have been made for the naming of dataset fields, as follows:<br><br><br>* No duplicate field names<br><br>   * When the field length is greater than or equal to 128 characters, the first 10 valid characters of the original field plus the 16\-character MD5 code of the remaining characters of the original field are used as the alias.<br><br>* When field names are duplicated<br><br>   * Automatically rename by adding the [table name] suffix when the field length is less than 128 characters.<br><br>   * Automatically rename by adding the [table name] suffix when the field length is greater than or equal to 128 characters: the first 10 valid characters of the original field plus the 16\-character MD5 code of the remaining characters of the original field are used as the alias. |


Differences between data source fields and dataset fields:


* Both data source fields and dataset fields can be used when adding or editing fields. The difference is that some dataset field expressions generated from data source fields have been modified, so the expression is no longer the data source field itself. To use the original field, you need to use the data source field.

* For example, in the screenshot, both are payment amount fields. The expression for the payment amount dataset field should originally be "`payment amount`", but it has now been changed to "`payment amount`\*10". To use the original payment amount field, select "`payment amount`" from the data source fields.

* When you double\-click a data source field, the field name added to the expression is the data source field itself. When you add a dataset field, it is enclosed in square brackets, and the field name is displayed in green.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d332cb04f41b9b3d928bec1a88b55~tplv-goo7wpa0wc-image.image) </span>


<span id="2e2ffd08"></span>
## Common functions

On the right side of the Add Field or Edit Field page, the [Common Functions] section provides a function dictionary for users to consult. You can also click the usage guide next to Common Functions to access the "Quick Start Guide to Common Functions in Expressions" document for more functions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acfb2d9d2d924af785cd9ddbfda2003c~tplv-goo7wpa0wc-image.image) </span>
