---
title: "Local Excel/CSV File"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Local_Excel_CSV_File"
---

This article shows you how to upload a local Excel/CSV file to create a dataset.

<span id="7ccd0418"></span>
# Precautions


* Uploaded Excel/CSV file size requirements:

   * Data connection upload file size limit: 500 M

   * Additional file size limit: 500 M

   * Alternative file size limit: 500 M

* Uploaded Excel/CSV file column name requirements:

   * The first column cannot be empty (the system will only read consecutive columns with non\-empty column names).

   * It needs to be ordinary text, prohibited from starting with numbers, all numbers, pictures, hyperlinkes, including formulas, composed of double underscores （__）

   * Do not use reserved words as column names (case insensitive): `index`, `constraint`

   * Listings cannot be repeated

   * The number of characters in the column name should not be too long (no more than 10 characters are recommended).

* Field value requirements: If the field value is in Chinese, the recommended length should not exceed 30 Chinese characters

* File encoding requirements: UTF\-8

* CSV connector support range: support text files & support specified delimiters


<span id="372e3e46"></span>
# New from data connection


1. Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

2. Select the Excel/CSV connection method on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d8eb3d22fa74383882bf7cc6ba8a92b~tplv-goo7wpa0wc-image.image) </span>

3. Select the Excel/CSV file that needs to be uploaded.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/634009e632864ec29d1407568048656d~tplv-goo7wpa0wc-image.image) </span>


<span id="df1b16d7"></span>
# Create a new dataset


1. Enter the Volcano Engine, click "Data Preparation" \- "Dataset", and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click Excel/CSV.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e39d66ae321f4351abecbc27e7ddf5c9~tplv-goo7wpa0wc-image.image) </span>

3. Select the Excel/CSV file that needs to be uploaded.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f8b5d3bbb3940669298dc5013826334~tplv-goo7wpa0wc-image.image) </span>


<span id="9010ea5a"></span>
# Next steps: Create a dataset


1. Create the dataset using the previously created data connection. Click "Data Preparation" \- "Dataset" and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. Search or drop down to select the previously created data connection. More please refer to [Overview of Dataset Creation](https://docs.byteplus.com/docs/dataagent/Overview_of_Dataset_Creation_).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/338b70f6489d4ec49b0b1052c0611315~tplv-goo7wpa0wc-image.image) </span>


<span id="67e4576a"></span>
# Other features

<span id="95c0896e"></span>
## Basic information view

Hover over the corresponding data connection to view the details of the data connection, including name, creator, and creation time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d115c039f4b4002a7c3ebb840fcd5e6~tplv-goo7wpa0wc-image.image) </span>

<span id="91d2195a"></span>
## Append file

Local files (Excel/CSV) do not support updates, but file appends are supported. Users can manually add new data to the dataset by file appends (equivalent to incremental updates).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The file append function does not affect the synchronization of data in the file before appending.</div>


<div data-tips="true" data-tips-type="warning">For example:</div>


<div data-tips="true" data-tips-type="warning">When the user does the following:</div>


<div data-tips="true" data-tips-type="warning">April 12: User creates dataset with A file (containing 100 rows of data) and completes first synchronization</div>


<div data-tips="true" data-tips-type="warning">April 13: Users use the file addition function to upload a B file (containing 10 lines of data) and save it before resynchronizing the data</div>


<div data-tips="true" data-tips-type="warning">Then the data for each partition in the system is as follows:</div>


<div data-tips="true" data-tips-type="warning">P_date = 0412:100 lines of data (from A file)</div>


<div data-tips="true" data-tips-type="warning">P_date = 0413:110 lines of data (from file A + file B)</div>


<div data-tips="true" data-tips-type="warning">Users can update additional data to the system by resynchronizing historical data.</div>


<div data-tips="true" data-tips-type="warning">After resynchronizing the data of 0412, P_date = 0412 should contain 110 lines of data (from file A + file B).</div>


**Operation steps**:


1. Go to the "Data Preparation" \- "Data Connection" page and click "Edit" \- "Add File".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4c132e253044db8ba650b40bbe02d1d~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94630d815c3146e9b756d563e0151713~tplv-goo7wpa0wc-image.image) </span>

2. Click "Upload" or "Upload File" and select the local Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c62bcc0b7af4564905754546ad96a96~tplv-goo7wpa0wc-image.image) </span>

3. For successfully uploaded appended data, the system will automatically match the appended field according to the name relationship between the appended field and the original table field. Users can click "Preview" to verify whether the matching relationship is accurate. If there is an error, you can choose to "Resolve", or manually adjust the correspondence between "Append Field" and "Original Table Field". After it is correct, click "OK".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18659c0a1e0d45d0a3e62fd3883cbbac~tplv-goo7wpa0wc-image.image) </span>

4. After saving, the data set created by the extraction method using this data connection needs to be manually synchronized to synchronize the new data to the bottom sheet, and the direct\-connected table does not need to be manually synchronized.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After appending, the downstream extracted dataset/visual modeling will not be available until the next update.   </div>
   

<span id="464cd27e"></span>
## Replace file

Local files (Excel/CSV) do not support updating, but file replacement is supported. Users can update all files by file replacement (equivalent to a full update).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After a file is replaced, the data in the replaced file will stop synchronizing.</div>


<div data-tips="true" data-tips-type="warning">For example:</div>


<div data-tips="true" data-tips-type="warning">When the user does the following:</div>


<div data-tips="true" data-tips-type="warning">April 12: User creates dataset with A file (containing 100 rows of data) and completes first synchronization</div>


<div data-tips="true" data-tips-type="warning">April 13: Users use the file replacement function to upload a B file (containing 10 lines of data) and save it before resynchronizing the data</div>


<div data-tips="true" data-tips-type="warning">Then the data for each partition in the system is as follows:</div>


<div data-tips="true" data-tips-type="warning">P_date = 0412:100 lines of data (from A file)</div>


<div data-tips="true" data-tips-type="warning">P_date = 0413:10 lines of data (from B file)</div>


<div data-tips="true" data-tips-type="warning">Users can update replacement data to the system by resynchronizing historical data.</div>


<div data-tips="true" data-tips-type="warning">After resynchronizing the data of 0412, P_date = 0412 should contain 10 lines of data (from the B file).</div>


**Operation steps** :


1. Go to the "Data Preparation" \- "Data Connection" page and click "Edit" \- "Replace File".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4c132e253044db8ba650b40bbe02d1d~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7e2a642be134a58a5490b05a9a7fce7~tplv-goo7wpa0wc-image.image) </span>

2. Click "Upload" or "Upload File" and select the local Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45e1de006d9248c5a6471973f08edb99~tplv-goo7wpa0wc-image.image) </span>

3. For the successfully uploaded additional data, the system will automatically match the replacement field and the original table field name relationship, and the user can click "Preview" to verify whether the matching relationship is accurate. If there is an error, you can choose to "Resolve", or manually adjust the correspondence between the "Replacement Field" and the "Original Table Field". For new fields in the replacement data, if not required, you can also choose "Clear New Fields". After it is correct, click "OK".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2b79cf12b744e2c889543e99ec8947b~tplv-goo7wpa0wc-image.image) </span>

4. After saving, the data set created by the extraction method using this data connection needs to be manually synchronized to synchronize the new data to the bottom sheet, and the direct\-connected table does not need to be manually synchronized.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the replacement, the downstream extracted dataset/visual modeling will not be available until the next update.   </div>
   

<span id="566cca80"></span>
## Authorization data connection

Click the "Permission Assignment" button in the upper right corner of the data connection to authorize the data connection to be used by other users.

Authorization items include: viewing, editing, and managing. For more information see [Detailed Explanation of User Permissions](https://docs.byteplus.com/docs/undefined/69eafa70cad2c105c48a35cc).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acf8126d3c1e46659903b920ed17128f~tplv-goo7wpa0wc-image.image) </span>

<span id="52fc332e"></span>
## Delete data connection

Click the Delete button on the right side of the data connection to delete the data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07ad70b92c624bb49ad861f6ed176224~tplv-goo7wpa0wc-image.image) </span>
