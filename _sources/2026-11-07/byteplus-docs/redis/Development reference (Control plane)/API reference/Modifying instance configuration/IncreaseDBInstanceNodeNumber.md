---
title: "IncreaseDBInstanceNodeNumber"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/increasedbinstancenodenumber"
---

Call the IncreaseDBInstanceNodeNumber API to increase the number of single shard nodes for target Redis instance.

## Request type

Asynchronous request.

## Precautions

* Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) always contain one node and do not support changing the number of nodes. For more details about configuration change solutions supported by different instance or architecture types, refer to [Solutions for modification of instance specifications](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification).

* Initiating a configuration change after enabling data flashback will automatically disable the data flashback feature. After the data flashback feature is disabled, previous flashback points will no longer be retained. You need to call the [StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) API to enable data flashback after the configuration change is complete. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=IncreaseDBInstanceNodeNumber&serviceCode=Redis&version=2020-12-07&groupName=变更实例配置)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ApplyImmediately |Boolean |Yes |true |Whether to execute the configuration modification immediately. Valid values:<br><br><br>* `true`: Execute now.<br><br>* `false`: Execute modification within the maintenance period.<br><br><br>> **tip**<br><br><br>> For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |
|NodesNumberToIncrease |Integer |Yes |2 |Set the number of nodes to increase in a single shard. Each shard supports 2 to 6 nodes, meaning 2 <= (current number of nodes + number of nodes to increase) <= 6.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of a specified instance, including the current number of nodes in each shard.<br><br><br>* > By default, each account can create a maximum of 4 nodes of 256MiB specification in each region. If you need to adjust the purchase quota for 256MiB specification nodes (up to 10), refer to [Constraints and Limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.6LSm5Y-36YWN6aKd).<br> |
|ConfigureNewNodes |Array of [ConfigureNode](https://docs.byteplus.com/en/docs/55/12464#configurenode) |No | |Configure the availability zone list for new nodes. |
|CreateBackup |Boolean |No |true |Whether to create a full backup before the change. Valid values:<br><br><br>* `true`: Create a backup.<br><br>* `false` (default value): Do not create. |
|BackupPointName |String |No |testbackup |Set the backup name for the full backup created before the change. The backup name must satisfy the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > This parameter takes effect only when the need to create a backup before the change is selected (that is, `CreateBackup` is `true`).<br><br><br>* > If no backup name is set, the backup ID is used as the name by default.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### ConfigureNode

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AZ |String |No |cn\-beijing\-a |Set the availability zone for the new nodes. The number of new nodes in the instance (i.e., the value of the `NodesNumberToIncrease` parameter) and the availability zone deployment scheme (i.e., the value of the `MultiAZ` parameter) will affect how this parameter is filled in. Specifically:<br><br><br>* When the instance deployment scheme is multi\-AZ (i.e., the `MultiAZ` value is `enabled`), **this parameter is required**, and **the number of availability zones entered must be equal to the number of single\-shard nodes to be added** (i.e., the `NodesNumberToIncrease` parameter value). For example, if you need to add 2 more nodes to each shard of a multi\-AZ instance, and these two nodes are in AZ A and B respectively, you can refer to the following settings:<br><br><br>```JavaScript```<br>```"NodesNumberToIncrease":2,```<br>```"ConfigureNewNodes": [```<br>```    {```<br>```        "AZ": "cn-beijing-a"```<br>```    },```<br>```    {```<br>```        "AZ": "cn-beijing-b"```<br>```    }```<br>```]    ```<br><br><br><br>* When the instance deployment scheme is single\-AZ (i.e., the `MultiAZ` value is `disabled`), there is no need to set this parameter. Newly added nodes will default to the availability zone where the instance currently resides.<br><br><br>> **tip**<br><br><br><br>* > You can call the [DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) API to query availability zone information under the target region, including availability zone ID.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the details of a specified instance, including whether a multi\-availability zone deployment scheme has been configured.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order716986589022527\*\*\*\* |Order ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=IncreaseDBInstanceNodeNumber&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "ApplyImmediately": true,
    "CreateBackup": true,
    "ConfigureNewNodes": [
        {
            "AZ": "cn-beijing-b"
        },
        {
            "AZ": "cn-beijing-a"
        }
    ],
    "NodesNumberToIncrease": 2
}
```

## Response example

```JSON
{
        "ResponseMetadata": {
                "RequestId": "20230509153711EDF4F0D1DBEFA625xxxx",
                "Action": "IncreaseDBInstanceNodeNumber",
                "Version": "2020-12-07",
                "Service": "Redis",
                "Region": "cn-beijing"
        },
        "Result": {
                "OrderNO": "Order723108288213844****"
        }
}
```

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=IncreaseDBInstanceNodeNumber&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "CreateBackup": true,
        "NodesNumberToIncrease": 2
}
```

## Response example

```JSON
{
        "ResponseMetadata": {
                "RequestId": "20230509153711EDF4F0D1DBEFA625xxxx",
                "Action": "IncreaseDBInstanceNodeNumber",
                "Version": "2020-12-07",
                "Service": "Redis",
                "Region": "cn-beijing"
        },
        "Result": {
                "OrderNO": "Order723108288213844****"
        }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
