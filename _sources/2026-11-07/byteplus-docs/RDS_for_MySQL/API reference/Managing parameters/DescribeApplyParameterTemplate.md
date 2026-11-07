---
title: "DescribeApplyParameterTemplate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeapplyparametertemplate1"
---

Call the DescribeApplyParameterTemplate API to query parameter changes when applying a specific parameter template to a specified MySQL instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TemplateId |String |Yes |mysql\-a77966bd88ee\*\*\*\* |Parameter template ID. |
|InstanceId |String |Yes |mysql\-d4942fd7\*\*\*\* |Instance ID to which the parameter template will be applied. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mysql\-5ca65a66\*\*\*\* |Instance ID to which the parameter template will be applied. |
|TemplateId |String |mysql\-a77966bd88ee\*\*\*\* |Parameter template ID. |
|Parameters |Object[] |Refer to the response example. |Parameter information. |
|Name |String |auto_increment_increment |Parameter Name. |
|OldValue |String |1 |Modify the previous parameter value. |
|NewValue |String |2 |Modified parameter value. |
|Restart |Boolean |false |Whether to restart the instance after modifying the parameters.<br><br><br>* `true`: Restart is required.<br><br>* `false`: No restart is required. |

## Sample request

```json
POST /?Action=DescribeApplyParameterTemplate&Version=2022-01-01 
HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-d4942fd7****",
    "TemplateId": "mysql-52566b825bcc****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308101202004055093B551C53F4EBF1",
        "Action": "DescribeApplyParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mysql-d4942fd7****",
        "Parameters": [
            {
                "Name": "auto_increment_increment",
                "NewValue": "6",
                "OldValue": "2",
                "Restart": false
            },
            {
                "Name": "auto_increment_offset",
                "NewValue": "7",
                "OldValue": "3",
                "Restart": false
            }
        ],
        "TemplateId": "mysql-52566b825bcc6c70"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
