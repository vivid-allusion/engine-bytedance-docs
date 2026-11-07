---
title: "Flink JAR Tasks"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_JAR_Tasks"
---

Flink supports the development of JAR type tasks. You can write your own business applications and build JAR packages. Simply upload the application JAR package and configure the key parameters to complete the development of the JAR task, which is very simple.

This article introduces the development process of Stream type JAR tasks. For information on Batch JAR tasks, please see [Develop Flink Batch JAR task.](https://docs.byteplus.com/docs/flink/Create_Flink_JAR_Jobs#c4872d77).

<span id="e1252c7a"></span>
## Prerequisites


* The project administrator (Project_Admin) has already created a Flink resource pool within the project, please see [创建资源池](https://docs.byteplus.com/docs/flink/Create_Resource_Pool).

* Developers must complete the development of business applications and build the JAR packages in advance. The JAR package file name must meet the console requirements and can only consist of uppercase and lowercase letters, numbers, underscores (_), hyphens (\-), and periods (.).


<span id="3e5453a0"></span>
## Experience Process

This article divides the development process of Flink JAR tasks into two phases: development and operations. Each phase involves different members and main tasks.


* **Development phase**: Typically, the project developers are responsible for uploading JAR packages, developing, and launching JAR tasks.

* **Operations phase**: Usually, the project operations staff are responsible for starting tasks and monitoring their execution.


<span id="e7f2652e"></span>
## Step one: Upload the JAR package

The Flink console offers unified management of JAR package resources. Before you start developing JAR tasks, you can upload the JAR packages to the console in advance.


1. Login to [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, then click on the project block to enter the project.

4. In the project's left navigation bar, select **File Management** and then click the **Upload Resource** button.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3be31c2f647b4f619a9123627994a2d0~tplv-goo7wpa0wc-image.image) </span>


5. In the **Upload file** dialog box, set the resource directory, upload the JAR package, fill in the resource description, then click **Confirm**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f094accd10e141f4844059f54c515642~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Resource Upload |Upload local files.<br><br><br>* The file name can only consist of uppercase and lowercase letters, numbers, underscores (_), hyphens (\-), and periods (.).<br><br>* The file size must not exceed 500 MB.<br><br>* If you re\-upload a file, the new file will replace the one already uploaded. |
|Resource Name |By default, it maintains the same name as the file you uploaded but supports custom renaming.<br><br>The file name can only consist of uppercase and lowercase letters, numbers, underscores (_), and periods (.), with a character length ranging from 1 to 60. |
|Folder |Select the folder to which the resource file belongs.<br><br>The system has a default folder by default , but to manage resource files more conveniently, you can freely create folders. |
|Resource Description |Provide a description for the uploaded resource files, typically regarding their function and purpose. |


<span id="4e7d7c6d"></span>
## Step Two: Development Task


1. Log in to the [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left sidebar, select **Project Management**, perform a fuzzy search by the project name in the search box, and then click the project block to enter the project.

4. In the project's left sidebar, select **Task Development**.

5. On the **Task Development** page, click the plus button to create a task.

   You can also select the target folder and create a task directly within that folder; or simply click on **Flink Task** under **Flink JAR**.

6. In the **Create Task** dialog, set key parameters such as task name, owning folder, and engine version, then click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/494c86cb4e9b48b7bce23cea90db6476~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Explanation** |
|---|---|
|Task Name |Customize the task name.<br><br>The character length of the name is limited to 1\-48, supporting numbers, uppercase and lowercase English letters, underscores (_), hyphens (\-), and periods (.), and the name must start and end with a letter or a number. |
|Job Type |Select **BytePlus Flink Task \> BytePlus Flink JAR**. |
|Associated Folder |Select the target folder from the dropdown list.<br><br>The system has a default **Data Development Folder**, but for more convenient task management, you can freely create folders. For information on how to create a task folder, please refer to [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders) this section. |
|Engine Version |Currently supports BytePlus Flink 1.11\-byted, BytePlus Flink 1.16\-byted, and BytePlus Flink 1.17\-byted versions; select as needed. |
|Task Description |Enter a description statement of the task, generally describing the task's functionality. |



6. In the task configuration area, set key task parameters.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a45743cb0917432b8fbbe79f84d33e5b~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the task name.<br><br>The character length of the name is limited to 1~48, supporting numbers, uppercase and lowercase English letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a number or letter. |
|Task Type |Select **BytePlus Flink task \> Flink Stream \> Jar**.<br><br>For a tutorial on SQL task development process, please refer to [Flink SQL tasks](https://docs.byteplus.com/docs/flink/Flink_SQL_tasks) |
|Corresponding Folder |The system provides folder management functionality for classifying and managing tasks. During the task development experience, you can directly select the **Data Development folder** that already exists in the system.<br><br>If you have requirements for managing tasks with custom folders, please click the folder button for creating folders, and then create a folder. |
|Engine Version |Currently supports BytePlus Flink 1.11\-byted, BytePlus Flink 1.16\-byted, and BytePlus Flink 1.17\-byted versions; please choose as needed. |
|Task Description |Input the task description sentence, generally describing the function implemented by the task. |



6. Configure tasks.

   In the task configuration area, set the key parameters and then click **Save**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7637b05bf943463e9543615120120c84~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Name set when creating the task. |
|JAR URI |Select an uploaded JAR package from the dropdown list. |
|Entrypoint Class |The main class of the business JAR program, please fill in according to the screen prompts. |
|Entrypoint main args |Main function args[] parameter of the business program, optional. `args[]` Please fill in according to the screen prompts. |


<span id="b9264411"></span>
## Step Three: Launch JAR Task

Development is isolated from production; after task developers complete development, they can deploy the task to the production environment.


1. In the **Task Launch Settings** dialog, select **Runtime Resource Pool**, set **Task Priority** and **Scheduling Strategy**, then click **Confirm**.

   The system will notify you that the task has been successfully launched, and you can go to the **Task Management** page to view it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d6ffe3165e14918a697188319f4e21d~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Runtime Resource Pool |Select the Flink resource pool where the task will run from the dropdown list.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the job you submit has auto\-tuning enabled, it must be run in a pay\-as\-you\-go resource pool.</div><br> |
   |Task Priority |The system's default preset priority is L3, but you can set the task priority as needed; the smaller the number, the higher the priority.<br><br>Task priority determines the internal scheduling order of tasks, with higher priority tasks being scheduled first, i.e., L3 is scheduled before L4. |
   |Scheduling Strategy |Configure the task scheduling strategy according to needs:<br><br><br>* GANG: Ensures all instances of a task are scheduled together, i.e., allocation only occurs when the remaining resources meet the normal operational needs of the task; if not, resources are not allocated.<br><br>   This strategy prevents the issue of resources being allocated and tasks being unable to start, thereby resolving resource deadlocks.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Flink Batch jobs do not support the GANG scheduling strategy, only the DRF scheduling strategy is supported. If the execution mode is selected as Batch, the GANG strategy will not be displayed on the online configuration page.   </div><br>   <br><br>* DRF: Considers multi\-dimensional resources to more reasonably distribute resources fairly among all tasks within the resource pool, thus enhancing utilization.<br><br>   For example: With remaining resources of 10 cores and 40 GB, task A requires 10 cores and 20 GB; task B requires 2 cores and 8 GB. If assigned to A, the remaining 0 cores and 20 GB of resources cannot be utilized; the DRF policy will choose to allocate to B, with 8 cores and 32 GB remaining for subsequent tasks. |
   |Scheduling duration |When setting the GANG scheduling strategy, it is necessary to set the scheduling duration. Scheduling duration represents the interval before rescheduling, i.e., if a task launch is unsuccessful, it will be rescheduled.<br><br>If the scheduling duration is exceeded, the task will fail to schedule. If set to 0, it will keep retrying. |
   


<span id="0f8f4382"></span>
## Step Four: Start JAR Task

Development is isolated from production; once task developers deploy the task to the production environment, it is started by the operations personnel.


1. In the project's left sidebar, select **Task Operations \> Task Management**.

2. On the **Task List** page, click **Operation** in the column and select **Start**.

3. In the **Start Task** dialog, select the task launch mode, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55b4fe5850d646c49f33aec3fa9e72ca~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Startup mode |Please choose a method to start the task based on the actual situation:<br><br><br>* Start from the latest state: Start with the latest Checkpoint or Savepoint.<br><br>* Start fresh: Start without using a Checkpoint or Savepoint.<br><br>* Start from a specified snapshot: Start with the designated target snapshot (Savepoint).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The task, when first launched online, can only be initiated by <strong>a brand new start</strong>.</div><br> |
   |Parameter Configuration |The task carries the parallelism on the development side, and the resource configurations for the Task Manager and Job Manager. Supports updating configurations and quick implementation when starting the task.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After updating the parameter settings and starting the task, a new task version will be added, and the latest configurations will be synchronized to the task development side.</div><br><br><br><br>* Parallelism: The global concurrency number of the task.<br><br>* Single TaskManager CPU count: The number of CPU cores in a single TaskManager.<br><br>* Single TaskManager Memory Size: The memory size occupied by a single TaskManager.<br><br>* Single TaskManager Slot Count: The number of slots in a single TaskManager.<br><br>* JobManager CPU Count: The number of CPU cores in a single JobManager.<br><br>* JobManager Memory Size: The memory size occupied by a single JobManager. |
   |More Settings |When developing and changing tasks, adding or modifying operators could prevent the task from recovering from a snapshot. In this case, you may choose to enable the **Allow Non Restored State** feature to ensure the task runs properly.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b0fd2f4aa1b4f90afe240188d2cc278~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Checking "Ignore certain operator statuses" is supported only when the <strong>specified snapshot start</strong> or <strong>start from the latest status</strong> option is selected.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you choose <strong>a brand new start</strong>, ignoring the operator status is not supported.</div><br> |
   


<span id="76fa1987"></span>
## Step Five: Review BytePlus Flink UI

Once the task is running normally in the production environment, you can learn about the operation of the task, TaskManager, and JobManager in detail through the BytePlus Flink UI interface.


1. In the project's left navigation bar, select **Task Operations & Management \> Task Management**.

2. On the **Task List** page, filter for the target task and click on the **Action** column under **BytePlus Flink UI**.

   The browser will automatically open the Apache Flink Dashboard page.

3. In the left navigation bar of the Apache Flink Dashboard, select **Task Managers** and then click on the task ID.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_795e48faa0a03fe38fa6f83681f17148.png) </span>

4. On the Task Manager details page of the task, click the **Stdout** tab, then search for `successfully` in the logs to view the task execution results.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b37bd0ddf5b656705fa4e48ca0c30db.png) </span>
