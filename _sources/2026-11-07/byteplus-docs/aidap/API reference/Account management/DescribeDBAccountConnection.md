---
title: "DescribeDBAccountConnection"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeDBAccountConnection"
---

Call the DescribeDBAccountConnection API to query connection information of the database account.

## Request type

Synchronous request.

## Precautions

This API can only operate workspaces using the PostgreSQL engine.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBAccountConnection&serviceCode=aidap&version=2025-10-01&groupName=)

## Request parameters

|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|ComputeId |String |Yes |cp\-cute\-fresh\-0e7d\*\*\*\* |Compute ID. |
|AccountName |String |No |test\-user |Account name. |
|DatabaseName |String |Yes |test\-db |Name of the database. |
|AddressId |String |No |addr\-78c22739ee479f6e\*\*\*\* |Address ID. Call the [DescribeWorkspaceEndpoint](https://docs.byteplus.com/en/docs/330/DescribeWorkspaceEndpoint) API to query connection information of a specified workspace.<br><br>> **tip**<br><br><br>> If not specified, returns public network connection information.<br> |

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountName |String |test\-user |Account name. |
|AccountPassword |String |<your\-password\> |Account password. |
|AllowHost |String |[\"0.0.0.0/0\", \"::/0\"] |Allow domain names to connect to the workspace |
|BranchId |String |br\-merry\-scup\-42d3\*\*\*\* |Branch ID. |
|ComputeId |String |cp\-cute\-fresh\-0e7d\*\*\*\* |Compute ID. |
|ConnectionExamples |Array of [ConnectionExample](https://docs.byteplus.com/en/docs/330/84434#connectionexample) |Refer to the Sample response. |Connection example. |
|ConnectionUrl |String |psql 'postgresql://test\-user:<your\-password\>@cp\-sure\-tide\-9371\*\*\*\*.pg.aidap\-global.cn\-beijing.volces.com/test\-db?sslmode=require&channel_binding=require' |Connection string. |
|DatabaseName |String |test\-db |Name of the database. |
|WorkspaceId |String |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |

### ConnectionExample

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ConnectionExample |String |postgresql://test\-user:<your\-password\>@cp\-sure\-tide\-9371\*\*\*\*.pg.aidap\-global.cn\-beijing.volces.com/test\-db?sslmode=require&channel_binding=require |Connection string for the corresponding language type. |
|ConnectionType |String |psql |Connection string type, values:<br><br><br>* `psql`<br><br>* `ConnectionString`<br><br>* `Parameters`<br><br>* `Golang`<br><br>* `Java`<br><br>* `Django` |

## Sample

### Sample request

```JSON
POST /?Action=DescribeDBAccountConnection&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-merry-scup-42d3****",
    "ComputeId": "cp-cute-fresh-0e7d****",
    "EndpointId": "ep-15d73b055d662534****",
    "AccountName": "test-user",
    "DatabaseName": "test-db"
}
```

### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202510161906237ACF29F5823D67C958B1-db70b1",
        "Action": "DescribeDBAccountConnection",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccountName": "test-user",
        "AccountPassword": "<your-password>",
        "AllowHost": "[\"0.0.0.0/0\", \"::/0\"]",
        "BranchId": "br-alert-duck-3bdf****",
        "ComputeId": "cp-sure-tide-9371****",
        "ConnectionExamples": [
            {
                "ConnectionExample": "psql 'postgresql://test-user:<your-password>@cp-sure-tide-9371****.pg.aidap-global.cn-beijing.volces.com/test-db?sslmode=require&channel_binding=require'",
                "ConnectionType": "psql"
            },
            {
                "ConnectionExample": "postgresql://test-user:<your-password>@cp-sure-tide-9371****.pg.aidap-global.cn-beijing.volces.com/test-db?sslmode=require&channel_binding=require",
                "ConnectionType": "ConnectionString"
            },
            {
                "ConnectionExample": "PGHOST='cp-sure-tide-9371****.pg.aidap-global.cn-beijing.volces.com'\nPGDATABASE='test-db'\nPGUSER='test-user'\nPGPASSWORD='<your-password>'\nPGSSLMODE='require'\nPGCHANNELBINDING='require'\n",
                "ConnectionType": "Parameters"
            },
            {
                "ConnectionExample": "package main\nimport (\n\t\"context\"\n\t\"github.com/jackc/pgx/v5\"\n)\n\nfunc main() {\n\tconnStr := \"postgresql://test-user:<your-password>@cp-sure-tide-9371****.pg.aidap-global.cn-beijing.volces.com/test-db?sslmode=require&channel_binding=require\"\n\tconn, err := pgx.Connect(context.Background(), connStr)\n\tif err != nil {\n\t\tpanic(err)\n\t}\n\tdefer conn.Close(context.Background())\n\t// do something with conn. such as CREATE TABLE、INSERT DATA\n\t_, err = conn.Exec(context.Background(), \"CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(50) NOT NULL, email VARCHAR(100) UNIQUE,age INT,created_at TIMESTAMP DEFAULT now());\")\n\tif err != nil {\n\t\tpanic(err)\n\t}\n}\n",
                "ConnectionType": "Golang"
            },
            {
                "ConnectionExample": "package com.test.aidb;\nimport java.sql.Connection;\nimport java.sql.DriverManager;\nimport java.sql.SQLException;\n\npublic class ConnectExample {\n    public static void main(String[] args) {\n        // connection url\n        String url = \"jdbc:postgresql://cp-sure-tide-9371****.pg.aidap-global.cn-beijing.volces.com/test-db?user=test-user&password=<your-password>&channelBinding=require&sslmode=require\";\n\n        try (Connection conn = DriverManager.getConnection(url)) {\n            if (conn != null) {\n                System.out.println(\"successfully connected to DB\");\n            } else {\n                System.out.println(\"failed to make connection!\");\n            }\n        } catch (SQLException e) {\n            e.printStackTrace();\n        }\n    }\n}\n",
                "ConnectionType": "Java"
            },
            {
                "ConnectionExample": "import psycopg2\nfrom urllib.parse import urlparse, parse_qsl, unquote\n\nconnection_url = (\n\t'postgresql://test-user:<your-password>@cp-sure-tide-9371****.pg.aidap-global.cn-beijing.volces.com/test-db?sslmode=require&channel_binding=require'\n)\n\n# parse connection url\nconnection_data = urlparse(connection_url)\n\n# define database settings\nDATABASES = {\n    'default': {\n        'ENGINE': 'django.db.backends.postgresql',\n        'NAME': connection_data.path.lstrip('/'),\n        'USER': connection_data.username,\n        'PASSWORD': unquote(connection_data.password),\n\t'HOST': connection_data.hostname,\n        'PORT': connection_data.port or 5432,\n        'OPTIONS': dict(parse_qsl(connection_data.query)),\n    }\n}\n\n# connect to database using psycopg2\ndb_conf = DATABASES['default']\nconn = psycopg2.connect(\n    dbname=db_conf['NAME'],\n    user=db_conf['USER'],\n    password=db_conf['PASSWORD'],\n    host=db_conf['HOST'],\n    port=db_conf['PORT'],\n    sslmode=db_conf['OPTIONS'].get('sslmode', 'require'),\n)\n\ncur = conn.cursor()\n\n# query all tables in current database except system tables\ncur.execute(\"\"\"\n    SELECT schemaname, tablename\n    FROM pg_tables\n    WHERE schemaname NOT IN ('pg_catalog', 'information_schema')\n    ORDER BY schemaname, tablename;\n\"\"\")\n\ntables = cur.fetchall()\nfor schema, table in tables:\n    print(f\"  - {schema}.{table}\")\n\ncur.close()\nconn.close()\n",
                "ConnectionType": "Django"
            }
        ],
        "ConnectionUrl": "psql 'postgresql://test-user:<your-password>@cp-sure-tide-9371****.pg.aidap-global.cn-beijing.volces.com/test-db?sslmode=require&channel_binding=require'",
        "DatabaseName": "",
        "WorkspaceId": "noble-heath-3a48****"
    }
}
```

## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
