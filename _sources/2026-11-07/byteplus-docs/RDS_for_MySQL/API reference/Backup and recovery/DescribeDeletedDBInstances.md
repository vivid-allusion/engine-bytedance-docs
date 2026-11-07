---
title: "DescribeDeletedDBInstances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedeleteddbinstances"
---

Call the DescribeDeletedDBInstances API to query the list of deleted instances.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PageNumber |Integer |No |1 |Current page number. Minimum value is 1. Default value is 1. |
|PageSize |Integer |No |10 |Number of records per page. Minimum value is 1, maximum value does not exceed 100. Default value is 10. |
|InstanceId |String |No |mysql\-ce1fee06\*\*\*\* |Instance ID.<br><br>tip<br><br><br>* When this parameter is specified, the backup information of the specified deleted instance is returned.<br><br>* When not specified, all results meeting the query conditions are returned. |
|InstanceName |String |No |Test Instance |Instance name. Supports fuzzy matching. |
|ProjectName |String |No |default |Project name. Supports querying by project. |
|DeletionAfterTime |String |No |2024\-10\-14T23:35:08.000Z |The start time of the query time range. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br>tip<br><br>The end time should be later than the start time (DeletionAfterTime). |
|DeletionBeforeTime |String |No |2024\-10\-15T08:39:28.000Z |The end time of the query time range. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br>tip<br><br>The start time should be earlier than the end time (DeletionAfterTime). |
|InstanceStatus |String |No |Recycled |Instance status, possible values:<br><br><br>* `Released`: Releasing.<br><br>* `Recycled`: Recycled. |

## Response parameters

null

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |324 |Total number of results matching the query conditions. |
|Datas |Object[] |Please refer to the response example. |List of deleted instances matching the query conditions. |
|BackupExpirationTime |String |2024\-10\-21T23:53:52.000Z |Backup set expiration release time.<br><br>tip<br><br>BackupExpirationTime = DeletionTime + DataKeepDays |
|CreateTime |String |2024\-10\-14T23:28:44.000Z |Instance creation time. Format: yyyy\-MM\-ddTHH:mm:ss.sssZ (UTC time). |
|DBEngineVersion |String |MySQL_8_0 |Compatible version. Valid values:<br><br><br>* `MySQL_5_7`: MySQL 5.7 version.<br><br>* `MySQL_8_0`: MySQL 8.0 version. |
|DataKeepDays |Integer |7 |Backup retention period in days. |
|DataKeepPolicy |String |Last |Whether to retain snapshots on the instance after release. Valid value: `Last`, retaining the last one. |
|DeletionTime |String |2024\-10\-14T23:53:52.000Z |Instance deletion time. |
|InstanceId |String |mysql\-ce1fee06\*\*\*\* |Instance ID. |
|InstanceName |String |Test instance |Instance name. |
|InstanceStatus |String |Recycled |Instance status. Valid values:<br><br><br>* `Released`: Being recycled.<br><br>* `Recycled`: Already recycled. |
|InstanceType |String |DoubleNode |Instance type. Valid values:<br><br><br>* `DoubleNode`: Dual\-node type.<br><br>* `MultiNode`: Multi\-node type. |
|NodeSpec |String |rds.mysql.2c4g |Instance specification. |
|ProjectName |String |default |The project to which the instance belongs. |
|StorageSpace |Integer |20 |Total storage space of the instance. Unit: GiB. |
|StorageType |String |LocalSSD |The storage type of the instance. Value range:<br><br><br>* `LocalSSD`: Local disk.<br><br>* `CloudESSD_FlexPL`: FlexPL cloud disk.<br><br>* `CloudESSD_PL0`: PL0 cloud disk. |

## Sample request

```json
POST /?Action=DescribeDeletedDBInstances&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241015165431BE09E69B68DE499597A6-17c86e",
        "Action": "DescribeDeletedDBInstances",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "Datas": [
            {
                "BackupExpirationTime": "2024-10-22T08:39:28.000Z",
                "CreateTime": "2024-07-02T08:13:06.000Z",
                "DBEngineVersion": "MySQL_5_7",
                "DataKeepDays": 7,
                "DataKeepPolicy": "Last",
                "DeletionTime": "2024-10-15T08:39:28.000Z",
                "InstanceId": "mysql-886aaa00****",
                "InstanceName": "测试实例1",
                "InstanceStatus": "Released",
                "InstanceType": "HA",
                "NodeNumber": 0,
                "NodeSpec": "rds.mysql.4c32g",
                "ProjectName": "default",
                "StorageSpace": 200,
                "StorageType": "LocalSSD"
            },
            {
                "BackupExpirationTime": "2024-10-22T08:34:07.000Z",
                "CreateTime": "2024-10-07T02:51:56.000Z",
                "DBEngineVersion": "MySQL_8_0",
                "DataKeepDays": 7,
                "DataKeepPolicy": "Last",
                "DeletionTime": "2024-10-15T08:34:07.000Z",
                "InstanceId": "mysql-80214d72****",
                "InstanceName": "测试实例2",
                "InstanceStatus": "Released",
                "InstanceType": "MultiNode",
                "NodeNumber": 0,
                "NodeSpec": "rds.mysql.1c2g",
                "ProjectName": "default",
                "StorageSpace": 20,
                "StorageType": "LocalSSD"
            },
            {
                "BackupExpirationTime": "2024-10-22T08:37:52.000Z",
                "CreateTime": "2024-10-11T05:50:46.000Z",
                "DBEngineVersion": "MySQL_8_0",
                "DataKeepDays": 7,
                "DataKeepPolicy": "Last",
                "DeletionTime": "2024-10-15T08:37:52.000Z",
                "InstanceId": "mysql-c9cd2846****",
                "InstanceName": "测试实例3",
                "InstanceStatus": "Released",
                "InstanceType": "HA",
                "NodeNumber": 0,
                "NodeSpec": "rds.mysql.1c2g",
                "ProjectName": "default",
                "StorageSpace": 100,
                "StorageType": "LocalSSD"
            },
            {
                "BackupExpirationTime": "2024-10-21T23:37:19.000Z",
                "CreateTime": "2024-10-14T23:16:31.000Z",
                "DBEngineVersion": "MySQL_8_0",
                "DataKeepDays": 7,
                "DataKeepPolicy": "Last",
                "DeletionTime": "2024-10-14T23:37:19.000Z",
                "InstanceId": "mysql-b6d44cb6****",
                "InstanceName": "测试实例4",
                "InstanceStatus": "Recycled",
                "InstanceType": "HA",
                "NodeNumber": 0,
                "NodeSpec": "rds.mysql.2c4g",
                "ProjectName": "default",
                "StorageSpace": 50,
                "StorageType": "LocalSSD"
            },
            {
                "BackupExpirationTime": "2024-10-21T23:49:27.000Z",
                "CreateTime": "2024-10-14T23:28:20.000Z",
                "DBEngineVersion": "MySQL_5_7",
                "DataKeepDays": 7,
                "DataKeepPolicy": "Last",
                "DeletionTime": "2024-10-14T23:49:27.000Z",
                "InstanceId": "mysql-eb6f7d9f****",
                "InstanceName": "测试实例5",
                "InstanceStatus": "Recycled",
                "InstanceType": "MultiNode",
                "NodeNumber": 0,
                "NodeSpec": "rds.mysql.2c4g",
                "ProjectName": "default",
                "StorageSpace": 20,
                "StorageType": "LocalSSD"
            }
        ],
        "Total": 144
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
