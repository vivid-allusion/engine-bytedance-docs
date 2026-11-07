---
title: "CreateDBInstance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createdbinstance"
---

Call the CreateDBInstance API to create Redis instance.

## Request type

Asynchronous request.

## Precautions

Since May 17, 2022, customers who newly activate Redis and customers with existing instances must complete cross\-service access authorization. Complete the authorization as soon as possible; otherwise, an error will occur when calling APIs such as [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance), [ModifyDBInstanceSubnet](https://docs.byteplus.com/en/docs/redis/modifydbinstancesubnet), and [CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointpublicaddress). For information on cross\-service access authorization, see [Cross-Service Access Authorization](https://docs.byteplus.com/en/docs/redis/cross-service-access-authorization).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBInstance&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/redis/describeregions) API to query all region information supported by a Redis instance, including the region IDs.<br> |
|EngineVersion |String |Yes |5.0 |Database version number. Valid values:<br><br><br>* `5.0`: Redis 5.0.<br><br>* `6.0`: Redis 6.0.<br><br>* `7.0`: Redis 7.0. |
|ShardedCluster |Integer |Yes |0 |Whether to enable sharding cluster. Valid values:<br><br><br>* `0`: Disable.<br><br>* `1`: Enable.<br><br><br>> **tip**<br><br><br>> For more information about the architecture of Cache for Redis, see [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br> |
|ShardNumber |Integer |No |2 |Number of shards in the instance. Value range: 2 to 256.<br><br>> **tip**<br><br><br>> This parameter must be specified only when sharding cluster is enabled (that is, `ShardedCluster` is set to `1`).<br> |
|NodeNumber |Integer |Yes |2 |Number of nodes per shard. The value range is 1 to 6.<br><br>> **tip**<br><br><br><br>* > For nodes with a memory capacity of 256 MiB, you can create up to four nodes per account in each region by default (that is, the value of `ShardCapacity` is `256`). To adjust the purchase quota of 256 MiB nodes (maximum is 10), refer to [Account quota](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.6LSm5Y-36YWN6aKd).<br><br><br>* > A value of `1` indicates the creation of a single node instance; a value greater than `1` indicates the creation of a primary\-secondary instance. Single node instances and primary\-secondary instances support different features. For details on the feature differences between the two instance types, see [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).<br> |
|ShardCapacity |Long |Yes |1024 |Memory capacity of each shard, unit: MiB. Valid values:<br><br><br>* When sharding cluster is not enabled (i.e., when `ShardedCluster` is `0`), the memory capacity per shard can be selected from: 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 24576, 65536.<br><br>* When sharding cluster is enabled (i.e., when `ShardedCluster` is `1`), the memory capacity per shard can be selected from: 1024, 2048, 4096, 8192, 16384.<br><br><br>> **tip**<br><br><br><br>* > When creating a single node instance (i.e., `NodeNumber` is `1`), selecting a 256 MiB memory capacity is not supported.<br><br><br>* > For more details on Redis product specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification).<br> |
|MultiAZ |String |Yes |enabled |Set the availability zone deployment plan for the instance. Valid values:<br><br><br>* `disabled`: Single availability zone deployment plan.<br><br>* `enabled`: Multi\-availability zone deployment plan.<br><br><br>> **tip**<br><br><br><br>* > When a new instance is a single node instance (i.e., `NodeNumber` is `1`), only a single\-AZ deployment scheme is allowed, in which case `MultiAZ` must be `disabled`.<br><br><br>* > For more information on availability zone deployment solutions, refer to [Multi\-availability\-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution).<br> |
|ConfigureNodes |Array of [ConfigureNode](https://docs.byteplus.com/en/docs/55/12508#configurenode) |Yes |Refer to the sample request. |Set the availability zone to which the new nodes belong. |
|VpcId |String |Yes |vpc\-rs5811nceqyov0x58x4\*\*\*\* |Set the instance's Virtual Private Cloud ID.<br><br>> **tip**<br><br><br><br>* > We recommend that you connect Redis instances to ECS instances in the same VPC. Otherwise, they cannot achieve optimal communication performance. You can call the [CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc) API to create a Virtual Private Cloud.<br><br><br>* > You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query Virtual Private Cloud information that matches specified conditions, including the Virtual Private Cloud ID.<br> |
|SubnetId |String |Yes |subnet\-1g15j13jtzgu88ibuxwqp\*\*\*\* |Set the instance's subnet ID.<br><br>> **tip**<br><br><br><br>* > Subnets have availability zone attributes. You must select a subnet in the target Virtual Private Cloud that belongs to the same availability zone as the instance.<br><br><br>* > A subnet is an IP address block within a Virtual Private Cloud. All cloud resources in the Virtual Private Cloud must be deployed within a subnet. The subnet allocates private IP addresses to cloud resources. You can call the [CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet) API to create a subnet.<br><br><br>* > You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query information about all subnets in a specified availability zone, including their subnet IDs.<br> |
|InstanceName |String |No |testInstance |Instance name. The name must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1 to 128 characters.<br><br><br>> **tip**<br><br><br>> If this parameter is blank, the instance ID is used as the instance name by default.<br> |
|Password |String |No |Pwd@12\*\*\*\* |Set the password for the default account of the default database. The password must meet the following requirements:<br><br><br>* The length is 8~64 characters.<br><br>* It contains at least two of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* It supports the following special characters:<br><br><br>```Plain```<br>```()`~!@#$%^&*-+=_\|{}[];<>,.?```<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, no password will be set for the default account. The system will automatically generate a password for the default account to ensure instance access security. No account can retrieve this random password. Therefore, before connecting to the instance, you must reset the default account's password using the [ModifyDBAccount](https://docs.byteplus.com/en/docs/redis/modifydbaccount) API.<br><br><br>* > You can also set up new accounts and passwords using the [CreateDBAccount](https://docs.byteplus.com/en/docs/redis/createdbaccount) API, based on your business requirements.<br><br><br>* > To use the password\-free access feature, you must first enable it via the [ModifyDBInstanceVpcAuthMode](https://docs.byteplus.com/en/docs/redis/modifydbinstancevpcauthmode) API.<br> |
|Port |Integer |No |6379 |Customize the port number for the private network address. The value range is 1024\-65535.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the private network address defaults to using port 6379.<br><br><br>* > After creating the instance successfully, you can modify the port number of the private address. For specific procedures, refer to [Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port).<br> |
|ProjectName |String |No |default |Select the project to which the instance belongs. If this parameter is left blank, new instances are added to the default (i.e., `default`) project.<br><br>> **tip**<br><br><br>> A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources. For more details, see [Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Product_Overview).<br> |
|AllowListIds |Array of String |No |["acl\-cq014ioqkm9zt5j\*\*\*\*","acl\-cq015pp15v8buvl\*\*\*\*"] |Allowlist ID list. If this parameter is left blank, new instances are not added to any allowlist by default.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) API to query all IP allowlist information within the specified region under the current account, including allowlist ID information.<br><br><br>* > Each instance can be associated with a maximum of 100 allowlists. A maximum of 100 allowlists can be associated at a time.<br><br><br>* > Each instance can be associated with up to 1,000 IP addresses or IP address segments in CIDR format.<br> |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/55/12508#tag) |No |Refer to the sample request. |An array object of tag keys and tag values to be bound. If this parameter is left empty, new instances do not associate any tags by default. |
|ChargeType |String |No |PostPaid |Billing method. Valid values:<br><br><br>* `PostPaid` (default value): Pay\-as\-you\-go.<br><br>* `PrePaid`: Subscription.<br><br><br>> **tip**<br><br><br>> For more information about billing types, see [Pay\-as\-you\-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go) and [Subscription](https://docs.byteplus.com/en/docs/redis/subscription).<br> |
|PurchaseMonths |Integer |No |1 |The purchase duration, in months. Valid values:<br><br><br>* Monthly purchase: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`.<br><br>* Annual purchase: `12`, `24`, `36`.<br><br><br>> **tip**<br><br><br>> When `ChargeType` is `PrePaid`, this parameter is required.<br> |
|AutoRenew |Boolean |No |false |Whether to enable automatic renewal. Valid values:<br><br><br>* `false` (default): Disable.<br><br>* `true`: enable.<br><br><br>> **tip**<br><br><br>> Only valid when `ChargeType` is `PrePaid`.<br> |
|DeletionProtection |String |No |enabled |Enable or disable instance deletion protection. Valid values:<br><br><br>* `disabled` (default value): Disable.<br><br>* `enabled`: Enable.<br><br><br>> **tip**<br><br><br>> For more information on deletion protection, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection).<br> |
|NoAuthMode |String |No |open |Enable or disable password\-free access for new instances. Valid values:<br><br><br>* `open`: Enable password\-free access.<br><br>* `close` (Default value): Disable password\-free access.<br><br><br>> **tip**<br><br><br><br>* > Parameter values are case\-insensitive.<br><br><br>* > After the instance is created successfully, you can also call the [ModifyDBInstanceVpcAuthMode](https://docs.byteplus.com/en/docs/redis/modifydbinstancevpcauthmode) API to enable or disable password\-free access. For more information on password\-free access, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
|ParameterGroupId |String |No |pg\-cnlfm5yzmxehmkw\*\*\*\* |Parameter template to apply to new instances.<br><br>> **tip**<br><br><br><br>* > For Cache for Redis, a default system parameter template is created for each database version. The template contains all the parameters supported by this version and the default parameter values. If this parameter is left blank, the system will automatically select and apply the appropriate system parameter template for the new instance based on your configured database version (i.e., `EngineVersion`) and whether the instance type is a single node (i.e., if `NodeNumber` is `1`).<br><br><br>* > You can call the [DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) API to query the basic information of all parameter templates under the current account and Region, including the parameter template ID.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### ConfigureNode

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AZ |String |Yes |cn\-beijing\-a |Set the availability zone to which the new nodes belong. The number of nodes in the instance (i.e., `NodeNumber`) and the availability zone deployment scheme (i.e., the value of the `MultiAZ` parameter) both affect how this parameter is filled in. Specifically:<br><br><br>* When creating a `single node instance` (i.e., `NodeNumber` is `1`), only a single\-availability zone deployment scheme is allowed (i.e., `MultiAZ` must be `disabled`). In this case, simply pass one availability zone in `AZ`, and all nodes in the instance will be deployed in that availability zone. For example, if you need to create a single node instance and all nodes are in availability zone A, you can refer to the following settings:<br><br><br>```JSON```<br>```"NodeNumber":1,```<br>```"MultiAZ": "disabled",```<br>```"ConfigureNodes": [```<br>```    {```<br>```        "AZ": "cn-beijing-a"```<br>```    }```<br>```]```<br><br><br><br>* When creating a `primary-secondary instance` (i.e., `NodeNumber` is greater than or equal to `2`), the **number of availability zones passed must be equal to the number of nodes in a single shard** (i.e., the value of the `NodeNumber` parameter), and the value of `AZ` must comply with the multi\-availability zone deployment scheme rules. The specific rules are as follows:<br><br>   * If the `primary-secondary instance` is configured with a multi\-availability zone deployment scheme (i.e., `MultiAZ` is `enabled`), then `AZ` must contain at least 2 different availability zone IDs, and the first availability zone must be where the `primary node` is located.<br><br>      For example, if you need to create a multi\-availability zone instance with 3 nodes per shard, where the primary node is in availability zone A and the other two secondary nodes are both in availability zone C, you can refer to the following settings:<br><br>   ```JSON```<br>```   "NodeNumber":3,```<br>```   "MultiAZ": "enabled",```<br>```   "ConfigureNodes": [```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-c"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-c"```<br>```       }```<br>```   ]```<br>```   ```<br>   <br><br>   * If the `primary-secondary instance` is configured with a single\-availability zone deployment scheme (i.e., `MultiAZ` is `disabled`), then the availability zone passed for each node must be consistent.<br><br>      For example, if you need to create a single\-availability zone instance with 3 nodes per shard, with all nodes in availability zone A, you can refer to the following settings:<br><br>   ```JSON```<br>```   "NodeNumber":3,```<br>```   "MultiAZ": "disabled",```<br>```   "ConfigureNodes": [```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       },```<br>```       {```<br>```           "AZ": "cn-beijing-a"```<br>```       }```<br>```   ]```<br>```   ```<br>   <br><br><br>> **tip**<br><br><br>> You can call the [DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) API to query availability zone information under the target region, including availability zone ID.<br> |

### Tag

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |department |The tag key to be associated.<br><br>> **tip**<br><br><br><br>* > If this parameter is left empty, the new instance will not be bound to any tags. When associating tags with an instance, the tag key (Key) is required, and the tag value (Value) is optional. If the tag value is not provided, the tag value for the corresponding tag key will be empty.<br><br><br>* > Supports passing in multiple sets of tag key\-value pairs at once. Multiple sets of tag key\-value pairs are separated by commas (,). You can specify up to 20 sets of tag key\-value pairs at a time.<br><br><br>* > Each instance can be associated with up to 50 tags. Tag keys must comply with the setting rules. For details, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).<br> |
|Value |String |No |game |The tag value corresponding to the tag to be bound.<br><br>> **tip**<br><br><br><br>* > When associating tags with an instance, the tag key is required, while the tag value is optional. Leaving the tag value blank means the tag value for the corresponding tag key is empty.<br><br><br>* > Supports passing in multiple sets of tag key\-value pairs at once. Multiple sets of tag key\-value pairs are separated by commas (,). You can specify up to 20 sets of tag key\-value pairs at a time.<br><br><br>* > Each instance can be associated with up to 50 tags. Tag values must comply with the setting rules. For details, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderNO |String |Order702856788643751\*\*\*\* |Order number. |
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateDBInstance&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "RegionId":"cn-beijing",
    "ShardedCluster":1,
    "ShardNumber":2,
    "Password":"Pwd@12****",
    "EngineVersion":"5.0",
    "NodeNumber":3,
    "MultiAZ": "enabled",
    "ConfigureNodes": [
                {
                    "AZ": "cn-beijing-a"
                },
                {
                    "AZ": "cn-beijing-b"
                },
                {
                    "AZ": "cn-beijing-b"
                }
    ],
    "ShardCapacity":8192,
    "VpcId":"vpc-rs5811nceqyov0x58x4****",
    "SubnetId":"subnet-1g15j13jtzgu88ibuxwqp****",
    "AllowListIds":[
        "acl-cq014ioqkm9zt5j****",
        "acl-cq015pp15v8buvl****"
    ],
    "Tags":[
        {
            "Key":"department",
            "Value":"game"
        },
        {
            "Key":"owner",
            "Value":"Alice"
        }
    ]
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204151541400102120740810061****",
          "Action": "CreateDBInstance",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": {
          "InstanceId": "redis-cn0212gzmh2xs****",
          "OrderNO": "Order702856788643751****"
     }
}
```

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateDBInstance&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "RegionId": "cn-beijing",
    "ShardedCluster": 0,
    "Password": "Pwd@12****",
    "EngineVersion": "5.0",
    "NodeNumber": 2,
    "MultiAZ": "disabled",
    "ConfigureNodes": [
                {
                    "AZ": "cn-beijing-a"
                },
               {
                    "AZ": "cn-beijing-a"
                }
    ],
    "ShardCapacity": 8192,
    "VpcId": "vpc-rs5811nceqyov0x58x4****",
    "SubnetId": "subnet-1g15j13jtzgu88ibuxwqp****"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204151541400102120740810061****",
          "Action": "CreateDBInstance",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": {
          "InstanceId": "redis-cn0212gzmh2xs****",
          "OrderNO": "Order702856788643751****"
     }
}
```

## Error code

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/redis/error-code).
