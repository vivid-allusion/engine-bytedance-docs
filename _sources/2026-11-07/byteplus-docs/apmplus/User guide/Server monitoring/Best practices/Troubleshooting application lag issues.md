---
title: "Troubleshooting application lag issues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Troubleshoot_application_lag_issues"
---

Web lag and slow page loading are common issues in Internet applications, but locating and troubleshooting them present many challenges. To address these issues, APMPIus provides comprehensive application monitoring and enhanced observability to help you better understand Internal service operations and perform error diagnosis. This topic introduces how to use APMPlus to troubleshoot application lag issues.

<span id="THnnCiyk"></span>
## Background

Application lag refers to slow response and choppy operation during runtime, such as page freezes or slow loading, which severely impacts user experience. Traditional troubleshooting and resolution of application lag is complex and time\-consuming. The main pain points are as follows:


* **Vague user feedback**: Typically, users can only describe surface symptoms of lag, such as "it feels slow," without providing specific details like the exact action, time, or frequency of occurrence. This makes it difficult for developers to pinpoint the root cause of lag based solely on user feedback.

* **Lack of application monitoring data**: Applications need a comprehensive monitoring system to automatically track every interface and log problematic calls. However, some applications lack proper performance monitoring mechanisms and cannot capture critical data during lag, such as resource usage of components or function call stacks. This is especially true for small or legacy applications that may not have integrated professional performance monitoring tools.

* **Overly long application execution chains**: Modern applications often consist of multiple modules, services, and components with complex interdependencies and interactions. From frontend pages to backend gateways, and from web servers to databases, any failure can cause overall lag. Pinpointing whether lag occurs in frontend rendering, backend processing, or database queries is very difficult. Moreover, applications using microservice architectures have even more complex chains, with different components potentially maintained by different teams, which increases troubleshooting difficulty.

* **Incomplete or hard\-to\-interpret logs**: Lag and errors often occur in unpredictable places. Application logs may lack sufficient lag\-related information, or their format may be complex and difficult to parse. For example, some application logs only record basic operation information, without capturing critical data like resource usage or function execution time.


<span id="TaVczGbr"></span>
## Procedure

<span id="1AkHXmop"></span>
### Step 1: Install the APMPlus probe

A probe is a tool or component used to collect application runtime data for fault diagnosis. Installing the APMPlus probe for your application enables comprehensive monitoring. Without modifying application code, you can comprehensively monitor all slow calls in your application via capabilities such as continuous profiling, call chain diagnosis, and interface monitoring.

The process of integrating your application to APMPlus includes data reporting and ingestion, as well as the installation of the APMPlus probe. You can choose an appropriate integration method for your application based on your actual needs. For details, see: [APMPlus integration guide](https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_server-side_monitoring).

<span id="wvtLZOlG"></span>
### Step 2: View slow call information

After the APMPlus probe is installed, APMPlus collects and displays comprehensive observability data for the selected time range, including total requests, average response time, error count, HTTP status codes, interface\-level aggregated metrics, upstream/downstream call metrics, runtime metrics, error/exception counts, and slow SQL count.

You can refer to the following steps to view slow call statistics:


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Click **Enter service list** to go to the service list page.

3. Click the target service name. On the **Service details** page, go to the **Interface monitoring** tab to view QPS, error rate, and latency data for specific interfaces and quickly identify high\-latency ones.


<span id="XBcpLV5z"></span>
### Step 3: Analyze and locate downstream calls

After identifying slow calls at the request entry point, you can use trace analysis to pinpoint the specific downstream services and calls that affect the request.


1. On the **Service details** page, go to the **Service details** tab, click the name of the slow interface, and navigate to the **Request snapshot** page for that interface.

2. In the filter box on the left, specify a lower latency limit, or sort by the latency column in the table on the right, to filter out calls with high latency.

3. Click the target TraceID to go to the **Single trace details** page for that call. View Span information across the entire trace, as well as associated logs and metrics, through flame graphs, topology maps, or list views.

4. By analyzing span durations, you can quickly pinpoint the specific downstream services and calls that affect the request.


<span id="k2A31Txd"></span>
### Step 4: Drill down to analyze host performance

After identifying the specific downstream service affecting the request, you can drill down to host performance to analyze whether resource contention is causing application lag.


1. Select the span for that service, then select the **Details \> Resource** tab on the right to view various host performance metrics, including CPU, memory, load, disk usage, and I/O latency.

2. Continue to analyze the memory usage distribution of processes on the host to help assess the impact of other processes on the application.


<span id="En4PlXG2"></span>
### Step 5: Further analyze relevant logs

After the APMPlus probe is installed, APMPlus automatically correlates traces and logs, and provides convenient query capabilities for trace\-related logs. On the **Single trace details** page, select the **Full trace logs** tab to display all logs related to this trace. With these full end\-to\-end logs, you can further analyze application lag issues.

<span id="RnrBYx9l"></span>
## What to do next

We recommend [creating alerting tasks](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks) to monitor application status in real time. When issues occur or metrics become abnormal, alerts are automatically sent, helping you stay informed of risks and avoid reactive troubleshooting after problems arise.
