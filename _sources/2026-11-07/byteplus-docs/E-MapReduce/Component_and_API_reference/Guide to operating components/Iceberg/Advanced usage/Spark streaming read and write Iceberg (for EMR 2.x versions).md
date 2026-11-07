---
title: "Spark streaming read and write Iceberg (for EMR 2.x versions)"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/spark_streaming_read_adn_write_iceberg_EMR_2x"
---

This article uses Spark 2.x operations on Iceberg tables as an example to introduce how to use Spark Structured Streaming to perform streaming read and write operations on Iceberg tables.

<span id="_1-前提条件"></span>
## 1 Prerequisites


1. Suitable for E\-MapReduce (EMR) 2.x versions

2. An EMR cluster has been created, and the Iceberg component is installed. There are two ways to install the Iceberg component:

   1. When creating an EMR cluster, select Iceberg as an optional component. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

   2. For an existing EMR cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg service.


<span id="_2-操作步骤"></span>
## 2 Procedure


1. Create a new Maven project and add dependencies to the pom.xml file:


```yaml
<dependency>
    <groupId>org.apache.spark</groupId>
    <artifactId>spark-sql_2.11</artifactId>
    <version>2.4.8</version>
    <scope>compile</scope>
</dependency>
<dependency>
    <groupId>org.apache.iceberg</groupId>
    <artifactId>iceberg-spark-runtime-3.2_2.12</artifactId>
    <version>0.14.0</version>
    <scope>compile</scope>
</dependency>
```



2. Streaming write


Spark Structured Streaming writes data to Iceberg tables in streaming mode through the DataStreamWriter interface. The code is as follows.

```Plain
val name = TableIdentifier.of("default","spark2_streaming_demo")
val tableIdentifier = name.toString
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


<div data-tips="true" data-tips-type="tip">The <strong>tableIdentifier</strong> in the code is the metadata table name or table path. <strong>checkpointPath</strong> is the checkpoint address used by the Spark streaming data processing program. Streaming write supports the following two modes:</div>



* <div data-tips="true" data-tips-type="tip">append: Appends each batch of data to the Iceberg table, which is equivalent to insert into.</div>


* <div data-tips="true" data-tips-type="tip">complete: Uses the latest batch of data to completely overwrite the Iceberg table, which is equivalent to insert overwrite.</div>


3. Streaming read


```Plain
val df = spark.readStream
    .format("iceberg")    
    .option("stream-from-timestamp", Long.toString(streamStartTimestamp))
    .load("database.table_name")
```


<span id="_3-完整示例"></span>
## 3 Complete example

This example uses the Linux netcat command to send data. After Spark receives the data, it writes it into the Iceberg table.


1. Write Spark code.


Using Scala code as an example, the code sample is as follows.

```scala
import org.apache.iceberg.Schema
import org.apache.iceberg.catalog.TableIdentifier
import org.apache.iceberg.hive.HiveCatalog
import org.apache.iceberg.types.Types
import org.apache.spark.SparkConf
import org.apache.spark.sql.SparkSession
import org.apache.spark.sql.streaming.Trigger

object IcebergSpark2StreamingScalaExample {
  def main(args: Array[String]): Unit = {
    // Configure to use data lake metadata.
    val sparkConf = new SparkConf()
    val spark = SparkSession
      .builder()
      .config(sparkConf)
      .appName("IcebergSparkStreamingScalaExample")
      .getOrCreate()
    import spark.implicits._

    val name = TableIdentifier.of("default","spark2_streaming_demo")
    val tableName = name.toString
    val warehouseLocation = "/warehouse/tablespace/managed/hive"
    val catalog = new HiveCatalog()
    catalog.setConf(spark.sparkContext.hadoopConfiguration)
    val properties = new util.HashMap[String, String]
    properties.put("warehouse", "/user/hive/warehouse/iceberg/hive")
    properties.put("uri", "thrift://emr-master-1:9083")
    catalog.initialize("hive", properties)
    
    val schema = new Schema(
      Types.NestedField.optional(1, "value", Types.StringType.get()))
    try {
      // Create Iceberg table
      catalog.createTable(name, schema)
    } catch {
      case _: org.apache.iceberg.exceptions.AlreadyExistsException =>
    }

    // Create DataFrame representing the stream of input lines from connection to localhost:9999
    val lines = spark.readStream
      .format("socket")
      .option("host", "localhost")
      .option("port", 9999)
      .load()

    // Split the lines into words
    val words = lines.as[String].flatMap(_.split(" "))

    val checkpointPath = "/tmp/iceberg_checkpointPath"
    // Streaming write to Iceberg table
    val query = words.toDF().writeStream
      .format("iceberg")
      .outputMode("append")
      .trigger(Trigger.ProcessingTime("2 seconds"))
      .option("checkpointLocation", checkpointPath)
      .option("path", tableName)
      .start()

    query.awaitTermination()
  }
}
```



2. Package the program and deploy it to the EMR cluster.

   1. Check the Maven plugin for compiling Scala code. You can configure the following plugin in pom.xml.

   ```plain
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

   ```plain
   mvn clean package
   ```
   

   3. Upload the generated JAR file to the EMR cluster

3. Prepare some data using the Linux netcat command

   ```plain
   netcat -lk -p 9999
   ```
   

   and enter some strings.

4. Run the Spark job using the spark\-submit command

   ```scala
   spark-submit --class com.bytedance.IcebergSpark2StreamingScalaExample iceberg-spark2-example-1.0.jar
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The class name and JAR file need to be modified according to your own code project. The iceberg\-spark2\-example\-1.0.jar mentioned above is the JAR file generated from your code project.   </div>
   

5. View the data in the Iceberg table using spark\-shell. The results are as follows

   ```plain
   spark-shell --master yarn
   ```
   

   Execute the following code in the spark\-shell console:

   ```plain
   import org.apache.iceberg.catalog.TableIdentifier
   val name = TableIdentifier.of("default","spark2_streaming_demo")
   val tableName = name.toString
   spark.read.format("iceberg").load(tableName).show()
   ```
   

   The data entered in Step 4 can be printed out.
