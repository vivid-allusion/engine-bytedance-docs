---
title: "Use the Task Plugin"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ds_use_task_plugin_task_plugin"
---

<span id="0ae52106"></span>
# Note

Based on **dolphnscheduler 3.1.9**, the Volcano Engine EMR product provides the VolcanoEMRServerless task plugin, which supports submitting the following types of Serverless tasks: SQL, Spark Jar, and PySpark, making it easy to connect to EMR Serverless.

<span id="25ff60f3"></span>
# Dolphin installation and deployment

<span id="b226a955"></span>
## Download serverless\-plugin plugin

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/456aca983c304c28bf7721685e34b524~tplv-goo7wpa0wc-image.image" name="serverless-plugin.zip">serverless-plugin.zip</Attachment>


&nbsp;

<span id="29e84d4e"></span>
## Update Dolphin master\-server

```Shell
# 替换为上述下载包
unzip serverless-plugin.zip

# 替换为实际dolphin用户目录
chown -R dolphinscheduler:dolphinscheduler serverless-plugin
# 替换为实际的dolphin_scheduler master-server路径
cp -rp serverless-plugin/. /usr/lib/emr/current/dolphin_scheduler/master-server/libs
```


<span id="a442e2ca"></span>
## Update Dolphin worker\-server

```Shell
# 替换为上述下载包
unzip serverless-plugin.zip

# 替换为实际dolphin用户目录
chown -R dolphinscheduler:dolphinscheduler serverless-plugin

# 替换为实际的dolphin_scheduler worker-server路径
cp -rp serverless-plugin/. /usr/lib/emr/current/dolphin_scheduler/worker-server/libs
```


<span id="b73e82fe"></span>
## Update Dolphin api\-server

```Shell
# 下载包
unzip serverless-plugin.zip

# 替换为实际dolphin用户目录
chown -R dolphinscheduler:dolphinscheduler serverless-plugin

# 替换为实际的dolphin_scheduler api-server路径
cp -rp serverless-plugin/. /usr/lib/emr/current/dolphin_scheduler/api-server/libs

# 先对原始 ui 产物做备份
mv /usr/lib/emr/current/dolphin_scheduler/api-server/ui /usr/lib/emr/current/dolphin_scheduler/api-server/ui-bak
# 放入 serverless 提供的 ui
mv serverless-plugin/ui /usr/lib/emr/current/dolphin_scheduler/api-server/ui
```


<span id="f0a514b1"></span>
# Submit EMR Serverless task

On the DolphinScheduler service page, click "Service Link" to enter the DolphinScheduler console page. After completing the installation and deployment of the above task plugin, you can refer to the following steps to submit an EMR Serverless task.

<span id="cf6f9803"></span>
## Initialization: Create a data source

Before submitting an EMR Serverless data source, you need to create a data source first, and set the runtime queue, task submission address, authentication, and other information for subsequent Serverless tasks. The entry point and key parameters are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b972170dab342269571578da79afdf3~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Note |
|---|---|
|Data source |Select: `VOLCANO_EMR_SERVERLESS` |
|Data source name |Customize the data source name. |
|Region |Select the region where you want to submit tasks.<br><br><br>* Beijing: `cn-beijing`<br><br>* East China: `cn-shanghai`<br><br>* South China: `cn-guangzhou`<br><br>* Johor: `ap-southeast-1` |
|Endpoint |* For settings, see [Service address](https://docs.byteplus.com/docs/E-MapReduce/Service_address_ecs) |
|Queue name |Set to the name of the EMR Serverless queue. Subsequent Serverless tasks will run on this queue, so you must ensure that the queue set here is an available running queue. |
|Access key AK & secret key SK |Set to the AK and SK of your Volcano Engine account. |


After the data source is created, you can refer to the following to submit various types of Serverless tasks.

<span id="109e81f6"></span>
## Submit SparkSQL task

The following describes the entry point and main parameters for submitting a SparkSQL task.


1. In Project Management \> Workflow \> Workflow Definition, create a workflow and select the "**VolcanoEMRServerless**" task node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c9219fb2c594ada9ae743a4591e3735~tplv-goo7wpa0wc-image.image) </span>

2. Configure SparkSQL task details on the pop\-up task node configuration page.

   
   |Parameters |Note |
   |---|---|
   |Node name |Customize the task node name. |
   |Data source type & data source instance |* Select "**VOLCANO_EMR_SERVERLESS**" as the data source type.<br><br>* Select the data source instance created in the previous steps. |
   |Task name & task type |* Customize the task name.<br><br>* Select the task type "SparkSQL". |
   |Spark SQL |Enter the SparkSQL task code. |
   |Compute group name |Configure the name of an available (running) compute group in the EMR Serverless queue specified by the above\-configured data source instance.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd862e22c88f45f09a82af6d2f50621e~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="be50e2b8"></span>
## Submit SparkJar task

<span id="4a1790fe"></span>
### Preparation: Prepare task resource files

When submitting a SparkJar task, you need to upload the task code file to Volcano Engine Object Storage TOS in the same region as the Serverless queue, and obtain the TOS address of the corresponding code file.

<span id="f5177c42"></span>
### Submit task

The following describes the entry point and main parameters for submitting a SparkJar task.


1. In Project Management \> Workflow \> Workflow Definition, create a workflow and select the "**VolcanoEMRServerless**" task node.

2. Configure SparkJar task details on the pop\-up task node configuration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1103eb5403cf47ca85d20ae8f2c8d017~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Node name |Customize the task node name. |
   |Data source type & data source instance |* Select "**VOLCANO_EMR_SERVERLESS**" as the data source type.<br><br>* Select the data source instance created in the previous steps. |
   |Task name & task type |* Customize the task name.<br><br>* Select the task type "SparkJar". |
   |Main application file path |Configure the TOS path address for the task code file in Preparation. |
   |Main function class |Configure as the main function class in the task code file. |
   |Compute group name |Configure the name of an available (running) compute group in the EMR Serverless queue specified by the above\-configured data source instance.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd862e22c88f45f09a82af6d2f50621e~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="e493d3cd"></span>
## Submit PySpark task

<span id="6d6c078e"></span>
### Preparation: Prepare task resource files

When submitting a SparkJar task, you need to upload the task code file to Volcano Engine Object Storage TOS in the same region as the Serverless queue, and obtain the TOS address of the corresponding code file.

After completing the preparation, the following describes the entry point and main parameters for submitting a PySpark task in various typical task scenarios.

<span id="bdfc7970"></span>
### Task scenario 1: Submit a task by accessing TOS


* Main program: Upload the main program file of the task code to TOS

   The following is a task code sample.

   ```Python
   import argparse
   from pyspark.sql import SparkSession
   from pyspark import SparkFiles
   
   # Create a SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   parser = argparse.ArgumentParser(description='这是一个示例程序')
   parser.add_argument('--inputFile', help='输入文件')
   parser.add_argument('--outputFile', help='输出文件')
   args = parser.parse_args()
   inputFile = args.inputFile
   outputFile = args.outputFile
   # Print parameter values
   print('输入文件:', inputFile)
   print('输出文件:', outputFile)
   
   file_df = spark.sparkContext.textFile(inputFile)
   file_df_data = file_df.collect()
   
   SparkFiles.get(inputFile)
   print("inputFile data:")
   for line in file_df_data:
       print(line)
   
   # Create sample data
   data = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]
   df = spark.createDataFrame(data, ["Name", "Age"])
   # Save DataFrame as CSV file
   df.write.csv(outputFile, 'overwrite')
   
   spark.stop()
   ```
   

* Job submission parameters

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c31e88dc633344c4b64c395aabad6447~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Node name |Customize the task node name. |
   |Data source type & data source instance |* Select "**VOLCANO_EMR_SERVERLESS**" as the data source type.<br><br>* Select the data source instance created in the previous steps. |
   |Task name & task type |* Customize the task name.<br><br>* Select "PySpark" as the task type. |
   |Main application file path |Configure the TOS path address for the task code file in Preparation. |
   |Compute group name |Configure the name of an available (running) compute group in the EMR Serverless queue specified by the above\-configured data source instance.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd862e22c88f45f09a82af6d2f50621e~tplv-goo7wpa0wc-image.image) </span> |
   |Configuration parameters |Configure as the TOS path for input and output data when processing data in subsequent PySpark tasks.<br><br>For example: `--inputFile;tos://lei-hns/demo/data/data_01.csv;--outputFile;tos://lei-hns/demo/data/data_output.csv` |
   


<span id="9ad54dd8"></span>
### Task scenario 2: Depend on a custom Jar

When the task depends on a custom JAR, refer to the following for task configuration.


* Main program: Upload to TOS

   The following is a task code sample.

   ```Python
   from pyspark.sql import SparkSession
   
   # Create a SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   print("demo: ")
   spark.sql("select 1").show()
   
   spark.stop()
   ```
   

* Job submission parameters

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88cab3056dbc4866b768fc16d746b241~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Node name |Customize the task node name. |
   |Data source type & data source instance |* Select "**VOLCANO_EMR_SERVERLESS**" as the data source type.<br><br>* Select the data source instance created in the previous steps. |
   |Task name & task type |* Customize the task name.<br><br>* Select "PySpark" as the task type. |
   |Main application file path |Configure the TOS path address for the task code file in Preparation. |
   |Compute group name |Configure the name of an available (running) compute group in the EMR Serverless queue specified by the above\-configured data source instance.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd862e22c88f45f09a82af6d2f50621e~tplv-goo7wpa0wc-image.image) </span> |
   |Dependent Jar file |Configure the TOS path where the dependent Jar file is located.<br><br>For example: `tos://doctest/serverless/spark/pyspark/spark-jar-demo.jar` |
   


<span id="c94782bd"></span>
### Task scenario 3: Depend on a custom image


* Main program: Upload to TOS

   ```Python
   from pyspark.sql import SparkSession
   
   # Create a SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   print("demo: ")
   spark.sql("select 1").show()
   
   spark.stop()
   ```
   

* Job submission parameters

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8700eae25f704f2c828c27bf0898aa0a~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Node name |Customize the task node name. |
   |Data source type & data source instance |* Select "**VOLCANO_EMR_SERVERLESS**" as the data source type.<br><br>* Select the data source instance created in the previous steps. |
   |Task name & task type |* Customize the task name.<br><br>* Select "PySpark" as the task type. |
   |Main application file path |Configure the TOS path address for the task code file in Preparation. |
   |Compute group name |Configure the name of an available (running) compute group in the EMR Serverless queue specified by the above\-configured data source instance.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd862e22c88f45f09a82af6d2f50621e~tplv-goo7wpa0wc-image.image) </span> |
   |Configuration parameters |Configure the custom image value according to the following format requirements.<br><br>`spark.kubernetes.container.image=actual image value` |
   


<span id="7b384355"></span>
### Task scenario 4: Depend on a custom Module


* Main program: Upload to TOS

   ```Python
   import time
   
   from pyspark.sql import SparkSession
   from pyspark.sql.functions import udf
   from pyspark.sql.types import FloatType
   
   from basic_statistics.file_info import getFile1
   from basic_statistics.file_info import get_all_files
   from tools import func
   from module1 import my_module1
   from module2 import my_module2
   
   # Create a SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   get_all_files("./")
   getFile1("/")
   
   taxCut = udf(lambda salary: func.tax(salary), FloatType())
   
   staff_data = [
       {"name": "Alice", "salary": 70000},
       {"name": "Bob", "salary": 60000},
       {"name": "Charlie", "salary": 50000},
       {"name": "David", "salary": 80000},
       {"name": "Eve", "salary": 75000},
       {"name": "Frank", "salary": 40000},
       {"name": "Grace", "salary": 95000},
       {"name": "Hannah", "salary": 30000},
   ]
   df = spark.createDataFrame(staff_data)
   
   taxCut = udf(lambda salary: func.tax(salary), FloatType())
   df.select("name", taxCut("salary").alias("final salary")).show()
   
   # Create DataFrame
   data = [(1,), (2,), (3,), (4,)]
   df = spark.createDataFrame(data, ["value"])
   
   # Use functions in the module
   result_multiply = df.rdd.map(lambda x: my_module1.multiply(x[0], 5)).collect()
   print("\n result_multiply is :", result_multiply)
   result_add = df.rdd.map(lambda x: my_module2.add(x[0], 10)).collect()
   print("\n result_add is :", result_add)
   
   spark.stop()
   ```
   

* Job submission parameters

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b29d5beb9f01473591827f8a8ecea9fe~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Node name |Customize the task node name. |
   |Data source type & data source instance |* Select "**VOLCANO_EMR_SERVERLESS**" as the data source type.<br><br>* Select the data source instance created in the previous steps. |
   |Task name & task type |* Customize the task name.<br><br>* Select "PySpark" as the task type. |
   |Main application file path |Configure the TOS path address for the task code file in Preparation. |
   |Compute group name |Configure the name of an available (running) compute group in the EMR Serverless queue specified by the above\-configured data source instance.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd862e22c88f45f09a82af6d2f50621e~tplv-goo7wpa0wc-image.image) </span> |
   |Configuration parameters |Configure the environment parameters and runtime parameter values for the task.<br><br>For example: `spark.executorEnv.PYTHONPATH=/opt/spark/work-dir/module1.zip:/opt/spark/work-dir/module2.zip:/opt/spark/work-dir/basic_statistics.zip:/opt/spark/work-dir/tools.zip;spark.driver.cores=2;spark.driver.maxResultSize=10g` |
   |Dependent Python files |Configure the TOS storage path address for the dependent Module files.<br><br>For example, `tos://lei-hns/demo/spark/python/basic_statistics.zip;tos://lei-hns/demo/spark/python/tools.zip;tos://lei-hns/demo/spark/python/module1.zip;tos://lei-hns/demo/spark/python/module2.zip;` |
   


<span id="6b463f37"></span>
### Task scenario 5: Depend on a custom Conda


* Main program: Upload to TOS

   ```Python
   from pyspark.sql import SparkSession
   import numpy as np
   
   # Create a SparkSession object
   spark = SparkSession.builder \
       .enableHiveSupport() \
       .getOrCreate()
   
   print("demo: ")
   spark.sql("select 1").show()
   
   x = np.linspace(0, 2 * np.pi, 100)
   y = np.sin(x)
   print("x is ", x)
   print("y is ", y)
   
   spark.stop()
   ```
   

* Job submission parameters

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d85b8626569c4238bcc9cfbdc1747e3c~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Node name |Customize the task node name. |
   |Data source type & data source instance |* Select "**VOLCANO_EMR_SERVERLESS**" as the data source type.<br><br>* Select the data source instance created in the previous steps. |
   |Task name & task type |* Customize the task name.<br><br>* Select "PySpark" as the task type. |
   |Main application file path |Configure the TOS path address for the task code file in Preparation. |
   |Compute group name |Configure the name of an available (running) compute group in the EMR Serverless queue specified by the above\-configured data source instance.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd862e22c88f45f09a82af6d2f50621e~tplv-goo7wpa0wc-image.image) </span> |
   |Configuration parameters |Configure the runtime parameter values for the task and the TOS path address for the dependent Conda file.<br><br>For example: `spark.unpackUseCommand.enabled=true;las.spark.jar.depend.archives=[{"fileName": "tos://lei-hns/demo/conda/python38_new.zip"}];spark.pyspark.python=python38_new.zip/python38_new/bin/python3;spark.pyspark.driver.python=python38_new.zip/python38_new/bin/python3;` |
   


<span id="db9ff997"></span>
# Advanced application practices

<span id="79a32db5"></span>
## Use user\-defined parameters

<span id="3f60ddf8"></span>
### Feature description


* Starting from version 3.20.0 of the EMR software stack, the EMR Serverless job plugin supports using user\-defined variable parameters when submitting Serverless tasks.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a95ccf764244aa98c0d9375e99766f2~tplv-goo7wpa0wc-image.image) </span>

   As shown in the figure above, you can add parameters as needed via "Custom parameters" when configuring task parameters.

* Caution: The current custom parameter feature does not support configuring parameters of the OUT type.

* Refer to the [Upgrade historical versions](https://docs.byteplus.com/docs/E-MapReduce/ds_use_task_plugin_task_plugin#5a283498) section below for upgrade instructions.


<span id="a80871e0"></span>
### Application example

The following is a simple workflow example demonstrating the use of custom parameters in upstream and downstream nodes.


* Example scenario

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9190aadd55e8416fb002c20ce2b26d9a~tplv-goo7wpa0wc-image.image) </span>

   In this scenario, it is currently supported to pass custom parameters from upstream task nodes to downstream SparkSQL task nodes. Passing custom parameters from SparkSQL task nodes to downstream task nodes is not supported.

* Task node configuration

   * Upstream shell task

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0605b9153e14d6da60b13031eed1a85~tplv-goo7wpa0wc-image.image) </span>

   * Intermediate Spark task

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4558adefd4cc4e4190833a7e2c495abd~tplv-goo7wpa0wc-image.image) </span>

   * Downstream shell task

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/436348058e654b9faf3238df3e07ecf7~tplv-goo7wpa0wc-image.image) </span>


<span id="5a283498"></span>
# Upgrade historical versions

Users of historical versions can refer to the following steps for configuration upgrade. After completing the upgrade, you can use the new features available in the corresponding version.

<span id="09bf0037"></span>
## Obtain the new JAR package

Obtain the new version of the JAR package and update DolphinScheduler.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de623e01bfd744a9a18ceb4cb4a8a1a7~tplv-goo7wpa0wc-image.image" name="update.tar.gz">update.tar.gz</Attachment>


&nbsp;

<span id="a95f4855"></span>
## Upgrade frontend assets

For frontend asset upgrades, replace the old version of the UI folder with the new version, and back up the old UI folder. UI folder address

On the node where the api\-server service is located, perform operations on the following directories.

```Shell
# 检查目录
/usr/lib/emr/current/dolphin_scheduler/api-server/ui
# 备份目录
mv /usr/lib/emr/current/dolphin_scheduler/api-server/ui /usr/lib/emr/current/dolphin_scheduler/api-server/ui-bak
# 更新目录
mv ${path_to_new_ui} /usr/lib/emr/current/dolphin_scheduler/api-server/ui
```


<span id="5bcac97b"></span>
## Upgrade Serverless SDK

The Serverless SDK is the tool that actually interacts with Serverless. The relevant dependency package is: **serverless\-sdk\-query.jar**. When updating the package, replace the corresponding package in the following paths:


1. In the directory on the node where the master\-server service is located, find the location of the serverless SDK JAR package and replace it.

   ```Shell
   # 查看
   /usr/lib/emr/current/dolphin_scheduler/master-server/libs | grep serverless-sdk
   ```
   

2. In the directory on the node where the api\-server service is located, find the location of the serverless SDK JAR package and replace it.

   ```Shell
   # 查看
   /usr/lib/emr/current/dolphin_scheduler/api-server/libs | grep serverless-sdk
   ```
   

3. In the directory on the node where the worker\-server service is located, find the location of the serverless SDK JAR package and replace it.

   ```Shell
   # 查看
   /usr/lib/emr/current/dolphin_scheduler/worker-server/libs | grep serverless-sdk
   ```
   


<span id="303375ba"></span>
## Upgrade plugins

Plugins are the tools that actually interact with DolphinScheduler. The relevant dependency packages are:


* **dolphinscheduler\-task\-volcanoemrserverless\-3.1.9.jar (task\-related configuration)** 

* **dolphinscheduler\-datasource\-volcanoemrserverless\-3.1.9.jar (data source\-related configuration)** 

* **dolphinscheduler\-spi\-3.1.9.jar (rarely changed)** 


When updating the package, replace the corresponding package in the following paths:


1. In the directory on the node where the master\-server service is located, find the package to be replaced and replace it.

   ```Shell
   # 查看
   /usr/lib/emr/current/dolphin_scheduler/master-server/libs | grep volcanoemr
   ```
   

2. In the directory on the node where the api\-server service is located, find the package to be replaced and replace it.

   ```Shell
   # 查看
   /usr/lib/emr/current/dolphin_scheduler/api-server/libs | grep volcanoemr
   ```
   

3. In the directory on the node where the worker\-server service is located, find the package to be replaced and replace it.

   ```Shell
   # 查看
   /usr/lib/emr/current/dolphin_scheduler/worker-server/libs | grep volcanoemr
   ```
   


<span id="b3d52be5"></span>
## Restart to apply the upgrade

After the upgrade, restart the corresponding DolphinScheduler components during off\-peak business hours to apply the upgrade. You only need to restart the components that have been changed.
