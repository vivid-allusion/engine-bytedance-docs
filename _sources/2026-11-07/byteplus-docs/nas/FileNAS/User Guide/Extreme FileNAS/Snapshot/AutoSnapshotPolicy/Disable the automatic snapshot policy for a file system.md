---
title: "Disable the automatic snapshot policy for a file system"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Disable-the-auto-snapshot-policy-for-a-file-system"
---

When the file system does not need to create automatic snapshots, you can remove the automatic snapshot policy for the instance to avoid using up the snapshot quota.

<span id=".5Zyo5paH5Lu257O757uf5YiX6KGo6aG16Z2i6Kej57uR"></span>
## Unbind automatic snapshot policy on the file system list page


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System** \> **File System List**.

4. Click  **...**  \> **Unbind Auto Snapshot Policy** in the target file system **Actions** column.

5. Click **OK** in the **Unbind the automatic snapshot policy** dialog box.


<span id=".5Zyo6Ieq5Yqo5b-r54Wn562W55Wl5YiX6KGo56e76Zmk"></span>
## Unbind the automatic snapshot policy on the automatic snapshot policy list


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the Snapshot page, click **Auto Snapshot Policy** tab.

5. Click **Link to File System** in the target strategy **Actions** column.

6. In the pop\-up panel, click **Associated with the file system of this policy ** tab, check the file system that needs to remove the automatic snapshot policy, and click **Remove**.

7. Click **OK** in the pop\-up dialog box.
