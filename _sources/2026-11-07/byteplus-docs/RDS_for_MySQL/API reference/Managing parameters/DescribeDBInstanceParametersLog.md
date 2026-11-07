---
title: "DescribeDBInstanceParametersLog"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceparameterslog"
---

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-h441603c\*\*\*\* |Instance ID. |
|StartTime |String |Yes |2020\-03\-01T00:00:00Z |Query start time. Format: `yyyy-MM-ddTHH:mm:ssZ` (UTC time). |
|EndTime |String |Yes |2020\-03\-01T10:00:00Z |Query end time. Format: `yyyy-MM-ddTHH:mm:ssZ` (UTC time). |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value: 1. |
|PageSize |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 1,000. The default value is 10. |

## Response parameter

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of records returned by the query. |
|ParameterChangeLogs |Array of [ParameterChangeLogObject](https://docs.byteplus.com/en/docs/40/15453#parameterchangelogobject) |None. |Parameter modification history list. |

### ParameterChangeLogObject

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ParameterName |String |innodb_stats_sample_pages |Parameter name. |
|Status |String |Applied |State. Values:<br><br><br>* `Applied`: effective.<br><br>* `Invalid`: not effective.<br><br>* `Syncing`: applying, not yet effective. |
|NewParameterValue |String |3 |Parameter value (after applying template). |
|OldParameterValue |String |8 |Parameter value (before applying template) |
|ModifyTime |String |2020\-03\-01T00:00:00Z |Timestamp for modifying parameters. Format: `yyyy-MM-ddTHH:mmZ` (UTC time). |
|CustomNodeIds |Array of String |[<br><br>"mysql\-b630addf\*\*\*\*\-r1415"<br><br>] |A list of node IDs to which the parameter modification is applied. |
|ParamApplyScope |String |AllNode |Specifies the application scope of the parameter modification. Values:<br><br><br>* `AllNode`: All nodes.<br><br>* `OnlyMasterSlaveNode`: only the primary and secondary nodes.<br><br>* `OnlyReadOnlyNode`: all read\-only nodes.<br><br>* `CustomNode`: the specified read\-only node.<br><br><br>> **tip**<br><br><br>> When the returned CustomNodeIds field is not empty, the value of this field is only a **placeholder retained for compatibility** and carries no practical meaning.<br> |
|ApplyParamTemplateInfo |Object of [ApplyParamTemplateInfo](https://docs.byteplus.com/en/docs/40/15453#applyparamtemplateinfo) | |Parameter template information |

### ApplyParamTemplateInfo

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TemplateId |String | |Parameter template ID |
|TemplateName |String | |Parameter template name |
|TemplateSource |String |System |Backup creator. Values:<br><br><br>* `System`: system.<br><br>* `User`: user. |

## Sample

Call the DescribeDBInstanceParametersLog API to query the modification history of an instance parameter.

### Sample request

```json
POST /?Action=DescribeDBInstanceParametersLog&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-8baa525f****",
    "StartTime": "2023-01-01T00:00:00Z",
    "EndTime": "2024-11-10T00:00:00Z"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024101020003027D28AE4A308840C6BC8-7f9cbd",
        "Action": "DescribeDBInstanceParametersLog",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ParameterChangeLogs": [
            {
                "ApplyParamTemplateInfo": {
                    "TemplateId": "mysql-8baa525f****",
                    "TemplateName": "Parameters_demo",
                    "TemplateSource": "User"
                },
                "ModifyTime": "2024-10-10T11:55:42.000Z",
                "NewParameterValue": "2",
                "OldParameterValue": "1",
                "ParamApplyScope": "OnlyMasterSlaveNode",
                "ParameterName": "auto_increment_increment",
                "Status": "Applied"
            },
            {
                "CustomNodeIds": [
                    "mysql-8baa525f****-r6e37"
                ],
                "ModifyTime": "2024-10-10T11:55:42.000Z",
                "NewParameterValue": "2",
                "OldParameterValue": "1",
                "ParamApplyScope": "OnlyMasterSlaveNode",
                "ParameterName": "auto_increment_increment",
                "Status": "Applied"
            }
        ],
        "Total": 2
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
