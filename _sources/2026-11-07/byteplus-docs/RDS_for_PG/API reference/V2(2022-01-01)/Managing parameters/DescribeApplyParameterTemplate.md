---
title: "DescribeApplyParameterTemplate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeApplyParameterTemplate"
---

Call the DescribeApplyParameterTemplate API to query the parameter changes after applying the parameter template (only query, not actually apply).

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-a3e7eb2f\*\*\*\* |Instance ID. |
|TemplateId |String |Yes |postgresql\-11b3a53c7d97\*\*\*\* |Parameter template ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-a3e7eb2f\*\*\*\* |Instance ID. |
|Parameters |Array of [InstanceParamChgObject](https://docs.byteplus.com/en/docs/61/48138#instanceparamchgobject) |Refer to the sample response. |Changes to the instance's parameters after applying the specified parameter template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is not returned if applying the specified parameter template does not change the instance parameters.</div><br> |
|TemplateId |String |postgresql\-11b3a53c7d97\*\*\*\* |Parameter template ID. |


<span id="instanceparamchgobject"></span>
### InstanceParamChgObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |auto_explain.log_buffers |Parameter name. |
|NewValue |String |on |Running value defined for the parameter in the parameter template. |
|OldValue |String |off |Running value of this parameter in the current instance. |
|Restart |Boolean |false |Whether the parameter modification requires an instance restart. Values:<br><br><br>* `true`: required.<br><br>* `false`: not required. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeApplyParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-a3e7eb2f****",
    "TemplateId": "postgresql-11b3a53c7d97****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202505071634404CE78800F77F017F85CE-ac4293",
        "Action": "DescribeApplyParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "postgres-a3e7eb2f****",
        "Parameters": [
            {
                "Name": "auto_explain.log_buffers",
                "NewValue": "on",
                "OldValue": "off",
                "Restart": false
            },
            {
                "Name": "auto_explain.log_analyze",
                "NewValue": "on",
                "OldValue": "off",
                "Restart": false
            }
        ],
        "TemplateId": "postgresql-11b3a53c7d97****"
    }
}
```
