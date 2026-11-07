---
title: "User-defined function (UDF)"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/UDF"
---

You can create user\-defined functions (UDFs) to meet different computational requirements. The usage of UDFs is similar to that of standard built\-in functions. This article introduces the development and usage process of user\-defined functions.

<span id="_1-udf-分类"></span>
## 1 UDF classification


|**UDF classification** |**Description** |
|---|---|
|UDF（User Defined Scalar Function） |A user\-defined scalar function is commonly referred to as a UDF. It has a one\-to\-one relationship between input and output, that is, it reads one row of data and writes one output value. |
|UDTF（User Defined Table\-valued Function） |A user\-defined table\-valued function is used to handle scenarios where a single function call outputs multiple rows of data. It is also the only type of user\-defined function that can return multiple fields. |
|UDAF（User Defined Aggregation Function） |A user\-defined aggregation function has a many\-to\-one relationship between input and output, that is, it aggregates multiple input records into a single output value. It can be used in conjunction with the Group By statement in SQL. |


<span id="_2-前提条件"></span>
## 2 Prerequisites


* A cluster has been created. For details, see [创建集群](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92).


<span id="_3-开发-udf"></span>
## 3 Develop UDF


1. Use local developer tools to create a Maven project


```shell
mvn archetype:generate -DgroupId=com.example -DartifactId=hiveudf -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```



2. Add pom dependencies


```xml
<dependency>
      <groupId>org.apache.hive</groupId>
      <artifactId>hive-exec</artifactId>
      <version>3.1.2</version>
      <exclusions>
         <exclusion>
           <groupId>org.pentaho</groupId>
           <artifactId>*</artifactId>
         </exclusion>
      </exclusions>
</dependency>
```



3. Create a class that inherits from the Hive UDF class.


Note: The class name can be freely defined. In this article, MyUDF is used as an example.

```java
package org.example;

import org.apache.hadoop.hive.ql.exec.UDF;

/** * Hello world! * */
public class MyUDF extends UDF
{
    public String evaluate(final String s) {
        if (s == null) { return null; }
        return s + ":HelloWorld";
    }
}
```



4. Package the custom code into a JAR file


```bash
mvn clean package -DskipTests
```


A JAR file named hiveudf\-1.0\-SNAPSHOT.jar will appear in the target directory, indicating that the UDF development is complete.

<span id="_4-使用-udf"></span>
## 4 Use UDF


1. Log in to the cluster primary node using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Use a file transfer tool to upload the generated JAR file to the current SSH node.

3. Upload the generated JAR file to HDFS


```Plain
hadoop fs -put hiveudf-1.0-SNAPSHOT.jar /user/hive/
```



4. Create a UDF function

   * Run the following command to enter the Hive command line

   ```Plain
   su hive
   hive
   ```
   

   * After entering Hive, run the following command to apply the generated JAR and create the function

   ```Plain
   CREATE FUNCTION myfunc AS "org.example.MyUDF" USING JAR "hdfs:///user/hive/hiveudf-1.0-SNAPSHOT.jar";
   ```
   



|Parameters |Note |
|---|---|
|myfunc |Name of the UDF function |
|org.example.MyUDF |This was created during UDF development. |
|hdfs:///user/hive/hiveudf\-1.0\-SNAPSHOT.jar |Path for uploading the JAR file to HDFS |


When the following information appears, it indicates that the creation was successful

> Added [/tmp/8df0a4d5\-5251\-4a2f\-99c5\-413e88189041_resources/hiveudf\-1.0\-SNAPSHOT.jar] to class path Added resources: [hdfs:///user/hive/hiveudf\-1.0\-SNAPSHOT.jar] OK Time taken: 0.612 seconds


5. Run the following command to use the UDF function


```Plain
SELECT myfunc("Hive");
```


The following information is returned:

> OK

> Hive:HelloWorld

> Time taken: 1.781 seconds, Fetched: 1 row(s)
