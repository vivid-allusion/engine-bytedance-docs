---
title: "Best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/airflow_best_practices"
---

This article presents a basic ETL scenario, connects it to the major big data components in the cluster, and incorporates some Airflow design principles to help you further master the use of Airflow.

In general, writing a DAG file involves two main parts:


1. Create the DAG source file by writing code so that it becomes a workflow recognized by Airflow.

2. Test the file to ensure it meets our expectations.


<span id="_1-前提条件"></span>
## 1 Prerequisites

The following example is based on a Hadoop\-type cluster with the Airflow service added. For details on cluster creation, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-工作流实现指引"></span>
## 2 Workflow implementation guide

<span id="_2-1-正确定义-airflow-task"></span>
### 2.1 Properly define Airflow tasks

Airflow is a programmatic workflow scheduling component. While it provides flexibility, it also introduces risks that tasks may not execute as expected due to nonstandard implementations. The following notes will guide you in writing correct task logic.


1. We should treat tasks in Airflow the same way we treat transactions in the database domain. This means that incomplete data should not be written to locations such as HDFS or TOS at the end of a task.

2. When a task fails to run, Airflow will automatically retry it. This process requires the task itself to be idempotent. Not only should the output remain consistent when the input does not change, but the input itself should also remain stable. The following are some practices that help maintain stability during task execution and retries:

   * Do not use `INSERT` in task definitions, as this may result in duplicate rows during retries. Using `UPSERT` instead is a better choice.

   * To ensure input stability, it is best to read and write within a specific partition. We should not read the latest data in a task. If the data is updated before and after a retry of a particular run, this can cause a specific DAG run to produce different results. We recommend using something like `data_interval_start` as the specific partition for a given run. When writing data, this partitioning method should also be followed.

   * Avoid using methods such as `datetime.datetime.now()`, especially when they are involved in critical calculations, as this can lead to inconsistent outputs.

3. To keep the Airflow environment organized, repetitive parameters such as connection information should be specifically configured in Airflow Connections, rather than being defined separately in each DAG. In each DAG, it is also a good practice to define a dedicated `default_args` to manage variables. These variables apply globally to the DAG, all Operators can reuse them, and the layout will be cleaner and more readable.


<span id="_2-2-任务间通信"></span>
### 2.2 Inter\-task communication

In EMR Airflow, tasks defined in a DAG run on different nodes across the cluster. This means that if there is data that needs to be used across tasks, a global storage solution is required for exchange. It is not sufficient to simply agree on a directory, write files locally, and have different tasks read the file.

For inter\-task communication scenarios, Airflow provides the `XCom` component, which is designed to exchange **small amounts of information** between upstream and downstream tasks within a workflow. A good practice is to store large data outputs that need to be used downstream in the HDFS component (mandatory for Hadoop clusters, optional for Presto/Trino clusters) or in TOS, and then use `XCom` to pass the file path information to downstream tasks.

During interactions with other components, authentication information may be involved. This information should not be hardcoded in the DAG; it is best to configure it in Airflow Connections. Airflow ensures the security and reliability of connection information, which can then be referenced in the DAG using the Connection Id.

<span id="jump"></span>
### 2.3 Correctly write DAG top\-level code

Let us first review a mechanism: in Airflow Scheduler, the DAG source file is executed at intervals defined by `min_file_process_interval`. This update mechanism ensures that the workflow definitions in Airflow remain consistent with the actual descriptions in the source file.

The essence of this execution process by the Scheduler is to run all the code in the DAG file except for the specific logic of the Operators. An important factor affecting the efficiency of this execution is the design of the top\-level code in the file, which is often overlooked. The principle here is that, apart from the logic necessary to define the DAG structure, any logic required for the specific execution of Operators should not be defined in the top\-level code, but rather within the scope of the corresponding specific process.

Here are some examples of poor top\-level code: importing a heavyweight module in the top\-level code, establishing a database connection (such as using Airflow Variables, which reads the corresponding variable values from the database), making HTTP requests, and so on. These pieces of code are unrelated to the DAG structure, yet they significantly increase processing time when the Scheduler parses and updates the DAG structure.

The following are two official examples for illustration:

<span id="_2-3-1-反例"></span>
#### 2.3.1 Bad example

```python
from datetime import datetime

from airflow import DAG
from airflow.operators.python import PythonOperator

import numpy as np  # <-- THIS IS A VERY BAD IDEA! DON'T DO THAT!

with DAG(
    dag_id="example_python_operator",
    schedule_interval=None,
    start_date=datetime(2021, 1, 1),
    catchup=False,
    tags=["example"],
) as dag:

    def print_array():
        """Print Numpy array."""
        a = np.arange(15).reshape(3, 5)
        print(a)
        return a

    run_this = PythonOperator(
        task_id="print_the_context",
        python_callable=print_array,
    )
```


<span id="_2-3-2-正例"></span>
#### 2.3.2 Good example

```python
from datetime import datetime

from airflow import DAG
from airflow.operators.python import PythonOperator

with DAG(
    dag_id="example_python_operator",
    schedule_interval=None,
    start_date=datetime(2021, 1, 1),
    catchup=False,
    tags=["example"],
) as dag:

    def print_array():
        """Print Numpy array."""
        import numpy as np  # <- THIS IS HOW NUMPY SHOULD BE IMPORTED IN THIS CASE

        a = np.arange(15).reshape(3, 5)
        print(a)
        return a

    run_this = PythonOperator(
        task_id="print_the_context",
        python_callable=print_array,
    )
```


<span id="_2-4-简化dag"></span>
### 2.4 Simplify the DAG

Although Airflow has undergone many performance optimizations and is designed as a scheduling component that can support the execution of many DAGs and tasks, fundamentally, whether an Airflow service can operate efficiently still depends on the actual workload, that is, the complexity of the DAGs being scheduled and executed in Airflow.

There is no clear metric to define whether a DAG is simple enough. Essentially, DAGs should be viewed like any other Python code file, and there are some general principles for evaluating whether the code quality is high enough. From the perspective of Airflow itself, there are some specific principles that can guide us in writing more streamlined DAG source files:


1. As mentioned earlier in [2.3 Correctly write DAG top-level code](https://docs.byteplus.com/docs/E-MapReduce/109187#jump), the top\-level code design of a DAG file should only relate to structure definition.

2. When defining workflow logic, it is best to keep it as linear as possible, such as the `A->B->C` structure, and avoid complex branching systems. This can significantly improve Airflow's scheduling performance, both during parsing and in the actual scheduling and execution phases.

3. Whenever possible, keep one file corresponding to one DAG. In Airflow 2.x, there are specific optimizations for scenarios where multiple DAG objects are defined in a single source file. However, it is still considered best practice to split multiple DAG objects into their own separate files. This approach reduces the parsing time for each file and allows their processing to be distributed across multiple FileProcessors, enabling parallel processing that can reduce overall processing time.


<span id="_3-场景说明"></span>
## 3 Scenario note


1. During operation, your production cluster may generate a formatted data file named stu.txt under certain scenarios, which is persisted in the cluster's HDFS, but the exact time of generation is uncertain.

2. When stu.txt exists, it needs to be loaded into a Hive table as the data source before processing.

3. The loaded data needs to be read by Spark for further transformation and processing.


<span id="_4-具体实现"></span>
## 4 Implementation details

<span id="_4-1-数据源"></span>
### 4.1 Data source

```python
101,'CAI',3RD,'USA',usa
102,'ANTO',10TH,'ENGLAND',usa
103,'PRABU',2ND,'INDIA',usa
104,'KUMAR',4TH,'USA',usa
105,'JEKI',2ND,'INDIA',usa
```


<span id="_4-2-过程"></span>
### 4.2 Process


1. Detection and reading of the data file

   This requirement calls for the use of HdfsSensor to detect whether a specific file exists in HDFS.

2. Parsing and loading into the Hive table

   HiveOperator is used here to create the table and perform the load operation.

3. Spark reading and transformation

   Based on the loaded data source, Spark tasks can be executed for processing, using SparkSqlOperator and SparkSubmitOperator.


```python
from airflow import DAG
from airflow.operators.bash import BashOperator
from airflow.providers.apache.hdfs.sensors.hdfs import HdfsSensor
from airflow.providers.apache.hive.operators.hive import HiveOperator
from airflow.providers.apache.spark.operators.spark_submit import SparkSubmitOperator
from airflow.providers.apache.spark.operators.spark_sql import SparkSqlOperator
from airflow.utils.dates import days_ago

args = {
    'owner': 'airflow',
}

with DAG(
    dag_id='emr_etl_case',
    default_args=args,
    schedule_interval='30 10 * * *',
    start_date=days_ago(2),
    tags=['example'],
) as dag:

    prepare_file = BashOperator(
        task_id='raw_file_generate',
        bash_command='''
cat << EOF > ~/stu.txt
101,'CAI',3RD,'USA',usa
102,'ANTO',10TH,'ENGLAND',usa
103,'PRABU',2ND,'INDIA',usa
104,'KUMAR',4TH,'USA',usa
105,'JEKI',2ND,'INDIA',usa
EOF
'''
    )
    
    put_file = BashOperator(
        task_id='put_into_hdfs',
        bash_command = '''hadoop dfs -put -f ~/stu.txt /'''
    )
    
    file_sensor = HdfsSensor(
        filepath="/stu.txt",
        task_id='detect_raw_file',
        hdfs_conn_id='hdfs_conn_id',
        poke_interval=10,
        timeout=5
    )
    
    table_create = HiveOperator(
        task_id='create_table_case',
      hive_cli_conn_id='hiveserver2_emr',
        schema='default',
        hql='''create table if not exists student( std_id int,std_name string,std_grade string,std_addres string) partitioned by (country string) row format delimited fields terminated by ',';
        '''
    )
    
    load_data = HiveOperator(
        task_id='load_data_case',
      hive_cli_conn_id='hiveserver2_emr',
        schema='default',
        hql='''load data inpath '/stu.txt' into table student partition(country='usa');
        '''
    )
    
    spark_sql_case = SparkSqlOperator(
        task_id='spark_case',
        sql='''select * from student;
        ''',
        master='yarn',
        name='airflow-spark-sql-select'   
    )
    
    #spark_submit_case = SparkSubmitOperator(
        
    #)
    
prepare_file >> put_file >> file_sensor >> table_create >> load_data >> spark_sql_case
```


<span id="_5-测试"></span>
## 5 Testing

To deploy a DAG in production, the corresponding testing is essential. Airflow provides a variety of testing methods to evaluate a DAG's production readiness from multiple dimensions.

<span id="_5-1-dag-loader-测试"></span>
### 5.1 DAG Loader testing

This is the most basic test. After each DAG is written, it must first be confirmed whether it can be correctly recognized by Airflow. In an environment consistent with actual Airflow operation (such as the corresponding venv environment), run

```shell
python my_dag.py
```


to quickly check the DAG file.

If combined with the built\-in Linux time tool, you can also measure the parsing time of the DAG file. This result can be used to verify the effect before and after optimizing the DAG code file.

```shell
time python my_dag.py
```


This testing method will start an additional interpreter, which is unnecessary overhead during Airflow runtime. By adding the `-c` option, you can obtain parsing time that is closer to the actual runtime.

```shell
time python -c my_dag.py
```


<span id="_5-1-1-dag-loader-的单元测试示例"></span>
#### 5.1.1 Unit test example for DAG Loader

```python
import pytest

from airflow.models import DagBag


@pytest.fixture()
def dagbag(self):
    return DagBag()


def test_dag_loaded(self, dagbag):
    dag = dagbag.get_dag(dag_id="emr_etl_case")
    assert dagbag.import_errors == {}
    assert dag is not None
    assert len(dag.tasks) == 6
```


<span id="_5-2-测试-dag-的-dag"></span>
### 5.2 DAG for testing DAGs

This may sound a bit strange, but it is indeed a viable approach. In our actual workflows, we may use many modules from Providers offered by the Airflow community. There is not much need to conduct unit tests for these modules, as the community has already provided assurances.

At this point, what we care about is whether the Tasks organized using the corresponding Operators and other modules actually run as expected. We can write a separate DAG for this kind of task execution. After the corresponding Task runs, there will be a subsequent Task responsible for checking (such as various Sensors).

**Example:** 

```python
put_file_in_hdfs = BashOperator(...)

file_sensor = HdfsSensor(
        filepath="/your_expect_path",
        task_id='detect_file',
        hdfs_conn_id='hdfs_conn_id',
        poke_interval=10,
        timeout=5
    )
    
put_file_in_hdfs >> file_sensor
```


<span id="_5-3-预发布环境测试"></span>
### 5.3 Pre\-release environment testing

To fully test and run DAG files before going live, it is best to have a pre\-release environment aligned with the production environment. To support multi\-environment operation, it is best to ensure that all environment\-related operations in the DAG, such as parameter reading, are parameterized rather than hard\-coded, so that switching between environments does not require modifying the code definitions in the DAG.

```python
import os


deployment = os.environ.get("DEPLOYMENT", "PROD")
```


<span id="_6-airflow-扩容适配"></span>
## 6 Airflow scaling adaptation

<span id="_6-1-背景"></span>
### 6.1 Background

For Airflow workflows to run properly, the machines participating in scheduling must hold the DAG files corresponding to those workflows. In scenarios such as elastic scaling, for newly added nodes, if there are Airflow Worker components on them, workflow file distribution is required. Otherwise, workflows scheduled to those nodes will fail to run.

<span id="_6-2-解决方案"></span>
### 6.2 Solution

For node scaling, EMR provides the [Guided operations](https://docs.byteplus.com/docs/E-MapReduce/105420) capability, allowing scripts to be executed before and after component deployment when new nodes are added. We can adopt a post\-deployment strategy to obtain workflow files on new nodes.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fdc94c4ed1615d87169b3e30e02b686d.png) </span>

Here is a script for defining a synchronous workflow for your reference:

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39876cf955bffa3d26a0bb35e82ae87f.sh" name="airflow_extend.sh">airflow_extend.sh</Attachment>


```bash
#!/usr/bin/env bash

# Assume that all your workflow definitions are on the emr-master-1 machine, and the dag_folder is configured as /usr/lib/emr/current/airflow/dags
mkdir /usr/lib/emr/current/airflow/dags
scp -o "StrictHostKeyChecking no" -r emr-master-1:/usr/lib/emr/current/airflow/dags/* /usr/lib/emr/current/airflow/dags
chown -R airflow:airflow /usr/lib/emr/current/airflow/dags
```
