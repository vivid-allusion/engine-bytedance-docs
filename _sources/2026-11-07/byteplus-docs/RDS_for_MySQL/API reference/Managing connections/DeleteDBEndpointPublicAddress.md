---
title: "DeleteDBEndpointPublicAddress"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbendpointpublicaddress"
---

Call the DeleteDBEndpointPublicAddress API to delete a public endpoint address.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |The ID of the instance. |
|EndpointId |String |Yes |mysql\-e26822cf\*\*\*\*\-cluster |The ID of the instance connection endpoint. |
|Domain |String |Yes |mysql\-e26822cf\*\*\*\*\-public.rds.volces.com |The access domain of the database. |
|EipId |String |Yes |eip\-h0agizep3thc3kyadhvy\*\*\*\* |The ID of the EIP. You can use [DescribeEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes)to query the basic information of an EIP. |

## Response parameters

null

## Sample request

```json
POST /?Action=DeleteDBEndpointPublicAddress&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-3c25f219****",
    "EndpointId": "mysql-3c25f219****-cluster",
    "EipId": "eip-h0agizep3thc3kyadhvy****",
    "Domain": "mysql-3c25f219****-public.rds.volces.com"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111154723C4732E51B93E0A8A3689",
        "Action": "DeleteDBEndpointPublicAddress",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
