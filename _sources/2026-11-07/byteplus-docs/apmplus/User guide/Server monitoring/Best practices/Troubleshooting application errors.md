---
title: "Troubleshooting application errors"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Troubleshoot_application_errors"
---

Webpage errors are common issues, but pinpointing and troubleshooting these errors often present significant challenges. To address such issues, APMPlus provides comprehensive application monitoring that enhances observability. This helps provide a better understanding of internal service operations and assists with error diagnosis. This topic introduces how to use APMPlus to troubleshoot application errors.

<span id="THnnCiyk"></span>
## Background

Application error prompts refer to issue notifications sent to users or developers when a program encounters an unhandled situation during runtime. Error messages typically contain the error type, the location where the error occurred, and possible causes, helping developers quickly locate and resolve issues. Operations engineers or R&D engineers often need to log in to servers and examine logs to locate issues. For applications with relatively simple logic and a short deployment history, this approach can resolve the majority of web application errors. However, in the following scenarios, relying solely on log analysis often makes it difficult to pinpoint issues:


* **Microservices architecture scenarios**: Applications built on a microservices architecture have more complex call chains, and different components may be maintained by different teams and individuals, further increasing the difficulty of troubleshooting. For example, in a distributed application cluster, knowing the timing and frequency of a particular type of error can help pinpoint the root cause.

* **Complex system environments**: The environment in which an application runs may involve interactions among various hardware, software, and network factors, making it difficult to determine which factor is causing the error. For example, a system that has been running for a long time may have historical issues due to complex system environments. However, when analyzing problems, you may not be concerned with legacy exceptions. Instead, you only want to compare the additional exception information and related logs between today and yesterday, or between after and before a release.

* **Unclear error messages**: Sometimes only a simple error code or a vague error message is displayed, making it difficult to directly determine the root cause of the issue. For example, a customer service representative provides an order number for a failed user purchase, and you need to analyze the reason why the user's order placement failed.

* **Hidden logic errors**: Logic errors do not directly trigger obvious error messages and require in\-depth analysis of the program logic to be identified. For example, while troubleshooting an error, you may need to examine the Web request and related parameters associated with a specific exception.


<span id="TaVczGbr"></span>
## Procedure

<span id="y3HbMfKO"></span>
### Step 1: Install the APMPlus probe

A probe agent is a tool or add\-on used to collect runtime data from applications, providing capabilities such as data collection and fault diagnosis. Installing the APMPlus probe for your application enables comprehensive monitoring. Without modifying application code, you can use the APMPlus features such as continuous profiling, call chain diagnostics, and API monitoring to comprehensively monitor all slow calls in your application.

The process of integrating your application to APMPlus includes data reporting and ingestion, as well as the installation of the APMPlus probe. You can choose an appropriate integration method for your application based on your actual needs. For details, see [APMPlus integration guide](https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_server-side_monitoring).

<span id="uB4df6UZ"></span>
### Step 2: View interface errors and exception stacks

After your application completes the APMPlus probe installation, APMPlus will collect and display global interface error and exception observability data for the selected time range.


<Tabs>
<Tab zoneid="XysKUrA93O" title="Method 1: View all applications">
<TabTitle>Method 1: View all applications</TabTitle>

You can refer to the following steps to view global API error and exception call statistics:


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Click **Enter service list** to go to the service list page.

3. In the left navigation pane, select **Service monitoring \> Error analysis** to go to the Error analysis page and view global interface errors and exception stacks.

4. On the **Error analysis** page, switch to the **Error distribution** chart to view aggregated analysis by dimensions such as service name, error type, interface name, and Root Cause exception.

5. On the **Error analysis** page, click an interface name under the **Interface errors** tab, or click an error message under the **Exceptions** tab to view error details.

6. On the error details page, click the Trace ID associated with the error/exception to go to the **Single trace details** page. View the exception stack, as well as Span information, associated logs, and metrics across the entire call chain through three views: flame graph, topology graph, and list. Then, based on the exception stack, quickly locate the code position and perform rapid fixes.


</Tab>
<Tab zoneid="HayHjJf6zZ" title="Method 2: View a specific application">
<TabTitle>Method 2: View a specific application</TabTitle>

You can refer to the following steps to view API error and exception call statistics for a specific application:


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Click **Enter service list** to go to the service list page.

3. Click the target service name, and on the **Service details** page, go to the **Error analysis** tab to view interface errors and exception stacks for a specific application.

4. On the **Error analysis** page, switch to the **Error distribution** chart to view aggregated analysis by dimensions such as service name, error type, interface name, and Root Cause exception.

5. On the **Error analysis** page, click an interface name under the **Interface errors** tab, or click an error message under the **Exceptions** tab to view error details.

6. On the error details page, click the Trace ID associated with the error/exception to go to the **Single trace details** page. View the exception stack, as well as Span information, associated logs, and metrics across the entire call chain through three views: flame graph, topology graph, and list. Then, based on the exception stack, quickly locate the code position and perform rapid fixes.


</Tab>
</Tabs>


<span id="Ro47Qa5Y"></span>
### Step 3: Drill down to analyze host performance

After identifying the specific service where the error request occurred, you can drill down to host performance to analyze whether host resource constraints cause the application lag.


1. Select the Span of the service, and select **Details \> Resource** tab on the right to view various host performance metrics, including CPU, memory, load, disk usage, and I/O latency.

2. Further drill down to analyze the memory usage distribution of processes on the host, helping to assess the impact of other processes on the application.


<span id="iyZcVT8A"></span>
### Step 4: Further analyze related logs

After the APMPlus probe is installed, APMPlus automatically correlates traces and logs, and provides convenient query capabilities for trace\-related logs. On the **Single trace details** page, select the **Full trace logs** tab to view all logs for this trace. With these full end\-to\-end logs, you can further analyze the application errors.

<span id="RnrBYx9l"></span>
## What to do next

We recommend [creating alerting tasks](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks) to monitor application status in real time. When issues occur or metrics become abnormal, alerts are automatically sent, helping you stay informed of risks and avoid reactive troubleshooting after problems arise.
