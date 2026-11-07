---
title: "CheckDataLakeSecretConnection"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CheckDataLakeSecretConnection"
---

Call CheckDataLakeSecretConnection API to verify the connectivity of the data lake connection.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API only supports operations on workspaces using the PostgreSQL engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|SecretName |String |Yes |testConnection |Name of the data lake connection. |
|DatabaseName |String |Yes |testDB |Name of the database. |
|Endpoint |String |No |tos\-cn\-beijing.volces.com |Access address of Object Storage TOS. |
|Scope |String |No | | |
|AccessKeyID |String |No |AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU\*\*\*\* |ID of the access key for tenant identity. |
|SecretAccessKey |String |No |WW1WaVpqaGtOamsyWm1ZMU5EazRaVGt4WldJNU1ETmtNRGN6TlRCak\*\*\*\*== |SecretAccessKey of tenant identity access key. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None.

<span id=".56S65L6L"></span>
## Sample

<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
