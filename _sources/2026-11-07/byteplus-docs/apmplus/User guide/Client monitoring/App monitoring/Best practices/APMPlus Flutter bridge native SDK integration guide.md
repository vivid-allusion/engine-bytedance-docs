---
title: "APMPlus Flutter bridge native SDK integration guide"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/APMPlus_Flutter_bridge_native_SDK_integration_guide"
---

This article introduces how to use the APMPlus Android or iOS native SDK to report and monitor data related to Flutter applications, such as custom error, custom event, custom log, and many other monitoring data.

<span id="rkqULsH4"></span>
## Background Information

APMPlus officially no longer provides a Flutter SDK. To facilitate unified calls on the Flutter side, developers have designed the `APMPlusBridge` class, which encapsulates all details of native platform communication and allows monitoring data to be reported via Flutter\-to\-Native bridging.


* The complete code for `APMPlusBridge.dart` is as follows:


```Dart
import 'dart:async';
import 'package:flutter/services.dart';

// APMPlus log level
enum APMLogLevel {
  debug,
  info,
  warn,
  error,
}

// Custom error severity level
enum APMErrorSeverity {
  fatal,
  error,
  warn,
  info,
}

// APMPlus Flutter bridge core class
class APMPlusBridge {
  static const MethodChannel _channel = MethodChannel('apmplus_flutter_bridge');

  // Initialize native APMPlus SDK
  //
  // [config] must contain both 'appID' and 'appToken'; other parameters are optional depending on the platform.
  // The required parameters for Android and iOS are different. Please refer to the integration documentation for each platform.
  //
  // Example:
  // {
  //   // --- Common parameters ---
  //   'appID': 'YOUR_APP_ID', // Replace with your App ID
  //   'appToken': 'YOUR_APP_TOKEN', // Replace with your App Token
  //   'channel': 'App Store',
  //   'enableDebug': true, // Debug mode, be sure to set to false in the production environment
  //
  //   // --- Android-specific parameters ---
  //   'apm_insight_plugin_enable': true, // Whether to enable the instrumentation plugin
  //
  //   // --- iOS-specific parameters ---
  //   // (if any)
  // }
  static Future<void> initialize(Map<String, dynamic> config) async {
    try {
      await _channel.invokeMethod('initialize', config);
    } on PlatformException catch (e) {
      print("Failed to initialize APMPlus: '${e.message}'.");
    }
  }

  // Set user ID
  //
  // [userId] Unique identifier for the user
  static Future<void> setUserID(String userId) async {
    try {
      await _channel.invokeMethod('setUserID', {'userId': userId});
    } on PlatformException catch (e) {
      print("Failed to set user ID: '${e.message}'.");
    }
  }

  // Report custom error
  //
  // [type] Error type/name, such as `payment_error`
  // [message] Error message
  // [stack] Error stack trace information
  // [severity] Error severity level
  // [tags] Dimension tags for classification and filtering
  // [extras] Additional information for troubleshooting
  static Future<void> reportCustomError({
    required String type,
    required String message,
    String? stack,
    APMErrorSeverity severity = APMErrorSeverity.error,
    Map<String, String>? tags,
    Map<String, dynamic>? extras,
  }) async {
    final Map<String, dynamic> params = {
      'type': type,
      'message': message,
      'stack': stack ?? '',
      'severity': severity.toString().split('.').last,
      'tags': tags ?? {},
      'extras': extras ?? {},
    };
    try {
      await _channel.invokeMethod('reportCustomError', params);
    } on PlatformException catch (e) {
      print("Failed to report custom error: '${e.message}'.");
    }
  }

  // Report custom event
  //
  // [eventName] Event name
  // [attributes] Event dimension attributes (enumerable)
  // [metrics] Event metrics (non-enumerable numeric values)
  static Future<void> reportCustomEvent({
    required String eventName,
    Map<String, String>? attributes,
    Map<String, double>? metrics,
  }) async {
    final Map<String, dynamic> params = {
      'eventName': eventName,
      'attributes': attributes ?? {},
      'metrics': metrics ?? {},
    };
    try {
      await _channel.invokeMethod('reportCustomEvent', params);
    } on PlatformException catch (e) {
      print("Failed to report custom event: '${e.message}'.");
    }
  }

  // Record custom log (Alog/VLog)
  //
  // [level] Log level
  // [tag] Log tag
  // [message] Log content
  static Future<void> log({
    required APMLogLevel level,
    required String tag,
    required String message,
  }) async {
    final Map<String, dynamic> params = {
      'level': level.toString().split('.').last,
      'tag': tag,
      'message': message,
    };
    try {
      await _channel.invokeMethod('log', params);
    } on PlatformException catch (e) {
      print("Failed to log: '${e.message}'.");
    }
  }
}
```



* The following is a sample Flutter call:


```Dart
void main() {
  runApp(MyApp());

  // Initialize APMPlus when the application starts
  _initAPMPlus();

  // Example: Report a custom error
  APMPlusBridge.reportCustomError(
    type: 'FlutterLoginError',
    message: 'User failed to login with error code 500',
    stack: '...', // You can pass in stack trace information captured by try-catch
    severity: APMErrorSeverity.fatal,
    tags: {'login_method': 'email'},
    extras: {'user_email': 'test@example.com'},
  );

  // Example: Report a custom event
  APMPlusBridge.reportCustomEvent(
    eventName: 'addToCart',
    attributes: {'item_category': 'electronics'},
    metrics: {'item_price': 1999.99},
  );

  // Example: Record a log
  APMPlusBridge.log(
    level: APMLogLevel.info,
    tag: 'ShoppingCart',
    message: 'Item successfully added to cart.',
  );
}

void _initAPMPlus() {
  // Prepare different configurations according to the platform
  final Map<String, dynamic> config = {
    // --- Common parameters ---
    'appID': 'YOUR_APP_ID', // Replace with your App ID
    'appToken': 'YOUR_APP_TOKEN', // Replace with your App Token
    'channel': 'flutter_channel',
    'enableDebug': true, // Debug mode, be sure to set to false in the production environment

    // --- Android-specific parameters ---
    'blockDetect': true,
    'seriousBlockDetect': true,
    'fpsMonitor': true,
    'memoryMonitor': true,
    'batteryMonitor': true,
    'cpuMonitor': true,
    'diskMonitor': true,
    'trafficMonitor': true,
    'operateMonitor': true,
    'startMonitor': true,
    'pageMonitor': true,
    'netMonitor': true,
    'enableLogRecovery': true,

    // --- iOS-specific parameters ---
    'defaultMonitors': 0x1 | 0x2 | 0x4, // Example: Enable crash, network, and start monitoring
  };

  APMPlusBridge.initialize(config);
  APMPlusBridge.setUserID('user_12345');
}
```


<span id="DguvOJzf"></span>
## Prerequisites

Before calling `initialize` and `setUserID`, be sure to obtain the user's privacy authorization.

<span id="MV8uvFUg"></span>
## Limits


* All bridge calls mentioned in this solution are executed on the main thread by default. Although most parts of the APMPlus native SDK are thread\-safe, to be safe, it is recommended that all calls from Flutter be initiated on the main thread.

* When reporting custom error, be sure to strictly use the official interface. On Android, use `MonitorCrash.reportCustomErr`; on iOS, use the `UserException` module interface.

* Necessary parameter validation should be added in the native bridge code to prevent native code crashes caused by illegal parameters passed from Flutter, such as null or type errors.

* The `enableDebug` configuration is used to enable or disable Debug mode. Enabling this configuration will print detailed APMPlus logs, making it easier to verify data reporting during development. **When releasing the production version, be sure to set it to false.** 

* Be sure to call `APMPlusBridge.initialize` as early as possible after the app starts to ensure the accuracy of performance and other data collection. Native SDK initialization should be triggered by the first call from Flutter in `Application#onCreate` (Android) or `AppDelegate#didFinishLaunchingWithOptions` (iOS). The native side can add a static boolean value `isInitialized` to prevent repeated initialization.


<span id="JJY5mJlz"></span>
## Operation Procedure


<Tabs>
<Tab zoneid="flAglh3dCE" title="Android integration guide">
<TabTitle>Android integration guide</TabTitle>

1. Add Maven repository. In the `build.gradle` file in the project root directory, add the Maven repository addresses for platform and byteX. The sample code is as follows:


```Groovy
// project/build.gradle
buildscript {
    repositories {
        // ... Other repositories
        maven {
            url "https://artifact.bytedance.com/repository/Volcengine/"
        }
    }
}

allprojects {
    repositories {
        // ... Other repositories
        maven {
            url "https://artifact.bytedance.com/repository/Volcengine/"
        }
    }
}
```



2. Add Gradle dependency. In the `build.gradle` file of the app module, add the APMPlus\-related dependencies. The sample code is as follows:


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If using an overseas application, replace the <code>.cn</code> suffix with <code>.oversea</code>.</div>


```Groovy
// app/build.gradle
dependencies {
    // ... Other dependencies
    // APMPlus core dependency (domestic version)
    implementation 'com.volcengine:apm_insight:1.5.25.cn'
    // APMPlus crash monitoring module
    implementation 'com.volcengine:apm_insight_crash:1.5.18'
}
```



3. Bridge code implementation. In the Android part of the Flutter plugin or main project, create a Kotlin class to implement the bridge logic. The sample code for `APMPlusFlutterBridgePlugin.kt` is as follows:


```Kotlin
package com.example.your_project_name // Replace with your package name

import android.app.Application
import android.content.Context
import com.apm.insight.MonitorCrash
import com.bytedance.apm.insight.ApmInsight
import com.bytedance.apm.insight.ApmInsightInitConfig
import com.bytedance.apm.insight.IDynamicParams
import com.apm.insight.log.VLog
import io.flutter.embedding.engine.plugins.FlutterPlugin
import io.flutter.plugin.common.MethodCall
import io.flutter.plugin.common.MethodChannel
import org.json.JSONObject

class APMPlusFlutterBridgePlugin : FlutterPlugin, MethodChannel.MethodCallHandler {
    private lateinit var channel: MethodChannel
    private lateinit var context: Context
    private lateinit var mMonitorCrash: MonitorCrash

    override fun onAttachedToEngine(flutterPluginBinding: FlutterPlugin.FlutterPluginBinding) {
        channel = MethodChannel(flutterPluginBinding.binaryMessenger, "apmplus_flutter_bridge")
        channel.setMethodCallHandler(this)
        context = flutterPluginBinding.applicationContext
    }

    override fun onMethodCall(call: MethodCall, result: MethodChannel.Result) {
        when (call.method) {
            "initialize" -> {
                val config = call.arguments as? Map<String, Any> ?: return
                initializeApm(config)
                result.success(null)
            }
            "setUserID" -> {
                val userId = (call.arguments as? Map<String, Any>)?.get("userId") as? String
                if (userId != null) {
                    mMonitorCrash?.config()?.setUID(userId)
                    ApmInsight.getInstance().setUserId(userId)
                }
                result.success(null)
            }
            "reportCustomError" -> {
                val args = call.arguments as? Map<String, Any>
                reportCustomError(args)
                result.success(null)
            }
            "reportCustomEvent" -> {
                val args = call.arguments as? Map<String, Any>
                reportCustomEvent(args)
                result.success(null)
            }
            "log" -> {
                val args = call.arguments as? Map<String, Any>
                log(args)
                result.success(null)
            }
            else -> result.notImplemented()
        }
    }

    private fun initializeApm(config: Map<String, Any>) {
        val appID = config["appID"] as? String ?: return
        val appToken = config["appToken"] as? String ?: return
        val channel = config["channel"] as? String ?: "unknown"
        val enableDebug = config["enableDebug"] as? Boolean ?: false

        // 1. Initialize crash monitoring
        val crashConfig = MonitorCrash.Config.app(appID)
            .token(appToken)
            .channel(channel)
            .debugMode(enableDebug)
            .build()
        mMonitorCrash = MonitorCrash.init(context as? Application, crashConfig)

        // 2. Initialize performance monitoring
        ApmInsight.getInstance().init(context as? Application)
        VLog.init(context, 20) // Initialize custom log, maximum disk usage is 20MB

        val builder = ApmInsightInitConfig.builder()
            .aid(appID)
            .token(appToken)
            .channel(channel)
            .debugMode(enableDebug)
            .blockDetect(config["blockDetect"] as? Boolean ?: false)
            .seriousBlockDetect(config["seriousBlockDetect"] as? Boolean ?: false)
            .fpsMonitor(config["fpsMonitor"] as? Boolean ?: false)
            .memoryMonitor(config["memoryMonitor"] as? Boolean ?: false)
            .batteryMonitor(config["batteryMonitor"] as? Boolean ?: false)
            .cpuMonitor(config["cpuMonitor"] as? Boolean ?: false)
            .diskMonitor(config["diskMonitor"] as? Boolean ?: false)
            .trafficMonitor(config["trafficMonitor"] as? Boolean ?: false)
            .operateMonitor(config["operateMonitor"] as? Boolean ?: false)
            .startMonitor(config["startMonitor"] as? Boolean ?: false)
            .pageMonitor(config["pageMonitor"] as? Boolean ?: false)
            .netMonitor(config["netMonitor"] as? Boolean ?: false)
            .enableLogRecovery(config["enableLogRecovery"] as? Boolean ?: false)

        ApmInsight.getInstance().start(builder.build())
    }

    private fun reportCustomError(args: Map<String, Any>?) {
        if (args == null) return
        val type = args["type"] as? String ?: "unknown_error"
        val message = args["message"] as? String ?: ""
        val stack = args["stack"] as? String
        val severity = args["severity"] as? String ?: "error"
        val tags = args["tags"] as? Map<String, String> ?: emptyMap()
        val extrasAny = args["extras"] as? Map<String, Any> ?: emptyMap()

        // Merge extras/tags into data (String->String)
        val data = mutableMapOf<String, String>()
        data.putAll(tags)
        data["severity"] = severity
        extrasAny.forEach { (k, v) ->
            if (v != null) data[k] = v.toString()
        }

        // throwable: Prefer to construct using stack trace string; pass null if there is no stack trace
        val throwable: Throwable? = if (!stack.isNullOrBlank()) RuntimeException(stack) else null

        mMonitorCrash？.reportCustomErr(message, type, throwable, data)
    }

    private fun reportCustomEvent(args: Map<String, Any>?) {
        if (args == null) return
        val eventName = args["eventName"] as? String ?: return
        val attributes = args["attributes"] as? Map<String, String>
        val metrics = args["metrics"] as? Map<String, Double>

        ApmInsight.getInstance().monitorEvent(eventName, attributes, metrics)
    }

    private fun log(args: Map<String, Any>?) {
        if (args == null) return
        val level = args["level"] as? String ?: "info"
        val tag = args["tag"] as? String ?: "FlutterLog"
        val message = args["message"] as? String ?: ""

        when (level) {
            "debug" -> VLog.d(tag, message)
            "info" -> VLog.i(tag, message)
            "warn" -> VLog.w(tag, message)
            "error" -> VLog.e(tag, message)
        }
    }

    override fun onDetachedFromEngine(binding: FlutterPlugin.FlutterPluginBinding) {
        channel.setMethodCallHandler(null)
    }
}
```


Detailed parameter alignment description is as follows:


|Dart APMPlusBridge method |Parameters |Android native API |Mapping relationship |
|---|---|---|---|
|initialize |config |MonitorCrash.Config, ApmInsightInitConfig |Set each field such as appID, appToken, and channel in the Map to the native Config object one by one.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">appID and appToken are required during initialization.</div><br> |
|setUserID |userId |MonitorCrash.setUserUniqueID, ApmInsight.getInstance().setUserId |Directly pass the userId string to the native interface. |
|reportCustomError |type |The type of MonitorCrash.reportCustomErr |Direct mapping. |
||message |The message of MonitorCrash.reportCustomErr |Direct mapping. |
||stack |The throwable of MonitorCrash.reportCustomErr |When the stack trace is not empty, use `new RuntimeException(stack)`; otherwise, pass null. |
||tags, extras, severity |MonitorCrash.reportCustomErr's data |Merge into `Map<String, String>`, and safely convert non\-string values to String. |
|reportCustomEvent |eventName |monitorEvent's serviceName |Direct mapping. |
||attributes |monitorEvent's dimension |Direct mapping. |
||metrics |metric of monitorEvent |Direct mapping. |
|log |level, tag, message |VLog.d, VLog.i, VLog.w, VLog.e |Select the corresponding VLog method according to the level, and pass in tag and message. |





</Tab>
<Tab zoneid="OLPXPvrgIv" title="iOS integration guide">
<TabTitle>iOS integration guide</TabTitle>

1. Add private source. In the `Podfile` file at the root directory of the project, add the platform's private Podspec repository. Sample code is as follows:


```Ruby
# Podfile
source 'https://github.com/volcengine/volcengine-specs.git'
source 'https://cdn.cocoapods.org/' # Ensure the official source exists
```



2. Add Pod dependency. In the `Podfile` file, add the `RangersAPM` dependency for the Target and add submodules as needed. Sample code is as follows:


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After adding, run the <code>pod install</code> command to install dependencies.</div>


```Ruby
# Podfile
target 'Runner' do
  use_frameworks!
  # ... Other configurations

  pod 'RangersAPM', '5.2.9', :subspecs => [
    'Crash',          # (Required) crash monitoring
    'UserException',  # custom error
    'EventMonitor',   # custom event
    'APMLog',         # custom log (Alog)
    'CN'              # Reporting domain name, use 'CN' for Chinese mainland, use 'Global' for overseas
    # Add other modules as needed, such as 'LAG', 'OOM', 'NetworkPro', and more
  ]
end
```



3. Bridge code implementation. In the iOS section of the Flutter plugin or the main project, create a Swift class to implement the bridging logic. Sample code for `APMPlusFlutterBridgePlugin.swift` is as follows:


```Swift
import Flutter
import UIKit
import RangersAPM

public class APMPlusFlutterBridgePlugin: NSObject, FlutterPlugin {
    public static func register(with registrar: FlutterPluginRegistrar) {
        let channel = FlutterMethodChannel(name: "apmplus_flutter_bridge", binaryMessenger: registrar.messenger())
        let instance = APMPlusFlutterBridgePlugin()
        registrar.addMethodCallDelegate(instance, channel: channel)
    }

    public func handle(_ call: FlutterMethodCall, result: @escaping FlutterResult) {
        switch call.method {
        case "initialize":
            guard let config = call.arguments as? [String: Any] else { return }
            initializeApm(config: config)
            result(nil)
        case "setUserID":
            guard let args = call.arguments as? [String: Any], let userId = args["userId"] as? String else { return }
            RangersAPM.setUserID(userId)
            result(nil)
        case "reportCustomError":
            guard let args = call.arguments as? [String: Any] else { return }
            reportCustomError(args: args)
            result(nil)
        case "reportCustomEvent":
            guard let args = call.arguments as? [String: Any] else { return }
            reportCustomEvent(args: args)
            result(nil)
        case "log":
            guard let args = call.arguments as? [String: Any] else { return }
            log(args: args)
            result(nil)
        default:
            result(FlutterMethodNotImplemented)
        }
    }

    private func initializeApm(config: [String: Any]) {
        guard let appID = config["appID"] as? String else { return }
        guard let appToken = config["appToken"] as? String else { return }
        
        let apmConfig = RangersAPMConfig.config(withAppID: appID, appToken: appToken)
        if let channel = config["channel"] as? String {
            apmConfig.channel = channel
        }
        if let enableDebug = config["enableDebug"] as? Bool, enableDebug {
            RangersAPM.allowDebugLog(using: nil)
        }
        if let defaultMonitors = config["defaultMonitors"] as? UInt {
            apmConfig.defaultMonitors = RangersAPMMonitorSwitch(rawValue: defaultMonitors)
        }

        RangersAPM.start(with: apmConfig)
        
        // Enable Alog
        if let enableLogRecovery = config["enableLogRecovery"] as? Bool, enableLogRecovery {
            RangersAPM.setALogEnabled()
        }
    }

    private func reportCustomError(args: [String: Any]) {
        guard let type = args["type"] as? String,
              let message = args["message"] as? String else { return }

        let stack = args["stack"] as? String ?? ""
        let severity = args["severity"] as? String ?? ""
        let extras = args["extras"] as? [String: Any] ?? [:]

        // Construct customParams: merge extras and add the "stack" key
        var customParams: [String: Any] = extras
        customParams["stack"] = stack

        // Construct filters: Prefer to use tags; if empty and there is a single tag field, construct {"tag": tag}
        var filtersDict: [String: String] = [:]
        if let tags = args["tags"] as? [String: String], !tags.isEmpty {
            filtersDict = tags
        } else if let singleTag = args["tag"] as? String, !singleTag.isEmpty {
            filtersDict = ["tag": singleTag]
        }

        // Swift bridge name may be: RangersAPM.trackUserException(withExceptionType:title:subTitle:customParams:filters:callback:)
        // If the bridge name is different, you can directly use the Objective-C form:
        // [RangersAPM trackUserExceptionWithExceptionType:type title:message subTitle:severity customParams:customParams filters:filtersDict.isEmpty ? nil : filtersDict callback:^(BOOL success, NSString *uuid) {}];
        RangersAPM.trackUserException(
            withExceptionType: type,
            title: message,
            subTitle: severity,
            customParams: customParams,
            filters: filtersDict.isEmpty ? nil : filtersDict,
            callback: { success, uuid in
                // no-op
            }
        )
    }

    private func reportCustomEvent(args: [String: Any]) {
        guard let eventName = args["eventName"] as? String else { return }
        
        let attributes = args["attributes"] as? [String: String] ?? [:]
        let metrics = args["metrics"] as? [String: Double] ?? [:]
        
        RangersAPM.trackEvent(eventName, metrics: metrics, dimension: attributes, extraValue: nil)
    }
    
    private func log(args: [String: Any]) {
        guard let level = args["level"] as? String,
              let tag = args["tag"] as? String,
              let message = args["message"] as? String else { return }

        switch level {
        case "debug":
            RangersAPM.debugALog(message, tag: tag, fileName: #file, funcName: #function, line: #line)
        case "info":
            RangersAPM.infoALog(message, tag: tag, fileName: #file, funcName: #function, line: #line)
        case "warn":
            RangersAPM.warnALog(message, tag: tag, fileName: #file, funcName: #function, line: #line)
        case "error":
            RangersAPM.errorALog(message, tag: tag, fileName: #file, funcName: #function, line: #line)
        default:
            break
        }
    }
}
```


Detailed parameter alignment description is as follows:


|Dart APMPlusBridge method |Parameters |iOS native API |Mapping relationship |
|---|---|---|---|
|initialize |config |RangersAPMConfig, RangersAPM.start(with:) |Set each field (such as appID, appToken, and channel) from the Map to the RangersAPMConfig object individually.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">appID and appToken are required during initialization.</div><br> |
|setUserID |userId |RangersAPM.setUserID(_:) |Directly pass the userId string to the native interface. |
|reportCustomError |type, message, stack |RangersAPM.trackUserException(withExceptionType:title:subTitle:customParams:filters:callback:) |type→exceptionType，message→title；stack→customParams["stack"]。 |
| |severity(String), tags(Map<String,String\>) or tag(String), extras(Map<String,Any\>) |RangersAPM.trackUserException(withExceptionType:title:subTitle:customParams:filters:callback:) |* severity→subTitle；tags→filters。 If there is only a single tag field, construct as {"tag": tag}; if empty, pass nil<br><br>* extras→customParams (merged with "stack"). Pass a placeholder closure for callback `{ success, uuid in /* no-op */ }`. |
|reportCustomEvent |eventName |RangersAPM.trackEvent(_:withParameters:) |Directly map to the eventName parameter. |
| |attributes, metrics |withParameters of trackEvent |Merge attributes and metrics into the withParameters dictionary. |
|log |level, tag, message |RangersAPM.debugALog, infoALog, warnALog, errorALog |Select the corresponding ALog method according to the level, and pass in tag and message.<br><br>fileName, funcName, and line are automatically filled using Swift's #file, #function, and #line macros. |





</Tab>
</Tabs>
