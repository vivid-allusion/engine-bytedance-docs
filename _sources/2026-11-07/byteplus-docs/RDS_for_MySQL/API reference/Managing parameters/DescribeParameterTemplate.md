---
title: "DescribeParameterTemplate"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeparametertemplate1"
---

Call the DescribeParameterTemplate API to query the details of a specified parameter template.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TemplateId |String |Yes |mysql\-sys\-80bb93aa14be\*\*\*\* |The ID of the parameter template. |
|ProjectName |String |No |default |The project to which the parameter template belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this request parameter must be included. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|TemplateInfo |Object |Please refer to the return example. |Parameter template list. |
|AccountId |String |0 |Account ID. |
|CreateTime |String |2023\-11\-19 19:23:22 |Creation time. |
|NeedRestart |Boolean |true |Whether the template contains parameters that require restart. |
|ParameterNum |Long |100 |The number of parameters included in the template. |
|ProjectName |String |default |The project to which the template belongs.<br><br>tip<br><br>If the parameter template is an existing template and has not been assigned to a specific project, the return value will be empty. |
|TemplateCategory |String |DBEngine |The template category, with a value of `DBEngine`(database engine parameters). |
|TemplateDesc |String |MySQL 8.0 default parameter template |Parameter template description. |
|TemplateId |String |mysql\-sys\-80bb93aa14be\*\*\*\* |Parameter template ID. |
|TemplateName |String |MySQL_8.0_Default |Parameter template name. |
|TemplateParams |Object[] |[<br><br>{<br><br>"DefaultValue": "1",<br><br>"Description": "Auto\-increment columns are incremented by this.",<br><br>"ExpectValue": "",<br><br>"Name": "auto_increment_increment",<br><br>"Restart": false,<br><br>"RunningValue": "1",<br><br>"ValueRange": "[1\-65535]"<br><br>}<br><br>] |The parameters included in the template. |
|DefaultValue |String |1 |Default value of the parameter. |
|Description |String |Auto\-increment columns are incremented by this. |Description of the parameter. |
|Name |String |auto_increment_increment |Instance parameter name.<br><br>tip<br><br>When used as request parameters in CreateParameterTemplate and ModifyParameterTemplate, only `Name` and `RunningValue` need to be passed. |
|Restart |Boolean |false |Whether instance restart is required to take effect. |
|RunningValue |String |1 |Running value of the parameter.<br><br>tip<br><br>When used as request parameters in CreateParameterTemplate and ModifyParameterTemplate, only `Name` and `RunningValue` need to be passed. |
|ValueRange |String |[1\-65535] |Valid value range of the parameter. |
|Expression |String | |Parameter expression. |
|ExpectValue |String |3 |Expected value of the parameter. |
|TemplateSource |String |System |The types of parameter templates. Values:<br><br><br>* `System`: System template.<br><br>* `User`: User template. |
|TemplateType |String |Mysql |The database type of the parameter template, with the default value of `Mysql`. |
|TemplateTypeVersion |String |MySQL_5_7 |Parameter template database version, value range:<br><br><br>* `MySQL_5_7`: MySQL version 5.7.<br><br>* `MySQL_8_0`: MySQL version 8.0. |
|UpdateTime |String |2022\-10\-10 10:10:37 |The modification time of the template. |
|EngineType |String |RocksDB |Database engine type. Valid values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br>tip<br><br>When used as a request parameter, the default value is `InnoDB`. |

## Sample request

```json
POST /?Action=DescribeParameterTemplate&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateId": "mysql-a3ba0f1eee19****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230809193449E3FDCA6F98F2188DCD5D",
        "Action": "DescribeParameterTemplate",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TemplateInfo": {
            "AccountId": "2100000746",
            "CreateTime": "2023-08-09 19:23:30",
            "NeedRestart": false,
            "ParameterNum": 2,
            "ProjectName": "",
            "TemplateCategory": "DBEngine",
            "TemplateDesc": "这是一段描述",
            "TemplateId": "mysql-a3ba0f1e****",
            "TemplateName": "test1234",
            "TemplateParams": [
                {
                    "Name": "auto_increment_increment",
                    "RunningValue": "2"
                },
                {
                    "Name": "auto_increment_offset",
                    "RunningValue": "3"
                }
            ],
            "TemplateSource": "User",
            "TemplateType": "MySQL",
            "TemplateTypeVersion": "MySQL_5_7",
            "UpdateTime": "2023-08-09 19:28:32"
        }
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
