---
title: "Authorize by User"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/authorize-by-user"
---

**Permission Management \-**  \*\*Authorize by User \*\*is used to configure permissions by user dimension. After selecting a user on the left, the administrator can configure the object's functional permissions and resource visibility on the right. The page is divided into two parts:

* **Left user list:**  Used to switch users or roles, and supports fuzzy search by username, account name, or role name.

* **Right permission configuration area:**  used to view the current user information, and configure function permissions, visible range of resources.

Function permissions are divided into **view, edit, manage** three levels, the hierarchy of permissions is: view < edit < manage.

|Permission level |Permission description |Inclusion relation |
|---|---|---|
|View |You can enter the function page, but the page configuration items cannot be edited. |without |
|Edit |On the basis of viewing, you can create, modify, publish/take offline, but can not delete. |Include view |
|Manage |On the basis of editing, you can delete, transfer ownership, and assign permissions to other users. |Includes edit and view |

# Notes/Prerequisites

1. **Confirm the authorization object:**  Check the user name, user ID and account number of the target user before operation to avoid false authorization.

2. **Confirm the scope of authorization:**  The current account can only configure items with manage permissions; "Cancel all authorization" and "Open all view permissions" only apply to this scope.

3. **Note that permissions are automatically adjusted:**  when checking Edit or Manage, the system will automatically check lower\-level permissions; when canceling View or Edit, higher\-level permissions will be automatically cancelled. Administrative permissions include delete, transfer ownership, and allocation of permissions. Please grant them according to actual responsibilities.

# Operating instructions

## Enter the page and select the user

1. Log in to the BytePlus console, select iDA to enter iDA, click the currently displayed user name in the lower left corner of the iDA interface, and select **Setting \> Permission Management \> Authorize by User**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67ac3f13ef3d40bc90b189091983eea1~tplv-goo7wpa0wc-image.image)

2. After entering the page, confirm that the left side is the user list and the right side is the permission configuration area.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59fd2d5c285a4ef0ae76fffcf29368ea~tplv-goo7wpa0wc-image.image)

## Configure user feature permissions

1. Enter your username, account name, or role name in the search box on the left to search.

2. Click on the target user or role in the search results, and check the user name, user ID, and account number on the right to confirm that it is correct before starting the configuration.

3. View the function permission table, the table is listed as **module, view, edit, manage**. To configure child functions, click the Expand button in front of the parent module. Locate the target module or child function. Tick permissions according to your needs:

   * Only allow **viewing** pages: Check **View**.

   * Allow **viewing, creating and editing**, not deleting: check **Edit**.

   * Allow **viewing, creating, editing and deleting**, and authorize others: Check **Manage**.

4. System permission association result:

   * After checking **Edit**, View will also be automatically checked.

   * Once **Manage** is checked, **Edit and View** will also be checked automatically.

5. If you need to withdraw the permission, cancel the corresponding permission:

   * When you cancel **view**, **edit and manage** permission are also automatically cancelled.

   * After canceling the **edit**, **manage** permission \*\*\*\* is also automatically canceled.

> **说明**

> To operate all functions, click the Select All button above the "Feature Permissions List".

# Common problem

|Common problem |Processing method |
|---|---|
|The function or resource checkbox cannot be clicked. |The current operation account does not have the management authority of the corresponding function or resource, so you need to contact the administrator with the authority to configure it. |
|After checking Edit, View permission automatically checked. |This is a permission association rule, and edit permission includes view permission. |
|Edit and Manage permissions disappeared after canceling View permission. |This is a permission association rule. Canceling lower\-level permissions results automatically canceling higher\-level permissions. |
|Users can view resources but cannot edit them. |Check whether the account has edit permission of the corresponding function; the view permission of resource only controls whether the resource is viewable. |
|After canceling all authorizations, there are still permissions remaining. |Residual permissions may belong to functions that the current operating account does not have manage permissions. And the corresponding administrator needs to be contacted to deal with them. |
