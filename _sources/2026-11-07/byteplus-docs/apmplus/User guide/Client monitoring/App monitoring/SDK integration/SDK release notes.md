---
title: "SDK release notes"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SDK_update_log"
---

This topic records the release notes for the app\-side SDK.

## iOS platform

### RangersAPM

> **danger**

> SDK versions 3.10.6 and earlier are no longer maintained. Replace them with a maintained SDK (preferably the latest version) as soon as possible. Otherwise, these versions may cause issues such as OOM (out\-of\-memory) and disrupt normal operation.

See [APMInsight_iOS release notes](https://github.com/volcengine/APMInsight_iOS/blob/master/%E8%AF%B4%E6%98%8E.md).

### RangersAPMDoctor

#### 2024\-07\-30

|Version number |Type |Descriptions |Version requirements |
|---|---|---|---|
|2.0.0 |Fixed issues |Fixed the issue where add\-on integration with dynamic libraries did not take effect. |RangersAPM \>= 4.1.0 |
||New features (incompatible) |Added a global switch for plugin features, which is disabled by default. ||

#### 2024\-07\-19

|Version number |Type |Descriptions |Version requirements |
|---|---|---|---|
|1.0.2 |Improvements |Optimized some processing logic. |RangersAPM \>= 4.1.0 |

#### 2024\-07\-09

|Version number |Type |Descriptions |Version requirements |
|---|---|---|---|
|1.0.1 |Improvements |Optimized the prompt when the switch is not enabled. |RangersAPM \>= 4.1.0 |

#### 2024\-07\-05

|Version number |Type |Descriptions |Version requirements |
|---|---|---|---|
|1.0.0 |New features |Supports integration verification for most features of the performance monitoring add\-on. |RangersAPM \>= 4.1.0 |

## Harmony platform

See the `Release notes` tab under[@volcengine/apmplus](https://ohpm.openharmony.cn/#/cn/detail/@volcengine%252Fapmplus).

## Android platform

> **danger**

* > `apm_insight:1.5.3.cn` and earlier versions of the performance monitoring SDK are no longer maintained. Replace them with a maintained SDK (preferably the latest version) as soon as possible. Otherwise, these versions may cause failures and affect normal use.

* > `apm_insight_crash:1.5.0` and earlier versions of the performance monitoring SDK are no longer maintained. Replace them with a maintained SDK (preferably the latest version) as soon as possible. Otherwise, these versions may cause failures and disrupt normal operation.

### 2026\-5\-13

#### Android：`apm_insight_crash:1.5.21`

* Feature updates

   * Fixed the issue where the platform could not display due to invalid tombstone file formats.

### 2026\-1\-15

#### Android：`apm_insight_crash:1.5.20`

* Feature updates

   * Adapted to native stack offsets in higher versions.

   * Adapted to target36 network protocol changes.

### 2025\-9\-3

#### Android：`apm_insight:1.5.25.cn`

* Feature updates

   * Fixed NoClassDefFoundError caused by Reflect.

   * Adapted to Android 15 16kb page size.

   * Scattered setting requests

### 2025\-9\-3

#### Android：`apm_insight:1.5.24.oversea`

* Feature updates

   * Fixed NoClassDefFoundError caused by Reflect.

   * Adapted to Android 15 16kb page size.

   * Scattered setting requests

### 2025\-7\-30

#### Android：`apm_insight_crash:1.5.18.oversea`

* Feature updates

   * Improved ANR Trace capture success rate.

   * Adapted to Android 15 16kb page size.

### 2025\-7\-30

#### Android：`apm_insight_crash:1.5.18`

* Feature updates

   * Improved ANR Trace capture success rate.

   * Adapted to Android 15 16kb page size.

### 2025\-4\-15

#### Android：`apm_insight_crash:1.5.10`

* Feature updates

   * Fixed the issue of missing system version in configuration requests.

   * Fixed the issue of incomplete native crash stacks.

   * Optimized native secondary crash issues

### 2025\-4\-15

#### Android：`apm_insight_crash:1.5.11.oversea`

* Feature updates

   * Fixed the issue of missing system version in configuration requests

   * Fixed the issue of incomplete native crash stacks

   * Optimized native secondary crash issues

### 2025\-3\-13

#### Android：`apm_insight:1.5.13.oversea`

* Feature updates

   * Fixed compatibility issues in FPS monitoring on Android 12+.

### 2025\-3\-13

#### Android：`apm_insight:1.5.12.cn`

* Feature updates

   * Fixed compatibility issues in FPS monitoring on Android 12+.

### 2025\-3\-10

#### Android：`apm_insight:1.5.11.oversea`

* Feature updates

   * Fixed the abnormal FPS collection issue caused by the possible failure of the onFront callback during two\-step initialization

### 2025\-3\-10

#### Android：`apm_insight:1.5.10.cn`

* Feature updates

   * Fixed the abnormal FPS collection issue caused by the possible failure of the onFront callback during two\-step initialization

### 2024\-11\-21

#### Android：`apm_insight:1.5.9.cn`

* Feature updates

   * Added a user privacy data switch (device model, resolution, OS version, and more).

   * Categorized SocketException in network monitoring as a connection error.

### 2024\-11\-13

#### Android：`apm_insight_crash:1.5.9`

* Feature updates

   * Added a user privacy data switch (device model, resolution, OS version, and more).

### 2024\-11\-12

#### Android：`apm_insight_crash:1.5.8.oversea`

* Feature updates

   * Added a user privacy data switch (device model, resolution, OS version, and more).

### 2024\-10\-15

#### Android：`apm_insight_crash:1.5.7`

* Feature updates

   * Avoided the occasional crash issue during ANR information collection on Xiaomi 12 and later models.

   * Added a PV data correction switch (fixPageView)

   * Added switches respectively for ANR INFO and Looper monitoring

### 2024\-09\-04

#### Android：`apm_insight:1.5.7.oversea`

* Feature updates

   * Released the overseas version, reporting data to Johor, Malaysia

### 2024\-07\-22

#### Android：`apm_insight:1.5.6.cn`

* Feature updates

   * Added a collection time interval for traffic monitoring

   * Optimize header resolution data

   * Updated the configuration broadcast name to be independent among applications

   * Removed the dependency on support

### 2024\-05\-22

#### Android：`apm_insight_crash:1.5.1`

* Feature updates

   * Adapted the memory snapshot acquisition feature for Android 10 and later versions

   * Limited the total volume of custom error reports and the number of reports with identical stacks

   * Fixed the resolution classification error

### 2024\-02\-29

#### Android：`apm_insight:1.5.4.cn-rc.1`

* Feature updates

   * Startup monitoring now supports custom end points

### 2024\-01\-17

#### Android：`apm_insight:1.5.3.cn`

* Feature updates

   * Added new H5 monitoring capabilities

### 2024\-01\-04

#### Android：`apm_insight_crash:1.5.0`

* Feature updates

   * Optimized the crash data reporting logic

   * Optimized the stability when acquiring full\-thread stacks

### 2023\-12\-15

#### Android：`apm_insight:1.5.3.cn-rc.4`

* Feature updates

   * Compatible with Android 14

   * Added fallback capabilities for Activity leaks

### 2023\-10\-23

#### Android：`apm_insight_crash:1.4.9`

* Feature updates

   * Java crash protection feature

   * Crash optimization feature \- TransactionTooLargeException optimization solution

### 2023\-10\-13

#### Android：`apm_insight:1.5.2.cn`

* Feature updates

   * Released stable version 1.5.2

### 2023\-10\-13

#### Android：`apm_insight_crash:1.4.8`

* Feature updates

   * Released stable version 1.4.8

### 2023\-09\-20

#### Android：`apm_insight_crash:1.4.8-rc.5`

* Feature updates

   * Supports a switch to control the collection of GAID

### 2023\-09\-15

#### Android：`apm_insight_crash:1.4.8-rc.4`

* Feature updates

   * Supports monitoring and reporting of app exit reasons

   * Crash information, custom errors, process exit reasons, and other data are written into APMPlus logs

### 2023\-09\-14

#### Android：`apm_insight:1.5.1.cn-rc.8`

* Feature updates

   * Optimized the "unKnow" type issue in network monitoring

   * Optimized the time consumption of active vlog reporting

   * Retrieval supports APMPlus logs

* Bug fixes

   * Fixed the issue of incorrect URLs in network monitoring for redirected requests

### 2023\-08\-28

#### Android：`apm_insight:1.5.1.cn-rc.5`

* Feature updates

   * Added cache monitoring to network monitoring

   * Monitoring will not be enabled if no sampling is triggered for lags

   * No network monitoring data will be collected without initialization

   * Added configurations during initialization to control whether to report network, startup, and page data

* Bug fixes

   * Fixed a potential exception issue caused by setting the OkHttp EventListener multiple times

### 2023\-06\-15

#### Android：`apm_insight:1.5.1.cn-rc.1`

* Feature updates

   * Added monitoring for user metrics and user session duration

### 2023\-05\-23

#### Android：`apm_insight:1.5.0.cn`

* Feature updates

   * Compliant initialization is divided into the init and start methods. Data is only collected when start is called.

### 2023\-05\-23

#### Android：`apm_insight_crash:1.4.7`

* Feature updates

   * Fixed the issue where custom logs were still reported after the main crash reporting switch was turned off

   * Supports an initialization method that does not automatically collect user information. Monitoring and information collection begin after the startup monitoring method is called

### 2023\-05\-15

#### Android：`apm_insight_crash:1.4.7-rc.7`

* Feature updates

   * Handled the occasional secondary crash issue on Android 12 and later devices

   * Supports the delivery of custom log time configurations along with crash reports

### 2023\-05\-15

#### Android：`apm_insight:1.5.0.cn-rc.7`

* Feature updates

   * Added custom retrieval functionality

   * Added sampling and switch control capabilities for active vlog reporting

### 2023\-04\-10

#### Android：`apm_insight_crash:1.4.7-rc.2`

* Feature updates

   * Added switches to control the acquisition of android_id and OAID

### 2023\-03\-28

#### Android：`apm_insight_crash:1.4.7-rc.1`

* Feature updates

   * Added a proxy interface for network requests

   * Modified the battery level acquisition method

   * Optimized potential secondary crash issues during the information collection process after a crash

### 2023\-03\-28

#### Android：`apm_insight:1.5.0.cn-rc.4`

* Feature updates

   * Added a proxy interface for network requests

   * Added a lifecycle initialization method

### 2023\-03\-20

#### Android：`apm_insight_sdk:1.1.8`

* Feature updates

   * Released the event logging add\-on for SDK monitoring

#### Android：`apm_insight_cloud:0.0.3.sdk`

* Feature updates

   * Released the log retrieval add\-on for SDK monitoring

### 2023\-01\-16

#### Android：`apm_insight:1.4.10.cn-rc.0`

* Feature updates

   * Added traffic monitoring

### 2023\-01\-04

#### Android：`apm_insight_crash:1.4.6-rc.17`

* Bug fixes

   * Fixed potential issues affecting crash information collection

### 2022\-12\-29

#### Android：`apm_insight_crash:1.4.6-rc.16`

* Feature updates

   * PV events support custom tag filtering

   * Optimized the access frequency of some interfaces

### 2022\-12\-29

#### Android：`apm_insight:1.4.9.cn`

* Feature updates

   * Added monitoring for HttpURLConnection

   * The whitelist now supports user_id

   * Added a performance fault\-tolerance mechanism

* Bug fixes

   * Fixed the bug where FPS was not reported on version 12

   * Filtered out lag data without stack traces

### 2022\-11\-22

#### Android：`apm_insight_crash:1.4.6-rc.14`

* Feature updates

   * No more data will be reported once the event quota is exhausted

   * Supports uploading custom files upon a crash

* Bug fixes

   * Fixed the issue of frequent requests for carrier information under special circumstances

### 2022\-11\-21

#### Android：`apm_insight:1.4.9.cn-rc.5`

* Feature updates

   * Optimized startup time

   * Data collection and reporting will stop once the event quota is exhausted

   * Unified the utility library used for acquiring process names

   * Added monitoring for the host in the header to network monitoring

   * Added a callback for active vlog reporting

* Bug fixes

   * Fixed the issue where the CPU switch became ineffective

   * Fixed the issue of duplicate interceptor additions in special network monitoring scenarios

### 2022\-10\-12

#### Android：`apm_insight:1.4.9.cn-rc.1`

* Optimized startup time and optimized to avoid potential ANR issues

#### Android：`apm_insight_crash:1.4.6-rc.10`

* Optimized startup time and potential ANR issues

### 2022\-09\-15

#### Android：`apm_insight_plugin:1.4.2`

* Fixed some compilation exceptions in certain ASM versions and updated the code

### 2022\-09\-15

#### Android：`apm_insight:1.4.8`

* Added end\-to\-end network monitoring capabilities, connecting network traces with the backend

* Added configurations for the setting fetch period and data reporting period

* Added disk monitoring to monitor disk size and remaining space, and detect abnormal and expired files

* Added an authentication token mechanism to protect platform data security

* Updated the vlog version and changed the default level to v

* Fixed the excessive time consumption issue in page monitoring

* Fixed the excessive time consumption issue in startup monitoring

### 2022\-09\-14

#### Android：`apm_insight_crash:1.4.6-rc.8`

* Added interface authentication functionality

* New initialization method

### 2022\-08\-30

#### Android：`apm_insight_crash:1.4.6-rc.6`

* Optimized logcat log capture

### 2022\-08\-04

#### Android：`apm_insight_crash:1.4.6-rc.4`

* Fixed the issue where ANR occasionally causes native crashes

### 2022\-07\-19

#### Android：`apm_insight_crash:1.4.6-rc.1`

* Modified the obfuscation file

### 2022\-06\-29

#### Android：`apm_insight_crash:1.4.5`

* Removed sensitive API calls and updated the utility library

* Added a crash callback interface to the MonitorCrash class

* Modified the field judgment for triggering sampling of custom exceptions

* SDK monitoring now supports determining ANR reporting based on Activity

### 2022\-06\-29

#### Android：`apm_insight:1.4.7.cn`

* Added custom tag functionality for performance data

* Removed sensitive API calls and updated the utility library

* Implemented real\-time synchronous reporting of DID and UID

* Fixed the issue where Vlog.changeLevel() became ineffective

* Fixed the issue where reporting failed when event parameters were empty

### 2022\-04\-14

#### Android：`apm_insight:1.4.6.cn`

* Optimized CPU thread monitoring by using an independent thread to collect CPU monitoring data

* Added system version and device model to configuration requests. The new configuration version supports filtering.

* Updated the applog version and removed the dependency on the miit library

* Moved the value of the JS key to the server

* Replaced with the BytePlus domain for compliance

### 2021\-12\-30

#### Android：`apm_insight:1.4.5.cn`

* Added CPU monitoring

* Added a switch to control whether all network errors are reported

* Added support for reporting extra with events, which can be viewed in single\-point logs to analyze the current event

* Added monitoring capabilities for trace_id in network monitoring

* Removed the call to the sensitive API getRunningAppProcesses()

* Updated the applog version. Removed the declaration and usage of the sensitive permission READ_PHONE_STATE

* Updated userid to be obtained via a callback instead of only being set during initialization
