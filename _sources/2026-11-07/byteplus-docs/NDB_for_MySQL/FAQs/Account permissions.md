---
title: "Account permissions"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Account_permissions_faq"
---

<span id="高权限账号和普通账号有什么区别？"></span>
### What is the difference between a super account and a normal account?

Super account: An instance can only create one super account, and can manage all normal accounts and databases. Normal account: An instance can create multiple normal accounts, and it is necessary to manually grant the permissions of a specific database to the normal account.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on account permissions, refer to <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Account_permission_description">Account permission description</a>.</div>


<span id="高权限账号能否在控制台修改指定权限？"></span>
### Can super accounts modify specific permissions in the console?

No. Super accounts inherently possess all permissions across all databases by default, and can only be reset to their initial state via the console. Permission modifications are only applicable to normal accounts.

<span id="一个数据库是否可以绑定多个账号？"></span>
### Can a database be associated with multiple accounts?

Yes.

<span id="使用-sql-为普通用户授予权限失败。"></span>
### Failed to grant permissions to a standard user via SQL.

Error:

```sql
mysql> GRANT SELECT, SHOW DATABASES, REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'test123';
ERROR 1045 (28000): Access denied for user 'admin_root'@'%' (using password: YES)
```


Granting `SHOW DATABASES` permission to standard users is not supported.

<span id="在-vedb-mysql-中使用-grant-命令直接创建用户授权失败了？"></span>
### Are you encountering `grant` command failures during user creation/authorization in NDB for MySQL?

**Error:** 

```sql
mysql> grant select,insert,update,delete on `testdb1`.`auth_role` to 'testuser'@'%';
ERROR 1410 (42000): You are not allowed to create a user with GRANT
```


This error occurs because community MySQL 8.0 no longer supports user creation via the grant command, as this feature has been deprecated. For details, refer to [MySQL documentation](https://dev.mysql.com/blog-archive/how-to-grant-privileges-to-users-in-mysql-80/).

**Solution:** 

Create a user, followed by authorization. The syntax reference is as follows:

```sql
-- Create user
mysql> create user 'testuser' identified by 'Root****';
Query OK,0 rows affected (0.01 sec)

-- Authorize
mysql> grant select,insert,update,delete on `testdb1`.`auth_role` to 'testuser';
Query OK,0 rows affected (0.00 sec)
```


<span id="如何查询某个实例，是由哪个账号创建的？"></span>
### How to query which account created a specific instance?

You can log on to the [Cloud Audit console](https://console.byteplus.com/cloudtrail/event) and query the instance's creator by selecting the corresponding event source and time range. For more information on cloud audit, refer to [Querying cloud audit logs](https://www.byteplus.com/en/docs/7015/166040#%E6%9F%A5%E8%AF%A2%E4%BA%91%E5%AE%A1%E8%AE%A1%E6%97%A5%E5%BF%97).
