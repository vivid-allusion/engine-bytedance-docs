---
title: "Flutter Player SDK: Log retrieval"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-log-retrieval"
---

Log retrieval helps troubleshoot playback issues on a device. The SDK records logs locally and queries the server for retrieval tasks. When a task matches the device and time range, the SDK uploads the logs for BytePlus technical support to analyze. Enabling log retrieval does not immediately upload all logs.

## Prerequisites

Integrate BytePlus Flutter Player SDK `1.52.101` or later. For details, see [Integrating the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-quickstart).

## Enable log retrieval

Before the first call to `startWithConfiguration`, assign a `TTSDKLogConfiguration` to the SDK initialization configuration. The minimum configuration requires only `enable: true`; the remaining fields use the native SDK defaults.

```Dart
import 'package:byteplus_vod/ve_vod.dart';

final config = TTSDKConfiguration.defaultConfigurationWithAppIDAndLicPath(
  appID: 'YOUR_APP_ID',
  licenseFilePath: 'assets/VEVod.lic',
  channel: 'your-channel',
);
config.logConfiguration = const TTSDKLogConfiguration(enable: true);
await FlutterTTSDKManager.startWithConfiguration(config);
```

Replace the app ID and license file path with your own values. If your app already initializes the SDK, add `logConfiguration` to the existing configuration instead of initializing the SDK again.

To customize the log level or disk usage, use the following configuration before initialization:

```Dart
config.logConfiguration = const TTSDKLogConfiguration(
  enable: true,
  logLevel: TTSDKLogLevel.debug,
  maxLogSizeM: 50,
  singleLogSizeM: 5,
);
```

## Configuration parameters and default behavior

|Parameter |Description |Behavior when omitted |
|---|---|---|
|`enable` |Enables or disables local log recording and retrieval task queries. Required when creating the configuration object. |No default value; must be specified. |
|`logLevel` |Log level. Valid values: `verbose`, `debug`, `info`, `warning`, `error`, and `none`. |Uses the native SDK's default log level. |
|`logPath` |Directory for log files. |Uses the native SDK's default directory. |
|`maxLogSizeM` |Maximum total log size, in MB. |100 MB. |
|`singleLogSizeM` |Maximum size of a single log file, in MB. |2 MB. |
|`logExpireTimeS` |Log retention period, in seconds. |7 days. |
|`deviceID` |Custom device ID for log retrieval. |Uses the SDK's default device ID. |

Size and retention values must be positive integers no greater than `2147483647`. The single\-file size cannot exceed the total log size, including when an omitted field uses its default value. If specified, the log path and device ID must not be empty. Invalid configurations throw an `ArgumentError` before native SDK initialization.

* **No configuration**: When `logConfiguration` is `null`, Flutter does not override the native or server\-delivered configuration. This does not guarantee that log retrieval is enabled.

* **Explicitly enable or disable**: `enable: true` enables local log recording and retrieval task queries; `enable: false` explicitly disables them. On iOS, explicitly disabling log retrieval takes precedence over server\-delivered settings that enable it. To retain server control, leave `logConfiguration` unset.

* **Debug output**: `openAllLog()` enables debug log output and does not replace log retrieval configuration. You do not need to call `openAllLog()` to enable log retrieval.

## Request log retrieval and verify the results

1. Enable log retrieval, start the app, and reproduce the playback issue. Record the time of the issue, time zone, device operating system, and app version.

2. Obtain the device ID for retrieval. If you have not configured a custom `deviceID`, use the default ID returned by `getDeviceID()`. If the ID has not been generated yet, try again later. If you have configured a custom `deviceID`, use that value.

3. Provide the device ID, the time range of the issue, and a description of the symptoms to BytePlus technical support to arrange a retrieval task.

4. Keep the app running on the device with network access. Confirm that the device queries the task and uploads the logs, then ask technical support to verify that the logs are available on the server.

```Dart
// Obtain the default device ID after SDK initialization.
final deviceId = await FlutterTTSDKManager.getDeviceID();
```

Successful SDK initialization, local log file creation, or an app build alone does not prove that logs have been uploaded. Verify the complete process: task delivery, device queries, upload, and log availability on the server.

## FAQ

### Why are logs not uploaded immediately after I enable retrieval?

Local log recording and server\-side retrieval tasks are separate steps. Check that you have fully restarted the app, that the device ID and issue time range match the task, and that the server\-side task has been created.

### How do I disable log retrieval?

Pass `TTSDKLogConfiguration(enable: false)` before the first SDK initialization. After changing the configuration, fully exit and restart the app.

### How do I restore the SDK's default behavior?

Leave `logConfiguration` unset, then fully exit and restart the app. Restoring the default behavior does not explicitly enable log retrieval.

## Related documentation

* [Android Player SDK: Getting SDK logs](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-sdk-logs-android)

* [iOS Player SDK: Getting SDK logs](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-sdk-logs-ios)
