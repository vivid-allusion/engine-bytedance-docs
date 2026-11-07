---
title: "Overview"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/data_operation_overview"
---

The DataLeap Operations Center can manage and maintain online tasks and supports **Batch Task Operations** and **Stream Task Operations**. Different operation and maintenance functions are provided based on the characteristics of each task type, such as intelligent task diagnostics, data backfill, and task rerun.

<span id="233a44ed"></span>
## **Batch Task Operations**

The modules include Overview, Task Operations, Instance Operations, Data Backfill, and Alarm Monitor. The specific functions of each module are as follows:


* Overview:

   Displays an overview of all active tasks under the project, helping you gain a macro\-level understanding of the distribution of task instance states and running periods for the current day. You can also view information such as the number of tasks per owner, task type distribution, task scheduling method distribution, historical task run analysis and ranking, and more.

* Task operations:

   * Display active batch tasks under the project.

   * View task dependency DAG, task priority, and other task info as needed.

   * Perform data backfill, monitor settings, and other operation and maintenance actions on the task.

   * Perform actions such as turning the task on or off, and other state\-related actions.

* Instance operations:

   * Display the run instance information for the task.

   * View instance state changes in real time, and quickly locate exceptions using dependencies, diagnostics, and logs.

   * Perform actions such as rerun, set to Success, terminate, and other actions on the instance.

* Data backfill:

   Through data backfill, you can complete the **backfill/rerun** action for a task within a specified historical time range. Backfill is supported for a single task, a single task and downstream, multiple tasks, or multiple tasks and downstream. After initiating a backfill, you can view the backfill instances in Instance Operations.

* Alarm Monitor:

   * The batch alarm monitoring functionality displays batch tasks created under the current project, as well as near real\-time monitoring information. Monitoring types include rule monitoring and baseline monitoring.

   * Through the Alarm Record module, you can view all alarms that have been triggered under the project.


<span id="65e7be0c"></span>
## **Streaming task Operations**

The modules include Overview, Task Operations, and Alarm Monitor; the specific functions of each module are as follows:


* Overview:

   Provides an overview of all activated streaming tasks under the project, helping you gain a macro\-level understanding of the distribution of streaming task instance execution statuses, resource usage analysis, and other key metrics. You can quickly filter and analyze tasks by task type or owner, enabling you to better understand the running status of streaming tasks within the project, promptly identify and handle abnormal tasks, and improve streaming task operations efficiency.

* Task operations:

   * Display active tasks under the project.

   * View task running state, task lineage, operation log, execution log, and other information.

   * Perform alarm settings and alarm shielding actions for tasks

   * Perform state operations such as restart and stop on tasks.

* Alarm Monitor:

   * Display the execution monitor rules for streaming jobs created under the project

   * Through the Alarm Record module, view all triggered streaming task alarms under the project.
