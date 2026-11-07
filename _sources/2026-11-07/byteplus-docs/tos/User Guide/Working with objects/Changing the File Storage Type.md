---
title: "Changing the File Storage Type"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-changing-the-file-storage-type"
---

TOS supports multiple storage types. This topic describes how to change the storage type of a file in the TOS console.

<span id="f92560c8"></span>
## **Note**


|**Category** ||**Note** |
|---|---|---|
|**Versioning** ||* You need to toggle off **Display Version** in the upper\-right corner of the TOS console before you can change the storage type of files.<br><br>* If you enable versioning for a bucket, changing the storage type of a file in the bucket will not permanently delete the file but will instead turn it into a historical version. |
|**File** ||* To change the storage type of a file in the console, make sure the file size is smaller than 5 GiB. |
|**Storage type** ||* Files in a bucket can be in Standard Storage, Intelligent Tiering Storage, Infrequent Access Storage, Flashback Archive, Archive Storage，Cold A rchive or Deep Cold Archive.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Cold Archive storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.   </div><br>   <br><br>* Objects in a multi\-AZ bucket support the following storage classes:Standard Storage (multi\-AZ), Intelligent\-Tiered (multi\-AZ), Infrequent Access (multi\-AZ), and Flashback Archive (multi\-AZ). For more detailed information about multi\-AZ, see [Multi-AZ Redundancy](https://docs.byteplus.com/en/docs/tos/Multi-az-redundancy).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only the Asia Pacific (Johor) regions support the multi\-AZ redundancy feature.   </div><br>    |
|**Billing** |**Infrequent Access Storage** |The minimum duration for Infrequent Access Storage is 30 days,which means a 30\-day fee will be charged even if the storage type is changed before the 30\-day duration ends. For billing details, see[ Storage Fee](https://docs.byteplus.com/en/tos/docs/storage-fee?version=1.0.0). |
||**Flashback Archive** |* Changing the storage type of a file in Flashback Archive incurs a data retrieval fee. For billing details, see [Data Processing Fee](https://docs.byteplus.com/en/tos/docs/data-processing-fee?version=1.0.0).<br><br>* The minimum duration for Flashback Archive is 90 days, which means a 90\-day fee will be charged even if the storage type is changed before the 90\-day duration ends. For billing details, see[ Storage Fee](https://docs.byteplus.com/en/tos/docs/storage-fee?version=1.0.0). |
||**Archive Storage** |* You need to restore files in Archive Storage to readable before transitioning them to another storage type, which incurs a data retrieval fee. For billing details, see [Data Processing Fee](https://docs.byteplus.com/en/tos/docs/data-processing-fee?version=1.0.0).<br><br>* The minimum duration for Archive Storage is 90 days, which means a 90\-day fee will be charged even if the storage type is changed before the 90\-day duration ends. For billing details, see[ Storage Fee](https://docs.byteplus.com/en/tos/docs/storage-fee?version=1.0.0). |
||**Cold Archive** |* Files in Cold Archive must be restored to a readable state before their storage type can be changed, and data retrieval fees will be charged during the restoration. For billing details, see [Data Retrieval Fee](https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee).<br><br>* The minimum storage duration for files in Cold Archive is 180 days. If you change the storage type before the 180\-day period is met, storage capacity fees will be calculated based on a 180\-day period. For billing details, see [Storage Fee](https://docs.byteplus.com/en/tos/docs/storage-fee?version=1.0.0). |
||**Deep Cold Archive** |* Files in Deep Cold Archive must be restored to a readable state before their storage type can be changed, and data retrieval fees will be charged during the restoration. For billing details, see [Data Retrieval Fee](https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee).<br><br>* The minimum storage duration for files in Deep Cold Archive is 180 days. If you change the storage type before the 180\-day period is met, storage capacity fees will be calculated as if the file had been stored for 180 days. For billing details, see [Storage Fee](https://docs.byteplus.com/en/tos/docs/storage-fee?version=1.0.0). |


<span id="465fef0f"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click  **··· \> Change Storage Type** in the **Actions** column of the target object.

4. In the pop\-up dialog box, select the new storage type and click **Save**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information, see <a href="https://docs.byteplus.com/en/tos/docs/storage-type?version=1.0.0">Storage Type</a>.   </div>
