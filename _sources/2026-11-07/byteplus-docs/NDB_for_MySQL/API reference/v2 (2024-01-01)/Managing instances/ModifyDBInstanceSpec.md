---
title: "ModifyDBInstanceSpec"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec_v2"
---

Call the ModifyDBInstanceSpec to modify the node configuration of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id="OEIBJT9g"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceSpec&serviceCode=vedbm&version=2024-01-01&groupName=)


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).

* When reducing nodes, the system will first delete nodes with larger node ID numbers. Different node types have different effects on connection endpoints:

   * The target delete node is the primary node

      When the target deletion node is the primary node, you need to switch the primary node first. It is recommended to switch the node with the smallest node ID number to the primary node, and then reduce the number of nodes. For operation details, see [Switching to primary node](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node).

   * The target delete node is a read\-only node

      * Custom read\-only endpoint: If a custom read\-only endpoint is associated only with the read\-only node to be deleted, you must first call the [ModifyDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpoint) API to associate this endpoint with other read\-only nodes. If the endpoint is not in use, you can also delete it directly by calling the [DeleteDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBEndpoint) API. After that, you can reduce the number of nodes.

      * Custom read and write connection endpoint: If the custom read/write endpoint is associated with the primary node and the read\-only node to be deleted, after reducing the read\-only node, the read/write endpoint will not be able to read\-write separation, resulting in an increase in pressure on the primary node. It is recommended to call the [ModifyDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpoint) API to associate other read\-only nodes with the read\-write endpoint before reducing the number of nodes.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-h441603c68aaa\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|PrePaidStorageInGB |Integer |No |60 |* If the storage billing type is pay\-as\-you\-go, you do not need to select storage capacity. The storage capacity will automatically scale up and down as the amount of data increases or decreases, and will be billed on an hourly basis based on actual usage.<br><br>* If the storage billing type is yearly or monthly subscription, you need to enter the changed storage space size in steps of 10 GiB, with an increment of 10 GiB.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The storage space range varies by node specification. For details, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specification</a>.</div><br> |
|ScheduleType |String |No |Immediate |Execution method. Possible values:<br><br><br>* `Immediate`: Execute now (default).<br><br>* `MaintainTime`: Execute during the maintenance window. |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/265/113319#nodeinfoobject) |No |See the request example. |Specification and configuration of the instance node. |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|NodeType |String |Yes |DBEngine |Node type. Value:<br><br>`DBEngine`: Primary node/Read\-only node. |
|NodeSpec |String |Yes |vedb.mysql.x4.large |The node specification code for the instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For detailed information on instance node specifications, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specifications</a>.</div><br> |
|NodeNumber |Integer |Yes |2 |Number of nodes.<br><br>When `NodeType` is set to `DBEngine` (Primary node/Read\-only node), the value of this parameter ranges from 2 to 16.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">By default, at least two nodes (one primary node and one read\-only node) are required to ensure high cluster availability.</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |Availability zone ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> API to query the availability zone ID of the specified instance.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-h441603c68aaa\*\*\*\* |Instance ID. |
|OrderId |String |Order707643373078888\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Request example

Change the primary node/read\-only node.

```JSON
POST /?Action=ModifyDBInstanceSpec&Version=2024-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b76789****
{
    "InstanceId": "vedbm-fihrnbtgrmr4",
    "NodeInfo": [
        {
            "ZoneId": "cn-chongqing-a",
            "NodeNumber": 3,
            "NodeSpec": "vedb.mysql.x8.large",
            "NodeType": "DBEngine"
        }
    ]
}

```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202307191557433BA18653C86F63A04B1B",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "vedbm-gzwdsf9b****",
        "OrderId": "Order725743560891294****"
    }
}
```


<span id="i7CNOXjC"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
