---
title: "Batch installing Cloud Monitor plugin"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Batch-install-cloud-monitor-plugin"
---

This topic describes how to use the cloud assistant feature to batch install the Cloud Monitor plugin on Linux ECS instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also manually install the Cloud Monitor plugin on the target instance. For more details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent">Installing an agent</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Cloud assistant Agent is installed on the instance. For operation details, refer to [Installing cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

You can install the Cloud Monitor plugin on your instance to monitor metrics for the instance in dimensions such as operating system, TCP connection, and process.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Monitoring \> Cloud assistant," then select the "Job Management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Click the "Create a job" button to enter the Create a job page.

5. Enter the following job information as instructed.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Job name |Set the job name. |Install Cloud Monitor plugin |
   |Command type |Select **Public commands**. |\- |
   |Command |Select "Install Cloud Monitor Agent on Linux instance". |\- |
   |Execution path |Enter the command execution path. For Linux instances, the default path is `/home`. |/home |
   |Execute user |You can specify an existing user in the target instance to execute commands. We recommend that you avoid using the root user to reduce security risks.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specify a user with the permission to execute commands.</div><br> |user1 |
   |Timeout |Set the timeout period for command execution on each instance. If the command execution times out, the O&M assistant marks the job as failed on the corresponding instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the job type in this topic, the default timeout period is 120s. You can manually adjust the period from 30s to 1800s.</div><br> |100 |
   |Execution mode |Select "Execute immediately". This indicates that after the task is created, it is executed immediately. |\- |
   |Object | |\- |
   

6. Click the "Confirm" button to complete the job creation.

7. After the job is created, the system automatically redirects you to the Job management page. The new job is then executed immediately.


<span id=".5p-l55yL5a6J6KOF57uT5p6c"></span>
## View installation result


1.   Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Monitoring \> Cloud assistant," then select the "Job Management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Find the target job in the job list or search by "Job name".

5. Click the target job name or the number in the "Execution result" column to open the job details page.

6. Select the "Execute object" tab to view the command execution results for each instance.

   To view the command output during execution on an instance, click the "+" button on the left side of the target instance name.

7. If the task status is **Execution successful**, the Cloud Monitor plugin has been successfully installed on all instances.
