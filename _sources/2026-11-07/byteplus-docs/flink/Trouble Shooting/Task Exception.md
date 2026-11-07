---
title: "Task Exception"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Task_Exception"
---

This text explains the basic troubleshooting steps for exceptions encountered during task startup and runtime.

<span id="4f9351ae"></span>
## Running Exception

If your task encounters exceptions during runtime, or even stops, you can generally view the task logs to analyze the causes of the exceptions and solve the problem.

<span id="34f763df"></span>
### View the JobManager logs of the task


1. In the **task management** page, click the target task name to enter the task details page.

   You can also select **Operation Management \> Log Service** from the left navigation bar and then view the logs.

2. In the task details page, click the **Logs** tab, and then choose the **Job Manager** log type.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c39936f0981443e83af343ce43e8d77~tplv-goo7wpa0wc-image.image" width="800px" /></div>



3. Set the task type to **ERROR** and automatically search for error logs.

   Please independently find the cause of the exception in the error logs and then resolve the issue.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b2ec08cce964c3290fb381f286e456d~tplv-goo7wpa0wc-image.image" width="770px" /></div>


<span id="f02fcdb3"></span>
### View the TaskManager logs of a task


1. In the **Task Management** page, click on the target task name to enter the task details page.

2. On the task details page, click the **Logs** tab, select **Task Manager** log type, and then click the target Task.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a9e34b9086649c3a7639c872ed5d9ff~tplv-goo7wpa0wc-image.image" width="750px" /></div>



3. Set the task type to **ERROR** and automatically query the error logs.

   Please independently identify the cause of the error from the error logs and then resolve the issue.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38c346295bc44156b8f5becbeacbd93e~tplv-goo7wpa0wc-image.image) </span>


<span id="6992ddde"></span>
## Startup Exception

If your task encounters an exception during startup, causing it to fail to start normally, you can investigate the failure reason by examining the event run.

<span id="b27c4284"></span>
### View Run Events


1. In the **Task Management** page, click on the target task name to enter the task details page.

2. On the task details page, click the **Run Events** tab to find the cause of the failure.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/681ab1d31cd44d408e4fd874f25684ca~tplv-goo7wpa0wc-image.image" width="800px" /></div>
