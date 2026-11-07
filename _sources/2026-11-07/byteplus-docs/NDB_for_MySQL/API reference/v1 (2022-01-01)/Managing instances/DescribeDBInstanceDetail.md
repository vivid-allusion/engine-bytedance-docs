---
title: "DescribeDBInstanceDetail"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail"
---

Call the DescribeDBInstanceDetail to query the instance details.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceDetail&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example |Description |
|---|---|---|---|
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/265/57344#chargedetailobject) |Refer to the Sample response. |Detailed billing information. |
|Nodes |Array of [NodeObject](https://docs.byteplus.com/en/docs/265/57344#nodeobject) |Refer to the Sample response. |Details of the instance node. |
|Endpoints |Array of [EndpointObject](https://docs.byteplus.com/en/docs/265/57344#endpointobject) |Refer to the Sample response. |Detailed information of the connection endpoint. |
|InstanceDetail |Object of [InstanceDetailObject](https://docs.byteplus.com/en/docs/265/57344#instancedetailobject) |Refer to the Sample response. |Instance basic information. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/265/57344#tagobject) |Refer to the Sample response. |An array object of tag keys and tag values bound to the instance. |


<span id="chargedetailobject"></span>
### ChargeDetailObject


|Name |Type |Example |Description |
|---|---|---|---|
|ChargeType |String |PostPaid |Calculate billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|ChargeStatus |String |Normal |Payment status:<br><br><br>* `Normal`: Normal.<br><br>* `Overdue`: Overdue.<br><br>* `Shutdown`: Shut down. |
|OverdueReclaimTime |String |2022\-09\-27T06:09:20Z |The estimated release time for a shutdown due to an overdue payment, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). |
|OverdueTime |String |2022\-10\-04T07:50:22Z |The shutdown time for an overdue instance, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). |
|AutoRenew |Boolean |true |Specifies whether to enable Due Automatic renewal for prepaid instances. Value:<br><br><br>* `true`: enables auto\-renewal.<br><br>* `false`: no automatic renewal. |
|ChargeStartTime |String |2023\-09\-22T08:08:35Z |The time when billing starts. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|ChargeEndTime |String |2023\-09\-22T08:08:35Z |The expiration time for subscription billing, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time). |


<span id="nodeobject"></span>
### NodeObject


|Name |Type |Example |Description |
|---|---|---|---|
|NodeId |String |vedbm\-h441603c68aaa\*\*\*\*\-\*\* |Node ID. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|NodeType |String |Primary |Node type. Value:<br><br><br>* `Primary`: Primary node.<br><br>* `ReadOnly`: Read\-only node. |
|vCPU |Integer |8 |CPU size. For example, a value of 1 indicates a CPU size of 1U. |
|Memory |Integer |32 |Memory size, in GiB. |
|NodeSpec |String |vedb.mysql.x4.xlarge |The node specification of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information on instance node specifications, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specifications</a>.</div><br> |
|FailoverPriority |Integer |5 |The priority of the node for switching to primary. The value ranges from 0 to 15. The larger the value, the higher the priority. |


<span id="endpointobject"></span>
### EndpointObject


|Name |Type |Example |Description |
|---|---|---|---|
|Addresses |Array of [AddressObject](https://docs.byteplus.com/en/docs/265/57344#addressobject) |Refer to the Sample response. |Address information. |
|AutoAddNewNodes |Boolean |true |Specifies whether to automatically associate new nodes. The valid values are:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|Description |String |Primary address |Address description. |
|EndpointId |String |vedbm\-h441603c68aaa\*\*\*\* |Instance endpoint ID. |
|EndpointName |String |Default_endpoint |The name of the instance connection endpoint. |
|EndpointType |String |Cluster |Connection endpoint type. The value can be:<br><br><br>* `Cluster`: Default endpoint.<br><br>* `Primary`: Primary node endpoint.<br><br>* `Custom`: Custom endpoint. |
|MasterAcceptReadRequests |Boolean |true |Whether the primary node accepts read requests. Only valid for endpoints in Read/Write mode.<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|NodeIds |Array of String |["vedbm\-r3sar8zi\*\*\*\*\-0", "vedbm\-r3sar8zi\*\*\*\*\-1"] |The list of nodes for the endpoint configuration. |
|ReadWriteMode |String |ReadWrite |The Read/Write mode of the endpoint. The values are:<br><br><br>* `ReadWrite`: Read/Write.<br><br>* `ReadOnly`: Read\-only. |
|DistributedTransaction |Boolean |true |Specifies whether to enable transaction splitting. This parameter is valid only for endpoints in Read/Write mode. Value:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |
|ConsistLevel |String |Session |The consistency level, which is valid only for endpoints in Read/Write mode. Value:<br><br><br>* `Eventual`: Eventual consistency.<br><br>* `Session`: Session consistency.<br><br>* `Global`: Global consistency. |
|ConsistTimeout |Integer |10000 |When the delay is large, the timeout time for the read\-only node to synchronize the latest data, in units of us, ranges from 1us to 100000000us.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConsistTimeoutAction |String |ReadMaster |The read\-only node synchronization data timeout policy supports the following two policies:<br><br><br>* `ReturnError`: returns an SQL error (wait replication complete timeout, please retry).<br><br>* `ReadMaster`: sends the request to the primary node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>ConsistLevel</code> is set to <code>Global</code> or <code>Session</code>.</div><br> |
|ConnectionPool |String |Off |Connection pool state. For more information about connection pools, refer to [Connection pool](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool). Value range:<br><br><br>* `Off`: Disable the connection pool.<br><br>* `Session`: Enables the session\-level connection pool.<br><br>* `Transaction`: Enables the transaction\-level connection pool. |


<span id="addressobject"></span>
### AddressObject


|Name |Type |Example |Description |
|---|---|---|---|
|DNSVisibility |Boolean |false |Resolution method. The current return value can only be `false` (Volcengine private network resolution). |
|Domain |String |vedbm\-fkfb7ag0\*\*\*\*.master.mysql.vedb.ivolces.com |The internal domain of the instance. |
|IPAddress |String |100. ** *.* ** .\*\*\* |IP address. |
|NetworkType |String |Private |Network type:<br><br><br>* `Private`: Virtual private cloud.<br><br>* `Public`: Public network access. |
|Port |String |3306 |The port for internal access to the instance. |
|SubnetId |String |subnet\-3tfam28a\*\*\*\* |Subnet ID. The subnet must belong to the selected availability zone. |
|EipId |String |eip\-13g56dc5u2uio3n6nu4kb\*\*\*\* |Public network ID. |


<span id="instancedetailobject"></span>
### InstanceDetailObject


|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |vedbm\-h441603c68aaa\*\*\*\* |Instance ID. |
|InstanceName |String |test |Instance name. |
|InstanceStatus |String |Running |Instance status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a detailed description of the instance state, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Instance_status_description">Instance state description</a>.</div><br> |
|RegionId |String |cn\-beijing |Region ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRegions">DescribeRegions</a> API to query information about regions where instances can be created, including the region ID.</div><br> |
|ZoneIds |String |cn\-beijing\-a |Availability zone ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones">DescribeAvailabilityZones</a> API to query the availability zone resources supported by the instance.</div><br> |
|DBEngineVersion |String |MySQL_8_0 |The compatible version of the instance. Value range:<br><br><br>* `MySQL_8_0`: Compatible with MySQL version 8.0.<br><br>* `MySQL_5_7`: Compatible with MySQL version 5.7. |
|SpecFamily |String |Exclusive |Instance specification type. The valid values are:<br><br><br>* `General`: General type.<br><br>* `Exclusive`: Exclusive type. |
|CreateTime |String |2022\-06\-21T07:54:05Z |Instance creation time, in the format YYYY\-MM\-DDTHH:MM:SSZ (UTC). |
|StorageChargeType |String |PostPaid |Storage billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|PrePaidStorageInGB |Integer |50 |Total capacity of the prepaid storage in GiB. |
|StorageUsedGiB |Double |0.23 |The used storage space in GiB. |
|VpcId |String |vpc\-3cikbvy7jw0e86c6rrt8i\*\*\*\* |Virtual private cloud (VPC) ID. |
|SubnetId |String |subnet\-1g0d851lg1s748ibuxxvg\*\*\*\* |Subnet ID. The subnet must belong to the selected availability zone. |
|TimeZone |String |UTC +08:00 |The time zone of the instance. The default time zone for all regions in China is `UTC + 08:00`. |
|ProjectName |String |vedb_project |The project to which the instance belongs. |
|LowerCaseTableNames |String |1 |Whether table names are case sensitive.<br><br>Value range:<br><br><br>* `0`: table names are stored as is and are case\-sensitive.<br><br>* `1`: table names are stored in lowercase and are case\-insensitive. |
|InstanceStructures |Array of [InstanceStructureObject](https://docs.byteplus.com/en/docs/265/57344#instancestructureobject) |Refer to the Sample response. |Deployment architecture of the instance. |
|DeletionProtection |String |enabled |Whether deletion protection is enabled for the instance. Value range:<br><br><br>* `enabled`: Enable.<br><br>* `disabled`: Disable. |
|MaintenanceWindow |Object of [MaintenanceWindow](https://docs.byteplus.com/en/docs/265/57344#maintenancewindow) |Refer to the Sample response. |The maintenance window for the instance. |
|StorageType |String |IOOptimizedStorage |Storage type. Value range:<br><br><br>* `IOOptimizedStorage`: IO performance type.<br><br>* `SmartCompressedStorage`: Intelligent compression type. |
|CompressedStorageUsedGiB |Double |0.11 |Compressed data space in GiB. |


<span id="instancestructureobject"></span>
### InstanceStructureObject


|Name |Type |Example |Description |
|---|---|---|---|
|SubInstanceType |String |Primary |Instance type. The value is fixed as `Primary` (Primary instance). |
|ZoneIds |String |cn\-beijing\-b |Availability zone ID. |
|Nodes |Array of [NodeObject](https://docs.byteplus.com/en/docs/265/57344#nodeobject) |Refer to the Sample response. |Details of the instance node. |


<span id="maintenancewindow"></span>
### MaintenanceWindow


|Name |Type |Example |Description |
|---|---|---|---|
|DayKind |String |Week |The granularity of the maintenance period. The default value is `Week`. |
|DayOfWeek |Array of String |["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"] |The day of the week for the maintenance window. The default value is every day: `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday`, `Sunday`. |
|DayOfMonth |Array of Integer |[] |Specifies the day of the month for the maintenance window. It is empty by default, which means every day is specified. |
|MaintenanceTime |String |19:00Z\-20:59Z |The maintenance window for the instance. Format: HH:mmZ\-HH:mmZ (UTC time). |


<span id="tagobject"></span>
### TagObject


|Name |Type |Example |Description |
|---|---|---|---|
|Key |String |department |Tag key bound to the instance. |
|Value |String |game |Tag value bound to the instance. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DescribeDBInstanceDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-1ql2ff4u****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2023080110352963A9D3FB2611C013333C",
        "Action": "DescribeDBInstanceDetail",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChargeDetail": {
            "ChargeStatus": "Normal",
            "ChargeType": "PostPaid",
            "OverdueReclaimTime": "",
            "OverdueTime": ""
        },
        "Endpoints": [
            {
                "Addresses": [
                    {
                        "DNSVisibility": false,
                        "Domain": "vedbm-gzwdsf9b****.pri.mysql.vedb.ivolces.com",
                        "EipId": "",
                        "IPAddress": "192.***.***.3",
                        "NetworkType": "Private",
                        "Port": "3306",
                        "SubnetId": "subnet-13fz1bsbrsw743n6nu47c****"
                    }
                ],
                "AutoAddNewNodes": false,
                "ConsistLevel": "Global",
                "ConsistTimeout": 0,
                "ConsistTimeoutAction": "ReadMaster",
                "ConnectionPool": "Off",
                "Description": "主节点终端",
                "DistributedTransaction": false,
                "EndpointId": "vedbm-gzwdsf9b****-Primary",
                "EndpointName": "主节点终端",
                "EndpointType": "Primary",
                "MasterAcceptReadRequests": true,
                "NodeIds": [
                    "vedbm-gzwdsf9b****-1"
                ],
                "ReadWriteMode": "ReadWrite"
            },
            {
                "Addresses": [
                    {
                        "DNSVisibility": false,
                        "Domain": "vedbm-gzwdsf9b****.default.mysql.vedb.ivolces.com",
                        "EipId": "",
                        "IPAddress": "192.***.***.2",
                        "NetworkType": "Private",
                        "Port": "3306",
                        "SubnetId": "subnet-13fz1bsbrsw743n6nu47c****"
                    }
                ],
                "AutoAddNewNodes": true,
                "ConsistLevel": "Session",
                "ConsistTimeout": 20000,
                "ConsistTimeoutAction": "ReadMaster",
                "ConnectionPool": "Off",
                "Description": "默认终端",
                "DistributedTransaction": true,
                "EndpointId": "vedbm-gzwdsf9b****-ReadWriteSplit",
                "EndpointName": "默认终端",
                "EndpointType": "Cluster",
                "MasterAcceptReadRequests": true,
                "NodeIds": [
                    "vedbm-gzwdsf9b****-0",
                    "vedbm-gzwdsf9b****-1"
                ],
                "ReadWriteMode": "ReadWrite"
            }
        ],
        "InstanceDetail": {
            "CompressedStorageUsedGiB": 0,
            "CreateTime": "2023-07-14T03:36:42Z",
            "DBEngineVersion": "MySQL_8_0",
            "DeletionProtection": "disabled",
            "InstanceId": "vedbm-gzwdsf9b****",
            "InstanceName": "yangrui_test1",
            "InstanceStatus": "Running",
            "InstanceStructures": [
                {
                    "Nodes": [
                        {
                            "Memory": 16,
                            "NodeId": "vedbm-gzwdsf9b****-0",
                            "NodeSpec": "vedb.mysql.x4.large",
                            "NodeType": "ReadOnly",
                            "ZoneId": "cn-beijing-b",
                            "vCPU": 4
                        },
                        {
                            "Memory": 16,
                            "NodeId": "vedbm-gzwdsf9b****-1",
                            "NodeSpec": "vedb.mysql.x4.large",
                            "NodeType": "Primary",
                            "ZoneId": "cn-beijing-b",
                            "vCPU": 4
                        }
                    ],
                    "SubInstanceType": "Primary",
                    "ZoneIds": "cn-beijing-b"
                }
            ],
            "LowerCaseTableNames": "1",
            "PrePaidStorageInGB": 50,
            "PrimaryDBAccount": "",
            "ProjectName": "default",
            "RegionId": "cn-beijing",
            "SpecFamily": "General",
            "StorageChargeType": "PostPaid",
            "StorageType": "IOOptimizedStorage",
            "StorageUsedGiB": 0.997,
            "SubnetId": "subnet-13fz1bsbrsw743n6nu47c****",
            "TimeZone": "UTC +08:00",
            "VpcId": "vpc-13fz0iip9nlds3n6nu4fi****",
            "ZoneIds": "cn-beijing-b"
        },
        "Nodes": [
            {
                "Memory": 16,
                "NodeId": "vedbm-gzwdsf9b****-0",
                "NodeSpec": "vedb.mysql.x4.large",
                "NodeType": "ReadOnly",
                "ZoneId": "cn-beijing-b",
                "vCPU": 4
            },
            {
                "Memory": 16,
                "NodeId": "vedbm-gzwdsf9b****-1",
                "NodeSpec": "vedb.mysql.x4.large",
                "NodeType": "Primary",
                "ZoneId": "cn-beijing-b",
                "vCPU": 4
            }
        ],
        "Tags": [
            {
                "Key": "instancetype",
                "Value": "cluster"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
