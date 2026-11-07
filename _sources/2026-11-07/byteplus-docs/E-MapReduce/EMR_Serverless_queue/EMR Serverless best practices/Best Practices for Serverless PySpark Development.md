---
title: "Best Practices for Serverless PySpark Development"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Best_Practices_for_Serverless_PySpark_Development"
---

<span id="38f17d46"></span>
## SDK Installation

Before using the Python SDK, you need to install the dependent packages required by the SDK locally through the wheel file.

Installation Package:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77b66154b0c348a5b11ffeba355f357e~tplv-goo7wpa0wc-image.image" name="python_serverless-1.0.3-py3-none-any.whl">python_serverless-1.0.3-py3-none-any.whl</Attachment>


&nbsp;

After downloading the above files, execute the following command for installation, and you can start using the Python SDK to submit jobs.

```Bash
pip3 install python_serverless-1.0.3-py3-none-any.whl
```


<span id="6fa48c7a"></span>
## SDK Parameter Explanation

The Pyspark task provides users with support for customized data analysis requirements by writing Python Spark applications. For details, see [PySpark Job Development Guide](https://docs.byteplus.com/docs/undefined/6878e47d349d2e0519c165f5).

PySparkTask is an interface provided by the SDK for executing PySpark tasks:


|Parameter |Type |Mandatory |Description |
|---|---|---|---|
|script |str |Y |The SparkJar resources used during task execution require a TOS path to be passed in, for example: ['tos://bucket/path/to/pyfile'] |
|args |list |N |The main function parameter of the spark application, defaulting to an empty list |
|name |str |N |The task name. If not specified, it will be generated in the form of SparkJarTask_$ |
|conf |dict |N |Used to specify task parameters, default is empty |
|queue |str |N |Specify the name of the running queue. If not filled, the public queue will be selected |
|depend_jars |[ ]str |N |Dependent jar files, corresponding to the \-\-jars option of spark\-submit. For example: ['tos://bucket/path/to/jar'] |
|files |[ ]str |N |Dependent files, corresponding to the \-\-files option of spark\-submit. For example: ['tos://bucket/path/to/file'] |
|archives |[ ]str |N |Dependent archive files, corresponding to the \-\-archieves option of spark\-submit. For example: ['tos://bucket/path/to/archive'] |
|pyfiles |[ ]str |N |The dependent pyfile, corresponding to the \-\-pyfiles option of spark\-submit. For example: ['tos://bucket/path/to/pyfile'] |


<span id="60361544"></span>
## Create a pyspark task

<span id="95a49149"></span>
### Common parameters


* The supported regions are as follows:

   * `ap-southeast-1`

* Spark parameters.



|Attribute |Attribute name |Description |Default value |
|---|---|---|---|
|**Related to Driver** |`spark.driver.memory` |The size of the Driver's in\-heap memory |12g |
||`spark.driver.memoryOverhead` |The size of off\-heap memory for the Driver |4g |
||`spark.driver.cores` |The number of CPU cores for the Driver program |4 |
||`spark.driver.maxResultSize` |The maximum size of the result returned by the Driver |3g |
|**Related to Executor** |`spark.executor.cores` |The number of CPU cores per Executor |4 |
||`spark.executor.memory` |The memory size per Executor |12g |
||`spark.executor.memoryOverhead` |The off\-heap memory size per Executor |4g |
||`spark.executor.instances` |Number of Executor instances (dynamic is enabled by default, no need to set this parameter) |1 |
|**Related to dynamic** |`spark.dynamicAllocation.enabled` |Whether to enable dynamic |true |
||`spark.dynamicAllocation.minExecutors` |Minimum number of Executors |1 |
||`spark.dynamicAllocation.maxExecutors` |Maximum number of Executors |30 |
|**Parallelism and task scheduling** |`spark.sql.files.maxPartitionBytes` |File size of a single Map task |268435456 |
||`spark.sql.shuffle.partitions` |Number of partitions generated during Shuffle operation |200 |



* Please refer to [the Spark official website](https://spark.apache.org/docs/latest/configuration.html#server-configuration) for other parameters.


<span id="10365fc9"></span>
### Execute SQL tasks


* spark\-demo\-sql.py


```Python
from pyspark.sql import SparkSession

# Create a SparkSession object
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

ak = '<your AK>'
sk = '<your SK>'
region = 'ap-southeast-1'
service = 'emr_serverless'
endpoint = 'emr-serverless.ap-southeast-1.byteplusapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_sql.py'
    # Customize parameters
    main_args = []
  

      task = PySparkTask(name='lei pyspark task test',
                       script=pyscript_resource,
                       args=main_args,
                       conf={'serverless.spark.access.key': ak,
                             'serverless.spark.secret.key': sk,
                             # Use custom resources. By default, the driver and executor are 4 cores/16GB
                             # 'spark.driver.cores': '4',
                             # 'spark.driver.maxResultSize': '100g',
                             # 'spark.driver.memory': '12g',
                             # 'spark.driver.memoryOverhead': '4g',
                             # 'spark.executor.cores': '4',
                             # 'spark.executor.memory': '12g',
                             # 'spark.executor.memoryOverhead': '4g',

                             # Use custom image
                             'las.cluster.type': 'vke',
                             'spark.kubernetes.container.image': 'emr-serverless-online-bp-{region}.cr.bytepluses.com/emr-serverless-spark/spark:online-SQL-1.0.0.103-20240627105213'
                             }
                       #queue=xxx; If not filled, the default is the public queue
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


<span id="506e6a64"></span>
### Access the TOS file


* spark\-demo\-tos.py


```Python
import argparse
from pyspark.sql import SparkSession
from pyspark import SparkFiles

# Create a SparkSession object
spark = SparkSession.builder \
    .enableHiveSupport() \
    .getOrCreate()

parser = argparse.ArgumentParser(description='Sample program')
parser.add_argument('--name', help='name')
parser.add_argument('--inputFile', help='input file')
parser.add_argument('--archiveName', help='output file')
parser.add_argument('--archiveFile', help='Output file path')
args = parser.parse_args()
inputFile = args.inputFile
name = args.name
archiveName = args.archiveName
archiveFile = args.archiveFile
# Print the value of the parameter
print('input file path:', name)
print('input file path:', inputFile)
print('Output file path:', archiveName)
print('Show detailed information:', archiveFile)

print('Start to output the content of the file:', inputFile)
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

ak = '<your AK>'
sk = '<your SK>'
region = 'ap-southeast-1'
service = 'emr_serverless'
endpoint = 'emr-serverless.ap-southeast-1.byteplusapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_sql.py'
    # Custom parameters
    main_args = ['--inputFile', 'rel.txt', '--archiveName', 'archives_data.zip', '--archiveFile', 'rel.txt']
    # Dependent files, corresponding to the --files option of spark-submit
    files = ['tos://emr-qa/lei/demo/spark/rel.txt']
    # Dependent archive files, corresponding to the --archives option of spark-submit
    archives = ['tos://emr-qa/lei/demo/spark/archives_data.zip']
    # Dependent pyfile files, corresponding to the --pyfiles option of spark-submit
    pyfiles = ['tos://emr-qa/lei/demo/spark/basic_statistics.zip']

    task = PySparkTask(name='lei pyspark task test',
                       script=pyscript_resource,
                       args=main_args,
                       conf={'serverless.spark.access.key': ak,
                             'serverless.spark.secret.key': sk,

                             # Use custom image
                             'las.cluster.type': 'vke',
                             'spark.kubernetes.container.image': 'emr-serverless-online-bp-{region}.cr.bytepluses.com/emr-serverless-spark/spark:online-SQL-1.0.0.103-20240627105213'
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


<span id="69187a21"></span>
### Rely on a custom image


* Configure the `conf` parameter of `PySparkTask`.


```Python
{
  'serverless.spark.access.key': 'xx',
  'serverless.spark.secret.key': 'xx',
  'las.cluster.type': 'vke',
  'spark.kubernetes.container.image': 'emr-serverless-online-bp-{region}.cr.bytepluses.com/emr-serverless-spark/spark:online-SQL-1.0.0.103-20240708105213'
}
```


<span id="0034dc39"></span>
### Rely on a custom jar


* Configure the conf parameters.


```Python
{
  'serverless.spark.access.key': 'xx',
  'serverless.spark.secret.key': 'xx',
  'las.spark.jar.depend.jars': '[{\"fileName\": \"tos://lei-las-formation/pyspark/spark-jar-demo-1.0-SNAPSHOT.jar\"}]'
}
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33055522ba81443992b9b0764f079b6b~tplv-goo7wpa0wc-image.image" width="2936px" /></div>


<span id="fe58a01c"></span>
### Depend on the custom module


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


# Create a DataFrame
data = [(1,), (2,), (3,), (4,)]
df = spark.createDataFrame(data, ["value"])

# Use functions in the module
result_multiply = df.rdd.map(lambda x: my_module1.multiply(x[0], 5)).collect()
result_add = df.rdd.map(lambda x: my_module2.add(x[0], 10)).collect()

time.sleep(360)
spark.stop()
```



* Submit the spark task client.


```Python
from serverless.task import PySparkTask
from serverless.auth import StaticCredentials
from serverless.client import ServerlessClient
from serverless.enums import JobStatus
from serverless.exceptions import QuerySdkError
import time

ak = '<your AK>'
sk = '<your SK>'
region = 'ap-southeast-1'
service = 'emr_serverless'
endpoint = 'emr-serverless.ap-southeast-1.byteplusapi.com'


def submit():
    client = ServerlessClient(credentials=StaticCredentials(ak, sk), service=service, region=region, endpoint=endpoint)
    pyscript_resource = 'tos://emr-qa/lei/demo/spark/pyspark_demo_module.py'
    # Customize parameters
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


<div data-tips="true" data-tips-type="tip">Users need to replace the TOS file path in the command with the actual TOS file path.</div>



* The dependent packages are as follows.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a652b66c005b4b59874b11be957f1cef~tplv-goo7wpa0wc-image.image" name="basic_statistics.zip">basic_statistics.zip</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46fd597ebc354fa0bda936343b2cddd1~tplv-goo7wpa0wc-image.image" name="module1.zip">module1.zip</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e361bb7a3ff4a8d9d1f4a94861dbeba~tplv-goo7wpa0wc-image.image" name="module2.zip">module2.zip</Attachment>


&nbsp;

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6ab9cd4d1f14a41b2bc17ccfbb1a527~tplv-goo7wpa0wc-image.image" name="tools.zip">tools.zip</Attachment>


&nbsp;

<span id="d19561d7"></span>
### Depend on the custom conda environment


* The `conf` parameter of `PySparkTask`.


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


<div data-tips="true" data-tips-type="tip">Users need to replace the TOS file path in the command with the actual TOS file path.</div>



* Install with conda.


```Shell
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh
vi .bashrc
export PATH="/root/miniconda3/bin:$PATH" 
source .bashrc
```



* Build a python3.8 environment with conda.


```Shell
conda create --name python38_new python=3.8
source activate python38_new
pip3 install pandas
pip3 install scipy
pip3 install scikit-learn

which python3
cd /root/miniconda/python38_new/env
zip -r python38_new.zip python38_new/
```


<span id="891afdf9"></span>
## Other usages

<span id="c391a4b4"></span>
### Serverless Spark accesses HMS


* Pseudocode (pythonSDK)


```Bash
task = PySparkTask(name='pyspark hms demo',
                   script=pyscript_resource,
                   args=main_args,
                   conf={'serverless.spark.access.key': ak,
                         'serverless.spark.secret.key': sk,
                         'las.cross.vpc.access.enabled':'true',
                         # byteplus - Tenant ID
                         'las.cross.vpc.accountId':'xxx',
                         # byteplus - HMS - Private Network ID
                         'las.cross.vpc.vpc.id':'xxx',
                         # byteplus - HMS - Private Network - Subnet ID
                         'las.cross.vpc.subnet.id':'xxx',
                         # byteplus - HMS - Private Network - Security Group ID
                         'las.cross.vpc.security.group.id':'xxx'}
                   )
```


<span id="ac3bcb09"></span>
### Serverless Spark accesses byteplus ES


* Main steps:

   1. Serverless Spark and byteplus ES establish VPC network connectivity.

   2. The dependent jars of ES are placed in the TOS under your account.

   3. When submitting a spark task, include the path of the ES dependencies in the depends jar.

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
                         # byteplus - Tenant ID
                         'las.cross.vpc.accountId':'xxx',
                         # byteplus - ES - Private Network ID
                         'las.cross.vpc.vpc.id':'xxx',
                         # byteplus - ES - Private Network - Subnet ID
                         'las.cross.vpc.subnet.id':'xxx',
                         # byteplus - ES - Private Network - Security Group ID
                         'las.cross.vpc.security.group.id':'xxx'}
                   )
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Users need to replace the TOS file path in the command with the actual TOS file path.</div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/701f3630034349acac35299977460066~tplv-goo7wpa0wc-image.image" width="1686px" /></div>


<span id="ee7925d8"></span>
### Cross\-VPC access


* Create an auxiliary network card in the customer's VPC and bind the specified security group.

* The started driver and executor are bound to the auxiliary network card of the previous step to enable cross\-VPC access.

* Configure the conf parameters.


```Python
{
  'las.cluster.type': 'vke',
  'las.cross.vpc.access.enabled': 'true',
  # byteplus - User - VPCId
  'las.cross.vpc.vpc.id': 'vpc-xxx',
  # byteplus - User - Subnet ID
  'las.cross.vpc.subnet.id': 'subnet-xxx',
  # byteplus - User VPC Security Group ID
  'las.cross.vpc.security.group.id': 'sg-xxx',
  #byteplus - Tenant ID of the user
  'las.cross.vpc.accountId': 'xxx'
}
```
