---
title: "Android Player SDK: Getting SDK logs"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-sdk-logs-android"
---

The Android Player SDK provides local debugging logs and remote log retrieval. Local debugging lets you view logs in Logcat during development. Remote retrieval uploads SDK logs for a specified device and time range in response to server\-side tasks.

<span id="logging-best-practices"></span>
## Logging best practices

Starting with BytePlus Android Player SDK `1.52.100.5`, the Player SDK provides enhanced log retrieval. Choose one of the following three approaches based on your application's release stage. For the gradual rollout stage, we strongly recommend approach two, which lets you obtain logs from the time an issue occurred after you receive user feedback.

<span id="approach-1-collect-logs-yourself-through-the-log-callback"></span>
### Approach 1: Collect logs yourself through the log callback

Suitable for the development and internal testing stages. Integrate the SDK's [log listener](https://docs.byteplus.com/en/docs/25/120710#enable-local-debugging-logs) to write logs to files yourself and collect them through your own log retrieval platform. If you suspect an SDK issue, provide the logs to BytePlus technical support for analysis.

This approach requires you to implement log file writing and retrieval yourself.

<span id="approach-2-enable-local-log-recording-for-byteplus-to-retrieve-recommended"></span>
### Approach 2: Enable local log recording for BytePlus to retrieve (recommended)

Suitable for the gradual rollout stage. Use the [log retrieval configuration](https://docs.byteplus.com/en/docs/25/120710#enable-log-retrieval) to enable real\-time log writing to the local disk. After receiving user feedback, provide the affected device ID to BytePlus technical support. **With your permission, BytePlus retrieves and analyzes the logs through its own log retrieval platform.** 

Continuous log writing on the client can introduce some performance overhead. To reduce this overhead, the SDK first writes logs to a memory\-mapped file (mmap) and then flushes them to disk asynchronously. This avoids frequent synchronous disk I/O and minimizes the impact on player performance.

<span id="approach-3-have-byteplus-send-configuration-for-affected-devices"></span>
### Approach 3: Have BytePlus send configuration for affected devices

Suitable for the full release stage. After receiving user feedback, provide the affected device ID to BytePlus technical support. **With your permission, BytePlus sends configuration to the affected device to enable local log recording and retrieval polling, and retrieves and analyzes the logs through its own log retrieval platform.** 

Log recording and retrieval take effect only after the configuration is delivered and the device uses the app. This introduces a delay, and the issue might no longer recur, which can make it impossible to obtain logs from the time the issue occurred.

<span id="upgrading-from-earlier-versions"></span>
## Upgrading from earlier versions

Starting with BytePlus Android Player SDK `1.52.100.5`, use `LogConfig` to configure log retrieval. Existing Logcat and log listener APIs remain available and operate independently of log retrieval.

Existing local debugging and log listener integrations do not require migration. To enable remote retrieval, add `LogConfig` to your existing `Env.start()` configuration.


|Existing integration |Upgrade guidance |
|---|---|
|`VodSDK.openAllVodLog()` |Continue using it for full Logcat output during development. It does not enable log retrieval. |
|Module\-specific `turnOn()` methods |Retain them as needed to control local debugging output. |
|`TTVideoEngineLog.setLogNotifyLevel()` and `TTVideoEngineLog.setListener()` |Retain them as needed. Log retrieval does not replace your app's log listener. |
|No remote log retrieval |Add `Config.Builder.setLogConfig()`. |
|Direct calls to `VodALog.setLog()` |Migrate to `Config.Builder.setLogConfig()` to avoid maintaining two configuration entry points. |


<span id="enable-local-debugging-logs"></span>
## Enable local debugging logs

Before initializing the SDK, enable local debugging logs as described in [Enable logging for debugging](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk#8592ffc2). That section also explains log levels and the log listener.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Use full local debugging logs only during development and issue reproduction. Disable full Logcat output in production to reduce performance overhead. Log retrieval works independently and does not require <code>VodSDK.openAllVodLog()</code>.</div>


<span id="enable-log-retrieval"></span>
## Enable log retrieval

This configuration requires BytePlus Android Player SDK `1.52.100.5` or later. Create `LogConfig` before the first call to `Env.start()` and pass it through `Config.Builder.setLogConfig()`.

The following example shows the logging configuration to add to your SDK initialization. Use the `vodBuilder` from your existing initialization code and retain any other application\-specific settings.

```Java
Context appContext = context.getApplicationContext();
LogConfig logConfig = new LogConfig.Builder(appContext)
        .setEnable(true)
        .build();

// Include your existing VOD settings and application details.
Config config = new Config.Builder()
        .setApplicationContext(appContext)
        .setAppID(appId)
        .setAppName(appName)
        .setAppVersion(appVersion)
        .setAppChannel(appChannel)
        .setLicenseUri(licenseUri)
        .setVodConfig(vodBuilder.build())
        .setBizType(BIZ_TYPE_VOD)
        .setLogConfig(logConfig)
        .build();

Env.start(config);
```


For the complete initialization flow, see [Initialize the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk#3334c95d).

`setEnable(true)` enables both local log file recording and server\-side task polling. `setEnable(false)` disables both. The SDK first stores logs locally and uploads them only when the server sends a task matching the device and time range. Logs are therefore not necessarily uploaded immediately after retrieval is enabled.

Log retrieval covers Engine, Player, MDL, and Playlist Cache. You do not need to register a separate retrieval callback for each module.

<span id="optional-configuration"></span>
### Optional configuration

For the default configuration, only `setEnable(true)` is needed. You can also configure the device ID, log path, capacity, retention period, and log level.

```Java
LogConfig logConfig = new LogConfig.Builder(appContext)
        .setEnable(true)
        .setDeviceID(deviceId)
        .setLogPath(logRootPath)
        .setMaxLogSizeM(100)
        .setSingleLogSizeM(2)
        .setLogExpireTimeS(7 * 24 * 60 * 60)
        .setLogLevel(LogConfig.LogLevel.Debug)
        .build();
```



|Method |Description |
|---|---|
|`setDeviceID(String)` |Sets the device ID. Uses the AppLog DID if omitted. |
|`setLogPath(String)` |Sets the root log directory. Uses the SDK's default directory if omitted. |
|`setMaxLogSizeM(int)` |Sets the total log capacity in MB. Default: `100`. |
|`setSingleLogSizeM(int)` |Sets the maximum size of an individual log file in MB. Default: `2`. |
|`setLogExpireTimeS(int)` |Sets log retention in seconds. Default: 7 days. |
|`setLogLevel(int)` |Sets the minimum log level using `LogConfig.LogLevel` constants: `Verbose`, `Debug`, `Info`, `Warning`, `Error`, or `None`. `None` disables new log writes. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Set <code>setLogConfig()</code>, the log path, device ID, and capacity before the first call to <code>Env.start()</code>. After initialization, only the log level supports dynamic updates.</div>


<span id="verify-log-retrieval"></span>
### Verify log retrieval


1. Start the app and play a video.

2. Check that VOD log files have been created in the app's files directory, or in your custom log directory if configured.

3. Provide the device DID and the time range of the issue to BytePlus technical support to arrange a log retrieval task.

4. Confirm that the client receives the task and uploads the logs.

5. Check that the retrieved logs contain Engine, Player, MDL, and Cache logs.


<span id="usage-notes"></span>
### Usage notes


* The standard TTSDK AAR includes the required consumer rules. No additional JNI keep rules are needed.

* VOD and live streaming maintain separate log files and upload tasks. When both run in the same process, a small amount of shared player kernel logging may also appear in the VOD logs. This does not affect playback.
