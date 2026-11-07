---
title: "Flink uses Proton"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Flink_uses_Proton"
---

The open\-source version of Flink does not support streaming writes to the object storage service (TOS) with EXACTLY_ONCE semantics. To meet such requirements, you need to use the Proton SDK for data writing. Starting from Volcano Engine E\-MapReduce (EMR) version 3.2.1, the Proton SDK has been integrated by default into the Volcano EMR Flink runtime environment, allowing you to use Flink to read and write TOS out of the box. For existing clusters, you need to download the Proton SDK and perform additional configuration for proper operation. Refer to [Proton release versions](https://docs.byteplus.com/docs/E-MapReduce/109371) to manually download the Proton SDK.

<span id="_1-火山-emr"></span>
## 1 Volcano EMR

<span id="_1-1-集群配置"></span>
### 1.1 Cluster configuration

Since version 3.2.1, Volcano EMR clusters have integrated Proton dependencies by default, including Hadoop data lake clusters and Flink real\-time computing clusters, with no additional configuration required.

For clusters prior to version 3.2.1, to add or upgrade the Flink Proton dependency package, after downloading the Proton SDK, copy the Proton SDK to each EMR node and extract it:


* Place `plugins/flink/proton-flink{flink.version}-bundle-{proton.version}.jar`, for example `plugins/flink/proton-flink1.16-bundle-2.0.1.jar`, into the Flink lib directory `/usr/lib/emr/current/flink/lib/`. If an older version of the jar exists, remove it.

* Use `proton-hadoop${hadoop.major.version}-bundle-{proton.version}.jar` to replace `proton-hadoop${hadoop.major.version}-bundle-{old.proton.version}.jar` in `/usr/lib/emr/current/hadoop/share/hadoop/hdfs/`. When copying, use the corresponding Hadoop series jar package. For example, in a Hadoop2x environment, select `proton-hadoop2-bundle-{proton.version}.jar`


<span id="_1-2-认证配置"></span>
### 1.2 Authentication configuration

Volcano EMR has configured TOS and IAM authentication information by default, with no additional configuration required. To customize configuration, use `core-site.xml` or `flink-conf.yaml`. The `flink-conf.yaml` configuration can refer to the following configuration information:

```YAML
fs.tos.access-key-id: xxxx
fs.tos.secret-access-key: xxx
# Set the corresponding endpoint address for each region. If running on Volcano ECS, you can use the internal address http://tos-cn-xxx.ivolces.com
fs.tos.endpoint: http://tos-cn-guangzhou.volces.com 

# You can also set authentication information for each bucket
fs.tos.bucket.{bucketname}.access-key-id：xxx
fs.tos.bucket.{bucketname}.secret-access-key：xxx
```


To use the Filesystem connector to read Parquet data stored on TOS, due to the current limitation of Flink `ParquetVectorizedInputFormat` in obtaining configuration information, TOS and IAM authentication information must be added to `core-site.xml` for proper reading. For detailed `core-site.xml` configuration, refer to [Hadoop 使用 Proton - 配置修改](https://docs.byteplus.com/docs/E-MapReduce/109384#_2-1-hadoop3-%E7%B3%BB%E5%88%97) section.

```XML
<configuration>
   <property>
        <name>fs.tos.access-key-id</name>
        <value>{iam.role.access.key}</value>
   </property>
   <property>
        <name>fs.tos.secret-access-key</name>
        <value>{iam.role.access.val}</value>
    </property>
    <property>
        <name>fs.tos.impl</name>
        <value>io.proton.fs.RawFileSystem</value>
    </property>
    <property>
        <name>fs.tos.endpoint</name>
        <value>http://tos-cn-guangzhou.volces.com</value>
    </property>
</configuration>
```


<span id="_2-自建-hadoop-flink-集群"></span>
## 2 Self\-built Hadoop + Flink cluster

<span id="_2-1-集群配置"></span>
### 2.1 Cluster configuration

In a self\-built Hadoop + Flink cluster, to enable Flink streaming writes to TOS storage with EXACTLY_ONCE semantics, after downloading the Proton SDK, copy `proton-flink{flink.version}-bundle-{proton.version}.jar` to the Flink lib directory.

<span id="_2-2-认证配置"></span>
### 2.2 Authentication configuration

Refer to the above [火山EMR - 认证配置](https://docs.byteplus.com/docs/E-MapReduce/109375#_1-2-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE) section for custom configuration.

<span id="_3-独立-flink-集群"></span>
## 3 Standalone Flink cluster

<span id="_3-1-集群配置"></span>
### 3.1 Cluster configuration

Standalone Flink clusters are similar to self\-built Hadoop + Flink clusters. After downloading the Proton SDK, copy `proton-flink${flink.version}-bundle-${proton.version}.jar` to the Flink lib directory, then add IAM and TOS configuration information in `core-site.xml` or `flink-conf.yaml`.

<span id="_3-2-认证配置"></span>
### 3.2 Authentication configuration

Refer to the above [火山EMR - 认证配置](https://docs.byteplus.com/docs/E-MapReduce/109375#_1-2-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE) section for custom configuration.

<span id="7c08951c"></span>
## 4 Custom configuration

<span id="8f4f06b2"></span>
### 4.1 Entropy injection (Entropy Injection)

`proton-flink` supports enabling the Entropy Injection feature, which uses a fixed\-length random string to replace a specific segment in the write path. This resolves the QPS limit issue for a single shard in object storage by randomizing part of the path, distributing objects across multiple shards, and improving write efficiency.

For example, when writing to TOS object storage, you need to add the following parameters in `flink-conf.yaml`:

```YAML
tos.entropy.key: <user-defined-key>
tos.entropy.length: <user-defined-length>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, Flink runtime only uses the Entropy Injection option for checkpoint data files. All other files, including checkpoint metadata and external URIs, do not use Entropy Injection to ensure the predictability of checkpoint URIs.</div>


<span id="859dc361"></span>
### 4.2 Enable Proton cache acceleration mode

When the use cases utilize Proton's cache acceleration mode and you also want to accelerate Flink read and write operations, you can add the following parameters in `flink-conf.yaml` or `core-site.xml` to enable acceleration mode.

```YAML
proton.cache.enable: true
proton.metaserver.addresses: <proton-metaserver-host:port>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When enabling acceleration mode, you should consider the actual use cases to determine whether cache acceleration mode is necessary. For example, consider the reusability of data, real\-time consistency of metadata, and so on. If Flink's use cases are limited to ingesting data from external data sources and then Save it to object storage, and the ingested data will not be consumed by downstream systems within a short period, it is not recommended to use the cache acceleration mode for Flink data synchronization tasks.</div>


<span id="9eade89f"></span>
### 4.3 Hive Connector exactly\-once semantics

By default, for streaming write tasks, Flink only supports write operations via rename. Most object storage systems do not support rename operations, so generally, when writing to object storage through the hive connector, exactly\-once semantics cannot be supported. However, you can modify the following parameters in `flink-conf.yaml` and use Flink's native Parquet or Orc writer to support exactly\-once semantics. (Effective only for parquet and orc file types)

```YAML
table.exec.hive.fallback-mapred-writer: false
```


<span id="_4-使用样例"></span>
## 5 Usage examples

<span id="_4-1-flink-sql-任务读写-tos"></span>
### 5.1 Flink SQL task read and write TOS


1. Start the SQL Client.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When accessing TOS using SQL Client, you need to explicitly set <code>HADOOP_CLASSPATH</code>.   </div>
   

   ```bash
   export HADOOP_CLASSPATH=`$HADOOP_HOME/bin/hadoop classpath`
   /usr/lib/emr/current/flink/bin/sql-client.sh embedded
   
   set execution.target=yarn-per-job;
   ```
   

2. Create a data source.

   ```SQL
   create table datagen (
       id          int,
       first_name  varchar,
       last_name   varchar,
       phone       bigint,
       address     varchar,
       company     int
   ) with (
       'connector' = 'datagen',
       'rows-per-second' = '10',
       'fields.id.kind' = 'sequence',
       'fields.id.start' = '1',
       'fields.id.end' = '100000',
       'fields.first_name.length' = '5',
       'fields.last_name.length' = '5',
       'fields.phone.min' = '0000000',
       'fields.phone.min' = '9999999',
       'fields.address.length' = '7',
       'fields.company.min' = '10',
       'fields.company.max' = '20'
   );
   ```
   

3. Write data.

   ```SQL
   CREATE TABLE tos_parquet_user_sink_tbl (
       id          int,
       first_name  varchar,
       last_name   varchar,
       phone       bigint,
       address     varchar,
       company     int
   ) PARTITIONED BY (company) WITH (
    'connector' = 'filesystem',
    'path' = 'tos://{bucket}/xxxxx/flink/tos_parquet_user_tbl',
    'format' = 'parquet',
    'sink.rolling-policy.file-size' = '5MB',
    'sink.rolling-policy.rollover-interval' = '5min',
    'sink.rolling-policy.check-interval' = '1min',
    'parquet.compression'='SNAPPY' -- If compression is not required, you can omit this configuration
   );
   
   SET 'execution.checkpointing.interval' = '300s';
   
   INSERT INTO tos_parquet_user_sink_tbl SELECT * FROM datagen;
   ```
   


<span id="_4-2-flink-jar-任务读写-tos"></span>
### 5.2 Flink Jar task read and write TOS


1. Code example.

   1. pom.xml

      ```xml
      <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
          <modelVersion>4.0.0</modelVersion>
      
          <groupId>org.apache.flink</groupId>
          <artifactId>flink-kafka-tos-demo</artifactId>
          <packaging>jar</packaging>
          <version>1.0-SNAPSHOT</version>
      
          <name>flink-kafka-tos-demo</name>
      
          <properties>
              <flink.version>1.16.1</flink.version>
              <hadoop.version>3.3.4</hadoop.version>
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
                  <artifactId>flink-core</artifactId>
                  <version>${flink.version}</version>
                  <scope>provided</scope>
              </dependency>
              <dependency>
                  <groupId>org.apache.flink</groupId>
                  <artifactId>flink-java</artifactId>
                  <version>${flink.version}</version>
                  <scope>provided</scope>
              </dependency>
              <dependency>
                  <groupId>org.apache.flink</groupId>
                  <artifactId>flink-clients</artifactId>
                  <version>${flink.version}</version>
                  <scope>provided</scope>
              </dependency>
              <dependency>
                  <groupId>org.apache.hadoop</groupId>
                  <artifactId>hadoop-common</artifactId>
                  <version>${hadoop.version}</version>
                  <scope>provided</scope>
              </dependency>
      
              <dependency>
                  <groupId>org.apache.flink</groupId>
                  <artifactId>flink-connector-kafka</artifactId>
                  <version>${flink.version}</version>
              </dependency>
      
              <dependency>
                  <groupId>org.apache.flink</groupId>
                  <artifactId>flink-parquet</artifactId>
                  <version>${flink.version}</version>
              </dependency>
      
              <dependency>
                  <groupId>org.apache.parquet</groupId>
                  <artifactId>parquet-avro</artifactId>
                  <version>1.12.2</version>
                  <exclusions>
                      <exclusion>
                          <groupId>org.apache.hadoop</groupId>
                          <artifactId>hadoop-client</artifactId>
                      </exclusion>
                      <exclusion>
                          <groupId>it.unimi.dsi</groupId>
                          <artifactId>fastutil</artifactId>
                      </exclusion>
                  </exclusions>
              </dependency>
          </dependencies>
      
          <build>
              <plugins>
                  <plugin>
                      <groupId>org.apache.maven.plugins</groupId>
                      <artifactId>maven-shade-plugin</artifactId>
                      <version>3.2.1</version>
                      <executions>
                          <!-- Run shade goal on package phase -->
                          <execution>
                              <phase>package</phase>
                              <goals>
                                  <goal>shade</goal>
                              </goals>
                              <configuration>
                                  <transformers>
                                      <transformer
                                              implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                          <mainClass>org.apache.flink.KafkaToTosDemo</mainClass>
                                      </transformer>
                                  </transformers>
                              </configuration>
                          </execution>
                      </executions>
                  </plugin>
                  <plugin>
                      <groupId>org.apache.maven.plugins</groupId>
                      <artifactId>maven-compiler-plugin</artifactId>
                      <configuration>
                          <source>8</source>
                          <target>8</target>
                      </configuration>
                  </plugin>
              </plugins>
          </build>
      </project>
      ```
      

   2. Business logic.

      * KafkaToTosDemo.java

         ```java
         /* * ByteDance Volcengine EMR, Copyright 2022. * * Licensed under the Apache License, Version 2.0 (the "License"); * you may not use this file except in compliance with the License. * You may obtain a copy of the License at * *     http://www.apache.org/licenses/LICENSE-2.0 * * Unless required by applicable law or agreed to in writing, software * distributed under the License is distributed on an "AS IS" BASIS, * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. * See the License for the specific language governing permissions and * limitations under the License. */
         
         package org.apache.flink;
         
         import org.apache.flink.api.common.eventtime.WatermarkStrategy;
         import org.apache.flink.api.common.serialization.SimpleStringSchema;
         import org.apache.flink.api.common.typeinfo.Types;
         import org.apache.flink.api.java.tuple.Tuple2;
         import org.apache.flink.api.java.utils.ParameterTool;
         import org.apache.flink.connector.kafka.source.KafkaSource;
         import org.apache.flink.connector.kafka.source.enumerator.initializer.OffsetsInitializer;
         import org.apache.flink.core.fs.Path;
         import org.apache.flink.formats.parquet.avro.AvroParquetWriters;
         import org.apache.flink.shaded.jackson2.com.fasterxml.jackson.databind.JsonNode;
         import org.apache.flink.shaded.jackson2.com.fasterxml.jackson.databind.ObjectMapper;
         import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
         import org.apache.flink.streaming.api.functions.sink.filesystem.OutputFileConfig;
         import org.apache.flink.streaming.api.functions.sink.filesystem.StreamingFileSink;
         import org.apache.flink.streaming.api.functions.sink.filesystem.bucketassigners.DateTimeBucketAssigner;
         import org.apache.flink.streaming.api.functions.sink.filesystem.rollingpolicies.OnCheckpointRollingPolicy;
         import org.apache.flink.streaming.api.windowing.assigners.TumblingProcessingTimeWindows;
         import org.apache.flink.streaming.api.windowing.time.Time;
         import org.apache.parquet.hadoop.metadata.CompressionCodecName;
         
         public class KafkaToTosDemo {
           public static void main(String[] args) throws Exception {
             ParameterTool pt = ParameterTool.fromArgs(args);
         
             final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
         
             String outputPath = pt.get("tos.output.path");
             String topic = pt.getRequired("kafka.topic");
             String consumerGroup = pt.get("kafka.consumer.group.id", "kafka-to-tos-demo-group");
             String bootstrapServers = pt.getRequired("kafka.bootstrap.servers");
             String checkpointPath = pt.getRequired("checkpoint.path");
             long checkpointInterval = pt.getLong("checkpoint.interval", 10_000L);
         
             env.getCheckpointConfig().setCheckpointStorage(checkpointPath);
             env.getCheckpointConfig().setCheckpointInterval(checkpointInterval);
         
             ObjectMapper jsonParser = new ObjectMapper();
         
             env.fromSource(createKafkaSource(topic, bootstrapServers, consumerGroup),
                     WatermarkStrategy.forMonotonousTimestamps(), "Kafka Source")
                 .map(data -> {
                   JsonNode jsonNode = jsonParser.readValue(data, JsonNode.class);
                   return new Tuple2<>(jsonNode.get("ticker").toString(), 1);
                 }).returns(Types.TUPLE(Types.STRING, Types.INT))
                 .keyBy(v -> v.f0)
                 // .timeWindow(Time.minutes(1)) // Tumbling window definition // Flink 1.11
                 .window(TumblingProcessingTimeWindows.of(Time.minutes(1))) // since Flink 1.13
                 .sum(1) // Count the appearances by ticker per partition
                 .map(t -> new TickCount(t.f0, t.f1))
                 .addSink(createTosSnappySinkFromStaticConfig(outputPath))
                 .name("TOS Parquet Sink");
         
             env.execute("kafka-to-tos-demo");
           }
         
           private static KafkaSource<String> createKafkaSource(String topic, String bootstrapServers, String consumerGroup) {
             return KafkaSource.<String>builder()
                 .setBootstrapServers(bootstrapServers)
                 .setTopics(topic)
                 .setGroupId(consumerGroup)
                 .setStartingOffsets(OffsetsInitializer.earliest())
                 .setValueOnlyDeserializer(new SimpleStringSchema())
                 .build();
           }
         
           private static StreamingFileSink<TickCount> createTosSinkFromStaticConfig(String outputPath) {
             return StreamingFileSink
                 .forBulkFormat(new Path(outputPath), AvroParquetWriters.forReflectRecord(TickCount.class))
                 .withBucketAssigner(new DateTimeBucketAssigner<>("'year='yyyy'/month='MM'/day='dd'/hour='HH/"))
                 .withRollingPolicy(OnCheckpointRollingPolicy.build())
                 .withOutputFileConfig(OutputFileConfig.builder()
                     .withPartPrefix("complete")
                     .withPartSuffix(".parquet")
                     .build())
                 .build();
           }
         
           private static StreamingFileSink<TickCount> createTosSnappySinkFromStaticConfig(String outputPath) {
             return StreamingFileSink
                 .forBulkFormat(new Path(outputPath),
                     CompressionAvroParquetWriters.forReflectRecord(TickCount.class, CompressionCodecName.SNAPPY))
                 .withBucketAssigner(new DateTimeBucketAssigner<>("'year='yyyy'/month='MM'/day='dd'/hour='HH/"))
                 .withRollingPolicy(OnCheckpointRollingPolicy.build())
                 .withOutputFileConfig(OutputFileConfig.builder()
                     .withPartPrefix("complete")
                     .withPartSuffix(".parquet")
                     .build())
                 .build();
           }
         }
         ```
         

      * TickCount.java

         ```java
         /* * ByteDance Volcengine EMR, Copyright 2022. * * Licensed under the Apache License, Version 2.0 (the "License"); * you may not use this file except in compliance with the License. * You may obtain a copy of the License at * *     http://www.apache.org/licenses/LICENSE-2.0 * * Unless required by applicable law or agreed to in writing, software * distributed under the License is distributed on an "AS IS" BASIS, * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. * See the License for the specific language governing permissions and * limitations under the License. */
         
         package org.apache.flink;
         
         public class TickCount {
           private String tick;
           private int count;
         
           public TickCount(String tick, int count) {
             this.tick = tick;
             this.count = count;
           }
         
           public String getTick() {
             return tick;
           }
         
           public void setTick(String tick) {
             this.tick = tick;
           }
         
           public int getCount() {
             return count;
           }
         
           public void setCount(int count) {
             this.count = count;
           }
         }
         ```
         

      * CompressionAvroParquetWriters.java

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The <code>AvroParquetWriters</code> provided by Flink by default do not support compression and need to be reimplemented.         </div>
         

         ```java
         /* * ByteDance Volcengine EMR, Copyright 2022. * * Licensed under the Apache License, Version 2.0 (the "License"); * you may not use this file except in compliance with the License. * You may obtain a copy of the License at * *     http://www.apache.org/licenses/LICENSE-2.0 * * Unless required by applicable law or agreed to in writing, software * distributed under the License is distributed on an "AS IS" BASIS, * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. * See the License for the specific language governing permissions and * limitations under the License. */
         
         package org.apache.flink;
         
         import org.apache.avro.Schema;
         import org.apache.avro.generic.GenericData;
         import org.apache.avro.generic.GenericRecord;
         import org.apache.avro.reflect.ReflectData;
         import org.apache.avro.specific.SpecificData;
         import org.apache.avro.specific.SpecificRecordBase;
         import org.apache.flink.formats.parquet.ParquetBuilder;
         import org.apache.flink.formats.parquet.ParquetWriterFactory;
         import org.apache.parquet.avro.AvroParquetWriter;
         import org.apache.parquet.hadoop.ParquetWriter;
         import org.apache.parquet.hadoop.metadata.CompressionCodecName;
         import org.apache.parquet.io.OutputFile;
         
         import java.io.IOException;
         
         public class CompressionAvroParquetWriters {
           public static <T extends SpecificRecordBase> ParquetWriterFactory<T> forSpecificRecord(
               Class<T> type, CompressionCodecName compressionCodecName) {
             final String schemaString = SpecificData.get().getSchema(type).toString();
             final ParquetBuilder<T> builder =
                 (out) -> createAvroParquetWriter(schemaString, SpecificData.get(), out, compressionCodecName);
             return new ParquetWriterFactory<>(builder);
           }
         
           /**   * Creates a ParquetWriterFactory that accepts and writes Avro generic types. The Parquet   * writers will use the given schema to build and write the columnar data.   *   *@param schema The schema of the generic type.   */
           public static ParquetWriterFactory<GenericRecord> forGenericRecord(
               Schema schema,
               CompressionCodecName compressionCodecName) {
             final String schemaString = schema.toString();
             final ParquetBuilder<GenericRecord> builder =
                 (out) -> createAvroParquetWriter(schemaString, GenericData.get(), out, compressionCodecName);
             return new ParquetWriterFactory<>(builder);
           }
         
           /**   * Creates a ParquetWriterFactory for the given type. The Parquet writers will use Avro to   * reflectively create a schema for the type and use that schema to write the columnar data.   *   *@param type The class of the type to write.   */
           public static <T> ParquetWriterFactory<T> forReflectRecord(Class<T> type, CompressionCodecName compressionCodecName) {
             final String schemaString = ReflectData.get().getSchema(type).toString();
             final ParquetBuilder<T> builder =
                 (out) -> createAvroParquetWriter(schemaString, ReflectData.get(), out, compressionCodecName);
             return new ParquetWriterFactory<>(builder);
           }
         
           private static <T> ParquetWriter<T> createAvroParquetWriter(
               String schemaString, GenericData dataModel, OutputFile out,
               CompressionCodecName compressionCodecName) throws IOException {
         
             final Schema schema = new Schema.Parser().parse(schemaString);
         
             return AvroParquetWriter.<T>builder(out)
                 .withSchema(schema)
                 .withDataModel(dataModel)
                 .withCompressionCodec(compressionCodecName)
                 .build();
           }
         
           // ------------------------------------------------------------------------
         
           /**   * Class is not meant to be instantiated.   */
           private CompressionAvroParquetWriters() {
           }
         }
         ```
         

2. Task execution.

   1. You can generate data using the following script.

      ```python
      # generate_dummy_data.py
      import datetime
      import json
      import random
      
      
      def get_data():
          return {
              'event_time': datetime.datetime.now().isoformat(),
              'ticker': random.choice(['AAPL', 'AMZN', 'MSFT', 'INTC', 'TBV']),
              'price': round(random.random() * 100, 2)
          }
      
      if __name__ == '__main__':
          num = 1000
          with open("/root/kafka/dummy_data.json", "a") as f:
              for _ in range(0, num):
                  f.write(json.dumps(get_data()) + '\n')
      ```
      

      ```bash
      mkdir /root/kafka/
      python generate_dummy_data.py
      
      ./bin/kafka-topics.sh --bootstrap-server {borker1_ip}:9092,{borker2_ip}:9092 --topic {topic_name} --create
      
      ./bin/kafka-console-producer.sh --bootstrap-server {borker1_ip}:9092,{borker2_ip}:9092 --topic {topic_name} < /root/kafka/dummy_data.json
      ```
      

   2. Submit the task

      ```bash
      /usr/lib/emr/current/flink/bin/flink run-application \
      -t yarn-application /opt/flink-kafka-tos-demo-1.0-SNAPSHOT.jar \
      --tos.output.path tos://{bucket}/xxxx/flink/sdk/ticket_stat_snappy \
      --kafka.topic xxx_test \
      --kafka.bootstrap.servers {borker1_ip}:9092,{borker2_ip}:9092 \
      --checkpoint.path tos://{bucket}/xxxx/flink/ckp/ticket_snappy/
      ```
