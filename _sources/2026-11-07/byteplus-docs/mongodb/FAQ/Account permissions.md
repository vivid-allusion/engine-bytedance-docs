---
title: "Account permissions"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/account-and-permission"
---

This topic summarizes account and permission FAQs for Document Database for MongoDB.

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5b2T5YmN5o-Q5L6b5LqG5ZOq5Lqb6KeS6Imy5p2D6ZmQ77yf"></span>
### What account permissions does Document Database for MongoDB currently provide?

Document Database for MongoDB provides the following account permissions. For more details about account permissions, refer to [Database and account permissions](https://docs.byteplus.com/en/docs/mongodb/account-overview).


|Permission type |Permission name |Permissions description |
|---|---|---|
|Administrator operation permission |dbAdmin |Permission to perform management operations on database objects, but not read/write operations on the database. |
||userAdmin |Permission to create users on this database. |
||dbOwner |Permission to perform all operations on this database. |
|Cluster operation permission |clusterMonitor |Permissions to query clusters and replica sets. |
|Ordinary operation permission |read |Permission to perform query operations on this database. |
||readWrite |Permission to perform add, delete, modify, query operations on this database. |
|Instance operation permission |readAnyDatabase |Permission to query all databases in this instance. |
||readWriteAnyDatabase |Permissions to create, delete, modify, and query all databases in this instance. |
||userAdminAnyDatabase |Permissions to create users on all databases in this instance. |
||dbAdminAnyDatabase |dbAdmin permissions for all databases in this instance. |
|Backup operation permission |backup |Permission to perform backup operations on all databases in this instance. |


<span id=".5a6e5L6L5Yib5bu65aW95ZCO77yM5oCO5LmI5bey57uP5pyJ6LSm5Y-35LqG77yf"></span>
### Why is there already an account after instance created?

When you create a MongoDB instance, the system creates a root account with the built\-in root permission of MongoDB in the admin database by default.

You can set the root account and password when [Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance). You can also set the password for the root account after the instance is created. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-root-account).

<span id=".5aaC5L2V5Yib5bu6LW1vbmdvZGIt5pWw5o2u5bqT6LSm5Y-377yf"></span>
### How to create MongoDB database account?

Document Database for MongoDB automatically creates an account with root permissions in the admin database by default. You can also create accounts with other permissions to give users specific permission for specific databases. For specific procedures, refer to [Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account).

<span id=".5aaC5L2V5Li65a2Q55So5oi36L-b6KGM6Leo5pyN5Yqh6K6_6Zeu5o6I5p2D77yf"></span>
### How to authorize cross\-service access for IAM users?

Before using Document Database for MongoDB, you need to authorize cross\-service access to allow Redis instances to access other services (such as VPC and EIP). For specific procedures, refer to [Cross-service access authorization](https://docs.byteplus.com/en/docs/mongodb/cross-service-access-authorization).

If you need to authorize cross\-service access for IAM users, the IAM users must have the `IAMFullAccess` permissions, otherwise an error will occur during authorization. For more information on how to authorize IAM users, refer to [About users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-users).

<span id=".5aaC5L2V5L-u5pS5LW1vbmdvZGIt5pWw5o2u5bqT6LSm5Y-355qE5a-G56CB77yf"></span>
### How to change password of MongoDB database account?

You can choose any of the following methods to change database account password:


* **Modify via MongoDB console**

   For specific procedures on modifying account passwords via the MongoDB console, refer to [Modifying password](https://docs.byteplus.com/en/docs/mongodb/reset-password) or [Reset root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account).

* **Modify via API**

   You can call the [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) API to modify the password of a specified account in the target MongoDB instance.

* **Modify via ** **`db.changeUserPassword()`**  ** command**

   You can use the `db.changeUserPassword()` command to modify the password of a specified account (including root accounts and self\-created accounts). For specific usage, refer to [db.changeUserPassword()](https://www.mongodb.com/docs/v4.0/reference/method/db.changeUserPassword/#db-changeuserpassword).


<span id=".5b2T6L-e5o6l5Liy5Lit6LSm5Y-35a-G56CB5YyF5ZCr5LqG54m55q6K5a2X56ym5pe277yM5Li65L2V5Lya5a-86Ie06L-e5o6l5aSx6LSl77yf"></span>
### Why do connections fail when account passwords in the connection string include special characters?

Document Database for MongoDB supports using `_#!@$%^&*()+=-` special characters in database account passwords. However, when you connect to a MongoDB instance via MongoDB shell tools or program code, some special characters may cause program ambiguity and cannot be recognized correctly, leading to connection failure. You need to escape these characters into their corresponding URL encodings before using them in the connection string for correct recognition.

Special characters that need to be escaped in the connection string and their corresponding URL encodings are shown in the table below.


|Special character |Escaped URL encoding |
|---|---|
|`!` |`%21` |
|`#` |`%23` |
|`$` |`%24` |
|`%` |`%25` |
|`@` |`%40` |
