---
title: "Running multiple ArkClaw O&M commands at a time"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Running_multiple_ArkClaw_OM_commands_at_a_time"
---

Batch O&M is designed to meet the O&M requirements of enterprise\-grade large\-scale deployments. It is primarily used for the efficient management of multiple instances and resources. This reduces repetitive O&M operations, improves O&M efficiency, minimizes misoperations, and ensures cluster configuration consistency and stability across multiple instances. This topic describes how to create a job and run multiple O&M commands on ArkClaw instances at a time.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[Beta] This feature is in the beta phase. To use it, read the disclaimer and contact your customer manager to obtain the trial use permissions.</div>


<span id="bFSIaVDU"></span>
## Disclaimer

The batch O&M feature allows you to define execution code and script logic. The platform only provides a unified scheduling and execution channel for batch O&M. **It does not perform syntax validation, logic verification, security audit, or correctness assurance for the submitted O&M code content**. You need to ensure the compliance, accuracy, and security of the run code, evaluate execution risks, and perform a thorough test.

You shall be independently and wholly responsible for all losses, such as service exceptions, data loss, and business interruption, caused by invalid code, logic defects, improper configuration, or malicious code. **The platform assumes no legal or joint compensation liability**.

<span id="j9wwdlgK"></span>
## Prerequisites


* The ArkClaw instances for which the batch O&M job is to be executed are in the "Running" state.

* O&M commands have been prepared and fully verified to ensure the commands are available and do not pose data loss risks.

* (Recommended) Before you execute a batch job, we recommend performing an ArkClaw data backup for quick rollback if needed.


<span id="BSMplvEa"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **O&M \> Batch O&M**.

3. Click **Create job**. Specify the parameters of the batch job based on your business requirements and then click **Confirm** to immediately execute the batch O&M job.

   
   |Configuration item |Description |
   |---|---|
   |Job name |Specify a custom job name. |
   |Command type |Select the type of O&M command. Only the Linux shell is supported. |
   |Command details |Edit or paste the prepared O&M command in the custom command input area.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When you distribute O&M commands in batches, you need to import environment variables. Do not modify the following preset commands when configuring custom commands.</div><br><br><br><div data-tips="true" data-tips-type="warning">```Shell```<br>```export HOME=/root ```<br>```export XDG_RUNTIME_DIR=/run/user/$(id -u) ```<br>```export DBUS_SESSION_BUS_ADDRESS=unix:path=${XDG_RUNTIME_DIR}/bus```<br></div><br> |
   |Job timeout |The timeout period for executing the O&M command on each instance. Value range: 30 seconds to 24 hours. After the command execution times out, the cloud assistant will mark the job as failed on the corresponding instance and forcibly terminate the job process. |
   |Object |Select ArkClaw instances that meet your job execution requirements by instance name, project, tag, or other information.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can select up to 200 execution objects for each O&M job.</div><br> |
   |Execution time |Batch jobs can be immediately executed. The commands will run on the selected ArkClaw instances immediately after the job is created. |
   

4. After the job is complete, you will return to the Job list tab. Click **Execution result** in the Actions column that corresponds to the target job to view the job execution results for all ArkClaw instances.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the job fails to be executed on an instance, click <strong>View logs</strong> in the Actions column that corresponds to the execution result to view detailed logs and locate the issue.   </div>
