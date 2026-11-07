---
title: "ModifyDBProxySpec"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyspec"
---

## Request type

Asynchronous request.

## Precautions

Database proxy configurations cannot be modified for overdue or recovering instances.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-cf4f3ddc\*\*\*\* |Instance ID. |
|ProxyNodeCustom |Object of [ProxyNodeCustomObject](https://docs.byteplus.com/en/docs/40/54511#proxynodecustomobject) |Yes |See the request example. |The specification of the database proxy service for the instance. |
|SwitchType |String |No |MaintainTime |Execution time. The valid values are:<br><br><br>* `Immediate`: switch now (default).<br><br>* `MaintainTime`: switch during the maintenance window.<br><br>* `SpecifiedTime`: switch during the specified time period.<br><br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) API to query the instance's maintenance window.<br><br><br>* > When the value is `SpecifiedTime`, the start and end time for the time period must be set in the `SpecifiedSwitchStartTime` and `SpecifiedSwitchEndTime` parameters.<br> |
|SpecifiedSwitchStartTime |String |No |2024\-12\-25T14:00:00Z |The start time of the specific time period for execution(UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br>> **tip**<br><br><br><br>* > When SwitchType is set to `SpecifiedTime`, this parameter is required.<br><br><br>* > The start time of the task cannot be later than seven days after the current date.<br> |
|SpecifiedSwitchEndTime |String |No |2024\-12\-25T15:59:00Z |The end time of the specific time period for execution (UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br>> **tip**<br><br><br><br>* > When SwitchType is set to `SpecifiedTime`, this parameter is required.<br><br><br>* > The minimum time period is one hour and fifty\-nine minutes.<br><br><br>* > Time periods cannot be set across days. The task's start and end times must be within a 24\-hour window.<br> |

### ProxyNodeCustomObject

|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Values are as follows:<br><br><br>* Value range: Upper limit 1024.<br><br>* For multiple node instances:<br><br>   * The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`.<br><br>* For double node instances:<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.5`. |

## Response parameter

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|OrderId |String |(Null) |The configuration order number. |

Call the ModifyDBProxySpec API to modify the proxy configuration of an instance.

## Sample

### Sample request

```json
POST /?Action=ModifyDBProxySpec&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-cf4f3ddc****",
    "ProxyNodeCustom": {
        "CpuNum": 4
    }
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250625164341A4083DEECF7C3A009742-25785d",
        "Action": "ModifyDBProxySpec",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
