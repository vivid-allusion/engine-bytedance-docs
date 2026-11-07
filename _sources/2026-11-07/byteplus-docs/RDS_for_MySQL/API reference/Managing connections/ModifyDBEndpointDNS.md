---
title: "ModifyDBEndpointDNS"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpointdns"
---

Call the ModifyDBEndpointDNS API to modify the resolution method of a private network address.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |Instance ID. |
|EndpointId |String |Yes |mysql\-e26822cf\*\*\*\*\-cluster |Instance connection endpoint ID. |
|NetworkType |String |Yes |Private |The network address type, which can be `Private`, indicating a private network address. |
|DNSVisibility |Boolean |Yes |false |* `false`: Volcengine private network resolution (default).<br><br>* `true`: Volcengine private and public network resolution. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyDBEndpointDNS&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-62e07c2c****",
    "EndpointId": "mysql-62e07c2c****-cluster",
    "NetworkType": "Private",
    "DNSVisibility": true
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230118155840AB43F2987AF578AE6958",
        "Action": "ModifyDBEndpointDNS",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
