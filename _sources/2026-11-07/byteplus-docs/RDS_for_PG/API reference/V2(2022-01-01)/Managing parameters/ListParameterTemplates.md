---
title: "ListParameterTemplates"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ListParameterTemplates"
---

Call the ListParameterTemplates API to query the parameter templates of the account in the current region.

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|TemplateCategory |String |No |DBEngine |Classification of the parameter template. The current value can only be `DBEngine`. |
|TemplateType |String |No |PostgreSQL |Parameter template type. The current value can only be `PostgreSQL`. |
|TemplateTypeVersion |String |No |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|TemplateSource |String |No |System |source of the parameter template. Current value can only be `User`. |

## Response parameters

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TemplateInfos |Array of [ParameterTemplateInfoObject](https://docs.byteplus.com/en/docs/61/48136#parametertemplateinfoobject) |Refer to the Sample response. |Parameter template list. |
|Total |Integer |38 |The number of parameter templates that meet the specified query conditions. |

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
|TemplateSource |String |User |Source of the parameter template. Current value can only be `User`. |
|TemplateType |String |PostgreSQL |Parameter template type. The current value can only be `PostgreSQL`. |
|TemplateTypeVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|UpdateTime |String |2025\-05\-07T08:15:02.000Z |Last modification time of the parameter template. Format is `yyyy-MM-ddTHH:mm:ss.sss`Z (UTC time).<br><br>> **tip**<br><br><br>> If the parameter template has not been updated since its creation, this field will have the same value as CreateTime.<br> |

## Sample

### Sample request

```json
POST /?Action=ListParameterTemplates&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateTypeVersion": "PostgreSQL_12"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202505071625172068C54AA16BA58A0CEA-ed49ac",
        "Action": "ListParameterTemplates",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijijng"
    },
    "Result": {
        "TemplateInfos": [
            {
                "AccountId": "2100069040",
                "CreateTime": "2025-05-07T07:44:14.000Z",
                "NeedRestart": false,
                "ParameterNum": 1,
                "TemplateCategory": "DBEngine",
                "TemplateDesc": "这是一段参数模板的描述信息。",
                "TemplateId": "postgresql-4ad4ac5f712f****",
                "TemplateName": "参数模板_测试3",
                "TemplateSource": "User",
                "TemplateType": "PostgreSQL",
                "TemplateTypeVersion": "PostgreSQL_12",
                "UpdateTime": "2025-05-07T08:16:37.000Z"
            },
            {
                "AccountId": "2100069040",
                "CreateTime": "2025-05-07T04:22:39.000Z",
                "NeedRestart": true,
                "ParameterNum": 1,
                "TemplateCategory": "DBEngine",
                "TemplateDesc": "",
                "TemplateId": "postgresql-a90388ac5e47****",
                "TemplateName": "参数模板_测试2",
                "TemplateSource": "User",
                "TemplateType": "PostgreSQL",
                "TemplateTypeVersion": "PostgreSQL_12",
                "UpdateTime": "2025-05-07T04:22:39.000Z"
            },
            {
                "AccountId": "2100069040",
                "CreateTime": "2025-05-02T10:31:49.000Z",
                "NeedRestart": true,
                "ParameterNum": 33,
                "TemplateCategory": "DBEngine",
                "TemplateDesc": "",
                "TemplateId": "postgresql-805d440402ed****",
                "TemplateName": "参数模板_测试1",
                "TemplateSource": "User",
                "TemplateType": "PostgreSQL",
                "TemplateTypeVersion": "PostgreSQL_12",
                "UpdateTime": "2025-05-02T10:31:49.000Z"
            }
        ],
        "Total": 3
    }
}
```
