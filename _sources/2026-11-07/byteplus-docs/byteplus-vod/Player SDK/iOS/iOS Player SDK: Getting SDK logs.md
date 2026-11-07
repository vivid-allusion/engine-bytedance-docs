---
title: "iOS Player SDK: Getting SDK logs"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-sdk-logs-ios"
---

The iOS Player SDK supports log recording, remote log retrieval, and real\-time log callbacks for debugging and troubleshooting.

<span id="logging-best-practices"></span>
## Logging best practices

Starting with BytePlus iOS Player SDK `1.52.100.4`, the Player SDK provides enhanced log retrieval. Choose one of the following three approaches based on your application's release stage. For the gradual rollout stage, we strongly recommend approach two, which lets you obtain logs from the time an issue occurred after you receive user feedback.

<span id="approach-1-collect-logs-yourself-through-the-log-callback"></span>
### Approach 1: Collect logs yourself through the log callback

Suitable for the development and internal testing stages. Integrate the SDK's [log callback interface](https://docs.byteplus.com/en/docs/25/120711#receive-real-time-log-callbacks) to write logs to files yourself and collect them through your own log retrieval platform. If you suspect an SDK issue, provide the logs to BytePlus technical support for analysis.

This approach requires you to implement log file writing and retrieval yourself.

<span id="approach-2-enable-local-log-recording-for-byteplus-to-retrieve-recommended"></span>
### Approach 2: Enable local log recording for BytePlus to retrieve (recommended)

Suitable for the gradual rollout stage. Use the [SDK log configuration interface](https://docs.byteplus.com/en/docs/25/120711#configure-logging) to enable real\-time log writing to the local disk. After receiving user feedback, provide the affected device ID to BytePlus technical support. **With your permission, BytePlus retrieves and analyzes the logs through its own log retrieval platform.** 

Continuous log writing on the client can introduce some performance overhead. To reduce this overhead, the SDK first writes logs to a memory\-mapped file (mmap) and then flushes them to disk asynchronously. This avoids frequent synchronous disk I/O and minimizes the impact on player performance.

<span id="approach-3-have-byteplus-send-configuration-for-affected-devices"></span>
### Approach 3: Have BytePlus send configuration for affected devices

Suitable for the full release stage. After receiving user feedback, provide the affected device ID to BytePlus technical support. **With your permission, BytePlus sends configuration to the affected device to enable local log recording and retrieval polling, and retrieves and analyzes the logs through its own log retrieval platform.** 

Log recording and retrieval take effect only after the configuration is delivered and the device uses the app. This introduces a delay, and the issue might no longer recur, which can make it impossible to obtain logs from the time the issue occurred.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">If you want to use server\-delivered configuration, do not explicitly set <code>enable</code> to <code>NO</code> locally. Local configuration takes precedence over server\-delivered configuration. If you explicitly disable log retrieval, server\-delivered configuration cannot enable it.</div>


<span id="configure-logging"></span>
## Configure logging

The following configuration applies to BytePlus iOS Player SDK `1.52.100.4` and later. You can enable log recording and retrieval locally without waiting for the server to send configuration.

Before initializing `TTSDKManager`, create a `TTSDKLogConfiguration` and assign it to `TTSDKConfiguration.logConfiguration`. Configure logging in AppDelegate or another early initialization stage to capture logs from SDK startup.

<span id="usage"></span>
### Usage

```objectivec
// Initialize the SDK configuration.
TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:appId licenseName:licenseName];

// Enable log recording and retrieval.
configuration.logConfiguration = [TTSDKLogConfiguration defaultLogConfigurationWithEnabled:YES];

// Optional logging settings.
configuration.logConfiguration.logLevel = TTSDKLogLevelDebug;
configuration.logConfiguration.maxLogSizeM = 50; // Total capacity in MB.
configuration.logConfiguration.singleLogSizeM = 5; // Per-file capacity in MB.

// Retain any other SDK configuration required by your application.
[TTSDKManager startWithConfiguration:configuration];
```


<span id="configuration-parameters"></span>
### Configuration parameters


|Property |Type |Required |Description |Default |
|---|---|---|---|---|
|`enable` |BOOL |Yes |Enables log recording and retrieval when set to `YES`. |`NO` |
|`logLevel` |TTSDKLogLevel |No |Minimum log level to record. |`TTSDKLogLevelInfo` |
|`logPath` |NSString \* |No |Log storage path. When `nil`, uses `/Library/Volclog/`. |`nil` |
|`maxLogSizeM` |NSUInteger |No |Maximum total size of all log files, in MB. |`100` |
|`singleLogSizeM` |NSUInteger |No |Maximum size of each log file, in MB. |`2` |
|`logExpireTimeS` |NSUInteger |No |Retention period in seconds. Expired files are automatically removed. |`604800` (7 days) |
|`deviceID` |NSString \* |No |Custom device ID for server\-side log retrieval. Set it only if needed. |`nil` |


<span id="receive-real-time-log-callbacks"></span>
## Receive real\-time log callbacks

Use log callbacks when you need to process individual log strings in real time, such as forwarding them to your own monitoring system. If you use approach one, integrate your own log file writing and retrieval logic in the callback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Log callbacks and <code>TTSDKLogConfiguration</code> can coexist. The configuration controls internal logging, such as file writes, while the delegate provides an external log stream.</div>



1. Before initializing `TTSDKManager`, call `setLogFlag:` to select the logs to receive. During debugging, you can enable all logs.

2. Create a class that implements `TTVideoEngineLogDelegate` and register its instance with `TTVideoEngine`.


```objectivec
// Before calling [TTSDKManager startWithConfiguration:...]:
[TTVideoEngine setLogFlag:TTVideoEngineLogFlagAll];

// MyLogger.h
@interface MyLogger : NSObject <TTVideoEngineLogDelegate>
@end

// MyLogger.m
@implementation MyLogger
- (void)consoleLog:(NSString *)log {
    NSLog(@"[TTVideoEngine_Callback] %@", log);
}
@end

// After initializing TTSDKManager and before starting playback:
self.logger = [[MyLogger alloc] init];
[TTVideoEngine setLogDelegate:self.logger];
```
