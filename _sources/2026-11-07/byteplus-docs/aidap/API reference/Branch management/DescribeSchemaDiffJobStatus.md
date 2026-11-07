---
title: "DescribeSchemaDiffJobStatus"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeSchemaDiffJobStatus"
---

Call DescribeSchemaDiffJobStatus to query the status of the branch comparison task.

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
|SchemaDiffJobId |String |Yes |schema\-diff\-7cf8b8402a17426f8bcef50f62db\*\*\*\* |The ID of the branch comparison task. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CreatedAt |String |2026\-05\-11T12:21:58Z |Creation time of the branch comparison task (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|ErrorMessage |String |generating plan statements: generating migration statements: resolving index diff: generating alter statements for \"test9_src\".\"users_pkey\": generating sql: index diff could not be resolved   schema.Index{Name: \"users_pkey\",\n  \tOwningRelName: schema.SchemaQualifiedName{\n\- \t\tSchemaName:  \"test9_src1\",\n+ \t\tSchemaName:  \"test9_src\",\n  \t\tEscapedName: `\"rename_users\"`,\n  \t},\n  \tOwningRelKind: \"r\",\n  \tColumns:       {\"id\"},\n  \tIsInvalid:     false,\n  \tIsUnique:      true,\n  \tConstraint:    &{Type: \"p\", EscapedConstraintName: `\"users_pkey\"`, ConstraintDef: \"PRIMARY KEY (id)\", IsLocal: true},\n  \tGetIndexDefStmt: strings.Join({\n  \t\t\"CREATE UNIQUE INDEX users_pkey ON test9_src\",\n\- \t\t\"1\",\n  \t\t\".rename_users USING btree (id)\",\n  \t}, \"\"),\n  \tParentIdx: nil,\n  }\n |Information on branch comparison task failure.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">Returned when the branch comparison task fails.</div><br> |
|Exists |Boolean |true |Whether the specified branch comparison task exists. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|FinishedAt |String |2026\-05\-11T12:21:58Z |Completion time of the branch comparison task (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|Status |String |finished |Status on branch comparison task failure. Values:<br><br><br>* `running`: Executing.<br><br>* `waitingUploadTOS`: Pending upload TOS.<br><br>* `finished`: Completed.<br><br>* `failed`: The execution failed.<br><br>* `Expire`: Expired. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeSchemaDiffJobStatus&Version=2025-10-01
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
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSchemaDiffJobStatus",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreatedAt": "2026-05-11T12:21:58Z",
        "Exists": true,
        "FinishedAt": "2026-05-11T12:21:58Z",
        "Status": "finished"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
