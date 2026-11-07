---
title: "Query Current User Authorization Resource ID Range"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-current-user-authorization-resource-id-range"
---

Calling this interface queries the numeric resource_id accessible to the current authenticated user by resource type and action; the tenant administrator returns unrestricted = true.

# Interface description

* Interface name: get_authorized_resource_ids_permission_authorized_resource_ids_post

* Interface address:/permission/authorized\-resource\-ids

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|resource_type |String |Yes |resource type |
|required_action |String |Yes |requested permission action |

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
|unrestricted |Boolean |Yes |Is it not limited by the resource ID ACL scope? |
|resource_ids |Array |No |List of DISTINCT numeric resource IDs |
