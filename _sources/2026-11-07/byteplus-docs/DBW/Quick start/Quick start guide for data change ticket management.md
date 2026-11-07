---
title: "Quick start guide for data change ticket management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/getting-started-with-ticket-management"
---

This topic describes how to submit and approve a ticket on the Database Workshop (DBW) console as a DBW administrator and a DBW normal user.

<span id="prerequisites"></span>
## Prerequisites


* An RDS for MySQL instance is created and is in the running state. For more information, refer to [Creating RDS for MySQL instances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A sub\-account is created. 

* You have viewed your role on the DBW console. For more information, refer to [Viewing roles](https://docs.byteplus.com/en/docs/DBW/viewing-roles).


<span id="precautions"></span>
## Precautions

The procedure applies to RDS for MySQL instances.

<span id="procedure-for-dbw-system-administrators"></span>
## Procedure for DBW administrators

When you are added as a DBW administrator, you can perform the operations on the DBW console as described in the following table.


|**Procedure** |**Description** |
|---|---|
|1. Preparations |Log on to the DBW console as a DBW administrator or using the primary account of BytePlus. Alternatively, go to the **User management** page to add a sub\-account as a DBW administrator, and then log on to the DBW console using the sub\-account. For more information, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql). |
|2. [Adding ticket approvers](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql) |1. Log on to the DBW console using the sub\-account that is added as a DBW administrator.<br><br>2. On the **User management** page, add another BytePlus sub\-account as a DBW role, such as a DBW administrator or a DBW normal user, so that the sub\-account can serve as a ticket approver.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This user can serve as an instance owner, who is a tier\-1 ticket approver, or an instance DBA, who is a tier\-2 ticket approver, to enable security control for an instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Both the system administrator role and the normal user role can be set to an instance owner or an instance DBA. For more information on roles, refer to <a href="https://docs.byteplus.com/en/docs/DBW/role-description">Role description</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If both the instance owner and instance DBA are set to RootAccount when security control is enabled, you do not need to add a new user as a ticket approver.</div><br> |
|3. [Enabling security controls](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql) |1. Log on to the DBW console using the sub\-account that is added as a DBW administrator.<br><br>2. On the **Instance list** page, enable security control for the target instance. After security control is enabled for the instance, you can manage modifications to the database instance using tickets, implementing unified management of the instance. |
|4. [Adding ticket submitters](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql) |On the **User management** page, add a user for submitting tickets.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on roles, refer to <a href="https://docs.byteplus.com/en/docs/DBW/role-description">Role description</a>.</div><br> |
|5. [Authorizing ticket submitters](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql) |1. Log on to the DBW console using the sub\-account that is added as a DBW administrator.<br><br>2. On the **User management** page, grant required instance management permissions by instance, database, table, or column to the ticket submitter.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If a ticket approver needs to submit tickets, you must also grant the required instance management permissions to the ticket approver.</div><br> |
|6. Submitting tickets<br><br>* [Creating a SQL change ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-normal-sql-change-ticket-for-mysql)<br><br>* [Creating a structural change ticket (OnlineDDL ticket)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql) |Before making SQL or structural modifications to a database instance for which security control is enabled, the ticket submitter must submit a ticket and obtain approval from the ticket approver. To submit a ticket:<br><br><br>1. Log on to the DBW console using the sub\-account that is added as a DBW administrator.<br><br>2. On the **Ticket list** page, submit a ticket. |
|7. [Approving tickets as an approver](https://docs.byteplus.com/en/docs/DBW/ticket-management-for-mysql) |System administrators can view and approve pending tickets on the **Ticket list** page. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A primary account assumes the system administrator role on the DBW console by default, having all the permissions for the DBW.</div>


<span id="procedure-for-dbw-normal-users"></span>
## Procedure for DBW normal users

When you are added as a DBW normal user, you can perform the following operations on the **Ticket list** page:


* Submit a ticket

   
   |**Procedure** |**Description** |
   |---|---|
   |1. Preparations |Make sure that you are using a primary account of BytePlus or a sub\-account added as a DBW administrator. Then, make preparations as follows:<br><br><br>1. Log on to the DBW console and enable security control for the target instance. For more information, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).<br><br>2. Add a sub\-account as a DBW normal user. For more information, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).<br><br>3. Grant the DBW normal user the permissions to enable security control for an instance. For more information, refer to [Granting permissions to a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql). |
   |2. Submitting tickets<br><br>* [Creating a SQL change ticket](https://docs.byteplus.com/en/docs/DBW/creating-a-normal-sql-change-ticket-for-mysql)<br><br>* [Creating a structural change ticket (OnlineDDL ticket)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql) |Before making SQL or structural modifications to a database instance for which security control is enabled, the ticket submitter must submit a ticket and obtain approval from the ticket approver. To submit a ticket **:** <br><br><br>1. Log on to the DBW console using the sub\-account that is added as a DBW normal user.<br><br>2. On the **Ticket list** page, submit a ticket. |
   

* Approve a ticket

   
   |**Procedure** |**Description** |
   |---|---|
   |1. Preparations |Make sure that you are using a primary account of BytePlus ** or ** a sub\-account added as a DBW administrator. Then, make preparations as follows:<br><br><br>1. Log on to the DBW console and enable security control for the target instance. For more information, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).<br><br>2. Add a sub\-account as a DBW normal user. For more information, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql). |
   |2. [Approving tickets](https://docs.byteplus.com/en/docs/DBW/ticket-management-for-mysql) |If a primary account or a DBW administrator role sets the DBW normal user as an instance DBA or instance owner when enabling security control, you can also view and approve pending tickets on the **Ticket list** page. |
   


&nbsp;
