---
title: "Use new H5 monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_new_H5_monitoring"
---

This article uses Android applications as an example to introduce the detailed steps for integrating the SDK and using the New H5 monitor.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Subsequent updates will be made only based on the features of the New H5 monitor. Businesses that have already integrated the H5 monitor may delete the old version and integrate the New H5 monitor.</div>


* <div data-tips="true" data-tips-type="warning">Alignment of main monitoring capabilities between New H5 monitor and WebPro endpoint More comprehensive capabilities require integration with WebPro\-side monitoring.</div>



<span id="ed8ab47b"></span>
## Step 1: Delete H5 monitor

Subsequent platform updates will be made only based on the New H5 monitor feature. Sourcemap management in H5 monitor and file management will be discontinued. For businesses that have already integrated H5 monitor, it is recommended to follow the steps below: delete the old H5 monitor, and then integrate the New H5 monitor.


1. Delete the content about turning on webview monitoring during SDK initialization.

   ```Java
   //Control whether to enable WebView monitoring
   builder.enableWebViewMonitor(true);
   ```
   

2. Delete the content of the WebView configuration

   ```Java
   // Set the WebView's WebChromeClient as follows, or inherit from WebViewMonitorWebChromeClient
   webView.setWebChromeClient( new WebViewMonitorWebChromeClient());
   // Set the WebViewClient for webView as follows, or extend WebViewMonitorWebViewClient
   webView.setWebViewClient(new WebViewMonitorWebViewClient());
   //You need to call the following function when WebView loads a URL
   WebViewMonitorHelper.getInstance().onLoadUrl(webView, url);
   ```
   


<span id="863af114"></span>
## Step 2: Integrate the SDK


1. Add the Maven address in the project\-level `build.gradle` file.

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

   1. In the dependencies section of the project\-level `build.gradle` file, add the following code to integrate the plugin component for assisting with instrumentation. `apm_insight_plugin` uses the same version both domestically and internationally.

      ```Java
      classpath "com.volcengine:apm_insight_plugin:1.4.2"
      ```
      

   2. In the dependencies section of the `build.gradle` file in the app module, add the following code, and select one of the two versions below depending on whether your application is for domestic or overseas use.

      * For domestic applications, connect to the cn version, report to China, and use the following dependencies:

         ```Java
         // For domestic applications, add to dependencies
         implementation 'com.volcengine:apm_insight:1.5.6.cn'
         implementation 'com.volcengine:apm_insight_crash:1.5.9'
         ```
         

      * Overseas applications integrate with the oversea version, report to Johor, Malaysia, and use the following dependencies:

         ```Java
         // For overseas applications, add to dependencies
         implementation 'com.volcengine:apm_insight:1.5.7.oversea'
         implementation 'com.volcengine:apm_insight_crash:1.5.8.oversea'
         ```
         


<span id="ff0f4f49"></span>
## Step 3: Initialize SDK and turn on new H5 monitor


1. In the onCreate method of Application, add the following code to initialize performance\-related features.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please add the code for initializing performance\-related features in the main thread.   </div>
   

   ```Java
   //Must be placed in the onCreate method of Application; it will register a lifecycle listener and does not involve data collection or privacy compliance issues.
   ApmInsight.getInstance().init(application);
   // Initialize custom log and configure the maximum disk usage for custom log. The typical internal configuration is 20, which means the maximum disk usage is 20 MB. This API has been available since version 1.4.1.
   VLog.init(this,20);
   ```
   

2. Start the New H5 monitor and begin collecting data.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Call the method to collect data only after the user has agreed to the privacy policy.   </div>
   

   ```Java
   //Call after agreeing to privacy compliance to start performance component monitoring
   ApmInsightInitConfig.Builder builder = ApmInsightInitConfig.builder();
   //Control whether to enable the New H5 monitor
   builder.enableHybridMonitor(true);
   ApmInsight.getInstance().start(builder.build());
   ```
   

3. Configure WebView monitoring.

   ```Java
   webView.setWebChromeClient(new WebChromeClient(){
       @Override
       public void onProgressChanged(WebView view, int newProgress) {
           super.onProgressChanged(view, newProgress);
           //Call the following function to control the loading of the New H5 monitor JS
           HybridMonitorManager.getInstance().onProgressChanged(view,newProgress);
       }
   });
   
   //You must call the following function before loading a url in WebView
   HybridMonitorManager.getInstance().onLoadUrl(webView,url);
   webView.loadUrl(url);
   ```
   


<span id="689bdf1e"></span>
## Step 4: Complete SDK setting

On the **SDK setting** page, modify the **New H5 monitor** module parameter **New H5 monitor sampling rate**. The default sampling rate is 20%. For specific operations, refer to [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

<span id="19b10049"></span>
## Step 5: Use New H5 monitor


* On the **H5 alert** page, create an alert task, and configure the alert strategy with the alert type and metric of the New H5 monitor. For details, refer to [Create an alert task](https://docs.byteplus.com/en/docs/apmplus/alert_management#.5bSp5rqD5oql6K2m).

   When an alert notification is received, view the monitoring data of the page on the New H5 monitor feature page.

* On the **custom dashboard** page, configure the chart types you want to monitor and the metrics for the New H5 monitor. For details, refer to [create dashboard](https://docs.byteplus.com/en/docs/apmplus/custom_dashboard_app#66d5bf1c).

   Regularly view dashboard data and pay attention to changes in the New H5 monitor metrics.
