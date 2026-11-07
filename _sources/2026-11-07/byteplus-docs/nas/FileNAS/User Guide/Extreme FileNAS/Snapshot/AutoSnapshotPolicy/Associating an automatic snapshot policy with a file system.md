---
title: "Associating an automatic snapshot policy with a file system"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Associating-an-auto-snapshot-policy-with-a-file-system"
---

This topic describes the steps to set up automatic snapshot policies for file system binding.

<span id="前提条件"></span>
## Prerequisite

Automatic snapshot policy has been created.For specific steps, please refer to [Creating an auto snapshot policy](https://docs.byteplus.com/docs/nas/Creating-an-auto-snapshot-policy).

<span id="注意事项"></span>
## Precautions


* A file system can only be associated with one automatic snapshot policy.

* An automatic snapshot policy can be associated with multiple file systems.

* Only extreme file storage supports the association of automatic snapshot policies.

* After associating with an automatic snapshot policy, only file systems in the **running** state can automatically create snapshots.


<span id="在自动快照策略列表关联"></span>
## Associate automatic snapshot policies on the automatic snapshot policy list


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** page, click **Auto Snapshot Policy** tab.

5. Click **Link to File System** in the target strategy **Actions** column.

6. In the pop\-up panel, select the file system that needs to be associated with an automatic snapshot policy on the **All File** **Systems** tab, and click **Association**.

   After successful association, you can view the automatic snapshot policy associated with the file system through the following methods.

   * In the **Associated with the file system of this policy** tab,you can view the file system associated with the corresponding policy.

   * On the File System **Overview** page, you can view the associated automatic snapshot policies.


<span id="在文件系统列表页面关联"></span>
## Associate automatic snapshot policies on the file system list page


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System** \> **File System List**.

4. Click  **...**  in the target file system **Actions** column and select **Associate Automatic Snapshot Policy**.

5. In the **Associate automatic snapshot policies** dialog box, select the policy name that needs to be associated from the drop\-down list and click **OK**.
