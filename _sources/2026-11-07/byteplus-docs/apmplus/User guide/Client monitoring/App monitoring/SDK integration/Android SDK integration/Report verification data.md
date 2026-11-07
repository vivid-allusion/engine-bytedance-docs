---
title: "Report verification data"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Report_verification_data_Android"
---

Based on your business requirements, use the following module descriptions to check whether each corresponding module has been successfully integrated.

<span id="ed6f8ff6"></span>
## Prerequisites

<span id="6d5ab6c6"></span>
### Complete SDK reporting configuration


* Configure device allowlist

   **SDK setting** page uses a low default sampling rate. During the SDK integration testing phase, please configure the DID allowlist to ensure that all performance data from the current device is sampled and reported to the platform, so you can view this data. For details, refer to [Create allowlist](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#22523dce) and [How to obtain DID?](https://docs.byteplus.com/en/docs/apmplus/How_to_obtain_a_DID).

* Configure the module sampling rates

   Crash events are reported at a 100% rate and are not affected by the sampling rate. Except for crashes, other monitoring data require sampling reporting to be set up on the **SDK setting** page. By default, data is reported only when sampling is hit.

   For example, before verifying lag data, please enable the main switch on the **SDK setting** page and set the lag sampling rate configuration to 100%. Once verification is complete, modify it to a suitable sampling rate. For details, refer to [Create SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#b29d0396).


<span id="a36a9cb5"></span>
## Java crash/Java startup crash


1. Add the following code and wait for the app to crash.

   ```Java
   throw new RuntimeException("Monitor Exception"); // It crashes as soon as it is executed. If the app crashes within 8 seconds after startup, it is judged as a startup crash and reported.
   ```
   

2. Restart the app. The SDK will immediately report any crashes that occurred during the previous start. Then, view the logs of successful reports in the console.


<span id="bd89ef28"></span>
## lag analytic


1. Call the following functions on the main thread and wait for the app to lag.

   ```Java
   private void testSeriousBlock() {
       try {
           Thread.sleep(3500);
       } catch (Exception e){
       }
   }
   ```
   

   For severe lag, change the sleep time to 6000 milliseconds.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You only need to run the sample code once; running it multiple times may result in ANR. At this time, if you have integrated only the performance component, you will not be able to view the ANR log. To view the ANR log, you must also integrate the crash component.   </div>
   

2. When initializing the SDK, the main thread is blocked. The app will automatically detect lag and report it to the server within two minutes.


<span id="8bb8c9fd"></span>
## Startup analytic/page response

When initializing the SDK, enable the switches for startup analytic and page response. After the app has been running for a period of time, the SDK will automatically report data for startup analytic and page response.

<span id="c528a8ec"></span>
## **Smoothness/frame loss**

When initializing the SDK, enable the configuration feature. After the user enters the page and scrolls for a period of time, the SDK will automatically report smoothness data and frame loss data.

<span id="1d901434"></span>
## **Memory optimization**

When initializing the SDK, enable the configuration feature switch and set the debug test mode.

```Java
builder.debugMode(true);
builder.memoryMonitor(true);
```


The above code can simulate the occurrence of the following two scenarios:


* Oom obtain mode

   * By default, memory file analysis is performed when an OOM (out\-of\-memory) event occurs, typically when memory usage reaches or approaches 100%.

   * Call the method for simulating OOM`OOMMaker.createOOM();`.

   * After restarting, memory data will be automatically reported. After a few minutes, view the memory data on the server.

* Memory limit mode

   * If the number of daily active users is too low and there are no OOM events or very few OOM events, but you still want to analyze memory issues, you can configure the **SDK setting** page to set the **memory usage ratio for start log collection**. After configuration, when memory usage reaches the specified ratio, the SDK will report start log collection memory information for memory file analysis.

   * Call the method to simulate increased memory usage`OOMMaker.createReachTop(80);`.

      The threshold configuration in the example is set to 80%. Modify the threshold according to your actual business scenario.

   * Wait one minute to obtain the memory file. Then, after restarting, the memory data will be automatically reported. After a few minutes, go to the server to view the memory data.


<span id="e99d0749"></span>
## **Network analysis**

During SDK initialization, configure the okHttp3Switch of the instrumented ApmPlugin to enable network monitoring. When the app uses okhttp3 for access, monitoring is performed automatically and the monitoring result is reported to the server. The minimum supported version of okhttp for instrumentation is `3.10.0`. Currently, okhttp3 exposes an interface for reporting network monitoring data. For other network libraries, you need to collect network monitoring data yourself and then report the network data through the network monitoring data interface before you can view the monitoring data on the platform. To obtain the specific reporting interface and reporting data structure, please contact technical support.

<span id="3a4d8532"></span>
### Reporting policy

Network monitoring logs are not reported immediately after being recorded. Reporting is triggered every 60 seconds.

<span id="33c2ce17"></span>
## **Battery analytic**

Turn on the battery switch when initializing the SDK. After the app starts, when a sampling hit occurs on the device, battery data will be automatically collected and reported.

<span id="15d3ed08"></span>
## **Event reporting**

Add a new event and configure sampling on the **Event management** page; the event will only be reported if the sampling criteria are met.

<span id="f3e06c1a"></span>
### Rules for configuring event reporting

```Java
HashMap<String, String> dimension = new HashMap<>();
//dimension value
dimension.put("key1", "value1");
dimension.put("key2", "value2");
HashMap<String, Double> metric = new HashMap<>();
//metric value
metric.put("metric1", (double) 10);
metric.put("metric2", 8.8);
ApmInsightAgent.monitorEvent("event1", dimension, metric);
```


<span id="4d6eaa63"></span>
### Event sampling configuration

```Java
/**
 * Event reporting
 *
 * 
 * @param serviceName The name of the event
 * @param dimension   Enumerable Key - Value pairs representing dimensions. The key represents the dimension name, and the value represents the dimension value. The platform will automatically calculate the percentage and reporting volume of the values under each key.
 * @param metric      Non - enumerable Key - Value pairs representing metrics. The key represents the metric name, and the value represents the metric value. The platform will automatically calculate the average and reporting volume of the values.
 */
public static void monitorEvent(final String serviceName, final Map<String, String> dimension, final Map<String, Double> metric) {
}
/**
 * Event reporting
 *
 * @param serviceName The name of the event
 * @param dimension   Enumerable Key - Value pairs identifying dimensions
 * @param metric      Non - enumerable Key - Value pairs identifying metrics
 * @param extraJson   Data for auxiliary analysis of the event, which can only be viewed in the single - point raw logs
 *
 */
public static void monitorEvent(final String serviceName, final Map<String, String> dimension, final Map<String, Double> metric, final JSONObject extraJson) {
}
```


After configuring event sampling through the above event reporting interface, you can view event information on the platform. Examples of events to view on the platform

```Plain
// Indicates that the sampling for event1 was not hit.
2021-04-11 21:19:01.019 13535-13587/com.example.apm.insight.demo D/ApmInsight: Receive:EventData event1 simple:false
// Indicates that the sampling for event2 was hit.
2021-04-11 21:19:01.916 13535-13587/com.example.apm.insight.demo D/ApmInsight: Receive:EventData event102 simple:true
```


<span id="596a8908"></span>
### Reporting policy

Event logs are not reported immediately after being recorded. Reporting is triggered every 60 seconds.

<span id="753f38dc"></span>
## CPU monitor

When initializing the SDK, enable the CPU monitor. The CPU metric will be automatically collected and reported. You can simulate a CPU anomaly on the client side, then wait for the client to detect and report the exception. After that, you can view the exception data on the platform. Add the following code to simulate a CPU anomaly:

```Java
for (int i = 0; i < 6; i++) {
    new Thread(new Runnable() {
        @Override
        public void run() {
            while (true) {
                Math.acos(Math.cos(java.lang.Double.valueOf(9999999)));
            }
        }
    },"cpu-"+i).start();
}
```


After enabling the debug switch, filter for ApmInsight in the Logcat log to view the following logs:

```Plain
// Abnormal CPU data
2021-12-30 15:29:29.512 26285-26887/com.example.apm.insight.demo D/ApmInsight: Receive:ExceptionCpuData
// CPU metrics
2021-12-30 15:29:29.512 26285-26887/com.example.apm.insight.demo D/ApmInsight: Receive: ProcessCpuDat
```


<span id="adcbff1b"></span>
## Disk monitor

During the testing phase, it is recommended to set the sampling rate of all disk\-related parameters to 100%, set the threshold of all disk\-related parameters to 1, use the default value of 20 for the maximum number of exception files reported, and set `builder.debugMode(true)` on the client. The app reports disk data only once per launch. To reduce the impact on performance, the SDK is configured by default to collect and report disk data only once when the App is in the Background. After applying the recommended configuration for the testing phase, you can set debug mode to enable disk data collection and reporting in the Foreground as well. After a Cold Start, if you filter for ApmInsight, you will see the `Receive:DiskData` log, which indicates that disk monitoring data has been reported successfully. You can view the data on the **disk anomaly** page.

<span id="c27a49c6"></span>
## Traffic monitor

When initializing the SDK, enable the traffic switch. After the app starts, when a sampling hit occurs on the client, traffic data will be automatically collected and reported. Traffic metric is collected every 10 minutes. A traffic anomaly requires that client\-side traffic consumption over a 10\-minute period exceeds the threshold configured by the platform. Add the following code to simulate a traffic anomaly:

```Java
// Ten - minute traffic
2023-01-12 21:10:49.615 5472-5576/com.example.apm.insight.demo D/ApmInsight: TrafficData10
// Abnormal traffic
2023-01-12 21:10:49.615 5472-5576/com.example.apm.insight.demo D/ApmInsight: TrafficDataException
```
