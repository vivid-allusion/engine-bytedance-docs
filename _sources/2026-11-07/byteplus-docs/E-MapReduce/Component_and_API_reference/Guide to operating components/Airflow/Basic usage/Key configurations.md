---
title: "Key configurations"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Key_configurations"
---

You can easily and conveniently modify Airflow runtime configurations through the E\-MapReduce (EMR) console (for details, see: [Manage service configuration parameters](https://docs.byteplus.com/docs/E-MapReduce/105412)), and this article introduces several key Airflow configurations.


|**Module** |**Parameter** |**Description** |
|---|---|---|
|**core** |**dags_folder** |Defines the directory from which Airflow reads DAG files. |
||**plugins_folder** |Defines the directory from which Airflow reads plugin files. |
||**default_timezone** |Default time zone setting. Supports IANA time zone identifiers.<br><br>The default value is Asia/Shanghai. |
||**parallelism** |The maximum number of tasks that can run concurrently across Airflow globally.<br><br>The default value is 32. |
||**max_active_runs_per_dag** |Defines the maximum number of DAG Runs that can be triggered simultaneously for a single DAG.<br><br>The default value is 16. |
||**max_active_tasks_per_dag** |Defines the maximum number of task instances that can run simultaneously for a single DAG.<br><br>The default value is 16. |
||**default_task_retries** |Defines the maximum number of retries for a task. Can be defined separately at the DAG and Task levels.<br><br>The default value is 0. |
|**scheduler** |**parsing_processes** |Controls how many Scheduler processes Airflow can use to concurrently parse DAG files.<br><br>The default value is 2. |
||**catchup_by_default** |Controls whether the Scheduler performs backfill operations between the current time and the DAG's start_date. This value does not affect backfill performed via the command line.<br><br>The default value is true. |
||**dag_dir_list_interval** |Defines how often the Scheduler scans the DAGs directory to discover new files.<br><br>The default value is 300 seconds. |
||**min_file_process_interval** |Controls how often parsed DAG files are re\-parsed for updates. If the interval is too short, it will significantly increase system load.<br><br>The default value is 30 seconds. |
||**scheduler_zombie_task_threshold** |Running tasks periodically report heartbeats to the database. This parameter controls how long a task can go without reporting to the database before the Scheduler marks it as failed and reschedules it.<br><br>The default value is 300 seconds. |
|**celery** |**worker_concurrency** |This property takes effect when you start a worker using the `airflow celery worker` command. It defines the number of task instances the worker will acquire and starts a fixed number of worker threads accordingly. When you have sufficient understanding of the workload, you can use this parameter to define a fixed thread count to avoid dynamic scaling.<br><br>The default value is 16. |
||**worker_autoscale** |Defines the upper and lower limits of the celery worker thread pool in the format `{{max_concurrency}},{{min_concurrency}}`. Celery will maintain at least the minimum number (min_concurrency) of threads and dynamically scale based on task load. If this value is defined, the worker_concurrency configuration will be ignored.<br><br>The default value is "", example value is "16,12". |
|**webserver** |**default_ui_timezone** |Specifies the default time zone for displaying all data in the UI. Supports IANA time zone strings.<br><br>The default is Asia/Shanghai. If not specified, it will be consistent with `default_timezone`. |
||**page_size** |Uniformly controls the number of entries displayed in all list views on the Airflow UI. |
||**default_dag_run_display_number** |Controls the number of DAG Runs displayed in the UI. |


For a complete description of Airflow component configurations, refer to the official documentation: [Configuration Reference](https://airflow.apache.org/docs/apache-airflow/2.2.0/configurations-ref.html).
