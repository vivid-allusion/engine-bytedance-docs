---
title: "Permission descriptions"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/datasail_permission"
---

<span id="0e4f3336"></span>
## 1 Background

By default, DataLeap sub\-accounts cannot create or manage integrated tasks, integrated Datasources, or Exclusive Integrated Resource Groups. These actions are only permitted for the main account and sub\-accounts that have been granted the DataLeapFullAccess, DataLeapSailCreateTaskAccess, or other permission policies.

This article introduces the data integration operations that sub\-users with different permission policies are allowed to perform, and explains the steps for adding permission policies.

<span id="aefb857c"></span>
## 2 Use prerequisites

The information for the sub\-user accounts that need to be used has been created. For details, see [Account preparation](https://docs.byteplus.com/docs/undefined/689b46e8da1adf0528d3aaed).

<span id="72d632b5"></span>
## 3 Account description

At the global level, DataLeap includes two types of users: the main account (tenant admin) and IAM user (tenant member).


* Main account

   It can be regarded as a special user (referred to as the root user), who is the owner of cloud service resources and is also the primary entity for resource metering and billing. By default, the main account has all permissions under the account, including operational permissions for all module products within the DataLeap service, such as Data Development, Task Release, Project Console, Data Security, and so on.

* IAM user

   You can create user accounts under a project, each belonging to a different member. By using the main account to grant different policy permissions, you can achieve fine\-grained control over members' access to cloud resources.


The DataLeap platform allows the main account to grant resource permissions to IAM users (sub\-accounts), ensuring that only IAM users who have permission can perform various resource actions in the DataLeap Console. This helps prevent security risks that may arise from exposing the main account key.

<span id="211103ba"></span>
## 4 operation steps

We will now explain the steps for the main account to assign relevant permission policies to sub\-users.


1. Log in to [BytePlus IAM Control Interface](https://console.byteplus.com/iam/identitymanage/user) using the main account.

2. In the left navigation bar, choose **User Management \> User** to enter the Sub\-user Management page.

3. Search for sub\-username information that requires authorization in the search box in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/027c772e002842b6be044909f7859867~tplv-goo7wpa0wc-image.image) </span>

4. Click the username to enter the User detail page. Then switch to the **Policy** tab.

5. Click **Authorize** button to enter the policy selection page.

6. On the Add Permissions page, after searching for the relevant permission policy name and selecting it, click the **Confirm** button to add the corresponding permission policy to the sub\-user.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8743345cb37b4d8096c0ecba3ae5a3f4~tplv-goo7wpa0wc-image.image) </span>

<span id="a7c5742c"></span>
## 5 Permission policy description

<span id="5287774e"></span>
### 5.1 Description of DataLeap permissions

The DataLeap platform supports the **DataLeapFullAccess** permission policy. Currently, this permission policy grants IAM users the full read\-write policy for the DataLeap service.


|Permission policies |Permission descriptions |
|---|---|
|DataLeapFullAccess |Has full management permissions for the purchase and unsubscription of all resources, project creation, and task creation on the DataLeap platform.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The DataLeapFullAccess permission policy does not support access rights to database tables. You can apply for the relevant access rights through the <a href="https://docs.byteplus.com/en/docs/dataleap/Rights_Management">Permission management</a> feature of <strong>Data Security</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If IAM sub\-users do not require permission to purchase or unsubscribe from DataLeap platform resources, or permission to create projects, and only need task development permission, you do not need to grant the DataLeapFullAccess permission. Instead, grant the specific DataLeap Project Auth. See details <a href="https://docs.byteplus.com/docs/dataleap/manage_project_member">Manage Member Information</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If IAM sub\-user task development involves creating and using DataSail Data Integration tasks, Exclusive Integrated Resource Groups, or other related content, you need to add the relevant DataSail permissions. See details <a href="https://docs.byteplus.com/docs/dataleap/datasail_permission#c7a680e6">5.2 Description of DataSail permissions</a>.</div><br> |


<span id="c7a680e6"></span>
### 5.2 Description of DataSail permissions

For DataSail\-related operations, if an IAM user does not require the DataLeapFullAccess permission, you can grant them permission policies such as DataLeapSailReadOnlyAccess and DataLeapSailCreateTaskAccess.

The restrictions on data integration\-related actions under different permission policies are as follows:


| |Actions |Project role requirements |**DataLeapSailReadOnlyAccess** |**DataLeapSailCreateTaskAccess** |**DataLeapFullAccess** |
|---|---|---|---|---|---|
|Tenant console (not project\-specific) |Create, expand, scale down, renew, unsubscribe from, or delete an exclusive integrated resource group |None |Not supported |Not supported |✅ |
||View exclusive integrated resource group list, view usage, view Run Instance, and view Project binding |None |✅ |✅ |✅ |
||Project binding and unbinding for resource groups |Project Administrator |Not supported |✅ |✅ |
|Within a single project |Create, edit, or delete datasources |Project Administrator |Not supported |✅ |✅ |
||Ordinary integration task creation and operation and maintenance |Project administrator or developer |Not supported |✅ |✅ |
||Create, modify, or delete solutions |Project administrator or developer |Not supported |✅ |✅ |
||Permission to view the list of datasources, ordinary integration tasks, and solutions |Project administrators, developers, reviewers, and visitors |✅ |✅ |✅ |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The <strong>visitor</strong> role can only access projects of the <strong>public</strong> type. For details on project type distinctions, see <a href="https://docs.byteplus.com/docs/dataleap/create_project">Create a Project</a>.</div>


* <div data-tips="true" data-tips-type="tip">The permission restrictions for the Invalid Permissions policy DataLeapSailFullAccess are consistent with those for DataLeapFullAccess.</div>



<span id="16dd7ac4"></span>
## 6 Action

After sub\-users complete adding the corresponding permission policies, they can go to the DataLeap project to perform related operations such as creating a Datasource, creating a task, and other related operations.
