---
title: "DescribeDBInstances"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances"
---

Call the DescribeDBInstances interface to query the HBase instance list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeRegions">DescribeRegions</a> API to query resource information in all available regions for the instance, including the Region ID.</div><br> |
|PageNumber |Integer |Yes |1 |The page number of the instance list. The value cannot exceed the maximum value of the Integer data type. The starting value is 1. |
|PageSize |Integer |Yes |10 |Number of records per page. An integer from 1 to 100. |
|InstanceId |String |No |hb\-cn019f341d51\*\*\*\* |Specify the ID of the instance to query. Fuzzy search is supported. |
|InstanceName |String |No |hbase_test |The name of the instance to query. Fuzzy search is supported. |
|InstanceStatus |String |No |Running |Specifies the status of the instance to query. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/219/60843#tag) |No |See the request example. |An array of tag key\-value pairs for querying and filtering.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Up to 10 tag key\-value pairs can be passed in at a time for querying and filtering.</div><br> |
|CreateTimeStart |String |No |2022\-11\-08T12:26:23Z |The start time of the query. The system queries all instances with a creation time on or after the specified start time. Format: *yyyy\-MM\-ddTHH:mmZ*** (UTC time).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If both <code>CreateTimeStart</code> and <code>CreateTimeEnd</code> are specified, the start time must be earlier than the end time.</div><br> |
|CreateTimeEnd |String |No |2022\-11\-08T12:26:30Z |The end time for the query. The system retrieves all instances created on or before this time. Format: *yyyy\-MM\-ddTHH:mmZ*** (UTC time).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If both <code>CreateTimeStart</code> and <code>CreateTimeEnd</code> are specified, the start time must be earlier than the end time.</div><br> |
|ProjectName |String |No |default |The name of the project to which the instance belongs. If this parameter is left empty, instances that meet the filter criteria in all projects are queried. |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|TagKey |String |Yes |chargetype |The tag key associated with the instance. |
|TagValue |String |Yes |postpaid |The tag key associated with the instance. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example value |Description |
|---|---|---|---|
|TotalCount |Integer |1 |Number of instances. |
|Instances |Array of [InstanceObject](https://docs.byteplus.com/en/docs/219/60843#instanceobject) |Refer to the Sample response. |Instance basic information. |


<span id="instanceobject"></span>
### InstanceObject


|Name |Type |Example value |Description |
|---|---|---|---|
|ChargeType |String |PostPaid |Billing type. The valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|CreateTime |String |2022\-05\-25T04:19:39Z |The time when the instance was created (UTC). |
|ExpireTime |String |2022\-05\-25T04:19:39Z |The expiration time of the yearly/monthly subscription instance (UTC). |
|DBInstanceEndpoint |Array of [DBInstanceEndpointObject](https://docs.byteplus.com/en/docs/219/60843#dbinstanceendpointobject) |Refer to the Sample response. |A list of connection addresses. |
|DeletionProtection |String |enabled |The status of instance deletion protection. For more information about removal protection, see [Instance deletion protection](https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection). The valid values are as follows:<br><br><br>* `enabled`: The feature is enabled.<br><br>* `disabled`: The feature is disabled. |
|EngineVersion |String |HBase_2.0 |HBase database version. Only HBase 2.0 is supported. |
|InstanceId |String |hb\-bbf19cb0\*\*\*\* |Instance ID. |
|InstanceName |String |testInstance |Instance name. |
|InstanceType |String |Standard |The instance type. Only the `Standard` edition is currently supported. |
|ProjectName |String |default |The project to which the instance belongs. |
|RSCount |Integer |2 |The number of RegionServer nodes. |
|RegionId |String |cn\-beijing |The ID of the region where the instance is located. |
|Status |String |Running |The current state of the instance. For more information about instance states, see [Instance status description](https://docs.byteplus.com/en/docs/HBase/Instance_status_description). |
|StorageType |String |HdfsHdd |The storage type of the instance. Valid values include:<br><br><br>* `HdfsHdd`: HDD file storage.<br><br>* `HdfsSsd`: SSD file storage. |
|StorageCapacity |Integer |500 |The total storage capacity of the instance in GiB. |
|UsedStorage |Double |50 |The storage capacity used by the instance, in MiB. |
|VpcId |String |vpc\-rs5811nceqyov0x58x4\*\*\*\* |The private network ID of the instance. |
|SubnetId |String |subnet\-2d6pl8bcpl2io58ozfd43\*\*\*\* |The subnet ID of the instance. |
|VpcName |String |test_vpc |The name of the instance's private network. |
|ZoneId |String |cn\-beijing\-a |The ID of the availability zone to which the instance belongs. |
|ZoneName |String |Availability zone A |The name of the availability zone to which the instance belongs. |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/219/60843#tag-response) |Refer to the Sample response. |An array object of tag keys and tag values bound to the instance. |
|RelationId |String |ha\-cnglbbaaa1ba\*\*\*\* |The associated ID of the primary/standby instance. |


<span id="dbinstanceendpointobject"></span>
### DBInstanceEndpointObject


|Name |Type |Example value |Description |
|---|---|---|---|
|AddressType |String |Zk |The connection address type. For more information, see [Viewing connection address](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address). The value range is as follows:<br><br><br>* `Zk`: The ZK address.<br><br>* `Thrift`: The Thrift2 address.<br><br>* `HBaseReUsedEipId`: This parameter is returned when public network access is enabled for the ZK or Thrift2 connection address. It indicates the ID of the EIP that is shared and associated with other components in the instance, such as RS and Master nodes. |
|EndpointId |String |hb\-cngla853d1ba\*\*\*\*\-zk\-Private |The connection address ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, only the ZK private connection address is returned. If you apply for a Thrift2 connection address or enable public network access for a ZK or Thrift2 connection address, a corresponding connection address ID is also generated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the connection address type is <code>HBaseReUsedEipId</code>, the connection address ID is also <code>HBaseReUsedEipId</code>.</div><br> |
|EndpointStr |String |hb\-cnglbbb73ea0\*\*\*\*\-zk.config.ivolces.com:2181 |The connection string for the connection address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, only the ZK private connection address is returned. If you have applied for a Thrift2 connection address or enabled public network access for a ZK or Thrift2 connection address, the corresponding connection strings for those addresses are also returned.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the connection address type is <code>HBaseReUsedEipId</code>, the connection string is also <code>HBaseReUsedEipId</code>.</div><br> |
|NetworkType |String |Private |The network type of the connection address. The valid values are as follows:<br><br><br>* `Public`: Public access address.<br><br>* `Private`: Private access address. |
|EipId |String |eip\-3qe8rudt1yiv47prml165\*\*\*\* |The EIP ID. This parameter is returned when public network access is enabled for the ZK or Thrift2 connection address. |


<span id="tag-response"></span>
### Tag


|Name |Type |Example value |Description |
|---|---|---|---|
|TagKey |String |chargetype |The tag key associated with the instance. |
|TagValue |String |postpaid |The tag key associated with the instance. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6LIDE="></span>
### Request example

```json
POST /?Action=DescribeDBInstances&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "PageSize": 10,
    "PageNumber": 1,
    "RegionId": "cn-beijing",
    "Tags": [
        {
            "Key": "chargetype",
            "Value": "postpaid"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6LIDE="></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230828142506841D7D5EA6A6F344****",
        "Action": "DescribeDBInstances",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "Instances": [
            {
                "ChargeType": "PostPaid",
                "CreateTime": "2023-08-25T08:19:50Z",
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
                "InstanceName": "api_test",
                "InstanceType": "Standard",
                "ProjectName": "",
                "RSCount": 2,
                "RegionId": "cn-beijing",
                "RelationId": "ha-cnglbbaaa1ba****",
                "Status": "Running",
                "StorageCapacity": 500,
                "StorageType": "HdfsHdd",
                "UsedStorage": 0,
                "SubnetId": "subnet-1g15j13jtzgu88ibuxwqp****",
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
                "VpcId": "vpc-2bznmyi2p7ojk2dx0eedi****",
                "VpcName": "test_vpc",
                "ZoneId": "cn-beijing-a",
                "ZoneName": "可用区A"
            }
        ],
        "TotalCount": 1
    }
}
```
