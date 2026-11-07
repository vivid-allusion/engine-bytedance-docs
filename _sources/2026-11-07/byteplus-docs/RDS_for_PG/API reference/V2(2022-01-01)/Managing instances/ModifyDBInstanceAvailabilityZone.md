---
title: "ModifyDBInstanceAvailabilityZone"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceavailabilityzone"
---

Call the ModifyDBInstanceAvailabilityZone API to migrate nodes from one AZ to another AZ in the same region.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-aa7e1633\*\*\*\* |Instance ID. |
|NodeInfo |Array of [NodeZoneInfoObject](https://docs.byteplus.com/en/docs/61/15774#nodezoneinfoobject) |Yes |Refer to the request example. |Nodes to be migrated and the destination availability zone.<br><br><br>* Only migrating a single\-availability\-zone instance to a multi\-availability\-zone instance is supported.<br><br>* Only support migrating secondary nodes or read\-only nodes, and support migrating secondary nodes and read\-only nodes simultaneously. |


<span id="nodezoneinfoobject"></span>
### NodeZoneInfoObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|NodeId |String |Yes |postgres\-ca7b7019\*\*\*\* |Node ID. You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) API to query the node information of the instance. |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone of each node in the instance. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones) API to query the availability zone information of the current region. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-aa7e1633\*\*\*\* |Instance ID. |
|OrderId |String | |Order ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The return value of this field is empty.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBInstanceAvailabilityZone&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-aa7e1633****",
    "NodeInfo": [
        {
            "NodeId": "postgres-aa7e1633****",
            "ZoneId": "cn-beijing-b"
        },
        {
            "NodeId": "postgres-aa7e1633****-pxcm",
            "ZoneId": "cn-beijing-c"
        },
        {
            "NodeId": "postgres-aa7e1633****-roe6c0",
            "ZoneId": "cn-beijing-b"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202401082241020D9550F8209B0738F56A",
        "Action": "ModifyDBInstanceAvailabilityZone",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "postgres-aa7e1633****",
        "OrderId": ""
    }
}
```
