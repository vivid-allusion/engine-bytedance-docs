---
title: "Accounts"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Accounts"
---

Once the main account or project administrator adds a sub\-user (IAM user) as a project member, the system automatically synchronizes the project members to the User Management page. The main account can view the projects that the sub\-users have joined, as well as remove users directly from the system.

<span id="457f51ec"></span>
## Function Restrictions

The User Management page is only accessible to the main account; other project members cannot view this page.

<span id="63093d40"></span>
## Prerequisites

When the main account first uses BytePlus Flink, the User Management page will have no user information. Until the main account or project administrator (Project_Admin) adds a sub\-user (IAM user) as a project member, the system will automatically synchronize the project members to the User Management page.

For instructions on how to add project members, please see [Member Management](https://docs.byteplus.com/docs/flink/Member_Management).

<span id="53987597"></span>
## View user list


1. Main account login to [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the navigation bar on the left of the console, select **User Management**.

4. On the **User Management** page, view the user list, and information about the projects users have joined.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4cf0a66fcfb42dca91357768e85e5a2~tplv-goo7wpa0wc-image.image) </span>

<span id="519e1aa3"></span>
## Remove IAM user

If you want to remove an IAM user from the Flink console, transfer the user's tasks and data permissions to another user in advance to prevent inability to operate related tasks.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Removing a user from the system by the main account will also remove the user from the projects they have joined. Please carefully assess the impact of removing users to ensure it does not harm the business.</div>



1. In the user list, filter by user name, click on **Actions** under the **Remove User** column.

2. In the confirmation of removal dialog, check **Understand and proceed**, then click **Delete**.
