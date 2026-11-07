---
title: "FAQs and important notes"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/FAQs_and_important_notes"
---

<span id="_1-常见问题"></span>
## 1 FAQs

The following are some FAQs you may encounter when using Airflow.


* Q1: Why is the newly added DAG file not displayed on the page?

* Q2: What important notes should be considered when modifying a DAG?

* Q3: How can I troubleshoot failed tasks?

* Q4: How do I manually restart a failed DAG Run?

* Q5: What should I do if I cannot see logs for a TaskInstance?

* Q6: How can I adjust Airflow's concurrency and behavior mode?

* Q7: How to optimize Airflow UI for slow loading?

* Q8: How should I define utility class logic that is reused across DAGs?


<span id="q1：新加入的-dag-文件为什么页面上没有展示？"></span>
### Q1: Why is the newly added DAG file not displayed on the page?

Airflow determines the interval for parsing new DAG files from the system directory based on the value defined by the `dag_dir_list_interval` parameter. This value is in seconds, with a default of 300.

If the DAG does not appear after the specified interval, please contact us via [ticket](https://console.volcengine.com/workorder/create?step=2&SubProductID=P00000203).

<span id="q2：需要对-dag-做修改，我应该注意什么？"></span>
### Q2: What important notes should be considered when modifying a DAG?

Airflow refreshes updates to already parsed DAG files based on the interval specified by the `min_file_process_interval` configuration. It is recommended to ensure that no tasks are running in the DAG during updates to avoid conflicts between execution and updates.

When the corresponding DAG code file changes while the DAG is running, here are some scenarios for your reference:


* If you delete a Task from the DAG while it is running, Airflow will set it to the "removed" state and print the following log: `State of this instance has been externally set to removed.` `Taking the poison pill.`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8e8dabcef12dae1c691610c70b64db3.png) </span>

* If you add a Task to the DAG, after Airflow refreshes, this step will be visible in the UI, and subsequent DAG Runs will execute the step. Historical DAG Runs will be displayed according to the new DAG definition, but the execution status for the newly added Task will be empty.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8939ec5c4d1838ac80d2abd67a4f1098.png) </span>

* If you modify the logic of a Task in the DAG, this change will apply to TaskInstances that have not yet been executed or completed.


In principle, it is generally not recommended to modify the definition of a DAG. A better approach is to create a new DAG file to implement the new workflow, and then disable the old DAG as needed to stop its scheduling.

<span id="q3：怎么排查执行失败的任务？"></span>
### Q3: How do I troubleshoot failed tasks?


1. Go to the Airflow UI **DAGs** page. In the DAG list, find the Runs for the corresponding DAG, click the red\-marked run, and enter the DAG Runs List for failed executions of that DAG.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7f17df40ae06ec537a7001dad3eb0ac1.png) </span>

2. In this list, locate the specific failed DAG Run. Click the DAG id to enter the DAG details page, where you will arrive at the Graph subpage. This page displays a diagram of the DAG Run, with each box representing a specific TaskInstance.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d93d42e12d143168e721f9046f5a333~tplv-goo7wpa0wc-image.image) </span>

3. Click the specific failed Task, then click Log in the popup window to view the logs.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7c3b82b36f2c324d579ad4f556803205.png) </span>


<span id="q4：如何手动重启失败的-dag-run？"></span>
### Q4: How do I manually restart a failed DAG Run?


1. Go to the Airflow UI **DAGs** page. In the DAG list, find the Runs for the corresponding DAG, click the red\-marked run, and enter the DAG Runs List for failed executions of that DAG.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfd2d09200aa526746a5bdb5ebaa1927.png) </span>

2. In this list, locate the specific failed DAG Run, select it, and then click Clear. The Scheduler will treat this DAG Run as if it has not been run, and will reschedule it for execution.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ae9a166a9eeaad691f5883a00603175.png) </span>


<span id="q5：taskinstance-看不到日志，我应该怎么办？"></span>
### Q5: What should I do if TaskInstance logs are not visible?

In certain cases, you may encounter the error shown below when viewing logs. Please try the following solutions:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a78f576f6e7f2a290c28898ee1a925de.png) </span>


* **Refer to the previous instructions and manually restart the DAG Run.** 

* **Check whether each machine in the cluster has the DAG file for this scheduling run.** 

   EMR deploys the Airflow Worker process on every machine in the cluster. All machines participating in scheduling must have the DAG source file locally; otherwise, the issue described above will occur. For DAG distribution, refer to [快速开始-步骤三](https://docs.byteplus.com/docs/E-MapReduce/109183#%E6%AD%A5%E9%AA%A4%E4%B8%89%EF%BC%9A-%E4%B8%8A%E4%BC%A0-dag-%E6%96%87%E4%BB%B6).

* **Submit a support ticket to contact us.** 

   If the issue cannot be resolved after following the above troubleshooting steps, please contact us. Our developers will provide one\-on\-one support.


<span id="q6：怎么调整-airflow-运行的并发度与行为模式？"></span>
### Q6: How do I adjust Airflow concurrency and execution mode?


* There are three key global configurations in Airflow that define cluster\-wide and DAG\-level concurrency, and determine the number of Worker processes.

   * [parallelism](https://airflow.apache.org/docs/apache-airflow/2.2.0/configurations-ref.html#config-core-parallelism)

   * [max_active_tasks_per_dag](https://airflow.apache.org/docs/apache-airflow/2.2.0/configurations-ref.html#config-core-max-active-tasks-per-dag)

   * [max_active_runs_per_dag](https://airflow.apache.org/docs/apache-airflow/2.2.0/configurations-ref.html#config-core-max-active-runs-per-dag)

      Relevant descriptions can be found in the documentation [Key configurations](https://docs.byteplus.com/docs/E-MapReduce/109191).

* When defining DAGs, there are parameters that can improve concurrency performance:

   * `max_active_tasks`: Overrides [max_active_tasks_per_dag](https://airflow.apache.org/docs/apache-airflow/2.2.0/configurations-ref.html#config-core-max-active-tasks-per-dag).

   * `max_active_runs`: Overrides [max_active_runs_per_dag](https://airflow.apache.org/docs/apache-airflow/2.2.0/configurations-ref.html#config-core-max-active-runs-per-dag).

* When defining Operators/Tasks, there are also parameters to adjust concurrency and determine priority:

   * `max_active_tis_per_dag`: This parameter defines the overall concurrency of this task across **all** DAG Runs.

   * `pool`: See [Pools](https://airflow.apache.org/docs/apache-airflow/2.2.0/concepts/pools.html#concepts-pool). In Airflow, Pools define the maximum overall concurrency for Tasks running within them, allowing users to categorize and adjust according to the actual load of the destination system.

   * `priority_weight`: See [Priority Weights](https://airflow.apache.org/docs/apache-airflow/2.2.0/concepts/priority-weight.html#concepts-priority-weight). The priority policy in Airflow by default supports three strategies: upstream priority, downstream priority, and absolute value.


<span id="q7：airflow-ui-加载慢怎么调优？"></span>
### Q7: How to optimize slow loading of the Airflow UI?


* To reduce the loading time of your Airflow UI homepage, you can lower the value of the `page_size` configuration. This setting uniformly controls the number of entries displayed in all list views on the Airflow UI.

* To improve the loading speed of your DAG details page, you can lower the value of the `default_dag_run_display_number` configuration. This controls the number of DAG Runs displayed in the UI.


<span id="q8：如何定义一些跨-dag-复用的逻辑？"></span>
### Q8: How to define logic that can be reused across DAGs?

In Airflow, the DAG file directory is added to the module search path, and the Scheduler scans this directory for DAG file updates. Therefore, you can directly add utility modules or corresponding packages in this directory for management. These packages and modules can be used directly in DAG definitions.

Finally, do not forget to add the path information for the corresponding modules or packages to the .airflowignore file (supports relative paths and wildcards), so the scheduler will ignore these utilities when searching for DAGs.

<span id="_2-注意事项"></span>
## 2 Important notes

<span id="_2-1-数据库要求"></span>
### 2.1 Database requirements

Airflow deployed in EMR is version 2.2.0, leveraging its out\-of\-the\-box Scheduler HA to provide a highly available and high\-performance experience. In this scenario, the official recommendation is to use a database version of **MySQL8.0+**  or higher, because the new version of Airflow utilizes advanced statements such as `NOWAIT` and `SKIP LOCKED` when deploying multiple Schedulers.

The **built\-in** MySQL database version already meets this requirement, but **does not** offer a high availability guarantee. You can use the **RDS** product to provide a highly available database for the cluster, but you need to **ensure yourself** that the RDS database version is sufficiently high.
