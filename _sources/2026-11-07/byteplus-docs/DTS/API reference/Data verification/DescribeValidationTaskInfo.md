---
title: "DescribeValidationTaskInfo"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/describevalidationtaskinfo"
---

Call the DescribeValidationTaskInfo API to view data verification task details.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |d496677038544e4a82d0ff0d9d\*\*\*\*\*\* |Verification task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/DTS/describevalidationtasks">DescribeDataValidationTasks</a> interface to query the data verification task ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TaskInfo |Object of [TaskInfo](https://docs.byteplus.com/en/docs/57/47098#taskinfo) |```json```<br>```{```<br>```    "ResponseMetadata": {```<br>```        "RequestId": "202412101725348099E9905A095805FBE9-cace50",```<br>```        "Action": "DescribeValidationTaskInfo",```<br>```        "Version": "2022-10-01",```<br>```        "Service": "dts",```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Result": {```<br>```        "TaskInfo": {```<br>```            "ChargeConfig": {```<br>```                "ChargeType": "PostPaid",```<br>```                "DestRegion": "cn-beijing",```<br>```                "DestType": "Volc_Mongo",```<br>```                "EnableV2": true,```<br>```                "SrcRegion": "cn-beijing",```<br>```                "SrcType": "Volc_Mongo",```<br>```                "TaskType": "DataValidation",```<br>```                "Times": 1,```<br>```                "TrafficSpec": "Compact"```<br>```            },```<br>```            "ChargeDetail": {```<br>```                "ChargeEndTime": 7258089600000,```<br>```                "ChargeStartTime": 1733822722000,```<br>```                "ChargeStatus": "Normal",```<br>```                "ChargeType": "PostPaid",```<br>```                "OrderNo": ""```<br>```            },```<br>```            "CreateTime": 1733822707944,```<br>```            "DestConfig": {```<br>```                "Category": "MongoDB",```<br>```                "CreateTime": 1733822707933,```<br>```                "DataSourceId": "1866402178390831111",```<br>```                "EndpointType": "Volc_Mongo",```<br>```                "ModifyTime": 1733822723986,```<br>```                "VolcMongoSettings": {```<br>```                    "DBInstanceId": "mongo-replica-d91799021291",```<br>```                    "DBInstanceName": "",```<br>```                    "DeployType": "ReplicaSet",```<br>```                    "MongoAuthSourceDB": "admin",```<br>```                    "Password": "******",```<br>```                    "RegionSettings": {```<br>```                        "Region": "cn-beijing"```<br>```                    },```<br>```                    "Username": "root"```<br>```                }```<br>```            },```<br>```            "EnableCloudMonitor": true,```<br>```            "EndTime": 0,```<br>```            "ParentTaskID": "4c1d32fe38c64ec7bf7f02d87926e94d",```<br>```            "ParentTaskName": "dts-483oh5l2ne",```<br>```            "ProjectName": "default",```<br>```            "SolutionSettings": {```<br>```                "Mongo2MongoPkCompareSettings": {```<br>```                    "ObjectMappings": [```<br>```                        {```<br>```                            "DestObjName": "__mongodb_systems__",```<br>```                            "MappingList": [```<br>```                                {```<br>```                                    "DestObjName": "*",```<br>```                                    "ObjectMappingSetting": {```<br>```                                        "PolicyForKeyConflict": "TableNone",```<br>```                                        "SetObjectTransType": false```<br>```                                    },```<br>```                                    "ObjectType": "Table",```<br>```                                    "SrcObjName": "*"```<br>```                                },```<br>```                                {```<br>```                                    "DestObjName": "mongodb_sla",```<br>```                                    "ObjectMappingSetting": {```<br>```                                        "PolicyForKeyConflict": "TableNone",```<br>```                                        "SetObjectTransType": false```<br>```                                    },```<br>```                                    "ObjectType": "Table",```<br>```                                    "SrcObjName": "mongodb_sla"```<br>```                                }```<br>```                            ],```<br>```                            "ObjectType": "Database",```<br>```                            "SrcObjName": "__mongodb_systems__"```<br>```                        },```<br>```                        {```<br>```                            "DestObjName": "cecehi",```<br>```                            "MappingList": [```<br>```                                {```<br>```                                    "DestObjName": "*",```<br>```                                    "ObjectMappingSetting": {```<br>```                                        "PolicyForKeyConflict": "TableNone",```<br>```                                        "SetObjectTransType": false```<br>```                                    },```<br>```                                    "ObjectType": "Table",```<br>```                                    "SrcObjName": "*"```<br>```                                },```<br>```                                {```<br>```                                    "DestObjName": "ddd",```<br>```                                    "ObjectMappingSetting": {```<br>```                                        "PolicyForKeyConflict": "TableNone",```<br>```                                        "SetObjectTransType": false```<br>```                                    },```<br>```                                    "ObjectType": "Table",```<br>```                                    "SrcObjName": "ddd"```<br>```                                },```<br>```                                {```<br>```                                    "DestObjName": "d",```<br>```                                    "ObjectMappingSetting": {```<br>```                                        "PolicyForKeyConflict": "TableNone",```<br>```                                        "SetObjectTransType": false```<br>```                                    },```<br>```                                    "ObjectType": "Table",```<br>```                                    "SrcObjName": "d"```<br>```                                }```<br>```                            ],```<br>```                            "ObjectType": "Database",```<br>```                            "SrcObjName": "cecehi"```<br>```                        }```<br>```                    ]```<br>```                },```<br>```                "SolutionType": "Mongo2MongoPkCompare"```<br>```            },```<br>```            "SrcConfig": {```<br>```                "Category": "MongoDB",```<br>```                "CreateTime": 1733822707931,```<br>```                "DataSourceId": "1866402178390831110",```<br>```                "EndpointType": "Volc_Mongo",```<br>```                "ModifyTime": 1733822723579,```<br>```                "VolcMongoSettings": {```<br>```                    "DBInstanceId": "mongo-replica-386df9f4fd7c",```<br>```                    "DBInstanceName": "",```<br>```                    "DeployType": "ReplicaSet",```<br>```                    "MongoAuthSourceDB": "admin",```<br>```                    "Password": "******",```<br>```                    "RegionSettings": {```<br>```                        "Region": "cn-beijing"```<br>```                    },```<br>```                    "Username": "root"```<br>```                }```<br>```            },```<br>```            "StartTime": 1733822723214,```<br>```            "TaskId": "38b77a44d6fc4cb89fe6964b8******",```<br>```            "TaskName": "test2",```<br>```            "TaskStatus": "Running",```<br>```            "TaskSubType": "FullPkCompare",```<br>```            "TaskType": "DataValidation",```<br>```            "TenantId": "2100******",```<br>```            "TrafficSpec": "Compact"```<br>```        }```<br>```    }```<br>```}```<br> |Data verification task details. |


<span id="taskinfo"></span>
### TaskInfo


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|TaskId |String |6f2fd63c0ea947b280877f5d2a\*\*\*\*\*\*\* |Task ID. |
|TaskName |String |test\*\*\*\* |Task name. |
|ParentTaskID |String |4f85ae2481a643d99c0f45444\*\*\*\*\*\* |Primary task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When bidirectional synchronization is enabled, the value of this parameter is the ID of the forward synchronization task corresponding to the reverse synchronization task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When querying data verification tasks and bidirectional synchronization tasks, it indicates the ID of the primary task.</div><br> |
|ParentTaskName |String |diff |Primary task name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When bidirectional synchronization is enabled, the value of this parameter is the name of the forward synchronization task corresponding to the reverse synchronization task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When querying data verification tasks and bidirectional synchronization tasks, it indicates the name of the primary task.</div><br> |
|TenantId |String |21000\*\*\*\*\* |Account ID. |
|TaskStatus |String |Failed |Task status. The valid values are:<br><br><br>* `Cancelled`: Indicates that the task is cancelled.<br><br>* `Failed`: Indicates that the task failed.<br><br>* `Running`: Indicates that the task is in progress.<br><br>* `Pause`: Indicates that the task is paused.<br><br>* `Init`: Indicates that the task is to be started.<br><br>* `Terminating`: Indicates that the task is terminating.<br><br>* `Success`: Indicates that the task was successful. |
|TaskType |String |DataSubscription |Task type. The values are as follows:<br><br><br>* `DataMigration`: Indicates a data migration task.<br><br>* `DataSubscription`: Indicates a data subscription task.<br><br>* `DataSynchronization`: Indicates a data synchronization task.<br><br>* `DataValidation`: Indicates a data verification task. |
|SrcConfig |Object of [DataSource](https://docs.byteplus.com/en/docs/57/47098#datasource) |```JSON```<br>```{```<br>```    "Category": "MySQL",```<br>```    "CreateTime": 1767700785480,```<br>```    "DataSourceId": "200850054678025****",```<br>```    "EndpointType": "Volc_veDB_MySQL",```<br>```    "ModifyTime": 1767700803345,```<br>```    "VolcveDBMySQLSettings": {```<br>```        "DBInstanceId": "vedbm-arjlc5di****",```<br>```        "DBInstanceName": "",```<br>```        "Password": "******",```<br>```        "RegionSettings": {```<br>```            "Region": "cn-beijing"```<br>```        },```<br>```        "Username": "root"```<br>```    }```<br>```}```<br> |Source information. |
|DestConfig |Object of [DataSource](https://docs.byteplus.com/en/docs/57/47098#datasource) |```JSON```<br>```{```<br>```    "Category": "MySQL",```<br>```    "CreateTime": 1767700785480,```<br>```    "DataSourceId": "200850054678025****",```<br>```    "EndpointType": "Volc_veDB_MySQL",```<br>```    "ModifyTime": 1767700803345,```<br>```    "VolcveDBMySQLSettings": {```<br>```        "DBInstanceId": "vedbm-arjlc5di****",```<br>```        "DBInstanceName": "",```<br>```        "Password": "******",```<br>```        "RegionSettings": {```<br>```            "Region": "cn-beijing"```<br>```        },```<br>```        "Username": "root"```<br>```    }```<br>```}```<br> |Destination information. |
|SolutionSettings |Object of [SolutionSettings](https://docs.byteplus.com/en/docs/57/47098#solutionsettings) |```JSON```<br>```{```<br>```    "MySQL2MySQLSettings": {```<br>```        "EnableFullIncr": true```<br>```    },```<br>```    "SolutionType": "MySQL2MySQL"```<br>```}```<br> |The configuration information of the migration, subscription, synchronization, or verification task object. |
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/57/47098#chargedetailobject) |```JSON```<br>```{```<br>```    "ChargeEndTime": 7258089600000,```<br>```    "ChargeStartTime": 1767700647000,```<br>```    "ChargeStatus": "Normal",```<br>```    "ChargeType": "PostPaid",```<br>```    "OrderNo": ""```<br>```}```<br> |Billing information. |
|ChargeConfig |Object of [ChargeConfig](https://docs.byteplus.com/en/docs/57/47098#chargeconfig) |```JSON```<br>```{```<br>```    "ChargeType": "PostPaid",```<br>```    "DestRegion": "cn-beijing",```<br>```    "DestType": "Volc_veDB_MySQL",```<br>```    "EnableV2": true,```<br>```    "IsBidirectional": false,```<br>```    "SrcRegion": "cn-beijing",```<br>```    "SrcType": "Volc_veDB_MySQL",```<br>```    "TaskType": "DataMigration",```<br>```    "TrafficSpec": "Standard"```<br>```}```<br> |Billing Configuration. |
|TrafficSpec |String |Compact |Task link specifications. support Compact, Medium, and Standard values. For details about the link specification, refer to [Product specification](https://docs.byteplus.com/en/docs/DTS/product_specifications). |
|ProgressSummary |Object of [ProgressSummary](https://docs.byteplus.com/en/docs/57/47098#progresssummary) |```JSON```<br>```{```<br>```    "Infos": [```<br>```        {```<br>```            "CompletePercentage": 100,```<br>```            "ErrorInfo": "",```<br>```            "NameCN": "结构迁移",```<br>```            "ProgressType": "Meta",```<br>```            "Status": "Done"```<br>```        },```<br>```        {```<br>```            "CompletePercentage": 100,```<br>```            "NameCN": "全量迁移",```<br>```            "ProgressType": "Full",```<br>```            "Status": "Doing"```<br>```        },```<br>```        {```<br>```            "Delay": 0,```<br>```            "NameCN": "增量迁移",```<br>```            "ProgressType": "Incr",```<br>```            "Status": "Doing"```<br>```        },```<br>```        {```<br>```            "CompletePercentage": 0,```<br>```            "ErrorInfo": "",```<br>```            "NameCN": "后置结构迁移",```<br>```            "ProgressType": "PostMeta",```<br>```            "Status": "Todo"```<br>```        }```<br>```    ]```<br>```}```<br> |Total progress of the task. |
|ErrorInfo |String |```json```<br>```{```<br>```    "biz_context":"{```<br>```          "log_id":"88e5ed340fb4466b999bc89****",```<br>```          "tenant_id":"2100157781",```<br>```          "instance_id":"6f2fd63c0ea947b280877f5****"```<br>```    }",```<br>```    "reason":"mysql endpoint error: dial tcp 172.****",```<br>```    "kind":1,```<br>```    "app":"AppMySQLIncr2Kafka",```<br>```    "app_id":"1049"```<br>```}```<br> |Task error message. |
|CreateTime |Long |1661242976288 |Task creation time, using milliseconds timestamp format. |
|StartTime |Long |1661242976288 |Task start time, in milliseconds timestamp format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is set, the query end time (that is, the <code>EndTime</code>) parameter is also required.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is left blank, all existing tasks under the current task type are returned by default.</div><br> |
|EndTime |Long |0 |Task end time, using milliseconds timestamp format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is set, the query end time (that is, the <code>EndTime</code>) parameter is also required.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The end time must be later than the start time.</div><br> |
|ProjectName |String |default |Project name. |
|AddSyncObjectAllowed |Boolean |true |Whether modification of the synchronization object is allowed. The values are as follows:<br><br><br>* `true`: Indicates that the synchronization object can be modified.<br><br>* `false`: Indicates that the synchronization object cannot be modified. |
|EnableDataValidation |Boolean |true |Whether to enable data verification. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `False`: Indicates close. |
|TaskSubType |String |Default |Data type. The values are as follows:<br><br><br>* `Default`: Indicates the value of the migration or subscription task.<br><br>* `ForwardSync`: Indicates forward synchronization.<br><br>* `BackwardSync`: Indicates reverse synchronization.<br><br>* `FullRowCountCompare`: Indicates full row\-count verification.<br><br>* `FullRowCompare`: Indicates full data verification.<br><br>* `FullPkCompare`: Indicates full primary key validation.<br><br>* `IncrDataValidation`: Indicates Increment validation.<br><br>* `MetaCompare`: Indicates Schema Verification. |
|EnableCloudMonitor |Boolean |true |Whether to enable cloud monitor, with the following values:<br><br><br>* `true`: Indicates enabled.<br><br>* `false`: Indicates disabled (default). |
|UpdateTime |Long |1661242976290 |Task update time, using milliseconds timestamp format. |
|SnapshotGtid |String |SnapshotGtid |Full data consistency migration configuration. |


<span id="datasource"></span>
### DataSource


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Category |String |MySQL |The type of instance. The values are as follows:<br><br><br>* `MySQL`: Indicates that the instance type is MySQL.<br><br>* `PostgreSQL`: Indicates that the instance type is PostgreSQL.<br><br>* `ElasticSearch`: Indicates that the instance type is Elasticsearch.<br><br>* `MongoDB`: Indicates that the instance type is MongoDB.<br><br>* `Redis`: Indicates that the instance type is Redis. |
|CreateTime |Long |1734070854504 |Creation time of the data source. Millisecond timestamp. |
|DataSourceId |String |1867454442941460510 |Source or target instance ID. |
|ModifyTime |Long |1734070873088 |The most recent time the data source was updated. Millisecond timestamp. |
|EndpointType |String |Volc_MySQL |The access method of the instance. the values are as follows:<br><br><br>* `Volc_MySQL`: Indicates BytePlus NDB for MySQL.<br><br>* `Volc_veDB_MySQL`: Indicates BytePlus NDB for MySQL.<br><br>* `Volc_PostgreSQL`: Indicates Volcengine RDS for PostgreSQL.<br><br>* `Volc_Mongo`: Indicates Volcengine Database for MongoDB.<br><br>* `Volc_ElasticSearch`: Indicates Volcengine Cloud Search Service.<br><br>* `Volc_Kafka`: Indicates Message Queue for Kafka.<br><br>* `Volc_RocketMQ`: Indicates Message Queue for RocketMQ.<br><br>* `Volc_Redis`: Indicates Volcengine Cache for Redis.<br><br>* `Public_MySQL`: Indicates MySQL connected over public network.<br><br>* `Public_PostgreSQL`: Indicates  connected over public network.<br><br>* `Public_Mongo`: Indicates MongoDB connected over public network..<br><br>* `Public_ElasticSearch`: Indicates Cloud Search connected over public network.<br><br>* `Public_Redis`: Indicates Redis connected over express network.<br><br>* `Builtin_Kafka`: Indicates the built\-in middleware.<br><br>* `Express_MySQL`: Indicates MySQL connected over express network.<br><br>* `Express_PostgreSQL`: Indicates PostgreSQL connected over express network.<br><br>* `Express_Mongo`: Indicates MongoDB connected over express network.<br><br>* `Express_Redis`: Indicates Redis connected over express network.<br><br>* `Express_Kafka`: Indicates Kafka connected over express network.<br><br>* `Express_ElasticSearch`: Indicates ElasticSearch connected over express network. |
|VolcMySQLSettings |Object of [VolcMySQLSettings](https://docs.byteplus.com/en/docs/57/47098#volcmysqlsettings) |```JSON```<br>```{```<br>```    "DBInstanceId": "mysql-0b5d385f*****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-shanghai"```<br>```    },```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine RDS for MySQL. This parameter is required when `EndpointType` is set to `Volc_MySQL`. |
|VolcveDBMySQLSettings |Object of [VolcveDBMySQLSettings](https://docs.byteplus.com/en/docs/57/47098#volcvedbmysqlsettings) |```JSON```<br>```{```<br>```    "DBInstanceId": "vedbm-arjlc5di****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "root"```<br>```}```<br> |Indicates the information of the source or target database where the access method is BytePlus veDB for MySQL. This parameter is required when `EndpointType` is set to `Volc_veDB_MySQL`. |
|VolcPostgreSQLSettings |Object of [VolcPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47098#volcpostgresqlsettings) |```JSON```<br>```{```<br>```    "DBInstanceId": "postgres-5d17bd5c****",```<br>```    "DBInstanceName": "",```<br>```    "DBName": "huahua",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine RDS for PostgreSQL. This parameter is required when `EndpointType` is set to `Volc_PostgreSQL`. |
|VolcMongoSettings |Object of [VolcMongoSettings](https://docs.byteplus.com/en/docs/57/47098#volcmongosettings) |```JSON```<br>```{```<br>```    "DBInstanceId": "mongo-replica-8ea79132****",```<br>```    "DBInstanceName": "",```<br>```    "DeployType": "ReplicaSet",```<br>```    "MongoAuthSourceDB": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Username": "root"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine Database for MongoDB. This parameter is required when `EndpointType` is set to `Volc_Mongo`. |
|VolcElasticSearchSettings |Object of [VolcElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47098#volcelasticsearchsettings) |```JSON```<br>```{```<br>```    "DBInstanceId": "o-00g0sqi*****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-shanghai"```<br>```    },```<br>```    "Username": "admin"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine Cloud Search Service. This parameter is required when `EndpointType` is set to `Volc_ElasticSearch`. |
|VolcKafkaSettings |Object of [VolcKafkaSettings](https://docs.byteplus.com/en/docs/57/47098#volckafkasettings) |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "InstanceId": "kafka-cnnge0tckudy****",```<br>```    "InstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Topic": "huahua",```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the target database when the access method is Volcengine Kafka. This parameter is required when `EndpointType` is set to `Volc_Kafka`. |
|VolcRocketMQSettings |Object of [VolcRocketMQSettings](https://docs.byteplus.com/en/docs/57/47098#volcrocketmqsettings) |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "InstanceId": "rocketmq-cnou964d1e******",```<br>```    "InstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Topic": "zaizai",```<br>```    "Username": "uSmQgOHNTy5Uh98nqBGPvCzK"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine RocketMQ. This parameter is required when `EndpointType` is set to `Volc_RocketMQ`. |
|VolcRedisSettings |Object of [VolcRedisSettings](https://docs.byteplus.com/en/docs/57/47098#volcredissettings) |```JSON```<br>```{```<br>```    "DBInstanceId": "redis-cnlf1xx7vjjw9****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine Cache for Redis. This parameter is required when `EndpointType` is set to `Volc_Redis`. |
|PublicMySQLSettings |Object of [PublicMySQLSettings](https://docs.byteplus.com/en/docs/57/47098#publicmysqlsettings) |```JSON```<br>```{```<br>```    "Host": "rm-2zey7i58n36x0****.mysql.rds.aliyuncs.com",```<br>```    "Password": "******",```<br>```    "Port": 3306,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "rootgg"```<br>```}```<br> |Indicates the source database or target database information with the access method as public network MySQL. This parameter is required when `EndpointType` is set to `Public_MySQL`. |
|PublicPostgreSQLSettings |Object of [PublicPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47098#publicpostgresqlsettings) |```JSON```<br>```{```<br>```    "DBName": "postgres",```<br>```    "Host": "aurora-pg-17-replica-instance-1.czenkuaf0oxm.ap-southeast-2.rds.amazonaws.com",```<br>```    "Password": "******",```<br>```    "Port": 5432,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "dts"```<br>```}```<br> |Indicates the information of the source database or target database with the access method as PostgreSQL connected over public network. This parameter is required when `EndpointType` is set to `Public_PostgreSQL`. |
|PublicMongoSettings |Object of [PublicMongoSettings](https://docs.byteplus.com/en/docs/57/47098#publicmongosettings) |```JSON```<br>```{```<br>```    "DeployType": "Standalone",```<br>```    "Endpoints": [```<br>```        "123"```<br>```    ],```<br>```    "MongoAuthSourceDB": "123",```<br>```    "Password": "123",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-chongqing-sdv"```<br>```    },```<br>```    "Username": "123"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MongoDB connected over public network. This parameter is required when `EndpointType` is set to `Public_Mongo`. |
|PublicElasticSearchSettings |Object of [PublicElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47098#publicelasticsearchsettings) |```JSON```<br>``````<br>```{```<br>```    "Endpoints": [```<br>```        "********"```<br>```    ],```<br>```    "Password": "dddd",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "ddd"```<br>```}```<br> |Indicates information of source database or target database ElasticSearch connected over public network. This Parameter is required when `EndpointType` is set to `Public_ElasticSearch`. |
|PublicRedisSettings |Object of [PublicRedisSettings](https://docs.byteplus.com/en/docs/57/47098#publicredissettings) |```JSON```<br>```{```<br>```    "Host": "redis-sy013ku146******.redis.inner.ivolces.com",```<br>```    "Password": "******",```<br>```    "Port": 6379,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |Information about the source database or target database with access method as Redis connected over public network. This parameter is Required when `EndpointType` is set to `Public_Redis`. |
|BuiltinKafkaSettings |Object of [BuiltinKafkaSettings](https://docs.byteplus.com/en/docs/57/47098#builtinkafkasettings) |```JSON```<br>```{```<br>```    "Brokers": [```<br>```        "192.168.2.5:9092",```<br>```        "192.168.2.5:9192",```<br>```        "192.168.2.5:9292",```<br>```        "192.168.2.5:9392",```<br>```        "192.168.2.5:9492",```<br>```        "192.168.2.5:9592"```<br>```    ],```<br>```    "Topic": "123e8d8a3cc54477b45db3e3c708****"```<br>```}```<br> |Indicates the parameter information for subscribing to the built\-in middleware in the data subscription task. This parameter is required when `EndpointType` is set to `Builtin_Kafka`. |
|ExpressMongoSettings |Object of [ExpressMongoSettings](https://docs.byteplus.com/en/docs/57/47098#expressmongosettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "DeployType": "ReplicaSet",```<br>```    "Endpoints": [```<br>```        "eee"```<br>```    ],```<br>```    "MongoAuthSourceDB": "eee",```<br>```    "Password": "e",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-3jh1vsccsmjuo3pncmesj****",```<br>```        "VPCId": "vpc-30ukbt5glgyyo7r2qr2e6****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-chongqing-sdv"```<br>```    },```<br>```    "Username": "e"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MongoDB connected over express network. This parameter is required when `EndpointType` is `Express_Mongo`. |
|ExpressMySQLSettings |Object of [ExpressMySQLSettings](https://docs.byteplus.com/en/docs/57/47098#expressmysqlsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Host": "192.168.0.65",```<br>```    "Password": "******",```<br>```    "Port": 3306,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2d74b6pbyewao58ozferi****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9*****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "rootgg"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MySQL connected over express network. Required when `EndpointType` is `Express_MySQL`. |
|ExpressPostgreSQLSettings |Object of [ExpressPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47098#expresspostgresqlsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "DBName": "src",```<br>```    "Host": "192.168.0.65",```<br>```    "Password": "Bd2021_bd",```<br>```    "Port": 5432,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2bznv8i16voqo2dx0efg0****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "suser"```<br>```}```<br> |Indicates the information of the source or target database where the access method is PostgreSQL connected over express network. This parameter is required when `EndpointType` equals `Express_PostgreSQL`. |
|ExpressRedisSettings |Object of [ExpressRedisSettings](https://docs.byteplus.com/en/docs/57/47098#expressredissettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ArchType": "Standalone",```<br>```    "Host": "192.168.32.28",```<br>```    "Password": "pwd",```<br>```    "Port": 6399,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-3re9nvjumjthc5zsk2i5z****",```<br>```        "VPCId": "vpc-2bzf04ctm2pz42dx0eebh****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |This represents the information of the source database or target database with access method of Redis connected over express network. When `EndpointType` is `Express_Redis`, this parameter is required. |
|ExpressElasticSearchSettings |Object of [ExpressElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47098#expresselasticsearchsettings) |```JSON```<br>```{```<br>```    "Endpoints": [```<br>```        "http://192.****.0.****:9200"```<br>```    ],```<br>```    "Password": "123456",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2d6asbw971nnk58ozfeei****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "elastic"```<br>```}```<br> |Indicates the information of the source or target database where the access method is ElasticSearch connected over express network. This parameter is required when `EndpointType` is set to `Express_ElasticSearch`. |
|ExpressKafkaSettings |Object of [ExpressKafkaSettings](https://docs.byteplus.com/en/docs/57/47098#expresskafkasettings) |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "BrokerEndpoints": [```<br>```        "192.168.0.65:9092"```<br>```    ],```<br>```    "Password": "admin-secret",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2bz5swar08oao2dx0ee******",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9******"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Topic": "dial_test",```<br>```    "Username": "admin"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Kafka connected over express network. This parameter is required when `EndpointType` is set to `Express_Kafka`. |
|Name |String |test |Task name of the data source. This parameter is required when you call the CreateDataSource API to create a data source. |


<span id="volcmysqlsettings"></span>
### VolcMySQLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DBInstanceId |String |mysql\-3d224def\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_MySQL</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> interface to query the instance ID.</div><br> |
|DBInstanceName |String |testDB |Instance name. |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47098#crossaccountsettings) |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="regionsettings"></span>
### RegionSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Region |String |cn\-beijing |Region ID. |


<span id="crossaccountsettings"></span>
### CrossAccountSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SourceAccount |String |2100\*\*\*\*\*\* |Source account ID. |
|Role |String |test |The role name created by source accounts for the transmission of data. |


<span id="volcvedbmysqlsettings"></span>
### VolcveDBMySQLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DBInstanceId |String |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_veDB_MySQL</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> interface to query the Instance ID.</div><br> |
|DBInstanceName |String |TestveDB |Instance name. |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47098#crossaccountsettings) |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="volcpostgresqlsettings"></span>
### VolcPostgreSQLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DBInstanceId |String |postgres\-h441603c68aaa\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when EndpointType is set to <code>Volc_PostgreSQL</code> in <code>EndpointType</code>.</div><br> |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|DBName |String |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47098#crossaccountsettings) |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |
|ExtraParams |Array of [ExtraParam](https://docs.byteplus.com/en/docs/57/47098#extraparam) | | |


<span id="extraparam"></span>
### ExtraParam


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Key |String | | |
|Value |String | | |


<span id="volcmongosettings"></span>
### VolcMongoSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DBInstanceId |String |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Mongo</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances">DescribeDBInstanceDetail</a> API to query the instance ID.</div><br> |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|MongoAuthSourceDB |String |ReplicaSet |Account verification database. When` EndpointType `is set to `Volc_Mongo`, the default value of this parameter is `root`. |
|DeployType |String |ShardedCluster |The instance type of MongoDB. The values are as follows:<br><br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47098#crossaccountsettings) |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |
|PullMethod |String |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |


<span id="volcelasticsearchsettings"></span>
### VolcElasticSearchSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DBInstanceId |String |ztuc43y38z4w\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_ElasticSearch</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstances">DescribeInstances</a> interface to query the instance ID.</div><br> |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volckafkasettings"></span>
### VolcKafkaSettings


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|InstanceId |String |kafka\-\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Kafka</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/kafka/DescribeInstancesSummary-v1">DescribeInstancesSummary</a> interface to query the Instance ID.</div><br> |
|AuthType |String |plain |Authentication method. The default value is `plain`. |
|Username |String |test\*\*\*\* |The username for the Kafka instance using the PLAIN mode. |
|Password |String |test\*\*\*\* |The password for the Kafka instance using the PLAIN mode. |
|Topic |String |my_topic |Kafka's Topic name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volcrocketmqsettings"></span>
### VolcRocketMQSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|InstanceId |String |MQ_INST_ ** *\*\*\*\*\** **  |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_RocketMQ</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/6410/67914">GetInstance</a> API to query the Instance ID.</div><br> |
|AuthType |String |plain |Authentication method. The default value is `plain`. |
|Username |String |test\*\*\*\* |The username of the RocketMQ instance. |
|Password |String |test\*\*\*\* |User password for RocketMQ instance. |
|Topic |String |my_topic |Topic name of RocketMQ. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volcredissettings"></span>
### VolcRedisSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DBInstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Redis</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/redis/describedbinstances">DescribeDBInstances</a> interface to query the Instance ID.</div><br> |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47098#crossaccountsettings) |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="publicmysqlsettings"></span>
### PublicMySQLSettings


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Host |String |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |4 |The port number of the self\-managed instance. |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|SSLSettings |Object of [SSLSettings](https://docs.byteplus.com/en/docs/57/47098#sslsettings) |```JSON```<br>```{```<br>```    "EnableSSL": true,```<br>```    "Cert":"-----BEGIN CERTIFICATE----- ...... -----END CERTIFICATE-----"```<br>```}```<br><br><br> |Instance encryption information. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="sslsettings"></span>
### SSLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|EnableSSL |Boolean |false |Whether to enable SSL encryption connection method. The values are as follows:<br><br><br>* `true`: Indicates that SSL encryption is enabled.<br><br>* `false`: Indicates that SSL encryption is not enabled. |
|Cert |String |\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\- ...... \-\-\-\-\-END CERTIFICATE\-\-\-\-\- |CA certificate content.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>EnableSSL</code> is set to <code>true</code>, this parameter is required.</div><br> |


<span id="publicpostgresqlsettings"></span>
### PublicPostgreSQLSettings


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Host |String |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |4 |The port number of the self\-managed instance. |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|DBName |String |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|ExtraParams |Array of [ExtraParam](https://docs.byteplus.com/en/docs/57/47098#extraparam) | | |


<span id="publicmongosettings"></span>
### PublicMongoSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br><br><br> |The region of the instance. |
|DeployType |String |Standalone |The type of MongoDB instance. The values are as follows:<br><br><br>* `Standalone`: Indicates a single node.<br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|PullMethod |String |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |
|Endpoints |Array of String |192.168.\*\*\*.\*\*\*:4 |Mongo address in the format of `host:port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |test\*\*\*\* |mongos database account. |
|Password |String |test\*\*\*\* |Database password of mongos. |
|MongoAuthSourceDB |String |admin |Authentication database name for mongos. |
|Shards |Array of [MongoShardSetting](https://docs.byteplus.com/en/docs/57/47098#mongoshardsetting) |```JSON```<br>```{```<br>```    "Address": "192.168.0.1:27019,192.168.0.1:27020",```<br>```    "Username": "test****",```<br>```    "Password": "test****",```<br>```    "AuthDb": "admin"```<br>```}```<br> |Shard address information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If used as a return parameter, the relevant information about the parameter is not returned.</div><br> |
|UseNewShardingDatasource |Boolean |true |Whether to select the new version of shard access method, with the following optional values:<br><br><br>* `false`: Indicates that the new shard access method is not used.<br><br>* `true`: Indicates that the new shard method is used. The default value is the shard set scenario for the deployment type. |


<span id="mongoshardsetting"></span>
### MongoShardSetting


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Address |String |192.168.0.1:27019,192.168.0.1:27020 |Shard address, such as `IP:Port` or `Domain:Port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|AuthDb |String |admin |Account verification database. |


<span id="publicelasticsearchsettings"></span>
### PublicElasticSearchSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Endpoints |Array of String |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="publicredissettings"></span>
### PublicRedisSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Host |String |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |4 |The port number of the self\-managed instance. |
|Username |String |test\*\*\*\* |Database account. |
|Password |String |test\*\*\*\* |Database account password. |
|DBName |String |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="builtinkafkasettings"></span>
### BuiltinKafkaSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Brokers |Array of String |&nbsp;<br><br>```JSON```<br>```[```<br>```     "100.67.158.158:9092",```<br>```     "100.67.158.158:9192",```<br>```     "100.67.158.158:9292",```<br>```     "100.67.158.158:9392",```<br>```     "100.67.158.158:9492"```<br>```]```<br> |The IP address and port number of the Broker, in the format of `host:port`. |
|Topic |String |6f2fd63c0ea947b280877f5d2a\*\*\*\*\*\* |Kafka's Topic ID. |


<span id="expressmongosettings"></span>
### ExpressMongoSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|DeployType |String |ShardedCluster |The instance type of the instance. The values are as follows:<br><br><br>* `Standalone`: Indicates a single node.<br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|PullMethod |String |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47098#privatenetworksettings) |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|Endpoints |Array of String |192.168.\*\*\*.\*\*\*:4 |Mongo address in the format of `host:port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |test\*\*\*\* |mongos database account. |
|Password |String |test\*\*\*\* |Database password of mongos. |
|MongoAuthSourceDB |String |admin |Authentication database name for mongos. |
|Shards |Array of [MongoShardSetting](https://docs.byteplus.com/en/docs/57/47098#mongoshardsetting) |```JSON```<br>```{```<br>```    "Address": "192.168.0.1:27019,192.168.0.1:27020",```<br>```    "Username": "test****",```<br>```    "Password": "test****",```<br>```    "AuthDb": "admin"```<br>```}```<br> |Shard address information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If used as a return parameter, the relevant information about the parameter is not returned.</div><br> |
|UseNewShardingDatasource |Boolean |true |Whether to select the new version of shard access method, with the following optional values:<br><br><br>* `false`: Indicates that the new shard access method is not used.<br><br>* `true`: Indicates that the new shard method is used. The default value is the shard set scenario for the deployment type. |


<span id="privatenetworksettings"></span>
### PrivateNetworkSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|VPCId |String |vpc\-bp1opxu1zkhn00gz\*\*\*\* |VPC ID. The VPC ID values are as follows, based on the connection method of the virtual private cloud:<br><br><br>* Direct connect: Set any VPC ID of the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Set the VPC ID bound to the VPN gateway when achieving data connectivity through VPN. |
|SubnetId |String |subnet\-bpkdt37pq72zv\*\*\*\* |Subnet ID within the VPC ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The subnet CIDR block must be added to the allowlist or security group rule of the target database.</div><br> |


<span id="expressmysqlsettings"></span>
### ExpressMySQLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Host |String |192.168.\*\*\* *.\*\*\**  |The host address of the MySQL instance connected over express network. |
|Port |Integer |4 |The port of the MySQL instance connected over express network. |
|Username |String |test\*\*\* |Database account of MySQL instance connected over express network. |
|Password |String |Admin@\*\*\* |Database account password of MySQL instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47098#privatenetworksettings) |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="expresspostgresqlsettings"></span>
### ExpressPostgreSQLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Host |String |192.168.\*\*\* *.\*\*\**  |The host address of the PostgreSQL instance connected over express network. |
|Port |Integer |4 |The port of the Express_Kafka instance connected over express network. |
|Username |String |test\*\*\* |Database account of PostgreSQL instance connected over express network. |
|Password |String |Admin@\*\*\* |Database account password of PostgreSQL instance connected over express network. |
|DBName |String |test\*\*\*\* |Database name. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47098#privatenetworksettings) |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|ExtraParams |Array of [ExtraParam](https://docs.byteplus.com/en/docs/57/47098#extraparam) | | |


<span id="expressredissettings"></span>
### ExpressRedisSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ArchType |String |Standalone |Architecture type. The values are as follows:<br><br><br>* `Standalone`: `Standalone edition`.<br><br>* `Cluster`: `Cluster edition`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the cluster of the Redis connected over express network instance has a proxy service, the <code>ArchType</code> must be set to <code>Standalone</code>.</div><br> |
|Host |String |192.168.\*\*\*.\*\*\* |The host address of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the parameter <code>ArchType</code> is set to <code>Standalone</code>.</div><br> |
|Port |Integer |4 |The port of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter must be set when <code>ArchType</code> is set to <code>Standalone</code>.</div><br> |
|Endpoints |Array of String |10.10.10.10:3717 |Enter the` IP: port` of the primary nodes for each shard of the Cache for Redis cluster in the private network connected via the dedicated line, separated by commas. For example: `ip1:port1,ip2:port2,ip3:port3`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the parameter <code>ArchType</code> is set to <code>Cluster</code>.</div><br> |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47098#privatenetworksettings) |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|Username |String |test\*\*\* |Database account of the Redis instance connected over express network. |
|Password |String |Admin@\*\*\* |Database account password of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the parameter <code>ArchType</code> is set to <code>Cluster</code>, passwords for multiple shards must be consistent; otherwise, connection can not be established.</div><br> |


<span id="expresselasticsearchsettings"></span>
### ExpressElasticSearchSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Endpoints |Array of String |[192.168.\*\*\* *.\*\*\** ] |The host address of ElasticSearch connected over express network. |
|Username |String |test\*\*\* |Database account of the Elasticsearch instance connected over express network. |
|Password |String |Admin@\*\*\* |Database account password of ElasticSearch instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47098#privatenetworksettings) |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="expresskafkasettings"></span>
### ExpressKafkaSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|BrokerEndpoints |Array of String |[10.1.\*\*\*.\*\*\*:9093] |The IP address and port number of the Kafka connected over express network instance Broker, in the format of `host1:port1`. If there are multiple Brokers, separate them with commas (,). |
|AuthType |String |plain |Authentication method. The default value is `plain`. |
|Username |String |test\*\*\* |Database account of the Kafka instance connected over express network. |
|Password |String |Admin@\*\*\* |Database account password of the Kafka instance connected over express network. |
|Topic |String |dts_sydtest |Topic information of the Kafka instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47098#privatenetworksettings) |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47098#regionsettings) |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="solutionsettings"></span>
### SolutionSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SolutionType |String |MySQL2MySQL |Task type. The values are as follows:<br><br><br>* `MySQL2MySQL`: Indicates a migration or synchronization task from MySQL to MySQL.<br><br>* `MySQL2ES`: Indicates a synchronization task from MySQL to Elasticsearch.<br><br>* `MySQL2Kafka`: Indicates a subscription task from MySQL to Kafka.<br><br>* `MySQL2RocketMQ`: Indicates a subscription task from MySQL to RocketMQ.<br><br>* `Pg2pg`: Indicates a migration or synchronization task from PostgreSQL to PostgreSQL.<br><br>* `PG2Kafka`: Indicates a subscription task from PostgreSQL to Kafka.<br><br>* `Pg2rocketmq`: Indicates a subscription task from PostgreSQL to RocketMQ.<br><br>* `Mongo2Mongo`: Indicates a migration or synchronization task from MongoDB to MongoDB.<br><br>* `Redis2Redis`: Indicates a migration or synchronization task from Redis to Redis.<br><br>* `MySQL2MySQLMigrationAssessment`: Indicates a migration evaluation task from MySQL to MySQL.<br><br>* `MySQL2MySQLDataValidation`: Indicates a verification task from MySQL to MySQL.<br><br>* `PG2PGDataValidation`: Indicates a verification task from PostgreSQL to PostgreSQL.<br><br>* `Mongo2MongoDataValidation`: Indicates a verification task from MongoDB to MongoDB.<br><br>* `Mongo2RocketMQ`: Indicates a migration or synchronization task from MongoDB to RocketMQ.<br><br>* `Redis2RocketMQ`: Indicates a migration or synchronization task from Redis to RocketMQ.<br><br>* `MSSQL2MSSQL`: Indicates a migration task from SQL Server to SQL Server.<br><br>* `MySQL2MySQLRowCompare`: Indicates a full validation task from MySQL to MySQL.<br><br>* `MySQL2MySQLIncrDataValidation`: Indicates an increment validation task from MySQL to MySQL.<br><br>* `MySQL2MySQLRowCountCompare`: Indicates a row verification task from MySQL to MySQL.<br><br>* `MySQL2MySQLMetaCompare`: Indicates a schema verification task from MySQL to MySQL.<br><br>* `PG2PGRowCompare`: Indicates a full data verification task from PostgreSQL to PostgreSQL.<br><br>* `Mongo2MongoRowCompare`: Indicates a full data verification task from MongoDB to MongoDB.<br><br>* `Mongo2MongoPkCompare`: Indicates a primary key validation task from MongoDB to MongoDB.<br><br>* `Mongo2MongoIncrDataValidation`: Indicates an increment validation task from MongoDB to MongoDB.<br><br>* `Mongo2MongoRowCountCompare`: Indicates a row verification task from MongoDB to MongoDB.<br><br>* `Redis2RedisRowCompare`: Indicates a full validation task from Redis to Redis.<br><br>* `MSSQL2MSSQLRowCompare`: Indicates a full validation task from SQL Server to SQL Server.<br><br>* `MSSQL2MSSQLRowCountCompare`: Indicates a row verification task from SQL Server to SQL Server.<br><br>* `Milvus2Milvus`: Indicates a migration or synchronization task from Milvus to Milvus. |
|AutoStart |Boolean |false |Whether to automatically start the task after task creation. The values are as follows:<br><br><br>* `true`: indicates automatic start of the task.<br><br>* `false`: (default) indicates the task does not start automatically and requires manual start. |
|MySQL2MySQLSettings |Object of [MySQL2MySQLSettings](https://docs.byteplus.com/en/docs/57/47098#mysql2mysqlsettings) |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```    },```<br>```    "EnableForeignKeyChecks": false,```<br>```    "EnableFullIncr": true,```<br>```    "EnableFullTrxPartitionByChunk": false,```<br>```    "EnableTriggerPreMigration": false,```<br>```    "EnableTrxRewrite": false,```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true,```<br>```        "Snapshot": false```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true,```<br>```        "Statements": [```<br>```            "StmtDDLAll",```<br>```            "StmtDMLDelete",```<br>```            "StmtDMLInsert",```<br>```            "StmtDMLUpdate"```<br>```        ]```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "test",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta",```<br>```                            "Incr",```<br>```                            "Full"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableOverride",```<br>```                        "SetObjectTransType": true```<br>```                    },```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "View",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Function",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Procedure",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Trigger",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Event",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectMappingSetting": {```<br>```                "LastWriteWinsKey": "",```<br>```                "ObjectTransTypes": [```<br>```                    "Meta",```<br>```                    "Full",```<br>```                    "Incr"```<br>```                ],```<br>```                "PolicyForKeyConflict": "TableOverride",```<br>```                "SetObjectTransType": true```<br>```            },```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "test"```<br>```        }```<br>```    ],```<br>```    "PolicyForPrimaryKeyConflict": "Override"```<br>```}```<br> |When the `SolutionType` is set to `MySQL2MySQL`, it refers to the parameter configuration for the migration or synchronization from source instances of MySQL to target instances of MySQL. This parameter is required. |
|MySQL2ESSettings |Object of [MySQL2ESSettings](https://docs.byteplus.com/en/docs/57/47098#mysql2essettings) |```JSON```<br>```{```<br>```    "ESExtraArgs": {```<br>```        "Analyzer": "",```<br>```        "CustomIndexType": "",```<br>```        "IdxNameRule": "DBAndTable",```<br>```        "InsertMode": "<UNSET>",```<br>```        "ReplicaNum": 1,```<br>```        "RetryTimes": 0,```<br>```        "ShardNum": 5,```<br>```        "TZ": ""```<br>```    },```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true,```<br>```        "Statements": [```<br>```            "StmtDMLDelete",```<br>```            "StmtDMLInsert",```<br>```            "StmtDMLUpdate"```<br>```        ]```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "testdb_bak",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "testdb_bak_auth_operation",```<br>```                    "ObjectMappingSetting": {```<br>```                        "ESMetaMappingSetting": {```<br>```                            "EnableRouting": false,```<br>```                            "TypeName": ""```<br>```                        },```<br>```                        "LastWriteWinsKey": "",```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "auth_operation"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "testdb_bak"```<br>```        }```<br>```    ],```<br>```    "PolicyForPrimaryKeyConflict": "Override"```<br>```}```<br><br><br> |When the `SolutionType` is set to `MySQL2ES`, it refers to the parameter configuration for the synchronization from source instances of Elasticsearch to target instances of MySQL. This parameter is required. |
|MySQL2KafkaSettings |Object of [MySQL2KafkaSettings](https://docs.byteplus.com/en/docs/57/47098#mysql2kafkasettings) |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "EnableFullIncr": true,```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 7200```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true,```<br>```        "Statements": [```<br>```            "StmtDMLInsert",```<br>```            "StmtDMLUpdate",```<br>```            "StmtDMLDelete",```<br>```            "StmtDDLAll"```<br>```        ]```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "huahua",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "auth_operation",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta",```<br>```                            "Incr",```<br>```                            "Full"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": true```<br>```                    },```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "auth_operation"```<br>```                }```<br>```            ],```<br>```            "ObjectMappingSetting": {```<br>```                "LastWriteWinsKey": "",```<br>```                "ObjectTransTypes": [```<br>```                    "Full",```<br>```                    "Incr",```<br>```                    "Meta"```<br>```                ],```<br>```                "PolicyForKeyConflict": "TableNone",```<br>```                "SetObjectTransType": true```<br>```            },```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "huahua"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "PartitionPolicy": "Table",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "",```<br>```        "VPCSubnetId": ""```<br>```    }```<br>```}```<br><br><br> |When the value of `SolutionType` is `MySQL2Kafka`, it refers to the parameter configuration for subscribing source instances of MySQL to Kafka, and this parameter is required. |
|MySQL2RocketMQSettings |Object of [MySQL2RocketMQSettings](https://docs.byteplus.com/en/docs/57/47098#mysql2rocketmqsettings) |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": false```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "database1",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "database1"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "PartitionPolicy": "Table",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "",```<br>```        "VPCSubnetId": ""```<br>```    }```<br>```}```<br><br><br> |When the value of `SolutionType` is `MySQL2RocketM`, it refers to the parameter configuration for subscribing source instances of MySQL to Message Queue for RocketMQ. This parameter is required. |
|PG2PGSettings |Object of [PG2PGSettings](https://docs.byteplus.com/en/docs/57/47098#pg2pgsettings) |```JSON```<br>```{```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "0",```<br>```            "DestObjName": "0"```<br>```        },```<br>```        {```<br>```            "ObjectType": "Table",```<br>```            "SrcObjName": "1",```<br>```            "DestObjName": "1"```<br>```        },```<br>```        {```<br>```            "ObjectType": "View",```<br>```            "SrcObjName": "2",```<br>```            "DestObjName": "2"```<br>```        },```<br>```        {```<br>```            "ObjectType": "PostSequence",```<br>```            "SrcObjName": "3",```<br>```            "DestObjName": "3"```<br>```        }```<br>```    ],```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": "true"```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableMeta": "true"```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableMeta": "true"```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 7200```<br>```    }```<br>```}```<br> |When `SolutionType` is set to `PG2PG`, it refers to the parameter configuration for migrating source instances of PostgreSQL to target instances of PostgreSQL, and this parameter is required. |
|PG2KafkaSettings |Object of [PG2KafkaSettings](https://docs.byteplus.com/en/docs/57/47098#pg2kafkasettings) |```JSON```<br>```{```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 7200```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": false```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": false```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "public",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "public"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "vpc-3ez4xswg5j94w72200ry****",```<br>```        "VPCSubnetId": "subnet-3ez4xts0nc4qo72200r******"```<br>```    }```<br>```}```<br> |When the value of `SolutionType` is `PG2Kafka`, it refers to the parameter configuration for subscribing source instances of PostgreSQL to Kafka, and this parameter is required. |
|PG2RocketMQSettings |Object of [PG2RocketMQSettings](https://docs.byteplus.com/en/docs/57/47098#pg2rocketmqsettings) |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": false```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": false```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "public",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "public"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "PartitionPolicy": "Table",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "",```<br>```        "VPCSubnetId": ""```<br>```    }```<br>```}```<br><br><br> |When the value of` SolutionType` is `PG2RocketMQ`, it refers to the parameter configuration for subscribing source instances of PostgreSQL to Message Queue for RocketMQ. This parameter is required. |
|Mongo2MongoSettings |Object of [Mongo2MongoSettings](https://docs.byteplus.com/en/docs/57/47098#mongo2mongosettings) |```JSON```<br>```{```<br>```    "TaskName": "test",```<br>```    "TrafficSpec": "Standard",```<br>```    "ProjectName": "default",```<br>```    "Tags": [```<br>``````<br>```    ],```<br>```    "CreateBackwardSyncTask": false,```<br>```    "ChargeConfig": {```<br>```        "ChargeType": "PostPaid",```<br>```        "Times": 1```<br>```    },```<br>```    "SrcConfig": {```<br>```        "EndpointType": "Public_Mongo",```<br>```        "PublicMongoSettings": {```<br>```            "RegionSettings": {```<br>```                "Region": "×××××××××"```<br>```            },```<br>```            "DeployType": "ShardedCluster",```<br>```            "PullMethod": "Oplog",```<br>```            "Endpoints": [```<br>```                "192.168..***.***:27***"```<br>```            ],```<br>```            "MongoAuthSourceDB": "admin",```<br>```            "Username": "root",```<br>```            "Password": "admin",```<br>```            "Shards": [```<br>```                {```<br>```                    "Username": "root",```<br>```                    "Password": "admin",```<br>```                    "Address": "192.168.***.***:27***,192.168.***.***:27***",```<br>```                    "AuthDb": "admin"```<br>```                },```<br>```                {```<br>```                    "Address": "192.168.***.***:27***,192.168.***.***:27***",```<br>```                    "AuthDb": "admin",```<br>```                    "Username": "root",```<br>```                    "Password": "admin"```<br>```                }```<br>```            ],```<br>```            "UseNewShardingDatasource": true```<br>```        }```<br>```    },```<br>```    "DestConfig": {```<br>```        "EndpointType": "Volc_Mongo",```<br>```        "VolcMongoSettings": {```<br>```            "RegionSettings": {```<br>```                "Region": "×××××××××"```<br>```            },```<br>```            "DeployType": "ShardedCluster",```<br>```            "PullMethod": "None",```<br>```            "DBInstanceId": "mongo-shard-××××××××",```<br>```            "Username": "root",```<br>```            "Password": "admin",```<br>```            "UseNewShardingDatasource": true```<br>```        }```<br>```    },```<br>```    "SolutionSettings": {```<br>```        "SolutionType": "Mongo2Mongo",```<br>```        "Mongo2MongoSettings": {```<br>```            "TaskRunType": [```<br>```                "Incr",```<br>```                "Full",```<br>```                "Meta"```<br>```            ],```<br>```            "PolicyForMongoPrimaryKeyConflict": "Override",```<br>```            "ObjectMappings": [```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "test",```<br>```                    "DestObjName": "test",```<br>```                    "MappingList": [```<br>```                        {```<br>```                            "ObjectType": "Table",```<br>```                            "SrcObjName": "*",```<br>```                            "DestObjName": "*"```<br>```                        }```<br>```                    ]```<br>```                }```<br>```            ],```<br>```            "ErrorBehaviorSettings": {```<br>```                "MaxRetrySeconds": 600```<br>```            },```<br>```            "FullTransmissionSettings": {```<br>```                "FullSyncParalell": 8,```<br>```                "EnableFull": true```<br>```            },```<br>```            "AccountTransmissionSettings": {```<br>```                "EnableAccount": false```<br>```            },```<br>```            "MetaTransmissionSettings": {```<br>```                "EnableMeta": true```<br>```            },```<br>```            "IncrTransmissionSettings": {```<br>```                "EnableIncr": true```<br>```            }```<br>```        }```<br>```    },```<br>```    "TaskType": "DataSynchronization"```<br>```}```<br> |When `SolutionType` is set to `Mongo2Mongo`, it refers to the parameter configuration for migrating source instances of MongoDB to target instances of MongoDB, and this parameter is required. |
|Redis2RedisSettings |Object of [Redis2RedisSettings](https://docs.byteplus.com/en/docs/57/47098#redis2redissettings) |```JSON```<br>```{```<br>```    "TaskName": "rudonxxxxx-1",```<br>```    "TaskType": "DataMigration",```<br>```    "TrafficSpec": "Compact",```<br>```    "ProjectName": "default",```<br>```    "Tags": [```<br>```        {```<br>```            "Key": "key1",```<br>```            "Value": "value1"```<br>```        }```<br>```    ],```<br>```    "SrcConfig": {```<br>```        "EndpointType": "Public_Redis",```<br>```        "PublicRedisSettings": {```<br>```            "Host": "192.168.***.***",```<br>```            "Port": 4,```<br>```            "Username": "test****",```<br>```            "Password": "test****",```<br>```            "DBName": "test****",```<br>```            "RegionSettings": {```<br>```                "Region": "cn-beijing"```<br>```            }```<br>```        }```<br>```    },```<br>```    "DestConfig": {```<br>```        "EndpointType": "Volc_Redis",```<br>```        "VolcRedisSettings": {```<br>```            "RegionSettings": {```<br>```                "Region": "cn-beijing"```<br>```            },```<br>```            "DBInstanceId": "redis-cnlfe66ipof9y86qz",```<br>```            "Username": "default",```<br>```            "Password": "ASDFasdf@2020"```<br>```        }```<br>```    },```<br>```    "SolutionSettings": {```<br>```        "SolutionType": "Redis2Redis",```<br>```        "Redis2RedisSettings": {```<br>```            "ObjectMappings": [```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "0",```<br>```                    "DestObjName": "0"```<br>```                },```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "1",```<br>```                    "DestObjName": "1"```<br>```                },```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "2",```<br>```                    "DestObjName": "2"```<br>```                }```<br>```            ],```<br>```            "ErrorBehaviorSettings": {```<br>```                "MaxRetrySeconds": 7200```<br>```            },```<br>```            "FullTransmissionSettings": {```<br>```                "EnableFull": true```<br>```            },```<br>```            "IncrTransmissionSettings": {```<br>```                "EnableIncr": false```<br>```            }```<br>```        }```<br>```    },```<br>```    "ChargeConfig": {```<br>```        "ChargeType": "PostPaid"```<br>```    }```<br>```}```<br> |When `SolutionType` is set to `Redis2Redis`, it refers to the parameter configuration for migrating source instances of Redis to target instances of Redis, and this parameter is required. |
|EnableMsLvlLatency |Boolean |false |Enable or disable millisecond\-level latency monitoring. The values are as follows:<br><br><br>* `true`: (Default) Enable. When enabled, it provides high\-precision, full\-link, proactive end\-to\-end delay measurement, effectively improving monitoring stability and awareness of abnormal scenarios such as network interruptions and idle disconnections.<br><br>* `false`: Disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be set when creating the following tasks:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Synchronization task</div><br><br><br>   * <div data-tips="true" data-tips-type="default">MySQL type</div><br><br><br>   * <div data-tips="true" data-tips-type="default">MongoDB type</div><br><br><br>* <div data-tips="true" data-tips-type="default">Subscription task</div><br><br><br>   * <div data-tips="true" data-tips-type="default">PostgreSQL subscription to Kafka</div><br><br><br>   * <div data-tips="true" data-tips-type="default">PostgreSQL subscription to RocketMQ</div><br><br><br>   * <div data-tips="true" data-tips-type="default">AIDAP subscription to RocketMQ</div><br> |
|Tos2MySQLReplaySettings |Object of [Tos2MySQLReplaySettings](https://docs.byteplus.com/en/docs/57/47098#tos2mysqlreplaysettings) | | |


<span id="mysql2mysqlsettings"></span>
### MySQL2MySQLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|EnableForeignKeyChecks |Boolean |false |Select whether to enable foreign key check as needed. When enabled, the tool supports migrating cascading updates and deletes of foreign keys from the source, ensuring data integrity and consistency throughout the migration. The values are as follows:<br><br><br>* `true`: Indicates that foreign key check is enabled.<br><br>* `false`: (default) Indicates that foreign key check is disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter supports configuration only when <code>TaskType</code> is <code>DataMigration</code>.</div><br> |
|AccountTransmissionSettings |Object of [AccountTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#accounttransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableAccount": true```<br>```}```<br><br><br> |Migrates specified non\-system accounts and their associated permissions from the source database to the target database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter supports configuration only when <code>TaskType</code> is <code>DataMigration</code> or <code>DataSynchronization</code>.</div><br> |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br><br><br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |
|MySQLPosition |Object of [MySQLPosition](https://docs.byteplus.com/en/docs/57/47098#mysqlposition) |```JSON```<br>```{```<br>```"Gtid": "3e11fa47-71ca-11e1-9e33-c80aa9429562:58",```<br>```"Gset":"f76eb90f-82a2-11e5-a162-7ca23e9126c5:3",```<br>```"Timestamp":1679642652```<br>```}```<br> |Set to pull Binlog logs from a specified position or timestamp.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>TaskType</code> is set to <code>DataSynchronization</code>, this configuration parameter is not supported during full initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When this parameter is not set, it defaults to the earliest point in time that the system can recognize.</div><br> |
|PolicyForPrimaryKeyConflict |String |Override |Primary key conflict handling. The processing method when a row with the same primary key value already exists in the target database. The values are as follows:<br><br><br>* `ThrowError`: Indicates abort on conflict. An error is reported during the pre\-check, and the relevant data needs to be modified manually. Otherwise, the synchronization task can not be started.<br><br>* `Ignore`: Indicates ignore on conflict. During the pre\-check, rows with the same primary key value in the target database will be skipped, and the synchronization task can be started normally.<br><br>* `Override`: Overwrite on conflict. Use the source database data to overwrite the target database data. The synchronization task can be started normally.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the value is <code>Ignore</code>, data inconsistency may occur, which may bring risks to the business. Choose carefully.</div><br> |
|AccountMapping |Array of [AccountMapping](https://docs.byteplus.com/en/docs/57/47098#accountmapping) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Account": "test****",```<br>```    "ResetPassword": "true",```<br>```    "Password": "*Test****"```<br>```}```<br> |The database account information to be migrated.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter supports configuration only when <code>TaskType</code> is <code>DataMigration</code> or <code>DataSynchronization</code>.</div><br> |
|EnableTrxRewrite |Boolean |true |Select whether to enable transaction merging when transmitting data. Enabling transaction merging optimizes transmission tasks by combining multiple individual transactions, improving overall efficiency and performance while ensuring data consistency. When data transmission occurs frequently with large volumes, enabling transaction merging enhances the transmission efficiency.<br><br><br>* `true`: Indicates that transaction merging is enabled.<br><br>* `false`: (Default) Indicates that transaction merging is not enabled. |


<span id="objectmapping"></span>
### ObjectMapping


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ObjectType |String |Function |Object type. The values are as follows:<br><br><br>* `Database`: indicates a database.<br><br>* `Table`: indicates a table.<br><br>* `View`: indicates a view.<br><br>* `Column`: Indicates the `column`.<br><br>* `Function`: Indicates the `function`.<br><br>* `Procedure`: Indicates the `procedure`.<br><br>* `Trigger`: Indicates the `trigger`.<br><br>* `Type`: Indicates the `type`.<br><br>* `Domain`: Indicates the `domain`.<br><br>* `Sequence`: Indicates the `sequence`.<br><br>* `Rule`: Indicates the `rule`.<br><br>* `Operator`: Indicates the `operator`.<br><br>* `Aggregate`: Indicates the `aggregate`.<br><br>* `Extension`: Indicates an extension.<br><br>* `Constraint`: Indicates a constraint.<br><br>* `PostSequence`: Indicates a PostgreSQL sequence.<br><br>* `Schema`: Indicates a mode.<br><br>* `Event`: Indicates an event.<br><br>* `DomainConstraint`: Indicates a domain constraint. |
|SrcObjName |String |ceshi\*\*\*\* |Source object name. |
|DestObjName |String |test\*\*\*\* |Target object name. |
|MappingList |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Transmission task object. |
|ObjectMappingSetting |Object of [ObjectMappingSetting](https://docs.byteplus.com/en/docs/57/47098#objectmappingsetting) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ESMetaMappingSetting": {```<br>```        "PidCol": [```<br>```            "id",```<br>```            "name"```<br>```        ],```<br>```        "EnableRouting": true,```<br>```        "RoutingCol": [```<br>```            "id"```<br>```        ]```<br>```    }```<br>```}```<br> |Additional parameter information that needs to be configured when synchronizing data to Elasticsearch. |


<span id="objectmappingsetting"></span>
### ObjectMappingSetting


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ESMetaMappingSetting |Object of [ESMetaMappingSetting](https://docs.byteplus.com/en/docs/57/47098#esmetamappingsetting) |```JSON```<br>```{```<br>```    "PidCol": [```<br>```        "id",```<br>```        "name"```<br>```    ],```<br>```    "EnableRouting": true,```<br>```    "RoutingCol": [```<br>```        "id"```<br>```    ]```<br>```}```<br> |Structure mapping parameters of Elasticsearch. |


<span id="esmetamappingsetting"></span>
### ESMetaMappingSetting


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|PidCol |Array of String |["id", "name"] |Primary key (_id) value. If this parameter is not set, the default is the column of the primary key. |
|EnableRouting |Boolean |EnableRouting |Whether to enable Routing. The values are as follows:<br><br><br>* `true`: Indicates that Routing is enabled.<br><br>* `false`: Indicates that Routing is not enabled. |
|RoutingCol |Array of String |["id"] |The value of `_routing`. This parameter is required when `EnableRouting` is set to `true`. |


<span id="accounttransmissionsettings"></span>
### AccountTransmissionSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|EnableAccount |Boolean |false |Whether to enable user migration. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `false`: Indicates disabled. |


<span id="metatransmissionsettings"></span>
### MetaTransmissionSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|EnableMeta |Boolean |true |Whether to enable the migration or subscription of database and table structures. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `false`: Indicates disabled. |
|DisablePostMeta |Boolean |true |When you select schema migration/schema initialization as the PostgreSQL database migration/synchronization type, DTS will automatically migrate/synchronize the post\-schema after incremental migration/synchronization concludes. Alternatively, you can choose to skip post\-schema migration/synchronization, meaning DTS will not migrate/synchronize the post\-schema.<br><br>PostgreSQL database post\-schema synchronization and migration objects include ordinary trigger, event trigger, RULE, exclusive constraint, foreign key constraint, check constraint, Domain constraint, and Sequence value setting.<br><br>Whether to skip PostgreSQL post\-schema migration or post\-schema synchronization. The values are as follows:<br><br><br>* `true`: Indicates skipping PostgreSQL post\-schema migration or post\-schema synchronization.<br><br>* `false`: Indicates not skipping PostgreSQL post\-schema migration or post\-schema synchronization. |


<span id="fulltransmissionsettings"></span>
### FullTransmissionSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|EnableFull |Boolean |true |Whether to enable full migration, full subscription, or full initialization. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `False`: indicates disabled (default value). |
|Snapshot |Boolean |true |Whether to enable full data consistency migration. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `False`: indicates disabled (default value). |
|ExtraConditions |Array of [FullExtraCondition](https://docs.byteplus.com/en/docs/57/47098#fullextracondition) |```JSON```<br>```{```<br>```    "Db": "TestName",```<br>```    "Table": "TableName",```<br>```    "WhereSql": "id = 5"```<br>```}```<br> |Full filter condition. |
|RPSLimit |Integer |100,000 |Rows migrated or synchronized per second. The value range is 1 to 100,000, and the default value is 100,000. |
|BPSLimit |Integer |25000 |Data volume migrated or synchronized per second. The value range is 1 to 25,000 (KB), and the default value is 25,000. |
|FullSyncParalell |Integer |8 |Concurrency of the migration or synchronization task. The default value is 8, and the valid range is 1 to 64. |


<span id="fullextracondition"></span>
### FullExtraCondition


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Db |String |TestName |The database name to be filtered. |
|Table |String |TableName |Table names to be filtered. |
|WhereSql |String |id = 5 |Filtered SQL statements. |


<span id="incrtransmissionsettings"></span>
### IncrTransmissionSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|EnableIncr |Boolean |true |Whether to enable incremental migration, incremental subscription, or incremental synchronization. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `False`: indicates disabled (default value).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|Statements |Array of String |&nbsp;<br><br>```JSON```<br>```[```<br>```     "StmtDDLAll",```<br>```     "StmtDMLDelete",```<br>```      "StmtDMLUpdate",```<br>```     "StmtDMLInsert"```<br>```]```<br> |The operation statements to be transmitted. The values are as follows:<br><br><br>* `StmtDMLInsert`<br><br>* `StmtDMLUpdate`<br><br>* `StmtDMLDelete`<br><br>* `StmtDDLAll`<br><br>* `StmtDDLAlterTable`<br><br>* `StmtDDLAlterView`<br><br>* `StmtDDLCreateFunction`<br><br>* `StmtDDLCreateIndex`<br><br>* `StmtDDLCreateProcedure`<br><br>* `StmtDDLCreateTable`<br><br>* `StmtDDLCreateView`<br><br>* `StmtDDLDropIndex`<br><br>* `StmtDDLDropTable`<br><br>* `StmtDDLDropFunction`<br><br>* `StmtDDLDropProcedure`<br><br>* `StmtDDLTruncateTable`<br><br>* `StmtDDLRenameTable`<br><br>* `StmtDDLDropView` |


<span id="etlsettings"></span>
### ETLSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Script |String |```json```<br>```(defn        desensitization        []```<br>```                (dts/match-table        "user"        (dts/map-column        'id_card        str/md5)))```<br> |Script for streaming data ETL. For syntax information about script dependencies, refer to [DSL syntax](https://docs.byteplus.com/en/docs/DTS/dsl_syntax). |


<span id="errorbehaviorsettings"></span>
### ErrorBehaviorSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|MaxRetrySeconds |Integer |600 |Maximum error retry time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |


<span id="mysqlposition"></span>
### MySQLPosition


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Gtid |String |3e11fa47\-71ca\-11e1\-9e33\-c80aa9429562:58 |Indicates that the Binlogs are pulled from the specified GTID in the format of `source_id:transaction_id`. |
|Gset |String |f76eb90f\-82a2\-11e5\-a162\-7ca23e9126c5:3 |Indicates that the Binlog logs are pulled from the specified GTID_EXECUTED, in the format of `source_id:transaction_id`. When there are multiple GTID_EXECUTEDs, they can be separated by commas (,).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For how to obtain the instance's GTID_EXECUTED, refer to <a href="https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance">How to obtain the GTID_EXECUTED of the instance</a>.</div><br> |
|Timestamp |Long |1679642652 |Indicates that the Binlog logs are pulled from the specified timestamp. |


<span id="accountmapping"></span>
### AccountMapping


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Account |String |test\*\*\*\* |The account name to be migrated. |
|ResetPassword |Boolean |true |Whether to reset the password. The values are as follows:<br><br><br>* `true`: Indicates resetting to a new password.<br><br>* `false`: Indicates not resetting to a new password. Default value. |
|Password |String |\*Test\*\*\*\* |The new password of the account to be migrated. |


<span id="mysql2essettings"></span>
### MySQL2ESSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "huahua",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectType": "Table",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "huahua"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |Streaming data ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |
|ESExtraArgs |Object of [ESExtraArgs](https://docs.byteplus.com/en/docs/57/47098#esextraargs) |```JSON```<br>```{```<br>```    "IdxNameRule": "Table",```<br>```    "ShardNum": 3,```<br>```    "ReplicaNum": 1,```<br>```    "TZ": "UTC +08:00",```<br>```    "RetryTimes": 600,```<br>```    "Analyzer": "standard",```<br>```    "InsertMode": "Replace"```<br>```}```<br> |Parameter information when synchronizing to Elasticsearch. |
|PolicyForPrimaryKeyConflict |String |ThrowError |Primary key conflict handling. The processing method when a row with the same primary key value already exists in the target database. The values are as follows:<br><br><br>* `ThrowError`: Indicates abort on conflict. An error is reported during the pre\-check, and the relevant data needs to be modified manually. Otherwise, the synchronization task can not be started.<br><br>* `Ignore`: Indicates ignore on conflict. During the pre\-check, rows with the same primary key value in the target database will be skipped, and the synchronization task can be started normally.<br><br>* `Override`: Overwrite on conflict. Use the source database data to overwrite the target database data. The synchronization task can be started normally.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When set to <code>Ignore</code>, it may cause data inconsistency and pose risks to business. Select with caution.</div><br> |


<span id="esextraargs"></span>
### ESExtraArgs


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|IdxNameRule |String |Table |Index concatenation rule<br><br><br>* `Table`: Indicates the table name concatenation method is used.<br><br>* `DBAndTable`: Indicates the database name + table name concatenation method is used. |
|ShardNum |Long |3 |Number of shard(s) |
|ReplicaNum |Long |1 |Number of copies. |
|TZ |String |UTC +08:00 |Time zone. Supports UTC\-12:00 to +13:00. The default value is the time zone of the Region. |
|RetryTimes |Long |7200 |Error retry time. |
|Analyzer |String |standard |The supported analyzer. |
|InsertMode |String |Replace |Insert in the source end. The values are as follows:<br><br><br>* `Replace`: Indicates that when a corresponding index does not exist on the target end, a new data entry will be inserted; when a corresponding index does exist, the corresponding index will be updated.<br><br>* `Update`: Indicates that when a corresponding index does not exist on the target end, it will be skipped. When a corresponding index exists on the target end, the corresponding data will be updated. |


<span id="mysql2kafkasettings"></span>
### MySQL2KafkaSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47098#subscriptionsettings) |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "AttachPoints.1.SubnetId=subnet-2fexiqjlgjif45oxruvso****&AttachPoints.2.SubnetId=subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": false,```<br>```    "SubscribePartBeforeImage": false```<br>```}```<br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|MySQLPosition |Object of [MySQLPosition](https://docs.byteplus.com/en/docs/57/47098#mysqlposition) |```JSON```<br>```{```<br>```    "Gtid": "3e11fa47-71ca-11e1-9e33-c80aa9429562:58",```<br>```    "Gset": "f76eb90f-82a2-11e5-a162-7ca23e9126c5:3",```<br>```    "Timestamp": 1679642652```<br>```}```<br> |Set to pull Binlog logs from a specified position or timestamp. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter configuration is not supported during full initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When this parameter is not set, it defaults to the earliest point in time that the system can recognize.</div><br> |


<span id="subscriptionsettings"></span>
### SubscriptionSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Protocol |String |Volc |The subscription format. The values are as follows:<br><br><br>* `Volc`: Indicates BytePlus Proto.<br><br>* `Canal`: Indicates Canal Proto.<br><br>* `CanalJSON`: Indicates Canal JSON.<br><br>* `Avro`: Indicates the Avro format.<br><br>* `DebeziumJSON`: DebeziumJSON: Indicates Debezium JSON format.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details on subscription formats, refer to <a href="https://docs.byteplus.com/en/docs/DTS/data_subscription_format">Data subscription format</a>.</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>Protocol</code> is set to <code>DebeziumJSON</code>, <code>ProgressType</code> can not be set to <code>Meta</code>.</div><br> |
|PartitionPolicy |String |P0 |The Partition reception policy for the Topic. The values are as follows:<br><br><br>* `P0`: Indicates unified delivery to Partition 0.<br><br>* `Table`: Indicates delivery to different Partitions based on the combined hash value of the database name and table name.<br><br>* `Key`: Indicates deliver to different Partitions based on the hash value of the primary key.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>Task type</code> is <code>Data subscription</code>, and <code>Endpoint type</code> is <code>Volc_Kafka</code>, this configuration is supported.</div><br> |
|VPCId |String |vpc\-bp1opxu1zkhn00gz\*\*\*\* |VPC ID. |
|VPCSubnetId |String |AttachPoints.1.SubnetId=subnet\-2fexiqjlgjif45oxruvso\*\*\*\*&AttachPoints.2.SubnetId=subnet\-7rtsu6whhle6j\*\*\*\* |Subnet ID within the VPC ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The subnet in the target VPC must have at least one available IP.</div><br> |
|EnableBeginCommitMessage |Boolean |false |Set whether to subscribe to messages by transaction as needed to ensure message consistency and completeness. The values are as follows:<br><br><br>* `true`: Indicates subscription to Begin/Commit messages.<br><br>* `false`: (Default) Indicates no subscription to Begin/Commit messages.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The following conditions must be met to configure this parameter:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><code>Protocol</code> selects <code>Volc</code>, <code>Canal</code>, <code>CanalJSON</code> or <code>Avro</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><code>EndpointType</code> selects <code>Builtin_Kafka</code>, and <code>EndpointType</code> selects <code>Volc_Kafka</code> or <code>Express_Kafka</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The <code>EndpointType</code> is set to<code> Volc_Kafka</code><strong></strong> or <code>Express_Kafka</code>, and the <code>PartitionPolicy</code> must be set to<code> P0</code>.</div><br> |
|SubscribePartBeforeImage |Boolean |true<br><br> |Set whether to subscribe to all fields as needed. The values are as follows:<br><br><br>* `true`: (Default) Indicates the before\-image of all fields is subscribed.<br><br>* `false`: Indicates that only the before\-image of changed fields is subscribed.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be configured only when the <strong>Instance type</strong> is <strong>MySQL</strong>, the middleware access method is <strong>Message Queue for Kafka</strong> or <strong>Kafka connected over express network</strong>, and the <strong>Subscription format</strong> is <strong>Canal JSON</strong>.</div><br> |


<span id="mysql2rocketmqsettings"></span>
### MySQL2RocketMQSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47098#subscriptionsettings) |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": true,```<br>```    "SubscribePartBeforeImage": true```<br>```}```<br><br><br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |Streaming data ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|MySQLPosition |Object of [MySQLPosition](https://docs.byteplus.com/en/docs/57/47098#mysqlposition) |```JSON```<br>```{```<br>```    "Gtid": "3e11fa47-71ca-11e1-9e33-c80aa9429562:58",```<br>```    "Gset": "f76eb90f-82a2-11e5-a162-7ca23e9126c5:3",```<br>```    "Timestamp": 1679642652```<br>```}```<br> |Set to pull Binlog logs from a specified position or timestamp. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter configuration is not supported during full initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When this parameter is not set, it defaults to the earliest point in time that the system can recognize.</div><br> |


<span id="pg2pgsettings"></span>
### PG2PGSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "huahua",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectType": "Table",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "huahua"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br><br><br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |
|SkipNoPermissionTables |Boolean | | |


<span id="pg2kafkasettings"></span>
### PG2KafkaSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47098#subscriptionsettings) |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": true,```<br>```    "SubscribePartBeforeImage": true```<br>```}```<br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|SkipNoPermissionTables |Boolean | | |


<span id="pg2rocketmqsettings"></span>
### PG2RocketMQSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47098#subscriptionsettings) |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": true,```<br>```    "SubscribePartBeforeImage": true```<br>```}```<br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br><br><br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br><br><br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br><br><br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|SkipNoPermissionTables |Boolean | | |
|SkipMessageOverMaxLength |Boolean | | |


<span id="mongo2mongosettings"></span>
### Mongo2MongoSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#metatransmissionsettings) |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47098#etlsettings) |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |


<span id="redis2redissettings"></span>
### Redis2RedisSettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47098#objectmapping) |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#fulltransmissionsettings) |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47098#incrtransmissionsettings) |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47098#errorbehaviorsettings) |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |


<span id="tos2mysqlreplaysettings"></span>
### Tos2MySQLReplaySettings


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Files |Array of String | | |
|ReplayType |Array of String | | |
|EndTimestamp |Long | | |
|ReplayLogType |String | | |
|StartTimestamp |Long | | |
|ReplayPressurePercentage |Integer | | |


<span id="chargedetailobject"></span>
### ChargeDetailObject


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ChargeStartTime |Long |1668569330000 |The time when the task starts billing, in milliseconds timestamp. |
|ChargeStatus |String |Normal |Task order state. The values are as follows:<br><br><br>* `Init`: The order is to be started.<br><br>* `Normal`: The order is in a normal state.<br><br>* `Overdue`: The order is overdue.<br><br>* `Unpaid`: The order is unpaid. |
|ChargeType |String |Postpaid |Billing method, with the following values:<br><br><br>* `NotEnabled`: Indicates that billing is disable.<br><br>* `PostPaid`: Indicates pay\-as\-you\-go.<br><br>* `PrePaid`: Indicates subscription. |
|OrderNo |String |Order7166450525830\*\*\*\*\*\* |Billing order ID. |
|ChargeEndTime |Long |1888569330000 |The time when the task ends billing, in milliseconds timestamp. |


<span id="chargeconfig"></span>
### ChargeConfig


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ChargeType |String |PrePaid |Billing method, with the following values:<br><br><br>* `NotEnabled`: Indicates that billing is disable.<br><br>* `PostPaid`: Indicates pay\-as\-you\-go.<br><br>* `PrePaid`: Indicates subscription. |
|Times |Integer |12 |Purchase duration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This configuration is supported when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br> |
|AutoRenew |Boolean |true |Whether to renew automatically. The values are as follows:<br><br><br>* `true`: Indicates automatic renewal.<br><br>* `false`: Indicates no automatic renewal. Default value. |
|OneStep |Boolean |false |Whether to pay immediately. The values are as follows:<br><br><br>* `true`: Indicates immediate payment.<br><br>* `false`: Indicates no immediate payment. Default value. |


<span id="progresssummary"></span>
### ProgressSummary


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Infos |Array of [ProgressSummaryInfo](https://docs.byteplus.com/en/docs/57/47098#progresssummaryinfo) |```JSON```<br>```{```<br>```    "Infos": [```<br>```        {```<br>```            "CompletePercentage": 100,```<br>```            "ErrorInfo": "",```<br>```            "NameCN": "用户迁移",```<br>```            "ProgressType": "Account",```<br>```            "Status": "Done"```<br>```        }```<br>```    ]```<br>```}```<br> |Overall progress information of the transmission task. |


<span id="progresssummaryinfo"></span>
### ProgressSummaryInfo


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ErrorInfo |String |mysql endpoint error: dial tcp 172.17.\*\*\*\*.\*\*\*\*:3306: i/o timeout |Task error message. |
|NameCN |String |Incremental subscription |The type of task progress. The values include user migration, schema migration, full migration, post\-schema migration, database and table schema subscription, full subscription, incremental subscription, user synchronization, full synchronization, schema synchronization, incremental synchronization, post\-schema synchronization. |
|ProgressType |String |Incr |Task type. The values are as follows:<br><br><br>* `Account`: Indicates user migration.<br><br>* `Meta`: Indicates structural migration, database and table structure subscription, or structure initialization.<br><br>* `Full`: Indicates full migration, full subscription, or full initialization.<br><br>* `Incr`: Indicates incremental migration, incremental subscription, or incremental synchronization.<br><br>* `PostMeta`: Indicates post\-structural migration. |
|Status |String |Doing |Task status. The values are as follows:<br><br><br>* `Doing`: Indicates that the verification task is in progress.<br><br>* `Todo`: Indicates that the verification task is pending.<br><br>* `Done`: Indicates that the verification task is completed. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeValidationTaskInfo&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "d496677038544e4a82d0ff0d9d******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "DescribeValidationTaskInfo",
        "Region": "cn-north-1",
        "Service": "dts",
        "Version": "2022-10-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
    "TaskInfo": {
        "ResponseMetadata ": {
            "RequestId ": "202412101725348099E9905A095805FBE9-cace50  ",
            "Action ": "DescribeValidationTaskInfo  ",
            "Version ": "2022-10-01  ",
            "Service ": "dts  ",
            "Region ": "cn-beijing  "
        },
        "Result ": {
            "TaskInfo ": {
                "ChargeConfig ": {
                    "ChargeType ": "PostPaid  ",
                    "DestRegion ": "cn-beijing  ",
                    "DestType ": "Volc_Mongo  ",
                    "EnableV2 ": true,
                    "SrcRegion ": "cn-beijing  ",
                    "SrcType ": "Volc_Mongo  ",
                    "TaskType ": "DataValidation  ",
                    "Times ": 1,
                    "TrafficSpec ": "Compact  "
                },
                "ChargeDetail ": {
                    "ChargeEndTime ": 7258089600000,
                    "ChargeStartTime ": 1733822722000,
                    "ChargeStatus ": "Normal  ",
                    "ChargeType ": "PostPaid  ",
                    "OrderNo ": "  "
                },
                "CreateTime ": 1733822707944,
                "DestConfig ": {
                    "Category ": "MongoDB  ",
                    "CreateTime ": 1733822707933,
                    "DataSourceId ": "1866402178390831111",
                    "EndpointType ": "Volc_Mongo  ",
                    "ModifyTime ": 1733822723986,
                    "VolcMongoSettings ": {
                        "DBInstanceId ": "mongo-replica-d91799021291  ",
                        "DBInstanceName ": "  ",
                        "DeployType ": "ReplicaSet  ",
                        "MongoAuthSourceDB ": "admin  ",
                        "Password ": "******  ",
                        "RegionSettings ": {
                            "Region ": "cn-beijing  "
                        },
                        "Username ": "root  "
                    }
                },
                "EnableCloudMonitor ": true,
                "EndTime ": 0,
                "ParentTaskID ": "4c1d32fe38c64ec7bf7f02d87926e94d  ",
                "ParentTaskName ": "dts-483oh5l2ne  ",
                "ProjectName ": "default  ",
                "SolutionSettings ": {
                    "Mongo2MongoPkCompareSettings ": {
                        "ObjectMappings ": [
                            {
                                "DestObjName ": "__mongodb_systems__  ",
                                "MappingList ": [
                                    {
                                        "DestObjName ": "*  ",
                                        "ObjectMappingSetting ": {
                                            "PolicyForKeyConflict ": "TableNone  ",
                                            "SetObjectTransType ": false
                                        },
                                        "ObjectType ": "Table  ",
                                        "SrcObjName ": "*  "
                                    },
                                    {
                                        "DestObjName ": "mongodb_sla  ",
                                        "ObjectMappingSetting ": {
                                            "PolicyForKeyConflict ": "TableNone  ",
                                            "SetObjectTransType ": false
                                        },
                                        "ObjectType ": "Table  ",
                                        "SrcObjName ": "mongodb_sla  "
                                    }
                                ],
                                "ObjectType ": "Database  ",
                                "SrcObjName ": "__mongodb_systems__  "
                            },
                            {
                                "DestObjName ": "cecehi  ",
                                "MappingList ": [
                                    {
                                        "DestObjName ": "*  ",
                                        "ObjectMappingSetting ": {
                                            "PolicyForKeyConflict ": "TableNone  ",
                                            "SetObjectTransType ": false
                                        },
                                        "ObjectType ": "Table  ",
                                        "SrcObjName ": "*  "
                                    },
                                    {
                                        "DestObjName ": "ddd  ",
                                        "ObjectMappingSetting ": {
                                            "PolicyForKeyConflict ": "TableNone  ",
                                            "SetObjectTransType ": false
                                        },
                                        "ObjectType ": "Table  ",
                                        "SrcObjName ": "ddd  "
                                    },
                                    {
                                        "DestObjName ": "d  ",
                                        "ObjectMappingSetting ": {
                                            "PolicyForKeyConflict ": "TableNone  ",
                                            "SetObjectTransType ": false
                                        },
                                        "ObjectType ": "Table  ",
                                        "SrcObjName ": "d  "
                                    }
                                ],
                                "ObjectType ": "Database  ",
                                "SrcObjName ": "cecehi  "
                            }
                        ]
                    },
                    "SolutionType ": "Mongo2MongoPkCompare  "
                },
                "SrcConfig ": {
                    "Category ": "MongoDB  ",
                    "CreateTime ": 1733822707931,
                    "DataSourceId ": "1866402178390831110",
                    "EndpointType ": "Volc_Mongo  ",
                    "ModifyTime ": 1733822723579,
                    "VolcMongoSettings ": {
                        "DBInstanceId ": "mongo-replica-386df9f4fd7c  ",
                        "DBInstanceName ": "  ",
                        "DeployType ": "ReplicaSet  ",
                        "MongoAuthSourceDB ": "admin  ",
                        "Password ": "******  ",
                        "RegionSettings ": {
                            "Region ": "cn-beijing  "
                        },
                        "Username ": "root  "
                    }
                },
                "StartTime ": 1733822723214,
                "TaskId ": "38b77a44d6fc4cb89fe6964b8******  ",
                "TaskName ": "test2  ",
                "TaskStatus ": "Running  ",
                "TaskSubType ": "FullPkCompare  ",
                "TaskType ": "DataValidation  ",
                "TenantId ": "2100******  ",
                "TrafficSpec ": "Compact  "
            }
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
