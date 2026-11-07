---
title: "DescribeDBInstanceDetail"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DescribeDBInstanceDetail"
---

Call the DescribeDBInstanceDetail interface to query detailed information about a specified instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn019f341d51\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example value |Description |
|---|---|---|---|
|ChargeType |String |PostPaid |Billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|ColdStorage |Long |800 |The total size of the instance's capacity\-based storage, in GiB. |
|CreateTime |String |2022\-11\-07T07:17:55Z |The time when the instance was created (UTC). |
|DBInstanceEndpoint |Array of [DBInstanceEndpointObject](https://docs.byteplus.com/en/docs/219/60844#dbinstanceendpointobject) |Refer to the Sample response. |A list of connection addresses. |
|DeletionProtection |String |enabled |The status of instance deletion protection. Value range:<br><br><br>* `enabled`: Enabled.<br><br>* `disabled`: Disabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about removal protection, see <a href="https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection">Instance deletion protection</a>.</div><br> |
|EngineVersion |String |HBase_2.0 |HBase database version. Only HBase 2.0 is supported. |
|InstanceId |String |hb\-cnglbbb73ea0\*\*\*\* |Instance ID. |
|InstanceName |String |test_api |Instance name. |
|InstanceType |String |Standard |The instance type. Only the `Standard` edition is currently supported. |
|MasterCount |Integer |2 |The number of Master nodes. |
|MasterSpec |String |hbase.x1.4xlarge |The specification code of the master node. |
|ProjectName |String |default |The project to which the instance belongs. |
|RSCount |Integer |2 |The number of RegionServer nodes. |
|RSSpec |String |hbase.x1.4xlarge |The specification code for the RegionServer node. |
|RegionId |String |cn\-beijing |The ID of the region where the instance is located. |
|Status |String |Running |The current state of the instance. For more information about instance states, see [Instance status description](https://docs.byteplus.com/en/docs/HBase/Instance_status_description). |
|StorageType |String |HdfsHdd |The storage type of the instance. Valid values include:<br><br><br>* `HdfsHdd`: HDD file storage.<br><br>* `HdfsSsd`: SSD file storage. |
|StorageCapacity |Integer |500 |The total storage capacity of the instance in GiB. |
|SubnetId |String |subnet\-2d6pl8bcpl2io58ozfd43\*\*\*\* |The subnet ID of the instance. |
|UsedColdStorage |Long |500 |The size of the capacity storage used by the instance, in MiB. |
|UsedStorage |Double |0 |The storage capacity used by the instance, in MiB. |
|VpcId |String |vpc\-rs5811nceqyov0x58x4\*\*\*\* |The ID of the private network to which the instance belongs. |
|VpcName |String |test_vpc |The name of the instance's private network. |
|ZoneId |String |cn\-beijing\-a |The ID of the availability zone to which the instance belongs. |
|ZoneName |String |Availability zone A |The name of the availability zone to which the instance belongs. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/219/60844#tag) |Refer to the Sample response. |An array object of tag keys and tag values bound to the instance. |
|ChargeStatus |String |Normal |Billing status. Value:<br><br><br>* `Normal`: Normal.<br><br>* `Overdue`: Overdue.<br><br>* `Shutdown`: Shut down. |
|AutoRenew |Boolean |false |Specifies whether to enable Due Automatic renewal for prepaid instances. Value:<br><br><br>* `true`: enables auto\-renewal.<br><br>* `false`: no automatic renewal. |
|PrivateDNSVisibility |Boolean |false |Indicates whether public DNS resolution is enabled for the private domain name. |
|EnableSearchIndex |Boolean |false |Indicates whether the multi\-index feature is enabled for the instance. Value:<br><br><br>* `true`: Enabled.<br><br>* `false`: Not enabled. |
|EsInstanceId |String |o\-00g0sqic\*\*\*\* |The ID of the ES instance associated with the enabled search index feature. |
|RelationId |String |ha\-cnglbbaaa1ba\*\*\*\* |The associated ID of the primary/standby instance. |
|DDLDisabled |Boolean |false |DDL disabled status. Value:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|MaintenanceWindow |Object of [MaintenanceWindow](https://docs.byteplus.com/en/docs/219/60844#maintenancewindow) |Refer to the Sample response. |The maintenance window for the instance. |


<span id="dbinstanceendpointobject"></span>
### DBInstanceEndpointObject


|Name |Type |Example value |Description |
|---|---|---|---|
|AddressType |String |Zk |The connection address type. For more information, see [Connection address types](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address#.6L-e5o6l5Zyw5Z2A57G75Z6L). The value range is as follows:<br><br><br>* `Zk`: The ZK address.<br><br>* `Thrift`: The Thrift2 address.<br><br>* `HBaseReUsedEipId`: This parameter is returned when public network access is enabled for the ZK or Thrift2 connection address. It indicates the ID of the EIP that is shared and associated with other components in the instance, such as RS and Master nodes. |
|EndpointId |String |hb\-cngla853d1ba\*\*\*\*\-zk\-Private |The connection address ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, only the ZK private connection address is returned. If you apply for a Thrift2 connection address or enable public network access for a ZK or Thrift2 connection address, a corresponding connection address ID is also generated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the connection address type is <code>HBaseReUsedEipId</code>, the connection address ID is also <code>HBaseReUsedEipId</code>.</div><br> |
|EndpointStr |String |hb\-cnglbbb73ea0\*\*\*\*\-zk.config.ivolces.com:2181 |The connection string for the connection address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, only the ZK private connection address is returned. If you have applied for a Thrift2 connection address or enabled public network access for a ZK or Thrift2 connection address, the corresponding connection strings for those addresses are also returned.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the connection address type is <code>HBaseReUsedEipId</code>, the connection string is also <code>HBaseReUsedEipId</code>.</div><br> |
|NetworkType |String |Private |The network type of the connection address. The valid values are as follows:<br><br><br>* `Public`: Public endpoint.<br><br>* `Private`: Private endpoint. |
|EipId |String |eip\-3qe8rudt1yiv47prml165\*\*\*\* |The EIP ID. This parameter is returned when public network access is enabled for the ZK or Thrift2 connection address. |
|PrivateDNSVisibility |Boolean |false |Indicates whether public DNS resolution is enabled for the private domain name. |


<span id="tag"></span>
### Tag


|Name |Type |Example value |Description |
|---|---|---|---|
|TagKey |String |chargetype |The tag key associated with the instance. |
|TagValue |String |postpaid |The tag key associated with the instance. |


<span id="maintenancewindow"></span>
### MaintenanceWindow


|Name |Type |Example value |Description |
|---|---|---|---|
|Period |Long |4 |The duration of the maintenance window. |
|DayKind |String |Week |The granularity of the maintenance period. The default value is `Week`. |
|StartTime |String |18:00Z |The start time of the maintenance window. |
|DayOfWeeks |Array of String |["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"] |The day of the week for the maintenance window. The default value is every day. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6LIDE="></span>
### Request example

```json
POST /?Action=DescribeDBInstanceDetail&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cn019f341d51****"
}
```


<span id=".6L-U5Zue56S65L6LIDE="></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022110917242101022508219902CF****",
        "Action": "DescribeDBInstanceDetail",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChargeStatus": "Normal",
        "ChargeType": "PostPaid",
        "CreateTime": "2022-11-07T07:17:55Z",
        "DBInstanceEndpoint": [
            {
                "AddressType": "Zk",
                "EndpointId": "hb-cn019f341d51****-zk-Private",
                "EndpointStr": "hb-cn019f341d51****-zk.config.ivolces.com:2181",
                "NetworkType": "Private"
            }
        ],
        "DeletionProtection": "enabled",
        "EngineVersion": "HBase_2.0",
        "InstanceId": "hb-cn019f341d51****",
        "InstanceName": "test_api",
        "InstanceType": "Standard",
        "MaintenanceWindow": {
            "DayKind": "Week",
            "DayOfWeeks": [
                "Sunday",
                "Monday",
                "Tuesday",
                "Wednesday",
                "Thursday",
                "Friday",
                "Saturday"
            ],
            "Period": 4,
            "StartTime": "18:00Z"
        },
        "MasterCount": 2,
        "MasterSpec": "hbase.x1.4xlarge",
        "ProjectName": "",
        "RSCount": 3,
        "RSSpec": "hbase.x1.4xlarge",
        "RegionId": "cn-beijing",
        "RelationId": "ha-cnglbbaaa1ba****",
        "Status": "Running",
        "StorageCapacity": 500,
        "StorageType": "HdfsSsd",
        "SubnetId": "subnet-2d6pl8bcpl2io58ozfd43****",
        "Tags": [
            {
                "Key": "chargetype",
                "Value": "postpaid"
            },
            {
                "Key": "instancetype",
                "Value": "cluster"
            }
        ],
        "UsedStorage": 0,
        "VpcId": "vpc-3redy6326y7ls5zsk2iko****",
        "VpcName": "test_vpc",
        "ZoneId": "cn-beijing",
        "ZoneName": "华北2（北京）-可用区A"
    }
}
```
