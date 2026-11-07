---
title: "User profile"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/user-management"
---

To ensure data security while maintaining operational flexibility, Database Workshop (DBW ) provides two methods for managing BytePlus sub\-users added to DBW system roles: personal ** ** users and user groups.

<span id="LLbHxArC"></span>
## Background

BytePlus sub\-users can be added to DBW either as personal users or as members of user groups, with assignable roles as administrators or normal users. This permission structure enables primary accounts to implement granular access control.

In the DBW system, BytePlus sub\-users play important roles. When added as personal users, they can be granted specific operational permissions to perform relevant tasks independently. When added to user groups, centralized management and permission allocation can be achieved for multiple sub\-users.

Furthermore, when a BytePlus sub\-user is authorized as a DBW administrator, they obtain higher\-level privileges to perform comprehensive system management and configuration. When authorized as normal users, they can only perform operations within their assigned permission scope.

This flexible authorization mechanism enables primary accounts to implement more granular permission segregation. By assigning appropriate permissions based on different business needs and sub\-user responsibilities, it improves work efficiency, ensures data security, and achieves more standardized and orderly system management.

<span id="gthVrk33"></span>
## Precautions

Sub\-users not added to DBW user management are not recognized as individual users or user groups within DBW. Therefore, they do not support instance security control, passwordless login for the Data Interaction Console, or platform features such as user management, security control, and ticket lists. To ensure a full feature experience, we recommend adding BytePlus sub\-users to DBW's individual users or user groups.

<span id="9YCCx8L0"></span>
## **Difference comparison**


|Type |Personal user |User group |
|---|---|---|
|**Management approach** |Personal user management requires separate permission configuration for each account, offering granular control but increased complexity.  |User group management enables centralized permission assignment for all members, significantly simplifying administration. |
|**Permission assignment** |Permissions are granted directly to individual users. |Permissions are assigned to the user group and automatically inherited by all members. |
|**Application scenarios** |Personal user management suits cases requiring unique permission settings for specific users. |User group management applies when uniform permissions are needed across user groups, such as department\-wide or project\-based access control. |
|**Advantages** |* Precise control: Personal users receive customized permissions for specified demands |* Simplified administration: Centralized user group management reduces configuration overhead<br><br>* Flexible inheritance: Users joining multiple groups gain combined permissions through inheritance, meeting complex access requirements |


<span id="OdBNNsNS"></span>
## Role to permission mapping

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The table symbols represent the following:</div>



* <div data-tips="true" data-tips-type="tip">✔️ : The DBW role is authorized to configure DBW functionality.</div>


* <div data-tips="true" data-tips-type="tip">❌ : The DBW role is not authorized to configure DBW functionality.</div>




|Features ||Personal user ||Group user ||
|---|---|---|---|---|---|
|||**Administrator** |**Normal user** |**Administrator** |**Normal user** |
|**Instace list** |**Fuzzy search** |✔️ |✔️ |✔️ |✔️ |
||**Login to the data interaction platform** |✔️ |✔️ |✔️ |✔️ |
||**Login to observation and dignosis** |✔️ |✔️ |✔️ |✔️ |
||**Security control enabling** |✔️ |❌ |✔️ |❌ |
||**Automatic inspection enabling** |✔️ |✔️ |✔️ |✔️ |
|**Data management** |**Data interaction platform** |✔️ |✔️ |✔️ |✔️ |
||**User management** |✔️ |❌ |✔️ |❌ |
||**Security rules** |✔️ |❌ |✔️ |❌ |
||**Ticket list** |✔️ |✔️ |✔️ |✔️ |
||**Task management** |✔️ |✔️ |✔️ |✔️ |
||**My permissions** |✔️ |✔️ (Application entry only) |✔️ |✔️ (Application entry only) |
||**Approval workflow** |✔️ |❌ |✔️ |❌ |
||**Action trail** |✔️ |✔️ (View own actions only) |✔️ |✔️ (View own actions only) |
|**Operation and maintenance management** |**Session management** |✔️ |✔️ |✔️ |✔️ |
||**Slow log analysis** |✔️ |✔️ |✔️ |✔️ |
||**Audit logs** |✔️ |✔️ |✔️ |✔️ |
||**Space analysis** |✔️ |✔️ |✔️ |✔️ |
||**Transaction and lock** |✔️ |✔️ |✔️ |✔️ |
||**One\-click diagnosis** |✔️ |✔️ |✔️ |✔️ |
||**Performance monitoring** |✔️ |✔️ |✔️ |✔️ |
||**Full SQL insight** |✔️ |✔️ |✔️ |✔️ |
||**Automated operation and maintenance** |✔️ |✔️ |✔️ |✔️ |
||**Database inspection** |✔️ |✔️ |✔️ |✔️ |
