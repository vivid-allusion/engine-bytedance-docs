---
title: "Ksana for SparkSQL"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ksana_for_SparkSQL"
---

<span id="_1-权限管理"></span>
## **1 Permission management**

After installation, some user permissions are preset by default, such as the preset permissions for the hive user. To add new users and new permissions, you can add a new permission policy in the Ranger Admin interface. For details, refer to the [Spark integration](https://docs.byteplus.com/docs/E-MapReduce/109417) section in the Ranger help documentation.

<span id="_2-ksana-for-sparksql-高级配置"></span>
## **2 Advanced configuration for Ksana for SparkSQL**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In EMR\-3.4.0 and later versions, take down Ksana component\-related features.</div>


* <div data-tips="true" data-tips-type="tip">In EMR\-3.3.0 and earlier versions, Ksana component\-related features are still retained. You can create clusters of EMR\-3.3.0 or earlier versions to use Ksana features.</div>



<span id="_2-1-使用-hudi"></span>
### **2.1 Using Hudi**

Hudi parameters can be specified when creating a connection. This method takes effect for the current connection:

```Plain
beeline --hiveconf spark.sql.extensions=org.apache.spark.sql.hudi.HoodieSparkSessionExtension --hiveconf spark.serializer=org.apache.spark.serializer.KryoSerializer --hiveconf spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog  -u "jdbc:hive2://emr-master-1:10005/default;auth=LDAP" -n <user> -p <password>
```


**Create a Hudi table**:

```Plain
create table hudi_mor_tbl (
    id int,
    name string,
    price double,
    ts bigint

) using hudi

tblproperties (
    type = 'cow',
    primaryKey = 'id',
    preCombineField = 'ts'

);
```


**Insert data**:

```Plain
insert into hudi_mor_tbl_1(id, name, price, ts)values(1, 'test', 1, 1);
```


**Query results**:

```Plain
select * from hudi_mor_tbl;

[pool-30-thread-5] INFO  com.bytedance.emr.midas.engine.spark.operation.SparkOperation  - Processing EXECUTE_STATEMENT  statement: EXECUTE_STATEMENT , time taken: 0.471 seconds
+----------------------+------------------------+---------------------+-------------------------+----------------------------------------------------+-----+--------+--------+-----+
| _hoodie_commit_time  |  _hoodie_commit_seqno  | _hoodie_record_key  | _hoodie_partition_path  |                 _hoodie_file_name                  | id  |  name  | price  | ts  |
+----------------------+------------------------+---------------------+-------------------------+----------------------------------------------------+-----+--------+--------+-----+
| 20220429103652951    | 20220429103652951_0_1  | id:1                |                         | a4cadbf7-973c-44c1-b54c-1b07222e6040-0_0-2.parquet | 1   | test  | 1.0    | 1   |
+----------------------+------------------------+---------------------+-------------------------+----------------------------------------------------+-----+--------+--------+-----+
1 row selected (2.077 seconds)
```


<span id="_2-2-使用iceberg"></span>
### **2.2 Using Iceberg**

Iceberg parameters can be specified when creating a connection. This method takes effect for the current connection:

```Plain
beeline --hiveconf spark.sql.catalog.iceberg=org.apache.iceberg.spark.SparkCatalog --hiveconf spark.sql.catalog.iceberg.type=hive --hiveconf spark.sql.catalog.iceberg.uri=thrift://emr-master-1:9083,thrift://emr-master-2:9083,thrift://emr-master-3:9083 --hiveconf spark.sql.catalog.iceberg.warehouse=hdfs://emr-master-1:8020/user/hive/warehouse/iceberg/hive --hiveconf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions -u "jdbc:hive2://emr-master-1:10005/default;auth=LDAP" -n <user> -p <password>
```


<span id="_2-3-引擎默认参数"></span>
### **2.3 Engine default parameters**

Ksana for SparkSQL submits the Spark engine on Yarn in advance to receive SQL and return execution results. When you use Submit Job, you can specify parameter information, or modify the component parameter configuration to set default resources. The modification method is as follows:


1. **Cluster details \> Service list \> Spark \> Service parameters**

2. Search for the following parameters to modify their default values:



|Parameter name |Note |
|---|---|
|spark.master |The job submission mode. The default mode is "yarn". |
|spark.driver\-memory |The default driver memory is 1 GB. |
|spark.driver\-cores |The default number of cores for the driver is 1. |
|spark.executor\-cores |The default number of cores for the executor is 1. |
|spark.num\-executors |The default number of executors is 1. |
|spark.executor\-memory |The default executor memory is 1 GB. |
|spark.queue |Job submission queue. The default queue is "default". |


In addition to modifying global default parameters through the configuration file, you can also dynamically override a parameter when creating a connection. The parameter takes effect for the current connection. For example, you can:

```shell
./bin/beeline  --hiveconf spark.queue=队列名称
```


Modify the default queue. All other parameters can also be set in this way. In addition, Ksana for SparkSQL is compatible with all native Spark parameters, which can be set via the following path:

**Cluster details \> Service list \> Spark \> Service parameters \> Custom parameters**

For information about native Spark parameters, see: [https://spark.apache.org/docs/latest/configuration.html#overriding-configuration-directory](https://spark.apache.org/docs/latest/configuration.html#overriding-configuration-directory)

<span id="_2-4-资源隔离级别"></span>
### 2.4 Resource isolation levels

Ksana for SparkSQL supports three different resource isolation levels: Session, User, and Open. The specific definitions are as follows:


* Session：

   At the session level, Ksana for SparkSQL creates a Spark engine for each connection. All SQL jobs under this connection are executed by this Spark engine. When the connection is closed, the Spark engine is stopped.

   This mode can be selected for jobs with high resource isolation requirements or those that require exclusive resource usage.

* User：

   At the User level, Ksana for SparkSQL creates a Spark engine for each user. All SQL jobs submitted by that user are executed by this Spark engine. After the connection is closed, the Spark engine does not stop; if no new user jobs are submitted within the specified threshold period, the engine will automatically stop.

   This mode can be used for scenarios where jobs need to be submitted at the user level.

* Open：

   In Open mode, all users' SQL jobs are submitted to the same Spark engine.

   This mode can be used when strict account permission control is not required or when resource information needs to be shared.


The methods for using different isolation levels are as follows:

When establishing a connection, set midas.engine.isolation to SESSION/USER/OPEN to specify the isolation level mode for this connection. For example:

```shell
./bin/beeline --hiveconf midas.engine.isolation=SESSION
```


The above command starts a Spark engine in SESSION mode to execute jobs. Since Ksana for SparkSQL essentially launches a resident Spark job on Yarn, when the resource isolation level is USER or OPEN, if the Spark job does not receive any SQL jobs within a certain period, the Spark job will be stopped on Yarn. The default idle period is 1 hour. Users can choose to log in via ssh to the machine where Ksana for SparkSQL is installed and edit the following file `/usr/lib/emr/current/midas-dist/config/midas-env.sh` to modify the following values:

```Plain
export KSANA_ENGINE_TIME_OUT=3600000
export KSANA_SESSION_TIME_OUT=3600000
```


The default unit for this parameter is milliseconds. After modification, Ksana for SparkSQL needs to be restarted.

<span id="_2-5-引擎预热"></span>
### 2.5 Engine warm\-up

Engine warm\-up means that Yarn will keep multiple active Spark engines running for a long time, waiting to receive SparkSQL jobs. This reduces the waiting time caused by cold starts when jobs are executed for the first time. The engine warm\-up feature is disabled by default. To use it, engine warm\-up must be enabled first. The enabling method is as follows:


1. **Cluster details \> Service list \> Spark \> Service parameters**

2. Set the value of midas.prepare.engine to true and configure the engine parameters. The relevant parameters are as follows:



|Parameter name |Note |
|---|---|
|midas.prepare.engine |Engine preheating feature. The default is false (not enabled). |
|midas.prepare.engine.maximum |The maximum number of engines. The default is 3. |
|midas.prepare.engine.minimum |The minimum number of engines. The default is 1. |
|midas.prepare.engine.username |By default, the user who submits the Spark engine is the built\-in hive user. |
|midas.prepare.engine.level |Resource isolation level, default is USER level. |
|midas.prepare.engine.queue |Engine queue, default is "default". |
|midas.prepare.engine.driverMemory |Driver memory resource, default is 1G. |
|midas.prepare.engine.driverCores |Number of driver cores, default is 1. |
|midas.prepare.engine.executorCores |Number of executor cores, default is 1. |
|midas.prepare.engine.numExecutor |Number of executors, default is 1. |
|midas.prepare.engine.executorMemory |Executor memory resource, default is 1G. |


Ksana for SparkSQL calculates the appropriate number of jobs to run in advance on Yarn based on the current cluster resources and the values of midas.prepare.engine.maximum and midas.prepare.engine.minimum.

<span id="_2-6-开启-spark-动态资源"></span>
### 2.6 Enable Spark dynamic resources

Ksana for SparkSQL disables Spark dynamic resource management by default. To enable this feature, configure as follows:


1. **Cluster details \> Service list \> Spark \> Service parameters**

2. Modify the following parameters:



|Parameter name |Note |
|---|---|
|spark.dynamicAllocation.enabled |Dynamic resource switch. Set to true, default is false. |
|spark.shuffle.service.enabled |Dynamic resource switch. Set to true, default is false. |
|spark.dynamicAllocation.minExecutors |Minimum resource quantity, default is 1. |


This enables Spark dynamic resource management.

<span id="_2-7-作业日志查看"></span>
### 2.7 Job log viewing

Ksana for SparkSQL runs SparkSQL jobs using the Spark engine. Therefore, you can view the corresponding job status on the Yarn page, and also access the relevant logs on the machine. The viewing method is as follows:


1. In **Cluster management \> Cluster list \> Specific cluster name,**  go to the **Cluster details** page.

2. In the navigation bar, click **Service list**, then click the **Spark** service to enter.

3. Click the ECS ID of the emr cluster node (host name emr\-master\-1) to jump to the cloud server instance page. Click the **Remote connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.


Go to the /usr/lib/emr/current/midas\-dist/workers directory. Ksana for SparkSQL categorizes logs by submitting user by default. You can view the execution logs of specific SQL statements in this directory.

<span id="_2-8-日志周期配置"></span>
### 2.8 Log retention configuration

Ksana for SparkSQL retains logs for 7 days by default. To retain logs for a longer period, go to:


1. **Cluster details \> Service list \> Spark \> Service parameters**

2. Modify the following parameter information:

   
   |Parameter name |Note |
   |---|---|
   |midas.log.timeout.period |Log retention period, default is 7 days, 1000 \* 60 \* 60 \* 24 \* 7. |
   |midas.log.archive.size |Log file archive size, default is 1GB. |
   


You can set the expiration time according to business requirements.

<span id="_2-9-使用代码连接-ksana-for-sparksql"></span>
### 2.9 Connect to Ksana for SparkSQL using code

Ksana for SparkSQL is compatible with the Hive Driver. Therefore, you can use the Hive driver, modify the connection port, and execute SQL jobs. For example, to connect to Ksana for SparkSQL using Java code:


1. Import the relevant driver:

   ```xml
   <dependency>
       <groupId>org.apache.hive</groupId>
       <artifactId>hive-jdbc</artifactId>
       <version>您的Hive版本</version>
   </dependency>
   <dependency>
       <groupId>org.apache.hadoop</groupId>
       <artifactId>hadoop-common</artifactId>
       <version>您的hadoop版本</version>
   </dependency>
   ```
   

2. Use the following code to execute SparkSQL jobs:

   ```java
   public static void main(String[] args) throws SQLException {
       Connection connection = null;
       try {
           Class.forName("org.apache.hive.jdbc.HiveDriver");
           Properties properties = new Properties();
           properties.put("user", "您的用户名");
           properties.put("password", "您的密码");
           connection = DriverManager.getConnection("您的Ksana for SparkSQL连接地址", properties);
           HiveStatement hiveStatement = (HiveStatement) connection.createStatement();
           ResultSet rs = hiveStatement.executeQuery("SLQ作业");
           while (rs.next()) {
               //todo Output results
           }
           for (String log: hiveStatement.getQueryLog()) {
               //todo Logs can be obtained
           }
       } catch (SQLException | ClassNotFoundException e) {
           e.printStackTrace();
       } finally {
           assert connection != null;
           connection.close();
       }
   }
   ```
   


You can adjust relevant parameters in the properties object based on business requirements, such as queue, memory, and more.
