---
title: "Flutter Player SDK: Automatic playback source refresh"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-automatic-playback-source-refresh"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip"><strong>Applicable version</strong>: byteplus_vod Flutter SDK ≥ <strong>1.50.103</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>Platforms</strong>: iOS and Android</div>


<div data-tips="true" data-tips-type="tip"><strong>Overview</strong>: When a signed playback URL expires or an HLS segment request fails, the SDK automatically asks your app for a new playback URL. Playback continues seamlessly without recreating the player or restarting playback.</div>


<span id="overview"></span>
## Overview

Automatic playback source refresh prevents playback failures caused by **signed playback URLs that have a limited validity period**. BytePlus VOD playback URLs typically contain authentication parameters, such as `auth_key` and an expiration timestamp. The URL can expire during playback in scenarios such as long\-form video playback, resuming after the app has remained in the background, or long\-running HLS playback. This can cause loading failures, playback freezes, or errors.

After you enable this feature, the SDK requests a new playback URL from your app when it detects an expired URL or a segment error. The SDK then replaces the URL without interrupting playback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Common use cases</div>



* <div data-tips="true" data-tips-type="tip">Long\-form videos or live\-stream replays whose playback duration may exceed the URL validity period</div>


* <div data-tips="true" data-tips-type="tip">Resuming playback after the app has remained in the background or the device has been locked for a long time</div>


* <div data-tips="true" data-tips-type="tip">Short\-drama and VOD feed scenarios that require continuous playback over a long period</div>


* <div data-tips="true" data-tips-type="tip">HLS (M3U8) segments that return a 4xx or 403 error because their signatures expire during playback</div>



<span id="quickstart"></span>
## Quickstart

Complete the integration in three steps: **implement the callback, register the callback, and enable the strategy before playback starts**.

```Dart
import 'package:byteplus_vod/ve_vod.dart';

// 1. Implement the URL refresh callback.
class MyUrlRefreshCallback implements TTVideoEngineUrlRefreshCallback {
  @override
  Future<dynamic> refreshUrl(TTVideoEngineUrlRequest request) async {
    // request.url / request.cacheKey / request.vid
    // Request new playback information from your app server.
    // The callback can return PlayInfoList from GetPlayInfo.
    final playInfoList = await fetchNewPlayInfoList(request.vid);
    return playInfoList;
    // Alternatively, return
    // TTVideoEngineUrlResult(url: newUrl, expireTimeInMS: ts).
  }

  @override
  void cancel() {
    // Cancel the network request in progress.
  }
}

// 2. Register the callback. We recommend doing this when the app starts
// or when the playback page opens.
TTVideoEngineSourceRefreshStrategy.setUrlRefreshCallback(
  MyUrlRefreshCallback(),
);

// 3. Enable the strategy before setting the playback source.
await player.enableSourceRefreshStrategy(enableHlsSegError: true);
await player.setMediaSource(mediaSource);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip"><strong>The call order is important</strong>: Register the callback by calling <code>setUrlRefreshCallback()</code>, and call <code>enableSourceRefreshStrategy()</code> <strong>before</strong> <code>setMediaSource()</code>. Otherwise, the strategy does not take effect for the current playback source.</div>


<span id="api-reference"></span>
## API reference

<span id="callback-interface"></span>
### Callback interface

Your app must implement the following callback interface:

```Dart
abstract class TTVideoEngineUrlRefreshCallback {
  /// Refreshes an expired URL. The callback can return
  /// TTVideoEngineUrlResult, or a MediaSource, Map, or List that contains
  /// all playback URLs. The SDK automatically finds the matching URL.
  Future<dynamic> refreshUrl(TTVideoEngineUrlRequest request);

  /// Cancels the refresh operation in progress.
  void cancel();
}
```


<span id="request-and-result-models"></span>
### Request and result models


|Type |Field |Description |
|---|---|---|
|`TTVideoEngineUrlRequest` |`url` (String) |The expired playback URL. |
||`cacheKey` (String) |The cache key associated with the URL. |
||`vid` (String?) |The video ID associated with the playback source. This field may be empty. |
|`TTVideoEngineUrlResult` |`url` (String) |The new playback URL. |
||`expireTimeInMS` (int) |The expiration time of the new URL as a timestamp. For details, see [Timestamp unit for expireTimeInMS](https://docs.byteplus.com/en/docs/25/113721#expiretimeinms-unit). |


<span id="ttvideoenginesourcerefreshstrategy-static-methods"></span>
### TTVideoEngineSourceRefreshStrategy static methods


|Method |Description |
|---|---|
|`init()` |Initializes the channel handler. The SDK automatically initializes it when another method is called for the first time, so you generally do not need to call this method. |
|`setUrlRefreshCallback(cb)` |Registers the URL refresh callback. This method is required. |
|`clearUrlRefreshCallback()` |Clears the URL refresh callback. |
|`setGenerateFileKeyCallback(cb)` |Registers an HLS cache key generation callback. This method is optional. For details, see [Generate HLS cache keys](https://docs.byteplus.com/en/docs/25/113721#generate-hls-cache-keys-optional). |
|`clearGenerateFileKeyCallback()` |Clears the HLS cache key generation callback. |


<span id="vodplayerflutter-methods"></span>
### VodPlayerFlutter methods

```Dart
/// Enables automatic playback source refresh.
/// [enableHlsSegError] specifies whether to handle HLS segment errors.
/// The default value is true.
/// Call this method before setMediaSource().
Future<void> enableSourceRefreshStrategy({bool enableHlsSegError = true});

/// Disables automatic playback source refresh.
Future<void> disableSourceRefreshStrategy();
```



* **enableHlsSegError**: When this parameter is enabled, an error caused by an expired signature on an HLS (M3U8) segment also triggers a refresh. You can disable it for non\-HLS sources such as MP4 files.


<span id="return-values-of-refreshurl"></span>
## Return values of refreshUrl

The SDK normalizes the value returned by `refreshUrl()` to `{url, expireTimeInMS}`. The callback supports the following return types:


|Return type |Behavior |
|---|---|
|`TTVideoEngineUrlResult` |The SDK directly uses the URL and expiration time in the object. |
|`Map` containing `url` and `expireTimeInMS` or `expireInMS` |The SDK directly uses the URL in the map. |
|`TTVideoEngineMediaSource` or a `Map` containing complete playback information |The SDK matches a new URL to the path of the expired URL. |
|`List`, such as PlayInfoList |The SDK checks each item for a matching path and uses the first matching URL. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Recommended approach</div>


<div data-tips="true" data-tips-type="tip">Your app can return <code>PlayInfoList</code> from the BytePlus VOD <a href="https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a> response, or return the entire response without selecting a stream. The SDK automatically matches the path of the expired URL to the same resolution in the new playback information.</div>


<span id="url-matching-logic"></span>
### URL matching logic


* The SDK removes the query string from the expired URL and uses its **path** to find a URL with the same path in the new playback information.

* The SDK supports multiple field names, including `urls`, `MainPlayUrl`, `BackupPlayUrl`, `expires`, `urlExpiredTimes`, `MainUrlExpire`, `BackupUrlExpire`, `playInfoList`, and `PlayInfoList`, and supports data nested in `Result`.

* The SDK uses the `a=0` query parameter in the expired URL to determine whether to prefer `MainPlayUrl` or `BackupPlayUrl`.


<span id="expiretimeinms-unit"></span>
### Timestamp unit for expireTimeInMS

The SDK supports expiration timestamps in both seconds and milliseconds. A value less than `100000000000` is treated as seconds and automatically multiplied by 1,000. Therefore, the SDK can parse both second\-level timestamps, such as `1875780093`, and millisecond\-level timestamps.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When the callback returns <code>TTVideoEngineUrlResult</code> or a <code>Map</code>, <code>expireTimeInMS</code> is required. If it is missing, the SDK throws a <code>TTError</code>. When the callback returns a complete PlayInfoList, the SDK reads the expiration time from fields such as <code>MainUrlExpire</code>.</div>


<span id="generate-hls-cache-keys-optional"></span>
## Generate HLS cache keys (optional)

By default, the cache key of an HLS TS segment is derived from its complete URL. If authentication parameters change, the same segment may be treated as a different file, reducing the cache hit rate. You can register a `generateFileKey` callback that removes authentication parameters and generates a stable cache key. This keeps the cache key unique and reusable when a signature changes.

```Dart
typedef GenerateFileKeyCallback = String Function(
    String url, String fileKey, Map<String, String> extraInfo);

String myGenerateFileKey(
    String url, String fileKey, Map<String, String> extraInfo) {
  final uri = Uri.parse(url);
  final params = Map<String, String>.from(uri.queryParameters)
    ..removeWhere((k, v) =>
        k.toLowerCase().contains('token') ||
        k.toLowerCase().contains('sign') ||
        k.toLowerCase().contains('auth'));
  final cleanUrl = uri.replace(queryParameters: params).toString();
  return cleanUrl.hashCode.toString(); // Use a stable hash such as MD5 in production.
}

// Register the optional callback.
TTVideoEngineSourceRefreshStrategy.setGenerateFileKeyCallback(myGenerateFileKey);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This callback is optional. If you do not register it, the SDK uses its default cache key generation method. We recommend implementing the callback if your authentication parameter names are fixed and known, to improve the cache hit rate.</div>


<span id="faq"></span>
## FAQ


|Question |Troubleshooting |
|---|---|
|Why is the callback never triggered? |Check that you have registered the callback by calling `setUrlRefreshCallback()`, called `enableSourceRefreshStrategy()` before `setMediaSource()`, and encountered an expired URL or segment error. Filter logs by the `Flutter_SourceRefresh` tag to inspect the process. |
|Why does the SDK report “Invalid refreshUrl result”? |The return value is unsupported, or the SDK cannot find a URL whose path matches the expired URL in the returned playback information. Make sure that the new and expired URLs have the same path and represent the same resolution. |
|Why does the SDK report “expireTimeInMS is required”? |A `TTVideoEngineUrlResult` or `Map` return value must include an expiration time. Alternatively, return the complete PlayInfoList so that the SDK can read the expiration time. |
|Must I enable HLS segment error handling for an MP4 source? |No. Set `enableHlsSegError` to `false` for a non\-HLS source. |
|How do I disable this feature? |Call `player.disableSourceRefreshStrategy()`. If you no longer need the callback, also call `clearUrlRefreshCallback()`. |
