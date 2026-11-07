---
title: "DescribeDBInstanceParameters"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters"
---

Call the DescribeDBInstanceParameters API to query the list of parameters supported by the target MongoDB instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-55d59354\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|ParameterRole |String |No |Node |The node type to which the target parameter belongs, and the value range is as follows:<br><br><br>* `Node`: The replica set instance node.<br><br>* `Shard`: The Shard node in the sharding cluster instance.<br><br>* `ConfigServer`: The ConfigServer node in the sharding cluster instance.<br><br>* `Mongos`: The Mongos node in the sharding cluster instance.<br><br><br>tip<br><br><br>* When the `InstanceId` passed in is the replica set instance ID, the `ParameterRole` can be left blank or set to `Node`.<br><br>* When the `InstanceId` passed in is the sharded cluster instance ID, if the `ParameterRole` is not filled in, the parameters of all types of nodes in the sharded cluster will be returned by default. |
|ParameterNames |String |No |connPoolMaxConnsPerHost |The name of the parameter to query.<br><br>tip<br><br><br>* Fuzzy query is supported (case insensitive). For example, you can input `pool` to query the details about the parameters whose names contain `pool`.<br><br>* If this parameter is left blank, the details about all the parameters in the current instance are queried by default. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|InstanceId |String |mongo\-replica\-55d59354\*\*\*\* |Instance ID. |
|DBEngine |String |MongoDB |Database engine. The value is always set to `MongoDB`. |
|DBEngineVersion |String |MongoDB_5_0 |Database engine version. |
|Total |String |1 |The number of parameters that meet the query requirements. |
|InstanceParameters |Object[] | |Details list of all parameters that meet the query requirements. |
|ForceModify |Boolean |true |Whether the value of the target parameter can be modified. The value range is as follows:<br><br><br>* `true`: Supports modification.<br><br>* `false`: Does not support modification. |
|CheckingCode |String |200 \- 2000 |The value range of the parameter. |
|ForceRestart |Boolean |true |After modification, does the new parameter value need to restart the instance to take effect. The value range is as follows:<br><br><br>* `true`: Need to restart.<br><br>* `false`: Do not need to restart. |
|ParameterRole |String |Node |The node types to which the target parameter belongs, and the value range is as follows:<br><br><br>* `Node`: The replica set instance node.<br><br>* `Shard`: The Shard node in the sharding cluster instance.<br><br>* `ConfigServer`: The ConfigServer node in the sharding cluster instance.<br><br>* `Mongos`: The Mongos node in the sharding cluster instance. |
|ParameterType |String |Integer |The data type of the parameter value, and the value range is as follows:<br><br><br>* `Integer`: Integer type.<br><br>* `String`: String type.<br><br>* `Boolean`: Boolean type. |
|ParameterNames |String |connPoolMaxConnsPerHost |Parameter name. |
|ParameterValue |String |1 |The current value of the target parameter. |
|ParameterDescription |String |Indicates the max connections in the connection pool for the current instance used to communicate with other mongod instances. |Parameter description. |
|ParameterDefaultValue |String |600 |The default value of the target parameter. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-55d59354****",
    "ParameterNames": "connPoolMaxConnsPerHost"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "DescribeDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "DBEngine": "MongoDB",
        "DBEngineVersion": "MongoDB_4_0",
        "InstanceId": "mongo-replica-55d59354****",
        "InstanceParameters": [
            {
                "CheckingCode": "200 - 2000",
                "ForceModify": true,
                "ForceRestart": true,
                "ParameterDefaultValue": "600",
                "ParameterDescription": "Indicates the max connections in the connection pool for the current instance used to communicate with other mongod instances",
                "ParameterNames": "connPoolMaxConnsPerHost",
                "ParameterRole": "Node",
                "ParameterType": "Integer",
                "ParameterValue": "601"
            }
        ],
        "Total": "1"
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
