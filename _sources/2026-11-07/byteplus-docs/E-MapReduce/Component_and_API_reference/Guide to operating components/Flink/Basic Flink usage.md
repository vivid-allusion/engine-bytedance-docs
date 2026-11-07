---
title: "Basic Flink usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Basic_Flink_usage"
---

<span id="_1-背景信息"></span>
## **1 context**

Log in to the Volcano Engine E\-MapReduce (EMR) server via SSH and submit a job using the command line.

Flink deployed in YARN mode supports operations for Application mode, Session mode, and Per\-Job mode.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6744647db77d04a810a5adad8ef7c254.png) </span>

Image from the official Flink documentation: [https://nightlies.apache.org/flink/flink-docs-release-1.15/docs/deployment/overview/#deployment-modes](https://docs.byteplus.com/docs/E-MapReduce/109226#deployment-modes)


|Mode |Description |Advantages and disadvantages |
|---|---|---|
|Application mode |Application mode creates a cluster for each submitted application. This cluster can be considered a session cluster shared only among jobs of the specific application, and is closed when all jobs are finished. At the application granularity, application mode provides the same resource isolation and load balancing guarantees as per\-job mode. The main() method of the job runs on the JobManager, which reduces CPU pressure on the submitter and saves bandwidth required for downloading dependencies locally. |* Advantages:<br><br>   * Provides better resource isolation guarantees.<br><br>   * Reduces the pressure on the submitter when submitting jobs.<br><br>* Disadvantages:<br><br>   * Job startup time and resource overhead are higher. |
|Per\-job mode |In per\-job mode, each job starts a dedicated Flink cluster. Jobs do not affect each other, providing better resource isolation guarantees. The cluster shuts down after the job is completed. |* Advantages:<br><br>   * Provides better resource isolation guarantees.<br><br>* Disadvantages:<br><br>   * Job startup time and resource overhead are higher. |
|Session mode |The session mode starts a Flink cluster in advance, allowing multiple jobs to run in the same cluster. The cluster is not automatically released after the jobs finish running. There is poor isolation between jobs. If an exception in one job causes the Task Manager to exit, all jobs running on that Task Manager will fail. |* Advantages:<br><br>   * Because the cluster is started in advance, jobs can be submitted more quickly.<br><br>* Disadvantages:<br><br>   * Poor resource isolation; jobs can affect each other. |


<span id="_2-使用前提"></span>
## 2 prerequisites


1. An EMR cluster with Flink component services has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. The cluster access link requires the ECS ID instance of the emr\-master\-1 node to be bound to an Elastic Public IP. For details, see [Bind Public IP](https://www.volcengine.com/docs/6401/68687).

3. To continue accessing, add the source address and corresponding port to the allowlist in **Cluster Details \> Access Link \> Quick Service Port Configuration**.

4. Flink version：1.16.1。


<span id="_3-基础使用"></span>
## 3 basic usage

<span id="_3-1-application-模式"></span>
### 3.1 Application mode


1. Connect to the cluster via SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Run the following command to submit a job.

   ```shell
   flink run-application -t yarn-application -j /usr/lib/emr/current/flink/examples/streaming/WordCount.jar
   ```
   

   After successful submission, the YARN Application ID of the submitted Flink job will be returned. The following similar information will be returned.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a26b012e627ed39f58cee2decdc9c333.png) </span>

3. Run the following command to check the job status.

   ```shell
   flink list -t yarn-application -Dyarn.application.id=application_XXXX_YY
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e543481c8d64aab8820b05de154b5f72.png) </span>

   You can also access the YARN ResourceManager UI, search by YARN Application ID, and view the Flink Web UI.

4. Run the following command to stop the job.

   ```shell
   flink cancel -t yarn-application -Dyarn.application.id=application_XXXX_YY <jobId>
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61453483a43e9628646a44bc004f97b0.png) </span>


<span id="_3-2-session-模式"></span>
### 3.2 Session mode


1. Connect to the cluster via SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Run the following command to create a session cluster.

   ```shell
   /usr/lib/emr/current/flink/bin/yarn-session.sh --detached
   ```
   

   After successful creation, the YARN Application ID of the Session cluster will be returned. The following similar information will be returned.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_398a7b02cc15f5a7a70fcbf514dcfa10.png) </span>

3. Run the following command to submit a job.

   ```shell
   flink run -t yarn-session --detached -j /usr/lib/emr/current/flink/examples/streaming/TopSpeedWindowing.jar -Dyarn.application.id=application_XXXX_YY
   ```
   

4. After successful submission, the Job ID of the submitted Flink job will be returned. The following similar information will be returned.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d3f3be8dc3d5687f1c39b6ce566b3d7.png) </span>

5. Run the following command to check the job status.

   ```shell
   flink list -t yarn-session -Dyarn.application.id=application_XXXX_YY
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26d540e5f88d1772ccb6f66a76692fc7.png) </span>

   You can also access the YARN ResourceManager UI, search by YARN Application ID, and view the Flink Web UI.

6. Run the following command to stop the job.

   ```shell
   flink cancel -t yarn-session -Dyarn.application.id=application_XXXX_YY <jobId>
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b9049c277902455eea880ebd0acdc79e.png) </span>

7. Run the following command to stop the cluster.

   ```shell
   echo "stop" | /usr/lib/emr/current/flink/bin/yarn-session.sh -id application_XXXXX_XXX
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b610f55644dcaf2783d866520c3f833.png) </span>


<span id="_3-3-per-job-模式"></span>
### 3.3 Per\-job mode


1. Connect to the cluster via SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Run the following command to submit a job.

   ```shell
   flink run -t yarn-per-job --detached -j /usr/lib/emr/current/flink/examples/streaming/TopSpeedWindowing.jar
   ```
   

   After successful submission, the YARN Application ID and Job ID of the submitted Flink job will be returned. The following similar information will be returned.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15b21003ae160317744b5c845a269921.png) </span>

3. Run the following command to check the job status.

   ```shell
   flink list -t yarn-per-job -Dyarn.application.id=application_XXXX_YY
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea2bd7167201648bcfd37709569def92.png) </span>

   You can also access the YARN ResourceManager UI, search by YARN Application ID, and view the Flink Web UI.

4. Run the following command to stop the job.

   ```shell
   flink cancel -t yarn-per-job -Dyarn.application.id=application_XXXX_YY <jobId>
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3dfb3c74ee84839a64f94b640a7f6134.png) </span>


<span id="_4-datastream-开发指南"></span>
## 4 DataStream development guide

<span id="_4-1-pom-依赖"></span>
### 4.1 Pom dependencies

Flink core dependencies do not need to be included in the final jar package. The maven\-shade\-plugin is used to build the fat jar. A demo is provided below. For more information, refer to: [Flink packaging Pom dependency example](https://github.com/volcengine/emr-tutorial/tree/master/flink-examples)

```xml
<properties>
  <maven.compiler.source>8</maven.compiler.source>
  <maven.compiler.target>8</maven.compiler.target>
  <flink.version>1.16.1</flink.version>
</properties>

<dependencies>
  <!--flink core dependencies-->
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

  <!-- kafka connector dependencies-->
  <dependency>
    <groupId>org.apache.flink</groupId>
    <artifactId>flink-connector-kafka</artifactId>
    <version>${flink.version}</version>
  </dependency>
</dependencies>

<build>
  <finalName>kafka-2-kafka-job</finalName>
  <plugins>
    <!-- We use the maven-shade plugin to create a fat jar that contains all necessary dependencies. -->
    <!-- Change the value of <mainClass>...</mainClass> if your program entry point changes. -->
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-shade-plugin</artifactId>
      <version>3.0.0</version>
      <executions>
        <execution>
          <phase>package</phase>
          <goals>
            <goal>shade</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```


<span id="_4-2-java-实现"></span>
### 4.2 Java implementation

```java
import org.apache.flink.api.common.eventtime.WatermarkStrategy;
import org.apache.flink.api.common.serialization.SimpleStringSchema;
import org.apache.flink.connector.base.DeliveryGuarantee;
import org.apache.flink.connector.kafka.sink.KafkaRecordSerializationSchema;
import org.apache.flink.connector.kafka.sink.KafkaSink;
import org.apache.flink.connector.kafka.source.KafkaSource;
import org.apache.flink.connector.kafka.source.enumerator.initializer.OffsetsInitializer;
import org.apache.flink.streaming.api.datastream.DataStreamSource;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.streaming.api.functions.sink.PrintSinkFunction;

public class Kafka2KafkaJob {

  private static final String BROKERS = "ip:port,ip1:port1,ip2:port2";

  public static void main(final String[] args) {
    new Kafka2KafkaJob().run();
  }

  private void run() {
    final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
    env.getConfig().setParallelism(1);
    final KafkaSource<String> source = KafkaSource.<String>builder()
        .setBootstrapServers(BROKERS)
        .setTopics("emr-topic-test")
        .setGroupId("emr-group")
        .setStartingOffsets(OffsetsInitializer.earliest())
        .setValueOnlyDeserializer(new SimpleStringSchema())
        .build();
    final DataStreamSource<String> kafkaSource = env.fromSource(source, WatermarkStrategy.noWatermarks(),
        "Kafka Source");

    /*     * print sink.     */
    kafkaSource.addSink(new PrintSinkFunction<>());

    /*     * kafka sink.     */
    final KafkaSink<String> kafkaSink = KafkaSink.<String>builder()
        .setBootstrapServers(BROKERS)
        .setRecordSerializer(KafkaRecordSerializationSchema.builder()
            .setTopic("emr-topic-test-1")
            .setValueSerializationSchema(new SimpleStringSchema())
            .build()
        )
        .setDeliverGuarantee(DeliveryGuarantee.AT_LEAST_ONCE)
        .build();
    kafkaSource.sinkTo(kafkaSink);

    try {
      env.execute("kafka2KafkaJob");
    } catch (final Exception e) {
      e.printStackTrace();
    }
  }
}
```


<span id="_4-3-作业-ui-图"></span>
### 4.3 Job UI diagram

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_174cd1bc4c90f6c375443e7cb630e439.png) </span>

<span id="_4-4-注意事项："></span>
### 4.4 important notes:


1. Anonymous classes must not be used in the code; lambda expressions or explicit declarations are allowed.

2. When submitting a Kafka job, you must specify parent\-first class loading to avoid dependency conflicts. The parameter is `-D classloader.resolve-order=parent-first`
