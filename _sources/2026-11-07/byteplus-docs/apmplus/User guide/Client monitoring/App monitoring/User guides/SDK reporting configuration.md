---
title: "SDK reporting configuration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration"
---

After the application integrates the SDK, the SDK will report the data it samples according to the platform's default configuration values. The SDK reporting configuration feature allows you to configure the sampling and threshold for SDK reporting data according to your business requirements. This document describes how to configure SDK reporting configuration for each module.

<span id="2376043a"></span>
## Precautions


* Crash data is important. By default, all samples are collected and reported. Configuration of the sampling rate is not supported; only configuration to turn on or turn off reporting is available.

* Performance\-related data supports configuration sampling; only data that matches the sampling criteria will be reported, while data that does not match will not be reported. The sampling ratio for business configuration is typically calculated based on DAU. To obtain meaningful performance data, it is generally necessary to ensure a user base of several hundred thousand.

* After modifying the SDK setting, the change will not take effect immediately. The client fetches the reporting configuration every few hours and caches it locally.

* You can use configuration switches to control whether to enable related capabilities and data collection and reporting. For example, disk monitoring and memory optimization switches, along with sampling controls, can be used to manage the collection and reporting of disk and memory data.


<span id="b29d0396"></span>
## Module sampling configuration

<span id="cb80bde4"></span>
### Step 1: Turn on the sampling switch


1. In the upper left corner of the console, select **All features \> SDK reporting configuration**.

2. Select the operating system, and turn on the sampling switch for the target module.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the sampling switch is turned on, data is reported according to the sampling configuration. When it is turned off, the entire module does not report data.   </div>
   

<span id="b564fce8"></span>
### Step 2: Configure sampling reporting policy


1. After turning on the module sampling switch, click **create configuration**.

2. On the **Create configuration** page, configure the reporting policy for modules as needed.

   * Configuration parameters: Please configure the sampling reporting policy for different modules according to business requirements.

   * Filter criteria: Optional. If your business scenario only needs to focus on one or several metrics, you can configure filter conditions.

      For example, if you configure the App version to 1.1.4, the SDK will only collect data from App version 1.1.4. From this data, 15 percent (sampling rate) will be randomly selected for reporting.

3. After configuration is complete, click **Save changes**.


<span id="c89cfdf7"></span>
### Module parameter descriptions

<span id="884c5be8"></span>
#### crash analytic


|**Configuration items** |**DescriptionS** |**Android default values** |**The Harmony default value** |**iOS default values** |
|---|---|---|---|---|
|Upload custom log |Whether to upload a custom log during a crash. The custom log will be displayed on the crash details page. |No |Not supported |No |
|APMPlus crash log reporting sampling rate |Whether to collect APMPlus logs during a crash. Collection is disabled by default. To enable collection, configure the sampling rate.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The APMPlus log sampling rate only controls whether the device records APMPlus logs; it does not control whether logs are uploaded.</div><br><br><br><div data-tips="true" data-tips-type="tip">When you configure the APMPlus log reporting sampling rate to 100%, if the APMPlus log recovery task is not configured, APMPlus logs will not be reported and no charges will be incurred. When you need to recover logs, you can configure a recovery task. For specific operations, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Recovery">recovery</a>.</div><br> |0 |Not supported |0 |
|Custom logs within the N seconds before collection |Collect custom logs for N seconds before a crash. Range: [0–300], unit: s. |30 |Not supported |30 |
|Whether to report the extension crash log |Should extension crash logs be reported? |Not supported |Not supported |Yes |
|Zombie object sampling rate |The sampling rate for zombie object monitoring incurs performance overhead; it is recommended to enable it sparingly in production. |Not supported |Not supported |0% |
|Zombie object analysis allowlist |When classes in the allowlist are deallocated, the stack trace is saved for analyzing zombie issues. Refer to the following format: ["MyClass", "MyClass2"]. |Not supported |Not supported |[] |
|Zombie object collection allowlist |Only monitor zombie issues occurring in classes in the allowlist. Use the following format: ["MyClass", "MyClass2"]. |Not supported |Not supported |[] |
|Maximum number of dealloc stack traces |Maximum number of object deallocation stack traces that can be retained. Refer to the "zombie object analysis allowlist." The greater the number of stack traces, the more memory is used. |Not supported |Not supported |100 |
|Enable register analysis? |After you turn on register analysis, register\-related information will be recorded and reported in the event of a crash. Turning on this feature will increase the crash log size and may reduce the success rate of reporting. |Not supported |Not supported |No |
|Do you want to turn on asynchronous call stack analysis? |After you turn on asynchronous call stack analysis, asynchronous call information will be recorded, which results in some performance loss. |Not supported |Not supported |No |
|Enable stack memory analysis? |After you turn on stack memory analysis, information related to stack memory will be recorded and reported when a crash occurs. After turning on this feature, crash log size will increase and the reporting success rate may decrease. |Not supported |Not supported |No |
|Maximum number of stack memory analyses allowed |Maximum stack memory quantity. A higher quantity results in a larger crash log and may reduce the reporting success rate. |Not supported |Not supported |256 |
|GWPASan sampling rate |GWPASan sampling rate. |Not supported |Not supported |0% |
|Maximum number of simultaneous allocations for GWPASan |The maximum number of memory block creation and destruction events that GWPASan records. |Not supported |Not supported |1024 |
|GWPASan memory allocation sampling rate |GWPASan records the sampling rate of memory blocks.<br><br>Calculation formula: 1/SampleRate. For example, if memory units [m1, m2, m3, ... , m1000] are allocated, a sampling rate of 100 percent records the values of all memory units, while a sampling rate of 10 percent records the values of [m1, m10, m20, m30, ... , m1000]. |Not supported |Not supported |1/20 |
|Coredump sampling rate |Coredump sampling rate. |0% |Not supported |0% |
|Custom file sampling rate |Custom file sampling rate. |0% |0% |Not supported |
|Ignore crashes on application exit |Ignore crashes that occur when the application exits. If the configuration is set to Yes, the application name must also be configured accordingly. |Not supported |Not supported |No |
|Whether to ignore the SIGPIPE signal |Ignore the crash issue caused by the SIGPIPE signal. iOS SDK version 5.1.1 or later is required for support. |Not supported |Not supported |No |


<span id="d17639da"></span>
#### MetricKit


|**Parameters** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|MetricKit stability sampling rate |MetricKit stability sampling rate. |Not supported |20% |
|MetricKit performance sampling rate |MetricKit performance sampling rate. |Not supported |0% |


<span id="d73cc92f"></span>
#### crash protection


|**Configuration items** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Crash protection sampling rate |Control the sampling rate for data reporting of the crash protection module.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the sampling rate is 0%, the module does not report data, but the feature is not turned off. To turn off the feature, please adjust the "Crash Protection Submodule Switch" configuration.</div><br> |Not supported |100% |
|Crash protection submodule switch |Control whether the crash protection submodule is turned on. For details, refer to [crash protection](https://docs.byteplus.com/en/docs/apmplus/iOS_crash_protection). |Not supported |63 |
|Array creation protection logic rules |Control the protection rules that crash protection applies to arrays. For details, refer to [crash protection](https://docs.byteplus.com/en/docs/apmplus/iOS_crash_protection).<br><br><br>* **Strict mode**: Gives priority to ensuring the correctness of array indices.<br><br>* **Compatibility mode**: Give priority to ensuring that the array is created successfully. |Not supported |Strict mode |
|Crash protection count |Configure the number of crashes that can be protected against during a single run of the process. Protection will no longer be performed after the number of protections exceeds this value. |5 |Not supported |


<span id="37ee9ea1"></span>
#### error analytic


|**Configuration items** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Custom error sampling rate |Sampling rate for custom error reporting. |100% |10% |
|Sampling rate for native custom exceptions |Custom exception sampling rate for Native. |0% |Not supported |
|GWPASan sampling rate |The GWPASan sampling rate |0% |Not supported |


<span id="ed6a6480"></span>
#### lag analytic


|**Parameters** |**DescriptionS** |**The Android default value** |**iOS default values** |
|---|---|---|---|
|Lag sampling rate |Sampling rate for lag data reporting. |20% |5% |
|The lag threshold |If the duration exceeds the threshold defined for lag, it is considered lag and a stack trace will be collected. The unit is seconds. |2.5 |2.5 |
|Severe lag threshold |The threshold for serious lag is defined as follows: if the duration exceeds this threshold, it is considered serious lag and a stack trace will be collected. Unit: seconds. |4 |Not supported |


<span id="9cd4f030"></span>
#### user experience


|**Configuration parameters** |**DescriptionS** |**Android default values** |**The iOS default value** |
|---|---|---|---|
|Set the sampling rate |Enable the sampling rate for monitoring data reporting |20% |10% |
|Whether an app update counts as the first launch |Define whether the first launch includes an app update. |No |No |
|Prewarm determination threshold |This threshold is used to determine which exception phases during startup analytic need to be ignored. For details, refer to [user experience-startup analysis](https://docs.byteplus.com/en/docs/apmplus/User_experience). |Not supported |1500 |
|The page sampling rate |Sampling rate of page experience data: including page response time, smoothness, and frame loss. |20% |10% |
|Interval thresholds for page lifecycle stages |This threshold can be used to filter out outliers during each lifecycle period. Unit: seconds. For details, refer to [user experience](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features#73699796). |Not supported |20 |


<span id="063eb934"></span>
#### Page analysis


|**Configuration items** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|The WebView sampling rate |All features in page monitoring (WebView Monitoring) are uniformly sampled based on DeviceID. Once a DeviceID is matched, all feature data in page monitoring will be collected. |20% |20% |


<span id="a92ed7a9"></span>
#### New H5 monitor


|**Configuration parameters** |**DescriptionS** |**Android default values** |**iOS default value** |
|---|---|---|---|
|New H5 monitor sampling rate |Sampling rate of the new H5 Monitor |20% |20% |


<span id="3842f2a7"></span>
#### memory optimization


|**Parameters** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Sampling rate for OOM analysis |The sampling rate for reporting memory files affects the amount of data for leaks, large objects, and queries on a single device. |100% |5% |
|Memory metric sampling rate |Sampling rate of extended metrics in the OOM trend. |10% |10% |
|Start log collection memory usage ratio |The memory file generated during a memory exception will only be reported when the memory usage ratio exceeds the "start threshold." |100% |Not supported |
|Memory leak detection sampling rate |Is leak detection turned on for the fallback solution for controlling memory leaks? |100% |Not supported |
|Memory leak fallback sampling rate |Control whether the memory leak fallback mechanism is enabled. |0% |Not supported |
|Is C++ local symbolization turned on |After you turn on this feature, C++ object symbols will be parsed locally, which may have some impact on performance. |Not supported |Yes |
|Memory collection start threshold |The log file for a memory exception will only be reported if memory exceeds the "start threshold" at the time of the exception. Unit: MB.<br><br>In some scenarios, the operating system may interrupt processes before memory usage reaches the threshold. In such cases, you can modify this value. |Not supported |1024 |
|Maximum memory allowed for this module |MemoryGraph limits its own memsize. Maximum memory allowed for APM SDK during MemoryGraph collection. If exceeded, a downgrade will be triggered. At this time, the SDK collects only node information and does not collect reference information. A single device query displays only the cluster list, without information such as reference trees or dominator trees. The unit is MB. |Not supported |200 |
|Maximum disk space occupied by log files |The SDK has imposed a limit on the disk space occupied by generated memory snapshot files. The maximum disk space that a single MemoryGraph file can occupy is limited to a specific value. Once this limit is exceeded, only node information is collected, and reference information is not collected. In this case, you can only view the cluster list; information about the reference tree and dominator tree is not available. Unit: MB.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not set the threshold too high; otherwise, when you start the upload next time, loading files into memory may trigger an out\-of\-memory (OOM) error again. For more information, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_adjust_the_maximum_disk_space_threshold_for_logs">How to adjust the maximum disk space threshold for log files?</a>.</div><br> |Not supported |250 |
|Maximum number of triggers per user per day |For a single device, there is a maximum number of times per day that MemoryGraph collection can be triggered. If this value is set too high, it will affect the user experience. Unit: times per day per person. |Not supported |10 |
|Interval between two collections by a device |For a single device, the minimum time interval between two memory analyses during a single usage period. The unit is minutes. |Not supported |20 |
|Memory increase from two collections on a single device |For a single device, the next collection is triggered only if the increase in Physical Memory usage during one usage period exceeds this value. Unit: MB. |Not supported |200 |


<span id="60fb4f24"></span>
#### network analytic


|**Parameters** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Network sampling rate |Sampling rate for network monitoring data reporting.<br><br>Matched network data will take effect under the network error and error alert strategies. |5% |5% |
|Report when the network is disconnected |Will data generated during a network outage be reported after the network is restored? |Yes |Yes |
|Whether all network errors are reported |Are network errors reported in full? If so, network errors ignore the sampling rate and are always reported. You can find network errors in a single log query. |No |No |


<span id="c30dd871"></span>
#### battery analytic


|**Parameters** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Data collection interval |Battery metric collection period. The unit is minutes. |5 |Not supported |
|Enable background collection |Does the App collect battery metric in Background. |Yes |Not supported |
|Overall battery monitoring sampling rate |The overall sampling rate of battery data. |10% |Not supported |
|Battery exception attribution reporting sampling rate |Sampling rate for battery exception data reporting. |50% |Not supported |
|The maximum duration for a single positioning session |Threshold duration for reporting a single positioning use as an exception. Unit: seconds. |120 |Not supported |
|Number of times positioning is obtained within 10 minutes |If positioning is used multiple times within 10 minutes, report it as an exception. |4 |Not supported |
|Duration of location queries within 10 minutes |Report an exception if the usage duration within a 10\-minute positioning period exceeds the threshold; the unit is seconds. |240 |Not supported |
|Duration of each wake lock hold |The duration for which a wake lock is held in a single instance before it is reported as an exception. The unit is seconds. |5 |Not supported |
|Wake lock acquisitions within 10 minutes |Obtaining the wake lock multiple times within 10 minutes will be reported as an exception. |240 |Not supported |
|Wake lock held duration in a 10\-minute period |The duration for which the wake lock is held within 10 minutes is reported as an exception. The unit is seconds. |120 |Not supported |
|Alarm (wake_up type): Number of wake\-ups within 10 minutes |An Alarm (wake_up type) that is triggered multiple times within 10 minutes should be reported as an exception. |5 |Not supported |
|Alarm wake\-up count within 10 minutes |If the alarm wakes up multiple times within 10 minutes, report as an exception. |10 |Not supported |


<span id="7f784366"></span>
#### CPU monitor


|**Configuration items** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Sampling rate for reporting the CPU metric |Sampling rate for CPU metric reporting. |5% |Not supported |
|CPU data sampling frequency in the foreground |The CPU metric collection period in the foreground. Unit: seconds. |120 |Not supported |
|CPU data sampling frequency for the application in the background |CPU metric collection period when in background. Unit: seconds. |600 |Not supported |
|Application data aggregation (processing of collected data) / reporting frequency |The reporting interval for aggregated application data. Unit: seconds. |120 |Not supported |
|Sampling rate for reporting CPU anomaly data |CPU anomaly data reporting sampling rate. |5% |Not supported |
|Exception threshold for CPU usage rate of background processes in applications |When running in the background, if the CPU Usage Rate exceeds this value, it is considered an exception. |2 |Not supported |
|Exception threshold for CPU Usage Rate of foreground processes in an application |In the foreground, if the CPU Usage Rate exceeds this value, it is considered an exception. |3 |Not supported |
|Thread CPU usage exception threshold |Thread CPU usage is considered abnormal when it exceeds this value. |0.05 |Not supported |
|Control whether to collect CPU exceptions for all processes |Collect CPU anomaly data for all processes. If No is selected, random sampling will be performed. |No |Not supported |
|Collect the sampling rate for the main process stack trace if the main thread exceeds the exception threshold |Sampling rate for collecting main thread stack trace information when a CPU anomaly occurs. |5% |Not supported |
|CPU anomaly sampling rate |CPU anomaly sampling rate. |Not supported |20% |
|CPU exception threshold |If the average CPU sampling rate within 60 seconds exceeds the threshold, a CPU anomaly is considered to have occurred. |Not supported |0.8 |
|CPU threshold for thread stack trace capture |When a thread's CPU usage exceeds the threshold, capture a stack trace for that thread. |Not supported |0.05 |
|Is it necessary to suspend the thread when capturing the stack trace |When capturing a thread's stack trace, is it necessary to suspend the thread? Capturing the stack while suspended is more accurate, but increases performance overhead. |Not supported |No |
|CPU metric sampling rate |The CPU metric sampling rate |Not supported |10 |
|CPU metric collection time interval |The CPU metric collection period. The unit is seconds. |Not supported |30 |


<span id="0f1b8df6"></span>
#### disk monitor


|**Configuration parameters** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Disk metrics sampling rate |Sampling rate of disk metrics. |1% |1% |
|Disk anomaly sampling rate |Disk anomaly sampling rate. |10% |10% |
|Disk collection time interval |The time difference between two disk collections. The unit is hours. |Not supported |24 |
|Threshold for disk usage analysis |Threshold for triggering disk file usage analysis. Unit: MB.<br><br>Expired files, exception files, and top\-consuming files will only be reported when the threshold is exceeded. |Not supported |100 |
|Maximum number of exception files to report |Reported file count (k). Regardless of whether they are expired files or folders, or exception files or folders, only the largest k files or folders are reported.<br><br><br>* Expired files and folders are sorted by expiration time.<br><br>* Exception files and folders are sorted based on file size. |20 |20 |
|File expiration time threshold |File expiration time threshold. Unit: days.<br><br>Only files that exceed this threshold will be reported as expired files. |20 |30 |
|Disk threshold for exception folder |The exception folder threshold size. The unit is MB.<br><br>The reporting of the exception folder will be triggered only when this threshold is exceeded. |20 |20 |
|Exception folder count threshold |Threshold for the number of sub\-files in the exception folder.<br><br>When the number of subfiles exceeds this threshold, the folder will be reported as an exception folder. |Not supported |20 |
|Exception threshold for disk usage |Threshold for reporting exception disk data.<br><br>The collection of detailed file data will occur only if the total size of App data exceeds this threshold. The unit is MB. |100 |Not supported |


<span id="60a15e13"></span>
#### traffic monitor


|**Configuration parameters** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Sampling rate for traffic metric monitoring |Sampling rate for traffic metric monitoring. |5% |Not supported |
|Traffic anomaly monitoring sampling rate |Traffic anomaly monitoring sampling rate. |5% |Not supported |
|Background 10\-minute traffic anomaly threshold |Background 10\-minute traffic anomaly threshold. Unit: MB. |50 |Not supported |
|The 10\-minute exception traffic threshold |10\-minute exception traffic threshold. Unit: MB. |500 |Not supported |
|The minimum size of traffic anomaly URLs |Minimum URL size for traffic anomaly. Unit: KB. |0 |Not supported |


<span id="f5bc7ef3"></span>
#### custom file


|**Configuration items** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Proactively report custom log sampling rate |Control the sampling status of actively reported Vlog/Alog logs to prevent backend file accumulation. |100% |100% |
|APMPlus log sampling rate |Customize the sampling rate for APMPlus logs. APMPlus logs include exception, performance, network, and event log data generated by the built\-in instrumentation of the APMPlus SDK. |100% |0% |


<span id="9a9fbd01"></span>
#### User metrics


|**Configuration parameters** |**DescriptionS** |**Android default values** |**iOS default value** |
|---|---|---|---|
|The user session duration sampling rate |User session duration sampling rate |2% |Not supported |
|Background duration sampling rate |Background duration sampling rate. |1% |Not supported |


<span id="d8944872"></span>
#### application exit


|**Parameter** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Application exit sampling rate |Apply the exit sampling rate. |1% |Not supported |


<span id="03637390"></span>
#### General settings


|**Configuration items** |**DescriptionS** |**Android default values** |**iOS default values** |
|---|---|---|---|
|Configure expiration time |Expiration time for the sampling configuration on the endpoint. After the platform updates the SDK sampling configuration, the client will only fetch the configuration again after the previous configuration expires. Unit: seconds. |3600 |3600 |
|Data reporting intervals |The client SDK polls and reports data according to the reporting interval, affecting the performance metrics, events, network, and other modules. Unit: seconds. |60 |60 |


<span id="22523dce"></span>
## Allowlist configuration

If you need to focus on the reported data from a specific device or user, you can do so by creating an allowlist. After creating the allowlist, all data from every feature module of the device or user is collected and reported in full.


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> SDK setting**.

4. In the filter area, select operating system.

5. Under the **device allowlist configuration** tab, click **create allowlist**.

6. On the **create allowlist** page, complete the following configuration, and then click **confirm**.

   Parameter description:

   
   |Parameter |DescriptionS |
   |---|---|
   |DeviceID |Enter DeviceID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After configuring the DeviceID, all data from every feature module of the current DeviceID is fully sampled and fully reported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">As long as either DeviceID or UserID is configured, data from all feature modules will be fully sampled and fully reported.</div><br> |
   |UserID |Enter UserID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After configuring the UserID, all data from all feature modules for the current UserID will be fully sampled and reported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If both DeviceID and UserID are configured, data from all feature modules will be fully sampled and reported as long as either one is valid.</div><br> |
   |Due Time |Configure the expiration time. Supports **Never expire** and **Selected date**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the same DeviceID or UserID appears in multiple configurations, the longest duration shall apply.</div><br> |
