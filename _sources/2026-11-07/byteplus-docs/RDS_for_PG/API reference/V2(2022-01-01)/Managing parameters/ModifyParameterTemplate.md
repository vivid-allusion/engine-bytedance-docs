---
title: "ModifyParameterTemplate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyParameterTemplate"
---

Call the ModifyParameterTemplate API to modify a parameter template.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|TemplateId |String |Yes |postgresql\-6d57281c3313\*\*\*\* |ID of the parameter template. |
|TemplateName |String |Yes |Parameter template_test |New name of the parameter template. |
|TemplateDesc |String |No |This is a description of the parameter template. |New description for the parameter template. It supports up to 200 characters. |
|TemplateParams |Array of [ParameterObject](https://docs.byteplus.com/en/docs/61/48134#parameterobject) |Yes |See the request example. |Parameters configuration in the parameter template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If it contains parameters already in the original parameter template, the parameter values will use the newly provided ones.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If it contains parameters not in the original parameter template, those parameters will be added to the parameter template.</div><br> |


<span id="parameterobject"></span>
### ParameterObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |auto_explain.log_analyze |Parameter name. |
|Value |String |Yes |off |Parameter value. Refers specifically to the current instance running value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateId": "postgresql-6d57281c3313****",
    "TemplateName": "参数模板_测试-",
    "TemplateDesc": "这是一段参数模板的描述信息。",
    "TemplateParams": [
        {
            "Name": "auto_explain.log_analyze",
            "Value": "on"
        },
        {
            "Name": "auto_explain.log_buffers",
            "Value": "on"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250507155747117C127A35D4369CA572-7113d4",
        "Action": "ModifyParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
