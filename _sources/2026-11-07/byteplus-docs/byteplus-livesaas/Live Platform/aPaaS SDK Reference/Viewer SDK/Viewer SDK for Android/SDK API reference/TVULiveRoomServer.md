---
title: "TVULiveRoomServer"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvuliveroomserver"
---

The class used when integrating live room components independently.

```java
public class TVULiveRoomServer
```


<span id="c1c46f81"></span>
## Member Functions

<span id="d7e92e4f"></span>
### TVULiveRoomServer

Creates a `TVULiveRoomServer` instance.

```java
public TVULiveRoomServer(Context context, long activityId, String token, int serverType)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |
|activityId |Long |The activity ID of the live room to join. You can get the ID by calling [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) or [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|token |String |The authorization token required to join the live room. You can get the token by calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi). |
|serverType |Integer |The type of the live room.<br><br>Default value: `SERVER_TYPE_LIVEROOM`.<br><br><br>* SERVER_TYPE_LIVEROOM(1): A full\-featured live room in landscape mode, to which you can bind the chat component, custom player, and other live room components.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The TVULiveRoomServer instance is a singleton, meaning only one instance can exist at a time. To create a new instance, you must first destroy the current one.   </div><br>   <br><br>* SERVER_TYPE_PORTRAIT_LIVEROOM(2): A full\-featured live room in portrait mode, to which you can bind the chat component, custom player, and other live room components.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>TVULiveRoomServer</code> instance exists in singleton form, and there can be only one instance at any time. If you need a new instance, you must first destroy the existing instance.   </div><br>   <br><br>* SERVER_TYPE_SINGLE(3): A live room with a custom player, to which only the custom player component can be bound. Multiple instances are supported simultaneously, allowing you to display multiple custom players on your own page. |


**Return Value**

The `TVULiveRoomServer` instance.

<span id="e5275d46"></span>
### setPlayerView

Sets a `PlayerView` instance that is bound to the `TVULiveRoomServer` instance.

```java
public void setPlayerView(PlayerView playerView)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|playerView |PlayerView |The [PlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/playerview) instance that is bound to the `TVULiveRoomServer` instance. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call this method before calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a>.</div>


<span id="3068420a"></span>
### setRoomAuthMode

Sets the authentication mode of the live room.

```java
public void setRoomAuthMode(TVULiveRoom.TVURoomAuthMode roomAuthMode)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|roomAuthMode |TVURoomAuthMode |The authentication mode of the live room, which can be `PUBLIC` or `CUSTOM`, depending on the `mode` value passed to [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi).<br><br><br>* PUBLIC: If the mode value is 1, set the parameter value to PUBLIC. Viewers join the live room as guests. In scenarios that require user information (such as tapping the comment text box or liking comments), they must enter a nickname to complete guest registration.<br><br>* CUSTOM: If the mode value is 2, set the parameter value to CUSTOM. Viewers join the live room using their user accounts from your app, allowing them to send and like comments directly. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call this method before calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a>.</div>


<span id="fd188940"></span>
### setListener

Sets the listener of the live room.

```java
public void setListener(ITVULiveRoomServerListener tVULiveRoomListener)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|tVULiveRoomListener |ITVULiveRoomServerListener |The listener of the live room, including callbacks related to live room initialization and status changes. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call this method before calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a>.</div>


<span id="6f796abf"></span>
### start

Starts the live room. After calling this method, the TVULiveRoomServer instance will call the back\-end API to authenticate and obtain live room data. A successful call to this method initializes the local live room data.

```java
public void start()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the live room is no longer needed, you can call the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#9a50d0bb">closeRoom</a> method to destroy the current live room and release the resources.</div>


<span id="187fb8f6"></span>
### play

Plays the video.

```java
public void play()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call this method after calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a> and before calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#9a50d0bb">closeRoom</a>.</div>


<span id="a4751de2"></span>
### pause

Pauses the video.

```java
public void pause()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call this method after calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a> and before calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#9a50d0bb">closeRoom</a>.</div>


<span id="fab7b98f"></span>
### onPause#{#onPause}#

Pauses the video. This method is suitable for when the live room's Activity moves to the background.

```java
public void onPause()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call this method after calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a> and before calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#9a50d0bb">closeRoom</a>.</div>


<span id="0e000da9"></span>
### onResume#{#onResume}#

Resumes the video. This method is suitable for when the live room's Activity returns to the foreground.

```java
public void onResume()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call this method after calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a> and before calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#9a50d0bb">closeRoom</a>.</div>


<span id="c789dd75"></span>
### pausePollingData

After successful initialization, the TVULiveRoomServer instance regularly polls the BytePlus Live console to update the live room's status (e.g., live, playback, preview, or ended). If you do not want the TVULiveRoomServer instance to poll for the live room status from the console, you can use this method to pause it.

```java
public void pausePollingData()
```


<span id="09a0d1e2"></span>
### continuePollingData

Instructs the TVULiveRoomServer instance to resume polling for the live room status from the console.

```java
public void continuePollingData()
```


<span id="9a50d0bb"></span>
### closeRoom

Destroys the current live room.

```java
public void closeRoom()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Be sure to call this method after calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#6f796abf">start</a>.</div>


* <div data-tips="true" data-tips-type="tip">Do not call any other methods on the TVULiveRoomServer instance after calling this method. You can set the TVULiveRoomServer instance to null after calling this method.</div>



<span id="82e33355"></span>
### getCommentDataManager

Gets the CommentDataManager for the live room's message list.

```Java
public CommentDataManager getCommentDataManager()
```


**Return Value**


|Type |Description |
|---|---|
|CommentDataManager |The management class for the message list in the live room. For more information, see [CommentDataManager](https://docs.byteplus.com/docs/byteplus-livesaas/commentdatamanager). |


<span id="2323d292"></span>
### getDynamicSettings

Gets the DynamicCustomSettings for the live room. You can call this method either before or after viewers join the live room to customize the relevant settings of the live room.

```Java
public DynamicCustomSettings getDynamicSettings()
```


**Return Value**

The `DynamicCustomSettings` instance. For more information, see [DynamicCustomSettings](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings).
