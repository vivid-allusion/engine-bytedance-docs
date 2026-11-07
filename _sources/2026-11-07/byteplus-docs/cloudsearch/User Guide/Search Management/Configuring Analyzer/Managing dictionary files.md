---
title: "Managing dictionary files"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/manage-dictionary-files"
---

This topic describes how to configure analyzer terms by uploading IK dictionary files via front\-end GUI in BytePlus Cloud Search console.

You can configure main words and stop words in local dictionary files and upload the dictionary files to configure IK analysis.

<span id="a6e60564"></span>
## Background information

Before you upload IK analysis files, update files in hot or cold mode, and use the IK analysis features, familiarize yourself with the following basic information.

<span id="e9e0a01e"></span>
### Dictionary file types


* Main dictionary: if IK analysis is used when creating an index, and the data written contains the main term, then the index will be created and can be searched by keyword.

* Stop word dictionary: if IK segmentation is used when creating the index, any data written that contains the stop word, the stop word will be filtered out from the data.



<Tabs>
<Tab zoneid="Za3KbWGFzh" title="Main dictionary">
<TabTitle>Main dictionary</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/160505c52a9240f3b0ec760fca30f6c9~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="DUBMuBbgQy" title="Stop word dictionary">
<TabTitle>Stop word dictionary</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86b62ef41d5a4360af278081cd6a94d5~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


By default, one main dictionary file named `SYSTEM_MAIN.dic` and one stop word dictionary file named `SYSTEM_STOPWORD.dic` are provided by the system. In addition, enabling the analyzer terms configured via GUI will also automatically generate IK dictionary files: namely the main dictionary file `SYSTEM_DICTIONARY_MAIN.dic`, and the stop word dictionary file `SYSTEM_DICTIONARY_STOPWORD.dic`. You can also upload customized dictionary files as needed. All the above dictionary files can be downloaded to your local device to view the analyzer terms.

<span id="3e177e8f"></span>
### Limits on dictionary files

When you upload an IK dictionary file, pay attention to the following points:


* Files must be in`.dic` format and encoded in `UTF-8`.

* Each line can contain only one word.

* Maximum of 10 files can be uploaded at a time, and each file should be less than or equal to 5MiB.

* The newly uploaded dictionary files must have unique names. When you update a dictionary file enabled in cold or hot mode, upload the file with its file name unchanged.

* A file name can contain only uppercase letters, lowercase letters, digits, and three kinds of special characters (i.e. `- _ .`).


<span id="af1f8a75"></span>
### How dictionary files take effect


* After the dictionary file update operation (add, edit, or delete) is completed, it will take effect on the existing and new indices using the updated analyzer terms. It will take about two minutes for the file update to actually take effect.

* For the existing indices, the updated analyzer terms only effective for the newly added data. If you want to apply the updated analyzer terms to the historical data of the existing indices, you can refresh the index data using the data refresh feature. For more information, please see [Refreshing data](https://docs.byteplus.com/docs/cloudsearch/31990).



|**Module** |**Description** |**Dictionary file type** |**Instance restart required** |
|---|---|---|---|
|Enable |A dictionary file uploaded for the first time must be enabled before it can take effect. |Customized dictionary file |No |
|Hot Module Replacement |If you want to update the content of an enabled dictionary file, you can download the file, modify it locally, and then enable it in hot mode. |Customized dictionary file |No |
|Cold update |The default main and stopword dictionary files provided by the system can only be updated in cold mode.<br><br>If you want to update the default dictionary files, you can upload a file with the same name and update it in cold mode. Cold update requires Instance restart to take effect. |System dictionary file |Yes |


<span id="950334f1"></span>
## Uploading dictionary files


1. Log into [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, click the name of the desired instance.

4. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/160505c52a9240f3b0ec760fca30f6c9~tplv-goo7wpa0wc-image.image) </span>

5. On the **Analyzer management** page, you can upload Main dictionary or Stop word dictionary.

   
   <Tabs>
   <Tab zoneid="AqXBJ2AFTX" title="Upload Main dictionary">
   <TabTitle>Upload Main dictionary</TabTitle>
   
      1. On the \*\*\*\* **File management** panel of **Main term** page, click **Add file**.
   
      2. In the displayed dialog box, click or drag the dictionary file to upload it, and then click **Close**.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cd533eea69e49789847d347bc70ed0c~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   <Tab zoneid="myaR13u3C3" title="Upload Stop word dictionary">
   <TabTitle>Upload Stop word dictionary</TabTitle>
   
      1. On the \*\*\*\* **File management** panel of **Stop word** page, click **Add file**.
   
      2. In the displayed dialog box, click or drag the dictionary file to upload it, and then click **Close**.
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfa276e4bbf742dea16df3eda7500277~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   </Tabs>
   

6. In the displayed dialog box, choose whether to enable the dictionary file immediately or not.

   * If you want the file to take effect immediately, click **Enable**. The file is automatically enabled and takes effect.

   * If you do not want the file to take effect immediately, click **Cancel**. The file will be saved in the file list but not take effect.


<span id="f297e1d3"></span>
## **Enable** dictionary **files**

A dictionary file uploaded for the first time must be enabled before it can take effect.


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

3. On the **File management** panel of **Main term** or **Stop word** page, find the desired file in`to be enabled` status, and then click **Enable** in the **Actions** column.

4. In the dialog box of **Enable file**, click **Enable**.


<span id="95071748"></span>
## Hot Module Replacement for customized dictionary

If you want to update the content of an enabled customized dictionary file, you can download the file, modify it locally, and then enable it in hot mode. Enabling a dictionary file in hot mode does not trigger an instance restart. Instead, the system loads the dictionary during its operating process.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The default main and stop word dictionary files provided by the system can only be updated in cold mode. If you want to update the default dictionary files, you can upload a file with the same name and update it in cold mode. Cold update requires Instance restart to take effect.</div>


* <div data-tips="true" data-tips-type="tip">The dictionary files generated from analyzer terms configured via GUI cannot be updated in cold or hot mode. You can directly edit and enable the terms via GUI. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31992#765f5dd6">Edit analyzer terms</a>.</div>


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

3. On the **File management** panel of **Main term** or **Stop word** page, find the desired customized dictionary in`enabled` status from the file list, and then click **Hot Module Replacement** in the **Actions** column.

4. In the displayed dialog box, upload the updated file with the unchanged file name, and then click **Close**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/010b78951f38448b9d57c1e0c03c7a78~tplv-goo7wpa0wc-image.image) </span>

5. In the displayed dialog box, click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cef3ee0f04f4a5d895e80fabb92e41e~tplv-goo7wpa0wc-image.image) </span>


<span id="8171bed0"></span>
## Cold update for system dictionary

The default main and stop word dictionary files provided by the system can only be updated in cold mode. If you want to update the default dictionary files, you can upload a file with the same name and update it in cold mode.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Cold update requires Instance restart to take effect. Please perform cold update operation during off\-peak hours.</div>


* <div data-tips="true" data-tips-type="tip">Please exercise caution with cold update operation for default dictionary files. If you only need to add user\-defined terms, it is recommended to configure analyzer terms via GUI or by uploading a customized dictionary file. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31992#2e12e6c1">Add analyzer terms</a> or <a href="https://docs.byteplus.com/docs/cloudsearch/31988#950334f1">Uploading dictionary files</a>.</div>


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

3. On the **File management** panel of **Main term** or **Stop word** page, find the system default dictionary from the file list, and then click **Cold update** in the **Actions** column.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/116589f39b014e7bb096204d6110759a~tplv-goo7wpa0wc-image.image) </span>


4. In the displayed dialog box, review the precautions, upload the updated file with the unchanged file name, and then click **Close**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a35fc2175b040288f842d4618a71d7b~tplv-goo7wpa0wc-image.image) </span>

5. In the displayed dialog box, click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cef3ee0f04f4a5d895e80fabb92e41e~tplv-goo7wpa0wc-image.image) </span>


<span id="81a55c85"></span>
## Download dictionary file

The dictionary files can be downloaded to view and update the analyzer terms in the file.


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**.

3. On the **File management** panel of **Main term** or **Stop word** page, find the desired dictionary from the file list, and then click **Download** in the **Actions** column. Then the corresponding file will be downloaded into local directory.


<span id="55683d48"></span>
## Delete dictionary file

Only customized dictionary files can be deleted. Please carefully execute the operation of deleting a dictionary file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When deleting a dictionary file, please understand the following notes:</div>



* <div data-tips="true" data-tips-type="tip">Please make sure that the terms in the deleted file are not currently used by indices, otherwise the cluster status will be abnormal. If you want to update the term, please use Hot Module Replacement feature.</div>


* <div data-tips="true" data-tips-type="tip">After deleting the file, this operation only takes effect on newly created indices. If you want the historical data in the existing indices to take effect, you can refresh the index data using the data refresh feature. For more information, please see <a href="https://docs.byteplus.com/docs/cloudsearch/31990">Refreshing data</a>.</div>


1. On the **Instances** page, click the name of the desired instance.

2. On the left navigation bar of **Instance details** page, select **Search management \> Analyzer management**..

3. On the **File management** panel of **Main term** or **Stop word** page, find the desired dictionary from the file list, click `...` in the **Actions** column, and then click **Delete**.

4. In the displayed dialog box, review the precautions, confirm the file to be deleted, and then click **Delete**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a28ab18a162422680872a0737ffdf63~tplv-goo7wpa0wc-image.image) </span>
