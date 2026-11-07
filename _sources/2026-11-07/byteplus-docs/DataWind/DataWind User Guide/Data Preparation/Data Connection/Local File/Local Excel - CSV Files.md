---
title: "Local Excel/CSV Files"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Local_Excel_CSV_Files"
---

This article describes how to upload local Excel/CSV files to create datasets.

<span id="13513e37"></span>
# Precautions


* File upload size requirements:

   * Data connection upload file size limit: 500 M

   * Append file size limit: 500 M

   * Replace file size limit: 500 M

* Column name requirements:

   * The first column name cannot be empty (the system only reads columns with consecutive non\-empty column names; it stops reading at the first empty column name).

   * Column names must be plain text. They cannot start with a number, be entirely numeric, be an image, a hyperlink, contain a formula, or consist only of double underscores (__).

   * Reserved words cannot be used as column names (case\-insensitive): `index`, `constraint`

   * Column names must be unique.

   * Column names should not be too long (recommended not to exceed 10 characters).

* Field value requirements: If the field value is in Chinese, it is recommended that the length not exceed 30 Chinese characters.

* File encoding requirement: UTF\-8

* CSV connector support scope: supports text files and supports specifying delimiters.


<span id="d2be010f"></span>
# Create from data connection


1. Go to Volcano Engine, select a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select the Excel/CSV connection method on the page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02dfaa453cff476e84912df50aa5d311~tplv-goo7wpa0wc-image.image) </span>


3. Select the Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf22068e6e6d4638b5975ea67c405b56~tplv-goo7wpa0wc-image.image) </span>


<span id="62d41bb1"></span>
# Create from dataset


1. Go to Volcano Engine, click "Data Preparation" \- "Dataset", select the "Create" button in the upper left corner to create a new dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image) </span>


2. When selecting a data connection, click Excel/CSV.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/baab1b6ce125434992e80d6ad7a095af~tplv-goo7wpa0wc-image.image) </span>

3. Select the Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/687916df96094d2abafefbd587c7093c~tplv-goo7wpa0wc-image.image) </span>


<span id="6cb3b9a7"></span>
# Next steps: Create a dataset


1. Create a dataset using the previously created data connection. Click "Data Preparation" \- "Dataset", and select the "Create" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image) </span>

2. Search for or select from the drop\-down list the previously created data connection. For more information, see [Dataset Creation Overview](https://docs.byteplus.com/docs/DataWind/109998).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/baab1b6ce125434992e80d6ad7a095af~tplv-goo7wpa0wc-image.image) </span>


<span id="b8a8e200"></span>
# Other features

<span id="1a41f008"></span>
## View basic information

Hover the mouse over the corresponding data connection to view detailed information about the data connection, including the name, creator, and creation time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9259e4d2918e44b9a02cf9e5a9621b18~tplv-goo7wpa0wc-image.image) </span>

<span id="dced972f"></span>
## Append file

Local files (Excel/CSV) do not support updates, but file appending is supported. Users can manually add new data to the dataset by appending files (equivalent to incremental updates).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The file append feature does not affect the synchronization of data that existed in the file before the append operation.</div>


<div data-tips="true" data-tips-type="warning">For example:</div>


<div data-tips="true" data-tips-type="warning">When the user performs the following operations:</div>


<div data-tips="true" data-tips-type="warning">April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization.</div>


<div data-tips="true" data-tips-type="warning">April 13: The user uploads file B (containing 10 rows of data) using the file append feature, saves it, and then re\-synchronizes the data.</div>


<div data-tips="true" data-tips-type="warning">The data in each partition in the system is as follows:</div>


<div data-tips="true" data-tips-type="warning">P_date=0412: 100 rows of data (from file A)</div>


<div data-tips="true" data-tips-type="warning">P_date=0413: 110 rows of data (from file A + file B)</div>


<div data-tips="true" data-tips-type="warning">The user can update the appended data to the system by re\-synchronizing historical data.</div>


<div data-tips="true" data-tips-type="warning">After re\-synchronizing the data for 0412, P_date=0412 should contain 110 rows of data (from file A + file B).</div>


**Operation steps**:


1. Go to the "Data Preparation" \- "Data Connection" page, and click "Edit" \- "Append File".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20640c51fc614c1e88c539250e83ea55~tplv-goo7wpa0wc-image.image) </span>

2. Click "Upload" or "Upload File", and select a local Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85c5c4f476b64f3aa76d2f3972cb4816~tplv-goo7wpa0wc-image.image) </span>

3. For successfully uploaded appended data, the system will automatically match the appended fields with the original table field names. Users can click "Preview" to verify whether the fields are matched correctly. If there are errors, select "Re\-parse", or manually adjust the mapping between "Appended Fields" and "Original Table Fields". If correct, click "OK".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e371360e9b24b039d402b3be03f1777~tplv-goo7wpa0wc-image.image) </span>

4. After saving, for datasets created using this data connection and the extraction method, manual synchronization is required to sync the new data to the base table. For direct tables, manual synchronization is not required.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After appending, downstream data extraction datasets and visual modeling can only obtain the latest data during the next update.   </div>
   

<span id="af8342da"></span>
## Replace file

Local files (Excel/CSV) do not support updates, but file replacement is supported. Users can update all files by replacing files (equivalent to a full update).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After replacing a file, the data in the replaced file will stop synchronizing.</div>


<div data-tips="true" data-tips-type="warning">For example:</div>


<div data-tips="true" data-tips-type="warning">When the user performs the following operations:</div>


<div data-tips="true" data-tips-type="warning">April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization.</div>


<div data-tips="true" data-tips-type="warning">April 13: The user uploads file B (containing 10 rows of data) using the file replace feature, saves it, and then re\-synchronizes the data.</div>


<div data-tips="true" data-tips-type="warning">The data in each partition in the system is as follows:</div>


<div data-tips="true" data-tips-type="warning">P_date=0412: 100 rows of data (from file A)</div>


<div data-tips="true" data-tips-type="warning">P_date=0413: 10 rows of data (from file B)</div>


<div data-tips="true" data-tips-type="warning">The user can update the replaced data to the system by re\-synchronizing historical data.</div>


<div data-tips="true" data-tips-type="warning">After re\-synchronizing the data for 0412, P_date=0412 should contain 10 rows of data (from file B).</div>


**Operation steps**:


1. Go to the "Data Preparation" \- "Data Connection" page, and click "Edit" \- "Replace File".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63ba0f556d7a4c0fa6eb2f67889665d2~tplv-goo7wpa0wc-image.image) </span>

2. Click "Upload" or "Upload File", and select a local Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc53c3d0abab4db89b8513f006966ce8~tplv-goo7wpa0wc-image.image) </span>

3. For successfully uploaded replacement data, the system will automatically match the replacement fields with the original table field names. Users can click "Preview" to verify whether the fields are matched correctly. If there are errors, select "Re\-parse", or manually adjust the mapping between "Replacement Fields" and "Original Table Fields". If the newly added fields in the replacement data are not needed, you can select "Clear New Fields". If correct, click "OK".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf2a47c4f54e45498e397baeb13f83a4~tplv-goo7wpa0wc-image.image) </span>

4. After saving, for datasets created using this data connection and the extraction method, manual synchronization is required to sync the new data to the base table. For direct tables, manual synchronization is not required.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After replacement, downstream data extraction datasets and visual modeling can only obtain the latest data during the next update.   </div>
   

<span id="e72401f8"></span>
## Authorize data connection

Click the "Permission assignment" button in the upper right corner of the data connection to grant other users access to this data connection.

The available permissions include: view, edit, and manage. For more information, see [Detailed explanation of permission functions](https://docs.byteplus.com/docs/undefined/670796878c66ba0323ada03f).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e97227be9d094e6daf99b4bb48d6cf7e~tplv-goo7wpa0wc-image.image) </span>

<span id="ee62f639"></span>
## Delete a data connection

Click the delete button on the right side of the data connection to delete this data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3141d478754844e8b410df5e4a0070a7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the prompt displays "This data connection is associated with x downstream datasets that will become unavailable", proceed with caution.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c153123a2baa4d499b79cf7e13e679d2~tplv-goo7wpa0wc-image.image" width="1898px" /></div>
