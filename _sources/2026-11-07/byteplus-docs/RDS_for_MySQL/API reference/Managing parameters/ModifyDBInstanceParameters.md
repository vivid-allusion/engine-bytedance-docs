---
title: "ModifyDBInstanceParameters"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceparameters"
---

## Request type

Asynchronous request.

## Precautions

If the `innodb_buffer_pool_size` parameter is modified, the system verifies each node set in the `ParamApplyScope` parameter one by one to check whether its value meets the value range requirements. If verification fails for any node, this request is rejected synchronously, and no subsequent task is created.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-h441603c\*\*\*\* |Instance ID. |
|Parameters |Array of [ParametersObject](https://docs.byteplus.com/en/docs/40/15452#parametersobject) |Yes |Null |Parameter value object. It is the parameter values customized by the user based on the default parameter template. |
|TemplateId |String |No |mysql\-411668b4ab18\*\*\*\* |The ID of the parameter template used to modify the instance parameters.<br><br>> **tip**<br><br><br><br>* > The parameter template must have the same engine version as the instance.<br><br><br>* > If this field is specified, the parameter settings from the specified parameter template are used, and the settings in the Parameters field are ignored. To modify the parameters of the instance using a parameter template, you can pass an empty array for the Parameters field.<br> |
|ParamApplyScope |String |No |AllNode |Specifies the application scope of the parameter modification. Values:<br><br><br>* `AllNode`: all nodes. Default value.<br><br>* `OnlyMasterSlaveNode`: only the primary and secondary nodes.<br><br>* `OnlyReadOnlyNode`: all read\-only nodes.<br><br>* `CustomNode`: the specified read\-only node.<br><br><br>> **tip**<br><br><br><br>* > This parameter applies only when the instance type is a double node.<br><br><br>* > If this parameter is not specified, the default value is `AllNode`.<br><br><br>* > When the value is `OnlyReadOnlyNode` or `CustomNode`, the instance must have read\-only nodes.<br><br><br>* > If the modified parameter needs to take effect on all nodes, this parameter value must be `AllNode`.<br> |
|CustomNodeIds |Array of String |No |["mysql\-c7a79d83\*\*\*\*\-r417e"] |The ID of the read\-only node to which the parameter modifications apply.<br><br>> **tip**<br><br><br><br>* > This parameter takes effect only when the value of the `ParamApplyScope` parameter is **CustomNode**. `This parameter must be non-empty at this time`.<br><br><br>* > The value must be a **valid read\-only node ID** for the current instance.<br> |

### ParametersObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|ParameterName |String |No |auto_increment_increment |Parameter name. |
|ParameterValue |String |No |1 |Parameter value. The parameter value or expression to be set. |

## Response parameter

null

## Sample

### Sample request

```json
POST /?Action=ModifyDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-8baa525f****",
    "Parameters": [
        {
            "ParameterName": "auto_increment_increment",
            "ParameterValue": "1"
        }
    ]
}
```

### Sample response

Call the ModifyDBInstanceParameters API to modify instance parameters.

```json
{
    "ResponseMetadata": {
        "RequestId": "20230111142239CD77A5FDFBB20E7FD96C",
        "Action": "ModifyDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
