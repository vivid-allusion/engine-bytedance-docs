---
title: "Spark-submit tool usage instructions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Spark-submit_tool_usage_instructions"
---

<span id="3358caba"></span>
## Environment requirements

JDK8 / JDK17 must be installed locally, and the JAVA_HOME environment variable must be set.

```Bash
echo $JAVA_HOME #Query JAVA_HOME directory location
java -version #Check version
```


<span id="90ded9ae"></span>
## Install the toolkit


1. Click the attachment link below to download the toolkit.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55b1bc6e017b431483013d576b4329b5~tplv-goo7wpa0wc-image.image" name="emr.spark.serverless_spark_submit_1.0.0.53.tar.gz">emr.spark.serverless_spark_submit_1.0.0.53.tar.gz</Attachment>
   

2. Run the following command to extract the toolkit to the specified local directory.


```Bash
cd /工具包路径/
tar -xzf emr.spark.serverless_spark_submit_{version}.tar.gz
```


The file directory structure is as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/527622d9f3504c6bbe214c57881108eb~tplv-goo7wpa0wc-image.image) </span>


3. Configure environment variables.


```Bash
export SPARK_HOME=/工具包路径/
export PATH=$SPARK_HOME/bin:$PATH
```



4. Check whether the command installation is successful.


```Bash
spark-submit --help
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7d006d7e4bf409f87a5f19695ba179d~tplv-goo7wpa0wc-image.image) </span>

<span id="d6d4428f"></span>
## Configure related parameters

Before submitting, modify the following parameters in the spark\-defaults.conf file under the conf folder as appropriate:

```Properties
spark.app.name=serverless-spark-jar   #修改为您的的作业名称，也可在命令行提交时指定
serverless.spark.region=cn-beijing    #修改为您需要访问的Serverless Spark产品Region
serverless.spark.endpoint=https://open.volcengineapi.com   #固定值，暂无需修改
serverless.spark.service=emr_serverless   #固定值，暂无需修改
serverless.spark.access.key=YOUR_ACCESS_KEY   #修改为您的账号Access Key
serverless.spark.secret.key=YOUR_SECRET_KEY   #修改为您的账号Secret Key
serverless.spark.tos.bucket=YOUR_TOS_BECKET_NAME   #修改为您的TOS桶名，请确保您的AK/SK对此TOS桶有访问权限，该桶将被用于上传本地jar等依赖文件，这些文件会在Spark运行时被加载。
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Note</strong></div>


<div data-tips="true" data-tips-type="tip">In the file, <code>#</code> and everything after it are comments. After modifying the parameters, users need to delete these comments.</div>


<span id="877ec83b"></span>
## Submit a Spark Jar job

Use the `spark-submit` command to submit a Spark Jar sample job. A minimal submission example is as follows (with the above parameters configured).

```Bash
spark-submit --class com.volcengine.emr.serverless.demo.ServerlessSparkDemo lib/serverless-spark-submit-example-1.0.0.jar
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The serverless\-spark\-submit\-example\-1.0.0.jar file in the example is located in the lib directory after extracting the toolkit.</div>


<span id="599223bc"></span>
### Example 1: Submit a local Jar package job

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Parameters specified on the command line have higher priority. When both are configured, the parameters in the spark\-defaults.conf file will be overridden.</div>


```Bash
spark-submit --name ServerlessJarDemo --async --jars /path/to/dependency1.jar --region cn-beijing --access-key-id your-access-key --access-key-secret your-secret-key --tos-bucket your-tos-bucket --class your-main-class /path/to/primary-dependency.jar arg1 arg2
```


<span id="b8d2bbe1"></span>
### Example 2: Submit a TOS Jar package job

```Bash
spark-submit --name ServerlessJarDemo --async --jars tos://your-bucket/dependency1.jar --region cn-beijing --access-key-id your-access-key --access-key-secret your-secret-key --class your-main-class tos://your-bucket/primary-dependency.jar arg1 arg2
```


<span id="a46ac93d"></span>
## Submit a Spark SQL job

The `spark-sql` command can be used to submit SQL jobs. It supports submitting SQL text stored in a TOS bucket, stored on the local system, or entered from the command line. See the examples below for details.

<span id="7cff898e"></span>
### Example 1: Use the "\-f" parameter to submit an SQL file located in a TOS bucket

```SQL
spark-sql -f tos://your-bucket/path/to/query.sql
```


<span id="9e07bfde"></span>
### Example 2: Use the "\-f" parameter to submit an SQL file located locally

```SQL
spark-sql -f /path/to/query.sql
```


<span id="fd412bcf"></span>
### Example 3: Use the "\-e" parameter to submit SQL text entered from the command line

```SQL
spark-sql -e "select 1"
```


<span id="7b130b83"></span>
## Parameter description

<span id="3b6c8f27"></span>
### Command line parameter description

The specific descriptions of the command line parameters are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can configure global job parameters in the toolkit's spark\-defaults.conf, or specify parameters explicitly via command line arguments when submitting a job. In this case, the parameters set are job\-level parameters and take precedence over the configuration in spark\-defaults.conf.</div>


* <div data-tips="true" data-tips-type="tip">If the "Required" field for the corresponding parameter is "Yes", then a value in either spark\-defaults.conf or the command line parameter is sufficient.</div>




|Command line parameter name |Corresponding spark\-defaults.conf parameter value |Required |Default value |Note |
|---|---|---|---|---|
|\-\-name |spark.app.name |Yes |None |Task name |
|\-\-class |tqs.spark.jar.class |No |None |The main class for task execution. If not specified, the Main Class will be attempted to be retrieved from the jar package. |
|\-\-region |serverless.spark.region |Yes |None |The Volcano Engine region where the Serverless Spark task is executed.<br><br><br>* North China: cn\-beijing<br><br>* East China: cn\-shanghai<br><br>* South China: cn\-guangzhou<br><br>* Johor: ap\-southeast\-1<br><br>* Autonomous Driving Cloud: cn\-beijing\-selfdrive |
|\-\-access\-key\-id |serverless.spark.access.key |Yes |None |Your account Access Key |
|\-\-access\-key\-secret |serverless.spark.secret.key |Yes |None |Your account Secret Key |
|\-\-session\-token |serverless.spark.session.token |No |None |In the Assume Role scenario, you need to provide the session token. |
|\-\-tos\-bucket |serverless.spark.tos.bucket |No |None |Specify a TOS bucket to upload your local jar files to this bucket. When the Spark task starts, it will load the jar files from this TOS bucket. If your files already exist in the TOS bucket, this parameter can be omitted. |
|\-\-tos\-endpoint |serverless.spark.tos.endpoint |No |None |Specify the TOS endpoint address. When accessing the TOS bucket via the internal network of Volcano Engine, you can configure it as the internal endpoint of TOS. For example, for North China, you can configure it as tos\-cn\-beijing.ivolces.com |
|\-\-conf |None |No |None |Spark runtime parameters. For reference, see: [Spark configuration official documentation](https://spark.apache.org/docs/latest/configuration.html) |
|\-\-properties\-file |spark.properties |No |$SPARK_HOME/conf/spark\-defaults.conf |The path to the Spark configuration file. The default is $SPARK_HOME/conf/spark\-defaults.conf, which is conf/spark\-defaults.conf under the installation package location mentioned above. |
|\-\-driver\-cores |spark.driver.cores |No |4 |Number of driver cores |
|\-\-driver\-memory |spark.driver.memory |No |16g |Driver memory size |
|\-\-driver\-java\-options |spark.driver.extraJavaOptions |No |None |Driver JVM parameters |
|\-\-driver\-class\-path |spark.driver.extraClassPath |No |None |Additional class path for the driver |
|\-\-print\-driver\-log |None |No |None |Whether to print the execution log of the driver. Optional values:<br><br><br>* stderr: Standard error output<br><br>* stdout: Standard output |
|\-\-executor\-memory |spark.executor.memory |No |16g |Executor memory size |
|\-\-executor\-cores |spark.executor.cores |No |4 |Number of executor cores |
|\-\-num\-executors |spark.executor.instances |No |1 |Number of executors |
|\-\-queue |spark.queue |No |None |Name of the queue in which the task runs |
|\-\-async |None |No |None |If specified, the spark\-submit command will exit after the task is successfully submitted and will not wait for the task to complete. |
|\-\-jars |spark.jars |No |None |Comma\-separated jar file paths. These jar files will be loaded at Spark runtime. Both local files and TOS files are supported. |
|\-\-archives |spark.archives |No |None |Comma\-separated archive files, which will be loaded into the working directory at Spark runtime. Both local files and TOS files are supported. |
|\-\-files |spark.files |No |None |Comma\-separated other files, which will be loaded into the working directory at Spark runtime. Both local files and TOS files are supported. |
|\-\-kill\-job\-on\-signal |serverless.spark.kill.job.on.signal |No |None |After specifying this parameter, if the spark\-submit process is killed or the running terminal receives a SIGINT (Ctrl+C) signal, the submitted EMR Serverless Spark job will also be terminated synchronously. |
|\-f |None |No |None |The SQL file location accepted by the spark\-sql command. You can specify an SQL file in a TOS bucket or a local SQL file. |
|\-e |None |No |None |The SQL text accepted by the spark\-sql command. |
|\-\-skip\-print\-result |None |No |None |Specifies whether the spark\-sql command skips printing results. |


<span id="91c7a3b5"></span>
### Common resource parameters


|Parameter type |Parameter key |Note |Default value |
|---|---|---|---|
|**Driver related** |`spark.driver.memory` |Driver heap memory size |12g |
||`spark.driver.memoryOverhead` |Driver off\-heap memory size |4g |
||`spark.driver.cores` |Number of CPU cores for the Driver program |4 |
||`spark.driver.maxResultSize` |Maximum size of the result returned by the Driver |3g |
|**Executor related** |`spark.executor.cores` |Number of CPU cores for each Executor |4 |
||`spark.executor.memory` |Memory size for each Executor |12g |
||`spark.executor.memoryOverhead` |Off\-heap memory size for each Executor |4g |
||`spark.executor.instances` |Number of Executor instances (if dynamic allocation is enabled by default, this parameter does not need to be set) |1 |
|**Dynamic allocation settings** |`spark.dynamicAllocation.enabled` |Enable dynamic allocation |true |
||`spark.dynamicAllocation.minExecutors` |Minimum number of Executors |1 |
||`spark.dynamicAllocation.maxExecutors` |Maximum number of Executors |30 |
|**File read parallelism** |`spark.sql.files.maxPartitionBytes` |File size for each Map task |268435456 |
||`spark.sql.shuffle.partitions` |Number of partitions generated during Shuffle operations |200 |
|**AQE** |`spark.sql.adaptive.enabled` |Adaptive execution switch, includes automatic adjustment of parallelism and optimizations for resolving data skew |true |
||`spark.sql.adaptive.maxNumPostShufflePartitions` |Maximum number of post\-shuffle partitions. For tasks with large shuffle volumes, increasing this value can reduce the amount of data processed by each task. For example, 1024. |500 |
||`spark.sql.adaptive.minNumPostShufflePartitions` |Lower limit for the number of shuffle partitions dynamically adjusted by AQE. |5 |
