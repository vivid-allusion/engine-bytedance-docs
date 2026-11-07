---
title: "Lark Sheets"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Lark_Sheets"
---

<span id="_1-概述"></span>
# 1. Overview

Supports uploading Lark Sheets to create datasets. Datasets support **scheduled offline data updates.** 

**Prerequisite**: To enable Lark datasets, you must first complete “**2. Basic configuration**” in [Lark Integration](https://docs.byteplus.com/docs/dataagent/Lark_Integration_).

<span id="_2-快速入门"></span>
# 2. Quick start

(1) Click Data Preparation, select Dataset \> Create new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3244389cc7145bd8b1663a2ae326811~tplv-goo7wpa0wc-image.image) </span>

(2) Select Lark Sheets.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bdd40af52bd4f479621920a50ac9b1b~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(3) Enter the link of the document to upload, click Confirm. Once Lark Sheets information is displayed, the connection is complete.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bdd40af52bd4f479621920a50ac9b1b~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-2-注意事项"></span>
## 3.1 Caution


* The person scanning the code must have read permission for the link entered.

* Entering a single link will import all sheets under that document.

* Only standard spreadsheets are supported.

* The document must be named and cannot be “Untitled Sheet”. Document and sheet names must not contain the English period '.', otherwise the document schema may fail to be retrieved.

* Only the first group of columns with consecutive non\-empty column names will be read. The first column name must not be empty, otherwise an error will occur.

* Column names should be plain text, must not start with a digit, must not be images or hyperlinks, must not be named p_date, must not contain $, `(backtick), or !, otherwise synchronization may fail. After creating the dataset, do not arbitrarily modify column names in Lark Sheets, otherwise synchronization may fail. Column names that are too long may cause synchronization to fail.

* Column names should not be duplicated.

* Rows should not be empty. Fully empty rows are counted in the sheet's row count and will be added to the data in a format like [null, null, null, null].

* Merged cells and formulas are not supported.

* Do not mix different data types in a single column, otherwise synchronization may fail.


<span id="_3-3-常见报错原因"></span>
## 3.2 Common error causes


* Incorrect connection information

* Invalid link

* No permission

* Untitled sheet

* Token expired

* Schema error

* First column name is empty

* Invalid column name format


Note: If you encounter an error message not covered above, please contact CSM or initiate an after\-sales service inquiry.
