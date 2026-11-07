---
title: "Manage data insight tasks"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks"
---

The Data Insight Task specifies the execution goals and methods of the Data Insight Policy and acts as its executor. This article describes the steps and related actions for creating a Data Insight Task.

<span id="64bb8197"></span>
## Background information

Data Insight Tasks include export tasks, analysis tasks, and capacity query tasks. The execution results of export tasks and capacity query tasks can be exported to the file system, object storage buckets, or a browser. Description:


* **Export task**

   The task aims to obtain the result file of the task execution. The task execution result file contains attribute information about the exported files.

* **Analysis task**

   A task aimed at obtaining analysis information based on task execution results The system, built on Log Service TLS, offers task execution result analysis charts. You can further query, retrieve, and visualize data insight results in the analysis charts.

* **Capacity query task**

   A task aimed at obtaining file system capacity data The query results include files showing the capacity of first\-level and second\-level subdirectories.


<span id="qI9XabiR"></span>
## Restrictions


|Limit |Note |
|---|---|
|Create Task |Each file system supports only one recurring task. |
|Run task |A single file system can only run one Data Insight task at a time. When the execution time of a new task conflicts with an existing task, the system will handle the situation according to the following rules:<br><br><br>* One\-off tasks: Queue according to the task creation time.<br><br>* Recurring tasks: Terminate the conflicting instance of the subtask. |
|Execution directory |A single task can be associated with up to 10 execution directories. |


&nbsp;

<span id="106550ed"></span>
## Prerequisites


* Ensure that a data insight policy exists within the same region before executing actions. For instructions, see [Create data insight policy](https://docs.byteplus.com/en/docs/pfs/Manage_data_insight_policies#e05deaf7).

* The target file system already exists. For instructions, see [Creating a file system](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system).

   * The target file system has enabled custom task features for Data Insight service. For instructions, see [Enabling data insight service](https://docs.byteplus.com/en/docs/pfs/Enable_Data_Insight_Service).

   * The execution directory for the task in the target file system already exists. If the directory is Fileset, make sure the target Fileset exists. For instructions, see [Managing filesets](https://docs.byteplus.com/en/docs/pfs/Managing-fileset).

* When exporting to object storage, ensure that the object storage bucket for task results exists in the same region. For instructions, see [Creating a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="f256f405"></span>
## Create Data Insight Task


1. Log in to the [PFS console](https://console.byteplus.com/pfs).

2. In the upper navigation bar, select the region where the target file system is located.

3. In the left navigation bar, select **Data Insights** \> **Task** **management**.

4. On the **Task** **management** page, click **Create task**.

5. On the **Create Data Insight task** page, configure the following parameters.

   * **Basic information**

      Fill in the basic information for the Data Insight task, including the task name and description.

      
      |**Parameter** |**Required** |**Note** |
      |---|---|---|
      |Task name |Yes |Set the Data Insight task name. The naming rules are as follows:<br><br><br>* Start with a letter or Chinese character.<br><br>* The permission group name can only contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* Length must be between 1 and 128 characters. |
      |Description |No |Set a description for the Data Insight task. The following constraints apply:<br><br><br>* Start with Chinese characters, letters, or numbers.<br><br>* Contain only Chinese characters, letters, numbers, spaces, periods (.), Chinese periods (。), underscores (_), hyphens (\-), equal signs (=), English commas (,), Chinese commas (，), or enumeration commas (、).<br><br>* The length must be between 0 and 120 characters. |
      

   * **Associate Policy**

      Select the file system for the data insight task, choose the data insight policy to use, and specify the execution directory.

      
      |**Parameter** |**Required** |**Note** |
      |---|---|---|
      |File policy |Yes |Select the Data Insight policy you want to use You can choose Data Insight policies available in the same region. |
      |Associated file system |Yes |Select the file system to execute the task.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the selected file system is running other Data Insight tasks, the current task will be queued after creation.</div><br> |
      |Execution directory |Yes |Set the target directory for task execution. The execution directory can be a **Fileset** or a **Directory**:<br><br><br>* **Fileset**: Select Fileset from the dropdown list. You can set subdirectories as needed. Each subdirectory must be a relative path within the Fileset, starting and ending with a slash (/).<br><br>* **Directory (absolute path, root is /)** : Enter the absolute path of the directory in the file system, starting and ending with a slash (/).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Add Directory</strong> to add multiple execution directories, up to 10 entries.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The directory constraints are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The path cannot exceed 8 directory levels.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Can contain letters, numbers, periods (.), underscores (_), hyphens (\-), and forward slashes (/).</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Length of the complete path string must not exceed 1,024 characters, and each subpath segment must be limited to 255 characters or fewer.</div><br> |
      

   * **Task time**

      Select the execution plan and time for this task.

      
      |Parameter |Required |Note |
      |---|---|---|
      |Task execution plan |Yes |Select a task execution schedule. The available options are:<br><br><br>* **One\-time task**: This task runs only once.<br><br>* **Recurring task**: This task runs multiple times on a scheduled basis. |
      |Task execution time |Yes |When **Task execution plan** selects **One\-time task**, you need to choose the execution time. The available options are as follows:<br><br><br>* Execute immediately: Execute this task right away.<br><br>* Specified time: Select a specific time to execute this task. |
      |Specify time |No |When the **task execution plan** is set to **one\-time task** and **task execution time** is set to **specified time**, you can select the specific time in the time picker, down to the second. |
      |Execution cycle |No |When the **task execution plan** selects **recurring task**, you need to set the task frequency. The available options are as follows:<br><br><br>* **Hour**: Enter an integer between 2 and 8760.<br><br>* **Day**: Enter an integer between 1 and 365.<br><br>* **Week**: Enter an integer between 1 and 52.<br><br>* **Month**: Enter an integer between 1 and 12. |
      |First execution time |No |When the **task execution plan** is set to **recurring task**, you need to select the execution time for the first task, accurate to the second.<br><br>After selection, the page will display the specific execution times for the next 5 tasks. |
      

   * **Task content**

      Enter detailed information for the data insight task.

      
      |**Parameter** |**Required** |**Note** |
      |---|---|---|
      |Task type |Yes |Select the data insights task type. Options:<br><br><br>* **Export**: Export the results of the data insights task as a file list.<br><br>* **Analysis**: Send the results of the data insights task to TLS for further data retrieval and analysis.<br><br>* **Capacity query**: View file system capacity data. |
      |Export task configuration |No |When **Task Type** is set to **Export**, you need to configure how to export the task result and specify export properties.<br><br><br>* **Export Mode**: Choose how to export the task, and set the target path or object storage bucket. For details about export modes, see [Description of export methods](https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks?lang=en#wx9qvohg).<br><br>* **Export Properties**: Select file attributes to export. By default, all attributes are selected You can perform the following actions as needed:<br><br>   * Add or remove file attributes in the multi\-select dropdown.<br><br>   * Move the cursor over an attribute, then drag it after selection to adjust its position. The attribute order in the exported file will match this arrangement.<br><br>   * For details about file attributes, refer to [Description of file properties](https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks?lang=en#JWjVzTig).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The task result file includes the policy filter result file, which will be exported to the same file system, object storage bucket, or browser based on your selected export mode. For specific steps to view the task result file, see <a href="https://docs.byteplus.com/en/docs/pfs/View_data_insight_results">View data insight results</a>.</div><br> |
      |Analysis task configuration |No |When **task type** is set to **analysis**, select the attributes to analyze. The system will automatically generate a TLS index based on the selected analysis attributes.<br><br>When creating an analysis task for the first time, click **Authorize**, then in the **Authorization** dialog, click **Authorize Now** to authorize PFS to access the TLS log service.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After enabling the analysis task, you can further query and visualize the results of the data insight task. The default storage period for analyzed data in the log service is 30 days, and log service fees are billed separately. For details, see <a href="https://docs.byteplus.com/en/docs/tls/billable_items">TLS Billing overview</a>. You can also adjust the storage period as needed in the corresponding TLS log topic.</div><br> |
      |Capacity query task configuration |No |When **Task Type** is set to **Capacity Query**, you must configure query items and the export method.<br><br><br>* **Primary Subdirectory Capacity Query**: Enable **Primary Subdirectory Capacity Query** to check the capacity of primary subdirectories in the execution directory.<br><br>* **Secondary Subdirectory Capacity Query**: Enable **Secondary Subdirectory Capacity Query** to check the capacity of secondary subdirectories in the execution directory.<br><br>* **Export Method**: Select how the task results will be exported and set the target path or object storage bucket. For details about export methods, see [Description of export methods](https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks#wx9qvohg). |
      

6. Click **Confirm**.


<span id="JWjVzTig"></span>
### Description of file properties


|Attribute name |Attribute field |Note |
|---|---|---|
|Inode |Inode |File index. |
|File access permissions |Mode |Read, write, and execute permissions for file owner, group, and other users. |
|Number of links |NLink |Number of file links. |
|File size |Size |File size. |
|File name |Name |File name excluding file path. |
|File type |Type |File type, used to indicate whether it is a regular file, directory, link, or other special file type. |
|File extension |Extension |File extension, typically used to indicate the file format. |
|File path |Path |Full path including the file name. |
|Creation time |CreationTime |File creation time. |
|Last access time |AccessTime |Last accessed (read) time of file. |
|Last metadata change time |ChangeTime |The last modification time of the file metadata. |
|Last data modification time |ModifyTime |Last modified time of file data. |


<span id="wx9qvohg"></span>
### Description of export methods


|**Parameter** |**Note** |
|---|---|
|Export to file system |Export task results to the specified directory in the same file system.<br><br>Set the export directory with the following restrictions:<br><br><br>* Enter the absolute path in the file system, starting and ending with a forward slash (/).<br><br>* The path cannot exceed 8 directory levels.<br><br>* Can contain letters, numbers, periods (.), underscores (_), hyphens (\-), and forward slashes (/).<br><br>* Length of the complete path string must not exceed 1,024 characters, and each subpath segment must be limited to 255 characters or fewer. |
|Export to object storage |Export task results to the specified TOS bucket.<br><br>Set the TOS bucket and bucket prefix for export:<br><br><br>* TOS bucket: Select a TOS bucket in the same Region.<br><br>* TOS bucket prefix: (Optional) Enter the TOS bucket prefix with the following constraints:<br><br>   * Must start and end with a forward slash (/).<br><br>   * Cannot contain consecutive forward slashes such as (//).<br><br>   * The length must be between 3 and 1024 characters. |
|Download from console |Export task results to the browser. You can later download the exported file from the PFS console. |


<span id="5a259564"></span>
## Related operations


|**Operation** |**Note** |**Steps** |
|---|---|---|
|View task details |You can view detailed information about the task, including **Basic** **information** **of** **the** **task**, **Affiliation** **policy** **information**, **task content**, and specific information for each type of task. |1. On the **Data Insight** \> **Task Management** page, click the target task name to view detailed information about the task in the **Overview** page.<br><br>2. (Optional) If the target task is an **Analysis** task, you can click **Analysis Task** \> **Analysis Chart** and select **View** to enter the **Analysis Chart** page and review the task analysis chart. |
|Edit task name |You can change the task name. Naming guidelines are as follows:<br><br><br>* Start with a letter or Chinese character.<br><br>* The permission group name can only contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* The length must be between 1 and 128 characters. |1. On the **Data Insight** \> **Task Management** page, click the **Edit** icon next to the target task name.<br><br>2. Enter the new task name in the dialog box.<br><br>3. Click **Save**. |
|Copy task |You can copy a task to repeat the same task. |1. In the task list, click **Copy** in the **Actions** column of the target task.<br><br>2. On the **Copy Data Insight Task** page, configure as needed and click **Confirm**. |
|Cancel a task |You can cancel Data Insight tasks. |1. On the **Data Insight** \> **Task Management** page, click **Cancel** in the **Actions** column for the target task.<br><br>2. In the **Cancel task** dialog, click Cancel task. |
|Delete tasks |You can delete tasks that are no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ongoing tasks cannot be deleted. You must terminate the task before deleting it.</div><br> |1. On the **Data Insight** \> **Task Management** page, click  **...**  \> **Delete** in the **Actions** column of the mount target you want to remove.<br><br>2. In the **Delete tasks** dialog box, click **Delete task**. |
