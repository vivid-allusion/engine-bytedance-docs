---
title: "DescribeDataLakeSecretConnection"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeDataLakeSecretConnection"
---

Call the DescribeDataLakeSecretConnection API to query the data lake connection.

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
|DatabaseName |String |Yes |testDB |Name of the database. |
|SecretName |String |No |testConnection |Name of the data lake connection.<br><br><div data-tips="true" data-tips-type="default">Decscription</div><br><br><br><div data-tips="true" data-tips-type="default">If not specified, queries all data lake connections under the specified Database.</div><br> |
|Limit |Integer |No |5 |Pagination query count can be an integer greater than or equal to 1, with a default value of 10. |
|Offset |Integer |No |1 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Secrets |Array of [DataLakeSecret](https://docs.byteplus.com/en/docs/330/106715#datalakesecret) |Refer to the sample response. |Details of data lake connections that meet query conditions. |
|Total |Long |3 |Total number of results matching the query criteria. |


<span id="datalakesecret"></span>
### DataLakeSecret


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccessKeyID |String |AKLTMDcyNTA4YzIwYWUxNDkzNDhmYzRkNDU1NmUwZGU\*\*\*\* |ID of the access key for tenant identity. |
|DatabaseName |String |testDB |Name of the database. |
|Endpoint |String |tos\-cn\-beijing.volces.com |Access address of Object Storage TOS. |
|Name |String |testConnection |Name of the data lake connection. |
|Scope |String | | |
|Type |String |TOS |Type of Object Storage connect. Currently only `TOS` type is supported. |
|Username |String |testUser |User name. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeDataLakeSecretConnection&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "ideal-fir-9fc8****",
    "BranchId": "br-merry-scup-42d3****",
    "SecretName": "testConnection",
    "Limit": 5,
    "Offset": 1,
    "DatabaseName": "testDB"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202607072123529FCB9DAB7883835B208E-84c51a",
        "Action": "DescribeDataLakeSecretConnection",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-guilin-boe"
    },
    "Result": {
        "Secrets": [
            {
                "AccessKeyID": "",
                "DatabaseName": "testDB",
                "Endpoint": "tos-cn-beijing.volces.com",
                "Name": "testconnection",
                "Scope": "",
                "Type": "TOS",
                "Username": "user_admin"
            },
            {
                "AccessKeyID": "",
                "DatabaseName": "testDB",
                "Endpoint": "tos-cn-beijing.volces.com",
                "Name": "testconnection2",
                "Scope": "",
                "Type": "TOS",
                "Username": "user_admin"
            },
            {
                "AccessKeyID": "",
                "DatabaseName": "testDB",
                "Endpoint": "tos-cn-beijing.volces.com",
                "Name": "testconnection3",
                "Scope": "",
                "Type": "TOS",
                "Username": "user1"
            }
        ],
        "Total": 3
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
