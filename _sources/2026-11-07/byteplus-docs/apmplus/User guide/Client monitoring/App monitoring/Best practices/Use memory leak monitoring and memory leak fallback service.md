---
title: "Use memory leak monitoring and memory leak fallback service"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_memory_leak_monitoring_and_memory_leak_fallback_service"
---

This article uses an Android App as an example to introduce the complete process of integrating and using memory leak in App applications.

<span id="d7d35153"></span>
## Step 1: Obtain the SDK


1. In the project\-level `build.gradle` file, add the Maven address.

   ```Java
   buildscript {
       repositories {
           maven {
               url "https://artifact.bytedance.com/repository/Volcengine/"
           }
           maven {
               url "https://artifact.bytedance.com/repository/byteX/"
           }
       }
   }
   allprojects {
       repositories {
           maven {
               url "https://artifact.bytedance.com/repository/Volcengine/"
           }
       }
   }
   ```
   

2. Integrate Application Performance Management Plus.

   1. In the dependencies section of the project\-level `build.gradle` file, add the following code to integrate the plugin component for auxiliary instrumentation. `apm_insight_plugin` The same version is used both domestically and overseas.

      ```Java
      classpath "com.volcengine:apm_insight_plugin:1.4.2"
      ```
      

   2. In the dependencies section of the `build.gradle` file in the app module, add the following code. Select one of the two versions below depending on whether your application is domestic or overseas.

      * Applications in China integrate with the cn version, report data to servers in China, and use the following dependencies:

         ```Java
         // Add domestic applications in dependencies
         implementation 'com.volcengine:apm_insight:1.5.6.cn'
         implementation 'com.volcengine:apm_insight_crash:1.5.9'
         ```
         

      * For overseas applications, use the oversea version, report to Johor, Malaysia, and use the following dependencies:

         ```Java
         // Add overseas applications to dependencies
         implementation 'com.volcengine:apm_insight:1.5.7.oversea'
         implementation 'com.volcengine:apm_insight_crash:1.5.8.oversea'
         ```
         


<span id="21c4e473"></span>
## Step 2: Initialize SDK and turn on monitoring


1. In the onCreate method of Application, add the following code to initialize performance\-related features.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please add the code for initializing performance\-related features in the main thread.   </div>
   

   ```Java
   //Must be placed in Application's onCreate method; registers a lifecycle listener and does not involve data collection or privacy compliance issues.
   ApmInsight.getInstance().init(application);
   //Initialize custom log and configure the maximum disk usage for custom log. Typically, the internal configuration is set to 20, which means the maximum disk usage is 20 MB. This API was introduced in version 1.4.1.
   VLog.init(this,20);
   ```
   

2. Start performance monitoring and begin collecting data.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Call the method to collect data only after the user has agreed to the privacy policy.   </div>
   

   ```Java
   ApmInsightInitConfig.Builder builder = ApmInsightInitConfig.builder();
   //Turn on leak detection and leak fallback detection capabilities. Sampling for leak detection and leak fallback detection must be configured separately on the platform.
   builder.detectActivityLeak(new IActivityLeakListener() {
       @Override
       public void onActivityLeaked(Activity activity) {
           // Callback for activity leakage
      }
   });
   ApmInsight.getInstance().start(builder.build());
   ```
   

3. At the outermost level of the `build.gradle` file in the app module, add the following code to complete instrumentation.

   To enable startup analytic and page experience features that depend on plugin instrumentation, you must configure the ApmPlugin whiteList to include your package name. After configuration, the code in your package directory will be instrumented.

   ```Java
   ApmPlugin {// Whether to perform instrumentation
       enable true// Whether to instrument the Debug package; instrumentation is disabled by default
       enableInDebug true// DEBUG("DEBUG"), INFO("INFO"), WARN("WARN"), ERROR("ERROR"); // The DEBUG level log aggregates all instrumented classes for viewing. Path: app/build/ByteX/ApmPlugin/ApmPlugin_log.txt
       logLevel "DEBUG"// Startup analytic switch: To monitor App startup duration, pageLoadSwitch must also be enabled
       startSwitch = true// Page response switch: Monitoring Activity lifecycle duration
       pageLoadSwitch = true// Network monitoring switch: Monitoring network requests made by okhttp3
       okHttp3Switch = true// Switch to display instrumentation for HttpUrlConnection network requests
       httpUrlConnectionSwitch = true// Instrumentation is performed for packages under the allowlist. You need to specify the package name where the class to be instrumented is located; prefix configuration is supported.
       whiteList = ["com"
       ]// Classes under blocklist packages are not instrumented. You can configure package names and class names; if none, leave blank.
       blackList = ["com.xxx"
       ]
   }
   ```
   


<span id="4ffa4f92"></span>
## Step 3: Complete the SDK reporting configuration

After turning on the leak detection and leak fallback handling switches on the client side, the platform can also control leak detection and leak fallback handling. Leak fallback handling depends on leak detection. For the detailed procedure, refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> SDK setting**.

4. In the filter area, click the **Android** operating system.

5. Under the **each module sampling rate configuration** tab, click **memory optimization**.

6. On the memory optimization configuration page, turn on the **main switch**.

   When the main switch is turned on, data is reported according to the sampling configuration; when it is turned off, the entire module does not report data.

7. Select the parameter **memory leak detection sampling rate**, then click **create configuration**, and modify the sampling rate.

8. Select the parameter **memory leak fallback sampling rate**, then click **create configuration**, and modify the sampling rate.

   * Memory leak detection sampling rate: Controls whether memory leak detection is enabled in the fallback solution for memory leaks.

   * Memory leak fallback sampling rate: Controls whether the memory leak fallback solution is performed

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please turn on the memory leak fallback sampling rate with caution, and gradually increase the sampling rate. The fallback operation will clear the background image of the view to prevent exceptions caused by improper logic that may still attempt to modify the view's background image after Activity onDestroy.   </div>
   

<span id="6a54bf55"></span>
## Step 4: Configure leak events

After a leak event is detected on the client side, if it is determined that the platform is configured to report leak events, the name of the leaked Activity will be reported to the platform. This allows the platform to view which Activity has more leak occurrences. However, because parsing the leak reference chain requires dumping memory, which has a significant impact on performance, we do not dump memory snapshots here to analyze the leak reference chain. Instead, the leak reference chain is used only as a monitoring metric. The specific leak reference chain can be identified and troubleshooted by hooking into the OOM crash event to obtain a memory dump for analysis.


1. In the upper left corner of the console, select **All features \> Event management**.

2. In the filter area, click **Android**, then click **Add event**.

3. On the create event page, complete the following configuration, then click **create**.

   Parameter description:

   
   |Configuration area |Parameter |DescriptionS |Example |
   |---|---|---|---|
   |Event information |Event name |Custom name used to identify the event. The event name must not be the same as any existing event name. |apmplus_activity_leak_monitor |
   ||Event description |Enter event description. |None |
   ||System |Select operating system. You can choose Android or iOS. |Android |
   ||Tag |Select tags. Makes it easier to find the event. |None |
   |Metric and dimension information |Name |Enter the metric or dimension name. |leak_activity |
   ||Type |Supports selecting type, metrics, and dimensions.<br><br><br>* Dimension: If you only want to view the report volume of custom data, select the custom dimension.<br><br>* Metric: If you want to view the report volume, average value, and PCT value of custom data, select custom metric. |Subnamespace |
   ||Description |Enter a description of a metric or dimension. |None |
   |Report configuration |Rule name |The custom rule name is used to identify the rule. |Full collection |
   ||Sampling rate |Configure the sampling rate.<br><br>Event report volume is related to billing, and the sampling rate should be configured appropriately based on the size of the business volume. |100% |
   ||Rule conditions |Configure rules to report events when a rule is satisfied. |None |
   


<span id="80190f8a"></span>
## Step 5: View leak events


1. In the upper left corner of the console, select **All features \> Event trends**.

2. In the filter area, click the **Android** operating system and other business\-related filter options.

3. In the report volume tab on the left, click the leak event name apmplus_activity_leak_monitor, select the dimension leak_activity, and then click the dimension name leak_activity in the dimension list.

4. View leak details for the leak_activity metric on the details page.


<span id="d15f4893"></span>
## Principle description

If the Android client implements the requirements with improper code, it can result in Activity leaks. Leaks involving Activity can affect a range of objects, especially various Views and their background Bitmaps, which occupy a large amount of memory and represent a significant proportion of memory leaks. Leak analysis supports detecting and reporting Activity leaks, and can also safeguard against memory leaks caused by Activity leaks by breaking the View's reference to the picture, thereby reducing leaked memory.

<span id="c9c34ed8"></span>
### Glossary


|Glossary |DescriptionS |
|---|---|
|**What is a memory leak?**  |In computing, a memory leak occurs when a program fails to release memory that is no longer in use due to negligence or error.<br><br>In Java, there are some allocated objects.<br><br><br>* These objects are reachable, that is, in a directed graph, there is a path from GC ROOT to each of them. \*\*<br><br>* These objects are no longer needed, that is, the program will not use them again in the future.<br><br><br>If objects meet both of these conditions, they can be identified as memory leaks in Java. Such objects are not reclaimed by the GC, yet they still occupy memory. |
|**How to detect if an Activity has leaked?**  |Once an Activity has executed onDestroy(), its lifecycle has ended and it should not be referenced by any object. The Activity that has executed onDestroy() should be reclaimed during the next GC cycle. If garbage collection is performed and the object is still not reclaimed, it is determined that the current Activity has a strong reference and has already leaked. |
|**How to determine whether GC has occurred?**  |Code can trigger GC programmatically; however, frequent GC is not beneficial for the smooth operation of the app and may cause lag. Supports configuring delayed detection of Activity leaks, allowing the operating system to trigger GC reclaim itself as much as possible, rather than manual triggering.<br><br>After the Activity's onDestroy event, create a WeakReference to a new Object(). If this new Object() is reclaimed, this is considered to trigger GC. |
|**How to determine whether an Activity has been reclaimed** |Use `WeakReference(T referent, ReferenceQueue<? super T> q)` to wrap the Activity. After the Activity is reclaimed by the garbage collector, the reference will be placed into the internal `ReferenceQueue`.<br><br>In other words, all references retrieved from the ReferenceQueue refer to objects that have already been successfully reclaimed. |
|**What is the fallback mechanism for memory leaks?**  |Some leaked objects have reached the end of their lifecycle, but strong references still exist, preventing the garbage collector (GC) from reclaiming them. By proactively breaking the trace from leaked objects to the GC ROOT through code, or releasing the referenced objects held by the leaked objects, these leaked objects can be reclaimed during the next garbage collection, freeing up memory space. This serves as the fallback mechanism for memory leaks. It is like an automatic floor\-cleaning robot that continuously helps you clean up trash in the room. |
|**Which objects does the fallback handling for memory leaks cover?**  |* Who uses more memory<br><br>* Who has a higher leak frequency<br><br>* After confirming the fallback mechanism, business logic should avoid accessing leaked objects as much as possible to prevent null pointer exceptions.<br><br><br>By using delayed processing for the background picture of the View tree and the picture in the ImageView, both of which are held by the leaked Activity, these images are set to null after the Activity leaks to prevent picture leaks.<br><br>Of course, a more aggressive approach would be to remove all child views from the RootView. However, due to the complexity of business logic, it is highly likely that further operations on the view tree may still occur after removal, which can result in a null pointer exception. |
