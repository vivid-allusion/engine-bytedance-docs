---
title: "SwitchDBBlueGreen"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/SwitchDBBlueGreen"
---

Call the SwitchDBBlueGreen API to switch the blue\-green deployment.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=SwitchDBBlueGreen&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |The ID of the blue instance in the blue\-green deployment. |
|Endpoints |Array of [SwitchDBEndpoint](https://docs.byteplus.com/en/docs/40/61065#switchdbendpoint) |Yes |See the request example. |Instance connection information |
|SwitchType |String |No |MaintainTime |Execution time. The valid values are:<br><br><br>* `Immediate`: switch now (default).<br><br>* `MaintainTime`: switch during the maintenance window.<br><br>* `SpecifiedTime`: switch during the specified time period.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail">DescribeDBInstanceDetail</a> API to query the instance's maintenance window.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the value is <code>SpecifiedTime</code>, you must set the start and end time of the time period in the <code>SpecifiedSwitchStartTime</code> and <code>SpecifiedSwitchEndTime</code> parameters.</div><br> |
|SpecifiedSwitchStartTime |String |No |2024\-12\-25T14:00:00Z |The start time of the specific time period for execution(UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When SwitchType is set to <code>SpecifiedTime</code>, this parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The start time of the task cannot be later than seven days after the current date.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Must be on the hour.</div><br> |
|SpecifiedSwitchEndTime |String |No |2024\-12\-25T15:59:00Z |The end time of the specific time period for execution (UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of SwitchType is <code>SpecifiedTime</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is one hour and fifty\-nine minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days. The task's start and end times must be within a 24\-hour window.</div><br> |


<span id="switchdbendpoint"></span>
### SwitchDBEndpoint


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|OriginEndpointId |String |Yes |mysql\-f83edc2e\*\*\*\*\-cluster |The connection endpoint ID of the blue instance. |
|TargetEndpointId |String |Yes |mysql\-06c7db72\*\*\*\*\-cluster |The connection endpoint ID of the green instance. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=SwitchDBBlueGreen&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-f83edc2e****",
    "Endpoints": [
        {
            "OriginEndpointId": "mysql-f83edc2e****-cluster",
            "TargetEndpointId": "mysql-06c7db72****-cluster"
        }
    ],
    "SwitchType": "Immediate"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025072419542973B0F32A7EF77611C384-1b83a0",
        "Action": "SwitchDBBlueGreen",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
