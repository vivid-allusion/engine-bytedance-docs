---
title: "DescribeSlots"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describeslots"
---

Call the DescribeSlots API to query the replication slots of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-96138f57\*\*\*\* |ID of the instance to which the replication slot belongs. |
|SlotName |String |No |ExampleOfSlotName |Name of the replication slot to query.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value: none. If this field is not provided, all results under the query conditions limited by other parameters will be returned.</div><br> |
|SlotType |String |No |logical |Types of replication slots. Values:<br><br><br>* `physical`: physical replication slot.<br><br>* `logical`: logical replication slot.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">No default value. Returns all query results under other parameter\-restricted query conditions if this field is not passed.</div><br> |
|Plugin |String |No |pgoutput |Name of the extension used by the logical replication slot to parse WAL logs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When slottype is <code>physical</code>, no value needs to be passed for this field.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Default value. Returns all query results under other parameter\-restricted query conditions if this field is not passed.</div><br> |
|Database |String |No |postgres |Database where the replication slot is located.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When SlotType is <code>physical</code>, no value is needed for this field.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Default value. When this field is not passed, all query results within the query conditions defined by other parameters are returned.</div><br> |
|Temporary |Boolean |No |true |Whether it is a temporary copy slot. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. Returns all query results under other parameter\-restricted query conditions if this field is not passed.</div><br> |
|SlotStatus |String |No |ACTIVE |Status of replication slot. Values:<br><br><br>* `ACTIVE`: active.<br><br>* `INACTIVE`: inactive.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. When this field is not passed, all query results within the query conditions defined by other parameters are returned.</div><br> |
|IPAddress |String |No |10.xxx.xxx.1 |IP address. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |3 |Quantity of replication slots for the instance. |
|ReplicationSlots |Array of [ReplicationSlotObject](https://docs.byteplus.com/en/docs/61/28077#replicationslotobject) |Refer to the sample response. |Slots for copying specified by query conditions in the instance. |


<span id="replicationslotobject"></span>
### ReplicationSlotObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|SlotName |String |Slot000003 |Slot name. |
|SlotType |String |logical |Types of replication slots. Values:<br><br><br>* `physical`: physical replication slot.<br><br>* `logical`: logical replication slot. |
|Plugin |String |pgoutput |Extension name used with the logical replication slot to parse WAL logs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When slotType is <code>physical</code>, this field returns<code>null</code>。</div><br> |
|Database |String |postgres |Database where the copy slot resides.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When SlotType is set to <code>physical</code>, this field returns<code>null</code>。</div><br> |
|Temporary |Boolean |false |Whether it is a temporary copy slot. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|SlotStatus |String |INACTIVE |Status of replication slot. Values:<br><br><br>* `ACTIVE`: active.<br><br>* `INACTIVE`: inactive. |
|WalDelay |Long |50327736 |The accumulated WAL logs corresponding to the replication slots. Unit: Byte. |
|IPAddress |String |10.xxx.xxx.1 |IP address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only active replication slots have IP addresses.</div><br> |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeSlots&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-96138f57****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202407181601463F9A69D65646D0A65A1B-262141",
        "Action": "DescribeSlots",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ReplicationSlots": [
            {
                "Database": "null",
                "Plugin": "null",
                "SlotName": "Slot000001",
                "SlotStatus": "INACTIVE",
                "SlotType": "physical",
                "Temporary": false,
                "WalDelay": 0
            },
            {
                "Database": "null",
                "Plugin": "null",
                "SlotName": "Slot000002",
                "SlotStatus": "INACTIVE",
                "SlotType": "physical",
                "Temporary": false,
                "WalDelay": 50331608
            },
            {
                "Database": "postgres",
                "Plugin": "pgoutput",
                "SlotName": "Slot000003",
                "SlotStatus": "INACTIVE",
                "SlotType": "logical",
                "Temporary": false,
                "WalDelay": 50327792
            },
            {
                "Database": "postgres",
                "Plugin": "pgoutput",
                "SlotName": "Slot000004",
                "SlotStatus": "INACTIVE",
                "SlotType": "logical",
                "Temporary": false,
                "WalDelay": 50327736
            },
            {
                "Database": "postgres",
                "Plugin": "pgoutput",
                "SlotName": "Slot000005",
                "SlotStatus": "ACTIVE",
                "SlotType": "logical",
                "Temporary": true,
                "WalDelay": 50327624
            }
        ],
        "Total": 5
    }
}
```
