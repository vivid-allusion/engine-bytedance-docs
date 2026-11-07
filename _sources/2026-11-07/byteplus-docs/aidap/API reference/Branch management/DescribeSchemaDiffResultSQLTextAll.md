---
title: "DescribeSchemaDiffResultSQLTextAll"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeSchemaDiffResultSQLTextAll"
---

Call the DescribeSchemaDiffResultSQLTextAll API to query the complete migration SQL text for the branch comparison task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

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
|MigrationSQL |String |/\*\nStatement 0\n\*/\nCREATE TABLE \"DestinationSchema\".\"SourceSchemaTable1\" (\n\t\"column1\" character varying COLLATE \"pg_catalog\".\"default\",\n\t\"column2\" character varying COLLATE \"pg_catalog\".\"default\"\n);\n\n/\*\nStatement 1\n\*/\nCREATE TABLE \"DestinationSchema\".\"SourceSchemaTable2\" (\n\t\"column1\" name COLLATE \"pg_catalog\".\"C\" NOT NULL,\n\t\"column2\" date NOT NULL\n);\n\n/\*\nStatement 2\n\*/\nCREATE UNIQUE INDEX \"SourceSchemaTable2_pkey\" ON \"DestinationSchema\".\"SourceSchemaTable2\" USING btree (column1, column2);\n\n/\*\nStatement 3\n\*/\nALTER TABLE \"DestinationSchema\".\"SourceSchemaTable2\" ADD CONSTRAINT \"SourceSchemaTable2_pkey\" PRIMARY KEY USING INDEX \"SourceSchemaTable2_pkey\";\n\n/\*\nStatement 4\n  \- DELETES_DATA: Deletes all rows in the table (and the table itself)\n\*/\nDROP TABLE \"DestinationSchema\".\"DestinationSchemaName\"; |Complete migration SQL. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeSchemaDiffResultSQLTextAll&Version=2025-10-01
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
        "Action": "DescribeSchemaDiffResultSQLTextAll",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "MigrationSQL": "/*\\nStatement 0\\n*/\\nCREATE TABLE \\\"DestinationSchema\\\".\\\"SourceSchemaTable1\\\" (\\n\\t\\\"column1\\\" character varying COLLATE \\\"pg_catalog\\\".\\\"default\\\",\\n\\t\\\"column2\\\" character varying COLLATE \\\"pg_catalog\\\".\\\"default\\\"\\n);\\n\\n/*\\nStatement 1\\n*/\\nCREATE TABLE \\\"DestinationSchema\\\".\\\"SourceSchemaTable2\\\" (\\n\\t\\\"column1\\\" name COLLATE \\\"pg_catalog\\\".\\\"C\\\" NOT NULL,\\n\\t\\\"column2\\\" date NOT NULL\\n);\\n\\n/*\\nStatement 2\\n*/\\nCREATE UNIQUE INDEX \\\"SourceSchemaTable2_pkey\\\" ON \\\"DestinationSchema\\\".\\\"SourceSchemaTable2\\\" USING btree (column1, column2);\\n\\n/*\\nStatement 3\\n*/\\nALTER TABLE \\\"DestinationSchema\\\".\\\"SourceSchemaTable2\\\" ADD CONSTRAINT \\\"SourceSchemaTable2_pkey\\\" PRIMARY KEY USING INDEX \\\"SourceSchemaTable2_pkey\\\";\\n\\n/*\\nStatement 4\\n  - DELETES_DATA: Deletes all rows in the table (and the table itself)\\n*/\\nDROP TABLE \\\"DestinationSchema\\\".\\\"DestinationSchemaName\\\";"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
