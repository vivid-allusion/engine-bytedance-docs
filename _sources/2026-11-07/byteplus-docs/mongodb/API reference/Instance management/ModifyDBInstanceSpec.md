---
title: "ModifyDBInstanceSpec"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbinstancespec"
---

Call the ModifyDBInstanceSpec API to modify the configuration of the target MongoDB instance (such as node specification or storage capacity).

## Request type

Asynchronous request.

## Precautions

* During configuration change, one or two temporary disconnections may occur, lasting for about 30 seconds each time. Be cautious with this operation. We recommend you change configurations during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

   For more information about changing the instance configuration, refer to [Changing instance configuration](https://docs.byteplus.com/en/docs/mongodb/solutions-for-spec-modification).

* When calling this API, you must modify at least one configuration item of the instance. That is, you cannot leave blank all the parameters `NodeSpec`, `MongosNodeSpec`, `ShardNumber`, `MongosNodeNumber`, and `StorageSpaceGB` or keep their values unchanged.

* For details of the fee settlement rules for changing the instance configuration of the instance, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/pay-as-you-go#.5Y-Y5pu06YWN572u) and [Yearly or monthly subscription](https://docs.byteplus.com/en/docs/mongodb/subscription#.5Y-Y5pu06YWN572u).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|InstanceType |String |Yes |ReplicaSet |The instance types of MongoDB, and the value range is as follows:<br><br><br>* `ReplicaSet`: Replica set.<br><br>* `ShardedCluster`: Sharding cluster. |
|NodeSpec |String |No |mongo.2c4g |Specification code of the instance. Where:<br><br><br>* When the instance type is Replica Set (i.e., the value of `InstanceType` is `ReplicaSet`), this parameter indicates the compute node specifications of the replica set instance (such as `mongo.2c4g`).<br><br>* When the instance type is Sharding Cluster (i.e., the value of `InstanceType` is `ShardedCluster`), this parameter indicates the specifications of the shard node (such as `mongo.mongos.2c4g`).<br><br><br>tip<br><br><br>* You can call the [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) API to check the instance specification information, including the specification code.<br><br>* If this parameter is left blank or indicates the existing specification of the current node in the instance, the specification of the current node will not be modified. |
|ShardNumber |Integer |No |4 |Number of shards in a sharding cluster. Value range: 2 to 32.<br><br>tip<br><br><br>* Currently, the number of shards can be increased but cannot be reduced.<br><br>* This parameter is valid only when `InstanceType` is `ShardedCluster`.<br><br>* If this parameter is left blank or is the same as the current shard number of the instance, the shard number of the current instance will not be modified. |
|MongosNodeSpec |String |No |mongo.mongos.4c8g |Specification code of Mongos nodes.<br><br>tip<br><br><br>* You can call the [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) API to query the supported node specifications that can be used for creating MongoDB instances, including the node specification code.<br><br>* This parameter is valid only when `InstanceType` is `ShardedCluster`.<br><br>* If this parameter is left blank or indicates the existing specification of the current node in the instance, the specification of the current node will not be modified. |
|MongosNodeNumber |Integer |No |4 |Number of Mongos nodes. Value range: 2 to 32.<br><br>tip<br><br><br>* The number of Mongos nodes can be reduced only when it is greater than or equal to 3. The number of nodes can be reduced to a maximum of 2.<br><br>* This parameter is valid only when `InstanceType` is `ShardedCluster`.<br><br>* If this parameter is left blank or is the same as the current node number of the instance, the Mongos node number of the current instance will not be modified. |
|StorageSpaceGB |Integer |No |25 |Storage capacity (in GiB).<br><br>tip<br><br><br>* To ensure the normal operation of the instance after change, the reduced storage capacity must be greater than or equal to 1.2 times the used space.<br><br>* When `InstanceType` is `ReplicaSet`, the value of the `StorageSpaceGB` parameter will be the total storage capacity of the instance.<br><br>* When `InstanceType` is `ShardedCluster`, the total capacity of the instance = Value of `StorageSpaceGB` parameter × Number of shards.<br><br>* If this parameter is left blank or is same with the current storage capacity of the instance, the storage capacity of the current instance will not be modified. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID. |
|OrderNO |String |Order708525331148613\*\*\*\* |Order ID. |

## Request sample 1

Reduce the node specification of the replica set instance to 2 cores 4 GiB, and the storage capacity to 50 GiB.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBInstanceSpec&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-e405f8e2****",
    "InstanceType": "ReplicaSet",
    "NodeSpec": "mongo.2c4g",
    "StorageSpaceGB": 50
}
```

## Response sample 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20220309171813010212150034080B****",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2020-12-07",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mongo-replica-e405f8e2****",
        "OrderNO": "Order708525331148613****"
    }
}
```

## Request sample 2

Increase the number of shard and Mongos nodes in the sharding cluster to 3 respectively, and upgrade the shard and Mongos nodes to 4 cores 8 GiB.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBInstanceSpec&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-596e1fdf****",
    "InstanceType": "ShardedCluster",
    "NodeSpec": "mongo.shard.4c8g",
    "MongosNodeSpec": "mongo.mongos.4c8g",
    "MongosNodeNumber": 3,
    "ShardNumber": 3
}
```

## Response sample 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20220309171813010212150034080B****",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2020-12-07",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mongo-replica-e405f8e2****",
        "OrderNO": "Order708525331148613****"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
