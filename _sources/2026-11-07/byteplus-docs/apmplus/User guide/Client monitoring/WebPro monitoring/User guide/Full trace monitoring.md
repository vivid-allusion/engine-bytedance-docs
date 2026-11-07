---
title: "Full trace monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Full_trace_monitoring_webpro"
---

WebPro Monitoring builds a comprehensive end\-to\-end monitoring system for application systems, covering both frontend and backend, to enable rapid issue detection and pinpointing. By associating monitoring data on the server side using TraceID, you can observe the complete trace process of WebPro requests.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

To receive and process a request, the system requires multiple network devices and applications to work together. A single request triggers a sequential chain of calls between different applications. A complete request trace is a Trace, and the TraceID associates all nodes in the entire trace.

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation Procedure


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **Webpro\-side Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> data explore**.

4. On the left area of the data explore page, select the dimension for analysis. In the right area, click the data to be analyzed, and then, in the right panel, click **Report content**.

5. Click the run_trace_id link, and you will be taken to the single trace query page, where you can view more information in the backend system.

   * **Trace details**: View the distribution of total time.

   * **Trace full log**: View detailed log information.

6. Click **Jump to Web Pro**, back to the frontend to view the frontend request.
