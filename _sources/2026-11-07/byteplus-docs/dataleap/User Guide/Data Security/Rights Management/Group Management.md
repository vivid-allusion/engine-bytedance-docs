---
title: "Group Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Group_Management"
---

A user group combines a set of people and a set of resources. When you request resources in bulk, create a user group to manage members and request permissions for the group to improve efficiency. This article introduces how to create and manage user groups.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A many\-to\-many relationship exists among users, user groups, and resources:</div>



* <div data-tips="true" data-tips-type="tip">A user can join multiple user groups, and a user group can include multiple users.</div>


* <div data-tips="true" data-tips-type="tip">A user group can be granted multiple resource permissions, and a resource permission can be assigned to multiple user groups.</div>



<span id="01ba1745"></span>
## Constraints


* User group admins have full operation permissions; non\-admins can only view member details, add resource permissions, and renew resource permissions.

* When the user group type is **Data Development**, resource permissions are open only to the group's admins and developers.

* To manage members in the Data Development user group, go to the **member information** page of the project. See [Manage Member Information](https://docs.byteplus.com/docs/dataleap/manage_project_member) for detailed operations. After the information is set successfully, it takes about 5 minutes to synchronize permissions to the **Data Security** module.

* Renewal is allowed only if the resource permits it and the expiration date is less than 14 days away. The renewal period cannot exceed the duration of the last granted validity period. For a longer period, reapply is required. For explanations on whether resource permissions allow renewal or open application, see [Set Application Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions).


<span id="_1-新建用户组"></span>
## Create a User Group


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Group Management** to enter the group management page.

3. Click the **Create User Group** button to open the **Create User Group** window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b61ae46edadc471583ced88cf68591fd~tplv-goo7wpa0wc-image.image) </span>

4. Set user group information to complete the creation.

   Support creating two types of user groups: Data Security and Data Development.

   * Enter the user group name and description, assign 1 to 2 admins, then click the **OK** button to complete the creation of a Data Security user group.

   * Click **Data Development Project Management** to go to the project management page. Create a project to create a Data Development user group.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Projects created through data development project management can be directly used as data development user groups in the data security platform.      </div>
      

<span id="_2-管理用户组"></span>
## Manage User Groups


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Group Management** to enter the user group management page.

3. View the existing user group list and perform the following management actions:

   * Search for user groups

      Set search criteria to find user groups that match the conditions. When setting multiple search criteria, the intersection of all criteria is used for the query.

      * Enter the group name or description in the search box and click the search icon on the right to view matching user groups.

      * Select a user group type from the type dropdown list to view user groups of that type.

      * Use the **I managed** option to view user groups where you are an admin.

      * Use the **I joined** option to view user groups where you are a member.

      * Use the **All** option to view all user groups where you are either an admin or a member.

   * View details

      Click the **View detail** button in the **Action** column for a user group in the list to enter the details page and view detailed information of that user group.

   * Edit user group

      On a user group details page, click the **Edit** button. In the popped\-up window, the admin can edit the user group information again, such as group name, description, and modify admins.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Data development user groups can only be edited on the <strong>Member information</strong> page of data development project management.      </div>
      

   * Delete User Group

      Click the **Delete** button in the **Action** column of a user group in the list. In the pop\-up **Delete Group** dialog, click the **Delete** button to remove the user group. After deletion, members of the user group will no longer have user group permissions.


<span id="_3-管理用户组明细"></span>
## Manage User Group Details

<span id="_3-1-管理用户组成员"></span>
### Manage User Group Members


1. On the user group management page, click the **View detail** button in the **Action** column of a user group in the list to enter the details page.

2. Click the **Member Details** tab to manage user group members on the member details page.

   * When the user group **Type** is **Data Security**, you can add, delete, or view user group members.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c68bcc030484a76b798fc06d342e0dd~tplv-goo7wpa0wc-image.image) </span>

      * Search Member

         Enter a member name in the search box and click the search icon to the right to view matching information.

      * Add Members

         Click the **Add Member** button. In the pop\-up window, enter keywords to select accounts, then click the **OK** button.

      * Delete single or multiple members

         Click the **Delete** button in the **Action** column for a member in the member list, or select one or more members and click the **Delete Member** button. In the pop\-up dialog, click the **Delete** button to confirm deletion.

   * When the **Type** of the user group is **Data Development**, click **Data Development Project** to go to the **Project Console \> Member information** page to manage user group members.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7753edb0b03e4ebaa338e73854b448df~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">New members automatically obtain the permissions of the user group; removed members no longer have the user group permissions.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The main account, as a member of the data development user group, does not appear in the <strong>Member details</strong>.   </div>
   


<span id="_3-2-管理用户组资源"></span>
### Manage User Group Resources


1. On the user group management page, click the **View detail** button in the **Action** column of a user group in the list to enter the details page.

2. Click the **Resource Details** tab to enter the resource details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71cf34f5b9ea4856b64f93f099c89ca8~tplv-goo7wpa0wc-image.image) </span>

3. The following user group resource management actions can be performed:

   * Search Resources

      Set search criteria to view user group resource information that matches the conditions. When setting multiple search criteria, the query uses the intersection of all conditions.

   * Renew a single resource or renew in batches

      Click the **Renew** button in the **Action** column for a resource in the resource list, or select one or more options and then click the **Batch Renew** button. In the pop\-up window, set the renewal information and click the **OK** button.

   * Add Permissions

      Click the **Add Permissions** button to enter the **Apply** page, where you can request resource permissions for the user group.

   * Return permissions individually or in batch

      1. Click the **Return** button in the **Action** column for a resource in the resource list, or select one or more options and click the **Batch Return** button to open the corresponding permission return window.

      2. After setting return information, click the **OK** button, and a return confirmation dialog appears.

      3. Click the **OK** button to complete the permission return.


<span id="_4-相关消息通知说明"></span>
## Related Message Notifications Description


* administrators receive email alerts in the following scenarios:

   * user group name or description modified

   * added or removed as administrator

   * resource about to expire

* user group members receive email alerts in the following scenarios:

   * user group deleted (notify all members)

   * user group permissions revoked or returned (notify all members)

   * added or removed from user group (notify affected members)

   * resource about to expire (notify requester or active authorizer)
