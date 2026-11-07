---
title: "Basic usage of Iceberg (applicable to EMR 2.x versions)"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Basic_usage_of_Iceberg_EMR_2x"
---

This article describes how to create and perform other operations on Iceberg tables using the Spark DataFrame API in E\-MapReduce (EMR) cluster version 2.x.

<span id="_1-前提条件"></span>
## 1. Prerequisites

The Iceberg component must be installed on the EMR cluster. There are two ways to install the Iceberg component:


* When creating an E\-MapReduce cluster, select Iceberg as an optional component. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

* For an already installed E\-MapReduce cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg service.


<span id="_2-操作步骤"></span>
## 2. Procedure


1. Create a new Maven project and add the pom dependencies:


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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the version information of the Spark component and Iceberg component, refer to the corresponding version information in the EMR service.</div>



3. Create a table:


```scala
import org.apache.iceberg.hive.HiveCatalog;
val catalog = new HiveCatalog()
catalog.setConf(spark.sparkContext.hadoopConfiguration)
val properties = new util.HashMap[String, String]
properties.put("warehouse", "/user/hive/warehouse/iceberg/hive")
properties.put("uri", "thrift://emr-master-1:9083")
catalog.initialize("hive", properties)
catalog.createTable(name, schema, spec);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Fill in the properties configuration according to the EMR cluster information. "warehouse" refers to the data storage address, and "uri" refers to the Hive Metastore address.</div>



4. Append data:

   ```scala
   val dataFrame = spark.createDataFrame(Seq((2, "LiSi", 20))).toDF("id", "name", "age")
   dataFrame.write.format("iceberg").mode("append").save("db.table")
   ```
   

5. Overwrite data:

   ```scala
   val dataFrame = spark.createDataFrame(Seq((3, "WangWu", 20))).toDF("id", "name", "age")
   dataFrame.write.format("iceberg").mode("overwrite").save("db.table")
   ```
   

6. Query data:

   ```scala
   val dataFrame = spark.table("iceberg.iceberg_db.iceberg_001")
   // named metastore table
   spark.read.format("iceberg").load("db.table")// Hadoop path table
   ```
   

   To run SQL `SELECT` statements on Iceberg tables in 2.4, register the DataFrame as a temporary table:

   ```java
   val df = spark.read.format("iceberg").load("db.table")df.createOrReplaceTempView("table")
   spark.sql("""select count(1) from table""").show()
   ```
   


<span id="_3-完整示例"></span>
## 3. Complete example

This example uses the Spark DataFrame API for batch reading and writing of Iceberg tables.


1. Write Spark code.

   Taking the Scala version as an example, the code sample is as follows.


```scala
package com.bytedance

import org.apache.spark.SparkConf
import org.apache.spark.sql.SparkSession
import org.apache.iceberg.{PartitionSpec, Schema}
import org.apache.iceberg.catalog.TableIdentifier
import org.apache.iceberg.hive.HiveCatalog
import org.apache.iceberg.types.Types

object IcebergSpark2ScalaExample {
  def main(args: Array[String]): Unit = {
    // Configure to use data lake metadata.
    val sparkConf = new SparkConf()
    val spark = SparkSession
      .builder()
      .config(sparkConf)
      .appName("IcebergSparkScalaExample")
      .getOrCreate()

    val name = TableIdentifier.of("default","spark2_demo");
    val tableName = name.toString
    val catalog = new HiveCatalog()
    catalog.setConf(spark.sparkContext.hadoopConfiguration)
    
    val properties = new util.HashMap[String, String]
    properties.put("warehouse", "/user/hive/warehouse/iceberg/hive")
    properties.put("uri", "thrift://emr-master-1:9083")
    catalog.initialize("hive", properties)
   
    val schema = new Schema( Types.NestedField.required(1, "id", Types.IntegerType.get()),
      Types.NestedField.optional(2, "name", Types.StringType.get()),
      Types.NestedField.required(3, "age", Types.IntegerType.get()))
    val spec = PartitionSpec.builderFor(schema).bucket("id", 2).build();
    try {
      // Create Iceberg table
      catalog.createTable(name, schema, spec);
    } catch {
      case e: org.apache.iceberg.exceptions.AlreadyExistsException =>
    }

    // Create or replace Iceberg table from DataFrame
    val df1 = spark.createDataFrame(Seq((1, "ZhangSan", 20), (2, "LiSi", 25), (3, "WangWu", 30)))
      .toDF("id", "name", "age")
    df1.write.format("iceberg").mode("overwrite").save(tableName)
    // Read Iceberg table
    spark.read.format("iceberg").load(tableName).show()

    // Write DataFrame to Iceberg table
    val df2 = spark.createDataFrame(Seq((4, "LiLei", 28), (5, "XiaoMing", 22)))
      .toDF("id", "name", "age")
    df2.write.format("iceberg").mode("append").save(tableName)
    // Read Iceberg table
    spark.read.format("iceberg").load(tableName).show()
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
   

   2. Run the compilation command

   ```plain
   mvn clean package
   ```
   

   3. Upload the generated JAR file to the EMR cluster

3. Run the Spark job using the spark\-submit command

   ```scala
   spark-submit --class com.bytedance.IcebergSpark2ScalaExample iceberg-spark2-example-1.0.jar
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The class name and JAR file need to be modified according to your own code project. The iceberg\-spark2\-example\-1.0.jar mentioned above is the JAR file generated from your code project.</div>


The output is as follows

```scala
+---+--------+---+
| id|    name|age|
+---+--------+---+
|  4|   LiLei| 28|
|  1|ZhangSan| 20|
|  5|XiaoMing| 22|
|  2|    LiSi| 25|
|  3|  WangWu| 30|
+---+--------+---+
```
