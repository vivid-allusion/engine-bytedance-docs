---
title: "External instance management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/self-managed-database-administration"
---

Database Workshop DBW supports connecting to your self\-managed external database instances—hosted in IDCs, ECS, or other environments—via the public internet, enabling unified management along with centralized permission control, operational auditing, and efficient collaboration. This effectively reduces operational complexity and helps meet compliance requirements. This article describes how to manage external database instances in the DBW console.

<span id="VCcR8I9s"></span>
## Prerequisites

When connecting to a self\-managed database instance over the public internet in a self\-built setup, and the instance has access restrictions enabled, you must add DBW's server IP address to the target instance's whitelist or security group before registering the instance.  The DBW server IP addresses are `145.223.191.0/28`, `145.223.191.128/28`, `145.223.191.192/28`.

<span id="R4fAhHys"></span>
## Precautions


* Currently, only self\-managed MySQL and PostgreSQL instances hosted in your IDC, ECS, or other environments are supported for connection.

* Under a single region, each account can manage up to a provisional limit of 2,000 instances.

* Currently supports managing MySQL or PostgreSQL instances by connecting them via a public network self\-built setup.

* It is recommended to use a dedicated account for DBW access, following the principle of least privilege and granting only the necessary DML, DDL, and object\-level permissions at the instance or database level as required.

* It is recommended to enable the instance's security control. If not enabled, you will need to manually enter your account and password for each login, and features such as password\-free login will not be available.

* To avoid interference, do not add spaces or other symbols before or after the entered information.

* Databases in public network environments are vulnerable to attacks. Please configure an IP whitelist for database access to enhance security.

* Added instances are assigned to "All Account Resources" by default, while DBW defaults to the default project. If the instance is not found after successful addition, please switch the project to "Account All Resources" to view it.

* This feature is currently available to allowlisted users only. To use it, please [Submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.


<span id="emURl6Gm"></span>
## Advantages


* Unified management portal

   Regardless of whether the database is deployed on BytePlus, other public clouds (such as Alibaba Cloud, AWS, Tencent Cloud), local IDC, or self\-built ECS environments, all can be centrally managed through DBW, eliminating the need to switch between multiple tools.

* Enhanced security

   * Supports secure hosting: DBW encrypts and manages database account credentials, eliminating the need for you to know plaintext credentials and reducing the risk of credential leakage.

* Improved collaboration efficiency

   * Supports passwordless login (requires enabling secure hosting), simplifying daily operations.


<span id="Y3c2MPAv"></span>
## Add external instance


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. On the **Instance list** page, click **Add external instance**.

5. On the **Create database instance** control panel, configure the following parameters.

   
   <Tabs>
   <Tab zoneid="cLEiQOJCAG" title="RDS for MySQL engine">
   <TabTitle>RDS for MySQL engine</TabTitle>
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance name** |Custom instance names must meet the following requirements:<br><br><br>* The length must not exceed 128 characters and cannot be empty.<br><br>* Only Chinese characters, letters, numbers, underscores (_), and hyphens (\-) are supported.<br><br>* Cannot start with digits or hyphen (\-). |
   |**Database type** |Select a database type as needed. This example uses **MySQL**. |
   |**Access method** |Currently, only **MySQL connected over public network** is supported for connecting external instances. |
   |**Region** |The region is determined by the region selected in the top\-left corner of the top menu bar and cannot be modified. |
   |**Host address** |Enter the public IP address or resolvable domain name of the target instance. |
   |**Port** |Port of the target instance. |
   |**Database account** |Enter the database account for the target instance. It is recommended to use a dedicated account, follow the principle of least privilege, and grant instance\-level or database\-level DML, DDL, and object operation permissions as needed. |
   |**Database password** |Enter the database account and password for the target instance. |
   |**Test connectivity** |Click **Test connectivity** to verify whether the instance is successfully connected.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connectivity** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed, check if the network is normal**: When this error prompt appears, verify your network connectivity.<br><br>* **Connection authentication failed. Check if the username and password are correct**: when this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify your IP address. |
   |**Security control mode** |Enable security control as needed. We recommend enabling security control for the instance. If disabled, you must manually enter the account password each time you log in, and features like password\-free login will be unavailable. |
   |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br>For more information on security rule sets, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security-rule-management?lang=en). |
   |**Instance DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
   |**Instance owner** |Select the instance owner from the drop\-down list. Both administrator and normal user can be assigned as the instance owner. The instance owner will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance Owner will automatically serve as the first\-level approver. |
   |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br>The primary account can approve all tickets by default. For more information on the approval workflow, see [Approval workflow management](https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management?lang=en). |
   
   
   
   
   
   </Tab>
   <Tab zoneid="VZN3yU7Lfn" title="RDS for PostgreSQL engine">
   <TabTitle>RDS for PostgreSQL engine</TabTitle>
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Instance name** |Custom instance names must meet the following requirements:<br><br><br>* The length must not exceed 128 characters and cannot be empty.<br><br>* Only Chinese characters, letters, numbers, underscores (_), and hyphens (\-) are supported.<br><br>* Cannot start with digits or hyphen (\-). |
   |**Database type** |Select the database type as needed. This example uses **PostgreSQL**. |
   |**Access method** |Currently, only **PostgreSQL connected over public network** instances can be added as external instances. |
   |**Region** |The region is determined by the region selected in the top\-left corner of the top menu bar and cannot be modified. |
   |**Host address** |Enter the public IP address or resolvable domain name of the target instance. |
   |**Port** |Port of the target instance. |
   |**Database account** |Enter the database account for the target instance. It is recommended to use a dedicated account, follow the principle of least privilege, and grant instance\-level or database\-level DML, DDL, and object operation permissions as needed. |
   |**Database password** |Enter the database account and password for the target instance. |
   |**Test connectivity** |Click **Test connectivity** to verify whether the instance is successfully connected.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connectivity** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed, check if the network is normal**: When this error prompt appears, verify your network connectivity.<br><br>* **Connection authentication failed. Check if the username and password are correct**: when this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify your IP address. |
   |**Security control mode** |Enable security control as needed. We recommend enabling security control for the instance. If disabled, you must manually enter the account password each time you log in, and features like password\-free login will be unavailable. |
   |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br>For more information on security rule sets, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_?lang=en). |
   |**Instance DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
   |**Instance owner** |Select the instance owner from the drop\-down list. Both administrator and normal user can be assigned as the instance owner. The instance owner will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance Owner will automatically serve as the first\-level approver. |
   |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br>The primary account can approve all tickets by default. For more information on the approval workflow, see [Approval workflow management](https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management?lang=en). |
   
   
   
   
   
   </Tab>
   </Tabs>
   

6. Click **OK**.


<span id="Ec5p4wuY"></span>
## Manage external instances


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. On the **Instance list** page, click the **Connection normal** tab.

5. On the **Connection normal** tab, filter the **Database type** to **Public network self\-built database**.


You can search for the target instance by instance ID or instance name in the upper left corner of the **Instance list** page, or filter instances that meet the criteria through **Security control**.


|**Actions** |**Description** |
|---|---|
|View instance information |In the **Instance list**, you can view information such as **Instance name/ID**, **Database type**, **Security control**, **Creation time**, and **Status in DBW**.<br><br>The fields in the instance list support customization, so the fields displayed in the list may vary. |
|Customize list fields |In the upper right area of the list, click the ⚙️ icon. In the **Customize list fields** dialog, you can customize and select the fields to be displayed in the list.<br><br><br>* The default resources in the instance list include **Instance name/ID**, **Database type**, **Security control**, **Automatic inspection**, **Primary node availability zone**, **Instance type**, **Database version**, **Projects**, **Creation time**, and **Status in DBW**.<br><br>* Grayed\-out fields indicate non\-editable fields. |
|Enabling security control |DBW supports unified management of database instances. Enabling security control allows database changes to go through a ticket approval workflow, simplifying and standardizing database management operations and improving data management processes. For specific operations and precautions for enabling security control, please refer to the enable security control features of the respective databases below.<br><br><br>* [Enable security control for a MySQL connected over public network database](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql?lang=en)<br><br>* [Enable security control for a PostgreSQL connected over public network database](https://docs.byteplus.com/en/docs/DBW/enabling-security-control?lang=en) |
|Log on to the data interaction platform |Click **Log in** in the actions column of the target instance to log in to the instance's data interaction platform. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures.<br><br><br>* [Log in to the public network self-built MySQL console](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql?lang=en)<br><br>* [Log in to the public network self-built PostgreSQL console](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG?lang=en) |
|Edit instance details |You can edit added public network instances:<br><br><br>1. Select the target instance **Actions** \>  **...** , and click **Edit instance details**.<br><br>2. In the **Edit database instance** panel, edit the instance information as needed. For parameter details, see [Add external instance](https://docs.byteplus.com/en/docs/DBW/self-managed-database-administration?lang=en#Y3c2MPAv). |
|Remove DBW management |You can delete added public network instances:<br><br><br>1. Select the target instance, choose **Actions** \>  **...** , and click **Delete**.<br><br>2. In the **Delete instance** dialog box, click **OK**.<br><br><br>The deletion here only terminates DBW's management relationship with this instance and will not have any impact on the actual instance on the cloud platform. |
