---
title: "ModifyDBEndpointDNS"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointdns"
---

Call ModifyDBEndpointDNS API to modify the instance DNS.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|EndpointId |String |No |postgres\-ca7b7019\*\*\*\*\-custom\-f07b |Instance connection endpoint ID.If this parameter is not specified, the default endpoint is selected by default. |
|NetworkType |String |Yes |Private |Network type. Currently, only the `Private` type is supported. |
|DNSVisibility |Boolean |Yes |false |Private and public network resolution of BytePlus.<br><br><br>* `false`: Default value. PrivateZone of BytePlus.<br><br>* `true`: Private and public network resolution of BytePlus. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyDBEndpointDNS&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.ap-southeast-1.byteplusapi.com
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "EndpointId": "postgres-ca7b7019****-custom-f07b",
    "DNSVisibility": true,
    "NetworkType": "Private"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230802162934534215E5A7894CF84238",
        "Action": "ModifyDBEndpointDNS",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
