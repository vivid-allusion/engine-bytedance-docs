---
title: "CreateDBEndpoint"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/createdbendpoint"
---

Call the CreateDBEndpoint API to create a connection address for the target MongoDB instance.

## Request type

Asynchronous request.

## Precautions

* Currently, only instance\- or component\-level addresses can be created through APIs. After the API is successfully called, the system will automatically generate addresses for all nodes (including the primary and secondary nodes) under the instance or component.

* Different types of MongoDB instances support different types of addresses for application or release. For more information, refer to [Address types](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction#.6L-e5o6l5Zyw5Z2A57G75Z6L).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-011d2479\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|ObjectId |String |No |mongo\-shard\-011d2479\*\*\*\*\-s0 |The ID of a single Shard or ConfigServer component for which a connection address needs to be created.<br><br>tip<br><br><br>* This parameter is only valid for MongoDB sharding cluster instances.<br><br>* When applying for a connection address for a Shard (or ConfigServer component) in a sharding cluster instance, only one parameter can be selected from `ObjectId`, `ObjectIds`, or `AllShard` to pass in; otherwise, an error will be reported when calling the interface.<br><br>* You can call the [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) API to query the IDs of all components under the target sharding cluster instance.<br><br>* Currently only instance\- or component\-level addresses can be created through APIs. A separate address cannot be created for a node under a component (primary or secondary node). |
|ObjectIds |String[] |No |[mongo\-shard\-011d2479\*\*\*\*\-s0] |A list of Shard or ConfigServer component IDs for which connection addresses need to be created.<br><br>tip<br><br><br>* This parameter is only valid for MongoDB sharding cluster instances.<br><br>* When applying for a connection address for a Shard (or ConfigServer component) in a sharding cluster instance, only one parameter can be selected from `ObjectId`, `ObjectIds`, or `AllShard` to pass in; otherwise, an error will be reported when calling the interface.<br><br>* You can call the [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) API to query the IDs of all components under the target sharding cluster instance.<br><br>* Currently only instance\- or component\-level addresses can be created through APIs. A separate address cannot be created for a node under a component (primary or secondary node). |
|AllShard |Boolean |No |false |Whether to batch create connection addresses for all shards in the current instance. The value range is as follows:<br><br><br>* `true`: Batch create.<br><br>* `false`: Do not batch create.<br><br><br>tip<br><br><br>* This parameter is only valid for MongoDB sharding cluster instances.<br><br>* When applying for a connection address for a Shard (or ConfigServer component) in a sharding cluster instance, only one parameter can be selected from `ObjectId`, `ObjectIds`, or `AllShard` to pass in; otherwise, an error will be reported when calling the interface. |
|NetworkType |String |No |Private |The network type of the address, with the following range of values:<br><br><br>* `Private` (default): Private address<br><br>* `Public`: Public address. |
|MongosNodeIds |String[] |No |["mongo\-shard\-9a554522\*\*\*\*\-0","mongo\-shard\-9a554522\*\*\*\*\-1"] |The ID of the Mongos node for which a public network connection address needs to be applied.<br><br>tip<br><br><br>* This parameter is required only when applying for the public network address of the Mongos node in a sharding cluster instance.<br><br>* It supports applying for the public network addresses of multiple Mongos nodes at the same time, and multiple Mongos node IDs are separated by English commas (,).<br><br>* You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) API to query the information of all Mongos nodes under the target instance sharding cluster instance, including the node ID of the Mongos. |
|EipIds |String[] |No |["eip\-2d744t595x6o058ozfeht\*\*\*\*","eip\-2byu2l2b27lz42dx0efko\*\*\*\*"] |The list of EIP IDs that need to be bound when applying for a public address.<br><br>tip<br><br><br>* This parameter is required only when `NetworkType` is `Public`. The number of EIPs to be filled in varies depending on the instance or component type. Specifically:<br><br>   * When applying for a public address for a Mongos node, the number of EIPs passed in must be the same as the number of `MongosNodeIds`. For example, if only 1 Mongos node ID is passed in, then only 1 EIP ID needs to be passed in.<br><br>   * When applying for a public address for a replica set instance, Shard shard, or ConfigServer, 2 EIP IDs must be filled in for each instance or component at the same time. For details on the number of EIPs that need to be bound to each public network address, refer to [Address introduction](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction).<br><br>* You can call the [DescribeEipAddress](https://docs.byteplus.com/en/docs/eip/DescribeEipAddresses) API to query the list of all EIP information, including available EIP IDs. |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample 1

Apply for a public address for the replica set instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "NetworkType": "Public",
    "InstanceId": "mongo-replica-617a883d****",
    "EipIds": [
        "eip-2d744t595x6o058ozfeht****",
        "eip-2byu2l2b27lz42dx0efko****"
    ]
}
```

## Response sample 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20220314172456010212194039160D****",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Request sample 2

Apply for a private address for a shard in a sharding cluster instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ObjectId": "mongo-shard-9a554522****-s0",
    "NetworkType": "Private",
    "InstanceId": "mongo-shard-9a554522****"
}
```

## Response sample 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20220314172456010212194039160D****",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Request sample 3

Apply for a public address for a ConfigServer in a sharding cluster instance.

> **说明**

> Before applying for a public address for a ConfigServer or shard, you must apply for a private address for the corresponding component.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ObjectId": "mongo-shard-9a554522****-config",
    "NetworkType": "Public",
    "InstanceId": "mongo-shard-9a554522****",
    "EipIds": [
        "eip-2d744t595x6o058ozfeht****",
        "eip-2byu2l2b27lz42dx0efk****"
    ]
}
```

## Response sample 3

```json
{
    "ResponseMetadata": {
        "RequestId": "20220314172456010212194039160D****",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Request sample 4

Apply for a public address for a Mongos node in a sharding cluster instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=CreateDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "ObjectId": "mongo-shard-9a554522****",
    "NetworkType": "Public",
    "InstanceId": "mongo-shard-9a554522****",
    "MongosNodeIds": [
        "mongo-shard-9a554522****-0"
    ],
    "EipIds": [
        "eip-2d744t595x6o058ozfeht****"
    ]
}
```

## Response sample 4

```json
{
    "ResponseMetadata": {
        "RequestId": "20220314172456010212194039160D****",
        "Action": "CreateDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
