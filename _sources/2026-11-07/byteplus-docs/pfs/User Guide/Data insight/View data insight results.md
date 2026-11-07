---
title: "View data insight results"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/View_data_insight_results"
---

This article describes the steps to view the results of a Data Insight task.

<span id="106550ed"></span>
## Prerequisites

The Data Insight task has been completed. For more information, see [Create data insight task](https://docs.byteplus.com/en/docs/pfs/Manage_Data_Insight_tasks#f256f405).

<span id="e81916b9"></span>
## View export task results or capacity query task result files


<Tabs>
<Tab zoneid="OzSuBY37FK" title="Export to file system">
<TabTitle>Export to file system</TabTitle>

1. Log in to any management node of the relevant PFS file system. .

2. Run the following command to view the task result file.

   ```Bash
   ls /<File system mount directory>/<Export directory>/<Data insight task ID>
   ```
   

   Note:

   * `<File system mount directory>`: The file system mount directory where the task is executed.

   * `<Export directory>`: The export directory for the data insight task, used to store the task result files. Set it when creating or editing a data insight task.

   * `<Data insight task ID>`: The ID of the data insight task being executed.

   The files listed in the echo information are as follows:

   
   |Filename |Description |Note |
   |---|---|---|
   |`file_list.txt` |Export result file, includes all **export attributes** selected during task creation. |Generated only when creating an **Export** task. |
   |`first_level_subdir_cap.txt` |First\-level subdirectory capacity query result file. |Only generated when creating a **capacity query** task and enabling the **first\-level subdirectory capacity query** switch. |
   |`second_level_subdir_cap.txt` |Secondary subdirectory capacity query result file. |Only generated when creating a **capacity query** task and enabling the **second\-level subdirectory capacity query** switch. |
   

3. Run the `vim` command to view the file content.

   For example, run the command `vim file_list.txt` to view the content of the exported result file.


</Tab>
<Tab zoneid="IDFRzX1RD1" title="Export to object storage">
<TabTitle>Export to object storage</TabTitle>

1. Log in to the [TOS Console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Bucket List**.

3. In the bucket list, click the target **Bucket Name** to go to the **File List** page.

4. In the list, click the target **File Name** (bucket prefix).

5. Click the target task folder. The folder name is the Data Insight Task ID, for example`lenstask-cnsh1*****`.

   The page displays information about the exported result files for the task:

   * `file_list.txt`: The exported result file containing the properties of the exported files.

   * `first_level_subdir_cap.txt`: Result file for first\-level subdirectory capacity queries.

   * `second_level_subdir_cap.txt`: Result file for second\-level subdirectory capacity queries.

6. View or download the exported files.

   * Click **Details** in the **Actions** column for the target file to view its contents.

   * Click **Download** in the **Actions** column for the target file to download the file.


</Tab>
<Tab zoneid="NhldSgELjk" title="Download from console">
<TabTitle>Download from console</TabTitle>

1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation bar, select **Data Insight** \> **Task Management**.

4. On the **Task List** page, select the **Export Task** or **Capacity Query Task** column for the target task and click **Download**.

5. In the **Download** dialog box, click **Actions** in the column and then click **Download** to download the corresponding file type.


</Tab>
</Tabs>


<span id="oSwkX7br"></span>
## View analysis task charts

Follow these steps to view task execution result analysis charts:


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation bar, select **Data Insight** \>  **Task Management**.

4. On the **Task Management** page, click **View** in the **Analysis Chart** column of the target task to enter the **Analysis Chart** page.

   You can further query, search, and visualize task execution results on the **Analysis Chart** page.
