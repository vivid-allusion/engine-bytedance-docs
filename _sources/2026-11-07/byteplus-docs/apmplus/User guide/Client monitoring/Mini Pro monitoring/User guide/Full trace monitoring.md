---
title: "Full trace monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Full_trace_monitoring_minipro"
---

Mini Pro Monitoring establishes a comprehensive end\-to\-end monitoring system for application systems, covering both frontend and backend, enabling rapid issue detection and identification. By associating server side Monitoring data with TraceID, you can observe the complete trace process of Mini Program Pro request calls.

<span id="CvoOr5BV"></span>
## Background Information

To receive and process a request, the operating system requires multiple network devices and applications to work together. A single request triggers a series of sequential invocation relationships among different applications. A complete request trace is called a Trace, and the TraceID associates all nodes along the entire trace.

<span id="NzRAu1Gd"></span>
## Operation Procedure


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Mini Program Pro Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> data explore**.

4. In the left panel of the data explore page, select the dimension for analysis. In the right panel, click the data to be analyzed, then click **Reported content**.

5. Click the TraceID link to enter the single trace query page. More information is available in the backend.

   * **Trace details**: View the distribution of total time.

   * **Trace complete log**: View detailed log information.

6. Click **Go to Mini Program pro to view**, then return to the Client side to view the Mini Program pro request.
