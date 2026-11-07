---
title: "TVULiveRoomServer"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvuliveroomserver-zh-CN"
---

用于独立集成直播间组件时使用的类。

```java
public class TVULiveRoomServer
```


<span id="c1c46f81"></span>
## 成员函数

<span id="d7e92e4f"></span>
### TVULiveRoomServer

创建一个`TVULiveRoomServer`实例。

```java
public TVULiveRoomServer(Context context, long activityId, String token, int serverType)
```


**输入参数**


|名称 |类型 |描述 |
|---|---|---|
|context |Context |直播间页面的 context。 |
|activityId |Long |要加入的直播间的活动 ID。可通过调用[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN)或[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |
|token |String |加入直播间所需的授权 token。可通过调用[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)获取 token。 |
|serverType |Integer |直播间类型。<br><br>默认值：`SERVER_TYPE_LIVEROOM`。<br><br><br>* SERVER_TYPE_LIVEROOM(1)：横屏模式下的完整直播间，可绑定聊天组件、独立播放器及其他直播间组件。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">TVULiveRoomServer 实例为单例模式，即同一时间只能存在一个实例。要创建新的实例，必须先销毁当前实例。   </div><br>   <br><br>* SERVER_TYPE_PORTRAIT_LIVEROOM(2)：竖屏模式下的完整直播间，可绑定聊天组件、独立播放器及其他直播间组件。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>TVULiveRoomServer</code>实例以单例形式存在，任何时候只能有一个实例。如需新的实例，必须先销毁现有实例。   </div><br>   <br><br>* SERVER_TYPE_SINGLE(3)：带有独立播放器的直播间，仅可绑定独立播放器组件。支持同时存在多个实例，可在自有页面上展示多个独立播放器。 |


**返回值**

`TVULiveRoomServer`实例。

<span id="e5275d46"></span>
### setPlayerView

设置绑定到`TVULiveRoomServer`实例的`PlayerView`实例。

```java
public void setPlayerView(PlayerView playerView)
```


**输入参数**


|名称 |类型 |描述 |
|---|---|---|
|playerView |PlayerView |绑定到`TVULiveRoomServer`实例的[PlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/playerview-zh-CN)实例。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>前调用此方法。</div>


<span id="3068420a"></span>
### setRoomAuthMode

设置直播间的鉴权模式。

```java
public void setRoomAuthMode(TVULiveRoom.TVURoomAuthMode roomAuthMode)
```


**输入参数**


|名称 |类型 |描述 |
|---|---|---|
|roomAuthMode |TVURoomAuthMode |直播间的鉴权模式，可为`PUBLIC`或`CUSTOM`，取决于传递给[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)的`mode`值。<br><br><br>* PUBLIC：若 mode 值为 1，则参数值设置为 PUBLIC。观众以嘉宾身份加入直播间。在需要用户信息的场景（如点击评论输入框或点赞评论），必须输入昵称以完成嘉宾注册。<br><br>* CUSTOM：如果 mode 的值为 2，则将参数值设置为 CUSTOM。观众通过应用中的用户账号加入直播间，可以直接发送和点赞评论。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>之前调用此方法。</div>


<span id="fd188940"></span>
### setListener

设置直播间的监听器。

```java
public void setListener(ITVULiveRoomServerListener tVULiveRoomListener)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|tVULiveRoomListener |ITVULiveRoomServerListener |直播间的监听器，包括与直播间初始化和状态变化相关的回调。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>之前调用此方法。</div>


<span id="6f796abf"></span>
### start

启动直播间。调用此方法后，TVULiveRoomServer 实例会调用后端 API 进行鉴权并获取直播间数据。成功调用此方法后会初始化本地直播间数据。

```java
public void start()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果不再需要直播间，可以调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#9a50d0bb">closeRoom</a>方法销毁当前直播间并释放资源。</div>


<span id="187fb8f6"></span>
### play

播放视频。

```java
public void play()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>之后且在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#9a50d0bb">closeRoom</a>之前调用此方法。</div>


<span id="a4751de2"></span>
### pause

暂停视频。

```java
public void pause()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>之后且在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#9a50d0bb">closeRoom</a>之前调用此方法。</div>


<span id="fab7b98f"></span>
### onPause#{#onPause}#

暂停视频。此方法适用于直播间的 Activity 进入后台时。

```java
public void onPause()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>之后且在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#9a50d0bb">closeRoom</a>之前调用此方法。</div>


<span id="0e000da9"></span>
### onResume#{#onResume}#

恢复视频播放。此方法适用于直播间的 Activity 返回前台时。

```java
public void onResume()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>之后且在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#9a50d0bb">closeRoom</a>之前调用此方法。</div>


<span id="c789dd75"></span>
### pausePollingData

初始化成功后，TVULiveRoomServer 实例会定期轮询 BytePlus Live 控制台以更新直播间状态（如直播、回放、预告或已结束）。如不希望 TVULiveRoomServer 实例从控制台轮询直播间状态，可通过此方法暂停轮询。

```java
public void pausePollingData()
```


<span id="09a0d1e2"></span>
### continuePollingData

指示 TVULiveRoomServer 实例恢复从控制台轮询直播间状态。

```java
public void continuePollingData()
```


<span id="9a50d0bb"></span>
### closeRoom

销毁当前直播间。

```java
public void closeRoom()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">请务必在调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#6f796abf">start</a>之后调用此方法。</div>


* <div data-tips="true" data-tips-type="tip">调用此方法后，不要在 TVULiveRoomServer 实例上调用其他方法。调用此方法后，可以将 TVULiveRoomServer 实例设置为 null。</div>



<span id="82e33355"></span>
### getCommentDataManager

获取直播间消息列表的 CommentDataManager。

```Java
public CommentDataManager getCommentDataManager()
```


**返回值**


|类型 |接口行为 |
|---|---|
|CommentDataManager |直播间消息列表的管理类。更多信息请参见[CommentDataManager](https://docs.byteplus.com/docs/byteplus-livesaas/commentdatamanager-zh-CN)。 |


<span id="2323d292"></span>
### getDynamicSettings

获取直播间的 DynamicCustomSettings。可在观众加入直播间前或后调用此方法，自定义直播间相关设置。

```Java
public DynamicCustomSettings getDynamicSettings()
```


**返回值**

`DynamicCustomSettings`实例。更多信息请参见[动态自定义设置](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN)。
