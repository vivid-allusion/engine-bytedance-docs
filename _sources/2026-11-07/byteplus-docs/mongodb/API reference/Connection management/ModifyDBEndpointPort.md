---
title: "ModifyDBEndpointPort"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbendpointport"
---

Call the ModifyDBEndpointPort API to modify port number of connection address corresponding to target MongoDB instance.

## Request type

Asynchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) interface to query the basic information of all MongoDB instances in the target Region, including instance ID. |
|Port |String |Yes |1000 |The modified port number of the link address, with a value range of 1000 to 65535.<br><br>warning<br><br><br>* Currently, only the port number of the connection address of replica set instances and the Mongos nodes in and sharding cluster instances can be modified. The effective scopes of new ports vary depending on the instance or component type. For the specific effective range, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports).<br><br>* Modifying the port number will cause the access of some services to be affected in a short time. Please operate with caution.<br><br>* After modifying the port number, the original connection will be disconnected. Please modify the connection information of the client in a timely manner. For the specific operation steps of connecting an instance, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell). |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Request sample 1

Change the port number corresponding to the connection address in the replica set instance to 1000.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBEndpointPort&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-replica-e405f8e2****",
    "Port": "1000"
}
```

## Response sample 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "ModifyDBEndpointPort",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Request sample 2

Change the port number of the connection address corresponding to the Mongos node in the sharding cluster instance to 1001.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBEndpointPort&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-shard-011d2479****",
    "Port": "1001"
}
```

## Response sample 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "ModifyDBEndpointPort",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
