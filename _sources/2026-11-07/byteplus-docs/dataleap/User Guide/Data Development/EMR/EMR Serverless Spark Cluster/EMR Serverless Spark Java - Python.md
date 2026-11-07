---
title: "EMR Serverless Spark Java/Python"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/emr_serverless_spark_java_and_python"
---

DataLeap supports integration with Serverless Spark instances in BytePlus E\-MapReduce (EMR). You can write Java or Python code locally and upload it to the TOS object storage system. Then, in DataLeap, you can visually configure Spark Java or Python jobs, reference resources, and execute tasks to meet the data development demand in your business scenarios. This article will introduce the configuration operations for EMR Serverless Spark Java and Python tasks in DataLeap.@bytehouse ce

<span id="a4939f06"></span>
## 1 The functionality background

EMR Serverless Spark is a serverless data product within the EMR framework that is ready to use and fully compatible with the open\-source Spark engine. It features a built\-in high\-availability Remote Shuffle Service (RSS), which allows the Shuffle Service to run independently of Spark and enables direct read\-write access to the TOS object storage system. This decouples storage and computation, resulting in improved availability and performance.

In business scenarios involving large\-scale machine learning and deep learning training, you can use DataLeap to execute Serverless Spark Java/Python tasks to process massive data and perform complex calculations. By leveraging the high availability and compute\-storage separation architecture capabilities of EMR Serverless Spark, you can accelerate the model training process and effectively improve the accuracy and efficiency of business decisions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54b3dfaf5ab24cb19e170bc36c0c5d59~tplv-goo7wpa0wc-image.image) </span>

<span id="89ef557a"></span>
## 2 Limitted use


* You must enable **Big Data Analytics, DataOps Development** or **Distributed data autonomy** services in the DataLeap service version before the project can continue binding the **EMR Serverless Spark** instance. See details [Billing Instructions for Version Services](https://docs.byteplus.com/docs/dataleap/Billing_Instructions_for_Version_Services).

* Switching between language types in EMR Serverless Spark Java/Python tasks is not supported yet. Switching the language type will clear the current configuration, so please switch with caution.

* This task type does not yet support sending message notifications after a debug execution succeeds or fails.


<span id="124df66c"></span>
## 3 Prerequisites for use


1. The \*\*\*\* [EMR Serverless Spark Queue](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Queue_management) resource instance has been enabled. When using sub\-users to access EMR Serverless Spark queue resources in DataLeap, you must ensure that you have the EMRServerlessReadOnlyAccess or a higher permission policy. A sub\-user can request the main account to add permission policies in the Access Control interface, or configure the relevant permissions using a custom policy.

2. The TOS object storage service is used to store LAS Catalog database and table data and JAR package resources. Therefore, you must enable the TOS service in advance and [create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket). When sub\-users access TOS resources through EMR Serverless Spark Java or Python tasks, you need to ensure that they have the required TOS access rights. For details on permission configuration operations, see [TOS permission configuration](https://docs.byteplus.com/en/docs/tos/docs-permission-configuration-guide).

3. If you create an EMR Serverless Spark Java task, the resource package uploaded to TOS will be used directly, and you need to obtain the resource package path information. For details on the resource package upload action, see [Upload file](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

4. The corresponding EMR Serverless Spark service instance has already been bound in the DataLeap Project Console. See details[Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).


<span id="6e856aa7"></span>
## 4 Create a task


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc), go to the project's **IDE development** interface, and create a new task using the **New Task** function.

2. Click the **New Task** button:

   1. Go to **Data Development \> EMR Serverless Spark \> EMR Serverless Spark Java/Python** and select the task type.

   2. Associated instance: The EMR Serverless Spark instance bound to the default option item. For details about binding, see [Create a Project](https://docs.byteplus.com/docs/dataleap/create_project).

3. Fill in the basic task information and enter the task name, for example: emr_serverless_spark_task. Then, choose the target folder where the task will be stored. Click the **Confirm** button to complete task creation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">In the Project Console management interface, if you add or modify an engine, you must refresh the entire DataLeap Data Development interface in the Data Development task creation window to view the newly added or modified engine task types.</div>


2. <div data-tips="true" data-tips-type="warning">Task name may only contain the following characters: periods（.）, letters, numbers, underscore, hyphens, [], 【】, （）, (), and Chinese characters, and must not exceed 127 characters.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/858ff30decf749bd9042183907bd6c18~tplv-goo7wpa0wc-image.image) </span>

<span id="be910b8e"></span>
## 5 Task configuration description

After creating a new task, you can configure the following parameters in the task configuration interface.

<span id="e5d201f8"></span>
### **5.1 Language settings**

Language type supports Java and Python.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Conversion between language types is not supported yet; switching the language type will clear the current configuration, so please switch with caution.</div>


<span id="430039ed"></span>
### **5.2 Import resources**

For tasks with different language types, the method for importing resources varies.


|Language type |Description |
|---|---|
|JAVA |When the language type is set to Java, the following two methods for importing resources are supported:<br><br><br>* Project resources: You can select existing Jar resources from the Resources Library using a dropdown menu. If you have not yet created a Jar Resource for the EMR Serverless Spark Engine, you can click the **New Resource** button to go to the Resources Library to create one. See details [Resources Library](https://docs.byteplus.com/docs/undefined/682aa9fee638492ec7c94266).<br><br>* TOS method: This method will directly use the resource package that has already been uploaded to TOS. You can directly input the path information of the resource that has already been uploaded to TOS. For example: tos://test\-tos/emr\-spark/tos\-jar/spark\-examples\-2.3.4.jar. For details about the file upload action in TOS, see [File upload](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).<br><br><br>If the task also requires other resource packages, you can add the required dependency package information under **Dependency packages**.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa9b17901090487db3e3692a84f416d2~tplv-goo7wpa0wc-image.image) </span> |
|Python |When Language type is set to Python, Resource Type defaults to Python type. You can input Python statements in the editor below. If your statement depends on other Python files or needs to reference other custom JAR packages, you need to, in the editor, add the following command:<br><br>```Python```<br>```set las.spark.jar.depend.pyFiles=[{"fileName":"tos://xx.zip"}, {"fileName":"tos://xx.py"}]```<br><br><br>For more advanced usage, please refer to [PySpark Development Guide](https://docs.byteplus.com/en/docs/E-MapReduce/ServerlessP_Best_Practices_for_Serverless_PySpark_Development).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Currently, only Python 3.7 is supported as the Python execution engine version in DataLeap.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you need to set system environment variables in a statement, please avoid directly overwriting them. Please specify the variable by appending to the existing value, for example <code>PATH=$PATH:/home/lihua/apps/bin/</code>;</div><br> |


<span id="aa464452"></span>
### **5.3 Parameter configuration**


|Parameters |Note |
|---|---|
|Spark parameters ||
|Main Class |When you choose Java as the language type, you need to fill in the main class information, for example, org.apache.spark.examples.JavaSparkPi. |
|Conf parameters |Commonly used Spark configuration parameters in configurable tasks include the driver memory allocation parameter`spark.driver.memory`, the driver CPU cores parameter`spark.driver.cores`, and more. More parameters can be found at:[https://spark.apache.org/docs/latest/configuration.html](https://spark.apache.org/docs/latest/configuration.html)<br><br>You can use the following two methods to configure:<br><br><br>* Single line edit mode: Enter the key\-value pairs for the parameters in the corresponding text box.<br><br>* Script edit mode: JSON and YAML formats are supported, allowing configuration parameters to be set directly using scripts.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b88b84b5f99a4c71abe17bc9c255846e~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When an EMR Serverless Spark Java or Python task accesses TOS resources, TOS authentication is required. See <a href="https://docs.byteplus.com/en/docs/tos/docs-permission-configuration-guide">TOS permission configuration</a> for details. Therefore, you must add the AK/SK information of the account that has permission to access the TOS storage bucket to the Conf Parameters. For specific information, you can log in to BytePlus, go to the Console, open the <a href="https://console.byteplus.com/iam/keymanage">Access Key Management interface</a>, and copy the Access Key ID and Secret Access Key information. If you are a sub\-user, please contact the main account to obtain the key.</div><br><br><br><div data-tips="true" data-tips-type="warning">An example of how to fill in using the single line edit mode is as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">serverless.spark.access.key: xxxxxxx</div><br><br><br>* <div data-tips="true" data-tips-type="warning">serverless.spark.secret.key: xxxxxxx</div><br><br><br><br><div data-tips="true" data-tips-type="warning">You can configure encryption for sensitive information such as AK/SK keys using custom project parameters. For value configuration, use placeholders such as {{AK}} and {{SK}}. For details on the specific encryption operation, see <a href="https://docs.byteplus.com/docs/dataleap/parameter_information_setting">Parameter Information Settings</a>.</div><br> |
|Task Parameters ||
|Custom parameters |Additional parameters that need to be passed in the input task, such as data input/output path parameters, business time parameters for data processing, filter condition parameters, and so on.<br><br>Multiple parameters are separated by spaces, for example, param1 param2 param3. The parameters will ultimately be passed in as a string. You can configure time parameters using formats such as "${DATE}" and "${HOUR}". Other upstream task input parameters or project parameters are in formats such as {{param1}}.<br><br><br>* See details about time parameters [Description of platform time variables and constants](https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252)<br><br>* For details on input from upstream tasks and how to use project parameters, see [Input and Output Parameter Settings](https://docs.byteplus.com/docs/dataleap/input_and_output_parameter_settings). |


<span id="ee5b5875"></span>
### 5.4 **Register the data produced by the task**

Register task output data to record information about the task and its data lineage. This does not affect code logic.

If an EMR Serverless Spark Java or Python task outputs LAS Catalog database and table data, it is strongly recommended to manually register the task output data table information here. This facilitates subsequent maintenance of task data lineage and also enables downstream tasks to add upstream dependencies using the table name information.

The information you manually enter constitutes the task output table. You can fill in multiple tables. When other downstream tasks depend on the output data tables of this task, you can add the EMR Serverless Spark Java/Python task database/table name information set here as a dependency item in the downstream task's **scheduling dependencies**, either by using **dependency recommendations** or **adding manually**. The specific registration content includes the following data types:


* EMR Serverless Spark: This task will write data to a LAS Catalog table. You need to fill in the LAS Catalog data directory, database name, table name, and partition name. You can use variables for the partition content, for example, in the form of ${date} or ${hour}.

* Other: This task logic does not write data to the LAS Catalog table.


<span id="d778d134"></span>
## 6 Schedule settings

After completing the task configuration, click the **Scheduling Configuration** button in the right navigation bar to enter the scheduling configuration window. Here, you can set **scheduling properties, dependencies, task input and output parameters** and other information. For detailed parameter settings, see [Schedule Settings](https://docs.byteplus.com/en/docs/dataleap/scheduling_settings).

When selecting in **Scheduling Basic Info \> Compute Queue**, you can choose from the dropdown the Spark queue types that have already been bound in the Project Console to execute EMR Serverless Spark Java or Python tasks.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To execute tasks, select a queue with sufficient resident resource capacity in the <strong>Default calculation group</strong>. EMR Serverless Spark Java/Python tasks do not support using the assigned resource capacity of Spark SQL or Presto SQL calculation groups; task execution will result in an exception.</div>


<div data-tips="true" data-tips-type="warning">If the selected Spark Queue contains some <strong>SQL calculation group</strong> resources, you need to add the following parameter to the Spark Conf parameters above: tqs.query.engine.type = sparkcli, so that it will run on the residual <strong>Default Resident</strong> resources.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3b9b04a3e714b6cb958c275c3c89156~tplv-goo7wpa0wc-image.image" width="2044px" /></div>


For more actions on compute queues, see [Queue management](https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_Queue_management).

<span id="48f1d493"></span>
## 7 Debug and run, then submit

After the task configuration is complete, you can click the **Save** and **Debug** buttons in the Action bar to perform task debugging. For details on debug record actions, see [7 Debug](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_sql#bd996a75).

After confirming that the Debug Results are correct, click the **Commit for Deploy** button. In the **Commit for Deploy** dialog box, select parameters such as **Backfill data, Monitor Settings, Commit settings**. Finally, click the **Confirm** button to complete the job submission. see [4 Commit for Deploy](https://docs.byteplus.com/docs/dataleap/data-development-overview#_5-%E6%8F%90%E4%BA%A4%E4%B8%8A%E7%BA%BF).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Debug operation. Directly use online data for debugging. Caution.</div>


* <div data-tips="true" data-tips-type="warning">This task type does not currently support sending message notifications after debug execution succeeds or fails.</div>


* <div data-tips="true" data-tips-type="warning">Debug log data in the Data Development interface is retained for 15 days. You can view the corresponding debug log details within this period.</div>


* <div data-tips="true" data-tips-type="warning">If the tenant main account or project administrator has enabled pipeline process validation in the <strong>Project Console\>Pipeline Management</strong>, you need to ensure that the submitted task meets the validation rules of the pipeline extension in order to submit it successfully. See details <a href="https://docs.byteplus.com/docs/dataleap/data-development-overview#_4-%E6%B5%81%E6%B0%B4%E7%BA%BF%E7%AE%A1%E7%90%86">3 Pipeline Management</a>.</div>



See details of subsequent task operations and actions: [Task Operation](https://docs.byteplus.com/docs/dataleap/task_operation).

<span id="ba62a01b"></span>
## 8 Examples

<span id="d21c102c"></span>
### 8.1 Example of estimating pi

<span id="0cb84c13"></span>
#### 8.1.1 Task configuration

The following example demonstrates how to estimate pi by executing a Python script using the Python language in an EMR Serverless Spark Python task.


1. Create **EMR Serverless Spark Java/Python task**. See details above [4 Create a task](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_java_and_python#6e856aa7).

2. Enter the task configuration interface, select Language type as **Python**, and select Import resource type as **Python**.

3. In the code editing area, edit the following Python statements:

   ```python
   import sys
   from random import random
   from operator import add
   from pyspark.sql import SparkSession
   
   if __name__ == "__main__":
       """
           Usage: pi [partitions]
       """
       spark = SparkSession\
           .builder\
           .appName("PythonPi")\
           .getOrCreate()
   
       partitions = int(sys.argv[1]) if len(sys.argv) > 1 else 2
       n = 100000 * partitions
   
       def f(_: int) -> float:
           x = random() * 2 - 1
           y = random() * 2 - 1
           return 1 if x ** 2 + y ** 2 <= 1 else 0
   
       count = spark.sparkContext.parallelize(range(1, n + 1), partitions).map(f).reduce(add)
       print("Pi is roughly %f" % (4.0 * count / n))
   
       spark.stop()
   ```
   

4. After you have finished editing the Python script, you also need to add the following Conf parameters for TOS authentication:

   * serverless.spark.access.key: xxxxxxx

   * serverless.spark.secret.key: xxxxxxx


<span id="730ba217"></span>
#### 8.1.2 Debug

After the task configuration is complete, you can click the **Save** and **Debug** buttons in the action bar to perform task debugging.

<span id="7d2b8920"></span>
#### 8.1.3 View log output results


1. After the task has been executed successfully, you can go to the **Debug records\-Overview** page and click the Tracking URL log link to enter the Spark log interface.

2. In the Spark Log interface, click the **Executors** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fbb0b8300ed4304a154ddf474683203~tplv-goo7wpa0wc-image.image) </span>

3. In the **Logs** column, click the **stdout** button to view the task execution result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28abea04cf8f47ad87e85b479caaf2a0~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60cbe742802543a2a8341239450e75ff~tplv-goo7wpa0wc-image.image) </span>


<span id="57e3c30b"></span>
### 8.2 LAS Catalog metadata query example

<span id="bf88f8d5"></span>
#### 8.2.1 Task configuration

This example demonstrates how to use Python in an EMR Serverless Spark Python task to execute a PySpark script for accessing metadata in the LAS Catalog.


1. Create **an EMR Serverless Spark Java/Python task** See details above[3 新建任务](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_java_and_python#6e856aa7).

2. Go to the task configuration interface. For Language type, choose **Python**. For the resource type under Import resources, choose **Python**.

3. In the code editing area, edit the following Python statements:

   ```python
   from pyspark.sql import SparkSession
   
   # Create a SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   df1 = spark.sql("insert into database.table_name partition (date='${date}') values(1,'testa',26),(2,'json',3345343)(2,'TOM',10)")
   df2 = spark.sql("select * from database.table_name where date='${date}';")
   df2.show()
   
   spark.stop()
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the SQL statement in the Python example script above, you need to replace it with your own SQL statement, modify it according to the actual scenario, and then execute it.   </div>
   

4. When accessing LAS Catalog metadata resources in TOS using this method, after you have finished editing the Python script, you also need to add the following Conf parameters to authenticate through TOS:

   * serverless.spark.access.key: xxxxxxx

   * serverless.spark.secret.key: xxxxxxx

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e907dc9de426436d82770ec2146a5547~tplv-goo7wpa0wc-image.image) </span>

      For a description of the conf parameters, see [5.3 Parameter configuration](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_java_and_python#aa464452).


<span id="47e2ce2e"></span>
#### 8.2.2 Run in debug mode

After the task configuration is complete, you can click the **Save** and **Debug** buttons in the action bar to debug the task.

<span id="e6783fd7"></span>
#### 8.2.3 View log output results


1. After the task execution is successful, you can go to the **Debug records \- Overview** interface and click the Tracking URL log link to access the Spark log interface.

2. In the Spark Log interface, click the **Executors** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e729d3e56e4544e78f1364031323701e~tplv-goo7wpa0wc-image.image) </span>

3. In the **Logs** column, click the **stdout** button to enter and view the task execution result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28abea04cf8f47ad87e85b479caaf2a0~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbc8e54cef75465489d0c8f6d6339486~tplv-goo7wpa0wc-image.image) </span>
