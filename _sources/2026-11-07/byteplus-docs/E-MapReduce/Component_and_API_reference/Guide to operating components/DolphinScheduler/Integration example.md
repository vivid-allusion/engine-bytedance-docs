---
title: "Integration example"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Integration_example"
---

This article demonstrates how to run Spark and Flink tasks in DolphinScheduler on Volcano Engine E\-MapReduce (EMR), helping you better understand how to use DolphinScheduler.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An EMR cluster with the DolphinScheduler component has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. To access the DolphinScheduler Web UI, you need to bind an elastic public IP to the **emr\-master\-1\-1** machine instance and configure the service port (the default service port for DolphinScheduler is **12345**). For details, see [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).


<span id="_2-资源中心"></span>
## 2 Resource center

In DolphinScheduler, the **resource center** is typically used for uploading files, UDF functions, and managing task groups. The resource center in EMR DolphinScheduler is based on the Hadoop cluster within the same cluster. The default directory is `/dolphinscheduler`, defined by the configuration item `resource_upload_path`. For information on how to modify service configuration parameters, refer to [Manage service configuration parameters](https://docs.byteplus.com/docs/E-MapReduce/105412).

In this example, we will run a classic WordCount program. You need to upload the required Spark jar, Flink jar, and word text file (see below) to the resource center first, and then reference them when defining the specific workflow later.


* Spark jar:

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_803d35deaf7a3561af78e1f48005d54f.jar" name="spark_test_jar.jar">spark_test_jar.jar</Attachment>
   

* Flink jar:

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d80e63439876c9572bc2b339d2bad05.jar" name="Flink_test_jar.jar">Flink_test_jar.jar</Attachment>
   

* Word text information

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ce4eaf1a200cb58f19e92f977fa3fa2.txt" name="wordcount文件.txt">wordcount文件.txt</Attachment>
   


The upload steps are as follows:


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, click **Cluster Management \> Cluster List \> DolphinScheduler Cluster Details \> Access Link \> DolphinScheduler UI Access Link** to enter the Web UI login page.

3. Enter the corresponding username and password, and after confirmation, access the Web UI interface. For information on creating users, see [快速开始---创建用户](https://docs.byteplus.com/docs/E-MapReduce/109217#_5-%E5%88%9B%E5%BB%BA%E7%94%A8%E6%88%B7).

4. In the top navigation bar, click the **Resource Center** button to enter the resource folder management page.

5. In the **File Management** page, click the **Upload File** button, select the corresponding file from your local machine, and click the **Confirm** button to complete the resource upload.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_773b7a41317502d7b6bbac247a9737e1.png) </span>


<span id="_3-数据源中心"></span>
## 3 Data source center

When running Spark SQL or Hive SQL tasks, DolphinScheduler requires you to pre\-configure the data source connection information in the data source center. Here, as an example, we configure a Spark data source in a Hadoop\-type cluster of EMR version 3.x.

<span id="_3-1-ha-集群"></span>
### 3.1 HA cluster

The HA cluster configuration example is as follows:


1. Click the **Data Source Center** button in the top navigation bar to enter the data source center page.

2. Click **Create Data Source** and configure the following data source information:

   
   |Configuration item |Example |Note |
   |---|---|---|
   |Data source |spark |Select the data source type from the dropdown; here, select the Spark data source type. |
   |Data source name |spark_source |Enter the data source name. |
   |Description |HA cluster configuration |Enter a description for this data source to facilitate subsequent management. |
   |IP hostname |emr\-master\-1\-1,emr\-master\-2,emr\-master\-3 |Enter the master node name for the Spark data source. |
   |Port |2181 |Fill in the corresponding port number. |
   |Username |hive |The username for the Spark data source. |
   |Password |<br>---<br><br> |The password for the Spark data source. |
   |Database name |default |The database name for the data source. |
   |Jdbc connection parameters | |Enter connection parameters in JSON format, using the format {"key1":"value1","key2":"value2"...}; this field is optional. |
   

3. The username and password used above can be obtained from the following path:

   1. Go to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home) \> **Cluster management \> Cluster list \> DolphinScheduler cluster details \> Service list \> OpenLDAP \> Service parameters** page.

   2. Obtain the administrator account information for the Hive service parameter name:

      * Account: `hive_admin` configuration item content;

         * Password: `hive_password` configuration item content.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3032a475ae1d3a549dd86b382a58eb3a.png) </span>


<span id="_3-2-非-ha-集群"></span>
### 3.2 Non\-HA cluster

The configuration example for a non\-HA cluster is as follows:


|Configuration item |Example |Note |
|---|---|---|
|Data source |spark |Select the data source type from the dropdown; here, select the Spark data source type. |
|Data source name |spark_data |Enter the data source name. |
|Description |Non\-HA cluster configuration |Enter a description for this data source to facilitate subsequent management. |
|IP hostname |emr\-master\-1\-1 |Enter the master node name for the Spark data source. |
|Port |10005 |Fill in the corresponding port number. |
|Username |hive |The username for the Spark data source. |
|Password |<br>---<br><br> |The password for the Spark data source. |
|Database name |default |The database name for the data source. |
|Jdbc connection parameters | |Enter connection parameters in JSON format, using the format {"key1":"value1","key2":"value2"...}; this field is optional. |


<span id="_4-工作流定义"></span>
## 4 Workflow definition

<span id="_4-1-使用前提"></span>
### 4.1 Prerequisites


1. The relevant DolphinScheduler project, user information, and queue information have been created. For details, see [quickstart](https://docs.byteplus.com/docs/E-MapReduce/109217).


<span id="_4-2-操作步骤"></span>
### 4.2 Procedure


1. Click the **Project management** button at the top of the page to enter the project list page.

2. Click the specific **project name** to enter the project overview page.

3. In the left navigation bar, click the **Workflow \> Workflow definition** button to enter the workflow definition page.

4. Click the **Create workflow** button to enter the workflow DAG editing page. Drag the corresponding task type to the right panel to add the corresponding task.


<span id="_4-3-hive-spark-sql"></span>
### 4.3 Hive / Spark SQL

<span id="_4-3-1-配置作业"></span>
#### 4.3.1 Configure job

Drag the SQL task type to the right panel and complete the following configuration information:


|Parameter |Note |
|---|---|
|Node name |Enter the node name for the task type. |
|Run flag |Select the task execution status. Supported options are **Normal, Disabled**. If "Disabled" is selected, the workflow will not execute this task. |
|Description |Enter a task description for the current node to facilitate later differentiation. |
|Task priority |Select the priority level for the current task. There are five levels from HIGHEST to LOWEST. You can select based on actual requirements. When the number of worker threads is insufficient, tasks with higher priority will be executed first in the queue. Tasks with the same priority are executed in a first\-in, first\-out order. |
|Worker group |Select a successfully created worker group from the dropdown. |
|Environment name |Configure the environment for task execution. Select a successfully created environment name from the dropdown. |
|Task group name |Manage the resources occupied by task instances through task groups to prevent excessive resource usage from affecting other components in the cluster. You can create a task group in **Resource Center \> Task Group Management**. See [Task Group Management](https://dolphinscheduler.apache.org/zh-cn/docs/3.1.3/guide/resource/task-group) for details. |
|In\-group priority |Set the priority of this task within the current task group so that it can obtain resources first within the group. |
|Retry count on failure |The number of times the task is resubmitted after failure. This can be manually entered. |
|Retry interval on failure |The interval between resubmitting the task after failure. This can be manually entered. |
|Delayed execution time |The time to delay task execution, in minutes. |
|Timeout alert |Configure timeout alert and timeout failure. When the task exceeds the "timeout duration", an alert email will be sent and the task execution will fail. |
|Data source type |Select a successfully created Spark data source from the dropdown. |
|Data source instance |Select the Spark data source instance that has passed the connectivity test. |
|SQL type\-\-\-Query |* SQL query type. You can choose whether to enable email alerts:<br><br>   * Subject: The subject information for alert emails.<br><br>   * Alert group: Select the corresponding alert group information for email receipt. For detailed configuration, see [quickstart](https://docs.byteplus.com/docs/E-MapReduce/109217).<br><br>* Log display: Specifies the number of query result rows shown in the log. |
|SQL type\-\-\-non\-query |Multiple SQL statements can be executed, and a delimiter can be set for segment execution. |
|SQL statement |Enter the SQL execution statement. |
|UDF function |For HIVE\-type data sources, you can reference UDF functions created in the resource center. Other types of data sources currently do not support UDF functions. |
|Custom parameters |For SQL task types, the parameter order is custom, as with stored procedures. You can set values for methods, custom parameter types, and data types, just as with stored procedure task types. The difference is that custom parameters for SQL task types will replace ${variable} in the SQL statement. |
|Pre\-SQL statement |Pre\-SQL is executed before the SQL statement. |
|Post\-SQL statement |Post\-SQL is executed after the SQL statement. |
|Predecessor task |Set the predecessor (upstream) task for the current task to establish upstream and downstream dependencies. |


Spark SQL is consistent with Hive; you only need to select the correct type and instance when choosing the data source.

SQL statement example:

```sql
-- SQL statement:
create table if not exists dolphin_test_spark_x(id int);
```


<span id="_4-3-2-运行作业"></span>
#### 4.3.2 Run job

After the job configuration is completed, you can perform the following steps to execute the configured job:


1. In the editing page, click the **Save** button in the upper right corner to save the workflow configuration.

2. Return to the workflow definition list page and click the **Online** button in the operation column to complete the job release.

3. Click the **Run** button to run the workflow. The workflow will generate the corresponding workflow instance. You can go to the **Workflow instance** page to view the specific instance execution status.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ae0c6c5256d807fbe8f380c3072449e.png) </span>

4. After the workflow instance has finished running, log in to the instance node of the DolphinScheduler cluster and execute the following command:

   For login methods, see [创建租户-集群远程登录](https://docs.byteplus.com/docs/E-MapReduce/109217#_4-%E5%88%9B%E5%BB%BA%E7%A7%9F%E6%88%B7).


```shell
spark-sql

show tables;
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_611386598ab76b0e80cab9a6f3620800.png) </span>

<span id="_4-4-flink"></span>
### 4.4 Flink

Flink tasks support both SQL and JAR submission methods.

<span id="_4-4-1-jar-包提交"></span>
#### 4.4.1 JAR submission

The main workflow parameter configuration is as follows:


|Parameter |Example value |Note |
|---|---|---|
|Program type |JAVA |Supports selecting JAVA, SQL, SCALA, or PYTHON types. |
|Main function class |org.apache.flink.streaming.examples.wordcount.WordCount |Enter the main function class information from the Jar package. |
|Main program package |Flink_test_jar.jar |Use the dropdown to select a successfully uploaded Jar package resource. |
|Deployment mode |pre\-job/cluster |Supports pre\-job/cluster (optional when Flink version is greater than 1.10), application, and local deployment modes. |
|Flink version |> =1.12 |Supports selecting '<1.10', '1.11', or '\>=1.12' for Flink version information. |
|Main program parameters |\-input hdfs://emr\-master\-1\-1:8020/dolphinscheduler/project_name/resources/wordcount文件.txt \-\-output hdfs:/emr\-master\-1\-1:8020/tmp/test_x |Fill in the main program parameters according to the actual path and file name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For HA clusters, use hdfs://emr\-cluster/...</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This example runs a WordCount program, which requires an input text file and outputs the results to a specified location. Here, we specify these using the <code>--input</code> and <code>--output</code> parameters in the main program.</div><br> |
|Resource |wordcount文件.txt |Use the dropdown to select a successfully uploaded file. |


<span id="_4-4-2-sql"></span>
#### 4.4.2 SQL

To run a Flink SQL task, simply select SQL as the program type and enter the required SQL in the script input box. For the support status of different Flink deployment methods in EMR, please refer to [Basic Flink usage](https://docs.byteplus.com/docs/undefined/69a962388a3fb00506e9840f).

<span id="_4-5-spark-submit"></span>
### 4.5 Spark\-submit

Similar to the Flink JAR submission method, Spark\-submit also relies on program packages and supporting resource files uploaded through the resource center.

The main workflow parameter configuration is as follows:


|Parameter |Example value |Note |
|---|---|---|
|Program type |JAVA |Supports selecting JAVA, SQL, SCALA, or PYTHON types. |
|Spark version |SPARK2 |Select the Spark version according to the actual scenario. Supports Spark1 and Spark2. |
|Main function class |org.apache.spark.examples.JavaWordCount |Enter the main function class information from the Jar package. |
|Main program package |spark_test_jar.jar |Use the dropdown to select a successfully uploaded Jar package resource. |
|Deployment mode |cluster |Supports cluster, client, and local deployment modes. |
|Main program parameters |/dolphinscheduelr/tenant_name/resources/resource_center_folder_name/file_name |Fill in the main program parameters according to the actual tenant name and file name. |
|Resource |wordcount文件.txt |Use the dropdown to select a successfully uploaded file. |


After completing the configuration and successfully running the workflow task, you can log in to the YARN UI to view the corresponding execution results:


1. Go to the **Cluster Management \> Cluster List \> DolphinScheduler Cluster Details \> Service List \> OpenLDAP \> Service Parameters** page.

2. Obtain the username and password for logging in to the YARN UI.

3. Go to **DolphinScheduler Cluster Details \> Access Links,**  click the **YARN ResourceManager UI** access link, and log in.

4. Under the corresponding Spark job ID, view the final execution log results.
