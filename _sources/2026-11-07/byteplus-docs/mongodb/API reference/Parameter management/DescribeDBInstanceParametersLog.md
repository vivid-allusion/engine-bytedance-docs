---
title: "DescribeDBInstanceParametersLog"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameterslog"
---

Call the DescribeDBInstanceParametersLog API to query the parameter modification history of the target MongoDB instance within the specified time.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-a1f25ba5\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|StartTime |String |Yes |2022\-07\-18T21:05Z |The time when the query starts. The format is *yyyy\-MM\-dd*T*HH:mm*Z (UTC). |
|EndTime |String |Yes |2022\-07\-18T21:06Z |The time when the query ends. The format is *yyyy\-MM\-dd*T*HH:mm*Z (UTC).<br><br>tip<br><br>The query end time should be later than the query start time. |
|PageNumber |Integer |Yes |1 |This parameter modifies the page number of the historical information list. The value cannot exceed the max value for the integer data type, which starts from 1. |
|PageSize |Integer |Yes |10 |The number of records is 1 to 1000 on each page. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |1 |The total number of parameters that have been modified. |
|ParameterChangeLog |Object[] |Refer to Response example. |A list of information about the parameter modification history. |
|ModifyTime |String |2022\-07\-18 21:05:08 |The time (UTC) when the target parameter was modified. |
|NewParameterValue |String |600001 |Parameter value after modification. |
|OldParameterValue |String |600000 |Parameter value before modification. |
|ParameterName |String |cursorTimeoutMillis |The name of the target parameter. |
|ParameterRole |String |Node |The type of node to which the target parameter belongs, with the value range as below:<br><br><br>* `Node`： Replica set instance nodes.<br><br>* `Shard`： Shard nodes in a sharding cluster instance.<br><br>* `ConfigServer`： ConfigServer node in a sharding cluster instance.<br><br>* `Mongos`： Mongos nodes in a sharding cluster instance. |
|ParameterStatus |String |Applied |Whether the new parameter value is in effect. The value range is as follows:<br><br><br>* `Applied`： In effect.<br><br>* `Invalid`： Not in effect. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBInstanceParametersLog&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-55d59354****",
    "StartTime": "2022-07-18T21:05Z",
    "EndTime": "2022-07-18T21:06Z",
    "PageSize": 10,
    "PageNumber": 1
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022052716480301022508219902F0****",
        "Action": "DescribeDBInstanceParametersLog",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ParameterChangeLog": [
            {
                "ModifyTime": "2022-07-18 21:05:08",
                "NewParameterValue": "600001",
                "OldParameterValue": "600001",
                "ParameterName": "cursorTimeoutMillis",
                "ParameterRole": "Node",
                "ParameterStatus": "Applied"
            }
        ],
        "Total": 1
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
