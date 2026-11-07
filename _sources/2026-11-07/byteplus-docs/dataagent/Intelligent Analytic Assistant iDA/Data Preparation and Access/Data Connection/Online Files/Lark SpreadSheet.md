---
title: "Lark SpreadSheet"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Lark_SpreadSheet__"
---

<span id="c8709fe7"></span>
# 1. Overview

Support uploading Feishu table to create a dataset, and the dataset supports **offline data to be updated regularly.** 

**Premise** : To open the Feishu dataset, you need to complete [Lark Integration](https://docs.byteplus.com/docs/undefined/69eafc0af72032055845ac44) the "**2. Basic configuration**" first.

<span id="d3ecb778"></span>
# 2. Quick start

(1) Click Data Preparation and select Dataset \- New Dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

(2) Click to select the Feishu form.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4aa341b39cdf4c6fb9699e128476eca9~tplv-goo7wpa0wc-image.image" width="600px" /></div>


(3) Fill in the document link that needs to be uploaded, click OK, and display the Feishu form information to complete the connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c5e8e0ea78a4171ac08615c34efa097~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="efbef482"></span>
# 3. Function introduction

<span id="7c78e2d4"></span>
## 3.1 Precautions


* Fill in the link, the scanner needs to have read permission;

* Filling in a link will import all the sheets under the document;

* Only support the identification of ordinary spreadsheets.

* The document needs to be named, not "unnamed table", and the document and sheet names should not contain the English dot '.', otherwise the document schema may fail to obtain;

* Only the first set of columns with consecutive non\-null column names will be read; the first column column name cannot be null, otherwise an error will be reported;

* The column name should be plain text, not starting with a number, not a picture, hyperlink, not named p_date, not including $, ' (backquotes),!, otherwise the synchronization may fail; after creating the dataset, the column name of the Feishu table should not be modified casually, otherwise the synchronization will fail. If the column name is too long, synchronization may fail;

* Listings should not be repeated;

* Rows should not be empty as much as possible, because if they are included in the number of rows in the sheet, they will also be added to the data in a format similar to [null, null, null, null];

* Does not support the processing of merged cells, does not support the processing of formulas;

* Try not to have different data types in a column, otherwise synchronization may fail.


<span id="f83b6c65"></span>
## 3.2 Common causes of errors


* The connection information is incorrect.

* The link is invalid.

* No permission.

* Unnamed table.

* Token expiration.

* Schema error.

* The first column is empty.

* Column format is not legal.


Description: If you have an error message that is not covered by the above problems, please contact CSM or initiate after\-sales services consultation.
