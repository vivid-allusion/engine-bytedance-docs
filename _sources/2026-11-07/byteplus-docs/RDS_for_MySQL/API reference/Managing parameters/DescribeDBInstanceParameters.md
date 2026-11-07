---
title: "DescribeDBInstanceParameters"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceparameters"
---

Call the DescribeDBInstanceParameters API to query instance parameters.

## Request type

Synchronous request.

## Request parameters

|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-h441603c\*\*\*\* |Instance ID. |
|ParameterName |String |No |auto_increment_increment |Parameter name. |
|NodeId |String |No |mysql\-8baa525f\*\*\*\*\-mf741\-0 |Queries the parameter setting of the specified node.<br><br>> **tip**<br><br><br>> If this field is not set, only the parameter settings for the primary and secondary nodes are returned.<br> |

## Response parameters

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-h441603c\*\*\*\* |Instance ID. |
|DBEngine |String |Mysql |Database type. The value is fixed to `Mysql`. |
|DBEngineVersion |String |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0. |
|ParameterCount |Integer |56 |Number of parameters. |
|Parameters |Array of [InstanceParametersObject](https://docs.byteplus.com/en/docs/40/15445#instanceparametersobject) |Refer to the Sample response. |The list of parameters of the current instance. |
|ApplyParamTemplateInfo |Object of [ApplyParamTemplateInfo](https://docs.byteplus.com/en/docs/40/15445#applyparamtemplateinfo) | |Parameter template information |

### InstanceParametersObject

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ParameterName |String |auto_increment_increment |Parameter name. |
|ParameterValue |String |1 |Parameter value. Specifically refers to the current instance running value. |
|CheckingCode |String |[1\-65535] |Parameter value range. |
|ForceRestart |Boolean |false |Whether the parameter modification requires an instance restart. |
|ParameterDefaultValue |String |1 |Parameter default value. |
|ParameterDescription |String |Auto\-increment columns are incremented by this. |Parameter description. |
|Expression |String |`{MAX(DBInstanceCpu, 2)}` |Parameter expression. |

### ApplyParamTemplateInfo

|Parameter |Type |Sample value |Description |
|---|---|---|---|
|TemplateId |String | |Parameter template ID |
|TemplateName |String | |Parameter template name |
|TemplateSource |String |System |Backup creator. Values:<br><br><br>* `System`: system.<br><br>* `User`: user. |

## Sample

### Sample request

```json
POST /?Action=DescribeDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-8baa525f****",
    "ParameterName": "auto_increment_increment"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111141659DE3A3BEFAE571076CBB2",
        "Action": "DescribeDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ApplyParamTemplateInfo": {
            "TemplateId": "mysql-8baa525f****",
            "TemplateName": "Parameters_demo",
            "TemplateSource": "User"
        },
        "DBEngine": "Mysql",
        "DBEngineVersion": "MySQL_5_7",
        "InstanceId": "mysql-8baa525f****",
        "ParameterCount": 1,
        "Parameters": [
            {
                "CheckingCode": "[1-65535]",
                "ForceRestart": false,
                "ParameterDefaultValue": "1",
                "ParameterDescription": "Auto-increment columns are incremented by this.",
                "ParameterName": "auto_increment_increment",
                "ParameterValue": "1"
            }
        ]
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
