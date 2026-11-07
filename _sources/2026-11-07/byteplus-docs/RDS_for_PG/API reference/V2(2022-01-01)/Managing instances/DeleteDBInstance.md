---
title: "DeleteDBInstance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/deletedbinstance"
---

Call the DeleteDBInstance API to delete an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DeleteDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-21a3333b****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306192210363F139D5899821071AAB5",
        "Action": "DeleteDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
