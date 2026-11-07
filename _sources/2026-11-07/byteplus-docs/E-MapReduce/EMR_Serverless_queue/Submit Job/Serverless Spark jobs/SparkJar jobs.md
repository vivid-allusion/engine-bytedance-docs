---
title: "SparkJar jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/SparkJar_jobs"
---

To meet users' needs for customized data query and analysis, EMR Serverless Spark provides a visual method for submitting SparkJar jobs. Users can write Java code and submit SparkJar jobs to perform distributed data processing. This article introduces multiple procedures for submitting SparkJar jobs.

# Prerequisites

* A resource queue or public queue with general resources has been created. For specific procedures, refer to: [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue). Queue Developer/Admin permissions are required.

* The job files, dependency Jar packages, and dependency files have been uploaded to the TOS bucket in the same region as the current Serverless queue.

* To use a runtime role to access cloud resources, create and configure a job runtime role and copy the complete role TRN. For detailed instructions, see [Runtime Roles](https://docs.byteplus.com/docs/undefined/6adb36d276430b031596a173).

# **Submit Job**

## Submit Job: via console

1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the top menu bar, select the region and project space from the drop\-down menus according to your actual scenario.

3. Click Job center \> Job management or Job instance to enter the Create job page

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7c6b3ca8f50408099947bf93322a75c~tplv-goo7wpa0wc-image.image)

4. Configure the parameters for the Spark JAR job.

   1. Configure the job **basic information**. See the table below for parameter descriptions.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb7d64d11cd04797be8cda85df04c6a2~tplv-goo7wpa0wc-image.image)

      |**Parameter** |**Configuration operation** |
      |---|---|
      |Job Name |The name of this job. It cannot be changed after creation. |
      |Job types |The type of job to be created. |
      |Execution resources |The EMR resources used to execute the job, divided into resource type drop\-down and queue/project drop\-down.<br><br>You can select specific resources and search by name or ID. |
      |development model |* UI: Submit job content through the visual interface.<br><br>* JSON: Submit job content in JSON format, which is more suitable for batch configuration or reusing existing configurations. For example:<br><br><br>```JSON```<br>```{```<br>``` "JobType": "SparkJar",```<br>``` "ServerlessSparkRuntimeVersion": "spark4.1",```<br>``` "MainClass": "com.example.MainClass",```<br>``` "MainApplicationFile": "tos://<your-bucket>/<path>/your-app.jar",```<br>``` "SparkConf": {```<br>``` "RuntimeRole": "trn:iam::{$AccountID}:role/{$RoleName}"```<br>``` "emr.execute.resource.type": "EMR_Serverless",```<br>``` "tqs.query.engine.type": "Spark"```<br>``` },```<br>``` "Jars": [```<br>``` "tos://<your-bucket>/<path>/extra-dependency.jar"```<br>``` ],```<br>``` "Files": [```<br>``` "tos://<your-bucket>/<path>/dependency-file"```<br>``` ],```<br>``` "Archives": [],```<br>``` "MainArguments": []```<br>```}```<br> |

   2. Configure the **job content**. The parameter entry points differ depending on the development mode. See the table below for parameter descriptions.

      |**UI mode parameters** |**JSON mode parameters** |**Required** |**Note** |
      |---|---|---|---|
      |EngineRuntime |ServerlessSparkRuntimeVersion |Y |Select the Spark compute engine environment. You can choose the Spark version and the corresponding Java Runtime or Bolt Runtime.<br><br><br>* Java Runtime: Standard Java runtime.<br><br>* Bolt Runtime: BytePlusSelf\-developed native kernel acceleration engine that can improve the execution speed of Spark, Presto, and other jobs. For details, see [Spark on Native engine: Bolt](https://docs.byteplus.com/en/docs/E-MapReduce/sq_spark_on_native_engine).<br><br><br>> **注意**<br><br><br>> The EngineRuntime parameter of the job takes precedence over the default compute group and general compute group parameters.<br> |
      |Main method |MainClass |Y |The main class for running the SparkJar job. |
      |Main task file |MainApplicationFile |Y |The main task Jar file for the SparkJar job.<br><br>They must be uploaded to TOS and the path specified here. |
      |Runtime role |RuntimeRole |N |The IAM identity used to access cloud resources during job runtime. For more information, see [Runtime Roles](https://docs.byteplus.com/docs/undefined/6adb36d276430b031596a173). |
      |Dependency Jar |Jars |N |Third\-party or custom JAR packages that the main JAR file depends on at runtime. Executors will automatically load them when executing tasks.<br><br>They must be uploaded to TOS and the path specified here. |
      |Depend on File resources |Files |N |Resource files that the job depends on.<br><br>They must be uploaded to TOS and the path specified here. |
      |Dependency Archive |Archives |N |Archive dependencies for the job.<br><br>They must be uploaded to TOS and the path specified here. |
      |Spark parameters (spark conf) |SparkConf |N |Environment variables and resources used by the job.<br><br>For example, `"spark.emr.connect.engine.allow.other.users": true`.<br><br>> **注意**<br><br><br>> In UI mode, the EngineRuntime parameter is passed as an option. If you submit the EngineRuntime parameter here, it will not take effect.<br> |
      |Main parameter (Main conf) |MainArguments |N |Enter the input parameters required when running the job's main class. |
      |Storage path mount |This parameter is not yet supported in JSON mode. |N |Set the storage path that may need to be mounted for the current job. For details, see [Overview of storage mounting](https://docs.byteplus.com/docs/E-MapReduce/Overview_of_storage_mounting). |

## Submit Job: via SDK

Currently, EMR Serverless supports Java and Python SDKs. For Java SDK usage, refer to: [Java Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Java_Query_SDK); for Python SDK usage, refer to: [Python Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Python_Query_SDK).

## Submit Job: via Spark Submit

For usage, refer to the documentation: [Spark-submit tool usage instructions](https://docs.byteplus.com/docs/E-MapReduce/Spark-submit_tool_usage_instructions).

## Submit Job: Add dependencies via parameters

You can add dependencies such as Jar files, Python packages, and others when submitting a job. The parameter list is as follows:

|Parameter name |Parameter description |Parameter usage |
|---|---|---|
|las.spark.jar.depend.jars |Jar packages that the job depends on |[{"fileName": "tos://bucketName/xxx.jar"},{"fileName": "tos://bucketName/yyy.jar"}] |
|las.spark.jar.depend.files |Files that the job depends on |[{"fileName": "tos://bucketName/xxx.csv"},{"fileName": "tos://bucketName/yyy.csv"}] |
|las.spark.jar.depend.archives |Archive files that the job depends on |[{"fileName": "tos://bucketName/xxx.zip"}, {"fileName": "tos://bucketName/yyy.zip"}] |
|las.spark.jar.depend.pyFiles |Python files that the job depends on |[{"fileName": "tos://bucketName/xxx.zip"},{"fileName": "tos://bucketName/yyy.zip"}] |

## Advanced operation: how to read and write database tables

By default, SparkJar jobs cannot read or write LAS database tables under the user's account. To read and write database tables in SparkJar jobs using Spark SQL/Table API, additional settings are required in Spark parameters:

```Java
"Conf":{
  "serverless.spark.runtime.role": "trn:iam::{$AccountID}:role/{$RoleName}"
}
```

|Parameter name |Parameter value |
|---|---|
|serverless.spark.runtime.role |The runtime role for Submit Job and reading data. For more information, see [Runtime Roles](https://docs.byteplus.com/docs/undefined/6adb36d276430b031596a173). |

# View/run/delete jobs

After a job is created, you can view all created jobs on the job list page, manually trigger a job to run, or edit, modify, and delete jobs.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1941ed94ade4f4cbbd2cde209b34c06~tplv-goo7wpa0wc-image.image)

# View and diagnose job instances

After submitting a job, you can also view the details of all submitted job run instances on the Job center \> Job instance page, including run status, job type, resource details, submitter, and more.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ff2963cba543d1a50fb25d9508db7e~tplv-goo7wpa0wc-image.image)

* At the top of the page, you can quickly filter job instances by scope, submitter, and other criteria to view the details of the job instances.

* For jobs that failed to run, you can click "Log" to view detailed job run logs and locate the cause of the failure; you can also use the "AI diagnosis" feature to perform intelligent job diagnosis.
