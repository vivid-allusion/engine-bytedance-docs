---
title: "DescribeDBInstanceSSL"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceSSL"
---

Call the DescribeDBInstanceSSL API to query the SSL settings of the specified instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-f006d308\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Address |Array of String |[<br><br>"postgresf006d308\*\*\*\*.rds\-pg.ivolces.com"<br><br>] |Protected address. |
|ForceEncryption |Boolean |true |Is force encryption enabled? Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|IsValid |Boolean |true |Is the SSL certificate valid? Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|SSLEnable |Boolean |true |Is SSL functionality enabled? Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|SSLExpireTime |String |2026\-09\-10T04:50:55Z |SSL certificate expiration time. Format: `yyyy-MM-ddTHH:mm:ss` (UTC time). |
|TLSVersion |Array of String |[<br><br>"TLSv1_2",<br><br>"TLSv1_3"<br><br>] |Supported TLS versions. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstanceSSL&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-f006d308****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910212750FB6F70C0B435BAD38BED-d402ca",
        "Action": "DescribeDBInstanceSSL",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Address": [
            "postgresf006d308****.rds-pg.ivolces.com"
        ],
        "ForceEncryption": true,
        "IsValid": true,
        "SSLEnable": true,
        "SSLExpireTime": "2026-09-10T04:50:55Z",
        "TLSVersion": [
            "TLSv1_2",
            "TLSv1_3"
        ]
    }
}
```
