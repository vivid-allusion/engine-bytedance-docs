---
title: "AssociateAllowList"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/associateallowlist"
---

Call the AssociateAllowList API to associate an allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The system supports associating not only multiple allowlists with a single instance, but also a single allowlist with multiple instances. The system does not support associating multiple allowlists with multiple instances within a single operation.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions


* You can associate up to 100 allowlists with one instance each time.

* Each instance can associate up to 100 allowlists.

* You can associate up to 50 instances with an allowlist at a time.

* Each allowlist can associate up to 1,000 instances.

* The total number of IP addresses or CIDR blocks in all allowlists associated with each instance cannot exceed 300.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|AllowListIds |Array of String |Yes |["acl\-2b7d64502b0a4210a24c58e739de\*\*\*\*"] |ID of the allowlist to associate with the instance. |
|InstanceIds |Array of String |Yes |["postgres\-4b38053d\*\*\*\*","postgres\-5efe96ae\*\*\*\*"] |ID of the instance associated with an allowlist |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=AssociateAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListIds": [
        "acl-2b7d64502b0a4210a24c58e739de****"
    ],
    "InstanceIds": [
        "postgres-4b38053d****",
        "postgres-5efe96ae****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423193611E80D10ED81E54EDE7E89-82c4fa",
        "Action": "AssociateAllowList",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-guangzhou"
    },
    "Result": null
}
```
