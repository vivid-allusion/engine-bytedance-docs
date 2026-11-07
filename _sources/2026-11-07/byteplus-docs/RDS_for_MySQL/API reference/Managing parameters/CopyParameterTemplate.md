---
title: "CopyParameterTemplate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/copyparametertemplate1"
---

Call the CopyParameterTemplate API to copy a parameter template.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|SrcTemplateId |String |Yes |mysql\-f60d7bc5\*\*\*\* |The ID of the source parameter template. |
|TemplateName |String |Yes |copytest |The name of the new parameter template. |
|TemplateDesc |String |No |copytest |The description of the new parameter template. |
|ProjectName |String |No |default |The project to which the parameter template belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this request parameter needs to be specified. |
|Region |String |No |cn\-shanghai |The target region where the parameter template will be copied to.<br><br>tip<br><br>If this field is not specified, the parameter template will be copied to the current region. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|TemplateId |String |mysql\-ad91d8e6f75c\*\*\*\* |The template ID. |

## Sample request

```json
POST /?Action=CopyParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "SrcTemplateId": "mysql-62ddbb705021****",
    "TemplateName": "copytest",
    "TemplateDesc": "copytest",
    "ProjectName": "default",
    "Region": "cn-shanghai"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CopyParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-north-1"
    },
    "Result": {
        "TemplateId": "mysql-ad91d8e6f75c****"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
