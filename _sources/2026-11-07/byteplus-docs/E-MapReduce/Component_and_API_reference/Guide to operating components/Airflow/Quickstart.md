---
title: "Quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/component_quick_start"
---

This article introduces how to quickly use the Airflow component for workflow scheduling through the Volcano Engine E\-MapReduce (EMR) console.

<span id="步骤一：-服务引入"></span>
## Step 1: Service integration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When creating an EMR cluster, Airflow service capabilities are available in the following three types of clusters: Hadoop, Presto, and Trino.</div>



* If you have not created a cluster, select the Airflow service when creating an EMR Hadoop, Presto, or Trino cluster type. For details on cluster creation, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

* For existing clusters, if the Airflow component is not listed in the service list, you can add Airflow by using the add service feature. For detailed operations, refer to: [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409).

   After the cluster service is successfully created, you can see Airflow in the **Cluster Details \> Service List**.


<span id="步骤二：-dag文件编写"></span>
## Step 2: Write the DAG file

After integrating the Airflow service, you need to create workflows programmatically so that Airflow can serve you.

Here is an official sample DAG that can be started and run without any additional dependencies, allowing you to quickly get started.

```python
"""
### Tutorial Documentation
Documentation that goes along with the Airflow tutorial located
[here](https://airflow.apache.org/tutorial.html)
"""
# [START tutorial]
# [START import_module]
from datetime import datetime, timedelta
from textwrap import dedent

# The DAG object; we'll need this to instantiate a DAG
from airflow import DAG

# Operators; we need this to operate!
from airflow.operators.bash import BashOperator

# [END import_module]


# [START instantiate_dag]
with DAG(
    'tutorial',
    # [START default_args]
    # These args will get passed on to each operator
    # You can override them on a per-task basis during operator initialization
    default_args={
        'depends_on_past': False,
        'email': ['airflow@example.com'],
        'email_on_failure': False,
        'email_on_retry': False,
        'retries': 1,
        'retry_delay': timedelta(minutes=5),
        # 'queue': 'bash_queue',
        # 'pool': 'backfill',
        # 'priority_weight': 10,
        # 'end_date': datetime(2016, 1, 1),
        # 'wait_for_downstream': False,
        # 'sla': timedelta(hours=2),
        # 'execution_timeout': timedelta(seconds=300),
        # 'on_failure_callback': some_function,
        # 'on_success_callback': some_other_function,
        # 'on_retry_callback': another_function,
        # 'sla_miss_callback': yet_another_function,
        # 'trigger_rule': 'all_success'
    },
    # [END default_args]
    description='A simple tutorial DAG',
    schedule_interval=timedelta(days=1),
    start_date=datetime(2021, 1, 1),
    catchup=False,
    tags=['example'],
) as dag:
    # [END instantiate_dag]

    # t1, t2 and t3 are examples of tasks created by instantiating operators
    # [START basic_task]
    t1 = BashOperator(
        task_id='print_date',
        bash_command='date',
    )

    t2 = BashOperator(
        task_id='sleep',
        depends_on_past=False,
        bash_command='sleep 5',
        retries=3,
    )
    # [END basic_task]

    # [START documentation]
    t1.doc_md = dedent(
        """\
    #### Task Documentation
    You can document your task using the attributes `doc_md` (markdown),
    `doc` (plain text), `doc_rst`, `doc_json`, `doc_yaml` which gets
    rendered in the UI's Task Instance Details page.
    ![img](http://montcs.bloomu.edu/~bobmon/Semesters/2012-01/491/import%20soul.png)
    """
    )

    dag.doc_md = __doc__  # providing that you have a docstring at the beginning of the DAG
    dag.doc_md = """
    This is a documentation placed anywhere
    """  # otherwise, type it like this
    # [END documentation]

    # [START jinja_template]
    templated_command = dedent(
        """
    {% for i in range(5) %}
        echo "{{ ds }}"
        echo "{{ macros.ds_add(ds, 7)}}"
        echo "{{ params.my_param }}"
    {% endfor %}
    """
    )

    t3 = BashOperator(
        task_id='templated',
        depends_on_past=False,
        bash_command=templated_command,
        params={'my_param': 'Parameter I passed in'},
    )
    # [END jinja_template]

    t1 >> [t2, t3]
# [END tutorial]
```


<span id="步骤三：-上传-dag-文件"></span>
## Step 3: Upload the DAG file

After you finish writing the DAG file, you need to submit the code file to the cluster so that Airflow can discover the workflow.

You can proceed as follows:


1. After developing the DAG, there are multiple ways to upload it:

   1. You can bind the cluster machine to a public network, then use a command\-line tool or terminal on your local machine to upload the code file to the cluster.

   2. If the public network is not enabled, you can also log in to the machine using ECS Terminal. For details, see: [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404)  **.**  After logging in, use a text editor in the system to save your code as a py file and place it on the cluster node.

2. Assuming the code exists as a file in the cluster and is named `test.py`, you then need to place the file in the DAG directory specified by Airflow. You can configure this directory location through the `dags_folder` service parameter in the Airflow component.

   EMR provides a convenient command in the system, `dagdispatch`, which is used to quickly distribute a file to a specified directory on all machines in the cluster (the directory must exist in advance).

   The usage format is `dagdispatch [dag_file_path] [dags_folder_path]`. If you have not changed the system default `dags_folder` configuration, then the path is optional; otherwise, you need to provide your custom directory as the second parameter.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The dags_folder component configuration parameter supports customization only in EMR\-1.3.x and later versions. In versions prior to 1.3.x, the default specified path is: /usr/lib/emr/current/airflow/home/dags.</div>


<span id="步骤四：-进入-airflow-服务-ui-操作"></span>
## Step 4: Access the Airflow service UI for operation

After you have successfully uploaded the DAG file, you can then access the built\-in Airflow WebUI to start the workflow and view the running status on the page. For details on accessing the built\-in UI of the service component, see: [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).

After entering the Airflow UI, the homepage will list all runnable DAGs that have been successfully parsed by Airflow. If you are using the example DAG, you will see a row named `tutorial` in the interface. Trigger it to start scheduling.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30b7ec0a300aa13ef50e05ba3be9acb7.png) </span>

In some cases, you may not see this DAG on the interface temporarily. For more information, see [FAQs and important notes](https://docs.byteplus.com/docs/E-MapReduce/109184).

<span id="步骤五：-查看-dag-运行状态"></span>
## Step 5: View the DAG running status

The Airflow UI provides full lifecycle management for DAG runs. When a workflow starts scheduling, Airflow provides key information, running status, and execution logs for both DAG Runs and Tasks:


1. DAG homepage overview

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8700569ec3c292e4cfade484118babb7.png) </span>

2. View execution logs

   Logs are generated during the execution of each Task (step). This execution is called a TaskInstance. To view logs, you also need to locate a specific TaskInstance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_128cb5de4e3c2d13b5e6cbbdc2046f63.png) </span>


For the complete content about the Airflow UI, see: [official documentation](https://airflow.apache.org/docs/apache-airflow/2.2.0/ui.html).
