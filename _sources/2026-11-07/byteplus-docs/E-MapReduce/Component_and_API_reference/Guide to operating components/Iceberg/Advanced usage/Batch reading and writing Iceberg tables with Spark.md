---
title: "Batch reading and writing Iceberg tables with Spark"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Batch_reading_and_writing_Iceberg_tables_with_Spark"
---

[Apache Spark](https://spark.apache.org/) is a distributed, open\-source processing system designed for big data workloads. This article uses Spark 3.x operating on Iceberg tables as an example to introduce how to use the Spark API to read and write Iceberg tables in batch mode.

<span id="_1-前提条件"></span>
## 1. Prerequisites


1. Applicable to E\-MapReduce (EMR) version 1.2.0 and later (including EMR 1.2.0).

2. Not compatible with EMR 2.x versions. For information about using Spark to operate Iceberg tables in EMR 2.x versions, see [Basic usage of Iceberg (applicable to EMR 2.x versions)](https://docs.byteplus.com/docs/E-MapReduce/109274)

3. An EMR cluster has been created and the Iceberg component is installed. There are two ways to install the Iceberg component:

   1. When creating an EMR cluster, select Iceberg as an optional component. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

   2. For an existing EMR cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg service.


<span id="_2-操作步骤"></span>
## 2. Procedure


1. Create a Maven project and add the dependencies to the pom file:

   ```Plain
   <dependency>
       <groupId>org.apache.spark</groupId>
       <artifactId>spark-core_2.12</artifactId>
       <version>3.2.1</version>
       <scope>provided</scope>
   </dependency>
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The version information for the Spark and Iceberg components should refer to the corresponding version information of these components in the EMR service.   </div>
   

2. Configure the Catalog:

   When writing data to Iceberg tables with Spark 3.x, the V1 DataFrame API is no longer recommended. It is recommended to use the DataFrameWriterV2 API. The following code uses the V2 API as an example to write to an Iceberg table named sample.

   First, configure the Catalog by adding the necessary configuration items to SparkConf.

   ```Plain
   sparkConf.set("spark.sql.extensions", "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions")
   sparkConf.set("spark.sql.catalog.<yourCatalogName>", "org.apache.iceberg.spark.SparkCatalog")
   sparkConf.set("spark.sql.catalog.<yourCatalogName>.type", "hadoop")
   sparkConf.set("spark.sql.catalog.<yourCatalogName>.warehouse", "hdfs://emr-master-1:8020/user/hive/warehouse/iceberg/hive")
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <code><yourCatalogName></code> is the name of the Catalog. Please modify the Catalog name as needed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, the warehouse field should be set to the HDFS path. Please modify it as appropriate.   </div>
   

3. Create a table:

   ```Plain
   val dataFrame = spark.createDataFrame(Seq((1, "ZhangSan", 20))).toDF("id", "name", "age")
   dataFrame.writeTo("iceberg.iceberg_db.iceberg_001").create()
   ```
   

4. Append data:

   ```Plain
   val dataFrame = spark.createDataFrame(Seq((2, "LiSi", 20))).toDF("id", "name", "age")
   dataFrame.writeTo("iceberg.iceberg_db.iceberg_001").append()
   ```
   

5. Overwrite data:

   ```Plain
   val dataFrame = spark.createDataFrame(Seq((3, "WangWu", 20))).toDF("id", "name", "age")
   dataFrame.writeTo("iceberg.iceberg_db.iceberg_001").overwritePartitions()
   ```
   

6. Query data:

   ```Plain
   val dataFrame = spark.table("iceberg.iceberg_db.iceberg_001")
   ```
   


<span id="_3-完整示例"></span>
## 3. Complete example

This example demonstrates batch reading and writing of Iceberg tables using the Spark DataFrame API.


1. Write Spark code.

   For example, the Scala code sample is as follows.

   ```Plain
   package com.bytedance
   
   import org.apache.spark.SparkConf
   import org.apache.spark.sql.SparkSession
   
   object IcebergSparkScalaExample {
     def main(args: Array[String]): Unit = {
       // 配置使用数据湖元数据。
       val sparkConf = new SparkConf()
       sparkConf.set("spark.sql.extensions", "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions")
       sparkConf.set("spark.sql.catalog.iceberg", "org.apache.iceberg.spark.SparkCatalog")
       sparkConf.set("spark.sql.catalog.iceberg.type", "hadoop")
       sparkConf.set("spark.sql.catalog.iceberg.warehouse", "/warehouse/tablespace/managed/hive")
   
       val spark = SparkSession
         .builder()
         .config(sparkConf)
         .appName("IcebergSparkScalaExample")
         .getOrCreate()
   
       // 从DataFrame中创建或替换Iceberg表
       val df1 = spark.createDataFrame(
           Seq((1, "ZhangSan", 20),
               (2, "LiSi", 25),
               (3, "WangWu", 30))
         )
         .toDF("id", "name", "age")
       df1.writeTo("iceberg.iceberg_db.sample").createOrReplace()
   
       // 读Iceberg表
       spark.table("iceberg.iceberg_db.sample").show()
   
       // 将DataFrame写入Iceberg表
       val df2 = spark.createDataFrame(Seq((4, "LiLei", 28), (5, "XiaoMing", 22)))
         .toDF("id", "name", "age")
       df2.writeTo("iceberg.iceberg_db.sample").append()
   
       // 读Iceberg表
       spark.table("iceberg.iceberg_db.sample").show()
     }
   }
   ```
   

2. Package the program and deploy it to the EMR cluster.

   1. Check the Maven plugin for compiling Scala code. You can configure the following plugin in the pom.xml file.

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
   

   2. Run the compilation command.

   ```Plain
   mvn clean package
   ```
   

   3. Upload the generated JAR file to the EMR cluster.

3. Run the Spark job using the spark\-submit command.

   ```Plain
   spark-submit --class com.bytedance.IcebergSparkScalaExample  iceberg-spark-example-1.0.jar
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The class name and JAR file need to be modified based on your own code project. The iceberg\-spark\-example\-1.0.jar mentioned above is the JAR file generated from your code project.   </div>
   

The execution result is as follows.

```Plain
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
