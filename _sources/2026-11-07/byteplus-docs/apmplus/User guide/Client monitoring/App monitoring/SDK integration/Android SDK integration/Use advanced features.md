---
title: "Use advanced features"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features_Android"
---

In addition to common features such as crash analytic, startup analytic, and lag analytic, the SDK also supports several enhanced features. You can select whether to integrate these features based on your business needs.

<span id="eb14c2ce"></span>
## **Custom log and APMPlus log**

There are three use cases for custom logs: crash log reporting, log recovery, and proactive reporting.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The maximum string limit for custom logs is 4\*1024 characters.</div>


<span id="c488dd70"></span>
### Automatic reporting


1. Enable custom log when initializing the SDK.

   ```Java
   // Enable the custom log retrieval capability
   builder.enableLogRecovery(true);
   // Enable APMPlus log recording, which can be retrieved later.
   builder.enableAPMPlusLocalLog(true);
   ApmInsight.getInstance().init(this, builder.build());
   / Initialize custom logs and configure the maximum disk space occupied by custom logs. Internally, it is usually configured as 20, which means a maximum of 20MB disk space can be occupied. This feature has been available since version 1.4.1.
   VLog.init(this,20);
   ```
   

2. Actively report Vlog log files.

   ```Java
   // Example: Upload vlog logs from 10 minutes before the current time.
   ApmInsightAgent.uploadVlog(System.currentTimeMillis() - 1000 * 60 * 10, System.currentTimeMillis());
   
   /**
    * Vlog log active reporting
    *
    * @param Start time (milliseconds)
    * @param End time (milliseconds)
    */
   public static void uploadVlog(long start, long end) {
   }
   ```
   

3. Actively report APMPlus log.

   ```Java
   // Example: Upload APMPlus logs from 10 minutes before the current time.
   ApmInsightAgent.uploadAPMPlusLog(System.currentTimeMillis() - 1000 * 60 * 10, System.currentTimeMillis()，null);
   
   /**
    * APMPlus log active reporting
    *
    * @param start    Start time (milliseconds)
    * @param end      End time (milliseconds)
    * @param Callback for success or failure
    */
   public static void uploadAPMPlusLog(long start, long end, IALogActiveUploadCallback callback) {
   }
   
   /**
    * APMPlus logs and business Vlog logs active reporting
    *
    * @param start    Milliseconds
    * @param end      Milliseconds
    * @param callback Callback for success or failure
    */
   public static void uploadAPMPlusAndVlog(long start, long end, IALogActiveUploadCallback callback) {
   }
   ```
   

   The log file is relatively large. Each report consumes approximately 200 events. Log files are rotated based on size, with each file not exceeding 2 MB.

4. On the **custom file** page, query log files by DID or User ID.


<span id="87114e63"></span>
### Actively report when a crash occurs


1. Enable the custom log when initializing the SDK.

   ```Java
   // Enable the custom log retrieval capability
   builder.enableLogRecovery(true);
   // Enable APMPlus log collection
   builder.enableAPMPlusLocalLog(true);
   ApmInsight.getInstance().init(this, builder.build());
   // Initialize custom logs and configure the maximum disk space occupied by custom logs. Internally, it is usually configured as 20, which means a maximum of 20MB disk space can be occupied. This feature has been available since version 1.4.1.
   VLog.init(this,20);
   ```
   

2. In the crash analytic section of the **SDK setting** page, configure whether to upload custom log.

3. On the **crash details** page, under **custom log**, view the logs printed by the Vlog class.


<span id="1dc51677"></span>
### Log recovery

When users encounter issues that require log investigation, problems are diagnosed by recovering logs printed by custom log Vlog on the client side.


1. When initializing the SDK, enable the custom log.

   ```Java
   // Enable the custom log retrieval capability
   builder.enableLogRecovery(true);
   // Enable APMPlus log collection
   builder.enableAPMPlusLocalLog(true);
   ApmInsight.getInstance().init(this, builder.build());
   // Initialize custom logs and configure the maximum disk space occupied by custom logs. Internally, it is usually configured as 20, which means a maximum of 20MB disk space can be occupied. This feature has been available since version 1.4.1.
   VLog.init(this,20);
   ```
   

2. Record custom logs through the API.

   ```Java
   // com.apm.insight.VLog;
   VLog.v(String tag, String msg);
   VLog.d(String tag, String msg);
   VLog.i(String tag, String msg);
   VLog.w(String tag, String msg);
   VLog.e(String tag, String msg);
   // You can also set the effective log level through the interface.
   VLog.changeLevel(com.apm.insight.LogLevel.WARN);
   ```
   

3. Create a task on the **log recovery** page, enter a DID or UID to recover the specified user's custom log for troubleshooting.

   * Configuration during UID initialization

      ```Java
      @Override
          public String getUserId() {
               // Optional. The unique identifier of the user. Users can customize the user_id to associate platform data with their own users. getUserId is a parameter of the callback class and can be set after initialization.
               return "userid";
          }
      ```
      

   * The configuration during DID initialization

      ```Java
      @Override
          public String getDid() {
              // Optional for versions 1.4.0 and above, required for other versions. The unique identifier of the device. If you rely on AppLog, you can get it through AppLog.getDid(). You can also generate it yourself.
              return null;
          }
      ```
      

      If DID returns null, log recovery can be performed using the UID configuration.


<span id="f076a974"></span>
## Custom recovery

Recovery supports custom recovery. Users enter custom recovery parameters, and the desired recovery results can be returned based on these parameters.

```Java
// Optional, custom retrieval settings
ApmInsightAgent.setRecoveryTemplate(new ITemplateConsumer() {
    @Override
    public CustomResult handleTemplateMessage(JSONObject template) {
        // template is the 【Custom retrieval parameters】 configured on the platform.
        if (template != null) {
            String type = template.optString("type");
            if (!TextUtils.isEmpty(type)) {
                if (type.equals("type_one")) {
                    // Return the retrieval results of type_one
                    HashMap<String, String> result = new HashMap<>();
                    result.put("result", "File retrieval succeeded");
                    // The result will be directly displayed on the platform, and the file can be downloaded on the platform.
                    CustomResult customResult = new CustomResult(result, application.getFilesDir());
                    // The returned retrieval results
                    return customResult;
                } else if (type.equals("type_two")) {
                   // Return the retrieval results of type_two
                    return null;
                }
            }
        }
        return null;
    }
});
```


<span id="e8ba34e4"></span>
## **Custom crash data**

A lot of data is reported when a crash occurs. If users want to report some custom data together with the crash data during a crash, they can refer to the example code below.

<span id="cf3e51df"></span>
### **Other crash fields**

Configure other crash fields, including channel, version number, and all custom fields.

```Java
public Config config()
```


<span id="62c35163"></span>
### Custom dimensions

Custom dimensions of the crash component:

```Java
public MonitorCrash addTags(String key, String value)
```


Custom dimensions for the performance component: Reported tags can be queried in log queries or raw log files.

```Java
// Example
ApmInsightAgent.addPerfTag("tag_test","tag_1");
/**
 * Add a tag to performance data
 * @param key
 * @param value
 */
public static void addPerfTag(@NonNull String key, @NonNull String value) {
}
/**
 * Remove a tag from performance data
 * @param key
 * @param value
 */
public static void removePerfTag(@NonNull String key, @Nullable String value) {
}
```


<span id="ccc8f679"></span>
### Custom error

The message and type parameters can be any string (not excessively long) and can be used to filter.

```Java
/**
 * @param message message（On - site data display)
 * @param Type (Display of list error types)
 * @param throwable
 */
public void reportCustomErr(String message, String type, Throwable throwable)

/**
 * @param message message (On - site data display)
 * @param type Type (Display of list error types)
 * @param throwable
 * @param data Custom data (On - site data display)
 */
public void reportCustomErr(String message, String type, Throwable throwable, @Nullable Map<String, String> data)
```


For example:

```Java
MonitorCrash crash = The MonitorCrash instance returned by initialization
crash.reportCustomErr("test err", "type1", new RuntimeException());
```


<span id="fe664d24"></span>
## Start custom event tracking

<span id="1ed016c9"></span>
### Set the maximum startup time threshold

```Java
builder.setMaxLaunchTime();
// Set the maximum reporting threshold for the startup duration, in milliseconds. The internal default value is 15 seconds: APP_LAUNCH_MAX_LIMIT_MS = 15 * 1000L
```


<span id="914e033e"></span>
### Custom start nodes

Start Monitoring supports custom event tracking; methods must be used in pairs. Add the following code between Application's onCreate and the first Activity's onResume to configure custom event tracking.

```Java
LaunchTrace.startSpan("initData");
LaunchTrace.endSpan("initData");
```


After adding the above code, you can view the duration of custom event logging in the **Startup Node Duration** section of **Startup Analysis**.

<span id="a1a19318"></span>
### Customize start and end points

By default, startup monitoring is implemented using instrumentation code, with the end point being the onResume method of the first page. The following method allows you to customize the end point.

```Plain
// Initialize and set the custom reporting for startup monitoring, indicating that the reportLaunchEnd() method is used to define the end point of startup.
LaunchTrace.customLaunchEnd(true);
LaunchTrace.customLaunchEnd(true);
// Report the end time point of custom startup monitoring, representing the end point of startup.
LaunchTrace.reportLaunchEnd();
```


<span id="c771dabf"></span>
## Trace monitoring

After integrating with APMPlus server\-side monitoring, configure the client as follows to enable trace monitoring. For more information, refer to [end-to-end monitoring](https://docs.byteplus.com/en/docs/apmplus/Full_trace_monitoring).

```Plain
ApmInsightInitConfig.Builder builder = ApmInsightInitConfig.builder();
// Enable the full - link monitoring capability. It will inject a trace_id into the request and report it to the server in network monitoring. Through the trace_id, it can be connected with the backend data of the APMPlus server - side monitoring to achieve the goal of full - link monitoring.
builder.enableNetTrace(true);
ApmInsight.getInstance().start(builder.build());
```


<span id="9f182e42"></span>
## Register crash callback

Registering a crash callback allows you to invoke the callback when an exception occurs and record key information at the time of the exception.

```Java
MonitorCrash Instance usage
 /**
 * Callback when an exception occurs, supporting callbacks for Java, Launch, Native, and ANR exceptions.
 * It is convenient for business function expansion.
 *
 * @param crashCallback Callback
 * @param type Crash type, does not support {@link CrashType#CUSTOM_JAVA}
 */
 public void registerCrashCallback(ICrashCallback var1, CrashType var2)

 /**
 * Remove the Crash callback
 *
 * @param crashCallback Callback
 * @param type Crash type, does not support {@link CrashType#CUSTOM_JAVA}
 */
 public void unregisterCrashCallback(ICrashCallback var1, CrashType var2)
```
