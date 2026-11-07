---
title: "RestoreToNewInstance"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/restoretonewinstance"
---

Call the RestoreToNewInstance API to restore the instance data to a new instance according to the backup file or time point.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|SrcDBInstanceId |String |Yes |mongo\-replica\-3b96fa21\*\*\*\* |The instance ID of the source instance used for backup and restoration.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) interface to query the basic information of all MongoDB instances in the target region, including the instance ID. |
|BackupId |String |No |b8174a144f22443ca3a1a6bcd49d\*\*\*\* |The backup file ID of the source instance, which is used to specify the backup to be used when restoring from the backup file.<br><br>tip<br><br><br>* One of the `BackupId` and `RestoreTime` parameters must be selected for input.<br><br>* You can call the [DescribeBackups](https://docs.byteplus.com/en/docs/mongodb/describebackups) interface to query all backup information under the specified instance, including the backup ID.<br><br>* Currently, only replica set instances support restoring to a new instance from a backup set, and sharded cluster instances are not supported. For more information about restoring to a new instance from a backup file, refer to [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file). |
|RestoreTime |String |No |2024\-04\-10T14:17:20Z |Used to specify the time point required for restoration according to the time point, in the format of *yyyy\-MM\-dd*T*HH:mm:ss*Z (UTC).<br><br>tip<br><br><br>* Either the `BackupId` or `RestoreTime` parameter must be selected for input.<br><br>* You can call the [DescribeRecoverableTime](https://docs.byteplus.com/en/docs/mongodb/describerecoverabletime) interface to query the recoverable time period supported by the specified instance.<br><br>* It is recommended to select a time point within 7 days for restoration. If the restoration time point exceeds 7 days, it will affect the read and write performance of the primary\-secondary instance. For more information about restoring to a new instance according to the time point, refer to [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point). |
|ZoneId |String |Yes |ap\-southeast\-1a |The ID of the availability zone where the new instance is located.<br><br>tip<br><br><br>* You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/mongodb/describeavailabilityzones) interface to view the information of all availability zones where MongoDB instances can be created under the current account, including the availability zone ID.<br><br>* If you need to deploy the new instance in multiple availability zones, you can pass in three availability zone IDs at the same time, separated by English commas (,). For more details, refer to [Multi-availability zone disaster recovery solution](https://docs.byteplus.com/en/docs/mongodb/feature-introduction). |
|VpcId |String |Yes |vpc\-rs5811nceqyov0x58x4\*\*\*\* |Virtual Private Cloud (VPC) ID.<br><br>tip<br><br>You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) interface to query the list information of all Virtual Private Clouds (VPCs) under the current account, including the Virtual Private Cloud (VPC) ID. |
|SubnetId |String |Yes |subnet\-274c1ohtlim0w7fap8sna\*\*\*\* |Subnet ID.<br><br>tip<br><br>You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) interface to query the subnet list information under the specified Virtual Private Cloud (VPC), including the Subnet ID. |
|DBEngine |String |No |MongoDB |Database engine.<br><br>tip<br><br>No need to set. After recovery, the database engine of the new instance is consistent with that of the source instance, and the value is fixed as `MongoDB`. |
|DBEngineVersion |String |No |MongoDB_5_0 |Database engine version.<br><br>tip<br><br>No need to set. The database version of the new instance after restoration is the same as that of the source instance. For example, if the source instance is MongoDB 5.0, the new instance must also be MongoDB 5.0. |
|InstanceType |String |No |ReplicaSet |The instance types of MongoDB. The value range is as follows:<br><br><br>* `ReplicaSet`: Replica set.<br><br>* `ShardedCluster`: Sharding cluster.<br><br><br>tip<br><br>The instance type of the new instance needs to be consistent with that of the source instance. For example, if the source instance type is a sharding cluster, the new instance must also be a sharding cluster. |
|NodeSpec |String |Yes |mongo.2c4g |The specification code of the instance. Where:<br><br><br>* When the source instance type is a replica set (i.e., the value of `InstanceType` is `ReplicaSet`), this parameter represents the specification of the compute node of the new replica set instance after restoration.<br><br>* When the source instance type is a sharded cluster (i.e., the value of `InstanceType` is `ShardedCluster`), this parameter represents the specification of the Shard node of the new sharded cluster instance after restoration.<br><br><br>tip<br><br>You can call the [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) interface to view the instance specification information, including the specification code. |
|NodeNumber |Integer |No |3 |Node count, where:<br><br><br>* When the source instance type is a replica set (i.e., the value of `InstanceType` is `ReplicaSet`), this parameter represents the number of compute nodes of the new replica set instance after restoration.<br><br>* When the source instance type is a sharding cluster (i.e., the value of `InstanceType` is `ShardedCluster`), this parameter represents the number of nodes in each shard of the new sharding cluster instance after restoration.<br><br><br>tip<br><br>Currently, each replica set instance and each shard only support 3 nodes, and the value is fixed at `3`. |
|MongosNodeSpec |String |No |mongo.mongos.2c4g |The specification code of the Mongos node in the sharding cluster.<br><br>tip<br><br><br>* When the instance type is a sharding cluster (i.e., the value of `InstanceType` is `ShardedCluster`), this parameter is required.<br><br>* You can call the [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) interface to view the instance specification information of the sharding cluster, including the specification code. |
|MongosNodeNumber |Integer |No |2 |The number of Mongos nodes in the sharding cluster. The value range is 2 to 32.<br><br>tip<br><br>When the instance type is a sharding cluster (that is, the value of `InstanceType` is `ShardedCluster`), this parameter is required. |
|ShardNumber |Integer |No |2 |The number of shards in the sharding cluster. Value range: 2 to 32.<br><br>tip<br><br>When the instance type is a sharding cluster (that is, the value of `InstanceType` is `ShardedCluster`), this parameter is required. |
|StorageSpaceGB |Integer |Yes |100 |The total storage space of the replica set instance, or the storage space of a single Shard shard in the sharding cluster, in GiB, with a step size of 10.<br><br>tip<br><br><br>* If the instance type is a sharding cluster (i.e., the value of `InstanceType` is `ShardedCluster`), the total capacity of the entire instance after successful creation is the storage space of a single Shard shard multiplied by the number of Shard shards.<br><br>* You can call the [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) interface to view the specification information of the MongoDB instance, including the storage space specifications supported by different nodes.<br><br>* To ensure the normal operation of the new instance after restoration, the storage space capacity of the new instance must be **greater than or equal to 1.2 times the used space of the original instance**. For more details, refer to [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file) or [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point). |
|ConfigServerNodeSpec |String |No |mongo.config.2c4g |The specification code of the ConfigServer node in the sharding cluster. The default value is `mongo.config.2c4g`.<br><br>tip<br><br><br>* This parameter takes effect only when the instance type is a sharding cluster (i.e., the value of `InstanceType` is `ShardedCluster`).<br><br>* You can call the [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) interface to view the instance specification information of the sharding cluster, including the specification code. |
|ConfigServerStorageSpaceGB |Integer |No |20 |The storage space of the ConfigServer in the sharding cluster, in GiB. The step size is 10, and the default value is 20.<br><br>tip<br><br><br>* This parameter takes effect only when the instance type is a sharding cluster (that is, the value of `InstanceType` is `ShardedCluster`).<br><br>* Different node specifications correspond to different upper limits of supported storage space. You can call the [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) API to view the specification information of the MongoDB instance, including the storage space specifications supported by different nodes.<br><br>* To ensure the normal operation of the new instance after restoration, the storage space capacity of the new instance must be **greater than or equal to 1.2 times the used space of the original instance**. For more details, refer to [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file) or [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point). |
|SuperAccountName |String |No |root |Database account name. Currently, only the super administrator account can be set when creating an instance, and the account name is fixed as `root`. |
|SuperAccountPassword |String |No |Passwor\*\*\*\* |The password of the root account. The password must meet the following conditions simultaneously:<br><br><br>* It can only be composed of upper and lower case letters, numbers, and the following special characters: `_#!@$%^&*()+=-`.<br><br>* The length should be between 8 and 32 characters.<br><br>* It should contain at least three of the following: upper case letters, lower case letters, numbers, or special characters.<br><br>* Weak passwords that are easy to crack (such as `Admin@123`) are not allowed.<br><br><br>tip<br><br><br>* If this parameter is left blank, it means no password is set for the root account, and in this case, the system will automatically generate a password for the root account to ensure the security of instance access.<br><br>* You can also modify the password of the root account through the [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) interface after the instance is created.<br><br>* If you use special characters in the password, you may need to escape the special characters when connecting to the instance. For more details, refer to [Special characters that need to be escaped](https://docs.byteplus.com/en/docs/mongodb/account-and-permission#why-does-the-connection-fail-when-the-account-password-in-the-connection-string-contains-special-characters).<br><br>* For details about the weak passwords prohibited in MongoDB, refer to [Weak password list](https://docs.byteplus.com/en/docs/mongodb/account-overview#weak-password-list). |
|InstanceName |String |No |testname |Instance name. The name must meet the following requirements at the same time:<br><br><br>* It cannot start with a number or a hyphen (\-).<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length must be 2 to 64 characters.<br><br><br>tip<br><br><br>* If this parameter is not filled in, the instance ID will be used as the instance name by default.<br><br>* You can customize the instance name according to your needs. There is no uniqueness requirement for the instance name. |
|ChargeType |String |No |Prepaid |The instance billing method of the instance. The value range is as follows:<br><br><br>* `PostPaid` (default): Pay\-as\-you\-go (also known as post\-paid).<br><br>* `Prepaid`: Yearly or monthly subscription (also known as pre\-paid).<br><br><br>tip<br><br>For more information about the billing method, refer to [Billing methods](https://docs.byteplus.com/en/docs/mongodb/billing-method). |
|AutoRenew |Boolean |No |true |Whether to enable auto\-renewal, with the following value range:<br><br><br>* `false` (default): Do not enable auto\-renewal.<br><br>* `true`: Enable auto\-renewal.<br><br><br>tip<br><br>When the value of `ChargeType` is `Prepaid`, this parameter is required. |
|PeriodUnit |String |No |Year |Specify the yearly or monthly subscription instance as the yearly or monthly type. The values are as follows:<br><br><br>* `Year`: Yearly subscription.<br><br>* `Month`: Monthly subscription.<br><br><br>tip<br><br>When the value of `ChargeType` is `Prepaid`, this parameter is required. |
|Period |Integer |No |3 |The purchase duration of the yearly/monthly instance, where:<br><br><br>* When `PeriodUnit` is `Year`, the value of `Period` is from 1 to 3.<br><br>* When `PeriodUnit` is `Month`, the value of `Period` is from 1 to 9.<br><br><br>tip<br><br>When the value of `ChargeType` is `Prepaid`, this parameter is required. |
|ProjectName |String |No |default |Select the project to which the instance belongs. If this parameter is left blank, the new instance will be added to the default project by default.<br><br>tip<br><br>A project is a virtual concept that includes a set of resources, users, and roles. Through a project, a set of resources can be viewed and managed uniformly, and the permissions of users and roles within the project to these resources can be controlled. For more details, refer to [Resource management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects). |
|Tags |Object[] |No | |Arrays of tag keys and tag values objects to be associated with.<br><br>tip<br><br>Leaving this parameter empty means that no tags will be associated with the new instance. |
|Key |String |Yes |instancetype |The tag key corresponding to the tag needs to be associated with.<br><br>tip<br><br><br>* When associating tags with an instance, the tag key (Key) is required, and the tag value (Value) is optional. Not filling in the tag value means that the tag value corresponding to the tag key is empty.<br><br>* Supports passing in multiple sets of tag key\-value objects at a time, with multiple sets of tag key\-value objects separated by English commas (,). Up to 20 sets of tag key\-value pairs can be passed in at the same time.<br><br>* A single instance can be associated with a maximum of 50 tags. The tag key must meet the setting rules. For specific rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/mongodb/associate-tag#tag-setting-rules). |
|Value |String |No |replica |The tag value corresponding to the tag needs to be associated with.<br><br>tip<br><br><br>* When associating tags with an instance, the tag key (Key) is required, and the tag value (Value) is optional. Not filling in the tag value means that the tag value corresponding to the tag key is empty.<br><br>* It is supported to pass in multiple sets of tag key\-value objects at a time, and multiple sets of tag key\-value objects are separated by English commas (,). Up to 20 sets of tag key\-value pairs can be passed in at the same time.<br><br>* A single instance can be associated with up to 50 tags. The tag key needs to meet the setting rules. For specific rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/mongodb/associate-tag#tag-setting-rules). |
|NodeAvailabilityZone |Object[] |No | |Add read\-only node information, including the availability zone and quantity of the read\-only nodes.<br><br>tip<br><br>Leaving this parameter blank means not adding any read\-only nodes to the instance. |
|ZoneId |String |Yes |ap\-southeast\-1a |The availability zone where the read\-only node is located.<br><br>tip<br><br>The availability zone where the read\-only node is located must be a subset of the availability zone where the instance is located. |
|NodeNumber |Integer |Yes |1 |The number of read\-only nodes to be added in the current availability zone.<br><br>Currently, only the replica set instances and the shard in sharding cluster instances support adding read\-only nodes. Among them:<br><br><br>* When the instance type is a replica set (i.e., the value of `InstanceType` is `ReplicaSet`), this value represents the total number of read\-only nodes in a single replica set instance. Each replica set instance supports adding up to 5 read\-only nodes.<br><br>* When the instance type is a sharding cluster (i.e., the value of `InstanceType` is `ShardedCluster`), this value represents the number of read\-only nodes in each shard. Each shard can add up to 5 read\-only nodes.<br><br><br>tip<br><br>For more information about the function introduction and usage restrictions of read\-only nodes, refer to [Managing read-only nodes](https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes). |
|Port |String |No |3713 |Set the port number for the private network connection address for the restored new instance. The valid value range is from 1000 to 65535.<br><br>tip<br><br><br>* If this parameter is left blank, the private network connection address of the instance will use port 3717 by default.<br><br>* After the instance is successfully created, you can also modify the port number of the network address through the [ModifyDBEndpointPort](https://docs.byteplus.com/en/docs/mongodb/modifydbendpointport) interface. For more details on modifying port number, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports). |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID. |
|OrderNO |String |Order707662635934417\*\*\*\* |Order ID. |

## Request sample 1

Restore the data of the source replica set instance to a new replica set instance by specifying the backup file.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=RestoreToNewInstance&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "SrcDBInstanceId": "mongo-replica-3b96fa21****",
    "BackupId": "b8174a144f22443ca3a1a6bcd49d****",
    "ZoneId": "ap-southeast-1a,ap-southeast-1b,ap-southeast-1c",
    "NodeSpec": "mongo.4c8g",
    "StorageSpaceGB": 30,
    "VpcId": "vpc-13fuw95qz5fk03n6nu45b****",
    "SubnetId": "subnet-mjm6qdbzuio05smt1bwf****",
    "InstanceType": "ReplicaSet"
}
```

## Response sample 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "RestoreToNewInstance",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mongo-replica-3b97ba41****",
        "OrderNO": "Order707662635934417****"
    }
}
```

## Request sample 2

Restore the backup data at a specified time point in the source sharding cluster instance to a new sharding cluster instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=RestoreToNewInstance&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "SrcDBInstanceId": "mongo-shard-fc1c77c3****",
    "RestoreTime": "2024-04-10T14:59:00Z",
    "ZoneId": "ap-southeast-1a,ap-southeast-1b,ap-southeast-1c",
    "NodeSpec": "mongo.shard.2c4g",
    "StorageSpaceGB": 30,
    "MongosNodeSpec": "mongo.mongos.2c4g",
    "ShardNumber": 2,
    "MongosNodeNumber": 2,
    "VpcId": "vpc-13fuw95qz5fk03n6nu45b****",
    "SubnetId": "subnet-mjm6qdbzuio05smt1bwf****",
    "InstanceType": "ShardedCluster"
}
```

## Response sample 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "RestoreToNewInstance",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mongo-shard-8bcaa3e1****",
        "OrderNO": "Order735625423621919****"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
