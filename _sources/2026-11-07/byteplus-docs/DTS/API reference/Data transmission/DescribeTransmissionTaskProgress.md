---
title: "DescribeTransmissionTaskProgress"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskprogress"
---

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|TaskId |String |No |4ddec6d036384248a25862fb17cb\*\*\*\* |Task ID. |
|ProgressType |String |No |Account |Task type. The values are as follows:<br><br><br>* `Account`: Indicates user migration. This value is supported when `TaskType` is `DataMigration`.<br><br>* `Meta`: Indicates structural migration, database and table structure subscription, or structure initialization.<br><br>* `Full`: Indicates full migration, full subscription, or full initialization.<br><br>* `Incr`: Indicates incremental migration, incremental subscription, or incremental synchronization.<br><br>* `PostMeta`: Indicates post\-structural migration. This value is supported when `TaskType` is `DataMigration`.<br><br>* `MigrationAssessment`: Indicates migration evaluation. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1000, with a default of 10. |
|TransmissionState |String |No |Transmitting |The task transmission state. The values are as follows:<br><br><br>* `None`: Indicates that the task is to be started.<br><br>* `Transmitting`: Indicates that the task is in transmission.<br><br>* `Completed`: Indicates that the task is completed.<br><br>* `Removed`: Indicates that the task transmission failed. |
|ObjectType |String |No |Database |Object type. The values are as follows:<br><br><br>* `Database`: indicates a database.<br><br>* `Table`: indicates a table.<br><br>* `View`: indicates a view.<br><br>* `Column`: Indicates the `column`.<br><br>* `Function`: Indicates the `function`.<br><br>* `Procedure`: Indicates the `procedure`.<br><br>* `Trigger`: Indicates the `trigger`.<br><br>* `Type`: Indicates the `type`.<br><br>* `Domain`: Indicates the `domain`.<br><br>* `Sequence`: Indicates the `sequence`.<br><br>* `Rule`: Indicates the `rule`.<br><br>* `Operator`: Indicates the `operator`.<br><br>* `Aggregate`: Indicates the `aggregate`.<br><br>* `Extension`: Indicates an extension.<br><br>* `Constraint`: Indicates a constraint.<br><br>* `PostSequence`: Indicates a PostgreSQL sequence. This parameter must be configured when the parameter is PostgreSQL.<br><br>* `Schema`: Indicates a mode.<br><br>* `Event`: Indicates an event.<br><br>* `DomainConstraint`: Indicates a domain constraint. |
|Name |String |No |test\*\*\* |Object name. |
|LatencyDesc |Boolean |No |true |Whether to sort in descending order of delay. The values are as follows:<br><br><br>* `true`: Sort in descending order.<br><br>* `false`: Do not sort in descending order. |
|TransferEstimateRowsDesc |Boolean |No |false |Indicates whether to sort in descending order based on the estimated number of rows for transmission. The values are as follows:<br><br><br>* `true`: Sort in descending order.<br><br>* `false`: Do not sort in descending order. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TaskProgress |Object of [TaskProgress](https://docs.byteplus.com/en/docs/57/15952#taskprogress) |```json```<br>```{```<br>```    "FullProgress":[```<br>```        {```<br>```            "Database":{```<br>```                "DestObjName":"test****1",```<br>```                "ObjectType":"Database",```<br>```                "SrcObjName":"test****1"```<br>```            },```<br>```            "FinishTime":1679299572000,```<br>```            "Object":{```<br>```                "DestObjName":"i_log",```<br>```                "ObjectType":"Table",```<br>```                "SrcObjName":"i_log"```<br>```            },```<br>```            "RowAvgBytes":0,```<br>```            "ShardID":"",```<br>```            "StartTime":1679299572000,```<br>```            "State":"Completed",```<br>```            "TransferBytes":0,```<br>```            "TransferEstimateBytes":0,```<br>```            "TransferEstimateRows":0,```<br>```            "TransferRows":0```<br>```        }```<br>```    ],```<br>```    "ProgressType":"Full",```<br>```    "Total":10```<br>```}```<br> |Detailed information on the progress of the task. |


<span id="taskprogress"></span>
### TaskProgress


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ProgressType |String |Full |Task type. The values are as follows:<br><br><br>* `Account`: Indicates user migration. This value is supported when `TaskType` is `DataMigration`.<br><br>* `Meta`: Indicates structural migration, database and table structure subscription, or structure initialization.<br><br>* `Full`: Indicates full migration, full subscription, or full initialization.<br><br>* `Incr`: Indicates incremental migration, incremental subscription, or incremental initialization.<br><br>* `MigrationAssessment`: Indicates the migration evaluation progress. |
|Total |Integer |10 |The total number of tasks. |
|AccountProgress |Array of [AccountProgressItem](https://docs.byteplus.com/en/docs/57/15952#accountprogressitem) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "Account": "`zaizai`@`%`",```<br>```        "Statement": "GRANT REFERENCES ON `huahua`.* TO `zaizai`@`%`;",```<br>```        "state": "Completed",```<br>```        "type": "Privilege"```<br>```    }```<br>```]```<br> |User migration progress. |
|MetaProgress |Array of [MetaProgressItem](https://docs.byteplus.com/en/docs/57/15952#metaprogressitem) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "Database": {```<br>```            "DestObjName": "huahua",```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "huahua"```<br>```        },```<br>```        "Ddl": " CREATE DATABASE `huahua` /*!40100 DEFAULT CHARACTER SET utf8 */",```<br>```        "FinishTime": 1707191069645339,```<br>```        "Object": {```<br>```            "DestObjName": "auth_operation",```<br>```            "ObjectType": "Table",```<br>```            "SrcObjName": "auth_operation"```<br>```        },```<br>```        "StartTime": 0,```<br>```        "State": "Completed"```<br>```    }```<br>```]```<br> |The progress of schema migration, database and table schema subscription, or schema initialization tasks. |
|FullProgress |Array of [FullProgressItem](https://docs.byteplus.com/en/docs/57/15952#fullprogressitem) |```JSON```<br>```[```<br>```    {```<br>```        "Database": {```<br>```            "DestObjName": "huahua",```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "huahua"```<br>```        },```<br>```        "FinishTime": 1707191094000,```<br>```        "Object": {```<br>```            "DestObjName": "auth_operation",```<br>```            "ObjectType": "Table",```<br>```            "SrcObjName": "auth_operation"```<br>```        },```<br>```        "RowAvgBytes": 341,```<br>```        "ShardID": "",```<br>```        "StartTime": 1707191089000,```<br>```        "State": "Completed",```<br>```        "TransferBytes": 5318,```<br>```        "TransferEstimateBytes": 16368,```<br>```        "TransferEstimateRows": 48,```<br>```        "TransferRows": 48```<br>```    }```<br>```]```<br> |Task progress of full migration, full subscription, or full initialization. |
|IncrProgress |Array of [IncrProgressItem](https://docs.byteplus.com/en/docs/57/15952#incrprogressitem) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "Database": {```<br>```            "DestObjName": "test****",```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "test****"```<br>```        },```<br>```        "TransferRows": 1,```<br>```        "Object": {```<br>```            "DestObjName": "test****",```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "test****"```<br>```        },```<br>```        "TransferBytes": 1,```<br>```        "ShardID": 0,```<br>```        "State": "Completed",```<br>```        "LatencySeconds": 0```<br>```    }```<br>```]```<br><br><br> |Task progress of incremental migration, incremental subscription, or incremental initialization. |
|MigrationAssessmentProgress |Array of [MigrationAssessmentProgressItem](https://docs.byteplus.com/en/docs/57/15952#migrationassessmentprogressitem) |```JSON```<br>```[```<br>```    {```<br>```        "Category": "BasicInfo",```<br>```        "Description": "检查源实例是否含有开启TDE加密的表",```<br>```        "IsLast": false,```<br>```        "ItemCode": "TDE",```<br>```        "ItemName": "源实例 TDE 检查",```<br>```        "ResultInfo": "{\"ResultCode\":\"\",\"EncryptTables\":[]}",```<br>```        "Status": "Success",```<br>```        "StatusDesc": "不存在 TDE 加密的表",```<br>```        "Suggestion": ""```<br>```    }```<br>```]```<br> |Migration evaluation task progress. |
|DflowRuntimeReadyTimestampMs |Long |0 |Indicates the start timestamp (in milliseconds) when a data stream task in incremental migration or incremental initialization is dispatched to the execution node by the scheduling system. It marks the point when the task transitions from "wait" to "execute" phase. |
|DflowDispatchStartTimestampMs |Long |0 |It represents the timestamp (in milliseconds) when the data flow task completes initialization, resources are ready, and it can start processing data on the execution node during incremental migration or incremental initialization. It marks the endpoint when the task transitions from "starting" to "runnable" state. |


<span id="accountprogressitem"></span>
### AccountProgressItem


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Account |String |test\*\*\*\* |The name of the account. |
|StartTime |Long |0 |The start time of the user migration, in milliseconds. |
|FinishTime |Long |1679300319338820 |End time of user migration, in milliseconds timestamp. |
|Statement |String |StmtDDLAll |SQL statements to be transmitted. The values are as follows:<br><br><br>* `StmtDMLInsert`<br><br>* `StmtDMLUpdate`<br><br>* `StmtDMLDelete`<br><br>* `StmtDDLAll`<br><br>* `StmtDDLAlterTable`<br><br>* `StmtDDLAlterView`<br><br>* `StmtDDLCreateFunction`<br><br>* `StmtDDLCreateIndex`<br><br>* `StmtDDLCreateProcedure`<br><br>* `StmtDDLCreateTable`<br><br>* `StmtDDLCreateView`<br><br>* `StmtDDLDropIndex`<br><br>* `StmtDDLDropTable`<br><br>* `StmtDDLDropFunction`<br><br>* `StmtDDLDropProcedure`<br><br>* `StmtDDLTruncateTable`<br><br>* `StmtDDLRenameTable`<br><br>* `StmtDDLDropView` |
|state |String |None |Single task transmission state. The values are as follows:<br><br><br>* `None`: Indicates that the task is to be started.<br><br>* `Transmitting`: Indicates that the task is in transmission.<br><br>* `Completed`: Indicates that the task is completed.<br><br>* `Removed`: Indicates that the task transmission failed. |
|type |String |Account |The type of user migration. The values are as follows:<br><br><br>* `Account`: Indicates the migration account.<br><br>* `Privileges`: Indicates the migration account privileges. |


<span id="metaprogressitem"></span>
### MetaProgressItem


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/15952#objectmapping) |&nbsp;<br><br>```JSON```<br>```{```<br>```      "DestObjName": "test****",```<br>```      "ObjectType": "Database",```<br>```      "SrcObjName": "test****"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/15952#objectmapping) |&nbsp;<br><br>```JSON```<br>```{```<br>```      "DestObjName": "test****",```<br>```      "ObjectType": "Database",```<br>```      "SrcObjName": "test****"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |
|StartTime |Long |0 |Start time for database and table migration, subscription, or initialization, in milliseconds timestamp. |
|FinishTime |Long |1679300319338837 |The end time of schema migration, subscription, or initialization for databases and tables, in milliseconds. |
|Ddl |String |\nCREATE DATABASE `test****` /\*!40100 DEFAULT CHARACTER SET utf8 \*/ |Operation statements for creating the database and table schema. |
|State |String |Completed |The task transmission state. The values are as follows:<br><br><br>* `None`: Indicates that the task is to be started.<br><br>* `Transmitting`: Indicates that the task is in transmission.<br><br>* `Completed`: Indicates that the task is completed.<br><br>* `Removed`: Indicates that the task transmission failed. |


<span id="objectmapping"></span>
### ObjectMapping


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ObjectType |String |Function |Object type. The values are as follows:<br><br><br>* `Database`: indicates a database.<br><br>* `Table`: indicates a table.<br><br>* `View`: indicates a view.<br><br>* `Column`: Indicates the `column`.<br><br>* `Function`: Indicates the `function`.<br><br>* `Procedure`: Indicates the `procedure`.<br><br>* `Trigger`: Indicates the `trigger`.<br><br>* `Type`: Indicates the `type`.<br><br>* `Domain`: Indicates the `domain`.<br><br>* `Sequence`: Indicates the `sequence`.<br><br>* `Rule`: Indicates the `rule`.<br><br>* `Operator`: Indicates the `operator`.<br><br>* `Aggregate`: Indicates the `aggregate`.<br><br>* `Extension`: Indicates an extension.<br><br>* `Constraint`: Indicates a constraint.<br><br>* `PostSequence`: Indicates a PostgreSQL sequence.<br><br>* `Schema`: Indicates a mode.<br><br>* `Event`: Indicates an event.<br><br>* `DomainConstraint`: Indicates a domain constraint.<br><br>* `Blocklist`: indicates that this table is a blocklist table, filtered during subscription, and not synchronized to the destination. |
|SrcObjName |String |ceshi\*\*\*\* |Source object name.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the parameter <code>ObjectType</code> is set to <code>BlackTable</code>, the table name to be added to the blocklist must be provided.</div><br> |
|DestObjName |String |test\*\*\*\* |Target object name.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">When the parameter <code>ObjectType</code> is set to <code>BlackTable</code>, the table name to be added to the blocklist must be provided.</div><br> |
|MappingList |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/15952#objectmapping) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Transmission task object. |
|ObjectMappingSetting |Object of [ObjectMappingSetting](https://docs.byteplus.com/en/docs/57/15952#objectmappingsetting) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ESMetaMappingSetting": {```<br>```        "PidCol": [```<br>```            "id",```<br>```            "name"```<br>```        ],```<br>```        "EnableRouting": true,```<br>```        "RoutingCol": [```<br>```            "id"```<br>```        ]```<br>```    }```<br>```}```<br> |Additional parameter information that needs to be configured when synchronizing data to Elasticsearch. |


<span id="objectmappingsetting"></span>
### ObjectMappingSetting


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ESMetaMappingSetting |Object of [ESMetaMappingSetting](https://docs.byteplus.com/en/docs/57/15952#esmetamappingsetting) |```JSON```<br>```{```<br>```    "PidCol": [```<br>```        "id",```<br>```        "name"```<br>```    ],```<br>```    "EnableRouting": true,```<br>```    "RoutingCol": [```<br>```        "id"```<br>```    ]```<br>```}```<br> |Structure mapping parameters of Elasticsearch. |
|EmbeddingSetting |Object of [EmbeddingSetting](https://docs.byteplus.com/en/docs/57/15952#embeddingsetting) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableEmbedding": true,```<br>```    "VectorFieldName": "age_vector",```<br>```    "VectorType": "FloatVector",```<br>```    "MetricType": "L2",```<br>```    "IndexType": "AUTOINDEX",```<br>```    "KeepOriginalText": true,```<br>```    "OriginalTextNewFieldName": "age"```<br>```}```<br> |Vectorization configuration information of the table. Indicates converting source column data into vectorization. |
|PreVectorizedSetting |Object of [PreVectorizedSetting](https://docs.byteplus.com/en/docs/57/15952#prevectorizedsetting) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "VectorType": "FloatVector",```<br>```    "MetricType": "L2",```<br>```    "IndexType": "AUTOINDEX",```<br>```    "Dimension": 128,```<br>```    "SourceEncoding": "FloatArray"```<br>```}```<br><br><br> |Pre\-vectorization setting information. Indicates the source column data has completed vectorization and can be directly synchronized. |


<span id="esmetamappingsetting"></span>
### ESMetaMappingSetting


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|PidCol |Array of String |["id", "name"] |Primary key (_id) value. If this parameter is not set, the default is the column of the primary key. |
|EnableRouting |Boolean |EnableRouting |Whether to enable Routing. The values are as follows:<br><br><br>* `true`: Indicates that Routing is enabled.<br><br>* `false`: Indicates that Routing is not enabled. |
|RoutingCol |Array of String |["id"] |The value of `_routing`. This parameter is required when `EnableRouting` is set to `true`. |


<span id="embeddingsetting"></span>
### EmbeddingSetting


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|IndexType |String |AUTOINDEX |Vector index type, currently only supported to be set as `AUTOINDEX`. |
|MetricType |String |L2 |Metric type, values include: L2, IP, COSINE. |
|VectorType |String |FloatVector |Vector type, currently only `FloatVector` is supported. |
|EnableEmbedding |Boolean |true |Whether to enable vectorization configuration, values are as follows:<br><br><br>* `true`: indicates enabling vectorization configuration.<br><br>* `no`: indicates that vectorization configuration is not enabled. |
|VectorFieldName |String |age_vector |Name of vectorization. |
|KeepOriginalText |Boolean |true |Keep original text options are as follows:<br><br><br>* `true`: indicates to keep original text.<br><br>* `false`: indicates not to keep original text. |
|OriginalTextNewFieldName |String |test |New column name in the source text; if empty, it means no modification and the original name is retained. |


<span id="prevectorizedsetting"></span>
### PreVectorizedSetting


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Dimension |Integer |128 |Represents vector dimension, default is 128, range is 1~32768. |
|IndexType |String |AUTOINDEX |Vector index type, currently only supported to be set as `AUTOINDEX`. |
|MetricType |String |L2 |Metric type, values include: L2, IP, COSINE. |
|VectorType |String |FloatVector |Vector type, currently only `FloatVector` is supported. |
|SourceEncoding |String |FloatArray |The encoding format of source data, currently only `FloatArray` is supported. |


<span id="fullprogressitem"></span>
### FullProgressItem


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/15952#objectmapping) |```JSON```<br>```{```<br>```    "DestObjName": "test****1",```<br>```     "ObjectType": "Database",```<br>```    "SrcObjName": "test****1"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/15952#objectmapping) |```JSON```<br>```{```<br>```    "DestObjName": "auth_operation",```<br>```    "ObjectType": "Table",```<br>```    "SrcObjName": "auth_operation"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |
|StartTime |Long |1679300366000 |Start time for full migration, subscription, or initialization, in milliseconds timestamp. |
|FinishTime |Long |1679300366000 |The end time of full migration, subscription, or initialization, in milliseconds. |
|TransferRows |Long |0 |Rows transmitted. |
|TransferBytes |Long |0 |Number of bytes transmitted. |
|TransferEstimateRows |Long |0 |Estimated rows |
|State |String |Completed |The task transmission state. The values are as follows:<br><br><br>* `None`: Indicates that the task is to be started.<br><br>* `Transmitting`: Indicates that the task is in transmission.<br><br>* `Completed`: Indicates that the task is completed.<br><br>* `Removed`: Indicates that the task transmission failed. |
|ShardID |String |0 |Shard ID. |
|RowAvgBytes |Long |0 |Row average size |
|TransferEstimateBytes |Long |0 |Estimated total amount of transmission data. |


<span id="incrprogressitem"></span>
### IncrProgressItem


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Database |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/15952#objectmapping) |```JSON```<br>```{```<br>```      "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database information. |
|Object |Object of [ObjectMapping](https://docs.byteplus.com/en/docs/57/15952#objectmapping) |```JSON```<br>```{```<br>```     "DestObjName": "test****",```<br>```     "ObjectType": "Database",```<br>```     "SrcObjName": "test****"```<br>```}```<br> |Database and table mapping objects between the source and target ends. |
|TransferRows |Long |0 |Rows transmitted. |
|TransferBytes |Long |0 |Number of bytes transmitted. |
|ShardID |String |0 |Shard ID. |
|State |String |Completed |The task transmission state. The values are as follows:<br><br><br>* `None`: Indicates that the task is to be started.<br><br>* `Transmitting`: Indicates that the task is in transmission.<br><br>* `Completed`: Indicates that the task is completed.<br><br>* `Removed`: Indicates that the task transmission failed. |
|LatencySeconds |Long |0 |Delay. Unit: second (s). |


<span id="migrationassessmentprogressitem"></span>
### MigrationAssessmentProgressItem


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Category |String |BasicInfo |Evaluation category. |
|ItemCode |String |DBVersion |The unique identifier of the evaluation item. |
|ItemName |String |Source instance and target instance versions |Name of the evaluation item. |
|Description |String |Is the source version to target version migration supported? |Description of the evaluation item. |
|ResultInfo |String |```JSON```<br>```{```<br>```    "ResultCode":"Success",```<br>```    "SrcDBVersion":"5.6.51",```<br>```    "DstDBVersion":"5.7.32-log"```<br>```}```<br> |Detailed information on the evaluation results. |
|Status |String |Success |The status of the evaluation item. The values are as follows:<br><br><br>* `Success`: Pass.<br><br>* `Warn`: Prompt.<br><br>* `Failed`: Failed. |
|StatusDesc |String |Source end: 5.6.51, destination: 5.7.32\-log |Instructions for the evaluation results. |
|IsLast |Boolean |false |Whether this is the last evaluation item.<br><br><br>* `true`: Indicates that this is the last evaluation item.<br><br>* `false`: Indicates that this is not the last evaluation item. |
|Suggestion |String |The impact of migrating tables without primary keys mainly comes from two aspects:<br><br><br>* Risk of interruption during full migration: Since DTS cannot resume interrupted data transfer, if an interruption occurs during the migration process, a full resynchronization is required, which significantly extends the migration time and increases the load on the source database.<br><br>* Incremental data inconsistency: During the incremental synchronization phase, the absence of a primary key table may lead to duplicate or missing data, causing inconsistencies between the target and source data. Recommended improvement solutions:<br><br>   * Add business primary key: add a unique identifier field with business meaning as the primary key on the source end's no\-primary\-key table to ensure unique data identification.<br><br>   * Operate during business low peak: perform ALTER TABLE operations during low business periods, reducing table lock time using `ALGORITHM=INPLACE`.<br><br>* Verify data consistency: after migration, use data verification tools to compare the source and destination data consistency. This method requires no dynamic database parameter modifications and permanently resolves no\-primary\-key table issues through DDL operations, ensuring data completeness and accuracy in migration. |Optimization suggestions given after evaluation.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the value of <code>State</code> is <code>Success</code>, the content of <code>Suggestion</code> is empty.</div><br> |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeTransmissionTaskProgress&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.volcengineapi.com
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "af16a602e1134abdbb281864ca******",
    "ProgressType": "Full",
    "PageNumber": 1,
    "PageSize": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230320160648C9A57C0DA2D94117B1C5",
        "Action": "DescribeTransmissionTaskProgress",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {
        "TaskProgress": {
            "FullProgress": [
                {
                    "Database": {
                        "DestObjName": "test****1",
                        "ObjectType": "Database",
                        "SrcObjName": "test****1"
                    },
                    "FinishTime": 1679299572000,
                    "Object": {
                        "DestObjName": "i_log",
                        "ObjectType": "Table",
                        "SrcObjName": "i_log"
                    },
                    "RowAvgBytes": 0,
                    "ShardID": "",
                    "StartTime": 1679299572000,
                    "State": "Completed",
                    "TransferBytes": 0,
                    "TransferEstimateBytes": 0,
                    "TransferEstimateRows": 0,
                    "TransferRows": 0
                }
            ],
            "ProgressType": "Full",
            "Total": 1
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
