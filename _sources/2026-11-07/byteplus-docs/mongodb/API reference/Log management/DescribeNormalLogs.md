---
title: "DescribeNormalLogs"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describenormallogs"
---

Call the DescribeNormalLogs API to query the running log or error log information of the target MongoDB instance within the specified time period.

## Request type

Synchronous request.

## Precautions

* Currently, only the details of operation logs or error logs within the last 7 days can be viewed.

* DescribeNormalLogs is a streaming API that supports the pagination query mechanism. If there are many log records in your instance, you usually need to call this API multiple times to obtain complete logs.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |
|Limit |Long |Yes |10 |Number of records per page, with a value range of 1 to 1000. |
|Context |String |No |0,1749808482010,210209079374,618991 |The pagination query credential for the query result of log records, which is used to mark the pagination position.<br><br>tip<br><br><br>* DescribeNormalLogs is a streaming API that supports the pagination query mechanism. If there are many log records in your Instance, usually you need to call this API multiple times to obtain the complete logs.<br><br>* You can determine whether there are unloaded log records according to the value of the return parameter `ListOver`, and obtain them in segments in combination with the `Context` pagination query credential:<br><br>   * If the value of `ListOver` is `false`, it means that there are still log records that meet the query conditions that have not been loaded completely. You can call the DescribeNormalLogs API again and use the pagination position marked by `Context` in the return parameters of the previous API call to query the remaining log records backwards.<br><br>   * If the value of `ListOver` is `true`, it means that all log records that meet the query conditions have been completely loaded. |
|PodName |String |Yes |mongo\-replica\-e405f8e2\*\*\*\*\-0 |The node ID for querying log information.<br><br>tip<br><br>You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) API to obtain detailed information of a specified instance, including the node ID of each node in the instance. Among them:<br><br><br>* The `NodeId` in a replica set instance is the `PodName`.<br><br>* In a sharded cluster instance:<br><br>   * The `ConfigServersId` is the `PodName` of the ConfigServer node.<br><br>   * The `MongosNodeId` is the `PodName` of the Mongos node.<br><br>   * The `NodeId` is the `PodName` of the Shard node. |
|Sort |String |No |DESC |Sort the query results in ascending or descending order according to the log generation time. The value range is as follows:<br><br><br>* `DESC` (default): Sort in descending order.<br><br>* `ASC`: Sort in ascending order. |
|LogLevel |String |No |RunningLog |The log level to be queried. The value range is as follows:<br><br><br>* `ErrorLog` (default): Error log.<br><br>* `RunningLog`: Running log. |
|Keys |String |No |warning error |Retrieve keywords for retrieving operation logs or error logs that contain the keywords.<br><br>tip<br><br><br>* If no keyword is passed in, it means that the log query results are not filtered by keywords.<br><br>* It supports passing in multiple keywords for retrieval at the same time. Multiple keywords are separated by spaces, and the relationship between the keywords is **or**.<br><br><br>For example, setting the retrieval keyword `"Keys":"warning error"` means retrieving logs that contain the keyword `warning` or `error`.<br><br><br>* The log retrieval statement supports a maximum length of 4 KiB. In addition to the `Keys` parameter part, there are also some system preset fields in the retrieval statement. At the same time, to improve retrieval efficiency and accuracy, it is recommended not to pass in too many keywords.<br><br>* It does not support passing in reserved keywords for retrieval. For more information about reserved keywords, refer to [Reserved keywords for log search](https://docs.byteplus.com/en/docs/56/..../mongodb/log-overview#reserved-keywords-for-log-search). |
|QueryStartTime |String |No |2025\-06\-12T08:30:00Z |Query start time, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>tip<br><br>If this parameter is left blank, the actual query start time defaults to the time 1 hour before the current time (UTC).<br><br>For example, if the current time is 08:30:00 on June 25, 2024 (UTC), and `QueryStartTime` is not filled, then the actual query start time is `2024-06-25T07:30:00Z`. |
|QueryEndTime |String |No |2025\-06\-13T08:30:00Z |Query end time, with the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>tip<br><br><br>* If this parameter is left blank, the actual query end time will be defaulted to the current time (UTC).<br><br>* The query end time should be later than the query start time. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |10 |Total number of query result entries. |
|Datas |Object[] | |Details of the log list that meets the query criteria. |
|LogType |String |NETWORK |The current log record's log type. |
|Message |String |end connection 172.30. ** *.* ** :37948 (14 connections now open) |The detailed information of the currently logged logs. |
|Connection |String |conn171 |The currently logged connection information. |
|CreateTime |String |2025\-06\-13T09:54:44Z |The generation time of the current log record, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|Context |String |0,1749808482010,210209079374,618991 |The pagination query credential for the query result of the log record, which is used to mark the pagination position. |
|ListOver |Boolean |false |Whether the log content has been fully loaded. The value range is as follows:<br><br><br>* `true`: It has been fully loaded.<br><br>* `false`: It has not been fully loaded.<br><br><br>tip<br><br>If `ListOver` returns `false`, you can call DescribeNormalLogs again and pass in the pagination position marked by `Context` in the request parameters to query the details of the logs that have not been loaded. |

## Sample request 1

For the first time, query the details of the running logs (`RunningLog`) through the DescribeNormalLogs API, and return 10 records per page.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeNormalLogs&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "Limit": 10,
    "InstanceId": "mongo-replica-e405f8e2****",
    "PodName": "mongo-replica-e405f8e2****-0",
    "QueryStartTime": "2025-06-12T09:54:45Z",
    "QueryEndTime": "2025-06-13T09:54:45Z",
    "Sort": "DESC",
    "LogLevel": "RunningLog"
}
```

## Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "DescribeNormalLogs",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Context": "0,1749808482010,210209079374,618991",
        "Datas": [
            {
                "Connection": "conn171",
                "CreateTime": "2025-06-13T09:54:44Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.30.***.***:37948 (14 connections now open)"
            },
            {
                "Connection": "conn170",
                "CreateTime": "2025-06-13T09:54:44Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.30.***.***:37940 (15 connections now open)"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:44Z",
                "LogType": "NETWORK",
                "Message": "start control connection, connectionCount is 16"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:44Z",
                "LogType": "NETWORK",
                "Message": "connection accepted from 172.30.***.***:37948 #171 (16 connections now open)"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:44Z",
                "LogType": "NETWORK",
                "Message": "start control connection, connectionCount is 15"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:44Z",
                "LogType": "NETWORK",
                "Message": "connection accepted from 172.30.***.***:37940 #170 (15 connections now open)"
            },
            {
                "Connection": "conn169",
                "CreateTime": "2025-06-13T09:54:42Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.30.***.***:37694 (14 connections now open)"
            },
            {
                "Connection": "conn168",
                "CreateTime": "2025-06-13T09:54:42Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.30.***.***:37688 (15 connections now open)"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:42Z",
                "LogType": "NETWORK",
                "Message": "start control connection, connectionCount is 16"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:42Z",
                "LogType": "NETWORK",
                "Message": "connection accepted from 172.30.***.***:37694 #169 (16 connections now open)"
            }
        ],
        "ListOver": false,
        "Total": 10
    }
}
```

## Sample request 2

The details of the running logs (`RunningLog`) have been queried through the DescribeNormalLogs API. However, not all query results have been loaded (i.e., `ListOver` in the API response is `false`). You can use the pagination identifier in the previous response (i.e., the value of `Context` in the response, which is `0,1749808482010,210209079374,618991` in this example) to call the API again to query the remaining log details. The number of records per page is 10.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeNormalLogs&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "Limit": 10,
    "InstanceId": "mongo-replica-23fc14ec****",
    "PodName": "mongo-replica-23fc14ece7ce-0",
    "Context": "0,1749808482010,210209079374,618991",
    "QueryStartTime": "2025-06-12T09:54:45Z",
    "QueryEndTime": "2025-06-13T09:54:45Z",
    "Sort": "DESC",
    "LogLevel": "RunningLog"
}
```

## Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "DescribeNormalLogs",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Context": "0,1749808479728,210209079360,618991",
        "Datas": [
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:42Z",
                "LogType": "NETWORK",
                "Message": "start control connection, connectionCount is 15"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:42Z",
                "LogType": "NETWORK",
                "Message": "connection accepted from 172.30.***.***:37688 #168 (15 connections now open)"
            },
            {
                "Connection": "conn166",
                "CreateTime": "2025-06-13T09:54:40Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.18.***.***:59318 (14 connections now open)"
            },
            {
                "Connection": "conn167",
                "CreateTime": "2025-06-13T09:54:40Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.18.***.***:59338 (15 connections now open)"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:40Z",
                "LogType": "NETWORK",
                "Message": "start control connection, connectionCount is 16"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:40Z",
                "LogType": "NETWORK",
                "Message": "connection accepted from 172.18.***.***:59338 #167 (16 connections now open)"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:40Z",
                "LogType": "NETWORK",
                "Message": "start control connection, connectionCount is 15"
            },
            {
                "Connection": "listener",
                "CreateTime": "2025-06-13T09:54:40Z",
                "LogType": "NETWORK",
                "Message": "connection accepted from 172.18.***.***:59318 #166 (15 connections now open)"
            },
            {
                "Connection": "conn164",
                "CreateTime": "2025-06-13T09:54:39Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.18.***.***:58870 (15 connections now open)"
            },
            {
                "Connection": "conn165",
                "CreateTime": "2025-06-13T09:54:39Z",
                "LogType": "NETWORK",
                "Message": "end connection 172.18.***.***:59030 (14 connections now open)"
            }
        ],
        "ListOver": false,
        "Total": 10
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
