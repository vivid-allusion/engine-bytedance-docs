---
title: "HiveSQL jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_SQL_job"
---

EMR Serverless Hive supports users in submitting Hive SQL jobs. You can submit Hive SQL jobs in the EMR Serverless console. Ready to use out of the box, with no additional cluster management required.

<span id="9e40bbc4"></span>
# important notes


|Breakdown |important notes |
|---|---|
|Syntax note |EMR Serverless Hive syntax is 100% compatible with the open\-source Hive 3.1.3 version. |
|Execution engine |Supports two execution engines: Hive on MR and Hive on Tez. Tez is used by default. You can switch by setting parameters:<br><br>```SQL```<br>```-- Use mr```<br>```set hive.execution.engine=mr;```<br>```-- Use tez```<br>```set hive.execution.engine=tez;```<br> |
|Metadata management |Unified metadata service and permission control service are provided through the independent LAS service. |


<span id="0df082ac"></span>
# prerequisites


* An EMR Serverless queue has been created, and you have Developer/Admin permissions for the queue. For operation details, see: [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue)、[Queue permissions](https://docs.byteplus.com/docs/E-MapReduce/Queue_permissions).

* A compute group has been created. Currently, only the general compute group is supported. For operation details, see [Create and manage compute groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups).


<span id="cc1570ef"></span>
# Submit Job

<span id="cc2c36b2"></span>
## Submit Job: Through the console


1. Log in to the EMR Serverless console, click Resources\>Serverless in the left navigation bar, click the Serverless queue resource for the task to be created, and enter the queue resource details page.

2. In the upper right corner of the queue details page, click SQL Editor to enter the SQL task editing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4280cbeb18274bd588ada90b427d67fc~tplv-goo7wpa0wc-image.image) </span>

3. On the job editing page, select the metadata database table and set resources. After completing these steps, you can edit the SQL job in the job editing area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/718ac353b8064eafb222eee1cbb6dcd7~tplv-goo7wpa0wc-image.image) </span>

   1. Edit SparkSQL jobs in the job editing box. After editing, you can use the **Format** button in the lower left corner of the editing box to standardize the job being edited.

   2. After completing SQL job editing, you can select compute resources using **Queue** and **Compute Group** in the upper right corner of the console. After selection, click the **Run** button in the lower left corner to submit the job.

4. After the job is submitted, a **Submission Successful** indicator will pop up. When the task executes successfully, the current query results will be displayed, and the query log below will show the job ID for this submission and the current task status. You can further view detailed task information in the job management section.


<span id="ccd9c88f"></span>
## Submit Job: Through Query SDK

To submit HiveSQL jobs using the Query SDK, refer to the Spark job method and additionally configure the **tqs.query.engine.type=hive** parameter.

<span id="4552f3e9"></span>
### Java SDK

For detailed operations, see [Java Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Java_Query_SDK).

```Java
import com.volcengine.emr.serverless.SQLTask;
import com.volcengine.emr.serverless.Job;
import com.volcengine.emr.serverless.JobStatus;

String sql = "${your_sql_statement}";  // SQL to be executed
String taskName = "${your_task_name}";  // SQL job name
String queueName = "${your_queue_name}";  // Queue to use, optional parameter. If not specified, it will be selected automatically
SQLTask sqlTask = SQLTask.builder(sql)
  .name(taskName)
  .queue(queueName)
  // Used to pass some task parameters. Important: select the engine type here. The default is SparkSQL
  .addConf("tqs.query.engine.type", "hive")
  .sync(true) // Execute synchronously until the task is completed
  .build();

// Execute task
Job job = client.executeSQL(sqlTask);

assertEquals(JobStatus.COMPLETED.status(), job.getStatus());
```


<span id="6bd06b94"></span>
### Python SDK

For detailed operations, see [Python Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Python_Query_SDK).

```Python
def execute_sql_task():
    from serverless.client import ServerlessClient
    from serverless.auth import StaticCredentials
    from serverless.task import SQLTask
    from serverless.exceptions import QuerySdkError

    ak = 'xxxx' # AccessKey for access credentials, can be obtained on the 'Access Control' > 'Key Management' page in the console
    sk = 'xxxx' # SecretKey for access credentials, obtained in the same way as AccessKey
    region = 'cn-beijing'
    service = 'emr_serverless'
    endpoint = 'https://emr-serverless.cn-beijing.volcengineapi.com'
    sql = '${CUSTOM_SQL_STATEMENT}'

    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region,endpoint=endpoint)

    try:
        job = client.execute(task=SQLTask(name='sql task', query=sql, conf={'tqs.query.engine.type': 'hive'}), is_sync=True)
        if job.is_success():
            result = job.get_result()
            for record in result:
                print(', '.join([col for col in record]))

    except QuerySdkError as e:
        print(
            "Error in executing sql task. code = %s, error = %s" % (
            e.error_code, e.info))


if __name__ == "__main__":
    execute_sql_task()
```


<span id="cebbfd74"></span>
## Submit Job: Through JDBC

EMR Serverless Hive supports submitting jobs using JDBC. You can use Spark's JDBC driver to submit HiveSQL jobs, and you can also integrate with commonly used BI software on the market.

<span id="b42213e7"></span>
### Environment preparation

Dependency: JDK 1.8

JDBC download address: [emr-serverless-spark-jdbc-driver.jar](https://serverless-spark.tos-cn-beijing.volces.com/spark/jdbc/emr-serverless-spark-jdbc-driver.jar)

<span id="f4f64214"></span>
### sample code

```Java
Class.forName("org.volcano.serverless.spark.jdbc.EMRServerlessSparkDriver");
Properties properties = new Properties();
properties.setProperty("user", "Ax");
properties.setProperty("password", "xx");
Connection conn = DriverManager.getConnection("jdbc:emr-serverless-spark://serverless-spark-jdbc.emr.cn-beijing.volces.com:10009/;queue_name=queueName-computeGroup?kyuubi.engine.type=HIVE_SQL&kyuubi.engine.share.level=CONNECTION", properties);
Statement statement = conn.createStatement();
String sql = "select 1";
ResultSet resultSet = statement.executeQuery(sql);
System.out.println(resultSet.getString(1));
```


<span id="3ac53127"></span>
### JDBC connection string note

```Bash
jdbc:emr-serverless-spark://${endpoint}:10009/;queue_name=${queueName}&user=${AccessKey}&password=${SecretKey}?kyuubi.engine.type=HIVE_SQL&kyuubi.engine.share.level=CONNECTION
```



|Parameter name |Note |
|---|---|
|endpoint |Address for connecting to EMR Serverless Spark. Region addresses are as follows.<br><br><br>* North China: serverless\-spark\-jdbc.emr.cn\-beijing.volces.com<br><br>* East China: serverless\-spark\-jdbc.emr.cn\-shanghai.volces.com<br><br>* South China: serverless\-spark\-jdbc.emr.cn\-guangzhou.volces.com<br><br>* Johor: serverless\-spark\-jdbc.emr.ap\-southeast\-1.volces.com |
|queue_name |Name of the queue and compute group used for the connection. If not specified, the public queue is used by default. Format: ${queue}\-$ |
|user |Enter the tenant's AccessKey |
|password |Enter the tenant's SecretKey |
|kyuubi.engine.type |Specify the engine type. Set this to HIVE_SQL; the default is SparkSQL |
|kyuubi.engine.share.level |The connection share level is used by default. Hive client is not shared between tasks (recommended) |


<span id="da38f88d"></span>
# View and diagnose job instances

After submitting a job, you can also view the details of all submitted job run instances on the Job center \> Job instance page, including run status, job type, resource details, submitter, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ff2963cba543d1a50fb25d9508db7e~tplv-goo7wpa0wc-image.image) </span>


* At the top of the page, you can quickly filter job instances by scope, submitter, and other criteria to view the details of the job instances.

* For jobs that failed to run, you can click "Log" to view detailed job run logs and locate the cause of the failure; you can also use the "AI diagnosis" feature to perform intelligent job diagnosis.
