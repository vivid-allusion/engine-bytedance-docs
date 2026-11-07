---
title: "ModifyDBInstanceAZConfigure"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstanceazconfigure"
---

Call the ModifyDBInstanceAZConfigure to modify the availability zone of a specified instance.

## Request type

Asynchronous request.

## Precautions

* During availability zone modification, the instance may experience 1 to 2 connection interruptions (each lasting less than 30 seconds) or about 10 seconds of read‑write unavailability. Proceed with caution and ensure that the client is configured with proper retry mechanisms.

* The time required to modify availability zones is affected by various factors, such as the network environment, task queue, and data volume. We recommend that you perform the operation during off\-peak hours.

* Migrating a **single\-node instance** from a single availability zone to multiple availability zones is not supported. For more details, refer to [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceAZConfigure&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ApplyImmediately |Boolean |Yes |true |Whether to execute the configuration modification immediately. Valid values:<br><br><br>* `true`: Execute now.<br><br>* `false`: Execute modification within the maintenance period. For more information on maintenance periods, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period). |
|MultiAZ |String |Yes |disabled |Set the availability zone deployment plan for the instance. Valid values:<br><br><br>* `enabled`: Multi\-availability zone deployment plan.<br><br>* `disabled`: Single availability zone deployment plan. For more information about the availability zone deployment scheme, see [Multi-AZ Zone-disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution). |
|ConfigureNodes |Array of [ConfigureNode](https://docs.byteplus.com/en/docs/55/12513#configurenode) |Yes |Refer to the Sample response. |Set the availability zone to which the new nodes belong. |
|CreateBackup |Boolean |No |true |Whether to create a full backup before the change. Valid values:<br><br><br>* `true`: Create backup.<br><br>* `false` (default): Do not create a backup.<br><br><br>> **tip**<br><br><br><br>* > This parameter is only valid for primary\-secondary instances (i.e., when `InstanceClass` is `PrimarySecondary`). Single node instances (i.e., when `InstanceClass` is `Standalone`) do not support the backup feature, so this parameter will not take effect for single node instances.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the detailed information of a specified instance, including the instance type.<br> |
|BackupPointName |String |No |b\-cn02xmmrp751i9cdzcphjmk4\*\*\*\* |Set the backup name for the full backup created before the change. If no backup name is set, the backup ID is used as the name by default. <br><br>If you need to set a backup name, it must meet the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br>> This parameter takes effect only when the need to create a backup before the change is selected (that is, `CreateBackup` is `true`).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### ConfigureNode

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AZ |String |Yes |cn\-beijing\-a |Set the availability zone to which the new nodes belong. The instance's availability zone deployment scheme affects how you configure these parameters. Specifically:<br><br><br>* When `MultiAZ` is set to `enabled` (meaning a multi\-availability zone deployment scheme is used), the number of availability zones you provide must equal the number of nodes in a single shard of the current instance. Additionally, the first availability zone must be the one where the primary node is located. For example, if the current instance contains 3 nodes per shard, you need to provide corresponding availability zone information for each node.<br><br>* When `MultiAZ` is set to `disabled` (meaning a single availability zone deployment scheme is used), provide only one availability zone. All nodes in the instance will be deployed in that availability zone.<br><br><br>> **tip**<br><br><br><br>* > You can call the [DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) API to query availability zone information under the target region, including availability zone ID.<br><br><br>* > You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) API to query the details of a specified instance, including whether a multi\-availability zone deployment scheme has been configured.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |No example value |Modifying the availability zone does not involve instance orders, so the response value of this parameter is blank. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceAZConfigure&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "MultiAZ": "disabled",
        "ConfigureNodes": [{
                "AZ": "cn-beijing-b"
        }],
        "CreateBackup": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230522150300E9F5BEC3072CC0BEC0BE",
        "Action": "ModifyDBInstanceAZConfigure",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNO": ""
    }
}
```

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceAZConfigure&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "MultiAZ": "enabled",
        "ConfigureNodes": [{
                "AZ": "cn-beijing-b"
        }, {
                "AZ": "cn-beijing-c"
        }],
        "CreateBackup": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230522150300E9F5BEC3072CC0BEC0BE",
        "Action": "ModifyDBInstanceAZConfigure",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNO": ""
    }
}
```

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceAZConfigure&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "MultiAZ": "enabled",
        "ConfigureNodes": [{
                "AZ": "cn-beijing-b"
        }, {
                "AZ": "cn-beijing-c"
        }],
        "CreateBackup": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230522150300E9F5BEC3072CC0BEC0BE",
        "Action": "ModifyDBInstanceAZConfigure",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNO": ""
    }
}
```

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceAZConfigure&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ApplyImmediately": true,
        "MultiAZ": "disabled",
        "ConfigureNodes": [{
                "AZ": "cn-beijing-a"
        }],
        "CreateBackup": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230522150300E9F5BEC3072CC0BEC0BE",
        "Action": "ModifyDBInstanceAZConfigure",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderNO": ""
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).
