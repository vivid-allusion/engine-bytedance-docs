---
title: "Recycle Bin"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Recycle-bin"
---

You can retrieve recently deleted data through the recycle bin feature, enhancing data security. After enabling the recycle bin feature, TOS moves deleted objects and directories to the designated recycle bin folder. Meanwhile, TOS automatically deletes objects and directories in the recycle bin according to the expiration rules.

<span id="oCdtMRsQ"></span>
## Prerequisites

A hierarchical namespace has been created. For detailed steps, refer to [Creating a hierarchical namespace](https://docs.byteplus.com/docs/tos/Create-a-hierarchical-namespaces).

<span id="Rjw7nDP6"></span>
## Notes


|Category ||Details |
|---|---|---|
|Description |Scope of application |Recycle bin functionality is only supported for **hierarchical namespace**. |
||Expiration time |Supports custom expiration time (in days), with a minimum of 1 day. |
||Data recovery method |* Can be manually handled (for example, restored by `rename` operation).<br><br>* Supports restoration via the console's provided restore function. |
|Path management |Default path rule |* The default console path is the `.Trash/` folder under the root directory.<br><br>* Currently, only setting any recycle bin path via API is supported; console setting is not supported. |
||Path creation and risk |After enabling the recycle bin, the system will immediately create the recycle bin directory.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You must avoid deleting the recycle bin directory or its parent directory before creating objects with the same name.</div><br> |
||Recycle bin directory operation risks |The recycle bin directory functions as a regular directory. You can upload or delete content normally, but the following risks exist:<br><br><br>* Deleting objects or empty directories in the recycle bin will permanently remove the data.<br><br>* Non\-empty directories require automatic cleanup and do not support manual permanent deletion.<br><br>* Uploading objects may cause them to be automatically cleared by the recycle bin. |
|Recycle bin path rules |Path length limit |The total length of the recycle bin path plus the actual object/directory path must not exceed 1024 characters, or moving to the recycle bin will fail. |
||Path format |Path format: `Recycle Bin Directory/(yyyymmddHH0000 \| yyyymmddHH3000)/Actual Path`, explained as follows:<br><br><br>* `yyyymmddHH` represents the year, month, day, and hour in the UTC\-0 time zone.<br><br>* `0000` indicates the [0,30) minute interval within one hour, while 3000 indicates the [30,60) minute interval.<br><br><br>Taking an object deleted at 12:00 on January 1, 2025 as an example:<br><br><br>* Objects or directories deleted between [12:00,12:30) enter the `20250101120000` directory.<br><br>* Objects or directories deleted between [12:30,13:00) enter the `20250101123000` directory. |
||Duplicate name conflict handling rules |Avoid conflicts by appending a suffix in the format: `yyyymmddHHMMSS.milliseconds.serial number`<br><br><br>* Composition description:<br><br>   * `yyyymmddHHMMSS`: UTC\-0 timezone timestamp accurate to the second.<br><br>   * `milseconds`: last 3 digits of UTC\-0 timezone millisecond timestamp.<br><br>   * `serial number`: When adding the suffix `yyyymmddHHMMSS.milseconds` to an object or directory name still causes a conflict, a serial number will be added after the existing suffix.<br><br>* Example: `20250101122510.345.1` |
|File overwrite into Recycle Bin |Application scope |Since hierarchical namespaces do not support overwriting directories with the same name, this feature only applies to objects. |
||Restore rules |The function still applies when restoring overwritten objects from the recycle bin. |
||Priority |This feature prioritizes the advanced recycle bin policy:<br><br>\- When the advanced policy does not enable this feature, the object will match the advanced policy whether the default policy enables this feature or not, and the feature will not take effect.<br><br>\- When the advanced policy enables this feature, the object will match the advanced policy whether the default policy enables this feature or not, and the feature will take effect. Existing objects will enter the recycle bin path specified by the advanced policy. |
|Other considerations |Delete operation |After enabling the recycle bin, deleting a non\-empty directory moves the directory and its contents to the recycle bin immediately, but cost reduction takes effect only after the recycle bin is cleared. |
||Lifecycle rule coexistence scenario |* **Delete process**: Lifecycle delete operations first move to the recycle bin and require the recycle bin expiration time before permanent deletion, with total time accumulating.<br><br>* **Path overlap rule**: If lifecycle rules overlap with recycle bin directories, expiration times combine (deletion triggers if any rule is met).<br><br>* **Transfer impact**: Lifecycle rules perform transfer operations on objects in the recycle bin. |


<span id="5GxB8HIz"></span>
## Procedure

<span id="WbEBQBpu"></span>
### Enable recycle bin


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**.

3. On the **Buckets** page, click the target bucket name.

4. In the left navigation bar, click **Recycle Bin**.

5. On the **Basic configurations** area, click **Withdrawn station status**.

6. Click **Edit** in the **Actions** column of the Default policy, and configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Recycling Bin Path |The console defaults to `.Trash/`. After enabling the Recycle Bin, deleted objects are placed in this folder.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The default policy does not support customize recycle bin paths. If you need to customize the recycle bin path, please do so via <strong>Advanced policy \> Create policy</strong>.</div><br> |
   |Cleanup time (days) |Set the retention time in the recycle bin for objects.<br><br>The unit is days, and the value range is 1\-9999, with a default value of 7.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">objects that meet the recycle bin retention period will be permanently deleted.</div><br> |
   |File overwrite into Recycle Bin |When enabled, when an object in the bucket is overwritten, the old object will automatically go to the Recycle Bin.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This feature is currently in closed beta. Please contact your account manager for access.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If this feature is disabled, uploading an object with the same name will directly overwrite the existing object, which may result in data loss. We recommend that you enable this feature.</div><br> |
   

7. After setting the parameters, click **OK**.


<span id="lmqEzmh8"></span>
### Further operations


|Operation |Steps |
|---|---|
|Create advanced policy |1. In the **Withdrawn policy** area, click **Advanced policy**.<br><br>2. Click **Create policy** to set the **Recycling Bin Path**, **Cleaning time (days)** , **File overwrite into Recycle Bin**, and **Matching path**. |
|Batch restore |1. In the **Withdrawn station list**, click the recycle bin name.<br><br>2. Select objects or folders, and click **Batch Restore**, you can restore objects or folders in batches. |
|Permanently delete  |1. In the **Withdrawn station list**, click the recycle bin name.<br><br>2. Select an object or folder, and click **Permanently Delete** in the **Actions** column to permanently delete the object or folder. |
|Count of objects/size |1. In the **Withdrawn station list**, click the recycle bin name.<br><br>2. Select objects or folders, and click **Number/size of statistical objects** in the **Actions** column to count the number of objects/size. |
|Disable recycle bin |If you no longer need the recycle bin feature, you can disable it by clicking **Withdrawn station status** in **Basic configurations ** area. |


<span id="rs00irKx"></span>
### Use recycle bin in the console

After enabling the recycle bin for the hierarchical namespace, you can view the **Recycle Bin Root Path** and **objects in the Recycle Bin** through the special icons on the **Objects** page.

<span id="jIKZnVxR"></span>
#### Recycle bin root path<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46ee79a16186af53592a0e18e4bb962a.png) </span>

<span id="EvDoKEfq"></span>
#### Recycle bin objects<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_06ff9b4fd427ae32b5cdcbcacb9518da.png) </span>

<span id="lKXfegWA"></span>
### Object operations after enabling the recycle bin


|**Action** |**Steps** |**Results** |
|---|---|---|
|Delete |Select an object on the **Objects** page, then click the **Delete** button.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7506614c3a94f122e27f46fb55ccaa5.png) </span><br><br> |Objects will be placed in the Recycle Bin. |
|Permanently delete |Select objects on the **Objects** page and click the **Permanently** **Delete** button.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1fe6ad7cee4cd0d90b68b0f2a667dc35.png) </span><br><br> |Objects will be deleted permanently and will not be placed in the Recycle Bin. |
|Restore |Enter the recycle bin folder from the Objects page, select an object, and click the **Restore** button.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c1726d5c9975196e5b91012c0acb3f3.png) </span> |Objects will be restored to their original path before deletion. Before restoring the object, the original path will be checked for occupancy. If the original path is occupied by an object, use one\-click rename to modify the restore path. |
|Clear recycle bin |Go to the Recycle Bin folder from the Objects page, select objects/folders, and click the ** Permanently Delete** button. |The object will be permanently deleted. |
