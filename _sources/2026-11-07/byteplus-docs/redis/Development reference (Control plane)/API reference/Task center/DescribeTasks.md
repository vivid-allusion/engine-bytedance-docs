---
title: "DescribeTasks"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/DescribeTasks"
---

Call the DescribeTasks API to query tasks.

## Request type

Synchronous request.

## Precautions

Only supports viewing tasks created within the last 30 days.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTasks&serviceCode=Redis&version=2020-12-07&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|PageNumber |Integer |Yes |1 |Page number for the task list, a positive integer greater than or equal to 1. |
|PageSize |Integer |Yes |10 |Number of records per page. An integer from 1 to 100. |
|CreationStartTime |String |No |2025\-01\-02T15:04:05Z |The start of the time range when querying by task creation time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> If `TaskId` is not specified, both `CreationStartTime` and `CreationEndTime` must be provided.<br> |
|CreationEndTime |String |No |2025\-01\-02T15:14:05Z |The end point of the time range when querying by task creation time, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> If `TaskId` is not specified, both `CreationStartTime` and `CreationEndTime` must be provided.<br> |
|InstanceId |String |No |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|InstanceName |String |No |test |Instance name. |
|TaskId |String |No |4027864 |Task ID. Used to query a specific task.<br><br>> **tip**<br><br><br>> If `TaskId` is not specified, both `CreationStartTime` and `CreationEndTime` must be provided.<br> |
|TaskName |String |No |ModifyDBInstanceShardNumber |Task actions. |
|ProjectName |String |No |default |Project name. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Tasks |Array of [OpTask](https://docs.byteplus.com/en/docs/55/118244#optask) |Refer to the Sample response. |Task list. |
|Total |Integer |1 |The total number of results that meet the query conditions. |

### OpTask

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CostTimeMS |Long |120000 |Elapsed time for the operation, in milliseconds. |
|CreateTime |String |2025\-01\-02T15:05:00Z |The creation time of the task, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC). |
|FinishTime |String |2025\-01\-02T15:07:05Z |The completion time of the task, formatted as `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC). |
|InstanceInfo |Object of [RelatedInstanceInfo](https://docs.byteplus.com/en/docs/55/118244#relatedinstanceinfo) |Refer to the Sample response. |Information about the instance after task execution. |
|InstanceName |String |test |Instance name. |
|OriginInstanceInfo |Object of [RelatedInstanceInfo](https://docs.byteplus.com/en/docs/55/118244#relatedinstanceinfo) |Refer to the Sample response. |Relevant information about the instance before task execution. |
|Progress |Integer |100 |Task execution progress. The unit is percentage. |
|StartTime |String |2025\-01\-02T15:05:05Z |The start time of the task, in the format `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC). |
|TaskAction |String |ModifyDBInstanceShardNumber |Task operation. |
|TaskDesc |String |test |The description of the task. |
|TaskId |String |4027864 |Task ID. |
|TaskName |String |ModifyDBInstanceShardNumber |Task name. |
|TaskParams |String |1111 |Task parameters. |
|TaskStatus |String |"Running" |Task status. |
|TaskStepInfo |Array of [TaskStepInfo](https://docs.byteplus.com/en/docs/55/118244#taskstepinfo) |Refer to the Sample response. |Progress information for each stage of the task. |

### RelatedInstanceInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ConfigureNodes |Array of String |["cn\-beijing\-a"] |Availability zone distribution details. |
|EngineVersion |String |6.0 |The database version number of the instance. |
|InstanceID |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|InstanceName |String |test |Instance name. |
|NodeNumber |Integer |2 |Number of replicas. |
|ProxyVersion |String |1.512.0 |Minor version of proxy.<br><br>> **tip**<br><br><br>> This parameter is only returned in tasks that upgrade the instance's minor version.<br> |
|ServerVersion |String |7.512.0 |Minor version of server.<br><br>> **tip**<br><br><br>> This parameter is only returned in tasks that upgrade the instance's minor version.<br> |
|ShardCapacity |Long |1024 |Shard capacity, in MiB. |
|ShardedCluster |Integer |1 |Indicates whether the current instance has enabled a sharding cluster. Valid values are as follows:<br><br><br>* `0`: Disabled (the instance contains only 1 shard).<br><br>* `1`: Enabled (the instance contains more than 1 shard). |
|ShardNumber |Integer |3 |Number of shards. |
|SubnetId |String |subnet\-rrz4zdgdv20wv0x58h\*\*\*\* |Subnet ID of the instance's subnet |
|VpcId |String |vpc\-rs5811nceqyov0x\*\*\*\* |ID of Virtual Private Cloud. |
|ZoneIds |Array of String |["cn\-beijing\-a"] |Instance availability zone |

### TaskStepInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |Task initialization |Stage name. |
|StepStatus |String |Running |Stage status. |
|ProgressDesc |String |Task initialization |Progress description. |
|StepProgress |Integer |10 |Stage progress. The unit is percentage. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeTasks&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "PageNumber": 1,
    "PageSize": 10,
    "CreationStartTime": "2026-06-21T15:04:05Z",
    "CreationEndTime": "2025-07-20T15:14:05Z",
    "InstanceId": "redis-cn0212gzmh2xs****",
    "InstanceName": "Redis-测试实例",
    "TaskId": "4027864",
    "TaskName": "ModifyDBInstanceShardCapacity",
    "ProjectName": "default"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTasks",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Total": 1,
        "Tasks": [
            {
                "CostTimeMS": 46926,
                "CreateTime": "2026-07-21T04:39:40Z",
                "FinishTime": "2026-07-21T04:40:28.09Z",
                "InstanceInfo": {
                    "ConfigureNodes": [
                        "cn-beijing-b",
                        "cn-beijing-a",
                        "cn-beijing-c"
                    ],
                    "EngineVersion": "6.0",
                    "InstanceID": "redis-cngzzlgtiykg6****",
                    "InstanceName": "Redis-测试实例",
                    "NodeNumber": 3,
                    "ShardCapacity": 1024,
                    "ShardNumber": 2,
                    "ShardedCluster": 1,
                    "SubnetId": "subnet-3u6vz8mposyrk3ael9eyk****",
                    "VpcId": "vpc-1m1sso3n4x8u86vtia6hh****",
                    "ZoneIds": [
                        "cn-beijing-b",
                        "cn-beijing-a",
                        "cn-beijing-c"
                    ]
                },
                "InstanceName": "Redis-测试实例",
                "OriginInstanceInfo": {
                    "ConfigureNodes": [
                        "cn-beijing-b",
                        "cn-beijing-a",
                        "cn-beijing-c"
                    ],
                    "EngineVersion": "6.0",
                    "InstanceID": "redis-cngzzlgtiykg6****",
                    "InstanceName": "Redis-测试实例",
                    "NodeNumber": 3,
                    "ShardCapacity": 8192,
                    "ShardNumber": 2,
                    "ShardedCluster": 1,
                    "SubnetId": "subnet-3u6vz8mposyrk3ael9eyk****",
                    "VpcId": "vpc-1m1sso3n4x8u86vtia6hh****",
                    "ZoneIds": [
                        "cn-beijing-b",
                        "cn-beijing-a",
                        "cn-beijing-c"
                    ]
                },
                "Progress": 100,
                "StartTime": "2026-07-21T04:39:41.164Z",
                "TaskAction": "ModifyDBInstanceShardCapacity",
                "TaskDesc": "",
                "TaskId": "4463505",
                "TaskName": "ModifyDBInstanceShardCapacity",
                "TaskParams": "{\"InstanceId\": \"redis-cngzzlgtiykg6****\", \"ShardCapacity\": 1024, \"ApplyImmediately\": true, \"CreateBackup\": true, \"BackupPointName\": \"\\u9ad8\\u9891\\u62e8\\u6d4b-\\u51cf\\u5c11\\u5206\\u7247\\u5bb9\\u91cf\"}",
                "TaskStatus": "Success",
                "TaskStepInfo": [
                    {
                        "Name": "任务初始化中",
                        "StepProgress": 100,
                        "StepStatus": "Success"
                    },
                    {
                        "Name": "备份中",
                        "StepProgress": 100,
                        "StepStatus": "Success"
                    },
                    {
                        "Name": "节点规格变更中",
                        "StepProgress": 100,
                        "StepStatus": "Success"
                    },
                    {
                        "Name": "配置修改中",
                        "StepProgress": 100,
                        "StepStatus": "Success"
                    },
                    {
                        "Name": "任务成功",
                        "StepProgress": 100,
                        "StepStatus": "Success"
                    }
                ]
            }
        ]
    }
}
```

## Error code

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/redis/error-code).
