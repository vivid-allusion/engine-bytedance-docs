---
title: "Crash analyses"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Crash_analyses"
---

The App Monitoring feature of Application Performance Monitoring Full\-Link Edition provides a crash analysis feature, supporting the collection and analysis of various abnormal crash types on both iOS and Android platforms, helping you resolve issues with greater accuracy.

Crash analysis provides analysis views from four dimensions and perspectives: crash trend analysis, crash distribution analysis, abnormal crash list, and crash details, making it easier for you to more comprehensively analyze the various abnormal crash types in your application.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Crash analysis has been integrated. For details, refer to [Integrating the Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) or [Integrating the iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app).

* Crash analysis has been configured. For details, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id="6c1cd704"></span>
## Crash trends

<span id="0a4b68a2"></span>
### Filter conditions

You can filter data using the following filter criteria:


* Filter dimensions supported by the Android system:

   Time, crash type, app version, crash details, device ID, user ID, issue creation status, presence of Hprof file, OOM status, foreground or background, system version, device model, app minor version, APM SDK version, download channel, ROM information, province, usage duration, process name, manufacturer, parsing status, app page, issue status, handler, tags, custom dimension, PV custom dimension.

   Android crash types include Java crash, Java startup crash, Native crash, and ANR.

* Filter dimensions supported by the iOS system

   Time, crash type, app version, crash details, device ID, User ID, issue creation status, start status, MemoryGraph file present, GWPAsan type, foreground or background, jailbreak status, system version, device model, app minor version, APM SDK version, download channel, province, usage duration, parsing status, app page, issue status, assignee, tags, custom dimension, PV custom dimension.

   The iOS crash types include crash, freeze, out\-of\-memory (OOM) crash, and extension crash.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An issue is a category of crash formed by aggregating crashes according to stack information.</div>


   <div data-tips="true" data-tips-type="tip">For example, after version 1.0 is released, crashes A, B, and C occurred. When version 2.0 is released and crash D occurs, crash D is considered a new issue.   </div>
   

* <div data-tips="true" data-tips-type="tip">The status label added to an issue indicates the version in which the issue first appeared.</div>


   <div data-tips="true" data-tips-type="tip">For example, the product has two versions: Banana 1.1.0 and Panda 1.1.0. Crash A occurs in both versions, but it first appears in Panda 1.1.0. Therefore, crash A is classified as a new issue. When you select the <strong>New issue status</strong> filter condition and choose <strong>New</strong>, you can only view crash data from the Panda 1.1.0 version.   </div>
   


<span id=".5bSp5rqD6LaL5Yq_"></span>
### Crash trend chart

Crash trend displays a trend chart of crash metrics based on filter criteria. You can also display the trend chart by grouping dimensions. You can view changes in crash data compared to the previous period on the right side of the metric data.


* Indicator description:

   
   |**Metric** |**DescriptionS** |
   |---|---|
   |Number of crashes |Number of crashes under filter conditions |
   |Crash rate |Number of crashes under filter conditions / Total number of launches under filter conditions (PV) |
   |Users affected by crashes |Number of users who experienced crashes under filter conditions |
   |User crash rate |Number of UVs with crash errors under filter conditions / Total number of UVs under filter conditions |
   |Number of users |UV when filters are applied |
   

* Supports displaying indicator trend charts by group.

   * Grouping dimensions commonly used across both platforms include: APP version, APP minor version number, crash type, foreground or background, system version, device model, APM SDK version, download channel, province, usage duration, parsing status, and APP page.

   * The grouping dimensions supported only on the Android side include: ROM information, process name, manufacturer, HarmonyOS, ANR attribution, FD count greater than 1000, successfully captured logcat, remaining system storage space, remaining memory storage space, remaining sdcard storage space, whether the device is 64\-bit, whether the APK is 64\-bit, whether the device is rooted, whether the device is x86, Java heap memory usage exceeding 95 percent, the Activity most recently resumed, thread with highest stm usage, thread with highest utm usage, virtual memory usage exceeding 2.8 GB for 32\-bit or 3.8 GB for 64\-bit, native heap memory usage exceeding 200 MB, successfully captured FD list, successfully captured thread state list, and successfully captured thread state.

   * The grouping dimensions that are only supported on iOS include: start status, jailbreak status, system memory pressure status, and app memory usage anomaly.

      * Memory pressure status: The overall memory pressure status of the system, including other processes. Different data represent the levels of memory pressure.

         * 0: Default value. It may not have been updated due to a rapid increase in memory usage or for other reasons.

         * 2: Memory pressure is low, and there is still some free system memory available. However, security warnings have already started to appear. If possible, unnecessary resources should start to be released.

         * 4: Memory pressure is moderate, and system memory is already tight. If an application consumes additional memory, the application may be turned off by the system. Therefore, proactive measures should be taken to reduce memory usage.

         * 16: Memory pressure is relatively high, system memory resources are already severely insufficient, and applications are about to be terminated by the system.


<span id=".5bSp5rqD5YiG5biD"></span>
### Crash distribution

Crash distribution supports multidimensional analysis to help understand the distribution of crashes and locate issues.


* Hovering over the distribution chart allows you to view the full name of the current category and its proportion within this metric type.

* By default, the error distribution is displayed across four dimensions: **system version**, **device model**, **app version**, and **app minor version number**. You can click the settings button to select other dimensions, for example, crash type, foreground or background, download channel, and many other options. The available dimensions differ between Android and iOS systems.

   The dimension supported by the Android system, **remaining system storage space**, refers to the `/system` partition. When the remaining system storage space is between 0 and 1k, there are two possibilities: first, the system partition space is relatively small; second, the system space size failed to be read.

* By default, the error distribution is displayed based on **report volume**, but you can also configure it to display the error distribution based on **user volume**.


<span id="064ccea2"></span>
#### ANR crash attribution

If your business scenario involves crashes of the ANR type, you can select ANR attribution for multidimensional analysis in the crash distribution module. By analyzing the original reported data—including stack information, ANR_INFO, scheduling sequence diagrams, updated memory information, and similar details—you can perform a preliminary classification of ANR attribution. Because the causes of ANR are complex and are usually not determined by a single factor, the results of preliminary classification are for reference only.


|**Attribution name** |**DescriptionS** |**Determination methods** |
|---|---|---|
|app_deadlock_or_block |Timeout of application main thread lock and other locks |The main thread call stack is waiting for a lock, and the wall time of the current message is greater than 1 second. |
|app_too_many_msg |The application sends messages too frequently, which causes message blocking. |There are more than 100 identical timeout messages in the scheduling sequence diagram, and the average interval between sending these messages is less than 5 ms. |
|app_with_barrier |The application's main thread is blocked for a long time by barrier messages |The first pending message is a barrier, and the current message has a wall time greater than 3 seconds, a cpu/wall ratio less than 0.3, and a msg of "no message running". |
|app_not_call_startforeground |The application did not call startForeground() within the required time. |The anr_reason is shown as "not call Service.startForeground". There are no timeout messages in the scheduling timing diagram, which indicates that the main thread is not busy. The system status is also good. |
|app_dex2oat |Dex2oat's CPU usage is too high |CPU usage of dex2oat in ANR_INFO is greater than 50%. |
|app_current_long_msg_exec(\>=1s) |The CPU runtime for the current message (excluding wait time) is too long |The CPU time of the current message is greater than or equal to 1 second. |
|app_sleeping_long |Application main thread sleep duration is too long |The main thread sleeps for more than 3 seconds |
|app_io_operation |Duration of IO operations on the application's main thread |Main thread IO operations take longer than 3 seconds |
|app_sync_with_sub_thread |A timeout occurs when the application's main thread and other subthreads complete tasks |The main thread waits for child threads for more than 3 seconds. |
|app_binder_call |Application main thread binder call timeout |Binder calls take more than 3 seconds |
|app_wait_gc |The application's main thread is blocked at WaitForGcToCompleteLocked, waiting for GC to complete. |Main thread waits for GC for more than 3 seconds |
|app_current_long_msg_wait(\>=3) |The wall time (including waiting time) for the current message is too long |The wall time of the current message is greater than or equal to 3 seconds, and the system status is good. |
|app_memleak |Application memory leak |Custom dimension (java_heap_leak): Java heap usage exceeds 95%<br><br>This is similar to excessive Java heap memory usage. |
||Application memory leaks |Live data\-memory data\-totalPss<br><br>Physical memory already used by the overall process (allocated according to the proportion of shared occupancy)<br><br>Applications with PSS greater than 500 MB |
|app_history_long_msg_exec(\>=1s) |The CPU takes a long time to process historical messages |Historical messages with CPU duration ≥ 1s |
|app_history_long_msg_wait(\>=5s) |Historical message wall experiences long wait times |Type 8 historical messages with a wall duration of at least 5 seconds and normal system status. |
|app_cpu_usage_high_sub_thread(\>=150%) |The application's CPU usage is high. |ANR_INFO<br><br>The application's CPU usage is high (≥150%), and subthreads account for the highest proportion among all threads. |
|app_cpu_usage_high_main_thread(\>=150%) |High CPU usage of the application |ANR_INFO<br><br>The application's CPU usage is high (≥150%), and the main thread has the highest CPU usage among all threads. |
|sys_kswapd_high(\>15%) |The system memory pressure is high |ANR_INFO<br><br>The application status shows no obvious abnormalities, but the CPU usage of the system process kswapd is greater than 15%. |
|sys_iowait_high(\>15%) |High system IO load |ANR_INFO<br><br>There are no obvious abnormalities in the application status, but the system's iowait percentage exceeds 15%. |
|sys_mmcqd_high(\>15%) |High system I/O load |ANR_INFO<br><br>There is no obvious abnormality in the application status, but the system process mmcqd accounts for more than 15%. |
|sys_load_high(\>20) |System load is too high |ANR_INFO<br><br>There is no obvious abnormality in the application status, but the system's CPU load is greater than 20. |
|sys_cpu_usage_high(\>=80%) |The system CPU usage is too high |ANR_INFO<br><br>The application status shows no obvious abnormalities, but the system's CPU usage exceeds 80%. |
|invalid_log |The captured log is incomplete. |SDK attribution information incomplete |
|reason_uncertain |Attribution cannot be confirmed based on the current judgment logic. |None of the above attribution logic is satisfied. |


<span id=".5byC5bi45bSp5rqD5YiX6KGo"></span>
### Abnormal crashes list

The abnormal crash list displays aggregated data for crashes of the same type, including the crash description, crash type, number of affected users, number of occurrences, crash rate, most recent occurrence time, log reporting time, status, and person responsible.


* Note: Click to go to **crash details** to view more information about the crash.

* Affected user count: Click the icon after the number to preview the trend chart. Hover over the trend chart to view the corresponding time.

* Occurrence count: Click the icon next to the number to preview the trend chart. Hover over the trend chart to view the corresponding time.

* Sorting: By default, the list is sorted in descending order by number of affected users, number of occurrences, and crash rate. Click **Latest occurrence time** or **Log reporting time** to sort by time in descending or ascending order.

* Download: Click the download button in the upper right to download the first 100 data entries, which will be presented in the `.xlsx` file format.

* Settings: Click the settings button in the upper right corner to customize the columns displayed in the list. In addition to the default column data, you can configure: year\-over\-year occurrence count, year\-over\-year affected user count, year\-over\-year crash rate, affected user rate, year\-over\-year affected user rate, start and end versions, and start and end minor version numbers.


<span id="fa387746"></span>
## Crash details

On the crash details page, you can view the properties of each field for an individual crash.


|Crash fields |DescriptionS |
|---|---|
|Crash summaries |Includes issue title, key stack information, most recent report time, most recent occurrence time, first occurrence time, crash description, number of crashes, number of affected users, crash rate, and crash user ratio. You can also configure custom labels for issues. For details, refer to [Label Management](https://docs.byteplus.com/en/docs/apmplus/Platform_setting#.5qCH562-566h55CG). |
|Crash trends |The trend in the number of crashes and affected users for this issue |
|[Automatic analyses](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses#.6Ieq5Yqo5YiG5p6Q) |Aggregate information about crash distribution to make the information more focused.<br><br>For more feature distributions, refer to [Crash distribution](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses#f26c8320). |
|Crash distributions |Gain insight into the distribution of issues across different dimensions through multidimensional analysis. |
|Logcat word cloud |Crash issue analysis involves multiple dimensions, and Logcat log files store logs of program execution within the crashed process. When troubleshooting crash issues, it is sometimes necessary to review large amounts of Logcat logs line by line, which can be quite time\-consuming.<br><br>A word cloud can automatically analyze logs under an issue to identify frequently occurring log segments, helping to analyze crash problems.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is currently not supported on iOS.</div><br> |
|Page history aggregation trees |Aggregates the historical paths of application pages and displays the aggregation status of the historical paths for the current issue. Detailed crash path history data can be viewed in the Page Tracking section under Site Data. |
|Details |Query the attributes of each field for a single crash. |
|Original stack & Retrace |* iOS: If the symbol table has not been uploaded, the raw stack trace is displayed, which is the stack trace information from the original logs uploaded by the client. After the symbol table is uploaded, the symbolicated stack trace is displayed, that is, the stack trace after symbolication.<br><br>* Android: If the symbol table is not uploaded, the obfuscated stack trace is displayed; after the symbol table is uploaded and parsed, the original stack trace is displayed.<br><br>* If the symbol table or parsing is incorrect, you can click **Retry Retrace** on the **Retrace** interface. |
|Symbol table |Upload and download symbol tables manually |
|Field data |On\-site data includes storage data at the time of the crash, reported custom field attributes, and recently opened pages. |
|Native information |For each crash occurrence, Native information includes Native's Maps details list, smart classification of Maps, FD classification, process status, thread status, and thread classification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is currently not supported on iOS.</div><br> |
|ANR_INFO |ANR_INFO reports and displays information such as processName, tag, shortMsg, longMsg, Reason, Load, Android time, CPU usage, and more when an ANR occurs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is currently not supported on iOS.</div><br> |
|Scheduling sequence diagrams |The scheduling sequence diagram visualizes message scheduling durations and errors, providing information such as Wall Time and CPU Time. Different colors are used to highlight error nodes and nodes with long execution times.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is not currently supported on iOS.</div><br> |
|Tracking logs |The tracking logs display the log stream before and after a crash, including process and thread information, log level, log details, and support search and filter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is temporarily not supported on iOS.</div><br> |
|Crash information |Different crash types display different crash information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is not currently supported on Android.</div><br> |
|Custom logs |Custom Logs support retrieving and reporting custom log content, including process and thread information, log level, log details, as well as search and filter. |
|File downloads |The file download feature supports downloading files, including original crash information, custom files, and more. |


<span id=".6Ieq5Yqo5YiG5p6Q"></span>
### Automatic analyses

Automatic analysis is the aggregation of information about crash distributions, making the information more focused. For more feature distributions, refer to [Crash distribution](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses#f26c8320).


<Tabs>
<Tab zoneid="txrJsphJ1v" title="">
<TabTitle></TabTitle>




</Tab>
</Tabs>


<span id="f26c8320"></span>
### Crash distributions

Crash distribution supports understanding how issues are distributed across different dimensions through multidimensional analysis.

Settings: Click the settings button in the upper right corner to configure other dimensions and view their distribution to locate issues.

<span id="19920764"></span>
### Logcat word cloud

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is not currently supported on iOS.</div>


Crash problem analysis involves multiple dimensions, and Logcat log files store logs of the program's execution within the crashed process. During crash troubleshooting, it is sometimes necessary to review large volumes of Logcat logs line by line, which can be quite time\-consuming. The word cloud feature can automatically analyze logs associated with an issue to identify frequently occurring log segments, assisting in the analysis of crash issues.

On the issue details page, switch to the **Logcat** tab to see the following analysis report example.

Logs in the analysis report are sorted by frequency; text color has no special meaning.

Explanation of terms:


|**Glossary** |**Meaning** |
|---|---|
|Frequency |Proportion of occurrences of this log line after desensitization in all Logcat log files |
|Weight |Leverage internal experience to perform dynamic weighting based on specific terms, highlighting specific terms that appear in logs. |
|Logs |The string generated after performing actions such as desensitization on a single log entry within Logcat logs |


The word cloud feature provides effective assistance in analyzing crash issues caused by leaks, disk full conditions, high\-frequency abnormal error reports, and other factors.

Problem description:


|**Problem types** |**Keyword examples** |
|---|---|
|Insufficient disk space |SQLiteFullException, disk I/O error, failed to open database, and many others |
|Communication\-related |socket timeout、Broken pipe |
|fd\-related |Too many open files, EMFILE, Bad file descriptor, and similar errors |
|Memory\-related |GL error, mmap failed, ashmem_create_region, and more |


<span id="8ceffc8d"></span>
### The page history aggregation tree

The page history aggregation tree aggregates the historical paths of application pages and displays the aggregation status of historical paths for the current issue. Detailed data on the history of crash paths can be viewed in the page tracking section under site data.


* The page path is recorded and restored according to Activity lifecycle methods, resulting in the historical path.

* In the historical path, the first layer is the page where the crash occurred. From top to bottom, the layers represent a backtrace of page paths, with a maximum backtrace depth of 10 layers. Among them, the width of each layer represents the percentage occupied by the current path.

* The node names in the page path include the class name of the Activity and the full names of its lifecycle methods. The lifecycle methods include the onCreate method and the onStart method.

   * The onCreate method generally indicates that this Activity has just been started.

   * The onStart method typically indicates that the Activity at the current node is returning from another page.

* The aggregation tree supports filtering crash data using filter options. The page displays up to 100 crash data entries in aggregate. If there is too little data, you can expand the time range to filter more crash data.

* Each color block in the aggregation tree supports double\-clicking to expand the current path, and double\-clicking again restores the color block to its initial state.

* The filter box in the upper left corner supports filtering pages where crashes occurred.


<span id=".6K-m57uG5L-h5oGv"></span>
### Detailed information

In the details, you can check the properties of each field for a single crash.


* **Trace**: Click **Trace** next to the device ID or UserID to navigate to [Single-point Trace](https://docs.byteplus.com/en/docs/apmplus/log_query) and query the complete context log stream.

* Switch crash details: Use the switch in the top right corner to switch between crashes.

* Download: Click the download button in the upper right corner to download the log file. The log details are provided as a `.txt` file.


<span id=".5Y6f5aeL5aCG5qCIJlJldHJhY2U="></span>
### The original stack and Retrace


<Tabs>
<Tab zoneid="kWF61TsN2Y" title="iOS">
<TabTitle>iOS</TabTitle>

If the symbol table has not been uploaded, the original stack trace is displayed, which refers to the stack trace from the original logs uploaded by the client. If the symbol table has been uploaded, the symbolized stack trace is displayed, that is, the stack trace after symbolization.


* If there is an error in the symbol table or parsing, you can re\-upload the symbol table or click **Retry Retrace** in the Retrace interface.

* When a deadlock occurs, the lock wait relationships of threads will be analyzed. If a lock wait relationship exists, it will be displayed in Retrace.

* If you turn on GWPAsan sampling, you can view the GWPAsan type and stack in Retrace.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Turning on GWPAsan may increase the crash rate; please consider carefully.</div>



</Tab>
<Tab zoneid="bioNVV6UCg" title="Android">
<TabTitle>Android</TabTitle>

If the symbol table is not uploaded, an obfuscated stack is displayed. After the symbol table is uploaded and parsed, the original stack is displayed. If there is an error with the symbol table or parsing, you can click **Retry Retrace** on the **Retrace** interface.


</Tab>
</Tabs>


<span id=".546w5Zy65pWw5o2u"></span>
### Site data


<Tabs>
<Tab zoneid="Un7GBR4LCp" title="iOS">
<TabTitle>iOS</TabTitle>

On\-site data includes storage information at the time of the crash, reported custom field attributes, and the most recently opened pages.


* **Storage data**: Displays storage information when a crash occurs

* **Custom data**: Display the attributes of reported custom fields

* **Page tracking**: Displays page actions before and after a crash


</Tab>
<Tab zoneid="jE3e8U3oqw" title="Android">
<TabTitle>Android</TabTitle>

On\-site data includes information about data stored at the time of the crash, reported custom field attributes, the most recently opened page, and the page viewed before the crash.


* **Storage data**: Displays storage information when a crash occurs

* **Page information**: Displays recent Create and Resume interfaces, among others, to assist in locating crash issues

* **Custom data**: Displays the properties of reported custom fields

* **Page tracking**: Displays page actions before and after a crash


</Tab>
</Tabs>


<span id="ffdac15c"></span>
### Native information

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is not currently supported on iOS.</div>


Native information includes details for each crash, such as the Native Maps details list, intelligent categorization of Maps, FD categorization, process status, thread status, and thread categorization.


|Crash information |DescriptionS |
|---|---|
|Maps details |Displays the starting address, ending address, page size, permission, file offset, memory segment name, and classification tag. |
|Maps Intelligent Attribution |This demonstrates intelligent crash attribution based on Maps details. |
|FD attribution |Display FD attribution based on the handle. |
|Process states |Display a detailed list of process states during a crash. |
|Thread states |Display a detailed list of thread statuses during a crash. |
|Thread categories |Display crash information categorized by thread.<br><br>Among them, Utm, Stm, and runtime duration represent the sum of the values of threads within the group.<br><br>For example, a runtime duration of 8 hours indicates the total runtime of all threads in this group. |


<span id="736cb458"></span>
### ANR_INFO

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently not supported on iOS.</div>


ANR_INFO reports and displays processName, tag, shortMsg, longMsg, Reason, Load, Android time, CPU usage, and related information when an ANR occurs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1bb6b195d891185ac6beae14fe3fe85e.png) </span>

<span id="ac3ea960"></span>
### Scheduling sequence diagrams

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is not currently supported on iOS.</div>


The scheduling sequence diagram displays the duration and errors involved in message scheduling, including information such as Wall Time and CPU Time. Different colors are used to highlight error nodes and nodes that take a long time.

After expanding the messages, if you want to collapse them, please first uncheck **Show only long\-duration messages**, and then check **Show only long\-duration messages**.

<span id="83de611e"></span>
### Tracking logs

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is not currently supported on iOS.</div>


The tracking logs display the log stream before and after a crash, including process and thread information, log level, and log details. Search and filter functions are supported.

<span id=".5bSp5rqD5L-h5oGv"></span>
### Crash information

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Android does not currently support this feature.</div>


Different crash types display different crash information.


|**Crash types** |**Display modules** |**DescriptionS** |
|---|---|---|
|Crash |Details |Display some specific information about the crash, such as crash type, crash cause, and more. |
||Registers |Register information at the time of a crash is not collected by default. You can enable collection reporting on the **SDK reporting configuration** page, in the **Crash Analysis \> Whether to enable register analysis** configuration. Language exceptions will not be reported. |
||Stack memory |Stack memory information at the time of a crash is not collected by default. You can turn on collection and reporting in the **SDK reporting configuration** page, in the **Crash analysis \> Enable stack memory analysis** configuration. Exceptions related to programming languages will not be reported. |
||Dealloc stack |Record the stack trace when a Zombie object is released. After you turn on the online Zombie Monitoring feature, this information will be reported if a Zombie issue occurs. |
|Frozen |\- |Display the duration of the application freeze before exit. |
|OOM crash |\- |Show the trend in memory usage before the application exits. |


<span id="4cd18601"></span>
## Crash rankings

<span id="93b22f78"></span>
### Filter criteria

You can filter data using the following filter criteria:

Time, system version, app version, APM SDK version, issue status

<span id="3d4abfaf"></span>
### Detailed data

The details list displays, by default, data sorted by crash rate from highest to lowest. This allows you to observe the distribution of crash rates for integrated applications and provides insights for application optimization analysis.


* Distribution chart: Click the **distribution chart** in the System Version Distribution column to view the distribution of system versions in which crashes occurred for that app version. If a particular system version accounts for a large proportion in the distribution chart, focused optimization and troubleshooting of issues are required. The channel and device model distribution charts function the same way as the system version distribution chart.

* Download: Click the download button in the upper right corner to download the first 10,000 crash data entries, displayed in xlsx format.


<span id="913174ab"></span>
## Application exit reasons

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Analysis of application exit reasons is only supported for data from Android applications.</div>


<span id="11199cea"></span>
### Filter criteria

You can filter data using the following filter criteria:

Time, device ID, User ID, **Whether the user exited voluntarily**, **Exit reason type**, **Exit reason subtype**, APP page, system version, device model, APP version, APP minor version number, APM SDK version, download channel, ROM information, province, usage time, process name, manufacturer, issue status, assignee, tags.

<span id="e7e7d51a"></span>
### Background Information

Supported exit reason types:


|**Status number** |**Status names** |**Exit reasons** |**Note** |
|---|---|---|---|
|0 |REASON_UNKNOWN |Unknown cause |Android 11 new features |
|1 |REASON_EXIT_SELF |A process requests to exit on its own, typically by actively calling exit. ||
|2 |REASON_SIGNALED |The process was terminated by a signal ||
|3 |REASON_LOW_MEMORY |Insufficient system memory causes processes to be killed. ||
|4 |REASON_CRASH |JavaCrash causes the process to exit ||
|5 |REASON_CRASH_NATIVE |NativeCrash causes process exit ||
|6 |REASON_ANR |ANR (Application Not Responding) causes the process to exit ||
|7 |REASON_INITIALIZATION_FAILURE |Process initialization failed, exiting. ||
|8 |REASON_PERMISSION_CHANGE |Exit due to application permission change ||
|9 |REASON_EXCESSIVE_RESOURCE_USAGE |The process exits due to excessive resource consumption. ||
|10 |REASON_USER_REQUESTED |The application process is terminated at the user's request, such as through "Force stop" or removal from "Recent apps". ||
|11 |REASON_USER_STOPPED |User stops process and exits ||
|12 |REASON_DEPENDENCY_DIED |The process that the current process depends on has died, causing the current process to be killed (binder c/s). ||
|13 |REASON_OTHER |Other unknown causes ||
|14 |REASON_FREEZER |The application process is killed by App Freezer, such as when it receives synchronous binder transactions while it is frozen. |What's new in Android 13 |


Support for exit reason subtypes:


|**Status ID** |**State name** |**State exit reason subtypes** |**Note** |
|---|---|---|---|
|0 |SUBREASON_UNKNOWN |Unknown substates |New features in Android 11 |
|1 |SUBREASON_WAIT_FOR_DEBUGGER |Process waiting for debugger ||
|2 |SUBREASON_TOO_MANY_CACHED |Process cache is excessive and needs to be released ||
|3 |SUBREASON_TOO_MANY_EMPTY |There are too many processes; please release resources. ||
|4 |SUBREASON_TRIM_EMPTY |Released an idle process ||
|5 |SUBREASON_LARGE_CACHED |The process cache is too large and needs to be released. ||
|6 |SUBREASON_MEMORY_PRESSURE |Processes were killed due to system memory pressure ||
|7 |SUBREASON_EXCESSIVE_CPU |The process is consuming excessive CPU resources and needs to be terminated. ||
|8 |SUBREASON_SYSTEM_UPDATE_DONE |The system update has been completed. The process resources need to be released. ||
|9 |SUBREASON_KILL_ALL_FG |Kill all foreground processes ||
|10 |SUBREASON_KILL_ALL_BG_EXCEPT |Kill all background processes except the specified process ||
|11 |SUBREASON_KILL_UID |Kill processes with the specified UID ||
|12 |SUBREASON_KILL_PID |Kill the process with the specified PID ||
|13 |SUBREASON_INVALID_START |Process failed to start ||
|14 |SUBREASON_INVALID_STATE |The process is in an invalid state. ||
|15 |SUBREASON_IMPERCEPTIBLE |Background process was killed. If the application is running in the background and there are many foreground processes, any background process that is killed will be marked as this type. ||
|16 |SUBREASON_REMOVE_LRU |Remove LRU subtype reason, delete least recently used application scenarios ||
|17 |SUBREASON_ISOLATED_NOT_NEEDED |Reasons why isolated processes do not require subtypes ||
|18 |SUBREASON_CACHED_IDLE_FORCED_APP_STANDBY |The process was terminated because it was in a forced application standby state and had been cached and<br><br>Attribution of REASON_OTHER subtypes for processes with an idle uid status |New in Android 12 |
|19 |SUBREASON_FREEZER_BINDER_IOCTL |Type attribution for REASON_FREEZER, but binder cannot be performed. ||
|20 |SUBREASON_FREEZER_BINDER_TRANSACTION |Type attribution for REASON_FREEZER, binder peer being killed, and other reasons ||
|21 |SUBREASON_FORCE_STOP |Force stop\-type kill |New features in Android 13 |
|22 |SUBREASON_REMOVE_TASK |remove task ||
|23 |SUBREASON_STOP_APP |stop app ||
|24 |SUBREASON_KILL_BACKGROUND |Background process was killed ||
|25 |SUBREASON_PACKAGE_UPDATE |Package update causes termination ||


<span id="36235f4e"></span>
### Reported trends chart

The reporting trend chart shows the trend of application exits under the current filter conditions. You can also display the trend chart by group. On the right side of the indicator data, you can view changes in reported data compared to the previous period.

Indicator description:


|Metric |DescriptionS |
|---|---|
|Reporting frequency |Number of app exit reports under filter conditions |
|Reporting rate |Number of reported application exits under filter conditions / total number of page views under filter conditions |
|Reported user count |Number of users who exited the application with a filter applied |
|Proportion of users reported |Number of users who exited the application under filter conditions / Total unique visitors under filter conditions |


<span id="b4a88896"></span>
### Report distribution maps

The reporting distribution feature enables users to understand the distribution of application exit reasons through multidimensional analysis, helping to locate issues.


* Hover over the distribution chart to view the full name of the current category and its proportion within this indicator type.

* By default, the error distribution is displayed across four dimensions: **APP version**, **APP minor version number**, **exit reason type**, and **exit reason subtype**. You can click the settings button to select other dimensions, for example, APP page, system version, download channel, and many other options.

* By default, the error distribution is displayed based on the **number of reports**, but it can also be configured to display the error distribution based on the **number of users**.


<span id="c9676352"></span>
### Report lists

The report list displays data aggregated by exit reason type, including exit type, number of reporting users, number of reports, reporting rate, application exit time, log reporting time, exit subtype, status, and handler.


* Exit reason: Click to navigate to the application exit reason details page to view more information about exit reasons.

* Reported user count / report frequency: You can preview the trend chart using the icon after the number. Hovering over the trend chart allows you to view the corresponding time.

* Sorting: By default, sorted in descending order by number of reporting users, number of reports, and reporting rate. You can sort the application exit time or log reporting time in ascending or descending order by clicking the column header.

* Download: Click the download button in the upper right corner to download the first 100 data entries from the list in `.xlsx` file format.

* Settings: Click the settings button in the upper right corner to customize the column data displayed in the list. In addition to the default column data, you can also configure year\-over\-year occurrence count, year\-over\-year affected user count, affected user rate, year\-over\-year affected user rate, year\-over\-year reporting rate, and start and end versions.


<span id="e621e222"></span>
### Application exit reason details

In the application exit reason details, a category of data aggregated based on the selected exit reason is displayed. Includes metric data, reporting trends, reporting distribution, detailed information and exit reasons, field data, tracking logs, and file download.


* Exit reason: View detailed information about application exit reasons, which is important for analysis.

* Field data: View the actual field data when the application exits to help analyze the reasons for application exit.

* Tracking logs: View the context logs of application exits to facilitate analysis and troubleshooting of application exit reasons.

* File download: Download `DumpFile.zip`, and view the packaged log files.
