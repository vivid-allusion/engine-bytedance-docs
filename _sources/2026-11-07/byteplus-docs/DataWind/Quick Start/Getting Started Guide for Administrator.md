---
title: "Getting Started Guide for Administrator"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Getting_Started_Guide_for_Administrator"
---

When you first use the product, the account you receive is the system administrator for this system. By default, the system supports only one system administrator and does not allow adding more. The system administrator can add more users by following the steps below.

<span id="c81f486e"></span>
# Permission system overview

The permission system of Intelligent Data Insight consists of three components: **roles**, **resources**, and **control modes**.

For detailed information about permissions, see [Permission Management](https://docs.byteplus.com/docs/DataWind/Permission_Management).


1. Roles are divided into platform roles and functional roles:

* **Platform roles** include system administrator, project administrator, project global viewer, resource administrator, and regular user, and are used to define the scope of user operations at the system level.

* **Functional roles** include role administrator, user group administrator, and user attribute administrator, and are used to refine management responsibilities for specific functional modules.

   
   |Category |Role name |Permission description |
   |---|---|---|
   |**Platform roles** |Regular user |Can access dashboards, datasets, visualization query pages, certain pages in Project Center, and create projects. |
   ||Project administrator<br><br>(Highest project\-level permission) |In addition to regular user permissions, can configure basic project information, manage project members, and grant all resource permissions in Project Center. |
   ||System administrator<br><br>(Highest system\-level permission) |In addition to project administrator permissions, can access dashboards, datasets, visualization query pages, certain pages in Project Center, and create projects. |
   |**Functional roles** |User attribute administrator |Manage the values of different user attributes in the user list. |
   ||User group administrator |Configure resource permissions and members of user groups (project\-level user groups). For details, refer to [User Group Management](https://docs.byteplus.com/docs/DataWind/User_Group_Management). |
   ||Role administrator |Configure resource permissions, row and column permissions, and role members. For details, refer to [Role Management](https://docs.byteplus.com/docs/DataWind/Role_Management). |
   

2. At the resource level, projects, dashboards, datasets, folders, and large screens are used as permission control objects. Users can obtain permissions through single\-resource authorization, user groups, roles, folders, and Feishu groups. The system uses a combination of "resource permissions + row and column permissions" for authentication logic, further enabling row\-level and column\-level data access control based on resource\-level authorization.

   In addition, the system provides three control modes—regular, moderate, and strict—to adjust the scope and strictness of permission policies, balancing security and flexibility for different scenarios.

   
   |Permission |Type |Details |
   |---|---|---|
   |Resource |Control object |Project, dashboard, dataset, folder, large screen, and more. |
   ||Permission acquisition method |Single resource authorization, user group, role, folder, Feishu group. |
   ||Authentication logic |Authentication based on a combination of resource permissions and row\-column permissions. |
   


<span id="cfcd3552"></span>
# Add users

As a system administrator, when you are trying out or first using this product, you use the username and password of your Volcano Engine account by default.

<span id="1165ba15"></span>
## Basic information settings


1. You can click the avatar in the upper right corner of the product interface, click Access Control under Permissions and Security, and select User Management \- Users in the side navigation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05768f8ecda94ccf8dec49fd4371f312~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38046aa796cd4a2ea8eb931359e4d1ba~tplv-goo7wpa0wc-image.image) </span>

2. In the upper right corner of the user management list, click the **New user** button and select a method to create a new user:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e36720e226643dcbe80bd6d237d4f38~tplv-goo7wpa0wc-image.image) </span>

* **Create by username:**  Click the Create by username button to enter the configuration process: enter basic information \> permission settings \> review \> complete.

   
   |Configuration item |Description |
   |---|---|
   |Basic information |Enter user information, including username (required), mobile number, email, display name, remarks, and tags. |
   |Access methods |Select access methods. Multiple selections are supported.<br><br><br>* Programmatic access: Assign an Access Key to the user for API access.<br><br>* Console access: Assign a password to the user for console login.<br><br>   * Access password: Choose to generate the password automatically or set a custom password. If you choose to set a custom password, you must specify the access password.<br><br>   * Password reset: Choose whether to require a password reset on the next login.<br><br>   * Enable login protection: Choose whether to enable two\-factor authentication at login. |
   

* **Create by phone number:**  Click the Create by phone number button to enter the configuration process. Enter basic information \> permission settings \> review.

   
   |Creation steps |Note |
   |---|---|
   |Basic information |1. Enter the relevant basic information. Including security mobile number (required), display name, email, and remarks.<br><br>2. Login settings: Console access is selected by default. Programmatic access can also be selected.<br><br><br>After completing the above configuration, click Next to proceed to permission settings. |
   |Permission settings |After entering permission settings, search for the policy name datawind, select the corresponding system policy, and click Next. For details, see the next section on permission settings. |
   |Review |For details, see the review section. |
   

* **Invite Ocean Engine account:**  Click the **Invite Ocean Engine account** button to enter the configuration process: invitation information settings \> permission settings \> review \> generate invitation link.

   
   |Configuration steps |Note |
   |---|---|
   |Basic information |1. Enter user information:<br><br>   * Number of invited users: Select the number of users to invite. Minimum is 1, maximum is 5.<br><br>   * Invitation validity period: Cannot be changed. The default is 24 hours.<br><br>2. Login settings: Multiple selections are supported. Console access is selected by default (assign a password to the user for console login). Programmatic access is optional (assign an Access Key to the user for API access). |
   |Generate invitation link |After configuring permissions and review for the user (see the following two sections for details) and completing secondary verification, the system generates an invitation link.<br><br>Please send the link to the users you want to invite and inform them to promptly enter their user information to complete creation. The link is valid for 24 hours.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Please click the link to copy it. After the page is closed, you will not be able to see this link again. To ensure security, please send the link via private message whenever possible. Do not expose the link to users who are not the intended recipients.</div><br> |
   


<span id="d3d9053b"></span>
## Permission settings

After selecting the method to add a user and completing the basic information according to the system configuration, you must grant the sub\-user the \*\*\*\* **DatawindFullAccess** permission in the permission settings. For details about the policy, see [Policy overview](https://www.volcengine.com/docs/6257/65058?lang=zh).


1. On the permission settings page, select the Add permission policy tab, enter datawind in the search box, select the **DatawindFullAccess** permission, and click Next to proceed to the review step.

2. To add the user to a user group, select the Add to user group tab, choose a user group, and then click Next to proceed to the review step.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/525af08396a14f5eb01ad9e29edb4303~tplv-goo7wpa0wc-image.image) </span>


<span id="bbb077cb"></span>
## Review

In the review step, you can view the configuration information. After confirming that the information is correct, click the Next button to proceed to authentication. Enter the authentication code and click Confirm to successfully add the user. You can view the added users in User Management \- User List.

If self\-binding is not performed, additional authentication is required. Click the Go to bind button in the system pop\-up window to enter the binding process. Select a security email or MFA device for secondary identity verification, and click Confirm after completion.

<span id="ec251341"></span>
# Add the user to the system

After adding a user, the system administrator needs to add the newly added user to the system.


1. Log in to the Volcano Engine console and click Intelligent Data Insight to enter the product interface.

2. On the product page, click the **System management** button on the upper right of the top navigation to enter system management.

3. Select User Management from the side navigation, enter the new username, and click the Confirm button to add the user.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18da5e95def046bb93ee0fb417c1c2df~tplv-goo7wpa0wc-image.image) </span>


<span id="b7636d97"></span>
# Bind the user to a project.

Select the corresponding project in the upper right corner of the system, click Project Center at the top of the system, enter the project, and add the user to the corresponding project.


1. On the Project Center page, select Permission Control \> User Management from the side navigation.

2. Click the Add User button above the list to enter the user addition and authorization configuration process.

3. On the Add User configuration page, enter the username, select the project permissions to grant from the dropdown, and click the Confirm button to complete user\-project binding and authorization.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c02d4a38b3124d4a9ee1b355fb5cd0cb~tplv-goo7wpa0wc-image.image) </span>

   
   |Project permissions |Permission details |
   |---|---|
   |View permissions |Grants access to enter the project, but does not allow viewing all resources under the project.<br><br><br>* Allows viewing resources within the project for which the user has permission<br><br>* Allows creating personal dashboards, datasets, or folders, and performing similar operations<br><br>* Allows creating public dashboards or folders in public folders where the user has edit permissions<br><br>* Allows creating folders or datasets in folders where the user has edit permissions<br><br>* Cannot create folders or datasets in the root directory of datasets<br><br>* Cannot create public folders or public dashboards in the root directory of public folders |
   |Edit permissions |On the basis of **View permissions**, allows creating public dashboards, public folders, or datasets in the root directory, and creating user attributes. |
   |Global view permissions |On the basis of **Edit permissions**,<br><br><br>* Allows viewing all public dashboards, public dashboard folders, and datasets within the project, and allows viewing all data without being restricted by row or column permissions (this does not mean having edit permissions for all resources)<br><br>* Allows viewing all personal dashboards via personal dashboard links, but the dashboard list will not display all personal dashboards |
   |Manage permissions |Allows managing permissions for all resources within the project, deleting the project, and performing any other operations. |
