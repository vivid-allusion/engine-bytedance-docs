---
title: "Permission management for the console: Grant permissions to IAM users"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/si_permission_control"
---

To ensure that IAM (Identity and Access Management) users can properly use the EMR Serverless OLAP Console features, you need to use BytePlusthe primary account to log in to the Access Control IAM Console and grant the corresponding permissions to IAM users.

<span id="_1-背景信息"></span>
## 1 **Background information**

Access Control IAM is a resource access control service provided by BytePlus. For details, see [Cloud Identity Product Overview](https://docs.byteplus.com/en/docs/CloudIdentity/ProductOverview).

The typical use cases for IAM in EMR Servereless OLAP are as follows:


* User: If you purchase an EMR Servereless OLAP instance, your organization may have multiple users (such as operations, development, or data analysis) who need to use these instances. You can create a policy to allow some users to use these instances. This avoids exposing the same AccessKey to multiple people.

* User group: You can create multiple user groups and grant different permission policies to them, enabling batch management of user permissions. The process for authorizing user groups is the same as for authorizing users.


<span id="_2-权限策略"></span>
## 2 **Permission policies**

Permission policies are divided into **system policies** and **Customer managed policies**:


* System policies

   The system policies used by EMR Servereless OLAP are as follows:

   
   |System policy name |Description |Included permissions |
   |---|---|---|
   |EMRServerlessFullAccess |EMR Serverless OLAP administrator permissions |All permissions. |
   |EMRServerlessReadOnlyAccess |EMR Serverless OLAP read\-only permissions |Only permissions to view the instance list and query instance details; no permissions to create, update, or modify instances. |
   

* Customer managed policies

   To create Customer managed policies for fine\-grained permission control, refer to if you are familiar with BytePlusvarious cloud service APIs. When creating, you need to precisely design the permission policy script.


<span id="_3-授权-iam-用户"></span>
## 3 **Authorize IAM users**

In the IAM console, grant EMR Servereless OLAP permission policies to IAM users:


1. Use BytePlusthe primary account or an IAM user with administrator permissions to log in to the [IAM Console](https://console.byteplus.com/iam/identitymanage/user).

2. In the left navigation bar, click **Access Control \> Users** to enter the user management page.

3. On the **Users** page, click the **Manage** button in the **Actions** column for the target IAM user.

4. On the **User details** page, switch to the **Permissions** tab, select the authorization scope, principal, and permissions as needed, and add the corresponding permissions for the IAM user.

5. Click the **Confirm** button in the lower right corner to complete adding permissions.


After authorization is completed, the permissions take effect immediately. You can log in to the EMR Servereless OLAP console using the authorized IAM user to perform related operations.
