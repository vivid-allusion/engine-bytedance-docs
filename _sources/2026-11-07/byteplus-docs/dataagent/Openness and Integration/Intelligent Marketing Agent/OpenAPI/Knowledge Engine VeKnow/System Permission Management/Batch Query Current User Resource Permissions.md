---
title: "Batch Query Current User Resource Permissions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/batch-query-current-user-resource-permissions"
---

Calling this interface queries the valid resource permissions of the current authenticated user in batches according to numerical resource_id, and does not query the upstream resource directory.

# Interface description

* Interface name: get_resource_actions_batch_permission_resource_actions_batch_post

* Interface address:/permission/resource\-actions/batch

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|resource_type |String |Yes |resource type |
|resource_ids |Array |Yes |List of numeric resource IDs, up to 500 |

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
|items |Array |No |One\-to\-one correspondence with the request resource_ids and in the same order. See the **items** table below for details |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|resource_id |Number |Yes |numeric resource ID |
|authorized_actions |Array |No |Valid permissions for the current user |
