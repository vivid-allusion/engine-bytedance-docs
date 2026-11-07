---
title: "Getting started with function deployment"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/FaaS_Quick_Start"
---

This topic describes the basic veFaaS capabilities and provides procedures for using veFaaS to help you get started quickly.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* A function in veFaaS is the fundamental execution unit of the compute service. With veFaaS, you can simply write business logic and configure triggers, with no server provisioning or infrastructure management required. This eliminates operational burdens while ensuring highly reliable, zero\-maintenance execution.

* This topic demonstrates how to create a Hello World function in the China (Beijing) region, set a timer trigger, and verify whether the function behavior meets expectations.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have completed account registration and verification. For details, see [Account registration and verification](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Log in to the [Function Service Console](https://console.byteplus.com/vefaas) and activate veFaaS based on the on\-screen instructions.

* If you need to enable the VPC invocation feature, ensure that you have activated BytePlus VPC and created a VPC, subnets, and security groups in the region where the function will be deployed. For details, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC)[Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* If you need to deliver function logs to a custom log store, ensure that you have activated BytePlus TLS and created the required TLS resources. For details, see [Creating log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Creating log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).


<span id=".5q2l6aqk5LiA77ya5Yib5bu65Ye95pWw"></span>
## Step 1: Create a function

Create a fundamental unit for scheduling and running function code.


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Function \> Function management**. On the **Function** page, click **Create function**.

4. On the Select function creation method page, click **Event function** \> **Create Event function.** 

   Specify some parameters of the function based on the following requirements. For other parameters, see [Creating event functions](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Provide a custom function name. In this example, set it to `hello-faas-demo`.<br><br>Function names must be unique within the same account. You cannot modify the function name after you create it. |
   |Runtime |Select a runtime environment for running the function. Keep the default **Python 3.12** runtime. |
   |Code package type |Select **Function template \> Hello World template**. |
   |Logging |Enable logging and select **Default log project**. |
   

5. Click **Confirm** to create the function.

   When the function is created, the system will automatically redirect to the function details page.


<span id=".5q2l6aqk5LqM77ya5Y-R5biD5Ye95pWw"></span>
## Step 2: Release the function

Release the function code and configuration.


1. On the function details page, click **Release** in the upper right corner.

2. In the function release panel, set the release parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Function revision |In this example, select **Latest**, which means releasing the function based on the current code and configuration. |
   |Version description |Describe the function version. This parameter can be left blank. |
   |Minimum instances |Specify the minimum number of instances (reserved instance count). The system will maintain and continuously run at least this number of instances until you set it to 0.<br><br>Reserved instances are billed continuously. For billing details, see [Billing overview](https://docs.byteplus.com/en/docs/faas/Billing_overview). |
   |Maximum instances |When you release a function version for the first time, you need to configure the maximum number of instances (upper scaling limit) required to support business operations. This value specifies the maximum number of instances that the function can scale to.<br><br>After the function is successfully released, the function resource settings will actually take effect. In this example, keep the default setting. |
   

3. Click **Confirm** to release the function.

   The function is successfully released if you see the following information on the page.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66Kem5Y-R5Zmo"></span>
## Step 3: Create a trigger

Configure a trigger for the function as needed to trigger function execution by the specified event types. This example creates a timer trigger to execute the function at scheduled intervals.


1. Go back to the function details page, and on the **Trigger** tab, click **Create trigger**.

2. In the **Create trigger** panel, configure the following parameters as described and keep the default settings for the remaining parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Trigger type |In this example, select **Scheduled trigger**. |
   |Trigger name |Specify a custom name for the trigger. Trigger names for the same function must be unique. After a trigger is created, you cannot change its name. In this example, set it to `timer`. |
   |Push time |In this example, trigger the function every 5 minutes. You can use one of the two methods to configure it:<br><br><br>* **Specified time**:<br><br>   **Recurrence cycle**: You do not need to configure a recurrence cycle in this example.<br><br>   **Trigger time**: Set the interval to 5 minutes.<br><br>* **Cron expression**: Set the expression to `*/5 * * * *`. |
   |Activate now |Specify whether to enable the trigger immediately when creating the trigger. In this example, enable it immediately. |
   

3. Click **Confirm** to create the trigger.


<span id=".5q2l6aqk5Zub77ya55uR5o6n5LiO6L-Q57u0"></span>
## Step 4: Perform monitoring and maintenance

Use the monitoring and logging features to monitor and debug the function. This helps you stay informed of the function status.


1. On the function details page, click the **Logs** tab.

2. In the **Logs** tab, select a time range to view the function execution logs for that time range.

3. On the function details page, click the **Monitoring** tab to view the function metrics collected.

   At this point, you have completed the veFaaS quick start.
