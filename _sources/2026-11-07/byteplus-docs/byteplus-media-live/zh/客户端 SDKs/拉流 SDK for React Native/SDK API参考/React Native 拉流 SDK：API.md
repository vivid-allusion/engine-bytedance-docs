---
title: "React Native 拉流 SDK：API"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-CN"
---

<span id="veliveplayer"></span>
## VeLivePlayer

类型：`class`

直播播放器。

<span id="f0fdefd0"></span>
### setConfig()

初始化播放器，并配置是否开启 SEI 消息、硬解、本地 DNS 预取等其他配置项。

**Note**

在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) 之前，需调用此方法初始化播放器。

**类型**

```TypeScript
(config: VeLivePlayerConfiguration) => void
```



* **参数**

   * **config**


类型：`VeLivePlayerConfiguration`

播放器配置项。详情请参见 [VeLivePlayerConfiguration](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerConfiguration)。

<span id="76d86fb7"></span>
### setObserver()

设置播放器观察者，用于监听直播播放器的事件，例如回放错误或状态更新、首帧音视频渲染、分辨率切换等。

**Note**

在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play) 之前需调用此方法。

**类型**

```TypeScript
(observer: VeLivePlayerObserver) => void
```



* **参数**

   * **observer**


类型：`VeLivePlayerObserver`

播放器观察者。详情请参见 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerObserver)。

<span id="c1362d95"></span>
### setRenderFillMode()

设置播放器画面的填充模式。

**Note**


* 在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) 前调用此方法，可设置播放器的初始填充模式。

* 在回放过程中也可调用此方法动态调整填充模式。


**类型**

```TypeScript
(fillMode: VeLivePlayerFillMode) => Promise<void>
```



* **参数**

   * **fillMode**


类型：`VeLivePlayerFillMode`

SurfaceView 的填充模式。默认值为 `VeLivePlayerFillModeAspectFill`。详情请参见 [VeLivePlayerFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerFillMode)。

**返回值**

`Promise<void>`

<span id="4850159c"></span>
### setPlayUrl()

设置拉流地址。

**Note**

在调用 play 前需调用此方法。

**类型**

```TypeScript
(url: string) => void
```



* **参数**

   * **url**


类型：`string`

拉流地址。

<span id="08be74d7"></span>
### setPlayStreamData()

设置多个在线流。如需启用需要多个在线流的功能，例如自适应码率、手动分辨率切换、主流和备流等，请调用此方法。

**Note**

在调用 play 前需调用此方法。

**类型**

```TypeScript
(streamData: VeLivePlayerStreamData) => void
```



* **参数**

   * **streamData**


类型：`VeLivePlayerStreamData`

多个拉流地址的配置项。详情请参见 [VeLivePlayerStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerStreamData)。

<span id="c10943ab"></span>
### play()

开始或恢复回放。

**Note**

调用此方法后，播放器完成拉流准备和首帧渲染时均会触发 `onPlayerStatusUpdate` 回调。

**类型**

```TypeScript
() => Promise<void>
```


**返回值**

`Promise<void>`

<span id="bfe7e8f4"></span>
### pause()

暂停回放。

**Note**

调用此方法后回放暂停时，会触发 `onPlayerStatusUpdate` 回调。

**类型**

```TypeScript
() => Promise<void>
```


**返回值**

`Promise<void>`

<span id="821b628f"></span>
### stop()

停止回放。此方法不会销毁播放器。

**Note**

调用此方法后回放停止时，会触发 `onPlayerStatusUpdate` 回调。

**类型**

```TypeScript
() => Promise<void>
```


**返回值**

`Promise<void>`

<span id="2ba0cb65"></span>
### destroy()

停止回放并销毁播放器。

**类型**

```TypeScript
() => void
```


<span id="b875a31c"></span>
### switchResolution()

切换视频分辨率。

**Note**


* 在调用此方法前，请先通过 [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplaystreamdata) 设置多种分辨率。

* 调用此方法后，播放器切换到新分辨率时会触发 [onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/player-android-api-1317627#veliveplayerobserver-onresolutionswitch) 回调。


**类型**

```TypeScript
(resolution: VeLivePlayerResolution) => void
```



* **参数**

   * **resolution**


类型：`VeLivePlayerResolution`

视频分辨率。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerResolution)。

**返回值**


* true：成功；

* false：失败。


<span id="a1c9ecfc"></span>
### isPlaying()

检测播放器是否正在回放。

**类型**

```TypeScript
() => boolean
```


**返回值**

`boolean` 播放器是否正在回放。


* true：播放器正在回放；

* false：播放器未在回放。


<span id="8aae15c5"></span>
### setPlayerVolume()

设置播放器音量。

**类型**

```TypeScript
(volume: number) => void
```



* **参数**

   * **volume**


类型：`number`

音量。默认值为 `1.0`。取值范围为 [0.0, 1.0]。

<span id="8031bd6b"></span>
### setMute()

设置是否静音回放。

**类型**

```TypeScript
(mute: boolean) => void
```



* **参数**

   * **mute**


类型：`boolean`

是否静音回放。默认值为 `false`。

```Plain Text
  * true：静音；
  * false：不静音。
```


<span id="abca2b64"></span>
### isMute()

检测回放是否静音。

**类型**

```TypeScript
() => boolean
```


**返回值**

`boolean` 回放是否静音。


* true：已静音；

* false：未静音。


<span id="2b9af50b"></span>
### setProperty()

配置播放器高级设置，包括离屏渲染、最大缓冲时长、自适应码率算法等。如需进一步信息，请联系 BytePlus 技术支持。

**类型**

```TypeScript
(key: string, value: Object) => void
```



* **参数**

   * **key**


类型：`string`

高级设置的参数名称。


* **value**


类型：`Object`

高级设置的参数值。

<span id="7b8ee64b"></span>
### setRenderRotation()

设置视频的顺时针旋转角度。

**说明**


* 你可以在回放前或回放过程中更改旋转角度。

* 每次调用该方法时，播放器都会基于原始视频进行旋转。

* 当你同时对视频应用旋转和镜像时，播放器会先对视频进行镜像处理，然后再进行旋转。


**类型**

```TypeScript
(rotation: VeLivePlayerRotation) => Promise<void>
```



* **参数**

   * **rotation**


类型：`VeLivePlayerRotation`

视频的顺时针旋转角度。默认未开启旋转。详情请参见[VeLivePlayerRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerRotation)。

**返回值**

`Promise<void>`

<span id="691650f7"></span>
### setRenderMirror()

配置镜像设置。

**说明**


* 你可以在回放前或回放过程中更改镜像设置。

* 每次调用该方法时，播放器都会将镜像设置应用于原始视频。

* 当你同时对视频应用旋转和镜像时，播放器会先对视频进行镜像处理，然后再进行旋转。


**类型**

```TypeScript
(mirror: VeLivePlayerMirror) => Promise<void>
```



* **参数**

   * **mirror**


类型：`VeLivePlayerMirror`

镜像设置。默认未开启镜像。详情请参见[VeLivePlayerMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerMirror)。

**返回值**

`Promise<void>`

<span id="4859375d"></span>
### setEnableSuperResolution()

开启或关闭超分。在使用该功能前，你需要先联系 BytePlus [technical support](https://www.byteplus.com/en/support) 进行开通。

**说明**


* 请在收到 [onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/byteplus-media-live/1317627#veliveplayerobserver-onFirstVideoFrameRender) 回调后或回放过程中调用该方法。

* 如果由于设备型号、视频分辨率或帧率等原因，SDK 未能成功开启超分，你将收到 [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onstreamfailedopensuperresolution) 回调。


**类型**

```TypeScript
(enable: boolean) => void
```



* **参数**

   * **enable**


类型：`boolean`

是否开启超分。

<span id="42746901"></span>
### startPictureInPicture()

启动画中画模式，并在悬浮窗中显示播放器。

**类型**

```TypeScript
(aspectRatio?: number, x?: number, y?: number) => Promise<void>
```



* **参数**

   * **aspectRatio**


类型: `number`

画中画窗口的视频长宽比（宽 / 高）。


* **x**


类型: `number`

距离屏幕左上角的水平偏移（像素）。


* **y**


类型: `number`

距离屏幕左上角的垂直偏移（像素）。

**返回值**

`Promise<void>`

<span id="024a4f92"></span>
### stopPictureInPicture()

退出画中画模式。

**类型**

```TypeScript
() => Promise<void>
```


**返回值**

`Promise<void>`

<span id="26ed0a11"></span>
### isPictureInPictureSupported()

检测当前环境是否支持画中画模式。

**类型**

```TypeScript
() => boolean
```


**返回值**

`boolean` 是否支持画中画。


* true: 支持。

* false: 不支持。


<span id="c83adae8"></span>
### setPictureInPictureListener()

设置画中画相关事件的监听器，例如画中画启动、停止或异常。

**类型**

```TypeScript
(listener: PictureInPictureManagerListener) => void
```



* **参数**

   * **listener**


类型: `PictureInPictureManagerListener`

画中画事件的监听器。

<span id="09029475"></span>
### enablePictureInPicture()

 **(仅限 iOS)**  当应用进入后台时，自动开启画中画模式。

**类型**

```TypeScript
() => Promise<void>
```


**返回值**

`Promise<void>`

<span id="5623783f"></span>
### disablePictureInPicture()

 **(仅限 iOS)**  关闭自动画中画模式。

**类型**

```TypeScript
() => Promise<void>
```


**返回值**

`Promise<void>`

<span id="703db4e3"></span>
### `static` getVersion()

获取拉流 SDK 的版本号。

**类型**

```TypeScript
() => string
```


**返回值**

`string` 拉流 SDK 的版本号。

<span id="a366ca4f"></span>
### `static` setLogLevel()

设置输出日志级别。

**类型**

```TypeScript
(logLevel: VeLivePlayerLogLevel) => void
```



* **参数**

   * **logLevel**


类型：`VeLivePlayerLogLevel`

输出日志级别。详情请参见[VeLivePlayerLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerLogLevel)。
