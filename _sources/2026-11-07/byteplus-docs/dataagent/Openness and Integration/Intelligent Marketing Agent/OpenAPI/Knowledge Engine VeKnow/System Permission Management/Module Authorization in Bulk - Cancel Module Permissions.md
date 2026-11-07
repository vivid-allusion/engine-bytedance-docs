---
title: "Module Authorization in Bulk/Cancel Module Permissions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/module-authorization-in-bulk-cancel-module-permissions"
---

Call this interface to batch authorize/cancel module permissions (support users, roles, departments).

# Interface description

* Interface name: batch_authorize_module_permission_authorize_module_batch_post

* Interface address:/permission/authorized/module/batch

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|object_type |String |Yes |Object type: user/role/department |
|object_ids |Array |Yes |Object ID list (user ID/role ID/department ID) |
|permissions |Array |Yes |For a list of module permissions, see the **permissions** table below |
|override |Boolean |No |Whether to overwrite existing permissions (default true) |

## permissions

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|module_type |String |Yes |module type |
|actions |Array |Yes |List of authorized permissions, empty means cancel all authorizations |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |No |Batch module permission operation results, see the following **data** table for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Was it successful? |
|message |String |Yes |result message |
|results |Array |No |Operation results for each object and each module, as detailed in the **results** table below |

## results

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|object_id |Number |Yes |Object ID (user/role/department) |
|module_type |String |Yes |module type |
|previous_actions |Array |No |Permissions list before operation |
|current_actions |Array |No |Permissions list after operation |
