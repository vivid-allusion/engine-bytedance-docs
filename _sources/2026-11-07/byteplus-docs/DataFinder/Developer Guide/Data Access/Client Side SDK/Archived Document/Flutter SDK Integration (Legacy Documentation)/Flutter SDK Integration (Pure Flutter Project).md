---
title: "Flutter SDK Integration (Pure Flutter Project)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Flutter_SDK_Integration_Pure_Flutter_Project"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Flutter SDK integration documentation has been revised, please check the new documentation: <a href="https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Integration">Flutter SDK Integration</a>.</div>


If you have no native Android/iOS/HarmonyOS development experience and your project is a new Flutter\-only project created with the flutter.create command, this document can be used as a supplementary reference for Flutter project access.

<span id="e27b4817"></span>
# 1 Add dependencies

<span id="68e212bb"></span>
### 1.1 flutter plugin dependencies

```YAML
dependencies:
  ......
  rangers_applog_flutter_plugin: 1.4.1
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The version in the above example 1.4.1 an example version, the latest version is available in the general SDK integration documentation: <a href="https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Integration_and_Event_Tracking">Flutter SDK Integration and Event Tracking</a>.</div>


<span id="af87c829"></span>
### 1.2 Android dependencies

Add applog dependency to android/app/build.gradle file

```Groovy
//The version number is on demand, you can refer to the Android SDK documentation to choose.
dependencies {
  implementation 'com.bytedance.applog:RangersAppLog-All-cn:6.x.x'
 }
```


<span id="e2728da6"></span>
### 1.3 Dependence iOS

Add RangersAppLog dependency to iOS Podfile

```objectivec
//The version number is on demand, you can refer to iOS SDK documentation to choose
target 'Runner' do
pod 'RangersAppLog', '6.x.x',
      :subspecs => [
          'Host/CN', //import when it is SaaS version, skip it for private deployment version
          'Core',
          'UITracker',
          'Log', //Remove it when do not need cicle function and real-time event tracking
          'Picker', //Remove it when do not need cicle function
          'Unique' #Used to collect IDFA after authorization, remove it when you do not need it.
      ]
end
```


<span id="9cbec488"></span>
### 1.4 Harmony OS dependencies

Obtain the SDK and access method: You need to contact BytePlus technical support to obtain it.

```objectivec
"dependencies": {
  "@volcengine/applog": "file:./har/applogx.har"
}
```


<span id="a58b45b3"></span>
# 2 Other configurations and event tracking

This document is for supplemental reference, and you will also need to consult the generic Flutter SDK integration documentation for additional access configurations and supported event tracking settings, see [Flutter SDK Integration and Event Tracking](https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Integration_and_Event_Tracking).
