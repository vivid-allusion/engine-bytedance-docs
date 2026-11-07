---
title: "DescribeSupportedValidationTypes"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/describesupportedvalidationtypes"
---

Call the DescribeSupportedValidationTypes API to view the supported data verification types that can be created.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SrcDataSource |Object of [DataSource](https://docs.byteplus.com/en/docs/57/47097#datasource) |Yes |&nbsp;<br><br>```Plain Text```<br>```{```<br>```    "Category": "MongoDB",```<br>```    "CreateTime": 1734070854504,```<br>```    "DataSourceId": "186745444294******",```<br>```    "EndpointType": "Volc_Mongo",```<br>```    "ModifyTime": 1734070872597,```<br>```    "VolcMongoSettings": {```<br>```        "DBInstanceId": "mongo-replica-386df9f4fd7c",```<br>```        "DBInstanceName": "",```<br>```        "DeployType": "ReplicaSet",```<br>```        "MongoAuthSourceDB": "admin",```<br>```        "Password": "******",```<br>```        "RegionSettings": {```<br>```            "Region": "cn-beijing"```<br>```         },```<br>```         "Username": "root"```<br>```    }```<br>```}```<br><br><br> |The source information of the data verification task. |
|DestDataSource |Object of [DataSource](https://docs.byteplus.com/en/docs/57/47097#datasource) |Yes |&nbsp;<br><br>```Plain Text```<br>```{```<br>```    "Category": "MongoDB",```<br>```    "CreateTime": 1734070854504,```<br>```    "DataSourceId": "186745444294******",```<br>```    "EndpointType": "Volc_Mongo",```<br>```    "ModifyTime": 1734070872597,```<br>```    "VolcMongoSettings": {```<br>```        "DBInstanceId": "mongo-replica-386df9f4fd7c",```<br>```        "DBInstanceName": "",```<br>```        "DeployType": "ReplicaSet",```<br>```        "MongoAuthSourceDB": "admin",```<br>```        "Password": "******",```<br>```        "RegionSettings": {```<br>```            "Region": "cn-beijing"```<br>```         },```<br>```         "Username": "root"```<br>```    }```<br>```}```<br><br><br> |The destination information of the data verification task. |


<span id="datasource"></span>
### DataSource


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Category |String |No |MySQL |The type of instance. The values are as follows:<br><br><br>* `MySQL`: Indicates that the instance type is MySQL.<br><br>* `PostgreSQL`: Indicates that the instance type is PostgreSQL.<br><br>* `ElasticSearch`: Indicates that the instance type is Elasticsearch.<br><br>* `MongoDB`: Indicates that the instance type is MongoDB.<br><br>* `Redis`: Indicates that the instance type is Redis. |
|CreateTime |Long |No |1734070854504 |Creation time of the data source. Millisecond timestamp. |
|DataSourceId |String |No |1867454442941460510 |Source or target instance ID. |
|ModifyTime |Long |No |1734070873088 |The most recent time the data source was updated. Millisecond timestamp. |
|EndpointType |String |Yes |Volc_MySQL |The access method of the instance. the values are as follows:<br><br><br>* `Volc_MySQL`: Indicates BytePlus NDB for MySQL.<br><br>* `Volc_veDB_MySQL`: Indicates BytePlus NDB for MySQL.<br><br>* `Volc_PostgreSQL`: Indicates Volcengine RDS for PostgreSQL.<br><br>* `Volc_Mongo`: Indicates Volcengine Database for MongoDB.<br><br>* `Volc_ElasticSearch`: Indicates Volcengine Cloud Search Service.<br><br>* `Volc_Kafka`: Indicates Message Queue for Kafka.<br><br>* `Volc_RocketMQ`: Indicates Message Queue for RocketMQ.<br><br>* `Volc_Redis`: Indicates Volcengine Cache for Redis.<br><br>* `Public_MySQL`: Indicates MySQL connected over public network.<br><br>* `Public_PostgreSQL`: Indicates PostgreSQL connected over public network.<br><br>* `Public_Mongo`: Indicates MongoDB connected over public network.<br><br>* `Public_ElasticSearch`: Indicates Cloud Search connected over public network.<br><br>* `Public_Redis`: Indicates Redis connected over public network.<br><br>* `Builtin_Kafka`: Indicates the built\-in middleware.<br><br>* `Express_MySQL`: Indicates MySQL connected over express network.<br><br>* `Express_PostgreSQL`: Indicates PostgreSQL connected over express network.<br><br>* `Express_Mongo`: Indicates MongoDB connected over express network.<br><br>* `Express_Redis`: Indicates Redis connected over express network.<br><br>* `Express_Kafka`: Indicates Kafka connected over express network.<br><br>* `Express_ElasticSearch`: Indicates ElasticSearch connected over express network. |
|VolcMySQLSettings |Object of [VolcMySQLSettings](https://docs.byteplus.com/en/docs/57/47097#volcmysqlsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "mysql-0b5d385f*****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-shanghai"```<br>```    },```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine RDS for MySQL. This parameter is required when `EndpointType` is set to `Volc_MySQL`. |
|VolcveDBMySQLSettings |Object of [VolcveDBMySQLSettings](https://docs.byteplus.com/en/docs/57/47097#volcvedbmysqlsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "vedbm-arjlc5di****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "root"```<br>```}```<br> |Indicates the information of the source or target database where the access method is BytePlus veDB for MySQL. This parameter is required when `EndpointType` is set to `Volc_veDB_MySQL`. |
|VolcPostgreSQLSettings |Object of [VolcPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47097#volcpostgresqlsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "postgres-5d17bd5c****",```<br>```    "DBInstanceName": "",```<br>```    "DBName": "huahua",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine RDS for PostgreSQL. This parameter is required when `EndpointType` is set to `Volc_PostgreSQL`. |
|VolcMongoSettings |Object of [VolcMongoSettings](https://docs.byteplus.com/en/docs/57/47097#volcmongosettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "mongo-replica-8ea79132****",```<br>```    "DBInstanceName": "",```<br>```    "DeployType": "ReplicaSet",```<br>```    "MongoAuthSourceDB": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Username": "root"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Volcengine Database for MongoDB. This parameter is required when `EndpointType` is set to `Volc_Mongo`. |
|VolcElasticSearchSettings |Object of [VolcElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47097#volcelasticsearchsettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "o-00g0sqi*****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-shanghai"```<br>```    },```<br>```    "Username": "admin"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine Cloud Search Service. This parameter is required when `EndpointType` is set to `Volc_ElasticSearch`. |
|VolcKafkaSettings |Object of [VolcKafkaSettings](https://docs.byteplus.com/en/docs/57/47097#volckafkasettings) |No |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "InstanceId": "kafka-cnnge0tckudy****",```<br>```    "InstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Topic": "huahua",```<br>```    "Username": "huahua"```<br>```}```<br> |Indicates the information of the target database when the access method is Volcengine Kafka. This parameter is required when `EndpointType` is set to `Volc_Kafka`. |
|VolcRocketMQSettings |Object of [VolcRocketMQSettings](https://docs.byteplus.com/en/docs/57/47097#volcrocketmqsettings) |No |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "InstanceId": "rocketmq-cnou964d1e******",```<br>```    "InstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-guangzhou"```<br>```    },```<br>```    "Topic": "zaizai",```<br>```    "Username": "uSmQgOHNTy5Uh98nqBGPvCzK"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine RocketMQ. This parameter is required when `EndpointType` is set to `Volc_RocketMQ`. |
|VolcRedisSettings |Object of [VolcRedisSettings](https://docs.byteplus.com/en/docs/57/47097#volcredissettings) |No |```JSON```<br>```{```<br>```    "DBInstanceId": "redis-cnlf1xx7vjjw9****",```<br>```    "DBInstanceName": "",```<br>```    "Password": "******",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |Indicates the information of the target database where the access method is Volcengine Cache for Redis. This parameter is required when `EndpointType` is set to `Volc_Redis`. |
|PublicMySQLSettings |Object of [PublicMySQLSettings](https://docs.byteplus.com/en/docs/57/47097#publicmysqlsettings) |No |```JSON```<br>```{```<br>```    "Host": "rm-2zey7i58n36x0****.mysql.rds.aliyuncs.com",```<br>```    "Password": "******",```<br>```    "Port": 3306,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "rootgg"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MySQL connected over public network. This parameter is required when `EndpointType` is set to `Public_MySQL`. |
|PublicPostgreSQLSettings |Object of [PublicPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47097#publicpostgresqlsettings) |No |```JSON```<br>```{```<br>```    "DBName": "postgres",```<br>```    "Host": "aurora-pg-17-replica-instance-1.czenkuaf0oxm.ap-southeast-2.rds.amazonaws.com",```<br>```    "Password": "******",```<br>```    "Port": 5432,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "dts"```<br>```}```<br> |Indicates the information of the source database or target database with the access method as PostgreSQL connected over public network. This parameter is required when `EndpointType` is set to `Public_PostgreSQL`. |
|PublicMongoSettings |Object of [PublicMongoSettings](https://docs.byteplus.com/en/docs/57/47097#publicmongosettings) |No |```JSON```<br>```{```<br>```    "DeployType": "Standalone",```<br>```    "Endpoints": [```<br>```        "123"```<br>```    ],```<br>```    "MongoAuthSourceDB": "123",```<br>```    "Password": "123",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-chongqing-sdv"```<br>```    },```<br>```    "Username": "123"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MongoDB connected over public network. This parameter is required when `EndpointType` is set to `Public_Mongo`. |
|PublicElasticSearchSettings |Object of [PublicElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47097#publicelasticsearchsettings) |No |```JSON```<br>``````<br>```{```<br>```    "Endpoints": [```<br>```        "********"```<br>```    ],```<br>```    "Password": "dddd",```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "ddd"```<br>```}```<br> |Indicates the information of the source or target database where the access method is ElasticSearch connected over public network. This Parameter is required when `EndpointType` is set to `Public_ElasticSearch`. |
|PublicRedisSettings |Object of [PublicRedisSettings](https://docs.byteplus.com/en/docs/57/47097#publicredissettings) |No |```JSON```<br>```{```<br>```    "Host": "redis-sy013ku146******.redis.inner.ivolces.com",```<br>```    "Password": "******",```<br>```    "Port": 6379,```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Redis connected over public network. This parameter is Required when `EndpointType` is set to `Public_Redis`. |
|BuiltinKafkaSettings |Object of [BuiltinKafkaSettings](https://docs.byteplus.com/en/docs/57/47097#builtinkafkasettings) |No |```JSON```<br>```{```<br>```    "Brokers": [```<br>```        "192.168.2.5:9092",```<br>```        "192.168.2.5:9192",```<br>```        "192.168.2.5:9292",```<br>```        "192.168.2.5:9392",```<br>```        "192.168.2.5:9492",```<br>```        "192.168.2.5:9592"```<br>```    ],```<br>```    "Topic": "123e8d8a3cc54477b45db3e3c708****"```<br>```}```<br> |Indicates the parameter information for subscribing to the built\-in middleware in the data subscription task. This parameter is required when `EndpointType` is set to `Builtin_Kafka`. |
|ExpressMongoSettings |Object of [ExpressMongoSettings](https://docs.byteplus.com/en/docs/57/47097#expressmongosettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "DeployType": "ReplicaSet",```<br>```    "Endpoints": [```<br>```        "eee"```<br>```    ],```<br>```    "MongoAuthSourceDB": "eee",```<br>```    "Password": "e",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-3jh1vsccsmjuo3pncmesj****",```<br>```        "VPCId": "vpc-30ukbt5glgyyo7r2qr2e6****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-chongqing-sdv"```<br>```    },```<br>```    "Username": "e"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MongoDB connected over express network. This parameter is required when `EndpointType` is `Express_Mongo`. |
|ExpressMySQLSettings |Object of [ExpressMySQLSettings](https://docs.byteplus.com/en/docs/57/47097#expressmysqlsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Host": "192.168.0.65",```<br>```    "Password": "******",```<br>```    "Port": 3306,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2d74b6pbyewao58ozferi****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9*****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "rootgg"```<br>```}```<br> |Indicates the information of the source or target database where the access method is MySQL connected over express network. Required when `EndpointType` is `Express_MySQL`. |
|ExpressPostgreSQLSettings |Object of [ExpressPostgreSQLSettings](https://docs.byteplus.com/en/docs/57/47097#expresspostgresqlsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "DBName": "src",```<br>```    "Host": "192.168.0.65",```<br>```    "Password": "Bd2021_bd",```<br>```    "Port": 5432,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2bznv8i16voqo2dx0efg0****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "suser"```<br>```}```<br> |Indicates the information of the source or target database where the access method is PostgreSQL connected over express network. This parameter is required when `EndpointType` equals `Express_PostgreSQL`. |
|ExpressRedisSettings |Object of [ExpressRedisSettings](https://docs.byteplus.com/en/docs/57/47097#expressredissettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ArchType": "Standalone",```<br>```    "Host": "192.168.32.28",```<br>```    "Password": "pwd",```<br>```    "Port": 6399,```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-3re9nvjumjthc5zsk2i5z****",```<br>```        "VPCId": "vpc-2bzf04ctm2pz42dx0eebh****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "default"```<br>```}```<br> |This represents the information of the source database or target database with access method of Redis connected over express network. When `EndpointType` is `Express_Redis`, this parameter is required. |
|ExpressElasticSearchSettings |Object of [ExpressElasticSearchSettings](https://docs.byteplus.com/en/docs/57/47097#expresselasticsearchsettings) |No |```JSON```<br>```{```<br>```    "Endpoints": [```<br>```        "http://192.****.0.****:9200"```<br>```    ],```<br>```    "Password": "123456",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2d6asbw971nnk58ozfeei****",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9****"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Username": "elastic"```<br>```}```<br> |Indicates the information of the source or target database where the access method is ElasticSearch connected over express network. This parameter is required when `EndpointType` is set to `Express_ElasticSearch`. |
|ExpressKafkaSettings |Object of [ExpressKafkaSettings](https://docs.byteplus.com/en/docs/57/47097#expresskafkasettings) |No |```JSON```<br>```{```<br>```    "AuthType": "PLAIN",```<br>```    "BrokerEndpoints": [```<br>```        "192.168.0.65:9092"```<br>```    ],```<br>```    "Password": "admin-secret",```<br>```    "PrivateNetworkSettings": {```<br>```        "SubnetId": "subnet-2bz5swar08oao2dx0ee******",```<br>```        "VPCId": "vpc-3rebt5uf5fr405zsk2if9******"```<br>```    },```<br>```    "RegionSettings": {```<br>```        "Region": "cn-beijing"```<br>```    },```<br>```    "Topic": "dial_test",```<br>```    "Username": "admin"```<br>```}```<br> |Indicates the information of the source or target database where the access method is Kafka connected over express network. This parameter is required when `EndpointType` is set to `Express_Kafka`. |
|Name |String |No |test |Task name of the data source. This parameter is required when you call the CreateDataSource API to create a data source. |


<span id="volcmysqlsettings"></span>
### VolcMySQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |mysql\-3d224def\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_MySQL</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> interface to query the instance ID.</div><br> |
|DBInstanceName |String |Yes |testDB |Instance name. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47097#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


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


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_veDB_MySQL</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> interface to query the Instance ID.</div><br> |
|DBInstanceName |String |Yes |TestveDB |Instance name. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47097#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="volcpostgresqlsettings"></span>
### VolcPostgreSQLSettings


|**Parameter** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |postgres\-h441603c68aaa\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_PostgreSQL</code>.</div><br> |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47097#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |
|ExtraParams |Array of [ExtraParam](https://docs.byteplus.com/en/docs/57/47097#extraparam) |No | | |


<span id="extraparam"></span>
### ExtraParam


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |No | | |
|Value |String |No | | |


<span id="volcmongosettings"></span>
### VolcMongoSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |No |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Mongo</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describedbinstances">DescribeDBInstanceDetail</a> API to query the instance ID.</div><br> |
|Username |String |No |test\*\*\*\* |Database account. |
|Password |String |No |test\*\*\*\* |Database account password. |
|MongoAuthSourceDB |String |No |ReplicaSet |Account verification database. When` EndpointType `is set to `Volc_Mongo`, the default value of this parameter is `root`. |
|DeployType |String |No |ShardedCluster |The instance type of MongoDB. The values are as follows:<br><br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47097#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |
|PullMethod |String |No |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> parameter value is <code>ShardedCluster</code>.</div><br> |


<span id="volcelasticsearchsettings"></span>
### VolcElasticSearchSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |ztuc43y38z4w\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_ElasticSearch</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstances">DescribeInstances</a> interface to query the instance ID.</div><br> |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volckafkasettings"></span>
### VolcKafkaSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Kafka</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/kafka/DescribeInstancesSummary-v1">DescribeInstancesSummary</a> interface to query the Instance ID.</div><br> |
|AuthType |String |Yes |plain |Authentication method. The default value is `plain`. |
|Username |String |Yes |test\*\*\*\* |The username for the Kafka instance using the PLAIN mode. |
|Password |String |Yes |test\*\*\*\* |The password for the Kafka instance using the PLAIN mode. |
|Topic |String |Yes |my_topic |Kafka's Topic name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volcrocketmqsettings"></span>
### VolcRocketMQSettings


|**Parameter** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |MQ_INST_ ** *\*\*\*\*\** **  |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_RocketMQ</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/6410/67914">GetInstance</a> interface to query the instance ID.</div><br> |
|AuthType |String |Yes |plain |Authentication method. The default value is `plain`. |
|Username |String |Yes |test\*\*\*\* |The username of the RocketMQ instance. |
|Password |String |Yes |test\*\*\*\* |User password for RocketMQ instance. |
|Topic |String |Yes |my_topic |Topic name of RocketMQ. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="volcredissettings"></span>
### VolcRedisSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|DBInstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when <code>EndpointType</code> is set to <code>Volc_Redis</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/redis/describedbinstances">DescribeDBInstances</a> interface to query the instance ID.</div><br> |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|CrossAccountSettings |Object of [CrossAccountSettings](https://docs.byteplus.com/en/docs/57/47097#crossaccountsettings) |No |```json```<br>```{```<br>```    "SourceAccount":"2100******",```<br>```    "Role":"test"```<br>```}```<br> |The configuration information for cross\-account data transmission. |


<span id="publicmysqlsettings"></span>
### PublicMySQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |Yes |4 |The port number of the self\-managed instance. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|SSLSettings |Object of [SSLSettings](https://docs.byteplus.com/en/docs/57/47097#sslsettings) |No |```JSON```<br>```{```<br>```    "EnableSSL": true,```<br>```    "Cert":"-----BEGIN CERTIFICATE----- ...... -----END CERTIFICATE-----"```<br>```}```<br><br><br> |Instance encryption information. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="sslsettings"></span>
### SSLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|EnableSSL |Boolean |No |false |Whether to enable SSL encryption connection method. The values are as follows:<br><br><br>* `true`: Indicates that SSL encryption is enabled.<br><br>* `false`: Indicates that SSL encryption is not enabled. |
|Cert |String |No |\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\- ...... \-\-\-\-\-END CERTIFICATE\-\-\-\-\- |CA certificate content.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>EnableSSL</code> is set to <code>true</code>.</div><br> |


<span id="publicpostgresqlsettings"></span>
### PublicPostgreSQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |Yes |4 |The port number of the self\-managed instance. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |
|ExtraParams |Array of [ExtraParam](https://docs.byteplus.com/en/docs/57/47097#extraparam) |No | | |


<span id="publicmongosettings"></span>
### PublicMongoSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br><br><br> |The region of the instance. |
|DeployType |String |Yes |Standalone |The type of MongoDB instance. The values are as follows:<br><br><br>* `Standalone`: Indicates a single node.<br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|PullMethod |String |No |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |
|Endpoints |Array of String |Yes |192.168.\*\*\*.\*\*\*:4 |Mongo address in the format of `host:port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |Yes |test\*\*\*\* |mongos database account. |
|Password |String |Yes |test\*\*\*\* |Database password of mongos. |
|MongoAuthSourceDB |String |Yes |admin |Authentication database name for mongos. |
|Shards |Array of [MongoShardSetting](https://docs.byteplus.com/en/docs/57/47097#mongoshardsetting) |No |```JSON```<br>```{```<br>```    "Address": "192.168.0.1:27019,192.168.0.1:27020",```<br>```    "Username": "test****",```<br>```    "Password": "test****",```<br>```    "AuthDb": "admin"```<br>```}```<br> |Shard address information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If used as a return parameter, the relevant information about the parameter is not returned.</div><br> |
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
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


<span id="publicredissettings"></span>
### PublicRedisSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\*.\*\*\* |The host address of the self\-managed instance. |
|Port |Integer |Yes |4 |The port number of the self\-managed instance. |
|Username |String |Yes |test\*\*\*\* |Database account. |
|Password |String |Yes |test\*\*\*\* |Database account password. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |The region of the instance. |


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
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |&nbsp;<br><br>```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|DeployType |String |Yes |ShardedCluster |The instance type of the instance. The values are as follows:<br><br><br>* `Standalone`: Indicates a single node.<br><br>* `ReplicaSet`: Indicates a replica set.<br><br>* `ShardedCluster`: Indicates a sharded cluster. |
|PullMethod |String |No |ChangeStream |Incremental acquisition method at the source end. The values are as follows:<br><br><br>* `ChangeStream`: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* `Oplog`: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to ChangeStream.<br><br>* `None`: After selecting None, incremental migration is not available. Only full migration can be selected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the <code>DeployType</code> is set to <code>ShardedCluster</code>.</div><br> |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47097#privatenetworksettings) |Yes |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|Endpoints |Array of String |Yes |192.168.\*\*\*.\*\*\*:4 |Mongo address in the format of `host:port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported. |
|Username |String |Yes |test\*\*\*\* |mongos database account. |
|Password |String |Yes |test\*\*\*\* |Database password of mongos. |
|MongoAuthSourceDB |String |Yes |admin |Authentication database name for mongos. |
|Shards |Array of [MongoShardSetting](https://docs.byteplus.com/en/docs/57/47097#mongoshardsetting) |No |```JSON```<br>```{```<br>```    "Address": "192.168.0.1:27019,192.168.0.1:27020",```<br>```    "Username": "test****",```<br>```    "Password": "test****",```<br>```    "AuthDb": "admin"```<br>```}```<br> |Shard address information.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If used as a return parameter, the relevant information about the parameter is not returned.</div><br> |
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
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47097#privatenetworksettings) |Yes |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="expresspostgresqlsettings"></span>
### ExpressPostgreSQLSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Host |String |Yes |192.168.\*\*\* *.\*\*\**  |The host address of the PostgreSQL instance connected over express network. |
|Port |Integer |Yes |4 |The port of the Express_Kafka instance connected over express network. |
|Username |String |Yes |test\*\*\* |Database account of PostgreSQL instance connected over express network. |
|Password |String |Yes |Admin@\*\*\* |Database account password of PostgreSQL instance connected over express network. |
|DBName |String |Yes |test\*\*\*\* |Database name. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47097#privatenetworksettings) |Yes |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |Yes |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|ExtraParams |Array of [ExtraParam](https://docs.byteplus.com/en/docs/57/47097#extraparam) |No | | |


<span id="expressredissettings"></span>
### ExpressRedisSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ArchType |String |No |Standalone |Architecture type. The values are as follows:<br><br><br>* `Standalone`: `Standalone edition`.<br><br>* `Cluster`: `Cluster edition`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the cluster of the Redis connected over express network instance has a proxy service, the <code>ArchType</code> must be set to <code>Standalone</code>.</div><br> |
|Host |String |No |192.168.\*\*\*.\*\*\* |The host address of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the parameter <code>ArchType</code> is set to <code>Standalone</code>.</div><br> |
|Port |Integer |No |4 |The port of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when the parameter <code>ArchType</code> is set to <code>Standalone</code>.</div><br> |
|Endpoints |Array of String |No |10.10.10.10:3717 |Enter the` IP: port` of the primary nodes for each shard of the Cache for Redis cluster in the private network connected via the dedicated line, separated by commas. For example: `ip1:port1,ip2:port2,ip3:port3`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ArchType</code> is set to <code>Cluster</code>.</div><br> |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47097#privatenetworksettings) |No |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |
|Username |String |No |test\*\*\* |Database account of the Redis instance connected over express network. |
|Password |String |No |Admin@\*\*\* |Database account password of the Redis instance connected over express network.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the parameter <code>ArchType</code> is set to <code>Cluster</code>, the passwords for multiple shards must be consistent. Otherwise, a successful connection can not be established.</div><br> |


<span id="expresselasticsearchsettings"></span>
### ExpressElasticSearchSettings


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Endpoints |Array of String |No |[192.168.\*\*\* *.\*\*\** ] |The host address of ElasticSearch connected over express network. |
|Username |String |No |test\*\*\* |Database account of the Elasticsearch instance connected over express network. |
|Password |String |No |Admin@\*\*\* |Database account password of ElasticSearch instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47097#privatenetworksettings) |No |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id="expresskafkasettings"></span>
### ExpressKafkaSettings


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|BrokerEndpoints |Array of String |No |[10.1.\*\*\*.\*\*\*:9093] |The IP address and port number of the Kafka connected over express network instance Broker, in the format of `host1:port1`. If there are multiple Brokers, separate them with commas (,). |
|AuthType |String |No |plain |Authentication method. The default value is `plain`. |
|Username |String |No |test\*\*\* |Database account of the Kafka instance connected over express network. |
|Password |String |No |Admin@\*\*\* |Database account password of the Kafka instance connected over express network. |
|Topic |String |No |dts_sydtest |Topic information of the Kafka instance connected over express network. |
|PrivateNetworkSettings |Object of [PrivateNetworkSettings](https://docs.byteplus.com/en/docs/57/47097#privatenetworksettings) |No |```JSON```<br>```{```<br>```    "VpcId": "vpc-bp1opxu1zkhn00gz****",```<br>```    "SubnetId": "subnet-bpkdt37pq72zv****"```<br>```}```<br> |Configuration of the virtual private cloud. |
|RegionSettings |Object of [RegionSettings](https://docs.byteplus.com/en/docs/57/47097#regionsettings) |No |```JSON```<br>```{```<br>```    "Region": "cn-shanghai"```<br>``` }```<br> |Region ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|SupportedDataValidationTypes |Array of String |["FullRowCompare"] |Data verification task type. The values are as follows:<br><br><br>* `FullRowCompare`: Indicates full data verification.<br><br>* `FullRowCountCompare`: Indicates full row\-count verification.<br><br>* `FullPkCompare`: Indicates full primary key validation.<br><br>* `MetaCompare`: Indicates Schema Verification.<br><br>* `IncrDataValidation`: Indicates Increment validation. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeSupportedValidationTypes&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "SrcDataSource": {
        "Category": "MongoDB",
        "CreateTime": 1734070854504,
        "DataSourceId": "1867454442941460509",
        "EndpointType": "Volc_Mongo",
        "ModifyTime": 1734070872597,
        "VolcMongoSettings": {
            "DBInstanceId": "mongo-replica-386df****",
            "DBInstanceName": "",
            "DeployType": "ReplicaSet",
            "MongoAuthSourceDB": "admin",
            "Password": "******",
            "RegionSettings": {
                "Region": "cn-beijing"
            },
            "Username": "root"
        }
    },
    "DestDataSource": {
        "Category": "MongoDB",
        "CreateTime": 1734070854506,
        "DataSourceId": "1867454442941460510",
        "EndpointType": "Volc_Mongo",
        "ModifyTime": 1734070873088,
        "VolcMongoSettings": {
            "DBInstanceId": "mongo-replica-d91799*******",
            "DBInstanceName": "",
            "DeployType": "ReplicaSet",
            "MongoAuthSourceDB": "admin",
            "Password": "******",
            "RegionSettings": {
                "Region": "cn-beijing"
            },
            "Username": "root"
        }
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "DescribeSupportedValidationTypes",
        "Region": "cn-beijing",
        "Service": "dts",
        "Version": "2022-10-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "SupportedDataValidationTypes": [
            "FullRowCompare"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
