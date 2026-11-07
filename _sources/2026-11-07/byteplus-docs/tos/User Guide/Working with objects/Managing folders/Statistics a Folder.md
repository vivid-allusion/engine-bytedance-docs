---
title: "Statistics a Folder"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Statistics-folder"
---

TOS supports counting the number of objects and the total size of objects in the folder via the console. This article describes precautions and operational steps for counting all objects and the total size of objects in the folder.

<span id="fe2a1ae8"></span>
## Precautions


|**Category** |**Precautions** |
|---|---|
|Object Count |* Supports statistics for up to 1 million objects only. For more objects, please use [Bucket Inventory](https://docs.byteplus.com/docs/tos/Bucket-inventory).<br><br>* When counting objects, symbolic link objects are treated as separate objects and included in the total object count. |
|Total Object Size |When calculating object size, only the original size of objects under the folder will be considered, not the size for billing. |
|Statistic Time |When there are many objects in a folder, it takes some time to complete the statistics. Please be patient. |


<span id="37c475e3"></span>
## Statistical instructions

TOS uses a flat structure to store objects, without the concept of folders. To facilitate classification and management, TOS defaults to display files ending with a slash (/) as folders. In reality, a folder in object storage is an object with 0KB of storage space.

Each object in TOS consists of three parts: Key, Data, and Metadata. When counting objects ending with / and those not, the process involves counting each object's unique identifier (i.e., the object key) to determine the number of objects. If an object with a slash (e.g., data/aaa/bbb.txt) is uploaded as a whole file containing only one key, it is only counted as one object.

<span id="3c60fe86"></span>
## **Procedure**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click ... \> **Number/size of statistical files** in the **Actions** column of the target folder.

4. In the **Number/size of statistical files** dialog, set the statistics items, support for multiple selections, and the description of statistics items is as follows.

   
   |Statistical Items |Description |
   |---|---|
   |Include / end objects |Whether to count objects ending with '/', description as follows:<br><br><br>* Selecting objects ending with "/": Indicates the counting of objects ending with "/", i.e., when counting the number of objects, TOS will count both objects ending with "/" and those not ending with "/".<br><br>* Deselecting objects ending with "/": Indicates not counting objects ending with "/", i.e., when counting the number of objects, TOS will only count objects not ending with "/". |
   |Includes historical versions |Counts historical versions of objects without a deletion mark.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only set the statistical items that <strong>Includes historical versions</strong> when you turn on the Show versions switch in the upper right corner of the file list page.</div><br> |
   |Include delete tag |Counts objects with a deletion mark.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only set the statistical items that <strong>Include delete tag</strong> under the following conditions. First, turn on the <strong>Show versions</strong> switch in the upper right corner of the file list page. And second, select the option to <strong>Includes historical versions</strong>.</div><br> |
   

5. Click **Start counting**.

   In the **Statistical results** area, you can view the total number of objects and the total size of objects in the folder.
