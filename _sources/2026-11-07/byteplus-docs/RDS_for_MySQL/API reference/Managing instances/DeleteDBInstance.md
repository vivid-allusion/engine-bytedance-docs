---
title: "DeleteDBInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbinstance1"
---

Call the DeleteDBInstance API to delete an instance.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |Instance ID.<br><br>tip<br><br><br>* You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to query instance information, including the instance ID.<br><br>* Only pay\-as\-you\-go instances support deletion via this API. For subscription instances, you need to unsubscribe them in the Refund Management console of the Billing Center. |
|DataKeepPolicy |String |No |Last |The policy for retaining backups after the instance is released. Supported values are as follows.<br><br><br>* `Last`: Retain the last backup. This is the default value.<br><br>* `All`: Retain all backups of the instance.<br><br>* `None`: Do not retain any backups. |
|DataKeepDays |Integer |No |7 |Backup retention period in days, default is 7 days. |

## Response parameters

null

## Sample request

```json
POST /?Action=DeleteDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-e26822cf****",
    "DataKeepPolicy": "Last"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2023120413593055A48DA4D95A611CCBDF",
        "Action": "DeleteDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
