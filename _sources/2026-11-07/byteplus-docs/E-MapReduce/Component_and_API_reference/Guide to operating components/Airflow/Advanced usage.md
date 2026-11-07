---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/airflow_Advanced_usage"
---

This chapter guides you through several topics to help you write DAG source files that better meet your requirements.

<span id="_1-dag-控制流"></span>
## 1 DAG control flow

In actual production environments, workflows are often non\-linear and require handling a variety of branching scenarios. Airflow generally provides four main methods for controlling flow, which are explained below.

<span id="_1-1-branching-operator"></span>
### 1.1 Branching Operator

Airflow provides a `BranchPythonOperator`, which accepts a `python_callable`. This function must return a `task_id` (or a list of `task_id`) to determine which specific branch or branches the current workflow should follow during subsequent execution.

Important: The `BranchPythonOperator` must be the direct upstream of each sub\-branch, or, in other words, the `python_callable` must return a `task_id` that is its direct downstream.

In a branching system, there may be cases where a task is the downstream of both the branch operator and one or more selected tasks. In such cases, even if the task is not selected by the branch operator, as long as other conditions are met, the task will still be executed.

```python
from datetime import datetime

from airflow.decorators import dag
from airflow.operators.dummy import DummyOperator
from airflow.operators.python import BranchPythonOperator


@dag(schedule_interval=None, start_date=datetime(2022, 9, 14), catchup=False, tags=['example'])
def demo_dag():
    start = DummyOperator(task_id="start")

    def get_selected_tasks():
        return "branch_a"

    branching = BranchPythonOperator(
        task_id="branching",
        python_callable=get_selected_tasks
    )

    task_a = DummyOperator(task_id="branch_a")

    task_after_a = DummyOperator(task_id="after_a")

    task_b = DummyOperator(task_id="branch_b")

    join = DummyOperator(task_id="join")

    start >> branching
    branching >> task_a >> task_after_a >> join
    branching >> join
    branching >> task_b


dag = demo_dag()
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9f0e9e766db7ff78303346ec42cecdd3.png) </span>

In the above sample code, our branching task did not select the join task, but since it is the direct downstream of after_a, it was still executed.

<span id="_1-1-1-basebranchoperator"></span>
#### 1.1.1 BaseBranchOperator

To implement your own branching operator logic, you can inherit from `BaseBranchOperator` and provide an implementation for the `choose_branch` method.

This is similar to the method previously provided to `BranchPythonOperator`. The implemented `choose_branch` should also return one or more `task_id`, and any tasks outside this range will be skipped.

<span id="_1-2-depends-on-past"></span>
### 1.2 Depends On Past

This mode applies to a special scenario where the execution of a task depends on the result of the same task in the previous DAG run. The task will only be executed in the current schedule if it succeeded in the previous run. To use this feature, set `depends_on_past` to True when defining the corresponding task.

When the DAG is executed for the first time, since there is no previous run to reference, Airflow will execute the task directly.

<span id="_1-3-only-latest"></span>
### 1.3 Only Latest

In many cases, within the context of the DAG we are running, its date may be some time in the past. To schedule certain tasks only for the most recent run based on the current time, use `LatestOnlyOperator`. For example, when migrating a DAG from a previous Airflow environment to a new one, the start_date defined in the DAG may be a long time ago.

`LatestOnlyOperator` will automatically skip all its downstream tasks when the current DAG Run is not the latest.

```python
import datetime

from airflow import DAG
from airflow.operators.dummy import DummyOperator
from airflow.operators.latest_only import LatestOnlyOperator
from airflow.utils.trigger_rule import TriggerRule

with DAG(
    dag_id='latest_only_with_trigger',
    schedule_interval=datetime.timedelta(hours=6),
    start_date=datetime.datetime(2022, 9, 1),
    catchup=True,
    tags=['example3'],
) as dag:
    latest_only = LatestOnlyOperator(task_id='latest_only')
    task1 = DummyOperator(task_id='task1')
    task2 = DummyOperator(task_id='task2')
    task3 = DummyOperator(task_id='task3')
    task4 = DummyOperator(task_id='task4', trigger_rule=TriggerRule.ALL_DONE)

    latest_only >> task1 >> [task3, task4]
    task2 >> [task3, task4]
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f1f4560de2efd79d8b7e5158d0e51e4.png) </span>

<span id="_1-4-trigger-rules"></span>
### 1.4 Trigger Rules

By default, a task will only run when all its upstream tasks have succeeded, but this behavior can be changed. Airflow provides many trigger rules to offer flexibility.

All trigger_rule options are as follows:


* all_success: Default value. Requires all upstream tasks to succeed.

* all_failed: Requires all upstream tasks to be in `failed` or `upstream_failed` status.

* all_done: All upstream tasks have completed their respective executions.

* one_failed: At least one upstream task has failed. Does not require waiting for all upstream tasks to finish.

* one_success: At least one upstream task has succeeded. Does not require waiting for all upstream tasks to finish.

* none_failed: All upstream tasks have either succeeded or been skipped.

* none_failed_min_one_success: At least one upstream task has succeeded, and none have failed.

* none_skipped: No upstream tasks have been skipped.

* always: No upstream dependencies. Can be scheduled for execution at any time.


Using together with Depends On Past allows for greater flexibility.

When using all_success or all_failed, if combined with a branching operator, it may cause tasks to be skipped in a cascading manner, as shown below:

```python
from datetime import datetime

from airflow.decorators import dag
from airflow.operators.dummy import DummyOperator
from airflow.operators.python import BranchPythonOperator


@dag(schedule_interval=None, start_date=datetime(2022, 9, 14), catchup=False, tags=['example'])
def demo_dag_c():
    start = DummyOperator(task_id="start")

    def get_selected_tasks():
        return "branch_a"

    branching = BranchPythonOperator(
        task_id="branching",
        python_callable=get_selected_tasks
    )

    task_a = DummyOperator(task_id="branch_a")

    task_after_a = DummyOperator(task_id="after_a")

    task_b = DummyOperator(task_id="branch_b")

    join = DummyOperator(task_id="join")

    start >> branching
    branching >> task_a >> task_after_a >> join
    branching >> join
    branching >> task_b >> join


dag = demo_dag_c()
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_277aa5c70144b40fc0f2a1a972ffdbb0.png) </span>

If we simply modify the trigger_rule for join, for example, changing it to none_failed_min_one_success, join can then be scheduled.

```python
from datetime import datetime

from airflow.decorators import dag
from airflow.operators.dummy import DummyOperator
from airflow.operators.python import BranchPythonOperator
from airflow.utils.trigger_rule import TriggerRule


@dag(schedule_interval=None, start_date=datetime(2022, 9, 14), catchup=False, tags=['example2'])
def demo_dag_d():
    start = DummyOperator(task_id="start")

    def get_selected_tasks():
        return "branch_a"

    branching = BranchPythonOperator(
        task_id="branching",
        python_callable=get_selected_tasks
    )

    task_a = DummyOperator(task_id="branch_a")

    task_after_a = DummyOperator(task_id="after_a")

    task_b = DummyOperator(task_id="branch_b")

    join = DummyOperator(task_id="join", trigger_rule=TriggerRule.NONE_FAILED_MIN_ONE_SUCCESS)

    start >> branching
    branching >> task_a >> task_after_a >> join
    branching >> join
    branching >> task_b >> join


dag = demo_dag_d()
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_16e7864985c11376978f7d3124eccffb.png) </span>

<span id="_2-dag-可视化定义"></span>
## 2 DAG visualization definitions

In Airflow, there are two ways to visualize a DAG: one is through the Airflow UI, and the other is by using the command line `airflow dags show {dag_id}` to obtain the corresponding digraph structure. It is recommended to view Airflow workloads in the UI, as it is more user\-friendly. In addition to the graphical display, all key data can be easily accessed.

As business grows, the corresponding DAG logic may become increasingly complex. At this point, you may want to customize and add notes to the DAG logic diagram. Here are two main approaches:

<span id="_2-1-任务分组"></span>
### 2.1 Task grouping

If certain tasks can be logically grouped together, you can use grouping. These groups support collapsing in the UI, which effectively reduces the complexity of the logic diagram. This is purely a UI concept; tasks within the group remain within the context of the DAG.

```python
with TaskGroup("group1") as group1:
    task1 = DummyOperator(task_id="task1")
    task2 = DummyOperator(task_id="task2")

task3 = DummyOperator(task_id="task3")

group1 >> task3
```


At the group level, you can pass in default_args to override parts of the global DAG definition.

```python
with DAG(dag_id='dag1', default_args={'scope': 'DAG'}) as dag:

    with TaskGroup("group1", default_args={'scope': 'group1'}) as group1:
        task1 = DummyOperator(task_id="task1")
        task2 = DummyOperator(task_id="task2")
    
    task3 = DummyOperator(task_id="task3")
    
    group1 >> task3
```


By default, the task_id for a task within a TaskGroup uses the group's group_id as a prefix. This ensures that tasks within the group have unique IDs. This behavior can be disabled by setting `prefix_group_id=False`.

<span id="_2-2-边的标签化"></span>
### 2.2 Edge labeling

If a DAG is sufficiently complex, especially with many branches, you may want to add descriptions to the edges extending from different branches for greater clarity, without needing to refer to the DAG code definition to understand the workflow.

You can directly insert a Label object between the `>>` and `<<` operators to describe the corresponding edge.

```python
from airflow.utils.edgemodifier import Label

my_task >> Label("When empty") >> other_task
```


If you define upstream and downstream relationships using object methods, you can use attributes to define them.

```python
from airflow.utils.edgemodifier import Label

my_task.set_downstream(other_task, Label("When empty"))
```


**Example**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5fd991a279b23b1d22f813b19140a38.png) </span>

<span id="_3-subdags"></span>
## 3 SubDAGs

In many cases, you may find similar task definitions across multiple DAGs and wish to extract these tasks for reuse in different DAGs. You can achieve this using SubDagOperator, which accepts a method that returns a DAG object. This DAG can contain an arbitrary number of methods, each with properties and usage independent of the external DAG. The following sections will explain these aspects in detail.

First, define a method that returns a set of task objects:

```python
from datetime import datetime

from airflow import DAG
from airflow.operators.dummy import DummyOperator


def subdag(parent_dag_name, child_dag_name, args):
    """
    Generate a DAG to be used as a subdag.

    :param str parent_dag_name: Id of the parent DAG
    :param str child_dag_name: Id of the child DAG
    :param dict args: Default arguments to provide to the subdag
    :return: DAG to use as a subdag
    :rtype: airflow.models.DAG
    """
    dag_subdag = DAG(
        dag_id=f'{parent_dag_name}.{child_dag_name}',
        default_args=args,
        start_date=datetime(2021, 1, 1),
        catchup=False,
        schedule_interval="@daily",
    )

    for i in range(5):
        DummyOperator(
            task_id=f'{child_dag_name}-task-{i + 1}',
            default_args=args,
            dag=dag_subdag,
        )

    return dag_subdag
```


Important: When defining dag_id and task_id here, prefixes are used. This is a good practice to keep IDs unique and self\-descriptive, avoiding confusion.

The DAG defined here must have a scheduling logic and be enabled. You must not set `schedule_interval` to `None` or `@once`; otherwise, during actual use, it will be directly set to the succeed state and nothing will be executed.

```python
from airflow import DAG
from airflow.example_dags.subdags.subdag import subdag
from airflow.operators.dummy import DummyOperator
from airflow.operators.subdag import SubDagOperator
from airflow.utils.dates import days_ago

DAG_NAME = 'example_subdag_operator'

args = {
    'owner': 'airflow',
}

with DAG(
    dag_id=DAG_NAME, default_args=args, start_date=days_ago(2), schedule_interval="@once", tags=['example']
) as dag:

    start = DummyOperator(
        task_id='start',
    )

    section_1 = SubDagOperator(
        task_id='section-1',
        subdag=subdag(DAG_NAME, 'section-1', args),
    )

    some_other_task = DummyOperator(
        task_id='some-other-task',
    )

    section_2 = SubDagOperator(
        task_id='section-2',
        subdag=subdag(DAG_NAME, 'section-2', args),
    )

    end = DummyOperator(
        task_id='end',
    )

    start >> section_1 >> some_other_task >> section_2 >> end
# [END example_subdag_operator]
```


In the main DAG, there are two SubDagOperator objects, and no duplicate tasks are defined additionally. Note that when creating a SubDAG object, the args from the external DAG are passed to the constructor method. This is a good practice for maintaining consistency between the internal and external environments.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ce3bf95749200cff998ea7fa5f29ca05.png) </span>

For a subDAG, after clicking, you can view the status of specific task instances within the DAG via the popup's `Zoom into Sub DAG` button.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3204719e983ad7b9e38b1daa4c472ae9.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a214ebc415b9a931f24edad92bc9de79.png) </span>

Clearing a SubDAG will also clear the status of all tasks within it.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fe9840275ad5719e1d7baac967d9e0f.png) </span>

It should be noted that for SubDAGs, there is no concept of Pool, so during execution, it may consume more resources than we have preset.

<span id="fe4a20d0"></span>
## 4 High availability access to other services within the cluster

This document mainly addresses the single point of failure issue when Airflow accesses other services within a high availability cluster.

In a high availability cluster, multiple component instances are deployed on different nodes, such as the Coordinator component of Presto. When you execute Presto jobs in Airflow, you expect Presto to handle single point failures and switch in real time to an available Presto Coordinator component instance. However, in practice, Airflow can only be configured with one Presto Coordinator address, which does not meet high availability requirements. The following uses Presto and Trino as examples, introducing the [load balancing](https://console.volcengine.com/clb) service on Volcano Engine to solve the high availability access issue. Other services can be addressed in a similar way.

<span id="bb71c558"></span>
### Preparation

First, you need to purchase or select an existing load balancing instance. This instance must be in the same VPC as your cluster, and its network type must be private.

<span id="503215bb"></span>
### High availability access configuration: Presto/Trino

Airflow by default accesses the first Presto/Trino Coordinator instance (master\-1\-1). If this Coordinator instance is unavailable, Airflow's execution of Presto tasks will fail. In this case, you need to use load balancing to route Airflow's traffic to an available Coordinator instance.


1. First, you need to identify the ECS instance where the Presto/Trino Coordinator is deployed. This can be found in the EMR console under Service List \- Deployment Topology.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e670cbfe79d48fba56f268df6e3aa56~tplv-goo7wpa0wc-image.image) </span>

2. Next, create a backend server group within the selected load balancer and add the corresponding ECS instances to this backend server group. The port used is the Coordinator's listening port, which can be obtained by querying the Presto/Trino service parameter `http-server.http.port` (if http\-server.https.enabled is set to true, check http\-server.https.port).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/279e715a40b54398babaa7dac95f3174~tplv-goo7wpa0wc-image.image) </span>

3. Then add a listener. Fill in the load balancing protocol (TCP) according to the Coordinator's configuration, select the backend server group you just created, and enable health checks. The health check path and timeout can be left as default values. (Caution: You need to allow the load balancer's network segment in the security group where the ECS instance resides; otherwise, health check failures and access issues may occur.)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f46a15fbe8224f4b819b5074a460c8cd~tplv-goo7wpa0wc-image.image) </span>

4. After creating the listener, you can configure the IP address of the above load balancer in Airflow. You need to log in to the Airflow WebUI and modify the Presto Connection configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c229825ac124446f94f64ad39a4b4bc4~tplv-goo7wpa0wc-image.image) </span>

5. Change the Host to the private/public IP address of the load balancer, then click Save.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to configure a private IP. If you have enabled the public network and there are no restrictions in the CLB allowlist or blocklist, you can also configure a public IP.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7f8487036b143a2a10b0d4d453a1fc0~tplv-goo7wpa0wc-image.image) </span>
