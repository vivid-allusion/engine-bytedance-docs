---
title: "Task Overview and Details"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Task_Overview_and_Details"
---

<span id="931158d9"></span>
# **Feature Overview**

In the Visual Knowledge Processing Task Overview section, you can view an overview of all visual knowledge processing tasks within the project, including task status statistics and task lists. In the details section of the visual knowledge processing task, you can view the detailed configuration information of the visual knowledge processing task, including basic information, processing flow, input and output table data preview, and operation records.

<span id="9167ad8c"></span>
# **Task Overview**

On the Task Overview page, users can view all visual modeling tasks within a project, and search for tasks by task name, input, output, and creator. Click on the visual knowledge processing task name to jump to the task details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33af46e7dff94d76af36e352d9fe365d~tplv-goo7wpa0wc-image.image) </span>

<span id="f5aaf712"></span>
## **Task status statistics**

The status of the most recent running record of each task business date is counted, and the status is filtered by clicking the card.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d037727aea0f49a6832a5dcea9d7c993~tplv-goo7wpa0wc-image.image) </span>

Definitions of each state:


|running state |instance state |explain |
|---|---|---|
|run successfully |success |All outputs are successful |
|failed to run |failure, termination |There is a failed or terminated output |
|running now. |Waiting for scheduling, waiting for upstream dependencies to complete, synchronization in progress |Executing output with no failures |
|other | |A task that has not yet been run and has no clear running status |


<span id="dd4c958b"></span>
## **Task list**

Search, supports searching tasks by task name/input/output/creator.


* filter

   * Operation Type: All/Manual/Periodic

   * Created by: Everyone/Just look at mine

* Sorting: Supports sorting by last run time.

* operation

   * Run: Select the output and business date of the task and run it in batches

   * Run record: Jump to the task details page Run record tab

   * Edit: Go to the task edit page

   * Delete: Delete to Recycle Bin, keep it for 15 days and delete it completely


<span id="f9cef684"></span>
## **Task action \- Run**

Support for manually triggering or backtracking the execution of specific interval tasks. Check the object that needs to be run, select the running business time, and click Confirm.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f06e98f15af4668a3839863689facbd~tplv-goo7wpa0wc-image.image) </span>

<span id="2ac881ca"></span>
## **Task operation \- Run log**

Click on the running record to jump to the details page of the task to view the running record of the task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7db43b24e34d496fbb2c0c1b7a03645d~tplv-goo7wpa0wc-image.image) </span>

<span id="381a5f52"></span>
## **Task action \- Edit**

Clicking the Edit button will take you to the Edit page of the task.

<span id="fe726119"></span>
## **Task action \- Delete**

Users can quickly delete tasks with one click on the overview page. The deleted tasks will enter the Recycle Bin, and the tasks will no longer be scheduled to run. The tasks can be restored within 15 days, and will be automatically deleted after 15 days. This operation only deletes the modeling task, not the corresponding dataset data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96082dcd1d5f40ccbee81818cc9f8f9c~tplv-goo7wpa0wc-image.image) </span>

<span id="901db047"></span>
# Offline T**ask Details**

<span id="a6bf87bf"></span>
## **Basic information**

Task basic information: creator, creation time, running frequency, last running time, last modified time and other information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c194e685a9d448098928df10661e8c0b~tplv-goo7wpa0wc-image.image) </span>

The top supports the following operations:


* Permission assignment: Assign permissions to visual modeling tasks.

* Edit: Edit and modify the dataset configuration.

* Operations: rename, move, copy, authorize, transfer owner, delete.


<span id="be06f583"></span>
## **Processing flow**

**Processing flow preview:**  support zoom and drag to view; **output list:**  display the corresponding table name and recent run information of the output node.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e17759e1f6ba45f5bfc812c1c8f99833~tplv-goo7wpa0wc-image.image) </span>

<span id="f833d4bd"></span>
## **Data preview**


* Support for selecting input/output tables.

* Support table structure/detailed data two preview modes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09cf971dd0b344409ff0d26bfb94e93b~tplv-goo7wpa0wc-image.image) </span>

<span id="3a481b38"></span>
## **Run record**

You can view and quickly modify the running configuration.

Support viewing the running record list:


|function |explain |
|---|---|
|search |Support search output table |
|filter |Support running state filtering |
|list operation |All states support "re\-run", and the running state supports "terminate". |
|batch run |Select output data and business date, submit batch run |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1fd24f411d64250b184059b15448045~tplv-goo7wpa0wc-image.image) </span>

<span id="78615dc8"></span>
## Bloodline view

There are two display modes of bloodline: **graph mode and list mode** .


* **Graph method** : display blood relationship with visual graphic link, clear and intuitive.

* **Table mode** : Display specific resources in table form, quickly understand the specific resource list, and facilitate the positioning of an asset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f7659d1f4e44481962b80a27c06c6f1~tplv-goo7wpa0wc-image.image) </span>

<span id="5e3004a9"></span>
# Live Task Details

The real\-time task details page displays the basic information of the task (creator/creation time, etc.), which is convenient for users to view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7429d891afb47e5a78b08cf52b602f8~tplv-goo7wpa0wc-image.image) </span>


* **Operation & Consumption Records** :

   * Run record: Display the basic information of the output node and "output content".

   * Production and consumption statistics: display task names for easy identification; support sliding to view, adapt to multi\-task display, and support hovering to view complete information.

* **Monitor the configuration process:** 

   * Consumption monitoring: Consumption monitoring conditions can be added, and three options can be selected, namely, consumption delay monitoring, write interruption monitoring, write rise monitoring, and input continuous x minutes, and cumulative consumption delay greater than x strips of 1 data.

   * Task Monitoring: Select the data file to be monitored

   * Monitor notifications: Choose how to receive dirty data alerts, email, WebEx, email group

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66914735ab144447af10fc49f170b227~tplv-goo7wpa0wc-image.image" width="2816px" />   </div>
   

* **Processing flow:** 

   * Process flow preview: support zoom and drag to view;

   * Output list: shows the corresponding table name and recent run information of the output node;

* **Data preview:** 

   * Support for selecting input/output tables.

   * Support table structure/detailed data two preview modes;


<span id="36c15c77"></span>
# **Recycle Bin**

Click on **Recycle Bin** to see the visual modeling tasks deleted in the past 15 days, including task name, owner information, remaining time for complete deletion, complete deletion/recovery.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a265603a6db74dca8d75aee5bbd22d88~tplv-goo7wpa0wc-image.image) </span>

<span id="e80ac6dd"></span>
# Common Problem

**Q1**: If the daily effective time is set to 0:00\-24:00 (i.e. all day), and the task interval is 30min, will it be recalculated when 0:00 is reached due to the 30\-minute task interval? For example, if a task was executed at 23:50 the night before, will the next task be executed at 0:20, or will the task execution cycle time be resumed at 0:00 every day?

**A**: The time will not be recalculated at 0:00. The next task calculation time in this example is 0:20.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0100d8c074448a19540a2ff4aa4734e~tplv-goo7wpa0wc-image.image) </span>
