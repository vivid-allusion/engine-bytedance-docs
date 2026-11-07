---
title: "DescribeDBInstanceSSL"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancessl"
---

Call the DescribeDBInstanceSSL API to query the SSL settings of a specified MySQL instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-d4942fd7\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|SSLEnable |Boolean |true |SSL switch, with possible values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|IsValid |Boolean |false |Whether the certificate is valid, with possible values:<br><br><br>* `true`: Valid.<br><br>* `false`: Invalid. |
|SSLExpireTime |String |2024\-08\-10T03:47:37.000Z |Certificate expiration time, in the format: yyyy\-MM\-dd HH:mm:ss (UTC time). |
|TLSVersion |String |TLSv1.1,TLSv1.2 |Supported TLS versions. Multiple versions are separated by English commas (,). |
|InstanceId |String |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|Address |String |mysqld4942fd7\*\*\*\*.rds\-boe.ivolces.com |Protected address. |

## Sample request

```json
POST /?Action=DescribeDBInstanceSSL&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-d4942fd7****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308101148194C92693AD273B64DDD92",
        "Action": "DescribeDBInstanceSSL",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Address": "mysqld4942fd7****.rds.ivolces.com",
        "InstanceId": "mysql-d4942fd7****",
        "IsValid": true,
        "SSLEnable": true,
        "SSLExpireTime": "2024-08-10T03:47:37.000Z",
        "TLSVersion": "TLSv1,TLSv1.1,TLSv1.2"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
