---
title: "Project/Application/Permission Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Project_Application_Permission_Management"
---

<span id="c0e58850"></span>
# 1.Project/Application Management

<span id="8c8dc0be"></span>
## What is the relationship between application ID and package name?

(1) There is no strong dependency between the package name and appid filled in when creating the application. At present, only the advertising module will use the package name, and other functions are not involved.

(2) If the customer has multiple applications, it is recommended that each application app needs to create an application ID. The disadvantage is that the data between applications is isolated, and multiple apps cannot be connected.

(3) Package names and appids are one\-to\-one, and a package name cannot have multiple appids.

<span id="98449c4c"></span>
## Why does it prompt "Package name repeated" when creating a new application? [Finder creates a new application, fill in the package name and prompt "package name already exists"]

Possible reasons: This application has been launched in large quantities, appid is applied in appcloud, and appcloud requires appid package name to be globally unique;

Solution:

(1) Confirm whether you have created other applications with this package name before? If not, you can synchronize with our customer service classmates or customer success manager to further investigate the cause.

(2) If the previously created application has been enabled and you want to create an application with the same package name again, if the historically created application is enabled to be deleted, you can provide the application ID that was accessed at that time, and we will assist in deleting the original application. After deletion, you can start the new creation process again.

<span id="c7d98dbc"></span>
## App List \- What is the use of modifying the time zone?

When querying and analyzing, display the date, select the corresponding time zone, and the date seen by the query and analysis is the time in the corresponding time zone.

<span id="79bbd216"></span>
## How to modify the application type selected when applying for an AppID?

It is not recommended that you modify it because the relevant configuration has been generated and you can reapply for the Appid.

<span id="cd558137"></span>
## Can applications from different platforms be integrated under the same app ID?


* iOS, the Android side can be integrated under the same Appid, for example, when creating an application, iOS and Android side are integrated in one application.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54c2affcb8fc4b3ba4a58c8b058955b8~tplv-goo7wpa0wc-image.image) </span>

* Applications on other platforms can create an application separately. If you need to aggregate data from multiple applications in one project for analysis, you can use the multi\-application function: [Use Multiple Apps](https://docs.byteplus.com/docs/DataFinder/Use_Multiple_Apps).


<span id="7c1f8393"></span>
## What does the App key do and what scenarios will it be used in?

APP Key is generally reported for application verification, such as HTTP API, Java SDK.

<span id="8520a5eb"></span>
## Can a SaaS\-cloud\-native environment delete group users?

At present, the direct deletion of group users is not supported in the SaaS\-cloud native environment, and a similar deletion effect can only be achieved by disabling it. If you need to delete a user, please contact BytePlus technical support for background operations. Note that SaaS\-Cloud Native does not support group user resources retained after deleting a group user, such as Kanban.

<span id="ab8b30cf"></span>
## Can SaaS\-cloud native environments delete and modify applications?


* SaaS\-cloud native modification of the application name can only be modified through the group overview. Others do not support modification.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45e02a77153c49e4bdc21d3010deb1a1~tplv-goo7wpa0wc-image.image) </span>

* In a SaaS\-cloud native environment, if you enable the multi\-application function and bind multiple applications in a project, users with project details editing permission can delete multiple applications that are added later.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4750ca1ec3694dd0892e725c3179dad9~tplv-goo7wpa0wc-image.image) </span>

   Delete without a delete button should not be supported.

* In SaaS\-non\-cloud native environments, you can delete apps from the group management page.


<span id="d831e437"></span>
## After deleting the app in the project, is there a way to undo the deletion operation and retrieve the data under the app?

After the project application is deleted, it cannot be restored and the deletion operation cannot be undone.

<span id="970237e0"></span>
## Does modifying the application time zone affect the processing data logic of the data stream?

No. Modifying the application time zone will not affect the parsing of the event_date. The overseas set community libraries are all UTC + 0. The application of the time zone is mainly to parse the time according to the set time zone when querying.

<span id="b7166f48"></span>
## The default time zone was not used when creating the application, and changing it to another time zone will affect the reported data?

A different time zone was selected when the app was created, and when data in datetime format is reported, it will be converted according to the current time zone. If you don't need to automatically convert the datetime data to the time in the corresponding time zone after modifying the time zone, it is recommended to report the time data of type string.

<span id="176549f0"></span>
# 2.Permission management

<span id="e4ddebac"></span>
## In a newly created project, even if the relevant user has been configured with role permissions, the user is still prompted No access.

The newly created project needs to create the app at the same time, otherwise the role permission configuration may be invalid. Make sure to create the app at the same time as the project is created, so that role permissions can take effect properly.

<span id="f63e86c9"></span>
## Can't view the group overview after authorizing the project administrator?


* In SaaS\-cloud native, project administrators cannot view the Group Overview page. The Group Overview sees information about all projects under the Group, so it cannot be provided to project administrators for viewing. If the project administrator wants to view the group overview page, he needs to grant the project administrator permissions for all projects under the group. Having permissions for all projects under the group is equivalent to the group administrator in order to view the group overview page.

* SaaS\-non\-cloud\-native is divided according to the group. The group administrator authority of SaaS\-non\-cloud\-native is not equal to the project administrator of SaaS\-cloud\-native. Only the main account authority of SaaS\-cloud\-native is the group administrator (except for the operation and maintenance whitelist users, who inherit the group administrator authority).


<span id="8e6758b0"></span>
## After having the management authority of all projects under the group, is it the group administrator?

Yes, if your account has management rights for all projects under the group, the current account is the group administrator and has group administrator rights. You can enter the group configuration page for group data viewing and group management operations.

<span id="0a5edfd5"></span>
## Why can't the group administrator reset the password?

Based on the perspective of security compliance; there are loopholes in the way the group administrator reset the password before, if the user creates a new group and invites other accounts to enter the group, you can directly reset the password of other accounts and log in. Therefore, from a security perspective, the authority to reset passwords is currently reserved for the super administrator (the system initialization user).

<span id="8f96db29"></span>
## Can the administrator account modify the username for the user in the user list?

No, only the user can modify the username under the main account\-account information.

<span id="e4714412"></span>
## I have data download permission, but I can't download data in the Finder. What's the reason?


1. Verify that the user role status is enabled and check if the user has project permissions.

2. Attempt to first authorize users to edit and download data.

3. Check if other users can download normally.

4. Attempt to clean the cache.

5. Re\-authorize the user's Kanban editing and download permissions (e.g. the downloaded content is Kanban data).


<span id="e332e566"></span>
## How to open saas operation and maintenance permissions?

After entering the finder product, click the file icon icon in the lower right corner, select "Allow DataRangers' operation and maintenance personnel to enter your group", and set the group opening time.

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

<span id="cd40e53b"></span>
# Data desensitization

<span id="d9937af2"></span>
## The properties of the finder part have been set for desensitization. How to remove desensitization?

On the Project Center \> Rights Management \> User Management page, view the details of DataFinder permissions owned by users associated with user roles that have been opened to DataFinder. This includes [Attribute Desensitization], which can be adjusted in this module.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ea80a0fae2a45de9e8a7d065bfd38fc~tplv-goo7wpa0wc-image.image) </span>
