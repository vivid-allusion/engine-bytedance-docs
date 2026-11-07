---
title: "ModifyDBInstanceParameters"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbinstanceparameters"
---

Call the ModifyDBInstanceParameters API to modify the specified parameters of the target MongoDB instance.

## Request type

Asynchronous request.

## Precautions

After some parameter values are modified, the instance needs to be restarted to take effect. The restart of the instance will cause a connection interruption. It is recommended to modify the relevant parameters during the off\-peak period of the business and ensure that the business has a reconnection mechanism.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-9a554522\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|ParametersObject |Object |Yes | |Details of the parameters that need to be modified. |
|ParameterName |String |Yes |cursorTimeoutMillis |The name of the target parameter.<br><br>tip<br><br>You can call the [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) API to query the details of the parameters supported by the target instance, including the parameter names. |
|ParameterRole |String |Yes |Node |The node type to which the target parameter belongs, and the value range is as follows:<br><br><br>* `Node`: Replica set instance node.<br><br>* `Shard`: Shard node in a sharding cluster instance.<br><br>* `ConfigServer`: ConfigServer node in a sharding cluster instance.<br><br>* `Mongos`: Mongos node in a sharding cluster instance.<br><br><br>tip<br><br>You can call the [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) API to query the details of the parameters supported by the target instance, including the node type to which the parameter belongs. |
|ParameterValue |String |Yes |600001 |The value of the target parameter.<br><br>tip<br><br>You can call the [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) API to query the details of the parameters supported by the target instance, including the value range of the target parameter (that is, the value of `CheckingCode`). |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mongo\-replica\-55d59354\*\*\*\* |Instance ID. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-55d59354****",
    "ParametersObject": {
        "ParameterName": "cursorTimeoutMillis",
        "ParameterRole": "Node",
        "ParameterValue": "600001"
    }
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022052716480301022508219902F0****",
        "Action": "ModifyDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "mongo-replica-55d59354****"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
