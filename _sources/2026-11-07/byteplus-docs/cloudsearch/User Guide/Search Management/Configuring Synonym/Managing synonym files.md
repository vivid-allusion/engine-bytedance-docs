---
title: "Managing synonym files"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/uploading-synonym-files"
---

Cloud Search allows you to configure synonyms by uploading synonym files that contain associated words and phrases. This feature enhances query accuracy.

<span id="49ebcaad"></span>
## Background information

Before uploading synonym files, please take note of the following guidelines:


* Synonym files must be in `.txt` format and encoded in `UTF-8`.

* Associated words or phrases in one line are separated by commas (,).

* Maximum of 10 files can be uploaded at a time, and each file should be less than or equal to 5MiB.

* When you upload synonym files, synonym files to be enabled in cold mode must have unique names. When you update a synonym file enabled in hot mode, upload the file with its file name unchanged.

* New synonym files take effect only after the uploaded files are enabled.

* The upload of synonym files affects only the indices and the data created after the upload.


<span id="7b9d916f"></span>
## Uploading a synonym file


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**.

5. On the **File management** panel of **Synonym management** page, click **Add file**.

6. In the dialog box of **Add file**, click or drag the synonym file to upload it, and then click **Close**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b3e5212d1ce44a590f41a520f71e34a~tplv-goo7wpa0wc-image.image) </span>

7. In the displayed dialog box, choose whether to enable the synonym file immediately or not.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/deb8cc2923bd4b68a01e34976d6b75f9~tplv-goo7wpa0wc-image.image) </span>

   * If you want the file to take effect immediately, click **Enable**. The file is automatically enabled in cold mode.

   * If you do not want the file to take effect immediately, click **Cancel**. The file will be saved in the file list but not take effect.


<span id="480a600a"></span>
## Enable a synonym file

The uploaded synonym files need to be enabled to take effect.


1. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**, and then click **File management** tab.

2. In the synonym file list, find the desired file in`to be enabled` status, and then click **Enable** in the **Actions** column.

3. In the dialog box of **Enable file**, click **Enable**.


<span id="3449b5c8"></span>
## Hot Module Replacement

If you want to update an enabled synonym file, you can download the file, modify its content locally, then enable it in hot mode. Enabling a synonym file in hot mode does not trigger the instance to restart. The modified synonym file is uploaded while the instance is running.


1. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**, and then click **File management** tab.

2. In the synonym file list, find the synonym file that you want to update, and then click **Hot Module Replacement** in the **Actions** column.

3. In the displayed dialog box, upload the updated file with the unchanged file name, and then click **Close**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/010b78951f38448b9d57c1e0c03c7a78~tplv-goo7wpa0wc-image.image) </span>

4. In the displayed dialog box, click **OK**.


<span id="36829c69"></span>
## Download a synonym file

The synonym files can be downloaded to view synonym details or update the synonym terms in the file.


1. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**, and then click **File management** tab.

2. In the synonym file list, find the synonym file that you want to download, and click **Download** in the **Actions** column. Then the corresponding file will be downloaded into local directory.


<span id="ca5b3b76"></span>
## Delete a synonym file

Please carefully execute the operation of deleting a synonym file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When deleting a synonym file, please understand the following notes:</div>



* <div data-tips="true" data-tips-type="tip">Please make sure that the terms in the deleted file are not currently used by indices, otherwise the cluster status will be abnormal. If you want to update the term, please use Hot Module Replacement feature.</div>


* <div data-tips="true" data-tips-type="tip">Before deleting the synonym file, please confirm that the relevant indices referencing the file have been removed, otherwise the cluster status will be abnormal.</div>


* <div data-tips="true" data-tips-type="tip">After deleting the file, this operation only takes effect on newly created indices. If you want the historical data in the existing indices to take effect, you can refresh the index data using the data refresh feature. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31990">Refreshing data</a>.</div>


1. On the left navigation bar of **Instance details** page, select **Search management \> Synonym management**, and then click **File management** tab.

2. In the synonym file list, find the synonym file that you want to delete.

3. Click `...` in the **Actions** column, and then click **Delete**.

4. In the displayed dialog box, review the precautions, confirm the file to be deleted, and then click **Delete**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88525e335f634a95b04c5397ced48faa~tplv-goo7wpa0wc-image.image) </span>
