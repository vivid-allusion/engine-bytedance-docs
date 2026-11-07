---
title: "Android crash protection"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Android_crash_protection"
---

Android crash protection provides Java crash protection and Java startup crash protection, which can increase app stability and improve user experience. The integration of exception protection is completely non\-intrusive to business code, provides fallback handling after exceptions, and reports issues to the platform to help you identify problems promptly.

When the operating system detects a Java exception that has not been handled with try\-catch, the application is forcibly exited by default in KillApplicationHandler, and a crash dialog is displayed. When this type of Java crash occurs, you can set a custom UncaughtExceptionHandler for the application. Java crash monitoring tools typically use UncaughtExceptionHandler to collect exception information. Under normal circumstances, the trace ultimately leads to KillApplicationHandler, which exits the application. The Android crash protection feature implements its own UncaughtExceptionHandler, which matches exception profiles based on the configuration delivered by the platform. If a match is found, the exception is consumed and the trace invocation is terminated, allowing the application to continue running normally. If a crash occurs on the main thread, protection will restart the loop and continue processing messages in the message queue. If an exception occurs in a child thread, it will exit or be suspended. Caution: Neither the main thread nor the sub\-thread can execute any program logic after the crash point.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When a crash occurs on the main thread, the ApmPlus SDK will restart the looper after the protection mechanism is triggered. If another unprotected crash occurs, the stack trace will include com.apm.insight, which can be ignored.</div>


<span id="3a112d42"></span>
## Prerequisites


* Crash protection has been integrated. For details, refer to [Android SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application).

* Complete crash protection configuration. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration) and [Create crash protection configuration](https://docs.byteplus.com/en/docs/apmplus/Android_crash_protection#7aac1ed8).


<span id="b300a594"></span>
## crash protection configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Android's crash protection cannot continue executing program logic after the point where the crash occurred. It is not recommended to turn on protection for important business logic and in scenarios where enabling protection may lead to a decline in user experience. Each rule should be carefully evaluated before it is created, and thoroughly tested before it is issued.</div>


* <div data-tips="true" data-tips-type="warning">When the SDK detects that the crash stack trace contains the onCreate, onStart, onResume, or onPause methods, protection will not be applied.</div>



<span id="93e3535d"></span>
### The default fallback policy

The built\-in policy of the crash protection configuration page is the default fallback policy. The default fallback policy is a summary, based on experience, of program exceptions caused by non\-business code. When such exceptions occur, they typically do not have a significant impact on the program. The policy is turned off by default. To use it, please go to the **crash protection configuration** page to enable the switch and configure the sampling rate.

<span id="7aac1ed8"></span>
### Create a crash protection configuration


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> crash protection configuration**.

4. On the **crash protection configuration** page, turn on the **main switch** in the upper right corner of the list, then click **create configuration**.

5. On the **Create configuration** page, complete the following settings, and then click **Confirm**.

   Parameter description:

   
   |Parameter |DescriptionS |
   |---|---|
   |Rule name |Custom rule name, used to identify this crash protection rule.<br><br>Chinese characters, uppercase and lowercase letters, numbers, and special symbols are supported, and there is no limit on length. |
   |Rule status |Status of crash protection rules configuration. Enabled by default.<br><br>If the rule status configuration is set to off, the rule will not be distributed. |
   |Eigenvalue |Characteristic values configured for crash protection, used to match crash profiles. A crash protection rule supports adding multiple sets of crash profiles, with a logical OR relationship between profiles, all sharing the current policy's filter conditions.<br><br><br>* The required feature values are the class where the crash occurred, the method where the crash occurred, and the exception class name.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The class and method where the crash occurs must be on the same line of the stack trace, and the exception class name must match the class name of the Throwable or Cause present in the stack trace.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Whenever possible, select crash classes and methods unique to the stack trace, preferably from the business stack trace. If a business stack trace is not available, select an operating system feature module stack trace instead, and avoid selecting an operating system utility class stack trace.   </div><br>   <br><br>   * The full obfuscated name of the class where the crash occurred can be obtained from the crash stack trace.<br><br>   * Crash method: The crash method of the class where the crash occurs, with its obfuscated full name.<br><br>   * Exception class name: the full class name of Throwable.<br><br>* Click **Add feature value**. You can optionally enter feature values. For example, crash process name, crash thread name, app minor version number, and exception information. The length of the feature value must be between 0 and 30.<br><br>   * Crash process name: The name of the process that crashed. If left blank, the rule matches all processes.<br><br>   * Crash thread name: The name of the thread where the crash occurred. If left blank, the rule matches all threads.<br><br>   * App minor version number: the application's version_code. If left blank, the rule matches all versions.<br><br>   * Exception information: Portions of the getMessage() of a Throwable can be extracted and used for feature matching. If the Message of the Throwable is empty, you do not need to provide a value. |
   |Filter criteria |Configure the filter criteria for crash protection, and the platform will distribute the configuration based on the filter criteria. If multiple crash profiles are configured in the feature values, the filter conditions apply to all crash profiles.<br><br><br>* Click **add filter** to customize filter criteria. For example, device model, download channel, device OS version, and Device ID.<br><br>   For example, if the filter condition is configured so that the device model is Xiaomi 10, only Xiaomi 10 devices will receive crash profiles with the above characteristic values. Only then, when a crash occurs, can the crash profile be used to match SDK protection. |
   |Sampling rate |The sampling rate configured for crash protection can be used for gray release validation. |
   


<span id="d23f5bf4"></span>
### Other operations


* Edit crash protection configuration

   In the crash protection list, click **edit** to modify all parameters in the already created crash protection configuration.

* Copy crash protection configuration

   In the crash protection list, click **Copy** to retain the parameters of the created crash protection configuration. You only need to customize the rule name.

* Delete crash protection configuration

   In the crash protection list, click **Delete**. In the secondary confirmation dialog, click Delete to delete the configuration.

* View protection data

   In the crash protection list, click **View protection data** to navigate to the **Crash protection** page and view detailed crash protection information.


<span id="5bd4d1ea"></span>
### Apply crash protection configuration

On the Java crash or Java start crash page, after evaluating whether protection is appropriate, you can click the **raw stack trace** tab and, within it, click the **crash protection** button. The platform will automatically generate a crash protection policy based on the current crash information. The automatically generated crash policy selects a crash profile based on aggregated information. The information selected may not always be reasonable, and adjustments can be made according to the actual situation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is not recommended to implement protection for resource exhaustion type crashes, as this is very likely to cause lag and will ultimately result in a crash.</div>


<span id="6231229c"></span>
## crash protection

Statistical data in crash protection can help the application intercept exceptions, but subsequent handling and resolution of issues is still required.

<span id="9b20703f"></span>
### Filter criteria

You can filter data for the Android operating system using the following filter criteria:

time, crash details, Device ID, User ID, issue new status, Foreground/Background State, OS version, device model, APP version, APP minor version, APM SDK Version, download channel, ROM Information, province, usage duration, process name, manufacturer, parsing status, APP page, issue status, assignee, tag, custom dimension, PV custom dimension.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After adding the reserved field <code>rule_id</code> as a filter condition to the custom dimension, if you turn on the crash protection feature, it is not recommended to use the rule_id custom dimension in crash monitoring.</div>


<span id="5322f629"></span>
### Crash interception trend

The crash interception trend displays a trend chart of the crash interception metric based on the selected filter conditions. You can also display the trend chart grouped by dimension. To the right of the metric data, you can view changes in intercepted crash data compared to the previous period.

Metric description:


|**Metric** |**DescriptionS** |
|---|---|
|Intercepted crash count |Number of successfully intercepted crashes |
|Crash interception rate |Number of intercepted crashes under filter conditions / total number of launches under filter conditions |
|Number of users whose crashes were intercepted |Number of users with deduplicated intercepted crashes under filter conditions |
|Rate of users whose crashes were intercepted |Deduplicated UV count under filter conditions where intercepted crash errors occurred / total deduplicated UV count under filter conditions |
|user count |The deduplicated UV count of intercepted crashes under filter conditions |


<span id="d8bf760b"></span>
### Distribution of crash interceptions

Multidimensional analysis of crash interception distribution provides insight into how intercepted exception crashes are distributed, helping to define problems.


* Hover over the distribution chart to view the full name of the current category and its proportion within the metric type.

* By default, the distribution of intercepted crashes is displayed across four dimensions: **OS version**, **device model**, **App version**, and **App minor version number**. Click the Settings button to select other dimensions, for example, APM SDK version, foreground/background state, download channel, ROM information, and many other options.

* By default, the distribution of errors is displayed by **report volume**. You can also configure it to display the distribution of intercepted crashes by **user volume**.


<span id="3c8a9328"></span>
### List of intercepted exception crashes

The intercepted exception crash list displays aggregated issue data for crashes of the same intercepted exception type, including impacted user count, occurrence count, crash ratio, most recent occurrence time, log report time, status, and assignee.


* Note: Click to jump to **crash details** to view more crash information.

* Impacted user count: Click the icon after the number to preview the trend chart. Hover over the trend chart to view the corresponding time.

* Occurrence count: Click the icon after the number to preview the trend chart. Hover over the trend chart to view the corresponding time.

* Crash ratio: Number of crashes of this type intercepted as exceptions divided by the total number of launches.

* Latest occurrence time: The time of the most recent intercepted exception crash.

* Log report time: The time when the intercepted exception crash information is reported to the server side.

   For example, the interception of an exception crash occurs in version 1.0, while the reporting takes place in version 1.2. To avoid information gaps, the list will report all contextual information from both the time the issue occurred and the time it was reported.

* Sorting: The list is sorted by impacted user, occurrence count, and crash ratio in descending order by default. Click **occurrence time** or **log report time** to sort by time in descending or ascending order.

* Download: Click the download button in the upper right corner to download the first 100 data entries in the `.xlsx` file format.

* Setting: Click the setting button in the upper right corner to customize the columns displayed in the list. In addition to the default column data, you can also configure the following: Year\-over\-Year occurrence count, Year\-over\-Year impacted user, Year\-over\-Year crash ratio, affected user rate, Year\-over\-Year affected user rate, and version range.


<span id="b7a7bcd0"></span>
### crash details

<span id="175ab73b"></span>
#### Issue overview

<span id="7d64eecc"></span>
#### Intercept crash trend

Crash trend details display the changes in two metrics—the number of crashes and the number of impacted users—for this type of issue.

The crash trend chart in details interception is different from the crash trend in list interception; the differences are as follows:


* List of intercepted crash trends: All intercepted exception crashes within the time range.

   For example, with a time period of seven days and an aggregation granularity of one hour, you can view the hourly intercepted crash trend over seven days, with a total of 20 intercepted crashes.

* Details of intercepted crash trends: Aggregation of all intercepted exception crashes within the specified time range.

   For example, with a time period of seven days and an aggregation granularity of one hour, the crash list contains five crash items. This means that the system categorizes twenty crashes into five crash items. When you open one of these crash items, the details section displays the crash trend for this type of crash over the seven\-day period.


<span id="c19d5b02"></span>
#### Details

You can view the attributes of each field for an individual crash to obtain detailed information.


* Show custom dimension: Click to display the custom dimension.

* Trace: Click **Trace** next to the device ID or UserID to jump to log query and view the complete context log stream.

* You can switch crash via the upper right corner.


<span id="58c224ef"></span>
#### Raw stack trace and Retrace


* The raw stack trace display contains the raw stack trace information found in the raw log uploaded by the client.

* Retrace displays the stack trace after symbolication.

   * The operating system stack trace will be handled.

   * If the symbol table is not uploaded, the client stack trace will not be processed.

   * If the symbol table has already been uploaded but the client stack trace has still not been processed, it may be because the symbol table was not fully uploaded.

* If the symbol table or parsing is incorrect, you can re\-upload the symbol table, and then click **Retry Retrace** in the Retrace interface.

* Copying the stack trace facilitates collaboration in analyzing stack trace information.


<span id="6e942abe"></span>
#### symbol table

On the symbol table page, manually upload the symbol table

<span id="34d88e97"></span>
#### on\-site data

On\-site data displays the status of the program's operation when crash protection occurs.
