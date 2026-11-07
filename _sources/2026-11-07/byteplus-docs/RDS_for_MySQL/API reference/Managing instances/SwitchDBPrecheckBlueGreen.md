---
title: "SwitchDBPrecheckBlueGreen"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/SwitchDBPrecheckBlueGreen"
---

Call the SwitchDBPrecheckBlueGreen API to initiate a pre\-check for a blue\-green deployment switch.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=SwitchDBPrecheckBlueGreen&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |The ID of the blue instance in the blue\-green deployment. |
|Recheck |Boolean |No |false |Whether to restart the pre\-check. Values:<br><br><br>* `true`: yes. Restarts the pre\-check and returns the event ID of the current pre\-check.<br><br>* `false`: no. If the instance has a valid pre\-check result, the system returns the event ID of the last successful pre\-check without starting a new one. Otherwise, the system starts a new pre\-check. Default value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has no default value.</div><br> |
|Endpoints |Array of [SwitchDBEndpoint](https://docs.byteplus.com/en/docs/40/61057#switchdbendpoint) |No |See the request example. |Instance connection information. |


<span id="switchdbendpoint"></span>
### SwitchDBEndpoint


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|OriginEndpointId |String |Yes |mysql\-f83edc2e\*\*\*\*\-cluster |The connection endpoint ID of the blue instance. |
|TargetEndpointId |String |Yes |mysql\-06c7db72\*\*\*\*\-cluster |The connection endpoint ID of the green instance. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|EventId |String |20250724171204259F91326A6ACD0B\*\*\*\*\-5176f4 |Event ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=SwitchDBPrecheckBlueGreen&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-f83edc2e****",
    "Recheck": false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202507241749444958F4F8739B10011CCC-32eedc",
        "Action": "SwitchDBPrecheckBlueGreen",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "EventId": "20250724171204259F91326A6ACD0B****-5176f4"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
