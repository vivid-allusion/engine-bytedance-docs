---
title: "Permission Management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Permission_Management"
---

<span id="_1-概述"></span>
## Overview

On the permission management page, you can manage permissions for LAS objects such as Schema, Table, UDF, and resources, including functions for adding, displaying, editing, and deleting permissions. The smallest granularity of permission management is the role; a role can contain multiple fine\-grained permission points.

<span id="_2-前置条件"></span>
## Prerequisites

Prerequisites for authorizing a user/group in LAS permission management:


* The user/group must have been granted the relevant Policy in IAM and be able to access the LAS service.

* Users can only manage permissions for objects for which they have the Admin role.


<span id="_3-权限管理"></span>
## Permission Management

Data management consists of three levels: **Catalog, Schema** and **Table or Function (UDF)** . You can select these via the **Permission Management \- Data Authorization** page using the **Level** dropdown menu.

<span id="_3-1-权限列表"></span>
### Permission List

When you select a level, such as Database or Table, the corresponding metadata permission list is displayed. Exact search by user or user group name is also supported.

<span id="_3-2-新增授权"></span>
### Add Authorization


* Click **Add Authorization** in the upper right corner of the permission list to grant the corresponding permissions of a metadata object to a specified list of users.

* In the **Authorized Resource** section, you must first select an authorization scope; currently, database, table, and function are supported. Then, you can select a specific metadata object from the dropdown list.

* In the **Authorized Principal** section, select the target to be granted permissions by searching; currently, user and user group are supported, and fuzzy search is available.

* In the **Grant Permission** section, select a specific **Permission Role**. Each permission role contains a set of permission packages; see the permission description section below for details.


<span id="90b9f014"></span>
### Edit Permission

If the grantee already has a permission role, duplicate granting is not allowed. You can find the authorization record in permission management and click edit to change the user's role.

<span id="2aa49d44"></span>
### Delete Permission

In the authorization list, you will see a delete button. If you do not want the user to continue having permissions for databases, tables, or functions, you can delete them directly.

<span id="_3-3-权限说明"></span>
### Permission Description

Different levels of metadata correspond to different permission points and roles, as well as their relationships. Details are as follows:


* Database (Schema) Level



|**Permission Point** ||**Permission Role** |||||||
|---|---|---|---|---|---|---|---|---|
|**Permission Name** |**Description** |**Admin** |**Developer** |**Viewer** |**Create** |**Read** |**Drop** |**Write** |
|CreateTable |Permission to create tables and views within the database |✔️ |✔️ | |✔️ | | | |
|CreateFunction |Permission to create functions within the database |✔️ |✔️ | |✔️ | | | |
|CreateResource |Permission to create resources within the database |✔️ |✔️ | |✔️ | | | |
|Describe |Read database metadata |✔️ |✔️ |✔️ | |✔️ | | |
|Select |Select permission on all tables within the database |✔️ |✔️ |✔️ | |✔️ | | |
|Insert |Insert permission on all tables within the database |✔️ |✔️ | | | | |✔️ |
|Show |List all objects in the database, including tables, resources, functions, instances, etc. |✔️ |✔️ |✔️ | |✔️ | | |
|Drop |Delete database |✔️ | | | | |✔️ | |
|Alter |Modify database information |✔️ | | | | | |✔️ |
|All |Has all the above permissions, including the permission to grant them |✔️ | | | | | | |



* Data Table (Table) Level



|**Permission Point** ||**Role** ||||||
|---|---|---|---|---|---|---|---|
|**Permission Name** |**Description** |**Admin** |**Developer** |**Viewer** |**Read** |**Drop** |**Write** |
|Describe |Read table metadata |✔️ |✔️ |✔️ |✔️ | | |
|Select |Read table data |✔️ |✔️ |✔️ |✔️ | | |
|Alter |Modify table metadata or add/delete partitions |✔️ |✔️ | | | |✔️ |
|Insert |Write/overwrite table data |✔️ |✔️ | | | |✔️ |
|Drop |Delete table |✔️ | | | |✔️ | |
|All |Has all the above permissions, including the permission to grant them |✔️ | | | | | |



* Function (UDF) Level



|**Permission Point** ||**Role** |||
|---|---|---|---|---|
|**Permission Name** |**Description** |**Admin** |**Developer** |**Viewer** |
|Read |Read function information |✔️ |✔️ |✔️ |
|Write |Update function |✔️ |✔️ | |
|Delete |Delete function |✔️ | | |
|Execute |Permission to execute function |✔️ |✔️ |✔️ |
|All |Has all the above permissions, including the permission to grant them |✔️ | | |
