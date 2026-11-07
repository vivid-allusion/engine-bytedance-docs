---
title: "ModifyReadOnlyNodeDelayReplicationTime"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyreadonlynodedelayreplicationtime"
---

Call the ModifyReadOnlyNodeDelayReplicationTime API to configure the delayed replication feature for a read\-only node.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only the read/write endpoints of double node instances support this setting.

* When a read\-only node in the instance is associated with other nodes under the same endpoint, configuring replication delay for this read\-only node is not supported.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyReadOnlyNodeDelayReplicationTime&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-3fb9a5be\*\*\*\* |The Instance ID of the instance to which the read\-only node to be queried belongs. |
|NodeId |String |Yes |mysql\-3fb9a5be\*\*\*\*\-r3e01 |The Node ID of the read\-only node to query. |
|DelayReplicationTime |Long |Yes |1000 |The Data delay time for the read\-only node. The value ranges from 0 to 604,800. The unit is Second.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A value of 0 disables replication delay for the read\-only node.</div><br> |
|UpdateEndpointIds |Array of String |Yes |["mysql\-3fb9a5be\*\*\*\*\-custom\-a774","mysql\-3fb9a5be\*\*\*\*\-cluster"] |The ID of the connection endpoint whose association with the read\-only node needs to be canceled to set the replication delay. Call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) API to query the connection endpoint associated with the read\-only node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After you enable replication delay for a read\-only node, the node can only be the sole node of a connection endpoint. Therefore, when you enable replication delay, you must cancel the association between the read\-only node and other endpoints.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When DelayReplicationTime is set to 0, which disables replication delay for the read\-only node, UpdateEndpointIds is optional.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the read\-only node is not associated with a connection endpoint, UpdateEndpointIds is optional.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyReadOnlyNodeDelayReplicationTime&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-3fb9a5be****",
    "NodeId": "mysql-3fb9a5be****-ra779",
    "DelayReplicationTime": 1000,
    "UpdateEndpointIds": [
        "mysql-3fb9a5be****-custom-a774",
        "mysql-3fb9a5be****-cluster"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202312251441147989AF4644F5D7556D08",
        "Action": "ModifyReadOnlyNodeDelayReplicationTime",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
