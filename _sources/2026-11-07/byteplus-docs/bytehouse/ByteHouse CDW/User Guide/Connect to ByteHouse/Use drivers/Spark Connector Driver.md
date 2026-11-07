---
title: "Spark Connector Driver"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/spark-connector-driver"
---

The ByteHouse Cloud Data Warehouse Spark Connector is specifically designed for loading data into ByteHouse Cloud Data Warehouse Edition via Spark. This tutorial introduces three methods for connecting to ByteHouse and processing data: Spark SQL, EMR\-supported Serverless Spark, and Spark Jar.

<span id="9898b997"></span>
# Constraints


* Java 8

* Scala 2.12 and later

* Spark 3.5


<span id="ccaabe25"></span>
# Install the driver

Please configure the dependencies for the following drivers in the program according to the method below.


1. ByteHouse Spark Connector.

2. The ClickHouse JDBC driver.

3. ByteHouse JDBC driver.


<span id="4f256dfd"></span>
## Maven dependencies

For Maven projects that need to be compiled using the Spark connector, add the following dependencies to the project's `pom.xml` file.


1. Add the following dependencies.

   
   |Spark version |Dependencies |Download |
   |---|---|---|
   |Spark 3.5 |```XML```<br>```<dependency>```<br>```    <groupId>com.clickhouse</groupId>```<br>```    <artifactId>clickhouse-jdbc</artifactId>```<br>```    <version>0.4.6</version>```<br>```</dependency>```<br>```<dependency>```<br>```    <groupId>com.bytedance.bytehouse</groupId>```<br>```    <artifactId>driver-java</artifactId>```<br>```    <version>1.1.75</version>```<br>```    <classifier>all</classifier>```<br>```</dependency>```<br>```<dependency>```<br>```    <groupId>com.bytedance.bytehouse</groupId>```<br>```    <artifactId>clickhouse-spark-runtime-3.5_2.12</artifactId>```<br>```    <version>0.8.0.15</version>```<br>```</dependency>```<br> |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ff1f49a5bef4811aa4aab72eb20694e~tplv-goo7wpa0wc-image.image" name="clickhouse-jdbc-0.4.6.jar">clickhouse-jdbc-0.4.6.jar</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/050436ca9de24df0aa57ff71600c891d~tplv-goo7wpa0wc-image.image" name="driver-java-1.1.75-all.jar">driver-java-1.1.75-all.jar</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50a092ccb8944a938e24ee6f03b968d7~tplv-goo7wpa0wc-image.image" name="clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar">clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar</Attachment><br> |
   

2. Add the following repositories to the `pom.xml` file:

   ```XML
   <repository>
       <id>bytedance</id>
       <name>ByteDance Public Repository</name>
       <url>https://artifact.bytedance.com/repository/releases</url>
   </repository>
   ```
   


<span id="db46bb73"></span>
# Usage instructions

<span id="d37d877d"></span>
## Obtain connection parameters

The general parameters and configuration instructions required to connect to ByteHouse are as follows. For more information about configuring connection parameters, see the [Configuration parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#15f90d38) section below.


|Parameters |Configuration instructions |
|---|---|
|`CLICKHOUSE_HOST`, spark.sql.catalog.clickhouse.host |Configure as the public network connection domain name for ByteHouse You can view the relevant information in the ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). |
|`CLICKHOUSE_PASSWORD`, spark.sql.catalog.clickhouse.password |That is, the value of the `API key`. You can obtain the value of the `API key` in the ByteHouse console under **Tenant management** \> **Connection information**. For details, see [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311). |
|`CLICKHOUSE_DATABASE`, spark.sql.catalog.clickhouse.database |Configure as the name of the ByteHouse database you want to connect to. You can view and copy the name of the database you need to connect to through **ByteHouse Console** \> **Database**. |
|`CLICKHOUSE_VW`, spark.sql.catalog.clickhouse.option.vw |Set the virtual warehouse name to ByteHouse. You can view the default compute group via **ByteHouse Console** \> **Tenant management** \> **Parameter settings**. |


<span id="6700a52a"></span>
## Local testing

Before running local tests, please load the following JAR files into `${SPARK_HOME/jars}`, or specify the local path to the JAR files using `--jars` when submitting the command.


1. ByteHouse Spark Connector.

2. ClickHouse JDBC driver.

3. ByteHouse JDBC driver.


<span id="3611e05a"></span>
### Spark SQL

Replace CLICKHOUSE_HOST, CLICKHOUSE_PASSWORD, CLICKHOUSE_DATABASE, and CLICKHOUSE_VW with actual values. For information on how to obtain these values, see [Obtain connection parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#d37d877d).

```Bash
export SPARK_LOCAL_IP=localhost
export SPARK_HOME=/opt/tiger/spark
export CLICKHOUSE_HOST=bytehouse-<REGION>.bytepluses.com
export CLICKHOUSE_PASSWORD=<your-api-key>
export CLICKHOUSE_DATABASE=<database>
export CLICKHOUSE_VW=<your-virtual-warehouse>

$SPARK_HOME/bin/spark-sql \
  --conf spark.sql.catalog.clickhouse=com.bytehouse.ByteHouseCatalog \
  --conf spark.sql.catalog.clickhouse.host=${CLICKHOUSE_HOST:-127.0.0.1} \
  --conf spark.sql.catalog.clickhouse.password=${CLICKHOUSE_PASSWORD:-} \
  --conf spark.sql.catalog.clickhouse.database=${CLICKHOUSE_DATABASE} \
  --conf spark.sql.catalog.clickhouse.option.vw=${CLICKHOUSE_VW} \
  --conf spark.driver.bindAddress=127.0.0.1 \
  --conf spark.bytehouse.write.batchSize=50000 \
  --conf spark.bytehouse.write.format=jdbc \
  --jars clickhouse-jdbc-0.4.6-all.jar,driver-java-1.1.75-all.jar,clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar
```



|Parameters |Configuration instructions |
|---|---|
|`--jars` |Set to the actual path of the JAR file in use. |


<span id="a2618e67"></span>
### Spark Jar

When using, replace spark.sql.catalog.clickhouse.host, spark.sql.catalog.clickhouse.password, spark.sql.catalog.clickhouse.database, and spark.sql.catalog.clickhouse.option.vw with actual values. For information on how to obtain these values, see [Obtain connection parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#d37d877d).

```Bash
import org.apache.spark.sql.SparkSession

object Main {

  def main(args: Array[String]): Unit = {
    val spark = SparkSession
      .builder()
      .appName("App")
      .master("local")
      .config("spark.sql.catalog.clickhouse", "com.bytehouse.ByteHouseCatalog")
      .config("spark.sql.catalog.clickhouse.host", "<your-host>")
      .config("spark.sql.catalog.clickhouse.protocol", "http")
      .config("spark.sql.catalog.clickhouse.password", "<your-api-key>")
      .config("spark.sql.catalog.clickhouse.database", "<database>")
      .config("spark.sql.catalog.clickhouse.option.vw", "<your-virtual-warehouse>")
      .config("spark.sql.catalog.clickhouse.option.query_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.connect_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.receive_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.send_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.max_execution_time", "80000")
      .config("spark.bytehouse.write.batchSize", "50000")
      .config("spark.bytehouse.write.format", "jdbc")
      .getOrCreate()

    val sql = "select * from clickhouse.xx.xx"
    val df = spark.sql(sql)
    spark.stop()
  }
}
```


<span id="8513ef0f"></span>
### PySpark

When using, replace spark.sql.catalog.clickhouse.host, spark.sql.catalog.clickhouse.password, spark.sql.catalog.clickhouse.database, and spark.sql.catalog.clickhouse.option.vw with actual values. For information on how to obtain these values, see [Obtain connection parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#d37d877d).

```Bash
from pyspark.sql import SparkSession
spark = SparkSession\
    .builder\
    .appName("App")\
    .master("local")\
    .config("spark.sql.catalog.clickhouse", "com.bytehouse.ByteHouseCatalog")\
    .config("spark.sql.catalog.clickhouse.host", "<your-host>")\
    .config("spark.sql.catalog.clickhouse.protocol", "http")\
    .config("spark.sql.catalog.clickhouse.password", "<your-api-key>")\
    .config("spark.sql.catalog.clickhouse.database", "<database>")\
    .config("spark.sql.catalog.clickhouse.option.vw", "<your-virtual-warehouse>")\
    .config("spark.sql.catalog.clickhouse.option.query_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.connect_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.receive_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.send_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.max_execution_time", "80000")\
    .config("spark.bytehouse.write.batchSize", "50000")\
    .config("spark.bytehouse.write.format", "jdbc")\
    .config("spark.jars", "clickhouse-jdbc-0.4.6-all.jar,driver-java-1.1.75-all.jar,clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar").\
    getOrCreate()
sql = "select count(*) from clickhouse.xxx.xxx"
df = spark.sql(sql)
df.show()
spark.stop()
```


<span id="b904b6f3"></span>
## Serverless Spark

The Serverless Spark method is applicable to the BytePlus EMR (E\-MapReduce) service. You can refer to the following commands to connect to ByteHouse using the Serverless Spark method. For Serverless Spark job development, please refer to relevant documentation, such as the [Serverless Spark Job Development Guide](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Job_Development).

You can connect ByteHouse and BytePlus EMR (E\-MapReduce) services using Serverless Spark, which supports connections via Spark SQL, Spark Jar, and PySpark.

<span id="9ca3c31b"></span>
### Spark SQL

You can refer to the following command to connect to ByteHouse using Spark SQL CLI. For details, see [Spark SQL Job Development Guide](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Spark_SQL_Job_Development_Guide).

<span id="4ae97725"></span>
#### Use the default calculation group to connect

The following command uses the Spark SQL default compute group to connect to ByteHouse. Both task\-level and queue\-level calculation groups are supported.

When using the command, replace the placeholders with the actual parameter values. For information on how to obtain these values, see the parameter descriptions below.


* Task\-level

   
   <Tabs>
   <Tab zoneid="n5e5pEsjbl" title="Private network connection">
   <TabTitle>Private network connection</TabTitle>
   
   ```Bash
   set serverless.cross.vpc.access.enabled = true;
   set serverless.cross.vpc.vpc.id = <your-vpc-id>;
   set serverless.cross.vpc.subnet.id = <your-subnet-id>;
   set serverless.cross.vpc.security.group.id = <your-securitygroup-id>;
   set emr.serverless.spark.only.parse.enabled  = true;
   set spark.sql.catalog.clickhouse=com.bytehouse.ByteHouseCatalog;
   set spark.sql.catalog.clickhouse.host=tenant-<your-account-id>-<region>.bytehouse.ivolces.com;
   set spark.sql.catalog.clickhouse.protocol=http;
   set spark.sql.catalog.clickhouse.password=<your-api-key>;
   set spark.sql.catalog.clickhouse.database=<database>;
   set spark.sql.catalog.clickhouse.option.vw=<your-virtual-warehouse>;
   
   set las.spark.jar.depend.jars = [{"schema":"","fileName":"tos://test-bh-tos/cdw/driver-java-1.1.75-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-jdbc-0.4.6-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar"}];
   use clickhouse;
   
   -- Query hive
   -- select * from spark_catalog.hive_db.hive_table;
   -- select * from people_t_copy;
   insert into people_t_copy select * from people_t; 
   ```
   
   
   
   </Tab>
   <Tab zoneid="ikduv1fOBM" title="Public network connection">
   <TabTitle>Public network connection</TabTitle>
   
   ```Bash
   set serverless.cross.vpc.access.enabled = true;
   set serverless.cross.vpc.vpc.id = <your-vpc-id>;
   set serverless.cross.vpc.subnet.id = <your-subnet-id>;
   set serverless.cross.vpc.security.group.id = <your-securitygroup-id>;
   set emr.serverless.spark.only.parse.enabled  = true;
   set spark.sql.catalog.clickhouse=com.bytehouse.ByteHouseCatalog;
   set spark.sql.catalog.clickhouse.host=bytehouse-<region>.volces.com;
   set spark.sql.catalog.clickhouse.protocol=http;
   set spark.sql.catalog.clickhouse.password=<your-api-key>;
   set spark.sql.catalog.clickhouse.database=<database>;
   set spark.sql.catalog.clickhouse.option.vw=<your-virtual-warehouse>;
   
   set las.spark.jar.depend.jars = [{"schema":"","fileName":"tos://test-bh-tos/cdw/driver-java-1.1.75-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-jdbc-0.4.6-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar"}];
   use clickhouse;
   
   -- Query hive
   -- select * from spark_catalog.hive_db.hive_table;
   -- select * from people_t_copy;
   insert into people_t_copy select * from people_t; 
   ```
   
   
   
   </Tab>
   </Tabs>
   

   **Parameter description**

   
   |Parameters |Configuration instructions |
   |---|---|
   |serverless.cross.vpc. |Configure it as VPC network information, go to the ByteHouse console and navigate to **Tenant management** \> **Basic information**. In the **Network information** section, click **Details** next to the private network domain name to view the VPC in use and related parameter information.<br><br><br>* serverless.cross.vpc.vpc.id: Set it to the VPC ID.<br><br>* serverless.cross.vpc.subnet.id: Set it to the subnet ID.<br><br>* serverless.cross.vpc.security.group.id: Set it to a security group ID.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When configuring a subnet, you must configure it in Availability Zone B.</div><br> |
   |spark.sql.catalog.clickhouse |* host: Configure the private or public network HOST address for ByteHouse. You can refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) to obtain the address.<br><br>* password: Configure the ByteHouse API key. You can refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) to obtain it.<br><br>* database: Set it as the database name for ByteHouse. You can use the **ByteHouse Console** \> **Database** to view and copy the name of the database you need to connect to.<br><br>* vw: Configured as the virtual warehouse name of ByteHouse. You can view the default compute group via **ByteHouse Console** \> **Tenant management** \> **Parameter settings**. |
   |las.spark.jar.depend.jars |Configure the TOS path for the jar that is actually used. |
   |Other |For more instructions on configuring connection parameters, please refer to the [Configuration parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#15f90d38) section below. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The expected format for the set parameter is "SET", "SET key", or "SET key=value". If the key needs to contain special characters, or the value contains a semicolon (;), you can enclose the key or value in backticks (<code>" "</code>).   </div>
   

* Queue\-level

   Before specifying a compute group, you need to log in to the **EMR Serverless Console**, click the **queue name**, navigate to the **Network Connection** module on the queue details page, and click **Network Settings** to configure network connectivity for the queue. Ensure that EMR and ByteHouse are in the **same VPC**. If the **global cross\-VPC routing** is enabled, it can be turned off.

   
   <Tabs>
   <Tab zoneid="wmZthhqvOe" title="Private network connection">
   <TabTitle>Private network connection</TabTitle>
   
   ```Bash
   set serverless.cross.vpc.access.enabled = true;
   set emr.serverless.spark.only.parse.enabled  = true;
   set spark.sql.catalog.clickhouse=com.bytehouse.ByteHouseCatalog;
   set spark.sql.catalog.clickhouse.host=tenant-<your-account-id>-<region>.bytehouse.ivolces.com;
   set spark.sql.catalog.clickhouse.protocol=http;
   set spark.sql.catalog.clickhouse.password=<your-api-key>;
   set spark.sql.catalog.clickhouse.database=<database>;
   set spark.sql.catalog.clickhouse.option.vw=<your-virtual-warehouse>;
   
   set las.spark.jar.depend.jars = [{"schema":"","fileName":"tos://test-bh-tos/cdw/driver-java-1.1.75-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-jdbc-0.4.6-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar"}];
   use clickhouse;
   
   -- Query hive
   -- select * from spark_catalog.hive_db.hive_table;
   -- select * from people_t_copy;
   insert into people_t_copy select * from people_t; 
   ```
   
   
   
   </Tab>
   <Tab zoneid="IrMuXPbuEk" title="Public network connection">
   <TabTitle>Public network connection</TabTitle>
   
   ```Bash
   set serverless.cross.vpc.access.enabled = true;
   set emr.serverless.spark.only.parse.enabled  = true;
   set spark.sql.catalog.clickhouse=com.bytehouse.ByteHouseCatalog;
   set spark.sql.catalog.clickhouse.host=bytehouse-<region>.volces.com;
   set spark.sql.catalog.clickhouse.protocol=http;
   set spark.sql.catalog.clickhouse.password=<your-api-key>;
   set spark.sql.catalog.clickhouse.database=<database>;
   set spark.sql.catalog.clickhouse.option.vw=<your-virtual-warehouse>;
   
   set las.spark.jar.depend.jars = [{"schema":"","fileName":"tos://test-bh-tos/cdw/driver-java-1.1.75-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-jdbc-0.4.6-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/cdw/clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar"}];
   use clickhouse;
   
   -- Query hive
   -- select * from spark_catalog.hive_db.hive_table;
   -- select * from people_t_copy;
   insert into people_t_copy select * from people_t; 
   ```
   
   
   
   </Tab>
   </Tabs>
   

   **Parameter description**

   
   |Parameters |Configuration instructions |
   |---|---|
   |spark.sql.catalog.clickhouse |* host: Configure the private or public network HOST address for ByteHouse. You can refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) to obtain the address.<br><br>* password: Configure the ByteHouse API key. You can refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) to obtain it.<br><br>* database: Set it as the database name for ByteHouse. You can use the **ByteHouse Console** \> **Database** to view and copy the name of the database you need to connect to.<br><br>* vw: Configured as the virtual warehouse name of ByteHouse. You can view the default compute group via **ByteHouse Console** \> **Tenant management** \> **Parameter settings**. |
   |las.spark.jar.depend.jars |Configure the TOS path for the jar that is actually used. |
   |Other |For more instructions on configuring connection parameters, please refer to the [Configuration parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#15f90d38) section below. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The expected format for the set parameter is "SET", "SET key", or "SET key=value". If the key needs to contain special characters, or the value contains a semicolon (;), you can enclose the key or value in backticks (<code>" "</code>).   </div>
   

<span id="0ea660f9"></span>
#### Use Spark SQL calculation group to connect

If you have created a Spark SQL calculation group and want to use it to connect to ByteHouse, you can do so as follows. For an introduction to Spark SQL calculation groups, see [Queue Management](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Queue_management).


1. Log in to the BytePlus EMR console. Click the **Queue name**, navigate to the **Network connection** module on the queue details page, and click **Network settings** to configure network connectivity for the queue. Ensure that EMR and ByteHouse are in the **same VPC**. If the **global cross\-VPC routing** is enabled, it can be turned off.

2. Under the **Resource Management** tab, click **Serverless**; click the queue you are using; click **Calculation Group**; click **Spark SQL Calculation Group**; click **Parameter Configuration**; then configure the following spark.jars custom parameters.

   ```Bash
   {
     "spark.jars": "tos://bytehouse-spark/cdw/driver-java-1.1.75-all.jar,tos://bytehouse-spark/cdw/clickhouse-jdbc-0.4.6-all.jar,tos://bytehouse-spark/cdw/clickhouse-spark-runtime-3.5_2.12-0.8.0.15.jar"
   }
   ```
   

3. After configuration is complete, you can use the following commands to connect to ByteHouse. When using the command, replace the placeholders with the actual parameter values. For information on how to obtain these values, refer to the parameter description below.

   
   <Tabs>
   <Tab zoneid="MiDixJiDsd" title="Private network connection">
   <TabTitle>Private network connection</TabTitle>
   
   ```Bash
   set emr.serverless.spark.only.parse.enabled  = true;
   set spark.sql.catalog.clickhouse=com.bytehouse.ByteHouseCatalog;
   set spark.sql.catalog.clickhouse.host=tenant-<your-account-id>-<region>.bytehouse.ivolces.com;
   set spark.sql.catalog.clickhouse.protocol=http;
   set spark.sql.catalog.clickhouse.password=<your-api-key>;
   set spark.sql.catalog.clickhouse.database=<database>;
   set spark.sql.catalog.clickhouse.option.vw=<your-virtual-warehouse>;
   
   use clickhouse;
   
   -- Query hive
   -- select * from spark_catalog.hive_db.hive_table;
   -- select * from people_t_copy;
   insert into people_t_copy select * from people_t; 
   ```
   
   
   
   </Tab>
   <Tab zoneid="gih5eXtT7N" title="Public network connection">
   <TabTitle>Public network connection</TabTitle>
   
   ```Bash
   set spark.sql.catalog.clickhouse=com.bytehouse.ByteHouseCatalog;
   set spark.sql.catalog.clickhouse.host=bytehouse-<region>.volces.com;
   set spark.sql.catalog.clickhouse.protocol=http;
   set spark.sql.catalog.clickhouse.password=<your-api-key>;
   set spark.sql.catalog.clickhouse.database=<database>;
   set spark.sql.catalog.clickhouse.option.vw=<your-virtual-warehouse>;
   
   use clickhouse;
   
   -- Query hive
   -- select * from spark_catalog.hive_db.hive_table;
   -- select * from people_t_copy;
   insert into people_t_copy select * from people_t; 
   ```
   
   
   
   </Tab>
   </Tabs>
   

   **Parameter description**

   
   |Parameters |Configuration instructions |
   |---|---|
   |spark.sql.catalog.clickhouse |* host: Configure the private or public HOST address for ByteHouse. You can refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) to obtain it.<br><br>* password: Configure the ByteHouse API key. You can refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) to obtain it.<br><br>* Configure the ByteHouse database name. You can view and copy the name of the database to connect to through **ByteHouse Console** \> **Database**.<br><br>* vw: Configured as the compute group name for ByteHouse. You can view the default compute group via **ByteHouse Console** \> **Tenant management** \> **Parameter settings**. |
   |Other |For more information about configuring connection parameters, see the [Configuration parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#15f90d38) section below. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The expected format for the set parameter is "SET", "SET key", or "SET key=value". If a key needs to contain special characters, or a value contains a semicolon (;), you can enclose it in backticks (````).   </div>
   

<span id="4bd4fea0"></span>
### Spark Jar

You can refer to the following commands to connect to ByteHouse using the Spark Jar method. Spark Jar job development guide: For details, see [Spark Jar job development guide](https://www.volcengine.com/docs/6491/1262325).

When submitting, you need to specify VPC\-related parameters in the submission parameters. The VPC must be consistent with the VPC where ByteHouse resides.

When using, replace spark.sql.catalog.clickhouse.host, spark.sql.catalog.clickhouse.password, spark.sql.catalog.clickhouse.database, and spark.sql.catalog.clickhouse.option.vw with actual values. For information on how to obtain these values, see [Obtain connection parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#d37d877d).

```Bash
import org.apache.spark.sql.SparkSession

object Main {

  def main(args: Array[String]): Unit = {
    val spark = SparkSession
      .builder()
      .appName("App")
      .master("local")
      .config("spark.sql.catalog.clickhouse", "com.bytehouse.ByteHouseCatalog")
      .config("spark.sql.catalog.clickhouse.host", "<your-host>")
      .config("spark.sql.catalog.clickhouse.protocol", "http")
      .config("spark.sql.catalog.clickhouse.password", "<your-api-key>")
      .config("spark.sql.catalog.clickhouse.database", "<database>")
      .config("spark.sql.catalog.clickhouse.option.vw", "<your-virtual-warehouse>")
      .config("spark.sql.catalog.clickhouse.option.query_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.connect_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.receive_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.send_timeout", "600000")
      .config("spark.sql.catalog.clickhouse.option.max_execution_time", "80000")
      .config("spark.bytehouse.write.batchSize", "50000")
      .config("spark.bytehouse.write.format", "jdbc")
      .getOrCreate()

    val sql = "select * from clickhouse.xx.xx"
    val df = spark.sql(sql)
    spark.stop()
  }
}
```


<span id="73709ddf"></span>
### PySpark

You can refer to the following command to connect to ByteHouse using PySpark. For details on the PySpark Job Development Guide, see [PySpark Job Development Guide](https://www.volcengine.com/docs/6491/1262326).

When submitting, you need to specify VPC\-related parameters in the submission parameters. The VPC must be consistent with the VPC where ByteHouse resides.

When using, replace spark.sql.catalog.clickhouse.host, spark.sql.catalog.clickhouse.password, spark.sql.catalog.clickhouse.database, and spark.sql.catalog.clickhouse.option.vw with actual values. For information on how to obtain these values, see [Obtain connection parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector-driver#d37d877d).

```Python
from pyspark.sql import SparkSession
spark = SparkSession\
    .builder\
    .appName("App")\
    .master("local")\
    .config("spark.sql.catalog.clickhouse", "com.bytehouse.ByteHouseCatalog")\
    .config("spark.sql.catalog.clickhouse.host", "<your-host>")\
    .config("spark.sql.catalog.clickhouse.protocol", "http")\
    .config("spark.sql.catalog.clickhouse.password", "<your-api-key>")\
    .config("spark.sql.catalog.clickhouse.database", "<database>")\
    .config("spark.sql.catalog.clickhouse.option.vw", "<your-virtual-warehouse>")\
    .config("spark.sql.catalog.clickhouse.option.query_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.connect_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.receive_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.send_timeout", "600000")\
    .config("spark.sql.catalog.clickhouse.option.max_execution_time", "80000")\
    .config("spark.bytehouse.write.batchSize", "50000")\
    .config("spark.bytehouse.write.format", "jdbc")\
    getOrCreate()
sql = "select count(*) from clickhouse.xxx.xxx"
df = spark.sql(sql)
df.show()
spark.stop()
```


<span id="15f90d38"></span>
## Configuration parameters


|Parameters |Required or optional |Default value |Data types |Description |Initial version |
|---|---|---|---|---|---|
|spark.sql.catalog.${catalog}.host |✅ |No default value |string |The format is `bytehouse-{REGION}.bytepluess.com`. For more information about available zones, please refer to [Supported regions and zones](https://docs.byteplus.com/en/docs/bytehouse/docs-supported-regions-and-providers). |0.8.0.2 |
|spark.sql.catalog.${catalog}.http_port |No |19000 |int |Keep the default value. |0.8.0.2 |
|spark.sql.catalog.${catalog}.protocol |No |http |string |Keep the default value. |0.8.0.2 |
|spark.sql.catalog.${catalog}.user |No |bytehouse |string |Simply keep the default value. |0.8.0.2 |
|spark.sql.catalog.${catalog}.password |✅ |No default value |string |Configure it as the API Key for ByteHouse. You can refer to the [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) section to obtain API Key information. |0.8.0.2 |
|spark.sql.catalog.${catalog}.database |No |default |string |Configure it as the default database name. After configuration, when you use Spark SQL to query tables in this database, you can directly use the table name to query, without needing to use the `*database name*.*table name*` format. |0.8.0.2 |
|spark.sql.catalog.${catalog}.gateway_version |No |auto |string |v1, v2, or auto. If the gateway is set to auto, v1 or v2 is selected automatically. |0.8.0.10 |
|spark.sql.catalog.${catalog}.timezone |No |server |string |The time zone in use can be configured as server, client, UTC+3, Asia/Shanghai, and more. |0.8.0.2 |
|spark.sql.catalog.${catalog}.dedup_key_mode |No |No default value |string |Strategies for handling duplicate key values in data are supported:<br><br><br>* throw<br><br>* append<br><br>* replace<br><br>* ignore |0.8.0.3 |
|spark.sql.catalog.${catalog}.option |✅ |No default value |map |The virtual warehouse parameter is required and should be configured as follows:<br><br>`spark.sql.catalog.${catalog}.option.vw=xx` |0.8.0.10 |
|spark.bytehouse.write.batchSize |No |10000 |int |None. |0.8.0.2 |
|spark.bytehouse.write.maxRetry |No |30 |int |Maximum number of retries on write failure. |0.8.0.3 |
|spark.bytehouse.write.retryInterval |No |10s |time |Write failure retry interval. |0.8.0.3 |
|spark.bytehouse.write.retryExponentialBackoffEnabled |No |true |boolean |During write operations, exponential backoff can be enabled for retry intervals. |0.8.0.9 |
|spark.bytehouse.write.sharding\-strategy |No |No default value |string |ClickHouse distributed sharding strategy. Supported values:<br><br><br>* `NONE`: Do not write to partitions.<br><br>* `HASH`: Hash write for shard_key. |0.8.0.9 |
|spark.bytehouse.write.sharding\-key |No |No default value |string |A hash partition key can consist of multiple fields, separated by commas. |0.8.0.9 |
|spark.bytehouse.write.sharding\-expression |No |No default value |string |The hash partitioning expression. If a hash partitioning expression is set, all involved field names must also be listed in the `sharding-key`. |0.8.0.9 |
|spark.bytehouse.read.byPartition |No |No default value |boolean |If set to true, the query will be split by partition. |0.8.0.9 |
|spark.bytehouse.read.byPartition.strategy |No |manual |string |Query partition policies. Supported values:<br><br><br>* In manual mode, you must specify the lower, upper, and partition count parameters simultaneously.<br><br>* In auto mode, partitions are automatically divided based on filter criteria and table partition keys. To enable automatic partitioning, the following conditions must be met:<br><br>   * Table partitions have one and only one column<br><br>   * The filter condition must be applied to the partition column of the table, and the condition supports predicate pushdown.<br><br>   * Supported filter conditions: `>, >=,=,<,<=, in, between and`<br><br>   * When 'in' and other conditions appear together, partitioning is performed based only on 'in'. |0.8.0.15 |
|spark.bytehouse.read.byPartition.count |No |100 |int |Number of partitions. |0.8.0.15 |
|spark.bytehouse.read.partition.lower |No |No default value |string |The lower bound range (including the lower bound value) used when scanning by partition. |0.8.0.9 |
|spark.bytehouse.read.partition.upper |No |No default value |string |Upper limit range for partition\-based scanning (including the upper limit value). |0.8.0.9 |
|spark.bytehouse.read.partition.stringAsDate |No |false |boolean |It supports setting the partition key type to String, and enables automatic partitioning for values formatted as yyyy\-MM\-dd. |0.8.0.15 |
|spark.bytehouse.read.partition.stringAsInt |No |true |boolean |It supports setting the partition key type to String, and enables automatic partitioning for values formatted as yyyyMMdd. |0.8.0.15 |
|spark.bytehouse.read.partition.detectMinMax |No |true |boolean |When the partitioning strategy is set to automatic, if the query condition contains only the upper or lower bound of the partition, you can query the maximum and minimum values of the partition column. |0.8.0.15 |
|spark.bytehouse.read.byBucket |No |No default value |boolean |If set to true, the query will be split by bucket. |0.8.0.9 |
|spark.bytehouse.read.maxRetry |No |30 |int |Maximum number of retry attempts on read failure. |0.8.0.9 |
|spark.bytehouse.read.retryInterval |No |10s |time |Read failure retry interval. |0.8.0.9 |
|spark.bytehouse.read.retryExponentialBackoffEnabled |No |true |boolean |It enables exponential backoff for retry intervals during read operations. When this setting is configured to true, if a read operation encounters an error or failure, the system will retry the operation at intervals that increase exponentially. |0.8.0.9 |


<span id="315000dd"></span>
# Usage examples

<span id="0aa7e92f"></span>
## Configure driver parameters

<span id="483cf834"></span>
### Set timeout parameters

You can set the timeout period: using the following parameters.

```Bash
set spark.sql.catalog.clickhouse.option.socket_timeout=60000;
set spark.sql.catalog.clickhouse.option.query_timeout=60000;
set spark.sql.catalog.clickhouse.option.connect_timeout=60000;
set spark.sql.catalog.clickhouse.option.receive_timeout=60000;
set spark.sql.catalog.clickhouse.option.send_timeout=60000;
set spark.sql.catalog.clickhouse.option.max_execution_time=80000;
```


<span id="18d235a7"></span>
### Other driver custom parameters

If you need to add custom parameters, you can do so by following the `spark.sql.catalog.clickhouse.option.xxx` pattern.

```Bash
set spark.sql.catalog.clickhouse.option.xxx=xxx;
```


<span id="070f9e16"></span>
## Parallel read

Spark supports parallel reading of bucket tables and partitioned tables, and also allows both bucket parallel reading and partition parallel reading to be enabled simultaneously, with the overall parallelism equal to the product of the two.

<span id="be952249"></span>
### Bucket tables

If the table being read is a bucket table, parallel reading by bucket can be enabled, with the degree of parallelism equal to the number of buckets. The table creation statement in this example specifies a parallelism of 32.

```SQL
CREATE TABLE IF NOT EXISTS test.createTable(
id UInt32,
name String DEFAULT ''
) 
ENGINE=CnchMergeTree
ORDER BY id
CLUSTER BY EXPRESSION cityHash64(id) % 32 INTO 32 BUCKETS
```


```SQL
# Enable parallel reading by bucket
set spark.bytehouse.read.byBucket=true;
```


<span id="66a835ae"></span>
### Partition table

If the table being read is a partitioned table, parallel reading by partition can be enabled.

An example of a table creation statement is as follows:

```SQL
CREATE TABLE IF NOT EXISTS test.createTable(
id UInt32,
name String DEFAULT '',
date Date
) 
ENGINE=CnchMergeTree
ORDER BY id
PARTITION BY date
```


Suppose you need to query data for date within the time range [2025\-01\-01, 2025\-01\-10]; you can use the following configuration with a parallelism of 10.

```SQL
set spark.bytehouse.read.byPartition=true;
set spark.bytehouse.read.partition.lower=20250101;
set spark.bytehouse.read.partition.upper=20250110;
```


<span id="77904c5b"></span>
## Write to a bucket

Spark supports writing to bucket tables. The following example demonstrates how to create the `test.createTable` table and enable data writing by configuring driver parameters.

```SQL
CREATE TABLE IF NOT EXISTS test.createTable(
id UInt32,
name String DEFAULT ''
) 
ENGINE=CnchMergeTree
ORDER BY id
CLUSTER BY EXPRESSION cityHash64(id) % 32 INTO 32 BUCKETS
```


```SQL
set spark.bytehouse.write.sharding-strategy=HASH;
set spark.bytehouse.write.sharding-key=id;
set spark.bytehouse.write.sharding-expression=`cityHash64(id) % 32`;
```


<span id="12795666"></span>
# Frequently\-used SQL

This section introduces commonly used SQL statements for writing data and deleting data.

<span id="b31facba"></span>
## Write data

<span id="9ef4a014"></span>
### Write temporary data


* Use values to write data and specify columns.

   ```SQL
   INSERT INTO clickhouse.db.table(id, age) values(1, 10)
   ```
   

* Use the SELECT clause.

   ```SQL
   INSERT INTO clickhouse.db.table SELECT 1 AS id, 10 AS age
   ```
   


<span id="6f48d07d"></span>
### Write data from another table


* Hive tables

   You can specify `spark_catalog` or leave it unspecified as needed.

   * Leave `spark_catalog` unspecified:

      ```SQL
      INSERT INTO clickhouse.db.table SELECT id, age FROM hive_db.hive_table
      ```
      

   * Specify `spark_catalog`:

      ```SQL
      INSERT INTO clickhouse.db.table SELECT id, age FROM spark_catalog.hive_db.hive_table
      ```
      

* ByteHouse tables

   ```SQL
   INSERT INTO clickhouse.db.table SELECT id, age FROM clickhouse.db1.table1
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">ByteHouse does not currently support the <code>insert overwrite [ partition_spec ]</code> syntax. Please do not use this method to write data.</div>


<span id="3e5e41a4"></span>
## Delete data

Use WHERE clause to delete data.

```SQL
DELETE FROM clickhouse.db.table WHERE id = 1
```


<span id="9e12585c"></span>
# Reference: Supported scenarios


|Scenario |Support status |Spark SQL syntax |ByteHouse Cloud Data Warehouse Edition SQL syntax |
|---|---|---|---|
|listTables |✅ |show tables |```SQL```<br>```SHOW TABLES FROM `xx````<br> |
|loadTable |✅ |show create table xx |```SQL```<br>```SHOW TABLES FROM `xx` LIKE `xxx````<br> |
|createTable |❌ |None |```SQL```<br>```CREATE TABLE [IF NOT EXISTS] [tableIdentifier] [UUID uuid]```<br>```(```<br>```    [tableColumnDfnt],```<br>```    [CONSTRAINT constraint_name CHECK columnExpr,]```<br>```    ...```<br>```) [engineClause]```<br> |
|dropTable |✅ |drop table `xx`.`xxx` |```SQL```<br>```DROP TABLE `xx`.`xxx````<br> |
|renameTable |✅ |rename table xx to xxx |```SQL```<br>```RENAME TABLE `xx`.`xxx` to `xx`.`xxx````<br> |
|listNamespaces |✅ |show databases |```SQL```<br>```SHOW DATABASES```<br> |
|createNamespace |✅ |create database xx |```SQL```<br>```CREATE DATABASE `xx` [with properties ('engine'='cnch')]```<br> |
|dropNamespace |✅ |drop database xx |```SQL```<br>```DROP DATABASE `xx````<br> |


<span id="3d2bbaca"></span>
# Reference: Supported data types


|Data types ||Read |Write |
|---|---|---|---|
|**Integer types** |UInt8 |✅ |✅ |
||UInt16 |✅ |✅ |
||UInt32 |✅ |✅ |
||UInt64 |✅ |✅ |
||Int8 |✅ |✅ |
||Int16 |✅ |✅ |
||Int32 |✅ |✅ |
||Int64 |✅ |✅ |
|**Floating\-point numbers** |Float32 |✅ |✅ |
||Float64 |✅ |✅ |
||Decimal |✅ |✅ |
||Decimal32 |✅ |✅ |
||Decimal64 |✅ |✅ |
|**Boolean** |bool |✅ |✅ |
|**Strings** |String |✅ |✅ |
||FixedString |✅ |✅ |
|**Dates** |Date |✅ |✅ |
||DateTime |✅ |✅ |
||DateTime64 |✅ |✅ |
|**UUID** |UUID |✅ |✅ |
|**Enum** |Enum8 |✅ |✅ |
||Enum16 |✅ |✅ |
|**Arrays** |Array(T) |✅ |✅ |
|**Maps** |Map(K, V) |✅ |✅ |
