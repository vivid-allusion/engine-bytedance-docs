---
title: "LAS Catalog"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Catalog_Reference_LAS_Catalog"
---

[LAS Catalog](https://www.volcengine.com/docs/6492/1263498) provides key features such as unified metadata management, data access control, metadata discovery, and data integration. The LAS Catalog connector provides read and write capabilities for LAS Catalog tables.

<span id="d117897e"></span>
## 1. Limitations


* Ensure the LAS Catalog unified metadata management service is activated. For more information, refer to the [LAS Catalog Activation Document](https://www.volcengine.com/docs/6492/1264537).

* The LAS Catalog connector is only supported on engine version **Flink 1.16\-volcano** or later.


<span id="1b5f8757"></span>
## 2. Steps

<span id="c7d00b7d"></span>
### 2.1 Create LAS Tables

Create data catalogs, databases, and data tables on the LAS Catalog platform. For details, see the [LAS Catalog documentation](https://www.volcengine.com/docs/6492/1264537) and the [Create Table documentation](https://www.volcengine.com/docs/6492/1264531). Additionally, ensure that LAS Catalog grants the necessary permissions to Flink users.

Notes:

**The default storage location for the LAS Hive data directory is ** **`files://`**  **, a virtual path that must be changed to an actual ** **`tos://`**  ** path to prevent write errors. As shown below:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a11343a1cf6d4dfc9e582a1419ba11cc~tplv-goo7wpa0wc-image.image) </span>

<span id="062bd00f"></span>
### 2.2 Create an LAS Catalog

**Prerequisites**: Flink synchronizes LAS metadata through API access. Required


1. Use API Key Management to create an AccessKey/AccessKeySecret for the sub\-account, which you will later need to enter in the WTIH parameters.

2. Grant the sub\-account LASFullAccess permission in Permission Management.


Create an LAS Catalog in Flink. The LAS Catalog is an extension of the Hive Catalog and requires you to pass its necessary parameters to create the corresponding HMS client. An example statement for creating the Catalog is as follows:

```SQL
CREATE CATALOG lf_catalog
WITH
  (
    'type' = 'hive',
    'is-lf' = 'true',
    'hive-version' = '3.1.3-with-lf3',
    -- Adjust the following based on the region.
    'hive.client.las.region.name' = 'cn-beijing',
    'hive.metastore.uris' = 'thrift://lakeformation.las.cn-beijing.ivolces.com:48869',
    'hive.hms.client.is.public.cloud' = 'true',
    -- Enter the AK/SK for the sub-account, which needs to be created in the console.
    'hive.client.las.ak' = 'xxx',
    'hive.client.las.sk' = 'xxx',
    -- Specify the LAS data directory. The default is hive.
    'catalog.properties.metastore.catalog.default' = 'hive'
  );
```


The following describes the Catalog parameters:


|**Parameter** |**Required** |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|type |Yes |hive |String |The catalog type is Hive. |
|is\-lf |Yes |false |Boolean |Set to true to access LAS Catalog metadata; set to false to access open\-source HMS. |
|hive\-version |Yes |None |String |Set to 3.1.3\-with\-lf3 to access LAS Catalog metadata. |
|hive.client.las.region.name |Yes |None |String |The region where the LAS Catalog is located:<br><br><br>* North China: cn\-beijing<br><br>* East China: cn\-shanghai<br><br>* South China: cn\-guangzhou<br><br>* Johor: ap\-southeast\-1 |
|hive.metastore.uris |Yes |None |String |The metastore addresses for LAS Catalog correspond to their respective regions:<br><br><br>* North China: thrift://lakeformation.las.cn\-beijing.ivolces.com:48869<br><br>* East China: thrift://lakeformation.las.cn\-shanghai.ivolces.com:48869<br><br>* South China: thrift://lakeformation.las.cn\-guangzhou.ivolces.com:48869<br><br>* Johor: thrift://lakeformation.las.ap\-southeast\-1.ivolces.com:48869 |
|hive.hms.client.is.public.cloud |Yes |false |Boolean |Set to true to access LAS Catalog metadata; set to false to access open\-source HMS. |
|hive.client.las.ak |Yes |None |String |Access key for the Volcano Engine account |
|hive.client.las.sk |Yes |None |String |Secret key for the Volcano Engine account |
|catalog.properties.\* |No |None |String |Passes any valid Hive configuration using this prefix. See the [official documentation](https://hive.apache.org/docs/latest/user/configuration-properties/) for existing Hive configurations. |
|catalog.properties.metastore.catalog.default |No |hive |String |**Set the data catalog for accessing LAS metadata**. The default is hive. Use this parameter to manually specify a different data catalog. |


<span id="ff9ec6ca"></span>
### 2.3 Reading from and Writing to LAS Catalog Tables

After creating a Catalog, you can reference data tables in Flink SQL using the three\-part format `Catalog`.`Database`.`Table`. This allows you to perform read and write operations, including batch reads, batch writes, and stream writes, just as you would with Hive tables.

<span id="ae94df16"></span>
#### 2.3.1 Batch Reads

```SQL
-- Create an LAS Catalog
CREATE CATALOG lf_catalog
WITH
  (
    'type' = 'hive',
    'is-lf' = 'true',
    'hive-version' = '3.1.3-with-lf3',
    'hive.client.las.region.name' = 'cn-beijing',
    'hive.metastore.uris' = 'thrift://lakeformation.las.cn-beijing.ivolces.com:48869',
    'hive.hms.client.is.public.cloud' = 'true',
    'hive.client.las.ak' = 'xxx',
    'hive.client.las.sk' = 'xxx'
  );

CREATE TABLE print_sink (
  a STRING,
  b INT,
  c DOUBLE,
  d BOOLEAN,
  `day` STRING,
  `hour` STRING
) WITH (
     'connector' = 'print',
     'print-identifier' = 'out'            
);

-- Batch read an LAS Catalog table
INSERT INTO print_sink
SELECT * FROM lf_catalog.lf_db_test.parquet_partition_table;
```


<span id="df5fd8a6"></span>
#### 2.3.2 Batch Writes

```SQL
-- Create an LAS Catalog
CREATE CATALOG lf_catalog
WITH
  (
    'type' = 'hive',
    'is-lf' = 'true',
    'hive-version' = '3.1.3-with-lf3',
    'hive.client.las.region.name' = 'cn-beijing',
    'hive.metastore.uris' = 'thrift://lakeformation.las.cn-beijing.ivolces.com:48869',
    'hive.hms.client.is.public.cloud' = 'true',
    'hive.client.las.ak' = 'xxx',
    'hive.client.las.sk' = 'xxx'
  );

-- Insert new data into a non-partitioned table
INSERT INTO lf_catalog.lf_db_test.mytable SELECT 'Tom', 25; 
-- Overwrite a non-partitioned table
INSERT OVERWRITE lf_catalog.lf_db_test.mytable SELECT 'Tom', 25; 
-- Insert new data into a partitioned table
INSERT INTO lf_catalog.lf_db_test.myparttable PARTITION (`date`='${date}') SELECT 'Tom', 25; 
-- Overwrite a partitioned table
INSERT OVERWRITE lf_catalog.lf_db_test.myparttable PARTITION (`date`='${date}') SELECT 'Tom', 25;
```


<span id="6e809545"></span>
#### 2.3.3 Stream Writes

```SQL
-- Create an LAS Catalog
CREATE CATALOG lf_catalog
WITH
  (
    'type' = 'hive',
    'is-lf' = 'true',
    'hive-version' = '3.1.3-with-lf3',
    'hive.client.las.region.name' = 'cn-beijing',
    'hive.metastore.uris' = 'thrift://lakeformation.las.cn-beijing.ivolces.com:48869',
    'hive.hms.client.is.public.cloud' = 'true',
    'hive.client.las.ak' = 'xxx',
    'hive.client.las.sk' = 'xxx'
  );

CREATE TABLE datagen_source (
  a STRING,
  b INT,
  c DOUBLE,
  d BOOLEAN
)
WITH
(
  'connector' = 'datagen',
  'rows-per-second' = '100'
);

-- Stream write to an LAS Catalog table
INSERT INTO lf_catalog.lf_db_test.parquet_partition_table 
  /*+ OPTIONS('sink.partition-commit.policy.kind'='metastore,success-file') */
SELECT
  a, b, c, d,
  cast(current_date as string) as `day`,
  cast(hour(current_timestamp) as string) as `hour`
FROM
  datagen_source;
```


&nbsp;

<span id="e9490d6a"></span>
## 3. Using the DataStream Connector

<span id="08854d7b"></span>
### 3.1 Loading LAS Catalog Connector Dependencies

The Connector JAR is as follows:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08e40ae9bed94bc2a28297a146a043d7~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-hive-las-formation-3_2.12-1.16-byted-connector-SNAPSHOT (4).jar">flink-sql-connector-hive-las-formation-3_2.12-1.16-byted-connector-SNAPSHOT (4).jar</Attachment>


After downloading it locally, install the LAS Catalog Connector to your local repository with maven install:

```Shell
mvn install:install-file -Dfile=flink-sql-connector-hive-las-formation-3_2.12-1.16-byted-connector-SNAPSHOT.jar -DgroupId=org.apache.flink -DartifactId=flink-sql-connector-hive-las-formation-3_2.12 -Dversion=1.16-byted-connector-SNAPSHOT -Dpackaging=jar
```


<span id="e18c6d37"></span>
### 3.2 DataStream Example

This example job writes to an LAS Catalog table and has two main parts:


* Register the LAS Catalog by passing the same parameters as the SQL Connector, such as lfRegion and lfThriftUris. For parameter details, refer to the table above.

* Write to the LAS table using the Table API. The LAS table is accessed using the three\-part format: `Catalog`.`Database`.`Table`.


```Java
package com.bigdata;

import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.table.api.EnvironmentSettings;
import org.apache.flink.table.api.SqlDialect;
import org.apache.flink.table.api.bridge.java.StreamTableEnvironment;
import org.apache.flink.table.catalog.hive.HiveCatalog;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class DatagenToLASFormationDemo2 {
    private static final Logger LOG = LoggerFactory.getLogger(DatagenToLASFormationDemo2.class);

    public static void main(String[] args) throws Exception {
        // Set LF-related parameters.
        String lfRegion = "cn-beijing";
        String lfThriftUris = "thrift://lakeformation.las.cn-beijing.ivolces.com:48869";
        Boolean lfMetastoreIsPublicCloud = true;
        String lfAccessKey = "xxx";
        String lfSecretKey = "xxx";
        String hiveDatabase = "lf_db";
        String hiveTable = "lf_table";
        final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
        EnvironmentSettings settings = EnvironmentSettings
                .newInstance()
                .inStreamingMode()
                .build();

        StreamTableEnvironment tableEnv = StreamTableEnvironment.create(env, settings);

        // Create the Elements Source.
        DataStream<String> elementStream = env.fromElements("a", "b", "c");

        // Register the LF Catalog.
        tableEnv.getConfig().setSqlDialect(SqlDialect.DEFAULT);
        String catalogName = "lf_catalog";
        HiveCatalog hiveCatalog = new HiveCatalog(catalogName, hiveDatabase, null, null, "3.1.3-with-lf3",
                true, lfRegion, lfThriftUris, lfMetastoreIsPublicCloud, lfAccessKey, lfSecretKey);
        tableEnv.registerCatalog(catalogName, hiveCatalog);

        // Convert the upstream DataStream to a Table API View for access.
        tableEnv.createTemporaryView("sourceTable", elementStream);

        // Write data to the LF table using the Table API.
        // Note: A dynamic parameter for the partition commit policy is injected via an option hint after the LF table when writing. This parameter is required and is set here to commit to the LF metastore and the TOS success-file.
        String insertSql = "insert into " + catalogName + "." + hiveDatabase + "." + hiveTable + " /*+ OPTIONS('sink.partition-commit.policy.kind'='metastore,success-file') */ select * from sourceTable";
        tableEnv.executeSql(insertSql);
    }
}
```


<span id="ced54b7d"></span>
### 3.3 pom.xml Dependencies

```XML
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.bigdata</groupId>
  <artifactId>flink-datastream-demo</artifactId>
  <version>1.0-SNAPSHOT</version>

  <properties>
    <maven.compiler.source>8</maven.compiler.source>
    <maven.compiler.target>8</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <flink.version>1.16.2</flink.version>
    <scala.binary.version>2.12</scala.binary.version>
  </properties>

<dependencies>
  <dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-streaming-java</artifactId>
    <version>${flink.version}</version>
    <scope>provided</scope>
  </dependency>

  <dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-streaming-scala_${scala.binary.version}</artifactId>
    <version>${flink.version}</version>
    <scope>provided</scope>
  </dependency>

  <dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-table-api-java-bridge</artifactId>
    <version>${flink.version}</version>
    <scope>provided</scope>
  </dependency>

  <dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-sql-connector-hive-las-formation-3_${scala.binary.version}</artifactId>
    <version>1.16-byted-connector-SNAPSHOT</version>
  </dependency>
</dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <executions>
          <execution>
            <id>shade-flink</id>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
            <configuration>
              <artifactSet>
                <includes>
                  <include>*:*</include>
                </includes>
              </artifactSet>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>

</project>
```


<span id="e9c258b2"></span>
## 4. FAQ

<span id="0520d9ee"></span>
### 4.1 Flink Fails to Write Data to LAS

Symptom: The Flink job that writes to LAS reports no errors, but no data is written. This issue may be caused by an incorrect storage path setting for the LAS table.

Troubleshooting steps:


1. Check if the storage path for the LAS table is set correctly. Go to the AI Data Lake service page and view the table information:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01e557e3a26f49ddbdea3b9f469b1658~tplv-goo7wpa0wc-image.image) </span>


2. Check if the data written from Flink to LAS is in the table's storage path. Click the storage location above to go to the TOS page and check for partitions and data files in the directory.
