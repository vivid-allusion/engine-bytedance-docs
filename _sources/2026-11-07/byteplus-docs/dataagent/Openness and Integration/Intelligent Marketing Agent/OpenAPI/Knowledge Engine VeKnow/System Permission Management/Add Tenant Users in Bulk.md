---
title: "Add Tenant Users in Bulk"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/add-tenant-users-in-bulk"
---

Call this interface to bulk add users to the current tenant.

# Interface description

* Interface name: add_tenant_users_permission_tenant_users_post

* Interface address:/permission/tenant/users

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|users |Array |Yes |List of users, see the **users** table below |

## users

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|user_id |Number |Yes |user ID |
|user_account |String |Yes |user account |
|user_name |String |No |user name |
|user_email |String |No |user email |
|user_avatar |String |No |user avatar URL |
|is_admin |Boolean |No |Is it an administrator? |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Add user results, see **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success_count |Number |Yes |Number of users successfully added |
|failed_count |Number |No |Add the number of failed users |
|failed_users |Array |No |Add a list of failed user accounts |
