---
title: "User and permission management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/User_and_permission_management"
---

This article describes how to manage users, roles, and permissions in StarRocks (version 3x).

StarRocks uses both role\-based access control (RBAC) and identity\-based access control (IBAC) to manage permissions within the cluster, allowing cluster administrators to easily restrict permissions at different levels of granularity.

In a StarRocks cluster, you can grant permissions to users or roles. A role is a set of permissions that can be granted to users or roles within the cluster as needed. A user or role can be granted one or more roles, which determine their permissions for different objects.

<span id="_1-查看用户和角色信息"></span>
## View user and role information

Users with the system pre\-set role `user_admin` can view information about users and roles in the StarRocks cluster.

<span id="_1-1-查看权限信息"></span>
### View permission information

You can use [SHOW GRANTS](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/SHOW_GRANTS/) to view the permissions granted to users or roles.


* View the permissions of the current user.


```sql
SHOW GRANTS;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Any user can view their own privileges without requiring any privileges.</div>


* View the permissions of a specific user.

* The following example shows the permissions of user `jack`.


```sql
SHOW GRANTS FOR jack@'{客户端IP}';
```



* View the permissions of a specific role.

* The following example shows the permissions of role `example_role`.


```sql
SHOW GRANTS FOR ROLE example_role;
```


<span id="_1-2-查看用户属性"></span>
### View user properties

You can use [SHOW PROPERTY](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/SHOW_PROPERTY/) to view user properties.

The following example shows the properties of user `jack`:

```sql
SHOW PROPERTY FOR jack@'{客户端IP}';
```


<span id="_1-3-查看角色"></span>
### View roles

You can use [SHOW ROLES](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/SHOW_ROLES/) to view all roles in the StarRocks cluster.

```sql
SHOW ROLES;
```


<span id="_1-4-查看用户"></span>
### View users

You can use SHOW USERS to view all users in the StarRocks cluster.

```sql
SHOW USERS;
```


<span id="_2-管理用户"></span>
## Manage users

Users with the system pre\-set role `user_admin` can create, modify, and delete users in StarRocks.

<span id="_2-1-创建用户"></span>
### Create users

You can create users by specifying user identity, authentication method, and default role.

StarRocks supports user authentication via password login or LDAP authentication. For more information about StarRocks authentication methods, see [User authentication](https://docs.starrocks.io/zh/docs/administration/user_privs/Authentication/). For more instructions on creating users, see [CREATE USER](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/CREATE_USER/).

The following example creates user `jack`, allows connections only from IP address `{客户端IP}`, sets their password to `xxxxx`, and assigns the role `example_role` as their default role:

```sql
CREATE USER jack@'{客户端IP}' IDENTIFIED BY '{password}' DEFAULT ROLE 'example_role';
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">StarRocks encrypts user passwords before storing them. You can use the password() function to obtain the encrypted password.</div>


* <div data-tips="true" data-tips-type="tip">If no default role is specified during user creation, StarRocks assigns the system preset role <code>PUBLIC</code> as the user's default role.</div>



<span id="_2-2-修改用户"></span>
### Modify users

You can modify a user's password, default role, or properties.

When a user connects to StarRocks, their default role is automatically activated. For instructions on how to enable all roles (default and granted) for a user after connecting, see [启用所有角色](https://docs.byteplus.com/docs/E-MapReduce/109501#%E5%90%AF%E7%94%A8%E6%89%80%E6%9C%89%E8%A7%92%E8%89%B2).

<span id="_2-2-1-修改用户默认角色"></span>
#### Modify a user's default role

You can use [SET DEFAULT ROLE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/SET_DEFAULT_ROLE/) or [ALTER USER](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/ALTER_USER/) to set a user's default role.

The following two examples both set `jack`'s default role to `db1_admin`. Before setting, make sure the `db1_admin` role has already been granted to `jack`.


* Set the default role using SET DEFAULT ROLE:


```sql
SET DEFAULT ROLE 'db1_admin' TO jack@'{客户端IP}';
```



* Set the default role using ALTER USER:


```sql
ALTER USER jack@'{客户端IP}' DEFAULT ROLE 'db1_admin';
```


<span id="_2-2-2-修改用户属性"></span>
#### Modify a user's properties

You can use [SET PROPERTY](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/SET_PROPERTY/) to set a user's properties.

User identities with the same username share the same property. In the following example, simply configure the property for `jack`, and the property configuration will apply to all user identities with the username `jack`.

Set the maximum number of connections for user `jack` to `1000`:

```sql
SET PROPERTY FOR jack 'max_user_connections' = '1000';
```


<span id="_2-2-3-重置用户密码"></span>
#### Reset a user's password

You can use [SET PASSWORD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/SET_PASSWORD/) or [ALTER USER](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/ALTER_USER/) to reset a user's password.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Any user can reset their own password without requiring any privileges.</div>


* <div data-tips="true" data-tips-type="tip">The password of the <code>root</code> user can only be reset by the <code>root</code> user themselves. If you lose your password and cannot connect to StarRocks, refer to <a href="https://docs.byteplus.com/docs/E-MapReduce/109501#%E9%87%8D%E7%BD%AE%E4%B8%A2%E5%A4%B1%E7%9A%84-root-%E5%AF%86%E7%A0%81">重置丢失的 root 密码</a>.</div>



The following two examples both reset `jack`'s password to `54321`:


* Reset the password using SET PASSWORD:


```sql
SET PASSWORD FOR jack@'{客户端IP}' = PASSWORD('54321');
```



* Reset the password using ALTER USER:


```sql
ALTER USER jack@'{客户端IP}' IDENTIFIED BY '54321';
```


<span id="_2-2-4-重置丢失的-root-密码"></span>
#### Reset a lost root password

To reset the root user's password if you have lost it and cannot connect to StarRocks, follow these steps:


1. Add the following configuration item to the configuration file **fe/conf/fe.conf** on **all FE nodes** to disable user authentication:


```yaml
enable_auth_check = false
```



2. Restart **all FE nodes** to apply the configuration.


```bash
./fe/bin/stop_fe.sh
./fe/bin/start_fe.sh
```



3. Use the `root` user to connect to StarRocks from the MySQL client. When user authentication is disabled, you can log in without a password.


```bash
mysql -h <fe_ip_or_fqdn -P<fe_query_port -uroot
```



4. Reset the `root` user's password.


```sql
SET PASSWORD for root = PASSWORD('xxxxxx');
```



5. In the configuration file **fe/conf/fe.conf** on **all FE nodes**, set the configuration item `enable_auth_check` to `true` to re\-enable user authentication.


```yaml
enable_auth_check = true
```



6. Restart **all FE nodes** to apply the configuration.


```bash
./fe/bin/stop_fe.sh
./fe/bin/start_fe.sh
```



7. Use the `root` user and the new password to connect to StarRocks from the MySQL client to verify that the password has been successfully reset.


```bash
mysql -h <fe_ip_or_fqdn -P<fe_query_port -uroot -p<xxxxxx
```


<span id="_2-3-删除用户"></span>
### Delete a user

You can use [DROP USER](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/DROP_USER/) to delete a user.

The following example deletes the user `jack`:

```sql
DROP USER jack@'{客户端IP}';
```


<span id="_3-管理角色"></span>
## Manage roles

Users with the system preset role `user_admin` can create, grant, revoke, and delete roles in StarRocks.

<span id="_3-1-创建角色"></span>
### Create a role

You can use [CREATE ROLE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/CREATE_ROLE/) to create a role. By default, each user can have up to 64 roles. You can also adjust this limit as needed by using the FE dynamic parameter `privilege_max_total_roles_per_user`. The nesting relationship of roles can be up to 16 levels deep. You can also adjust this by using the FE dynamic parameter `privilege_max_role_depth`.

The following example creates the role `example_role`:

```sql
CREATE ROLE example_role;
```


<span id="_3-2-授予角色"></span>
### Grant roles

You can use [GRANT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/GRANT/) to grant roles to users or other roles.


* Grant a role to a user.

* The following example grants the role `example_role` to the user `jack`:


```sql
GRANT example_role TO USER jack@'{客户端IP}';
```



* Grant a role to another role.

* The following example grants the role `example_role` to the role `test_role`:


```sql
GRANT example_role TO ROLE test_role;
```


<span id="_3-3-撤销角色"></span>
### Revoke roles

You can use [REVOKE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/REVOKE/) to revoke roles from users or other roles.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The system preset default role <code>PUBLIC</code> cannot be revoked.</div>


* <div data-tips="true" data-tips-type="tip">Revoke a role from a user.</div>


* <div data-tips="true" data-tips-type="tip">The following example revokes the role <code>example_role</code> from user <code>jack</code>:</div>



```sql
REVOKE example_role FROM USER jack@'{客户端IP}';
```



* Revoke a role from another role.

* The following example revokes the role `example_role` from the role `test_role`:


```sql
REVOKE example_role FROM ROLE test_role;
```


<span id="_3-4-删除角色"></span>
### Delete roles

You can use [DROP ROLE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/DROP_ROLE/) to delete roles.

The following example deletes the role `example_role`:

```sql
DROP ROLE example_role;
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">System preset roles cannot be deleted.</div>


<span id="_3-5-启用所有角色"></span>
### Enable all roles

A user's default roles are automatically activated each time the user connects to the StarRocks cluster. Permissions granted to a role take effect only after they are granted.

To have all users in the cluster automatically activate all roles (both default and granted roles) upon login, perform the following operation. This operation requires OPERATE permission at the system level.

Run the following statement to enable all roles for users in the cluster:

```sql
SET GLOBAL activate_all_roles_on_login = TRUE;
```


You can also manually activate owned roles by using SET ROLE. For example, the user jack@'{client IP}' has the roles `db_admin` and `user_admin`, but these roles are not their default roles, so they are not automatically activated upon login. When jack@'{client IP}' needs to activate `db_admin` and `user_admin`, they can manually execute `SET ROLE db_admin, user_admin;`. Caution: The SET ROLE command is overriding. To activate all owned roles, execute SET ROLE ALL.

<span id="_4-管理权限"></span>
## Manage privileges

Users with the system built\-in role `user_admin` can grant and revoke privileges in StarRocks.

<span id="_4-1-授予权限"></span>
### Grant privileges

You can use [GRANT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/GRANT/) to grant privileges to users or roles.


* Grant privileges to a user.

* The following example grants SELECT privilege on the table `sr_member` to the user `jack`, and allows `jack` to grant this privilege to other users or roles (by specifying WITH GRANT OPTION in SQL):


```sql
GRANT SELECT ON TABLE sr_member TO USER jack@'{客户端IP}' WITH GRANT OPTION;
```



* Grant privileges to a role.

* The following example grants the SELECT privilege on table `sr_member` to the role `example_role`:


```sql
GRANT SELECT ON TABLE sr_member TO ROLE example_role;
```


<span id="_4-2-撤销权限"></span>
### Revoke privileges

You can use [REVOKE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/account-management/REVOKE/) to revoke privileges from a user or role.


* Revoke privileges from a user.

* The following example revokes the SELECT privilege on table `sr_member` from user `jack` and prevents `jack` from granting this privilege to other users or roles:


```sql
REVOKE SELECT ON TABLE sr_member FROM USER jack@'{客户端IP}';
```



* Revoke privileges from a role.

* The following example revokes the SELECT privilege on table `sr_member` from the role `example_role`:


```sql
REVOKE SELECT ON TABLE sr_member FROM ROLE example_role;
```
