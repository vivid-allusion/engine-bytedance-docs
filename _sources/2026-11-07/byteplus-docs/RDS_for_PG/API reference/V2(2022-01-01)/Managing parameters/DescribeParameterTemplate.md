---
title: "DescribeParameterTemplate"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeParameterTemplate"
---

Call the DescribeParameterTemplate API to query the details of the parameter template.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|TemplateId |String |Yes |postgresql\-4ad4ac5f712f\*\*\*\* |ID of the parameter template. |

## Response parameters

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateInfo |Object of [ParameterTemplateInfoObject](https://docs.byteplus.com/en/docs/61/48137#parametertemplateinfoobject) |Refer to the Sample response. |Detail of the parameter template |

### ParameterTemplateInfoObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountId |String |210006\*\*\*\* |Account ID. |
|CreateTime |String |2025\-05\-07T07:44:14.000Z |Parameter template creation time. Format is `yyyy-MM-ddTHH:mm:ss.sss`Z (UTC time). |
|NeedRestart |Boolean |false |Is restart required to take effect when applying the parameter template (that is, does the parameter template contain parameters that require the Restart instance to take effect). Values:<br><br><br>* `true`: no restart needed.<br><br>* `false`: restart needed. |
|ParameterNum |Integer |1 |Number of parameters contained in this parameter template. |
|TemplateCategory |String |DBEngine |Classification of the parameter template. The current value can only be `DBEngine`. |
|TemplateDesc |String |This is a description of the parameter template. |Description of the parameter template. |
|TemplateId |String |postgresql\-4ad4ac5f712f\*\*\*\* |ID of the parameter template. |
|TemplateName |String |Parameter template_test |Name of parameter template. |
|TemplateParams |Array of [ParameterObject](https://docs.byteplus.com/en/docs/61/48137#parameterobject) |Refer to the sample response. |Configuration of the parameter template. |
|TemplateSource |String |User |Source of the parameter template. Current value can only be `User`. |
|TemplateType |String |PostgreSQL |Parameter template type. The current value can only be `PostgreSQL`. |
|TemplateTypeVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|UpdateTime |String |2025\-05\-07T08:15:02.000Z |Last modification time of the parameter template. Format is `yyyy-MM-ddTHH:mm:ss.sss`Z (UTC time).<br><br>> **tip**<br><br><br>> If the parameter template has not been updated since its creation, this field will have the same value as CreateTime.<br> |

### ParameterObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CheckingCode |String |[on\|off] |Parameter value range. |
|DefaultValue |String |off |Parameter default value. Refers to the default value provided in the default template corresponding to this instance. |
|Description |String |Use EXPLAIN ANALYZE for plan logging. |Parameter description in English. |
|DescriptionZH |String |Enable the sampling of EXPLAIN ANALYZE output. |Parameter description in Chinese. |
|ForceRestart |Boolean |false |Is a restart required to take effect? Values: `true` or `false`. |
|Name |String |auto_explain.log_analyze |Parameter name. |
|Type |String |bool |Parameter value type. Values: `string`, `integer`, `real`, `bool`, and `enum`. |
|Value |String |off |Parameter value. Refers specifically to the current instance running value. |

## Example

### Sample request

```json
POST /?Action=DescribeParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateId": "postgresql-4ad4ac5f712f****"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250507163039222DF7A7914CA7447807-837a1a",
        "Action": "DescribeParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "TemplateInfo": {
            "AccountId": "2100069040",
            "CreateTime": "2025-05-07T07:44:14.000Z",
            "NeedRestart": false,
            "ParameterNum": 1,
            "TemplateCategory": "DBEngine",
            "TemplateDesc": "这是一段参数模板的描述信息。",
            "TemplateId": "postgresql-4ad4ac5f712f****",
            "TemplateName": "克隆参数模板_测试",
            "TemplateParams": [
                {
                    "CheckingCode": "[on|off]",
                    "DefaultValue": "off",
                    "Description": "Use EXPLAIN ANALYZE for plan logging.",
                    "DescriptionZH": "启用 EXPLAIN ANALYZE 输出的采样。",
                    "ForceRestart": false,
                    "Name": "auto_explain.log_analyze",
                    "Type": "bool",
                    "Value": "off"
                }
            ],
            "TemplateSource": "User",
            "TemplateType": "PostgreSQL",
            "TemplateTypeVersion": "PostgreSQL_12",
            "UpdateTime": "2025-05-07T08:16:37.000Z"
        }
    }
}
```
