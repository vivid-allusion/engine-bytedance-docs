---
title: "DescribeDBInstances"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstances"
---

Call the DescribeDBInstances API to query basic information about Redis instances.

## Request type

Synchronous request.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstances&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |No |cn\-beijing |The ID of the region where the instance is located.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, filtering defaults to the region set in the signature. For more information about signature mechanisms, see [Signature mechanism](https://docs.byteplus.com/en/docs/redis/signature-mechanism).<br><br><br>* > You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/redis/describeregions) API to query all region information supported by a Redis instance, including the region IDs.<br> |
|PageNumber |Integer |No |1 |The page number of the instance information list. The value does not exceed the maximum value of the Integer data type; the starting and default values are both 1. |
|PageSize |Integer |No |10 |Number of records per page. The value is an integer from 1 to 1000, with a default of 10. |
|ZoneId |String |No |cn\-beijing\-a |The availability zone ID where the instance resides, supports fuzzy queries.<br><br>> **tip**<br><br><br>> You can call the [DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) API to query the availability zone resources for Redis instances in a specified region, including availability zone IDs.<br> |
|InstanceId |String |No |redis\-cn0212gzmh2xsh2xs |Instance ID, precise query.<br><br>> **tip**<br><br><br>> If this parameter is blank, you cannot filter by the instance ID.<br> |
|InstanceName |String |No |api_test |Instance name. Fuzzy search is supported.<br><br>> **tip**<br><br><br>> If this parameter is blank, you cannot filter by the instance name.<br> |
|ShardedCluster |Integer |No |1 |Whether the instance has sharding cluster enabled. Valid values:<br><br><br>* `0`: Disable.<br><br>* `1`: Enable.<br><br><br>> **tip**<br><br><br>> If this parameter is blank, you cannot filter by whether sharding cluster is enabled for instance.<br> |
|Status |String |No |Running |Instance status. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).<br><br>> **tip**<br><br><br>> If this parameter is blank, you cannot filter by the instance status.<br> |
|EngineVersion |String |No |5.0 |The database version number of the instance. Valid values:<br><br><br>* `5.0`<br><br>* `6.0`<br><br>* `7.0`<br><br><br>> **tip**<br><br><br>> If this parameter is blank, you cannot filter by the database version of an instance.<br> |
|VpcId |String |No |vpc\-rs5811nceqyov0xov0x |The Virtual Private Cloud (VPC) ID that the instance belongs to. Supports fuzzy search.<br><br>> **tip**<br><br><br><br>* > If this parameter is left empty, the instance's Virtual Private Cloud ID will not be used as a filtering condition.<br><br><br>* > Call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the list of all Virtual Private Clouds under the current account, including their Virtual Private Cloud IDs.<br> |
|ChargeType |String |No |PostPaid |The billing type for the instance. Valid values:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Subscription.<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, instance billing type conditions will not be used for filtering.<br><br><br>* > For more information about billing methods, see [Billing method](https://docs.byteplus.com/en/docs/redis/pay-as-you-go).<br> |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/55/12515#tagfilter) |No |Refer to the sample request. |An array of tag key\-value pairs for querying and filtering.<br><br>> **tip**<br><br><br>> If this parameter is left empty, tags will not be used for filtering.<br> |
|ProjectName |String |No |default |The name of the project to which the instance belongs.<br><br>> **tip**<br><br><br>> If this parameter is left blank, the project name of the instance will not be used for filtering.<br> |
|ServiceType |String |No |Basic |Service type of the instance. Valid values are as follows:<br><br><br>* `Basic` (default value): Community Edition.<br><br>* `Enterprise`: Enterprise Edition. |
|DataLayout |String |No |RAM |Instance data storage form.<br><br>> **tip**<br><br><br><br>* > This parameter is only relevant for enterprise edition instances (i.e., where `ServiceType` is `Enterprise`); community edition instances (i.e., where `ServiceType` is `Basic`) do not involve data storage layouts, and `DataLayout` is fixed to `RAM`.<br><br><br>* > If this parameter is left empty, filtering by data storage layout is not used.<br> |

### TagFilter

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |department |The tag key for querying and filtering.<br><br>> **tip**<br><br><br><br>* > When you use tags to filter query results, the tag key (Key) is required, but the tag value (Value) is optional. If you do not specify a tag value, the system searches for all instances associated with the specified tag key.<br><br><br>* > Up to 10 tag key\-value pairs can be passed in at a time for querying and filtering.<br><br><br>* > Duplicate tag keys are allowed.<br> |
|Value |String |No |game |Tag values corresponding to the tag key used for query filtering.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, no restrictions are placed on tag values, and all instances associated with the specified tag key will be filtered.<br><br><br>* > If an empty string is passed, it filters for instances where the tag value is empty under the corresponding tag key.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TotalInstancesNum |Integer |1 |The number of instances that meet the query conditions. |
|Instances |Array of [Instances](https://docs.byteplus.com/en/docs/55/12515#instances) |Refer to the Sample response. |List of basic instance information. |

### Instances

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BlueGreenRole |String |Blue |Role of the instance in blue\-green deployment. Valid values:<br><br><br>* `Blue`: Blue instance.<br><br>* `Green`: Green instance.<br><br><br>> **tip**<br><br><br>> This parameter is returned only for Redis instances that have used the blue/green deployment feature. For more details, refer to [Upgrading major versions using blue\-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment).<br> |
|Capacity |Object of [InstanceCapacity](https://docs.byteplus.com/en/docs/55/12515#instancecapacity) |Refer to the Sample response. |Instance capacity information. |
|ChargeType |String |PrePaid |Billing type. Valid values are:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Subscription.<br><br><br>> **tip**<br><br><br>> For more information about billing methods, see [Billing method](https://docs.byteplus.com/en/docs/redis/pay-as-you-go).<br> |
|CreateTime |String |2024\-04\-30T14:24:32Z |The instance's creation time, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|DataLayout |String |RAM |Data storage form of the instance.<br><br>> **tip**<br><br><br>> This parameter is meaningful only for Enterprise Edition instances, that is, instances whose `ServiceType` is `Enterprise`. Community Edition instances, that is, instances whose `ServiceType` is `Basic`, do not involve data storage forms, and `DataLayout` is fixed to `RAM`.<br> |
|DeletionProtection |String |enabled |The status of instance deletion protection. Valid values:<br><br><br>* `enabled`: Enable.<br><br>* `disabled`: Disable.<br><br><br>> **tip**<br><br><br>> For more details, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection).<br> |
|EngineVersion |String |5.0 |Database version of the instance. |
|ExpiredTime |String |2024\-09\-01 23:59:59 |Instance expiration time, in the format of `yyyy-MM-dd HH:mm:ss` (UTC+8).<br><br>> **tip**<br><br><br>> Only for monthly or yearly subscription instances (that is, when `ChargeType` is `PrePaid`), this parameter will be returned.<br> |
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|InstanceName |String |test |Instance name. |
|InstanceClass |String |PrimarySecondary |Instance type. Valid values:<br><br><br>* `PrimarySecondary`: primary\-secondary instance.<br><br>* `Standalone`: single node instance.<br><br><br>> **tip**<br><br><br>> For more information on instance type, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br> |
|MultiAZ |String |disabled |Availability zone deployment scheme for the instance. Valid values:<br><br><br>* `enabled`: Multi\-availability zone deployment plan.<br><br>* `disabled`: Single availability zone deployment plan.<br><br><br>> **tip**<br><br><br>> For more information on availability zone deployment solutions, refer to [Multi\-availability\-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/feature-introduction).<br> |
|NodeNumber |Integer |2 |Number of nodes per shard. |
|PrivateAddress |String |redis\-cngzxq26qdwpk\*\*\*\*.redis.cn\-guangzhou.ivolces.com |The domain name of the private connection address. |
|ProjectName |String |default |The name of the project to which the instance belongs. |
|RegionId |String |cn\-beijing |The region ID of the instance's region. |
|ShardCapacity |Double |2 |Memory capacity of each shard. Unit: GiB. |
|ShardedCluster |Integer |1 |Indicates whether the current instance has enabled a sharding cluster. Valid values are as follows:<br><br><br>* `0`: Disabled (the instance contains only 1 shard).<br><br>* `1`: Enabled (the instance contains more than 1 shard). |
|ShardNumber |Integer |2 |Number of shards in the instance. |
|ServiceType |String |Basic |Service type of the instance. Valid values:<br><br><br>* `Basic`: Community Edition.<br><br>* `Enterprise`: Enterprise Edition. |
|Status |String |Running |Instance status. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status). |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/55/12515#tag) |Refer to the Sample response. |Information about tags associated with the instance.<br><br>> **tip**<br><br><br>> This parameter is only returned for instances that have tags associated.<br> |
|VIP |String |192.168. ** *.* **  |The IPv4 address corresponding to the instance's private network address. |
|VIPv6 |String |2408:1000:abe5:ff40:a189:2f34:a82e:\*\*\*\* |The IPv6 address corresponding to the instance's private network address.<br><br>> **tip**<br><br><br>> This parameter is returned only when the instance uses an IPv6 address.<br> |
|VpcId |String |vpc\-rs5811nceqyov0x58x4\*\*\*\* |The instance's Virtual Private Cloud ID. |
|ZoneIds |Array of String |["cn\-beijing\-a"] |List of availability zones where the instance resides. |
|PrivatePort |String |6379 |The port number of the instance's private network connection address. |

### InstanceCapacity

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Used |Long |100 |Current instance used capacity. Unit: MiB. |
|Total |Long |36864 |Total memory capacity of the current instance. Unit: MiB. |

### Tag

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Key |String |department |The tag key bound to the current instance. |
|Value |String |game |The tag value of the tags associated with the current instance. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstances&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"RegionId": "cn-beijing",
	"PageNumber": 1,
	"PageSize": 10,
	"ServiceType":"Basic"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202204151542080102120420191760****",
        "Action": "DescribeDBInstances",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Instances": [
            {
                "Capacity": {
                    "Total": 2048,
                    "Used": 57
                },
                "ChargeType": "PostPaid",
                "CreateTime": "2024-04-30T14:24:32Z",                "DeletionProtection": "disabled",
                "EngineVersion": "5.0",
                "ExpiredTime": "",
                "InstanceClass": "PrimarySecondary",
                "InstanceId": "redis-cn0212gzmh2xs****",
                "InstanceName": "test",
                "NodeNumber": 2,
                "ProjectName": "default",
                "MultiAZ": "disabled",
                "RegionId": "cn-beijing",
                "ShardCapacity": 1,
                "ShardNumber": 2,
                "ShardedCluster": 1,
                "Status": "Running",
                "Tags": [
                    {
                        "Key": "owner",
                        "Value": "Alice"
                    },
                    {
                        "Key": "department",
                        "Value": "game"
                    }
                ],
                "VpcId": "vpc-rs5811nceqyov0x58x4****",
                "ZoneIds": [
                    "cn-beijing-a"
                ],
                "DataLayout": "RAM",
                "PrivateAddress": "redis-cn0212gzmh2xs****.redis.ivolces.com",
                "PrivatePort": "6379",
                "VIP": "192.168.***.***",
                "VIPv6": "2408:1000:abe5:ff40:a189:2f34:a82e:****"
            }
        ],
        "TotalInstancesNum": 1
    },
    "BlueGreenRole": "Blue"
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
