---
title: "Using NDB for MySQL with IAM users"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Using_veDB_MySQL_with_IAM_users"
---

IAM user is a type of identity for access control, created by an account (also known as a root user) or a user with permissions. After a user is granted a policy, they can log in to the console or use an Access Key to call an API to access cloud resources. Each Root user can create multiple IAM users and grant them different permissions to manage cloud resource access for different identities under the account. This article describes how to set the relevant permissions for IAM users to use the NDB for MySQL service.

<span id=".6YCC55So5Zy65pmv"></span>
## Applicable scenarios


* **Manage resources independently**: Create different IAM users for different services to access the resources that belong to each service.

* **Security concerns**: Using IAM user AK/SK to call OpenAPI interfaces effectively avoids the risk of leaking the root user AK/SK.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permission description

<span id=".562W55Wl566h55CG"></span>
### Policy management

A policy is a description of permissions. IAM users, user groups, and roles must be granted permissions by attaching policies. A policy can define the scope of actions, resources, and conditions for permissions to take effect. For details, refer to [Policy syntax structure](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax). IAM supports two types of policies: System default policy and User custom policy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If an IAM user needs to access the NDB for MySQL service, you must grant the IAM user at least the management or read\-only permissions for NDB for MySQL and Cloud Monitor services from the system default policy, as well as the custom policies described below.</div>


* <div data-tips="true" data-tips-type="tip">Cloud Monitor and custom policies can only be added for IAM users in the global scope, not as project permissions.</div>


* <div data-tips="true" data-tips-type="tip">NDB for MySQL instances, virtual private clouds, subnets, and allowlists can belong to different projects. Therefore, you need to grant IAM user permissions for all associated projects.</div>


* **System default policy**: Coarse\-grained collections of common permissions created and managed by BytePlus. System default policy can only be used for authorization and can not be edited or modified.

   
   |Associated services |Policy name |Description |
   |---|---|---|
   |All products in BytePlus that support IAM |AdministratorAccess |Includes administrative permissions for all products that support IAM, such as ECSFullAccess, VPCFullAccess, IAMFullAccess, and CloudMonitorFullAccess.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">IAM users with the <code>AdministratorAccess</code> permission will have administrative permissions for all BytePlus products within the authorized scope (project or global). Grant this permission with caution.</div><br> |
   |NDB for MySQL |VedbMysqlFullAccess |NDB for MySQL full management permissions. After adding this permission, users will have<br><br>Read/Write permissions for NDB for MySQL within the policy scope, such as creating instances, deleting instances, and changing instance configurations. |
   ||VedbMysqlReadOnlyAccess |Read\-only access permission for NDB for MySQL. Allows users to view NDB for MySQL instances within the policy scope. |
   |(Optional) Virtual private cloud |VPCFullAccess |Full management permissions for the virtual private cloud (VPC). After this permission is added, the user will have Read/Write permissions for the virtual private cloud within the policy scope, such as creating a virtual private cloud or binding a virtual private cloud or subnet to NDB for MySQL instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify a project when creating a VPC, but not when creating a subnet. By default, a subnet is in the same project as the VPC to which it belongs. Project changes for VPCs and subnets are independent. Modifying the affiliated project of a VPC does not simultaneously change the affiliated project of the subnets under that VPC. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Managing-projects">VPC Project Management</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you modify the affiliated project of a VPC, you also need to change the projects of its subnets to ensure consistency. Otherwise, IAM users without global permissions will be unable to select a subnet or will encounter an error when creating cloud resources. For specific instructions on how to modify the affiliated project, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-project-management">Managing projects</a>.</div><br> |
   ||VPCReadOnlyAccess |Read\-only access permissions for the virtual private cloud (VPC). Allows users to view private network and subnet information for NDB for MySQL instances within the policy scope. |
   |Cloud monitor |CloudMonitorFullAccess |Full management permissions for Cloud Monitor. After adding this permission, users will have Read/Write permissions for monitoring and alerts on NDB for MySQL instance within the policy scope, such as viewing instance monitoring data and adding alert policies for instance. |
   ||CloudMonitorReadOnlyAccess |Read\-only access for Cloud Monitor. Allows users to view monitoring data for NDB for MySQL instances within the policy scope. |
   |(Optional) Database Workshop |DbwFullAccess |Full management permissions for Database Workshop DBW. After adding this permission, users will have Read/Write permissions for the Database Workshop within the policy's scope, such as using data interaction and observation diagnosis features.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">IAM users with <code>DBWFullAccess</code> permission will have management permissions for NDB for MySQL instances within the authorized scope (Project or Global), and are not restricted by <code>VedbMysqlFullAccess</code>. Grant with caution.</div><br> |
   |(Optional) Tag service |TagFullAccess |This policy allows you to manage content related to the Tag service in your account, such as querying by Tag. <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If IAM user needs to see the root user existing tags in the drop\-down lists for tag keys and values when adding tags to a NDB for MySQL instance, this permission must be added for the IAM user at a global scope. Otherwise, the drop\-down lists will be empty.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">IAM user can add new Tags to an instance even without the <code>TagFullAccess</code> permission. For details on how to add a Tag, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Associating_or_adding_tag">Associating or adding tag</a>.</div><br> |
   

* **User custom policy**: Manually created, fine\-grained sets of permissions for resource management. When system default policy does not meet your requirements, you can create custom policies to define permissions at a granular level. For details, refer to [Creating a user custom policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

   To use the NDB for MySQL service, you also need to grant IAM users the following custom permissions under global permissions.

   1. Log in to the [console](https://console.byteplus.com/db/vedb-mysql) with your root user and click **IAM** in the personal center in the upper\-right corner.

   2. On the **IAM** \> **Permission policy** page, click **Create policy**, and select **JSON editor**. Set a **Policy name** (e.g., VedbMysql_Custom), copy the following content to the editor, and click **Submit**.

      ```json
      {
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "vpc:DescribeEipAddresses"
                  ],
                  "Resource": [
                      "*"
                  ]
              }
          ]
      }
      ```
      


<span id=".5L2c55So6IyD5Zu0"></span>
### Effective scope

After selecting a policy, specify its scope for IAM users:


* **Global permissions**: The policy applies to all projects within the account, including any future projects.

* **Project permissions**: The permission policy applies only to resources within the specified project.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [console](https://console.byteplus.com/db/vedb-mysql) with your root user and click **IAM** in the personal center in the upper\-right corner.

2. On the **IAM \> User management \> User** page, click **Create New User**.

3. On the **Create User** page, select the user creation method and fill in the basic information. For details, refer to [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

4. In the **Permission Settings** wizard, set the permission policy and scope for the user, and then click Submit.

   
   |Permission type |Permission policy |
   |---|---|
   |Management permissions |To grant IAM user administrative permissions for NDB for MySQL, you need to grant the IAM user the following permissions.<br><br><br>* Add `CloudMonitorFullAccess` and `VedbMysql_Custom` as global permissions.<br><br>* `VedbMysqlFullAccess` can be added as global permission (administrative permissions for all projects) or project permission (administrative permissions for a specified project). |
   |Read\-only permissions |If you want to grant an IAM user read\-only permissions for NDB for MySQL, you need to grant them the following permissions.<br><br><br>* Add `CloudMonitorReadOnlyAccess` and `VedbMysql_Custom` as global permissions.<br><br>* You can add `VedbMysqlReadOnlyAccess` as either global permissions (read\-only permissions for all projects) or project permissions (read\-only permissions for specified projects). |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the IAM user is successfully created, you can modify their permission policy at any time. For operation details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management">Managing users</a>.   </div>
   

5. Log in to the [console](https://console.byteplus.com/db/redis) as an IAM user and use theNDB for MySQL service.
