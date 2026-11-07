---
title: "Report verification data"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Report_verification_data_Harmony"
---

Based on your business requirements, follow the instructions below to check whether the corresponding modules have been successfully integrated.

<span id="febdf3a8"></span>
## Prerequisites

<span id="979a097c"></span>
### Complete SDK reporting configuration


* Configure device allowlists

   **SDK reporting configuration** page uses a default configuration with a low sampling rate. During the SDK integration testing phase, please configure the DID allowlist to ensure that all performance data from the current device is sampled and reported, so you can view this data on the platform. For details, refer to [create allowlist](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#22523dce) and [how to obtain a DID?](https://docs.byteplus.com/en/docs/apmplus/How_to_obtain_a_DID).

* Configure module sampling rates

   Crash reports are always sent at a 100% rate and are not affected by sampling rate controls. Except for crash data, other monitoring data requires sampling reporting to be configured on the **SDK setting** page. By default, data is only reported when sampling is hit.

   For example, before verifying startup monitoring data, please enable the main switch on the **SDK setting** page and set the startup sampling rate for user experience to 100%. After verification is complete, modify the sampling rate to an appropriate value. For details, refer to [Create SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration#b29d0396).


<span id="cfad7434"></span>
## JS crash


1. Add the following code and wait for the App to crash.

   ```Java
   // It is recommended to turn off appRecovery during testing
   // appRecovery.enableAppRecovery(appRecovery.RestartFlag.NO_RESTART)
   throw new Error("Monitor Exception");
   ```
   

2. Restart the app. The SDK will immediately report any crashes that occurred during the previous start. Then, view the log in the console to confirm that the report was successful.


<span id="ac1b4a20"></span>
## Native crash


1. Add the following code, and wait for the app to crash.

   ```Java
   // import { process } from '@kit.ArkTS';
   process.kill(11, process.pid)
   ```
   

2. Restart the app. The SDK will immediately report any crashes that occurred during the previous startup. Then, view the logs of successfully reported crashes in the console.


<span id="aaea9ed3"></span>
## AppFreeze


1. Add the following code, wait for the app to crash, and you may touch the screen if needed.

   ```Java
   // import { systemDateTime } from '@kit.BasicServicesKit';
   let start = systemDateTime.getTime();
   while (start + 10000systemDateTime.getTime()) {}
   ```
   

2. Restart the app. The SDK will report any crashes that occurred during the previous start. Then, check the console for logs of successfully reported crashes.

3. If you find that reporting has not occurred, wait for a while and then restart the app.


<span id="37309f49"></span>
## custom error


1. Modify the SDK setting and enable the custom error switch.

2. Add custom error feature allowlist to test devices.

3. Add the following code to proactively report custom exceptions, and view the data in the platform's "custom error" section.

   ```JSON
   const error = new Error();
   APMPlus.reportError(error, "test");
   ```
   

4. After verification is complete, adjust the sampling rate for custom errors in the SDK reporting configuration, and collect and report samples of custom error data in the production environment.


<span id="f511b535"></span>
## start


1. Initialize the SDK and confirm that start Monitoring has been turned on.

   ```JSON
   let builder = new APMPlusBuilder("AppID", "AppToken");
   builder.startMonitor = true;//Enable startup monitoring
   ```
   

2. Confirm that the sampling condition is met, confirm that the platform configuration includes an allowlist, or confirm that the sampling rate of the start configuration in the SDK reporting configuration is set to 100%.

3. After data collection, you will be able to view the data in the platform's `startup analytic`.

4. After the app is launched, the startup duration is collected and reported to the platform. By default, only the total startup duration is collected.

   * Start time: the time when the user clicks the icon.

   * Deadline: The time when the first page is displayed.


<span id="65502580"></span>
### Start custom tracking

<span id="85023994"></span>
#### Custom start node

Start monitoring supports custom event logging, and the methods must be used in pairs.

```JSON
LaunchTrace.startSpan("initApm");
LaunchTrace.endSpan("initApm");
```


After adding the above code, you can view the timing of custom markers in the **startup node timing** section of **startup analytic**.

<span id="67436400"></span>
#### Custom start and end points

By default, startup monitoring uses the start and end points defined by HiAppEvent's data monitoring. The following method allows you to customize both the start and end points.

```Plain
// Initialize and set the custom reporting for startup monitoring, indicating that the reportLaunchEnd() method is used to define the end point of startup. It needs to be called as early as possible, for example, in the onCreate method of AbilityStage.
LaunchTrace.customLaunchEnd(true);
// Report the end time point of custom startup monitoring, representing the end point of startup.
LaunchTrace.reportLaunchEnd();
```


The start data collection relies on the start data callback from HiAppEvent, and delays in the operating system callback may result in delayed reporting of start data. The HiAppEvent system callback log will display `APP_LAUNCH`. An example is shown below:

```Plain
06-17 19:29:43.114   3788-3788    A0001B/APM                     com.apmpl...ony.demo  I     Start --> event: APP_LAUNCH
```


<span id="d964df2c"></span>
## event analytic


1. Platform registration events On the **Event management** page, add a new event and configure sampling; the event will only be reported when the sampling criteria are met.

2. Log custom events on the client side

   ```Java
   // Dimension value string
   let category: object = new Object();
   category['version'] = "2.0";
   //metric value number
   let metric: object = new Object();
   metric['key'] = 2
   // Extra data string. Without aggregation, you can query the original log directly to view data.
   let extra: object = new Object();
   extra['apm_extra'] = 'extra info'
   // Event name
   APMPlusAgent.monitorEvent("harmony", category, metric, extra);
   ```
   

3. Data view. After tracking the above custom events, you can view event information on the platform.

   In client debug mode, filter for the log `A0001B/APM`. When you see a log indicating that an event sampling hit has occurred, as shown below, you can view the event data on the platform after two minutes.

   ```Plain
   // For the event harmony, the sampling hits: sample true; the sampling misses: sample false.
   06-14 18:21:36.625   62396-62396  A0001B/APM                     com.examp...lication  D     Event --> harmony sample true
   ```
   


<span id="4e5fc365"></span>
## Network monitoring

Network monitoring supports monitoring network requests made using the `request` method from `import http from '@ohos.net.http'`.


1. Enable network monitoring during initialization.

   ```Java
   builder.netMonitor = true;
   APMPlus.start(builder);
   ```
   

2. Set up network monitoring using HttpMonitor.

   ```Java
   let request = http.createHttp();
   let httpMonitor: HttpMonitor = new HttpMonitor(url, options);
   request.request(url, options, (error: Error, response: http.HttpResponse) => {
     httpMonitor.setResponse(error, response);
   });
   ```
   

3. Complete the sampling configuration. Confirm sampling has occurred, view the **network monitoring sampling rate** configuration in the platform **SDK reporting configuration**, or configure an allowlist during the testing phase.

4. After filtering for `001B`, you can view the following log. After two minutes, you will be able to view network monitoring data in the platform's **network analytic** **HTTP** module.

   ```Java
   //Received network monitoring data: receive:network
   10-11 11:37:21.654   35003-35003   A0001B/com.byt...hpem.demo/APM  com.byted...pem.demo  D     CommonDataHandler --> receive:network
   //network monitoring data hit sampling: sample true data:network
   10-11 11:37:22.816   35003-35003   A0001B/com.byt...hpem.demo/APM  com.byted...pem.demo  D     CommonDataHandler --> sample true data:network
   //Network monitoring data push aggregation succeeded: "service":"network"
   10-11 11:37:22.817   35003-35003   A0001B/com.byt...hpem.demo/APM  com.byted...pem.demo  I     PersistentBuffer --> push success: totalCount= 1,totalBytes=720, logItem= {"service":"network","log_type":"performance_monitor","uri":"https://sdfadfsbd/settings/gets","request_log":"{\"dns\":{},\"socket\":{},\"response\":{\"code\":0,\"sent_bytes\":239,\"via_proxy\":false,\"network_accessed\":true},\"timing\":{\"request\":{\"duration\":40,\"start_time\":1728617841582,\"response_recv_time\":1728617841622},\"detailed_duration\":{\"ttfb\":0,\"dns\":0,\"tcp\":0,\"ssl\":0,\"send\":0,\"header_recv\":0,\"body_recv\":0}},\"base\":{\"url\":\"https://sdfadfsbd/settings/gets\",\"method\":\"POST\"},\"error\":{\"error_code\":2300006,\"error_msg\":\"Couldn't resolve host name\"},\"other\":{\"libcore\":\"NetworkKit\",\"version\":\"1.0.0\",\"is_main_process\":true}}","data_type":2,"is_sample":1}
   ```
   


<span id="bd612ebc"></span>
## custom log

To facilitate troubleshooting of single\-point issues, support for custom business log printing is provided. Logs can be reported using various methods, including recovery, the user feedback button to actively call the API, and configuration to report logs together with crash reports. These methods assist in diagnosing single\-point problems.

<span id="813c82ac"></span>
### Initialization and event tracking


1. Initialize and open a custom log


```Plain
builder.logRecovery = true;// Optional. Whether to enable the custom Vlog logging capability.
APMPlus.start(builder);
```



2. Perform custom log event logging via the Vlog class


```Plain
VLog.v(String tag, String msg);
VLog.d(String tag, String msg);
VLog.i(String tag, String msg);
VLog.w(String tag, String msg);
VLog.e(String tag, String msg);
```


<span id="02c925a6"></span>
### Report and view methods

<span id="f1c76fdc"></span>
#### recovery

When users encounter issues that require log investigation, you can use recovery on the client side to obtain logs printed by the custom log Vlog for troubleshooting.

Create a new task on the **log recovery** page, and enter a DID or UID to recover the specified user's custom log to troubleshoot issues.

DID is set in the business through the `APMPlus.setDeviceId("device_id");` method.

The UID is set in business logic via the `APMPlus.setUserId("user_id");` method.

<span id="c80a9e6d"></span>
#### Active reporting

The business can also actively call the interface to report logs. Caution: The business controls the reporting sampling and frequency through code policy. Custom files are relatively large; reporting each file will consume 200 events.

```Plain
// Report custom logs from one hour before the current time.
APMPlusAgent.tryUploadAlog(systemDateTime.getTime(false) - 60 * 60 * 1000, systemDateTime.getTime(false), {
  onCallback(result: boolean, ret: JSON | null) {
  }
})
```


After reporting, you can use the **custom log** page's **custom log query** to query log files by DID or User ID.

<span id="0044d726"></span>
#### Report when a crash occurs


1. On the **SDK setting** page, in the **crash analytic** section, configure **whether to upload custom logs**.

2. Under **custom log** on the **crash details** page, view the logs printed by the Vlog class.


<span id="bc5ab1a7"></span>
## Performance data reporting policy

After recording performance data such as start and event, the data is not reported immediately; instead, aggregation triggers reporting once every 60 seconds. JS crash, Native crash, and AppFreeze are reported after the app restarts.
