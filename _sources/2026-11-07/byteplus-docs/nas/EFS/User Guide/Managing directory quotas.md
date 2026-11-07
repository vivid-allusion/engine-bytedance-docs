---
title: "Managing directory quotas"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Managing_directory_quotas"
---

The directory quota feature tracks and limits file count and storage usage within a specified EFS directory. This topic introduces how to create and view Accounting and Enforcement directory quotas.

<span id="oO3NVJyf"></span>
## Quota type

The directory quota feature offers two types of quotas: Accounting and Enforcement. The details are as follows:


|Type |**Feature description** |
|---|---|
|Accounting |Tracks file count and storage usage in a specified directory within the file system. |
|Enforcement |Combines monitoring and restrictions:<br><br><br>* Tracks file count and storage usage in a specified directory within the file system.<br><br>* Enforces limits on file count and storage usage in a specified directory within the file system.<br><br><br><div data-tips="true" data-tips-type="warning">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Once you reach the limit for either file count or storage usage, you will not be able to write files to the EFS file system. This includes operations such as expanding file size, creating files or directories, and moving files to a specified directory.</div><br> |


<span id="XUQMmVsC"></span>
## Prerequisites

You have mounted the file system and specified the directory path. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_FSX).

<span id="tex2d8v9"></span>
## Notes


|Category |**Description** |
|---|---|
|Directory |* Directory status: Quota can only be set for existing directories on EFS.<br><br>* Number of directories: Each file system can enforce quotas on up to 500 directories, and directory paths cannot exceed eight levels deep.<br><br>* Number of directory quotas: Each directory path can have only one directory quota. |
|Enforcement directory quota |* Latency: The directory quota feature works asynchronously, so activating or deactivating the enforcement quota usually takes 5 to 15 minutes.<br><br>* Risk notice: File writes will be blocked once the enforcement quota is reached. Currently, directory quota over\-limit alerts are not supported. Please assess and configure enforcement quota carefully. |


<span id="RRUyBp9o"></span>
## Accounting directory quota

<span id="zMugHdBz"></span>
### Creating an Accounting directory quota


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Directory quota**.

6. On the **Directory quota** page, click **Create directory quota**.

7. In the **Create directory quota** dialog, enter the **Directory path**. The requirements are as follows:

   * The directory path must start with a forward slash (/).

   * The directory path can only contain letters, numbers, underscores (_), hyphens (\-), or periods (.).

   * Enter an absolute path for the directory path. For example, if the mount target is `/localdir` and the target directory path is `/localdir/aaa`, set the directory path to `/aaa`.

8. Set **Restriction** **Type** to **Accounting**.

9. Click **OK**.


<span id="qnwfpfm1"></span>
### Viewing data statistics results


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Directory quota**.

6. On the **Directory quota** page, view information such as **Restriction** **Type**, **Used capacity**, and **No. of files used**.


<span id="g8cS9Wsy"></span>
## Enforcement directory quota

<span id="hokvPqtC"></span>
### Creating an Enforcement directory quota


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Directory quota**.

6. On the **Directory quota** page, click **Create directory quota**.

7. In the **Create directory quota** dialog, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Directory path |Enter the directory path. The requirements are as follows:<br><br><br>* The directory path must start with a forward slash (/).<br><br>* The directory path can only contain letters, numbers, underscores (_), hyphens (\-), or periods (.).<br><br>* Enter an absolute path for the directory path. For example, if the mount target is `/localdir` and the target directory path is `/localdir/aaa`, set the directory path to `/aaa`. |
   |Restriction Type |Select **Enforcement**. |
   |File count limit |The maximum number of files allowed in the directory. Range: 01–1,000,000,000.<br><br><div data-tips="true" data-tips-type="tip">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">To create an enforcement directory quota, you must specify either <strong>File</strong> <strong>count</strong> <strong>limit</strong> or <strong>Capacity</strong> <strong>limit</strong>. If left blank, the parameter will default to unlimited.</div><br> |
   |Capacity limit |The maximum storage capacity under the directory. Range: 1–10,485,760 GiB. |
   

8. Click **OK**.


<span id="sU6Xklg3"></span>
### Viewing directory limitations and data statistics results


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Directory quota**.

6. On the **Directory quota** page, view information such as **Restriction** **Type**, **Used capacity**, and **No. of files used**.


<span id="Aa0XZOYI"></span>
## Related operations


|Operation |Description |
|---|---|
|Edit quota type |1. On the **Directory quota** page, click **Modify quotas** in the **Actions** column.<br><br>2. In the **modify directory quota** dialog, change the **Restriction** **Type**.<br><br>3. Click **OK**. |
|Edit limits for an enforcement quota |1. On the **Directory quota** page, click **Modify quotas** in the **Actions** column.<br><br>2. In the **modify directory quota** dialog, modify the **File** **count** **limit** or **Capacity** **limit**.<br><br>3. Click **OK**. |
|Delete a directory quota |1. On the **Directory quota** page, click **Delete** in the **Actions** column.<br><br>2. In the **Delete directory quotas** dialog, click **Delete**. |


<span id="NRjGwYej"></span>
## FAQs

<span id="pIjdudxq"></span>
### Failed to create a directory quota


* #### Cause <span id="yx0TcePZ"></span>

   The directory you have created does not exist on EFS, or it already has a directory quota.

* #### Solution <span id="ZmHAtfDy"></span>

   Make sure that the directory exists and that no directory quota has been created for it.


<span id="1XzZfbZu"></span>
### The 'Disk quota exceeded' error occurs when writing data


* #### Cause <span id="8RglP7LO"></span>

   The storage usage or file count within the directory has exceeded the quota limit.

* #### Solution <span id="oKpwlVGm"></span>

   1. Clean up data to free up space or increase the quota limit.

   2. After cleanup, do a test write in the directory to refresh the quota cache asynchronously.

   3. Once it's successful, restart the service.
