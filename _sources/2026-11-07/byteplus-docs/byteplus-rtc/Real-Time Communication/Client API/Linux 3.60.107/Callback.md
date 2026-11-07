---
title: "Callback"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85517"
---

<span id="IRemoteEncodedVideoFrameObserver"></span>
# IRemoteEncodedVideoFrameObserver

```cpp
class bytertc::IRemoteEncodedVideoFrameObserver
```


Remote encoded video data monitor

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/25050#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe"></span>
### onRemoteEncodedVideoFrame

```cpp
virtual void onRemoteEncodedVideoFrame(
    const char* stream_id,
    const StreamInfo& stream_info,
    const IEncodedVideoFrame& video_stream
) = 0;
```


Call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerremoteencodedvideoframeobserver), the callback is triggered when the SDK detects the remote encoded video data

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The ID of the received remote stream |
|stream_info |const StreamInfo& |The information of the received remote stream. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|video_stream |const IEncodedVideoFrame& |The received remote video frame information. See [IEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IEncodedVideoFrame) |


<span id="IAudioEffectPlayerEventHandler"></span>
# IAudioEffectPlayerEventHandler

```cpp
class bytertc::IAudioEffectPlayerEventHandler
```


Event handler for [IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer). You must call [setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-seteventhandler) to set the corresponding event handler to get the events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual |[~IAudioEffectPlayerEventHandler](https://docs.byteplus.com/en/docs/12/25050#IAudioEffectPlayerEventHandler-~iaudioeffectplayereventhandler) |
|virtual void |[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/25050#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |


<span id="instructions"></span>
## Instructions

<span id="IAudioEffectPlayerEventHandler-~iaudioeffectplayereventhandler"></span>
### ~IAudioEffectPlayerEventHandler

```cpp
virtual ~IAudioEffectPlayerEventHandler() {}
```


<span id="IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged"></span>
### onAudioEffectPlayerStateChanged

```cpp
virtual void onAudioEffectPlayerStateChanged(
    int effect_id,
    PlayerState state,
    PlayerError error
) = 0;
```


Callback for audio mixing status change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |The ID of [IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer). Set by [getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getaudioeffectplayer). |
|state |PlayerState |See [PlayerState](https://docs.byteplus.com/en/docs/12/docs-85519#PlayerState). |
|error |PlayerError |See [PlayerError](https://docs.byteplus.com/en/docs/12/docs-85519#PlayerError). |


<span id="IEncryptHandler"></span>
# IEncryptHandler

```cpp
class bytertc::IEncryptHandler
```


Encryption/decryption handler

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual unsigned int |[onEncryptData](https://docs.byteplus.com/en/docs/12/25050#IEncryptHandler-onencryptdata) |
|virtual unsigned int |[onDecryptData](https://docs.byteplus.com/en/docs/12/25050#IEncryptHandler-ondecryptdata) |


<span id="instructions"></span>
## Instructions

<span id="IEncryptHandler-onencryptdata"></span>
### onEncryptData

```cpp
virtual unsigned int onEncryptData(
            const unsigned char* data, unsigned int length, unsigned char* buf, unsigned int buf_len) = 0;
```


Custom encryption.

Encrypts audio & video frame data before transmission using the custom encryption method set.

Encryption of the original audio and video frames is currently not available.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|data |const unsigned char\* |Raw audio & video frame data |
|length |unsigned int |Length of raw audio & video frame data |
|buf |unsigned char\* |Encrypted data buffer available for writing |
|buf_len |unsigned int |Size of encrypted data buffer available for writing |


**Return Value**

Encrypted data


* ≥ 0: size of data actually written to the buffer after encryption

* 0: Discard the frame


**Notes**


* Before using this interface for custom encryption, you must first set the custom encryption method. See `setCustomizeEncryptHandler`.

* Use [onDecryptData](https://docs.byteplus.com/en/docs/12/25050#IEncryptHandler-ondecryptdata) to decrypt encrypted audio & video frame data.

* The returned data size should be controlled within 90%~ 120% of the original data source, otherwise it will be discarded.

    &nbsp;


<span id="ondecryptdata"></span>
### onDecryptData

```cpp
virtual unsigned int onDecryptData(
            const unsigned char* data, unsigned int length, unsigned char* buf, unsigned int buf_len) = 0;
```


Custom decryption.

Decrypts custom encrypted audio & video frame data. For custom encryption, see [onEncryptData](https://docs.byteplus.com/en/docs/12/25050#IEncryptHandler-onencryptdata).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|data |const unsigned char\* |Raw audio & video frame data |
|length |unsigned int |Length of raw audio & video frame data |
|buf |unsigned char\* |Encrypted data buffer available for writing |
|buf_len |unsigned int |Size of encrypted data buffer available for writing |


**Return Value**

Encrypted data


* ≥ 0: size of data actually written to the buffer after encryption

* 0: Discard the frame


**Notes**


* Before using this interface to decrypt, you must first set the decryption method. See `setCustomizeEncryptHandler`.

* The returned data size should be controlled within 90%~ 120% of the original data source, otherwise it will be discarded.

    &nbsp;


<span id="irtcroomeventhandler"></span>
# IRTCRoomEventHandler

```cpp
class bytertc::IRTCRoomEventHandler
```


RTS room event callback interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onvideopublishstatechanged) |
|virtual void |[onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onaudiopublishstatechanged) |
|virtual void |[onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onvideosubscribestatechanged) |
|virtual void |[onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onaudiosubscribestatechanged) |
|virtual void |[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-ontokenwillexpire) |
|virtual void |[onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire) |
|virtual void |[onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire) |
|virtual void |[onRoomStats](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onroomstats) |
|virtual void |[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onremotestreamstats) |
|virtual void |[onUserJoined](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onuserjoined) |
|virtual void |[onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onuserpublishstreamvideo) |
|virtual void |[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onuserpublishstreamaudio) |
|virtual void |[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onvideostreambanned) |
|virtual void |[onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onavsyncstatechange) |
|virtual void |[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onaudiostreambanned) |
|virtual void |[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onforwardstreamstatechanged) |
|virtual void |[onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onforwardstreamevent) |
|virtual void |[onNetworkQuality](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onnetworkquality) |
|virtual void |[onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onsetroomextrainforesult) |
|virtual void |[onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onroomextrainfoupdate) |
|virtual void |[onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onroomstreamextrainfoupdate) |
|virtual void |[onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onuservisibilitychanged) |
|virtual void |[onAVSyncEvent](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onavsyncevent) |


<span id="instructions"></span>
## Instructions

<span id="IRTCRoomEventHandler-onvideopublishstatechanged"></span>
### onVideoPublishStateChanged

```cpp
virtual void onVideoPublishStateChanged(
            const char* stream_id, const StreamInfo& stream_info, PublishState state, PublishStateChangeReason reason) {
        (void)stream_id;
        (void)stream_info;
        (void)state;
        (void)reason;
    }
```


> Available since 3.60. since 3.60. Since version 3.60, this callback replaces `onStreamStateChanged` for reporting video publishing status changes. If you have upgraded to SDK version 3.60 or later and are still using this method, please migrate to this callback.


Callback on video\-stream state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const StreamInfo& |Stream information. |
|state |PublishState |State code. See [PublishState](https://docs.byteplus.com/en/docs/12/docs-85519#PublishState) for more. |
|reason |PublishStateChangeReason |The reason for the change of the publishing state of the local video stream. See [PublishStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#PublishStateChangeReason) for details. |


**Notes**

In addition to being triggered by local video stream state changes, this callback is also received when the local user joins the room.

<span id="IRTCRoomEventHandler-onaudiopublishstatechanged"></span>
### onAudioPublishStateChanged

```cpp
virtual void onAudioPublishStateChanged(
            const char* stream_id, const StreamInfo& stream_info, PublishState state, PublishStateChangeReason reason) {
        (void)stream_id;
        (void)stream_info;
        (void)state;
        (void)reason;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces `onStreamStateChanged` for reporting audio publishing status changes. If you have upgraded to SDK version 3.60 or later and are still using this method, please migrate to this callback.


Triggered when local audio stream publishing status changes, or the local user joins the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const StreamInfo& |Stream information. |
|state |PublishState |State code. See [PublishState](https://docs.byteplus.com/en/docs/12/docs-85519#PublishState) for more. |
|reason |PublishStateChangeReason |The reason for the change of the publishing state of the local audio stream. See [PublishStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#PublishStateChangeReason) for more. |


**Notes**

In addition to being triggered by local audio stream state changes, this callback is also received when the local user joins the room.

<span id="IRTCRoomEventHandler-onvideosubscribestatechanged"></span>
### onVideoSubscribeStateChanged

```cpp
virtual void onVideoSubscribeStateChanged(
            const char* stream_id, const StreamInfo& stream_info, SubscribeState state, SubscribeStateChangeReason reason) {
        (void)stream_id;
        (void)stream_info;
        (void)state;
        (void)reason;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces `onStreamStateChanged` and `onStreamSubscribed` for reporting the state changes of the subscription to camera\-video streams. If you have upgraded to SDK version 3.60 or later and are still using this two methods, please migrate to this callback.


Callback on state changes of the subscription to camera\-video streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const StreamInfo& |Stream information. |
|state |SubscribeState |Room state code. See [SubscribeState](https://docs.byteplus.com/en/docs/12/docs-85519#SubscribeState) for more. |
|reason |SubscribeStateChangeReason |The reason for the change of the subscription state of the video stream. See [SubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#SubscribeStateChangeReason) for more. |


**Notes**

You will receive this callback after calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamvideo).

<span id="IRTCRoomEventHandler-onaudiosubscribestatechanged"></span>
### onAudioSubscribeStateChanged

```cpp
virtual void onAudioSubscribeStateChanged(
            const char* stream_id, const StreamInfo& stream_info, SubscribeState state, SubscribeStateChangeReason reason) {
        (void)stream_id;
        (void)stream_info;
        (void)state;
        (void)reason;
    }
```


> Available since 3.60.


Callback on state changes of the subscription to microphone\-audio streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const StreamInfo& |Stream information. |
|state |SubscribeState |Room state code. See [SubscribeState](https://docs.byteplus.com/en/docs/12/docs-85519#SubscribeState) for more. |
|reason |SubscribeStateChangeReason |The reason for the change of the subscription state of the audio stream. See [SubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#SubscribeStateChangeReason) for more. |


**Notes**

You will receive this callback after calling [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamaudio).

<span id="IRTCRoomEventHandler-ontokenwillexpire"></span>
### onTokenWillExpire

```cpp
virtual void onTokenWillExpire() {
```


The callback is triggered when the SDK detects the joining room privilege from the Token will expires within 30s.

After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-updatetoken) to update the joining room privilege Token.

**Notes**

After a user's joining room privilege expires:


* When attempting to join a room, the user will receive with the error code "\-1000" indicating that the Token is invalid.

* If the user is already in the room, he/she will be removed from the room and receive with the error code "\-1009" indicating that the Token is expired. Remote users in the room will receive [onUserLeave](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onuserleave) with the reason "2" indicating that the Token is invalid.

    &nbsp;


<span id="onpublishprivilegetokenwillexpire"></span>
### onPublishPrivilegeTokenWillExpire

```cpp
virtual void onPublishPrivilegeTokenWillExpire() {
```


Callback triggered 30s before the publishing privilege of the Token expires.

After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-updatetoken) to update the publishing privilege Token.

**Notes**

Once a user's publishing privilege expires:


* Either during stream publishing or when attempting to publish a stream, the user will get the notification of `kPublishStateChangeReasonNoPublishPermission` via [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onaudiopublishstatechanged).

* The publishing streams of the user will be removed, and remote users in the room will get informed via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onuserpublishstreamaudio).

    &nbsp;


<span id="onsubscribeprivilegetokenwillexpire"></span>
### onSubscribePrivilegeTokenWillExpire

```cpp
virtual void onSubscribePrivilegeTokenWillExpire() {
```


Callback triggered 30s before the subscribing privilege of the Token expires.

After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-updatetoken) to update the subscribing privilege Token.

**Notes**

After a user's subscribing privilege expires, the user will get the notification of `kSubscribeStateChangeReasonNoSubscribePermission` via [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCRoomEventHandler-onaudiosubscribestatechanged).

<span id="IRTCRoomEventHandler-onroomstats"></span>
### onRoomStats

```cpp
virtual void onRoomStats(const RtcRoomStats& stats) {
        (void)stats;
    }
```


In\-room call statistics callback.

After the user enters the room and starts the call, he receives this callback every 2s.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |const RtcRoomStats& |Current RtcEngine statistics. See [RtcRoomStats](https://docs.byteplus.com/en/docs/12/docs-85519#RtcRoomStats) |


<span id="IRTCRoomEventHandler-onremotestreamstats"></span>
### onRemoteStreamStats

```cpp
virtual void onRemoteStreamStats(const char* stream_id, const bytertc::StreamInfo& stream_info, const RemoteStreamStats& stats) {
        (void)stream_id;
        (void)stream_info;
        (void)stats;
    }
```


Remote audio/video stream statistics and network quality callbacks for local subscriptions.

After the local user subscribes to the stream successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the subscribed stream during this reference period, including: sending audio & video bit rate, sending frame rate, encoded frame rate, network quality, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const bytertc::StreamInfo& |Stream information. |
|stats |const RemoteStreamStats& |Current RtcEngine statistics. See [RemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteStreamStats) |


<span id="IRTCRoomEventHandler-onuserjoined"></span>
### onUserJoined

```cpp
virtual void onUserJoined(const UserInfo& user_info) {
        (void)user_info;
    }
```


Callback for when a remote visible user joins the room, or when an invisible user in the room switches to being visible.


1. When a remote user sets themselves to be visible by calling the setUserVisibility method and then joins the room, other users in the room will receive this event.

2. When a remote visible user who has been disconnected re\-enters the room, other users in the room will receive this event.

3. When a hidden remote user in the room switches to being visible by calling the setUserVisibility method, other users in the room will receive this event.

4. A new user entering the room will receive an entry callback notification for visible users who were already in the room before they entered.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|user_info |const UserInfo& |See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-85519#UserInfo). |


<span id="IRTCRoomEventHandler-onuserpublishstreamvideo"></span>
### onUserPublishStreamVideo

```cpp
virtual void onUserPublishStreamVideo(const char* stream_id, const StreamInfo& stream_info, bool is_publish){
        (void)stream_id;
        (void)stream_info;
        (void)is_publish;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces the `onUserPublishStream`, `onUserUnpublishStream`, `onUserPublishScreen` and `onUserUnpublishScreen` methods for the functions described below. If you have upgraded to SDK version 3.60 or later and are still using these methods, please migrate to this callback.


Callback on a remote user publishing or stopping publishing video streams in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const StreamInfo& |Stream information. |
|is_publish |bool |Whether the video stream is published.<br><br><br>* `true`: Published.<br><br>* `false`: Stopped publishing. |


**Notes**

You will receive this callback after a remote user successfully published video stream in the room with [publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-publishstreamvideo). Then you can choose whether to call [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamvideo) to subscribe to the streams or not.

<span id="IRTCRoomEventHandler-onuserpublishstreamaudio"></span>
### onUserPublishStreamAudio

```cpp
virtual void onUserPublishStreamAudio(const char* stream_id, const StreamInfo& stream_info, bool is_publish){
        (void)stream_id;
        (void)stream_info;
        (void)is_publish;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces the `onUserPublishStream`, `onUserUnpublishStream`, `onUserPublishScreen` and `onUserUnpublishScreen` methods for the functions described below. If you have upgraded to SDK version 3.60 or later and are still using these methods, please migrate to this callback.


Callback on a remote user publishing or stopping publishing remote audio streams in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const StreamInfo& |Stream information. |
|is_publish |bool |Whether the stream is published.<br><br><br>* `true`: Published.<br><br>* `false`: Stopped publishing. |


**Notes**

You will receive this callback after a remote user successfully published audio streams in the room with [publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-publishstreamaudio). Then you can choose whether to call [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamaudio) to subscribe to the streams or not.

<span id="IRTCRoomEventHandler-onvideostreambanned"></span>
### onVideoStreamBanned

```cpp
virtual void onVideoStreamBanned(const char* uid, bool banned) {
        (void)uid;
        (void)banned;
    }
```


All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the video stream that was disabled/unbanned |
|banned |bool |Video stream sending status<br><br><br>&nbsp;<br><br>* true: Video stream sending was disabled<br><br>* false: Video stream sending was unbanned |


**Notes**


* When the specified user in the room is disabled/unbanned Video stream sending, all users in the room will receive the callback.

* If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

* After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

* If the Audio selection is enabled in the console, only the user whose stream is banned will receive this callback.

    &nbsp;


<span id="onavsyncstatechange"></span>
### onAVSyncStateChange

```cpp
virtual void onAVSyncStateChange(AVSyncState state) {
        (void)state;
    }
```


Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setmultideviceavsync) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |AVSyncState |A/V synchronization state, see [AVSyncState](https://docs.byteplus.com/en/docs/12/docs-85519#AVSyncState). |


<span id="IRTCRoomEventHandler-onaudiostreambanned"></span>
### onAudioStreamBanned

```cpp
virtual void onAudioStreamBanned(const char* uid, bool banned) {
        (void)uid;
        (void)banned;
    }
```


All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |Disabled/unbanned audio stream user ID |
|banned |bool |Audio stream sending status<br><br><br>&nbsp;<br><br>* true: audio stream sending is disabled<br><br>* false: audio stream sending is unbanned |


**Notes**


* Specified users in the room are prohibited/all users in the room when audio stream sending is unbanned Will receive the callback.

* If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

* After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

* The same room is created again after dissolution, and the state in the room is empty.

* If the Audio selection is enabled in the console, only the user whose stream is banned will receive this callback.

    &nbsp;


<span id="onforwardstreamstatechanged"></span>
### onForwardStreamStateChanged

```cpp
virtual void onForwardStreamStateChanged(
    ForwardStreamStateInfo* infos,
    int info_count
) {
    }
```


Callback returning the state and errors during relaying the media stream to each of the rooms

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|infos |ForwardStreamStateInfo\* |Array of the state and errors of each target room. Refer to [ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-85519#ForwardStreamStateInfo) for more information. |
|info_count |int |The number of the target rooms |


<span id="IRTCRoomEventHandler-onforwardstreamevent"></span>
### onForwardStreamEvent

```cpp
virtual void onForwardStreamEvent(
    ForwardStreamEventInfo* infos,
    int info_count
) {
    }
```


Callback returning the events during relaying the media stream to each room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|infos |ForwardStreamEventInfo\* |Array of the event of each target room. Refer to [ForwardStreamEventInfo](https://docs.byteplus.com/en/docs/12/docs-85519#ForwardStreamEventInfo) for more information. |
|info_count |int |The number of the target rooms |


<span id="IRTCRoomEventHandler-onnetworkquality"></span>
### onNetworkQuality

```cpp
virtual void onNetworkQuality(
    const NetworkQualityStats& local_quality,
    const NetworkQualityStats* remote_qualities,
    int remote_quality_num
) {
    }
```


Report the network quality of the users every 2s after the local user joins the room and starts publishing or subscribing to a stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|local_quality |const NetworkQualityStats& |Local network quality. Refer to [NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-85519#NetworkQualityStats) for details. |
|remote_qualities |const NetworkQualityStats\* |Network quality of the subscribed users. Refer to [NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-85519#NetworkQualityStats) for details. |
|remote_quality_num |int |Array length of `remoteQualities` |


<span id="IRTCRoomEventHandler-onsetroomextrainforesult"></span>
### onSetRoomExtraInfoResult

```cpp
virtual void onSetRoomExtraInfoResult(int64_t task_id, SetRoomExtraInfoResult result) {
        (void)task_id;
        (void)result;
    }
```


> Available since 3.52.


Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setroomextrainfo) to set extra information about the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|task_id |int64_t |The task ID of the API call. |
|result |SetRoomExtraInfoResult |See [SetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-85519#SetRoomExtraInfoResult) for the setting results and reasons. |


<span id="IRTCRoomEventHandler-onroomextrainfoupdate"></span>
### onRoomExtraInfoUpdate

```cpp
virtual void onRoomExtraInfoUpdate(const char*key, const char* value, const char* last_update_user_id, int64_t last_update_time_ms) {
        (void)key;
        (void)value;
        (void)last_update_user_id;
        (void)last_update_time_ms;
    }
```


> Available since 3.52.


Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setroomextrainfo).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |const char\* |Key of the extra information. |
|value |const char\* |Content of the extra information. |
|last_update_user_id |const char\* |The ID of the last user who updated this information. |
|last_update_time_ms |int64_t |The Unix time in ms when this information was last updated. |


**Notes**

The user will receive the all the historical information in the room once the user joins the room.

<span id="IRTCRoomEventHandler-onroomstreamextrainfoupdate"></span>
### onRoomStreamExtraInfoUpdate

```cpp
virtual void onRoomStreamExtraInfoUpdate(const char* stream_id, const StreamInfo& stream_info, const char* extra_info) {
        (void)stream_id;
        (void)stream_info;
        (void)extra_info;
    }
```


> Available since 3.60.


Callback used to receive the extra information set by the other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setstreamextrainfo).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID |
|stream_info |const StreamInfo& |Stream information. Refer to [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) for details. |
|extra_info |const char\* |Content of the extra information. |


**Notes**

The user will receive the all the historical information in the room once the user joins the room.

<span id="IRTCRoomEventHandler-onuservisibilitychanged"></span>
### onUserVisibilityChanged

```cpp
virtual void onUserVisibilityChanged(bool current_user_visibility, UserVisibilityChangeError error_code) {
        (void)current_user_visibility;
        (void)error_code;
    }
```


> Available since 3.54


Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setuservisibility).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|current_user_visibility |bool |Visibility of the current user.<br><br><br>&nbsp;<br><br>* true: Visible. The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* false: Invisible. The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |
|error_code |UserVisibilityChangeError |Error code for setting user visibility. See [UserVisibilityChangeError](https://docs.byteplus.com/en/docs/12/docs-85519#UserVisibilityChangeError). |


<span id="IRTCRoomEventHandler-onavsyncevent"></span>
### onAVSyncEvent

```cpp
virtual void onAVSyncEvent(
    const char* room_id,
    const char* uid,
    AVSyncEvent event
) {
    }
```


> Available since 3.60.


Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setmultideviceavsync) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |Room ID. |
|uid |const char\* |User ID. |
|event |AVSyncEvent |A/V synchronization error, see [AVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-85519#AVSyncEvent). |


<span id="IExternalVideoEncoderEventHandler"></span>
# IExternalVideoEncoderEventHandler

```cpp
class bytertc::IExternalVideoEncoderEventHandler
```


Custom coded frame callback class

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onStart](https://docs.byteplus.com/en/docs/12/25050#IExternalVideoEncoderEventHandler-onstart) |
|virtual void |[onStop](https://docs.byteplus.com/en/docs/12/25050#IExternalVideoEncoderEventHandler-onstop) |
|virtual void |[onRateUpdate](https://docs.byteplus.com/en/docs/12/25050#IExternalVideoEncoderEventHandler-onrateupdate) |
|virtual void |[onRequestKeyFrame](https://docs.byteplus.com/en/docs/12/25050#IExternalVideoEncoderEventHandler-onrequestkeyframe) |
|virtual void |[onActiveVideoLayer](https://docs.byteplus.com/en/docs/12/25050#IExternalVideoEncoderEventHandler-onactivevideolayer) |


<span id="instructions"></span>
## Instructions

<span id="IExternalVideoEncoderEventHandler-onstart"></span>
### onStart

```cpp
virtual void onStart(
    const char* stream_id,
    const StreamInfo& stream_info
) = 0;
```


Prompt custom encoded frames to start pushing callbacks.

After receiving this callback, you can call [pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-pushexternalencodedvideoframe) to push a custom encoded video frame to the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Encoded stream ID |
|stream_info |const StreamInfo& |Encoded stream information. Refer to [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |


<span id="IExternalVideoEncoderEventHandler-onstop"></span>
### onStop

```cpp
virtual void onStop(
    const char* stream_id,
    const StreamInfo& stream_info
) = 0;
```


When you receive the callback, you need to stop pushing custom encoded video frames to the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Encoded stream ID |
|stream_info |const StreamInfo& |Encoded stream information. Refer to [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |


<span id="IExternalVideoEncoderEventHandler-onrateupdate"></span>
### onRateUpdate

```cpp
virtual void onRateUpdate(
    const char* stream_id,
    const StreamInfo& stream_info,
    int32_t video_index,
    VideoRateInfo info
) = 0;
```


When the frame rate or bit rate of a custom encoded stream changes, the callback is triggered

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote encoded stream ID |
|stream_info |const StreamInfo& |Remote encoded stream information. Refer to [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|video_index |int32_t |The subscript of the corresponding encoded stream |
|info |VideoRateInfo |The encoded stream information after the change. See [VideoRateInfo](https://docs.byteplus.com/en/docs/12/docs-85519#VideoRateInfo) |


<span id="IExternalVideoEncoderEventHandler-onrequestkeyframe"></span>
### onRequestKeyFrame

```cpp
virtual void onRequestKeyFrame(
    const char* stream_id,
    const StreamInfo& stream_info,
    int32_t video_index
) = 0;
```


This callback is used to inform the stream publisher that a keyframe needs to be regenerated.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote encoded stream ID |
|stream_info |const StreamInfo& |Remote encoded stream information. Refer to [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|video_index |int32_t |The subscript of the corresponding encoded stream |


<span id="IExternalVideoEncoderEventHandler-onactivevideolayer"></span>
### onActiveVideoLayer

```cpp
virtual void onActiveVideoLayer(
    const char* stream_id,
    const StreamInfo& stream_info,
    int32_t video_index,
    bool active
) = 0;
```


> Available since 3.56


As the sender of a external encoded video stream, you will receive this callback at certain moments.

Based on the hints of this callback, you can selectively encode the video stream that is ready for transmission, in order to reduce the performance impact of video encoding on the local device. This callback is triggered based on a combination of factors, including the performance of the local device, the local network, and whether the stream is subscribed by the remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote encoded stream ID |
|stream_info |const StreamInfo& |Remote encoded stream information. Refer to [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|video_index |int32_t |Subscript of the corresponding encoded stream. |
|active |bool |The active state of the corresponding encoded stream. |


**Notes**

To receive the callback, call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideosourcetype) to set the input video source to custom encoded video and call [setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setexternalvideoencodereventhandler) to set the callback handler.

<span id="IMediaPlayerAudioFrameObserver"></span>
# IMediaPlayerAudioFrameObserver

```cpp
class bytertc::IMediaPlayerAudioFrameObserver
```


observer for the audio frames during local audio file mixing.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onFrame](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerAudioFrameObserver-onframe) |


<span id="instructions"></span>
## Instructions

<span id="IMediaPlayerAudioFrameObserver-onframe"></span>
### onFrame

```cpp
virtual void onFrame(
    int player_id,
    const IAudioFrame& frame
) = 0;
```


The callback for the audio frames during local audio file mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player_id |int |Player's ID |
|frame |const IAudioFrame& |See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame). |


<span id="IFaceDetectionObserver"></span>
# IFaceDetectionObserver

```cpp
class bytertc::IFaceDetectionObserver
```


Face detection observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onFaceDetectResult](https://docs.byteplus.com/en/docs/12/25050#IFaceDetectionObserver-onfacedetectresult) |


<span id="instructions"></span>
## Instructions

<span id="IFaceDetectionObserver-onfacedetectresult"></span>
### onFaceDetectResult

```cpp
virtual void onFaceDetectResult(const FaceDetectResult& result) = 0;
```


Callback of the result of face detection with Effect SDK.

After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|result |const FaceDetectResult& |Face detection result. See [FaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-85519#FaceDetectResult). |


<span id="IMediaPlayerCustomSourceProvider"></span>
# IMediaPlayerCustomSourceProvider

```cpp
class bytertc::IMediaPlayerCustomSourceProvider
```


In\-memory audio data playing callback interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int |[onReadData](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerCustomSourceProvider-onreaddata) |
|virtual int64_t |[onSeek](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerCustomSourceProvider-onseek) |
|virtual |[~IMediaPlayerCustomSourceProvider](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerCustomSourceProvider-~imediaplayercustomsourceprovider) |


<span id="instructions"></span>
## Instructions

<span id="IMediaPlayerCustomSourceProvider-onreaddata"></span>
### onReadData

```cpp
virtual int onReadData(
    uint8_t*buffer,
    int buffer_size
) = 0;
```


> Available since 3.53


Callback of getting the path and size of the audio data you input.

When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, this callback will be triggered and you need to enter the path and size of the audio data.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|buffer |uint8_t\* |The path of the audio data you input. The size of audio data should be equal to or less than the value of bufferSize. The supported formats are: mp3, aac, m4a, 3gp, wav. |
|buffer_size |int |The size of the audio data, in bytes. If you want to stop audio playing, you can enter a figure less than or equal to zero into bufferSize and then SDK will stop calling this callback. |


**Return Value**

Returns the size of the audio data that are actually read.

**Notes**

If calling [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource) API failed, please enter 0 into buffer and bufferSize. In this situation, SDK will stop calling this callback.

<span id="IMediaPlayerCustomSourceProvider-onseek"></span>
### onSeek

```cpp
virtual int64_t onSeek(
    int64_t offset,
    MediaPlayerCustomSourceSeekWhence whence
) = 0;
```


> Available since 3.53


Seeking the audio data based on the set starting position and offset to help SDK read and analyze data.

When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, or when you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setposition) to set the starting position of audio playing, this callback will be trigerred and you need to seek the audio data accorring to the value of offset and whence.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|offset |int64_t |The offset of the target position relative to the starting position, in bytes. The value can be positive or negative. |
|whence |MediaPlayerCustomSourceSeekWhence |The starting position of the seeking. Refer to [MediaPlayerCustomSourceSeekWhence](https://docs.byteplus.com/en/docs/12/docs-85519#MediaPlayerCustomSourceSeekWhence) for more details. |


**Return Value**

If the seeking succeeded, the information on the final adjusted play position after seeking or the size of the audio data will be returned.

If the seeking failed, \-1 will be returned.

<span id="IMediaPlayerCustomSourceProvider-~imediaplayercustomsourceprovider"></span>
### ~IMediaPlayerCustomSourceProvider

```cpp
virtual ~IMediaPlayerCustomSourceProvider() {}
```


<span id="IAudioFrameObserver"></span>
# IAudioFrameObserver

```cpp
class bytertc::IAudioFrameObserver
```


Audio data callback observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

The time interval for all callback functions in this interface is 20 ms.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameObserver-onrecordaudioframe) |
|virtual void |[onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameObserver-onplaybackaudioframe) |
|virtual void |[onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameObserver-onremoteuseraudioframe) |
|virtual void |[onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameObserver-onmixedaudioframe) |
|virtual void |[onRecordScreenAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameObserver-onrecordscreenaudioframe) |
|virtual void |[onCaptureMixedAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameObserver-oncapturemixedaudioframe) |


<span id="instructions"></span>
## Instructions

<span id="IAudioFrameObserver-onrecordaudioframe"></span>
### onRecordAudioFrame

```cpp
virtual void onRecordAudioFrame(const IAudioFrame& audio_frame) = 0;
```


Returns audio data recorded by microphone

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |const IAudioFrame& |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


<span id="IAudioFrameObserver-onplaybackaudioframe"></span>
### onPlaybackAudioFrame

```cpp
virtual void onPlaybackAudioFrame(const IAudioFrame& audio_frame) = 0;
```


Returns the mixed audio data of all subscribed remote users

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |const IAudioFrame& |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


<span id="IAudioFrameObserver-onremoteuseraudioframe"></span>
### onRemoteUserAudioFrame

```cpp
virtual void onRemoteUserAudioFrame(
    const char* stream_id,
    const StreamInfo& stream_info,
    const IAudioFrame& audio_frame
) = 0;
```


Returns the audio data of one remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote stream ID. |
|stream_info |const StreamInfo& |Remote stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|audio_frame |const IAudioFrame& |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


**Notes**

This callback works on the playback thread. Don't do anything time\-consuming in this callback, or it may affect the entire audio playback chain.

<span id="IAudioFrameObserver-onmixedaudioframe"></span>
### onMixedAudioFrame

```cpp
virtual void onMixedAudioFrame(const IAudioFrame& audio_frame) = 0;
```


Returns mixed audio data including both data recorded by the local microphone and data from all subscribed remote users

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |const IAudioFrame& |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


<span id="IAudioFrameObserver-onrecordscreenaudioframe"></span>
### onRecordScreenAudioFrame

```cpp
virtual void onRecordScreenAudioFrame(const IAudioFrame& audio_frame) {
    }
```


Returns the audio data played locally

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |const IAudioFrame& |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


<span id="IAudioFrameObserver-oncapturemixedaudioframe"></span>
### onCaptureMixedAudioFrame

```cpp
virtual void onCaptureMixedAudioFrame(const IAudioFrame& audio_frame) = 0;
```


Return the mixed audio data of the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |const IAudioFrame& |Audio data. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


<span id="IRTSRoomEventHandler"></span>
# IRTSRoomEventHandler

```cpp
class bytertc::IRTSRoomEventHandler
```


Audio & video room event callback interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onroomstatechanged) |
|virtual void |[onLeaveRoom](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onleaveroom) |
|virtual void |[onUserJoined](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onuserjoined) |
|virtual void |[onUserLeave](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onuserleave) |
|virtual void |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onroommessagereceived) |
|virtual void |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onroombinarymessagereceived) |
|virtual void |[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onroommessagesendresult) |
|virtual void |[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onusermessagereceived) |
|virtual void |[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onuserbinarymessagereceived) |
|virtual void |[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onusermessagesendresult) |
|virtual void |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onroommessagereceived-2) |
|virtual void |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onroombinarymessagereceived-2) |
|virtual void |[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onusermessagereceived-2) |
|virtual void |[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onuserbinarymessagereceived-2) |


<span id="instructions"></span>
## Instructions

<span id="IRTSRoomEventHandler-onroomstatechanged"></span>
### onRoomStateChanged

```cpp
virtual void onRoomStateChanged(const char* room_id, const char* uid,
            int state, const char* extra_info) {
        (void)room_id;
        (void)state;
        (void)extra_info;
    }
```


Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |Room ID. |
|uid |const char\* |User ID. |
|state |int |Room state code.<br><br><br>&nbsp;<br><br>* 0: Join room success.<br><br>* !0: Failed to join a room, abnormal exit, room\-related warnings or errors. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#ErrorCode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-85518#WarningCode) for specific indications. |
|extra_info |const char\* |Extra information.<br><br>`join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` means the user rejoins the room.<br><br>&nbsp;<br><br>`elapsed` indicates the time interval from calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-joinroom) to successfully joining room, in ms. |


<span id="IRTSRoomEventHandler-onleaveroom"></span>
### onLeaveRoom

```cpp
virtual void onLeaveRoom(const RtcRoomStats& stats) {
        (void)stats;
    }
```


Leave the room callback.

After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-leaveroom) method, the SDK stops all publishing subscription streams and notifies the user to leave the room successfully through this callback after releasing all audio & video resources related to the call.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |const RtcRoomStats& |Reserved parameter, currently empty. |


**Notes**


* After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-leaveroom) method to leave the room, if [destroy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-destroy) is called to destroy the room instance method is called to destroy the RTS engine immediately, this callback event will not be received.

* If the app needs to use the system audio & video device after leaving the room, it is recommended to initialize the audio & video device after receiving this callback, otherwise the initialization may fail due to the SDK occupying the audio & video device.


<span id="IRTSRoomEventHandler-onuserjoined"></span>
### onUserJoined

```cpp
virtual void onUserJoined(const UserInfo& user_info) {
        (void)user_info;
    }
```


Callback about remote users joining the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|user_info |const UserInfo& |See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-85519#UserInfo). |


<span id="IRTSRoomEventHandler-onuserleave"></span>
### onUserLeave

```cpp
virtual void onUserLeave(const char* uid, UserOfflineReason reason) {
        (void)uid;
        (void)reason;
    }
```


This callback is triggered when a remote user is disconnected.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |ID of the user who leaves the room. |
|reason |UserOfflineReason |Reason to leave the room. See [UserOfflineReason](https://docs.byteplus.com/en/docs/12/docs-85519#UserOfflineReason). |


<span id="IRTSRoomEventHandler-onroommessagereceived"></span>
### onRoomMessageReceived

```cpp
virtual void onRoomMessageReceived(const char* uid, const char* message) {
        (void)uid;
        (void)message;
    }
```


Receives a callback for broadcast messages in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the message sender. |
|message |const char\* |The content of the received message. |


**Notes**

Other users in the same room will receive this callback when they call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendroommessage) to send a broadcast message.

<span id="IRTSRoomEventHandler-onroombinarymessagereceived"></span>
### onRoomBinaryMessageReceived

```cpp
virtual void onRoomBinaryMessageReceived(const char* uid, int size, const uint8_t* message) {
        (void)uid;
        (void)size;
        (void)message;
    }
```


Receives a callback to a binary broadcast message in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the message sender. |
|size |int |The length of the received binary message. |
|message |const uint8_t\* |The content of the received binary message. |


**Notes**

Other users in the same room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendroombinarymessage) Receive this callback when sending a binary broadcast message.

<span id="IRTSRoomEventHandler-onroommessagesendresult"></span>
### onRoomMessageSendResult

```cpp
virtual void onRoomMessageSendResult(int64_t msgid, int error) {
        (void)msgid;
        (void)error;
    }
```


When the [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendroommessage) function is called to send a message, the sending result of this message (feedback) is called back.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |ID of this message |
|error |int |Message sending result<br><br>&nbsp;<br><br>See [RoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85519#RoomMessageSendResult) |


<span id="IRTSRoomEventHandler-onusermessagereceived"></span>
### onUserMessageReceived

```cpp
virtual void onUserMessageReceived(const char* uid, const char* message) {
        (void)uid;
        (void)message;
    }
```


> The interface will be deprecated in version 3.64. Please use [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onusermessagereceived-2) instead.

> Receive this callback when you receive a text message (P2P) from another user in the room.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the message sender. |
|message |const char\* |The content of the received text message. |


**Notes**

You must call the [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendusermessage) method before you can receive the callback.

<span id="IRTSRoomEventHandler-onuserbinarymessagereceived"></span>
### onUserBinaryMessageReceived

```cpp
virtual void onUserBinaryMessageReceived(const char* uid, int size, const uint8_t* message) {
        (void)uid;
        (void)size;
        (void)message;
    }
```


A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room.

> The callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTSRoomEventHandler-onuserbinarymessagereceived-2) instead.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the message sender. |
|size |int |The length of the binary message. |
|message |const uint8_t\* |The content of the received binary message. |


<span id="IRTSRoomEventHandler-onusermessagesendresult"></span>
### onUserMessageSendResult

```cpp
virtual void onUserMessageSendResult(int64_t msgid, int error) {
        (void)msgid;
        (void)error;
    }
```


After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |The ID of this message. |
|error |int |Text or binary message sending results. See [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85518#UserMessageSendResult) |


**Notes**

You must first call the [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendusermessage) or [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-senduserbinarymessage) interface to receive this callback.

<span id="IRTSRoomEventHandler-onroommessagereceived-2"></span>
### onRoomMessageReceived

```cpp
virtual void onRoomMessageReceived(int64_t msgid, const char* uid, const char* message) {
        (void)msgid;
        (void)uid;
        (void)message;
    }
```


Callback for receiving room messages.

Other users in the same room will receive this callback when they call [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendusermessage) to send a broadcast message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |Message ID. |
|uid |const char\* |User ID of the message sender. |
|message |const char\* |Content of the received message. |


<span id="IRTSRoomEventHandler-onroombinarymessagereceived-2"></span>
### onRoomBinaryMessageReceived

```cpp
virtual void onRoomBinaryMessageReceived(int64_t msgid, const char* uid, const uint8_t* message, int size) {
        (void)msgid;
        (void)uid;
        (void)message;
        (void)size;
    }
```


Receives a callback to a binary broadcast message in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |Message number. |
|uid |const char\* |User ID of the message sender. |
|message |const uint8_t\* |The content of the received binary message.. |
|size |int |Length of the received binary message. |


**Notes**

Other users in the same room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendroombinarymessage) Receive this callback when sending a binary broadcast message.

<span id="IRTSRoomEventHandler-onusermessagereceived-2"></span>
### onUserMessageReceived

```cpp
virtual void onUserMessageReceived(int64_t msgid, const char* uid, const char* message) {
        (void)msgid;
        (void)uid;
        (void)message;
    }
```


Receive this callback when you receive a text message (P2P) from another user in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |Message number. |
|uid |const char\* |User ID of the message sender. |
|message |const char\* |The content of the received text message. |


**Notes**

You must call the [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendusermessage) method before you can receive the callback.

<span id="IRTSRoomEventHandler-onuserbinarymessagereceived-2"></span>
### onUserBinaryMessageReceived

```cpp
virtual void onUserBinaryMessageReceived(int64_t msgid, const char* uid, const uint8_t* message, int size) {
        (void)msgid;
        (void)uid;
        (void)message;
        (void)size;
    }
```


A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |Message number. |
|uid |const char\* |User ID of the message sender. |
|message |const uint8_t\* |The content of the received binary message. |
|size |int |Length of the received binary message. |


<span id="IMediaPlayerEventHandler"></span>
# IMediaPlayerEventHandler

```cpp
class bytertc::IMediaPlayerEventHandler
```


Event handler for [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer). You must call [setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-seteventhandler) to set the corresponding event handler to get the events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual |[~IMediaPlayerEventHandler](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerEventHandler-~imediaplayereventhandler) |
|virtual void |[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerEventHandler-onmediaplayerstatechanged) |
|virtual void |[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |
|virtual void |[onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerEventHandler-onmediaplayerevent) |


<span id="instructions"></span>
## Instructions

<span id="IMediaPlayerEventHandler-~imediaplayereventhandler"></span>
### ~IMediaPlayerEventHandler

```cpp
virtual ~IMediaPlayerEventHandler() {}
```


<span id="IMediaPlayerEventHandler-onmediaplayerstatechanged"></span>
### onMediaPlayerStateChanged

```cpp
virtual void onMediaPlayerStateChanged(
    int player_id,
    PlayerState state,
    PlayerError error
) = 0;
```


Callback for audio mixing status change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player_id |int |The ID of [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer). Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getmediaplayer). |
|state |PlayerState |See [PlayerState](https://docs.byteplus.com/en/docs/12/docs-85519#PlayerState). |
|error |PlayerError |See [PlayerError](https://docs.byteplus.com/en/docs/12/docs-85519#PlayerError). |


<span id="IMediaPlayerEventHandler-onmediaplayerplayingprogress"></span>
### onMediaPlayerPlayingProgress

```cpp
virtual void onMediaPlayerPlayingProgress(
    int player_id,
    int64_t progress
) = 0;
```


Periodic callback for audio mixing progress. The period is set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setprogressinterval).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player_id |int |The ID of [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer). Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getmediaplayer). |
|progress |int64_t |Mixing progress in ms. |


<span id="IMediaPlayerEventHandler-onmediaplayerevent"></span>
### onMediaPlayerEvent

```cpp
virtual void onMediaPlayerEvent(
    int player_id,
    PlayerEvent event,
    const char* message
) = 0;
```


> Available since 3.59


Callback for media player events. You would receive the notification after calling [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-selectaudiotrack) and [setPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setposition).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player_id |int |The ID of the [IMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer). You can specify the ID via [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getmediaplayer). |
|event |PlayerEvent |The event of the player. |
|message |const char\* |The description of the event. It may be empty. |


<span id="IRTCEngineEventHandler"></span>
# IRTCEngineEventHandler

```cpp
class bytertc::IRTCEngineEventHandler
```


Audio & video engine event callback interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onWarning](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onwarning) |
|virtual void |[onError](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onerror) |
|virtual void |[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onextensionaccesserror) |
|virtual void |[onLogReport](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onlogreport) |
|virtual void |[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onconnectionstatechanged) |
|virtual void |[onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onnetworktypechanged) |
|virtual void |[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onsimulcastsubscribefallback) |
|virtual void |[onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onperformancealarms) |
|virtual void |[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudiodevicestatechanged) |
|virtual void |[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onvideodevicestatechanged) |
|virtual void |[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudiodevicewarning) |
|virtual void |[onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onvideodevicewarning) |
|virtual void |[onSysStats](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onsysstats) |
|virtual void |[onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onrecordingstateupdate) |
|virtual void |[onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onrecordingprogressupdate) |
|virtual void |[onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudiorecordingstateupdate) |
|virtual void |[onLoginResult](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onloginresult) |
|virtual void |[onLogout](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onlogout) |
|virtual void |[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onserverparamssetresult) |
|virtual void |[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-ongetpeeronlinestatus) |
|virtual void |[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) |
|virtual void |[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) |
|virtual void |[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) |
|virtual void |[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) |
|virtual void |[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) |
|virtual void |[onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onservermessagesendresult) |
|virtual void |[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onseimessagereceived) |
|virtual void |[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onseistreamupdate) |
|virtual void |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onremoteaudiopropertiesreport) |
|virtual void |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onlocalaudiopropertiesreport) |
|virtual void |[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudioplaybackdevicetestvolume) |
|virtual void |[onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudiodevicevolumechanged) |
|virtual void |[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onlocalaudiostatechanged) |
|virtual void |[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onuserstartaudiocapture) |
|virtual void |[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onuserstopaudiocapture) |
|virtual void |[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onactivespeaker) |
|virtual void |[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onstreamsyncinforeceived) |
|virtual void |[onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onnetworkdetectionresult) |
|virtual void |[onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onnetworkdetectionstopped) |
|virtual void |[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onuserstartvideocapture) |
|virtual void |[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onuserstopvideocapture) |
|virtual void |[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onlocalvideosizechanged) |
|virtual void |[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onremotevideosizechanged) |
|virtual void |[onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) |
|virtual void |[onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onfirstremoteaudioframe) |
|virtual void |[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onremoteaudiostatechanged) |
|virtual void |[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onlocalvideostatechanged) |
|virtual void |[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onremotevideostatechanged) |
|virtual void |[onAudioFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudioframesendstatechanged) |
|virtual void |[onVideoFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onvideoframesendstatechanged) |
|virtual void |[onFirstRemoteVideoFrameRendered](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onfirstremotevideoframerendered) |
|virtual void |[onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onfirstremotevideoframedecoded) |
|virtual void |[onAudioFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudioframeplaystatechanged) |
|virtual void |[onVideoFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onvideoframeplaystatechanged) |
|virtual void |[onFirstLocalAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onfirstlocalaudioframe) |
|virtual void |[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-oncloudproxyconnected) |
|virtual void |[onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onlocalproxystatechanged) |
|virtual void |[deprecated] [onAudioMixingPlayingProgress](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onaudiomixingplayingprogress) |


<span id="instructions"></span>
## Instructions

<span id="IRTCEngineEventHandler-onwarning"></span>
### onWarning

```cpp
virtual void onWarning(int warn) {
        (void)warn;
    }
```


A warning occurred during the SDK runtime. The SDK usually recovers automatically and warnings can be ignored.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|warn |int |Warning identification code, see: [WarningCode](https://docs.byteplus.com/en/docs/12/docs-85518#WarningCode) |


<span id="IRTCEngineEventHandler-onerror"></span>
### onError

```cpp
virtual void onError(int err) {
        (void)err;
    }
```


Error callback occurred. This callback is triggered when a network or media\-related error occurs during the

SDK runtime and cannot be automatically recovered and you may need to intervene.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|err |int |Error code. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#ErrorCode) |


<span id="IRTCEngineEventHandler-onextensionaccesserror"></span>
### onExtensionAccessError

```cpp
virtual void onExtensionAccessError(
    const char* extension_name,
    const char* msg
) {
```


> Available since 3.52


Failed to access the extension.

RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|extension_name |const char\* |The name of extension. |
|msg |const char\* |Error message. |


<span id="IRTCEngineEventHandler-onlogreport"></span>
### onLogReport

```cpp
virtual void onLogReport(const char* log_type, const char* log_content) {
        (void)log_type;
        (void)log_content;
    }
```


Terminal monitoring log callback. The callback is triggered when a terminal monitoring event is generated.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|log_type |const char\* |Event type. The current type is fixed to "live_webrtc_monitor_log". |
|log_content |const char\* |Terminal monitoring log content. |


<span id="IRTCEngineEventHandler-onconnectionstatechanged"></span>
### onConnectionStateChanged

```cpp
virtual void onConnectionStateChanged(bytertc::ConnectionState state) {
    }
```


SDK connection state change callback with signaling server. Triggered when the connection state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |bytertc::ConnectionState |The current connection status between the SDK and the signaling server. See [ConnectionState](https://docs.byteplus.com/en/docs/12/docs-85519#ConnectionState) |


**Notes**

Refer to [Getting Connection Status](https://docs.byteplus.com/byteplus-rtc/docs/95376) for more details.

<span id="IRTCEngineEventHandler-onnetworktypechanged"></span>
### onNetworkTypeChanged

```cpp
virtual void onNetworkTypeChanged(bytertc::NetworkType type) {
    }
```


SDK Current network connection type change callback. Callbacks the event when the current network connection type of the SDK changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |bytertc::NetworkType |SDK The current network connection type, see: [NetworkType](https://docs.byteplus.com/en/docs/12/docs-85519#NetworkType). |


<span id="IRTCEngineEventHandler-onsimulcastsubscribefallback"></span>
### onSimulcastSubscribeFallback

```cpp
virtual void onSimulcastSubscribeFallback(const char* stream_id, const StreamInfo& stream_info, const bytertc::RemoteStreamSwitch& event) {
         (void)stream_id;
         (void)stream_info;
         (void)event;
     }
```


This callback is triggered when media streams start to fall back or restore from a fallback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID |
|stream_info |const StreamInfo& |Stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|event |const bytertc::RemoteStreamSwitch& |Information about the fallback. See [RemoteStreamSwitch](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteStreamSwitch). |


<span id="IRTCEngineEventHandler-onperformancealarms"></span>
### onPerformanceAlarms

```cpp
virtual void onPerformanceAlarms(const char* stream_id, const StreamInfo& stream_info, bytertc::PerformanceAlarmMode mode,
            bytertc::PerformanceAlarmReason reason, const bytertc::SourceWantedData& data) {
        (void)stream_id;
        (void)stream_info;
        (void)mode;
        (void)reason;
        (void)data;
    }
```


When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setpublishfallbackoption) is not turned on locally, and when insufficient device performance is detected, this callback is received.

When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setpublishfallbackoption) is locally turned on, and when the publish performance fallback/recovery is caused due to device performance/network reasons, this callback is received.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID |
|stream_info |const StreamInfo& |Stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|mode |bytertc::PerformanceAlarmMode |Indicates whether the publish performance fallback function is turned on locally. See [PerformanceAlarmMode](https://docs.byteplus.com/en/docs/12/docs-85519#PerformanceAlarmMode)<br><br><br>&nbsp;<br><br>* When the publisher does not turn on the publish performance fallback, the mode value is kPerformanceAlarmModeNormal.<br><br>* When the publisher turns on the publish performance fallback, the mode value is kPerformanceAlarmModeSimulcast. |
|reason |bytertc::PerformanceAlarmReason |Reason for the alarm. See [PerformanceAlarmReason](https://docs.byteplus.com/en/docs/12/docs-85519#PerformanceAlarmReason) |
|data |const bytertc::SourceWantedData& |Performance fallback related data. See [SourceWantedData](https://docs.byteplus.com/en/docs/12/docs-85519#SourceWantedData). |


<span id="IRTCEngineEventHandler-onaudiodevicestatechanged"></span>
### onAudioDeviceStateChanged

```cpp
virtual void onAudioDeviceStateChanged(const char* device_id, bytertc::RTCAudioDeviceType device_type,
            bytertc::MediaDeviceState device_state, bytertc::MediaDeviceError device_error) {
        (void)device_id;
        (void)device_type;
        (void)device_state;
        (void)device_error;
    }
```


Callback of audio device state. Audio devices include audio capture devices and audio playback devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char\* |Device ID |
|device_type |bytertc::RTCAudioDeviceType |Device type. Refer to [RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-85519#RTCAudioDeviceType) for more details. |
|device_state |bytertc::MediaDeviceState |Device state. Refer to [MediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-85519#MediaDeviceState) for more details. |
|device_error |bytertc::MediaDeviceError |Device error. Refer to [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-85519#MediaDeviceError) for more details. |


<span id="IRTCEngineEventHandler-onvideodevicestatechanged"></span>
### onVideoDeviceStateChanged

```cpp
virtual void onVideoDeviceStateChanged(const char* device_id, bytertc::RTCVideoDeviceType device_type,
            bytertc::MediaDeviceState device_state, bytertc::MediaDeviceError device_error) {
        (void)device_id;
        (void)device_type;
        (void)device_state;
        (void)device_error;
    }
```


Callback of video device state. Video devices include cameras and screen sharing video capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char\* |Device ID |
|device_type |bytertc::RTCVideoDeviceType |Device type. Refer to [RTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-85519#RTCVideoDeviceType) for more details. |
|device_state |bytertc::MediaDeviceState |Device state. Refer to [MediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-85519#MediaDeviceState) for more details. |
|device_error |bytertc::MediaDeviceError |Device error. Refer to [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-85519#MediaDeviceError) for more details. |


<span id="IRTCEngineEventHandler-onaudiodevicewarning"></span>
### onAudioDeviceWarning

```cpp
virtual void onAudioDeviceWarning(const char* device_id, bytertc::RTCAudioDeviceType device_type,
            bytertc::MediaDeviceWarning device_warning) {
        (void)device_id;
        (void)device_type;
        (void)device_warning;
    }
```


Audio device warning callback. The audio devices include audio capture devices and audio rendering devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char\* |Device ID |
|device_type |bytertc::RTCAudioDeviceType |Device type. See [RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-85519#RTCAudioDeviceType) |
|device_warning |bytertc::MediaDeviceWarning |Device error type. See [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85519#MediaDeviceWarning) |


<span id="IRTCEngineEventHandler-onvideodevicewarning"></span>
### onVideoDeviceWarning

```cpp
virtual void onVideoDeviceWarning(const char* device_id, bytertc::RTCVideoDeviceType device_type,
            bytertc::MediaDeviceWarning device_warning) {
        (void)device_id;
        (void)device_type;
        (void)device_warning;
    }
```


Video device warning callback. The video devices include video capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char\* |Device ID |
|device_type |bytertc::RTCVideoDeviceType |Device type. See [RTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-85519#RTCVideoDeviceType) |
|device_warning |bytertc::MediaDeviceWarning |Device error type. See [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85519#MediaDeviceWarning) |


<span id="IRTCEngineEventHandler-onsysstats"></span>
### onSysStats

```cpp
virtual void onSysStats(const bytertc::SysStats& stats) {
    }
```


You will periodically(2s) receive the callbacks of the current CPU and memory information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |const bytertc::SysStats& |The structure containing the current CPU and memory information. See [SysStats](https://docs.byteplus.com/en/docs/12/docs-85519#SysStats). |


<span id="IRTCEngineEventHandler-onrecordingstateupdate"></span>
### onRecordingStateUpdate

```cpp
virtual void onRecordingStateUpdate(
        IVideoSource* video_source, RecordingState state, RecordingErrorCode error_code, RecordingInfo info) {
    }
```


Get a callback of the local recording status.

The callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startfilerecording) or [stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopfilerecording).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_source |IVideoSource\* |Reserved parameter |
|state |RecordingState |Recording state. See [RecordingState](https://docs.byteplus.com/en/docs/12/docs-85519#RecordingState) |
|error_code |RecordingErrorCode |Recording error code. See [RecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-85519#RecordingErrorCode) |
|info |RecordingInfo |For more information about the recorded file. See [RecordingInfo](https://docs.byteplus.com/en/docs/12/docs-85519#RecordingInfo) |


<span id="IRTCEngineEventHandler-onrecordingprogressupdate"></span>
### onRecordingProgressUpdate

```cpp
virtual void onRecordingProgressUpdate(
    IVideoSource* video_source,
    RecordingProgress process,
    RecordingInfo info
) {
    }
```


Local recording progress callback.

This callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startfilerecording). When the recording state is normal, the system will prompt the recording progress through this callback every second.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_source |IVideoSource\* |Reserved parameter |
|process |RecordingProgress |Recording progress. See [RecordingProgress](https://docs.byteplus.com/en/docs/12/docs-85519#RecordingProgress) |
|info |RecordingInfo |More information about the recorded file. See [RecordingInfo](https://docs.byteplus.com/en/docs/12/docs-85519#RecordingInfo) |


<span id="IRTCEngineEventHandler-onaudiorecordingstateupdate"></span>
### onAudioRecordingStateUpdate

```cpp
virtual void onAudioRecordingStateUpdate(
    AudioRecordingState state,
    AudioRecordingErrorCode error_code
) {
    }
```


When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopaudiorecording) to change the recording status, receive the callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |AudioRecordingState |See [AudioRecordingState](https://docs.byteplus.com/en/docs/12/docs-85519#AudioRecordingState). |
|error_code |AudioRecordingErrorCode |See [AudioRecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#AudioRecordingErrorCode). |


<span id="IRTCEngineEventHandler-onloginresult"></span>
### onLoginResult

```cpp
virtual void onLoginResult(const char* uid, int error_code, int elapsed) {
        (void)uid;
        (void)error_code;
        (void)elapsed;
    }
```


login result callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |Login user ID |
|error_code |int |Login result<br><br>&nbsp;<br><br>See [LoginErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#LoginErrorCode). |
|elapsed |int |The time taken from the call to the [login](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-login) interface to return the result is<br><br>&nbsp;<br><br>In ms. This callback is received after |


**Notes**

You will receive this callback after calling [login](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-login).

<span id="IRTCEngineEventHandler-onlogout"></span>
### onLogout

```cpp
virtual void onLogout(LogoutReason reason) {
    }
```


Callback of logout result

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|reason |LogoutReason |It describes the reason why users log out. See [LogoutReason](https://docs.byteplus.com/en/docs/12/docs-85519#LogoutReason) |


**Notes**

You will receive this callback when calling [logout](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-logout) or when the local user is kicked out because another user logs in with the same UserId.

<span id="IRTCEngineEventHandler-onserverparamssetresult"></span>
### onServerParamsSetResult

```cpp
virtual void onServerParamsSetResult(int error) {
        (void)error;
    }
```


Set the return result of the application server parameter

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|error |int |* 200, set successfully<br><br>* != 200: Failure. Refer to [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85518#UserMessageSendResult) for details. |


**Notes**

Receive this callback after calling [setServerParams](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setserverparams).

<span id="IRTCEngineEventHandler-ongetpeeronlinestatus"></span>
### onGetPeerOnlineStatus

```cpp
virtual void onGetPeerOnlineStatus(const char* peer_user_id, int status) {
        (void)peer_user_id;
        (void)status;
    }
```


The return result of querying the login status of the peer or local user

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|peer_user_id |const char\* |User ID |
|status |int |The user login status of the query<br><br>&nbsp;<br><br>See [UserOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85519#UserOnlineStatus). |


**Notes**

You must first call [getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getpeeronlinestatus) to receive this callback.

<span id="IRTCEngineEventHandler-onusermessagereceivedoutsideroom"></span>
### onUserMessageReceivedOutsideRoom

```cpp
virtual void onUserMessageReceivedOutsideRoom(const char* uid, const char* message) {
        (void)uid;
        (void)message;
    }
```


> This interface will be deprecated in version 3.64. Please use [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) instead.

> Triggered when a text message is received from a user outside the room who called [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |The ID of the message sender. |
|message |const char\* |The content of the received text message. |


<span id="IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom"></span>
### onUserBinaryMessageReceivedOutsideRoom

```cpp
virtual void onUserBinaryMessageReceivedOutsideRoom(const char* uid, int size, const uint8_t* message) {
        (void)uid;
        (void)size;
        (void)message;
    }
```


> This callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/25050#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) instead.

> Triggered when a binary message is received from a user outside the room who called [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-senduserbinarymessageoutsideroom).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |The ID of the message sender. |
|size |int |The length of the binary message. |
|message |const uint8_t\* |The content of the binary message. |


<span id="IRTCEngineEventHandler-onusermessagesendresultoutsideroom"></span>
### onUserMessageSendResultOutsideRoom

```cpp
virtual void onUserMessageSendResultOutsideRoom(int64_t msgid, int error) {
        (void)msgid;
        (void)error;
    }
```


Callback for the result of sending a message to a user outside the room.

Triggered after sending a message to a user outside the room via [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom) or [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-senduserbinarymessageoutsideroom).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |The ID of this message.<br><br>&nbsp;<br><br>All P2P and P2Server messages share a single ID sequence. |
|error |int |Message sending result. See [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85518#UserMessageSendResult). |


<span id="IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2"></span>
### onUserMessageReceivedOutsideRoom

```cpp
virtual void onUserMessageReceivedOutsideRoom(int64_t msgid, const char* uid, const char* message) {
        (void)msgid;
        (void)uid;
        (void)message;
    }
```


Triggered when you receive a text message from a user outside the room by calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |ID of the message received. |
|uid |const char\* |The ID of the message sender. |
|message |const char\* |Content of the received text message. |


<span id="IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2"></span>
### onUserBinaryMessageReceivedOutsideRoom

```cpp
virtual void onUserBinaryMessageReceivedOutsideRoom(int64_t msgid, const char* uid, const uint8_t* message, int size) {
        (void)msgid;
        (void)uid;
        (void)message;
        (void)size;
    }
```


This callback is triggered when a binary message is received from a user outside the room who calls [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-senduserbinarymessageoutsideroom).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |The ID of this message. |
|uid |const char\* |The user ID of the message sender. |
|message |const uint8_t\* |The content of the received binary message. |
|size |int |The length of the binary message in bytes. |


<span id="IRTCEngineEventHandler-onservermessagesendresult"></span>
### onServerMessageSendResult

```cpp
virtual void onServerMessageSendResult(int64_t msgid, int error, const bytertc::ServerACKMsg& msg) {
        (void)msgid;
        (void)error;
        (void)msg;
    }
```


Receives the callback after sending the message to the application server successfully.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|msgid |int64_t |The ID of this message<br><br>&nbsp;<br><br>All P2P and P2Server messages share a single ID sequence. |
|error |int |Message Sending Results. See [UserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85518#UserMessageSendResult). |
|msg |const bytertc::ServerACKMsg& |The message returned in ACK when the application server receives HTTP request. The message should not exceed 64 KB. |


**Notes**

This callback is asynchronous. You will receive this callback when you call [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendserverbinarymessage) to send a message to your application server.

<span id="IRTCEngineEventHandler-onseimessagereceived"></span>
### onSEIMessageReceived

```cpp
virtual void onSEIMessageReceived(const char* stream_id, const StreamInfo& stream_info, const uint8_t* message, int length){
        (void)stream_id;
        (void)stream_info;
        (void)message;
        (void)length;
    }
```


Receive this callback when you receive a video frame with a SEI message sent via [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendseimessage)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The ID of the video stream that received SEI message |
|stream_info |const StreamInfo& |Contains the user name, room name and media stream of the SEI sender. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|message |const uint8_t\* |The content of the SEI message received |
|length |int |Length of received SEI message |


<span id="IRTCEngineEventHandler-onseistreamupdate"></span>
### onSEIStreamUpdate

```cpp
virtual void onSEIStreamUpdate(const char* stream_id, const StreamInfo& stream_info, SEIStreamEventType type) {
        (void)stream_id;
        (void)stream_info;
        (void)type;
    }
```


Callback about publishing status of the black frame video stream .

In a voice call scenario, when the local user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendseimessage) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback.

You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The ID of the video stream that received SEI message |
|stream_info |const StreamInfo& |Contains the user name, room name and media stream of the SEI sender. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|type |SEIStreamEventType |State of the black frame video stream, see [SEIStreamEventType](https://docs.byteplus.com/en/docs/12/docs-85519#SEIStreamEventType). |


<span id="IRTCEngineEventHandler-onremoteaudiopropertiesreport"></span>
### onRemoteAudioPropertiesReport

```cpp
virtual void onRemoteAudioPropertiesReport(const RemoteAudioPropertiesInfo* audio_properties_infos, int audio_properties_info_number, int total_remote_volume) {
        (void)audio_properties_infos;
        (void)audio_properties_info_number;
        (void)total_remote_volume;
    }
```


After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about the subscribed remote audio streams.

The remote audio streams includes the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_properties_infos |const RemoteAudioPropertiesInfo\* |See [RemoteAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteAudioPropertiesInfo). |
|audio_properties_info_number |int |The length of `audio_properties_infos` |
|total_remote_volume |int |The volume of the mixing of all the subscribed audio streams. The range is [0,255].<br><br><br>&nbsp;<br><br>* [0,25] Is close to silent;<br><br>* [26,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


<span id="IRTCEngineEventHandler-onlocalaudiopropertiesreport"></span>
### onLocalAudioPropertiesReport

```cpp
virtual void onLocalAudioPropertiesReport(const LocalAudioPropertiesInfo* audio_properties_infos, int audio_properties_info_number) {
        (void)audio_properties_infos;
        (void)audio_properties_info_number;
    }
```


After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about local audio.

Local audio includes the microphone audio, the screen audio captured using RTC SDK internal mechanisms, and locally mixing audio.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_properties_infos |const LocalAudioPropertiesInfo\* |Information of the local audios. See [LocalAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-85519#LocalAudioPropertiesInfo). You can set the volume of the local audio via [setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-setaudiocapturedevicevolume). |
|audio_properties_info_number |int |The length of `audio_properties_infos` |


<span id="IRTCEngineEventHandler-onaudioplaybackdevicetestvolume"></span>
### onAudioPlaybackDeviceTestVolume

```cpp
virtual void onAudioPlaybackDeviceTestVolume(int volume) {
        (void)volume;
    }
```


Notification on the playing volume during the test for the local audio devices

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |Playing volume during the test for the local audio devices. The range is [0,255]. |


**Notes**

Start an audio\-device test by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-startaudioplaybackdevicetest) or [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-startaudiodevicerecordtest) will register this callback for regular notification on playing volume. You can set the time interval between each callback by passing a proper value when calling the API above.

<span id="IRTCEngineEventHandler-onaudiodevicevolumechanged"></span>
### onAudioDeviceVolumeChanged

```cpp
virtual void onAudioDeviceVolumeChanged(bytertc::RTCAudioDeviceType device_type, int volume, bool muted) {
        (void)device_type;
        (void)volume;
        (void)muted;
    }
```


Callback to notify you the volume of the audio device has been changed or when the device has been muted or unmuted. No need to activate the notification beforehand.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_type |bytertc::RTCAudioDeviceType |Includes microphones and speakers. Refer to [RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-85519#RTCAudioDeviceType) for more details. |
|volume |int |Volume ranging [0, 255]. When the volume turns to 0, muted turns to True. Note that on Windows, when the volume of a microphone turns to 0, muted remains unchanged. |
|muted |bool |Whether is muted. When a speaker is muted, muted turns True but volume remains unchanged. |


<span id="IRTCEngineEventHandler-onlocalaudiostatechanged"></span>
### onLocalAudioStateChanged

```cpp
virtual void onLocalAudioStateChanged(IAudioSource* audio_source, LocalAudioStreamState state, LocalAudioStreamError error) {
        (void)audio_source;
        (void)state;
        (void)error;
    }
```


When the state of the local audio changes, the callback notifies the current local audio state.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_source |IAudioSource\* |The audio source of the local audio stream. See: IAudioSource |
|state |LocalAudioStreamState |The state of the local audio device, see: [LocalAudioStreamState](https://docs.byteplus.com/en/docs/12/docs-85519#LocalAudioStreamState) |
|error |LocalAudioStreamError |Error code when the local audio state changes, see: [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-85519#LocalAudioStreamError) |


<span id="IRTCEngineEventHandler-onuserstartaudiocapture"></span>
### onUserStartAudioCapture

```cpp
virtual void onUserStartAudioCapture(const char* stream_id, const StreamInfo& stream_info) {
        (void)stream_id;
        (void)stream_info;
    }
```


Users in the room call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startaudiocapture) When audio capture is turned on, other users in the room will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The stream ID of the remote user who turns on audio capture |
|stream_info |const StreamInfo& |Information of the remote user who turn on audio capture, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |


<span id="IRTCEngineEventHandler-onuserstopaudiocapture"></span>
### onUserStopAudioCapture

```cpp
virtual void onUserStopAudioCapture(const char* stream_id, const StreamInfo& stream_info) {
        (void)stream_id;
        (void)stream_info;
    }
```


When a user in the room calls [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopaudiocapture) to turn off audio capture, other users in the room will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The stream ID of the remote user who turns off audio capture |
|stream_info |const StreamInfo& |Information of the remote user who turn off audio capture, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |


<span id="IRTCEngineEventHandler-onactivespeaker"></span>
### onActiveSpeaker

```cpp
virtual void onActiveSpeaker(const char* room_id, const char* uid) {
        (void)room_id;
        (void)uid;
    }
```


After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |Room ID. |
|uid |const char\* |The user ID of the active speaker. |


<span id="IRTCEngineEventHandler-onstreamsyncinforeceived"></span>
### onStreamSyncInfoReceived

```cpp
virtual void onStreamSyncInfoReceived(const char* stream_id, const StreamInfo& stream_info, SyncInfoStreamType stream_type,
                                         const uint8_t* data, int32_t length) {
        (void)stream_id;
        (void)stream_info;        
        (void)stream_type;
        (void)data;
        (void)length;
    }
```


Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendstreamsyncinfo) to send an audio stream synchronization message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote stream ID. |
|stream_info |const StreamInfo& |Remote stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|stream_type |SyncInfoStreamType |Media stream type. See [SyncInfoStreamType](https://docs.byteplus.com/en/docs/12/docs-85519#SyncInfoStreamType). |
|data |const uint8_t\* |Message content. |
|length |int32_t |Message length. |


<span id="IRTCEngineEventHandler-onnetworkdetectionresult"></span>
### onNetworkDetectionResult

```cpp
virtual void onNetworkDetectionResult(NetworkDetectionLinkType type, NetworkQuality quality, int rtt, double lost_rate,
                                      int bitrate, int jitter){
        (void)type;
        (void)quality;
        (void)rtt;
        (void)lost_rate;
        (void)bitrate;
        (void)jitter;
    }
```


Pre\-call network detection result.

After successfully calling [startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startnetworkdetection), you will receive this callback for the first time in 3s and every 2s thereafter.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |NetworkDetectionLinkType |Identifies the network type as uplink/downlink. |
|quality |NetworkQuality |Network quality, see [NetworkQuality](https://docs.byteplus.com/en/docs/12/docs-85519#NetworkQuality). |
|rtt |int |Network RTT in ms. |
|lost_rate |double |Packet loss rate. |
|bitrate |int |Network bandwidth in kbps. |
|jitter |int |Network jitter in ms |


<span id="IRTCEngineEventHandler-onnetworkdetectionstopped"></span>
### onNetworkDetectionStopped

```cpp
virtual void onNetworkDetectionStopped(NetworkDetectionStopReason reason){
        (void)reason;
    }
```


Pre\-call network probing ends

The following will stop detection and receive this primary callback:


1. This callback is received once when the [stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopnetworkdetection) interface is called to stop probing;

2. Stop detection when the first frame of remote/local audio is received;

3. Stop detecting when the detection exceeds 3 minutes;

4. When the probe link is disconnected for a certain period of time, the probe is stopped.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|reason |NetworkDetectionStopReason |See [NetworkDetectionStopReason](https://docs.byteplus.com/en/docs/12/docs-85519#NetworkDetectionStopReason) for reasons of stopping probing. |


<span id="IRTCEngineEventHandler-onuserstartvideocapture"></span>
### onUserStartVideoCapture

```cpp
virtual void onUserStartVideoCapture(const char* stream_id, const StreamInfo& stream_info) {
        (void)stream_id;
        (void)stream_info;
    }
```


The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startvideocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Video stream ID |
|stream_info |const StreamInfo& |Video stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |


<span id="IRTCEngineEventHandler-onuserstopvideocapture"></span>
### onUserStopVideoCapture

```cpp
virtual void onUserStopVideoCapture(const char* stream_id, const StreamInfo& stream_info) {
        (void)stream_id;
        (void)stream_info;
    }
```


The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopvideocapture).

If you don't start video capture before you publish video data, all visible user will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Video stream ID |
|stream_info |const StreamInfo& |Video stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |


<span id="IRTCEngineEventHandler-onlocalvideosizechanged"></span>
### onLocalVideoSizeChanged

```cpp
virtual void onLocalVideoSizeChanged(IVideoSource* video_source, const VideoFrameInfo& info) {
        (void)video_source;
        (void)info;
    }
```


Receive this callback when the local video size or rotation configuration changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_source |IVideoSource\* |Reserved parameter. |
|info |const VideoFrameInfo& |Video frame information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85519#VideoFrameInfo). |


<span id="IRTCEngineEventHandler-onremotevideosizechanged"></span>
### onRemoteVideoSizeChanged

```cpp
virtual void onRemoteVideoSizeChanged(const char* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info) {
        (void)stream_id;
        (void)stream_info;
        (void)info;
    }
```


Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation configuration changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote video stream ID. |
|stream_info |const StreamInfo& |Remote video stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|info |const VideoFrameInfo& |Video frame information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85519#VideoFrameInfo). |


<span id="IRTCEngineEventHandler-onfirstlocalvideoframecaptured"></span>
### onFirstLocalVideoFrameCaptured

```cpp
virtual void onFirstLocalVideoFrameCaptured(IVideoSource* video_source, const VideoFrameInfo& info) {
        (void)video_source;
        (void)info;
    }
```


RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_source |IVideoSource\* |Reserved parameter. |
|info |const VideoFrameInfo& |Video information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85519#VideoFrameInfo). |


**Notes**

For captured local video frames, you can call [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalvideocanvas) or [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalvideosink) to render locally.

<span id="IRTCEngineEventHandler-onfirstremoteaudioframe"></span>
### onFirstRemoteAudioFrame

```cpp
virtual void onFirstRemoteAudioFrame(const char* stream_id, const StreamInfo& stream_info) {
        (void)stream_id;
        (void)stream_info;
    }
```


The subscriber will receive this callback when the first frame of the receiving audio stream begins to decode. The following situations are included:


1. The publisher publishes audio, including the initial publication and restart after cancellation.The publisher can cancel the audio streaming proactively. Audio streaming can also be cancelled by the publisher to stop publishing, leave the room or go offline.

2. After the publisher stops audio capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.

3. After the publisher publishes audio, the subscriber cancels the subscription to audio and then re\-subscribes to it.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote audio stream ID. |
|stream_info |const StreamInfo& |Remote audio stream information, see [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |


**Notes**


* The callback is received when the user has just received each audio stream in the room.

* Camera streams, screen streams, internal audio streams, external audio streams, and audio streams subscribed automatically or manually, are all included.

    &nbsp;


<span id="onremoteaudiostatechanged"></span>
### onRemoteAudioStateChanged

```cpp
virtual void onRemoteAudioStateChanged(
            const char* stream_id, const StreamInfo& stream_info, RemoteAudioState state, RemoteAudioStateChangeReason reason) {
        (void)stream_id;
        (void)stream_info;
        (void)state;
        (void)reason;
    }
```


When the state of the audio stream from the remote user subscribes to changes, this callback will be received to understand the current state of the remote audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote audio stream ID. |
|stream_info |const StreamInfo& |Remote audio stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|state |RemoteAudioState |Remote audio stream state. See [RemoteAudioState](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteAudioState) |
|reason |RemoteAudioStateChangeReason |For remote audio stream state change. See [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteAudioStateChangeReason) |


<span id="IRTCEngineEventHandler-onlocalvideostatechanged"></span>
### onLocalVideoStateChanged

```cpp
virtual void onLocalVideoStateChanged(IVideoSource* video_source, LocalVideoStreamState state, LocalVideoStreamError error) {
        (void)video_source;
        (void)state;
        (void)error;
    }
```


Receive this event when the state of the local video stream changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_source |IVideoSource\* |Reserved parameter. |
|state |LocalVideoStreamState |Local video stream status. See [LocalVideoStreamState](https://docs.byteplus.com/en/docs/12/docs-85519#LocalVideoStreamState) |
|error |LocalVideoStreamError |Error code when local video status changes. See [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/docs-85518#LocalVideoStreamError) |


<span id="IRTCEngineEventHandler-onremotevideostatechanged"></span>
### onRemoteVideoStateChanged

```cpp
virtual void onRemoteVideoStateChanged(
            const char* stream_id, const StreamInfo& stream_info, RemoteVideoState state, RemoteVideoStateChangeReason reason) {
        (void)stream_id;
        (void)stream_info;
        (void)state;
        (void)reason;
    }
```


When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote video stream ID. |
|stream_info |const StreamInfo& |Remote video stream information, including the room ID, user ID, and stream type. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|state |RemoteVideoState |Remote video stream state. See [RemoteVideoState](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteVideoState). |
|reason |RemoteVideoStateChangeReason |For the remote video stream state change. See [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteVideoStateChangeReason). |


**Notes**

This callback is only applicable to the main stream and not applicable to the screen stream.

<span id="IRTCEngineEventHandler-onaudioframesendstatechanged"></span>
### onAudioFrameSendStateChanged

```cpp
virtual void onAudioFrameSendStateChanged(const char* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFrameSendState state) {
        (void)stream_id;
        (void)stream_info;
        (void)user;
        (void)state;
    }
```


Audio first frame sending status change callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the room where the audio is published |
|stream_info |const StreamInfo& |Audio stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|user |const RtcUser& |Local user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-85519#RtcUser) |
|state |FirstFrameSendState |First frame sending status. See [FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-85519#FirstFrameSendState) |


<span id="IRTCEngineEventHandler-onvideoframesendstatechanged"></span>
### onVideoFrameSendStateChanged

```cpp
virtual void onVideoFrameSendStateChanged(const char* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFrameSendState state) {
        (void)stream_id;
        (void)stream_info;
        (void)user;
        (void)state;
    }
```


Triggered when the local video stream first frame sending status changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Stream ID. |
|stream_info |const StreamInfo& |Video stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|user |const RtcUser& |Local user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-85519#RtcUser) |
|state |FirstFrameSendState |First frame sending status. See [FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-85519#FirstFrameSendState) |


<span id="IRTCEngineEventHandler-onfirstremotevideoframerendered"></span>
### onFirstRemoteVideoFrameRendered

```cpp
virtual void onFirstRemoteVideoFrameRendered(const char* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info) {
        (void)stream_id;
        (void)stream_info;
        (void)info;
    }
```


The subscriber will receive this callback when the first frame of the receiving video stream begins to render. The following situations are included:


1. The publisher publishes video for the first time.

2. In 1, the publisher cancels the video streaming after publishing and publishes it again.

3. In 1, the publisher stops video capture after publishing and restarts it. (Or when using an external source, the stream is stopped and restarted again.)

4. In 1, the subscriber cancels the video streaming and subscribes to it again. (The interface includes [subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribeallstreamsvideo), [pauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseallsubscribedstreamvideo)/[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeallsubscribedstreamvideo))


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote video stream ID. |
|stream_info |const StreamInfo& |Remote video stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|info |const VideoFrameInfo& |Video frame information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85519#VideoFrameInfo). |


<span id="IRTCEngineEventHandler-onfirstremotevideoframedecoded"></span>
### onFirstRemoteVideoFrameDecoded

```cpp
virtual void onFirstRemoteVideoFrameDecoded(const char* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info) {
        (void)stream_id;
        (void)stream_info;
        (void)info;
    }
```


The subscriber will receive this callback when the first frame of the receiving video stream begins to decode. The following situations are included:


1. The publisher publishes video, including the initial publication and restart after cancellation. The publisher can cancel the video streaming proactively. Video streaming can also be cancelled by the publisher to stop publishing, leave the room or go offline.

2. After the publisher stops video capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.

3. After the publisher publishes video, the subscriber cancels the subscription to video and then re\-subscribes to it.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote video stream ID. |
|stream_info |const StreamInfo& |Remote video stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|info |const VideoFrameInfo& |Video frame information. See VideoFrameInfo . |


**Notes**


* For main stream, after joining the room, the subscriber will receive this callback only when the publisher publishes video stream for the first time.

* For screen\-sharing stream, the subscriber will receive this callback every time the publisher publishes or republishes the screen video stream.

    &nbsp;


<span id="onaudioframeplaystatechanged"></span>
### onAudioFramePlayStateChanged

```cpp
virtual void onAudioFramePlayStateChanged(const char* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFramePlayState state) {
        (void)stream_id;
        (void)stream_info;
        (void)user;
        (void)state;
    }
```


Audio first frame playback state change callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the audio stream whose first frame playback state changes |
|stream_info |const StreamInfo& |Audio stream information whose first frame playback state changes. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|user |const RtcUser& |Remote user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-85519#RtcUser) |
|state |FirstFramePlayState |First frame playback status. See [FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-85519#FirstFramePlayState) |


<span id="IRTCEngineEventHandler-onvideoframeplaystatechanged"></span>
### onVideoFramePlayStateChanged

```cpp
virtual void onVideoFramePlayStateChanged(const char* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFramePlayState state) {
        (void)stream_id;
        (void)stream_info;
        (void)user;
        (void)state;
    }
```


Remote video stream first frame playback state change callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the video stream whose first frame playback state changes |
|stream_info |const StreamInfo& |Video stream information whose first frame playback state changes. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo) |
|user |const RtcUser& |Remote user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-85519#RtcUser) |
|state |FirstFramePlayState |First frame playback state. See [FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-85519#FirstFramePlayState) |


<span id="IRTCEngineEventHandler-onfirstlocalaudioframe"></span>
### onFirstLocalAudioFrame

```cpp
virtual void onFirstLocalAudioFrame(IAudioSource* audio_source) {
        (void)audio_source;
    }
```


Receive the callback when publishing local audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_source |IAudioSource\* |Audio source, see IAudioSource. |


**Notes**

If you publish audio stream without enabling local audio capture, SDK will push blank audio frames that you will also get this notification.

<span id="IRTCEngineEventHandler-oncloudproxyconnected"></span>
### onCloudProxyConnected

```cpp
virtual void onCloudProxyConnected(int interval) {
        (void)interval;
    }
```


Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interval |int |The interval in ms between starting cloud proxy and connects the cloud proxy server successfully. |


<span id="IRTCEngineEventHandler-onlocalproxystatechanged"></span>
### onLocalProxyStateChanged

```cpp
virtual void onLocalProxyStateChanged(LocalProxyType local_proxy_type, LocalProxyState local_proxy_state, LocalProxyError local_proxy_error) {
        (void)local_proxy_type;
        (void)local_proxy_state;
        (void)local_proxy_error;
    }
```


Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|local_proxy_type |LocalProxyType |The types of local proxies. Refer to [LocalProxyType](https://docs.byteplus.com/en/docs/12/docs-85519#LocalProxyType) for details. |
|local_proxy_state |LocalProxyState |The states of local proxy connection. Refer to [LocalProxyState](https://docs.byteplus.com/en/docs/12/docs-85519#LocalProxyState) for details. |
|local_proxy_error |LocalProxyError |The errors of local proxy connection. Refer to [LocalProxyError](https://docs.byteplus.com/en/docs/12/docs-85519#LocalProxyError) for details. |


<span id="IRTCEngineEventHandler-onaudiomixingplayingprogress"></span>
### onAudioMixingPlayingProgress

```cpp
virtual void onAudioMixingPlayingProgress(
    int mix_id,
    int64_t progress
) {
    }
```


> Deprecated since 3.54, use [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/25050#IMediaPlayerEventHandler-onmediaplayerplayingprogress) instead.


Callback for playback progress of mixed audio files

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mix_id |int |ID of the mixing task |
|progress |int64_t |The current playback progress (ms) of the mixed audio file |


**Notes**

After calling setAudioMixingProgressInterval to set the time interval to a value greater than 0, or calling startAudioMixing to set the time interval in AudioMixingConfig to a value greater than 0, the SDK will trigger the callback according to the set time interval.

<span id="IWTNStreamEventHandler"></span>
# IWTNStreamEventHandler

```cpp
class bytertc::IWTNStreamEventHandler
```


WTN event handler.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual |[~IWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-~iwtnstreameventhandler) |
|virtual void |[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnremotevideostats) |
|virtual void |[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnremoteaudiostats) |
|virtual void |[onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnvideosubscribestatechanged) |
|virtual void |[onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged) |
|virtual void |[onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnfirstremoteaudioframe) |
|virtual void |[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded) |
|virtual void |[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnseimessagereceived) |
|virtual void |[onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtndatamessagereceived) |


<span id="instructions"></span>
## Instructions

<span id="IWTNStreamEventHandler-~iwtnstreameventhandler"></span>
### ~IWTNStreamEventHandler

```cpp
virtual ~IWTNStreamEventHandler() {
    }
```


<span id="IWTNStreamEventHandler-onwtnremotevideostats"></span>
### onWTNRemoteVideoStats

```cpp
virtual void onWTNRemoteVideoStats(const char* stream_id, RemoteVideoStats stats) {
        (void)stream_id;
        (void)stats;
    }
```


> Available since 3.60.


Remote WTN video stream ID and statistics.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |
|stats |RemoteVideoStats |Remote WTN video stream statistics. See [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteVideoStats). |


<span id="IWTNStreamEventHandler-onwtnremoteaudiostats"></span>
### onWTNRemoteAudioStats

```cpp
virtual void onWTNRemoteAudioStats(const char* stream_id, RemoteAudioStats stats) {
        (void)stream_id;
        (void)stats;
    }
```


> Available since 3.60.


Remote WTN audio stream ID and statistics.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |
|stats |RemoteAudioStats |Remote WTN audio stream statistics. See [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteAudioStats) |


<span id="IWTNStreamEventHandler-onwtnvideosubscribestatechanged"></span>
### onWTNVideoSubscribeStateChanged

```cpp
virtual void onWTNVideoSubscribeStateChanged(const char* stream_id, WTNSubscribeState state_code, WTNSubscribeStateChangeReason reason) {
        (void)stream_id;
        (void)state_code;
        (void)reason;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces `onPlayPublicStreamResult` for reporting the subscription status changes of WTN video streams. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback for the change of WTN video stream's subscription status

You will be informed of the result of subscribing to the WTN video stream by this callback after calling [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN video stream |
|state_code |WTNSubscribeState |Video stream state code. See [WTNSubscribeState](https://docs.byteplus.com/en/docs/12/docs-85519#WTNSubscribeState) for specific indications. |
|reason |WTNSubscribeStateChangeReason |The reason why subscription state changes. See [WTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#WTNSubscribeStateChangeReason). |


<span id="IWTNStreamEventHandler-onwtnaudiosubscribestatechanged"></span>
### onWTNAudioSubscribeStateChanged

```cpp
virtual void onWTNAudioSubscribeStateChanged(const char* stream_id, WTNSubscribeState state_code, WTNSubscribeStateChangeReason reason) {
        (void)stream_id;
        (void)state_code;
        (void)reason;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces `onPlayPublicStreamResult` for reporting the subscription status changes of WTN audio streams. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback for the change of WTN audio stream's subscription status

You will be informed of the result of subscribing to the WTN audio stream by this callback after calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN audio stream |
|state_code |WTNSubscribeState |Audio stream state code. See [WTNSubscribeState](https://docs.byteplus.com/en/docs/12/docs-85519#WTNSubscribeState) for specific indications. |
|reason |WTNSubscribeStateChangeReason |The reason why subscription state changes. See [WTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#WTNSubscribeStateChangeReason). |


<span id="IWTNStreamEventHandler-onwtnfirstremoteaudioframe"></span>
### onWTNFirstRemoteAudioFrame

```cpp
virtual void onWTNFirstRemoteAudioFrame(const char* stream_id) {
        (void)stream_id;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces `onFirstPublicStreamAudioFrame`. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback of successfully decoding of the first audio frame of the WTN stream.

Refer to [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream) for details about subscribing to a WTN audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |


<span id="IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded"></span>
### onWTNFirstRemoteVideoFrameDecoded

```cpp
virtual void onWTNFirstRemoteVideoFrameDecoded(const char* stream_id, const VideoFrameInfo& info) {
        (void)stream_id;
        (void)info;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces `onFirstPublicStreamVideoFrameDecoded`. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback of successfully decoding of the first video frame of the WTN stream

Refer to [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream) for details about subscribing to a WTN video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |
|info |const VideoFrameInfo& |Information of the video stream. Refer to [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85519#VideoFrameInfo) for more details. |


<span id="IWTNStreamEventHandler-onwtnseimessagereceived"></span>
### onWTNSEIMessageReceived

```cpp
virtual void onWTNSEIMessageReceived(const char* stream_id, int channel_id, const uint8_t* message, int length) {
        (void)stream_id;
        (void)channel_id;
        (void)message;
        (void)length;
    }
```


> Available since 3.60. Since version 3.60, this callback replaces `onPublicStreamSEIMessageReceived` for the following function. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback on receiving the SEI message carried by the WTN stream.

After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream), you will receive this callback if the WTN stream has an SEI message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The ID of the WTN stream. |
|channel_id |int |SEI message channel ID. The value range is `[0 - 255]`. With this parameter, you can set different ChannelIDs for different recipients. In this way, different recipients can choose the SEI information based on the ChannelID received in the callback. |
|message |const uint8_t\* |The received SEI(supplemental enhancement information) message.<br><br>&nbsp;<br><br>The SEI message inserted by calling `sendSEIMessage` in the SDK.<br><br>&nbsp;<br><br>You receive SEI from all the video streams if the SEI messages do not have conflicts. However, if the SEI messages from different video streams have conflicts, you will receive only one of them. |
|length |int |The length of the SEI message. |


**Notes**

You also need to listen to [onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtndatamessagereceived) to receive data messages inserted via Open API in the server.

<span id="IWTNStreamEventHandler-onwtndatamessagereceived"></span>
### onWTNDataMessageReceived

```cpp
virtual void onWTNDataMessageReceived(const char* stream_id,
        const uint8_t* message,
        int message_length,
        DataMessageSourceType source_type) {
        (void)stream_id;
        (void)message;
        (void)message_length;
        (void)source_type;
    }
```


> Available since 3.60.


The data information contained in the callback of WTN stream..

After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream), you can listen to this callback and retrieve SEI messages inserted by Open API calls or audio volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |
|message |const uint8_t\* |The received data message's content is as follows:<br><br><br>&nbsp;<br><br>* Data inserted by calling the OpenAPI.<br><br>* Media volume in JSON, before you can receive which you need to enable it via calling the OpenAPI. Refer to the definition below to parse the JSON string.<br><br>   {<br><br>&nbsp;<br><br>   "Type" : "VolumeIndication", //Specific business type.<br><br>&nbsp;<br><br>   "VolumeInfos" : [ // Business type corresponding information<br><br>&nbsp;<br><br>   {<br><br>&nbsp;<br><br>   "RoomId":"1000001", // Room ID<br><br>&nbsp;<br><br>   "UserId":"1000001", // User ID<br><br>&nbsp;<br><br>   "StreamType":0, // 0:camera stream；1:screen stream<br><br>&nbsp;<br><br>   "LinearVolume":1 // LinearVolume<br><br>&nbsp;<br><br>   } |
|message_length |int |Length of the message |
|source_type |DataMessageSourceType |Message source. |


**Notes**

You also need to listen to [onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/25050#IWTNStreamEventHandler-onwtnseimessagereceived) to receive SEI inserted via API by the client SDK.

<span id="IAudioFrameProcessor"></span>
# IAudioFrameProcessor

```cpp
class bytertc::IAudioFrameProcessor
```


The custom audio processor.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int |[onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameProcessor-onprocessrecordaudioframe) |
|virtual int |[onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameProcessor-onprocessplaybackaudioframe) |
|virtual int |[onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameProcessor-onprocessremoteuseraudioframe) |
|virtual int |[onProcessScreenAudioFrame](https://docs.byteplus.com/en/docs/12/25050#IAudioFrameProcessor-onprocessscreenaudioframe) |


<span id="instructions"></span>
## Instructions

<span id="IAudioFrameProcessor-onprocessrecordaudioframe"></span>
### onProcessRecordAudioFrame

```cpp
virtual int onProcessRecordAudioFrame(IAudioFrame& audio_frame) = 0;
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame& |The address of the audio frame. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


**Notes**


* After custom processing, SDK will encode the processed audio frames and transmit to the remote user.

* After calling [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudioprocessor) with locally captured audio frame specified, you will receive this callback every 10 ms.

    &nbsp;


<span id="onprocessplaybackaudioframe"></span>
### onProcessPlayBackAudioFrame

```cpp
virtual int onProcessPlayBackAudioFrame(IAudioFrame& audio_frame) = 0;
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame& |The address of the audio frame. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


**Notes**

After calling [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudioprocessor) with mixed remote audio, you will receive this callback every 10 ms.

<span id="IAudioFrameProcessor-onprocessremoteuseraudioframe"></span>
### onProcessRemoteUserAudioFrame

```cpp
virtual int onProcessRemoteUserAudioFrame(
    const char* stream_id,
    const StreamInfo& stream_info,
    IAudioFrame& audio_frame
) = 0;
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote stream ID. |
|stream_info |const StreamInfo& |Remote stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85519#StreamInfo). |
|audio_frame |IAudioFrame& |The address of the audio frame. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) |


**Notes**

After calling [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudioprocessor) with audio streams of the remote users. You will receive this callback every 10 ms.

<span id="IAudioFrameProcessor-onprocessscreenaudioframe"></span>
### onProcessScreenAudioFrame

```cpp
virtual int onProcessScreenAudioFrame(IAudioFrame& audio_frame) = 0;
```


Returns the address of the shared\-screen audio frames for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame& |The address of audio frames. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame). |


**Notes**

After calling [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudioprocessor) to set the audio input to the shared\-screen audio. You will receive this callback every 10 ms.

<span id="ILocalEncodedVideoFrameObserver"></span>
# ILocalEncodedVideoFrameObserver

```cpp
class bytertc::ILocalEncodedVideoFrameObserver
```


Local video frame observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/25050#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe"></span>
### onLocalEncodedVideoFrame

```cpp
virtual void onLocalEncodedVideoFrame(
    IVideoSource*video_source,
    const IEncodedVideoFrame& video_stream
) = 0;
```


After calling [registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerlocalencodedvideoframeobserver), SDK will trigger this callback when it receives local video frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_source |IVideoSource\* |Reserved parameter. |
|video_stream |const IEncodedVideoFrame& |Information about the local video frame. See [IEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IEncodedVideoFrame). |
