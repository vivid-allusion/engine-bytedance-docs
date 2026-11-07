---
title: "DescribeTasks"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describetasks"
---

Call the DescribeTasks API to query tasks.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PageNumber |Integer |Yes |1 |The current page number. The minimum value is 1. The default value is 1. |
|PageSize |Integer |Yes |10 |The number of records per page. The minimum value is 1, and the maximum value cannot exceed 1000. The default value is 10. |
|InstanceId |String |No |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|CreationStartTime |String |No |2024\-01\-29T15:59:59Z |The start time of the task. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br><br>* Either the task time (CreationStartTime and CreationEndTime) or TaskId must be specified.<br><br>* The maximum time interval between the task start time (CreationStartTime) and task end time (CreationEndTime) cannot exceed 7 days. |
|CreationEndTime |String |No |2024\-01\-27T16:00:00Z |The end time of the task. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br><br>* Either the task time (CreationStartTime and CreationEndTime) or TaskId must be specified.<br><br>* The maximum time interval between the task start time (CreationStartTime) and task end time (CreationEndTime) cannot exceed 7 days. |
|TaskId |String |No |2024012922384660DE49D5E35F6015\*\*\*\*\-b248b3 |Task ID.<br><br>tip<br><br>Either TaskId or the task time (CreationStartTime and CreationEndTime) must be specified. |
|TaskAction |String |No |DeleteDatabase |Task name. |
|ProjectName |String |No |default |Project name. |
|TaskType |String |No |Web |Task type. Values:<br><br><br>* `Web`: Console request.<br><br>* `OpenAPI`: OpenAPI request.<br><br>* `AssumeRole`: Role\-playing request.<br><br>* `Other`: Other requests. |
|TaskSource |String |No |User |Task source. Values:<br><br><br>* `User`: Tenant.<br><br>* `System`: System.<br><br>* `SystemUser`: Internal operation and maintenance.<br><br>* `UserMaintain`: Maintenance operations initiated by the system/operation and maintenance administrator and visible to the tenant. |
|TaskStatus |String[] |No |["Running"] |Task status. The possible values are as follows (multiple selections allowed):<br><br><br>* `WaitSwitch`: Waiting for switchover<br><br>* `WaitStart`: Waiting to execute<br><br>* `Canceled`: Canceled<br><br>* `Stopped`: Stopped<br><br>* `Running_BeforeSwitch`: Running (before switchover)<br><br>* `Timeout`: Execution timeout<br><br>* `Success`: Execution succeeded<br><br>* `Failed`: Execution failed<br><br>* `Running`: Running<br><br>* `Stopping`: Stopping |
|TaskCategory |String[] |No |["BackupRecoveryManagement"] |Task category. The possible values are as follows (multiple selections allowed):<br><br><br>* `BackupRecoveryManagement`: Backup and recovery management.<br><br>* `DatabaseAdminManagement`: Database administration.<br><br>* `DatabaseProxy`: Database proxy.<br><br>* `HighAvailability`: High availability.<br><br>* `InstanceAttribute`: Instance attributes.<br><br>* `InstanceManagement`: Instance management.<br><br>* `NetworkManagement`: Network management.<br><br>* `SecurityManagement`: Security management.<br><br>* `SystemMaintainManagement`: System maintenance management.<br><br>* `VersionUpgrade`: Version upgrade. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |1 |Number of tasks. |
|Datas |Object[] |Refer to the response example. |Task information. |
|CostTimeMS |Long |3391 |Task duration in milliseconds. |
|CreateTime |String |2024\-01\-29T13:13:49.955Z |Task creation time. |
|FinishTime |String |2024\-01\-29T12:38:29.116Z |Task completion time. |
|Progress |Integer |45 |Task progress in percentage.<br><br>tip<br><br>Only tasks with a status of **Running**, i.e., tasks where TaskStatus is Running, will return the task progress. |
|RelatedInstanceInfos |Object |{<br><br>"InstanceID": "mysql\-5bde124c\*\*\*\*"<br><br>} |Task\-related instances. |
|InstanceID |String |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|ScheduledExecuteEndTime |String |2024\-12\-20T17:59:00Z |Planned start deadline in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>Only tasks in the "Waiting to start", "Waiting to execute", or "Waiting for switchover" status will return this field. |
|ScheduledExecuteStartTime |String |2024\-12\-20T16:00:00Z |Planned start time in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>Only tasks in the "Waiting to start", "Waiting to execute", or "Waiting for switchover" status will return this field. |
|ScheduledSwitchEndTime |String |2024\-12\-20T17:59:00Z |Planned switchover deadline in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>Only tasks in the "Waiting to start", "Waiting to execute", or "Waiting for switchover" status will return this field. |
|ScheduledSwitchStartTime |String |2024\-12\-20T16:00:00Z |Planned switchover start time in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>Only tasks in the "Waiting to start", "Waiting to execute", or "Waiting for switchover" status will return this field. |
|StartTime |String |2024\-01\-29T12:38:25.725Z |Task start time in the format `yyyy-MM-ddTHH:mm:ssZ`(UTC time). |
|TaskAction |String |CreateDBAccount |Task name. |
|TaskCategory |String |BackupRecoveryManagement |Task category, possible values:<br><br><br>* `BackupRecoveryManagement`: Backup and recovery management.<br><br>* `DatabaseAdminManagement`: Database administration management.<br><br>* `DatabaseProxy`: Database proxy.<br><br>* `HighAvailability`: High availability.<br><br>* `InstanceAttribute`: Instance attributes.<br><br>* `InstanceManagement`: Instance management.<br><br>* `MonitoringPerformance`: Monitoring and performance.<br><br>* `NetworkManagement`: Network management.<br><br>* `SecurityManagement`: Security management.<br><br>* `SystemMaintainManagement`: System maintenance management.<br><br>* `VersionUpgrade`: Version upgrade. |
|TaskDesc |String |This is a task description. |Task description. |
|TaskId |String |202401221959431F6913166F6F5A21\*\*\*\*\-682d5d |Task ID. |
|TaskParams |String | |Task parameters. |
|TaskSource |String |User |Source of the task. Values:<br><br><br>* `User`: Tenant.<br><br>* `System`: System.<br><br>* `SystemUser`: Internal operation and maintenance.<br><br>* `UserMaintain`: Maintenance operations initiated by the system/operation and maintenance administrator and visible to the tenant. |
|TaskStatus |String |Success |Task status, possible values:<br><br><br>* `WaitSwitch`: Waiting for switchover.<br><br>* `WaitStart`: Waiting to start.<br><br>* `Canceled`: Canceled.<br><br>* `Stopped`: Stopped.<br><br>* `Running_BeforeSwitch`: Running (before switchover).<br><br>* `Timeout`: Execution timeout.<br><br>* `Success`: Execution succeeded.<br><br>* `Failed`: Execution failed.<br><br>* `Running`: Running.<br><br>* `Stopping`: Stopping. |
|TaskProgress |Object[] |[<br><br>{<br><br>"Name": "InstanceInitialization",<br><br>"StepStatus": "Success"<br><br>},<br><br>{<br><br>"Name": "InstanceRecoveryPreparation",<br><br>"StepStatus": "Failed"<br><br>},<br><br>{<br><br>"Name": "DataBackupImport",<br><br>"StepStatus": "UnExecuted"<br><br>},<br><br>{<br><br>"Name": "LogBackupBinlogAdd",<br><br>"StepStatus": "UnExecuted"<br><br>},<br><br>{<br><br>"Name": "TaskSuccessful",<br><br>"StepStatus": "UnExecuted"<br><br>}<br><br>] |Progress details. |
|Name |String |InstanceInitialization |Step Name. Value:<br><br><br>* `InstanceInitialization`: Task initialization.<br><br>* `InstanceRecoveryPreparation`: Instance recovery preparation.<br><br>* `DataBackupImport`: Cold backup import.<br><br>* `LogBackupBinlogAdd`: Binlog replay.<br><br>* `TaskSuccessful`: Task succeeded. |
|StepStatus |String |Success |Status of the step. Values:<br><br><br>* `Running`: In progress.<br><br>* `Success`: Succeeded.<br><br>* `Failed`: Failed.<br><br>* `Unexecuted`: Not executed. |
|StepExtraInfo |Object[] |[<br><br>{<br><br>"Type": "CurDataSize",<br><br>"Unit": "Bytes",<br><br>"Value": 7579256<br><br>},<br><br>{<br><br>"Type": "RemainDataSize",<br><br>"Unit": "Bytes",<br><br>"Value": 0<br><br>}<br><br>] |The specific information of the steps. |
|Type |String |CurDataSize |Current stage<br><br><br>* `CostTime`: The time consumption of the current stage.<br><br>* `CurDataSize`: The amount of data imported currently.<br><br>* `CurBinlog`: The number of Binlog files being replayed currently.<br><br>* `RemainCostTime`: The remaining time consumption.<br><br>* `RemainDataSize`: The remaining amount of data to be imported.<br><br>* `RemainBinlog`: The remaining number of Binlog files to be replayed. |
|Unit |String |Bytes |Unit. Values:<br><br><br>* `MS`: milliseconds.<br><br>* `Bytes`: bytes.<br><br>* `Files`: number of (files). |
|Value |Double |7579256 |The specific value corresponding to the `Type`field. |

## Sample request 1

Query tasks created within a specified time period using CreationStartTime and CreationEndTime.

```json
POST /?Action=DescribeTasks&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "CreationEndTime": "2024-12-19T21:40:00Z",
    "CreationStartTime": "2024-12-19T21:30:00Z",
    "PageNumber": 1,
    "PageSize": 100
}
```

## Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202412201138271482F328AD8C800E91A0-aceec9",
        "Action": "DescribeTasks",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Datas": [
            {
                "CostTimeMS": 5132,
                "CreateTime": "2024-12-19T21:37:51.899Z",
                "FinishTime": "2024-12-19T21:37:57.031Z",
                "RelatedInstanceInfos": {
                    "InstanceID": "mysql-35444107e157"
                },
                "StartTime": "2024-12-19T21:37:51.899Z",
                "TaskAction": "CreateBackup",
                "TaskCategory": "BackupRecoveryManagement",
                "TaskDesc": "",
                "TaskId": "f5ecd0a0056e45e4bf9dde48211f4347",
                "TaskParams": "{\"InstanceId\":\"mysql-35444107e157\",\"BackupStrategy\":\"Instance\",\"BackupType\":\"Physical\",\"BackupMode\":\"Full\",\"BackupDataType\":\"Data\"}",
                "TaskReason": "DeleteDBInstance",
                "TaskSource": "User",
                "TaskStatus": "Success"
            },
            {
                "CostTimeMS": 26,
                "CreateTime": "2024-12-19T21:35:05.967Z",
                "FinishTime": "2024-12-19T21:35:05.993Z",
                "RelatedInstanceInfos": {
                    "InstanceID": "mysql-04af6e86****"
                },
                "StartTime": "2024-12-19T21:35:05.967Z",
                "TaskAction": "CreateDatabase",
                "TaskCategory": "DatabaseAdminManagement",
                "TaskDesc": "",
                "TaskId": "20241220053505D87B1953D97A39D9628A-6f2884",
                "TaskParams": "{\"InstanceId\":\"mysql-04af6e86****\",\"DBName\":\"io_observe995\",\"CharacterSetName\":\"utf8\",\"DBDesc\":\"\"}",
                "TaskReason": "User operation",
                "TaskSource": "User",
                "TaskStatus": "Success"
            },
            {
                "CostTimeMS": 180971,
                "CreateTime": "2024-12-19T21:31:45.167Z",
                "FinishTime": "2024-12-19T21:34:46.138Z",
                "RelatedInstanceInfos": {
                    "InstanceID": "mysql-5cd320d04a98"
                },
                "StartTime": "2024-12-19T21:31:45.167Z",
                "TaskAction": "CreateDBInstance",
                "TaskCategory": "InstanceManagement",
                "TaskDesc": "",
                "TaskId": "20241220053143A7560C55222B0AE868F5-891415",
                "TaskParams": "{\"DBEngineVersion\":\"MySQL_8_0\",\"InstanceType\":\"HA\",\"ZoneId\":\"\",\"NodeSpec\":\"\",\"NodeNumber\":0,\"NodeInfo\":[{\"ZoneId\":\"ap-southeast-1-a\",\"NodeType\":\"Primary\",\"NodeSpec\":\"rds.mysql.1c2g\",\"NodeOperateType\":\"Create\"},{\"ZoneId\":\"ap-southeast-1-a\",\"NodeType\":\"Secondary\",\"NodeSpec\":\"rds.mysql.1c2g\",\"NodeOperateType\":\"Create\"}],\"StorageType\":\"LocalSSD\",\"StorageSpace\":100,\"VpcId\":\"vpc-2ze1hcaoxk5c0610wgmc5****\",\"InstanceName\":\"测试实例3\",\"SuperAccountName\":\"rootgg\",\"SuperAccountPassword\":\"******\",\"LowerCaseTableNames\":\"1\",\"DBTimeZone\":\"UTC +08:00\",\"DBParamGroupId\":\"\",\"ChargeInfo\":{\"ChargeType\":\"PostPaid\",\"Number\":1},\"ProjectName\":\"default\",\"ShardNumber\":2,\"SubnetId\":\"subnet-257k5dxe6s5j44a7cffnk****\",\"Port\":3306}",
                "TaskReason": "User operation",
                "TaskSource": "User",
                "TaskStatus": "Success"
            }
        ],
        "Total": 3
    }
}
```

## Sample request 2

Query the details of a specified task by TaskId.

```json
POST /?Action=DescribeTasks&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "TaskId": "20241219213431ABD2ADEE7A33D166****-dac037",
    "PageNumber": 1,
    "PageSize": 100
}
```

## Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20241224141230E7B854577D989BBDE2A3-9131d9",
        "Action": "DescribeTasks",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Datas": [
            {
                "CostTimeMS": 5080,
                "CreateTime": "2024-12-19T21:38:00.911Z",
                "FinishTime": "2024-12-19T21:38:05.991Z",
                "RelatedInstanceInfos": {
                    "InstanceID": "mysql-9d90c967****"
                },
                "StartTime": "2024-12-19T21:38:00.911Z",
                "TaskAction": "CreateBackup",
                "TaskCategory": "BackupRecoveryManagement",
                "TaskDesc": "",
                "TaskId": "61fc851b46724ff09b3236ed24d74fb0",
                "TaskParams": "{\"InstanceId\":\"mysql-9d90c967****\",\"BackupStrategy\":\"Instance\",\"BackupType\":\"Physical\",\"BackupMode\":\"Full\",\"BackupDataType\":\"Data\"}",
                "TaskReason": "DeleteDBInstance",
                "TaskSource": "User",
                "TaskStatus": "Success"
            }
        ],
        "Total": 1
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
