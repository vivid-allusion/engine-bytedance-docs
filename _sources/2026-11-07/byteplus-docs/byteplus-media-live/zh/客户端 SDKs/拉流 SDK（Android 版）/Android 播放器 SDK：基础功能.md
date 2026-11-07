---
title: "Android 播放器 SDK：基础功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-2-zh-CN"
---

本文介绍如何实现 Android 播放器 SDK 的基础功能。

## 前提条件

你已按照 [集成 Android 播放器 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android) 和 [初始化 Android 播放器 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android) 中的说明完成播放器 SDK 的集成和初始化。

## 注意事项

播放器 SDK 使用多种 Android 音频和视频 API，这些 API 在模拟器上可能无法正常工作。建议使用真机进行调试。

## 创建播放器

要实现播放器 SDK 的基础功能，必须先创建播放器。

```Java
// 创建播放器。
VeLivePlayer mLivePlayer = new VideoLiveManager(Env.getApplicationContext());
```

> **警告**

> 为确保最佳播放效果，建议为每个播放会话创建新的播放器实例，而不是复用现有实例。

## 配置播放器

使用 [VeLivePlayerConfiguration](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration) 配置播放器的初始设置，并调用 [setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig) 应用配置。请在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前完成配置。下表介绍 `VeLivePlayerConfiguration` 中的参数。

|Parameter |Type |Description |
|---|---|---|
|enableSei |boolean |是否启用字符串 SEI 消息解析。默认值为 `false`。 |
|enableBinarySei |boolean |是否启用二进制 SEI 消息解析。默认值为 `false`。启用后，播放器接收二进制 SEI 消息，并且不再触发字符串 SEI 消息回调。 |
|enableHardwareDecode |boolean |是否启用硬件解码。默认值为 `true`。启用后，如果硬件解码启动失败或在播放期间失败，播放器会自动切换到软件解码。 |
|networkTimeoutMs |int |网络超时时间，单位为毫秒。默认值为 `5000`。发送网络请求后，如果在此时间内未收到服务器响应，播放器会认为请求失败。 |
|retryIntervalTimeMs |int |重试间隔，单位为毫秒。默认值为 `5000`。如果网络错误或类似问题中断直播播放，播放器会按此间隔重试播放。 |
|retryMaxCount |int |网络连接错误后的最大重试次数。默认值为 `5`。值为 `0` 时，禁用播放器内部重试。 |
|stallRetryTimeout |long |因卡顿停止重试的超时阈值，单位为毫秒。默认值为 `10000`（10 秒）。当卡顿时长超过此阈值时，播放器会停止重试。 |
|enableLiveDNS |boolean |是否启用本地 DNS 预取。默认值为 `false`。启用本地 DNS 预取可以减少起播所需时间。<br><br>> **警告**<br><br><br>> 本地 DNS 预取过程中的错误可能会影响播放器正常运行。<br> |
|enableStatisticsCallback |boolean |是否启用播放信息的周期性回调。默认值为 `false`。 |
|statisticsCallbackInterval |int |提供播放信息的周期性回调时间间隔，单位为秒。默认值为 `5`。 |

以下示例代码展示如何配置播放器的初始设置。

```Java
// 创建 VeLivePlayerConfiguration 实例。
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
// 启用提供播放信息的周期性回调。
config.enableStatisticsCallback = true;
// 启用本地 DNS 预取。
config.enableLiveDNS = true;
// 配置播放器的初始设置。
mLivePlayer.setConfig(config);
```

## 设置播放器观察者

调用 [setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver) 设置播放器观察者，并实现 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#veliveplayerobserver) 接口，以监听播放器状态更新、错误、首个音视频帧事件和周期性播放统计信息。请在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前设置观察者。示例代码如下。

```Java
// 创建播放器观察者实例。
VeLivePlayerObserver mLivePlayerObserver = new VeLivePlayerObserver() {
        
   @Override
   public void onError(VeLivePlayer player, VeLivePlayerError error) {
      // 播放器发生错误时触发。
   }

   @Override
   public void onInfo(VeLivePlayer player, VeLivePlayerError error) {
      // 播放器遇到内部错误时触发。
   }
   
   @Override
   public void onFirstVideoFrameRender(VeLivePlayer player, boolean isFirstFrame) {
      // 渲染首个视频帧时触发。
   }

   @Override
   public void onFirstAudioFrameRender(VeLivePlayer player, boolean isFirstFrame) {
      // 渲染首个音频帧时触发。
   }

   @Override
   public void onStallStart(VeLivePlayer player) {
    // 播放卡顿开始时触发。
  }

  @Override
   public void onStallEnd(VeLivePlayer player) {
    // 播放卡顿停止时触发。
  }

  @Override
   public void onVideoRenderStall(VeLivePlayer player, long stallTime) {
    // 视频渲染卡顿时触发。
  }

  @Override
   public void onAudioRenderStall(VeLivePlayer player, long stallTime) {
    // 音频渲染卡顿时触发。
  }

  @Override
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
    // 播放器切换到其他清晰度档位时触发。
  }

  @Override
   public void onVideoSizeChanged(VeLivePlayer player, int width, int height) {
    // 视频尺寸变化时触发。
  }

  @Override
   public void onReceiveSeiMessage(VeLivePlayer player, String message) {
    // 播放器收到字符串 SEI 消息时触发。
  }

  @Override
   public void onReceiveBinarySeiMessage(VeLivePlayer player, byte[] message) {
    // 播放器收到二进制 SEI 消息时触发。启用 enableBinarySei 以接收此回调。启用后，不再触发字符串 SEI 消息回调。
  }

  @Override
   public void onMainBackupSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStreamType streamType, VeLivePlayerError error) {
    // 播放器在主备流之间切换时触发。
  }

  @Override
   public void onStreamFormatSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerFormat fromStreamFormat, VeLivePlayerDef.VeLivePlayerFormat toStreamFormat, VeLivePlayerError error, Bundle extraInfo) {
    // 播放器切换流格式时触发。
  }

  @Override
   public void onPlayerStatusUpdate(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStatus status) {
    // 播放器状态变化时触发。
  }

  @Override
   public void onPlayerStatusUpdate(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStatus status, Bundle extraInfo) {
    // 播放器状态变化时触发。extraInfo 参数提供当前播放流的补充信息。
  }

  @Override
   public void onStatistics(VeLivePlayer player, VeLivePlayerStatistics statistics) {
    // 周期性触发，用于上报播放统计信息。
  }

  @Override
   public void onSnapshotComplete(VeLivePlayer player, Bitmap bitmap) {
    // 截图完成时触发。
  }

  @Override
   public void onRenderVideoFrame(VeLivePlayer player, VeLivePlayerVideoFrame videoFrame) {
    // 播放器解码视频帧时触发。
  }

  @Override
   public void onRenderAudioFrame(VeLivePlayer player, VeLivePlayerAudioFrame audioFrame) {
    // 播放器解码音频帧时触发。
  }

  @Override
   public void onStreamFailedOpenSuperResolution(VeLivePlayer player, VeLivePlayerError error) {
    // SDK 未能启用超分辨率时触发。
  }

  @Override
   public void onStreamFailedOpenSharpen(VeLivePlayer player, VeLivePlayerError error) {
    // SDK 未能启用视频锐化时触发。
  }
};

// 设置播放器观察者。
mLivePlayer.setObserver(mLivePlayerObserver);
```

## 设置渲染视图

要让播放器显示视频，需要为视频渲染设置视图。播放器提供两种渲染视图选项：`SurfaceView` 和 `TextureView`。

|Dimension |SurfaceView |TextureView |
|---|---|---|
|Characteristics |提供独立绘制表面，并可高效渲染复杂 UI。 |作为常规视图工作，并支持动画和变换。 |
|Thread |在单独线程上绘制，不占用主线程资源。 |使用与 `Activity` 或 `Fragment` 相同的生命周期。 |
|Recommended scenarios |复杂 UI 渲染、高效绘制、游戏和类似场景。 |图像显示、动画效果，以及需要兼容常规视图的场景。 |

根据你的需求选择渲染视图，并参考以下示例代码进行配置。

### 设置 SurfaceView

1. 在布局 XML 文件中声明 `SurfaceView`。

   ```XML
   <SurfaceView
       android:id="@+id/surfaceView"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```

2. 调用 [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder)，使用 `SurfaceView` 配置视频渲染。

   ```Java
   SurfaceView surfaceView = findViewById(R.id.surfaceView);
   mLivePlayer.setSurfaceHolder(surfaceView.getHolder());
   ```

> **警告**

> 如果使用 `SurfaceView` 渲染视频帧，设备的 API 级别必须为 24 或更高。否则，可能会出现视图层级问题、动画不同步或其他问题。如果设备的 API 级别低于 24，建议使用其他渲染方法，或升级 API 级别以获得最佳播放体验。

### 设置 TextureView

1. 在布局 XML 文件中声明 `TextureView`。

   ```XML
   <TextureView
       android:id="@+id/textureView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:background="@null" />
   ```

2. 调用 [setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface)，使用 `TextureView` 配置视频渲染。

   ```Java
   TextureView textureView = findViewById(R.id.textureView);
   
   // 配置 SurfaceTexture 监听器。
   textureView.setSurfaceTextureListener(new TextureView.SurfaceTextureListener() {
   
       @Override
       public void onSurfaceTextureAvailable(SurfaceTexture surfaceTexture, int width, int height) {
          // TextureView 的 SurfaceTexture 可用时触发。
           mLivePlayer.setSurface(new Surface(surfaceTexture));
       }
       
       @Override
       public void onSurfaceTextureSizeChanged(SurfaceTexture surfaceTexture, int width, int height) { 
           // TextureView 的尺寸变化时触发。
       }
       
       @Override
       public boolean onSurfaceTextureDestroyed(SurfaceTexture surfaceTexture) {
          // SurfaceTexture 即将销毁时触发。返回 true 可让 TextureView 自动释放 SurfaceTexture。如果此方法返回 false，请调用 surfaceTexture.release() 手动释放 SurfaceTexture。
           return true;
       }
       
       @Override
       public void onSurfaceTextureUpdated(SurfaceTexture surfaceTexture) {
          // TextureView 更新时触发。    
       }
   });
   ```

## 设置播放 URL

调用 [setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) 设置单个播放 URL。该方法支持 RTMP、FLV 和 HLS 等直播协议。请将示例代码中的 URL 替换为你的实际直播播放 URL。请在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前调用此方法。示例代码如下。

```Java
String playUrl = "http://pull.example.com/live/stream.flv";
mLivePlayer.setPlayUrl(playUrl); // 设置播放 URL。
```

> **说明**

> 要配置多个播放 URL，请调用 [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata)。此方法支持 RTM 拉流、QUIC 拉流、主备流切换、多清晰度档位和自适应码率（ABR）等功能。请在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前调用此方法。更多信息，请参见 [Android 播放器 SDK：高级功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2)。

## 调整播放画面

你可以配置填充模式、镜像和旋转，以获得更好的播放体验。

### 设置填充模式

调用 [setRenderFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) 设置播放画面的填充模式。播放器支持以下填充模式。

|Fill mode |Description |
|---|---|
|VeLivePlayerFillModeAspectFit |显示完整视频帧。视频帧会按比例缩放，直到完整画面适配画布。如果视频帧宽高比与画布宽高比不同，未填充区域会显示为黑色。 |
|VeLivePlayerFillModeFullFill |使视频帧适配画布。视频帧会非等比缩放，直到填满画布。在此过程中，视频帧的宽高比可能会改变。 |
|VeLivePlayerFillModeAspectFill |用视频填满画布。视频帧会按比例缩放，直到填满画布。超出屏幕的视频帧部分会被裁剪。因此，视频帧的某些部分可能不可见。 |

```Java
// 将填充模式设置为按比例填充。
mLivePlayer.setRenderFillMode(VeLivePlayerFillModeAspectFill);
```

### 设置镜像

调用 [setRenderMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrendermirror) 设置播放画面的镜像模式。播放器支持以下镜像模式。

|Mirroring mode |Description |
|---|---|
|VeLivePlayerMirrorNone |不镜像。 |
|VeLivePlayerMirrorHorizontal |水平镜像。 |
|VeLivePlayerMirrorVertical |垂直镜像。 |

```Java
// 设置水平镜像。
mLivePlayer.setRenderMirror(VeLivePlayerMirrorHorizontal);
```

### 设置旋转角度

调用 [setRenderRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) 设置播放画面的旋转角度。播放器支持以下旋转角度。

|Rotation angle |Description |
|---|---|
|VeLivePlayerRotation0 |不旋转。 |
|VeLivePlayerRotation90 |将视频顺时针旋转 90 度。 |
|VeLivePlayerRotation180 |将视频顺时针旋转 180 度。 |
|VeLivePlayerRotation270 |将视频顺时针旋转 270 度。 |

```Java
// 将视频顺时针旋转 90 度。
mLivePlayer.setRenderRotation(VeLivePlayerRotation90);
```

## 开始播放

调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 开始播放。

```Java
mLivePlayer.play(); // 开始播放。
```

你可以调用 [isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-isplaying) 获取当前播放状态。

```Java
boolean isPlaying = mLivePlayer.isPlaying(); // 获取播放状态。
```

## 停止播放

调用 [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop) 停止播放。调用 `stop` 不会销毁播放器。

```Java
mLivePlayer.stop(); // 停止播放。
```

## 销毁播放器

停止播放后，如果你不再需要播放器，请调用 [destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy) 销毁播放器并释放其关联内存。

```Java
mLivePlayer.destroy(); // 销毁播放器并释放其关联内存。
```

## 处理应用前后台切换

默认情况下，应用进入后台后播放器会继续播放音频。要防止音频在后台继续播放，请在应用进入后台时停止播放，并在应用返回前台时恢复播放，如以下代码所示：

```Java
@Override
protected void onResume() {
    super.onResume();
    if (mLivePlayer != null) {
        mLivePlayer.play(); // 应用切换到前台时恢复播放。
    }
}
 
@Override
protected void onPause() {
    super.onPause();
    if (mLivePlayer != null) {
        mLivePlayer.stop(); // 应用切换到后台时停止播放。
    }
}
```

## 静音

调用 [setMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setmute) 将音频静音或取消静音。

```Java
mLivePlayer.setMute(true); // 静音播放。
```

你可以调用 [isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-ismute) 查询音频是否静音。

```Java
boolean isMute = mLivePlayer.isMute(); // 获取静音状态。
```

## 设置播放器音量

调用 [setPlayerVolume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayervolume) 设置播放器音量。参数指定音量大小。默认值为 `1.0`。有效范围为 `[0.0, 1.0]`。

```Java
mLivePlayer.setPlayerVolume(0.5f); // 设置播放器音量。
```

## 设置日志级别

调用 [setLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setloglevel) 设置输出到控制台的日志级别。

```Java
// 将日志级别设置为 DEBUG。将输出 DEBUG、INFO、WARNING 和 ERROR 级别的日志。
VeLivePlayer.setLogLevel(VeLivePlayerLogConfig.VeLivePlayerLogLevel.VeLivePlayerLogLevelDebug);
```
