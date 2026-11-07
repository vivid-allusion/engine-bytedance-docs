---
title: "DeleteParameterTemplate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleteparametertemplate1"
---

Call the DeleteParameterTemplate API to delete a parameter template.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TemplateId |String |Yes |mysql\-84db6da5fc5d\*\*\*\* |The parameter template ID.<br><br>tip<br><br>Only user\-created templates can be deleted; system templates do not support deletion. |
|ProjectName |String |No |default |The project to which it belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this request parameter must be included. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|TemplateId |String |mysql\-a3ba0f1eee19\*\*\*\* |The parameter template ID. |

## Sample request

```json
POST /?Action=DeleteParameterTemplate&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateId": "mysql-5055d8bb****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230809193307A0A6B22CE7B5078EE439",
        "Action": "DeleteParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TemplateId": "mysql-a3ba0f1eee19****"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
