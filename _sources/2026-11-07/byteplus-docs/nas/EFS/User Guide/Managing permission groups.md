---
title: "Managing permission groups"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Managing_permission_groups"
---

To ensure data security, you can use permission groups to limit file system access by IP address and control permissions for different addresses. This topic explains how to create permission groups and perform related operations.

<span id="UqxBJtxh"></span>
## Background information


* When you create a file system, the console establishes a **default permission group** that grants access to the file system for any IP address within the same VPC.

* The default permission group cannot be changed or removed, but you can create new permission groups and rules based on your business needs.


<span id="Z9r5RW0g"></span>
## Notes


* You can create up to 100 permission groups per file system type in one region.

* A permission group can have up to 100 rules.


<span id="qsOvEnI4"></span>
## Creating a permission group


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **Permission groups**.

4. On the **Permission group list** page, click **Create permission group**.

5. In the **Create permission group** dialog, configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Permission group name |Set the name of the permission group. Naming rules:<br><br><br>* The permission group name must start with Chinese characters or English letters.<br><br>* The permission group name can only contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Length must be between 1 and 128 characters. |
   |Description |Provide additional information about the permission group to help you identify it later. Descriptions must:<br><br><br>* Start with Chinese characters, letters, or numbers.<br><br>* Contain only Chinese characters, letters, numbers, spaces, periods (.), underscores (_), hyphens (\-), equal signs (=) and English commas (,), Chinese commas, enumaration commas, or Chinese periods.<br><br>* Be between 0 and 255 characters long. |
   

6. Click **OK**.


<span id="u5ZJcGMS"></span>
## Configuring permission group rules


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the permission group you want to configure.

3. In the left navigation pane, select **Permission groups**.

4. On the **Permission group list** page, click **Manage rules** in the **Actions** column of the permission group.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Alternatively, click the name of the permission group, which will take you to the <strong>Permission Rule</strong> tab.   </div>
   

5. On the **Permission Rule** tab, click **Add rules**.

6. On the **Authorization management rule** page, configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Authorized address |Specify IP addresses or CIDR blocks that require access authorization. |
   |The permissions of read and write |Specify which actions authorized addresses can perform on the file system under this rule:<br><br><br>* **Read only**<br><br>* **Read and write** |
   |Users' permissions |Select the permissions for users accessing the file system:<br><br><br>* **Root user retention (no_root_squash)** : Allows root users to access the file system.<br><br>* **Root user anonymous (root_squash)** : Maps root users accessing the file system to anonymous users by default.<br><br>* **All visiting users are mapped to anonymous user or user groups (all_squash)** : Maps any user accessing the file system to anonymous users. |
   

7. Click **Save**.


<span id="kWX26fJS"></span>
## Related operations


|Operation |Description |
|---|---|
|View permission group details |You can view the details of a permission group on the **Permission group list** page. These details include **Permission group name/ID**, **State**, **No.of rules**, and **Creation time**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Click the name of the permission group to view its rules on the Permission Rule tab.</div><br> |
|Edit permission group information |Both **Permission group name** and **Description** are editable. Steps:<br><br><br>1. On the **Permission group list** page, click the edit icon that appears next to the name or description of the permission group.<br><br>2. In the box that appears, modify the information of the permission group.<br><br>3. Click **OK**. |
|Edit permission group rules |You can modify permission group rules. Steps:<br><br><br>1. On the **Permission group list** page, click **Manage rules** in the **Actions** column of the permission group.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Alternatively, click the name of the permission group, which will take you to the <strong>Permission Rule</strong> tab.   </div><br>   <br><br>2. On the **Permission Rule** tab, modify the rule based on your needs.<br><br>3. Click **Save** in the **Actions** column of the rule. |
|Delete permission group rules |You can delete permission group rules. Steps:<br><br><br>1. On the **Permission group list** page, click **Manage rules** in the **Actions** column of the permission group.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Alternatively, click the name of the permission group, which will take you to the <strong>Permission Rule</strong> tab.   </div><br>   <br><br>2. Click **Delete** in the **Actions** column of the rule you want to remove. |
|Delete permission groups |You can delete permission groups. Steps:<br><br><br>1. On the **Permission group list** page, click **Delete** in the **Actions** column of the permission group you want to remove.<br><br>2. In the box that appears, click **OK**. |
