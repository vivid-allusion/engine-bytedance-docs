---
title: "DeleteDBEndpoint"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/deletedbendpoint"
---

Call the DeleteDBEndpoint API to delete the specified address in the target MongoDB instance.

## Request type

Asynchronous request.

## Precautions

* After the private address is successfully released, the addresses of all nodes (including 3 nodes by default) in the Shard or ConfigServer will be released, and you cannot continue to connect to the node through this address. Please operate with caution.

* Different types of MongoDB instances support different types of addresses for application or release. For more information, refer to [Address types](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction#.6L-e5o6l5Zyw5Z2A57G75Z6L).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-011d2479\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|EndpointId |String |Yes |V0tAA0hFUENIV00SSg\*\*\*\* |Address ID.<br><br>tip<br><br><br>* You can call the [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) API to query the address information under the target instance, including the address ID.<br><br>* Only the addresses of the shard or ConfigServer nodes in the MongoDB sharding cluster instance can be released. The private addresses of the Mongos nodes in the replica set instance or the sharding cluster instance is provided by default and cannot be released. |
|MongosNodeIds |String[] |No |["mongo\-shard\-9a554522\*\*\*\*\-0","mongo\-shard\-9a554522\*\*\*\*\-1"] |ID of the Mongos node of the public address you want to release.<br><br>tip<br><br><br>* This parameter is required only when you release the public address of a Mongos node under a sharding cluster instance.<br><br>* You can release the public addresses of multiple Mongos nodes at the same time, which are separated by commas (,).<br><br>* You can call the [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) API to query the connection information about all the Mongos nodes under the sharding cluster instance of the target instance, including the IDs of Mongos nodes. |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample 1

Releases the public address of the replica set instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DeleteDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-617a883d****",
    "EndpointId": "UUtGBkJJVB5EBE****"
}
```

## Response sample 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202203141832270102120352320B0D****",
        "Action": "DeleteDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Request sample 2

Release the private address of a ConfigServer node or a shard in the sharding cluster instance.

> **说明**

> You need to release the public address before the private address for a node.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DeleteDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-9a554522****",
    "EndpointId": "XhtEUk5EVUhEVkNCSg****"
}
```

## Response sample 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202203141832270102120352320B0D****",
        "Action": "DeleteDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Request sample 3

Release the public addresses of the two Mongos nodes in the sharding cluster instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DeleteDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-shard-9a554522****",
    "EndpointId": "XhtEUk5EVUhEVk****",
    "MongosNodeIds": [
        "mongo-shard-9a554522****-0",
        "mongo-shard-9a554522****-1"
    ]
}
```

## Response sample 3

```json
{
    "ResponseMetadata": {
        "RequestId": "202203141832270102120352320B0D****",
        "Action": "DeleteDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
