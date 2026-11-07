---
title: "CreateParameterTemplate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/CreateParameterTemplate"
---

Call the CreateParameterTemplate API to create a parameter template.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|TemplateName |String |Yes |Parameter template_test |Name of the parameter template. The template name should satisfy the following rules:<br><br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 2–64 characters.<br><br>* It cannot start with a digit or hyphen (\-). |
|TemplateType |String |Yes |PostgreSQL |Parameter template type. The current value can only be `PostgreSQL`. |
|TemplateParams |Array of [ParameterObject](https://docs.byteplus.com/en/docs/61/48131#parameterobject) |Yes |Refer to the request example. |Parameters configuration in the parameter template. |
|TemplateTypeVersion |String |Yes |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|TemplateDesc |String |No |This is a description of the parameter. |Description of the template, facilitating subsequent template application and management. It supports up to 200 characters. |

### ParameterObject

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |auto_explain.log_analyze |Parameter name. |
|Value |String |Yes |off |Parameter value. Refers specifically to the current instance running value. |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateId |String |postgresql\-6d57281c3313\*\*\*\* |ID of the parameter template. |

## Example

### Sample request

```json
POST /?Action=CreateParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateName": "参数模板_测试",
    "TemplateType": "PostgreSQL",
    "TemplateTypeVersion": "PostgreSQL_12",
    "TemplateParams": [
        {
            "Name": "auto_explain.log_analyze",
            "Value": "off"
        }
    ]
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250507154042DB11BFB3A01D08296D2D-91d4e7",
        "Action": "CreateParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijijng"
    },
    "Result": {
        "TemplateId": "postgresql-6d57281c3313****"
    }
}
```
