---
title: "CreateDataLakeSecretConnection"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateDataLakeSecretConnection"
---

Call the CreateDataLakeSecretConnection API to create a data lake connection.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API only supports operations on workspaces using the PostgreSQL engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |ideal\-fir\-9fc8\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|DatabaseName |String |Yes |testDB |Name of the database. |
|Endpoint |String |Yes |tos\-cn\-beijing.volces.com |Access address of Object Storage TOS. |
|AccessKeyID |String |Yes |AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU\*\*\*\* |Access Key ID for tenant identity. |
|SecretAccessKey |String |Yes |WW1WaVpqaGtOamsyWm1ZMU5EazRaVGt4WldJNU1ETmtNRGN6TlRCak\*\*\*\*== |SecretAccessKey of tenant identity access key. |
|SecretName |String |No |testConnection |Name of the data lake connection. The Connection name must meet the following rules:<br><br><br>* It can only contain Chinese characters, letters (a~z and A~Z), numbers, and underscores (_).<br><br>* The length must not exceed 63 characters.<br><br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If not filled, it will be generated automatically.</div><br> |
|Scope |String |No | |Scope of the bucket used to create the data lake connection.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If not specified, all buckets under the tenant account will be used.</div><br> |
|Username |String |Yes |testUser |User name. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SecretName |String |testConnection |Connection name of the data lake. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=CreateDataLakeSecretConnection&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "ideal-fir-9fc8****",
    "BranchId": "br-merry-scup-42d3****",
    "AccessKeyID": "AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU****",
    "SecretAccessKey": "WW1WaVpqaGtOamsyWm1ZMU5EazRaVGt4WldJNU1ETmtNRGN6TlRCak****==",
    "Endpoint": "tos-cn-beijing.volces.com",
    "DatabaseName": "testDB",
    "Username": "testUser",
    "SecretName": "testConnection"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDataLakeSecretConnection",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "SecretName": "testConnection"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
