---
title: "DecreaseDBInstanceNodeNumber"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/decreasedbinstancenodenumber"
---

Call the DecreaseDBInstanceNodeNumber API to decrease the number of single shard nodes for a specified instance.

## Request type

Asynchronous request.

## Precautions

* Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) always contain one node and do not support changing the number of nodes. For more details about configuration change solutions supported by different instance or architecture types, refer to [Solutions for modification of instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You need to call the [StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) API to enable data flashback after the configuration change is complete. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DecreaseDBInstanceNodeNumber&serviceCode=Redis&version=2020-12-07&groupName=变更实例配置)

## Request parameters

|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ApplyImmediately |Boolean |Yes |true |Whether to execute the configuration modification immediately. Valid values:<br><br><br>* `true`: Execute now.<br><br>* `false`: Execute modification within the maintenance period.<br><br><br>> **tip**<br><br><br>> For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|NodesNumberToDecrease |Integer |Yes |2 |Set the number of nodes to decrease in a single shard. Each shard supports 2 to 6 nodes, meaning 2 <= (current number of nodes \- number of nodes to decrease) <= 6.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of a specified instance, including the current number of nodes in each shard.<br><br><br>* > By default, each account can create a maximum of 4 nodes of 256MiB specification in each region. If you need to adjust the purchase quota for 256MiB specification nodes (up to 10), refer to [Constraints and Limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.6LSm5Y-36YWN6aKd).<br> |
|NodesToRemove |Array of [ConfigureNode](https://docs.byteplus.com/en/docs/55/12462#configurenode) |No | |Set the list of availability zones from which nodes are to be reduced. |
|CreateBackup |Boolean |No |true |* Whether to create a full backup before the change. Valid values are as follows: `true`: create backup. `false` (default): do not create backup. |
|BackupPointName |String |No |testbackup |Set the backup name for the full backup created before the change. The backup name must satisfy the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > This parameter is effective only when creating a backup before the change is selected (i.e., `CreateBackup` is `true`).<br><br><br>* > If no backup name is set, the backup ID is used as the name by default.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### ConfigureNode

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AZ |String |No |cn\-beijing\-a |Configure the availability zones where nodes are to be decreased. The number of nodes to decrease for the instance (i.e., the `NodesNumberToDecrease` parameter value) and the availability zone deployment scheme (i.e., the `MultiAZ` parameter value) both influence how this parameter should be configured. Specifically:<br><br><br>* When the instance deployment scheme is multi\-availability zone (i.e., the `MultiAZ` value is `enabled`), **this parameter is required**, and **the number of availability zones entered must equal the number of nodes to be decreased per shard** (i.e., the `NodesNumberToDecrease` parameter value). For example, if you need to decrease 2 nodes from each shard in a multi\-availability zone instance, and these two nodes belong to availability zone A and B respectively, you can refer to the following settings:<br><br><br>```JavaScript```<br>```"NodesNumberToDecrease":2,```<br>```"NodesToRemove": [```<br>```    {```<br>```        "AZ": "cn-beijing-a"```<br>```    },```<br>```    {```<br>```        "AZ": "cn-beijing-b"```<br>```    }```<br>```]    ```<br><br><br><br>* When the instance deployment scheme is single\-availability zone (i.e., the `MultiAZ` value is `disabled`), this parameter does not need to be set. The availability zone of the nodes to be decreased is the instance's current availability zone.<br><br><br>> **tip**<br><br><br><br>* > Each primary\-secondary instance must retain at least 2 nodes. If the instance is deployed with a multi\-availability zone scheme, the remaining nodes must be deployed in at least 2 different availability zones.<br><br><br>* > You can call the [DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) API to query availability zone information under the target region, including availability zone ID.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the details of a specified instance, including whether a multi\-availability zone deployment scheme has been configured.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order716986589022527\*\*\*\* |Order ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DecreaseDBInstanceNodeNumber&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "CreateBackup": true,
        "NodesToRemove": [{
                "AZ": "cn-beijing-a"
        },{
                "AZ": "cn-beijing-b"
        }], 
        "NodesNumberToDecrease": 2
}
```

## Response example

```JSON
{
        "ResponseMetadata": {
                "RequestId": "20230509185031CB2269209DCB1A3F1A3F",
                "Action": "DecreaseDBInstanceNodeNumber",
                "Version": "2020-12-07",
                "Service": "Redis",
                "Region": "cn-beijing"
        },
        "Result": {
                "OrderNO": "Order723113289630009****"
        }
}
```

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DecreaseDBInstanceNodeNumber&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "CreateBackup": false,
        "NodesNumberToDecrease": 1
}
```

## Response example

```JSON
{
        "ResponseMetadata": {
                "RequestId": "20230509185031CB2269209DCB1A3F1A3F",
                "Action": "DecreaseDBInstanceNodeNumber",
                "Version": "2020-12-07",
                "Service": "Redis",
                "Region": "cn-beijing"
        },
        "Result": {
                "OrderNO": "Order723113289630009****"
        }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
