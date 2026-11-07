---
title: "React Native 拉流 SDK：回调"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback-zh-CN"
---

<span id="veliveplayerobserver"></span>
## VeLivePlayerObserver

类型：`interface`

拉流播放器观察者。

<span id="c107d3ac"></span>
### onError

当播放器发生错误时触发。

**类型**

```TypeScript
((player: VeLivePlayer, error: VeLivePlayerError) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **error**


类型：`VeLivePlayerError`

错误信息。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError)。

<span id="e161397d"></span>
### onFirstVideoFrameRender

在回放开始或回放过程中重试后渲染首帧视频时触发。

**类型**

```TypeScript
((player: VeLivePlayer, isFirstFrame: boolean) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **isFirstFrame**


类型：`boolean`

该视频帧是否为回放开始时渲染的首帧视频。

```Plain Text
  * true：该视频帧为回放开始时渲染的首帧视频；
  * false：该视频帧为回放过程中重试后渲染的首帧视频。
```


<span id="4454587f"></span>
### onFirstAudioFrameRender

在回放开始或回放过程中重试后渲染首帧音频时触发。

**类型**

```TypeScript
((player: VeLivePlayer, isFirstFrame: boolean) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **isFirstFrame**


类型：`boolean`

该音频帧是否为回放开始时渲染的首帧音频。

```Plain Text
  * true：该音频帧为回放开始时渲染的首帧音频；
  * false：该音频帧为回放过程中重试后渲染的首帧音频。
```


<span id="4d9fbfd7"></span>
### onStallStart

当回放卡顿开始时触发。

**类型**

```TypeScript
((player: VeLivePlayer) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。

<span id="2976e8f1"></span>
### onStallEnd

当回放卡顿结束，即音频缓冲足够后恢复播放时触发。

**类型**

```TypeScript
((player: VeLivePlayer) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。

<span id="8c25e99c"></span>
### onVideoRenderStall

当视频渲染发生卡顿时触发。

**类型**

```TypeScript
((player: VeLivePlayer, stallTime: number) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **stallTime**


类型：`number`

卡顿时长，单位为毫秒。

<span id="6188cc0f"></span>
### onAudioRenderStall

当音频渲染发生卡顿时触发。

**类型**

```TypeScript
((player: VeLivePlayer, stallTime: number) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **stallTime**


类型：`number`

卡顿时长，单位为毫秒。

<span id="f370517e"></span>
### onResolutionSwitch

当视频分辨率发生变化时触发。

**类型**

```TypeScript
((player: VeLivePlayer, resolution: VeLivePlayerResolution, error: VeLivePlayerError, reason: VeLivePlayerResolutionSwitchReason) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **resolution**


类型：`VeLivePlayerResolution`

更新后的分辨率。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerResolution)。


* **error**


类型：`VeLivePlayerError`

分辨率切换过程中是否发生错误。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError)。


* **reason**


类型：`VeLivePlayerResolutionSwitchReason`

分辨率切换原因。详情请参见 [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerResolutionSwitchReason)。

<span id="c146e694"></span>
### onVideoSizeChanged

当视频尺寸发生变化时触发。

**类型**

```TypeScript
((player: VeLivePlayer, width: number, height: number) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **width**


类型：`number`

更新后的视频宽度，单位为像素。


* **height**


类型：`number`

更新后的视频高度，单位为像素。

<span id="ab9560b3"></span>
### onReceiveSeiMessage

当拉流 SDK 收到 SEI 消息时触发。

**类型**

```TypeScript
((player: VeLivePlayer, message: string) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **message**


类型：`string`

SEI 消息。

<span id="08f634f6"></span>
### onMainBackupSwitch

当播放器在主流与备流之间切换时触发。

**类型**

```TypeScript
((player: VeLivePlayer, streamType: VeLivePlayerStreamType, error: VeLivePlayerError) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **streamType**


类型：`VeLivePlayerStreamType`

更新后的流类型。详情请参见 [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStreamType)。


* **error**


类型：`VeLivePlayerError`

切换原因。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError)。

<span id="330b176b"></span>
### onPlayerStatusUpdate

当回放状态发生变化时触发。

**类型**

```TypeScript
((player: VeLivePlayer, status: VeLivePlayerStatus) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **status**


类型：`VeLivePlayerStatus`

播放器更新后的状态。详情请参见 [VeLivePlayerStatus](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStatus)。

<span id="a2085fca"></span>
### onStatistics

定期触发，用于上报当前拉流地址、码率、帧率等信息。

**类型**

```TypeScript
((player: VeLivePlayer, statistics: VeLivePlayerStatistics) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **statistics**


类型：`VeLivePlayerStatistics`

回放统计信息。详情请参见 [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStatistics)。

<span id="6e424102"></span>
### onSnapshotComplete

调用截图后，截图完成时触发。

**类型**

```TypeScript
((player: VeLivePlayer, bitmap: any) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **bitmap**


类型：`any`

截图的 Bitmap 对象。

<span id="fbfd4048"></span>
### onRenderVideoFrame

播放器解码视频帧时触发。调用 [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/player-android-api-reference#veliveplayer-enablevideoframeobserver) 可开启视频帧回调。

**说明**

如果使用纹理格式进行外部渲染，建议在回调线程中渲染视频。

**类型**

```TypeScript
((player: VeLivePlayer, videoFrame: VeLivePlayerVideoFrame) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **videoFrame**


类型：`VeLivePlayerVideoFrame`

视频帧，包括像素格式、封装格式、视频宽高等信息。详情请参见 [VeLivePlayerVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerVideoFrame)。

<span id="a60df3d8"></span>
### onRenderAudioFrame

播放器解码音频帧时触发。调用 enableAudioFrameObserver 可开启音频帧回调。

**说明**

回调返回的音频数据类型为 Float32，且为大端字节序。

**类型**

```TypeScript
((player: VeLivePlayer, audioFrame: VeLivePlayerAudioFrame) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **audioFrame**


类型：`VeLivePlayerAudioFrame`

音频帧。详情请参见 [VeLivePlayerAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerAudioFrame)。

<span id="b65fb8f4"></span>
### onStreamFailedOpenSuperResolution

调用 setEnableSuperResolution 后，SDK 未能成功开启超分时触发。

**类型**

```TypeScript
((player: VeLivePlayer, error: VeLivePlayerError) => void) | undefined
```



* **参数**

   * **player**


类型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer)

触发回调函数的播放器对象。


* **error**


类型：`VeLivePlayerError`

失败原因。详情请参见 [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/byteplus-media-live/player-android-api-1317628#veliveplayererror-veliveplayererrorcode)。

<span id="bd30cb5c"></span>
## PictureInPictureManagerListener

类型：`interface`

用于监听画中画相关事件的接口，例如状态变化或用户交互。

<span id="731525d9"></span>
### onStartPictureInPicture

画中画模式启动时触发。

可通过此回调更新 UI 状态或添加分析追踪。

**类型**

```TypeScript
(() => void) | undefined
```


<span id="1dfac6bc"></span>
### onStopPictureInPicture

画中画模式退出时触发，可由用户操作或程序触发。

**类型**

```TypeScript
(() => void) | undefined
```


<span id="25914b59"></span>
### onClickPictureInPicture

 **(仅限 Android)**  画中画窗口被点击时触发。可通过此回调响应用户对画中画窗口的交互。

**类型**

```TypeScript
(() => void) | undefined
```


<span id="5922d709"></span>
### onError

画中画模式发生相关错误时触发。可通过此回调进行错误上报或降级处理。

**类型**

```TypeScript
((code: number, extraData: any) => void) | undefined
```



* **参数**

   * **code**


类型：`number`

错误码。


* 0：成功

* 1：不支持

* 2：参数无效

* 3：画中画已激活

   * **extraData**


类型：`any`

用于调试或错误处理的附加数据。
