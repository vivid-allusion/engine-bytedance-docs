---
title: "Excel/CSV Data Connection"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Excel_CSV_Data_Connection"
---

Support for uploading local files (Excel and CSV files) for data connection. This article shows you how to access Excel/CSV data.

<span id="805435c9"></span>
# Usage Restrictions


1. Upper limit: 500M

2. Function: support join

3. Prerequisites for use: Users need to have the "Project Edit" or "Permissions \- Manage by User \- Module \- Data Connection \- New Connection" permissions to create a new data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">The system will only read the first set of columns with consecutive non\-null column names; the first column name cannot be null, otherwise an error will be reported .</div>


2. <div data-tips="true" data-tips-type="warning">The column name should be an ordinary text as much as possible, not all numbers, not pictures, hyperlinkes, and do not bring formulas, otherwise the upload will fail .</div>


3. <div data-tips="true" data-tips-type="warning">Index is a reserved word and cannot be used as a column name, otherwise it will fail .</div>


4. <div data-tips="true" data-tips-type="warning">The file encoding must be UTF\-8 .</div>


5. <div data-tips="true" data-tips-type="warning">List names cannot be repeated .</div>


6. <div data-tips="true" data-tips-type="warning">If the number of characters in the column name is too long, it will fail. It is recommended that no more than 10 characters be used .</div>


7. <div data-tips="true" data-tips-type="warning">If the field value is Chinese, the recommended length is no more than 30 Chinese characters .</div>



<span id="538c5226"></span>
# Operation Steps

<span id="f3c5deb4"></span>
## New data connection


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. Select **Local File \- Excel or CSV** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d03a169ca5b8425c97c58050fad95914~tplv-goo7wpa0wc-image.image) </span>

3. After clicking, locate the target Excel/CSV file in the local file and click Open. It supports uploading up to 5 files, and the total file size does not exceed 500M. It is recommended to choose no more than 10 sheets, otherwise the upload may fail.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc7b6c04863b4ab2a48d860eaee6e552~tplv-goo7wpa0wc-image.image) </span>

4. When the loading is complete to 100%, you can select the contents of the sheet in the file. Click Next to **preview data** and set the **data connection name** . After the preview is completed, click **OK** to complete the data connection of Excel/CSV.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c795ff89bb0547bbb0d240fbe6eea114~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81dd1dc633ce4936b2b04303d19daaed~tplv-goo7wpa0wc-image.image) </span>


<span id="dfe57b90"></span>
## Data update

Local file Excel/CSV does not support update, users can click **Edit** , by **appending files** and **replacing files** for data update.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dee22234cb4349c887606a78b2305e5c~tplv-goo7wpa0wc-image.image) </span>


|data update method |append file |Replace file |
|---|---|---|
|difference |Only offline files (Excel, CSV) support file append, and users can manually add new data to the dataset by file append. The file append function does not affect the synchronization of data in the file before appending, for example, when the user does the following:<br><br><br>* April 12: Users create data from an A file (containing 100 lines of data) and complete the first synchronization. April 13: Users use the file append function to upload a B file (containing 10 lines of data) and save it before resynchronizing the data.<br><br>* The partition data in the system is as follows: P_date = 0412:100 lines of data (from A file); P_date = 0413:110 lines of data (from A file + B file).<br><br>* Users can update additional data to the system by resynchronizing historical data. After resynchronizing the data of 0412, P_date = 0412 should contain 110 lines of data (from file A + file B). |Only offline files (Excel, CSV) are supported for file replacement. After a file is replaced, the data in the replaced file will stop synchronizing, for example, when the user does the following:<br><br><br>* April 12: Users create data from an A file (containing 100 lines of data) and complete the first synchronization. April 13: Users use the file replacement function to upload a B file (containing 10 lines of data) and save it before resynchronizing the data.<br><br>* The partition data in the system is as follows: P_date = 0412:100 rows of data (from A file); P_date = 0413:10 rows of data (from B file).<br><br>* Users can update replacement data to the system by resynchronizing historical data. After resynchronizing the data of 0412, P_date = 0412 should contain 10 lines of data (from the B file). |
|specific operation |1. Click "Edit" \- "Add File".<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f14a372d54e149b0b811e28b3d8836b3~tplv-goo7wpa0wc-image.image) </span><br><br>2. Click "Upload" and select the file you need to add to upload.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87315946e39048209610994233b002be~tplv-goo7wpa0wc-image.image) </span><br><br>3. In "Sheet Settings", click "Finish" after setting the matching relationship between the appended file and the original table field.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24750bc24ce842eb94977eab17b6528f~tplv-goo7wpa0wc-image.image) </span> |1. Click "Edit" \- "Replace File".<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4f0fc3ed4ae434d9bbb7d2d49657a60~tplv-goo7wpa0wc-image.image) </span><br><br>2. Click "Upload" and select the file you need to replace to upload.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f64aa0709db4021abfff48a7bc25950~tplv-goo7wpa0wc-image.image) </span><br><br>3. In "Sheet Settings" \- "Replace Fields", drop down Select Fields to replace the original fields. After replacing, click "Finish".<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8260cc0fc3c04185b95812c49677d9aa~tplv-goo7wpa0wc-image.image) </span> |


<span id="2aad954b"></span>
## Permission assignment

<span id="e5f943b5"></span>
### Authorization

Click on the data connection in the upper right corner of the **permission allocation** , you can authorize the data connection to other users, if you need to authorize multiple users, you can use English commas separated and pasted into the box, such as user1, user2. Authorization items include: viewing, editing, and managing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63ba631f779d4037ad8a881536431c47~tplv-goo7wpa0wc-image.image) </span>

<span id="c8fe7a18"></span>
### Transfer owner

Click on the three points on the data connection to select "Transfer Owner" to transfer ownership.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/959365f1f23b49eb92f1e8e9e36f04c9~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6af247a292d48b59fcaa0e1226b866e~tplv-goo7wpa0wc-image.image) </span>

<span id="1ede3047"></span>
## Basic information view

Hover over the corresponding data connection to view the details of the data connection, including name, creator, and creation time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e9f2d6d03a742218fe4f880b27e6b47~tplv-goo7wpa0wc-image.image) </span>

<span id="e424cd70"></span>
## Data source deletion

Click on the three points on the data connection and select the "Delete" button to delete the data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/959365f1f23b49eb92f1e8e9e36f04c9~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e994eb7f4624380a4a05297d1fb6d35~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Attention</strong></div>


<div data-tips="true" data-tips-type="tip">If the prompt appears [This data connection is associated with x downstream will not be available], it needs to be handled with caution.</div>
