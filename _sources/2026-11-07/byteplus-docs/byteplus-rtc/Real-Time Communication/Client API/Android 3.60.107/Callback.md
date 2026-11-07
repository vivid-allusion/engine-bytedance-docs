---
title: "Callback"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081"
---

<span id="IRTCRoomEventHandler"></span>
# IRTCRoomEventHandler

```java
public abstract class com.ss.bytertc.engine.handler.IRTCRoomEventHandler
```


Room event callback interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onLeaveRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onleaveroom) |
|void |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroomstatechanged) |
|void |[onStreamStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onstreamstatechanged) |
|void |[onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onavsyncstatechange) |
|void |[onRoomStats](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroomstats) |
|void |[onUserJoined](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserjoined) |
|void |[onUserLeave](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserleave) |
|void |[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-ontokenwillexpire) |
|void |[onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire) |
|void |[onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire) |
|void |[onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onvideopublishstatechanged) |
|void |[onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onaudiopublishstatechanged) |
|void |[onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onvideosubscribestatechanged) |
|void |[onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onaudiosubscribestatechanged) |
|void |[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onlocalstreamstats) |
|void |[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onremotestreamstats) |
|void |[onStreamSubscribed](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onstreamsubscribed) |
|void |[onAVSyncEvent](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onavsyncevent) |
|void |[onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserpublishstreamvideo) |
|void |[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserpublishstreamaudio) |
|void |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroommessagereceived) |
|void |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroombinarymessagereceived) |
|void |[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onusermessagereceived) |
|void |[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserbinarymessagereceived) |
|void |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroommessagereceived-2) |
|void |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroombinarymessagereceived-2) |
|void |[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onusermessagereceived-2) |
|void |[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserbinarymessagereceived-2) |
|void |[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onusermessagesendresult) |
|void |[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroommessagesendresult) |
|void |[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onvideostreambanned) |
|void |[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onaudiostreambanned) |
|void |[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onforwardstreamstatechanged) |
|void |[onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onforwardstreamevent) |
|void |[onNetworkQuality](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onnetworkquality) |
|void |[onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onsetroomextrainforesult) |
|void |[onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroomextrainfoupdate) |
|void |[onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroomstreamextrainfoupdate) |
|void |[onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuservisibilitychanged) |


<span id="instructions"></span>
## Instructions

<span id="IRTCRoomEventHandler-onleaveroom"></span>
### onLeaveRoom

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onLeaveRoom(RTCRoomStats stats)
```


Leave the room successfully callback.

After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) method, the SDK will stop all publishing subscription streams, and after releasing all call\-related audio & video resources, this callback will notify the user to leave the room successfully.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |RTCRoomStats |Reserved parameter. |


**Notes**


* After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) method to leave the room, if [destroy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-destroy) is called to destroy the room instance or [destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-destroyrtcengine) method is called to destroy the RTC engine immediately, this callback event will not be received.

* If the app needs to use the system audio & video device after leaving the room, it is recommended to initialize the audio & video device after receiving this callback, otherwise the initialization may fail due to the SDK occupying the audio & video device.

    &nbsp;


<span id="onroomstatechanged"></span>
### onRoomStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomStateChanged(
    String roomId,
    String uid,
    int state,
    String extraInfo
)
```


Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |Room ID. |
|uid |String |User ID. |
|state |int |Room state code.<br><br><br>&nbsp;<br><br>* 0: Join room success.<br><br>* !0: Failed to join a room, abnormal exit, room\-related warnings or errors. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#ErrorCode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-70082#WarningCode) for specific indications. |
|extraInfo |String |Extra information.<br><br>&nbsp;<br><br>`join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` means the user rejoins the room.<br><br>&nbsp;<br><br>`elapsed` indicates the time interval from calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-joinroom) to successfully joining room, in ms. |


<span id="IRTCRoomEventHandler-onstreamstatechanged"></span>
### onStreamStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onStreamStateChanged(
    String roomId,
    String uid,
    int state,
    String extraInfo
)
```


Callback on stream state changes. You will receive this callback when you receive stream relating warnings and errors.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |Room ID. |
|uid |String |User ID. |
|state |int |Room state code. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#ErrorCode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-70082#WarningCode) for specific indications. |
|extraInfo |String |Extra information. Currently unavailable. |


<span id="IRTCRoomEventHandler-onavsyncstatechange"></span>
### onAVSyncStateChange

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onAVSyncStateChange(AVSyncState state)
```


Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setmultideviceavsync) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |AVSyncState |A/V synchronization state, see [AVSyncState](https://docs.byteplus.com/en/docs/12/docs-70083#AVSyncState). |


<span id="IRTCRoomEventHandler-onroomstats"></span>
### onRoomStats

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomStats(RTCRoomStats stats)
```


Room call statistics callback.

After the user enters the room and starts the call, he receives this callback every 2s.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |RTCRoomStats |Summary statistics in the room. See [RTCRoomStats](https://docs.byteplus.com/en/docs/12/docs-70083#RTCRoomStats). |


<span id="IRTCRoomEventHandler-onuserjoined"></span>
### onUserJoined

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserJoined(UserInfo userInfo)
```


You will receive this callback in following cases:


* The remote user calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) turns visible and joins your room.

* The remote visible user is disconnected and then reconnected to your room.

* The invisible remote user in your room calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) and turns visible.

* You join the room when there are visible users in the room.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|userInfo |UserInfo |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70083#UserInfo). |


<span id="IRTCRoomEventHandler-onuserleave"></span>
### onUserLeave

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserLeave(
    String uid,
    int reason
)
```


This callback is triggered when a remote user is disconnected or turns invisible.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |ID of the user who leaves the room, or switches to invisible. |
|reason |int |Reason to leave the room:<br><br><br>&nbsp;<br><br>* 0: The remote client calls [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) to leave the room.<br><br>* 1: The remote client is disconnected because of poor network connection or expired Token.<br><br>* 2: The remote client calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) to turn invisible.<br><br>* 3: The remote user has been removed from the room by the administrator via a OpenAPI call. |


<span id="IRTCRoomEventHandler-ontokenwillexpire"></span>
### onTokenWillExpire

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onTokenWillExpire()
```


The callback is triggered when the SDK detects the joining room privilege from the Token will expires within 30s.

After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-updatetoken) to update the joining room privilege Token.

**Notes**

After a user's joining room privilege expires:


* When attempting to join a room, the user will receive [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroomstatechanged) with the error code "\-1000" indicating that the Token is invalid.

* If the user is already in the room, he/she will be removed from the room and receive [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroomstatechanged) with the error code "\-1009" indicating that the Token is expired. Remote users in the room will receive [onUserLeave](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserleave) with the reason `1` indicating that the Token is invalid.

    &nbsp;


<span id="onpublishprivilegetokenwillexpire"></span>
### onPublishPrivilegeTokenWillExpire

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onPublishPrivilegeTokenWillExpire()
```


Callback triggered 30s before the publishing privilege of the Token expires.

After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-updatetoken) to update the publishing privilege Token.

**Notes**

Once a user's publishing privilege expires:


* Either during stream publishing or when attempting to publish a stream, the user will get the notification of `kPublishStateChangeReasonNoPublishPermission` via [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onaudiopublishstatechanged).

* The publishing streams of the user will be removed, and remote users in the room will get informed via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserpublishstreamaudio).

    &nbsp;


<span id="onsubscribeprivilegetokenwillexpire"></span>
### onSubscribePrivilegeTokenWillExpire

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onSubscribePrivilegeTokenWillExpire()
```


Callback triggered 30s before the subscribing privilege of the Token expires.

After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-updatetoken) to update the subscribing privilege Token.

**Notes**

After a user's subscribing privilege expires, the user will fail to subscribe to new streams, or the subscribed streams will be removed, and he/she will receive [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onaudiosubscribestatechanged) with error code "\-1003" indicating no permission to subscribe to streams.

<span id="IRTCRoomEventHandler-onvideopublishstatechanged"></span>
### onVideoPublishStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onVideoPublishStateChanged(
    String streamId,
    StreamInfo streamInfo,
    PublishState state,
    PublishStateChangeReason reason
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onStreamStateChanged` for reporting video publishing state changes. If you have upgraded to SDK version 3.60 or later and are still using this method, please migrate to this callback.


Callback on video publishing state change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific video stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|state |PublishState |Publish state code. See [PublishState](https://docs.byteplus.com/en/docs/12/docs-70083#PublishState). |
|reason |PublishStateChangeReason |The reason for the change of the publishing state of the local video stream. See [PublishStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#PublishStateChangeReason). |


<span id="IRTCRoomEventHandler-onaudiopublishstatechanged"></span>
### onAudioPublishStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onAudioPublishStateChanged(
    String streamId,
    StreamInfo streamInfo,
    PublishState state,
    PublishStateChangeReason reason
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onStreamStateChanged` for reporting audio publishing state changes. If you have upgraded to SDK version 3.60 or later and are still using this method, please migrate to this callback.


Callback on audio publishing state change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific audio stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|state |PublishState |Publish state code. See [PublishState](https://docs.byteplus.com/en/docs/12/docs-70083#PublishState). |
|reason |PublishStateChangeReason |The reason for the change of the publishing state of the local audio stream. See [PublishStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#PublishStateChangeReason). |


<span id="IRTCRoomEventHandler-onvideosubscribestatechanged"></span>
### onVideoSubscribeStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onVideoSubscribeStateChanged(
    String streamId,
    StreamInfo streamInfo,
    SubscribeState state,
    SubscribeStateChangeReason reason
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onStreamStateChanged` and `onStreamSubscribed` for reporting the state changes of the subscription to camera\-video streams. If you have upgraded to SDK version 3.60 or later and are still using this two methods, please migrate to this callback.


Callback on state changes of the subscription to camera\-video streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific video stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|state |SubscribeState |Room state code. See [SubscribeState](https://docs.byteplus.com/en/docs/12/docs-70083#SubscribeState) for more. |
|reason |SubscribeStateChangeReason |See [SubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#SubscribeStateChangeReason) for more. |


**Notes**

You will receive this callback after calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribestreamvideo).

<span id="IRTCRoomEventHandler-onaudiosubscribestatechanged"></span>
### onAudioSubscribeStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onAudioSubscribeStateChanged(
    String streamId,
    StreamInfo streamInfo,
    SubscribeState state,
    SubscribeStateChangeReason reason
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onStreamStateChanged` and `onStreamSubscribed` for reporting the state changes of the subscription to audio streams. If you have upgraded to SDK version 3.60 or later and are still using this two methods, please migrate to this callback.


Callback on state changes of the subscription to microphone\-audio streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific audio stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|state |SubscribeState |Room state code. See [SubscribeState](https://docs.byteplus.com/en/docs/12/docs-70083#SubscribeState) for more. |
|reason |SubscribeStateChangeReason |The reason why room state changes. See [SubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#SubscribeStateChangeReason) for more. |


**Notes**

You will receive this callback after calling [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribestreamaudio).

<span id="IRTCRoomEventHandler-onlocalstreamstats"></span>
### onLocalStreamStats

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onLocalStreamStats(
    String streamId,
    StreamInfo streamInfo,
    LocalStreamStats stats
)
```


Local stream data statistics and network quality callback.

After the local user publishes the flow successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the published flow during this reference period.

Statistics are passed to the user through the callback parameters of the [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70083#LocalStreamStats) type, including the sent audio & video bit rate, sent frame rate, encoded frame rate, network quality, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific local stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|stats |LocalStreamStats |Audio & video stream and network status statistics. See [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70083#LocalStreamStats). |


<span id="IRTCRoomEventHandler-onremotestreamstats"></span>
### onRemoteStreamStats

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRemoteStreamStats(
    String streamId,
    StreamInfo streamInfo,
    RemoteStreamStats stats
)
```


Remote audio/video stream statistics and network quality callbacks for local subscriptions.

After the local user subscribes to the stream successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the subscribed stream during this reference period, including: sending audio & video bit rate, sending frame rate, encoded frame rate, network quality, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific remote stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|stats |RemoteStreamStats |Audio & video stream and network status statistics. See [RemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteStreamStats). |


<span id="IRTCRoomEventHandler-onstreamsubscribed"></span>
### onStreamSubscribed

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onStreamSubscribed(
    int stateCode,
    String userId,
    SubscribeConfig info
)
```


Callback on subscription status of media streams

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stateCode |int |Subscription status of media streams, see [SubscribeState](https://docs.byteplus.com/en/docs/12/docs-70083#SubscribeState). |
|userId |String |The ID of the user who published the stream. |
|info |SubscribeConfig |Configurations of stream subscription, see [SubscribeConfig](https://docs.byteplus.com/en/docs/12/docs-70083#SubscribeConfig). |


**Notes**

Local users will receive this callback: After calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribestreamvideo) to change the subscription status of remote media streams captured by camera/microphone.

<span id="IRTCRoomEventHandler-onavsyncevent"></span>
### onAVSyncEvent

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onAVSyncEvent(
    String roomId,
    String uid,
    AVSyncEvent eventCode
)
```


> Available since 3.60.


Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setmultideviceavsync) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |Room ID. |
|uid |String |User ID. |
|eventCode |AVSyncEvent |A/V synchronization error, see [AVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70083#AVSyncEvent). |


<span id="IRTCRoomEventHandler-onuserpublishstreamvideo"></span>
### onUserPublishStreamVideo

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserPublishStreamVideo(
    String streamId,
    StreamInfo streamInfo,
    boolean isPublish
)
```


> Available since 3.60. Since version 3.60, this callback replaces the `onUserPublishStream`, `onUserUnpublishStream`, `onUserPublishScreen`, and `onUserUnpublishScreen` methods for the functions described below. If you have upgraded to SDK version 3.60 or later and are still using these methods, please migrate to this callback.


Callback on a remote user publishing or stopping publishing video streams in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific video stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|isPublish |boolean |Whether the remote user has published the video stream.<br><br><br>* `true`: Published.<br><br>* `false`: Unpblished. |


**Notes**

You will receive this callback after a remote user publishes or stops publishing video streams in the room with [publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-publishstreamvideo). Then you can choose whether to call [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribestreamvideo) to subscribe to or unsubscribe from the streams.

<span id="IRTCRoomEventHandler-onuserpublishstreamaudio"></span>
### onUserPublishStreamAudio

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserPublishStreamAudio(
    String streamId,
    StreamInfo streamInfo,
    boolean isPublish
)
```


> Available since 3.60. Since version 3.60, this callback replaces the `onUserPublishStream` and `onUserUnpublishStream` methods for the functions described below. If you have upgraded to SDK version 3.60 or later and are still using these methods, please migrate to this callback.


Callback on a remote user publishing or stopping publishing remote microphone\-audio streams in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the stream, used to identify a specific microphone \- captured audio stream. |
|streamInfo |StreamInfo |The stream information structure, containing detailed information such as room ID and user ID. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|isPublish |boolean |Whether the remote user has published the microphone\-audio stream.<br><br><br>* `true`: Published.<br><br>* `false`: Stopped publishing/Unpublished. |


**Notes**

You will receive this callback after a remote user publishes or stops publishing media streams captured by microphone in the room with [publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-publishstreamaudio). Then you can choose whether to call [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribestreamaudio) to subscribe to or unsubscribe from the streams.

<span id="IRTCRoomEventHandler-onroommessagereceived"></span>
### onRoomMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomMessageReceived(
    String uid,
    String message
)
```


> This callback will be deprecated since version 3.64. Use [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroommessagereceived-2) instead.

> Receive a callback for broadcast messages in the room.


This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message sender. |
|message |String |The content of the received message. |


<span id="IRTCRoomEventHandler-onroombinarymessagereceived"></span>
### onRoomBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomBinaryMessageReceived(
    String uid,
    ByteBuffer message
)
```


> This callback will be deprecated since version 3.64. Use [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onroombinarymessagereceived-2) instead.

> Receives a callback for broadcast binary messages in the room.


This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message sender. |
|message |ByteBuffer |The content of the received binary message. |


<span id="IRTCRoomEventHandler-onusermessagereceived"></span>
### onUserMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserMessageReceived(
    String uid,
    String message
)
```


> This callback will be deprecated since version 3.64. Use [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onusermessagereceived-2) instead.

> Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |The user ID of the sender of the message. |
|message |String |The content of the received text message. |


<span id="IRTCRoomEventHandler-onuserbinarymessagereceived"></span>
### onUserBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserBinaryMessageReceived(
    String uid,
    ByteBuffer message
)
```


> This callback will be deprecated since version 3.64. Use [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCRoomEventHandler-onuserbinarymessagereceived-2) instead.

> Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |The user ID of the sender of the message. |
|message |ByteBuffer |The binary message content received. |


<span id="IRTCRoomEventHandler-onroommessagereceived-2"></span>
### onRoomMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomMessageReceived(
    long msgid,
    String uid,
    String message
)
```


Receive a callback for broadcast messages in the room.

This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number |
|uid |String |User ID of the message sender. |
|message |String |The content of the received message. |


<span id="IRTCRoomEventHandler-onroombinarymessagereceived-2"></span>
### onRoomBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomBinaryMessageReceived(
    long msgid,
    String uid,
    ByteBuffer message
)
```


Receives a callback for broadcast binary messages in the room.

This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number |
|uid |String |User ID of the message sender. |
|message |ByteBuffer |The content of the received binary message. |


<span id="IRTCRoomEventHandler-onusermessagereceived-2"></span>
### onUserMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserMessageReceived(
    long msgid,
    String uid,
    String message
)
```


Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number. |
|uid |String |The user ID of the sender of the message. |
|message |String |The content of the received text message. |


<span id="IRTCRoomEventHandler-onuserbinarymessagereceived-2"></span>
### onUserBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserBinaryMessageReceived(
    long msgid,
    String uid,
    ByteBuffer message
)
```


Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number. |
|uid |String |The user ID of the sender of the message. |
|message |ByteBuffer |The binary message content received. |


<span id="IRTCRoomEventHandler-onusermessagesendresult"></span>
### onUserMessageSendResult

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserMessageSendResult(
    long msgid,
    int error
)
```


After sending a point\-to\-point text or point\-to\-point binary message to a single user in the room, the message sender will receive a callback with the result of the message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |The ID of this message. |
|error |int |Text or binary message sending results. See [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70082#UserMessageSendResult) |


**Notes**

Call [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage) or [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage) interface to receive this callback.

<span id="IRTCRoomEventHandler-onroommessagesendresult"></span>
### onRoomMessageSendResult

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomMessageSendResult(
    long msgid,
    int error
)
```


Receives this callback after sending a text message or a binary message to a room with [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) or [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |The ID of this message. |
|error |int |Message sending result. See [RoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70082#RoomMessageSendResult) |


<span id="IRTCRoomEventHandler-onvideostreambanned"></span>
### onVideoStreamBanned

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onVideoStreamBanned(
    String uid,
    boolean banned
)
```


All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |Disabled/unbanned video stream user ID |
|banned |boolean |Video stream sending status<br><br><br>&nbsp;<br><br>* true: Video stream sending is disabled<br><br>* false: Video stream sending is unbanned |


**Notes**


* When the specified user in the room is banned/unbanned video stream sending, all users in the room will receive the callback.

* If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

* After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

* After the same room is disbanded and created again, the status in the room is cleared.

    &nbsp;


<span id="onaudiostreambanned"></span>
### onAudioStreamBanned

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onAudioStreamBanned(
    String uid,
    boolean banned
)
```


All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |Disabled/unbanned audio stream user ID |
|banned |boolean |Audio stream sending status<br><br><br>&nbsp;<br><br>* true: Audio stream sending is disabled<br><br>* false: Audio stream sending is unbanned |


**Notes**


* When the specified user in the room is disabled/unbanned audio stream sending, all users in the room will receive the callback.

* If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

* After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

* After the same room is disbanded and created again, the status in the room is cleared.

* If the Audio selection is enabled in the console, only the user whose stream is banned will receive this callback.

    &nbsp;


<span id="onforwardstreamstatechanged"></span>
### onForwardStreamStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onForwardStreamStateChanged(ForwardStreamStateInfo[] stateInfos)
```


Callback returning the state and errors during relaying the media stream to each of the rooms

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stateInfos |ForwardStreamStateInfo [] |Array of the state and errors of each designated room. Refer to [ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-70083#ForwardStreamStateInfo) for more information. |


<span id="IRTCRoomEventHandler-onforwardstreamevent"></span>
### onForwardStreamEvent

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onForwardStreamEvent(ForwardStreamEventInfo[] eventInfos)
```


Callback returning the events during relaying the media stream to each room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|eventInfos |ForwardStreamEventInfo [] |Array of the event of each designated room. Refer to [ForwardStreamEventInfo](https://docs.byteplus.com/en/docs/12/docs-70083#ForwardStreamEventInfo) for more information. |


<span id="IRTCRoomEventHandler-onnetworkquality"></span>
### onNetworkQuality

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onNetworkQuality(
    NetworkQualityStats localQuality,
    NetworkQualityStats[] remoteQualities
)
```


Report the network quality of the users every 2s after the local user joins the room and starts publishing or subscribing to a stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|localQuality |NetworkQualityStats |Local network quality. Refer to [NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-70083#NetworkQualityStats) for details. |
|remoteQualities |NetworkQualityStats [] |Network quality of the subscribed users. Refer to [NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-70083#NetworkQualityStats) for details. |


**Notes**

See [In-call Stats](https://docs.byteplus.com/en/docs/12/docs-106866) for more information.

<span id="IRTCRoomEventHandler-onsetroomextrainforesult"></span>
### onSetRoomExtraInfoResult

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onSetRoomExtraInfoResult(
    long taskId,
    SetRoomExtraInfoResult result
)
```


> Available since 3.52


Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setroomextrainfo) to set extra information about the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|taskId |long |The task ID of the API call. |
|result |SetRoomExtraInfoResult |See [SetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70083#SetRoomExtraInfoResult) for the setting results and reasons. |


<span id="IRTCRoomEventHandler-onroomextrainfoupdate"></span>
### onRoomExtraInfoUpdate

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomExtraInfoUpdate(
    String key,
    String value,
    String lastUpdateUserId,
    long lastUpdateTimeMs
)
```


> Available since 3.52


Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setroomextrainfo).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |String |Key of the extra information. |
|value |String |Content of the extra information. |
|lastUpdateUserId |String |The ID of the last user who updated this information. |
|lastUpdateTimeMs |long |The Unix time in ms when this information was last updated. |


<span id="IRTCRoomEventHandler-onroomstreamextrainfoupdate"></span>
### onRoomStreamExtraInfoUpdate

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onRoomStreamExtraInfoUpdate(
    String streamId,
    StreamInfo streamInfo,
    String extraInfo
)
```


> Available since 3.54


Callback used to receive the extra information set by the other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setstreamextrainfo).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID of the extra information. |
|streamInfo |StreamInfo |Stream information of the extra information. |
|extraInfo |String |Extra information. |


**Notes**

The new user who enters the room will receive the notification of all the extra information in the room.

<span id="IRTCRoomEventHandler-onuservisibilitychanged"></span>
### onUserVisibilityChanged

```java
public void com.ss.bytertc.engine.handler.IRTCRoomEventHandler.onUserVisibilityChanged(
    boolean currentUserVisibility,
    UserVisibilityChangeError errorCode
)
```


> Available since 3.54


Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|currentUserVisibility |boolean |Visibility of the current user.<br><br><br>&nbsp;<br><br>* true: Visible. The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* false: Invisible. The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |
|errorCode |UserVisibilityChangeError |Error code for setting user visibility. See [UserVisibilityChangeError](https://docs.byteplus.com/en/docs/12/docs-70083#UserVisibilityChangeError). |


<span id="IAudioEffectPlayerEventHandler"></span>
# IAudioEffectPlayerEventHandler

```java
public interface com.ss.bytertc.engine.IAudioEffectPlayerEventHandler
```


Event handler for [IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer). You must call [setEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-seteventhandler) to set the corresponding event handler to get the events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/14167#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |


<span id="instructions"></span>
## Instructions

<span id="IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged"></span>
### onAudioEffectPlayerStateChanged

```java
void com.ss.bytertc.engine.IAudioEffectPlayerEventHandler.onAudioEffectPlayerStateChanged(
    int effectId,
    PlayerState state,
    PlayerError error
)
```


Callback for audio mixing status change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effectId |int |The ID of [IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer). Set by [getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getaudioeffectplayer). |
|state |PlayerState |See [PlayerState](https://docs.byteplus.com/en/docs/12/docs-70083#PlayerState). |
|error |PlayerError |See [PlayerError](https://docs.byteplus.com/en/docs/12/docs-70083#PlayerError). |


<span id="IRTCEngineEventHandler"></span>
# IRTCEngineEventHandler

```java
public abstract class com.ss.bytertc.engine.handler.IRTCEngineEventHandler
```


Audio & video engine event callback interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onWarning](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onwarning) |
|void |[onError](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onerror) |
|void |[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onextensionaccesserror) |
|void |[onSysStats](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onsysstats) |
|void |[onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onnetworktypechanged) |
|void |[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onuserstartvideocapture) |
|void |[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onuserstopvideocapture) |
|void |[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onuserstartaudiocapture) |
|void |[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onuserstopaudiocapture) |
|void |[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlocalaudiostatechanged) |
|void |[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onremoteaudiostatechanged) |
|void |[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlocalvideostatechanged) |
|void |[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onremotevideostatechanged) |
|void |[onFirstRemoteVideoFrameRendered](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onfirstremotevideoframerendered) |
|void |[onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onfirstremotevideoframedecoded) |
|void |[onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) |
|void |[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlocalvideosizechanged) |
|void |[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onremotevideosizechanged) |
|void |[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onconnectionstatechanged) |
|void |[onAudioRouteChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudioroutechanged) |
|void |[onFirstLocalAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onfirstlocalaudioframe) |
|void |[onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onfirstremoteaudioframe) |
|void |[onLogReport](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlogreport) |
|void |[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onseimessagereceived) |
|void |[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onseistreamupdate) |
|void |[onLoginResult](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onloginresult) |
|void |[onLogout](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlogout) |
|void |[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onserverparamssetresult) |
|void |[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-ongetpeeronlinestatus) |
|void |[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) |
|void |[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) |
|void |[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) |
|void |[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) |
|void |[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) |
|void |[onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onservermessagesendresult) |
|void |[onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onnetworkdetectionresult) |
|void |[onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onnetworkdetectionstopped) |
|void |[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudiodevicestatechanged) |
|void |[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onvideodevicestatechanged) |
|void |[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudiodevicewarning) |
|void |[onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onvideodevicewarning) |
|void |[onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onrecordingstateupdate) |
|void |[onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onrecordingprogressupdate) |
|void |[onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudiorecordingstateupdate) |
|void |[onAudioMixingPlayingProgress](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudiomixingplayingprogress) |
|void |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlocalaudiopropertiesreport) |
|void |[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudioplaybackdevicetestvolume) |
|void |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onremoteaudiopropertiesreport) |
|void |[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onactivespeaker) |
|void |[onEchoTestResult](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onechotestresult) |
|void |[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-oncloudproxyconnected) |
|void |[onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onnetworktimesynchronized) |
|void |[onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onhardwareechodetectionresult) |
|void |[onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlocalproxystatechanged) |
|void |[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onstreamsyncinforeceived) |
|void |[onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onremotesnapshottakentofile) |
|void |[onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onlocalsnapshottakentofile) |
|void |[onAudioFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudioframesendstatechanged) |
|void |[onVideoFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onvideoframesendstatechanged) |
|void |[onAudioFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudioframeplaystatechanged) |
|void |[onVideoFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onvideoframeplaystatechanged) |
|void |[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onsimulcastsubscribefallback) |
|void |[onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onperformancealarms) |
|void |[onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onmixedstreamevent) |
|void |[onSingleStreamEvent](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onsinglestreamevent) |
|void |[onExperimentalCallback](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onexperimentalcallback) |


<span id="instructions"></span>
## Instructions

<span id="IRTCEngineEventHandler-onwarning"></span>
### onWarning

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onWarning(int warn)
```


A warning occurred during the SDK runtime. The SDK usually recovers automatically and warnings can be ignored.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|warn |int |Warning code. See [WarningCode](https://docs.byteplus.com/en/docs/12/docs-70082#WarningCode) |


<span id="IRTCEngineEventHandler-onerror"></span>
### onError

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onError(int err)
```


Error callback occurred.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|err |int |BigInt, see: [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#ErrorCode) for detailed definitions |


**Notes**

Error callback occurred. This callback is triggered when a network or media\-related error occurs during the

SDK runtime and cannot be automatically recovered and you may need to intervene.and you may need to intervene.

<span id="IRTCEngineEventHandler-onextensionaccesserror"></span>
### onExtensionAccessError

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onExtensionAccessError(
    String extensionName,
    String msg
)
```


> Available since 3.52


Failed to access the extension.

RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|extensionName |String |The name of extension. |
|msg |String |Error message. |


<span id="IRTCEngineEventHandler-onsysstats"></span>
### onSysStats

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onSysStats(SysStats stats)
```


Callbacks occur every 2 seconds to inform the current CPU and memory usage information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |SysStats |Cpu, memory information. See [SysStats](https://docs.byteplus.com/en/docs/12/docs-70083#SysStats) data type for details. |


<span id="IRTCEngineEventHandler-onnetworktypechanged"></span>
### onNetworkTypeChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onNetworkTypeChanged(int type)
```


SDK Current network connection type change callback. Callbacks the event when the current network connection type of the SDK changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |int |Network type.<br><br><br>&nbsp;<br><br>* \-1: Unknown.<br><br>* 0: Disconnected.<br><br>* 1: LAN.<br><br>* 2: Wi\-Fi (including hotspots).<br><br>* 3: 2G mobile network.<br><br>* 4: 3G mobile network.<br><br>* 5: 4G mobile network.<br><br>* 6: 5G mobile network. |


<span id="IRTCEngineEventHandler-onuserstartvideocapture"></span>
### onUserStartVideoCapture

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserStartVideoCapture(
    String streamId,
    StreamInfo streamInfo
)
```


The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startvideocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Video stream ID |
|streamInfo |StreamInfo |Video stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |


<span id="IRTCEngineEventHandler-onuserstopvideocapture"></span>
### onUserStopVideoCapture

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserStopVideoCapture(
    String streamId,
    StreamInfo streamInfo
)
```


The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopvideocapture).

If you don't start video capture before you publish video data, all visible user will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Video stream ID |
|streamInfo |StreamInfo |Video stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |


<span id="IRTCEngineEventHandler-onuserstartaudiocapture"></span>
### onUserStartAudioCapture

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserStartAudioCapture(
    String streamId,
    StreamInfo streamInfo
)
```


Users in the room will receive this callback when they call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startaudiocapture) to turn on audio capture.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The stream ID of the remote user who turns on audio capture |
|streamInfo |StreamInfo |Information of the remote user who turn on audio capture, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |


<span id="IRTCEngineEventHandler-onuserstopaudiocapture"></span>
### onUserStopAudioCapture

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserStopAudioCapture(
    String streamId,
    StreamInfo streamInfo
)
```


Users in the room call [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopaudiocapture) when audio capture is turned off, other users in the room will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID |
|streamInfo |StreamInfo |Stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |


<span id="IRTCEngineEventHandler-onlocalaudiostatechanged"></span>
### onLocalAudioStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLocalAudioStateChanged(
    IAudioSource audioSource,
    LocalAudioStreamState state,
    LocalAudioStreamError error
)
```


When the state of the local audio stream changes, the callback notifies the current local audio stream state.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioSource |IAudioSource |Reserved parameter |
|state |LocalAudioStreamState |The status of the local audio device. See [LocalAudioStreamState](https://docs.byteplus.com/en/docs/12/docs-70083#LocalAudioStreamState) |
|error |LocalAudioStreamError |The error code when the state of the local audio stream changes. See [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-70083#LocalAudioStreamError) |


<span id="IRTCEngineEventHandler-onremoteaudiostatechanged"></span>
### onRemoteAudioStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onRemoteAudioStateChanged(
    String streamId,
    StreamInfo streamInfo,
    RemoteAudioState state,
    RemoteAudioStateChangeReason reason
)
```


When the state of the audio stream from the remote user subscribes to changes, this callback will be received to understand the current state of the remote audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Remote Stream Information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |
|state |RemoteAudioState |Remote Audio Stream Status. See [RemoteAudioState](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteAudioState) |
|reason |RemoteAudioStateChangeReason |Remote Audio Stream Status Change Reason. See [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteAudioStateChangeReason) |


<span id="IRTCEngineEventHandler-onlocalvideostatechanged"></span>
### onLocalVideoStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLocalVideoStateChanged(
    IVideoSource videoSource,
    LocalVideoStreamState state,
    LocalVideoStreamError error
)
```


Receive this event when the state of the local video stream changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |IVideoSource |Reserved parameter |
|state |LocalVideoStreamState |Local video stream state. See [LocalVideoStreamState](https://docs.byteplus.com/en/docs/12/docs-70083#LocalVideoStreamState) |
|error |LocalVideoStreamError |Error code when local video state changes. See [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/docs-70083#LocalVideoStreamError) |


<span id="IRTCEngineEventHandler-onremotevideostatechanged"></span>
### onRemoteVideoStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onRemoteVideoStateChanged(
    String streamId,
    StreamInfo streamInfo,
    RemoteVideoState videoState,
    RemoteVideoStateChangeReason videoStateReason
)
```


When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Remote Stream Information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |
|videoState |RemoteVideoState |Remote video stream status. See [RemoteVideoState](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteVideoState) |
|videoStateReason |RemoteVideoStateChangeReason |Remote video stream status change reason. See [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteVideoStateChangeReason) |


**Notes**

The callback works for video stream captured by the camera, not for screen stream.

<span id="IRTCEngineEventHandler-onfirstremotevideoframerendered"></span>
### onFirstRemoteVideoFrameRendered

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onFirstRemoteVideoFrameRendered(
    String streamId,
    StreamInfo streamInfo,
    VideoFrameInfo frameInfo
)
```


The subscriber will receive this callback when the first frame of the receiving video stream begins to render. The following situations are included:


1. The publisher publishes video for the first time.

2. In 1, the publisher cancels the video stream after publishing and publishes it again.

3. In 1, the publisher stops video capture after publishing and restarts it. (Or when using an external source, the stream is stopped and restarted again.)

4. In 1, the subscriber cancels the video stream and subscribes to it again. (The interface includes [subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribeallstreamsvideo), [pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-pauseallsubscribedstreamvideo).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Remote Stream Information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |
|frameInfo |VideoFrameInfo |Video Frame Information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70083#VideoFrameInfo) |


<span id="IRTCEngineEventHandler-onfirstremotevideoframedecoded"></span>
### onFirstRemoteVideoFrameDecoded

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onFirstRemoteVideoFrameDecoded(
    String streamId,
    StreamInfo streamInfo,
    VideoFrameInfo frameInfo
)
```


The subscriber will receive this callback when the first frame of the receiving video stream begins to decode. The following situations are included:


1. The publisher publishes video, including the initial publication and restart after cancellation.

2. After the publisher stops video capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.

3. After the publisher publishes video, the subscriber cancels the subscription to video and then re\-subscribes to it.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Remote Stream Information, see StreamInfo |
|frameInfo |VideoFrameInfo |Video Frame Information, see VideoFrameInfo |


**Notes**


* For main stream, after joining the room, the subscriber will receive this callback only when the publisher publishes video stream for the first time.

* For screen\-sharing stream, the subscriber will receive this callback every time the publisher publishes or republishes the screen video stream.

    &nbsp;


<span id="onfirstlocalvideoframecaptured"></span>
### onFirstLocalVideoFrameCaptured

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onFirstLocalVideoFrameCaptured(
    IVideoSource videoSource,
    VideoFrameInfo frameInfo
)
```


RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |IVideoSource |Reserved parameter. |
|frameInfo |VideoFrameInfo |Video information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70083#VideoFrameInfo) |


**Notes**

For captured local video frames, you can call [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvideocanvas) or [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvideosink) to render locally.

<span id="IRTCEngineEventHandler-onlocalvideosizechanged"></span>
### onLocalVideoSizeChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLocalVideoSizeChanged(
    IVideoSource videoSource,
    VideoFrameInfo frameInfo
)
```


Callback triggered when the local preview video size or rotation information has changed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |IVideoSource |Reserved parameter. |
|frameInfo |VideoFrameInfo |Video frame information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70083#VideoFrameInfo) |


<span id="IRTCEngineEventHandler-onremotevideosizechanged"></span>
### onRemoteVideoSizeChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onRemoteVideoSizeChanged(
    String streamId,
    StreamInfo streamInfo,
    VideoFrameInfo frameInfo
)
```


Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation information changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Remote Stream Information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |
|frameInfo |VideoFrameInfo |Video Frame Information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70083#VideoFrameInfo) |


<span id="IRTCEngineEventHandler-onconnectionstatechanged"></span>
### onConnectionStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onConnectionStateChanged(
    int state,
    int reason
)
```


Callback SDK and signaling server connection status related events. Callbacks the event when the network connection state of the SDK to the signaling server changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |int |The current SDK and signaling server connection status. See [ConnectionState](https://docs.byteplus.com/en/docs/12/docs-70083#ConnectionState) |
|reason |int |For a detailed definition of the cause of the signaling server connection state change, currently not enabled fixed to \-1. |


**Notes**

Refer to [Getting Connection Status](https://docs.byteplus.com/byteplus-rtc/docs/95376) for more details.

<span id="IRTCEngineEventHandler-onaudioroutechanged"></span>
### onAudioRouteChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioRouteChanged(AudioRoute route)
```


Receive the callback when the audio route changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|route |AudioRoute |Current audio playback device. Refer to [AudioRoute](https://docs.byteplus.com/en/docs/12/docs-70083#AudioRoute) for more information. |


**Notes**


* Either of the following actions will lead to audio route switching. See [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836).

   * Connecting/Disconnecting an audio device.

   * Designating the other audio device by calling [setAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setaudioroute).

       &nbsp;


<span id="onfirstlocalaudioframe"></span>
### onFirstLocalAudioFrame

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onFirstLocalAudioFrame(IAudioSource audioSource)
```


Receive the callback when publishing local audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioSource |IAudioSource |Reserved parameter |


<span id="IRTCEngineEventHandler-onfirstremoteaudioframe"></span>
### onFirstRemoteAudioFrame

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onFirstRemoteAudioFrame(
    String streamId,
    StreamInfo streamInfo
)
```


The subscriber will receive this callback when the first frame of the receiving audio stream begins to decode. The following situations are included:


1. The publisher publishes audio, including the initial publication and restart after cancellation.

2. After the publisher stops audio capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.

3. After the publisher publishes audio, the subscriber cancels the subscription to audio and then re\-subscribes to it.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Remote Stream Information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |


**Notes**

The callback will be received when the user has just received each audio stream subscribed to in the room.

<span id="IRTCEngineEventHandler-onlogreport"></span>
### onLogReport

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLogReport(
    String logType,
    JSONObject logContent
)
```


Callback this event when logging is reported.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|logType |String |Log type. |
|logContent |JSONObject |Log content. |


<span id="IRTCEngineEventHandler-onseimessagereceived"></span>
### onSEIMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onSEIMessageReceived(
    String streamId,
    StreamInfo streamInfo,
    ByteBuffer message
)
```


Receive this callback when you receive a video frame with a SEI message sent by calling [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID of the SEI sender |
|streamInfo |StreamInfo |Stream Information of the SEI sender. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |
|message |ByteBuffer |Received SEI message content |


<span id="IRTCEngineEventHandler-onseistreamupdate"></span>
### onSEIStreamUpdate

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onSEIStreamUpdate(
    String streamId,
    StreamInfo streamInfo,
    SEIStreamUpdateEvent event
)
```


Callback about publishing status of the black frame video stream .

In a voice call scenario, when the local user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback.

You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Information about stream from the remote user, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|event |SEIStreamUpdateEvent |State of the black frame video stream, see [SEIStreamUpdateEvent](https://docs.byteplus.com/en/docs/12/docs-70083#SEIStreamUpdateEvent). |


<span id="IRTCEngineEventHandler-onloginresult"></span>
### onLoginResult

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLoginResult(
    String uid,
    int errorCode,
    int elapsed
)
```


Login result callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |Login user ID |
|errorCode |int |Login result<br><br>&nbsp;<br><br>See [LoginErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#LoginErrorCode). |
|elapsed |int |The length of time it takes from calling the [login](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-login) interface to return the result.<br><br>&nbsp;<br><br>Is in ms. |


**Notes**

This callback is received after [login](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-login) is called

<span id="IRTCEngineEventHandler-onlogout"></span>
### onLogout

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLogout(int reason)
```


Callback of logout result

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|reason |int |It describes the reason why users log out. See [LogoutReason](https://docs.byteplus.com/en/docs/12/docs-70083#LogoutReason) |


**Notes**

You will receive this callback when calling [logout](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-logout) or when the local user is kicked out because another user logs in with the same UserId.

<span id="IRTCEngineEventHandler-onserverparamssetresult"></span>
### onServerParamsSetResult

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onServerParamsSetResult(int error)
```


Set the return result of the application server parameter

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|error |int |* 200, set successfully<br><br>* != 200: Failure. Refer to [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70082#UserMessageSendResult) for details. |


**Notes**

Receive this callback after calling [setServerParams](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setserverparams).

<span id="IRTCEngineEventHandler-ongetpeeronlinestatus"></span>
### onGetPeerOnlineStatus

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onGetPeerOnlineStatus(
    String peerUserId,
    int status
)
```


The return result of querying the login status of the peer or local user

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|peerUserId |String |User ID |
|status |int |The login status of the user queried<br><br>&nbsp;<br><br>See [UserOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70083#UserOnlineStatus). |


**Notes**

You must first call [getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getpeeronlinestatus) To receive this callback.

<span id="IRTCEngineEventHandler-onusermessagereceivedoutsideroom"></span>
### onUserMessageReceivedOutsideRoom

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserMessageReceivedOutsideRoom(
    String uid,
    String message
)
```


> This callback will be deprecated in version 3.64. Please use [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) instead.

> Receive this callback when you receive a text message from an out\-of\-room user calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom)


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message sender. |
|message |String |The content of the received text message. |


<span id="IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom"></span>
### onUserBinaryMessageReceivedOutsideRoom

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserBinaryMessageReceivedOutsideRoom(
    String uid,
    ByteBuffer message
)
```


> This callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) instead.

> Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom)


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message sender. |
|message |ByteBuffer |The content of the received binary message. |


<span id="IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2"></span>
### onUserMessageReceivedOutsideRoom

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserMessageReceivedOutsideRoom(
    long msgid,
    String uid,
    String message
)
```


Receive this callback when you receive a text message from an out\-of\-room user calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number. |
|uid |String |User ID of the message sender. |
|message |String |The content of the received text message. |


<span id="IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2"></span>
### onUserBinaryMessageReceivedOutsideRoom

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserBinaryMessageReceivedOutsideRoom(
    long msgid,
    String uid,
    ByteBuffer message
)
```


This is triggered when a binary message is received from an out\-of\-room user calling [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number. |
|uid |String |User ID of the message sender. |
|message |ByteBuffer |The content of the received binary message. |


<span id="IRTCEngineEventHandler-onusermessagesendresultoutsideroom"></span>
### onUserMessageSendResultOutsideRoom

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onUserMessageSendResultOutsideRoom(
    long msgid,
    int error
)
```


Callback for the result of sending a message to a user outside the room.

Triggered after you call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom) or [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |The ID of the message.<br><br>&nbsp;<br><br>All P2P and P2Server messages share a single ID sequence. |
|error |int |Message sending result. See [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70082#UserMessageSendResult). |


<span id="IRTCEngineEventHandler-onservermessagesendresult"></span>
### onServerMessageSendResult

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onServerMessageSendResult(
    long msgid,
    int error,
    ByteBuffer message
)
```


Receives the callback after sending the message to the application server successfully.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |The ID of this message<br><br>&nbsp;<br><br>All P2P and P2Server messages share a single ID sequence. |
|error |int |Message Sending Results. See [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70082#UserMessageSendResult). |
|message |ByteBuffer |The message returned in ACK when the application server receives HTTP request. The message should not exceed 64 KB. |


**Notes**

This callback is asynchronous. You will receive this callback when you call [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendserverbinarymessage) to send a message to your application server.

<span id="IRTCEngineEventHandler-onnetworkdetectionresult"></span>
### onNetworkDetectionResult

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onNetworkDetectionResult(
    NetworkDetectionLinkType type,
    int quality,
    int rtt,
    double lostRate,
    int bitrate,
    int jitter
)
```


Pre\-call network detection result.

After successfully calling [startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startnetworkdetection), you will receive this callback for the first time in 3s and every 2s thereafter.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |NetworkDetectionLinkType |Identifies the network type as uplink/downlink. |
|quality |int |Network quality, see [NetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70083#NetworkQuality). |
|rtt |int |Network RTT in ms. |
|lostRate |double |Packet loss rate. |
|bitrate |int |Network bandwidth in kbps. |
|jitter |int |Network jitter in ms |


<span id="IRTCEngineEventHandler-onnetworkdetectionstopped"></span>
### onNetworkDetectionStopped

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onNetworkDetectionStopped(NetworkDetectionStopReason reason)
```


Network detection before the call ends

The following conditions will stop the detection and receive this callback:


1. The callback is received once after the [stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopnetworkdetection) interface is called to stop probing;

2. Upon receipt of the distal/local audio first frame, stop the probe; When the detection exceeds 3 minutes, stop detection;

3. When the detection link is disconnected for a certain time, stop detection.


Reason

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|reason |NetworkDetectionStopReason |The type of reason to stop probing, refer to [NetworkDetectionStopReason](https://docs.byteplus.com/en/docs/12/docs-70083#NetworkDetectionStopReason) |


<span id="IRTCEngineEventHandler-onaudiodevicestatechanged"></span>
### onAudioDeviceStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioDeviceStateChanged(
    String deviceID,
    AudioDeviceType deviceType,
    int deviceState,
    int deviceError
)
```


Audio device state callback, returns the state of audio capture and audio playback devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |String |Device ID |
|deviceType |AudioDeviceType |Device type. See [AudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioDeviceType). |
|deviceState |int |Device state. See [MediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceState). |
|deviceError |int |Device error. See [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceError). |


<span id="IRTCEngineEventHandler-onvideodevicestatechanged"></span>
### onVideoDeviceStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onVideoDeviceStateChanged(
    String deviceID,
    VideoDeviceType deviceType,
    int deviceState,
    int deviceError
)
```


Video device state callback, returns the state of video capture and screen capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |String |Device ID |
|deviceType |VideoDeviceType |Device type. See [VideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-70083#VideoDeviceType). |
|deviceState |int |Device state. See [MediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceState). |
|deviceError |int |Device error. See [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceError). |


<span id="IRTCEngineEventHandler-onaudiodevicewarning"></span>
### onAudioDeviceWarning

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioDeviceWarning(
    String deviceID,
    AudioDeviceType deviceType,
    int deviceWarning
)
```


Audio device warning callback. The audio devices includes audio capture devices and audio rendering devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |String |Device ID |
|deviceType |AudioDeviceType |See [AudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioDeviceType) |
|deviceWarning |int |See [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceWarning) |


<span id="IRTCEngineEventHandler-onvideodevicewarning"></span>
### onVideoDeviceWarning

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onVideoDeviceWarning(
    String deviceID,
    VideoDeviceType deviceType,
    int deviceWarning
)
```


Video device warning callback, including video capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |String |Device ID |
|deviceType |VideoDeviceType |See [VideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-70083#VideoDeviceType) |
|deviceWarning |int |See [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceWarning) |


<span id="IRTCEngineEventHandler-onrecordingstateupdate"></span>
### onRecordingStateUpdate

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onRecordingStateUpdate(
    IVideoSource videoSource,
    RecordingState state,
    RecordingErrorCode errorCode,
    RecordingInfo info
)
```


Get a callback of the local recording status.

The callback is triggered by either [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startfilerecording) or [stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopfilerecording).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |IVideoSource |Reserved parameter |
|state |RecordingState |Recording status. See [RecordingState](https://docs.byteplus.com/en/docs/12/docs-70083#RecordingState) |
|errorCode |RecordingErrorCode |Recording error code. See [RecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-70083#RecordingErrorCode) |
|info |RecordingInfo |Recording file details. See [RecordingInfo](https://docs.byteplus.com/en/docs/12/docs-70083#RecordingInfo) |


<span id="IRTCEngineEventHandler-onrecordingprogressupdate"></span>
### onRecordingProgressUpdate

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onRecordingProgressUpdate(
    IVideoSource videoSource,
    RecordingProgress progress,
    RecordingInfo info
)
```


Local recording progress callback.

This callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startfilerecording). When the recording state is normal, the system will prompt the recording progress through this callback every second.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |IVideoSource |Reserved parameter |
|progress |RecordingProgress |Recording progress. See [RecordingProgress](https://docs.byteplus.com/en/docs/12/docs-70083#RecordingProgress) |
|info |RecordingInfo |Recorded file details. See [RecordingInfo](https://docs.byteplus.com/en/docs/12/docs-70083#RecordingInfo) |


<span id="IRTCEngineEventHandler-onaudiorecordingstateupdate"></span>
### onAudioRecordingStateUpdate

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioRecordingStateUpdate(
    AudioRecordingState state,
    AudioRecordingErrorCode errorCode
)
```


When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopaudiorecording) to change the recording status, receive the callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |AudioRecordingState |See [AudioRecordingState](https://docs.byteplus.com/en/docs/12/docs-70083#AudioRecordingState). |
|errorCode |AudioRecordingErrorCode |See [AudioRecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#AudioRecordingErrorCode). |


<span id="IRTCEngineEventHandler-onaudiomixingplayingprogress"></span>
### onAudioMixingPlayingProgress

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioMixingPlayingProgress(
    int mixId,
    long progress
)
```


Callback for playback progress of mixed audio files

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mixId |int |ID of the mixing task |
|progress |long |The current playback progress (ms) of the mixed audio file |


**Notes**

After calling setAudioMixingProgressInterval to set the time interval to a value greater than 0, or calling startAudioMixing to set the time interval in AudioMixingConfigto a value greater than 0, the SDK will trigger the callback according to the set time interval.

<span id="IRTCEngineEventHandler-onlocalaudiopropertiesreport"></span>
### onLocalAudioPropertiesReport

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLocalAudioPropertiesReport(LocalAudioPropertiesInfo[] audioPropertiesInfos)
```


After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about local audio.

Local audio includes the microphone audio, the screen audio captured using RTC SDK internal mechanisms, and locally mixing audio.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioPropertiesInfos |LocalAudioPropertiesInfo [] |See [LocalAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-70083#LocalAudioPropertiesInfo). |


<span id="IRTCEngineEventHandler-onaudioplaybackdevicetestvolume"></span>
### onAudioPlaybackDeviceTestVolume

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioPlaybackDeviceTestVolume(int volume)
```


Notification on the playing volume during the test for the local audio devices

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |Playing volume during the test for the local audio devices. The range is [0,255]. |


**Notes**

Start an audio\-device test by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-startaudioplaybackdevicetest) or [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-startaudiodevicerecordtest) will register this callback for regular notification on playing volume. You can set the time interval between each callback by passing a proper value when calling the API above.

<span id="IRTCEngineEventHandler-onremoteaudiopropertiesreport"></span>
### onRemoteAudioPropertiesReport

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onRemoteAudioPropertiesReport(
    RemoteAudioPropertiesInfo[] audioPropertiesInfos,
    int totalRemoteVolume
)
```


After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about the subscribed remote audio streams.

The remote audio streams includes the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioPropertiesInfos |RemoteAudioPropertiesInfo [] |See [RemoteAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteAudioPropertiesInfo). |
|totalRemoteVolume |int |The volume of the mixing of all the subscribed audio streams. The range is [0,255].<br><br><br>&nbsp;<br><br>* [0,25] Is close to silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


<span id="IRTCEngineEventHandler-onactivespeaker"></span>
### onActiveSpeaker

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onActiveSpeaker(
    String roomId,
    String uid
)
```


After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |Room ID. |
|uid |String |The user ID of the active speaker. |


<span id="IRTCEngineEventHandler-onechotestresult"></span>
### onEchoTestResult

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onEchoTestResult(EchoTestResult result)
```


Callback about the call test result.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|result |EchoTestResult |Test result, see [EchoTestResult](https://docs.byteplus.com/en/docs/12/docs-70083#EchoTestResult). |


**Notes**

The timing when this callback will be triggered is as follows:


* A device\-related error occurred during the test；

* After a successful test；

* After stopping the test, provided that the audio/video playback was not received during the test due to non\-device reasons.

    &nbsp;


<span id="oncloudproxyconnected"></span>
### onCloudProxyConnected

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onCloudProxyConnected(int interval)
```


Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interval |int |The interval in ms between starting cloud proxy and connects the cloud proxy server successfully. |


<span id="IRTCEngineEventHandler-onnetworktimesynchronized"></span>
### onNetworkTimeSynchronized

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onNetworkTimeSynchronized()
```


After calling [getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getnetworktimeinfo) for the first time, the SDK starts network time synchronization internally. This callback will be triggered when the synchronization is completed.

<span id="IRTCEngineEventHandler-onhardwareechodetectionresult"></span>
### onHardwareEchoDetectionResult

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onHardwareEchoDetectionResult(HardwareEchoDetectionResult hardwareEchoDetectionResult)
```


Callback that notifies you the result of the echo detection before a call

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|hardwareEchoDetectionResult |HardwareEchoDetectionResult |Refer to [HardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70083#HardwareEchoDetectionResult) for more details. |


**Notes**


* This callback notifies you the result of the echo detection by calling [startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-starthardwareechodetection).

* We recommend to call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stophardwareechodetection) to stop the detection.

* Listen to `MEDIA_DEVICE_WARNING_DETECT_LEAK_ECHO` in the callback of [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/14167#IRTCEngineEventHandler-onaudiodevicewarning) for the echo issue during a call.

    &nbsp;


<span id="onlocalproxystatechanged"></span>
### onLocalProxyStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLocalProxyStateChanged(
    LocalProxyType localProxyType,
    LocalProxyState localProxyState,
    LocalProxyError localProxyError
)
```


Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|localProxyType |LocalProxyType |The types of local proxies. Refer to [LocalProxyType](https://docs.byteplus.com/en/docs/12/docs-70083#LocalProxyType) for details. |
|localProxyState |LocalProxyState |The states of local proxy connection. Refer to [LocalProxyState](https://docs.byteplus.com/en/docs/12/docs-70083#LocalProxyState) for details. |
|localProxyError |LocalProxyError |The errors of local proxy connection. Refer to [LocalProxyError](https://docs.byteplus.com/en/docs/12/docs-70083#LocalProxyError) for details. |


<span id="IRTCEngineEventHandler-onstreamsyncinforeceived"></span>
### onStreamSyncInfoReceived

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onStreamSyncInfoReceived(
    String streamId,
    StreamInfo streamInfo,
    StreamSyncInfoConfig.SyncInfoStreamType streamType,
    ByteBuffer data
)
```


Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendstreamsyncinfo) to send an audio stream synchronization message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID |
|streamInfo |StreamInfo |Remote stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |
|streamType |StreamSyncInfoConfig.SyncInfoStreamType |Media stream type. See [SyncInfoStreamType](https://docs.byteplus.com/en/docs/12/docs-70083#SyncInfoStreamType) |
|data |ByteBuffer |Message content. |


<span id="IRTCEngineEventHandler-onremotesnapshottakentofile"></span>
### onRemoteSnapshotTakenToFile

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onRemoteSnapshotTakenToFile(
    String streamId,
    StreamInfo streamInfo,
    String filePath,
    int width,
    int height,
    SnapshotErrorCode errorCode,
    long taskId
)
```


> Available since 3.60.


Triggered after calling [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Information of the snapshotted video stream ID. |
|streamInfo |StreamInfo |Information of the snapshotted video stream. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|filePath |String |The path where the snapshot file is saved. |
|width |int |The width (px) of the snapshot image. |
|height |int |The height (px) of the snapshot image. |
|errorCode |SnapshotErrorCode |The error code for the snapshot task. See [SnapshotErrorCode](https://docs.byteplus.com/en/docs/12/docs-70083#SnapshotErrorCode) for specific indications. |
|taskId |long |The index for the snapshot task, which matches the return value of [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshottofile). |


<span id="IRTCEngineEventHandler-onlocalsnapshottakentofile"></span>
### onLocalSnapshotTakenToFile

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onLocalSnapshotTakenToFile(
    IVideoSource videoSource,
    String filePath,
    int width,
    int height,
    SnapshotErrorCode errorCode,
    long taskId
)
```


> Available since 3.60.


Triggered after calling [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |IVideoSource |Reserved parameter |
|filePath |String |The path where the snapshot file is saved. |
|width |int |The width (px) of the snapshot image. |
|height |int |The height (px) of the snapshot image. |
|errorCode |SnapshotErrorCode |The error code for the snapshot task. See [SnapshotErrorCode](https://docs.byteplus.com/en/docs/12/docs-70083#SnapshotErrorCode) for specific indications. |
|taskId |long |The index for the snapshot task, which matches the return value of [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshottofile). |


<span id="IRTCEngineEventHandler-onaudioframesendstatechanged"></span>
### onAudioFrameSendStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioFrameSendStateChanged(
    String streamId,
    StreamInfo streamInfo,
    RtcUser user,
    FirstFrameSendState state
)
```


Triggered when the local audio first frame send state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID. |
|streamInfo |StreamInfo |Stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|user |RtcUser |User information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-70083#RtcUser). |
|state |FirstFrameSendState |The first frame send state. See [FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-70083#FirstFrameSendState) for specific indications. |


<span id="IRTCEngineEventHandler-onvideoframesendstatechanged"></span>
### onVideoFrameSendStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onVideoFrameSendStateChanged(
    String streamId,
    StreamInfo streamInfo,
    RtcUser user,
    FirstFrameSendState state
)
```


Triggered when the local video first frame send state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID. |
|streamInfo |StreamInfo |Stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|user |RtcUser |User information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-70083#RtcUser). |
|state |FirstFrameSendState |The first frame send state. See [FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-70083#FirstFrameSendState) for specific indications. |


<span id="IRTCEngineEventHandler-onaudioframeplaystatechanged"></span>
### onAudioFramePlayStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioFramePlayStateChanged(
    String streamId,
    StreamInfo streamInfo,
    RtcUser user,
    FirstFramePlayState state
)
```


Triggered when the audio first frame play state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID. |
|streamInfo |StreamInfo |Stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|user |RtcUser |User information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-70083#RtcUser). |
|state |FirstFramePlayState |The first frame play state. See [FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-70083#FirstFramePlayState) for specific indications. |


<span id="IRTCEngineEventHandler-onvideoframeplaystatechanged"></span>
### onVideoFramePlayStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onVideoFramePlayStateChanged(
    String streamId,
    StreamInfo streamInfo,
    RtcUser user,
    FirstFramePlayState state
)
```


Triggered when the remote video stream first frame play state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID. |
|streamInfo |StreamInfo |Stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|user |RtcUser |User information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-70083#RtcUser). |
|state |FirstFramePlayState |The first frame play state. See [FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-70083#FirstFramePlayState) for specific indications. |


<span id="IRTCEngineEventHandler-onsimulcastsubscribefallback"></span>
### onSimulcastSubscribeFallback

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onSimulcastSubscribeFallback(
    String streamId,
    StreamInfo streamInfo,
    RemoteStreamSwitch event
)
```


When the simulcast subscribe fallback occurs, this callback is received.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID. |
|streamInfo |StreamInfo |Stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|event |RemoteStreamSwitch |The information about the change of the simulcast subscribe. See [RemoteStreamSwitch](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteStreamSwitch) for specific indications. |


<span id="IRTCEngineEventHandler-onperformancealarms"></span>
### onPerformanceAlarms

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onPerformanceAlarms(
    String streamId,
    StreamInfo streamInfo,
    PerformanceAlarmMode mode,
    PerformanceAlarmReason reason,
    SourceWantedData data
)
```


When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setpublishfallbackoption) is not turned on locally, and when insufficient device performance is detected, this callback is received.

When the [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setpublishfallbackoption) is locally turned on, ans when the publish performance fallback/recovery is caused due to device performance/network reasons, this callback is received.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID |
|streamInfo |StreamInfo |Stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|mode |PerformanceAlarmMode |Indicates whether the release fallback function is turned on locally. See [PerformanceAlarmMode](https://docs.byteplus.com/en/docs/12/docs-70083#PerformanceAlarmMode)<br><br><br>&nbsp;<br><br>* When the publisher does not turn on the release performance fallback, the mode value is NORMAL.<br><br>* When the publisher turns on the release performance fallback, the mode value is SIMULCAST. |
|reason |PerformanceAlarmReason |For alarm reasons. See [PerformanceAlarmReason](https://docs.byteplus.com/en/docs/12/docs-70083#PerformanceAlarmReason) |
|data |SourceWantedData |Performance fallback related data. See [SourceWantedData](https://docs.byteplus.com/en/docs/12/docs-70083#SourceWantedData). |


<span id="IRTCEngineEventHandler-onmixedstreamevent"></span>
### onMixedStreamEvent

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onMixedStreamEvent(
    MixedStreamTaskInfo info,
    MixedStreamTaskEvent event,
    MixedStreamTaskErrorCode error
)
```


> Available since 3.60. Since version 3.60, this callback replaces the `onStreamMixingEvent` and `onPushPublicStreamResult` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this callback.


Reports events during pushing a mixed stream to CDN or a WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|info |MixedStreamTaskInfo |Task details, see [MixedStreamTaskInfo](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamTaskInfo) |
|event |MixedStreamTaskEvent |Stream mixing and pushing status, see [MixedStreamTaskEvent](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamTaskEvent) |
|error |MixedStreamTaskErrorCode |Errors occurring during the pushing process. See [MixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#MixedStreamTaskErrorCode) |


<span id="IRTCEngineEventHandler-onsinglestreamevent"></span>
### onSingleStreamEvent

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onSingleStreamEvent(
    String taskId,
    SingleStreamTaskEvent event,
    SingleStreamTaskErrorCode error
)
```


> Available since 3.60.


Reports events during pushing a single stream to CDN

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|taskId |String |Task ID |
|event |SingleStreamTaskEvent |Stream pushing status, see [SingleStreamTaskEvent](https://docs.byteplus.com/en/docs/12/docs-70082#SingleStreamTaskEvent). |
|error |SingleStreamTaskErrorCode |Errors occurring during the pushing process. See [SingleStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#SingleStreamTaskErrorCode) |


<span id="IRTCEngineEventHandler-onexperimentalcallback"></span>
### onExperimentalCallback

```java
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onExperimentalCallback(String param)
```


> Available since 3.60.


callback for experimental api

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|param |String |Callback content (JSON string) |


<span id="IRemoteEncodedVideoFrameObserver"></span>
# IRemoteEncodedVideoFrameObserver

```java
public abstract class com.ss.bytertc.engine.mediaio.IRemoteEncodedVideoFrameObserver
```


Remote encoded video data monitor

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|abstract void |[onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/14167#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe"></span>
### onRemoteEncodedVideoFrame

```java
public abstract void com.ss.bytertc.engine.mediaio.IRemoteEncodedVideoFrameObserver.onRemoteEncodedVideoFrame(
    String streamId,
    StreamInfo streamInfo,
    RTCEncodedVideoFrame encodedVideoFrame
)
```


Call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerremoteencodedvideoframeobserver), the callback is triggered when the SDK detects the remote encoded video data

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the received remote stream |
|streamInfo |StreamInfo |The information of the received remote stream. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo) |
|encodedVideoFrame |RTCEncodedVideoFrame |Received remote video frame information. See [RTCEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70083#RTCEncodedVideoFrame) |


**Notes**

encodedVideoFrame is only valid within the scope of the callback function. Do not store this parameter and access the memory data of this parameter in other functions

<span id="IFaceDetectionObserver"></span>
# IFaceDetectionObserver

```java
public interface com.ss.bytertc.engine.video.IFaceDetectionObserver
```


Face detection observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onFaceDetectResult](https://docs.byteplus.com/en/docs/12/14167#IFaceDetectionObserver-onfacedetectresult) |


<span id="instructions"></span>
## Instructions

<span id="IFaceDetectionObserver-onfacedetectresult"></span>
### onFaceDetectResult

```java
void com.ss.bytertc.engine.video.IFaceDetectionObserver.onFaceDetectResult(FaceDetectionResult result)
```


Callback of the result of face detection with Effect SDK.

After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|result |FaceDetectionResult |Face detection result. See [FaceDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70083#FaceDetectionResult). |


<span id="IWTNStreamEventHandler"></span>
# IWTNStreamEventHandler

```java
public interface com.ss.bytertc.engine.IWTNStreamEventHandler
```


WTN event handler.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnremotevideostats) |
|void |[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnremoteaudiostats) |
|void |[onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnvideosubscribestatechanged) |
|void |[onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged) |
|void |[onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnfirstremoteaudioframe) |
|void |[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded) |
|void |[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnseimessagereceived) |
|void |[onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtndatamessagereceived) |


<span id="instructions"></span>
## Instructions

<span id="IWTNStreamEventHandler-onwtnremotevideostats"></span>
### onWTNRemoteVideoStats

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNRemoteVideoStats(
    String streamId,
    RemoteVideoStats stats
)
```


> Available since 3.60.


Remote WTN video stream ID and statistics.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream |
|stats |RemoteVideoStats |Remote WTN video stream statistics. See [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteVideoStats). |


<span id="IWTNStreamEventHandler-onwtnremoteaudiostats"></span>
### onWTNRemoteAudioStats

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNRemoteAudioStats(
    String streamId,
    RemoteAudioStats stats
)
```


> Available since 3.60.


Remote WTN audio stream ID and statistics.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream |
|stats |RemoteAudioStats |Remote WTN audio stream statistics. See [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteAudioStats). |


<span id="IWTNStreamEventHandler-onwtnvideosubscribestatechanged"></span>
### onWTNVideoSubscribeStateChanged

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNVideoSubscribeStateChanged(
    String streamId,
    WTNSubscribeState stateCode,
    WTNSubscribeStateChangeReason reason
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onPlayPublicStreamResult` for reporting the subscription status changes of WTN video streams. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback for the change of WTN video stream's subscription status

You will be informed of the result of subscribing to the WTN video stream by this callback after calling [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN video stream |
|stateCode |WTNSubscribeState |Video stream state code. See [WTNSubscribeState](https://docs.byteplus.com/en/docs/12/docs-70083#WTNSubscribeState) for specific indications. |
|reason |WTNSubscribeStateChangeReason |The reason why subscription state changes. See [WTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#WTNSubscribeStateChangeReason). |


<span id="IWTNStreamEventHandler-onwtnaudiosubscribestatechanged"></span>
### onWTNAudioSubscribeStateChanged

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNAudioSubscribeStateChanged(
    String streamId,
    WTNSubscribeState stateCode,
    WTNSubscribeStateChangeReason reason
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onPlayPublicStreamResult` for reporting the subscription status changes of WTN audio streams. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback for the change of WTN audio stream's subscription status

You will be informed of the result of subscribing to the WTN audio stream by this callback after calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN audio stream |
|stateCode |WTNSubscribeState |Audio stream state code. See [WTNSubscribeState](https://docs.byteplus.com/en/docs/12/docs-70083#WTNSubscribeState) for specific indications. |
|reason |WTNSubscribeStateChangeReason |The reason why subscription state changes. See [WTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70083#WTNSubscribeStateChangeReason). |


<span id="IWTNStreamEventHandler-onwtnfirstremoteaudioframe"></span>
### onWTNFirstRemoteAudioFrame

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNFirstRemoteAudioFrame(String streamId)
```


> Available since 3.60. Since version 3.60, this callback replaces `onFirstPublicStreamAudioFrame`. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback of successfully decoding of the first audio frame of the WTN stream

Refer to [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream) for details about subscribing to a WTN audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream |


<span id="IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded"></span>
### onWTNFirstRemoteVideoFrameDecoded

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNFirstRemoteVideoFrameDecoded(
    String streamId,
    VideoFrameInfo info
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onFirstPublicStreamVideoFrameDecoded`. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback of successfully decoding of the first video frame of the WTN stream

Refer to [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream) for details about subscribing to a WTN video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream |
|info |VideoFrameInfo |Information of the video stream. Refer to [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70083#VideoFrameInfo) for more details. |


<span id="IWTNStreamEventHandler-onwtnseimessagereceived"></span>
### onWTNSEIMessageReceived

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNSEIMessageReceived(
    String streamId,
    int channelId,
    ByteBuffer message
)
```


> Available since 3.60. Since version 3.60, this callback replaces `onPublicStreamSEIMessageReceived` for the following function. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback on receiving the SEI message carried by the WTN stream.

After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream), you will receive this callback if the WTN stream has an SEI message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the WTN stream. |
|channelId |int |SEI message channel ID. The value range is `[0 - 255]`. With this parameter, you can set different ChannelIDs for different recipients. In this way, different recipients can choose the SEI information based on the ChannelID received in the callback. |
|message |ByteBuffer |The received SEI(supplemental enhancement information) message.<br><br>&nbsp;<br><br>The SEI message inserted by calling `sendSEIMessage` in the SDK.<br><br>&nbsp;<br><br>You receive SEI from all the video streams if the SEI messages do not have conflicts. However, if the SEI messages from different video streams have conflicts, you will receive only one of them. |


<span id="IWTNStreamEventHandler-onwtndatamessagereceived"></span>
### onWTNDataMessageReceived

```java
void com.ss.bytertc.engine.IWTNStreamEventHandler.onWTNDataMessageReceived(
    String streamId,
    ByteBuffer message,
    DataMessageSourceType sourceType
)
```


> Available since 3.60.


The data information contained in the callback of WTN stream..

After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream), you can listen to this callback and retrieve SEI messages inserted by Open API calls or audio volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream |
|message |ByteBuffer |The received data message's content is as follows:<br><br><br>&nbsp;<br><br>* Data inserted by calling the OpenAPI.<br><br>* Media volume in JSON, before you can receive which you need to enable it via calling the OpenAPI. Refer to the definition below to parse the JSON string.<br><br>   {<br><br>&nbsp;<br><br>   "Type" : "VolumeIndication", //Specific business type.<br><br>&nbsp;<br><br>   "VolumeInfos" : [ // Business type corresponding information<br><br>&nbsp;<br><br>   {<br><br>&nbsp;<br><br>   "RoomId":"1000001", // Room ID<br><br>&nbsp;<br><br>   "UserId":"1000001", // User ID<br><br>&nbsp;<br><br>   "StreamType":0, // 0:camera stream；1:screen stream<br><br>&nbsp;<br><br>   "LinearVolume":1 // LinearVolume<br><br>&nbsp;<br><br>   } |
|sourceType |DataMessageSourceType |Message source. |


**Notes**

You also need to listen to [onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IWTNStreamEventHandler-onwtnseimessagereceived) to receive SEI inserted via API by the client SDK.

<span id="IMediaPlayerAudioFrameObserver"></span>
# IMediaPlayerAudioFrameObserver

```java
public interface com.ss.bytertc.engine.IMediaPlayerAudioFrameObserver
```


observer for the audio frames during local audio file mixing.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onFrame](https://docs.byteplus.com/en/docs/12/14167#IMediaPlayerAudioFrameObserver-onframe) |


<span id="instructions"></span>
## Instructions

<span id="IMediaPlayerAudioFrameObserver-onframe"></span>
### onFrame

```java
void com.ss.bytertc.engine.IMediaPlayerAudioFrameObserver.onFrame(
    int playerId,
    IAudioFrame frame
)
```


The callback for the audio frames during local audio file mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |Player's ID. |
|frame |IAudioFrame |See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


<span id="IAudioFileFrameObserver"></span>
# IAudioFileFrameObserver

```java
public interface com.ss.bytertc.engine.IAudioFileFrameObserver
```


The observer for the audio frames during local audio file mixing.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onAudioFileFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFileFrameObserver-onaudiofileframe) |


<span id="instructions"></span>
## Instructions

<span id="IAudioFileFrameObserver-onaudiofileframe"></span>
### onAudioFileFrame

```java
void com.ss.bytertc.engine.IAudioFileFrameObserver.onAudioFileFrame(
    int mixID,
    IAudioFrame audioFrame
)
```


The callback for the audio frames during local audio file mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mixID |int |Mixing ID. |
|audioFrame |IAudioFrame |See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


<span id="IRTSRoomEventHandler"></span>
# IRTSRoomEventHandler

```java
public abstract class com.ss.bytertc.engine.handler.IRTSRoomEventHandler
```


IRTSRoomEventHandler Class

Note: The callback is triggered on the SDK internal thread (non\-UI thread), do not do time\-consuming operations or directly operate the UI, or the app may crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onLeaveRoom](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onleaveroom) |
|void |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onroomstatechanged) |
|void |[onUserJoined](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onuserjoined) |
|void |[onUserLeave](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onuserleave) |
|void |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onroommessagereceived) |
|void |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onroombinarymessagereceived) |
|void |[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onusermessagereceived) |
|void |[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onuserbinarymessagereceived) |
|void |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onroommessagereceived-2) |
|void |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onroombinarymessagereceived-2) |
|void |[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onusermessagereceived-2) |
|void |[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onuserbinarymessagereceived-2) |
|void |[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onusermessagesendresult) |
|void |[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/14167#IRTSRoomEventHandler-onroommessagesendresult) |


<span id="instructions"></span>
## Instructions

<span id="IRTSRoomEventHandler-onleaveroom"></span>
### onLeaveRoom

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onLeaveRoom(RTCRoomStats stats)
```


Leave the room successfully callback.

After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) method, the SDK will stop all publishing subscription streams, and after releasing all call\-related audio & video resources, this callback will notify the user to leave the room successfully.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |RTCRoomStats |Reserved parameter. |


**Notes**


* After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) method to leave the room, if [destroy](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-destroy) is called to destroy the room instance or [destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-destroyrtcengine) method is called to destroy the RTC engine immediately, this callback event will not be received.

* If the app needs to use the system audio & video device after leaving the room, it is recommended to initialize the audio & video device after receiving this callback, otherwise the initialization may fail due to the SDK occupying the audio & video device.

    &nbsp;


<span id="onroomstatechanged"></span>
### onRoomStateChanged

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onRoomStateChanged(
    String roomId,
    String uid,
    int state,
    String extraInfo
)
```


Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |Room ID. |
|uid |String |User ID. |
|state |int |Room state code.<br><br><br>&nbsp;<br><br>* 0: Join room success.<br><br>* !0: Failed to join a room, abnormal exit, room\-related warnings or errors. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#ErrorCode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-70082#WarningCode) for specific indications. |
|extraInfo |String |Extra information.<br><br>&nbsp;<br><br>`join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` means the user rejoins the room.<br><br>&nbsp;<br><br>`elapsed` indicates the time interval from calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-joinroom) to successfully joining room, in ms. |


<span id="IRTSRoomEventHandler-onuserjoined"></span>
### onUserJoined

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onUserJoined(UserInfo userInfo)
```


You will receive this callback in following cases:


* The remote user calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) turns visible and joins your room.

* The remote visible user is disconnected and then reconnected to your room.

* The invisible remote user in your room calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) and turns visible.

* You join the room when there are visible users in the room.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|userInfo |UserInfo |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70083#UserInfo). |


<span id="IRTSRoomEventHandler-onuserleave"></span>
### onUserLeave

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onUserLeave(
    String uid,
    int reason
)
```


This callback is triggered when a remote user is disconnected or turns invisible.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |ID of the user who leaves the room, or switches to invisible. |
|reason |int |Reason to leave the room:<br><br><br>&nbsp;<br><br>* 0: The remote client calls [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) to leave the room.<br><br>* 1: The remote client is disconnected because of poor network connection or expired Token.<br><br>* 2: The remote client calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) to turn invisible.<br><br>* 3: The remote user has been removed from the room by the administrator via a OpenAPI call. |


<span id="IRTSRoomEventHandler-onroommessagereceived"></span>
### onRoomMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onRoomMessageReceived(
    String uid,
    String message
)
```


Receive a callback for broadcast messages in the room.

This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message sender. |
|message |String |The content of the received message. |


<span id="IRTSRoomEventHandler-onroombinarymessagereceived"></span>
### onRoomBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onRoomBinaryMessageReceived(
    String uid,
    ByteBuffer message
)
```


Receives a callback for broadcast binary messages in the room.

This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message sender. |
|message |ByteBuffer |The content of the received binary message. |


<span id="IRTSRoomEventHandler-onusermessagereceived"></span>
### onUserMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onUserMessageReceived(
    String uid,
    String message
)
```


Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |The user ID of the sender of the message. |
|message |String |The content of the received text message. |


<span id="IRTSRoomEventHandler-onuserbinarymessagereceived"></span>
### onUserBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onUserBinaryMessageReceived(
    String uid,
    ByteBuffer message
)
```


Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |The user ID of the sender of the message. |
|message |ByteBuffer |The binary message content received. |


<span id="IRTSRoomEventHandler-onroommessagereceived-2"></span>
### onRoomMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onRoomMessageReceived(
    long msgid,
    String uid,
    String message
)
```


Receive a callback for broadcast messages in the room.

This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number |
|uid |String |User ID of the message sender. |
|message |String |The content of the received message. |


<span id="IRTSRoomEventHandler-onroombinarymessagereceived-2"></span>
### onRoomBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onRoomBinaryMessageReceived(
    long msgid,
    String uid,
    ByteBuffer message
)
```


Receives a callback for broadcast binary messages in the room.

This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number |
|uid |String |User ID of the message sender. |
|message |ByteBuffer |The content of the received binary message. |


<span id="IRTSRoomEventHandler-onusermessagereceived-2"></span>
### onUserMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onUserMessageReceived(
    long msgid,
    String uid,
    String message
)
```


Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number |
|uid |String |The user ID of the sender of the message. |
|message |String |The content of the received text message. |


<span id="IRTSRoomEventHandler-onuserbinarymessagereceived-2"></span>
### onUserBinaryMessageReceived

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onUserBinaryMessageReceived(
    long msgid,
    String uid,
    ByteBuffer message
)
```


Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |Message number |
|uid |String |The user ID of the sender of the message. |
|message |ByteBuffer |The binary message content received. |


<span id="IRTSRoomEventHandler-onusermessagesendresult"></span>
### onUserMessageSendResult

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onUserMessageSendResult(
    long msgid,
    int error
)
```


After sending a point\-to\-point text or point\-to\-point binary message to a single user in the room, the message sender will receive a callback with the result of the message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |The ID of this message. |
|error |int |Text or binary message sending results. See [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70082#UserMessageSendResult) |


**Notes**

Call [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage) or [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage) interface to receive this callback.

<span id="IRTSRoomEventHandler-onroommessagesendresult"></span>
### onRoomMessageSendResult

```java
public void com.ss.bytertc.engine.handler.IRTSRoomEventHandler.onRoomMessageSendResult(
    long msgid,
    int error
)
```


Receives this callback after sending a text message or a binary message to a room with [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) or [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |long |The ID of this message. |
|error |int |Message sending result. See [RoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70082#RoomMessageSendResult) |


<span id="ILocalEncodedVideoFrameObserver"></span>
# ILocalEncodedVideoFrameObserver

```java
public interface com.ss.bytertc.engine.mediaio.ILocalEncodedVideoFrameObserver
```


Local video frame observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/14167#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe"></span>
### onLocalEncodedVideoFrame

```java
void com.ss.bytertc.engine.mediaio.ILocalEncodedVideoFrameObserver.onLocalEncodedVideoFrame(
    IVideoSource videoSource,
    RTCEncodedVideoFrame encodedVideoFrame
)
```


After calling [registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerlocalencodedvideoframeobserver), SDK will trigger this callback when it receives local video frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |IVideoSource |Reserved parameter |
|encodedVideoFrame |RTCEncodedVideoFrame |Information about the local video frame. See [RTCEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70083#RTCEncodedVideoFrame) |


**Notes**

encodedVideoFrame is only valid within the scope of the callback function. Do not store this parameter and access the memory data of this parameter in other functions

<span id="IExternalVideoEncoderEventHandler"></span>
# IExternalVideoEncoderEventHandler

```java
public abstract class com.ss.bytertc.engine.handler.IExternalVideoEncoderEventHandler
```


Custom coded frame callback class.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|abstract void |[onStart](https://docs.byteplus.com/en/docs/12/14167#IExternalVideoEncoderEventHandler-onstart) |
|abstract void |[onStop](https://docs.byteplus.com/en/docs/12/14167#IExternalVideoEncoderEventHandler-onstop) |
|abstract void |[onRateUpdate](https://docs.byteplus.com/en/docs/12/14167#IExternalVideoEncoderEventHandler-onrateupdate) |
|abstract void |[onRequestKeyFrame](https://docs.byteplus.com/en/docs/12/14167#IExternalVideoEncoderEventHandler-onrequestkeyframe) |
|abstract void |[onActiveVideoLayer](https://docs.byteplus.com/en/docs/12/14167#IExternalVideoEncoderEventHandler-onactivevideolayer) |


<span id="instructions"></span>
## Instructions

<span id="IExternalVideoEncoderEventHandler-onstart"></span>
### onStart

```java
public abstract void com.ss.bytertc.engine.handler.IExternalVideoEncoderEventHandler.onStart(
    String streamId,
    StreamInfo streamInfo
)
```


Prompt custom encoded frames to start pushing callbacks.

After receiving this callback, you can call [pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushexternalencodedvideoframe) to push a custom encoded video frame to the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the encoded stream that can be pushed |
|streamInfo |StreamInfo |The properties of the encoded stream that can be pushed |


<span id="IExternalVideoEncoderEventHandler-onstop"></span>
### onStop

```java
public abstract void com.ss.bytertc.engine.handler.IExternalVideoEncoderEventHandler.onStop(
    String streamId,
    StreamInfo streamInfo
)
```


When receiving the callback, you need to stop pushing custom encoded video frames to the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the encoded stream that needs to be stopped |
|streamInfo |StreamInfo |The properties of the encoded stream that needs to be stopped |


<span id="IExternalVideoEncoderEventHandler-onrateupdate"></span>
### onRateUpdate

```java
public abstract void com.ss.bytertc.engine.handler.IExternalVideoEncoderEventHandler.onRateUpdate(
    String streamId,
    StreamInfo streamInfo,
    int videoIndex,
    int fps,
    int bitrateKbps
)
```


When the frame rate or bit rate of a custom encoded stream changes, the callback is triggered

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the encoded stream that changes |
|streamInfo |StreamInfo |The properties of the encoded stream that changes |
|videoIndex |int |The subscript of the corresponding encoded stream |
|fps |int |The frame rate after the change, the unit: fps |
|bitrateKbps |int |The code rate after the change, the unit: kbps |


<span id="IExternalVideoEncoderEventHandler-onrequestkeyframe"></span>
### onRequestKeyFrame

```java
public abstract void com.ss.bytertc.engine.handler.IExternalVideoEncoderEventHandler.onRequestKeyFrame(
    String streamId,
    StreamInfo streamInfo,
    int videoIndex
)
```


This callback is used to inform the stream publisher that a keyframe needs to be regenerated.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote encoded stream ID |
|streamInfo |StreamInfo |Remote encoded stream property |
|videoIndex |int |Subscript of the corresponding encoded stream |


<span id="IExternalVideoEncoderEventHandler-onactivevideolayer"></span>
### onActiveVideoLayer

```java
public abstract void com.ss.bytertc.engine.handler.IExternalVideoEncoderEventHandler.onActiveVideoLayer(
    String streamId,
    StreamInfo streamInfo,
    int videoIndex,
    boolean active
)
```


> Available since 3.56


As the sender of a external encoded video stream, you will receive this callback at certain moments.

Based on the hints of this callback, you can selectively encode the video stream that is ready for transmission, in order to reduce the performance impact of video encoding on the local device. This callback is triggered based on a combination of factors, including the performance of the local device, the local network, and whether the stream is subscribed by the remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70083#streamindex-2). |
|streamInfo |StreamInfo |See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70083#streamindex-2). |
|videoIndex |int |Subscript of the corresponding encoded stream. |
|active |boolean |The active state of the corresponding encoded stream. |


**Notes**

To receive the callback, call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideosourcetype) to set the input video source to custom encoded video and call [setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setexternalvideoencodereventhandler) to set the callback handler.

<span id="IMediaPlayerEventHandler"></span>
# IMediaPlayerEventHandler

```java
public interface com.ss.bytertc.engine.IMediaPlayerEventHandler
```


Event handler for [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer). You must call [setEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-seteventhandler) to set the corresponding event handler to get the events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/14167#IMediaPlayerEventHandler-onmediaplayerstatechanged) |
|void |[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/14167#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |
|void |[onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/14167#IMediaPlayerEventHandler-onmediaplayerevent) |


<span id="instructions"></span>
## Instructions

<span id="IMediaPlayerEventHandler-onmediaplayerstatechanged"></span>
### onMediaPlayerStateChanged

```java
void com.ss.bytertc.engine.IMediaPlayerEventHandler.onMediaPlayerStateChanged(
    int playerId,
    PlayerState state,
    PlayerError error
)
```


Callback for audio mixing status change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |The ID of [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer). Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getmediaplayer). |
|state |PlayerState |See [PlayerState](https://docs.byteplus.com/en/docs/12/docs-70083#PlayerState). |
|error |PlayerError |See [PlayerError](https://docs.byteplus.com/en/docs/12/docs-70083#PlayerError). |


<span id="IMediaPlayerEventHandler-onmediaplayerplayingprogress"></span>
### onMediaPlayerPlayingProgress

```java
void com.ss.bytertc.engine.IMediaPlayerEventHandler.onMediaPlayerPlayingProgress(
    int playerId,
    long progress
)
```


Periodic callback for audio mixing progress. The period is set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setprogressinterval).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |The ID of [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer). Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getmediaplayer). |
|progress |long |Mixing progress in ms. |


<span id="IMediaPlayerEventHandler-onmediaplayerevent"></span>
### onMediaPlayerEvent

```java
void com.ss.bytertc.engine.IMediaPlayerEventHandler.onMediaPlayerEvent(
    int playerId,
    PlayerEvent event,
    String message
)
```


> Available since 3.59


Callback for audio mixing player events. This callback is triggered after you call [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-selectaudiotrack) and [setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |The ID of [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer). Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getmediaplayer). |
|event |PlayerEvent |See [PlayerEvent](https://docs.byteplus.com/en/docs/12/docs-70083#PlayerEvent). |
|message |String |Event description message, which may be empty. |


<span id="IAudioFrameObserver"></span>
# IAudioFrameObserver

```java
public interface com.ss.bytertc.engine.IAudioFrameObserver
```


Audio data callback observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

The time interval for all callback functions in this interface is 20 ms.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameObserver-onrecordaudioframe) |
|void |[onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameObserver-onplaybackaudioframe) |
|void |[onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameObserver-onremoteuseraudioframe) |
|void |[onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameObserver-onmixedaudioframe) |
|void |[onCaptureMixedAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameObserver-oncapturemixedaudioframe) |


<span id="instructions"></span>
## Instructions

<span id="IAudioFrameObserver-onrecordaudioframe"></span>
### onRecordAudioFrame

```java
void com.ss.bytertc.engine.IAudioFrameObserver.onRecordAudioFrame(IAudioFrame audioFrame)
```


Returns the audio data recorded by local microphone.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


<span id="IAudioFrameObserver-onplaybackaudioframe"></span>
### onPlaybackAudioFrame

```java
void com.ss.bytertc.engine.IAudioFrameObserver.onPlaybackAudioFrame(IAudioFrame audioFrame)
```


Returns the mixed audio data of all remote users subscribed by the local user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


<span id="IAudioFrameObserver-onremoteuseraudioframe"></span>
### onRemoteUserAudioFrame

```java
void com.ss.bytertc.engine.IAudioFrameObserver.onRemoteUserAudioFrame(
    String streamId,
    StreamInfo streamInfo,
    IAudioFrame audioFrame
)
```


Returns the audio data of one remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID. |
|streamInfo |StreamInfo |Remote stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|audioFrame |IAudioFrame |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


**Notes**

This callback works on the playback thread. Don't do anything time\-consuming in this callback, or it may affect the entire audio playback chain.

<span id="IAudioFrameObserver-onmixedaudioframe"></span>
### onMixedAudioFrame

```java
void com.ss.bytertc.engine.IAudioFrameObserver.onMixedAudioFrame(IAudioFrame audioFrame)
```


Returns the mixed audio data including the data recorded by local microphone and that of all remote users subscribed by the local user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


<span id="IAudioFrameObserver-oncapturemixedaudioframe"></span>
### onCaptureMixedAudioFrame

```java
void com.ss.bytertc.engine.IAudioFrameObserver.onCaptureMixedAudioFrame(IAudioFrame audioFrame)
```


Return the mixed audio data of the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


<span id="IRTCEncryptionHandler"></span>
# IRTCEncryptionHandler

```java
public interface com.ss.bytertc.engine.handler.IRTCEncryptionHandler
```


Encrypted event callback interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|byte[] |[onEncryptData](https://docs.byteplus.com/en/docs/12/14167#IRTCEncryptionHandler-onencryptdata) |
|byte[] |[onDecryptData](https://docs.byteplus.com/en/docs/12/14167#IRTCEncryptionHandler-ondecryptdata) |


<span id="instructions"></span>
## Instructions

<span id="IRTCEncryptionHandler-onencryptdata"></span>
### onEncryptData

```java
byte[] com.ss.bytertc.engine.handler.IRTCEncryptionHandler.onEncryptData(byte[] data)
```


Custom encryption.

Encrypts audio & video frame data before transmission using the custom encryption method set.

Encryption of the original audio and video frames is currently not available.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|data |byte[] |Unencrypted data. |


**Return Value**

Encrypted data

<span id="IRTCEncryptionHandler-ondecryptdata"></span>
### onDecryptData

```java
byte[] com.ss.bytertc.engine.handler.IRTCEncryptionHandler.onDecryptData(byte[] data)
```


Custom decryption.

Decrypts custom encrypted audio & video frame data. For custom encryption, see [onEncryptData](https://docs.byteplus.com/en/docs/12/14167#IRTCEncryptionHandler-onencryptdata).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|data |byte[] |Encrypted data. |


**Return Value**

Decrypted data

<span id="IMediaPlayerCustomSourceProvider"></span>
# IMediaPlayerCustomSourceProvider

```java
public interface com.ss.bytertc.engine.IMediaPlayerCustomSourceProvider
```


In\-memory audio data playing callback interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[onReadData](https://docs.byteplus.com/en/docs/12/14167#IMediaPlayerCustomSourceProvider-onreaddata) |
|long |[onSeek](https://docs.byteplus.com/en/docs/12/14167#IMediaPlayerCustomSourceProvider-onseek) |


<span id="instructions"></span>
## Instructions

<span id="IMediaPlayerCustomSourceProvider-onreaddata"></span>
### onReadData

```java
int com.ss.bytertc.engine.IMediaPlayerCustomSourceProvider.onReadData(
    ByteBuffer buffer,
    int bufferSize
)
```


> Available since 3.53


Callback of getting the path and size of the audio data you input.

When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, this callback will be triggered and you need to enter the path and size of the audio data.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|buffer |ByteBuffer |The path of the audio data you input. The size of audio data should be equal to or less than the value of bufferSize. The supported formats are: mp3, aac, m4a, 3gp, wav. |
|bufferSize |int |The size of the audio data, in bytes. If you want to stop audio playing, you can enter a figure less than or equal to zero into bufferSize and then SDK will stop calling this callback. |


**Return Value**

Returns the size of the audio data that are actually read.

**Notes**

If calling [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource) API failed, please enter 0 into buffer and bufferSize. In this situation, SDK will stop calling this callback.

<span id="IMediaPlayerCustomSourceProvider-onseek"></span>
### onSeek

```java
long com.ss.bytertc.engine.IMediaPlayerCustomSourceProvider.onSeek(
    long offset,
    MediaPlayerCustomSourceSeekWhence whence
)
```


> Available since 3.53


Seeking the audio data based on the set starting position and offset to help SDK read and analyze data.

When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, or when you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition) to set the starting position of audio playing, this callback will be trigerred and you need to seek the audio data accorring to the value of offset and whence.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|offset |long |The offset of the target position relative to the starting position, in bytes. The value can be positive or negative. |
|whence |MediaPlayerCustomSourceSeekWhence |The starting position of the seeking. Refer to [MediaPlayerCustomSourceSeekWhence](https://docs.byteplus.com/en/docs/12/docs-70083#MediaPlayerCustomSourceSeekWhence) for more details. |


**Return Value**

If the seeking succeeded, the information on the final adjusted play position after seeking or the size of the audio data will be returned.

If the seeking failed, \-1 will be returned.

<span id="ISnapshotResultCallback"></span>
# ISnapshotResultCallback

```java
public interface com.ss.bytertc.engine.video.ISnapshotResultCallback
```


The callback of taking snapshots.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onTakeLocalSnapshotResult](https://docs.byteplus.com/en/docs/12/14167#ISnapshotResultCallback-ontakelocalsnapshotresult) |
|void |[onTakeRemoteSnapshotResult](https://docs.byteplus.com/en/docs/12/14167#ISnapshotResultCallback-ontakeremotesnapshotresult) |


<span id="instructions"></span>
## Instructions

<span id="ISnapshotResultCallback-ontakelocalsnapshotresult"></span>
### onTakeLocalSnapshotResult

```java
void com.ss.bytertc.engine.video.ISnapshotResultCallback.onTakeLocalSnapshotResult(
    long taskId,
    IVideoSource videoSource,
    Bitmap image,
    int errorCode
)
```


Receives the callback after calling [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshot).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|taskId |long |The index for the snapshot, the same as the return value of [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshot). |
|videoSource |IVideoSource |Reserved parameter. |
|image |Bitmap |The snapshot image. If the snapshot task fails, the value is `null`. |
|errorCode |int |Error code:<br><br><br>&nbsp;<br><br>* 0: Success.<br><br>* \-1: Failure. Fails to generate the image.<br><br>* \-2: Failure. The stream is invalid.<br><br>* \-3: Failure. snapshot timeout, default 1s. |


<span id="ISnapshotResultCallback-ontakeremotesnapshotresult"></span>
### onTakeRemoteSnapshotResult

```java
void com.ss.bytertc.engine.video.ISnapshotResultCallback.onTakeRemoteSnapshotResult(
    long taskId,
    String streamId,
    StreamInfo streamInfo,
    Bitmap image,
    int errorCode
)
```


Receives the callback after calling [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshot).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|taskId |long |The index for the remote snapshot, the same as the return value of [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshot). |
|streamId |String |The ID of the remote stream. |
|streamInfo |StreamInfo |See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|image |Bitmap |The snapshot image. If the snapshot task fails, the value is `null`. |
|errorCode |int |Error code:<br><br><br>&nbsp;<br><br>* 0: Success.<br><br>* \-1: Failure. Fails to generate the image.<br><br>* \-2: Failure. The stream is invalid.<br><br>* \-3: Failure. snapshot timeout, default 1s. |


<span id="IAudioFrameProcessor"></span>
# IAudioFrameProcessor

```java
public interface com.ss.bytertc.engine.IAudioFrameProcessor
```


The custom audio processor.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameProcessor-onprocessrecordaudioframe) |
|int |[onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameProcessor-onprocessplaybackaudioframe) |
|int |[onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameProcessor-onprocessremoteuseraudioframe) |
|int |[onProcessEarMonitorAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameProcessor-onprocessearmonitoraudioframe) |
|int |[onProcessScreenAudioFrame](https://docs.byteplus.com/en/docs/12/14167#IAudioFrameProcessor-onprocessscreenaudioframe) |


<span id="instructions"></span>
## Instructions

<span id="IAudioFrameProcessor-onprocessrecordaudioframe"></span>
### onProcessRecordAudioFrame

```java
int com.ss.bytertc.engine.IAudioFrameProcessor.onProcessRecordAudioFrame(IAudioFrame audioFrame)
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |The address of the audio frame. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


**Return Value**


* 0: Success.

* <0: Failure.


**Notes**


* After custom processing, SDK will encode the processed audio frames and transmit to the remote user. The processing does not affect the SDK\-level ear\-monitoring audio.

* To enable this callback, call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioprocessor). You will receive this callback every 10 ms.

    &nbsp;


<span id="onprocessplaybackaudioframe"></span>
### onProcessPlayBackAudioFrame

```java
int com.ss.bytertc.engine.IAudioFrameProcessor.onProcessPlayBackAudioFrame(IAudioFrame audioFrame)
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |The address of the audio frame. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame) |


**Notes**

After calling [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioprocessor) with mixed remote audio, you will receive this callback every 10 ms.

<span id="IAudioFrameProcessor-onprocessremoteuseraudioframe"></span>
### onProcessRemoteUserAudioFrame

```java
int com.ss.bytertc.engine.IAudioFrameProcessor.onProcessRemoteUserAudioFrame(
    String streamId,
    StreamInfo streamInfo,
    IAudioFrame audioFrame
)
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID. |
|streamInfo |StreamInfo |Remote stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#StreamInfo). |
|audioFrame |IAudioFrame |The address of the audio frame. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame) |


**Notes**

After calling [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioprocessor) with remote audio streams, you will receive this callback every 10 ms.

<span id="IAudioFrameProcessor-onprocessearmonitoraudioframe"></span>
### onProcessEarMonitorAudioFrame

```java
int com.ss.bytertc.engine.IAudioFrameProcessor.onProcessEarMonitorAudioFrame(IAudioFrame audioFrame)
```


> Available since 3.50


You will receive the address of SDK\-level in\-ear monitoring audio frames for custom processing.

The audio effects set by `setVoiceReverbType` and `setVoiceChangerType` are included.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |The address of the SDK\-level in\-ear monitoring audio frames. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


**Return Value**


* 0: Success.

* <0: Failure.


**Notes**


* Modifying the data affects only SDK\-level in\-ear monitoring audio.

* To enable this callback, call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioprocessor). You will receive this callback every 10 ms.

    &nbsp;


<span id="onprocessscreenaudioframe"></span>
### onProcessScreenAudioFrame

```java
int com.ss.bytertc.engine.IAudioFrameProcessor.onProcessScreenAudioFrame(IAudioFrame audioFrame)
```


Returns the address of the shared\-screen audio frames for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |IAudioFrame |The address of audio frames. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IAudioFrame). |


**Notes**

After calling [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioprocessor) to set the audio input to the shared\-screen audio, you will receive this callback every 10 ms.
