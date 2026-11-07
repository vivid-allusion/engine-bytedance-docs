---
title: "RemoveDiagnosticsEntity"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/removediagnosticsentity"
---

Call the RemoveDiagnosticsEntity API to remove connection diagnostic records for an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-db6d920e\*\*\*\* |Instance ID. |
|DiagnosticsRecordIds |String[] |Yes |["6a2c3f29a96c45b3b400476eb6c2\*\*\*\*"] |Connection diagnostic record ID.<br><br>tip<br><br>A maximum of 100 record IDs can be passed in. |

## Response parameters

null

## Sample request

```json
POST /?Action=RemoveDiagnosticsEntity&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-db6d920e****",
    "DiagnosticsRecordIds": [
        "6a2c3f29a96c45b3b400476eb6c2****"
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "RemoveDiagnosticsEntity",
        "Region": "cn-north-1",
        "Service": "rds_mysql",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }，
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
