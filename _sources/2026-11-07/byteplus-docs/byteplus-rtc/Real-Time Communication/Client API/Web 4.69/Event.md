---
title: "Event"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104479"
---

<span id="wtnstreamevents"></span>
## WTNstreamEvents  

Type: `interface`


* **API**



|Method |Description |
|---|---|
|[onWTNPushStateChanged](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnpushstatechanged) |Callback of the result of publishing the WTN stream.<br><br>After calling [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn), you will be informed of the result through this callback. |
|[onWTNPlayStateChanged](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnplaystatechanged) |Callback of the result of subscribing to the WTN stream.<br><br>After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback. |
|[onWTNRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnremoteaudiostatechanged) |Callback of the subscription state of the audio of the WTN stream.<br><br>After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback. |
|[onWTNRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnremotevideostatechanged) |Callback of the subscription state of the video of the WTN stream.<br><br>After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback. |
|[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnremotevideostats) |Callback carrying the video statistics of the WTN stream.<br><br>You can receive this callback every 2 seconds after subscribing to the video of a WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn). |
|[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnremoteaudiostats) |Callback carrying the audio statistics of the WTN stream.<br><br>You can receive this callback every 2 seconds after subscribing to the audio of a WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn). |
|[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnfirstremotevideoframedecoded) |Callback of the successful decoding of the first video frame of the WTN stream.<br><br>Refer to [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) for details about subscribing to a WTN stream. |
|[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnseimessagereceived) |Callback of the SEI carried by the public video stream.<br><br>You will receive SEI by this callback if the WTN stream you subscribed to by calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) is carrying SEI. |
|[onWTNLocalStatsException](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnlocalstatsexception) |Exception event callback of local WTN media stream. |
|[onWTNRemoteStatsException](https://docs.byteplus.com/en/docs/12/14191#wtnstreamevents-onwtnremotestatsexception) |Exception event callback of remote WTN media stream. |


<span id="onwtnpushstatechanged"></span>
### onWTNPushStateChanged  

Callback of the result of publishing the WTN stream.

After calling [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn), you will be informed of the result through this callback.


* **Type**

   ```ts
   (event: onWTNPushStateChangedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNPushStateChangedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnpushstatechangedevent)


<span id="onwtnplaystatechanged"></span>
### onWTNPlayStateChanged  

Callback of the result of subscribing to the WTN stream.

After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback.


* **Type**

   ```ts
   (event: onWTNPlayStateChangedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNPlayStateChangedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnplaystatechangedevent)


<span id="onwtnremoteaudiostatechanged"></span>
### onWTNRemoteAudioStateChanged  

Callback of the subscription state of the audio of the WTN stream.

After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback.


* **Type**

   ```ts
   (event: onWTNRemoteAudioStateChangedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNRemoteAudioStateChangedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnremoteaudiostatechangedevent)


<span id="onwtnremotevideostatechanged"></span>
### onWTNRemoteVideoStateChanged  

Callback of the subscription state of the video of the WTN stream.

After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback.


* **Type**

   ```ts
   (event: onWTNRemoteVideoStateChangedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNRemoteVideoStateChangedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnremotevideostatechangedevent)


<span id="onwtnremotevideostats"></span>
### onWTNRemoteVideoStats  

Callback carrying the video statistics of the WTN stream.

You can receive this callback every 2 seconds after subscribing to the video of a WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn).


* **Type**

   ```ts
   (event: onWTNRemoteVideoStatsEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNRemoteVideoStatsEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnremotevideostatsevent)


<span id="onwtnremoteaudiostats"></span>
### onWTNRemoteAudioStats  

Callback carrying the audio statistics of the WTN stream.

You can receive this callback every 2 seconds after subscribing to the audio of a WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn).


* **Type**

   ```ts
   (event: onWTNRemoteAudioStatsEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNRemoteAudioStatsEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnremoteaudiostatsevent)


<span id="onwtnfirstremotevideoframedecoded"></span>
### onWTNFirstRemoteVideoFrameDecoded  

Callback of the successful decoding of the first video frame of the WTN stream.

Refer to [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) for details about subscribing to a WTN stream.


* **Type**

   ```ts
   (event: onWTNFirstRemoteVideoFrameDecodedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNFirstRemoteVideoFrameDecodedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnfirstremotevideoframedecodedevent)


<span id="onwtnseimessagereceived"></span>
### onWTNSEIMessageReceived  

Callback of the SEI carried by the public video stream.

You will receive SEI by this callback if the WTN stream you subscribed to by calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) is carrying SEI.


* **Type**

   ```ts
   (event: onWTNSEIMessageReceivedEvent) => void
   ```
   

* **Notes**

   When multiple streams in the WTN stream contain SEI:

   * You will receive SEI from all the video frames if the SEI do not have conflicts.

   * However, if SEI from video frames have conflicts, you will receive only one of them.

* **Parameters**

   * **event**

      Type: [onWTNSEIMessageReceivedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnseimessagereceivedevent)


<span id="onwtnlocalstatsexception"></span>
### onWTNLocalStatsException  

Exception event callback of local WTN media stream.


* **Type**

   ```ts
   (event: onWTNLocalStatsExceptionEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNLocalStatsExceptionEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnlocalstatsexceptionevent)


<span id="onwtnremotestatsexception"></span>
### onWTNRemoteStatsException  

Exception event callback of remote WTN media stream.


* **Type**

   ```ts
   (event: onWTNRemoteStatsExceptionEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onWTNRemoteStatsExceptionEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onwtnremotestatsexceptionevent)


<span id="engineevents"></span>
## EngineEvents  

Type: `interface`


* **API**



|Method |Description |
|---|---|
|[onPlayerEvent](https://docs.byteplus.com/en/docs/12/14191#engineevents-onplayerevent) |Player event |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserjoined) |Callback for a remote visible user joining the room, or an invisible user in the room switching to visible. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserleave) |Callback for a remote visible user leaving the room, or a visible user in the room switching to invisible. |
|[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/14191#engineevents-onconnectionstatechanged) |Connection state changed |
|[onUserPublishStream](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserpublishstream) |Callback on new media streams captured by camera/microphone in the room. |
|[onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserunpublishstream) |Callback on removal of remote media stream captured by camera/microphone. |
|[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserpublishscreen) |Callback on new screen sharing media streams from remote users in the room. |
|[onUserUnpublishScreen](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserunpublishscreen) |Callback on removal of screen sharing media streams from remote users in the room. |
|[onRemoteVideoFirstFrame](https://docs.byteplus.com/en/docs/12/14191#engineevents-onremotevideofirstframe) |The first video frame rendered. |
|[onRemoteAudioFirstFrame](https://docs.byteplus.com/en/docs/12/14191#engineevents-onremoteaudiofirstframe) |First remote audio frame received |
|[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/14191#engineevents-onvideodevicestatechanged) |Triggered when the video device connection state changes. For example, due to device disconnection or reconnection.<br><br>You need to get camera permission ([enableDevices](https://docs.byteplus.com/en/docs/12/docs-104478#enabledevices)) before you can receive this callback. |
|[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/14191#engineevents-onaudiodevicestatechanged) |Triggered when the audio device connection state changes. For example, due to device disconnection or reconnection.<br><br>You need to get microphone or speaker permission ([enableDevices](https://docs.byteplus.com/en/docs/12/docs-104478#enabledevices)) before you can receive this callback. |
|[onTrackEnded](https://docs.byteplus.com/en/docs/12/14191#engineevents-ontrackended) |Media track ended event. Please restart capture in the callback thread. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/14191#engineevents-onroommessagereceived) |Event of receiving a broadcast text message in the room |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14191#engineevents-onroombinarymessagereceived) |Event of receiving a broadcast binary message in the room |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/14191#engineevents-onusermessagereceived) |Receiving a point\-to\-point text message from one of the users in the room by calling [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendusermessage) |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserbinarymessagereceived) |Receiving a point\-to\-point binary message from one of the users in the room |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/14191#engineevents-onremotestreamstats) |Statistics of subscribed media streams and network states in a cycle of 2s |
|[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/14191#engineevents-onlocalstreamstats) |Statistics of local media streams and network states in a cycle of 2s |
|[onPublicStreamStats](https://docs.byteplus.com/en/docs/12/14191#engineevents-onpublicstreamstats) |This 2 s periodical callback notifies information of the WTN stream after calling [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream). |
|[onLocalStatsException](https://docs.byteplus.com/en/docs/12/14191#engineevents-onlocalstatsexception) |SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually causes a problem with the call quality. If the problem is resolved, you will also receive this callback. |
|[onRemoteStatsException](https://docs.byteplus.com/en/docs/12/14191#engineevents-onremotestatsexception) |SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually causes a problem with the call quality. If the problem is resolved, you will also receive this callback. |
|[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14191#engineevents-onlocalaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will periodically receive this callback for the instant information about local audio.<br><br>Local audio includes the microphone audio and the screen audio captured using RTC SDK internal mechanisms. |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14191#engineevents-onremoteaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will receive the cycling callbacks, each providing instant information about the subscribed remote audio streams.<br><br>The remote audio streams include the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism. |
|[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/14191#engineevents-onactivespeaker) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will periodically receive this callback for the information of the user with the highest voice volume. |
|[onAudioPlaybackDeviceChanged](https://docs.byteplus.com/en/docs/12/14191#engineevents-onaudioplaybackdevicechanged) |The current playback device has been changed successfully by calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice). |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserstartaudiocapture) |The remote clients in the room will be informed of the state change via this event after the publisher starts audio capture by calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture). |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserstopaudiocapture) |The remote clients in the room will be informed of the state change via this event after the publisher stops audio capture by calling [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopaudiocapture). |
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserstartvideocapture) |The remote clients in the room will be informed of the state change via this event after the publisher starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture). |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserstopvideocapture) |The remote clients in the room will be informed of the state change via this event after the publisher stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopvideocapture). |
|[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14191#engineevents-onseimessagereceived) |Event of receiving SEI data from video frames |
|[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/14191#engineevents-onseistreamupdate) |Stream update event of stream that contains SEI information.<br><br>In a voice call scenario, when a remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage) to send SEI data via the black frame video stream, the stream's sending status will be notified to the local user through this event callback.<br><br>If the video frame carrying SEI data is a black frame, you do not need to render the video frame. |
|[onAutoSubscribeResult](https://docs.byteplus.com/en/docs/12/14191#engineevents-onautosubscriberesult) |Result of the Auto\-Subscription |
|[onAutoPublishResult](https://docs.byteplus.com/en/docs/12/14191#engineevents-onautopublishresult) |Result of Auto\-publishing. You will receive this event if you enable Auto\-publish when calling `joinRoom` |
|[onAutoplayFailed](https://docs.byteplus.com/en/docs/12/14191#engineevents-onautoplayfailed) |Auto\-play fails. |
|[onError](https://docs.byteplus.com/en/docs/12/14191#engineevents-onerror) |An error occurred in the SDK. |
|[onAudioMixingStateChanged](https://docs.byteplus.com/en/docs/12/14191#engineevents-onaudiomixingstatechanged) |Event of the state change of audio mixing |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14191#engineevents-onusermessagereceivedoutsideroom) |Event of receiving a text message |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14191#engineevents-onuserbinarymessagereceivedoutsideroom) |Event of receiving a binary message |
|[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/14191#engineevents-ontokenwillexpire) |You will receive this callback 30 seconds before the Token expires.<br><br>Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to submit a new Token. The user will be removed from the room when the Token expires. |
|[onTokenPublishPrivilegeWillExpire](https://docs.byteplus.com/en/docs/12/14191#engineevents-ontokenpublishprivilegewillexpire) |This callback will be triggered 30 seconds before the token publishing permission expires.<br><br>Upon receiving this callback, call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the token. |
|[onTokenPublishPrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/14191#engineevents-ontokenpublishprivilegedidexpired) |This callback is triggered when the token publishing permission expires. Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the Token. |
|[onTokenSubscribePrivilegeWillExpire](https://docs.byteplus.com/en/docs/12/14191#engineevents-ontokensubscribeprivilegewillexpire) |This callback will be triggered 30 seconds before the token subscription permission expires.<br><br>Upon receiving this callback, call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the token. |
|[onTokenSubscribePrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/14191#engineevents-ontokensubscribeprivilegedidexpired) |This callback is triggered when the token subscription permission expires. Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the Token. |
|[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/14191#engineevents-oncloudproxyconnected) |Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-104478#startcloudproxy) to start cloud proxy, and the SDK connects to the proxy server successfully. |
|[onPushPublicStreamResult](https://docs.byteplus.com/en/docs/12/14191#engineevents-onpushpublicstreamresult) |Callback of the result of publishing the WTN stream.<br><br>After calling [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startpushpublicstream), you will be informed of the result through this callback. |
|[onPublicStreamSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14191#engineevents-onpublicstreamseimessagereceived) |Callback of the SEI carried by the public video stream.<br><br>You will receive SEI by this callback if the WTN stream you subscribed to by calling [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) is carrying SEI. |
|[onFirstPublicStreamVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/14191#engineevents-onfirstpublicstreamvideoframedecoded) |Callback of the successful decoding of the first video frame of the WTN stream.<br><br>Refer to [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) for details about subscribing to a WTN stream. |
|[onFirstPublicStreamAudioFrameDecoded](https://docs.byteplus.com/en/docs/12/14191#engineevents-onfirstpublicstreamaudioframedecoded) |Callback of the successful decoding of the first audio frame of the WTN stream.<br><br>Refer to [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) for details about subscribing to a WTN stream. |
|[onFirstPublicStreamVideoFrameRendered](https://docs.byteplus.com/en/docs/12/14191#engineevents-onfirstpublicstreamvideoframerendered) |Callback of the successful rendering of the first video frame of the WTN stream.<br><br>Refer to [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) for details about subscribing to a WTN stream. |
|[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/14191#engineevents-onaudioplaybackdevicetestvolume) |Notification on the playing volume during the test for the local audio devices |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/14191#engineevents-onnetworkquality) |The callback reports the upstream and downstream network quality of the local user every 2s after the user enters the room. |
|[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/14191#engineevents-onsimulcastsubscribefallback) |Receives this callback when fallback happens or the stream recovers from fallback. |
|[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/14191#engineevents-onremotevideosizechanged) |When the resolution of remote video changes, users who subscribed to the stream will receive this callback. |
|[onStreamMixingEvent](https://docs.byteplus.com/en/docs/12/14191#engineevents-onstreammixingevent) |Pushing a mixed stream to CDN events |
|[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/14191#engineevents-onvideostreambanned) |The callback is triggered when the openAPI BanUserStream/UnbanUserStream is called to ban/unban the video stream of the specified user from publishing. |
|[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/14191#engineevents-onaudiostreambanned) |The callback is triggered when the openAPI BanUserStream/UnbanUserStream is called to ban/unban the audio stream of the specified user from publishing. |
|[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/14191#engineevents-onlocalvideosizechanged) |The callback of the actual video capturing configuration. |
|[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/14191#engineevents-onserverparamssetresult) |Event of whether the setting for the message server succeeds |
|[onForwardStreamError](https://docs.byteplus.com/en/docs/12/14191#engineevents-onforwardstreamerror) |Event of failing to forward stream across rooms. |
|[onPlayerVisibility](https://docs.byteplus.com/en/docs/12/14191#engineevents-onplayervisibility) |Event of player visibility change, triggered every 30 seconds to notify users of changes in the visibility status of the player. |


<span id="onplayerevent"></span>
### onPlayerEvent  

Player event


* **Type**

   ```ts
   (event: PlayerEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [PlayerEvent](https://docs.byteplus.com/en/docs/12/docs-104481#playerevent)


<span id="onuserjoined"></span>
### onUserJoined  

Callback for a remote visible user joining the room, or an invisible user in the room switching to visible.


* **Type**

   ```ts
   (event: onUserJoinedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onUserJoinedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onuserjoinedevent)


<span id="onuserleave"></span>
### onUserLeave  

Callback for a remote visible user leaving the room, or a visible user in the room switching to invisible.


* **Type**

   ```ts
   (event: onUserLeaveEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onUserLeaveEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onuserleaveevent)


<span id="onconnectionstatechanged"></span>
### onConnectionStateChanged  

Connection state changed


* **Type**

   ```ts
   (event: ConnectionStateChangeEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [ConnectionStateChangeEvent](https://docs.byteplus.com/en/docs/12/docs-104481#connectionstatechangeevent)


<span id="onuserpublishstream"></span>
### onUserPublishStream  

Callback on new media streams captured by camera/microphone in the room.


* **Type**

   ```ts
   (event: { userId: string; mediaType: MediaType;}) => void
   ```
   

* **Notes**

   You will receive this callback after a remote user successfully publishes media streams captured by camera/microphone in the room with [publishStream](https://docs.byteplus.com/en/docs/12/docs-104478#publishstream). Then you can choose whether to call [subscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#subscribestream) to subscribe to the streams or not.

* **Parameters**

   * **event**

      Type: `{ userId: string; mediaType: `[MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)`; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |ID of the remote user who published the stream |
         |mediaType |`MediaType` |Remote stream type |
         


<span id="onuserunpublishstream"></span>
### onUserUnpublishStream  

Callback on removal of remote media stream captured by camera/microphone.


* **Type**

   ```ts
   (event: { userId: string; mediaType: MediaType; reason: StreamRemoveReason;}) => void
   ```
   

* **Notes**

   You will receive this callback after a remote user successfully unpublishes media streams captured by camera/microphone in the room with [unpublishStream](https://docs.byteplus.com/en/docs/12/docs-104478#unpublishstream). Then you can choose whether to call [unsubscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#unsubscribestream) to unsubscribe from the streams or not.

* **Parameters**

   * **event**

      Type: `{ userId: string; mediaType: `[MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)`; reason: `[StreamRemoveReason](https://docs.byteplus.com/en/docs/12/docs-104481#streamremovereason)`; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |ID of the remote user who removed the stream |
         |mediaType |`MediaType` |Remote stream type |
         |reason |`StreamRemoveReason` |The reason for the removal |
         


<span id="onuserpublishscreen"></span>
### onUserPublishScreen  

Callback on new screen sharing media streams from remote users in the room.


* **Type**

   ```ts
   (event: { userId: string; mediaType: MediaType;}) => void
   ```
   

* **Notes**

   You will receive this callback after a remote user successfully published screen sharing streams in the room with [publishScreen](https://docs.byteplus.com/en/docs/12/docs-104478#publishscreen). Then you can choose whether to call [subscribeScreen](https://docs.byteplus.com/en/docs/12/docs-104478#subscribescreen) to subscribe to the streams or not.

* **Parameters**

   * **event**

      Type: `{ userId: string; mediaType: `[MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)`; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |ID of the remote user who published the stream |
         |mediaType |`MediaType` |Remote stream type |
         


<span id="onuserunpublishscreen"></span>
### onUserUnpublishScreen  

Callback on removal of screen sharing media streams from remote users in the room.


* **Type**

   ```ts
   (event: { userId: string; mediaType: MediaType; reason: StreamRemoveReason;}) => void
   ```
   

* **Notes**

   You will receive this callback after a remote user successfully unpublishes media streams captured by camera/microphone in the room with [unpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104478#unpublishscreen). Then you can choose whether to call [unsubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-104478#unsubscribescreen) to unsubscribe from the streams or not.

* **Parameters**

   * **event**

      Type: `{ userId: string; mediaType: `[MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)`; reason: `[StreamRemoveReason](https://docs.byteplus.com/en/docs/12/docs-104481#streamremovereason)`; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |ID of the remote user who removed the stream |
         |mediaType |`MediaType` |Remote stream type |
         |reason |`StreamRemoveReason` |The reason for the removal |
         


<span id="onremotevideofirstframe"></span>
### onRemoteVideoFirstFrame  

The first video frame rendered.


* **Type**

   ```ts
   (event: onVideoFirstFrameRenderedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onVideoFirstFrameRenderedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onvideofirstframerenderedevent)


<span id="onremoteaudiofirstframe"></span>
### onRemoteAudioFirstFrame  

First remote audio frame received


* **Type**

   ```ts
   (event: onAudioFirstFrameDecodedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onAudioFirstFrameDecodedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onaudiofirstframedecodedevent)


<span id="onvideodevicestatechanged"></span>
### onVideoDeviceStateChanged  

Triggered when the video device connection state changes. For example, due to device disconnection or reconnection.

> You need to get camera permission ([enableDevices](https://docs.byteplus.com/en/docs/12/docs-104478#enabledevices)) before you can receive this callback.


* **Type**

   ```ts
   (event: DeviceInfo) => void
   ```
   

* **Parameters**

   * **event**

      Type: [DeviceInfo](https://docs.byteplus.com/en/docs/12/docs-104481#deviceinfo)

      Information and state of a media device.


<span id="onaudiodevicestatechanged"></span>
### onAudioDeviceStateChanged  

Triggered when the audio device connection state changes. For example, due to device disconnection or reconnection.

> You need to get microphone or speaker permission ([enableDevices](https://docs.byteplus.com/en/docs/12/docs-104478#enabledevices)) before you can receive this callback.


* **Type**

   ```ts
   (event: DeviceInfo) => void
   ```
   

* **Parameters**

   * **event**

      Type: [DeviceInfo](https://docs.byteplus.com/en/docs/12/docs-104481#deviceinfo)

      Information and state of a media device.


<span id="ontrackended"></span>
### onTrackEnded  

Media track ended event. Please restart capture in the callback thread.


* **Type**

   ```ts
   (event: { kind: string; isScreen: boolean;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ kind: string; isScreen: boolean; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |kind |`string` |Media stream kind. Refer to [kind](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/kind). |
         |isScreen |`boolean` |Whether it is a screen\-sharing stream. |
         


<span id="onroommessagereceived"></span>
### onRoomMessageReceived  

Event of receiving a broadcast text message in the room


* **Type**

   ```ts
   (event: { userId: string; message: any;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ userId: string; message: any; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |userID of the message sender. |
         |message |`any` |Contents of the message. |
         


<span id="onroombinarymessagereceived"></span>
### onRoomBinaryMessageReceived  

Event of receiving a broadcast binary message in the room


* **Type**

   ```ts
   (event: { userId: string; message: ArrayBuffer;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ userId: string; message: ArrayBuffer; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |userID of the message sender |
         |message |`ArrayBuffer` |Contents of the message |
         


<span id="onusermessagereceived"></span>
### onUserMessageReceived  

Receiving a point\-to\-point text message from one of the users in the room by calling [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendusermessage)


* **Type**

   ```ts
   (event: UserMessageEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [UserMessageEvent](https://docs.byteplus.com/en/docs/12/docs-104481#usermessageevent)


<span id="onuserbinarymessagereceived"></span>
### onUserBinaryMessageReceived  

Receiving a point\-to\-point binary message from one of the users in the room


* **Type**

   ```ts
   (event: UserBinaryMessageEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [UserBinaryMessageEvent](https://docs.byteplus.com/en/docs/12/docs-104481#userbinarymessageevent)


<span id="onremotestreamstats"></span>
### onRemoteStreamStats  

Statistics of subscribed media streams and network states in a cycle of 2s


* **Type**

   ```ts
   (stats: RemoteStreamStats) => void
   ```
   

* **Parameters**

   * **stats**

      Type: [RemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-104481#remotestreamstats)


<span id="onlocalstreamstats"></span>
### onLocalStreamStats  

Statistics of local media streams and network states in a cycle of 2s


* **Type**

   ```ts
   (stats: LocalStreamStats) => void
   ```
   

* **Parameters**

   * **stats**

      Type: [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-104481#localstreamstats)


<span id="onpublicstreamstats"></span>
### onPublicStreamStats  

This 2 s periodical callback notifies information of the WTN stream after calling [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream).


* **Deprecated**

   since 4.65, use [onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotevideostats) and [onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremoteaudiostats) instead.

* **Type**

   ```ts
   (stats: PublicStreamStats) => void
   ```
   

* **Parameters**

   * **stats**

      Type: [PublicStreamStats](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamstats)


<span id="onlocalstatsexception"></span>
### onLocalStatsException  

SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually causes a problem with the call quality. If the problem is resolved, you will also receive this callback.


* **Type**

   ```ts
   (exception: LocalStatsException) => void
   ```
   

* **Parameters**

   * **exception**

      Type: [LocalStatsException](https://docs.byteplus.com/en/docs/12/docs-104481#localstatsexception)


<span id="onremotestatsexception"></span>
### onRemoteStatsException  

SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually causes a problem with the call quality. If the problem is resolved, you will also receive this callback.


* **Type**

   ```ts
   (exception: RemoteStatsException) => void
   ```
   

* **Parameters**

   * **exception**

      Type: [RemoteStatsException](https://docs.byteplus.com/en/docs/12/docs-104481#remotestatsexception)


<span id="onlocalaudiopropertiesreport"></span>
### onLocalAudioPropertiesReport  

After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will periodically receive this callback for the instant information about local audio.

Local audio includes the microphone audio and the screen audio captured using RTC SDK internal mechanisms.


* **Type**

   ```ts
   (event: LocalAudioPropertiesInfo[]) => void
   ```
   

* **Parameters**

   * **event**

      Type: [LocalAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-104481#localaudiopropertiesinfo)`[]`

      Information about local audio.


<span id="onremoteaudiopropertiesreport"></span>
### onRemoteAudioPropertiesReport  

After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will receive the cycling callbacks, each providing instant information about the subscribed remote audio streams.

The remote audio streams include the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism.


* **Type**

   ```ts
   (event: RemoteAudioPropertiesInfo[]) => void
   ```
   

* **Parameters**

   * **event**

      Type: [RemoteAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-104481#remoteaudiopropertiesinfo)`[]`

      Information about remote audio.


<span id="onactivespeaker"></span>
### onActiveSpeaker  

After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will periodically receive this callback for the information of the user with the highest voice volume.


* **Type**

   ```ts
   (userInfo: UserInfo) => void
   ```
   

* **Parameters**

   * **userInfo**

      Type: [UserInfo](https://docs.byteplus.com/en/docs/12/docs-104481#userinfo)

      The information of the user with the highest voice volume.


<span id="onaudioplaybackdevicechanged"></span>
### onAudioPlaybackDeviceChanged  

The current playback device has been changed successfully by calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice).


* **Type**

   ```ts
   (event: MediaDeviceInfo) => void
   ```
   

* **Parameters**

   * **event**

      Type: `MediaDeviceInfo`

      Information of the media devices. See [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo).


<span id="onuserstartaudiocapture"></span>
### onUserStartAudioCapture  

The remote clients in the room will be informed of the state change via this event after the publisher starts audio capture by calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture).


* **Type**

   ```ts
   (event: { userId: string;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ userId: string; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |The publisher who starts the internal audio capture |
         


<span id="onuserstopaudiocapture"></span>
### onUserStopAudioCapture  

The remote clients in the room will be informed of the state change via this event after the publisher stops audio capture by calling [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopaudiocapture).


* **Type**

   ```ts
   (event: { userId: string;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ userId: string; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |The userId of the publisher who stops the internal audio capture. |
         


<span id="onuserstartvideocapture"></span>
### onUserStartVideoCapture  

The remote clients in the room will be informed of the state change via this event after the publisher starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture).


* **Type**

   ```ts
   (event: { userId: string;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ userId: string; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |The userId of the publisher who starts the internal video capture. |
         


<span id="onuserstopvideocapture"></span>
### onUserStopVideoCapture  

The remote clients in the room will be informed of the state change via this event after the publisher stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopvideocapture).


* **Type**

   ```ts
   (event: { userId: string;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ userId: string; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |The userId of the publisher who stops the internal video capture. |
         


<span id="onseimessagereceived"></span>
### onSEIMessageReceived  

Event of receiving SEI data from video frames


* **Type**

   ```ts
   (event: onSEIMessageEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onSEIMessageEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onseimessageevent)

      Event of receiving SEI data


<span id="onseistreamupdate"></span>
### onSEIStreamUpdate  

Stream update event of stream that contains SEI information.

In a voice call scenario, when a remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage) to send SEI data via the black frame video stream, the stream's sending status will be notified to the local user through this event callback.

If the video frame carrying SEI data is a black frame, you do not need to render the video frame.


* **Type**

   ```ts
   (event: onSEIStreamUpdateEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [onSEIStreamUpdateEvent](https://docs.byteplus.com/en/docs/12/docs-104481#onseistreamupdateevent)

      Stream containing SEI information update event.


<span id="onautosubscriberesult"></span>
### onAutoSubscribeResult  

Result of the Auto\-Subscription


* **Type**

   ```ts
   (event: { userId: string; isScreen: boolean; state: SubscribeState;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ userId: string; isScreen: boolean; state: `[SubscribeState](https://docs.byteplus.com/en/docs/12/docs-104481#subscribestate)`; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |userId |`string` |The userId of the publisher to be subscribed |
         |isScreen |`boolean` |Whether it is a screen\-sharing stream |
         |state |`SubscribeState` |Subscription state. |
         


<span id="onautopublishresult"></span>
### onAutoPublishResult  

Result of Auto\-publishing. You will receive this event if you enable Auto\-publish when calling `joinRoom`


* **Type**

   ```ts
   (event: { isScreen: boolean; state: PublishState;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ isScreen: boolean; state: `[PublishState](https://docs.byteplus.com/en/docs/12/docs-104481#publishstate)`; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |isScreen |`boolean` |Whether it is a screen\-sharing stream |
         |state |`PublishState` |Publish state. |
         


<span id="onautoplayfailed"></span>
### onAutoplayFailed  

Auto\-play fails.


* **Type**

   ```ts
   (event: AutoPlayFailedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [AutoPlayFailedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#autoplayfailedevent)

      Event related to the player


<span id="onerror"></span>
### onError  

An error occurred in the SDK.


* **Type**

   ```ts
   (event: { errorCode: ErrorCode.DUPLICATE_LOGIN | ErrorCode.RTM_DUPLICATE_LOGIN | ErrorCode.RTM_TOKEN_ERROR | ErrorCode.TOKEN_EXPIRED | ErrorCode.RECONNECT_FAILED | ErrorCode.KICKED_OUT | ErrorCode.ROOM_DISMISS; forbiddenTime?: number;}) => void
   ```
   

* **Parameters**

   * **event**

      Type: `{ errorCode: ErrorCode.DUPLICATE_LOGIN | ErrorCode.RTM_DUPLICATE_LOGIN | ErrorCode.RTM_TOKEN_ERROR | ErrorCode.TOKEN_EXPIRED | ErrorCode.RECONNECT_FAILED | ErrorCode.KICKED_OUT | ErrorCode.ROOM_DISMISS; forbiddenTime?: number | undefined; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |errorCode |`ErrorCode.KICKED_OUT \| ErrorCode.ROOM_DISMISS \| ErrorCode.TOKEN_EXPIRED \| ErrorCode.DUPLICATE_LOGIN \| ErrorCode.RTM_DUPLICATE_LOGIN \| ErrorCode.RTM_TOKEN_ERROR \| ErrorCode.RECONNECT_FAILED` |See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode). |
         |forbiddenTime |`number \| undefined` |The Unix timestamp in milliseconds when the room will be unbanned.<br><br>When `forbiddenTime` is 0, it represents that the user can enter the room again. |
         


<span id="onaudiomixingstatechanged"></span>
### onAudioMixingStateChanged  

Event of the state change of audio mixing


* **Type**

   ```ts
   (event: AudioMixingStateChangedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [AudioMixingStateChangedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#audiomixingstatechangedevent)


<span id="onusermessagereceivedoutsideroom"></span>
### onUserMessageReceivedOutsideRoom  

Event of receiving a text message


* **Type**

   ```ts
   (event: UserMessageEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [UserMessageEvent](https://docs.byteplus.com/en/docs/12/docs-104481#usermessageevent)


<span id="onuserbinarymessagereceivedoutsideroom"></span>
### onUserBinaryMessageReceivedOutsideRoom  

Event of receiving a binary message


* **Type**

   ```ts
   (event: UserBinaryMessageEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [UserBinaryMessageEvent](https://docs.byteplus.com/en/docs/12/docs-104481#userbinarymessageevent)


<span id="ontokenwillexpire"></span>
### onTokenWillExpire  

You will receive this callback 30 seconds before the Token expires.

Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to submit a new Token. The user will be removed from the room when the Token expires.


* **Type**

   ```ts
   () => void
   ```
   


<span id="ontokenpublishprivilegewillexpire"></span>
### onTokenPublishPrivilegeWillExpire  

This callback will be triggered 30 seconds before the token publishing permission expires.

Upon receiving this callback, call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the token.


* **Type**

   ```ts
   () => void
   ```
   

* **Notes**

   If the Token is not updated in time, the publishing permission will expire and the stream that is being published will stop. The publisher will receive the [onTokenPublishPrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/docs-104479#ontokenpublishprivilegedidexpired) callback, and the remote user will receive the [onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserunpublishstream)/[onUserUnpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserunpublishscreen) callback, with the reason being `STREAM_REMOVE_REASON_TOKEN_PRIVILEGE_EXPIRED`.


<span id="ontokenpublishprivilegedidexpired"></span>
### onTokenPublishPrivilegeDidExpired  

This callback is triggered when the token publishing permission expires. Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the Token.


* **Type**

   ```ts
   (e: { errorCode?: ErrorCode; message?: string;}) => void
   ```
   

* **Parameters**

   * **e**

      Type: `{ errorCode?: `[ErrorCode](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode)` | undefined; message?: string | undefined; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |errorCode |`ErrorCode \| undefined` |The `TOKEN_NO_PUBLISH_PERMISSION` error code. |
         |message |`string \| undefined` |Error message. |
         


<span id="ontokensubscribeprivilegewillexpire"></span>
### onTokenSubscribePrivilegeWillExpire  

This callback will be triggered 30 seconds before the token subscription permission expires.

Upon receiving this callback, call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the token.


* **Type**

   ```ts
   () => void
   ```
   

* **Notes**

   If the Token is not updated in time after receiving this callback, the streams that have been subscribed to will be unsubscribed once the token subscription permission expires, and the subscriber will receive the [onTokenSubscribePrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/docs-104479#ontokensubscribeprivilegedidexpired) callback.

   Also, attempts to subscribe to new streams will fail, returning an error code `TOKEN_NO_SUBSCRIBE_PERMISSION`, indicating that the token subscription permission has expired.


<span id="ontokensubscribeprivilegedidexpired"></span>
### onTokenSubscribePrivilegeDidExpired  

This callback is triggered when the token subscription permission expires. Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the Token.


* **Type**

   ```ts
   (e: { errorCode?: ErrorCode; message?: string;}) => void
   ```
   

* **Parameters**

   * **e**

      Type: `{ errorCode?: `[ErrorCode](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode)` | undefined; message?: string | undefined; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |errorCode |`ErrorCode \| undefined` |The `TOKEN_NO_SUBSCRIBE_PERMISSION` error code. |
         |message |`string \| undefined` |Error message. |
         


<span id="oncloudproxyconnected"></span>
### onCloudProxyConnected  

Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-104478#startcloudproxy) to start cloud proxy, and the SDK connects to the proxy server successfully.


* **Type**

   ```ts
   (event: CloudProxyConnectedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [CloudProxyConnectedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#cloudproxyconnectedevent)


<span id="onpushpublicstreamresult"></span>
### onPushPublicStreamResult  

Callback of the result of publishing the WTN stream.

After calling [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startpushpublicstream), you will be informed of the result through this callback.


* **Type**

   ```ts
   (event: PublicStreamResultEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [PublicStreamResultEvent](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamresultevent)


<span id="onpublicstreamseimessagereceived"></span>
### onPublicStreamSEIMessageReceived  

Callback of the SEI carried by the public video stream.

You will receive SEI by this callback if the WTN stream you subscribed to by calling [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) is carrying SEI.


* **Deprecated**

   since 4.65, use [onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnseimessagereceived) instead.

* **Type**

   ```ts
   (event: PublicStreamSEIMessageEvent) => void
   ```
   

* **Notes**

   When multiple streams in the WTN stream contain SEI:

   * You will receive SEI from all the video frames if the SEI do not have conflicts.

   * However, if SEI from video frames have conflicts, you will receive only one of them.

* **Parameters**

   * **event**

      Type: [PublicStreamSEIMessageEvent](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamseimessageevent)


<span id="onfirstpublicstreamvideoframedecoded"></span>
### onFirstPublicStreamVideoFrameDecoded  

Callback of the successful decoding of the first video frame of the WTN stream.

Refer to [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) for details about subscribing to a WTN stream.


* **Deprecated**

   since 4.65, use [onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnfirstremotevideoframedecoded) instead.

* **Type**

   ```ts
   (event: PublicStreamVideoFirstFrameDecodedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [PublicStreamVideoFirstFrameDecodedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamvideofirstframedecodedevent)


<span id="onfirstpublicstreamaudioframedecoded"></span>
### onFirstPublicStreamAudioFrameDecoded  

Callback of the successful decoding of the first audio frame of the WTN stream.

Refer to [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) for details about subscribing to a WTN stream.


* **Deprecated**

   since 4.65.

* **Type**

   ```ts
   (event: PublicStreamAudioFirstFrameDecodedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [PublicStreamAudioFirstFrameDecodedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamaudiofirstframedecodedevent)


<span id="onfirstpublicstreamvideoframerendered"></span>
### onFirstPublicStreamVideoFrameRendered  

Callback of the successful rendering of the first video frame of the WTN stream.

Refer to [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) for details about subscribing to a WTN stream.


* **Deprecated**

   since 4.65, use [onWTNRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotevideostatechanged) instead.

* **Type**

   ```ts
   (event: PublicStreamAudioFirstFrameDecodedEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [PublicStreamAudioFirstFrameDecodedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamaudiofirstframedecodedevent)


<span id="onaudioplaybackdevicetestvolume"></span>
### onAudioPlaybackDeviceTestVolume  

Notification on the playing volume during the test for the local audio devices


* **Type**

   ```ts
   (volume: number) => void
   ```
   

* **Notes**

   Starting an audio\-device test by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudioplaybackdevicetest) or [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiodevicerecordtest) will register this callback for regular notification on playing volume. You can set the time interval between each callback by passing a proper value when calling the API above.

* **Parameters**

   * **volume**

      Type: `number`

      playing volume during the test for the local audio devices in milliseconds. We recommend to set it to 200 ms. The range is [0,255].


<span id="onnetworkquality"></span>
### onNetworkQuality  

The callback reports the upstream and downstream network quality of the local user every 2s after the user enters the room.


* **Type**

   ```ts
   (uplinkNetworkQuality: NetworkQuality, downlinkNetworkQuality: NetworkQuality) => void
   ```
   

* **Parameters**

   * **uplinkNetworkQuality**

      Type: [NetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104481#networkquality)

      Upstream network quality.

   * **downlinkNetworkQuality**

      Type: [NetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104481#networkquality)

      Downstream network quality.


<span id="onsimulcastsubscribefallback"></span>
### onSimulcastSubscribeFallback  

Receives this callback when fallback happens or the stream recovers from fallback.


* **Type**

   ```ts
   (event: RemoteStreamSwitch) => void
   ```
   

* **Parameters**

   * **event**

      Type: [RemoteStreamSwitch](https://docs.byteplus.com/en/docs/12/docs-104481#remotestreamswitch)

      Information about stream switching


<span id="onremotevideosizechanged"></span>
### onRemoteVideoSizeChanged  

When the resolution of remote video changes, users who subscribed to the stream will receive this callback.


* **Type**

   ```ts
   (key: RemoteStreamKey, info: { width: number; height: number;}) => void
   ```
   

* **Parameters**

   * **key**

      Type: [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-104481#remotestreamkey)

      Information of the remote stream

   * **info**

      Type: `{ width: number; height: number; }`

      Information of video frame

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |width |`number` |Width（pixel） |
         |height |`number` |Height（pixel） |
         


<span id="onstreammixingevent"></span>
### onStreamMixingEvent  

Pushing a mixed stream to CDN events


* **Type**

   ```ts
   (event: StreamMixingEvent) => void
   ```
   

* **Parameters**

   * **event**

      Type: [StreamMixingEvent](https://docs.byteplus.com/en/docs/12/docs-104481#streammixingevent)


<span id="onvideostreambanned"></span>
### onVideoStreamBanned  

The callback is triggered when the openAPI BanUserStream/UnbanUserStream is called to ban/unban the video stream of the specified user from publishing.


* **Type**

   ```ts
   (event: VideoStreamBannedEvent) => void
   ```
   

* **Notes**

   * When the specified user in the room is banned/unbanned from sending video streams, all users in the room will receive the callback.

   * If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

   * If a user is banned, other users receive this callback again when they leave and re\-enter the room.

   * Only banned/unbanned user will receive this callback if the conference mode is enabled in the console.

   * If the room is dissolved and created again, the status in the room is cleared.

* **Parameters**

   * **event**

      Type: [VideoStreamBannedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#videostreambannedevent)


<span id="onaudiostreambanned"></span>
### onAudioStreamBanned  

The callback is triggered when the openAPI BanUserStream/UnbanUserStream is called to ban/unban the audio stream of the specified user from publishing.


* **Type**

   ```ts
   (event: AudioStreamBannedEvent) => void
   ```
   

* **Notes**

   * When the specified user in the room is banned/unbanned from sending audio streams, all users in the room will receive the callback.

   * If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

   * If a user is banned, other users receive this callback again when they leave and re\-enter the room.

   * Only banned/unbanned user will receive this callback if the conference mode is enabled in the console.

   * If the room is dissolved and created again, the status in the room is cleared.

* **Parameters**

   * **event**

      Type: [AudioStreamBannedEvent](https://docs.byteplus.com/en/docs/12/docs-104481#audiostreambannedevent)


<span id="onlocalvideosizechanged"></span>
### onLocalVideoSizeChanged  

The callback of the actual video capturing configuration.


* **Type**

   ```ts
   (e: { streamIndex: StreamIndex; info: { width: number; height: number; };}) => void
   ```
   

* **Parameters**

   * **e**

      Type: `{ streamIndex: `[StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)`; info: { width: number; height: number;}; }`

      The actual video capturing configuration.

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |streamIndex |`StreamIndex` |The attributes of the screen\-sharing stream. |
         |info |`{ width: number; height: number; }` |The actual capturing configuration. |
         |info.width |`number` |The width of the shared video (px). |
         |info.height |`number` |The height of the shared video (px). |
         


<span id="onserverparamssetresult"></span>
### onServerParamsSetResult  

Event indicating whether the message server configuration succeeds


* **Type**

   ```ts
   (error?: ErrorCode) => void
   ```
   

* **Notes**

   * This event notifies you of the result after the call of [setServerParams](https://docs.byteplus.com/en/docs/12/docs-104478#setserverparams).

   * If you lose internet connection after calling [setServerParams](https://docs.byteplus.com/en/docs/12/docs-104478#setserverparams), you will receive this event once the internet reconnects.

* **Parameters**

   * **error**

      Type: [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode)` | undefined`

      Error code


<span id="onforwardstreamerror"></span>
### onForwardStreamError  

Event of failing to forward stream across rooms.


* **Type**

   ```ts
   (e: ForwardStreamStateInfo) => void
   ```
   

* **Parameters**

   * **e**

      Type: [ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreamstateinfo)

      Status information for forwarding media stream across rooms.


<span id="onplayervisibility"></span>
### onPlayerVisibility  

Event of player visibility change, triggered every 30 seconds to notify users of changes in the visibility status of the player.


* **Type**

   ```ts
   (e: PlayerVisibility[]) => void
   ```
   

* **Parameters**

   * **e**

      Type: [PlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104481#playervisibility)`[]`

      Array of player visibility information, including player ID, user ID, and visibility status.
