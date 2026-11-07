---
title: "ListParameterTemplates"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/listparametertemplates1"
---

Call the ListParameterTemplates API to query the parameter template list of a MySQL instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TemplateCategory |String |No |DBEngine |Template category, with the value of `DBEngine`(database engine parameters). |
|TemplateType |String |No |Mysql |The database type of the parameter template, with the default value of `Mysql`. |
|TemplateTypeVersion |String |No |MySQL_5_7 |Database version of the parameter template. Valid values:<br><br><br>* `MySQL_5_7`: MySQL 5.7 version.<br><br>* `MySQL_8_0`: MySQL 8.0 version. |
|TemplateSource |String |No |System |Source of the parameter template. Valid values:<br><br><br>* `System`: System.<br><br>* `User`: User. |
|Limit |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 100. The default value is 10. |
|Offset |Integer |No |0 |Current page query offset. The minimum value is 0. The default value is 0. |
|ProjectName |String |No |default |The project it belongs to.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this request parameter needs to be specified. |
|TemplateName |String |No | |Template Name. |
|EngineType |String |No |RocksDB |Database engine type. Valid values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br>tip<br><br>When used as a request parameter, the default value is `InnoDB`. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |10 |Total number of parameter templates. |
|TemplateInfos |Object[] |Please refer to the response example. |Parameter template list. |
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
POST /?Action=ListParameterTemplates&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TemplateSource": "System"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308091938333AE08C8EA08E6091AACA",
        "Action": "ListParameterTemplates",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TemplateInfos": [
            {
                "AccountId": "0",
                "CreateTime": "2023-11-20 16:51:22",
                "NeedRestart": true,
                "ParameterNum": 203,
                "ProjectName": "",
                "TemplateCategory": "DBEngine",
                "TemplateDesc": "sync_binlog=1000, innodb_flush_log_at_trx_commit=2, async",
                "TemplateId": "mysql-sys-dec1f86e42872d8f",
                "TemplateName": "MySQL_8.0_HighPerformance",
                "TemplateParams": [],
                "TemplateSource": "System",
                "TemplateType": "MySQL",
                "TemplateTypeVersion": "MySQL_8_0",
                "UpdateTime": "2024-01-22 11:22:37"
            },
            {
                "AccountId": "0",
                "CreateTime": "2023-11-20 16:51:22",
                "NeedRestart": true,
                "ParameterNum": 203,
                "ProjectName": "",
                "TemplateCategory": "DBEngine",
                "TemplateDesc": "sync_binlog=1, innodb_flush_log_at_trx_commit=1, async",
                "TemplateId": "mysql-sys-fc06ea5a4b54c301",
                "TemplateName": "MySQL_8.0_Async",
                "TemplateParams": [],
                "TemplateSource": "System",
                "TemplateType": "MySQL",
                "TemplateTypeVersion": "MySQL_8_0",
                "UpdateTime": "2024-01-22 11:22:37"
            }
        ],
        "Total": 2
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
