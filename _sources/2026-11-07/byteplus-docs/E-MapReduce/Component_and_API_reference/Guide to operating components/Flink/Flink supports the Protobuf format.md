---
title: "Flink supports the Protobuf format"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Flink_supports_the_Protobuf_format"
---

Flink 1.16 already supports the Protobuf format[[1]](https://docs.byteplus.com/docs/E-MapReduce/109230), but by default, the relevant adaptation logic is not included in its release package. Therefore, to use the native Protobuf support feature in Flink, users need to manually download the required dependencies from the Maven repository. Taking Volcano Engine EMR Flink 1.16.1 as an example, users can [download](https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-protobuf/1.16.1/flink-sql-protobuf-1.16.1.jar) the corresponding version of the dependency package[[2]](https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-protobuf/1.16.1/flink-sql-protobuf-1.16.1.jar) and place the JAR dependency package in the lib directory of the Flink release package on the EMR primary node. If users do not want to modify the Flink release package, they can also introduce the dependency at the job level by adding the following dependency to the pom.xml file in their own Flink job project source code:

```Python
<dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-protobuf</artifactId>
    <version>1.16.1</version>
</dependency>
```


This allows users to properly process data in the Protobuf format in Flink SQL. For related demos and configuration, refer to the official documentation[[3]](https://docs.byteplus.com/docs/E-MapReduce/109230#how-to-create-a-table-with-protobuf-format).
