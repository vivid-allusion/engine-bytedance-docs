---
title: "Manage Member Information"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/manage_project_member"
---

This article provides a detailed introduction on how to manage members in a project and their corresponding permissions.

<span id="_1-约束限制"></span>
## Constraints


* Only Project Administrators can manage member information.

* The main tenant account as the project owner cannot be removed from the project, and is by the administrator role which cannot be revoked.

* After successfully setting the member information, it takes approximately 5 minutes to synchronize permissions to **Data Security**.


<span id="8ab1ae2a"></span>
## Prerequisites

A project has been created.

<span id="_2-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap Console.

2. Click on **Projects** in the left navigation bar to enter the **Project Management** page.

3. Check the **My managed projects** option to display the list of projects you manage.

4. Click the **Members** button in the **Action** column of a project in the list to enter the **Members** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f25d95b5ce854074a4b213ff91f6164f~tplv-goo7wpa0wc-image.image) </span>

5. You can manage project members in the following ways:

   * Add members

      Click the **Add Members** button, and in the **Add Members** window that pops up, choose the username and role, then click the **OK** button to complete the addition.

      The parameters related to adding members are as described in the following table. Parameters marked with an \* are required, while those not marked with \* are optional.

      
      |Parameters |Description |
      |---|---|
      |\*Username |The user name to be added as a project member; drop\-down to choose from all accounts under the tenant, supporting entering account keywords to filter options. |
      |Role Type |Users in the project can have multiple roles.<br><br>The following are the role types of project members and their corresponding permissions:<br><br><br>* Admin: Can view and edit all tasks within the project, can edit project configuration and member management, and supports **creating** data integration data sources.<br><br>* Developer: Can view and edit all tasks within the project, can **view** data integration data source configuration, with no task review permissions.<br><br>* Reviewer: Can view and edit all tasks within the project, and review officially released tasks.<br><br>* Visitor: Users with visitor permissions to the project can **view** all tasks within the project.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the project’s <strong>Project Type</strong> is <strong>Private</strong>, the <strong>Role Type</strong> of the project members will show the <strong>Visitor</strong> option.   </div><br>    |
      

   * Search for members

      Search for information that meets the criteria in the following ways. When setting multiple search criteria, the intersection of the criteria is used for the query.

      * From the dropdown list, choose the member role.

      * Enter the member name information, then click the search icon on the right side of the search box.

   * Edit member permissions

      Click the **Edit permissions** button in the **Action** column of a user in the member list. In the pop\-up **Edit Permissions** window, modify the user role and click the **Confirm** button to complete the permission change for that user.

   * Remove member

      * Click the **Delete** button in the **Action** column of a user in the member list. In the pop\-up confirmation dialog, click the **Confirm** button to remove that user from the project.

      * After selecting one or multiple options, click the **Batch Remove** button. In the pop\-up confirmation dialog, click the **Confirm** button to remove the selected users from the project.
