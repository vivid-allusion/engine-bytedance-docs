---
title: "SaveAsParameterTemplate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/SaveAsParameterTemplate"
---

Call the SaveAsParameterTemplate API to export the current parameter configuration of the instance as a parameter template.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-a3e7eb2f\*\*\*\* |Instance ID. |
|TemplateName |String |Yes |Parameter template exported from instance |New parameter template name. The template name should satisfy the following rules:<br><br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 2–64 characters.<br><br>* It cannot start with a digit or hyphen (\-). |
|TemplateDesc |String |No |This is a description of the parameter template. |Description of the template to facilitate subsequent application and management of the template. It supports up to 200 characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateId |String |postgresql\-11b3a53c7d97\*\*\*\* |ID of the parameter template. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=SaveAsParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-a3e7eb2f****",
    "TemplateName": "从实例导出的参数模板",
    "TemplateDesc": "这是一段参数模板的描述信息。"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202505071546307DB7B38D9A0F8354E8AB-920866",
        "Action": "SaveAsParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "TemplateId": "postgresql-11b3a53c7d97****"
    }
}
```
