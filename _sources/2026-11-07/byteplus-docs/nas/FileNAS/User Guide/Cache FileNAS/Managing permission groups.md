---
title: "Managing permission groups"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_permission_groups"
---

You can set permission group rules to limit file system access by IP address and control permissions for different addresses. This topic explains how to create a permission group and set its rules.

<span id="1b8dc975"></span>
## Background information

When you create a file system, a default permission group is automatically configured with open access from all IP addresses. The default permission group cannot be changed or removed, but you can create new permission groups and rules as needed.

<span id="7m3VpH1E"></span>
## Notes


* You can create up to 20 permission groups per file system type in one region.

* You can add up to 300 rules to a permission group.


<span id="c2789a69"></span>
## Creating permission groups


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **Permission groups**.

4. On the **Permission groups** page, go to the **Cache FileNAS** tab, and click **Create permission group**.

5. Set the following parameters in the dialog box.

   
   |**Parameters** |**Description** |
   |---|---|
   |Name |Enter the name of the permission group. Naming rules:<br><br><br>* Length must be between 1 and 128 characters.<br><br>* Start with uppercase or lowercase letters or Chinese characters, and can contain numbers, underscores (_), or hyphens (\-). |
   |Description |Provide additional information about the permission group. This is optional and can be any length from 0 to 120 characters. |
   

6. After completing the settings, click **Create**.


<span id="d4ffa51d"></span>
## Adding rules to the permission group


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **Permission groups**.

4. On the **Permission groups** page, click the **Cache FileNAS** tab.

5. On the **Permission groups** page, click **Manage rules** in the **Actions** column of the target permission group.

6. On the **Authorization management rule** page, click **Add rules** to set the rule parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To add additional rules, repeat the above steps.   </div>
   

   
   |**Parameters** |**Description** |
   |---|---|
   |Authorized address |Specify IP addresses or CIDR blocks that require access authorization. |
   |The permissions of read and write |Specify which actions authorized addresses can perform on the file system under this rule:<br><br><br>* **Read and write**<br><br>* **Read only** |
   |Users' permissions |Manage file system access permissions.<br><br><br>* **Root user retention (no_root_squash**): Allows root users to access the file system.<br><br>* **Root user anonymous (root_squash)** : Maps root users accessing the file system to anonymous users by default.<br><br>* **All visiting users are mapped to anonymous user or user groups (all_squash)** : Maps any user accessing the file system to anonymous users. |
   

7. After completing the settings, click **Save**.


<span id="903df3d5"></span>
## **Other actions** 

You can also perform these actions on the **Permission groups** page:


|**Actions** |**Description** |
|---|---|
|View permission group details |Click the target permission group in the **Permission groups** list to view details. |
|Delete permission groups |In the **Permission groups** list, click **Delete** in the **Actions** column of the target permission group. In the dialog box, click **Delete** to confirm.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Deletion is not permitted when the permission group is bound to a file system.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Default permission groups cannot be deleted.</div><br> |
|Edit authorization management rules |In the **Permission groups** list, click **Manage rules** in the **Actions** column of the target permission group. Navigate to the **Authorization management rule** page, modify the rule parameters, and click **Save**. |
|Delete authorization management rules |In the **Permission groups** list, click **Manage rules** in the **Actions** column of the target permission group. Navigate to the **Authorization management rule** page, click **Delete** in the **Actions** column of the target rule, and click **Save**. |
