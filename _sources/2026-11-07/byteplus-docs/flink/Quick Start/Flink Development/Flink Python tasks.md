---
title: "Flink Python tasks"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_Python_tasks"
---

Flink supports the development of Python\-based tasks. You can write Python programs and upload Python files to the repository to develop Python tasks on the platform.

This article introduces the development process for streaming\-type Python tasks. For information on Batch Python tasks, see [Develop Flink Batch Python tasks](https://docs.byteplus.com/docs/flink/Create_a_Flink_Python_Task#2f3c1c4b).

<span id="06b98cc4"></span>
## Prerequisites


* The project administrator (Project_Admin) has already created a Flink resource pool within the project, see [创建资源池](https://docs.byteplus.com/docs/flink/Create_Resource_Pool).

* Developers need to write Python programs in advance and upload the Python files to the repository. For information on how to upload files, see [Upload Resource Files](https://docs.byteplus.com/docs/flink/Upload_Resource_Files). You may refer to the following Python code content:

> **Attention**: Do not name the code files as "pyflink" or other names conflicting with the Flink Python libraries, as it may cause job failures.


```Python
from pyflink.datastream import StreamExecutionEnvironment

def main():
    env = StreamExecutionEnvironment.get_execution_environment()
    data_stream = env.from_collection([1, 2, 3, 4, 5])
    result_stream = data_stream.map(lambda x: x + 1)
    result_stream.print()
    env.execute("Simple PyFlink Example")

if __name__ == "__main__":
    main()
```


<span id="20a28bfd"></span>
## Functional Limitations

Currently, only the Flink 1.17\-byted version supports Flink Python tasks.

<span id="84d6c4ad"></span>
## Step One: Create a Flink Python Task


1. Log in to [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left sidebar, select **Project Management**, perform a fuzzy search by project name in the search box, then click on the project block to enter the project.

4. In the left sidebar of the project, select **Task Development \> Task Development**.

5. On the **Task Development** page, click the plus button to create a task.

   You can also choose the target folder, directly create the task in that folder; or simply click on the **Flink Python Task** under the guidance page.

6. In the **create task** dialog, set the job name, storage location, engine version, and other key parameters, then click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2861f6c0ab4e453c919330fe2863348d~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the name of the task.<br><br>The length of the name must be between 1 and 48 characters, supporting numbers, uppercase and lowercase English letters, underscores (_), dashes (\-), and periods (.), and it must start and end with either a letter or a number. |
|Task Type |Select **Task Type \> Flink Python** . |
|Storage Location |Select the target folder from the dropdown list.<br><br>There is a default **Data Development Folder**, but for easier task management, you can freely create folders. For instructions on how to create task folders, please see [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders) |
|Engine Version |Only BytePlus Flink 1.17\-byted version supports Flink Python tasks. |



6. In the task configuration area, set the key parameters of the task.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77baf0ab6d4b41c4aebc741b1dda277f~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Job Name |The name set when creating the job. |
|Python File URI |Select the uploaded Python file from the dropdown list. If you have not yet uploaded a file, please see [Upload Resource Files](https://docs.byteplus.com/docs/flink/Upload_Resource_Files). |
|Entry Module |The entry class of the program.<br><br><br>* If the Python job file is an `.py` file, this field is not required.<br><br>* If the Python job file is an `.zip` file, enter your Entry Module here, such as kafka_test. |
|Entry Point Main Arguments |Main function's `args` parameters of the business program, not mandatory. Fill in according to the on\-screen prompts. |
|Python Libraries |Third\-party Python packages.<br><br>Third\-party Python packages are added to the PYTHONPATH of the Python worker process, allowing direct access in custom Python functions. |



7. After completing task development and configuration, click **Save**.


<span id="3bc79abd"></span>
## Step Two: Launch Task

Development is isolated from production; once task developers have completed the development, they can launch the task into the production environment.


1. Under the **job development** section, find and click the target task, then click **launch**.

2. In the **task launch settings** dialog, select **runtime resource pool**, set **task priority** and **scheduling strategy**, then click **OK**.

   The system will indicate that the task has been successfully launched, and you can go to the **task management** page to view it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d6ffe3165e14918a697188319f4e21d~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Execution Resource Pool |Select the BytePlus Flink resource pool for the task from the drop\-down list. |
   |Task Priority |The system default priority is set as L3. You can set the task priority as needed; the smaller the number, the higher the priority.<br><br>Task priority determines the internal scheduling order of tasks; tasks with higher priority are scheduled first, meaning L3 is scheduled before L4. |
   |Scheduling Strategy |Configure the task scheduling strategy based on your needs:<br><br><br>* GANG: Ensures all instances of a task are scheduled together, meaning resources are allocated only if the remaining resources meet the task's normal operational requirements; if not, resources are not allocated.<br><br>   This strategy prevents the issue of resource allocation without task start\-up, thereby solving the problem of resource deadlock.<br><br>* DRF: Considering multidimensional resources, it more reasonably distributes resources fairly to each task within the resource pool, thereby enhancing utilization.<br><br>   For example: with remaining resources of 10 cores and 40 GB, Task A requires 10 cores and 20 GB; Task B requires 2 cores and 8 GB. If assigned to Task A, the remaining 0 cores and 20 GB of resources cannot be utilized; the DRF strategy would choose to allocate to Task B, leaving 8 cores and 32 GB available for future tasks. |
   |Scheduling Duration |When setting up the GANG scheduling policy, it is necessary to set the scheduling duration. Scheduling duration indicates the interval before rescheduling, meaning if a task fails to start, it will be scheduled again.<br><br>If it exceeds the scheduling duration, the task will fail to schedule. If set to 0, it will keep retrying. |
   


<span id="cbfbcc20"></span>
## Step Three: Start Task

After task developers have launched the task into the production environment, it is started by the operations personnel.


1. In the project's left sidebar, select **Task Operations \> Task Management**.

2. On the **Task List** page, select the target task and click **Operations** column's **Start**.

3. In the **Start Task** dialog, select the task startup mode, then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55b4fe5850d646c49f33aec3fa9e72ca~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Startup Method |Please select a startup method according to the actual situation:<br><br><br>* Start from the latest state: Start with the most recent Checkpoint or Savepoint.<br><br>* Fresh start: Start directly without using a Checkpoint or Savepoint.<br><br>* Specify snapshot start: Start with the specified target snapshot (Savepoint).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The first time a task goes live, it can only be started in <strong>initial</strong> mode.</div><br> |
   |Parameter Configuration |The task carries parallelism, TaskManager, and JobManager resource configurations developed on the developer side. Supports updating configurations and quick implementation when launching the task.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After updating the parameter settings and starting the task, a new task version will be added, and the latest settings will be synchronized to the task development side.</div><br><br><br><br>* Parallelism: total number of concurrent tasks globally.<br><br>* Single TaskManager CPU count: number of CPU cores in a single TaskManager.<br><br>* Single TaskManager memory size: the memory size occupied by a single TaskManager.<br><br>* Single TaskManager slot count: the number of slots in a single TaskManager.<br><br>* JobManager CPU count: the number of CPU cores in a single JobManager.<br><br>* JobManager memory size: the memory size occupied by a single JobManager. |
   |More settings |When adding or modifying operators during task development changes, it may cause the task to be unable to recover from the snapshot. In this case, you can choose to enable the **Allow Non Restored State** feature to ensure the task runs smoothly.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a011a4e8eb6546b880737c74d2a14685~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only when the <strong>specified snapshot start</strong> or <strong>start from the latest state</strong> method is selected, it supports checking the option to ignore some operator states.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you choose the <strong>fresh start</strong> method, ignoring the operator states is not supported.</div><br> |
   


<span id="e34632d4"></span>
## Step Four: Check the Flink UI

Once the task is running normally in the production environment, you can access detailed information about the task operation, TaskManager, and JobManager on the Flink UI interface.


1. In the project's left sidebar, select **Task Operations \> Task Management**.

2. On the **Task List** page, filter for the target task, and click **Operations** column's **Flink UI**.

   Your browser will automatically open the Apache Flink Dashboard page.

3. On the Apache Flink Dashboard page, check the details of the task operation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88a18a2bba014d4c892f188540d97c23~tplv-goo7wpa0wc-image.image) </span>
