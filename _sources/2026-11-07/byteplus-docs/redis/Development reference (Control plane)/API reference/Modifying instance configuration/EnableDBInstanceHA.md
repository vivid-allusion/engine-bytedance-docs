---
title: "EnableDBInstanceHA"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/enabledbinstanceha"
---

Call the EnableDBInstanceHA API to switch Redis single node instance to primary\-secondary instance.

## Request type

Asynchronous request.

## Precautions

* After a single\-node instance is switched to a primary\-secondary instance, the instance type changes, and supported features vary. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* During the process of switching to a primary\-secondary instance, if you also reduce the number of shards or downgrade node specifications, ensure that the current **Used memory** of the instance does not exceed the total new memory capacity, where total new memory capacity = modified single shard memory \* shard number. For how to view **used memory** information, see [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

   > Description

> You can view and confirm the **Used memory** metric data of each shard on the **Server** sub\-tab under the **Monitoring** tab. For more information about how to view monitoring data, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/redis/view-instance).

* If the single\-node instance before the change is an instance with sharding cluster enabled and a direct connection address has been applied for, then when switching to a primary\-secondary instance:

   * You cannot select to disable sharding cluster.

   * The instance's number of shards cannot exceed 8. If you need to increase the number of shards while direct connection is enabled, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* During the change process, the instance might prompt the error `-TRYAGAIN The specific keys are being migrated.\r\n`, or experience one or two temporary disconnections, each less than 30 seconds. Proceed with caution. It is recommended to perform configuration changes during off\-peak hours and ensure that the client is configured with a proper retry mechanism.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableDBInstanceHA&serviceCode=Redis&version=2020-12-07&groupName=变更实例配置)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ApplyImmediately |Boolean |Yes |true |Whether to execute the configuration modification immediately. Valid values:<br><br><br>* `true`: Execute now.<br><br>* `false`: Execute modification within the maintenance period.<br><br><br>> **tip**<br><br><br>> For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|NodeNumber |Integer |Yes |3 |Number of nodes per shard. Value range: 2 to 6.<br><br>> **tip**<br><br><br>> For nodes with a memory capacity of 256 MiB, you can create up to four nodes per account in each region by default (that is, the value of `ShardCapacity` is `256`). To adjust the purchase quota of 256 MiB nodes (maximum is 10), refer to [Account quota](https://vsop-online.bytedance.net/doc/manage/detail/6293/6293/71560#%E8%B4%A6%E5%8F%B7%E9%85%8D%E9%A2%9D).<br> |
|ShardedCluster |Integer |Yes |1 |Whether to enable sharding cluster. Valid values:<br><br><br>* `0`: Disable.<br><br>* `1`: Enable.<br><br><br>> **tip**<br><br><br>> If the single\-node instance before the change is an instance with sharding cluster enabled and a direct connection address has been applied for, then when switching to a primary\-secondary instance, it is not allowed to disable sharding cluster.<br> |
|ShardNumber |Integer |No |3 |Number of shards in the instance. Value range: 2 to 256.<br><br>> **tip**<br><br><br><br>* > This parameter must be specified only when sharding cluster is enabled (that is, `ShardedCluster` is set to `1`).<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the details of a specified instance, including whether sharding cluster is enabled and the number of shards.<br><br><br>* > To reduce the number of shards, ensure that the current **Used memory** of the instance does not exceed the total new memory capacity, where total new memory capacity = modified single shard memory x shard number. For how to view **used memory** information, see [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).<br><br><br>* > If the single\-node instance before the change is an instance with sharding cluster enabled and a direct connection address has been applied for, then when switching to a primary\-secondary instance, the number of shards for the instance cannot exceed 8. If you need to increase the number of shards while direct connection is enabled, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br> |
|ShardCapacity |Integer |No |1024 |Memory capacity of each shard, unit: MiB. Valid values:<br><br><br>* When sharding cluster is disabled (`ShardedCluster` value is `0`): 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 24576, 65536.<br><br>* When sharding cluster is enabled (`ShardedCluster` value is `1`): 1024, 2048, 4096, 8192, 16384.<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the instance's memory capacity will not be modified.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of the specified instance, including whether sharding is enabled and the memory capacity in each shard.<br><br><br>* > To reduce the shard capacity, ensure that the current **Used memory** of the instance does not exceed the total new memory capacity, where total new memory capacity = modified single shard memory x shard number. For how to view **used memory** information, see [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).<br><br><br>* > Each instance specification has its corresponding supported shard capacity and bandwidth. When modifying the instance shard capacity, the instance bandwidth and type are modified as well. For more information on Redis instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br> |
|MultiAZ |String |No |enabled |Set the availability zone deployment plan for the instance. Valid values:<br><br><br>* `disabled`: Single availability zone deployment plan.<br><br>* `enabled`: Multi\-availability zone deployment plan.<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the instance's availability zone deployment plan will not be modified.<br><br><br>* > For more details, refer to [Multi\-availability\-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution).<br> |
|ConfigureNodes |Array of [ConfigureNode](https://docs.byteplus.com/en/docs/55/90980#configurenode) |No |Refer to the Sample response. |Set the availability zone to which the new nodes belong.<br><br>> **tip**<br><br><br>> If this parameter is left blank, the availability zone of the instance node will not be modified.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### ConfigureNode

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AZ |String |Yes |cn\-beijing\-a |Set the availability zone to which the new nodes belong.<br><br>**The number of availability zones passed in must be equal to the number of nodes in a single shard** (that is, the value of the `NodeNumber` parameter), and the value of `AZ` needs to comply with the rules of the multi\-availability zone deployment plan (that is, the value of the `MultiAZ` parameter). The specific rules are as follows:<br><br><br>* If you select multi\-availability zone deployment plan (that is, the value of `MultiAZ` is `enabled`) when switch to primary\-secondary instance, then at least two different availability zone IDs must be passed in for the `AZ`, and the first availability zone must be where the primary node is located.<br><br>   For example, if you need to create a multi\-availability zone instance with 3 nodes per shard, where the primary node is in availability zone A and the other two secondary nodes are both in availability zone C, you can refer to the following settings:<br><br>   ```JSON```<br>```   "NodeNumber":3,```<br>```   "MultiAZ": "enabled",```<br>```   "ConfigureNodes": [```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-c"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-c"```<br>```       }```<br>```   ]```<br>```   ```<br>   <br><br>* If you select single\-availability zone deployment plan (that is, the value of `MultiAZ` is `disabled`) when switch to primary\-secondary instance, then the availability zone passed in for each node must be consistent.<br><br>   For example, if you need to create a single\-availability zone instance with 3 nodes per shard, with all nodes in availability zone A, you can refer to the following settings:<br><br>   ```JSON```<br>```   "NodeNumber":3,```<br>```   "MultiAZ": "disabled",```<br>```   "ConfigureNodes": [```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       }```<br>```   ]```<br>```   ```<br>   <br><br><br>> **tip**<br><br><br>> You can call the [DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) API to query availability zone information under the target region, including availability zone ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order702856788643751\*\*\*\* |Order number. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=EnableDBInstanceHA&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "ApplyImmediately": true,
    "ShardNumber": 3,
    "NodeNumber": 3,
    "ShardedCluster": 1
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420800210023228002****",
        "Action": "EnableDBInstanceHA",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNO": "Order702856788643751****"
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
