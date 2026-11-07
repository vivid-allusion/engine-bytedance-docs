---
title: "DescribeDBInstanceDetail"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail"
---

## Request type

Synchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |

## Response parameters

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BasicInfo |Object of [BasicInfoObject](https://docs.byteplus.com/en/docs/61/15767#basicinfoobject) |Refer to the sample response. |Basic information of the instance. |
|Endpoints |Array of [EndpointObject](https://docs.byteplus.com/en/docs/61/15767#endpointobject) |Refer to the sample response. |Instance connection information. |
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/61/15767#chargedetailobject) |Refer to the sample response. |Instance billing information. |
|Nodes |Array of [NodeObject](https://docs.byteplus.com/en/docs/61/15767#nodeobject) |Refer to the sample response. |Instance node information. |

### BasicInfoObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CreateTime |String |2022\-01\-01T10:10:10.000Z |Instance creation time. Format is `yyyy-MM-ddTHH:mm:ss.sss`Z (UTC time). |
|DBEngineVersion |String |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18。 |
|DataSyncMode |String |Async |Synchronization mode. Value is `Async`, meaning asynchronous synchronization. |
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|InstanceName |String |Test123 |Storage type. |
|InstanceStatus |String |Running |Instance state, values:<br><br><br>* `Running`: running.<br><br>* `Creating`: creating.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: Restarting.<br><br>* `Restoring`: recovering.<br><br>* `Updating`: modifying.<br><br>* `Upgrading`: upgrading.<br><br>* `Error`: error.<br><br>* `Released`: released.<br><br>* `CreateError`: create error.<br><br>* `MasterChanging`: primary node switching.<br><br>* `Deleted`: Deleted.<br><br>* `Recycled`: recycled. |
|InstanceTag |Array of [TagObject](https://docs.byteplus.com/en/docs/61/15767#tagobject) |[{<br><br>"Key": "test",<br><br>"Value": "123"<br><br>}] |Array of tag objects.<br><br>> **tip**<br><br><br>> If the instance is not bound with tags, this field is not returned.<br> |
|InstanceType |String |HA |Instance type. Value: `HA` (High\-availability Edition). |
|MaintenanceWindow |Object of [MaintenanceWindowObject](https://docs.byteplus.com/en/docs/61/15767#maintenancewindowobject) |Refer to the sample response. |The maintenance window for the instance. |
|Memory |Integer |50 |Memory size. Unit: GB. |
|NodeNumber |String |2 |Number of nodes. |
|NodeSpec |String |rds.postgres.1c2g |Primary node specifications. |
|ProjectName |String |Test |Affiliated project of the instance. |
|RegionId |String |cn\-beijing |Region ID. |
|StorageDataUse |Long |25666194 |The used data file space of the instance primary node. Unit: Byte. |
|StorageLogUse |Long |1095433115 |The log file space used by the primary node of the instance. Unit: Byte. |
|StorageSpace |Integer |200 |The storage space for the instance. Unit: GB. |
|StorageTempUse |Long |4096 |Temporary file space used by the instance primary node. Unit: Byte. |
|StorageUse |Long |142635726 |Instance storage space used. Unit: Byte. |
|StorageType |String |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |
|StorageWALUse |Long |1241523717 |The WAL file space used by the primary node of the instance. Unit: Byte. |
|SubnetId |String |subnet\-30uhx4w39n75s7r2qr0lq\*\*\*\* |Subnet ID. |
|UpdateTime |String |2022\-01\-01T10:10:10.000Z |Instance update time. Format is yyyy\-MM\-ddTHH:mm:ss.sssZ (UTC time). |
|VCPU |Integer |2 |CPU size. For example: 1 indicates 1U. |
|VpcID |String |vpc\-2gdgzrrl5icjk50ztyz6b\*\*\*\* |Virtual private cloud (VPC) ID. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|KMSTrn |String |trn:kms:cn\-beijing:210xxxx:keyrings/testxxxx/keys/testxxxx |KMS key ring TRN. Format: `trn:kms:<region>:<account_id>:keyrings/<ring_name>/keys/<key_name>`. |
|TDEEnable |Boolean |true |Whether the instance has TDE encryption enabled. Values:<br><br><br>* true: TDE encryption is enabled.<br><br>* false: TDE encryption is disabled.<br><br><br>> **tip**<br><br><br>> TDE encryption cannot be disabled once enabled.<br> |

### TagObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Key |String |abc |Tag key. Naming rules are as follows:<br><br><br>* It cannot start with any case\-insensitive variation of the prefix `volc:`. `volc:` is a system\-reserved tag key and is forbidden to use.<br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* The length must be between 1 and 128 characters.<br><br><br>> **tip**<br><br><br><br>* > The number of tags created at one time cannot exceed 20.<br><br><br>* > Tag keys cannot be duplicated under a single instance.<br> |
|Value |String |3 |Tag value. The naming rules are as follows:<br><br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* Nullable. Length must be between 0 and 256 characters. |

### MaintenanceWindowObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DayKind |String |Week |The granularity of the maintenance cycle, with values of `Week`. |
|DayOfWeekMaintenanceTime |Array of [DayOfWeekObject](https://docs.byteplus.com/en/docs/61/15767#dayofweekobject) |Refer to the sample. |Details of the instance maintenance window. |

### DayOfWeekObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|DayOfWeek |String |Monday,Tuesday |Specify the maintainable day for the instance each week. Multiple selections allowed.<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday.<br><br><br>> **tip**<br><br><br>> If this value is not specified or empty, it defaults to all seven days of the week.<br> |
|MaintenanceWindowStartTime |String |22:00Z |The instance's start time within the maintenance window on the maintainable day. Format: HH:mmZ (UTC time).<br><br>> **tip**<br><br><br>> Currently, only start times between 16:00Z and 20:00Z are supported for the maintenance window.<br> |
|Period |Integer |6 |Duration of the instance's maintenance window on a maintainable day.<br><br>> **tip**<br><br><br>> The duration is at least 2 hours and at most 6 hours.<br> |

### EndpointObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Address |Array of [AddressObject](https://docs.byteplus.com/en/docs/61/15767#addressobject) |Refer to the sample response. |Address list. |
|AutoAddNewNodes |String |Enable |When the endpoint type is read/write or read\-only, setting whether the new node joins automatically is supported. Values:<br><br><br>* `Enable`: automatically join.<br><br>* `Disable`: do not automatically join (default). |
|Description |String |Primary address |Address description. |
|EnableReadOnly |String |Enable |Whether global read\-only is enabled.<br><br><br>* `Enable`: Enabled.<br><br>* `Disable`: disabled. |
|EnableReadWriteSplitting |String |Enable |Whether read/write separation is enabled, value:<br><br><br>* `Enable`: enabled.<br><br>* `Disable`: disabled. |
|EndpointId |String |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|EndpointName |String |Primary connection endpoint |Instance endpoint name. |
|EndpointType |String |Cluster |Endpoint type:<br><br><br>* `Cluster`: default endpoint (created by default).<br><br>* `Custom`: customized_endpoint. |
|ReadOnlyNodeDistributionType |String |Default |Read\-only weight allocation mode. Values:<br><br><br>* `Default`: standard weight allocation (default value).<br><br>* `custom`: customized weight allocation. |
|ReadOnlyNodeMaxDelayTime |Integer |30 |Maximum latency threshold for read\-only nodes. When the latency of a read\-only node exceeds this value, read traffic will not be routed to that node. Unit is in seconds. Value range: 0\-3,600. Default value: 30.<br><br>> **tip**<br><br><br>> It supports setting this parameter for the default endpoint enabled with read/write separation.<br> |
|ReadOnlyNodeWeight |Array of [NodeWeightObject](https://docs.byteplus.com/en/docs/61/15767#nodeweightobject) |[<br><br>{<br><br>"NodeType" : "Primary",<br><br>"Weight" : 100<br><br>},<br><br>{<br><br>"NodeId" : "postgres\-ca7b7019\*\*\*\*\-2",<br><br>"Weight" : 100<br><br>},<br><br>{<br><br>"NodeId" : "postgres\-ca7b7019\*\*\*\*\-3",<br><br>"Weight" : 200<br><br>}<br><br>] |Node list configured for the connection endpoint and corresponding read\-only weights. |
|ReadWriteMode |String |ReadOnly |Read/Write mode:<br><br><br>* `ReadWrite`: Read/write.<br><br>* `ReadOnly`: read\-only. |
|ReadWriteProxyConnection |Integer |200 |Set the number of proxy connections for the endpoint after enabling read\-write separation.<br><br><br>* The minimum value of proxy connections is 20.<br><br>* The maximum number of proxy connections depends on the specification of the instance primary node. Different specifications support different maximum numbers of proxy connections. For details, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications). |
|WriteNodeHaltWriting |Boolean |false |Whether the terminal sends write requests to the write node (currently, only the primary node is the write node). Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no. |

### AddressObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CrossRegionDomain |String |postgresca7b7019\*\*\*\*.rds\-pg.cn\-beijing.ivolces.com |Private network address accessible across regions.<br><br>> **tip**<br><br><br>> This field is not returned if the address is unavailable.<br> |
|DNSVisibility |Boolean |false |Enable or disable public network resolution. Values are:<br><br><br>* false: Default value, BytePlus private network resolution.<br><br>* true: BytePlus private and public network resolution. |
|Domain |String |postgresca7b7019\*\*\*\*.rds\-pg.ivolces.com |Connection domain name. |
|DomainVisibilitySetting |String |CrossRegionDomain |Private network address type. Values:<br><br><br>* `LocalDomain`: local domain name.<br><br>* `CrossRegionDomain`: domain name accessible across regions. |
|EipId |String |eip\-3jhjud2zgy1og3pncmeh7\*\*\*\* |ID of EIP, valid only for public address. |
|IPAddress |String |192. ** *.* **  .253 |IP address. |
|NetworkType |String |Private |Network address type, values are:<br><br><br>* `Private`: private network connection address.<br><br>* `Public`: public network connection address.<br><br>* `Inner`: public service area address. |
|Port |String |5432 |Port. |
|SubnetId |String |subnet\-30uhx4w39n75s7r2qr0lq\*\*\*\* |Subnet ID. |

### NodeWeightObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NodeId |String |postgres\-c23003b1\*\*\*\*\-ojmo |Read\-only node requires passing in NodeId.<br><br>> **tip**<br><br><br>> No NodeId is needed for the primary node.<br> |
|NodeType |String |Primary |Node type. Values:<br><br><br>* `Primary`: primary node.<br><br>* `ReadOnly`: Read\-only node. |
|Weight |Integer |100 |The read weight of the node, increasing by 100, with a maximum value of 40,000.<br><br>> **tip**<br><br><br>> Weights cannot all be set to 0.<br> |

### ChargeDetailObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ChargeType |String |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go.<br><br>* `PrePaid`: subscription (default). |
|AutoRenew |Boolean |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `yes`: automatic renewal.<br><br>* `false`: no automatic renewal (default). |
|Number |Integer |1 |Number of instances. |
|PeriodUnit |String |Month |purchase period for prepaid scenarios.<br><br><br>* `Month`: monthly (default).<br><br>* `Year`: subscription. |
|Period |Integer |1 |Subscription duration in a prepaid scenario. default value: 1. |
|ChargeStatus |String |Normal |Payment status. Values:<br><br><br>* `Normal`: normal.<br><br>* `Overdue`: overdue.<br><br>* `Overdue`: waiting for payment. |
|ChargeStartTime |String |2023\-01\-10T11:13:30.000Z |Instance billing start time. |
|ChargeEndTime |String |2023\-01\-10T11:13:34.000Z |Subscription instance expiration time. |
|OverdueTime |String |2023\-01\-10T11:13:30.000Z |Overdue shutdown time of the instance. |
|OverdueReclaimTime |String |2023\-01\-15T16:00:00.000Z |Estimated release time after instance overdue shut down. |
|TempModifyStartTime |String |2023\-12\-01T10:10:10.000Z |Start time of temporary upgrade.<br><br>> **tip**<br><br><br><br>* > Return when the instance is under temporary upgrade.<br><br><br>* > If multiple consecutive temporary upgrades are performed on the instance, this returns the start time of the first temporary upgrade.<br> |
|TempModifyEndTime |String |2023\-12\-07T10:10:09.000Z |Restoration time of temporary upgrade.<br><br>> **tip**<br><br><br>> Return when the instance is under temporary upgrade.<br> |

### NodeObject

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|NodeId |String |postgres\-ca7b7019\*\*\*\*\-zgqy |Node ID. |
|RegionId |String |cn\-beijing |Region ID. You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_PG/describeregions) API to query the list of available regions. Use this parameter to specify the region where you want to create the instance. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|NodeType |String |Primary |Node type, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: indicates the secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|NodeStatus |String |Running |Node status. |
|NodeSpec |String |rds.postgres.1c2g |Node specification. |
|VCPU |Integer |4 |CPU size. For example: 1 means 1U. |
|Memory |Integer |16 |Memory size. Unit is GB. |
|CreateTime |String |2022\-01\-01T10:10:10Z |Node creation time. Format is yyyy\-MM\-ddTHH:mm:ss.sssZ (UTC time). |
|UpdateTime |String |2022\-01\-01T10:10:10Z |Node update time. Format is yyyy\-MM\-ddTHH:mm:ss.sssZ (UTC time). |

## Example

### Sample request

```json
POST /?Action=DescribeDBInstanceDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-d9ace5c3****"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20251014125209A66A6FBBB5A875A80B81-69f90e",
        "Action": "DescribeDBInstanceDetail",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BasicInfo": {
            "AllowListVersion": "v1",
            "CreateTime": "2023-04-06T01:26:57.000Z",
            "DBEngineVersion": "PostgreSQL_11",
            "DataSyncMode": "Async",
            "DeployType": "v5",
            "InstanceId": "postgres-d9ace5c3****",
            "InstanceName": "测试实例",
            "InstanceStatus": "Running",
            "InstanceTag": [
                {
                    "Key": "city",
                    "Value": "chengdu"
                },
                {
                    "Key": "owner",
                    "Value": "hechunxiong"
                },
                {
                    "Key": "TAG",
                    "Value": "测试分账功能"
                }
            ],
            "InstanceType": "HA",
            "InternetProtocol": "IPv4",
            "TDEEnable": true,
            "KMSTrn": "trn:kms:cn-beijing:210xxxx:keyrings/testxxxx/keys/testxxxx",
            "MaintenanceWindow": {
                "DayKind": "Week",
                "DayOfWeekMaintenanceTime": [
                    {
                        "DayOfWeek": "Sunday",
                        "MaintenanceWindowStartTime": "16:00Z",
                        "Period": 6
                    },
                    {
                        "DayOfWeek": "Monday",
                        "MaintenanceWindowStartTime": "16:00Z",
                        "Period": 6
                    }
                ]
            },
            "Memory": 2,
            "NodeNumber": "3",
            "NodeSpec": "rds.postgres.1c2g",
            "ProjectName": "default",
            "RegionId": "cn-beijing",
            "StorageDataUse": 14286027315,
            "StorageLogUse": 1859700470,
            "StorageSpace": 100,
            "StorageTempUse": 0,
            "StorageType": "LocalSSD",
            "StorageUse": 18561685963,
            "StorageWALUse": 2415958178,
            "SubnetId": "subnet-rrnkvy55npc0v0x57x8****",
            "UpdateTime": "2025-10-14T03:47:48.000Z",
            "VCPU": 1,
            "VpcID": "vpc-miswzgsgy77k5smt1ar9****",
            "ZoneId": "cn-beijing-a"
        },
        "ChargeDetail": {
            "AutoRenew": true,
            "ChargeEndTime": "2025-11-17T15:59:59.000Z",
            "ChargeStartTime": "2023-04-06T01:26:57.000Z",
            "ChargeStatus": "Overdue",
            "ChargeType": "PrePaid",
            "Number": 1,
            "OverdueReclaimTime": "2025-11-24T15:59:59.000Z",
            "OverdueTime": "2025-11-18T04:00:00.000Z",
            "Period": 1,
            "PeriodUnit": "Month"
        },
        "Endpoints": [
            {
                "Address": [
                    {
                        "DNSVisibility": false,
                        "Domain": "postgres-d9ace5c3****-public.rds-pg.cn-beijing.volces.com",
                        "EipId": "eip-1a1k0eh4m8mio8nvepkxv****",
                        "IPAddress": "101.126.28.254",
                        "IPv6Address": "",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Public",
                        "Port": "5432",
                        "SubnetId": "subnet-rrnkvy55npc0v0x57x8****"
                    },
                    {
                        "CrossRegionDomain": "postgres-d9ace5c3****-private.rds-pg.cn-beijing.ivolces.com",
                        "DNSVisibility": false,
                        "Domain": "postgresd9ace5c3****.rds-pg.ivolces.com",
                        "DomainVisibilitySetting": "LocalDomain",
                        "EipId": "",
                        "IPAddress": "192.***.***.0",
                        "IPv6Address": "",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Private",
                        "Port": "5432",
                        "SubnetId": "subnet-rrnkvy55npc0v0x57x8****"
                    }
                ],
                "AutoAddNewNodes": "Enable",
                "Description": "",
                "EnableReadOnly": "Disable",
                "EnableReadWriteSplitting": "Disable",
                "EndpointId": "postgres-d9ace5c3****",
                "EndpointName": "",
                "EndpointType": "Cluster",
                "ReadOnlyNodeDistributionType": "Default",
                "ReadOnlyNodeMaxDelayTime": 30,
                "ReadOnlyNodeWeight": [
                    {
                        "NodeId": "postgres-ro-41d8643f****",
                        "NodeType": "ReadOnly",
                        "Weight": 0
                    },
                    {
                        "NodeType": "Primary",
                        "Weight": 300
                    }
                ],
                "ReadWriteMode": "ReadWrite",
                "ReadWriteProxyConnection": 200,
                "WriteNodeHaltWriting": false
            },
            {
                "Address": [
                    {
                        "DNSVisibility": false,
                        "Domain": "postgres-ro-41d8643f****-public.rds-pg.cn-beijing.volces.com",
                        "EipId": "eip-3pt0ad8yolqm86csxyv4o****",
                        "IPAddress": "180.184.36.160",
                        "IPv6Address": "",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Public",
                        "Port": "5432",
                        "SubnetId": "subnet-rrnkvy55npc0v0x57x8****"
                    },
                    {
                        "DNSVisibility": false,
                        "Domain": "postgresro41d8643f****.rds-pg.ivolces.com",
                        "DomainVisibilitySetting": "LocalDomain",
                        "EipId": "",
                        "IPAddress": "192.***.***.255",
                        "IPv6Address": "",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Private",
                        "Port": "5432",
                        "SubnetId": "subnet-rrnkvy55npc0v0x57x8****"
                    }
                ],
                "AutoAddNewNodes": "Enable",
                "Description": "",
                "EnableReadOnly": "Disable",
                "EnableReadWriteSplitting": "Disable",
                "EndpointId": "postgres-ro-41d8643f****",
                "EndpointName": "",
                "EndpointType": "Custom",
                "ReadOnlyNodeDistributionType": "Default",
                "ReadOnlyNodeWeight": [
                    {
                        "NodeId": "postgres-ro-41d8643f****",
                        "NodeType": "ReadOnly",
                        "Weight": 300
                    }
                ],
                "ReadWriteMode": "ReadOnly",
                "ReadWriteProxyConnection": 200,
                "WriteNodeHaltWriting": false
            },
            {
                "Address": [
                    {
                        "CrossRegionDomain": "postgres-d9ace5c3****-custom-911a-private.rds-pg.cn-beijing.ivolces.com",
                        "DNSVisibility": false,
                        "Domain": "postgres-d9ace5c3****-custom-911a-private.rds-pg.ivolces.com",
                        "DomainVisibilitySetting": "LocalDomain",
                        "EipId": "",
                        "IPAddress": "192.***.***.4",
                        "IPv6Address": "",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Private",
                        "Port": "5432",
                        "SubnetId": "subnet-rrnkvy55npc0v0x57x8****"
                    }
                ],
                "AutoAddNewNodes": "Disable",
                "Description": "",
                "EnableReadOnly": "Disable",
                "EnableReadWriteSplitting": "Disable",
                "EndpointId": "postgres-d9ace5c3****-custom-911a",
                "EndpointName": "自定义终端",
                "EndpointType": "Custom",
                "ReadOnlyNodeDistributionType": "Default",
                "ReadOnlyNodeMaxDelayTime": 30,
                "ReadOnlyNodeWeight": [
                    {
                        "NodeType": "Primary",
                        "Weight": 300
                    }
                ],
                "ReadWriteMode": "ReadWrite",
                "ReadWriteProxyConnection": 200,
                "WriteNodeHaltWriting": false
            }
        ],
        "NodeInfo": [
            {
                "CreateTime": "2023-04-06T01:26:57.000Z",
                "InstanceId": "postgres-d9ace5c3****",
                "Memory": 2,
                "NodeId": "postgres-d9ace5c3****",
                "NodeSpec": "rds.postgres.1c2g",
                "NodeStatus": "Running",
                "NodeType": "Primary",
                "RegionId": "cn-beijing",
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            },
            {
                "CreateTime": "2023-04-06T01:26:57.000Z",
                "InstanceId": "postgres-d9ace5c3****",
                "Memory": 2,
                "NodeId": "postgres-d9ace5c3****-rlwb",
                "NodeSpec": "rds.postgres.1c2g",
                "NodeStatus": "Running",
                "NodeType": "Secondary",
                "RegionId": "cn-beijing",
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            },
            {
                "CreateTime": "2025-08-13T15:06:02.000Z",
                "InstanceId": "postgres-d9ace5c3****",
                "Memory": 2,
                "NodeId": "postgres-ro-41d8643f****",
                "NodeSpec": "rds.postgres.1c2g",
                "NodeStatus": "Running",
                "NodeType": "ReadOnly",
                "RegionId": "cn-beijing",
                "UpdateTime": "2025-08-13T15:27:06.000Z",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            }
        ],
        "Nodes": [
            {
                "CreateTime": "2023-04-06T01:26:57.000Z",
                "InstanceId": "postgres-d9ace5c3****",
                "Memory": 2,
                "NodeId": "postgres-d9ace5c3****",
                "NodeSpec": "rds.postgres.1c2g",
                "NodeStatus": "Running",
                "NodeType": "Primary",
                "RegionId": "cn-beijing",
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            },
            {
                "CreateTime": "2023-04-06T01:26:57.000Z",
                "InstanceId": "postgres-d9ace5c3****",
                "Memory": 2,
                "NodeId": "postgres-d9ace5c3****-rlwb",
                "NodeSpec": "rds.postgres.1c2g",
                "NodeStatus": "Running",
                "NodeType": "Secondary",
                "RegionId": "cn-beijing",
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            },
            {
                "CreateTime": "2025-08-13T15:06:02.000Z",
                "InstanceId": "postgres-d9ace5c3****",
                "Memory": 2,
                "NodeId": "postgres-ro-41d8643f****",
                "NodeSpec": "rds.postgres.1c2g",
                "NodeStatus": "Running",
                "NodeType": "ReadOnly",
                "RegionId": "cn-beijing",
                "UpdateTime": "2025-08-13T15:27:06.000Z",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            }
        ]
    }
}
```
