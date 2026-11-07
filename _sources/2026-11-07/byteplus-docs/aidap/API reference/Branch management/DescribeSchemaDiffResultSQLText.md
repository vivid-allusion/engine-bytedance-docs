---
title: "DescribeSchemaDiffResultSQLText"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeSchemaDiffResultSQLText"
---

Call DescribeSchemaDiffResultSQLText API to query the SQL text of the branch compare result.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate a workspace using the PostgreSQL engine or Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |perky\-bean\-1459\*\*\*\* |ID of the workspace. |
|SchemaDiffJobId |String |Yes |schema\-diff\-7cf8b8402a17426f8bcef50f62db\*\*\*\* |The ID of the branch comparison task. |
|ObjectName |String |Yes |SourceSchemaTable2 |Name of the difference object. |
|ObjectType |String |Yes |table |Type of the difference object. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CompareResultSQL |String |CREATE TABLE \"DestinationSchema\".\"SourceSchemaTable2\" (\n\t\"column1\" name COLLATE \"pg_catalog\".\"C\" NOT NULL,\n\t\"column2\" date NOT NULL\n);\nCREATE UNIQUE INDEX \"SourceSchemaTable2_pkey\" ON \"DestinationSchema\".\"SourceSchemaTable2\" USING btree (column1, column2);\nALTER TABLE \"DestinationSchema\".\"SourceSchemaTable2\" ADD CONSTRAINT \"SourceSchemaTable2_pkey\" PRIMARY KEY USING INDEX \"SourceSchemaTable2_pkey\"; |Executable SQL to change the structure of the source branch to the structure of the target branch. |
|SourceObjectDefinition |String |CREATE TABLE \"SourceSchema\".\"SourceSchemaTable2\" (\n\t\"column1\" name NOT NULL,\n\t\"column2\" date NOT NULL,\n\tCONSTRAINT \"SourceSchemaTable2_pkey\" PRIMARY KEY (\"column1\", \"column2\")\n) |Complete DDL definition of the source branch object. |
|TargetObjectDefinition |String |CREATE TABLE \"DestinationSchema\".\"DestinationSchemaName\" (\n\t\"column1\" character varying NOT NULL,\n\t\"column2\" boolean NOT NULL,\n\tCONSTRAINT \"DestinationSchemaName_pkey\" PRIMARY KEY (\"column1\")\n) |Complete DDL definition of the target branch object. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeSchemaDiffResultSQLText&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "perky-bean-1459****",
    "SchemaDiffJobId": "schema-diff-7cf8b8402a17426f8bcef50f62db****",
    "ObjectName": "SourceSchemaTable2",
    "ObjectType": "table"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260511125041F0069A1A1B1A31247781-1f47d7",
        "Action": "DescribeSchemaDiffResultSQLText",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "CompareResultSQL": "CREATE TABLE \"DestinationSchema\".\"SourceSchemaTable2\" (\n\t\"column1\" name COLLATE \"pg_catalog\".\"C\" NOT NULL,\n\t\"column2\" date NOT NULL\n);\nCREATE UNIQUE INDEX \"SourceSchemaTable2_pkey\" ON \"DestinationSchema\".\"SourceSchemaTable2\" USING btree (column1, column2);\nALTER TABLE \"DestinationSchema\".\"SourceSchemaTable2\" ADD CONSTRAINT \"SourceSchemaTable2_pkey\" PRIMARY KEY USING INDEX \"SourceSchemaTable2_pkey\";",
        "SourceObjectDefinition": "CREATE TABLE \"SourceSchema\".\"SourceSchemaTable2\" (\n\t\"column1\" name NOT NULL,\n\t\"column2\" date NOT NULL,\n\tCONSTRAINT \"SourceSchemaTable2_pkey\" PRIMARY KEY (\"column1\", \"column2\")\n)",
        "TargetObjectDefinition": ""
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
