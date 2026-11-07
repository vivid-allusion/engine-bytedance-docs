---
title: "Update User Status"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/update-user-status"
---

Calling this interface enables or disables the tenant user. The caller requires administrator or owner privileges and is subject to administrator, owner, and personal action restrictions.

# Interface description

* Interface name: update_user_status_permission_user_status_post

* Interface address:/permissions/user/status

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|user_ids |Array |Yes |List of user IDs to update status |
|status |Number |Yes |User status: 0 = disabled, 1 = enabled |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|updated_count |Number |Yes |Number of users who successfully updated their status |
|updated_user_ids |Array |No |List of user IDs that successfully updated status |
