---
title: "Viewing job execution results"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View-job-execution-results"
---

After the job starts executing, you can go to the console to view job information, such as command information and command content. Besides, you can also view the execution results and statuses of the current job for each execution object in the console at any time.

<span id="WwKgnQP0"></span>
## Usage note

You can query the execution information of the last 60 days, and the maximum retention of execution information is 5000 entries.

<span id="bdlLIc8L"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant", and then select the "Job management" tab.

3. In the top menu bar, select the region where your business is located.

4. Find the target job in the job list or search by "Job name".

5. In the "Status" column of the target task, learn about its current overall execution status.

   * When a job involves instances that have not finished executing commands, the status is **In progress**.

   * When all instances of the job have finished executing commands:

      * If all instances execute commands successfully, the status is **Execution successful**.

      * If a job is executed successfully, but involves instance(s) that fail to execute the command, the status is **Partial failure**.

      * If job execution fails, or if all instance executions in the job fail, the status is **Execution failed**.

6. Click the target job name, or click the "Execution result" button in the "Action" column to open the job details page. Here, you can view job details and command execution results of each instance.

   * In the "Overview" tab, you can view job information (For example, job name and ID), command information (For example, command name and command execution path), and detailed command contents.

   * On the "Execution result" tab, you can view the command execution results of each instance:

      1. Select the **Waiting for execution**, **Execution successful**, **Execution failed**, **In progress, and Deleted** tabs to view information about instances with corresponding execution results. Instance information covers instance name/ID, status, used image, availability zone, instance type, and other information.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">When the execution mode of the target job is "Periodic execution", multiple execution results may exist for each instance.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">When the execution mode of the target job is "Immediate execution" or "Scheduled execution", each instance will have only one execution result.         </div>
         

      2. Click the "Run log" button in the "Action" column of the target execution object to view the information output when the current command is executed on the selected instance.


<span id="UCsJhmEq"></span>
## Related documents

[DescribeInvocationResults](https://docs.byteplus.com/en/docs/ecs/DescribeInvocationResults_-_View_command_execution_results)
