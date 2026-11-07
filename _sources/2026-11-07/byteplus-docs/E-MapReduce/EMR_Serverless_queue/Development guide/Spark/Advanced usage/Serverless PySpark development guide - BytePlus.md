---
title: "Serverless PySpark development guide - BytePlus"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_PySpark_development_guide_-_BytePlus"
---

<span id="3514d7aa"></span>
## SDK installation

Before using the Python SDK, you need to install the required dependency packages locally via the wheel file.

Installation package:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77b66154b0c348a5b11ffeba355f357e~tplv-goo7wpa0wc-image.image" name="python_serverless-1.0.3-py3-none-any.whl">python_serverless-1.0.3-py3-none-any.whl</Attachment>


&nbsp;

After downloading the above files, execute the following command to install them. You can then start using the Python SDK to Submit Job.

```Bash
pip3 install python_serverless-1.0.3-py3-none-any.whl
```


<span id="9e4701f6"></span>
## SDK parameter description

The PySpark task provides users with support for customized data analysis requirements by writing Python Spark applications. For details, see [PySpark 作业开发指南](https://docs.byteplus.com/docs/undefined/66581c6fd9d1b4026c17ba14).

PySparkTask is the interface provided by the SDK for executing PySpark tasks:


|Parameter |Type |Required |Description |
|---|---|---|---|
|script |str |Y |The SparkJar resource used during task execution. You need to provide the TOS path, for example: ['tos://bucket/path/to/pyfile'] |
|args |list |N |The main function parameters of the Spark application. The default is an empty list. |
|name |str |N |Task name. If not specified, it will be generated as SparkJarTask_${current_time}. |
|conf |dict |N |Used to specify task parameters. The default is empty. |
|queue |str |N |Specify the name of the run queue. If not filled in, the public queue will be used. |
|depend_jars |[ ]str |N |Dependent jar files, corresponding to the \-\-jars option of spark\-submit, for example: ['tos://bucket/path/to/jar'] |
|files |[ ]str |N |Dependent files, corresponding to the \-\-files option of spark\-submit, for example: ['tos://bucket/path/to/file'] |
|archives |[ ]str |N |Dependent archive files, corresponding to the \-\-archives option of spark\-submit, for example: ['tos://bucket/path/to/archive'] |
|pyfiles |[ ]str |N |Dependent pyfile files, corresponding to the \-\-pyfiles option of spark\-submit, for example: ['tos://bucket/path/to/pyfile'] |


<span id="599135f1"></span>
## Create a PySpark task

<span id="4b11aa72"></span>
### Common parameters


* Supported regions are as follows:

   * `ap-southeast-1`

* spark parameters.



|Property |Property name |Description |Default value |
|---|---|---|---|
|**Driver related** |`spark.driver.memory` |Driver heap memory size |12g |
||`spark.driver.memoryOverhead` |Driver off\-heap memory size |4g |
||`spark.driver.cores` |Number of CPU cores for the Driver program |4 |
||`spark.driver.maxResultSize` |Maximum size of Driver return results |3g |
|**Executor related** |`spark.executor.cores` |Number of CPU cores for each Executor |4 |
||`spark.executor.memory` |Memory size for each Executor |12g |
||`spark.executor.memoryOverhead` |Off\-heap memory size for each Executor |4g |
||`spark.executor.instances` |Number of Executor instances (dynamic allocation is enabled by default, no need to set this parameter) |1 |
|**Dynamic allocation settings** |`spark.dynamicAllocation.enabled` |Whether to enable dynamic allocation |true |
||`spark.dynamicAllocation.minExecutors` |Minimum number of Executors |1 |
||`spark.dynamicAllocation.maxExecutors` |Maximum number of Executors |30 |
|**Parallelism and task scheduling** |`spark.sql.files.maxPartitionBytes` |File size per Map task |268435456 |
||`spark.sql.shuffle.partitions` |Number of partitions generated during Shuffle operations |200 |



* For other parameters, please refer to [Spark official website](https://spark.apache.org/docs/latest/configuration.html#server-configuration).


<span id="7378767c"></span>
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

ak = '<此处填写用户实际的 AK>'
sk = '<此处填写用户实际的 SK>'
region = 'cn-beijing'
service = 'emr_serverless'
endpoint = 'open.volcengineapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_sql.py'
    # Custom parameters
    main_args = []
  

      task = PySparkTask(name='lei pyspark task test',
                       script=pyscript_resource,
                       args=main_args,
                       conf={'serverless.spark.access.key': ak,
                             'serverless.spark.secret.key': sk,
                             # Use custom resources; by default, driver and executor are 4c/16g
                             # 'spark.driver.cores': '4',
                             # 'spark.driver.maxResultSize': '100g',
                             # 'spark.driver.memory': '12g',
                             # 'spark.driver.memoryOverhead': '4g',
                             # 'spark.executor.cores': '4',
                             # 'spark.executor.memory': '12g',
                             # 'spark.executor.memoryOverhead': '4g',

                             # Optional: Use a custom image as needed
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


<span id="18aec31c"></span>
### Access TOS files


* spark\-demo\-tos.py


```Python
import argparse
from pyspark.sql import SparkSession
from pyspark import SparkFiles

# Create SparkSession object
spark = SparkSession.builder \
    .enableHiveSupport() \
    .getOrCreate()

parser = argparse.ArgumentParser(description='这是一个示例程序')
parser.add_argument('--name', help='name')
parser.add_argument('--inputFile', help='输入文件')
parser.add_argument('--archiveName', help='输出文件')
parser.add_argument('--archiveFile', help='输出文件路径')
args = parser.parse_args()
inputFile = args.inputFile
name = args.name
archiveName = args.archiveName
archiveFile = args.archiveFile
# Print parameter values
print('name输入文件路径:', name)
print('输入文件路径:', inputFile)
print('输出文件路径:', archiveName)
print('显示详细信息:', archiveFile)

print('开始输出文件内容:', inputFile)
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

ak = '<此处填写用户实际的 AK>'
sk = '<此处填写用户实际的 SK>'
region = 'cn-beijing'
service = 'emr_serverless'
endpoint = 'open.volcengineapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_sql.py'
    # Custom parameters
    main_args = ['--inputFile', 'rel.txt', '--archiveName', 'archives_data.zip', '--archiveFile', 'rel.txt']
    # Dependent files, corresponding to the --files option of spark-submit
    files = ['tos://emr-qa/lei/demo/spark/rel.txt']
    # Dependent archive files, corresponding to the --archives option of spark-submit,
    archives = ['tos://emr-qa/lei/demo/spark/archives_data.zip']
    # Dependent Python files, corresponding to the --pyfiles option of spark-submit
    pyfiles = ['tos://emr-qa/lei/demo/spark/basic_statistics.zip']

    task = PySparkTask(name='lei pyspark task test',
                       script=pyscript_resource,
                       args=main_args,
                       conf={'serverless.spark.access.key': ak,
                             'serverless.spark.secret.key': sk,

                             # Optional: Use a custom image as needed
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


<span id="cfb26aa0"></span>
### Depend on a custom image


* Configure `PySparkTask`'s `conf` parameter.


```Python
{
  'serverless.spark.access.key': 'xx',
  'serverless.spark.secret.key': 'xx',
  'las.cluster.type': 'vke',
  'spark.kubernetes.container.image': 'emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-spark/spark:online-SQL-1.0.0.103-20240708105213'
}
```


<span id="256994dc"></span>
### Depend on a custom jar


* Configure the conf parameter.


```Python
{
  'serverless.spark.access.key': 'xx',
  'serverless.spark.secret.key': 'xx',
  'las.spark.jar.depend.jars': '[{\"fileName\": \"tos://lei-las-formation/pyspark/spark-jar-demo-1.0-SNAPSHOT.jar\"}]'
}
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33055522ba81443992b9b0764f079b6b~tplv-goo7wpa0wc-image.image" width="2936px" /></div>


<span id="9e6f542f"></span>
### Depend on a custom module


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



* Submit Spark task (client).


```Python
from serverless.task import PySparkTask
from serverless.auth import StaticCredentials
from serverless.client import ServerlessClient
from serverless.enums import JobStatus
from serverless.exceptions import QuerySdkError
import time

ak = '<此处填写用户实际的 AK>'
sk = '<此处填写用户实际的 SK>'
region = 'cn-beijing'
service = 'emr_serverless'
endpoint = 'open.volcengineapi.com'


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
                       conf={'serverless.spark.access.key': ak,
                             'serverless.spark.secret.key': sk,
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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The user must replace the TOS file path in the command with the actual TOS file path.</div>



* The dependencies are as follows.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a652b66c005b4b59874b11be957f1cef~tplv-goo7wpa0wc-image.image" name="basic_statistics.zip">basic_statistics.zip</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46fd597ebc354fa0bda936343b2cddd1~tplv-goo7wpa0wc-image.image" name="module1.zip">module1.zip</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e361bb7a3ff4a8d9d1f4a94861dbeba~tplv-goo7wpa0wc-image.image" name="module2.zip">module2.zip</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6ab9cd4d1f14a41b2bc17ccfbb1a527~tplv-goo7wpa0wc-image.image" name="tools.zip">tools.zip</Attachment>


&nbsp;

<span id="54aa08f7"></span>
### Depend on a custom conda environment


* `PySparkTask`'s `conf` parameter.


```Python
{
 'serverless.spark.access.key': '{access key}',
 'serverless.spark.secret.key': '{secret key}',
 'spark.unpackUseCommand.enabled': 'true',
 'las.spark.jar.depend.archives': '[{\"fileName\": \"tos://emr-qa/lei/demo/spark/python38_new.zip\"}]',
 'spark.pyspark.python': 'python38_new.zip/python38_new/bin/python3',
 'spark.pyspark.driver.python': 'python38_new.zip/python38_new/bin/python3'
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The user must replace the TOS file path in the command with the actual TOS file path.</div>



* conda installation.


```Shell
# 安装
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh
# 环境变量
vi .bashrc
export PATH="/root/miniconda3/bin:$PATH" 
source .bashrc
```



* conda builds python3.8 environment.


```Shell
# 构建python3.8环境
conda create --name python38_new python=3.8
source activate python38_new
pip3 install pandas
pip3 install scipy
pip3 install scikit-learn

# 打成压缩包
which python3
cd /root/miniconda/python38_new/env
zip -r python38_new.zip python38_new/
```


<span id="3461ff69"></span>
## Other usages

<span id="a9049736"></span>
### Serverless Spark accesses HMS


* Pseudocode (pythonSDK)


```Bash
task = PySparkTask(name='pyspark hms demo',
                   script=pyscript_resource,
                   args=main_args,
                   conf={'serverless.spark.access.key': ak,
                         'serverless.spark.secret.key': sk,
                         'las.cross.vpc.access.enabled':'true',
                         # Volcano Engine - Tenant ID
                         'las.cross.vpc.accountId':'xxx',
                         # Volcano Engine - HMS - Private network ID
                         'las.cross.vpc.vpc.id':'xxx',
                         # Volcano Engine - HMS - Private network subnet ID
                         'las.cross.vpc.subnet.id':'xxx',
                         # Volcano Engine - HMS - Private network security group ID
                         'las.cross.vpc.security.group.id':'xxx'}
                   )
```


<span id="c088440a"></span>
### Serverless Spark accesses Volcano ES


* Main steps:

   1. Establish VPC network connectivity between Serverless Spark and Volcano ES.

   2. Upload the ES dependency jar to your account's TOS.

   3. When submitting a Spark task, include the ES dependency path in the depends_jars parameter.

* Pseudocode (pythonSDK)


```Bash
task = PySparkTask(name='pyspark es demo',
                   script=pyscript_resource,
                   args=main_args,
                   depend_jars=['tos://emr-qa/lei/demo/spark/elasticsearch-spark-30_2.12-8.13.2.jar'],
                   conf={'serverless.spark.access.key': ak,
                         'serverless.spark.secret.key': sk,
                         'las.cluster.type':'vke',
                         'las.cross.vpc.access.enabled':'true',
                         # Volcano Engine - Tenant ID
                         'las.cross.vpc.accountId':'xxx',
                         # Volcano Engine - ES - Private network ID
                         'las.cross.vpc.vpc.id':'xxx',
                         # Volcano Engine - ES - Private network subnet ID
                         'las.cross.vpc.subnet.id':'xxx',
                         # Volcano Engine - ES - Private network security group ID
                         'las.cross.vpc.security.group.id':'xxx'}
                   )
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The user must replace the TOS file path in the command with the actual TOS file path.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/701f3630034349acac35299977460066~tplv-goo7wpa0wc-image.image" width="1686px" /></div>


<span id="432e7896"></span>
### Cross\-VPC access


* Create an auxiliary network interface in the customer's VPC and bind the specified security group.

* The started driver and executor are bound to the auxiliary network interface from the previous step, enabling cross\-VPC access.

* Configure the conf parameter.


```Python
{
  'las.cluster.type': 'vke',
  'las.cross.vpc.access.enabled': 'true',
  # Volcano Engine - User - VPCId
  'las.cross.vpc.vpc.id': 'vpc-xxx',
  # Volcano Engine - User - Subnet ID
  'las.cross.vpc.subnet.id': 'subnet-xxx',
  # Volcano Engine - User VPC security group ID
  'las.cross.vpc.security.group.id': 'sg-xxx',
  # Volcano Engine - User tenant ID
  'las.cross.vpc.accountId': 'xxx'
}
```
