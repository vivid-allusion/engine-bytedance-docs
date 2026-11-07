---
title: "UpgradeDBInstanceEngineMajorVersionPrecheck"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/UpgradeDBInstanceEngineMajorVersionPrecheck"
---

Call the UpgradeDBInstanceEngineMajorVersionPrecheck API to pre\-check the instance before upgrading to a major version.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpgradeDBInstanceEngineMajorVersionPrecheck&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-7510ba07\*\*\*\* |Instance ID. |
|TargetMajorVersion |String |Yes |MySQL 8.0.43 |The target major version for the instance upgrade. Only `MySQL 8.0.43` is currently supported. |
|MySQLSlaveDelayThreshold |Integer |Yes |10 |Data validation latency threshold. An integer from 1 to 10. Unit: seconds. |
|Recheck |Boolean |No |true |Whether to restart the pre\-check. Values:<br><br><br>* `true`: yes. Restarts the pre\-check and returns the event ID of the current pre\-check.<br><br>* `false`: no. If the instance has a valid pre\-check result, the system returns the event ID of the last successful pre\-check without starting a new one. Otherwise, the system starts a new pre\-check. Default value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|EventId |String |20250410145924BA7FA42A930CFDBD\*\*\*\*\-83bd31 |Event ID for the pre\-check of upgrading the instance major version. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=UpgradeDBInstanceEngineMajorVersionPrecheck&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-7510ba07****",
    "TargetMajorVersion": "MySQL 8.0.43",
    "MySQLSlaveDelayThreshold": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250410150011691A1F663A1C51B9BE86-253c40",
        "Action": "UpgradeDBInstanceEngineMajorVersionPrecheck",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "EventId": "20250410145924BA7FA42A930CFDBD****-83bd31"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
