---
title: "DescribeSlowLogs"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describeslowlogs"
---

Call the DescribeSlowLogs API to query the slow log information of the target MongoDB instance within the specified time.

## Request type

Synchronous request.

## Precautions

Currently, only the details of slow logs within the last 7 days can be viewed.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-46cb08bc\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|Limit |Long |Yes |10 |Number of records per page, with a value range of 1 to 1000. |
|Context |String |No |[1712731868000000,3559571755,2097165,null] |The slow log records the context of the query results and is used when more slow log records need to be loaded.<br><br>tip<br><br>After calling the DescribeSlowLogs API, you can determine whether there are unloaded slow log records according to the value of the returned parameter `ListOver`:<br><br><br>* If the value of `ListOver` is `false`, it means that there are still slow log records that meet the query criteria and have not been fully loaded. You can call the DescribeSlowLogs API again and use the `Context` value in the parameters returned by the previous API call to view the remaining slow log records.<br><br>* If the value of `ListOver` is `true`, it means that all slow log records that meet the query criteria have been fully loaded. |
|PodName |String |Yes |mongo\-replica\-46cb08bc\*\*\*\*\-1 |The node ID for querying log information.<br><br>tip<br><br>You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) API to obtain detailed information of a specified instance, including the node ID of each node in the instance. Among them:<br><br><br>* The `NodeId` in a replica set instance is the `PodName`.<br><br>* In a sharded cluster instance:<br><br>   * The `ConfigServersId` is the `PodName` of the ConfigServer node.<br><br>   * The `MongosNodeId` is the `PodName` of the Mongos node.<br><br>   * The `NodeId` is the `PodName` of the Shard node. |
|Sort |String |No |DESC |Sort the query results in ascending or descending order according to the log generation time. The value range is as follows:<br><br><br>* `DESC` (default): Sort in descending order.<br><br>* `ASC`: Sort in ascending order. |
|DBName |String |No |testdb |The database where the slow log is located. |
|Keys |String |No |warning error |Search keywords are used to search for slow logs containing the keywords.<br><br>tip<br><br><br>* If no keywords are passed in, it means that the query results of slow logs are not filtered by keywords.<br><br>* Multiple keywords can be passed in for retrieval at the same time, and multiple keywords are separated by spaces, and the relationship between keywords is **OR**.<br><br>   For example, setting the search keyword `"Keys":"warning error"` means to search for logs containing the keyword `warning` or `error`.<br><br>* The log search statement supports a maximum of 4 KiB. In addition to the `Keys` parameter passing part in the search statement, there are some system preset fields. At the same time, to improve the search efficiency and accuracy, it is recommended not to pass in too many keywords.<br><br>* Passing in reserved keywords for retrieval is not supported. For more information about reserved keywords, please refer to [Reserved keywords for log search](https://docs.byteplus.com/en/docs/mongodb/log-overview#reserved-keywords-for-log-search). |
|QueryStartTime |String |No |2025\-01\-02T07:33:00Z |Query start time, with the format of `yyyy-MM-ddTHH:mmZ` (UTC).<br><br>tip<br><br>If this parameter is left blank, the actual query start time defaults to the time 1 hour before the current time (UTC).<br><br>For example, if the current time is 08:30:00 on June 25, 2024 (UTC), and `QueryStartTime` is not filled in, then the actual query start time is `2024-06-25T07:30:00Z`. |
|QueryEndTime |String |No |2025\-01\-02T07:33:10Z |Query end time, with the format of `yyyy-MM-ddTHH:mmZ` (UTC).<br><br>tip<br><br><br>* If this parameter is left blank, the actual query end time defaults to the current time (UTC).<br><br>* The query end time needs to be later than the query start time. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |1 |Total number of query result entries. |
|Datas |Object[] | |Details of the slow log list that meet the query conditions. |
|SQL |String |Refer to the response example. |Slow query statement. |
|DBName |String |doctest |Database name. |
|Return |Long |2 |Number of returned rows. |
|ClientIP |String |127.0.\*\*\*.\*\*\* |The client address that sends the slow query request. |
|Duration |Long |108 |The execution duration of the slow query statement, in milliseconds (ms). |
|FileScan |Long |10 |The number of document lines scanned. |
|UserName |String |doctest@admin |Username. |
|IndexScan |Long |5 |The number of index lines scanned. |
|StartTime |String |2025\-06\-13T10:55:00.254 |The execution start time of the current slow log, in the format of `yyyy-MM-ddTHH:mm:ss.SSS` (UTC). |
|Context |String |[1712731868000000,3559571755,2097165,null] |Slow log records the context of the query results and is used when more slow log records need to be loaded. |
|ListOver |Boolean |true |Whether all the slow log content has been loaded. The value range is as follows:<br><br><br>* `true`: All have been loaded.<br><br>* `false`: Not all have been loaded.<br><br><br>tip<br><br>If `ListOver` returns `false`, you can call DescribeSlowLogs API again and pass in the value returned by `Context` in the request parameters to query the details of the slow logs that have not been loaded. |

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeSlowLogs&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "Limit": 10,
    "QueryStartTime": "2025-01-02T07:33:00Z",
    "QueryEndTime": "2025-01-02T07:33:10Z",
    "Sort": "ASC",
    "InstanceId": "mongo-replica-e405f8e2****",
    "PodName": "mongo-replica-e405f8e2****-1",
    "Context": "[1712731868000000,3559571755,2097165,null]"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104202D3110023228002****",
        "Action": "DescribeSlowLogs",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Total": 1,
        "Datas": [
            {
                "DBName": "test528683",
                "UserName": "root@admin",
                "SQL": "{ \t\"op\": \"select\", \t\"ns\": \"test528683.test528683\", \t\"command\": { **** \t}, \t\"user\": \"root@admin\" }",
                "StartTime": "2025-01-02T07:33:07.358",
                "Duration": 108,
                "ClientIP": "127.0.***.***",
                "FileScan": 10,
                "Return": 2,
                "IndexScan": 5
            }
        ],
        "Context": "[1712731868000000,3559571755,2097165,null]",
        "ListOver": true
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
