---
title: "Java Query SDK"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/sdk_Java_Query_SDK"
---

<span id="_1-简介"></span>
## Introduction

The Serverless Spark Java Query SDK helps users easily use the Serverless Spark query service with the Java language. The main features currently include task submission and cancellation, task information retrieval, result retrieval, and more.

This document provides sample code for the above features for your reference.

<span id="_2-概念说明"></span>
## Concepts

System concepts:


* Endpoint overview:

   * Endpoint: is the API domain name for Serverless Spark external services.

   * Region: is the physical location of the Serverless Spark data center.

      Currently, Serverless Spark supports regions and API domains For BytePlus, see[Service address](https://docs.byteplus.com/docs/E-MapReduce/Service_address_ecs).

* Access Key / Secret Access Key: Credentials for accessing the Volcano Engine API. Users can obtain the Access Key and Secret Access Key from the Volcano Engine "Key Management" page.


<span id="_3-安装-sdk"></span>
## Install SDK

Requirements:


* Java 1.8 or later

* Maven


Install the SDK by adding dependencies to your Maven project. Add the corresponding dependencies to the pom.xml file.

```xml
<repository>
    <id>bytedance-public</id>
    <name>bytedance maven</name>
    <url>https://artifact.bytedance.com/repository/releases</url>
</repository>

<dependency>
  <groupId>com.volcengine.emr.serverless</groupId>
  <artifactId>serverless-sdk-query</artifactId>
  <version>1.0.2</version>
</dependency>
```


<span id="_4-快速入门"></span>
## Quick Start

<span id="_4-1-初始化客户端"></span>
### Initialize client

The Serverless Spark SDK currently provides only one method for static client initialization, which is done by configuring the endpoint, region, Access Key, and Secret Access Key:

```java
import com.volcengine.emr.serverless.ServerlessClientOption;
import com.volcengine.emr.serverless.ServerlessQueryClient;

String ak = "${access_key}";
String sk = "${secret_key}";
String endpoint = "https://emr-serverless.cn-beijing.volcengineapi.com";
// Please fill in the corresponding endpoint according to the actual region
String service = "emr_serverless";
String region = "cn-beijing";
int connTimeoutMs = 30000;
int socketTimeoutMs = 30000;

ServerlessClientOption options = ServerlessClientOption.builder(ak, sk)
  .endpoint(endpoint)
  .service(service)
  .region(region)
  .connectionTimeoutMs(connTimeoutMs)
  .socketTimeoutMs(socketTimeoutMs)
  .build();

ServerlessQueryClient client = new ServerlessQueryClient(options);
```


`ServerlessQueryClient` is the entry point for invoking various Serverless Spark features. The current version of the client provides the following APIs:


|API |Feature |
|---|---|
|executeSQL |Execute SQL job |
|executeJar |Execute Jar job |
|cancelJob |Cancel task instance |
|getJob |Obtain task instance status |
|rerunJob |Rerun task instance |
|getResult |Obtain job result |
|getTrackingUrl |Obtain job UI link |
|getDriverLog |Obtain job driver log |
|getSubmissionLog |Obtain job submission log |


<span id="_4-2-第一个查询"></span>
### First query

After initializing the client, you can execute relevant tasks (currently supporting SparkSQL and SparkJar task types).

The following is an example of a simple SQL query:

```java
import com.volcengine.emr.serverless.SQLTask;
import com.volcengine.emr.serverless.Job;
import com.volcengine.emr.serverless.JobStatus;

String query = "select 1";
String name = "first_query_task";

// Define the task
SQLTask sqlTask = SQLTask.builder(query)
  .name(name)
  .sync(true)
  .build();

// Execute the task
Job job = client.executeSQL(sqlTask);
```


<span id="_5-更多示例"></span>
## More examples

This section presents additional Serverless Spark features in the form of code samples.

<span id="_5-1-提交-取消任务"></span>
### Submit/cancel tasks

<span id="_5-2-提交-sql-任务"></span>
### Submit SQL task

```java
import com.volcengine.emr.serverless.SQLTask;
import com.volcengine.emr.serverless.Job;
import com.volcengine.emr.serverless.JobStatus;

String sql = "${your_sql_statement}";  // SQL to be executed
String taskName = "${your_task_name}";  // SQL job name
String queueName = "${your_queue_name}";  // Queue to use, optional parameter; if not specified, it will be selected automatically
SQLTask sqlTask = SQLTask.builder(sql)
  .name(taskName)
  .queue(queueName)
  // Used to pass some task parameters, for example: spark.sql.shuffle.partitions -> 2000
  .addConf("serverless.compute.group.name", "xxx")  // Compute group name, optional parameter; the Default compute group is used by default
  .addConf("spark.sql.xxx", "xxx")
  .sync(true) // Execute synchronously until the task is completed
  .build();

// Execute the task
Job job = client.executeSQL(sqlTask);

assertEquals(JobStatus.COMPLETED.status(), job.getStatus());
```


Supports Spark 3.5 syntax

For differences between synchronous and asynchronous task submission, refer to section 5.1.3 Synchronous/Asynchronous Execution

<span id="_5-3-提交-sparkjar-任务"></span>
### Submit SparkJar task

SparkJar tasks allow users to meet customized data analysis requirements by developing Spark applications. See the [SparkJar jobs](https://docs.byteplus.com/docs/E-MapReduce/SparkJar_jobs) documentation.

Example:

```java
import com.volcengine.emr.serverless.JarTask;
import com.volcengine.emr.serverless.Job;
import com.volcengine.emr.serverless.JobStatus;


String jarResource = "${tos_path_to_jar_resource}";  // TOS path of the jar resource to be executed, for example: tos://bucket/path/to/spark_pi_example.jar
String mainClass = "${main_class_reference}";  // Main class of the jar job, for example: org.apache.spark.examples.SparkPi
List<String> mainArgs = ImmutableList.of("${param1}", "${param_2}");  // Main class parameters for the jar job
String taskName = "${your_task_name}";  // Jar job name
String queueName = "${your_queue_name}";  // Queue to use, optional parameter; if not specified, it will be selected automatically
JarTask jarTask = JarTask.builder(jarResource, mainClass)
  .name(taskName)
  .queue(queueName)
  .mainArgs(mainArgs)
  // Used to pass some task parameters, for example: spark.sql.shuffle.partitions -> 2000
  .addConf("spark.sql.xxx", "xxx")
  .sync(true) // Execute synchronously until the task is completed
  .build();

// Execute the task
Job job = client.executeJar(jarTask);

assertEquals(JobStatus.COMPLETED.status(), job.getStatus());
```


<span id="_5-4-同步-异步执行"></span>
### Synchronous/asynchronous execution

Control synchronization by configuring the sync parameter of the Task:

```java
// Synchronous: blocks until the task status changes to a terminal state such as Success/Failure/Canceled
SQLTask task = SQLTask.builder(query)
  .sync(true)
  .build();

// Asynchronous: immediately returns the current status of the task instance
SQLTask task = SQLTask.builder(query)
  .sync(false)
  .build();
// You can subsequently use custom logic to periodically check the latest task status for processing
/*
例如下面例子，将阻塞等待直至任务完成
waitForJob(client, job.getId(), jb -> {  JobStatus jobStatus = JobStatus.fromString(jb.getStatus());  return !JobStatus.isFinished(jobStatus);});
public static void waitForJob(ServerlessQueryClient client,
  String jobId, Function<Job, Boolean> condition
) {
  Job job = client.getJob(jobId);
  try {
    while (condition.apply(job)) {
      Thread.sleep(5 * 1000L);
      job = client.getJob(jobId);
    }
  } catch (InterruptedException e) {
    log.error("InterruptedException", e);
  }
}
waitForJob(client, job.getId(), jb -> {  JobStatus jobStatus = JobStatus.fromString(jb.getStatus());  return !JobStatus.isFinished(jobStatus);});
waitForJob(client, job.getId(), jb -> {
  JobStatus jobStatus = JobStatus.fromString(jb.getStatus());
  return !JobStatus.isFinished(jobStatus);
});
waitForJob(client, job.getId(), jb -> {  JobStatus jobStatus = JobStatus.fromString(jb.getStatus());  return !JobStatus.isFinished(jobStatus);});
*/
```


<span id="_5-5-取消任务"></span>
### Cancel task

```java
// Cancel directly by passing in the task ID
client.cancelJob("${jobId}");
```


<span id="_6-查看任务实例相关信息"></span>
## View task instance information

<span id="_6-1-获取任务实例"></span>
### Retrieve task instance

You can retrieve a task instance by task ID:

```java
// Obtain the current instance status of the task directly by passing in the task ID
client.getJob("${jobId}");
```


<span id="_6-2-获取引擎侧任务执行-ui"></span>
### Retrieve engine\-side task execution UI

Obtain the corresponding Spark UI page from the retrieved task instance:

```java
// If no interface is generated, an exception will be thrown; it is recommended to use try-catch when using
client.getTrackingUrl("${jobId}");
```


<span id="_7-获取查询结果"></span>
## Retrieve query result

Call `getResult()` on the job instance to retrieve the query result:

```java
import com.volcengine.emr.serverless.ResultCursor;

// Obtain the ResultCursor of the task directly by passing in the task ID
ResultCursor resultCursor = client.getResult("${jobId}");

// Output the result set header
List<String[]> resultHeader = resultCursor.getHeader();
for (String[] field : resultHeader) {
  System.out.println(Arrays.toString(field));
}

// Output the result set
while (resultCursor.hasNext()) {
  resultCursor.fetchNextPage();
  List<List<String>> currentRows = resultCursor.getCurrentRows();
  for (List<String> row : currentRows) {
    System.out.println(row);
  }
}
```


<span id="_8-获取任务日志"></span>
## Retrieve task logs

<span id="_8-1-获取提交日志"></span>
### Retrieve submission logs

Obtain the submission log by task ID

```python
String jobId = "${job_id}";
LogCursor logCursor = client.getSubmissionLog(jobId);

List<String> logRows = new ArrayList<>();
while (logCursor.hasNext()) {
    logCursor.fetchNextPage();
    List<String> currentRows = logCursor.getCurrentRows();
    logList.addAll(currentRows);
}
```


<span id="_8-2-获取执行日志"></span>
### Obtain the execution log

Obtain the execution log by task ID

```python
String jobId = "${job_id}";
LogCursor logCursor = client.getDriverLog(jobId);

List<String> logRows = new ArrayList<>();
while (logCursor.hasNext()) {
    logCursor.fetchNextPage();
    List<String> currentRows = logCursor.getCurrentRows();
    logList.addAll(currentRows);
}
```


<span id="_10-执行异常"></span>
## Execution exception

Task exceptions will be thrown as `com.volcengine.emr.serverless.QuerySdkException` (an unchecked exception, no explicit catch required), with the specific execution error information included in the exception message.
