---
title: "Crash not reported"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Crash_not_reported"
---

If app crashes are not reported, please first confirm whether the service has not been activated or the event quota has been exhausted. After excluding these two situations, you can troubleshoot the issue using the following methods.

<span id=".5pa55byP5LiA77ya6YCa6L-H5pel5b-X5o6S5p-l"></span>
## Method 1: Troubleshoot through logs


1. Before initializing MonitorCrash, enable the log switch, call Npth.getConfigManager().setDebugMode(true), and filter npth's logs.

2. After enabling the log switch, the following configuration update logs will appear.

   ```sql
   2022-09-22 21:16:20.756 5319-5367/com.example.crash.test I/npth: update config 187277 : {"crash_module":{"alog_crash_before_time":"60","switcher":1,"upload_alog":"1"}}
   2022-09-22 21:16:20.757 5319-5367/com.example.crash.test I/npth: after update aid 187277
   ```
   

   If configuration update logs are not printed, please check the following possible causes:

   * If there are no logs corresponding to aid, check whether the initialization code and parameters are correct.

   * Is the network functioning properly?

3. When a Java crash occurs, the following captured logs will be printed.

   ```sql
   I/npth: [uncaughtException] mLaunchCrashDisposer
   ```
   

   If capture logs are not printed, please check the following possible causes:

   * Determine from the Logcat logs whether a crash has actually occurred.

      * If there are error logs containing the FATAL keyword, then a crash has indeed occurred.

      * If there are no error logs containing the FATAL keyword, check whether a global catch mechanism is in place.

   * Check whether the UncaughtExceptionHandler has been registered correctly.

      Via the following sample code, traverse and print all UncaughtExceptionHandlers within the application. The target handler refers to the one whose APM package name is com.apm.insight.

      * If multiple handlers exist but the one with the package name com.apm.insight is not printed in the logs, it indicates that the APM handler has failed to register properly. It is recommended to initialize the APM SDK later.

      * Even when the handler is registered successfully, individual monitoring SDKs may fail to forward crashes. Thus, initializing the APM SDK later is still advisable. When troubleshooting unreported crashes, you can comment out the corresponding SDK for verification.

   ```sql
   Thread.UncaughtExceptionHandler handler = Thread.getDefaultUncaughtExceptionHandler();
   boolean next = false;
   do {
       System.out.println("UncaughtExceptionHandler " + handler.getClass().getName());
       next = false;
       Field[] fields = handler.getClass().getDeclaredFields();
       for (Field field : fields) {
           field.setAccessible(true);
           try {
               Object object = field.get(handler);
               if (object instanceof Thread.UncaughtExceptionHandler) {
                   handler = (Thread.UncaughtExceptionHandler)object;
                   next = true;
                   break;
               }
           } catch (Exception e) {
               e.printStackTrace();
           }
       }
   } while (next);
   ```
   

4. When a Native crash occurs, the following captured logs will be printed.

   ```sql
   2022-09-22 21:33:05.023 8847-8847/com.example.crash.test E/npth: Native crash was detected!
   2022-09-22 21:33:05.087 8847-8882/com.example.crash.test I/npth: [onNativeCrash] enter
   ```
   

   If captured logs are not printed, please check the following possible causes:

   * Check whether the so files are correctly packaged in the APK, including libapminsighta.so and libapminsightb.so. If there is any abnormality, please repackage.

5. No ANR logs have been captured yet. Once captured, they will be reported immediately.

   ```sql
   I/npth: uploadFromFile with allData [{"header":{"aid":"187277","update_version_code":1,"version_code":1,"app_version":"1.0","channel":"app_channel","device_id":"7550965448758202369","os":"Android","single_upload":0},"custom":{"app_custom":"app_value"},"filters":{"app_tag":"app_value"},"line_num":[{"start":0,"end":34}]},{"header":{"aid":"239017","update_version_code":123,"version_code":123,"app_version":"1.2.3","channel":"sdk_channel","package":["com.bytedance.testsdk1","com.example.crash.test"],"device_id":"7550965448758202369","os":"Android","so_list":["testsdk1.so"],"single_upload":0},"custom":{"sdk1_custom":"sdk1_value"},"filters":{"sdk1_tag":"sdk1_value"},"line_num":[{"start":14,"end":15},{"start":17,"end":21}]},{"header":{"aid":"1003","update_version_code":1,"version_code":1,"app_version":"1.1.1","package":["com.bytedance.testsdk3"],"device_id":"7550965448758202369","user_id":"1003","os":"Android","so_list":["testsdk3.so"],"single_upload":0},"custom":{"sdk3_custom":"sdk3_value"},"filters":{"sdk3_tag":"sdk3_value"},"line_num":[{"start":12,"end":14}]}]
   ```
   

   The logs uploaded for Java and native crashes are consistent. Please troubleshoot the following possible causes:

   * Check whether allData contains aid. If not, please analyze whether the stack matches the package name passed in during initialization.

   * Check the network.


<span id=".5pa55byP5LqM77ya6YCa6L-H5bSp5rqD5Lqn54mp5o6S5p-l"></span>
## Method 2: Troubleshoot using crash artifacts

After the crash is reported successfully, crash\-related artifacts will be deleted. Therefore, you need to obtain and inspect the crash artifacts after the crash occurs but before the report is successful.


1. Obtain the crash\-related artifacts collected in the data/data//files/apminsight directory on the device.

2. CrashLogJava saves Java crashes, Java start crashes, ANR, and other exceptions, while CrashLogNative saves native crashes.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bcbaffb1ecc5ec0f342491451dc88244.png) </span>

   * CrashLogNative has not been generated. Check whether initialization was successful.

   * Crash path is empty. Check whether initialization was successful. Among them, ANR can be used for network disconnection testing.

   * all_data.json does not exist. Check whether there is a mismatch in the crash stack or a problem with the configuration file.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6c0c9935b1648ee2fd71938564e55a0.png) </span>

3. The restart file has not been deleted.

   * Check the network.

   * Check whether the .so files are correctly packaged in the APK, including libapminsighta.so and libapminsightb.so.


<span id=".5pa55byP5LiJ77ya6YCa6L-H5oqT5YyF5o6S5p-l"></span>
## Method 3: Troubleshooting by packet capture


1. HTTPS domain name configuration (or simply set an HTTP domain name).

   ```sql
   android:networkSecurityConfig="@xml/network_security_config"
   配置增加BytePlus域名
   <domain includeSubdomains="true">https://apmplus.volces.com</domain>
   ```
   

2. Upload interface.

   
   |**Interfaces** |**The meaning** |
   |---|---|
   |/monitor/collect/c/crash |Java crashes, ANRs, Dart exceptions |
   |/monitor/collect/c/exception |Custom exception data reports |
   |/monitor/collect/c/native_bin_crash |Native crash reporting |
   |monitor/collect/c/cloudcontrol/file |Files uploaded via Alog |
   |/settings/get |Settings: Pull configuration |
   |/monitor/collect/c/exception/dump_collection |Start the crash reporting process |
   

3. The corresponding packet has been captured, but the platform still does not display it.

   * Check whether the initialization token is correct. For more information, refer to [Android SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application).

   * Check whether the domain name configuration is correct.


<span id=".5pa55byP5Zub77ya6YCa6L-H5rWL6K-V5bel5YW35o6S5p-l"></span>
## Method 4: Troubleshoot using testing tools

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_356557ae812afbb3500c257f3d66bb17.zip" name="test-release.zip">test-release.zip</Attachment>



1. After extracting the files, import locally by copying the AAR file to the libs directory of the app module, and then add it to dependencies in the app's build.gradle file.

   ```sql
   implementation files('libs/test-release.aar')
   ```
   

2. Compiling the APK will add a test entry. Click **test entry**.

3. Enter the test page, and then select the test items.
