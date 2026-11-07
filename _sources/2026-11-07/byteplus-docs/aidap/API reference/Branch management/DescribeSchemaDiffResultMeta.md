---
title: "DescribeSchemaDiffResultMeta"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeSchemaDiffResultMeta"
---

Call DescribeSchemaDiffResultMeta API to query detailed information of the Compare branch task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |perky\-bean\-1459\*\*\*\* |ID of the workspace. |
|SchemaDiffJobId |String |Yes |schema\-diff\-7cf8b8402a17426f8bcef50f62db\*\*\*\* |ID of the branch comparison task. |
|PageNum |Integer |No |2 |Start page for pagination query, integer value greater than or equal to 1, default is 1. |
|PageSize |Integer |No |20 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|JobBeginTime |String |2026\-05\-11T12:21:58Z |Start time of the branch comparison task (UTC). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|JobEndTime |String |2026\-05\-11T12:21:58Z |End time of the branch comparison task (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|RequestMessage |Object of [SchemaDiffRequestObject](https://docs.byteplus.com/en/docs/330/106696#schemadiffrequestobject) |Refer to the Sample response. |Request information on branch comparison task. |
|ResponseMessages |Array of [SchemaDiffResultMetaObject](https://docs.byteplus.com/en/docs/330/106696#schemadiffresultmetaobject) |Refer to the sample response. |Detailed results of the branch comparison task. |
|Status |String |finished |Status of the branch comparison task. |
|Total |Integer |3 |Total number of branch comparison task results. |


<span id="schemadiffrequestobject"></span>
### SchemaDiffRequestObject


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SourceBranchId |String |br\-neat\-taka\-9e46\*\*\*\* |ID of the source branch. |
|SourceDatabaseName |String |SourceDB |Source database name. |
|SourceSchemaName |String |SourceSchema |Name of the source schema. |
|TargetBranchId |String |br\-neat\-taka\-9e46\*\*\*\* |ID of the target branch. |
|TargetDatabaseName |String |SourceDB |Name of the target database. |
|TargetSchemaName |String |br\-neat\-taka\-9e46\*\*\*\* |Name of the target schema. |
|WorkspaceId |String |perky\-bean\-1459\*\*\*\* |ID of the workspace. |


<span id="schemadiffresultmetaobject"></span>
### SchemaDiffResultMetaObject


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CompareResultType |String |Source Only |Difference type. Values:<br><br><br>* `Common`: The object exists in both source Schema and target Schema with no differences.<br><br>* `Different`: The object exists in both source schema and target schema but with different definitions; diff_ddl contains changes.<br><br>* `Source Only`: Exists only in the source schema.<br><br>* `Target Only`: Exists only in the target schema. |
|ObjectType |String |table |Type of the difference object. Values:<br><br><br>* `table`: table, column, index, foreign_key, trigger.<br><br>* `sequence`: sequence.<br><br>* `function`: function.<br><br>* `procedure`: procedure.<br><br>* `view`: view.<br><br>* `materialized_view`: materialized view.<br><br>* `extension`: plugin.<br><br>* `enum`: enum. |
|SourceObjectName |String |SourceSchemaTable2 |Name of the source object. |
|SourceSchemaName |String |SourceSchema |Name of the source schema. |
|TargetObjectName |String |SourceSchemaTable2 |Name of the target object. |
|TargetSchemaName |String |DestinationSchema |Name of the target schema. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeSchemaDiffResultMeta&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "perky-bean-1459****",
    "SchemaDiffJobId": "schema-diff-7cf8b8402a17426f8bcef50f62db****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260511123357DEB2BB44F27758066D14-5efb5e",
        "Action": "DescribeSchemaDiffResultMeta",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "JobBeginTime": "2026-05-11T12:21:58Z",
        "JobEndTime": "2026-05-11T12:21:58Z",
        "RequestMessage": {
            "SourceBranchId": "br-neat-taka-9e46****",
            "SourceDatabaseName": "SourceDB",
            "SourceSchemaName": "SourceSchema",
            "TargetBranchId": "br-neat-taka-9e46****",
            "TargetDatabaseName": "SourceDB",
            "TargetSchemaName": "DestinationSchema",
            "WorkspaceId": "perky-bean-1459c86v"
        },
        "ResponseMessages": [
            {
                "CompareResultType": "Source Only",
                "ObjectType": "table",
                "SourceObjectName": "SourceSchemaTable1",
                "SourceSchemaName": "SourceSchema",
                "TargetObjectName": "SourceSchemaTable1",
                "TargetSchemaName": "DestinationSchema"
            },
            {
                "CompareResultType": "Source Only",
                "ObjectType": "table",
                "SourceObjectName": "SourceSchemaTable2",
                "SourceSchemaName": "SourceSchema",
                "TargetObjectName": "SourceSchemaTable2",
                "TargetSchemaName": "DestinationSchema"
            },
            {
                "CompareResultType": "Target Only",
                "ObjectType": "table",
                "SourceObjectName": "DestinationSchemaName",
                "SourceSchemaName": "SourceSchema",
                "TargetObjectName": "DestinationSchemaName",
                "TargetSchemaName": "DestinationSchema"
            }
        ],
        "Status": "finished",
        "Total": 3
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
