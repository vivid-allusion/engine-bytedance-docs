---
title: "DescribeRecoverableTime"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describerecoverabletime1"
---

Call the DescribeRecoverableTime API to view the recoverable time range.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-h441603c\*\*\*\* |Instance ID. |
|RestoreType |String |No |TABLE_LEVEL |Indicates the type of recovery. Currently, only the value of `TABLE_LEVEL` is supported, that is, library and table\-level recovery.<br><br>tip<br><br>This field will be deprecated soon. |
|BackupRegion |String |No |cn\-shanghai |The region where the backup is located. The default value is the region of the instance. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|RecoverableTimeInfo |Object[] |[<br><br>{<br><br>"EarliestRecoverableTime": "2023\-01\-10T14:27:44.000Z",<br><br>"LatestRecoverableTime": "2023\-01\-11T06:05:14.093Z"<br><br>}<br><br>] |The recoverable time period of the instance (+0800). If empty, it means the instance is currently not recoverable. |
|EarliestRecoverableTime |String |2022\-01\-01T10:10:10Z |The earliest recoverable time of the instance (+0800). If it is empty, it means that the instance is currently not recoverable. |
|LatestRecoverableTime |String |2022\-01\-01T10:10:10Z |The latest recoverable time of the instance (+0800), if it is empty, it means that the instance is not recoverable at present. |

## Sample request

```json
POST /?Action=DescribeRecoverableTime&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-ce48081d****",
    "RestoreType": "TABLE_LEVEL"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202301111405138FCE5A0097D88059AC62",
        "Action": "DescribeRecoverableTime",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RecoverableTimeInfo": [
            {
                "EarliestRecoverableTime": "2023-01-10T14:27:44.000Z",
                "LatestRecoverableTime": "2023-01-11T06:05:14.093Z"
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
