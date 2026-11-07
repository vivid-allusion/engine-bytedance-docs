---
title: "UpgradeDBInstanceEngineMajorVersion"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/UpgradeDBInstanceEngineMajorVersion"
---

Call the UpgradeDBInstanceEngineMajorVersion API to upgrade the major kernel version of an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

You can only upgrade MySQL 5.7 instances to MySQL 8.0. You cannot upgrade MySQL 5.7 or MySQL 8.0 instances to MySQL 8.4.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpgradeDBInstanceEngineMajorVersion&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-7510ba07\*\*\*\* |Instance ID. |
|TargetMajorVersion |String |Yes |MySQL 8.0.43 |The target major version for the instance upgrade. Only `MySQL 8.0.43` is currently supported. |
|MySQLSlaveDelayThreshold |Integer |Yes |10 |Data validation latency threshold. An integer from 1 to 10. Unit: seconds. |
|ObservationHours |Integer |No |24 |Set the observation duration after the instance upgrade. The value can be set to an integer between 0 and 72, in hours. The default value is 24. |
|SwitchType |String |No |MaintainTime |Execution time. The valid values are:<br><br><br>* `Immediate`: switch now (default).<br><br>* `MaintainTime`: switch during the maintenance window.<br><br>* `SpecifiedTime`: switch during the specified time period.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail">DescribeDBInstanceDetail</a> API to query the instance's maintenance window.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the value is <code>SpecifiedTime</code>, you must set the start and end time of the time period in the <code>SpecifiedSwitchStartTime</code> and <code>SpecifiedSwitchEndTime</code> parameters.</div><br> |
|SpecifiedSwitchStartTime |String |No |2024\-12\-25T14:00:00Z |The start time of the specific time period for execution(UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When SwitchType is set to <code>SpecifiedTime</code>, this parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The start time of the task cannot be later than seven days after the current date.</div><br> |
|SpecifiedSwitchEndTime |String |No |2024\-12\-25T15:59:00Z |The end time of the specific time period (UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of SwitchType is <code>SpecifiedTime</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is one hour and fifty\-nine minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days. The task's start and end times must be within a 24\-hour window.</div><br> |
|EstimateOnly |Boolean |No |false |Whether to start an evaluation. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you start a configuration change evaluation, the system evaluates the specifications determined by other fields, but the change is not actually executed.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|PreparedMinutes |Integer |30 |The duration of the preparation phase, in minutes. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=UpgradeDBInstanceEngineMajorVersion&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-0f7032f1****",
    "TargetMajorVersion": "MySQL 8.0.32",
    "MySQLSlaveDelayThreshold": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250410162906B3FB2CBF4C3BBEC59793-964567",
        "Action": "UpgradeDBInstanceEngineMajorVersion",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "EventId": "20250410162906B3FB2CBF4C3BBEC59793-964567",
        "PreparedMinutes": 18
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
