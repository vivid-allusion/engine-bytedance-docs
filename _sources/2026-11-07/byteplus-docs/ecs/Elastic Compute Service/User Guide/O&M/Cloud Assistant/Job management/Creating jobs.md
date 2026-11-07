---
title: "Creating jobs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-a-job"
---

You can create jobs in immediate, scheduled, and periodic execution modes. After being created, jobs are automatically executed by the cloud assistant Agent in the specified execution mode.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before jobs are executed by the cloud assistant, make sure that objects meet the following conditions:


* Status is **Running** (`Running`).

* You have installed the cloud assistant Agent. For detailed operations, refer to [Installing cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* The maximum number of concurrent O&M tasks can not exceed 100.

* If your cloud assistant Agent version is ≤ v1.6.0 and you execute the `systemd daemon-reload` command while the cloud assistant Agent is running, jobs or PIDs launched via cloud assistant may have Cgroup drift. This can eventually cause CPU throttling or out\-of\-memory (OOM) issues for the affected job or process. For detailed upgrade instructions of the cloud assistant Agent, refer to [Upgrading cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Upgrading-or-uninstalling-agents#upgrading-agent).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant", and then select the "Job management" tab.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you access the cloud assistant for the first time, follow the system instructions and click the "Immediately create" button on the Cross\-service access request page. This authorizes the platform official service account to access your ECS instance information. For details of the IAM feature that requires authorization, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-3">IAM overview</a>.   </div>
   

3. In the top menu bar, select the region where your business is located.

4. Click the "Create a job" button to enter the Create a job page.

5. Enter the following job information as instructed.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Job name |Set the job name. |Install the Cloud Monitor plugin |
   |**Execute command** |||
   |Command source |Select the type of O&M command that you want to execute, with currently supported types as follows:<br><br><br>* **Public commands**: Common O&M commands preset by the platform. For details, refer to [Public command summary](https://docs.byteplus.com/en/docs/ecs/Managing-public-command).<br><br>* **Custom commands**: If the preset commands do not meet your O&M requirements, you can create custom commands to perform O&M operations. For details, refer to [Custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands).<br><br>* **Manual input**: For simple O&M commands that require no dynamic content, you can manually enter the command here and directly create an O&M task for execution. |Public commands |
   |Command |Select the public command or custom command that you need to execute. |Install Cloud Monitor Agent on Linux instance |
   |Command type |When you select the "Manual input" command, you can use commands of the `Linux Shell`, `Python`, `Windows PowerShell`, or `Windows Bat` type. |\- |
   |Execute path (**optional**) |Enter the command execution path.<br><br><br>* For Linux instances, the default execution path is `/home`.<br><br>* For Windows instances, the default execution path is `C:\Windows\System32`. |/home |
   |Parameter​ |Specify values for custom parameters when you enter execution commands. For parameter descriptions, refer to [Public command summary](https://docs.byteplus.com/en/docs/ecs/Managing-public-command).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You are required to specify parameter values only for commands that use custom commands and public commands.</div><br> |\- |
   |Executing user |You can specify an existing user in the target instance to execute commands. We recommend that you avoid using the root user to reduce security risks.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specify a user with the permission to execute commands.</div><br> |user1 |
   |Login password |Enter the login password for the execution user.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You are required to enter the login password only if the command meets one of the following conditions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the command source is "Public commands" or "Custom commands", the commands are Windows\-related, and the execution user is not "system", you are required to enter the login password.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the command source is "Manual input", the command type is <code>Windows PowerShell</code> or <code>Windows Bat</code>, and the execution user is not "system", you are required to enter the login password.</div><br> |\- |
   |Timeout period |Set the timeout period for command execution on each instance. If the command execution times out, the cloud assistant will mark the job as failed on the corresponding instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default timeout period varies by commands, and you can manually adjust it within the range of 30 seconds to 86,400 seconds.</div><br> |60 seconds |
   |**Execution mode** |||
   |Execution mode |For the job execution modes, the following options are available:<br><br><br>* **Execute immediately**: After the job is created, it is executed for one time immediately.<br><br>* **Scheduled execution**: The job is executed automatically once at the time you specify.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The execution time must be accurate to the minute and must not be earlier than the current time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can manually stop scheduled jobs in the <strong>Waiting for execution</strong> or <strong>In progress</strong> state. For operation details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Stopping-task">Stopping jobs</a>.   </div><br>   <br><br>* **Periodic execution**: The job is executed automatically on a cycle starting from the specified start time, at intervals you specify (in minutes, hours, or days), and stops automatically at the specified end time. You need to configure the following information:<br><br>   * **Repeat cycle**: Specify the interval at which the job is executed repeatedly. The repeat interval must be longer than the timeout period. Value:<br><br>      * by minute: The minimum interval is 5 minutes.<br><br>      * by hour: The minimum interval is 1 hour.<br><br>      * by day: The minimum interval is 1 day.<br><br>   * **Start time**: Specify the time when the periodic job is first executed. This time must be later than the current time.<br><br>   * **Stop time**: Specify the time when the periodic job stops. The job automatically stops at this time. For jobs in the periodic execution mode, you can manually stop those in the **Waiting for execution** or **Executing periodically** state. For operation details, refer to [Stopping jobs](https://docs.byteplus.com/en/docs/ecs/Stopping-task).<br><br>      * If the job is not being executed at the stop time, it automatically stops and will never be executed again.<br><br>      * If the job is being executed at the stop time, it automatically stops after the execution is complete and will never be executed again.<br><br>      * If the interval between the stop time and the start time is less than one repeat cycle, the job is executed only once.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The execution interval is independent of the actual execution duration of the job and is calculated based on the "Start time" you specify. For example, if the start time for a job is <code>2022-12-20 11:00:00</code>, the repeat cycle is 1 hour, and the duration of the first execution is 3 minutes, the second execution starts at <code>2022-12-20 12:00:00</code>.   </div><br>    |Execute immediately |
   |**Execute object** |||
   |Object |Select ECS instances that meet the requirements for you to execute the job by instance name, project, tag, or other information. You can select multiple instances at one time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select up to 200 ECS instances.</div><br> |\- |
   |**Advanced configuration** |||
   |Project |You can add the Cloud assistant to the project and manage it uniformly by project dimension, which helps maintain resource independence and ensure data security. For more project details, refer to [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |default |
   |Tag |A tag is a key\-value pair used to identify resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your resources. For more information about tags, refer to [Tags](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key1:Value1 |
   

6. Click the "Confirm" button to create the job.

7. After the job is created, the system automatically redirects you to the Job management page. The new job then executes automatically based on its execution method.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The maximum number of concurrent O&M tasks can not exceed 100.   </div>
   

<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

To learn about job execution results and statuses, refer to [Viewing job execution results](https://docs.byteplus.com/en/docs/ecs/View-job-execution-results).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [RunCommand](https://docs.byteplus.com/en/docs/ecs/RunCommand_-_Execute_command): Creates and executes commands on one or more ECS instances.

* [InvokeCommand](https://docs.byteplus.com/en/docs/ecs/InvokeCommand_-_Execute_command): Triggers an O&M assistant command for one or more ECS instances.
