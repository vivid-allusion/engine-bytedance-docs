---
title: "Flink CDC Tasks (Beta)"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_CDC_Tasks"
---

Stream computing with Flink, based on Flink CDC, effectively achieves data ingestion from source to target through the development of YAML jobs. This article will introduce you to the operational steps of developing Flink CDC jobs.

<span id="ab195d65"></span>
## Prerequisites

The project administrator (Project_Admin) has already created a Flink resource pool within the project, please see [创建资源池](https://docs.byteplus.com/docs/flink/Create_Resource_Pool).

<span id="1a747d6c"></span>
## Experience Process

This article generally divides the Flink CDC task development process into two phases: the development phase and the operation and maintenance phase, each of which has different corresponding members and main tasks.


* **Development phase**: Typically, developers (Project_Dev) are responsible for developing the CDC tasks, completing development and debugging, and then deploying the tasks to the production environment.

* **Operation and maintenance phase**: Typically, operation personnel (Project_OPS) are responsible for starting the tasks and monitoring their execution.


<span id="123499d3"></span>
## Step One: Develop SQL Tasks


1. Log in to [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. On the left navigation pane, select **Project Management**, then click on the project tile to enter the project.

4. On the **Task Development** page, click the plus button to create a task.

   You can also select the target folder to create a task directly within that folder; or simply click under **Task creation** on **Flink CDC**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30e2cf0b63524cbbbff4874af02682cd~tplv-goo7wpa0wc-image.image) </span>


5. In the **Create Task** dialog, set the job name, job type, storage location, engine version, and other parameters. You can confirm the CDC job by previewing it, then click **Create Now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4db3e7b9934a4924ab7211ce8b7844b2~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Job Name |Customize the job name.<br><br>The name can have a length limit of 1\-48 characters, supporting digits, upper and lower\-case letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a digit or a letter. |
|Job Type |Select **job type \> Flink CDC**. |
|Template selection |Supports choosing types for data source (Source) and data downstream (Sink).<br><br>The current data source supports MySQL.<br><br>Data downstream supports ByteHouse CDW, Kafka, Doris/StarRocks, Paimon, and others. |
|Data routing |Add routing module in the Change Data Capture template. Routing (Route) specifies rules for matching a series of source tables and mapping to a target table (sink table). The most typical application scenario is the merger of sub\-databases and sub\-tables, that is, routing multiple upstream source tables to the same target table (sink table). |
|Data transformation |The Change Data Capture template has been enhanced with a data transformation module. The transformation module helps users to delete and expand data columns based on the data columns in the table. Additionally, it can help users filter out unnecessary data during the synchronization process. |
|Storage location |The system provides folder management functions for categorizing and managing tasks. During the development of the experience task, you can directly select the default **Data Development Folder** in the system.<br><br>If you have custom requirements for folder management tasks, please click the create folder button and then create a folder. |
|Engine version |Currently supports BytePlus Flink 1.16\-byted and BytePlus Flink 1.17\-byted versions, please choose as needed. |
|Task description |Enter a description of the task, generally describing the functionality implemented by the task. |



6. Edit the business logic code of the CDC job in the task editing area.

   Here is an example CDC YAML job code. The code means: create a new MySQL data source, synchronize all tables in app_db to the downstream in Doris. And perform some routing and field transformation on the tables.

   ```YAML
   source:
        type: mysql
        hostname: localhost
        port: 3306
        username: root
        password: 123456
        tables: app_db.\.*
   
      sink:
        type: doris
        fenodes: 127.0.0.1:8030
        username: root
        password: ""
   
      transform:
        - source-table: adb.web_order01
          projection: \*, UPPER(product_name) as product_name
          filter: id > 10 AND order_id > 100
          description: project fields and filter
        - source-table: adb.web_order02
          projection: \*, UPPER(product_name) as product_name
          filter: id > 20 AND order_id > 200
          description: project fields and filter
   
      route:
        - source-table: app_db.orders
          sink-table: ods_db.ods_orders
        - source-table: app_db.shipments
          sink-table: ods_db.ods_shipments
        - source-table: app_db.products
          sink-table: ods_db.ods_products
   
      pipeline:
        name: Sync MySQL Database to Doris
        parallelism: 2
   ```
   

7. Refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) upload mysql\-connector\-java into the dependency file


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe00a95fe2de4ef996c07f44a606640f~tplv-goo7wpa0wc-image.image) </span>


8. After completing the CDC task code editing, click the **verify** button.

   The system will automatically verify the correctness of your YAML statements, if there are errors, please modify the YAML statements according to the prompts. After verification, the system will indicate `success`.

9. After completing code editing and verification, click the **save** button to save the task code.


<span id="d68f9db2"></span>
## Step Two: Launch CDC Task

Development and production environments are isolated, and once task developers have completed task development and debugging, they can deploy the task into the production environment.


1. Under the **job development** section, find and click on the target task, then select the correct **execution mode** and **engine version** at the top of the editing area, followed by clicking **launch**.

2. In the **task launch settings** dialog, choose the runtime resource pool, set the task priority and scheduling strategy, then click **confirm**.

   The system will notify that the task launch was successful, and you can go to the **task management** page to view.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d6ffe3165e14918a697188319f4e21d~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Runtime Resource Pool |Select the Flink resource pool for the task to run from the dropdown list.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the task you submit is set for automatic tuning, it must run in a pay\-as\-you\-go type resource pool.</div><br> |
|Task Priority |The system default preset priority is L3, but you can set the task priority as needed; the smaller the number, the higher the priority.<br><br>Task priority determines the scheduling order within the task; tasks with higher priority are scheduled first, that is, L3 is scheduled before L4. |
|Scheduling Strategy |Configure task scheduling strategies according to requirements:<br><br><br>* GANG: Ensures all instances of a task are scheduled together, meaning resources are allocated only when sufficient for the task's normal operation; if resources are insufficient, no allocation is made.<br><br>   This strategy prevents the phenomenon where resources are allocated but the task cannot start, effectively solving resource deadlock issues.<br><br>* DRF: Considers multi\-dimensional resources to more rationally distribute them among the tasks in a resource pool, thereby enhancing utilization.<br><br>   For example: with remaining resources of 10 cores and 40 GB, if Task A requires 10 cores and 20 GB and Task B requires 2 cores and 8 GB: If allocated to A, the remaining 0 cores and 20 GB of resources cannot be utilized; the DRF strategy would choose to allocate to B, leaving 8 cores and 32 GB for future tasks. |
|Scheduling Duration |When setting to GANG scheduling strategy, it is necessary to set the scheduling duration. The scheduling duration refers to the interval between rescheduling attempts, meaning if a task launch is unsuccessful, it will be rescheduled.<br><br>If the scheduling duration is exceeded, the task will fail to schedule. If set to 0, it will keep retrying. |
|More settings |Change Data Capture tasks support skipping the in\-depth check before going live, allowing the task to be forced online.<br><br>Not selected by default. Checking **skip the pre\-launch check** means bypassing the Change Data Capture code depth check, and the task will go live directly. |


<span id="e69808ec"></span>
## Step Four: Start the CDC Task

Development is isolated from the production environment. After the task developers deploy the task to the production environment, the operations personnel will start the task.


1. In the project's left sidebar, select **Task Operations \> Task Management**.

2. On the **Task List** page, click on **Operation** in the column and then on **Start**.

3. In the **Start Task** dialog box, choose the way to start the task, then click **Confirm**.

   Starting the task takes some time, please be patient. Once started successfully, the status will be **Running**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55b4fe5850d646c49f33aec3fa9e72ca~tplv-goo7wpa0wc-image.image) </span>

   
   |**Settings** |**Description** |
   |---|---|
   |Startup Mode |Please choose the task startup mode based on actual conditions.<br><br><br>* Start from the latest state: Start with the latest checkpoint or savepoint (choose the most recent by time).<br><br>* Fresh start: Start without using any checkpoint or savepoint.<br><br>* Start with a specified snapshot: Start with a targeted snapshot (savepoint).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The first time a task goes live, it can only be started in a <strong>completely new startup</strong> mode.</div><br> |
   |Parameter Configuration |The job carries the parallelism, Task Manager, and Job Manager resource configurations on the development side. Supports updating configurations and quickly taking effect when starting the job.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Updating parameter configurations and starting tasks will create a new task version and synchronize the latest settings to the task development side.</div><br><br><br><br>* Parallelism: Global concurrency of the job.<br><br>* Single TaskManager CPU count: The number of CPU cores in a single TaskManager.<br><br>* Single TaskManager memory size: The memory size occupied by a single TaskManager.<br><br>* Number of slots per TaskManager: Number of slots in a single TaskManager.<br><br>* JobManager CPU count: Number of CPU cores in a single JobManager.<br><br>* Memory size of JobManager: Memory footprint of a single JobManager. |
   |More settings |When adding or modifying operators during task development could prevent the task from being restored from a snapshot. In this case, you can choose to enable the **Allow Non Restored State** feature to ensure the task runs smoothly.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a011a4e8eb6546b880737c74d2a14685~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only when the <strong>Specify Snapshot Startup</strong> or <strong>Start from Latest State</strong> modes are selected, it is possible to check the option to ignore certain operator states.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you choose the <strong>fresh start</strong> method, ignoring the operator state is not supported.</div><br> |
   


<span id="a4e823b3"></span>
## Step Five: View Flink UI

Once the task is running normally in the production environment, you can view detailed information about task execution, TaskManager, and JobManager in the Flink UI interface.


1. In the project's left sidebar, select **Task Operations \> Task Management**.

2. In the**task list** page, filter the target tasks, and click the **operation** column under **Flink UI**.

   The browser will automatically open the Apache Flink Dashboard page.

3. On the left navigation bar of the Apache Flink Dashboard, select **Task Managers**, then click on the task ID.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bd42e006b174cc37b4bd767d59c18a0b.png) </span>

4. On the Task Manager details page for the task, click on the **Stdout** tab to observe that the task is running normally, and you can confirm the business is functioning correctly through console outputs and logs.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b479b6aa71786511e2ad320bb80b180e.png) </span>
