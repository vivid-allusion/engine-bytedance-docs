---
title: "Integrate the Android component monitoring SDK"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_component_monitoring_SDK"
---

If your product is itself an SDK and you want to monitor its stability or perform custom event tracking, you can integrate the relevant capabilities as described in this article. After integrating the SDK and verifying that data reporting is successful, you can use related features on the Application Performance Management Plus platform.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The Android Component Monitoring SDK currently supports use in applications in China and overseas. In China, direct access is used. For overseas use, you need to obtain the reporting domain name from sales for configuration.</div>


* <div data-tips="true" data-tips-type="warning">The SDK collects user information during initialization. Please ensure that user authorization has been obtained before collecting any information. Users must agree to the SDK privacy policy. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/The_SDK_privacy_policy">the SDK privacy policy</a>. No user information will be collected without authorization.</div>



<span id="ef7e5bca"></span>
## Introduction to features

Main monitoring capabilities provided by APMPlus SDK include:


* [Stability monitoring](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_component_monitoring_SDK#48b33fba)

* [Custom event tracking](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_component_monitoring_SDK#21d20632)

* [Log recovery](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_component_monitoring_SDK#2b5b4426)

* DID acquisition, PV statistics, and UV statistics


<span id="48b33fba"></span>
## Stability monitoring

Stability monitoring includes Java crashes, Native crashes, ANR, and custom exceptions.

<span id="24307d56"></span>
### Step 1: Integrate dependencies


1. Add the Maven repository URL in the project\-level `build.gradle` file.

   ```Java
   maven {
       url 'https://artifact.bytedance.com/repository/Volcengine/'
   }
   ```
   

2. Add the following code to the dependencies section of the `build.gradle` file in the component module.

   ```Java
   implementation "com.volcengine:apm_insight_crash:1.5.10"
   ```
   


<span id="76cd6138"></span>
### Step 2: Initialize the SDK

```Java
MonitorCrash.Config config = MonitorCrash.Config.sdk({{AppId}})
        .token({{AppToken}})// Data authentication token. Can be obtained from platform application information. If the token is incorrect, data cannot be reported.
        .versionCode(1) // Required SDK version number
        .versionName("1.0") // Required SDK version name
        .keywords("a.b.c", "d.e.b") // Set specific strings (such as package names) that may appear in the crash stack trace. If not set, no filtering is applied. Regular expressions are not supported. Effective for Java crashes and ANR.
        .soList("a.so", "b.so", "c.so") //Native crash monitoring: if not set, no reporting; regular expressions not supported
        // Optional. You can set a custom did; if not set, the internal default will be used.
        //.dynamicParams(new MonitorCrash.Config.IDynamicParams() {
        //    @Override
        //    public String getDid() { // If the return value is empty, the internal default did will be used. }
        //        return null;
        //    }
        //
        //    @Override
        //    public String getUserId() {
        //        return null;
        //    }
        //})
        // Optional: add business-specific custom data to be displayed on the crash details page
        //.customData(crashType -> {
        //    HashMap<String, String> map = new HashMap<>();
        //    map.put("app_custom", "app_value");
        //    return map;
        //})
        //.pageViewTags(map) // Set PV custom dimension
        .build();
MonitorCrash monitorCrash = MonitorCrash.initSDK(this, config);
```


<span id="7f88d099"></span>
### Step 3: Verify data

For an introduction to the crash feature, refer to [crash analytic](https://docs.byteplus.com/en/docs/apmplus/Crash_analyses).

<span id="21d20632"></span>
## Custom event tracking

<span id="a03167b4"></span>
### Step 1: Integrate dependencies


1. Add the Maven address in the project\-level `build.gradle`.

   ```Java
   maven {
       url 'https://artifact.bytedance.com/repository/Volcengine/'
   }
   ```
   

2. In the dependencies section of the `build.gradle` file of the component module, add the following code.

   ```Java
   implementation "com.volcengine:apm_insight_sdk:1.1.8"
   ```
   


<span id="7b9e6fc7"></span>
### Step 2: Initialize the SDK

```Java
SDKEventInitConfig.Builder builder = SDKEventInitConfig.builder()
        .aid(sSDKAid)//Platform aid
        .token(sToken)// Platform token
        .context(getApplicationContext())//context
        .channel("channel")//SDK channel
        .appVersion("1.0.0")//SDK version number
        .updateVersionCode("10001")// Minor version number of the SDK
        .hostAid("APM_DEMO")// Unique identifier of the host app
        .debugMode(true)//In debug mode, test log will be printed. Set the production environment to release
        .setDynamicParams(new SDKEventIDynamicParams() {
            @Override
            public String getDid() {
                //Required. Returns the device identifier did, or you can use your own business-specific did.
                return AppLog.getInstance(sSDKAid).getDid();
            }

            @Override
            public String getUserId() {
                //return user id; if none, can be empty
                return "";
            }
        });
SDKEventManager.init(builder.build());
```


<span id="64f958f7"></span>
### Step 3: Report an event

When integrating APMPlus into the SDK, you can configure event reporting in your code as shown in the following example. Alternatively, you can add events on the platform, configure the key and value, and set sampling. Once the client reports the event, you can view it on the platform.

Reporting example:

```Java
HashMap<String, String> dimension = new HashMap<>();
//Dimension value
dimension.put("key1", "value1");
dimension.put("key2", "value2");
HashMap<String, Double> metric = new HashMap<>();
//Metric value Metric value must be a number
metric.put("metric1", (double) 10);
metric.put("metric2", 8.8);
SDKEventManager.getSDKMonitor(aid).monitorEvent("event_test", dimension, metric);
```


Interface description:

```Java
/**
Event reporting
 *
 *@paramserviceName event name
 *@paramdimension   Enumerable key-value pair that identifies a dimension
 *@parammetric      Non-enumerable key-value pair that identifies a metric.
 */
public void monitorEvent(final String serviceName, final Map<String, String> dimension, final Map<String, Double> metric)

/**
Reporting events
 *
 *@paramserviceName event name
 *@paramdimension   Enumerable key-value pairs that identify a dimension
 *@parammetric      Non-enumerable key-value pairs, used to identify a metric
 *@paramlogExtra    User-defined data that is not included in reports and can be viewed in individual queries of the original log.
 */
public void monitorEvent(final String serviceName, final Map<String, String> dimension, final Map<String, Double> metric,final JSONObject logExtra) 
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Event reporting only supports the interfaces mentioned above. Do not call other interfaces.</div>


<span id="7b6b90b3"></span>
### Step 4: Troubleshoot issues

If no event is displayed, provide a troubleshooting log. Initialize the configuration to debug mode, and provide all logs filtered by the Logcat log keyword `ApmInsight:` to R&D personnel for analysis and troubleshooting.

```Plain
//代表event1 采样没有命中
2021-04-11 21:28:01.317 13535-13592/com.example.apm.insight.demo D/ApmInsight: SDK event:event1 simple:false
//代表event2 采样命中
2021-04-11 21:28:01.771 13535-13592/com.example.apm.insight.demo D/ApmInsight: SDK event:event2 simple:true
```


<span id="c2e928b7"></span>
### Step 5: Verify data

For an introduction to the event feature, refer to [event analytic](https://docs.byteplus.com/en/docs/apmplus/Event_analytics).

You can also process event data through a custom dashboard. For detailed configuration, refer to [Custom Dashboard](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app).

<span id="2b5b4426"></span>
## Log recoveries

Supports SDK\-level log recovery and proactive log reporting, as well as log reporting during a crash, to effectively troubleshoot single\-point issues.

<span id="37a15b2f"></span>
### Step 1: Integrate dependencies


1. Add the Maven address in the project\-level `build.gradle`.

   ```Java
   maven {
       url 'https://artifact.bytedance.com/repository/Volcengine/'
   }
   ```
   

2. Add the following code to the dependencies section of the `build.gradle` file in the component module.

   ```CSS
   implementation "com.volcengine:apm_insight_cloud:0.0.3.sdk"
   ```
   


<span id="8d3651be"></span>
### Step 2: Initialize SDK

```TypeScript
// Initialize the Vlog log instance.
VLogConfig config = new VLogConfig.Builder(getApplicationContext())
        .setLogDirPath(this.getFilesDir() + "/Vlog/" + sSDKAid)//sSDKAid is the aid applied for by the platform
        .setMaxDirSize(5 * 1024 * 1024)  // max directory size
        .setSubProcessMaxDirSizeRatio(0.1f) // max directory size of each instance for sub process
        .setLogFileExpDays(14) // log file expired days
        .build();
VLog.createInstance(config, sSDKAid);      
 
// Initialize recovery component
SDKCloudInitConfig.Builder builder = SDKCloudInitConfig.builder();
builder.aid(sSDKAid);// Platform's aid
builder.token(sToken);// Platform token
builder.context(getApplicationContext());//context
builder.debugMode(true);//During the testing phase, setting to debug mode enables logging for troubleshooting. Online configuration is set to false
builder.channel("channel");// sdk channel
builder.updateVersionCode("1.1.1");// SDK version number
builder.setDynamicParams(new SDKIDynamicParams() {
    @Override
    public String getDid() {
        // Required. The device's unique identifier: did. The current implementation generates an internal default did, but it can also return a did defined by the business logic.
        return AppLog.getInstance(sSDKAid).getDid();
    }

    @Override
    public String getUserId() {
        // Unique user identifier (userid), can be null
        return "";
    }
});
// Timing for fetching the recovery command from the platform configuration: The recovery component fetches the command once during its default initialization.
SDKCloudManager.getInstance().init(builder.build());       
        
//logging
ILog iLog = VLog.getInstance(aid);
iLog.i("sdk_cloud", "test i");
iLog.e("sdk_cloud", "test e");

// Optional: In addition to supporting log recovery, active reporting of Vlog logs is also supported in cases of user feedback. Proactively reported logs can be queried on the platform by navigating to single point tracing -> custom file, and entering did in the custom file section.
//The Vlog log for the hour before reporting. Caution: Reporting logs will consume the platform event quota. Use appropriately.
SDKCloudManager.getSDKCloud(sSDKAid).uploadVlog(System.currentTimeMillis() - 60  * 60 * 1000, System.currentTimeMillis());
```


Method description:

```TypeScript
SDKCloud.java
/**
Active Vlog reporting
 *
 *@paramstart start time milliseconds
 *@paramend: end time (milliseconds)
 */
public void uploadVlog(long start, long end) {
    AlogActiveUploadManager.upLoadVlog(start, end, null, initConfig.getAid());
}
```


<span id="7f2e4527"></span>
### Step 3: Verify data

Introduction to the log recovery feature, refer to [recovery](https://docs.byteplus.com/en/docs/apmplus/Recovery).
