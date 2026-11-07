---
title: "Add project members"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Add_project_members"
---

The primary account should enter the project and add project members like project administrators, developers, operations staff, etc.

<span id="ec4b168b"></span>
## Prerequisites

The users that the primary account needs to add must be sub\-users created on the Access Control platform (IAM users) and must have been granted `FlinkFullAccess` permissions.

<span id="1c4f91c0"></span>
## Operation steps


1. Primary account login to [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left navigation bar, select **Project Management**, then click on the project block to enter the project.

4. In the project's left sidebar, select **Access Control**, click on the **Members** tab, then click on **Add Member**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The user to be added must be a sub\-user created in the access control platform by the main account, and must be granted <code>FlinkFullAccess</code> permissions.   </div>
   

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23916fb7b5f448ef9c789cc695bd8142~tplv-goo7wpa0wc-image.image) </span>


5. In the **Add Member** dialog, enter the IAM user name keyword for a fuzzy search, then select the member and set the associated role, and click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bce58c713c33436ea38b9009919d1719~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Member Name |Enter the IAM user name, conduct a fuzzy search for the user to be added as a project member. |
|Role |From the dropdown list, select the role associated with the project member in order to possess the permissions of that role.<br><br>The project has preset four roles: Project_Admin, Project_Dev, Project_OPS, and Project_Member, which can be directly selected for association; if the existing roles do not meet requirements, you can also create a custom role and bind the relevant permission policy. Please refer to [Role Management](https://docs.byteplus.com/docs/flink/Role_Management).<br><br><br>* Project_Admin: Project Administrator. Mainly responsible for managing project members, roles, and policies, as well as all permissions related to resource pool management.<br><br>* Project_Dev: Task Development Personnel. Possesses the necessary permissions for task development, such as creating, debugging, and deleting tasks.<br><br>* Project_OPS: Task Operations Personnel. Has permissions to start, stop, and deploy tasks online and offline.<br><br>* Project_Member: General Project User. Only has permissions to view tasks, resource pools, and other project resources. |
|Description |Enter a descriptive language for project members. |
