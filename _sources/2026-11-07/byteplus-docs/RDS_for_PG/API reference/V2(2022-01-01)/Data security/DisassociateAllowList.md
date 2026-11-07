---
title: "DisassociateAllowList"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/disassociateallowlist"
---

Call the DisassociateAllowList API to disassociate an allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The system supports disassociating not only multiple allowlists from a single instance, but also a single allowlist from multiple instances. Disassociating multiple allowlists from multiple instances in a single operation is not supported.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|AllowListIds |Array of String |Yes |["acl\-2b7d64502b0a4210a24c58e739de\*\*\*\*"] |ID of the allowlist to disassociate from the instance. |
|InstanceIds |Array of String |Yes |["postgres\-4b38053d\*\*\*\*"] |ID of the instance to disassociate with an allowlist. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DisassociateAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListIds": [
        "acl-2b7d64502b0a4210a24c58e739de****"
    ],
    "InstanceIds": [
        "postgres-4b38053d****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423194017B2017EFDCA4047D90871-5308fb",
        "Action": "DisassociateAllowList",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-guangzhou"
    },
    "Result": null
}
```
