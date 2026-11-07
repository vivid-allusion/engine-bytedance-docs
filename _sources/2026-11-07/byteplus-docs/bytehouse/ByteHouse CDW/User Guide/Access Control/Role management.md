---
title: "Role management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-access-control-administration"
---

ByteHouse Cloud Data Warehouse primarily uses an RBAC access control model for fine\-grained control over resources and data through Roles. This tutorial introduces the role management capabilities in ByteHouse, and how to customize roles, and manage role privileges and revocation.

<span id="f8619412"></span>
# Background

<span id="f220dd13"></span>
## General concept


|Terminology |Concept Description |
|---|---|
|Privileges |All actions executable within ByteHouse have defined privileges. For example: Viewing account resource usage, creating new users, querying data from a table, or loading large datasets into ByteHouse.<br><br>Privileges related to specific resources, such as creating tables (related to databases), inserting new data (related to tables), and running virtual warehouses (related to warehouses), are tied to specific resource instances or objects.<br><br>Other privileges, such as creating databases (note: databases are account\-level resources), viewing billing status, or creating new service users, are not bound to any specific object. |
|Roles |Access control in ByteHouse is performed at the role level. Every ByteHouse user can acquire one or more roles. |


For more details about the access control logic and concepts of ByteHouse, refer to [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview).

<span id="f12dd68d"></span>
## Built\-in roles and custom roles

ByteHouse provides default system roles, and you can also create custom roles based on business needs for flexible permission control.


|Role Type |Privileges |
|---|---|
|Default System Roles |* **AccountAdmin**: The default role for the main account in ByteHouse and the root role for the ByteHouse account, not authorized for other sub\-users.<br><br>* **SystemAdmin**: This is a direct sub\-role of the account administrator. Users with this role will have permission to all platform resources, such as databases, tables, virtual warehouses, and online spreadsheets. The scope of privileges is equivalent to the ByteHouseFullAccess IAM strategy. Sub\-users can be granted this role, and they will have all operational privileges in ByteHouse (excluding unsubscribing). |
|Custom Roles |In the ByteHouse Cloud Data Warehouse, custom roles can be created that grant necessary permissions to ByteHouse Cloud Data Warehouse resources and data. |


In the AccountAdmin role, you can click on "Access Control \> Roles" in the top navigation bar to view all available roles in the account.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c7e3d6e6afa4a68b4728a8cb90c5ae1~tplv-goo7wpa0wc-image.image) </span>

<span id="3871ee8b"></span>
# Caution

Only the main account or the sub\-account with the SystemAdmin or AccountAdmin role and the privilege to access the ByteHouse console can create roles, authorize roles, and perform related operations in the ByteHouse console.

<span id="bda669e9"></span>
# Create a custom role

If your business organization is complex and built\-in roles do not meet your access control needs, you can create appropriate custom roles for each business team according to the actual situation on the role management page by clicking "**Create Role**".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6db428963714d89a3d763bac0274705~tplv-goo7wpa0wc-image.image) </span>

<span id="627bbd99"></span>
# Set role privilege scope

After creating a custom role, you can go to the "Access Control \- Roles" page, click to enter the details of a specific role, and grant **Resource privileges** and **Data privileges** to the role.

<span id="6c3514f1"></span>
## Resource privileges

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d29c2461360d4629b9abdc69c8f112cc~tplv-goo7wpa0wc-image.image) </span>


|Resource Privilege Details |Privilege Configuration Description |
|---|---|
|Create database |Once the toggle is enabled, a role will have the privileges to create databases and browse the entire list of databases. |
|Create external catalog |Once the toggle is enabled, a role will have the privileges to create, delete, and view external catalogs. |
|Data loading management |Once the toggle is activated, a role will acquire full access to the data import module, including creating, editing, and deleting import tasks, as well as creating and deleting data sources. |
|Knowledge base management |Once the toggle is enabled, a role will have the privileges to create, view, and manage knowledge bases. |
|Virtual warehouse management |Custom roles are granted default view permissions for virtual warehouses. Depending on the situation, you can set whether the roles have USE, ALL permissions for virtual warehouses, and also determine whether the controlled compute scope is a specific one or all warehouses.<br><br><br>* VIEW: Allows a role to view virtual warehouses and query history.<br><br>* USE: Allows a role to query with the virtual warehouse and restores the virtual warehouse when "Automatic Restore" is enabled.<br><br>* ALL: Grants a role with all virtual warehouse privileges. |
|Global audit log |After enabling the switch, this role will have the privilege to view global audit logs, including SQL history, running queries, permission audits, virtual warehouse audits, and user activities. Sub\-users assigned this role can directly view the global audit log information of all sub\-users. |


<span id="06c0f056"></span>
## Data privileges

It supports setting Allow dotted for global, database, table, view, materialized view, dictionaries, external catalog, and UDF.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ade620cad0b4eeda6887a9fc0386bfe~tplv-goo7wpa0wc-image.image) </span>


|Data privilege |Privilege description |
|---|---|
|Global |Select the privileges to grant. After granting global privileges, all data objects in the environment will be granted the selected privileges. |
|Database |Select the database to be authorized, and grant database privileges. |
|Table |Select the databases to be authorized and their associated tables, and grant table privileges. |
|View |Select the databases and their subordinate views that require authorization, and grant view privileges. |
|Materialized view |Select the databases and their subordinate materialized views that require authorization, and grant privileges for the materialized views. |
|Dictionary |Select the databases and their subordinate dictionaries to grant privileges, and assign privileges to the dictionaries. |
|UDF |Select UDF privileges to be granted. |
|External catalog |Select the external catalog to authorize, and grant the corresponding privileges. |


<span id="5ea1f974"></span>
# Grant roles to users

After completing the role privilege settings, you can go to the role details page, click "**Grant users**". Select a user from the dropdown, and authorize the role's privileges to the specified user.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f7869f4077746f69e8d47475bdfa730~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Here, default or custom roles can be assigned to specific BytePlus IAM sub\-users.</div>


After authorization, you can see which users the role has been authorized to in the **Gtanted Users** list within that role.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2268dbcefb9b41c994f5541a22083f0e~tplv-goo7wpa0wc-image.image) </span>

<span id="dd6e3626"></span>
# Revoke role privileges

You can click the role name on the Roles page, enter the role detail page, and under the '**Granted Users**' tab, click the **Revoke** button beside the user and confirm, to revoke the user's role assignment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfb961b42aa74e3db5a63807fdf400aa~tplv-goo7wpa0wc-image.image) </span>

<span id="c0f6ee81"></span>
# Related Documents


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Best practices for access control](https://docs.byteplus.com/docs/bytehouse/best-practice-for-access-control)
