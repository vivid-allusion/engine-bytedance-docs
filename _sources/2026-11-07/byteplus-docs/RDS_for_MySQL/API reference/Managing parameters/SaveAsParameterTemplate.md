---
title: "SaveAsParameterTemplate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/saveasparametertemplate1"
---

Call the SaveAsParameterTemplate API to save the parameter configuration of a specified instance as a parameter template.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-5ca65a66\*\*\*\* |Instance ID. |
|TemplateName |String |Yes |test |Parameter template name. |
|TemplateDesc |String |No |test |Parameter template description. |
|ProjectName |String |No |default |The project it belongs to.<br><br>tip<br><br>If the AK/SK you use to call the interface belongs to a sub \- account, and this sub \- account only has the permission for a certain project, you need to pass in this request parameter. |

## Response parameters

null

|Name |Type |Example |Description |
|---|---|---|---|
|TemplateId |String |mysql\-ad91d8e6f75c\*\*\*\* |Parameter template ID. |

## Sample request

```json
POST /?Action=SaveAsParameterTemplate&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateName": "Test-template",
    "TemplateDesc": "描述",
    "InstanceId": "mysql-d4942fd7****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308101204370324152D1BA927F3F0D9",
        "Action": "SaveAsParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": nu{
        "TemplateId": "mysql-ad91d8e6f75c****"
    }ll
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
