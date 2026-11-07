---
title: "PySpark jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/PySpark_job"
---

To meet users' personalized data query and analysis requirements, EMR Serverless Spark supports users in writing Python and submitting PySpark jobs.

# Prerequisites

* An EMR Serverless queue has been created, and you have Developer/Admin permissions for the compute group. For detailed instructions, refer to: [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue).

* A compute group has been created. PySpark jobs use the general compute group in the queue.

* The job file has been uploaded to the TOS bucket in the same region as the current Serverless queue.

* To use a runtime role to access cloud resources, you must create and configure a job runtime role and copy the complete role TRN. For detailed instructions, see [Runtime Roles](https://docs.byteplus.com/docs/undefined/6adb36d276430b031596a173).

# **Submit job**

## Submit job: via console

1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the top menu bar, select the region and project space from the dropdown menus according to your actual scenario.

3. Click Job center \> Job management or Job instance to enter the Create job page

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7c6b3ca8f50408099947bf93322a75c~tplv-goo7wpa0wc-image.image)

4. Configure the parameters for the PySpark job.

   1. Configure the job **basic information**. See the table below for parameter details.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8b5f173e9d84bca882fc78bbb1654a0~tplv-goo7wpa0wc-image.image)

      |**Parameter** |**Configuration operation** |
      |---|---|
      |Job Name |The name of this job. It cannot be changed after creation. |
      |Job types |The type of job to be created. |
      |Execution resources |The EMR resources used to execute the job, divided into resource type dropdown and queue/project dropdown.<br><br>You can select specific resources and search by name or ID. |
      |development model |* UI: Submit job content through the visual interface.<br><br>* JSON: Submit job content in JSON format, which is more suitable for batch configuration or reusing existing configurations. For example:<br><br>   ```JSON```<br>```   {```<br>```    "JobType": "PySpark",```<br>```    "ServerlessSparkRuntimeVersion": "spark4.1",```<br>```    "MainApplicationFile": "tos://<your-bucket>/<path>/your-script.py",```<br>```    "SparkConf": {```<br>```    "RuntimeRole": "trn:iam::{$AccountID}:role/{$RoleName}"```<br>```    "emr.execute.resource.type": "EMR_Serverless",```<br>```    "tqs.query.engine.type": "Spark"```<br>```    },```<br>```    "Jars": [```<br>```    "tos://<your-bucket>/<path>/extra-dependency.jar"```<br>```    ],```<br>```    "Files": [```<br>```    "tos://<your-bucket>/<path>/dependency-file"```<br>```    ],```<br>```    "PyFiles": [```<br>```    "tos://<your-bucket>/<path>/python-file"```<br>```    ],```<br>```    "Archives": [],```<br>```    "MainArguments": []```<br>```   }```<br>```   ```<br>    |

   2. Configure the **job content**. The parameter entry points differ depending on the development mode. For parameter details, refer to the table below.

      |**UI mode parameters** |**JSON mode parameters** |**Required** |**Note** |
      |---|---|---|---|
      |EngineRuntime |ServerlessSparkRuntimeVersion |Y |Select the Spark compute engine environment. You can choose the Spark version and the corresponding Java Runtime or Bolt Runtime.<br><br><br>* Java Runtime: Standard Java runtime.<br><br>* Bolt Runtime: BytePlusA proprietary native kernel acceleration engine that can improve the execution speed of Spark, Presto, and other jobs. For a detailed introduction, see [Spark on Native engine: Bolt](https://docs.byteplus.com/en/docs/E-MapReduce/sq_spark_on_native_engine).<br><br><br>> **注意**<br><br><br>> The EngineRuntime parameter of the job takes precedence over the default compute group and general compute group parameters.<br> |
      |Python file |MainApplicationFile |Y |The core code file of the job. When the platform starts the job, it will pull this file from TOS and execute the entry command.<br><br>You must upload them to TOS and specify the path here. |
      |Runtime role |RuntimeRole |N |The IAM identity used by the job to access cloud resources at runtime. For more information, see [Runtime Roles](https://docs.byteplus.com/docs/undefined/6adb36d276430b031596a173). |
      |Dependency Jar |Jars |N |Third\-party or custom JAR packages that the main task file depends on during execution. Executors will automatically load them when running the task.<br><br>You must upload them to TOS and specify the path here. |
      |Depend on Python resources |Files |N |Model files that the task file depends on during execution.<br><br>You must upload them to TOS and specify the path here. |
      |Depend on File resources |PyFiles |N |Resource files for the PySpark job.<br><br>You must upload them to TOS and specify the path here. |
      |Dependent archive |Archives |N |Archive dependencies for the PySpark job.<br><br>You must upload them to TOS and specify the path here. |
      |Spark parameters (spark conf) |SparkConf |N |Environment variables for Spark components. For example:<br><br><br>* `serverless.emr.access.key=AKL*****`<br><br>* `serverless.emr.secret.key=WkR*****`<br><br><br>> **注意**<br><br><br>> In UI mode, the EngineRuntime parameter is provided as an option. If the EngineRuntime parameter is submitted here, it will not take effect.<br> |
      |Custom parameters (main conf) |MainArguments |N |Input parameters required when running the main task of the PySpark job. |
      |Storage path mount |This parameter is currently not supported in JSON mode. |N |Set the storage path that may need to be mounted for the current job. For details, see [Overview of storage mounting](https://docs.byteplus.com/docs/E-MapReduce/Overview_of_storage_mounting). |

5. After editing the job, click the Create and run button in the lower right corner to submit the job.

   You can also create the job only and manually trigger the task to run later from the job list page.

## Submit job: via SDK

Currently, EMR Serverless supports Java and Python SDKs. For Java SDK usage, refer to: [Java Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Java_Query_SDK); for Python SDK usage, refer to: [Python Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Python_Query_SDK).

## Submit job: via Spark Submit

For usage, refer to the documentation: [Spark-submit tool usage instructions](https://docs.byteplus.com/docs/E-MapReduce/Spark-submit_tool_usage_instructions).

## Submit job: Python SDK method

> **说明**

* > In addition to submitting via the Serverless page, EMR Serverless Spark also supports submitting PySpark jobs using the SDK.

* > For a Quick Start with the Python SDK, refer to: [Python Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Python_Query_SDK).

The following provides a minimal PySpark job example:

```Python
def execute_spark_task():
    from emr.client import ServerlessQueryClient
    from emr.auth  import StaticCredentials
    from emr.resource import JarResourceInfo
    from emr.task import SparkJarTask

    # AK required to access your TOS bucket and LAS Formation
    ak = 'your ak'# SK required to access your TOS bucket and LAS Formation
    sk = 'your sk'# Region where EMR Serverless Spark is located
    region = 'cn-beijing'# Volcano Engine official endpoint
endpoint = 'https:// emr-serverless.cn-beijing.volcengineapi.com'# Submit the file tos://bucketname/test/pi.py from your TOS as executable Python code to PySpark
    client = ServerlessQueryClient(credentials=StaticCredentials(ak, sk), region=region,
                       endpoint=endpoint)
    job = client.execute(task=SparkJarTask(name="Py Spark demo",
                   jar=JarResourceInfo.of('tos://bucketname/test/pi.py'),
                   main_args=['arg_xxx', 'arg_yyy']
                   ), is_sync=False)

    def when_to_exit() -> bool:
        return job.get_tracking_url() is not None# Wait for task submission
    job.wait_for(when_to_exit=when_to_exit, timeout=180)
    # Get the task TrackingURL print('Tracking Url: %s' % job.get_tracking_url())

    # Wait for task execution to finish
    job.wait_for_finished()
    print('The task executed successfully.')

if __name__ == "__main__":
    execute_spark_task()
```

## Simple job example

For example, using the test.py job:

Job content:

```SQL
set serverless.spark.access.key = XXXX;
set serverless.spark.secret.key = XXXX==;
set tqs.query.engine.type = sparkjar;
set spark.jar.resource = tos://{bucket name}/{path}/test.py;
```

> **说明**

> This demo enables you to use the Python code file located at `tos://bucketname/path/ test.py` as executable Python code in PySpark and submit it to Serverless Spark. The meanings of the parameters are as follows:

|Parameter name |Parameter value |
|---|---|
|serverless.spark.access.key |The Access Key required to access LAS Catalog tables and TOS. You can obtain your account's AK from IAM access keys. |
|serverless.spark.secret.key |The SK required to access LAS Catalog tables and TOS |
|tqs.query.engine.type |Job type, fixed as `sparkjar` |
|spark.jar.resource |The TOS path where your Python code is stored |

test.py file content:

```Python
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

> **说明**

> For more PySpark examples, see the official Spark documentation: [PySpark Overview](https://spark.apache.org/docs/3.5.1/api/python/index.html).

## Advanced operations

### Add custom Python files/Python dependencies

#### Use cases

The main Python file to be executed may also depend on other Python files or common Python libraries.

#### Usage

EMR Serverless Spark supports adding dependent Python files/Python dependencies via commands. In your command, you can add the following commands:

```python
set las.spark.jar.depend.pyFiles=[{"fileName":"tos://xx.zip"}, {"fileName":"tos://xx.py"}]
```

You can load the two files under the tos path: tos://xx.zip and tos://xx.py into a PySpark task, and reference them in Python using import.

Detailed explanation of parameters follows:

|Parameter name |Parameter description |
|---|---|
|las.spark.jar.depend.pyFiles |The TOS path where your py files/libraries are located, organized as a JSON array |

The dependency file types can be `PyFile` and `Zip`.

* Dependency on `PyFile` type resources

The resource content is a Python script. When referencing this script in the entry Python file, it is imported as a **module** , and the module name is the file name.

Example:

When the dependency is `start.py`, the main file references it as follows:

```python
from start import xxx
```

* Dependency on `Zip` type resources

The resource content is a zip package. When referencing the contents of the zip package in the entry Python file, you can directly use the contents of the zip package as a **package** .

Example:

The directory structure of the zip package is:

> core/start.py

> core/end.py

The reference method is:

```python
from core.start import xxx
from core.end import xxx
```

### Add custom files

#### Use cases

The main Python execution file needs to read files from TOS, but does not want to introduce the TOS SDK, and wants to read the files directly from the Classpath during code execution.

#### Usage

EMR Serverless Spark supports adding custom files using commands. You can add files from tos to the PySpark Classpath through commands and read them using Python code. In your command, you can add the following command:

```python
set las.spark.jar.depend.files = [{"fileName":"tos://xx.txt"}]
```

You can load the file under the tos path: tos://xx.txt into a PySpark task.

Parameter details:

|Parameter name |Parameter description |
|---|---|
|las.spark.jar.depend.files |The TOS path where your files are located, organized as a JSON array |

After adding, you can use the built\-in PySpark API to read and write files.

|Method |Parameter |Return value |
|---|---|---|
|SparkFiles.get('xxx') |String type parameter; xx is the access name |Returns the absolute path of the file |
|SparkFiles.getRootDirectory() | |Return the absolute path of the parent directory where the file is located |

### Add custom Jar

#### Use cases

To access other data sources via PySpark Dataframe, such as Volcano ES or VeDB, you need to add the corresponding connector jar.

> The following demo shows reading MySQL data via Spark Dataframe. In this case, you need to add the relevant MySQL JDBC Driver jar package.

```python
df = spark.read.format("jdbc") \
        .option("url", f"jdbc:mysql://{MYSQL_HOST}:{MYSQL_PORT}/{MYSQL_DATABASE}") \
        .option("dbtable", "xx") \
        .option("user", MYSQL_USERNAME) \
        .option("password", MYSQL_PASSWORD) \
        .option("driver", "com.mysql.cj.jdbc.Driver") \
        .option("partitionColumn", PARTITION_COL) \
        .option("lowerBound", 1) \
        .option("upperBound", PARTITION_UPPER_BOUND) \
        .option("numPartitions", PARTITION_NUM) \
        .load()
```

#### Usage

EMR Serverless Spark supports adding custom Jar packages. You can add custom Jar to the task Classpath by adding the following parameter in the command:

```sql
set las.spark.jar.depend.jars = [{"fileName":"tos://bucketname/elasticsearch-spark-35_2.12-8.13.2.jar"}]
```

Parameter details:

|Parameter name |Parameter description |
|---|---|
|las.spark.jar.depend.jars |The tos path where the dependent Jar files are located, organized as a JSON array |

### Use a custom Python environment

#### Use cases

There is a need for a custom Python version (EMR Serverless Spark uses Python 3.7 by default), and the Python environment dependencies are complex.

EMR Serverless Spark supports using a custom Python environment. You can customize your PySpark runtime environment, including but not limited to custom Python versions and custom Python dependencies.

#### Usage

> **注意**

> Python compilation environment requirement: X86_64

You can use virtualenv or conda to set up a custom Python version and dependency environment.

> **注意**

* > For complex dependencies, it is recommended to use conda, which provides a more comprehensive Python environment

* > Some dependency packages rely on underlying implementations that are not installed via pip. These packages cannot be packaged into an independent Python environment using virtualenv.

##### Build an independent Python environment

* Build an independent Python environment using conda

```Bash
# Construct a Python environment with Python version 3.7.9
conda create -n python379 python=3.7.9

# Enter this environment
conda activate python379

# Install pandas dependency
echo 'pandas' > requirements.txt
pip install -r requirements.txt

# Package the independent environment and generate the zip package python379.zip
cd ${conda_home}/envs/python379 && zip -r python379.zip *

# Exit
conda deactivate
```

* Build an independent Python environment using virtualenv

```Bash
# Construct a Python environment corresponding to the local Python 3 version
virtualenv --python=$(which python3) --clear python379

# Enter this environment
source python379/bin/activate

# Install koalas dependency
echo 'koalas' > requirements.txt
pip install -r requirements.txt

# Package the independent environment and generate the zip package python379.zip
cd python379 && zip -r python379.zip *

# Exit
deactivate
```

##### Run pyspark using a custom python environment

* Upload python379.zip to TOS. Here, the path is assumed to be: tos://bucketname/python379.zip

* Specify the archives dependency and add this resource dependency in archives.

```sql
set las.spark.jar.depend.archives=[{"fileName":"tos://bucketname/python379.zip"}]
```

* Set python parameters

```sql
set spark.unpackUseCommand.enabled = true;
set spark.pyspark.driver.python = python379.zip/bin/python3;
set spark.pyspark.python = python379.zip/bin/python3;
```

|Parameter name |Parameter value |Parameter description |
|---|---|---|
|spark.unpackUseCommand.enabled |true |Use the command\-line method to extract the zip package to prevent loss of data permissions |
|spark.pyspark.driver.python |python379.zip/bin/python3 |The driver uses Python, with the prefix path as the file name + .zip |
|spark.pyspark.python |python379.zip/bin/python3 |The executor uses Python, with the prefix path as the file name + .zip |

* Submit the task in the console to complete the submission of a custom python environment task.

# View/run/delete jobs

After a job is created, you can view all created jobs on the job list page, manually trigger a job to run, or edit, modify, and delete jobs.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1941ed94ade4f4cbbd2cde209b34c06~tplv-goo7wpa0wc-image.image)

# View and diagnose job instances

After submitting a job, you can also view the details of all submitted job run instances on the Job center \> Job instance page, including run status, job type, resource details, submitter, and more.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ff2963cba543d1a50fb25d9508db7e~tplv-goo7wpa0wc-image.image)

* At the top of the page, you can quickly filter job instances by scope, submitter, and other criteria to view the details of the job instances.

* For jobs that failed to run, you can click "Log" to view detailed job run logs and locate the cause of the failure; you can also use the "AI diagnosis" feature to perform intelligent job diagnosis.
