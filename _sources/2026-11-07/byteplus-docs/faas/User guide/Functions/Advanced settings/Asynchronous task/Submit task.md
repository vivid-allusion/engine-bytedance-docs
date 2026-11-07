---
title: "Submit task"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Submit_task"
---

This article introduces how to submit an async task. After the task is successfully submitted, the FaaS will return the status code 202 (Accepted) along with the unique identifier RequestID. RequestID can be used to subsequently query the execution status of the task or to terminate the task.

<span id="webserver-mode"></span>
## WebServer Mode

For async tasks in WebServer mode, there are three supported methods to submit a task.

<span id="scheduled-submission"></span>
### Scheduled Submission

Once released tasks, you can configure a [Timer trigger](https://docs.byteplus.com/en/docs/faas/Creating_a_Timer_trigger) for the task to enable scheduled execution.

<span id="console-test"></span>
### Console test

After successful service release, the console supports initiating function tests, simulating scheduled submission of tasks, or submitting tasks through the gateway domain name. For details, refer to [Function testing](https://docs.byteplus.com/en/docs/faas/Function_testing).

<span id="in-non-webserver-mode"></span>
## In non\-WebServer mode

In non\-WebServer mode, async tasks can be submitted in three ways.

<span id="scheduled-submission"></span>
### Scheduled Submission

Once released tasks, you can configure a [Timer trigger](https://docs.byteplus.com/en/docs/faas/Creating_a_Timer_trigger) for the task to enable scheduled execution.

&nbsp;

<span id="console-test"></span>
### Console test

After successful service release, the console supports initiating function tests, simulating scheduled submission of tasks, or submitting tasks through the gateway domain name. Among these, when submitting tasks using the simulated API Gateway domain method, it supports a custom start command.


1. On the function details page, click **Test**.

2. On the function test page, configure the relevant parameters.

   
   |Parameter |Description |
   |---|---|
   |Trigger type |Supports **Timer Trigger** and **API Gateway Trigger**. |
   |Startup command |When selecting the **API Gateway Trigger**, it supports custom start commands. If it is empty, the function's default start command will be used. |
   

3. Click **Test**.

   After the task is successfully submitted, the console will return the RequestID. Click **View Details** to jump to the async task list, where you can view the execution status of the current task.
