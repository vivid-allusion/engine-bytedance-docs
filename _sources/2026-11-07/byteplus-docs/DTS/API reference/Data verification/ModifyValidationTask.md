---
title: "ModifyValidationTask"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/modifyvalidationtask"
---

Call the ModifyValidationTask API to modify the data verification task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |cad03b2ed34d45a585d883d90f\*\*\*\*\*\* |Verification task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describevalidationtasks">DescribeValidationTasks</a> API to view the verification task ID.</div><br> |
|TaskName |String |No |dts\-fl8b2m\*\*\*\* |Data verification task name. |
|SrcConfig |Object of [DataSource](https://docs.byteplus.com/en/docs/57/47109#datasource) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Category": "MySQL",```<br>```    "CreateTime": 1769672325124,```<br>```    "DataSourceId": "2016759699713855503",```<br>```    "EndpointType": "Volc_MySQL",```<br>```    "ModifyTime": 1769672880664,```<br>```    "VolcMySQLSettings": {```<br>```        "DBInstanceId": "mysql-36632f******",```<br>```        "DBInstanceName": "",```<br>```        "Password": "******",```<br>```        "RegionSettings": {```<br>```            "Region": "cn-shanghai"```<br>```        },```<br>```        "Username": "huahua"```<br>```    }```<br>```}```<br><br><br> |Source information. |
|DestConfig |Object of [DataSource](https://docs.byteplus.com/en/docs/57/47109#datasource) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Category": "MySQL",```<br>```    "CreateTime": 1769672325124,```<br>```    "DataSourceId": "2016759699713855503",```<br>```    "EndpointType": "Volc_MySQL",```<br>```    "ModifyTime": 1769672880664,```<br>```    "VolcMySQLSettings": {```<br>```        "DBInstanceId": "mysql-36632f******",```<br>```        "DBInstanceName": "",```<br>```        "Password": "******",```<br>```        "RegionSettings": {```<br>```            "Region": "cn-shanghai"```<br>```        },```<br>```        "Username": "huahua"```<br>```    }```<br>```}```<br><br><br> |Destination information. |
|SolutionSettings |Object of [SolutionSettings](https://docs.byteplus.com/en/docs/57/47109#solutionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "MySQL2MySQLIncrDataValidationSettings": {```<br>```        "ObjectMappings": [```<br>```            {```<br>```                "DestObjName": "test123",```<br>```                "MappingList": [```<br>```                    {```<br>```                        "DestObjName": "*",```<br>```                        "ObjectType": "Table",```<br>```                        "SrcObjName": "*"```<br>```                    }```<br>```                ],```<br>```                "ObjectType": "Database",```<br>```                "SrcObjName": "test"```<br>```            }```<br>```        ]```<br>```    },```<br>```    "SolutionType": "MySQL2MySQLIncrDataValidation"```<br>```}```<br><br><br> |Configuration information of the data verification task object. |


<span id="datasource"></span>
### DataSource


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Category |String |No |MySQL |The type of instance. The values are as follows:<br><br><br>* `MySQL`: Indicates that the instance type is MySQL.<br><br>* `PostgreSQL`: Indicates that the instance type is PostgreSQL.<br><br>* `ElasticSearch`: Indicates that the instance type is Elasticsearch.<br><br>* `MongoDB`: Indicates that the instance type is MongoDB.<br><br>* `Redis`: Indicates that the instance type is Redis. |
|CreateTime |Long |No |1734070854504 |Creation time of the data source. Millisecond timestamp. |
|DataSourceId |String |No |1867454442941460510 |Source or target instance ID. |
|ModifyTime |Long |No |1734070873088 |The most recent time the data source was updated. Millisecond timestamp. |
|EndpointType |String |Yes |Volc_MySQL |The access method of the instance. the values are as follows:<br><br><br>* `Volc_MySQL`: Indicates BytePlus NDB for MySQL.<br><br>* `Volc_veDB_MySQL`: Indicates BytePlus NDB for MySQL.<br><br>* `Volc_PostgreSQL`: Indicates Volcengine RDS for PostgreSQL.<br><br>* `Volc_Mongo`: Indicates Volcengine Database for MongoDB.<br><br>* `Volc_ElasticSearch`: Indicates Volcengine Cloud Search Service.<br><br>* `Volc_Kafka`: Indicates Message Queue for Kafka.<br><br>* `Volc_RocketMQ`: Indicates Message Queue for RocketMQ.<br><br>* `Volc_Redis`: Indicates Volcengine Cache for Redis.<br><br>* `Public_MySQL`: Indicates MySQL connected over public network.<br><br>* `Public_PostgreSQL`: Indicates  connected over public network.<br><br>* `Public_Mongo`: Indicates MongoDB connected over public network..<br><br>* `Public_ElasticSearch`: Indicates Cloud Search connected over public network.<br><br>* `Public_Redis`: Indicates Redis connected over express network.<br><br>* `Builtin_Kafka`: Indicates the built\-in middleware.<br><br>* `Express_MySQL`: Indicates MySQL connected over express network.<br><br>* `Express_PostgreSQL`: Indicates PostgreSQL connected over express network.<br><br>* `Express_Mongo`: Indicates MongoDB connected over express network.<br><br>* `Express_Redis`: Indicates Redis connected over express network.<br><br>* `Express_Kafka`: Indicates Kafka connected over express network.<br><br>* `Express_ElasticSearch`: Indicates ElasticSearch connected over express network. |
|VolcMySQLSettings |Object of [VolcMySQLSettings](https://docs.byteplus.com/en/docs/57/47109#volcmysqlsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "mysql-0b5d385f*****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-shanghai"```<br>```    },```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine RDS for MySQL. This parameter is required when `EndpointType` is set to `Volc_MySQL`. |
|VolcveDBMySQLSettings |Object of [VolcveDBMySQLSettings](https://docs.byteplus.com/en/docs/57/47109#volcvedbmysqlsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "vedbm-arjlc5di****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "root"```<br>```}```<br> |Indicates the information of the source or target database where the access method is BytePlus veDB for MySQL. This parameter is required when `EndpointType` is set to `Volc_veDB_MySQL`. |
|VolcPostgreSQLSettings |Object of [VolcPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47109#volcpostgresqlsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "postgres-5d17bd5c****",```<br>```    "DBInstanceName": "",```<br>```    "DBName": "huahua",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine RDS for PostgreSQL. This parameter is required when `EndpointType` is set to `Volc_PostgreSQL`. |
|VolcMongoSettings |Object of [VolcMongoSettings](https://docs.byteplus.com/en/docs/57/47109#volcmongosettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "mongo-replica-8ea79132****",```<br>```    "DBInstanceName": "",```<br>```    "DeployType": "ReplicaSet",```<br>```    "MongoAuthSourceDB": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Username": "root"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine Database for MongoDB. This parameter is required when `EndpointType` is set to `Volc_Mongo`. |
|VolcElasticSearchSettings |Object of [VolcElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47109#volcelasticsearchsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "o-00g0sqi*****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-shanghai"```<br>```    },```<br>```    "Username": "admin"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine Cloud Search Service. This parameter is required when `EndpointType` is set to `Volc_ElasticSearch`. |
|VolcKafkaSettings |Object of [VolcKafkaSettings](https://docs.byteplus.com/en/docs/57/47109#volckafkasettings) |No |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "InstanceId": "kafka-cnnge0tckudy****",```<br>```    "InstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Topic": "huahua",```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the target database when the access method is Volcengine Kafka. This parameter is required when `EndpointType` is set to `Volc_Kafka`. |
|VolcRocketMQSettings |Object of [VolcRocketMQSettings](https://docs.byteplus.com/en/docs/57/47109#volcrocketmqsettings) |No |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "InstanceId": "rocketmq-cnou964d1e******",```<br>```    "InstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Topic": "zaizai",```<br>```    "Username": "uSmQgOHNTy5Uh98nqBGPvCzK"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine RocketMQ. This parameter is required when `EndpointType` is set to `Volc_RocketMQ`. |
|VolcRedisSettings |Object of [VolcRedisSettings](https://docs.byteplus.com/en/docs/57/47109#volcredissettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "redis-cnlf1xx7vjjw9****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine Cache for Redis. This parameter is required when `EndpointType` is set to `Volc_Redis`. |
|PublicMySQLSettings |Object of [PublicMySQLSettings](https://docs.byteplus.com/en/docs/57/47109#publicmysqlsettings) |No |```JSON```<br>```{```<br>```    "Host": "rm-2zey7i58n36x0****.mysql.rds.aliyuncs.com",```<br>```    "Password": "******",```<br>```    "Port": 3306,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "rootgg"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MySQL connected over public network. This parameter is required when `EndpointType` is set to `Public_MySQL`. |
|PublicPostgreSQLSettings |Object of [PublicPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47109#publicpostgresqlsettings) |No |```JSON```<br>```{```<br>```    "DBName": "postgres",```<br>```    "Host": "aurora-pg-17-replica-instance-1.czenkuaf0oxm.ap-southeast-2.rds.amazonaws.com",```<br>```    "Password": "******",```<br>```    "Port": 5432,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "dts"```<br>```}```<br> |Information indicating the access method is public network PostgreSQL for source database or target database. This parameter is required when `EndpointType` is set to `Public_PostgreSQL`. |
|PublicMongoSettings |Object of [PublicMongoSettings](https://docs.byteplus.com/en/docs/57/47109#publicmongosettings) |No |```JSON```<br>```{```<br>```    "DeployType": "Standalone",```<br>```    "Endpoints": [```<br>```        "123"```<br>```    ],```<br>```    "MongoAuthSourceDB": "123",```<br>```    "Password": "123",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-chongqing-sdv"```<br>```    },```<br>```    "Username": "123"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MongoDB connected over public network. This parameter is required when `EndpointType` is set to `Public_Mongo`. |
|PublicElasticSearchSettings |Object of [PublicElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47109#publicelasticsearchsettings) |No |```JSON```<br>``````<br>```{```<br>```    "Endpoints": [```<br>```        "********"```<br>```    ],```<br>```    "Password": "dddd",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "ddd"```<br>```}```<br> |Indicates information about the source database or target database accessed ElasticSearch connected over public network. This Parameter is required when `EndpointType` is set to `Public_ElasticSearch`. |
|PublicRedisSettings |Object of [PublicRedisSettings](https://docs.byteplus.com/en/docs/57/47109#publicredissettings) |No |```JSON```<br>```{```<br>```    "Host": "redis-sy013ku146******.redis.inner.ivolces.com",```<br>```    "Password": "******",```<br>```    "Port": 6379,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |Information about the source database or target database with access method as Redis connected over public network. This parameter is Required when `EndpointType` is set to `Public_Redis`. |
|BuiltinKafkaSettings |Object of [BuiltinKafkaSettings](https://docs.byteplus.com/en/docs/57/47109#builtinkafkasettings) |No |```JSON```<br>```{```<br>```    "Brokers": [```<br>```        "192.168.2.5:9092",```<br>```        "192.168.2.5:9192",```<br>```        "192.168.2.5:9292",```<br>```        "192.168.2.5:9392",```<br>```        "192.168.2.5:9492",```<br>```        "192.168.2.5:9592"```<br>```    ],```<br>```    "Topic": "123e8d8a3cc54477b45db3e3c708****"```<br>```}```<br> |Indicates the parameter information for subscribing to the built\-in middleware in the data subscription task. This parameter is required when `EndpointType` is set to `Builtin_Kafka`. |
|ExpressMongoSettings |Object of [ExpressMongoSettings](https://docs.byteplus.com/en/docs/57/47109#expressmongosettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "DeployType": "ReplicaSet",```<br>```    "Endpoints": [```<br>```        "eee"```<br>```    ],```<br>```    "MongoAuthSourceDB": "eee",```<br>```    "Password": "e",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-3jh1vsccsmjuo3pncmesj****",```<br>```        "VPCId": "vpc-30ukbt5glgyyo7r2qr2e6****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-chongqing-sdv"```<br>```    },```<br>```    "Username": "e"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MongoDB connected over express network. This parameter is required when `EndpointType` is `Express_Mongo`. |
|ExpressMySQLSettings |Object of [ExpressMySQLSettings](https://docs.byteplus.com/en/docs/57/47109#expressmysqlsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Host": "192.168.0.65",```<br>```    "Password": "******",```<br>```    "Port": 3306,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2d74b6pbyewao58ozferi****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9*****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "rootgg"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MySQL connected over express network. Required when `EndpointType` is `Express_MySQL`. |
|ExpressPostgreSQLSettings |Object of [ExpressPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47109#expresspostgresqlsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "DBName": "src",```<br>```    "Host": "192.168.0.65",```<br>```    "Password": "Bd2021_bd",```<br>```    "Port": 5432,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2bznv8i16voqo2dx0efg0****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "suser"```<br>```}```<br> |Indicates the information of the source or target database where the access method is PostgreSQL connected over express network. This parameter is required when `EndpointType` equals `Express_PostgreSQL`. |
|ExpressRedisSettings |Object of [ExpressRedisSettings](https://docs.byteplus.com/en/docs/57/47109#expressredissettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ArchType": "Standalone",```<br>```    "Host": "192.168.32.28",```<br>```    "Password": "pwd",```<br>```    "Port": 6399,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-3re9nvjumjthc5zsk2i5z****",```<br>```        "VPCId": "vpc-2bzf04ctm2pz42dx0eebh****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |This represents the information of the source database or target database with access method of Redis connected over express network. When `EndpointType` is `Express_Redis`, this parameter is required. |
|ExpressElasticSearchSettings |Object of [ExpressElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47109#expresselasticsearchsettings) |No |```JSON```<br>```{```<br>```    "Endpoints": [```<br>```        "http://192.****.0.****:9200"```<br>```    ],```<br>```    "Password": "123456",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2d6asbw971nnk58ozfeei****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "elastic"```<br>```}```<br> |Indicates the information of the source or target database where the access method is ElasticSearch connected over express network. This parameter is required when `EndpointType` is set to `Express_ElasticSearch`. |
|ExpressKafkaSettings |Object of [ExpressKafkaSettings](https://docs.byteplus.com/en/docs/57/47109#expresskafkasettings) |No |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "BrokerEndpoints": [```<br>```        "192.168.0.65:9092"```<br>```    ],```<br>```    "Password": "admin-secret",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2bz5swar08oao2dx0ee******",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9******"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Topic": "dial_test",```<br>```    "Username": "admin"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Kafka connected over express network. This parameter is required when `EndpointType` is set to `Express_Kafka`. |
|Name |String |No |test |Task name of the data source. This parameter is required when you call the CreateDataSource API to create a data source. |


<span id="volcmysqlsettings"></span>
### VolcMySQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |mysql\-3d224def\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_MySQL</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> interface to query the instance ID.</div><br> |
|DBInstanceName |String |Yes |testDB |Instance name. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47109#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="regionsettings"></span>
### RegionSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Region |String |No |cn\-beijing |Region ID. |


<span id="crossaccountsettings"></span>
### CrossAccountSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SourceAccount |String |Yes |2100\*\*\*\*\*\* |Source account ID. |
|Role |String |Yes |test |The role name created by source accounts for the transmission of data. |


<span id="volcvedbmysqlsettings"></span>
### VolcveDBMySQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_veDB_MySQL</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> interface to query the Instance ID.</div><br> |
|DBInstanceName |String |Yes |TestveDB |Instance name. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47109#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="volcpostgresqlsettings"></span>
### VolcPostgreSQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |postgres\-h441603c68aaa\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when EndpointType is set to <code>Volc_PostgreSQL</code> in <code>EndpointType</code>.</div><br> |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47109#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="volcmongosettings"></span>
### VolcMongoSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |No |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Mongo</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances">DescribeDBInstanceDetail</a> API to query the instance ID.</div><br> |
|Username |String |No |test\*\*\*\* |Database account. |
|Password |String |No |test\*\*\*\* |Database account password. |
|MongoAuthSourceDB |String |No |ReplicaSet |Account verification database. When` EndpointType `is set to `Volc_Mongo`, the default value of this parameter is `root`. |
|DeployType |String |No |ShardedCluster |The instance type of MongoDB. The values are as follows:<br><br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47109#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |
|PullMethod |String |No |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |


<span id="volcelasticsearchsettings"></span>
### VolcElasticSearchSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |ztuc43y38z4w\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_ElasticSearch</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstances">DescribeInstances</a> interface to query the instance ID.</div><br> |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volckafkasettings"></span>
### VolcKafkaSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Kafka</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/kafka/DescribeInstancesSummary-v1">DescribeInstancesSummary</a> interface to query the Instance ID.</div><br> |
|AuthType |String |Yes |plain |Authentication method. The default value is `plain`. |
|Username |String |Yes |test\*\*\*\* |The username for the Kafka instance using the PLAIN mode. |
|Password |String |Yes |test\*\*\*\* |The password for the Kafka instance using the PLAIN mode. |
|Topic |String |Yes |my_topic |Kafka's Topic name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volcrocketmqsettings"></span>
### VolcRocketMQSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |MQ_INST_ ** *\*\*\*\*\** **  |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_RocketMQ</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/6410/67914">GetInstance</a> API to query the Instance ID.</div><br> |
|AuthType |String |Yes |plain |Authentication method. The default value is `plain`. |
|Username |String |Yes |test\*\*\*\* |The username of the RocketMQ instance. |
|Password |String |Yes |test\*\*\*\* |User password for RocketMQ instance. |
|Topic |String |Yes |my_topic |Topic name of RocketMQ. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volcredissettings"></span>
### VolcRedisSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Redis</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/redis/describedbinstances">DescribeDBInstances</a> interface to query the Instance ID.</div><br> |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47109#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="publicmysqlsettings"></span>
### PublicMySQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |Yes |4 |The port number of the self\-managed instance. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|SSLSettings |Object of [SSLSettings](https://docs.byteplus.com/en/docs/57/47109#sslsettings) |No |```JSON```<br>```{```<br>```    "EnableSSL": true,```<br>```    "Cert":"-----BEGIN CERTIFICATE----- ...... -----END CERTIFICATE-----"```<br>```}```<br><br><br> |Instance encryption information. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="sslsettings"></span>
### SSLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|EnableSSL |Boolean |No |false |Whether to enable SSL encryption connection method. The values are as follows:<br><br><br>* `true`: Indicates that SSL encryption is enabled.<br><br>* `false`: Indicates that SSL encryption is not enabled. |
|Cert |String |No |\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\- ...... \-\-\-\-\-END CERTIFICATE\-\-\-\-\- |CA certificate content.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>EnableSSL</code> is set to <code>true</code>, this parameter is required.</div><br> |


<span id="publicpostgresqlsettings"></span>
### PublicPostgreSQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |Yes |4 |The port number of the self\-managed instance. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="publicmongosettings"></span>
### PublicMongoSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br><br><br> |The region of the instance. |
|DeployType |String |Yes |Standalone |The type of MongoDB instance. The values are as follows:<br><br><br>* `Standalone`: Indicates a single node.<br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|PullMethod |String |No |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |
|Endpoints |Array of String |Yes |192.168.\*\*\*.\*\*\*:4 |Mongo address in the format of `host:port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |Yes |test\*\*\*\* |mongos database account. |
|Password |String |Yes |test\*\*\*\* |Database password of mongos. |
|MongoAuthSourceDB |String |Yes |admin |Authentication database name for mongos. |
|Shards |Array of [MongoShardSetting](https://docs.byteplus.com/en/docs/57/47109#mongoshardsetting) |No |```JSON```<br>```{```<br>```    "Address": "192.168.0.1:27019,192.168.0.1:27020",```<br>```    "Username": "test****",```<br>```    "Password": "test****",```<br>```    "AuthDb": "admin"```<br>```}```<br> |Shard address information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If used as a return parameter, the relevant information about the parameter is not returned.</div><br> |
|UseNewShardingDatasource |Boolean |No |true |Whether to select the new version of shard access method, with the following optional values:<br><br><br>* `false`: Indicates that the new shard access method is not used.<br><br>* `true`: Indicates that the new shard method is used. The default value is the shard set scenario for the deployment type. |


<span id="mongoshardsetting"></span>
### MongoShardSetting


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Address |String |No |192.168.0.1:27019,192.168.0.1:27020 |Shard address, such as `IP:Port` or `Domain:Port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |No |test\*\*\*\* |Database account. |
|Password |String |No |test\*\*\*\* |Database account password. |
|AuthDb |String |No |admin |Account verification database. |


<span id="publicelasticsearchsettings"></span>
### PublicElasticSearchSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Endpoints |Array of String |Yes |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="publicredissettings"></span>
### PublicRedisSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |Yes |4 |The port number of the self\-managed instance. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="builtinkafkasettings"></span>
### BuiltinKafkaSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Brokers |Array of String |Yes |&nbsp;<br><br>```JSON```<br>```[```<br>```     "100.67.158.158:9092",```<br>```     "100.67.158.158:9192",```<br>```     "100.67.158.158:9292",```<br>```     "100.67.158.158:9392",```<br>```     "100.67.158.158:9492"```<br>```]```<br> |The IP address and port number of the Broker, in the format of `host:port`. |
|Topic |String |Yes |6f2fd63c0ea947b280877f5d2a\*\*\*\*\*\* |Kafka's Topic ID. |


<span id="expressmongosettings"></span>
### ExpressMongoSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|DeployType |String |Yes |ShardedCluster |The instance type of the instance. The values are as follows:<br><br><br>* `Standalone`: Indicates a single node.<br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|PullMethod |String |No |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47109#privatenetworksettings) |Yes |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|Endpoints |Array of String |Yes |192.168.\*\*\*.\*\*\*:4 |Mongo address in the format of `host:port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |Yes |test\*\*\*\* |mongos database account. |
|Password |String |Yes |test\*\*\*\* |Database password of mongos. |
|MongoAuthSourceDB |String |Yes |admin |Authentication database name for mongos. |
|Shards |Array of [MongoShardSetting](https://docs.byteplus.com/en/docs/57/47109#mongoshardsetting) |No |```JSON```<br>```{```<br>```    "Address": "192.168.0.1:27019,192.168.0.1:27020",```<br>```    "Username": "test****",```<br>```    "Password": "test****",```<br>```    "AuthDb": "admin"```<br>```}```<br> |Shard address information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If used as a return parameter, the relevant information about the parameter is not returned.</div><br> |
|UseNewShardingDatasource |Boolean |No |true |Whether to select the new version of shard access method, with the following optional values:<br><br><br>* `false`: Indicates that the new shard access method is not used.<br><br>* `true`: Indicates that the new shard method is used. The default value is the shard set scenario for the deployment type. |


<span id="privatenetworksettings"></span>
### PrivateNetworkSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|VPCId |String |Yes |vpc\-bp1opxu1zkhn00gz\*\*\*\* |VPC ID. The VPC ID values are as follows, based on the connection method of the virtual private cloud:<br><br><br>* Direct connect: Set any VPC ID of the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Set the VPC ID bound to the VPN gateway when achieving data connectivity through VPN. |
|SubnetId |String |Yes |subnet\-bpkdt37pq72zv\*\*\*\* |Subnet ID within the VPC ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The subnet CIDR block must be added to the allowlist or security group rule of the target database.</div><br> |


<span id="expressmysqlsettings"></span>
### ExpressMySQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\* *.\*\*\**  |The host address of the MySQL instance connected over express network. |
|Port |Integer |Yes |4 |The port of the MySQL instance connected over express network. |
|Username |String |Yes |test\*\*\* |Database account of MySQL instance connected over express network. |
|Password |String |Yes |Admin@\*\*\* |Database account password of MySQL instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47109#privatenetworksettings) |Yes |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="expresspostgresqlsettings"></span>
### ExpressPostgreSQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\* *.\*\*\**  |The host address of the PostgreSQL instance connected over express network. |
|Port |Integer |Yes |4 |The port of the Express_Kafka instance connected over express network. |
|Username |String |Yes |test\*\*\* |Database account of PostgreSQL instance connected over express network. |
|Password |String |Yes |Admin@\*\*\* |Database account password of PostgreSQL instance connected over express network. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47109#privatenetworksettings) |Yes |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="expressredissettings"></span>
### ExpressRedisSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ArchType |String |No |Standalone |Architecture type. The values are as follows:<br><br><br>* `Standalone`: `Standalone edition`.<br><br>* `Cluster`: `Cluster edition`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the cluster of the Redis connected over express network instance has a proxy service, the <code>ArchType</code> must be set to <code>Standalone</code>.</div><br> |
|Host |String |No |192.168.\*\*\*.\*\*\* |The host address of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the parameter <code>ArchType</code> is set to <code>Standalone</code>.</div><br> |
|Port |Integer |No |4 |The port of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter must be set when <code>ArchType</code> is set to <code>Standalone</code>.</div><br> |
|Endpoints |Array of String |No |10.10.10.10:3717 |Enter the` IP: port` of the primary nodes for each shard of the Cache for Redis cluster in the private network connected via the dedicated line, separated by commas. For example: `ip1:port1,ip2:port2,ip3:port3`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the parameter <code>ArchType</code> is set to <code>Cluster</code>.</div><br> |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47109#privatenetworksettings) |No |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|Username |String |No |test\*\*\* |Database account of the Redis instance connected over express network. |
|Password |String |No |Admin@\*\*\* |Database account password of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the parameter <code>ArchType</code> is set to <code>Cluster</code>, passwords for multiple shards must be consistent; otherwise, connection can not be established.</div><br> |


<span id="expresselasticsearchsettings"></span>
### ExpressElasticSearchSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Endpoints |Array of String |No |[192.168.\*\*\* *.\*\*\** ] |The host address of ElasticSearch connected over express network. |
|Username |String |No |test\*\*\* |Database account of the Elasticsearch instance connected over express network. |
|Password |String |No |Admin@\*\*\* |Database account password of ElasticSearch instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47109#privatenetworksettings) |No |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="expresskafkasettings"></span>
### ExpressKafkaSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|BrokerEndpoints |Array of String |No |[10.1.\*\*\*.\*\*\*:9093] |The IP address and port number of the Kafka connected over express network instance Broker, in the format of `host1:port1`. If there are multiple Brokers, separate them with commas (,). |
|AuthType |String |No |plain |Authentication method. The default value is `plain`. |
|Username |String |No |test\*\*\* |Database account of the Kafka instance connected over express network. |
|Password |String |No |Admin@\*\*\* |Database account password of the Kafka instance connected over express network. |
|Topic |String |No |dts_sydtest |Topic information of the Kafka instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47109#privatenetworksettings) |No |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47109#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="solutionsettings"></span>
### SolutionSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SolutionType |String |Yes |MySQL2MySQL |Task type. The values are as follows:<br><br><br>* `MySQL2MySQL`: Indicates a migration or synchronization task from MySQL to MySQL.<br><br>* `MySQL2ES`: Indicates a synchronization task from MySQL to Elasticsearch.<br><br>* `MySQL2Kafka`: Indicates a subscription task from MySQL to Kafka.<br><br>* `MySQL2RocketMQ`: Indicates a subscription task from MySQL to RocketMQ.<br><br>* `Pg2pg`: Indicates a migration or synchronization task from PostgreSQL to PostgreSQL.<br><br>* `PG2Kafka`: Indicates a subscription task from PostgreSQL to Kafka.<br><br>* `Pg2rocketmq`: Indicates a subscription task from PostgreSQL to RocketMQ.<br><br>* `Mongo2Mongo`: Indicates a migration or synchronization task from MongoDB to MongoDB.<br><br>* `Redis2Redis`: Indicates a migration or synchronization task from Redis to Redis.<br><br>* `MySQL2MySQLMigrationAssessment`: Indicates a migration evaluation task from MySQL to MySQL.<br><br>* `MySQL2MySQLDataValidation`: Indicates a verification task from MySQL to MySQL.<br><br>* `PG2PGDataValidation`: Indicates a verification task from PostgreSQL to PostgreSQL.<br><br>* `Mongo2MongoDataValidation`: Indicates a verification task from MongoDB to MongoDB.<br><br>* `Mongo2RocketMQ`: Indicates a migration or synchronization task from MongoDB to RocketMQ.<br><br>* `Redis2RocketMQ`: Indicates a migration or synchronization task from Redis to RocketMQ.<br><br>* `MSSQL2MSSQL`: Indicates a migration task from SQL Server to SQL Server.<br><br>* `MySQL2MySQLRowCompare`: Indicates a full validation task from MySQL to MySQL.<br><br>* `MySQL2MySQLIncrDataValidation`: Indicates an increment validation task from MySQL to MySQL.<br><br>* `MySQL2MySQLRowCountCompare`: Indicates a row verification task from MySQL to MySQL.<br><br>* `MySQL2MySQLMetaCompare`: Indicates a schema verification task from MySQL to MySQL.<br><br>* `PG2PGRowCompare`: Indicates a full data verification task from PostgreSQL to PostgreSQL.<br><br>* `Mongo2MongoRowCompare`: Indicates a full data verification task from MongoDB to MongoDB.<br><br>* `Mongo2MongoPkCompare`: Indicates a primary key validation task from MongoDB to MongoDB.<br><br>* `Mongo2MongoIncrDataValidation`: Indicates an increment validation task from MongoDB to MongoDB.<br><br>* `Mongo2MongoRowCountCompare`: Indicates a row verification task from MongoDB to MongoDB.<br><br>* `Redis2RedisRowCompare`: Indicates a full validation task from Redis to Redis.<br><br>* `MSSQL2MSSQLRowCompare`: Indicates a full validation task from SQL Server to SQL Server.<br><br>* `MSSQL2MSSQLRowCountCompare`: Indicates a row verification task from SQL Server to SQL Server.<br><br>* `Milvus2Milvus`: Indicates a migration or synchronization task from Milvus to Milvus. |
|AutoStart |Boolean |No |false |Whether to automatically start the task after task creation. The values are as follows:<br><br><br>* `true`: indicates automatic start of the task.<br><br>* `false`: (default) indicates the task does not start automatically and requires manual start. |
|MySQL2MySQLSettings |Object of [MySQL2MySQLSettings](https://docs.byteplus.com/en/docs/57/47109#mysql2mysqlsettings) |No |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```    },```<br>```    "EnableForeignKeyChecks": false,```<br>```    "EnableFullIncr": true,```<br>```    "EnableFullTrxPartitionByChunk": false,```<br>```    "EnableTriggerPreMigration": false,```<br>```    "EnableTrxRewrite": false,```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true,```<br>```        "Snapshot": false```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true,```<br>```        "Statements": [```<br>```            "StmtDDLAll",```<br>```            "StmtDMLDelete",```<br>```            "StmtDMLInsert",```<br>```            "StmtDMLUpdate"```<br>```        ]```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "test",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta",```<br>```                            "Incr",```<br>```                            "Full"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableOverride",```<br>```                        "SetObjectTransType": true```<br>```                    },```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "View",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Function",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Procedure",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Trigger",```<br>```                    "SrcObjName": "*"```<br>```                },```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Event",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectMappingSetting": {```<br>```                "LastWriteWinsKey": "",```<br>```                "ObjectTransTypes": [```<br>```                    "Meta",```<br>```                    "Full",```<br>```                    "Incr"```<br>```                ],```<br>```                "PolicyForKeyConflict": "TableOverride",```<br>```                "SetObjectTransType": true```<br>```            },```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "test"```<br>```        }```<br>```    ],```<br>```    "PolicyForPrimaryKeyConflict": "Override"```<br>```}```<br> |When the `SolutionType` is set to `MySQL2MySQL`, it refers to the parameter configuration for the migration or synchronization from source instances of MySQL to target instances of MySQL. This parameter is required. |
|MySQL2ESSettings |Object of [MySQL2ESSettings](https://docs.byteplus.com/en/docs/57/47109#mysql2essettings) |No |```JSON```<br>```{```<br>```    "ESExtraArgs": {```<br>```        "Analyzer": "",```<br>```        "CustomIndexType": "",```<br>```        "IdxNameRule": "DBAndTable",```<br>```        "InsertMode": "<UNSET>",```<br>```        "ReplicaNum": 1,```<br>```        "RetryTimes": 0,```<br>```        "ShardNum": 5,```<br>```        "TZ": ""```<br>```    },```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true,```<br>```        "Statements": [```<br>```            "StmtDMLDelete",```<br>```            "StmtDMLInsert",```<br>```            "StmtDMLUpdate"```<br>```        ]```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "testdb_bak",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "testdb_bak_auth_operation",```<br>```                    "ObjectMappingSetting": {```<br>```                        "ESMetaMappingSetting": {```<br>```                            "EnableRouting": false,```<br>```                            "TypeName": ""```<br>```                        },```<br>```                        "LastWriteWinsKey": "",```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": false```<br>```                    },```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "auth_operation"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "testdb_bak"```<br>```        }```<br>```    ],```<br>```    "PolicyForPrimaryKeyConflict": "Override"```<br>```}```<br><br><br> |When the `SolutionType` is set to `MySQL2ES`, it refers to the parameter configuration for the synchronization from source instances of Elasticsearch to target instances of MySQL. This parameter is required. |
|MySQL2KafkaSettings |Object of [MySQL2KafkaSettings](https://docs.byteplus.com/en/docs/57/47109#mysql2kafkasettings) |No |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "EnableFullIncr": true,```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 7200```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true,```<br>```        "Statements": [```<br>```            "StmtDMLInsert",```<br>```            "StmtDMLUpdate",```<br>```            "StmtDMLDelete",```<br>```            "StmtDDLAll"```<br>```        ]```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "huahua",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "auth_operation",```<br>```                    "ObjectMappingSetting": {```<br>```                        "LastWriteWinsKey": "",```<br>```                        "ObjectTransTypes": [```<br>```                            "Meta",```<br>```                            "Incr",```<br>```                            "Full"```<br>```                        ],```<br>```                        "PolicyForKeyConflict": "TableNone",```<br>```                        "SetObjectTransType": true```<br>```                    },```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "auth_operation"```<br>```                }```<br>```            ],```<br>```            "ObjectMappingSetting": {```<br>```                "LastWriteWinsKey": "",```<br>```                "ObjectTransTypes": [```<br>```                    "Full",```<br>```                    "Incr",```<br>```                    "Meta"```<br>```                ],```<br>```                "PolicyForKeyConflict": "TableNone",```<br>```                "SetObjectTransType": true```<br>```            },```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "huahua"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "PartitionPolicy": "Table",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "",```<br>```        "VPCSubnetId": ""```<br>```    }```<br>```}```<br><br><br> |When the value of `SolutionType` is `MySQL2Kafka`, it refers to the parameter configuration for subscribing source instances of MySQL to Kafka, and this parameter is required. |
|MySQL2RocketMQSettings |Object of [MySQL2RocketMQSettings](https://docs.byteplus.com/en/docs/57/47109#mysql2rocketmqsettings) |No |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": true```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": false```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": true```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "database1",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "database1"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "PartitionPolicy": "Table",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "",```<br>```        "VPCSubnetId": ""```<br>```    }```<br>```}```<br><br><br> |When the value of `SolutionType` is `MySQL2RocketM`, it refers to the parameter configuration for subscribing source instances of MySQL to Message Queue for RocketMQ. This parameter is required. |
|PG2PGSettings |Object of [PG2PGSettings](https://docs.byteplus.com/en/docs/57/47109#pg2pgsettings) |No |```JSON```<br>```{```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "0",```<br>```            "DestObjName": "0"```<br>```        },```<br>```        {```<br>```            "ObjectType": "Table",```<br>```            "SrcObjName": "1",```<br>```            "DestObjName": "1"```<br>```        },```<br>```        {```<br>```            "ObjectType": "View",```<br>```            "SrcObjName": "2",```<br>```            "DestObjName": "2"```<br>```        },```<br>```        {```<br>```            "ObjectType": "PostSequence",```<br>```            "SrcObjName": "3",```<br>```            "DestObjName": "3"```<br>```        }```<br>```    ],```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": "true"```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableMeta": "true"```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableMeta": "true"```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 7200```<br>```    }```<br>```}```<br> |When `SolutionType` is set to `PG2PG`, it refers to the parameter configuration for migrating source instances of PostgreSQL to target instances of PostgreSQL, and this parameter is required. |
|PG2KafkaSettings |Object of [PG2KafkaSettings](https://docs.byteplus.com/en/docs/57/47109#pg2kafkasettings) |No |```JSON```<br>```{```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 7200```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": false```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": false```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "public",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "public"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "vpc-3ez4xswg5j94w72200ry****",```<br>```        "VPCSubnetId": "subnet-3ez4xts0nc4qo72200r******"```<br>```    }```<br>```}```<br> |When the value of `SolutionType` is `PG2Kafka`, it refers to the parameter configuration for subscribing source instances of PostgreSQL to Kafka, and this parameter is required. |
|PG2RocketMQSettings |Object of [PG2RocketMQSettings](https://docs.byteplus.com/en/docs/57/47109#pg2rocketmqsettings) |No |```JSON```<br>```{```<br>```    "ETLSettings": {```<br>```        "Script": ""```<br>```    },```<br>```    "ErrorBehaviorSettings": {```<br>```        "MaxRetrySeconds": 600```<br>```    },```<br>```    "FullTransmissionSettings": {```<br>```        "EnableFull": false```<br>```    },```<br>```    "IncrTransmissionSettings": {```<br>```        "EnableIncr": true```<br>```    },```<br>```    "MetaTransmissionSettings": {```<br>```        "EnableMeta": false```<br>```    },```<br>```    "ObjectMappings": [```<br>```        {```<br>```            "DestObjName": "public",```<br>```            "MappingList": [```<br>```                {```<br>```                    "DestObjName": "*",```<br>```                    "ObjectType": "Table",```<br>```                    "SrcObjName": "*"```<br>```                }```<br>```            ],```<br>```            "ObjectType": "Database",```<br>```            "SrcObjName": "public"```<br>```        }```<br>```    ],```<br>```    "SubscriptionSettings": {```<br>```        "EnableBeginCommitMessage": false,```<br>```        "EnableMultiTopic": false,```<br>```        "Location": "",```<br>```        "PartitionPolicy": "Table",```<br>```        "Protocol": "Volc",```<br>```        "SubscribePartBeforeImage": false,```<br>```        "VPCId": "",```<br>```        "VPCSubnetId": ""```<br>```    }```<br>```}```<br><br><br> |When the value of` SolutionType` is `PG2RocketMQ`, it refers to the parameter configuration for subscribing source instances of PostgreSQL to Message Queue for RocketMQ. This parameter is required. |
|Mongo2MongoSettings |Object of [Mongo2MongoSettings](https://docs.byteplus.com/en/docs/57/47109#mongo2mongosettings) |No |```JSON```<br>```{```<br>```    "TaskName": "test",```<br>```    "TrafficSpec": "Standard",```<br>```    "ProjectName": "default",```<br>```    "Tags": [```<br>``````<br>```    ],```<br>```    "CreateBackwardSyncTask": false,```<br>```    "ChargeConfig": {```<br>```        "ChargeType": "PostPaid",```<br>```        "Times": 1```<br>```    },```<br>```    "SrcConfig": {```<br>```        "EndpointType": "Public_Mongo",```<br>```        "PublicMongoSettings": {```<br>```            "RegionSettings": {```<br>```                "Region": "×××××××××"```<br>```            },```<br>```            "DeployType": "ShardedCluster",```<br>```            "PullMethod": "Oplog",```<br>```            "Endpoints": [```<br>```                "192.168..***.***:27***"```<br>```            ],```<br>```            "MongoAuthSourceDB": "admin",```<br>```            "Username": "root",```<br>```            "Password": "admin",```<br>```            "Shards": [```<br>```                {```<br>```                    "Username": "root",```<br>```                    "Password": "admin",```<br>```                    "Address": "192.168.***.***:27***,192.168.***.***:27***",```<br>```                    "AuthDb": "admin"```<br>```                },```<br>```                {```<br>```                    "Address": "192.168.***.***:27***,192.168.***.***:27***",```<br>```                    "AuthDb": "admin",```<br>```                    "Username": "root",```<br>```                    "Password": "admin"```<br>```                }```<br>```            ],```<br>```            "UseNewShardingDatasource": true```<br>```        }```<br>```    },```<br>```    "DestConfig": {```<br>```        "EndpointType": "Volc_Mongo",```<br>```        "VolcMongoSettings": {```<br>```            "RegionSettings": {```<br>```                "Region": "×××××××××"```<br>```            },```<br>```            "DeployType": "ShardedCluster",```<br>```            "PullMethod": "None",```<br>```            "DBInstanceId": "mongo-shard-××××××××",```<br>```            "Username": "root",```<br>```            "Password": "admin",```<br>```            "UseNewShardingDatasource": true```<br>```        }```<br>```    },```<br>```    "SolutionSettings": {```<br>```        "SolutionType": "Mongo2Mongo",```<br>```        "Mongo2MongoSettings": {```<br>```            "TaskRunType": [```<br>```                "Incr",```<br>```                "Full",```<br>```                "Meta"```<br>```            ],```<br>```            "PolicyForMongoPrimaryKeyConflict": "Override",```<br>```            "ObjectMappings": [```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "test",```<br>```                    "DestObjName": "test",```<br>```                    "MappingList": [```<br>```                        {```<br>```                            "ObjectType": "Table",```<br>```                            "SrcObjName": "*",```<br>```                            "DestObjName": "*"```<br>```                        }```<br>```                    ]```<br>```                }```<br>```            ],```<br>```            "ErrorBehaviorSettings": {```<br>```                "MaxRetrySeconds": 600```<br>```            },```<br>```            "FullTransmissionSettings": {```<br>```                "FullSyncParalell": 8,```<br>```                "EnableFull": true```<br>```            },```<br>```            "AccountTransmissionSettings": {```<br>```                "EnableAccount": false```<br>```            },```<br>```            "MetaTransmissionSettings": {```<br>```                "EnableMeta": true```<br>```            },```<br>```            "IncrTransmissionSettings": {```<br>```                "EnableIncr": true```<br>```            }```<br>```        }```<br>```    },```<br>```    "TaskType": "DataSynchronization"```<br>```}```<br> |When `SolutionType` is set to `Mongo2Mongo`, it refers to the parameter configuration for migrating source instances of MongoDB to target instances of MongoDB, and this parameter is required. |
|Redis2RedisSettings |Object of [Redis2RedisSettings](https://docs.byteplus.com/en/docs/57/47109#redis2redissettings) |No |```JSON```<br>```{```<br>```    "TaskName": "rudonxxxxx-1",```<br>```    "TaskType": "DataMigration",```<br>```    "TrafficSpec": "Compact",```<br>```    "ProjectName": "default",```<br>```    "Tags": [```<br>```        {```<br>```            "Key": "key1",```<br>```            "Value": "value1"```<br>```        }```<br>```    ],```<br>```    "SrcConfig": {```<br>```        "EndpointType": "Public_Redis",```<br>```        "PublicRedisSettings": {```<br>```            "Host": "192.168.***.***",```<br>```            "Port": 4,```<br>```            "Username": "test****",```<br>```            "Password": "test****",```<br>```            "DBName": "test****",```<br>```            "RegionSettings": {```<br>```                "Region": "cn-beijing"```<br>```            }```<br>```        }```<br>```    },```<br>```    "DestConfig": {```<br>```        "EndpointType": "Volc_Redis",```<br>```        "VolcRedisSettings": {```<br>```            "RegionSettings": {```<br>```                "Region": "cn-beijing"```<br>```            },```<br>```            "DBInstanceId": "redis-cnlfe66ipof9y86qz",```<br>```            "Username": "default",```<br>```            "Password": "ASDFasdf@2020"```<br>```        }```<br>```    },```<br>```    "SolutionSettings": {```<br>```        "SolutionType": "Redis2Redis",```<br>```        "Redis2RedisSettings": {```<br>```            "ObjectMappings": [```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "0",```<br>```                    "DestObjName": "0"```<br>```                },```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "1",```<br>```                    "DestObjName": "1"```<br>```                },```<br>```                {```<br>```                    "ObjectType": "Database",```<br>```                    "SrcObjName": "2",```<br>```                    "DestObjName": "2"```<br>```                }```<br>```            ],```<br>```            "ErrorBehaviorSettings": {```<br>```                "MaxRetrySeconds": 7200```<br>```            },```<br>```            "FullTransmissionSettings": {```<br>```                "EnableFull": true```<br>```            },```<br>```            "IncrTransmissionSettings": {```<br>```                "EnableIncr": false```<br>```            }```<br>```        }```<br>```    },```<br>```    "ChargeConfig": {```<br>```        "ChargeType": "PostPaid"```<br>```    }```<br>```}```<br> |When `SolutionType` is set to `Redis2Redis`, it refers to the parameter configuration for migrating source instances of Redis to target instances of Redis, and this parameter is required. |


<span id="mysql2mysqlsettings"></span>
### MySQL2MySQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|EnableForeignKeyChecks |Boolean |Yes |false |Select whether to enable foreign key check as needed. When enabled, the tool supports migrating cascading updates and deletes of foreign keys from the source, ensuring data integrity and consistency throughout the migration. The values are as follows:<br><br><br>* `true`: Indicates that foreign key check is enabled.<br><br>* `false`: (default) Indicates that foreign key check is disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter supports configuration only when <code>TaskType</code> is <code>DataMigration</code>.</div><br> |
|AccountTransmissionSettings |Object of [AccountTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#accounttransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableAccount": true```<br>```}```<br><br><br> |Migrates specified non\-system accounts and their associated permissions from the source database to the target database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is only supported when <code>TaskType</code> is set to <code>DataMigration</code> or <code>DataSynchronization</code>.</div><br> |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br><br><br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |
|MySQLPosition |Object of [MySQLPosition](https://docs.byteplus.com/en/docs/57/47109#mysqlposition) |No |```JSON```<br>```{```<br>```"Gtid": "3e11fa47-71ca-11e1-9e33-c80aa9429562:58",```<br>```"Gset":"f76eb90f-82a2-11e5-a162-7ca23e9126c5:3",```<br>```"Timestamp":1679642652```<br>```}```<br> |Set to pull Binlog logs from a specified position or timestamp.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>TaskType</code> is set to <code>DataSynchronization</code>, this configuration parameter is not supported during full initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When this parameter is not set, it defaults to the earliest point in time that the system can recognize.</div><br> |
|PolicyForPrimaryKeyConflict |String |No |Override |Primary key conflict handling. The processing method when a row with the same primary key value already exists in the target database. The values are as follows:<br><br><br>* `ThrowError`: Indicates abort on conflict. An error is reported during the pre\-check, and the relevant data needs to be modified manually. Otherwise, the synchronization task can not be started.<br><br>* `Ignore`: Indicates ignore on conflict. During the pre\-check, rows with the same primary key value in the target database will be skipped, and the synchronization task can be started normally.<br><br>* `Override`: Overwrite on conflict. Use the source database data to overwrite the target database data. The synchronization task can be started normally.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the value is <code>Ignore</code>, it may cause data to be inconsistent, posing risks to the business. Choose carefully.</div><br> |
|AccountMapping |Array of [AccountMapping](https://docs.byteplus.com/en/docs/57/47109#accountmapping) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Account": "test****",```<br>```    "ResetPassword": "true",```<br>```    "Password": "*Test****"```<br>```}```<br> |The database account information to be migrated.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter supports configuration only when <code>TaskType</code> is <code>DataMigration</code> or <code>DataSynchronization</code>.</div><br> |
|EnableTrxRewrite |Boolean |No |true |Select whether to enable transaction merging when transmitting data. Enabling transaction merging optimizes transmission tasks by combining multiple individual transactions, improving overall efficiency and performance while ensuring data consistency. When data transmission occurs frequently with large volumes, enabling transaction merging enhances the transmission efficiency.<br><br><br>* `true`: Indicates that transaction merging is enabled.<br><br>* `false`: (Default) Indicates that transaction merging is not enabled. |


<span id="objectmapping"></span>
### ObjectMapping


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ObjectType |String |Yes |Function |Object type. The values are as follows:<br><br><br>* `Database`: indicates a database.<br><br>* `Table`: indicates a table.<br><br>* `View`: indicates a view.<br><br>* `Column`: Indicates the `column`.<br><br>* `Function`: Indicates the `function`.<br><br>* `Procedure`: Indicates the `procedure`.<br><br>* `Trigger`: Indicates the `trigger`.<br><br>* `Type`: Indicates the `type`.<br><br>* `Domain`: Indicates the `domain`.<br><br>* `Sequence`: Indicates the `sequence`.<br><br>* `Rule`: Indicates the `rule`.<br><br>* `Operator`: Indicates the `operator`.<br><br>* `Aggregate`: Indicates the `aggregate`.<br><br>* `Extension`: Indicates an extension.<br><br>* `Constraint`: Indicates a constraint.<br><br>* `PostSequence`: Indicates a PostgreSQL sequence.<br><br>* `Schema`: Indicates a mode.<br><br>* `Event`: Indicates an event.<br><br>* `DomainConstraint`: Indicates a domain constraint. |
|SrcObjName |String |Yes |ceshi\*\*\*\* |Source object name. |
|DestObjName |String |Yes |test\*\*\*\* |Target object name. |
|MappingList |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |No |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Transmission task object. |
|ObjectMappingSetting |Object of [ObjectMappingSetting](https://docs.byteplus.com/en/docs/57/47109#objectmappingsetting) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ESMetaMappingSetting": {```<br>```        "PidCol": [```<br>```            "id",```<br>```            "name"```<br>```        ],```<br>```        "EnableRouting": true,```<br>```        "RoutingCol": [```<br>```            "id"```<br>```        ]```<br>```    }```<br>```}```<br> |Additional parameter information that needs to be configured when synchronizing data to Elasticsearch. |


<span id="objectmappingsetting"></span>
### ObjectMappingSetting


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ESMetaMappingSetting |Object of [ESMetaMappingSetting](https://docs.byteplus.com/en/docs/57/47109#esmetamappingsetting) |No |```JSON```<br>```{```<br>```    "PidCol": [```<br>```        "id",```<br>```        "name"```<br>```    ],```<br>```    "EnableRouting": true,```<br>```    "RoutingCol": [```<br>```        "id"```<br>```    ]```<br>```}```<br> |Structure mapping parameters of Elasticsearch. |


<span id="esmetamappingsetting"></span>
### ESMetaMappingSetting


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|PidCol |Array of String |No |["id", "name"] |Primary key (_id) value. If this parameter is not set, the default is the column of the primary key. |
|EnableRouting |Boolean |No |EnableRouting |Whether to enable Routing. The values are as follows:<br><br><br>* `true`: Indicates that Routing is enabled.<br><br>* `false`: Indicates that Routing is not enabled. |
|RoutingCol |Array of String |No |["id"] |The value of `_routing`. This parameter is required when `EnableRouting` is set to `true`. |


<span id="accounttransmissionsettings"></span>
### AccountTransmissionSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|EnableAccount |Boolean |No |false |Whether to enable user migration. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `false`: Indicates disabled. |


<span id="metatransmissionsettings"></span>
### MetaTransmissionSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|EnableMeta |Boolean |No |true |Whether to enable the migration or subscription of database and table structures. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `false`: Indicates disabled. |
|DisablePostMeta |Boolean |No |true |When you select schema migration/schema initialization as the PostgreSQL database migration/synchronization type, DTS will automatically migrate/synchronize the post\-schema after incremental migration/synchronization concludes. Alternatively, you can choose to skip post\-schema migration/synchronization, meaning DTS will not migrate/synchronize the post\-schema.<br><br>PostgreSQL database post\-schema synchronization and migration objects include ordinary trigger, event trigger, RULE, exclusive constraint, foreign key constraint, check constraint, Domain constraint, and Sequence value setting.<br><br>Whether to skip PostgreSQL post\-schema migration or post\-schema synchronization. The values are as follows:<br><br><br>* `true`: Indicates skipping PostgreSQL post\-schema migration or post\-schema synchronization.<br><br>* `false`: Indicates not skipping PostgreSQL post\-schema migration or post\-schema synchronization. |


<span id="fulltransmissionsettings"></span>
### FullTransmissionSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|EnableFull |Boolean |No |true |Whether to enable full migration, full subscription, or full initialization. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `False`: indicates disabled (default value). |
|Snapshot |Boolean |No |true |Whether to enable full data consistency migration. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `False`: indicates disabled (default value). |
|ExtraConditions |Array of [FullExtraCondition](https://docs.byteplus.com/en/docs/57/47109#fullextracondition) |No |```JSON```<br>```{```<br>```    "Db": "TestName",```<br>```    "Table": "TableName",```<br>```    "WhereSql": "id = 5"```<br>```}```<br> |Full filter condition. |
|RPSLimit |Integer |No |100,000 |Rows migrated or synchronized per second. The value range is 1 to 100,000, and the default value is 100,000. |
|BPSLimit |Integer |No |25000 |Data volume migrated or synchronized per second. The value range is 1 to 25,000 (KB), and the default value is 25,000. |
|FullSyncParalell |Integer |No |8 |Concurrency of the migration or synchronization task. The default value is 8, and the valid range is 1 to 64. |


<span id="fullextracondition"></span>
### FullExtraCondition


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Db |String |No |TestName |The database name to be filtered. |
|Table |String |No |TableName |Table names to be filtered. |
|WhereSql |String |No |id = 5 |Filtered SQL statements. |


<span id="incrtransmissionsettings"></span>
### IncrTransmissionSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|EnableIncr |Boolean |No |true |Whether to enable incremental migration, incremental subscription, or incremental synchronization. The values are as follows:<br><br><br>* `true`: Indicates enabled.<br><br>* `False`: indicates disabled (default value).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|Statements |Array of String |No |&nbsp;<br><br>```JSON```<br>```[```<br>```     "StmtDDLAll",```<br>```     "StmtDMLDelete",```<br>```      "StmtDMLUpdate",```<br>```     "StmtDMLInsert"```<br>```]```<br> |The operation statements to be transmitted. The values are as follows:<br><br><br>* `StmtDMLInsert`<br><br>* `StmtDMLUpdate`<br><br>* `StmtDMLDelete`<br><br>* `StmtDDLAll`<br><br>* `StmtDDLAlterTable`<br><br>* `StmtDDLAlterView`<br><br>* `StmtDDLCreateFunction`<br><br>* `StmtDDLCreateIndex`<br><br>* `StmtDDLCreateProcedure`<br><br>* `StmtDDLCreateTable`<br><br>* `StmtDDLCreateView`<br><br>* `StmtDDLDropIndex`<br><br>* `StmtDDLDropTable`<br><br>* `StmtDDLDropFunction`<br><br>* `StmtDDLDropProcedure`<br><br>* `StmtDDLTruncateTable`<br><br>* `StmtDDLRenameTable`<br><br>* `StmtDDLDropView` |


<span id="etlsettings"></span>
### ETLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Script |String |No |```json```<br>```(defn        desensitization        []```<br>```                (dts/match-table        "user"        (dts/map-column        'id_card        str/md5)))```<br> |Script for streaming data ETL. For syntax information about script dependencies, refer to [DSL syntax](https://docs.byteplus.com/en/docs/DTS/dsl_syntax). |


<span id="errorbehaviorsettings"></span>
### ErrorBehaviorSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|MaxRetrySeconds |Integer |No |600 |Maximum error retry time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |


<span id="mysqlposition"></span>
### MySQLPosition


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Gtid |String |No |3e11fa47\-71ca\-11e1\-9e33\-c80aa9429562:58 |Indicates that the Binlogs are pulled from the specified GTID in the format of `source_id:transaction_id`. |
|Gset |String |No |f76eb90f\-82a2\-11e5\-a162\-7ca23e9126c5:3 |Indicates that the Binlog logs are pulled from the specified GTID_EXECUTED, in the format of `source_id:transaction_id`. When there are multiple GTID_EXECUTEDs, they can be separated by commas (,).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For how to obtain the instance's GTID_EXECUTED, refer to <a href="https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance">How to obtain the GTID_EXECUTED of the instance</a>.</div><br> |
|Timestamp |Long |No |1679642652 |Indicates that the Binlog logs are pulled from the specified timestamp. |


<span id="accountmapping"></span>
### AccountMapping


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Account |String |Yes |test\*\*\*\* |The account name to be migrated. |
|ResetPassword |Boolean |No |true |Whether to reset the password. The values are as follows:<br><br><br>* `true`: Indicates resetting to a new password.<br><br>* `false`: Indicates not resetting to a new password. Default value. |
|Password |String |No |\*Test\*\*\*\* |The new password of the account to be migrated. |


<span id="mysql2essettings"></span>
### MySQL2ESSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |No |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "huahua",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectType": "Table",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "huahua"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |Streaming data ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |
|ESExtraArgs |Object of [ESExtraArgs](https://docs.byteplus.com/en/docs/57/47109#esextraargs) |No |```JSON```<br>```{```<br>```    "IdxNameRule": "Table",```<br>```    "ShardNum": 3,```<br>```    "ReplicaNum": 1,```<br>```    "TZ": "UTC +08:00",```<br>```    "RetryTimes": 600,```<br>```    "Analyzer": "standard",```<br>```    "InsertMode": "Replace"```<br>```}```<br> |Parameter information when synchronizing to Elasticsearch. |
|PolicyForPrimaryKeyConflict |String |No |ThrowError |Primary key conflict handling. The processing method when a row with the same primary key value already exists in the target database. The values are as follows:<br><br><br>* `ThrowError`: Indicates abort on conflict. An error is reported during the pre\-check, and the relevant data needs to be modified manually. Otherwise, the synchronization task can not be started.<br><br>* `Ignore`: Indicates ignore on conflict. During the pre\-check, rows with the same primary key value in the target database will be skipped, and the synchronization task can be started normally.<br><br>* `Override`: Overwrite on conflict. Use the source database data to overwrite the target database data. The synchronization task can be started normally.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When set to <code>Ignore</code>, it may cause data inconsistency and pose risks to business. Select with caution.</div><br> |


<span id="esextraargs"></span>
### ESExtraArgs


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|IdxNameRule |String |No |Table |Index concatenation rule<br><br><br>* `Table`: Indicates the table name concatenation method is used.<br><br>* `DBAndTable`: Indicates the database name + table name concatenation method is used. |
|ShardNum |Long |No |3 |Number of shard(s) |
|ReplicaNum |Long |No |1 |Number of copies. |
|TZ |String |No |UTC +08:00 |Time zone. Supports UTC\-12:00 to +13:00. The default value is the time zone of the Region. |
|RetryTimes |Long |No |7200 |Error retry time. |
|Analyzer |String |No |standard |The supported analyzer. |
|InsertMode |String |No |Replace |Insert in the source end. The values are as follows:<br><br><br>* `Replace`: Indicates that when a corresponding index does not exist on the target end, a new data entry will be inserted; when a corresponding index does exist, the corresponding index will be updated.<br><br>* `Update`: Indicates that when a corresponding index does not exist on the target end, it will be skipped. When a corresponding index exists on the target end, the corresponding data will be updated. |


<span id="mysql2kafkasettings"></span>
### MySQL2KafkaSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47109#subscriptionsettings) |Yes |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "AttachPoints.1.SubnetId=subnet-2fexiqjlgjif45oxruvso****&AttachPoints.2.SubnetId=subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": false,```<br>```    "SubscribePartBeforeImage": false```<br>```}```<br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|MySQLPosition |Object of [MySQLPosition](https://docs.byteplus.com/en/docs/57/47109#mysqlposition) |No |```JSON```<br>```{```<br>```    "Gtid": "3e11fa47-71ca-11e1-9e33-c80aa9429562:58",```<br>```    "Gset": "f76eb90f-82a2-11e5-a162-7ca23e9126c5:3",```<br>```    "Timestamp": 1679642652```<br>```}```<br> |Set to pull Binlog logs from a specified position or timestamp. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter configuration is not supported during full initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When this parameter is not set, it defaults to the earliest point in time that the system can recognize.</div><br> |


<span id="subscriptionsettings"></span>
### SubscriptionSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Protocol |String |No |Volc |The subscription format. The values are as follows:<br><br><br>* `Volc`: Indicates BytePlus Proto.<br><br>* `Canal`: Indicates Canal Proto.<br><br>* `CanalJSON`: Indicates Canal JSON.<br><br>* `Avro`: Indicates the Avro format.<br><br>* `DebeziumJSON`: DebeziumJSON: Indicates Debezium JSON format.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details on subscription formats, refer to <a href="https://docs.byteplus.com/en/docs/DTS/data_subscription_format">Data subscription format</a>.</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>Protocol</code> is set to <code>DebeziumJSON</code>, <code>ProgressType</code> can not be set to <code>Meta</code>.</div><br> |
|PartitionPolicy |String |No |P0 |The Partition reception policy for the Topic. The values are as follows:<br><br><br>* `P0`: Indicates unified delivery to Partition 0.<br><br>* `Table`: Indicates delivery to different Partitions based on the combined hash value of the database name and table name.<br><br>* `Key`: Indicates deliver to different Partitions based on the hash value of the primary key.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSubscription</code> and <code>EndpointType</code> is <code>Volc_Kafka</code>, this configuration is supported.</div><br> |
|VPCId |String |No |vpc\-bp1opxu1zkhn00gz\*\*\*\* |VPC ID. |
|VPCSubnetId |String |No |AttachPoints.1.SubnetId=subnet\-2fexiqjlgjif45oxruvso\*\*\*\*&AttachPoints.2.SubnetId=subnet\-7rtsu6whhle6j\*\*\*\* |Subnet ID within the VPC ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The subnet in the target VPC must have at least one available IP.</div><br> |
|EnableBeginCommitMessage |Boolean |No |false |Set whether to subscribe to messages by transaction as needed to ensure message consistency and completeness. The values are as follows:<br><br><br>* `true`: Indicates subscription to Begin/Commit messages.<br><br>* `false`: (Default) Indicates no subscription to Begin/Commit messages.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The following conditions must be met to configure this parameter:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><code>Protocol</code> selects <code>Volc</code>, <code>Canal</code>, <code>CanalJSON</code> or <code>Avro</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><code>EndpointType</code> selects <code>Builtin_Kafka</code>, and <code>EndpointType</code> selects <code>Volc_Kafka</code> or <code>Express_Kafka</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The <code>EndpointType</code> is set to<code> Volc_Kafka</code><strong></strong> or <code>Express_Kafka</code>, and the <code>PartitionPolicy</code> must be set to<code> P0</code>.</div><br> |
|SubscribePartBeforeImage |Boolean |No |true<br><br> |Set whether to subscribe to all fields as needed. The values are as follows:<br><br><br>* `true`: (Default) Indicates the before\-image of all fields is subscribed.<br><br>* `false`: Indicates that only the before\-image of changed fields is subscribed.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter can be configured only when the <strong>Instance type</strong> is <strong>MySQL</strong>, the middleware access method is <strong>Message Queue for Kafka</strong> or <strong>Kafka connected over express network</strong>, and the <strong>Subscription format</strong> is <strong>Canal JSON</strong>.</div><br> |


<span id="mysql2rocketmqsettings"></span>
### MySQL2RocketMQSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47109#subscriptionsettings) |Yes |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": true,```<br>```    "SubscribePartBeforeImage": true```<br>```}```<br><br><br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |Streaming data ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|MySQLPosition |Object of [MySQLPosition](https://docs.byteplus.com/en/docs/57/47109#mysqlposition) |No |```JSON```<br>```{```<br>```    "Gtid": "3e11fa47-71ca-11e1-9e33-c80aa9429562:58",```<br>```    "Gset": "f76eb90f-82a2-11e5-a162-7ca23e9126c5:3",```<br>```    "Timestamp": 1679642652```<br>```}```<br> |Set to pull Binlog logs from a specified position or timestamp. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter configuration is not supported during full initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When this parameter is not set, it defaults to the earliest point in time that the system can recognize.</div><br> |


<span id="pg2pgsettings"></span>
### PG2PGSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "huahua",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectType": "Table",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "huahua"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br><br><br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). |


<span id="pg2kafkasettings"></span>
### PG2KafkaSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47109#subscriptionsettings) |Yes |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": true,```<br>```    "SubscribePartBeforeImage": true```<br>```}```<br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |


<span id="pg2rocketmqsettings"></span>
### PG2RocketMQSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SubscriptionSettings |Object of [SubscriptionSettings](https://docs.byteplus.com/en/docs/57/47109#subscriptionsettings) |Yes |```JSON```<br>```{```<br>```    "Protocol": "Volc",```<br>```    "PartitionPolicy": "P0",```<br>```    "VPCId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "VPCSubnetId": "subnet-7rtsu6whhle6j****",```<br>```    "EnableBeginCommitMessage": true,```<br>```    "SubscribePartBeforeImage": true```<br>```}```<br> |Configuration information of the subscription task object. |
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br><br><br> |Mapping information between source and target objects. |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br><br><br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br><br><br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br><br><br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |


<span id="mongo2mongosettings"></span>
### Mongo2MongoSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|MetaTransmissionSettings |Object of [MetaTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#metatransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableMeta": true,```<br>```    "DisablePostMeta": true```<br>```}```<br> |Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates schema migration.<br><br>* Data subscription: Indicates database and table schema subscription.<br><br>* Data synchronization: Indicates schema initialization. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br><br><br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ETLSettings |Object of [ETLSettings](https://docs.byteplus.com/en/docs/57/47109#etlsettings) |No |```JSON```<br>```{```<br>```    "Script": "(defn        desensitization        []\n                (dts/match-table        \"user\"        (dts/map-column        'id_card        str/md5)))"```<br>```}```<br> |ETL parameter configuration. |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |


<span id="redis2redissettings"></span>
### Redis2RedisSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ObjectMappings |Array of [ObjectMapping](https://docs.byteplus.com/en/docs/57/47109#objectmapping) |Yes |```JSON```<br>```[```<br>```    {```<br>```        "DestObjName": "test",```<br>```        "MappingList": [```<br>```            {```<br>```                "DestObjName": "*",```<br>```                "ObjectMappingSetting": {```<br>```                    "LastWriteWinsKey": "",```<br>```                    "ObjectTransTypes": [```<br>```                        "Meta"```<br>```                    ],```<br>```                    "PolicyForKeyConflict": "TableNone",```<br>```                    "SetObjectTransType": false```<br>```                },```<br>```                "ObjectType": "Event",```<br>```                "SrcObjName": "*"```<br>```            }```<br>```        ],```<br>```        "ObjectMappingSetting": {```<br>```            "LastWriteWinsKey": "",```<br>```            "ObjectTransTypes": [```<br>```                "Meta",```<br>```                "Full",```<br>```                "Incr"```<br>```            ],```<br>```            "PolicyForKeyConflict": "TableOverride",```<br>```            "SetObjectTransType": true```<br>```        },```<br>```        "ObjectType": "Database",```<br>```        "SrcObjName": "test"```<br>```    }```<br>```]```<br> |Mapping information between source and target objects. |
|FullTransmissionSettings |Object of [FullTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#fulltransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableFull": true,```<br>```    "Snapshot": true,```<br>```    "RPSLimit": 100000,```<br>```    "BPSLimit": 25000,```<br>```    "FullSyncParalell": 8,```<br>```    "ExtraConditions": {```<br>```        "Db": "TestName",```<br>```        "Table": "TableName",```<br>```        "WhereSql": "id = 5"```<br>```    }```<br>```}```<br> |Fully read the source table content and write it to the target database. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates full migration.<br><br>* Data subscription: Indicates full subscription.<br><br>* Data synchronization: Indicates full initialization. |
|IncrTransmissionSettings |Object of [IncrTransmissionSettings](https://docs.byteplus.com/en/docs/57/47109#incrtransmissionsettings) |No |```JSON```<br>```{```<br>```    "EnableIncr": true,```<br>```    "Statements": [```<br>```        "StmtDDLAll",```<br>```        "StmtDMLDelete",```<br>```        "StmtDMLUpdate",```<br>```        "StmtDMLInsert"```<br>```    ]```<br>```}```<br> |Parses and replays the target database incremental log. The meaning of this parameter varies depending on the task, as detailed below:<br><br><br>* Data migration: Indicates incremental migration.<br><br>* Data subscription: Indicates incremental subscription.<br><br>* Data synchronization: Indicates incremental synchronization.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TaskType</code> is <code>DataSynchronization</code>, this parameter is required.</div><br> |
|ErrorBehaviorSettings |Object of [ErrorBehaviorSettings](https://docs.byteplus.com/en/docs/57/47109#errorbehaviorsettings) |No |```JSON```<br>```{```<br>```    "MaxRetrySeconds": 7200```<br>```}```<br> |Error retry time. If the source database or target database disconnects, the task automatically recovers if reconnection occurs within that time. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyValidationTask&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host:dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "SolutionSettings": {
        "SolutionType": "MySQL2MySQLRowCompare",
        "MySQL2MySQLRowCompareSettings": {
            "SampleRate": 96,
            "ObjectMappings": [
                {
                    "ObjectType": "Database",
                    "SrcObjName": "dts_vedb_644309674613",
                    "DestObjName": "dts_vedb_644309674613",
                    "MappingList": [
                        {
                            "ObjectType": "Table",
                            "SrcObjName": "*",
                            "DestObjName": "*"
                        }
                    ]
                }
            ]
        }
    },
    "TaskId": "446a68e0a68841d28e3497be1d******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20241212200030CB6043C2633C8BE05A15-b56f1e",
        "Action": "ModifyValidationTask",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
