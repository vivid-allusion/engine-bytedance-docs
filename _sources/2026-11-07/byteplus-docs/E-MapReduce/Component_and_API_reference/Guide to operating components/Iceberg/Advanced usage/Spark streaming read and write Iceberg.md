---
title: "Spark streaming read and write Iceberg"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Spark_streaming_read_and_write_Iceberg"
---

This article uses Spark 3.x as an example to demonstrate how to use Spark Structured Streaming to perform streaming read and write operations on Iceberg tables.

<span id="_1-前提条件"></span>
### 1 prerequisites


1. Applicable to E\-MapReduce (EMR) versions 1.2.0 and later (including EMR 1.2.0)

2. Not compatible with EMR 2.x versions. For Spark streaming read and write Iceberg in EMR 2.x versions, please refer to [Spark streaming read and write Iceberg (for EMR 2.x versions)](https://docs.byteplus.com/docs/E-MapReduce/109279)

3. An EMR cluster has been created, and the Iceberg component is installed. There are two ways to install the Iceberg component:

   1. When creating an EMR cluster, select Iceberg as an optional component. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

   2. For an already installed EMR cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg service.


<span id="_2-操作步骤"></span>
### 2 procedure


1. Create a new Maven project and add pom dependencies:


```Plain
<dependency>
    <groupId>org.apache.spark</groupId>
    <artifactId>spark-sql_2.12</artifactId>
    <version>3.2.1</version>
    <scope>provided</scope>
</dependency>
```



2. Streaming write


Spark Structured Streaming writes data to Iceberg tables in streaming mode via the DataStreamWriter interface. The code is as follows.

```Plain
val tableIdentifier: String = "iceberg.iceberg_db.streamingtable"
val checkpointPath: String = "/tmp/iceberg_checkpointPath"
data.writeStream
    .format("iceberg")
    .outputMode("append")
    .trigger(Trigger.ProcessingTime(1, TimeUnit.MINUTES))
    .option("path", tableIdentifier)
    .option("checkpointLocation", checkpointPath)
    .start()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>tableIdentifier</strong> in the code is the metadata table name or table path. <strong>checkpointPath</strong> is the checkpoint directory used by the Spark streaming data processing program. Streaming write supports the following two modes:</div>



* <div data-tips="true" data-tips-type="tip">append: Appends each batch of data to the Iceberg table, equivalent to insert into.</div>


* <div data-tips="true" data-tips-type="tip">complete: Completely overwrites the Iceberg table with the latest batch of data, equivalent to insert overwrite.</div>


3. Streaming read


```Plain
val df = spark.readStream
    .format("iceberg")    
    .option("stream-from-timestamp", Long.toString(streamStartTimestamp))
    .load("database.table_name")
```


<span id="_3-完整示例"></span>
### 3 complete example

This example uses the netcat command in Linux to send data, which Spark receives and writes into the Iceberg table.


1. Write Spark code.


Using Scala code as an example, the code sample is as follows.

```Plain
import org.apache.spark.SparkConf
import org.apache.spark.sql.SparkSession
import org.apache.spark.sql.streaming.Trigger

object IcebergSparkStreamingScalaExample {
  def main(args: Array[String]): Unit = {
    // 配置使用数据湖元数据。
    val sparkConf = new SparkConf()
    val spark = SparkSession
      .builder()
      .config(sparkConf)
      .appName("IcebergSparkStreamingScalaExample")
      .getOrCreate()
    import spark.implicits._

    // Create DataFrame representing the stream of input lines from connection to localhost:9999
    val lines = spark.readStream
      .format("socket")
      .option("host", "localhost")
      .option("port", 9999)
      .load()

    // Split the lines into words
    val words = lines.as[String].flatMap(_.split(" "))

    val checkpointPath = "/tmp/iceberg_checkpointPath"
    // 流式写入Iceberg表
    val query = words.toDF().writeStream
      .format("iceberg")
      .outputMode("append")
      .trigger(Trigger.ProcessingTime("2 seconds"))
      .option("checkpointLocation", checkpointPath)
      .option("path", "iceberg.iceberg_db.streamingtable")
      .start()

    query.awaitTermination()
  }
}
```



2. Package the program and deploy it to the EMR cluster.

   1. Check the Maven plugin for compiling Scala code. You can configure the following plugin in pom.xml.

   ```Plain
   <build>
       <plugins>
           <!-- the Maven Scala plugin will compile Scala source files -->
           <plugin>
               <groupId>net.alchim31.maven</groupId>
               <artifactId>scala-maven-plugin</artifactId>
               <version>3.2.2</version>
               <executions>
                   <execution>
                       <goals>
                           <goal>compile</goal>
                           <goal>testCompile</goal>
                       </goals>
                   </execution>
               </executions>
           </plugin>
       </plugins>
   </build>
   ```
   

   2. Run the compile command

   ```Plain
   mvn clean package
   ```
   

   3. Upload the generated JAR file to the EMR cluster

3. Use Spark SQL to create the test database iceberg_db and table streamingtable. For detailed operations, see [Basic usage of Iceberg](https://docs.byteplus.com/docs/E-MapReduce/109275). You can also directly enter the following command:

   ```Plain
   spark-sql --master yarn \
     --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions \
     --conf spark.sql.catalog.iceberg=org.apache.iceberg.spark.SparkCatalog \
     --conf spark.sql.catalog.iceberg.type=hadoop \
     --conf spark.sql.catalog.iceberg.warehouse=/warehouse/tablespace/managed/hive
   ```
   

   Next, execute the following SQL statement in the Spark SQL console:

   ```Plain
   CREATE DATABASE IF NOT EXISTS iceberg_db;
   CREATE TABLE IF NOT EXISTS iceberg.iceberg_db.streamingtable(value STRING) USING iceberg;
   ```
   

4. Prepare some data using the netcat command in Linux

   ```Plain
   netcat -lk -p 9999
   ```
   

   and enter some strings.

5. Run the Spark job using the spark\-submit command

   ```Plain
   spark-submit --class com.bytedance.IcebergSparkStreamingScalaExample iceberg-spark-example-1.0.jar
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The class name and JAR file need to be modified according to your own code project. The iceberg\-spark\-example\-1.0.jar mentioned above is the JAR file generated from your code project.   </div>
   

6. View the data in the Iceberg table using Spark SQL. The results are as follows:

   ```plain
   spark-sql --master yarn \
     --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions \
     --conf spark.sql.catalog.iceberg=org.apache.iceberg.spark.SparkCatalog \
     --conf spark.sql.catalog.iceberg.type=hadoop \
     --conf spark.sql.catalog.iceberg.warehouse=/warehouse/tablespace/managed/hive
   ```
   

   Execute the following SQL statement in the Spark SQL console:

   ```plain
   SELECT * FROM iceberg.iceberg_db.streamingtable;
   ```
   

   The data entered in the previous step can be printed out.
