---
title: "Managing permission groups"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing-permission-groups"
---

You can restrict the IP addresses that can access the file system and manage access permissions for different addresses by creating permission group rules. This topic describes the steps to create permission groups and configure permission group rules.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

When you create a file system, the system will automatically create a default permission group that allows access to the file system from all IP addresses. The default permission group cannot be modified or deleted, but you can create permission groups and rules according to your business needs.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* One account supports creating 100 permission groups.

* A permission group can add up to 100 rules.


<span id=".5Yib5bu65p2D6ZmQ57uE5Y-K6KeE5YiZ"></span>
## Create permission groups and rules


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where the target file system is located.

3. Create a permission group.

   1. Select **File System** in the left navigation bar, then click **Permission Group**. On the **Permission Group** page, click **Create Permission Group**.

   2. In the pop\-up dialog box, set the following parameters.

      
      |Parameters |Description |
      |---|---|
      |Name |Customize the name of the permission group, the naming conventions are as follows:<br><br><br>* The length should be between 1 and 128 characters.<br><br>* It should start with uppercase or lowercase letters, or Chinese characters.<br><br>* It can include numbers, underscores (_), or hyphens (\-). |
      |Description |Custom permission group description information, optional, length of 0~120 characters. |
      

   3. After the parameter settings are completed, click **Create**.

4. Add permission group rules.

   1. On the Permission Group page, click **Management rules** corresponding to the target permission group in the **Action** column.

   2. On the **Authorization management rule** page, click **Add rule** and set the rule parameters.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you need to add multiple rules, you can repeat the above steps.      </div>
      

      
      |Parameters |Description |
      |---|---|
      |Authorized address |Set the IP address or network segment that requires authorization. |
      |The permissions of read and write |This rule allows authorized addresses to perform operations on the file system. The optional operations are as follows:<br><br><br>* **read and write**<br><br>* **read only** |
      |Users' permissions |Select the user's access permissions to the file system.<br><br><br>* **Root user retention (no_root_squash)** : Allows the Root user to access the file system.<br><br>* **Root user anonymous (root_squash)** : When accessing the file system as the Root user, it is mapped as an anonymous user by default.<br><br>* **All access users are mapped as anonymous users or user groups (all_squash)** : When accessing the file system with any identity, they will be mapped as anonymous users. |
      

   3. After completing the rule settings, click **Save**.


<span id=".5YW25LuW5pON5L2c"></span>
## Other operations

You can also perform the following actions on the permission group page:


* **View permission group details**: In the **Permission Group** list, click on the target permission group name to view its details.

* **Delete permission group**: In the **Permission Group** list, click **Delete** in the corresponding **Actions** column of the target permission group, and then click **Delete** in the pop\-up dialog box .

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When a permission group is bound to a file system, deletion is not allowed.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Default permission groups are not allowed to be deleted.   </div>
   

* **Edit authorization management rules**: In the **Permission Group** list, click **Management rules** corresponding to the target permission group in the **Actions** column. On the **Authorization management rule** page, modify the rule parameters and click **save**.

* **Delete authorization management rules**: In the **Permission Group** list, click **Management rules** corresponding to the target permission group in the **Actions** column. On the **Authorization management rule** page, click **Delete** corresponding to the target authorization management rule in the **Actions** column, and click **save** in the pop\-up dialog box.
