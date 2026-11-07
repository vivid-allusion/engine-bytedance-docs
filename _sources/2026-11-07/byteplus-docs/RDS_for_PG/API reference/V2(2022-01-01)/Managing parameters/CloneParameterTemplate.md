---
title: "CloneParameterTemplate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/CloneParameterTemplate"
---

Call the CloneParameterTemplate API to clone the parameter template.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|SrcTemplateId |String |Yes |postgresql\-6d57281c3313\*\*\*\* |Source parameter template ID. |
|TemplateName |String |Yes |Clone parameter template_test |New parameter template name. The template name should satisfy the following rules:<br><br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 2–64 characters.<br><br>* It cannot start with a digit or hyphen (\-). |
|TemplateDesc |String |No |This is a description of the parameter template. |Description of the template to facilitate subsequent application and management of the template. It supports up to 200 characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateId |String |postgresql\-4ad4ac5f712f\*\*\*\* |New parameter template ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CloneParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "SrcTemplateId": "postgresql-6d57281c3313****",
    "TemplateName": "克隆参数模板_测试",
    "TemplateDesc": "这是一段参数模板的描述信息。"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250507154413F55F88EC09E9686A42C8-20694f",
        "Action": "CloneParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "TemplateId": "postgresql-4ad4ac5f712f****"
    }
}
```
