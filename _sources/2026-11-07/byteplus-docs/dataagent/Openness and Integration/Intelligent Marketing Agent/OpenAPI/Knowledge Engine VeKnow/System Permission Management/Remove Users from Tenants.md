---
title: "Remove Users from Tenants"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/remove-users-from-tenants"
---

Call this interface to bulk remove users from the current tenant. The caller requires administrative privileges and cannot remove the administrative user.

# Interface description

* Interface name: remove_tenant_user_permission_remove_tenant_users_post

* Interface address:/permission/remove/tenant/users

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|user_ids |Array |Yes |List of user IDs to remove |
|include_module_permissions |Boolean |No |Whether to hand over module permissions together |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Remove user results, see **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|removed_count |Number |Yes |Number of users successfully removed |
|removed_user_ids |Array |No |List of user IDs successfully removed |
|transfer_stats |Object |No |Authority transfer statistics; backfill only when handover_user_id is not empty, see table below **transfer_stats** for details |

## transfer_stats

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|direct_transferred |Number |No |DIRECT resource permission transfer rows |
|modules_transferred |Number |No |Module permission transfers |
|owners_transferred |Number |No |Number of task\-holder transfers |
|conflicts_merged |Number |No |number of conflicting merges |
|recomputed_inherited_count |Number |No |SUBTREE Number of INHERITED rows for derivative recalculation |
|non_transferable_count |Number |No |Number of non\-transferable sources |
