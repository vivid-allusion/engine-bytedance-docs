---
title: "Overview"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/batch_task_operations_overview"
---

Present the overall situation of active tasks under the project. This helps users gain a macro\-level understanding of the distribution of task instance states and running periods for the current day, as well as information such as the number of tasks per owner, task type distribution, task scheduling method distribution, historical task run analysis and ranking, and other related information. At the same time, users can quickly identify and handle abnormal tasks, thereby improving operational efficiency.

<span id="625d32ab"></span>
## Instructions

The Overview interface provides statistics on the execution status of periodic scheduling tasks, manual tasks, and data integration tasks for each engine in the current project, and offers corresponding analysis of task operation status. Data is presented through the following three modules: **Today's instance execution distribution, Project task statistics, and Historical task execution analysis**.


* **Today's instance execution distribution**: Statistics on the distribution of execution states for instances scheduled to execute between today at 0 o'clock and the current time, as well as the distribution of instance execution counts across different time periods.

* **Task statistics for project**: Displays, as of the current time, statistics on the number of tasks for each owner under the project, statistics on the number of activated task types, and statistics on the status of task alarm settings.

* **Historical task execution analysis**: Displays the rankings of historical tasks under the current project by time spent and by execution failure count.


<span id="进入运维概览"></span>
## Enter the operation overview


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. For a specific project on the overview page, click the **Maintenance** button to enter the Batch Task Operations interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b5346e267ee40989fa2bf22494bd04e~tplv-goo7wpa0wc-image.image) </span>

3. In the left navigation bar, choose the **Overview** tab.


<span id="查看运维概览"></span>
## View the operation overview

<span id="今日实例运行分布"></span>
### **Today's running instance distribution**


1. Instance state distribution

   Displays the status of instances whose set execution time falls within the range from 0 o'clock today to the current time, including those that have run successfully, failed, or are pending execution. You can click a colored segment in the pie chart to access the instance list for the corresponding state.

2. Number of running instances in each time period

   Displays distribution statistics of instance running time across different intervals between 0 o'clock and the current time, and allows switching to minute\-level granularity or comparing with yesterday. You can also drag the timeline below to view the distribution of instances within a specific running time period.

3. Instance execution distribution for more dates

   Click the **More dates** button in the upper right corner to view the instance execution distribution for dates such as **Yesterday, Last 3 days, Last 7 days, Last 15 days, and Last 30 days**. In the instance execution distribution window, click the color block legend in the distribution chart to view the details of the instance list for the selected date range and perform the corresponding instance operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bddab97321fd4fdb949594938f280e1d~tplv-goo7wpa0wc-image.image) </span>

<span id="项目下的任务统计"></span>
### **Task statistics for projects**


1. Task count for each owner

   Displays the number of tasks for each owner in the project as of the current moment, including total tasks, tasks not yet deployed, enabled tasks, disabled tasks, periodic scheduling tasks, and manual scheduling tasks.

2. Statistics for each type of Deploy Task

   Displays the distribution of types of active Deploy Tasks in the project as of the current time.

3. Statistics of deploy task alarm settings

   Statistics on alarm settings for different types of deploy tasks within the project as of now.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e91a31cf50884e398b8a3cdb767e7b72~tplv-goo7wpa0wc-image.image) </span>

<span id="任务历史运行分析"></span>
### **Running analysis of task history**

Running Time filtering is supported, allowing you to view historical run analysis for Today, Yesterday, Past 3 Days, Past 7 Days, Past 15 Days, and Past 30 Days.


1. Task ranking by time spent running

   Display the ranking of all tasks by time spent running within the selected time range.

   * Click the “**View**” button on the right to view a line chart showing the time spent running this task over the last 30 days.

   * Click the "**export**" button in the upper right corner to export the run time ranking in Excel format to your local device.

2. Task ranking by number of failures

   Displays the ranking of all tasks by number of failures within the selected time range.

   Click the "**export**" button in the upper right corner to export the ranking of failed runs by number of failures in Excel format to your local device.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/496f5e73866049d58fc6bb1ebcc85d29~tplv-goo7wpa0wc-image.image) </span>
