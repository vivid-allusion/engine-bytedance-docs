---
title: "TVUSinglePlayerView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvusingleplayerview-zh-CN"
---

TVUSinglePlayerView 是一个可定制的视频回放视图组件。本 API 参考详细介绍了所有可用于控制播放器的成员函数。内容涵盖初始化、基础回放控制（播放、暂停）、状态获取（可播放状态、卡顿）、布局与分辨率管理，以及针对点播（进度跳转、播放速度）和直播流（刷新、线路切换）的专属控制。

<span id="ef40d04f"></span>
## 成员函数

<span id="bf477a17"></span>
### Init

调用 `init` 方法获取 `InitConfig` 参数，并初始化独立播放器的 `TVUSinglePlayerView` 实例。

```Java
public void init(InitConfig config)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|config |[InitConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#142a3b71) |独立播放器的初始化配置。 |


<span id="615a183b"></span>
### refreshLive

刷新当前直播流。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值为 `2` 时，可调用此方法。

```Java
public void refreshLive()
```


<span id="1be9767d"></span>
### play

播放视频。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值不为 `0` 时，可调用此方法。

```java
public void play()
```


<span id="c5ee7ddf"></span>
### pause

暂停视频。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值不为 `0` 时，可调用此方法。

```java
public void pause()
```


<span id="4d7c8619"></span>
### isPlaying

获取视频是否正在播放。

```java
public boolean isPlaying()
```


**返回值**


* `true`：视频正在播放。

* `false`：视频未在播放。


<span id="3a0455cd"></span>
### getPlayableStatus

获取资源当前的可播放状态。

```java
public int getPlayableStatus()
```


**返回值**


* `0`：无可播放资源，无法调用 [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#1be9767d) 方法。

* `1`：点播视频可播放。可调用 [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#1be9767d) 方法播放视频。

* `2`：直播流可播放。可调用 [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#1be9767d) 方法播放视频。


<span id="04ae6102"></span>
### isStalling

检测视频回放是否卡顿。

```java
public boolean isStalling()
```


**返回值**


* `true`：视频正在卡顿。

* `false`：视频未卡顿。


<span id="34c994a8"></span>
### setPlayerLayoutMode

设置视频缩放模式。

```java
public void setPlayerLayoutMode(int playerLayoutMode)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|playerLayoutMode |Integer |视频缩放模式。有效值：<br><br><br>* `0`：`ImageAspectFit`。在保持原始视频长宽比的前提下，将视频缩放至适配播放器边界。视频的一个维度会与播放器的对应维度一致，另一个维度会缩小；若视频长宽比与播放器不同，则会出现黑边或白边。<br><br>* `1`：`ImageToFill`。用视频填满播放器。视频长宽比可能会被改变。<br><br>* `2`：`ImageAspectFill`。在保持原始视频长宽比的前提下，将视频缩放至填满播放器边界。若视频长宽比与播放器不一致，视频会被裁剪以适配。 |


<span id="944e752b"></span>
### getResolutions

获取当前支持的分辨率列表。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值不为 `0` 时，可调用此方法。

```java
public String[] getResolutions()
```


**返回值**

一个字符串数组，表示当前支持的分辨率。

<span id="87d359b1"></span>
### getCurResolution

获取当前选中的分辨率。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值不为 `0` 时，可调用此方法。

```java
public String getCurResolution()
```


**返回值**

一个字符串，表示当前选中的分辨率。

<span id="39974b24"></span>
### setCurResolution

设置当前视频的分辨率。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值不为 `0` 时，可调用此方法。

```java
public void setCurResolution(String resolution)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|resolution |String |分辨率。 |


<span id="5741df2b"></span>
### getCurVodPlayTime

获取当前点播视频的回放时间，单位为毫秒（ms）。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值为 `1` 时，可调用此方法。

```java
public int getCurVodPlayTime()
```


**返回值**

当前点播视频的播放进度。

<span id="73d37e7d"></span>
### seekVodTime

跳转到当前点播视频指定的播放进度。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值为 `1` 时，可调用此方法。

```java
public void seekVodTime(int timeInMills, SeekCompletionListener listener)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|timeInMills |Integer |当前点播视频中指定的播放进度。单位：ms。 |
|listener |[SeekCompletionListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#a24195f6) |完成 seek 操作时触发的回调。 |


<span id="708726e4"></span>
### getCurVodDuration

获取当前点播视频的时长。单位为 ms。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值为 `1` 时，可调用此方法。

```Java
public int getCurVodDuration()
```


**返回值**

当前点播视频的时长。

<span id="13db6157"></span>
### getCurVodPlaySpeed

获取当前点播视频的播放速度。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值为 `1` 时，可调用此方法。

```Java
public float getCurVodPlaySpeed()
```


**返回值**

当前点播视频的播放速度。该值为浮点数，范围为 (0,2]。

若未播放点播视频，则返回 `-1`。

<span id="83257226"></span>
### setMute

设置视频是否静音。

```java
public void setMute(boolean isMute)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|isMute |Boolean |指定是否静音视频。默认值为`false`。<br><br><br>* `true`：静音。<br><br>* `false`：不静音。 |


<span id="d5db245a"></span>
### setVodLoop

设置点播视频是否循环播放。当 [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd) 的返回值为 `1` 时，可调用此方法。

```java
public void setVodLoop(boolean isLoop)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|isLoop |Boolean |是否循环播放点播视频。有效值：<br><br><br>* `true`：循环播放<br><br>* `false`：不循环播放。 |


<span id="8c9860a0"></span>
### setVodPlaySpeed

设置点播视频的回放速度。当[getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd)的返回值为`1`时，可以调用此方法。

```java
public void setVodPlaySpeed(float playSpeed)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|playSpeed |Float |回放速度。取值范围：(0,2] |


<span id="b16ac95d"></span>
### setInBackground

当播放器所在页面进入或退出后台时通知播放器。

```Java
public void setInBackground(boolean inBackground)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|inBackground |Boolean |包含独立播放器的页面是否在后台运行。可选值：<br><br><br>* `true`：在后台。<br><br>* `false`：在前台。 |


<span id="b025f007"></span>
### getLiveRoomStatus

获取直播间状态。

```Java
public int getLiveRoomStatus()
```


**返回值**


* `0`：由于`TVULiveRoomServer`实例尚未启动，无法获取状态。

* `1`：直播。

* `2`：预告。

* `3`：回放。

* `4`：结束。


<span id="0afd14cd"></span>
### getCurVodVid

获取当前点播视频的 Vid（视频 ID）。适用于拥有多个回放的直播间。当[getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd)的返回值为`1`时，可以调用此方法。

```Java
public String getCurVodVid()
```


**返回值**

当前点播视频的 Vid。若未播放点播视频，则返回空字符串。

<span id="d6b57534"></span>
### getCurReplayList

获取当前回放列表。此方法适用于拥有多个回放的直播间。当[getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#3a0455cd)的返回值为`1`且[getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#b025f007)的返回值为`3`时，可以调用此方法。

```Java
public List<Replay> getCurReplayList()
```


**返回值**

当前回放列表。若直播间无回放，则返回空列表。

<span id="5cee58ed"></span>
### getCurLiveLineId

获取当前直播源 ID。此方法适用于拥有多个直播源的直播间。当[getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#b025f007)的返回值为`1`时，可以调用此方法。

```Java
public long getCurLiveLineId()
```


**返回值**

当前直播源 ID。若[getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#b025f007)的返回值不为`1`，则返回`0`。

<span id="54d87f03"></span>
### getCurLiveLineList

获取当前直播源列表。此方法适用于拥有多个直播源的直播间。当[getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#b025f007)的返回值为`1`时，可以调用此方法。

```Java
public List<PullStreamUrl> getCurLiveLineList() 
```


**返回值**

当前直播源列表。若[getLiveRoomStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN#b025f007)的返回值不为`1`，则返回空列表。

<span id="f66fc68c"></span>
### setCoverImageContainerVisibility

设置直播间封面图容器的可见性。

```Java
public void setCoverImageContainerVisibility(int visibility)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|visibility |Integer |直播间封面图容器的可见性。默认值：[ ](https://developer.android.com/reference/android/view/View#VISIBLE)[View.VISIBLE](https://developer.android.com/reference/android/view/View#VISIBLE)。 |
