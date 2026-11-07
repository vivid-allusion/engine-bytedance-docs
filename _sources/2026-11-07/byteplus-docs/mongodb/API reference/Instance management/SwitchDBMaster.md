---
title: "SwitchDBMaster"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/switchdbmaster"
---

Call the SwitchDBMaster API to manually switch the primary and secondary nodes of the specified instance.

## Request type

Asynchronous request.

## Precautions

* The status of the instance is **Running** (i.e., `InstanceStatus` is `Running`). For more information on instance states, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* The node to be manually switched is a **secondary node** of an instance or a component of any of the following types:

   * Replica set instance

   * Shard in a sharding cluster instance

   * ConfigServer component in a sharding cluster instance

* Generally, manual switching of the primary node takes 30 seconds to 60 seconds, during which the instance may experience one or two temporary disconnections. Be cautious with this operation. We recommend you perform switching during off\-peak hours and ensure that applications have an automatic reconnection mechanism.

* Manual switching of the primary node only changes the node role, but not the availability zone and ID of the node.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-011d2479\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|NodeId |String |Yes |mongo\-shard\-100b2c546f14\-s0\-1 |ID of the secondary node on which the primary/secondary switchover is to be performed.<br><br>tip<br><br>The ID of secondary node (i.e., the `NodeRole` is `Secondary`). Hidden nodes (i.e., the `NodeRole` is `Hidden`) cannot be switched to primary nodes. You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) API to query the information about all nodes under the sharding cluster instance of the target instance, including node roles. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request 1

Manually switch the roles of the primary and secondary nodes of the replica set instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=SwitchDBMaster&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK*/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=*
{
    "InstanceId": "mongo-replica-c81b6e56****",
    "NodeId": "mongo-replica-c81b6e56****-1"
}
```

## Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202305161612331350F38EC0C05BC2****",
        "Action": "SwitchDBMaster",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Sample request 2

Manually switch the roles of the primary and secondary nodes of a shard in a sharding cluster instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=SwitchDBMaster&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK*/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=*
{
    "InstanceId": "mongo-shard-100b2c54****",
    "NodeId": "mongo-shard-100b2c54****-s0-1"
}
```

## Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202305161612331350F38EC0C05BC2****",
        "Action": "SwitchDBMaster",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Sample request 3

Manually switch the roles of the primary and secondary nodes of a ConfigServer node in a sharding cluster instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=SwitchDBMaster&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK*/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=*
{
    "InstanceId": "mongo-shard-100b2c54****",
    "NodeId": "mongo-shard-100b2c54****-config-0"
}
```

## Sample response 3

```json
{
    "ResponseMetadata": {
        "RequestId": "202305161612331350F38EC0C05BC2****",
        "Action": "SwitchDBMaster",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
