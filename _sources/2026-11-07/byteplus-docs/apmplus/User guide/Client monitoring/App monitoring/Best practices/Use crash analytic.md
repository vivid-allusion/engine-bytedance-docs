---
title: "Use crash analytic"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_crash_analytic"
---

This document describes the complete operational process required when an Android App needs to integrate App Monitoring and continuously monitor the day\-over\-day increase in crashes.

<span id="e048dbe6"></span>
## Step 1: Obtain the SDK


1. Add the Maven address in the `build.gradle` file at the project level.

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

   1. In the dependencies section of the project\-level `build.gradle` file, add the following code to integrate the plugin component that assists with instrumentation. `apm_insight_plugin` The same version is used both domestically and internationally.

      ```Java
      classpath "com.volcengine:apm_insight_plugin:1.4.2"
      ```
      

   2. In the dependencies section of the `build.gradle` file in the app module, add the following code and select one of the two versions below depending on whether your application is for the domestic market or overseas.

      * For domestic applications connecting to the cn version and reporting data to China, use the following dependencies:

         ```Java
         // Add domestic applications to dependencies
         implementation 'com.volcengine:apm_insight:1.5.6.cn'
         implementation 'com.volcengine:apm_insight_crash:1.5.9'
         ```
         

      * Integrate overseas applications with the oversea version, reporting to Johor, Malaysia. Use the following dependencies:

         ```Java
         // For overseas applications, add in dependencies
         implementation 'com.volcengine:apm_insight:1.5.7.oversea'
         implementation 'com.volcengine:apm_insight_crash:1.5.8.oversea'
         ```
         


<span id="be6b8059"></span>
## Step 2: Initialize the SDK and turn on Monitoring


1. In onCreate of Application, add the following code to initialize crash\-related features.

   ```Java
   MonitorCrash.Config config = MonitorCrash.Config.app({{AppId}})
                   .token({{AppToken}})// Setting the authentication token, which can be obtained from the platform application information; if there is a token error, data cannot be reported.
                 .build();
           MonitorCrash monitorCrash = MonitorCrash.init(ApplicationContext, config);
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to pass ApplicationContext as the context.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Parameters must not be null; otherwise, initialization will fail.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Initialize the returned MonitorCrash instance as the entry point for subsequent configuration.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Avoid calling the initialization method repeatedly, and perform a null pointer check on the object returned by init.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">aid can be obtained from the URL in the platform project browser.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the method to obtain AppID and AppToken, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken">How to query AppID and AppToken?</a>.   </div>
   

2. Start crash monitoring, begin collecting data.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please call the method to collect data only after the user has agreed to the privacy policy.   </div>
   

   ```Java
   // Start monitoring. If autoStart is set to false during initialization, monitoring will not be turned on automatically and you need to call the start method at the appropriate place in your code to turn on monitoring. If the autoStart parameter is not set during initialization or is set to true, monitoring will be turned on automatically and you do not need to call the start method.
           if (monitorCrash != null) {
               monitorCrash.start();
           }
   ```
   


<span id="6d2e7028"></span>
## Step 3: Verify data reporting

Crash reports are always sent at a 100% reporting rate and are not subject to sampling rate controls. You can perform the following actions to verify data reporting.


1. Add the following code, and wait for a Java crash to occur in the app.

   ```Java
   throw new RuntimeException("Monitor Exception"); // Crashes immediately upon execution. If the application crashes within 8 seconds after the application starts, it is considered a start crash and will be reported.
   ```
   

2. Restart the app. The SDK will immediately report any crashes that occurred during the previous launch. Then, view the logs of successfully reported crashes in the console.


<span id="a700f401"></span>
## Step 4: Create an alert task

You can create a crash alert task and set an appropriate alert strategy to help you continuously monitor the day\-over\-day increase in crashes.


1. Log in to [the Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. Click **App Monitoring** under the target application.

3. In the upper left corner of the console, select **All features \> Crash alert**.

4. On the **crash alert task** page, click **create alert task**.

5. On the **create alert task** page, complete the configuration as shown in the following example, then click **Save**.

   * Basic alert information

   * Create an alert strategy

   * Configure notification recipients


<span id="9c4255b5"></span>
## Step 5: View alert details

If the console is logged in, when a Lark group receives an alert notification, you can directly click **Details** in the message card to access the crash alert page.

If you are not logged in to the console and receive an alert notification, please log in and follow the steps below to view the alert details.


1. In the upper left corner of the console, select **All features \> Crash alert**.

2. On the **crash alert task** page, find the **task name** crash day\-over\-day, and click **alert detail** in the Actions column on the right.

3. On the **crash alert** page, view the alert distribution in the alert overview and view detailed alert content and other information in the alert list to help analyze crash issues.
