---
title: "Serverless PySpark development guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_PySpark_development_guide"
---

## SDK installation

Before using the Python SDK, you need to install the required dependency packages locally via the wheel file.

Refer to [Python Query SDK](https://docs.byteplus.com/docs/E-MapReduce/sdk_Python_Query_SDK) for SDK installation instructions.

After downloading the file, run the following command to install, and you can start using the Python SDK to Submit Job.

```Bash
pip3 install python_serverless-1.0.3-py3-none-any.whl
```

## SDK parameter notes

Pyspark tasks provide users with support for customized data analysis requirements by writing Python Spark applications.

PySparkTask is the interface provided by the SDK for executing PySpark tasks:

|Parameter |Type |Required |Description |
|---|---|---|---|
|script |str |Y |The SparkJar resource used during task execution. You must provide the TOS path, for example: ['tos://bucket/path/to/pyfile'] |
|args |list |N |Parameters for the main function of the Spark application. The default is an empty list |
|name |str |N |Task name. If not specified, it will be generated as SparkJarTask_$ |
|conf |dict |N |Used to specify task parameters. The default is empty |
|queue |str |N |Specify the queue name for running. If not filled, the public queue will be selected |
|depend_jars |[ ]str |N |Dependent jar files, corresponding to the \-\-jars option of spark\-submit, for example: ['tos://bucket/path/to/jar'] |
|files |[ ]str |N |Dependent files, corresponding to the \-\-files option of spark\-submit, for example: ['tos://bucket/path/to/file'] |
|archives |[ ]str |N |Dependent archive files, corresponding to the \-\-archives option of spark\-submit, for example: ['tos://bucket/path/to/archive'] |
|pyfiles |[ ]str |N |Dependent pyfile files, corresponding to the \-\-pyfiles option of spark\-submit, for example: ['tos://bucket/path/to/pyfile'] |

## Create a PySpark task

### Common parameters

* Supported regions are as follows:

   * `cn-beijing`

   * `cn-shanghai`

   * `cn-guangzhou`

   * `ap-southeast-1`

* Spark parameters.

|Property |Property name |Description |Default value |
|---|---|---|---|
|**Driver related** |`spark.driver.memory` |Driver heap memory size |12g |
||`spark.driver.memoryOverhead` |Driver off\-heap memory size |4g |
||`spark.driver.cores` |Number of CPU cores for the driver program |4 |
||`spark.driver.maxResultSize` |Maximum size of driver return results |3g |
|**Executor related** |`spark.executor.cores` |Number of CPU cores for each executor |4 |
||`spark.executor.memory` |Memory size for each executor |12g |
||`spark.executor.memoryOverhead` |Off\-heap memory size for each executor |4g |
||`spark.executor.instances` |Number of executor instances (Dynamic allocation is enabled by default, so there is no need to set this parameter.) |1 |
|**dynamic related** |`spark.dynamicAllocation.enabled` |Enable dynamic allocation |true |
||`spark.dynamicAllocation.minExecutors` |Minimum number of Executors |1 |
||`spark.dynamicAllocation.maxExecutors` |Maximum number of Executors |30 |
|**Parallelism and task scheduling** |`spark.sql.files.maxPartitionBytes` |File size for a single Map task |268435456 |
||`spark.sql.shuffle.partitions` |Number of partitions generated during Shuffle operations |200 |

* For other parameters, refer to [Spark official website](https://spark.apache.org/docs/latest/configuration.html#server-configuration).

### Execute SQL task

* spark\-demo\-sql.py

```Python
from pyspark.sql import SparkSession

# Create SparkSession object
spark = SparkSession.builder \
    .enableHiveSupport() \
    .getOrCreate()

spark.sql("select 1").show()

spark.stop()
```

* spark\-submit.py

```Python
from serverless.task import PySparkTask
from serverless.auth import StaticCredentials
from serverless.client import ServerlessClient
from serverless.enums import JobStatus
from serverless.exceptions import QuerySdkError
import time

ak = '<your_actual_ak>'
sk = '<your_actual_sk>'
region = 'cn-beijing'
service = 'emr_serverless'
endpoint = 'emr-serverless.cn-beijing.volcengineapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_sql.py'
# Custom parameters
    main_args = []

      task = PySparkTask(name='lei pyspark task test',
                       script=pyscript_resource,
                       args=main_args,
                       conf={'serverless.spark.runtime.role': 'trn:iam::{$AccountID}:role/{$RoleName}',
                             # Use custom resources; by default, driver and executor are 4c/16g
                             # 'spark.driver.cores': '4',
                             # 'spark.driver.maxResultSize': '100g',
                             # 'spark.driver.memory': '12g',
                             # 'spark.driver.memoryOverhead': '4g',
                             # 'spark.executor.cores': '4',
                             # 'spark.executor.memory': '12g',
                             # 'spark.executor.memoryOverhead': '4g',

                             # (Optional) You can choose whether to use a custom image as needed
                             'las.cluster.type': 'vke',
                             'spark.kubernetes.container.image': 'emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-spark/spark:online-SQL-1.0.0.103-20240627105213'
                             }
                       #queue=xxx; if not specified, the default is the public queue
                       )

    print('start submit task')
    job = client.execute(task=task, is_sync=False)
    while not JobStatus.is_finished(job.status):
        job = client.get_job(job.id)
        print('Id: %s, Status: %s' % (job.id, job.status))
        try:
            print('Tracking ui: %s' % job.get_tracking_url())
        except QuerySdkError:
            pass
        time.sleep(3)

    print('The task executed successfully!!!')
    print('Tracking ui: %s' % job.get_tracking_url())
    print('Result ui: %s' % job.get_result_url())


def get_conf():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    job = client.get_job(277548274)

    client.cancel_job(job)
    print('start_time: %s' % job.__getattribute__("start_time"))
    print('end_time: %s' % job.__getattribute__("end_time"))
    print('status: %s' % job.__getattribute__("status"))
    print('queue_name: %s' % job.__getattribute__("queue_name"))
    print('conf: %s' % job.__getattribute__("conf"))
    print('tracking_url: %s' % job.get_tracking_url())


def cancel_job():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    client.cancel_job(client.get_job(277548274))


if __name__ == "__main__":
    submit()
```

### Access TOS files

* spark\-demo\-tos.py

```Python
import argparse
from pyspark.sql import SparkSession
from pyspark import SparkFiles

# Create a SparkSession object
spark = SparkSession.builder \
    .enableHiveSupport() \
    .getOrCreate()

parser = argparse.ArgumentParser(description='This is an example program.')
parser.add_argument('--name', help='name')
parser.add_argument('--inputFile', help='Input file')
parser.add_argument('--archiveName', help='Output file')
parser.add_argument('--archiveFile', help='Output file path')
args = parser.parse_args()
inputFile = args.inputFile
name = args.name
archiveName = args.archiveName
archiveFile = args.archiveFile
# Print parameter values
print('Name input path:', name)
print('Input file path:', inputFile)
print('Output file path:', archiveName)
print('Show details:', archiveFile)

print('Start to output file content:', inputFile)
file_df = spark.sparkContext.textFile(inputFile)
file_df_data = file_df.collect()

SparkFiles.get(inputFile)
print("inputFile data:")
for line in file_df_data:
    print(line)


# Create sample data
data = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]
df = spark.createDataFrame(data, ["Name", "Age"])
# Save the DataFrame as a CSV file
output_path = "tos://emr-qa/lei/lei_db/people_table.csv"
df.write.csv(output_path)


spark.stop()
```

* spark\-submit.py

```Python
from serverless.task import PySparkTask
from serverless.auth import StaticCredentials
from serverless.client import ServerlessClient
from serverless.enums import JobStatus
from serverless.exceptions import QuerySdkError
import time

ak = '<your_actual_ak>'
sk = '<your_actual_sk>'
region = 'cn-beijing'
service = 'emr_serverless'
endpoint = 'emr-serverless.cn-beijing.volcengineapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_sql.py'
# Custom parameters
    main_args = ['--inputFile', 'rel.txt', '--archiveName', 'archives_data.zip', '--archiveFile', 'rel.txt']
# Dependent files, corresponding to the --files option of spark-submit
    files = ['tos://emr-qa/lei/demo/spark/rel.txt']
# Dependent archive files, corresponding to the --archives option of spark-submit,
    archives = ['tos://emr-qa/lei/demo/spark/archives_data.zip']
# Dependent pyfile files, corresponding to the --pyfiles option of spark-submit
    pyfiles = ['tos://emr-qa/lei/demo/spark/basic_statistics.zip']

    task = PySparkTask(name='lei pyspark task test',
                       script=pyscript_resource,
                       args=main_args,
                       conf={'serverless.spark.runtime.role': 'trn:iam::{$AccountID}:role/{$RoleName}',

                             # (Optional) You can choose whether to use a custom image as needed
                             'las.cluster.type': 'vke',
                             'spark.kubernetes.container.image': 'emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-spark/spark:online-SQL-1.0.0.103-20240627105213'
                             },
                       files=files,
                       archives=archives,
                       pyfiles=pyfiles
                       #queue=
                       )

    print('start submit task')
    job = client.execute(task=task, is_sync=False)
    while not JobStatus.is_finished(job.status):
        job = client.get_job(job.id)
        print('Id: %s, Status: %s' % (job.id, job.status))
        try:
            print('Tracking ui: %s' % job.get_tracking_url())
        except QuerySdkError:
            pass
        time.sleep(3)

    print('The task executed successfully!!!')
    print('Tracking ui: %s' % job.get_tracking_url())
    print('Result ui: %s' % job.get_result_url())


def get_conf(job_id: str):
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    job = client.get_job(job_id)

    client.cancel_job(job)
    print('start_time: %s' % job.__getattribute__("start_time"))
    print('end_time: %s' % job.__getattribute__("end_time"))
    print('status: %s' % job.__getattribute__("status"))
    print('queue_name: %s' % job.__getattribute__("queue_name"))
    print('conf: %s' % job.__getattribute__("conf"))
    print('tracking_url: %s' % job.get_tracking_url())


def cancel_job(job_id: str):
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    client.cancel_job(client.get_job(job_id))

if __name__ == "__main__":
    submit()
```

### Depend on custom image

* Configure the `conf` parameter of `PySparkTask`.

```Python
{
  'serverless.spark.runtime.role': 'trn:iam::<ACCOUNT_ID>:role/<ROLE_NAME>',
  'las.cluster.type': 'vke',
  'spark.kubernetes.container.image': 'emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-spark/spark:online-SQL-1.0.0.103-20240708105213'
}
```

### Depend on custom jar

* Configure the conf parameter.

```Python
{
  'serverless.spark.runtime.role': 'trn:iam::<ACCOUNT_ID>:role/<ROLE_NAME>',
  'las.spark.jar.depend.jars': '[{\"fileName\": \"tos://lei-las-formation/pyspark/spark-jar-demo-1.0-SNAPSHOT.jar\"}]'
}
```

### Depend on custom module

* spark\-demo\-module.py。

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

# Create SparkSession object
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

# Use functions from the module
result_multiply = df.rdd.map(lambda x: my_module1.multiply(x[0], 5)).collect()
result_add = df.rdd.map(lambda x: my_module2.add(x[0], 10)).collect()

time.sleep(360)
spark.stop()
```

* Submit the Spark task client.

```Python
from serverless.task import PySparkTask
from serverless.auth import StaticCredentials
from serverless.client import ServerlessClient
from serverless.enums import JobStatus
from serverless.exceptions import QuerySdkError
import time

ak = '<your_actual_ak>'
sk = '<your_actual_sk>'
region = 'cn-beijing'
service = 'emr_serverless'
endpoint = 'emr-serverless.cn-beijing.volcengineapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_module.py'
# Custom parameters
    main_args = []
  
    pyfiles = ['tos://emr-qa/lei/demo/spark/basic_statistics.zip', 'tos://emr-qa/lei/demo/spark/tools.zip',
           'tos://emr-qa/lei/demo/spark/module1.zip',
           'tos://emr-qa/lei/demo/spark/module2.zip']
    task = PySparkTask(name='lei pyspark task test',
                       script=pyscript_resource,
                       args=main_args,
                       conf={'serverless.spark.runtime.role': 'trn:iam::{$AccountID}:role/{$RoleName}',
                             'spark.executorEnv.PYTHONPATH': '/opt/spark/work-dir/module1.zip:/opt/spark/work-dir/module2.zip:/opt/spark/work-dir/basic_statistics.zip:/opt/spark/work-dir/tools.zip',
                             },
                       pyfiles=pyfiles
                       )

    print('start submit task')
    job = client.execute(task=task, is_sync=False)
    while not JobStatus.is_finished(job.status):
        job = client.get_job(job.id)
        print('Id: %s, Status: %s' % (job.id, job.status))
        try:
            print('Tracking ui: %s' % job.get_tracking_url())
        except QuerySdkError:
            pass
        time.sleep(3)

    print('The task executed successfully!!!')
    print('Tracking ui: %s' % job.get_tracking_url())
    print('Result ui: %s' % job.get_result_url())


def get_conf(job_id: str):
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    job = client.get_job(job_id)

    client.cancel_job(job)
    print('start_time: %s' % job.__getattribute__("start_time"))
    print('end_time: %s' % job.__getattribute__("end_time"))
    print('status: %s' % job.__getattribute__("status"))
    print('queue_name: %s' % job.__getattribute__("queue_name"))
    print('conf: %s' % job.__getattribute__("conf"))
    print('tracking_url: %s' % job.get_tracking_url())


def cancel_job(job_id: str):
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    client.cancel_job(client.get_job(job_id))


if __name__ == "__main__":
    submit()
```

> **说明**

> The user must replace the TOS file path in the command with the actual TOS file path.

* Dependencies are as follows.

[basic_statistics.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a652b66c005b4b59874b11be957f1cef~tplv-goo7wpa0wc-image.image)

[module1.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46fd597ebc354fa0bda936343b2cddd1~tplv-goo7wpa0wc-image.image)

[module2.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e361bb7a3ff4a8d9d1f4a94861dbeba~tplv-goo7wpa0wc-image.image)

[tools.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6ab9cd4d1f14a41b2bc17ccfbb1a527~tplv-goo7wpa0wc-image.image)

### Depend on custom conda environment

* `conf` parameter of `PySparkTask`.

```Python
{
 'serverless.spark.runtime.role': 'trn:iam::{$AccountID}:role/{$RoleName}',
 'spark.unpackUseCommand.enabled': 'true',
 'las.spark.jar.depend.archives': '[{\"fileName\": \"tos://emr-qa/lei/demo/spark/python38_new.zip\"}]',
 'spark.pyspark.python': 'python38_new.zip/python38_new/bin/python3',
 'spark.pyspark.driver.python': 'python38_new.zip/python38_new/bin/python3'
}
```

> **说明**

> The user must replace the TOS file path in the command with the actual TOS file path.

* conda installation.

```Shell
# install
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh
# environmental variable
vi .bashrc
export PATH="/root/miniconda3/bin:$PATH" 
source .bashrc
```

* Build a Python 3.8 environment with conda.

```Shell
# set python3.8
conda create --name python38_new python=3.8
source activate python38_new
pip3 install pandas
pip3 install scipy
pip3 install scikit-learn

# zip python3.8
which python3
cd /root/miniconda/python38_new/env
zip -r python38_new.zip python38_new/
```

## Other usage

### Serverless Spark access HMS

* Pseudocode (pythonSDK)

```Bash
task = PySparkTask(name='pyspark hms demo',
                   script=pyscript_resource,
                   args=main_args,
                   conf={'serverless.spark.runtime.role': 'trn:iam::{$AccountID}:role/{$RoleName}',
                         'serverless.cross.vpc.access.enabled':'true',
                         # Volcano Engine - Tenant ID
                         'serverless.cross.vpc.accountId':'xxx',
                         # Volcano Engine - HMS - Private network ID
                         'serverless.cross.vpc.vpc.id':'xxx',
                         # Volcano Engine - HMS - Private network - Subnet ID
                         'serverless.cross.vpc.subnet.ids':'xxx',
                         # Volcano Engine - HMS - Private network - Security group ID
                         'serverless.cross.vpc.security.group.id':'xxx'}
                   )
```

### Access Volcano ES with Serverless Spark.

* Main steps:

   1. Establish VPC network connectivity between Serverless Spark and Volcano ES.

   2. Upload ES dependency jar to your account's TOS.

   3. When submitting Spark tasks, include the ES dependency path in the depends_jars parameter.

* Pseudocode (pythonSDK)

```Bash
task = PySparkTask(name='pyspark es demo',
                   script=pyscript_resource,
                   args=main_args,
                   depend_jars=['tos://emr-qa/lei/demo/spark/elasticsearch-spark-30_2.12-8.13.2.jar'],
                   conf={'serverless.spark.runtime.role': 'trn:iam::{$AccountID}:role/{$RoleName}',
                         'serverless.cluster.type':'vke',
                         'serverless.cross.vpc.access.enabled':'true',
                         # Volcano Engine - Tenant ID
                         'serverless.cross.vpc.accountId':'xxx',
                         # Volcano Engine - ES - Private network ID
                         'serverless.cross.vpc.vpc.id':'xxx',
                         # Volcano Engine - ES - Private network - Subnet ID
                         'serverless.cross.vpc.subnet.ids':'xxx',
                         # Volcano Engine - ES - Private network - Security group ID
                         'serverless.cross.vpc.security.group.id':'xxx'}
                   )
```

> **说明**

> The user must replace the TOS file path in the command with the actual TOS file path.

### Cross VPC access

* Create an auxiliary network interface in the customer's VPC and bind the specified security group.

* The started driver and executor are bound to the auxiliary network interface from the previous step, enabling cross\-VPC access.

* Configure the conf parameter.

```Python
{
  'serverless.cluster.type': 'vke',
  'serverless.cross.vpc.access.enabled': 'true',
  # Volcano Engine - User - VPCId
  'serverless.cross.vpc.vpc.id': 'vpc-xxx',
  # Volcano Engine - User - Subnet ID
  'serverless.cross.vpc.subnet.ids': 'subnet-xxx',
  # Volcano Engine - User VPC security group ID
  'serverless.cross.vpc.security.group.id': 'sg-xxx',
  # Volcano Engine - User's tenant ID
  'serverless.cross.vpc.accountId': 'xxx'
}
```
