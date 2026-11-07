---
title: "ModifyParameterTemplate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyparametertemplate1"
---

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|TemplateId |String |Yes |mysql\-a3ba0f1eee19\*\*\*\* |Parameter templates ID. |
|TemplateName |String |Yes |test |Name of the parameter template. |
|TemplateParams |Array of [InstanceParam](https://docs.byteplus.com/en/docs/40/15447#instanceparam) |No |[<br><br>{<br><br>"Name": "auto_increment_increment","RunningValue": "1"<br><br>}<br><br>] |Parameters included in the parameter template. |
|TemplateDesc |String |No |test |Template description. |
|ProjectName |String |No |default |The project to which it belongs.<br><br>> **tip**<br><br><br>> This parameter is required if the AK/SK used for the API call belongs to an IAM account that only has permissions for a specific project.<br> |

Call the ModifyParameterTemplate API to modify a parameter template.

### InstanceParam

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|Name |String |Yes |auto_increment_increment |Instance parameter name.<br><br>> **tip**<br><br><br>> When used as request parameters in CreateParameterTemplate and ModifyParameterTemplate, you only need to pass `Name` and `RunningValue`.<br> |
|RunningValue |String |Yes |1 |The numeric value or expression configured in the parameter template.<br><br>> **tip**<br><br><br><br>* > When calling CreateParameterTemplate and ModifyParameterTemplate, this field passes in the numeric value or expression written to the template configuration.<br><br><br>* > When calling the DescribeParameterTemplate API to query templates, this field returns the configured value stored in the template.<br><br><br>* > When the template is applied to a specific instance, if the value is an expression, the system recalculates it based on the **specification of the target node**. Therefore, the final **running value that takes effect** on the instance may differ from the value configured in the template.<br> |

## Response parameter

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TemplateId |String |mysql\-a3ba0f1eee19\*\*\*\* |Parameter templates ID. |

## Sample

### Sample request

```json
POST /?Action=ModifyParameterTemplate&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateId": "mysql-a3ba0f1e****",
    "TemplateName": "test1234",
    "TemplateDesc": "这是一段描述",
    "TemplateParams": [
        {
            "Name": "auto_increment_increment",
            "RunningValue": "2"
        },
        {
            "Name": "auto_increment_offset",
            "RunningValue": "3"
        }
    ]
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230809192831904AA2BF4F4EA48EC998",
        "Action": "ModifyParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "TemplateId": "mysql-a3ba0f1eee19****"
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
