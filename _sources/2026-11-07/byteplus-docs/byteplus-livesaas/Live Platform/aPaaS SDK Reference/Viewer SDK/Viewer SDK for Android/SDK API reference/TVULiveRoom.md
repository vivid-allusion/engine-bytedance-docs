---
title: "TVULiveRoom"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-tvuliveroom"
---

The class used when integrating a full\-featured live room, including features such as joining and leaving the live room.

```java
public class com.bytedance.live.sdk.player.TVULiveRoom
```


<span id="d6403c6d"></span>
## Member Functions

<span id="b20db0d1"></span>
### joinLiveRoom

Joins the full\-featured live room.

```java
public static void joinLiveRoom(final Context context, JoinRoomConfig joinRoomConfig)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |
|joinRoomConfig |JoinRoomConfig |The configuration required to join the full\-featured live room. For more information, see [JoinRoomConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#4530ad0e). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before calling this method, you can call methods in <code>CustomSettings.Holder.mSettings</code> to customize the live room. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings">mSettings</a>.</div>


<span id="9fab7a9d"></span>
### leaveLiveRoom

Leaves the live room and destroys the current floating window.

```java
public static void leaveLiveRoom(final Context context)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1">joinLiveRoom</a> method before calling this method.</div>


<span id="e8fc71ab"></span>
### destroyFloatWindow

Destroys the current floating window as well as its playing resources. We recommend that you call this method after calling the [setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#8d1bd70f) method and detecting that the live room has been destroyed.

```java
public static void destroyFloatWindow()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1">joinLiveRoom</a> method before calling this method.</div>


<span id="f974fe00"></span>
### manualClickFloatWindow

Simulates a manual click on the current floating window.

```java
public static void manualClickFloatWindow()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1">joinLiveRoom</a> method before calling this method.</div>


<span id="0f1507fb"></span>
### manualClickFloatWindowExitBtn

Simulates a manual click on the exit button of the current floating window.

```java
public static void manualClickFloatWindowExitBtn()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1">joinLiveRoom</a> method before calling this method.</div>


<span id="44c0414d"></span>
### manualClickLiveRoomExitBtn

Simulates a manual click on the exit button of the live room. What happens next will be the same as when a viewer clicks the exit button of the live room.

```java
public static void manualClickLiveRoomExitBtn(final Context context)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Be sure to call the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1">joinLiveRoom</a> method before calling this method.</div>


<span id="5984565f"></span>
### clearCache

Clears all local caches of the SDK on the viewer's current device. The local cache includes:


* Records of reminder pop\-up windows. After the cache is cleared, viewers will see the pop\-up window again when they rejoin the live room.

* Records of live stream bookings in the system calendar when the authentication mode is public. After the cache is cleared, the **Book** button will revert to **Book now**, but the events in the system calendar will remain.

* Records of Video on Demand (VOD) video playback progress. After the cache is cleared, VOD videos will start from the beginning when viewers rejoin the live room.


```java
public static void clearCache(Context context)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |


<span id="0a6ab44b"></span>
### getCookieId

Gets the device ID (`deviceId`) generated locally by the SDK. Each device has a unique device ID, which can be used for log queries.

```java
public static String getCookieId(Context context)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |


**Return Value**

The device ID (`deviceId`) generated locally by the SDK.

<span id="8982a31c"></span>
### showFloatPermissionDialogInLiveRoom

Displays a permission request dialog box for floating windows in the full\-featured live room. This method only takes effect when the full\-featured live room page is present.

```Java
public static void showFloatPermissionDialogInLiveRoom(final Context context)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |
