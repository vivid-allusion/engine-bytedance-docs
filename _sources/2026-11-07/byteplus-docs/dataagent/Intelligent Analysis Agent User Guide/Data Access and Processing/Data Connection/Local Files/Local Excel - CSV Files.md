---
title: "Local Excel/CSV Files"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Local_Excel_CSV_files"
---

This article describes how to upload local Excel/CSV files to create datasets.

<span id="6cff77c4"></span>
# Precautions


* Requirements for the size of uploaded Excel/CSV files:

   * File size limit for uploading via data connection: 500 M

   * File size limit for appending files: 500 M

   * File size limit for replacing files: 500 M

* Requirements for column names in uploaded Excel/CSV files:

   * The column name of the first column cannot be empty (the system only reads columns with consecutive non\-empty column names).

   * Column names must be plain text. They must not start with a digit, consist entirely of digits, must not be images, hyperlinks, formulas, or consist of double underscores (__).

   * Reserved words cannot be used as column names (case\-insensitive): `index`, `constraint`

   * Column names must not be duplicated.

   * Column names should not be excessively long (recommended not to exceed 10 characters).

* Field value requirements: If the field value is in Chinese, it is recommended not to exceed 30 Chinese characters in length.

* File encoding requirement: UTF\-8

* CSV connector support scope: Supports text files and supports specifying delimiters


<span id="d81c4d25"></span>
# Create from data connection


1. Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select the Excel/CSV connection method on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a63e2d0d254da78088ff6fae352251~tplv-goo7wpa0wc-image.image) </span>

3. Select the Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aac3568abd4845e081969777b2d22514~tplv-goo7wpa0wc-image.image) </span>


<span id="1e551944"></span>
# Create from dataset


1. Go to BytePlus, click "Data Preparation" \- "Dataset", select the "Create" button in the upper left corner to create a dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click Excel/CSV.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1032b2db6742451b8e940541c7907c07~tplv-goo7wpa0wc-image.image) </span>

3. Select the Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ba50b6d08f244f1805a06029a7c0824~tplv-goo7wpa0wc-image.image) </span>


<span id="fe20f63d"></span>
# Next steps: Create a dataset


1. Create a dataset using the previously created data connection. Click "Data Preparation" \- "Dataset", select the "Create" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

2. Search for or select from the dropdown the previously created data connection. For more information, please refer to [Overview of Dataset Creation](https://docs.byteplus.com/docs/dataagent/Overview_of_Dataset_Creation).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd1734543b934f5b8ab20e7ed24aa366~tplv-goo7wpa0wc-image.image) </span>


<span id="2646b9d8"></span>
# Other features

<span id="54d0e895"></span>
## View basic information

Hover the mouse over the corresponding data connection to view its detailed information, including name, creator, and creation time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7f88360a1df42a09b942e2b8fce71dc~tplv-goo7wpa0wc-image.image) </span>

<span id="295b54d5"></span>
## Append files

Local files (Excel/CSV) do not support updates, but appending files is supported. Users can manually add new data to the dataset by appending files, which is equivalent to incremental updates.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The file append feature does not affect the synchronization of data in the file before appending.</div>


<div data-tips="true" data-tips-type="warning">For example:</div>


<div data-tips="true" data-tips-type="warning">When the user performs the following operations:</div>


<div data-tips="true" data-tips-type="warning">April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization.</div>


<div data-tips="true" data-tips-type="warning">April 13: The user uploads file B (containing 10 rows of data) using the file append feature, saves it, and resynchronizes the data.</div>


<div data-tips="true" data-tips-type="warning">The data in each partition in the system is as follows:</div>


<div data-tips="true" data-tips-type="warning">P_date=0412: 100 rows of data (from file A)</div>


<div data-tips="true" data-tips-type="warning">P_date=0413: 110 rows of data (from file A + file B)</div>


<div data-tips="true" data-tips-type="warning">The user can update the appended data to the system by resynchronizing historical data.</div>


<div data-tips="true" data-tips-type="warning">After resynchronizing the data for 0412, P_date=0412 should contain 110 rows of data (from file A + file B).</div>


**Operation steps**:


1. Go to the "Data Preparation" \- "Data Connection" page, and click "Edit" \- "Append File".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cb89846f7e64b3bac9a15c09648696f~tplv-goo7wpa0wc-image.image) </span>

2. Click the Append data button.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e71ec63eb8504ec3bf711ff5a5ba33ef~tplv-goo7wpa0wc-image.image) </span>


3. Click "Upload" and select a local Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6acb41ace52440d487506419cbede331~tplv-goo7wpa0wc-image.image) </span>

4. For successfully uploaded appended data, the system will automatically match the appended fields with the original table field names. Users can click "Preview" to verify whether the mapping is accurate. If there are errors, select "Re\-parse", or manually adjust the mapping between "Appended Fields" and "Original Table Fields". If correct, click "OK".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bcb5cc0dfae402e99882766af4e2995~tplv-goo7wpa0wc-image.image) </span>

5. For datasets created using this data connection and the extraction method, manual synchronization is required to sync new data to the base table. Direct connection tables do not require manual synchronization.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After appending, downstream data extraction and visual modeling will obtain the latest data at the next update.   </div>
   

<span id="4d46a806"></span>
## Replace file

Local files (Excel/CSV) do not support updates, but file replacement is supported. Users can update all data by replacing files, which is equivalent to a full update.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After replacing a file, the data within the replaced file will no longer be synchronized.</div>


<div data-tips="true" data-tips-type="warning">For example:</div>


<div data-tips="true" data-tips-type="warning">When the user performs the following operations:</div>


<div data-tips="true" data-tips-type="warning">April 12: The user creates a dataset using file A (containing 100 rows of data) and completes the initial synchronization.</div>


<div data-tips="true" data-tips-type="warning">April 13: The user uploads file B (containing 10 rows of data) using the file replace feature, saves it, and resynchronizes the data.</div>


<div data-tips="true" data-tips-type="warning">The data in each partition in the system is as follows:</div>


<div data-tips="true" data-tips-type="warning">P_date=0412: 100 rows of data (from file A)</div>


<div data-tips="true" data-tips-type="warning">P_date=0413: 10 rows of data (from file B)</div>


<div data-tips="true" data-tips-type="warning">The user can update the replaced data to the system by resynchronizing historical data.</div>


<div data-tips="true" data-tips-type="warning">After resynchronizing the data for 0412, P_date=0412 should contain 10 rows of data (from file B).</div>


**Operation steps**:


1. Go to the "Data Preparation" \- "Data Connection" page, and click "Edit" \- "Replace File".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9645c2d694504a5ea6543275ab446fb7~tplv-goo7wpa0wc-image.image) </span>

2. Click "Upload" or "Upload File", and select a local Excel/CSV file to upload.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6acb41ace52440d487506419cbede331~tplv-goo7wpa0wc-image.image) </span>

3. For successfully uploaded replacement data, the system will automatically match the replacement fields with the original table field names. Users can click "Preview" to verify whether the mapping is accurate. If there are errors, select "Re\-parse", or manually adjust the mapping between "Replacement Fields" and "Original Table Fields". If the newly added fields in the replacement data are not needed, you can also select "Clear New Fields". If correct, click "OK".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bcb5cc0dfae402e99882766af4e2995~tplv-goo7wpa0wc-image.image) </span>

4. For datasets created using this data connection and the extraction method, manual synchronization is required to sync new data to the base table. Direct connection tables do not require manual synchronization.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After replacement, downstream data extraction and visual modeling will obtain the latest data at the next update.   </div>
   

<span id="c4f315a0"></span>
## Authorize data connection

Click the "Assign permissions" button in the upper right corner of the data connection to authorize this data connection for other users to use.

Authorization options include: view, edit, and manage. For more information, see [Detailed Explanation of User Permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e1f0a4a42c340c0abb821ee685cde3a~tplv-goo7wpa0wc-image.image) </span>

<span id="1c4ec511"></span>
## Delete data connection

Click the delete button on the right side of the data connection to delete this data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/318850f821c446f8a8cffa809a48d128~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the prompt displays "This data connection is associated with x downstream datasets that will become unavailable", handle with caution.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcdd20094e66470b96f9d97cd5f8e447~tplv-goo7wpa0wc-image.image" width="1000px" /></div>
