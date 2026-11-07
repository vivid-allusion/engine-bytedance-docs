---
title: "Resource Permission Authorization/Cancel Authorization"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/resource-permission-authorization-cancel-authorization"
---

Call this interface resource permission to authorize/cancel authorization.

# Interface description

* Interface name: batch_authorize_resource_permission_authorize_resource_batch_post

* Interface address:/permission/authorized/resource/batch

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|object_type |String |Yes |Object type: user/role/department |
|object_ids |Array |Yes |Object ID list (user ID/role ID/department ID) |
|permissions |Array |Yes |resource permission list |
|override |Boolean |No |Whether to overwrite existing permissions (default true) |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Resource permission authorization results, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Was it successful? |
|message |String |Yes |result message |
|results |Array |No |Operation results per object per resource, as detailed in the **results** table below |

## results

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|object_id |Number |Yes |Object ID (user/role/department) |
|resource_type |String |Yes |resource type |
|resource_id |Number |Yes |Resource ID |
|previous_actions |Array |No |Permissions list before operation |
|current_actions |Array |No |Permissions list after operation |
