---
title: "CreateSchemaDiff"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/CreateSchemaDiff"
---

Call CreateSchemaDiff API to create a branch compare task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |perky\-bean\-1459\*\*\*\* |ID of the workspace. |
|SourceBranchId |String |Yes |br\-neat\-taka\-9e46\*\*\*\* |Source branch ID. |
|SourceDatabaseName |String |Yes |SourceDB |Name of the source database. |
|SourceSchemaName |String |Yes |SourceSchema |Name of the source schema. |
|TargetBranchId |String |Yes |br\-neat\-taka\-9e46\*\*\*\* |Target branch ID. |
|TargetDatabaseName |String |Yes |SourceDB |Name of the target database. |
|TargetSchemaName |String |Yes |DestinationSchema |Name of the target schema. |
|ForceReCompare |Boolean |Yes |false |Whether to enforce re\-comparison. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Return the latest compare branch result within 24 hours. If no compare branch result exists within 24 hours, initiate the comparison. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SchemaDiffJobId |String |schema\-diff\-7cf8b8402a17426f8bcef50f62db\*\*\*\* |Task ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=CreateSchemaDiff&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "perky-bean-1459****",
    "SourceBranchId": "br-neat-taka-9e46****",
    "SourceDatabaseName": "SourceDB",
    "SourceSchemaName": "SourceSchema",
    "TargetBranchId": "br-neat-taka-9e46****",
    "TargetDatabaseName": "SourceDB",
    "TargetSchemaName": "DestinationSchema",
    "ForceReCompare": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSchemaDiff",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "SchemaDiffJobId": "schema-diff-7cf8b8402a17426f8bcef50f62db****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
