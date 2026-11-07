---
title: "Lark Sheets"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Lark_Sheets"
---

<span id="_1-概述"></span>
# 1. Overview

Supports uploading Lark Sheets to create datasets, and datasets support **scheduled offline data updates.** 

**Prerequisite**: To enable Lark datasets, you must first complete the steps in [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9)“**2. Basic configuration**”.

<span id="_2-快速入门"></span>
# 2. Quick start

(1) Click Data Preparation, select Dataset—Create new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Click to select Lark Sheets.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3113dbaa92ae4817b2d9bbd0c76e8797~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(3) Enter the document link to upload, click OK, and once the Lark Sheets information is displayed, the connection is complete.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf2bfc8837f94e7eacf7573577e1d344~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-功能介绍"></span>
# 3. Features

<span id="_3-2-注意事项"></span>
## 3.1 Important notes


* Anyone using the link must have read permission.

* Providing a single link will import all sheets under that document.

* Only standard spreadsheets are supported.

* The document must be named and cannot be “Untitled Sheet”. Document and sheet names must not contain the English period '.', otherwise the document schema may fail to be retrieved.

* Only the first group of columns with consecutive non\-empty column names will be read; the first column name cannot be empty, otherwise an error will occur.

* Column names should be plain text, must not start with a number, must not be an image or hyperlink, must not be named p_date, and must not contain $, `(backtick), or !, otherwise synchronization may fail. After creating the dataset, do not arbitrarily modify the column names in Lark Sheets, or synchronization may fail. Column names that are too long may cause synchronization to fail.

* Column names should not be duplicated.

* Rows should not be empty. Fully empty rows are counted in the sheet's row count and will be included in the data as [null, null, null, null].

* Merged cells and formulas are not supported.

* Try to avoid having different data types in the same column, or synchronization may fail.


<span id="_3-3-常见报错原因"></span>
## 3.2 Common causes of errors


* Incorrect connection information

* Invalid link

* No permission

* Untitled sheet

* Token expired

* Schema error

* First column name is empty

* Invalid column name format


Note: If you encounter an error message not covered by the above issues, please contact CSM or initiate an after\-sales service inquiry.
