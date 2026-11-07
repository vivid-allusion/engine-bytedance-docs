---
title: "Create scheduled tasks"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-scheduled-tasks"
---

ByteHouse Enterprise Edition supports the function of scheduled tasks. By automating tasks, it can perform scheduled queries, data imports, and other operations, thus enhancing automation capabilities, reducing operational costs, and improving work efficiency.

<span id="cf223cf2"></span>
## Scheduled tasks overview

ByteHouse supports creating and managing scheduled tasks through the interface, which include the following types:


* Query Task: Supports running the SQL query on a schedule

* Data Import Task: Scheduled launch of the import execution task

* DataRanger's Technical Support Tasks: Cluster upgrade, cluster restart, etc. (Currently supports display only)


<span id="d867b4ec"></span>
## Query task

<span id="c9ad1b43"></span>
### New scheduled task


1. Visit the Task Center \-\> Cron tasks, and click on Create cron task \-\> Query task.

2. Input the following information:

   * Alert name

   * Scheduling time: 24\-hour format, can be configured daily, monthly, or weekly through CRON expression

      (e.g., If it runs every Monday at 9:30 AM, the expression is `30 9 * * *`)

   * Hover over the date to check the exact date and time of repeated tasks, with a visibility up to five weeks

   * Input the SQL to be scheduled

   * Select "Create" to complete the creation of the new scheduled task

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d4a2493e0384d45a265722922eb0bb7~tplv-goo7wpa0wc-image.image) </span>

> In addition to the scheduled task page, you can also directly select the query from the SQL Worksheet to create a scheduled task


<span id="623cc1f8"></span>
### View execution record


1. If you want to check the execution status of SQL, you can visit Data Query \-\> History to see the corresponding query history and whether it ran on time.

2. To view the status of scheduled tasks, access the Task Center \-\> Scheduled Tasks List page. Includes SQL query tasks and data import tasks; click on the Task ID to view the execution records.

   * Scheduled task statuses include: Running/Stopped/Complete

   * Supported actions: Start/Suspend, with support for pausing scheduled tasks

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d336d8df31884b4b8e02bf330e9c840c~tplv-goo7wpa0wc-image.image) </span>


<span id="a94b0646"></span>
## Import data

<span id="d6c27ca8"></span>
### Create new scheduled task

> Note: Before creating a scheduled data import task, please ensure you have already imported data on the Data Import page and have the name of the data import task.


1. Click Create New Scheduled Task \-\> Data import job.

2. Input the following information:

   1. Scheduled Task Name

   2. Scheduling Time

   3. Select Import Task

   4. If it is a file import task (such as the datasource is object storage), select the file path, and you can use regular expressions to match


<span id="f6a15b0e"></span>
### View execution record


1. Access Data Import \-\> Execution Plan

2. View the list of scheduled tasks: Access the Task Center \-\> Scheduled Tasks; the list includes SQL query tasks and data import tasks. Click on the Task ID to view the execution record.

   * Scheduled task statuses include: Running/Stopped/Complete

   * Supported actions: Start/Suspend, with support to suspend scheduled tasks


<span id="d0880303"></span>
## Maintenance center

The current ByteHouse Enterprise Edition supports viewing ongoing and completed technical support tasks, including creating tables and databases, cluster upgrades, rollbacks, vertical configuration changes, etc., facilitating the review and filtering of historical actions, retries, and thereby tracking and backing up past operation records.

You can View by accessing Task Center \-\> DataRanger's Technical Support Tasks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc36c25e47c44d41a070b09fc49ce8d8~tplv-goo7wpa0wc-image.image) </span>
