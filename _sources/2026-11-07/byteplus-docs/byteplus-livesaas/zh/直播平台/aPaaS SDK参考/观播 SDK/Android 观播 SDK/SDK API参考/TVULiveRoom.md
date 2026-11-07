---
title: "TVULiveRoom"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN"
---

用于集成完整直播间的类，包括加入和离开直播间等功能。

```java
public class com.bytedance.live.sdk.player.TVULiveRoom
```


<span id="d6403c6d"></span>
## 成员函数

<span id="b20db0d1"></span>
### joinLiveRoom

加入完整直播间。

```java
public static void joinLiveRoom(final Context context, JoinRoomConfig joinRoomConfig)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的上下文。 |
|joinRoomConfig |JoinRoomConfig |加入完整直播间所需的配置。更多信息请参见[JoinRoomConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#4530ad0e)。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在调用此方法前，可调用<code>CustomSettings.Holder.mSettings</code>中的方法自定义直播间。更多信息请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN">mSettings</a>。</div>


<span id="9fab7a9d"></span>
### leaveLiveRoom

离开直播间并销毁当前悬浮窗。

```java
public static void leaveLiveRoom(final Context context)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的上下文。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用此方法前先调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="e8fc71ab"></span>
### destroyFloatWindow

销毁当前悬浮窗及其回放资源。建议在调用[setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#8d1bd70f)方法并检测到直播间已被销毁后调用此方法。

```java
public static void destroyFloatWindow()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用此方法前先调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="f974fe00"></span>
### manualClickFloatWindow

模拟手动点击当前悬浮窗。

```java
public static void manualClickFloatWindow()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用此方法前先调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="0f1507fb"></span>
### manualClickFloatWindowExitBtn

模拟手动点击当前悬浮窗的退出按钮。

```java
public static void manualClickFloatWindowExitBtn()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用此方法前先调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="44c0414d"></span>
### manualClickLiveRoomExitBtn

模拟手动点击直播间的退出按钮。此操作会触发与观众点击直播间退出按钮相同的行为。

```java
public static void manualClickLiveRoomExitBtn(final Context context)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的上下文。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用此方法前先调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1">joinLiveRoom</a>方法。</div>


<span id="5984565f"></span>
### clearCache

清除观众当前设备上 SDK 的所有本地缓存。本地缓存包括：


* 提醒弹窗的记录。缓存清除后，观众重新加入直播间时会再次看到弹窗。

* 认证模式为公开时，系统日历中的直播流预约记录。缓存清除后，**预约**按钮会恢复为**立即预约**，但系统日历中的事件仍然保留。

* 点播视频播放进度的记录。缓存清除后，观众重新加入直播间时，点播视频将从头开始播放。


```java
public static void clearCache(Context context)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的上下文。 |


<span id="0a6ab44b"></span>
### getCookieId

获取 SDK 本地生成的设备 ID（`deviceId`）。每个设备都有唯一的设备 ID，可用于日志查询。

```java
public static String getCookieId(Context context)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的上下文。 |


**返回值**

本地生成的设备 ID（`deviceId`）。

<span id="8982a31c"></span>
### showFloatPermissionDialogInLiveRoom

在完整直播间中显示悬浮窗权限请求对话框。此方法仅在完整直播间页面处于活动状态时生效。

```Java
public static void showFloatPermissionDialogInLiveRoom(final Context context)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的上下文。 |
