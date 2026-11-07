---
title: "Database user management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/database-user-management"
---

ByteHouse Enterprise separates IAM sub\-users from database users, supports the independent creation of database users, and grants data privileges to these users. You can use a database user account to access the ByteHouse database via API, CLI, connection drivers, BI tools, IDE tools, and other methods. This tutorial explains how to create and manage database users.

<span id="5dcc4d81"></span>
# Background information

ByteHouse Enterprise currently supports managing ByteHouse privileges through IAM sub\-users or database users. The differences between the two are described below. Database users are part of the ByteHouse privilege model. For more information about users and the ByteHouse privilege model, see [Access control model](https://docs.byteplus.com/docs/bytehouse/privilege-model).


| |Sub\-user |Database users |
|---|---|---|
|Definition |A user created by the primary BytePlus user using the Identity and Access Management (IAM) Service. |Database\-level users created in ByteHouse. |
|Scope |Cluster or engine level |Database level |
|Login methods |* ByteHouse Enterprise Console<br><br>* API, connection drivers, command line, and ecosystem tool connections |API, connection drivers, command line, and ecosystem tool integrations |
|Use cases |Applicable to scenarios that require console operations, unified management across products, and similar situations. |Suitable for scenarios that require fine\-grained management of data access and operation privileges within the database. |


The procedure for creating and managing database users:


1. Create database users on the ByteHouse Enterprise Console.

2. Grant data privileges to database users.

3. Database users can access the ByteHouse database via the API, CLI, connection drivers, BI tools, IDE tools, and others.

4. If the database user is no longer being used, you can delete the database user.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f16f178a37a43c087e631870f494ba9~tplv-goo7wpa0wc-image.image) </span>

<span id="d312c32d"></span>
# Prerequisites

Only users with the SystemAdmin role can manage database users.

<span id="a01eded5"></span>
# Caution

A database user is a sub\-user who can be granted roles and database and table privileges, but cannot access the BytePlus Console.

<span id="b87d1b2e"></span>
# Create a database user


1. Log in to the ByteHouse Enterprise Console. On the **Access control** \> **User** page, click **Create new user** \> **Create Database User**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a968881a0f5a4007ba87aea5c64e8d96~tplv-goo7wpa0wc-image.image) </span>

2. On the Create Database User page, configure user information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13204e5799d7478a9503a04d7f8c1bb4~tplv-goo7wpa0wc-image.image) </span>

   
   |Param |Configuration description |
   |---|---|
   |**User** |Enter a custom username. The naming rules are as follows:<br><br><br>* The user name should start with a letter or an underscore, and can only contain uppercase and lowercase letters, numbers, hyphens, underscores, the at sign (@), and the period (.).<br><br>* You can enter up to 64 characters.<br><br>* The user name cannot be the same as an existing username. |
   |**Connection password** |The password for the database user must be set by the user. The password requirements are as follows:<br><br><br>* Length must be 8 to 30 characters;<br><br>* must contain uppercase letters A–Z;<br><br>* Must contain lowercase letters a to z. |
   |**Description** |Add a detailed description for the user; the description can be up to 200 characters long. |
   

3. After the user information is configured, click **Create**. After creation is complete, you can view user\-related information in the User list.


<span id="d0e57ae4"></span>
# Grant user privileges

<span id="c1d372b2"></span>
## Assign privileges through roles


1. Log in to the ByteHouse Enterprise Console. On the \*\*Access control \*\*\> **User** page, click the **User name** to go to the details page.

2. In the **Grant roles** module, click **Grant roles** to grant a role to the user. If you have not yet set up roles, you can refer to [Role management](https://docs.byteplus.com/docs/bytehouse/role-management).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39af086320d649ee8cbc163b34b85470~tplv-goo7wpa0wc-image.image) </span>

3. Select the scope for granting privilege, the roles to be granted, and adjust the Admin Option. The Admin Option privilege determines whether a user is allowed to grant the privileges they have been granted to other users.

   If you need to assign cluster role privileges for multiple clusters to a user, you can click **Add** to continue adding.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f754072c00654f48a0d409a8c2fbadd5~tplv-goo7wpa0wc-image.image) </span>

4. After adding a role, click **Submit**. The role authorization will take effect immediately, and you can view the granted privileges in the **Granted roles**, **User profile**, and **Privileges**.

5. (Optional) After authorization, if you need to adjust the role privileges granted to the user, you can click **Edit** in the **Grant roles** module. After making adjustments, click **Submit**.

   The following privileges can be adjusted:

   * Adjust the cluster scope, corresponding roles, and Admin Option that have already been granted.

   * Click **Add to** to keep adding clusters and authorizing roles.

   * To delete cluster authorization, hover the mouse over the corresponding cluster row and click the **Delete** button.


<span id="72acee90"></span>
## Grant privileges directly


1. Log in to the ByteHouse Enterprise Console. On the **Access control** \> **User** page, click the **User name** to view the details page.

2. Scroll to the bottom of the page. In the **Privileges** settings, click **Grant privileges directly**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5d6b268df27427d87904d45e5126e0b~tplv-goo7wpa0wc-image.image) </span>

3. On the Authorization page, select the type of data privilege to grant, the associated cluster, database, and privilege point. To grant privileges for multiple databases, click **Add** to continue adding databases and privileges. For details on privilege specifications, please refer to [Description of grantable database and table privileges](https://docs.byteplus.com/docs/bytehouse/privilege-model#e75a2c67).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57e4124750b74b84b759b50f937da508~tplv-goo7wpa0wc-image.image) </span>

4. After privileges have been added, click **Confirm**. The authorization will take effect immediately, and you can view the granted privileges under the Direct Authorization tab in User Param \> Privilege.

5. (Optional) After authorization, if you need to adjust the granted privileges, adjust the authorization in the **Privileges** module. Privileges that can be adjusted are as follows:

   * Add authorization: Click **Grant privileges directly**, and refer to Step 3 and Step 4.

   * Revoke privileges

      * Method 1: Expand the cluster and database, then click the **Delete** button next to the database to remove the corresponding database privilege.

      * Mode 2: Click **Revoke privileges directly**. In the popup window, select type, cluster, database, and privilege, and click **Confirm**.


<span id="7ccc24ae"></span>
# Reset the password


1. In the user list, click the **Reset password** button in the actions column for the username.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75e08b5c9caa4ef08167882486f2ea47~tplv-goo7wpa0wc-image.image) </span>

2. In the popup window, enter and confirm the new password.

3. Click **Confirm** to complete the password reset.


<span id="6feddb7f"></span>
# Delete a database user


1. In the User list, click the **Delete** button in the Actions column for the corresponding username.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38031b42e88442f78d2ff8e3efa583ac~tplv-goo7wpa0wc-image.image) </span>

2. Click **Confirm** to delete the current user.


<span id="d0033cc7"></span>
# Next steps: Use a database user to connect to ByteHouse

You can use a database user and password to connect to the ByteHouse database through API, CLI, drivers, BI tools, IDE tools, and other methods. For operation details, please refer to the following documents:


|Connection Methods |Related Document |
|---|---|
|API |[API reference](https://docs.byteplus.com/en/docs/bytehouse/api-reference) |
|CLI |[ClickHouse Client](https://docs.byteplus.com/docs/bytehouse/clickhouse-client) |
|Connection drivers |* [JDBC](https://docs.byteplus.com/docs/bytehouse/jdbc)<br><br>* [Python Driver](https://docs.byteplus.com/docs/bytehouse/python-driver)<br><br>* [Go Driver](https://docs.byteplus.com/docs/bytehouse/go-driver)<br><br>* [PHP Driver](https://docs.byteplus.com/docs/bytehouse/php-driver)<br><br>* [Flink Connector](https://docs.byteplus.com/docs/bytehouse/flink-connector)<br><br>* [Spark Connector](https://docs.byteplus.com/docs/bytehouse/spark-connector)<br><br>* [MySQL SQLAlchemy Conncetor](https://docs.byteplus.com/docs/bytehouse/mysql-sqlalchemy-conncetor-cdw) |
|BI tools |* [Metabase](https://docs.byteplus.com/docs/bytehouse/metabase)<br><br>* [Apache Superset](https://docs.byteplus.com/docs/bytehouse/apache-superset) |
|IDE tools |* [DataGrip](https://docs.byteplus.com/docs/bytehouse/datagrip) |
