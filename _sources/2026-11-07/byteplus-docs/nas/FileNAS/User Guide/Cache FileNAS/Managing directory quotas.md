---
title: "Managing directory quotas"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_directory_quotas"
---

The directory quota feature tracks and limits file count and storage usage within a specified Cache FileNAS directory. This topic introduces how to create and view statistical and restricted directory quotas.

<span id="b46abc65"></span>
## Quota type 

The directory quota feature offers two types of quotas: statistical and restricted. The details are as follows:


|**Category** |**Feature description** |
|---|---|
|Statistical |Tracks file count and storage usage in a specified directory within the file system. |
|Restricted |Combines monitoring and restrictions:<br><br><br>* Tracks file count and storage usage in a specified directory within the file system.<br><br>* Enforces limits on file count and storage usage in a specified directory within the file system.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once you reach the limit for either file count or storage usage, you won't be able to write files to the FileNAS file system. This includes operations such as expanding file size, creating files or directories, and moving files to a specified directory.</div><br> |


<span id="5e392ae9"></span>
## Prerequisites 

You have mounted the file system and specified the directory path. 

<span id="f321bfa6"></span>
## Notes


|**Category** |**Description** |
|---|---|
|Directory |* Directory status<br><br>   Quota can only be set for existing directories on Cache FileNAS.<br><br>* Number of directories<br><br>   Each file system can enforce quotas on up to 500 directories, and directory paths cannot exceed eight levels deep.<br><br>* Number of directory quotas<br><br>   Each directory path can have only one directory quota. |
|Restricted directory quota |* Latency<br><br>   The directory quota feature works asynchronously, so activating or deactivating the restricted quota usually takes 5 to 15 minutes.<br><br>* Risk notice<br><br>   File writes will be blocked once the restricted quota is reached. Currently, directory quota over\-limit alerts are not supported. Please assess and configure restricted quotas carefully. |


<span id="ffdbc59a"></span>
## Statistical directory quota

<span id="dcccfa52"></span>
### **Creating a statistical directory quota**


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. On the file system details page, click the **Directory quota** tab, and then click **Create directory quota.** 

6. In the **Create directory quota** dialog, enter the directory path and click **Confirm**.

   The system established these directory quotas as statistical quotas by default, which eliminates the need for type configuration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enter an absolute path for the directory path. For example, if the mount target is <code>/localdir</code> and the target directory path is <code>/localdir/aaa</code>, set the directory path to <code>/aaa</code>.   </div>
   

<span id="7aa4b5dd"></span>
### **Viewing data statistics results**


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. On the file system details page, click the **Directory quota** tab.

6. Click **Quota management** under the **Actions** column of the target directory path.

7. In the **Manage quota** panel, view information such as **Quota type**, **Current capacity**, and **Current No. of files**.


<span id="ec5b9ecb"></span>
## Restricted directory quota

<span id="b871d10b"></span>
### **Creating a restricted directory quota**


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the target file system.

5. Create a directory quota on the file system details page.

   1. Click the **Directory quota** tab, and then click **Create directory quota**.

   2. In the **Create directory quota** dialog, enter the directory path and click **Confirm**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Enter an absolute path for the directory path. For example, if the mount target is <code>/localdir</code> and the target directory path is <code>/localdir/aaa</code>, set the directory path to <code>/aaa</code>.      </div>
      

6. Set the directory quota type to restricted.

   1. On the **Directory quota** tab, click **Quota management** under the **Actions** column of the target directory path.

   2. In the **Manage quota** panel, click **Edit** under the **Actions** column.

   3. In the **Edit user quota** dialog, set **Quota type** to **Restricted**, and configure **File amount limitation** and **Capacity constraints**.

      
      |**Parameters** |**Description** |
      |---|---|
      |File System ID |Displays the ID of the file system to which the directory quota belongs. |
      |Directory path |Displays the configured directory path. |
      |User type |Currently, directory quotas can only be configured for all users and user\-specific quotas are not supported. |
      |Quota type |Select **Restricted**. |
      |File amount limitation |The maximum number of files allowed in the target directory. Range: 1 \- 1,000,000,000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To create a restricted directory quota, you must specify either <strong>File amount limitation</strong> or <strong>Capacity constraints</strong>. If left blank, the parameter will default to unlimited.</div><br> |
      |Capacity constraints |The maximum storage capacity under the target directory. Range: 1 \- 10,000,000 GiB. |
      

   4. After completing the settings, click **OK**.


<span id="be4ebb86"></span>
### **Viewing directory limitations**


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, select **File System \> File System list**. On the **File System list** page, click the target file system.

4. On the file system details page, click the **Directory quota** tab.

5. Click **Quota management** under the **Actions** column of the target directory path.

6. In the **Manage quota** panel, view information such as **Quota type**, **Capacity limitations**, and **File amount limitation**.


<span id="2e32c63e"></span>
## Related actions


* Edit quota type

   Go to the file system details page, and click the **Directory quota** tab. Click **Quota management** under the **Actions** column of the target directory path, and then click **Edit** under the **Actions** column. In the **Edit user quota** dialog, modify the quota type, complete the settings, and click **OK**.

* Edit limits for a restricted quota

   Go to the file system details page, and click the **Directory quota** tab. Click **Quota management** under the **Actions** column of the target directory path, and then click **Edit** under the **Actions** column. In the **Edit user quota** dialog, configure **File amount limitation** and **Capacity constraints**, and click **OK**.

* Delete a directory quota

   Go to the file system details page, and click the **Directory quota** tab. Click **Quota management** under the **Actions** column of the target directory path, and then click **Delete** under the **Actions** column. In the **Delete Quota** dialog, click **Delete**.


<span id="59c3824d"></span>
## FAQs


* Failed to create a directory quota

   The directory you have created does not exist on FileNAS, or it already has a directory quota. Verify that the target directory exists on FileNAS. Make sure that no directory quota has been created for it. Next, retry creating a directory quota.

* `Disk quota exceeded` when writing data

   The storage usage or file count in the target directory has exceeded the quota limit. Please clean up data to free up space or increase the quota limit. After cleanup, do a test write in the target directory to refresh the quota cache asynchronously. Once it's successful, restart the service.
