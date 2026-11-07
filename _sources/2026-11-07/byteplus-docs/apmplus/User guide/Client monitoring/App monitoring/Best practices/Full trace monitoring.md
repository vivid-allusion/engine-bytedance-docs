---
title: "Full trace monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Full_trace_monitoring"
---

To receive and process a request, the operating system requires multiple network devices and applications to work together. A single request triggers a sequential chain of calls between different applications. A complete request trace is a Trace, and the TraceId associates all nodes within the trace.

<span id="d7f49e66"></span>
## Enable full trace connectivity between client and APMPlus server side

APP monitoring establishes a comprehensive end\-to\-end monitoring system for the application system, spanning from the APP client to the backend, to enable rapid issue detection and pinpointing. By associating server side Monitoring data using TraceId, you can observe the complete trace of app network request calls.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### **Prerequisites**


* Full trace monitoring has been integrated. For details, refer to [Integrating your application with the Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) and [Integrating your application with the iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* Server\-side monitoring has been integrated. For details, refer to [How to integrate server-side monitoring](https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_server-side_monitoring).


<span id=".5pON5L2c5q2l6aqk"></span>
### Operation Procedure


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **All Features \> HTTP**.

4. In the left area of the **network overview** page, select the metric for analysis, in the right area, select the dimension for analysis, and then click **network details**.

5. In the **Details** section of the log search page, click the link under Full Link Trace.

6. Go to the **single trace query** page. View more information from the server side.

   * **Trace details**: View the distribution of total time.

      * Click **app request** to view detailed information about the request.

   * **Trace full log**: View detailed log information.


<span id="c9a161fa"></span>
## Establish end\-to\-end connectivity between client and self\-hosted server\-side

APMPlus supports full trace monitoring in two ways. First, it enables end\-to\-end monitoring by connecting the client with APMPlus server\-side monitoring. Second, it allows you to achieve full trace monitoring by setting your own TraceId and connecting your business's server\-side monitoring.

<span id="ebc472f2"></span>
### Operation Procedure


1. Add the following code. Set the TraceId key during SDK initialization, and turn on end\-to\-end monitoring.

   * Android client integration code

      ```Java
      ApmInsightInitConfig.Builder builder = ApmInsightInitConfig.builder();
      builder.setNetTraceId("xxx");//Turn on full trace monitoring. Network monitoring will obtain the value of the key 'xxx' from the response header of the business network request, which is the business's own traceid. After the traceid is reported, it will be displayed on the platform. The business can use the traceid to query the specific trace in its own backend monitoring system.
      ApmInsight.getInstance().init(context, builder.build());
      ```
      

   * iOS client integration code

      ```C
      #import <RangersAPM+NetworkPro.h>
      [RangersAPM setTraceIDKey:@"trace_id_key"];
      ```
      

   After turning on full trace monitoring, APMPlus SDK's network monitoring will obtain the value of the TraceId key from the response header of business network requests and report it along with the network monitoring data.

2. Obtain TraceId on the network monitoring page of the APMPlus console.

3. In the server\-side monitoring system, query the trace and duration of the current network request.
