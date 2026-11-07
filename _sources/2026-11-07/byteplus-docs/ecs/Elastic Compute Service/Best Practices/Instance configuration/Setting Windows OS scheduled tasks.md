---
title: "Setting Windows OS scheduled tasks"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Settings_Windows_Scheduled_Tasks"
---

Task Scheduler is a task scheduling tool in Windows used to create and manage tasks. The scheduled tasks can run automatically based on the trigger conditions you set. To create scheduled tasks for operations, such as regular backups, system maintenance, and automatic script execution, refer to this topic for guidance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have [created an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* The ECS instance status is **Running**.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

In the example provided in this topic, a Windows Server 2022 Datacenter Edition 64 bit English image is used to create one scheduled task. The task involves actions of restarting the ECS instance at a specified interval and starting the Notepad program each time the server starts.

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a6a5pe26YeN5ZCv5Lu75Yqh"></span>
### Step 1: Create a task for scheduled restarts


1. [Log in to the target Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the "Windows" icon and then select "Windows System \> Run".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2c44dff7e90b42224bea79fdf88b330.png) </span>

3. Enter the following content in the dialog box and click the "OK" button to open the Task Scheduler dialog box.

   ```Plain Text
   taskschd.msc
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_336a87014790031c54e94201aa84d6c6.png) </span>

4. In the left directory tree, select "Task Scheduler (Local) \> Task Scheduler Library".

5. In the "Actions" module on the right, click the "Create Task..." button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_99a3dc68538401dbbf98bb5acc76966f.png) </span>

6. Create the scheduled task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Below are the parameters necessarily involved. For more parameters, see <a href="https://learn.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page#run-time-requirements">Task Scheduler for developers</a>.   </div>
   

   1. In the "General" tab, configure the basic information of the scheduled task as follows.

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Name |Indicates the scheduled task name. |Reboot |
      |Security options |Configure security\-related options.<br><br><br>* `When running the task, use the following user account`: Specifies the user account for which to run the task. By default, the currently logged\-in account is used. You can change the account based on your needs after clicking the "Change User or Group" button.<br><br>* If you select `Run only when user is logged on`, the task runs only when the specified user account is logged in.<br><br>* If you check the `Run with highest privileges` option, the highest permissions are granted during the task runtime. This prevents the scheduled task from failing for permission\-related reasons. |\- |
      

      Configuration example:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e3cdfbb28580bfe4f53b72490168eb0f.png) </span>

   2. Select the "Triggers" tab, and then configure the task trigger.

      1. Click the "New..." button to create a new trigger.

      2. Configure trigger conditions.

         
         |Parameter |Description |Sample value |
         |---|---|---|
         |Begin the task |Indicates the trigger condition to start the task. Here, select `On a schedule` (task is started as scheduled).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the example provided in this topic, "On a schedule" is used. For more available trigger conditions, see <a href="https://learn.microsoft.com/en-us/windows/win32/taskschd/task-triggers">Task Triggers</a>.</div><br> |On a schedule |
         |Settings |Configure the task running cycle.<br><br><br>* Start: Indicates the time when the task will run for the first time.​<br><br>* Daily: Indicates the task runs repeatedly at a specified daily interval.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the example provided in this topic, the scheduled task runs repeatedly at the same time every day, starting from <code>8/12/2024 4:40:11 PM</code>. Adjust the time based on your needs.</div><br> |\- |
         

         Configuration example:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64d781581e39fb2b65f2cac26b7cd676.png) </span>

      3. Click the "OK" button to complete the creation.

   3. Select the "Actions" tab, and then configure the action the scheduled task performs.

      1. Click the "New..." button to create a new action.

      2. Configure the action of restarting the server.

         
         |Parameter |Description |Sample value |
         |---|---|---|
         |Action |Indicates the action type. Select `Start a program`. |Start a program |
         |Settings |Specifies action details.<br><br><br>* `Program/script`: Specifies the target program or script. Enter `shutdown`.<br><br>* `Add arguments (optional)`: Specifies arguments contained in the script. Enter `/r /f /t 0`. |\- |
         

         Configuration example:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ed9885d6622e44e384b3e2d5cf93759.png) </span>

      3. Click the "OK" button to complete the configuration.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_db14fa06a56fb142f2be6c410a7e413e.png) </span>

7. In the pop\-up window, enter the login password of the user account for which to run the task, and then click the "OK" button to complete creating the task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5700be2f042a4b56d6bc9e40e88edb4.png) </span>


<span id=".5q2l6aqk5LqM77ya5Yib5bu65byA5ZCv6Ieq5ZCv5Yqo56iL5bqP5Lu75Yqh"></span>
### Step 2: Create a task for program auto\-start


1. [Log in to the target Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the "Windows" icon and then select "Windows System \> Run".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2c44dff7e90b42224bea79fdf88b330.png) </span>

3. Enter the following content in the dialog box and click the "OK" button to open the Task Scheduler dialog box.

   ```Plain Text
   taskschd.msc
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_336a87014790031c54e94201aa84d6c6.png) </span>

4. In the left directory tree, select "Task Scheduler (Local) \> Task Scheduler Library".

5. In the "Actions" module on the right, click the "Create Task..." button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_99a3dc68538401dbbf98bb5acc76966f.png) </span>

6. Create the scheduled task.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Below are the parameters necessarily involved. For more parameters, see <a href="https://learn.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page#run-time-requirements">Task Scheduler for developers</a>.</div>



   1. In the "General" tab, configure the basic information of the scheduled task as follows.

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Name |Indicates the scheduled task name. |OpenNotepad |
      |Security options |Configure security\-related options.<br><br><br>* `When running the task, use the following user account`: Specifies the user account for which to run the task. By default, the currently logged\-in account is used. You can change the account based on your needs after clicking the "Change User or Group" button.<br><br>* If you check the `Run only when user is logged on` option, the task runs only when the user account for which to run the task is logged in.<br><br>* If you check the `Run with highest privileges` option, the highest permissions are granted during the task runtime. This prevents the scheduled task from failing for permission\-related reasons. |\- |
      

      Configuration example:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aecc05399f9685deec8e58dd8bbeefc8.png) </span>

   2. Select the "Triggers" tab, and then configure the task trigger.

      1. Click the "New..." button to create a new trigger.

      2. Configure trigger conditions.

         
         |Parameter |Description |Sample value |
         |---|---|---|
         |Begin the task |Indicates the trigger condition to start the task. Here, select `At log on` (login is the trigger condition).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the example provided in this topic, "At log on" is used. For more available trigger conditions, see <a href="https://learn.microsoft.com/en-us/windows/win32/taskschd/task-triggers">Task Triggers</a>.</div><br> |At log on |
         

         Configuration example:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_67a750eede2895408f3f892247b6e20e.png) </span>

      3. Click the "OK" button to complete the creation.

   3. Select the "Actions" tab, and then configure the action the scheduled task performs.

      1. Click the "New..." button to create a new action.

      2. Configure the action of restarting the server.

         
         |Parameter |Description |Sample value |
         |---|---|---|
         |Action |Indicates the action. In the example provided in this topic, select `Start a program` (action is starting a program). |Start a program |
         |Settings |Specifies action details.<br><br>`Program/script`: Specifies the program to run at startup.<br><br><br>1. Click the "Browse..." button.<br><br>2. Select the "notepad" program, and then click the "Open" button.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a36232cec9384d5e1e0550f58fd8d5a6.png) </span><br><br>3. Click the "OK" button to complete the creation.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e1291f9b76525e31f134020b4840161.png) </span><br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In this example, the Notepad program is automatically started at startup. Change it to the target program or script based on your needs.</div><br> |\- |
         

      3. Click the "OK" button to complete the configuration.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_62b93b5fa18793a7dda3f2dbe9b48e88.png) </span>

7. In the pop\-up window, enter the login password of the user account for which to run the task, and then click the "OK" button to complete creating the task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5700be2f042a4b56d6bc9e40e88edb4.png) </span>
