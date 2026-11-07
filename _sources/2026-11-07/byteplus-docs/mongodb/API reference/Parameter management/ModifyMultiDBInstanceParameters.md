---
title: "ModifyMultiDBInstanceParameters"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifymultidbinstanceparameters"
---

Call the ModifyMultiDBInstanceParameters API to modify multiple parameters in the target MongoDB instance.

## Request type

Async request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-shard\-9a554522\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|ParameterObjects |Object[] |Yes | |List of parameters to be modified.<br><br>tip<br><br>If multiple parameters need to be modified, it is necessary to ensure that the values of `ParameterRole` for multiple parameters are all the same. |
|ParameterName |String |Yes |cursorTimeoutMillis |The name of the target parameter.<br><br>tip<br><br>You can call the [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) API to query the details of the parameters supported by the target instance, including the parameter names. |
|ParameterRole |String |Yes |Node |The node type to which the target parameter belongs, and the value range is as follows:<br><br><br>* `Node`: Replica set instance node.<br><br>* `Shard`: Shard node in a sharding cluster instance.<br><br>* `ConfigServer`: ConfigServer node in a sharding cluster instance.<br><br>* `Mongos`: Mongos node in a sharding cluster instance.<br><br><br>tip<br><br>You can call the [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) API to query the details of the parameters supported by the target instance, including the node type to which the parameter belongs. |
|ParameterValue |String |Yes |600001 |The value of the target parameter.<br><br>tip<br><br>You can call the [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) API to query the details of the parameters supported by the target instance, including the value range of the target parameter (that is, the value of `CheckingCode`). |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request 1

Modify the values of `cursorTimeoutMillis` and `journalCommitInterval` parameters of the replica set instance simultaneously.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyMultiDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-replica-8d67f589****",
    "ParameterObjects": [
        {
            "ParameterName": "cursorTimeoutMillis",
            "ParameterValue": "600001",
            "ParameterRole": "Node"
        },
        {
            "ParameterName": "disableJavaScriptJIT",
            "ParameterValue": "false",
            "ParameterRole": "Node"
        }
    ]
}
```

## Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "ModifyMultiDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Sample request 2

Modify the values of the `wiredTigerConcurrentWriteTransactions` and `net.maxIncomingConnections` parameters in the Shard of the sharding cluster instance simultaneously.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyMultiDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-shard-9a554522****",
    "ParameterObjects": [
        {
            "ParameterName": "net.maxIncomingConnections",
            "ParameterValue": "Default",
            "ParameterRole": "Shard"
        },
        {
            "ParameterName": "wiredTigerConcurrentWriteTransactions",
            "ParameterValue": "120",
            "ParameterRole": "Shard"
        }
    ]
}
```

## Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "ModifyMultiDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
