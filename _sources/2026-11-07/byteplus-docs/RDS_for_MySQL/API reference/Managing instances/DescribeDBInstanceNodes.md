---
title: "DescribeDBInstanceNodes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancenodes"
---

Call the DescribeDBInstanceNodes API to query the detailed information of instance nodes.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceNodes&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-25651c34\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|NodeInfos |Array of [InstanceNode](https://docs.byteplus.com/en/docs/40/54508#instancenode) |Refer to the Sample response. |Details of the instance node. |


<span id="instancenode"></span>
### InstanceNode


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CPUUsedPercentage |Double |0.015 |CPU utilization of a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The return value here is a proportional coefficient ranging from 0 to 1, not a percentage value from 0 to 100.</div><br> |
|LastIOError |String |\- |The last I/O error of the node, which may be returned as empty. |
|LastSQLError |String |\- |The last SQL error of the node, which may be returned as empty. |
|MemoryUsedPercentage |Double |0.1727 |Memory usage rate of the node. May not be returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The return value here is a proportional coefficient ranging from 0 to 1, not a percentage value from 0 to 100.</div><br> |
|NodeId |String |mysql\-25651c34\*\*\*\*\-md1b4\-0 |Node ID. |
|NodeStatus |String |Running |Node status, with values:<br><br><br>* `Running`: running.<br><br>* `Creating`: creating.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: restarting.<br><br>* `Restoring`: recovering.<br><br>* `Updating`: modifying.<br><br>* `Upgrading`: upgrading.<br><br>* `InOperation`: In operation.<br><br>* `Error`: error. |
|NodeType |String |Primary |The primary node requires NodeType to be set to `Primary`, and the read\-only node does not require it. |
|SlaveIORunning |Boolean |true |Whether the IO thread of the node is normal. May not be returned. |
|SlaveSQLRunning |Boolean |true |Whether the node's SQL thread is normal. May not be returned. |
|SpaceUsedPercentage |Double |0.042298582457005976 |The storage usage of the node. May not be returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The return value here is a proportional coefficient ranging from 0 to 1, not a percentage value from 0 to 100.</div><br> |
|SyncDelay |Integer |73 |Synchronized latency of the node. The unit is milliseconds. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstanceNodes&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "instanceid": "mysql-25651c34****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250605202902007681F01031C6680603-3c0c42",
        "Action": "DescribeDBInstanceNodes",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "NodeInfos": [
            {
                "CPUUsedPercentage": 0.015,
                "MemoryUsedPercentage": 0.1727,
                "NodeId": "mysql-25651c34****-md1b4-0",
                "NodeStatus": "Running",
                "NodeType": "Primary",
                "SpaceUsedPercentage": 0.042298582457005976,
                "ZoneId": "cn-beijing-a"
            },
            {
                "CPUUsedPercentage": 0,
                "MemoryUsedPercentage": 0.1873,
                "NodeId": "mysql-25651c34****-sf57c-0",
                "NodeStatus": "Running",
                "NodeType": "Secondary",
                "SlaveIORunning": true,
                "SlaveSQLRunning": true,
                "SpaceUsedPercentage": 0.042298582457005976,
                "SyncDelay": 0,
                "ZoneId": "cn-beijing-a"
            },
            {
                "CPUUsedPercentage": 0,
                "MemoryUsedPercentage": 0.1818,
                "NodeId": "mysql-25651c34****-r399d",
                "NodeStatus": "Running",
                "NodeType": "ReadOnly",
                "SlaveIORunning": true,
                "SlaveSQLRunning": true,
                "SpaceUsedPercentage": 0.042298582457005976,
                "SyncDelay": 73,
                "ZoneId": "cn-beijing-a"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
