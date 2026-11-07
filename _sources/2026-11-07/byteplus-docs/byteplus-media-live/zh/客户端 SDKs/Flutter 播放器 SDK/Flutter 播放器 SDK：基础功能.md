---
title: "Flutter 播放器 SDK：基础功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-basic-features-zh-CN"
---

本主题介绍如何实现 Flutter 播放器 SDK 的基础功能。

## 前提条件

你已集成并初始化 Flutter 播放器 SDK。更多信息，请参见[集成 Flutter 播放器 SDK](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)和[初始化 Flutter 播放器 SDK](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter)。

## 创建播放器并配置渲染视图

如需使用 Flutter 播放器 SDK，你必须先创建播放器。如需在播放器中显示视频，你必须配置渲染视图。

```Dart
// 创建播放器。以下示例创建的播放器宽度等于屏幕宽度，高度等于屏幕高度的 9/16。 
VeLivePlayer manager = await VeLivePlayer.createManager();

@override
Widget build(BuildContext context) {
  return Scaffold(
    body: Container(
      height: MediaQuery.of(context).size.height * 9 / 16,
      width: MediaQuery.of(context).size.width,
      // 配置渲染视图。
      child: VeliveFlutterPlayerView(manager: manager),
    ),
  );
}
```

## 初始化播放器设置

创建播放器后，你可以使用 `VeLivePlayerConfiguration` 初始化其设置。下表列出了详细参数。

|Parameter |Type |Description |
|---|---|---|
|enableSei |boolean |是否启用补充增强信息（SEI）消息解析。默认值为 `false`。取值：<br><br><br>* `true`：启用。<br><br>* `false`：禁用。<br><br><br>> **说明**<br><br><br>> SEI 消息是与视频帧同步的数据通道，通常用于在特定时间点显示互动内容，例如问答、弹幕和虚拟道具，为观众提供更丰富的互动体验。<br> |
|enableHardwareDecode |boolean |是否启用硬件解码。默认值为 `true`。取值：<br><br><br>* `true`：启用。如果硬件解码失败，播放器会自动切换到软件解码。<br><br>* `false`：禁用。 |
|enableLiveDNS |boolean |是否启用本地 DNS 预解析。默认值为 `false`。取值：<br><br><br>* `true`：启用。启用本地 DNS 预解析可以缩短起播时间。<br><br>* `false`：禁用。<br><br><br>> **说明**<br><br><br>> 预解析期间的问题可能影响播放器的正常运行。<br> |
|enableStatisticsCallback |boolean |是否启用播放信息的周期性回调。默认值为 `false`。取值：<br><br><br>* `true`：启用。<br><br>* `false`：禁用。 |
|statisticsCallbackInterval |int |播放信息周期性回调的时间间隔。单位为秒。默认值为 `5`。 |
|networkTimeoutMs |int |网络超时时间。单位为毫秒。默认值为 `5000`。<br><br>如果网络请求在超时时间内未收到服务器响应，则认为请求失败。 |
|retryIntervalTimeMs |int |重试间隔。单位为毫秒。默认值为 `5000`。<br><br>直播期间，如果网络错误或类似问题导致中断，播放器会立即尝试重试。重试失败后，播放器会按每个重试间隔再次重试。<br><br>> **说明**<br><br><br>> 此参数仅在没有备用流时生效。如果存在备用流，发生网络错误或类似问题时，播放器会直接切换到备用流并继续播放。<br> |
|retryMaxCount |int |播放器发生网络连接错误时的最大重试次数。默认值为 `5`。值 `0` 表示禁用播放器内部重试机制。 |

```Dart
// 初始化播放器设置。以下示例启用了 SEI 消息解析和硬件解码。
VeLivePlayerConfiguration configuration = await VeLivePlayerConfiguration(
      enableSei: true
      enableHardwareDecode: true
    );
await manager.setConfig(configuration);    
```

## 配置播放 URL

配置支持 RTM、FLV 和 HLS 直播协议的播放 URL。

```Dart
// 通过 URL 播放。
String playUrl = "http://pull.example.com/live/stream.flv"
// 配置播放 URL。
manager.setPlayUrl(playUrl)
```

> **说明**

> 如需为播放器配置多个播放 URL，以便在播放期间切换，请使用 `setPlayStreamData` 方法。此方法支持主备流和自适应码率（ABR）功能。更多信息，请参见 [Flutter 播放器 SDK：高级功能](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features)。

## 开始播放

```Dart
Future<void> play();
```

## 检查播放器是否正在播放

```Dart
Future<bool?> isPlaying();
```

## 暂停播放

```Dart
Future<void> pause();
```

> **说明**

> 直播期间，暂停和停止播放的效果相同。如果在暂停播放后再次调用 `play` 方法，播放器会重新拉流。

## 停止播放

```Dart
Future<void> stop();
```

## 销毁播放器

播放停止后调用此方法，以销毁播放器并释放其关联内存。

```Dart
Future<void> destroy();
```

## 设置视频缩放模式

你可以使用播放器的 `setRenderFillMode` 方法设置视频缩放模式。播放器支持以下视频缩放模式。

|Video Scaling Mode |Description |
|---|---|
|aspectfill |保持视频的原始宽高比并填充播放器。如果视频宽高比与播放器宽高比不同，超出播放器边界的视频区域将被裁剪，这可能导致画面显示不完整。 |
|aspectfit |保持视频的原始宽高比，直到视频在播放器内完整显示。如果视频宽高比与播放器宽高比不同，未被视频填充的区域将显示为黑色。 |
|fullfill |视频完全填充播放器，但视频宽高比可能会变化。 |

以下示例代码设置视频缩放模式。

```Dart
Future<void> setRenderFillMode(VeLivePlayerFillMode fillMode);
```

## 静音和取消静音播放

设置播放是否静音。默认情况下，播放未静音。

```Dart
Future<void> setMute(bool mute);
```

## 获取播放是否静音

```Dart
Future<bool?> isMute();
```

## 设置视频旋转角度

```Dart
enum VeLivePlayerRotation {
  // 禁用旋转。
  rotation0,
  // 顺时针旋转 90 度。
  rotation90,
  // 顺时针旋转 180 度。
  rotation180,
  // 顺时针旋转 270 度。
  rotation270,
}

Future<void> setRenderRotation(VeLivePlayerRotation rotation);
```

## 配置事件监听器

你可以通过配置事件监听器接收播放器内部状态的信息，包括播放状态、错误信息、音视频首帧回调和周期性统计数据。示例代码如下。

1. 配置播放器回调。

   ```Dart
   Future<void> setObserver(VeLivePlayerObserver observer);
   ```

2. 处理播放器回调。

   ```Dart
     // 当播放器遇到错误时触发此回调。
     void Function(VeLivePlayerError error)? onError;
     
     // 当首个视频帧成功渲染时触发此回调。成功重试后渲染的首个视频帧也适用。
     void Function(bool isFirstFrame)? onFirstVideoFrameRender;
     
     // 当首个音频帧成功渲染时触发此回调。成功重试后渲染的首个音频帧也适用。
     void Function(bool isFirstFrame)? onFirstAudioFrameRender;
     
     // 当分辨率发生变化时触发此回调。
     void Function(VeLivePlayerResolution resolution, VeLivePlayerError? error, VeLivePlayerResolutionSwitchReason reason)? onResolutionSwitch;
     
     // 当播放卡顿开始时触发此回调。
     void Function()? onStallStart;
     
     // 播放卡顿结束回调。当音频缓冲区满足播放条件并开始播放时触发此回调。
     void Function()? onStallEnd;
     
     // 当视频宽度或高度发生变化时触发此回调。
     void Function(int width, int height)? onVideoSizeChanged;
     
     // 当视频渲染卡顿发生时触发此回调。
     void Function(int stallTime)? onVideoRenderStall;
     
     // 当音频渲染卡顿发生时触发此回调。
     void Function(int stallTime)? onAudioRenderStall;
     
     // 当播放状态发生变化时触发此回调。
     void Function(VeLivePlayerStatus status)? onPlayerStatusUpdate;
     
     // 周期性回调，提供播放统计信息，例如当前播放 URL、码率和帧率。
     void Function(VeLivePlayerStatistics statistics)? onStatistics;
     
     // 当 SDK 接收到 SEI 消息时触发此回调。
     void Function(String message)? onReceiveSeiMessage;
     
     // 当主备流切换时触发此回调。
     void Function(VeLivePlayerStreamType streamType, VeLivePlayerError? error)? onMainBackupSwitch;
   ```

## 获取 SDK 版本

```Dart
static Future<String?> getVersion();
```

## 设置日志级别

设置打印到控制台的日志级别。

```Dart
enum VeLivePlayerLogLevel {
  // 输出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 级别的日志。
  verbose,
  // 输出 DEBUG、INFO、WARNING 和 ERROR 级别的日志。
  debug,
  // 输出 INFO、WARNING 和 ERROR 级别的日志。
  info,
  // 输出 WARNING 和 ERROR 级别的日志。
  warn,
  // 输出 ERROR 级别的日志。
  error,
  // 禁用日志输出。
  none,
}

static Future<void> setLogLevel(VeLivePlayerLogLevel level);
```
