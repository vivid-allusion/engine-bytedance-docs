---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/access-control-overview"
---

ByteHouse Cloud Data Warehouse offers flexible access control capabilities. Combined with the BytePlus Access Control (IAM) product, it enables access control at the product level and environment level for sub\-users. This article introduces the access control capabilities of ByteHouse Cloud Data Warehouse.

<span id="2aae98e5"></span>
# Access control overview

When managing access in ByteHouse Cloud Data Warehouse, you need to first create IAM sub\-users in access control, grant them product access, and then use ByteHouse's role access control to grant granular ByteHouse access, as shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a99778b2e52546e786670920a9af4907~tplv-goo7wpa0wc-image.image) </span>

<span id="59c49524"></span>
## IAM sub\-users and IAM access strategies

ByteHouse users originate from the BytePlus account system, which means you need to first create BytePlus IAM users in BytePlus Access Control (IAM), grant them the ByteHouse Cloud Data Warehouse IAM Strategy, and only then can these users become ByteHouse Cloud Data Warehouse users.

ByteHouse access supported by IAM Include:


* **ByteHouseFullAccess**: Full operational access for ByteHouse (excluding unsubscribed).

* **ByteHouseReadOnlyAccess**: Users can access the ByteHouse Console, enter the console, view the Virtual warehouse page, but are unable to view databases, tables, and other resources and data. IAM users with this type of access need to subsequently carry on fine\-grained access control through the ByteHouse console, granting **resource access** and **data access** to access specific database tables.

* **Custom privilege policy**: You can also create and configure a custom policy to grant IAM users the privileges of the ByteHouse AccountAdmin or SystemAdmin role, and define privileges with granular control.


<span id="579daba7"></span>
### Database users and privileges

Database users must be created by ByteHouse Cloud Data Warehouse accounts with the SystemAdmin or AccountAdmin role, and granted environment, resource, and data permissions so that the user can access and use the environment, resources, and data resources of ByteHouse Cloud Data Warehouse.

Permissions that can be granted to database users include:


* **Environment permissions**: Usage permissions for the default `default` environment and other granted environments.

* **Resource permissions**: Usage permissions for the default virtual warehouse, default write virtual warehouse, and other granted virtual warehouses.

* **Data permissions**: CRUD (Create, Read, Update, Delete) permissions for granted data resources (including databases, tables, views, materialized views, and dictionaries).


<span id="1affd4ab"></span>
## ByteHouse RBAC access model

When carrying out fine\-grained access control on the ByteHouse console, you can first authorize the ByteHouse environment. Resource access and data access in each environment can be controlled by user roles, that is, the fine\-grained access model within the ByteHouse environment is the RBAC access model.

<span id="7842b90a"></span>
### Roles

ByteHouse provides you with default system roles, and you can also create custom roles according to business needs, enabling flexible control of access for roles.


|Role Type |Access Description |
|---|---|
|System Default Roles |* AccountAdmin: The default role of the main account, not authorized for any sub\-users.<br><br>* SystemAdmin: Scope of authority is equivalent to ByteHouseFullAccess IAM strategy, enabling sub\-users with this role to have all operational access of ByteHouse (excluding unsubscribing). |
|Custom Roles |Created internally in ByteHouse Cloud Data Warehouse, it gives necessary access over ByteHouse Cloud Data Warehouse resources and data to the role, with detailed provisions for resource and data access as mentioned below. |


<span id="4bd0791d"></span>
### Access points


|Resource access |Data access |
|---|---|
|Supports managing access settings for resources such as databases, data loading, virtual warehouses, and more, including:<br><br><br>* Create Database<br><br>* Data Loading Management<br><br>* Virtual Warehouse Management |Supports setting granular access for databases, tables, views, materialized views, and dictionary dimensions. Data access settings vary for different objects and mainly include:<br><br><br>* ALTER<br><br>* CREATE<br><br>* DROP<br><br>* GET<br><br>* INSERT<br><br>* OPTIMIZE<br><br>* SELECT<br><br>* SHOW<br><br>* TRUNCATE |


<span id="b2dfd494"></span>
# Authorization Operation Guidelines

No matter who the user is, the principle of access control is the "minimum access distribution" principle: only allocate the necessary access needed for the user's activities.


* General Operation Guidelines: [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management), [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration), [Data privilege management](https://docs.byteplus.com/docs/bytehouse/docs-permission), [Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management).

* Best Practice: [Best practices for access control](https://docs.byteplus.com/docs/bytehouse/best-practice-for-access-control).
