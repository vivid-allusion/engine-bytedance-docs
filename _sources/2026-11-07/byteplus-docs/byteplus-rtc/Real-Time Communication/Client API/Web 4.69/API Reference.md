---
title: "API Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478"
---

<span id="wtnstream"></span>
## WTNstream  

Type: `interface`


* **API**



|Method |Description |
|---|---|
|[startPushWTN](https://docs.byteplus.com/en/docs/12/14190#wtnstream-startpushwtn) |Starts publishing a WTN stream without joining a room. |
|[stopPushWTN](https://docs.byteplus.com/en/docs/12/14190#wtnstream-stoppushwtn) |Stops publishing the WTN stream which was published via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn). |
|[muteWTNLocalAudio](https://docs.byteplus.com/en/docs/12/14190#wtnstream-mutewtnlocalaudio) |Pauses/Resumes publishing the audio of a WTN stream. |
|[muteWTNLocalVideo](https://docs.byteplus.com/en/docs/12/14190#wtnstream-mutewtnlocalvideo) |Pauses/Resumes publishing the video of a WTN stream. |
|[sendWTNSEIMessage](https://docs.byteplus.com/en/docs/12/14190#wtnstream-sendwtnseimessage) |Sends SEI via a WTN stream. |
|[startPlayWTN](https://docs.byteplus.com/en/docs/12/14190#wtnstream-startplaywtn) |Subscribes to a designated WTN stream.<br><br>You can call this API to subscribe to a WTN stream whether you joined the room or not. |
|[stopPlayWTN](https://docs.byteplus.com/en/docs/12/14190#wtnstream-stopplaywtn) |Unsubscribes from a designated WTN stream. |
|[muteWTNRemoteAudio](https://docs.byteplus.com/en/docs/12/14190#wtnstream-mutewtnremoteaudio) |Pauses/Resumes subscribing to the audio of a WTN stream. |
|[muteWTNRemoteVideo](https://docs.byteplus.com/en/docs/12/14190#wtnstream-mutewtnremotevideo) |Pauses/Resumes subscribing to the video of a WTN stream. |
|[setWTNRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/14190#wtnstream-setwtnremotevideoplayer) |Sets the player information and rendering mode for the WTN stream. |
|[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14190#wtnstream-setwtnremoteaudioplaybackvolume) |Adjusts audio playback volume of a WTN stream. |
|[getWTNVideoPlayerVisibility](https://docs.byteplus.com/en/docs/12/14190#wtnstream-getwtnvideoplayervisibility) |Gets the visibility status of the specified WTN stream's video player. |


<span id="startpushwtn"></span>
### startPushWTN  

Starts publishing a WTN stream without joining a room.


* **Type**

   ```ts
   (token: string | null, streamId: string, videoMute: boolean, audioMute: boolean) => Promise<void>
   ```
   

* **Notes**

   * Users with the same `appID` can call [startPlayWTN](https://docs.byteplus.com/en/docs/12/14190#startplaywtn) to subscribe to and play the WTN stream regardless of whether the user has joined the room.

   * Users with different `userID` can call this API with the same stream ID to update the parameters.

   * Call this API with different stream IDs to publish multiple WTN streams.

   * Call [stopPushWTN](https://docs.byteplus.com/en/docs/12/14190#stoppushwtn) to stop publishing the WTN stream.

* **Parameters**

   * **token**

      Type: `string | null`

      Dynamic key. It is used for authentication and verification of users publishing a WTN stream.

      When testing, you can use the console to generate temporary tokens where you can set any value for RoomId. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Use Token to complete authentication](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.

      Apps with different AppIDs are not interoperable.

      Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will fail.

   * **streamId**

      Type: `string`

      The WTN stream's ID. The string must conform to the regular expression: `[a-zA-Z0-9_@\-\.]{1,128}`.

   * **videoMute**

      Type: `boolean`

      Whether to disable video. `true`: Disable video. `false`: Enable video.

   * **audioMute**

      Type: `boolean`

      Whether to disable audio. `true`: Disable audio. `false`: Enable audio.

* **Return Value**

   Type: `Promise<void>`

   You will also receive the [onWTNPushStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnpushstatechanged) callback.


<span id="stoppushwtn"></span>
### stopPushWTN  

Stops publishing the WTN stream which was published via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn).


* **Type**

   ```ts
   (streamId: string) => Promise<void>
   ```
   

* **Notes**

   To stop publishing a WTN stream initiated by [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream), call [stopPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stoppushpublicstream).

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID.

      The WTN stream must be published by the current user.

* **Return Value**

   Type: `Promise<void>`

   You will also receive the [onWTNPushStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnpushstatechanged) callback.


<span id="mutewtnlocalaudio"></span>
### muteWTNLocalAudio  

Pauses/Resumes publishing the audio of a WTN stream.


* **Type**

   ```ts
   (streamId: string, mute: boolean) => Promise<void>
   ```
   

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID. The local user has published the WTN stream via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn).

   * **mute**

      Type: `boolean`

      Whether to exclude audio.

* `true`: Exclude

* `false`: Include

* **Return Value**

   Type: `Promise<void>`

   You will also receive the [onWTNPushStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnpushstatechanged) callback.


<span id="mutewtnlocalvideo"></span>
### muteWTNLocalVideo  

Pauses/Resumes publishing the video of a WTN stream.


* **Type**

   ```ts
   (streamId: string, mute: boolean) => Promise<void>
   ```
   

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID. The local user has published the WTN stream via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn).

   * **mute**

      Type: `boolean`

      Whether to exclude video.

* `true`: Exclude

* `false`: Include

* **Return Value**

   Type: `Promise<void>`

   You will also receive the [onWTNPushStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnpushstatechanged) callback.


<span id="sendwtnseimessage"></span>
### sendWTNSEIMessage  

Sends SEI via a WTN stream.


* **Type**

   ```ts
   (streamId: string, sei: Uint8Array, repeatCount: number) => void
   ```
   

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID. The local user has published the WTN stream via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn).

   * **sei**

      Type: `Uint8Array`

      SEI message.

   * **repeatCount**

      Type: `number`

      The number of times the SEI message is sent. The value range is [0, max{29, %{video frame rate}\-1}]. The recommended range is [2,4].

&nbsp;

      After calling this API, the SEI data will be added to the consecutive `repeat_count+1` video frames starting from the current video frame.


<span id="startplaywtn"></span>
### startPlayWTN  

Subscribes to a designated WTN stream.

You can call this API to subscribe to a WTN stream whether you joined the room or not.


* **Type**

   ```ts
   (token: string | null, streamId: string, videoMute: boolean, audioMute: boolean) => Promise<void>
   ```
   

* **Notes**

   * Before calling this API, we recommend that you call [setPublicStreamVideoPlayer](https://docs.byteplus.com/en/docs/12/14190#setpublicstreamvideoplayer) first to set the player information and rendering mode for the WTN stream.

   * After calling this API, you will receive [onFirstPublicStreamVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-104479#onfirstpublicstreamvideoframedecoded) and [onFirstPublicStreamAudioFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-104479#onfirstpublicstreamaudioframedecoded) once the first frame has been decoded.

   * If the WTN stream contains SEI message, you will receive the message by being informed through [onPublicStreamSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onpublicstreamseimessagereceived).

   * Call [stopPlayPublicStream](https://docs.byteplus.com/en/docs/12/14190#stopplaypublicstream) to unsubscribe from the WTN stream.

* **Parameters**

   * **token**

      Type: `string | null`

      Dynamic key. It is used for authentication and verification of users subscribing to a WTN stream.

      When testing, you can use the console to generate temporary tokens. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Use Token to complete authentication](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.

      Apps with different AppIDs are not interoperable.

      Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will fail.

   * **streamId**

      Type: `string`

      The WTN stream's ID. The WTN stream can be published by calling [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#startpushwtn) or [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startpushpublicstream).

      If the designated stream is not published when you call this API, you will receive the WTN stream once it is published.

   * **videoMute**

      Type: `boolean`

      Whether to disable video. `true`: Disable video. `false`: Enable video.

   * **audioMute**

      Type: `boolean`

      Whether to disable audio. `true`: Disable audio. `false`: Enable audio.

* **Return Value**

   Type: `Promise<void>`


<span id="stopplaywtn"></span>
### stopPlayWTN  

Unsubscribes from a designated WTN stream.


* **Type**

   ```ts
   (streamId: string) => Promise<void>
   ```
   

* **Notes**

   Call [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/14190#startplaypublicstream) to subscribe to the WTN stream.

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID.

* **Return Value**

   Type: `Promise<void>`


<span id="mutewtnremoteaudio"></span>
### muteWTNRemoteAudio  

Pauses/Resumes subscribing to the audio of a WTN stream.


* **Type**

   ```ts
   (streamId: string, mute: boolean) => Promise<void>
   ```
   

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID. The local user has subscribed to the WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/14190#startplaywtn).

   * **mute**

      Type: `boolean`

      Whether to exclude audio.

* `true`: Exclude

* `false`: Include

* **Return Value**

   Type: `Promise<void>`


<span id="mutewtnremotevideo"></span>
### muteWTNRemoteVideo  

Pauses/Resumes subscribing to the video of a WTN stream.


* **Type**

   ```ts
   (streamId: string, mute: boolean) => Promise<void>
   ```
   

* **Notes**

   You can use this method to pause/resume the audio of a WTN stream after you have subscribed to the WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/14190#startplaywtn).

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID. The local user has subscribed to the WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/14190#startplaywtn).

   * **mute**

      Type: `boolean`

      Whether to exclude video.

* `true`: Exclude

* `false`: Include

* **Return Value**

   Type: `Promise<void>`


<span id="setwtnremotevideoplayer"></span>
### setWTNRemoteVideoPlayer  

Sets the player information and rendering mode for the WTN stream.


* **Type**

   ```ts
   (streamId: string, videoPlayerOption: Omit<VideoPlayerOption, 'userId' | 'playerId'>) => HTMLVideoElement | undefined
   ```
   

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID.

   * **videoPlayerOption**

      Type: `Omit<`[VideoPlayerOption](https://docs.byteplus.com/en/docs/12/docs-104481#videoplayeroption)`, "userId" | "playerId">`

      Player information and rendering mode.

* **Return Value**

   Type: `HTMLVideoElement | undefined`

   Refer to [HTMLVideoElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLVideoElement).


<span id="setwtnremoteaudioplaybackvolume"></span>
### setWTNRemoteAudioPlaybackVolume  

Adjusts audio playback volume of a WTN stream.


* **Type**

   ```ts
   (streamId: string, volume: number) => void
   ```
   

* **Notes**

   * It is recommended to set the playback volume after the playing has started.

   * If the playing has not yet started when you call this API, the setting will take effect after it starts.

* **Parameters**

   * **streamId**

      Type: `string`

      The Id of a specified WTN stream.

   * **volume**

      Type: `number`

      The percentage of playback volume to the original volume in the range of [0, 400]. The default value is 100%.

      For better call quality, it is recommended to set the value in the range of [0, 100].


<span id="getwtnvideoplayervisibility"></span>
### getWTNVideoPlayerVisibility  

> Available since v4.67.


Gets the visibility status of the specified WTN stream's video player.


* **Type**

   ```ts
   (streamId: string) => PlayerVisibility | undefined
   ```
   

* **Parameters**

   * **streamId**

      Type: `string`

      The WTN stream's ID.

* **Return Value**

   Type: [PlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104481#playervisibility)` | undefined`

   Returns the visibility status of the video player, or `undefined` if the player does not exist.


<span id="rtcengine"></span>
## RTCEngine  

Type: `interface`


* **API**



|Method |Description |
|---|---|
|[joinRoom](https://docs.byteplus.com/en/docs/12/14190#rtcengine-joinroom) |Join an existing room or create a new room and join.<br><br>When calling this method, you need to specify the `roomId`. If a room corresponding to the specified roomId already exists, the SDK will directly join that room. If no room corresponds to the specified roomId, the SDK will automatically create a new room using that roomId and join it. |
|[leaveRoom](https://docs.byteplus.com/en/docs/12/14190#rtcengine-leaveroom) |Leave the room.<br><br>The user calls this API to leave the room, end the call process, and release all call\-related resources. |
|[publishStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-publishstream) |Publishes media streams captured by camera/microphone in the current room. |
|[unpublishStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-unpublishstream) |Stops publishing media streams captured by camera/microphone in the current room. |
|[publishScreen](https://docs.byteplus.com/en/docs/12/14190#rtcengine-publishscreen) |Publishes local screen sharing streams in the current room. |
|[unpublishScreen](https://docs.byteplus.com/en/docs/12/14190#rtcengine-unpublishscreen) |Stops publishing local screen sharing streams in the current room. |
|[subscribeStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-subscribestream) |Subscribes to specific remote media streams captured by camera/microphone.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[unsubscribeStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-unsubscribestream) |Unsubscribes from specific remote media streams captured by camera/microphone.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[subscribeScreen](https://docs.byteplus.com/en/docs/12/14190#rtcengine-subscribescreen) |Subscribes to a specific screen sharing media stream.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[unsubscribeScreen](https://docs.byteplus.com/en/docs/12/14190#rtcengine-unsubscribescreen) |Unsubscribes from specific screen sharing media stream.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[updateToken](https://docs.byteplus.com/en/docs/12/14190#rtcengine-updatetoken) |Update Token.<br><br>You will receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#ontokenwillexpire) 30 s before the Token expires. Call this API to submit a new Token. |
|[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setaudiocapturedevice) |Switch the microphone used for internal audio capturing. |
|[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setvideocapturedevice) |Switch the camera used for internal video capturing. |
|[startVideoCapture](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startvideocapture) |Enable internal video capture. The default state is off.<br><br>Internal video capture refers to: capturing video using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartvideocapture) after the publisher starts video capture by calling this API. |
|[stopVideoCapture](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopvideocapture) |Stop internal video capture. The default setting is off.<br><br>Internal video capture refers to: capturing video using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstopvideocapture) after the publisher stops video capture by calling this API. |
|[startAudioCapture](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startaudiocapture) |Start internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartaudiocapture) after the publisher starts audio capture by calling this API. |
|[stopAudioCapture](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopaudiocapture) |Stop internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstopaudiocapture) after stopping audio capture by calling this API. |
|[startAudioAndVideoCapture](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startaudioandvideocapture) |Enable audio and video capture using the internal capture module. When calling this method, the browser will request microphone and camera permissions simultaneously, and the user only needs to grant permission once.<br><br>When calling this method, other users in the room will receive the callback of [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartvideocapture) and [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartaudiocapture). |
|[startScreenCapture](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startscreencapture) |Use the capture module provided by the RTC SDK to capture the current screen stream for sharing. |
|[stopScreenCapture](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopscreencapture) |Stop screen sharing. |
|[setLocalVideoPlayer](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setlocalvideoplayer) |Add the local media stream to a player and set the rendering mode for the rendering of the local stream.<br><br>Listen to `onPlayerEvent` for the state after binding a view to the local video stream.<br><br>Call this API again with a blank view to remove the stream from the player. Doing this without a playerId while there are multiple players including a default player will remove the stream from the default player. |
|[setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setremotevideoplayer) |Add the remote media stream to a player and set the rendering mode for the rendering of the remote stream.<br><br>It is recommended to call this API and bind a view once the event of [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishstream)/[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishscreen) is triggered.<br><br>Call this API again with a blank view to remove the stream from the player. Doing this without a playerId while there are multiple players including a default player will remove the stream from the default player. |
|[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setlocalvideomirrortype) |Enable or disable the mirror mode for the local video stream. |
|[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setremotevideomirrortype) |When using internal rendering, enable mirroring for the remote stream. |
|[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setaudioplaybackdevice) |Sets the speaker or the earpiece as the audio playback device. The audio playback device defaults to the speaker. |
|[play](https://docs.byteplus.com/en/docs/12/14190#rtcengine-play) |Play audio and video stream manually.<br><br>Call this API when the user needs to take part in the audio and video interaction after calling [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine) and setting autoPlay to false. |
|[stop](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stop) |Pause the specified media stream. |
|[getAudioVolume](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getaudiovolume) |Gets the volume of the remote audio stream or the local audio stream captured by the local microphone and screen audio stream. |
|[setAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setaudioframecallback) |Toggle the callbacks carrying the audio frames. |
|[pauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-pauseallsubscribedstream) |Pause receiving remote media streams. |
|[resumeAllSubscribedStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-resumeallsubscribedstream) |Resume receiving remote media streams |
|[sendUserMessage](https://docs.byteplus.com/en/docs/12/14190#rtcengine-sendusermessage) |Send point\-to\-point text messages to a specified user in the room.<br><br>The recipient receives the message via [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onusermessagereceived) once the message is sent successfully. |
|[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/14190#rtcengine-senduserbinarymessage) |Send point\-to\-point binary messages to a specified user in the room.<br><br>The recipient receives the message via [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onuserbinarymessagereceived) once the message is sent successfully. |
|[sendRoomMessage](https://docs.byteplus.com/en/docs/12/14190#rtcengine-sendroommessage) |Send text messages to all other users in the room.<br><br>Users in the room will receive the message via [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onroommessagereceived) once the message is sent successfully. |
|[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/14190#rtcengine-sendroombinarymessage) |Send binary messages to all other users in the room.<br><br>Users in the room will receive binary message via [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onroombinarymessagereceived) once the message is sent successfully. |
|[sendSEIMessage](https://docs.byteplus.com/en/docs/12/14190#rtcengine-sendseimessage) |Send supplemental enhancement information (SEI) through video frames.<br><br>In the video call scenario, the SEI data will be sent with the video frames. In the voice call scenario, the SDK will generate a 16px × 16px black frame video stream to send the data. |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setvideoencoderconfig) |Configures the encoding settings for the camera videos on the publisher side. |
|[setScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setscreenencoderconfig) |Set the encoding configuration of the screen\-sharing stream, which is also applied in video capture.<br><br>If the configuration is not supported by your browser, the video will be captured based on the supported configuration. You will also receive the callback [onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalvideosizechanged). |
|[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setremotesimulcaststreamtype) |Sets your expected quality level of the remote video stream that you want to subscribe to or have subscribed to. |
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setlocalsimulcastmode) |Enables the Simulcast feature and configures the lower\-quality camera videos for the stream publisher. |
|[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14190#rtcengine-enableaudiopropertiesreport) |Enable audio information prompts. |
|[startLiveTranscoding](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startlivetranscoding) |Starts pushing media streams to CDN and sets the relevant configurations. |
|[updateLiveTranscoding](https://docs.byteplus.com/en/docs/12/14190#rtcengine-updatelivetranscoding) |Update configuration needed when pushing media streams to CDN.<br><br>After calling [startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#startlivetranscoding) to enable the function of pushing streams to CDN, you can call this API to update the relevant configurations. |
|[stopLiveTranscoding](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stoplivetranscoding) |Stop pushing media streams to CDN<br><br>To start pushing media streams to CDN, refer to [startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#startlivetranscoding). |
|[setBusinessId](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setbusinessid) |Set the business ID.<br><br>You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication. |
|[setUserVisibility](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setuservisibility) |Set user visibility. The local user is visible to others by default before calling this API.<br><br>An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capability](https://docs.byteplus.com/en/docs/12/docs-257549). |
|[setExternalVideoTrack](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setexternalvideotrack) |Set a custom videoTrack as the video source.<br><br>Before calling this API, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setvideosourcetype) to enable custom video capture. |
|[setExternalAudioTrack](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setexternalaudiotrack) |Set a custom audioTrack as the audio source.<br><br>Before calling this API, you must call [setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiosourcetype) to enable custom audio capture. |
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setvideosourcetype) |Switch the source from the internal to custom video capture.<br><br>Internal video capture refers to using built\-in video capture video. |
|[setAudioSourceType](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setaudiosourcetype) |Switch the source from the internal to custom audio capture.<br><br>Internal audio capture refers to using built\-in audio capture. |
|[getAudioMixingManager](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getaudiomixingmanager) |Creates an audio mixing manager object. |
|[getWTNStreamManager](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getwtnstreammanager) |Creates a WTN stream manager object. |
|[getCallId](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getcallid) |Get the call ID. Call this method after joining a room.<br><br>After creating a room, a `callId` is generated to identify the call for this room. |
|[setAudioCaptureConfig](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setaudiocaptureconfig) |Configure the internal audio capture. Different browsers have their own default settings. |
|[login](https://docs.byteplus.com/en/docs/12/14190#rtcengine-login) |Sign in to the RTM server.<br><br>Call this method before users within the same `appID` can communicate with each other via messages. |
|[logout](https://docs.byteplus.com/en/docs/12/14190#rtcengine-logout) |Log out of the RTS service. After calling this API to logout you are not able to call APIs to send messages and server messages. |
|[updateLoginToken](https://docs.byteplus.com/en/docs/12/14190#rtcengine-updatelogintoken) |Update the Token used to login. Since all tokens have a limited time\-to\-live, call this API to refresh the token. |
|[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getpeeronlinestatus) |Get the status of a user before sending him/her a P2P message. You can also call this API to check the status of the current user. |
|[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14190#rtcengine-sendusermessageoutsideroom) |Send point\-to\-point (P2P) text message to a user. |
|[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14190#rtcengine-senduserbinarymessageoutsideroom) |Send point\-to\-point (P2P) binary message to a user. |
|[setServerParams](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setserverparams) |Set the params of the server before calling [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendserverbinarymessage) to send messages to the server. |
|[sendServerMessage](https://docs.byteplus.com/en/docs/12/14190#rtcengine-sendservermessage) |Send point\-to\-point (P2P) text message to the server. |
|[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/14190#rtcengine-sendserverbinarymessage) |Send point\-to\-point (P2P) binary message to the server. |
|[startCloudProxy](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startcloudproxy) |Start cloud proxy |
|[stopCloudProxy](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopcloudproxy) |Stop cloud proxy |
|[startPushPublicStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startpushpublicstream) |Starts publishing a WTN stream after the user joins a room. |
|[updatePublicStreamParam](https://docs.byteplus.com/en/docs/12/14190#rtcengine-updatepublicstreamparam) |Update the properties of the WTN stream published by the current user via [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream). |
|[stopPushPublicStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stoppushpublicstream) |Stops publishing the WTN stream published by the current user via [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream). |
|[startPlayPublicStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startplaypublicstream) |Subscribes to a designated WTN stream.<br><br>You can call this API to subscribe to a WTN stream whether you joined the room or not. |
|[stopPlayPublicStream](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopplaypublicstream) |Unsubscribes from a designated WTN stream.<br><br>Call [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) to subscribe to the WTN stream. |
|[setPublicStreamVideoPlayer](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setpublicstreamvideoplayer) |Sets the player information and rendering mode for the WTN stream. |
|[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setdummycaptureimagepath) |Set the placeholder image during local video capture pause |
|[defaultTranscoding](https://docs.byteplus.com/en/docs/12/14190#rtcengine-defaulttranscoding) |Get the default parameters of `LiveTranscodeConfig`. |
|[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setsubscribefallbackoption) |Set the fallback option for remote media stream<br><br>Fallback means to enable media stream fallback or to subscribe to only audio stream under poor network conditions to ensure smooth communication. |
|[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setremoteuserpriority) |Set the priority of the remote user's media stream.<br><br>Use this API with [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-104478#setsubscribefallbackoption).<br><br>With video stream fallback enabled and user priority specified, the stream quality of higher priority user is the last to be compromised. |
|[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startaudioplaybackdevicetest) |Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will report the audio volume via the [onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-104479#onaudioplaybackdevicetestvolume) periodically. |
|[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopaudioplaybackdevicetest) |Stop the playback test for the local audio device. |
|[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startaudiodevicerecordtest) |Start the capture and playback test for local audio devices.<br><br>We recommend registering [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport) callback via [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport). Once the test starts, you can get the volume of the capturing audio by this callback. |
|[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopaudiodevicerecordandplaytest) |Call this API to stop recording in the test and start to play the recording.<br><br>After calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiodevicerecordtest), you need to call this API within 30 seconds. Otherwise, the recording will automatically stop and begin playing back the recorded audio. |
|[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopaudiodeviceplaytest) |Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiodevicerecordtest).<br><br>Before the test ends by itself, you can call this API to stop the recording or playing. |
|[setAudioProfile](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setaudioprofile) |Set the sound quality. |
|[getLocalStreamTrack](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getlocalstreamtrack) |Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the local audios or videos. |
|[getRemoteStreamTrack](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getremotestreamtrack) |Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the remote audios or videos. |
|[getPublicStreamTrack](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getpublicstreamtrack) |Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the audios or videos from the subscribed WTN stream. |
|[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/14190#rtcengine-takelocalsnapshot) |Take a snapshot of the local video. |
|[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/14190#rtcengine-takeremotesnapshot) |Take a snapshot of the remote video. |
|[registerExtension](https://docs.byteplus.com/en/docs/12/14190#rtcengine-registerextension) |Registers an extension.<br><br>You can use the extension to implement features such as [Beauty Effects](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148646), [Virtual Background](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148647). |
|[setRemoteStreamRenderSync](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setremotestreamrendersync) |Set whether the remote audio and video streams are rendered synchronously.<br><br>You can achieve ultra low latency by turning off the audio and video synchronization. |
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setcapturevolume) |Adjust audio capture volume. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setplaybackvolume) |Adjust audio playback volume of a specified remote user. |
|[setPublicStreamVolume](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setpublicstreamvolume) |Adjusts audio playback volume of a WTN stream. |
|[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14190#rtcengine-startforwardstreamtorooms) |Start forwarding media stream across rooms. See [Forward media stream across rooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104398) for details.<br><br>After calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-joinroom), you can call this API to publish the media stream to multiple rooms. This feature is suitable for scenarios such as co\-host PK and online karaoke. |
|[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14190#rtcengine-updateforwardstreamtorooms) |Update information of the rooms where the stream will be forwarded after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startforwardstreamtorooms). |
|[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14190#rtcengine-stopforwardstreamtorooms) |Stop forwarding media stream to all rooms. |
|[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14190#rtcengine-pauseforwardstreamtoallrooms) |Pause forwarding media stream to all rooms.<br><br>After calling this API, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-resumeforwardstreamtoallrooms) to resume. |
|[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14190#rtcengine-resumeforwardstreamtoallrooms) |Resume forwarding media stream to all rooms. |
|[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setaudioselectionconfig) |Set the priority of the local audio stream to be published. |
|[getRemoteVideoStats](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getremotevideostats) |Gets the statistics of subscribed video streams and network states. |
|[getRemoteAudioStats](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getremoteaudiostats) |Gets the statistics of subscribed audio streams and network states. |
|[getLocalVideoStats](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getlocalvideostats) |Gets the statistics of local video streams and network states. |
|[getLocalAudioStats](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getlocalaudiostats) |Gets the statistics of local audio streams and network states. |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setearmonitormode) |Enable/Disable in\-ear monitoring. |
|[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setearmonitorvolume) |Set the monitoring volume. |
|[getLocalVideoPlayerVisibility](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getlocalvideoplayervisibility) |Get the visibility state of local video player and reasons for invisibility. |
|[getRemotePlayerVisibility](https://docs.byteplus.com/en/docs/12/14190#rtcengine-getremoteplayervisibility) |Gets the visibility state of remote video player and reasons for invisibility. |


<span id="joinroom"></span>
### joinRoom  

Join an existing room or create a new room and join.

When calling this method, you need to specify the `roomId`. If a room corresponding to the specified roomId already exists, the SDK will directly join that room. If no room corresponds to the specified roomId, the SDK will automatically create a new room using that roomId and join it.


* **Type**

   ```ts
   (token: string | null, roomId: string, userInfo: UserInfo, roomConfig?: RoomConfig) => Promise<void>
   ```
   

* **Notes**

   * In the same room with the same App ID, the user ID of each user must be unique. The user will be kicked out of the room when a user with the same userID joins the room because of the error of `DUPLICATE_LOGIN`.

   * Remote users will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined) callback when a visible user joins the room. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14190#setuservisibility) to switch the visibility of the user.

   * By default, the user is visible in an RTC room. Joining fails when the number of users in an RTC room reaches the upper limit. To avoid this, call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14190#setuservisibility) to change the visibility of the audience users to false by considering the capacity for the invisible users is much larger than that for visible users. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capability](https://docs.byteplus.com/en/docs/12/docs-257549).

   * RTC SDK will try to reconnect after losing connection to the server caused by a poor network connection. At this point, [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. The remote user will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined) if a visible user reconnected successfully.

* **Parameters**

   * **token**

      Type: `string | null`

      Dynamic key. It is used for authentication and verification of users entering the room.

      You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Use Token to complete authentication](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.

      Apps with different AppIDs are not interoperable.

      Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will cause joining the room to fail.

   * **roomId**

      Type: `string`

      The ID of room you want to join or create. The string must conform to the regular expression: `[a-zA-Z0-9_@\-\.]{1,128}`.

   * **userInfo**

      Type: [UserInfo](https://docs.byteplus.com/en/docs/12/docs-104481#userinfo)

      User information.

   * **roomConfig**

      Type: [RoomConfig](https://docs.byteplus.com/en/docs/12/docs-104481#roomconfig)` | undefined`

      Room parameter configuration, set the room mode and whether to automatically publish or subscribe to the flow.

* **Return Value**

   Type: `Promise<void>`

   * `INVALID_TOKEN`: Failed to enter the room due to using an expired or invalid token.

   * `JOIN_ROOM_FAILED`: Failed to enter the room.

   * `REPEAT_JOIN`: Join the same room repeatedly.

   * `ROOM_FORBIDDEN`: Failed to enter the room because the room has been banned.

   * `USER_FORBIDDEN`: Failed to enter the room because the user has been banned.


<span id="leaveroom"></span>
### leaveRoom  

Leave the room.

The user calls this API to leave the room, end the call process, and release all call\-related resources.


* **Type**

   ```ts
   (waitAck?: boolean) => Promise<void>
   ```
   

* **Notes**

   * After visible users leave the room, other users in the room will receive [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-104479#onuserleave) callback notification.

   * You must call this API to end the call, after calling the [joinRoom](https://docs.byteplus.com/en/docs/12/14190#joinroom) method to join the room. Otherwise you cannot start the next call. Repeatedly call this method have no negative impact.

* **Parameters**

   * **waitAck**

      Type: `boolean | undefined`

      Reserved parameter, no actual significance.

* **Return Value**

   Type: `Promise<void>`


<span id="publishstream"></span>
### publishStream  

Publishes media streams captured by camera/microphone in the current room.


* **Type**

   ```ts
   (mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   * An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14190#setuservisibility) to change your visibility in the room.

   * Call [publishScreen](https://docs.byteplus.com/en/docs/12/14190#publishscreen) to start screen sharing.

   * After you call this API, the other users in the room will receive [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishstream).

   * Call [unpublishStream](https://docs.byteplus.com/en/docs/12/14190#unpublishstream) to stop publishing streams.

* **Parameters**

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to publish audio stream or video stream.

* **Return Value**

   Type: `Promise<void>`

   * `NO_PUBLISH_PERMISSION`: No permission to publish streams. Please call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14190#setuservisibility) to switch the user to be visible first.

   * `TOKEN_NO_PUBLISH_PERMISSION`: The Token has no publishing permission or the publishing permission has expired, call [updateToken](https://docs.byteplus.com/en/docs/12/14190#updatetoken) to update the Token's publishing permission.

   * `PUBLISH_FAILED`: Failed to publish a stream. Please check the returned message for the specific reason.


<span id="unpublishstream"></span>
### unpublishStream  

Stops publishing media streams captured by camera/microphone in the current room.


* **Type**

   ```ts
   (mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   * After calling [publishStream](https://docs.byteplus.com/en/docs/12/14190#publishstream), call this API to stop publishing streams.

   * After calling this API, the other users in the room will receive [onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserunpublishstream).

* **Parameters**

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to stop publishing audio stream or video stream.

* **Return Value**

   Type: `Promise<void>`


<span id="publishscreen"></span>
### publishScreen  

Publishes local screen sharing streams in the current room.


* **Type**

   ```ts
   (mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   * An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14190#setuservisibility) to change your visibility in the room.

   * After you called this API, the other users in the room will receive [onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishscreen).

   * Call [unpublishScreen](https://docs.byteplus.com/en/docs/12/14190#unpublishscreen) to stop publishing screen sharing streams.

* **Parameters**

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to publish audio stream or video stream.

* **Return Value**

   Type: `Promise<void>`

   * `NO_PUBLISH_PERMISSION`: No permission to publish streams. Please call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14190#setuservisibility) to switch the user to be visible first.

   * `TOKEN_NO_PUBLISH_PERMISSION`: The Token has no publishing permission or the publishing permission has expired, call [updateToken](https://docs.byteplus.com/en/docs/12/14190#updatetoken) to update the Token's publishing permission.

   * `PUBLISH_FAILED`: Failed to publish a stream. Please check the returned message for the specific reason.


<span id="unpublishscreen"></span>
### unpublishScreen  

Stops publishing local screen sharing streams in the current room.


* **Type**

   ```ts
   (mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   * After calling [publishScreen](https://docs.byteplus.com/en/docs/12/14190#publishscreen), call this API to stop publishing streams.

   * After calling this API, the other users in the room will receive [onUserUnpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserunpublishscreen).

* **Parameters**

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to stop publishing audio stream or video stream.

* **Return Value**

   Type: `Promise<void>`


<span id="subscribestream"></span>
### subscribeStream  

Subscribes to specific remote media streams captured by camera/microphone.

You can call this API in both automatic subscription mode and manual subscription mode.


* **Type**

   ```ts
   (userId: string, mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   You must first get the remote stream information through [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishstream) before calling this API to subscribe to streams accordingly.

* **Parameters**

   * **userId**

      Type: `string`

      The ID of the remote user who published the target audio/video stream.

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to subscribe to the audio stream or the video stream.

* **Return Value**

   Type: `Promise<void>`

   * `STREAM_NOT_EXIST`: The target stream does not exist. Please enter the correct ID or make sure that the target stream is in the room.

   * `TOKEN_NO_SUBSCRIBE_PERMISSION`: The Token has no subscription permission or the subscription permission has expired, call [updateToken](https://docs.byteplus.com/en/docs/12/14190#updatetoken) to update the Token's subscription permission.


<span id="unsubscribestream"></span>
### unsubscribeStream  

Unsubscribes from specific remote media streams captured by camera/microphone.

You can call this API in both automatic subscription mode and manual subscription mode.


* **Type**

   ```ts
   (userId: string, mediaType: MediaType) => Promise<void>
   ```
   

* **Parameters**

   * **userId**

      Type: `string`

      The ID of the remote user who published the target audio/video stream.

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to unsubscribe from the audio stream or the video stream.

* **Return Value**

   Type: `Promise<void>`

   `STREAM_NOT_EXIST`: The target stream does not exist. Please enter the correct ID or make sure that the target stream is in the room.


<span id="subscribescreen"></span>
### subscribeScreen  

Subscribes to a specific screen sharing media stream.

You can call this API in both automatic subscription mode and manual subscription mode.


* **Type**

   ```ts
   (userId: string, mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   You must first get the remote stream information through [onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishscreen) before calling this API to subscribe to streams accordingly.

* **Parameters**

   * **userId**

      Type: `string`

      The ID of the remote user who published the target screen audio/video stream.

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to subscribe to the audio stream or the video stream.

* **Return Value**

   Type: `Promise<void>`

   * `STREAM_NOT_EXIST`: The target stream does not exist. Please enter the correct ID or make sure that the target stream is in the room.

   * `TOKEN_NO_SUBSCRIBE_PERMISSION`: The Token has no subscription permission or the subscription permission has expired, call [updateToken](https://docs.byteplus.com/en/docs/12/14190#updatetoken) to update the Token's subscription permission.


<span id="unsubscribescreen"></span>
### unsubscribeScreen  

Unsubscribes from specific screen sharing media stream.

You can call this API in both automatic subscription mode and manual subscription mode.


* **Type**

   ```ts
   (userId: string, mediaType: MediaType) => Promise<void>
   ```
   

* **Parameters**

   * **userId**

      Type: `string`

      The ID of the remote user who published the target screen audio/video stream.

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type, used for specifying whether to unsubscribe from the audio stream or the video stream.

* **Return Value**

   Type: `Promise<void>`


<span id="updatetoken"></span>
### updateToken  

Update Token.

You will receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#ontokenwillexpire) 30 s before the Token expires. Call this API to submit a new Token.


* **Type**

   ```ts
   (token: string) => Promise<void>
   ```
   

* **Notes**

   * If you call [joinRoom](https://docs.byteplus.com/en/docs/12/14190#joinroom) with an expired token, the joining will fail with an error code `INVALID_TOKEN`. And you need to obtain a valid token and call this API to update the token.

   * If joining a room failed because the token expired, call this API with an updated token. And then RTC SDK will automatically rejoin the room without calling [joinRoom](https://docs.byteplus.com/en/docs/12/14190#joinroom) again.

   * The user will be removed from the room when the Token expires.

* **Parameters**

   * **token**

      Type: `string`

      A valid token.

* **Return Value**

   Type: `Promise<void>`

   * `UPDATE_TOKEN_WITH_INVALID_TOKEN`: Invalid Token.

   * `UPDATE_TOKEN_BEFORE_JOIN`: The user has not joined a room yet. Please make sure the user is already in the room.


<span id="setaudiocapturedevice"></span>
### setAudioCaptureDevice  

Switch the microphone used for internal audio capturing.


* **Type**

   ```ts
   (deviceId: string) => Promise<void>
   ```
   

* **Notes**

   If the internal audio capturing is on, the switch is effective once you call this API. If the internal audio capturing is off, the setting will be effective when capture starts.

* **Parameters**

   * **deviceId**

      Type: `string`

      Device ID. Call [enumerateDevices](https://docs.byteplus.com/en/docs/12/14190#enumeratedevices) to get the device list.

* **Return Value**

   Type: `Promise<void>`


<span id="setvideocapturedevice"></span>
### setVideoCaptureDevice  

Switch the camera used for internal video capturing.


* **Type**

   ```ts
   (deviceId: string) => Promise<void>
   ```
   

* **Notes**

   * If the internal video capturing is on, the switch is effective once you call this API. If the internal video capturing is off, the setting will be effective when capture starts.

   * For mobile devices, set deviceId as `"user"` to use the front camera. Set deviceId as `"environment"` to use the rear camera.

   * The default camera is set by the browser.

* **Parameters**

   * **deviceId**

      Type: `string`

      Device ID. Call [enumerateDevices](https://docs.byteplus.com/en/docs/12/14190#enumeratedevices) to get the device list.

* **Return Value**

   Type: `Promise<void>`


<span id="startvideocapture"></span>
### startVideoCapture  

Enable internal video capture. The default state is off.

Internal video capture refers to: capturing video using the built\-in module.

The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartvideocapture) after the publisher starts video capture by calling this API.


* **Type**

   ```ts
   (deviceId?: string) => Promise<MediaTrackSettings>
   ```
   

* **Notes**

   * Call [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14190#stopvideocapture) to stop the internal video capture. Otherwise, the internal video capture will sustain until you destroy the engine instance.

   * Once you create the engine instance, you can start internal video capture regardless of the video publishing state. The video stream will start publishing only after the video capture starts.

   * Call [setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/14190#setvideocapturedevice) to switch the camera used by the internal video capture module.

* **Parameters**

   * **deviceId**

      Type: `string | undefined`

      ID of the capture device which you need to pass in to avoid exceptions such as no screen or a screen that is not the desired one. You can call [enumerateDevices](https://docs.byteplus.com/en/docs/12/14190#enumeratedevices) to obtain the list of devices.

* **Return Value**

   Type: `Promise<MediaTrackSettings>`

   The actual effective video capture parameters. See [MediaTrackSettings](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackSettings). Pay attention to the properties: `frameRate`, `height`, and `width`.

   The following error codes may be returned.

   * `REPEAT_CAPTURE`: Capture has already started.

   * `GET_VIDEO_TRACK_FAILED`: Capture failed. Please check if there are available capture devices or if they are being used by other apps.

   * `STREAM_TYPE_NOT_MATCH`: Wrong stream type. Triggered when you call internal capture APIs after switching to the custom stream source with setVideoSourceType.


<span id="stopvideocapture"></span>
### stopVideoCapture  

Stop internal video capture immediately.

Internal video capture refers to: capturing video using the built\-in module.

The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstopvideocapture) after the publisher stops video capture by calling this API.


* **Type**

   ```ts
   () => Promise<void>
   ```
   

* **Notes**

   * Call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14190#startvideocapture) to enable the internal video capture.

   * Without calling this API the internal video capture will sustain until you destroy the engine instance.

* **Return Value**

   Type: `Promise<void>`

   `STREAM_TYPE_NOT_MATCH`: Wrong stream type. Triggered when you call internal capture APIs after switching to the custom stream source with setVideoSourceType.


<span id="startaudiocapture"></span>
### startAudioCapture  

Start internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartaudiocapture) after the publisher starts audio capture by calling this API.


* **Type**

   ```ts
   (deviceId?: string) => Promise<MediaTrackSettings>
   ```
   

* **Notes**

   * Call [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14190#stopaudiocapture) to stop the internal audio capture. Otherwise, the internal audio capture will sustain until you destroy the engine instance.

   * Once you create the engine instance, you can start internal audio capture regardless of the audio publishing state. The audio stream will start publishing only after the audio capture starts.

* **Parameters**

   * **deviceId**

      Type: `string | undefined`

      ID of the capture device which you need to pass in to avoid exceptions such as no sound. You can call [enumerateDevices](https://docs.byteplus.com/en/docs/12/14190#enumeratedevices) to obtain the list of devices.

* **Return Value**

   Type: `Promise<MediaTrackSettings>`

   The actual effective audio capture parameters. See [MediaTrackSettings](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackSettings).

   The following error codes may be returned.

   * `REPEAT_CAPTURE`: Capture has already started.

   * `GET_AUDIO_TRACK_FAILED`: Capture failed. Please check if there are available capture devices or if they are being used by other apps.

   * `STREAM_TYPE_NOT_MATCH`: Wrong stream type. Triggered when you call internal capture APIs after switching to the custom stream source with setAudioSourceType.


<span id="stopaudiocapture"></span>
### stopAudioCapture  

Stop internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstopaudiocapture) after stopping audio capture by calling this API.


* **Type**

   ```ts
   () => Promise<void>
   ```
   

* **Notes**

   * Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14190#startaudiocapture) to enable the internal audio capture.

   * Without calling this API the internal audio capture will sustain until you destroy the engine instance.

* **Return Value**

   Type: `Promise<void>`

   `STREAM_TYPE_NOT_MATCH`: Wrong stream type. Triggered when you call internal capture APIs after switching to the custom stream source with setAudioSourceType.


<span id="startaudioandvideocapture"></span>
### startAudioAndVideoCapture  

Enable audio and video capture using the internal capture module. When calling this method, the browser will request microphone and camera permissions simultaneously, and the user only needs to grant permission once.

When calling this method, other users in the room will receive the callback of [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartvideocapture) and [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartaudiocapture).


* **Type**

   ```ts
   (optionsOrAudioDeviceId?: { audioDeviceId?: string; videoDeviceId?: string;} | string, videoDeviceId?: string) => Promise<{ audioTrackSettings: MediaTrackSettings; videoTrackSettings: MediaTrackSettings;}>
   ```
   

* **Notes**

   * The audio and video capture can be published using [publishStream](https://docs.byteplus.com/en/docs/12/14190#publishstream) and unpublished using [unPublishStream](https://docs.byteplus.com/en/docs/12/14190#unpublishstream).

   * The method cannot be called simultaneously with [startVideoCapture](https://docs.byteplus.com/en/docs/12/14190#startvideocapture) / [startAudioCapture](https://docs.byteplus.com/en/docs/12/14190#startaudiocapture).

   * If either the camera or the microphone fails to complete the capture when calling this method, the audio and video capture will fail.

   * To stop audio and video capture, call [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14190#stopvideocapture) / [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14190#stopaudiocapture).

* **Parameters**

   * **optionsOrAudioDeviceId**

      Type: `string | { audioDeviceId?: string | undefined; videoDeviceId?: string | undefined; } | undefined`

      When using a single parameter, both audio and video device IDs can be set simultaneously. When using two parameters, the audio device's ID can be set.

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |audioDeviceId |`string \| undefined` |Audio device's ID. |
         |videoDeviceId |`string \| undefined` |Video device's ID. |
         

   * **videoDeviceId**

      Type: `string | undefined`

      Video device's ID.

* **Return Value**

   Type: `Promise<{ audioTrackSettings: MediaTrackSettings; videoTrackSettings: MediaTrackSettings }>`

   The actual audio and video capture parameters that take effect. Refer to [MediaTrackSettings](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackSettings). Pay attention to the properties: `deviceId`, `channelCount`, `sampleRate`, `frameRate`, `height` and `width`.

   The following error codes may be returned.

   * `REPEAT_CAPTURE`: Capture has already started.

   * `GET_AUDIO_TRACK_FAILED`: Audio capture failed. Please check if there are available capture devices or if they are being used by other apps.

   * `GET_VIDEO_TRACK_FAILED`: Video capture failed. Please check if there are available capture devices or if they are being used by other apps.

   * `STREAM_TYPE_NOT_MATCH`: Wrong stream type. Triggered when you call internal capture APIs after switching to the custom stream source with setAudioSourceType or setVideoSourceType.


<span id="startscreencapture"></span>
### startScreenCapture  

Use the capture module provided by the RTC SDK to capture the current screen stream for sharing.


* **Type**

   ```ts
   (screenConfig?: ScreenConfig) => Promise<void>
   ```
   

* **Notes**

   * Call this API will start screen stream video capture but will not publish the captured video. Publishing a screen\-sharing stream by calling [publishScreen](https://docs.byteplus.com/en/docs/12/14190#publishscreen).

   * To turn off screen video source capture, call [stopScreenCapture](https://docs.byteplus.com/en/docs/12/14190#stopscreencapture).

   * Before calling this API, you can call [setScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/14190#setscreenencoderconfig) to set the capture frame rate and encoding resolution of the screen video stream.

* **Parameters**

   * **screenConfig**

      Type: [ScreenConfig](https://docs.byteplus.com/en/docs/12/docs-104481#screenconfig)` | undefined`

      Specify properties for the sharing screen.

* **Return Value**

   Type: `Promise<void>`

   `GET_SCREEN_TRACK_FAILED`: Capture failed.


<span id="stopscreencapture"></span>
### stopScreenCapture  

Stop screen sharing.


* **Type**

   ```ts
   () => Promise<void>
   ```
   

* **Return Value**

   Type: `Promise<void>`


<span id="setlocalvideoplayer"></span>
### setLocalVideoPlayer  

Add the local media stream to a player and set the rendering mode for the rendering of the local stream.

Listen to `onPlayerEvent` for the state after binding a view to the local video stream.

Call this API again with a blank view to remove the stream from the player. Doing this without a playerId while there are multiple players including a default player will remove the stream from the default player.


* **Type**

   ```ts
   (streamIndex: StreamIndex, videoPlayerOption?: Partial<Omit<VideoPlayerOption, 'rotation'>>) => HTMLVideoElement | undefined
   ```
   

* **Notes**

   * You should bind the view after the user joins a room. This setting will sustain when the user leaves the room.

   * If the stream has already been added to the specific player, repeated calls will not create duplicate players.

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Video stream properties

   * **videoPlayerOption**

      Type: `Partial<Omit<`[VideoPlayerOption](https://docs.byteplus.com/en/docs/12/docs-104481#videoplayeroption)`, "rotation">> | undefined`

      View information and rendering mode. Call this API repeatedly with different playerId to add the stream to different players.

* **Return Value**

   Type: `HTMLVideoElement | undefined`


<span id="setremotevideoplayer"></span>
### setRemoteVideoPlayer  

Add the remote media stream to a player and set the rendering mode for the rendering of the remote stream.

It is recommended to call this API and bind a view once the event of [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishstream)/[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishscreen) is triggered.

Call this API again with a blank view to remove the stream from the player. Doing this without a playerId while there are multiple players including a default player will remove the stream from the default player.


* **Type**

   ```ts
   (streamIndex: StreamIndex, videoPlayerOption: VideoPlayerOption) => HTMLVideoElement | undefined
   ```
   

* **Notes**

   You should bind the view after the user joins a room. This setting will sustain until the user leaves the room.

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Video stream properties.

   * **videoPlayerOption**

      Type: [VideoPlayerOption](https://docs.byteplus.com/en/docs/12/docs-104481#videoplayeroption)

      View information and rendering mode. Since V4.61, call this API repeatedly with different playerIds to add the stream to different players.

      Since V4.56, you can set the rotation of the stream via the `rotation` property.

* **Return Value**

   Type: `HTMLVideoElement | undefined`


<span id="setlocalvideomirrortype"></span>
### setLocalVideoMirrorType  

Enable or disable the mirror mode for the local video stream.


* **Type**

   ```ts
   (mirrorType: MirrorType) => void
   ```
   

* **Parameters**

   * **mirrorType**

      Type: [MirrorType](https://docs.byteplus.com/en/docs/12/docs-104481#mirrortype)

      Whether to turn on mirror mode.


<span id="setremotevideomirrortype"></span>
### setRemoteVideoMirrorType  

When using internal rendering, enable mirroring for the remote stream.


* **Type**

   ```ts
   (userId: string, streamIndex: StreamIndex, mirrorType: MirrorType) => void
   ```
   

* **Notes**

   * In addition, you must also call [setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setremotevideoplayer) to mirror the remote stream in the specified player.

* **Parameters**

   * **userId**

      Type: `string`

      ID of the remote user

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Mainstream or screen\-sharing stream.

   * **mirrorType**

      Type: [MirrorType](https://docs.byteplus.com/en/docs/12/docs-104481#mirrortype)

      The mirror type for the remote stream.


<span id="setaudioplaybackdevice"></span>
### setAudioPlaybackDevice  

Sets the speaker or the earpiece as the audio playback device. The audio playback device defaults to the speaker.


* **Type**

   ```ts
   (deviceId: string) => Promise<void>
   ```
   

* **Notes**

   * This method is available on Chrome.

   * You can call this API before or after the user joins a room.

* **Parameters**

   * **deviceId**

      Type: `string`

      ID of the audio playback device. Call [enumerateDevices](https://docs.byteplus.com/en/docs/12/14190#enumeratedevices) to get device ID.

* **Return Value**

   Type: `Promise<void>`

   * `INVALID_DEVICE_ID`: Invalid device ID.

   * `NOT_SUPPORTED`: The browser does not support audio device test or audio capture.


<span id="play"></span>
### play  

Play audio and video stream manually.

Call this API when the user needs to take part in the audio and video interaction after calling [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine) and setting autoPlay to false.


* **Type**

   ```ts
   (userId?: string, mediaType?: MediaType, streamIndex?: StreamIndex, playerId?: string) => Promise<void>
   ```
   

* **Parameters**

   * **userId**

      Type: `string | undefined`

      The user ID or the WTN stream ID. The empty value indicates the local stream. When you specify a WTN stream ID, the `mediaType` or `streamIndex` will not take effect.

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)` | undefined`

      For audio or video. It defaults to `AUDIO_AND_VIDEO`. The local audio is not included. While the Audio selection is enabled, it can only be set to `VIDEO`.

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)` | undefined`

      Main stream or screen\-sharing stream. By default, the action will apply to both the main stream and the screen\-sharing stream.

   * **playerId**

      Type: `string | undefined`

      Player ID. An empty value indicates the default player.

* **Return Value**

   Type: `Promise<void>`

   Calling this API when the audio and video are playing will also return a Promise.


<span id="stop"></span>
### stop  

Pause the specified media stream.


* **Type**

   ```ts
   (userId?: string, mediaType?: MediaType, streamIndex?: StreamIndex, playerId?: string) => void
   ```
   

* **Notes**

   When the audio selection is enabled, this method will not take effect.

   After using this method to pause the media stream,

   * The billing duration will not stop counting since the subscription does not cancel.

   * The stream will not remove from the player. You can call [play](https://docs.byteplus.com/en/docs/12/14190#play) to resume the stream.

   * The volume of the stream will not be `0`, which you can obtain via the callback of [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport) or [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onremoteaudiopropertiesreport).

* **Parameters**

   * **userId**

      Type: `string | undefined`

      The user ID or the WTN stream ID. The empty value indicates the local stream. When you specify a WTN stream ID, the `mediaType` or `streamIndex` will not take effect.

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)` | undefined`

      For audio or video. It defaults to `AUDIO_AND_VIDEO`. The local audio is not included. While the Audio selection is enabled, it can only be set to `VIDEO`.

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)` | undefined`

      Main stream or screen\-sharing stream. By default, the action will apply to both the main stream and the screen\-sharing stream.

   * **playerId**

      Type: `string | undefined`

      Player ID. An empty value indicates the default player.


<span id="getaudiovolume"></span>
### getAudioVolume  

Gets the volume of the remote audio stream or the local audio stream captured by the local microphone and screen audio stream.


* **Type**

   ```ts
   (streamIndex: StreamIndex, userId?: string) => { linearVolume: number; nonlinearVolume: number;}
   ```
   

* **Notes**

   * The interval for repeatedly calling this method should be at least 100 milliseconds.

   * You can also get the audio volume via [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport) and [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onremoteaudiopropertiesreport).

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Main stream or screen\-sharing stream

   * **userId**

      Type: `string | undefined`

      The user ID. The empty value indicates the local stream.

* **Return Value**

   Type: `{ linearVolume: number; nonlinearVolume: number; }`

   If the specified stream does not exist, the volume values are `0`.

   * linear volume. The value is in linear relation to the original volume. The higher the value, the higher the volume. The range is [0,255].

&nbsp;

      * [0, 25]: Nearly silent

      * [26, 75]: Low volume

      * [76, 204]: Medium volume

      * [205, 255]: High volume

   * non\-linear volume in dB. The value is in proportion to the log value of the original volume. You can use the value to recognize the Active Speaker in the room. The range is [\-127, 0].

      * [\-127, \-60]: Nearly silent

      * [\-59, \-40]: Low volume

      * [\-39, \-20]: Medium volume

      * [\-19, 0]: High volume


<span id="setaudioframecallback"></span>
### setAudioFrameCallback  

Toggle the callbacks carrying the audio frames.


* **Type**

   ```ts
   (streamIndex: StreamIndex, userId?: string, callback?: ((data: AudioFrameData) => void) | undefined, frameSize?: number) => void
   ```
   

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Audio from microphone or device audio.

   * **userId**

      Type: `string | undefined`

      ID of the remote user who published the audio. An empty value indicates the local audio.

      When the Audio selection enabled, only the local audio frames are available.

      You will get the callback carrying the audio data as soon as the user starts publish audio.

   * **callback**

      Type: `((data: `[AudioFrameData](https://docs.byteplus.com/en/docs/12/docs-104481#audioframedata)`) => void) | undefined`

      The callback function to receive the audio frames. An empty value indicates disabling the callback.

      When the user disconnects, the audio data is zero amplitude.

   * **frameSize**

      Type: `number | undefined`

      The number of samples per frame. The interval between callbacks increases as the frameSize gets larger.

      It can be set to 256, 512, 1024, 2048, 4096, 8192, or 16384. It defaults to 4096. We recommend using the default value unless the application where the audio frames to be used requires a specific size.


<span id="pauseallsubscribedstream"></span>
### pauseAllSubscribedStream  

Pause receiving remote media streams.


* **Type**

   ```ts
   (mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   * Calling this API does not change the capture state and the transmission state of the remote clients.

   * Calling this API does not cancel the subscription or change any subscription configuration.

   * To resume, call [resumeAllSubscribedStream](https://docs.byteplus.com/en/docs/12/14190#resumeallsubscribedstream).

* **Parameters**

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type subscribed to.

* **Return Value**

   Type: `Promise<void>`


<span id="resumeallsubscribedstream"></span>
### resumeAllSubscribedStream  

Resume receiving remote media streams


* **Type**

   ```ts
   (mediaType: MediaType) => Promise<void>
   ```
   

* **Notes**

   * Calling this API does not change the capture state and the transmission state of the remote clients.

   * Calling this API does not change any subscription configuration.

* **Parameters**

   * **mediaType**

      Type: [MediaType](https://docs.byteplus.com/en/docs/12/docs-104481#mediatype)

      Media stream type

* **Return Value**

   Type: `Promise<void>`


<span id="sendusermessage"></span>
### sendUserMessage  

Send point\-to\-point text messages to a specified user in the room.

The recipient receives the message via [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onusermessagereceived) once the message is sent successfully.


* **Type**

   ```ts
   (userId: string, message: string) => Promise<unknown> | undefined
   ```
   

* **Notes**

   Call [joinRoom](https://docs.byteplus.com/en/docs/12/14190#joinroom) to join the room before calling this API.

* **Parameters**

   * **userId**

      Type: `string`

      User ID of the recipient

   * **message**

      Type: `string`

      Text message content. The default size limit for a single message is 1 KB. To send a larger message (up to 64 KB), you must [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). If you enable Advanced RTS functions while the SDK is running, re\-initialize the engine for the configuration to take effect.

* **Return Value**

   Type: `Promise<unknown> | undefined`

   * `USER_MESSAGE_TIMEOUT`: P2P message failed to be sent due to a timeout.

   * `USER_MESSAGE_BROKEN`: P2P message failed to be sent due to a broken channel.

   * `USER_MESSAGE_NO_RECEIVER`: No receiver. Please make sure you pass in the right userId.

   * `USER_MESSAGE_NOT_JOIN`: The sender has not joined any room.

   * `USER_MESSAGE_UNKNOWN`: Unknown error.


<span id="senduserbinarymessage"></span>
### sendUserBinaryMessage  

Send point\-to\-point binary messages to a specified user in the room.

The recipient receives the message via [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onuserbinarymessagereceived) once the message is sent successfully.


* **Type**

   ```ts
   (userId: string, message: ArrayBuffer) => Promise<unknown>
   ```
   

* **Notes**

   Call [joinRoom](https://docs.byteplus.com/en/docs/12/14190#joinroom) to join the room before calling this API.

* **Parameters**

   * **userId**

      Type: `string`

      User ID of the recipient

   * **message**

      Type: `ArrayBuffer`

      Binary message content. The default size limit for a single message is 1 KB. To send a larger message (up to 64 KB), you must [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). If you enable Advanced RTS functions while the SDK is running, re\-initialize the engine for the configuration to take effect.

* **Return Value**

   Type: `Promise<unknown>`

   * `USER_MESSAGE_TIMEOUT`: P2P message failed to be sent due to a timeout.

   * `USER_MESSAGE_BROKEN`: P2P message failed to be sent due to a broken channel.

   * `USER_MESSAGE_NO_RECEIVER`: No receiver. Please make sure you pass in the right userId.

   * `USER_MESSAGE_NOT_JOIN`: The sender has not joined any room.

   * `USER_MESSAGE_UNKNOWN`: Unknown error.


<span id="sendroommessage"></span>
### sendRoomMessage  

Send text messages to all other users in the room.

Users in the room will receive the message via [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onroommessagereceived) once the message is sent successfully.


* **Type**

   ```ts
   (message: string) => Promise<any> | undefined
   ```
   

* **Parameters**

   * **message**

      Type: `string`

      Text message content. The default size limit for a single message is 1 KB. To send a larger message (up to 64 KB), you must [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). If you enable Advanced RTS functions while the SDK is running, re\-initialize the engine for the configuration to take effect.

* **Return Value**

   Type: `Promise<any> | undefined`


<span id="sendroombinarymessage"></span>
### sendRoomBinaryMessage  

Send binary messages to all other users in the room.

Users in the room will receive binary message via [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onroombinarymessagereceived) once the message is sent successfully.


* **Type**

   ```ts
   (message: ArrayBuffer) => Promise<any> | undefined
   ```
   

* **Parameters**

   * **message**

      Type: `ArrayBuffer`

      Binary message content. The default size limit for a single message is 1 KB. To send a larger message (up to 64 KB), you must [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). If you enable Advanced RTS functions while the SDK is running, re\-initialize the engine for the configuration to take effect.

* **Return Value**

   Type: `Promise<any> | undefined`


<span id="sendseimessage"></span>
### sendSEIMessage  

Send supplemental enhancement information (SEI) through video frames.

In the video call scenario, the SEI data will be sent with the video frames. In the voice call scenario, the SDK will generate a 16px × 16px black frame video stream to send the data.


* **Type**

   ```ts
   (streamIndex: StreamIndex, message: Uint8Array | string, repeatCount: number) => void
   ```
   

* **Notes**

   * **Compatibility**

&nbsp;

      * SEI messages are only supported with H.264 encoding and are available only in browsers with Chromium 86+, Firefox 117+, or Safari 15.4+.

      * Android devices do not support sending SEI data in voice call scenarios.

      * SEI messages cannot be used on iOS devices.

   * In voice call scenarios, you still need to publish and subscribe to video streams, instead of audio streams. The subscriber can enable automatic subscribing to video streams when entering the room, or call [subscribeStream](https://docs.byteplus.com/en/docs/12/14190#subscribestream) with the media stream type `AUDIO_AND_VIDEO`.

   * In voice call scenarios, if no SEI data is sent within 1 minute after calling this interface, the SDK will automatically cancel the publication of the black frame video stream.

   * After the message is sent successfully, the remote end will receive [onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onseimessagereceived).

   * In voice call scenarios, the sending status of the black frame video stream will be notified to remote users through the [onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/docs-104479#onseistreamupdate) event.

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Specify the type of media stream carrying SEI information. In the voice call scenario, it is recommended to set this value to `STREAM_INDEX_MAIN`.

   * **message**

      Type: `string | Uint8Array`

      SEI message within 4 KB.

      Empty message or message exceeding this size will not be sent with respective error prompt.

      The SEI PayLoadType must be `5` or `100`.

   * **repeatCount**

      Type: `number`

      Number of times a message is sent repeatedly. The SEI will be added to a consecutive `repeatCount+1` number of video frames starting from the current frame. The value range is `[0, min{30, %{video frame rate}×2}]`, and the recommended range is `[2,4]`.


<span id="setvideoencoderconfig"></span>
### setVideoEncoderConfig  

Configures the encoding settings for the camera videos on the publisher side.


* **Type**

   ```ts
   (descriptions: VideoEncoderConfig | VideoEncoderConfig[]) => Promise<void>
   ```
   

* **Notes**

   * To publish Simulcast streams, enable and configure the Simulcast streams through [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setlocalsimulcastmode). When Simulcasting is enabled, calling this method configures the high\-quality stream.

   * Before calling this method, the SDK defaults to publishing a stream with a resolution of 640 × 480 pixels, a frame rate of 15 FPS, and a maximum encoding bitrate of 600 Kbps.

   * You can call this method before or after publishing the video stream.

   * When using a mobile device to publish a video stream in portrait mode, the set resolution width and height are reversed in the actual streaming parameters. For example, when setting the sending resolution to 640 × 480 pixels, the actual streaming parameters are 480 × 640 pixels.

   * If the set parameters are not supported by the browser, the RTC SDK will capture and encode based on the parameter range supported by the browser, and notify the actual parameters through the [onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalvideosizechanged) callback.

   * This method is applicable to video streams captured by the camera. For setting the screen sharing stream parameters, refer to [setScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/14190#setscreenencoderconfig).

* **Parameters**

   * **descriptions**

      Type: [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104481#videoencoderconfig)` | `[VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104481#videoencoderconfig)`[]`

      The configurations of the video streams to be published.

* **Return Value**

   Type: `Promise<void>`


<span id="setscreenencoderconfig"></span>
### setScreenEncoderConfig  

Set the encoding configuration of the screen\-sharing stream, which is also applied in video capture.

If the configuration is not supported by your browser, the video will be captured based on the supported configuration. You will also receive the callback [onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalvideosizechanged).


* **Type**

   ```ts
   (description: ScreenEncoderConfig) => Promise<void>
   ```
   

* **Notes**

   * The default parameters are 1920 × 1080 px, 15 FPS, with 3000 Kbps max bitrate.

   * We recommend that you set the encoding configuration before video capture. Otherwise, the video will be captured based on the default configuration.

* **Parameters**

   * **description**

      Type: [ScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104481#screenencoderconfig)

      The encoding configuration of the screen\-sharing stream.

* **Return Value**

   Type: `Promise<void>`


<span id="setremotesimulcaststreamtype"></span>
### setRemoteSimulcastStreamType  

Sets your expected quality level of the remote video stream that you want to subscribe to or have subscribed to.


* **Type**

   ```ts
   (userId: string, streamType: SimulcastStreamType) => Promise<void>
   ```
   

* **Notes**

   * This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14190#setlocalsimulcastmode) to enable publishing multiple video streams, in which case the subscriber will receive a stream that is closest to the set configuration.

   * If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive the highest\-quality video stream by default.

   * You can call this method before or after joining a room.

   * Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1359024) for more information.

* **Parameters**

   * **userId**

      Type: `string`

      ID of the remote video stream publisher you expect to configure subscription parameters for.

      When the specified Simulcast stream is not published, the SDK will automatically subscribe to the next lower quality stream.

   * **streamType**

      Type: [SimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-104481#simulcaststreamtype)

      The preference for the quality of the subscribed stream.

* **Return Value**

   Type: `Promise<void>`

   Refer to [MIXING_OLD_AND_NEW_APIS](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode) for the details of the error code.


<span id="setlocalsimulcastmode"></span>
### setLocalSimulcastMode  

Enables the Simulcast feature and configures the lower\-quality camera videos for the stream publisher.


* **Type**

   ```ts
   (mode: VideoSimulcastMode, streamConfig?: VideoEncoderConfig[]) => Promise<void>
   ```
   

* **Parameters**

   * **mode**

      Type: [VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104481#videosimulcastmode)

      Whether to publish lower\-quality streams and how many of them to be published. By default, it is set to Single, where the publisher sends the video in a single profile.

      This parameter must be set before joining a room.

   * **streamConfig**

      Type: [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104481#videoencoderconfig)`[] | undefined`

      The specification of the lower quality stream(s).

      The resolution of the lower quality stream must be smaller than the standard stream set via [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setvideoencoderconfig). The specifications in the array must be arranged in ascending order based on resolution.

      You can configure the lower quality stream(s) before or after joining a room. However, after publishing the streams, you can no longer change the number of lower quality streams.

      When the Simulcast feature is enabled, the low\-quality stream is set to a default resolution of 120px × 90px

* **Return Value**

   Type: `Promise<void>`

   Refer to [SET_SIMULCAST_FAILED](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode) and [MIXING_OLD_AND_NEW_APIS](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode) for the details of the error code.


<span id="enableaudiopropertiesreport"></span>
### enableAudioPropertiesReport  

Enable audio information prompts.


* **Type**

   ```ts
   (config?: AudioPropertiesConfig) => void
   ```
   

* **Notes**

   With the prompt on, you can:

   * Get the information of the audio stream captured by the local microphone and screen audio stream through [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport).

   * Get the information of the subscribed remote audio streams through [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onremoteaudiopropertiesreport).

* **Parameters**

   * **config**

      Type: [AudioPropertiesConfig](https://docs.byteplus.com/en/docs/12/docs-104481#audiopropertiesconfig)` | undefined`

      Audio information prompts\-related configurations.


<span id="startlivetranscoding"></span>
### startLiveTranscoding  

Starts pushing media streams to CDN and sets the relevant configurations.


* **Type**

   ```ts
   (transcode: LiveTranscodeConfig) => Promise<void>
   ```
   

* **Notes**

   * After calling this API, you will receive events for pushing a mixed stream to CDN via [onStreamMixingEvent](https://docs.byteplus.com/en/docs/12/docs-104479#onstreammixingevent).

   * If you have subscribed to the push\-to\-CDN server callback in the [console](https://console.byteplus.com/rtc/cloudRTC?tab=callback), calling this API will receive a [TranscodeStarted](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodestarted) server callback notification. When calling this API repeatedly, subsequent calls to this API will trigger both [TranscodeStarted](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodestarted) and [TranscodeUpdated](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodeupdated) callbacks.

   * Call [stopLiveTranscoding](https://docs.byteplus.com/en/docs/12/14190#stoplivetranscoding) to stop pushing mixed streams to CDN.

* **Parameters**

   * **transcode**

      Type: [LiveTranscodeConfig](https://docs.byteplus.com/en/docs/12/docs-104481#livetranscodeconfig)

      Configurations to be set when pushing media streams to CDN.

* **Return Value**

   Type: `Promise<void>`


<span id="updatelivetranscoding"></span>
### updateLiveTranscoding  

Update configuration needed when pushing media streams to CDN.

After calling [startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#startlivetranscoding) to enable the function of pushing streams to CDN, you can call this API to update the relevant configurations.


* **Type**

   ```ts
   (transcode: Partial<LiveTranscodeConfig>) => Promise<void>
   ```
   

* **Parameters**

   * **transcode**

      Type: `Partial<`[LiveTranscodeConfig](https://docs.byteplus.com/en/docs/12/docs-104481#livetranscodeconfig)`>`

      Updated configurations. Some of the configurations cannot be updated. See [LiveTranscodeConfig](https://docs.byteplus.com/en/docs/12/docs-104481#livetranscodeconfig) for specific indications.

* **Return Value**

   Type: `Promise<void>`


<span id="stoplivetranscoding"></span>
### stopLiveTranscoding  

Stop pushing media streams to CDN

To start pushing media streams to CDN, refer to [startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#startlivetranscoding).


* **Type**

   ```ts
   () => Promise<void>
   ```
   

* **Return Value**

   Type: `Promise<void>`


<span id="setbusinessid"></span>
### setBusinessId  

Set the business ID.

You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication.


* **Type**

   ```ts
   (businessId: string) => boolean
   ```
   

* **Notes**

   You must call this API before the [joinRoom](https://docs.byteplus.com/en/docs/12/14190#joinroom) API, otherwise it will be invalid.

* **Parameters**

   * **businessId**

      Type: `string`

      Your customized businessId

      BusinessId is a tag, and you can customize its granularity.

* **Return Value**

   Type: `boolean`

   * `true`: Success.

   * `false`: Failure.


<span id="setuservisibility"></span>
### setUserVisibility  

Set user visibility. The local user is visible to others by default before calling this API.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capability](https://docs.byteplus.com/en/docs/12/docs-257549).


* **Type**

   ```ts
   (enable: boolean) => Promise<void>
   ```
   

* **Notes**

   * You can call this API whether the user is in a room or not.

   * When you call this API, the other users in the room will be informed via the related callback:

      * Switch from `false` to `true`: [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined)

      * Switch from `true` to `false`: [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-104479#onuserleave)

* **Parameters**

   * **enable**

      Type: `boolean`

      Visibility of the user in the room.

      * `true`: The user can publish media streams. And the other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.

      * `false`: The user cannot publish media streams. And the other users in the room do not get informed of the behaviors of the user, such as joining, starting video capture, or leaving.

* **Return Value**

   Type: `Promise<void>`


<span id="setexternalvideotrack"></span>
### setExternalVideoTrack  

Set a custom videoTrack as the video source.

Before calling this API, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setvideosourcetype) to enable custom video capture.


* **Type**

   ```ts
   (index: StreamIndex, track: MediaStreamTrack) => Promise<void>
   ```
   

* **Parameters**

   * **index**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      specify a stream index.

   * **track**

      Type: `MediaStreamTrack`

      specify a video track. See [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack).

* **Return Value**

   Type: `Promise<void>`


<span id="setexternalaudiotrack"></span>
### setExternalAudioTrack  

Set a custom audioTrack as the audio source.

Before calling this API, you must call [setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiosourcetype) to enable custom audio capture.


* **Type**

   ```ts
   (index: StreamIndex, track: MediaStreamTrack) => Promise<void>
   ```
   

* **Parameters**

   * **index**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      specify a stream index.

   * **track**

      Type: `MediaStreamTrack`

      specify an audio track. See [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack).

* **Return Value**

   Type: `Promise<void>`


<span id="setvideosourcetype"></span>
### setVideoSourceType  

Switch the source from the internal to custom video capture.

Internal video capture refers to using built\-in video capture video.


* **Type**

   ```ts
   (index: StreamIndex, videoSourceType: VideoSourceType) => Promise<void>
   ```
   

* **Parameters**

   * **index**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      audio stream index

   * **videoSourceType**

      Type: [VideoSourceType](https://docs.byteplus.com/en/docs/12/docs-104481#videosourcetype)

      Type of the module for video capture

* **Return Value**

   Type: `Promise<void>`


<span id="setaudiosourcetype"></span>
### setAudioSourceType  

Switch the source from the internal to custom audio capture.

Internal audio capture refers to using built\-in audio capture.


* **Type**

   ```ts
   (index: StreamIndex, audioSourceType: AudioSourceType) => Promise<void>
   ```
   

* **Parameters**

   * **index**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      audio stream index

   * **audioSourceType**

      Type: [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-104481#audiosourcetype)

      Type of the module for audio capture

* **Return Value**

   Type: `Promise<void>`


<span id="getaudiomixingmanager"></span>
### getAudioMixingManager  

Creates an audio mixing manager object.


* **Type**

   ```ts
   () => IAudioMixingManager
   ```
   

* **Return Value**

   Type: [IAudioMixingManager](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager)

   audio mixing manager object


<span id="getwtnstreammanager"></span>
### getWTNStreamManager  

Creates a WTN stream manager object.


* **Type**

   ```ts
   () => IWTNStream
   ```
   

* **Return Value**

   Type: [IWTNStream](https://docs.byteplus.com/en/docs/12/14190#wtnstream)

   WTN stream manager object


<span id="getcallid"></span>
### getCallId  

> Available since v4.66.


Get the call ID. Call this method after joining a room.

After creating a room, a `callId` is generated to identify the call for this room.


* **Type**

   ```ts
   () => string | undefined
   ```
   

* **Return Value**

   Type: `string | undefined`

   The call ID (`callId`) of the room.


<span id="setaudiocaptureconfig"></span>
### setAudioCaptureConfig  

Configure the internal audio capture. Different browsers have their own default settings.


* **Type**

   ```ts
   (config: TrackCaptureConfig) => Promise<void>
   ```
   

* **Notes**

   You should call this API before starting audio capture and publishing streams.

* **Parameters**

   * **config**

      Type: [TrackCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-104481#trackcaptureconfig)

      Configuration of the internal audio capture such as, disabling audio 3A processing. Refer to [MediaTrackConstraints](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints) for more details.

* **Return Value**

   Type: `Promise<void>`


<span id="login"></span>
### login  

Sign in to the RTM server.

Call this method before users within the same `appID` can communicate with each other via messages.


* **Type**

   ```ts
   (token: string | null, userId: string) => Promise<void>
   ```
   

* **Notes**

   * Call [logout](https://docs.byteplus.com/en/docs/12/14190#logout) to log out the IM server.

   * In the same App ID, the user ID of each user must be unique. The user will be logged out when a user with the same userID joins the room because of the error of `RTM_DUPLICATE_LOGIN`.

* **Parameters**

   * **token**

      Type: `string | null`

      Token for authentication.

      During testing, you can generate a temporary Token on [Console](https://console.byteplus.com/auth/login), and fill in any value with `roomId`.

      To officially go live, you need to implement token generation on your server. The `roomId` field should be empty string ("") . See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

   * **userId**

      Type: `string`

      User ID.

* **Return Value**

   Type: `Promise<void>`

   * `ALREADY_LOGIN`: The user has already logged in.

   * `LOGIN_FAILED`: Login failed. Please check the returned message for the specific reason.


<span id="logout"></span>
### logout  

Log out of the RTS service. After calling this API to logout you are not able to call APIs to send messages and server messages.


* **Type**

   ```ts
   () => Promise<void>
   ```
   

* **Return Value**

   Type: `Promise<void>`


<span id="updatelogintoken"></span>
### updateLoginToken  

Update the Token used to login. Since all tokens have a limited time\-to\-live, call this API to refresh the token.


* **Type**

   ```ts
   (token: string | null) => Promise<void>
   ```
   

* **Notes**

   * Call this API to refresh the token after the token has expired with no need for calling [login](https://docs.byteplus.com/en/docs/12/14190#login).

   * You will be informed of the expiration of the token if you tried to login with an expired token or during a reconnection. If the token expired after the user has signed in, no actions need to be taken.

* **Parameters**

   * **token**

      Type: `string | null`

      updated token

* **Return Value**

   Type: `Promise<void>`


<span id="getpeeronlinestatus"></span>
### getPeerOnlineStatus  

Get the status of a user before sending him/her a P2P message. You can also call this API to check the status of the current user.


* **Type**

   ```ts
   (userId: string) => Promise<USER_ONLINE_STATUS>
   ```
   

* **Notes**

   Call [login](https://docs.byteplus.com/en/docs/12/14190#login) before calling this API.

* **Parameters**

   * **userId**

      Type: `string`

      ID of the user whose status you intend to know

* **Return Value**

   Type: `Promise<`[USER_ONLINE_STATUS](https://docs.byteplus.com/en/docs/12/docs-104481#user_online_status)`>`


<span id="sendusermessageoutsideroom"></span>
### sendUserMessageOutsideRoom  

Send point\-to\-point (P2P) text message to a user.


* **Type**

   ```ts
   (userId: string, message: string) => Promise<any>
   ```
   

* **Notes**

   * Before calling this API, make sure you have [enabled Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console. If you enable this feature while the SDK is running, re\-initialize the engine for the configuration to take effect.

   * Call [login](https://docs.byteplus.com/en/docs/12/14190#login) before calling this API.

   * The recipient must be logged into the server and will receive the text message via [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-104479#onusermessagereceivedoutsideroom) if the message has been sent successfully.

* **Parameters**

   * **userId**

      Type: `string`

      ID of the recipient

   * **message**

      Type: `string`

      Text message within 64 KB.

* **Return Value**

   Type: `Promise<any>`

   * `USER_MESSAGE_TIMEOUT`: P2P message failed to be sent due to a timeout.

   * `USER_MESSAGE_BROKEN`: P2P message failed to be sent due to a broken channel.

   * `USER_MESSAGE_NO_RECEIVER`: No receiver. Please make sure you pass in the right userId.

   * `NOT_LOGIN`: The sender has not logged in yet.

   * `USER_MESSAGE_UNKNOWN`: Unknown error.


<span id="senduserbinarymessageoutsideroom"></span>
### sendUserBinaryMessageOutsideRoom  

Send point\-to\-point (P2P) binary message to a user.


* **Type**

   ```ts
   (userId: string, message: ArrayBuffer) => Promise<any>
   ```
   

* **Notes**

   * Before calling this API, make sure you have [enabled Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console. If you enable this feature while the SDK is running, re\-initialize the engine for the configuration to take effect.

   * Call [login](https://docs.byteplus.com/en/docs/12/14190#login) before calling this API.

   * The recipient must be logged into the server and will receive the text message via [EngineEventsTypes.onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-104479#onuserbinarymessagereceivedoutsideroom) if the message has been sent successfully.

* **Parameters**

   * **userId**

      Type: `string`

      ID of the recipient

   * **message**

      Type: `ArrayBuffer`

      Binary message within 64 KB

* **Return Value**

   Type: `Promise<any>`

   * `USER_MESSAGE_TIMEOUT`: P2P message failed to be sent due to a timeout.

   * `USER_MESSAGE_BROKEN`: P2P message failed to be sent due to a broken channel.

   * `USER_MESSAGE_NO_RECEIVER`: No receiver. Please make sure you pass in the right userId.

   * `NOT_LOGIN`: The sender has not logged in yet.

   * `USER_MESSAGE_UNKNOWN`: Unknown error.


<span id="setserverparams"></span>
### setServerParams  

Set the params of the server before calling [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendserverbinarymessage) to send messages to the server.


* **Type**

   ```ts
   (signature: string, url: string) => Promise<any>
   ```
   

* **Notes**

   * Call [login](https://docs.byteplus.com/en/docs/12/14190#login) before calling this API.

   * [onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-104479#onserverparamssetresult) notifies you whether the setting successes.

* **Parameters**

   * **signature**

      Type: `string`

      Dynamic signature. The App server may use the signature to verify the source of messages.

      You need to define the signature yourself. It can be any non\-empty string. It is recommended to encode information such as UID into the signature.

      The signature will be sent to the address set through the "url" parameter in the form of a POST request.

   * **url**

      Type: `string`

      Address of the IM server

* **Return Value**

   Type: `Promise<any>`


<span id="sendservermessage"></span>
### sendServerMessage  

Send point\-to\-point (P2P) text message to the server.


* **Type**

   ```ts
   (message: string) => Promise<any>
   ```
   

* **Notes**

   * Before calling this API, make sure you have [enabled Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console. If you enable this feature while the SDK is running, re\-initialize the engine for the configuration to take effect.

   * Before sending a message to the server, you must first call [login](https://docs.byteplus.com/en/docs/12/14190#login) to complete the login process.

* **Parameters**

   * **message**

      Type: `string`

      Text message within 64 KB.

* **Return Value**

   Type: `Promise<any>`

   * `USER_MESSAGE_TIMEOUT`: P2P message failed to be sent due to a timeout.

   * `USER_MESSAGE_BROKEN`: P2P message failed to be sent due to a broken channel.

   * `USER_MESSAGE_NO_RECEIVER`: No receiver. Please make sure you pass in the right userId.

   * `USER_MESSAGE_SEND_TO_SERVER_ERROR`: No response from the server.

   * `USER_MESSAGE_SERVER_RESPONSE_ERROR`: Failed to send message to the server. Response status code is not 200.

   * `NOT_LOGIN`: The sender has not logged in yet.

   * `USER_MESSAGE_SERVER_PARAMS_NOTSET`: The server params have not been set yet.

   * `USER_MESSAGE_UNKNOWN`: Unknown error.


<span id="sendserverbinarymessage"></span>
### sendServerBinaryMessage  

Send point\-to\-point (P2P) binary message to the server.


* **Type**

   ```ts
   (message: ArrayBuffer) => Promise<any>
   ```
   

* **Notes**

   * Before calling this API, make sure you have [enabled Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console. If you enable this feature while the SDK is running, re\-initialize the engine for the configuration to take effect.

   * Before sending a message to the server, you must first call [login](https://docs.byteplus.com/en/docs/12/14190#login) to complete the login process.

* **Parameters**

   * **message**

      Type: `ArrayBuffer`

      Binary message within 64 KB.

* **Return Value**

   Type: `Promise<any>`

   * `USER_MESSAGE_TIMEOUT`: P2P message failed to be sent due to a timeout.

   * `USER_MESSAGE_BROKEN`: P2P message failed to be sent due to a broken channel.

   * `USER_MESSAGE_NO_RECEIVER`: No receiver. Please make sure you pass in the right userId.

   * `USER_MESSAGE_SEND_TO_SERVER_ERROR`: No response from the server.

   * `USER_MESSAGE_SERVER_RESPONSE_ERROR`: Failed to send message to the server. Response status code is not 200.

   * `NOT_LOGIN`: The sender has not logged in yet.

   * `USER_MESSAGE_SERVER_PARAMS_NOTSET`: The server params have not been set yet.

   * `USER_MESSAGE_UNKNOWN`: Unknown error.


<span id="startcloudproxy"></span>
### startCloudProxy  

Start cloud proxy


* **Type**

   ```ts
   (cloudProxyInfo: CloudProxyInfo) => void
   ```
   

* **Notes**

   * Call this API before joining the room.

   * Start pre\-call network detection after starting cloud proxy.

   * After starting cloud proxy and connects the cloud proxy server successfully, receives [onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-104479#oncloudproxyconnected).

   * To stop cloud proxy, call [stopCloudProxy](https://docs.byteplus.com/en/docs/12/14190#stopcloudproxy).

* **Parameters**

   * **cloudProxyInfo**

      Type: [CloudProxyInfo](https://docs.byteplus.com/en/docs/12/docs-104481#cloudproxyinfo)

      cloud proxy information list.


<span id="stopcloudproxy"></span>
### stopCloudProxy  

Stop cloud proxy


* **Type**

   ```ts
   () => void
   ```
   

* **Notes**

   To start cloud proxy, call [startCloudProxy](https://docs.byteplus.com/en/docs/12/14190#startcloudproxy).


<span id="startpushpublicstream"></span>
### startPushPublicStream  

Starts publishing a WTN stream after the user joins a room.


* **Type**

   ```ts
   (publicStreamId: string, publicStreamParam: PublicStreamConfig) => Promise<void>
   ```
   

* **Notes**

   * Users with the same `appID` can call [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) to subscribe to and play the WTN stream regardless of whether the user has joined the room.

   * You cannot update the parameters of the WTN stream by repeatedly calling this API with the same stream ID by the same user. Call [updatePublicStreamParam](https://docs.byteplus.com/en/docs/12/14190#updatepublicstreamparam) to update the parameters instead.

   * Users with different `userID` can call this API with the same stream ID to update the parameters.

   * Call this API with different stream IDs to publish multiple WTN streams.

   * Call [stopPushPublicStream](https://docs.byteplus.com/en/docs/12/14190#stoppushpublicstream) to stop publishing the WTN stream.

* **Parameters**

   * **publicStreamId**

      Type: `string`

      The WTN stream's ID. The string must conform to the regular expression: `[a-zA-Z0-9_@\-\.]{1,128}`.

   * **publicStreamParam**

      Type: [PublicStreamConfig](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamconfig)

      The WTN stream's parameters.

      A WTN stream can contain several media streams and will appear as the designated layout.

      If the designated media stream is not published yet, the WTN stream will automatically update once the media stream is published.

* **Return Value**

   Type: `Promise<void>`

   `REPEAT_PUSH`: Publish a WTN stream repeatedly.


<span id="updatepublicstreamparam"></span>
### updatePublicStreamParam  

Update the properties of the WTN stream published by the current user via [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream).


* **Type**

   ```ts
   (publicStreamId: string, publicStreamParam: Partial<PublicStreamConfig>) => Promise<void>
   ```
   

* **Parameters**

   * **publicStreamId**

      Type: `string`

      The WTN stream's ID.

      The WTN stream must be published by the current user.

   * **publicStreamParam**

      Type: `Partial<`[PublicStreamConfig](https://docs.byteplus.com/en/docs/12/docs-104481#publicstreamconfig)`>`

      The WTN stream's parameters.

* **Return Value**

   Type: `Promise<void>`

   `REPEAT_PLAY`: Subscribe to a WTN stream repeatedly.


<span id="stoppushpublicstream"></span>
### stopPushPublicStream  

Stops publishing the WTN stream published by the current user via [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream).


* **Type**

   ```ts
   (publicStreamId: string) => Promise<void>
   ```
   

* **Notes**

   To stop publishing a WTN stream initiated by [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), call [stopPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stopplaywtn).

* **Parameters**

   * **publicStreamId**

      Type: `string`

      The WTN stream's ID.

      The WTN stream must be published by the current user.

* **Return Value**

   Type: `Promise<void>`


<span id="startplaypublicstream"></span>
### startPlayPublicStream  

Subscribes to a designated WTN stream.

You can call this API to subscribe to a WTN stream whether you joined the room or not.


* **Deprecated**

   since 4.65, use [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) instead.

* **Type**

   ```ts
   (publicStreamId: string) => Promise<void>
   ```
   

* **Notes**

   * Before calling this API, we recommend that you call [setPublicStreamVideoPlayer](https://docs.byteplus.com/en/docs/12/14190#setpublicstreamvideoplayer) first to set the player information and rendering mode for the WTN stream.

   * After calling this API, you will receive [onFirstPublicStreamVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-104479#onfirstpublicstreamvideoframedecoded) and [onFirstPublicStreamAudioFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-104479#onfirstpublicstreamaudioframedecoded) once the first frame has been decoded.

   * If the WTN stream contains SEI message, you will receive the message by being informed through [onPublicStreamSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onpublicstreamseimessagereceived).

   * Call [stopPlayPublicStream](https://docs.byteplus.com/en/docs/12/14190#stopplaypublicstream) to unsubscribe from the WTN stream.

* **Parameters**

   * **publicStreamId**

      Type: `string`

      The WTN stream's ID.

      If the designated stream is not published when you call this API, you will receive the WTN stream once it is published.

* **Return Value**

   Type: `Promise<void>`


<span id="stopplaypublicstream"></span>
### stopPlayPublicStream  

Unsubscribes from a designated WTN stream.

Call [startPlayPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startplaypublicstream) to subscribe to the WTN stream.


* **Deprecated**

   since 4.65, use [stopPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stopplaywtn) instead.

* **Type**

   ```ts
   (publicStreamId: string) => Promise<void>
   ```
   

* **Parameters**

   * **publicStreamId**

      Type: `string`

      The WTN stream's ID.

* **Return Value**

   Type: `Promise<void>`


<span id="setpublicstreamvideoplayer"></span>
### setPublicStreamVideoPlayer  

Sets the player information and rendering mode for the WTN stream.


* **Deprecated**

   since 4.65, use [setWTNRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-setwtnremotevideoplayer) instead.

* **Type**

   ```ts
   (publicStreamId: string, videoPlayerOption: Omit<VideoPlayerOption, 'userId' | 'playerId'>) => void
   ```
   

* **Parameters**

   * **publicStreamId**

      Type: `string`

      The WTN stream's ID.

   * **videoPlayerOption**

      Type: `Omit<`[VideoPlayerOption](https://docs.byteplus.com/en/docs/12/docs-104481#videoplayeroption)`, "userId" | "playerId">`

      Player information and rendering mode.


<span id="setdummycaptureimagepath"></span>
### setDummyCaptureImagePath  

Set the placeholder image during local video capture pause


* **Type**

   ```ts
   (index: StreamIndex, filePath: string) => Promise<void>
   ```
   

* **Notes**

   * Only available to Chrome browser on Mac

   * It is recommended to call this API before stopping video capture to avoid blank frame in video recording.

   * You cannot see the image during local preview.

* **Parameters**

   * **index**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

   * **filePath**

      Type: `string`

      Image path in HTTP protocol; or Blob object.

      The format of the image can be: JPG, PNG, or BMP.

      When the ratio of the image is not the same as the video encoder configuration, the image will be resized with fixed ratio until the width and the height are no more than that of the encoder configuration.

* **Return Value**

   Type: `Promise<void>`


<span id="defaulttranscoding"></span>
### defaultTranscoding  

Get the default parameters of `LiveTranscodeConfig`.


* **Type**

   ```ts
   () => Required<LiveTranscodeConfig>
   ```
   

* **Return Value**

   Type: `Required<`[LiveTranscodeConfig](https://docs.byteplus.com/en/docs/12/docs-104481#livetranscodeconfig)`>`

   The default parameters of `LiveTranscodeConfig`.


<span id="setsubscribefallbackoption"></span>
### setSubscribeFallbackOption  

Set the fallback option for remote media stream

Fallback means to enable media stream fallback or to subscribe to only audio stream under poor network conditions to ensure smooth communication.


* **Type**

   ```ts
   (option: SubscribeFallbackOption) => boolean
   ```
   

* **Notes**

   * Prerequisite: The local user has joined a room. And Simulcast has been enabled via [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14190#rtcengine-setlocalsimulcastmode). After joining the room, changing the option will not take effect.

   * After you enable the fallback, you will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-104479#onsimulcastsubscribefallback) and [onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onremotevideosizechanged) when the resolution of your subscribed stream is lowered or restored.

   * You can set media stream fallback using API or cloud configuration. The latter takes a higher priority.

* **Parameters**

   * **option**

      Type: [SubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-104481#subscribefallbackoption)

      Fallback options for subscribed media stream

* **Return Value**

   Type: `boolean`

   * `true` Success

   * `false` Failure


<span id="setremoteuserpriority"></span>
### setRemoteUserPriority  

Set the priority of the remote user's media stream.

Use this API with [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-104478#setsubscribefallbackoption).

With video stream fallback enabled and user priority specified, the stream quality of higher priority user is the last to be compromised.


* **Type**

   ```ts
   (userId: string, priority: RemoteUserPriority) => boolean
   ```
   

* **Parameters**

   * **userId**

      Type: `string`

      The ID of the remote user

   * **priority**

      Type: [RemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-104481#remoteuserpriority)

      The priority of the remote user's media stream

* **Return Value**

   Type: `boolean`

   * `true` Success

   * `false` Failure


<span id="startaudioplaybackdevicetest"></span>
### startAudioPlaybackDeviceTest  

Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will report the audio volume via the [onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-104479#onaudioplaybackdevicetestvolume) periodically.


* **Type**

   ```ts
   (filePath: string, indicationInterval: number) => Promise<void>
   ```
   

* **Notes**

   * You can call this API whether the user is in the room.

   * Call [stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14190#stopaudioplaybackdevicetest) to stop the playback test before moving on to the other device tests.

* **Parameters**

   * **filePath**

      Type: `string`

      Specify the path of the audio file for the playback test, including \*.wav and \*.mp3.

   * **indicationInterval**

      Type: `number`

      The time interval between each callback in milliseconds. We recommend setting it to 200 ms. The minimal value is 100 ms.

* **Return Value**

   Type: `Promise<void>`

   Resolve when the test ends.

   `REPEAT_DEVICE_TEST`: The test has already started.


<span id="stopaudioplaybackdevicetest"></span>
### stopAudioPlaybackDeviceTest  

Stop the playback test for the local audio device.


* **Type**

   ```ts
   () => void
   ```
   

* **Notes**

   Call this API to stop the playback test started by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14190#startaudioplaybackdevicetest) before moving on to the other device tests.


<span id="startaudiodevicerecordtest"></span>
### startAudioDeviceRecordTest  

Start the capture and playback test for local audio devices.

We recommend registering [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport) callback via [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport). Once the test starts, you can get the volume of the capturing audio by this callback.


* **Type**

   ```ts
   (indicationInterval: number, onAutoplayFailed?: ((resume: () => Promise<any>) => any) | undefined) => Promise<void>
   ```
   

* **Notes**

   * You can call this API whether the user is in a room.

   * You can call [setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setcapturevolume) to adjust the capture volume during audio route testing. You cannot call [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setplaybackvolume) during audio route testing.

   * The audio capturing will stop and begin to play the recording in 30 seconds after calling this API. Before that, call [stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/14190#stopaudiodevicerecordandplaytest) to stop capturing and start playing the recording.

   * You must stop the test before starting another test for audio devices.

   * Call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14190#stopaudiodeviceplaytest) to stop the test, including capturing and playing the recording.

   * This test performs locally and does not involve network connection testing.

* **Parameters**

   * **indicationInterval**

      Type: `number`

      The time interval between each callback of [onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-104479#onaudioplaybackdevicetestvolume) via which you get informed of the playback volume during the test. We recommend setting it to 200 ms. The minimal value is 100 ms.

   * **onAutoplayFailed**

      Type: `((resume: () => Promise<any>) => any) | undefined`

      Autoplay fails due to the limitation of the browser. We recommend executing `resume` as soon as the user clicks on the UI element.

* **Return Value**

   Type: `Promise<void>`

   Resolve when the test ends.

   The following error codes may be returned.

   * `NOT_SUPPORTED`: The browser does not support audio device test or audio capture.

   * `REPEAT_DEVICE_TEST`: The test has already started.

   * `AUDIO_DEVICE_RECORD_FAILED`: Failed to start the audio device test.


<span id="stopaudiodevicerecordandplaytest"></span>
### stopAudioDeviceRecordAndPlayTest  

Call this API to stop recording in the test and start to play the recording.

After calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiodevicerecordtest), you need to call this API within 30 seconds. Otherwise, the recording will automatically stop and begin playing back the recorded audio.


* **Type**

   ```ts
   () => void
   ```
   

* **Notes**

   After calling this API, the recording starts playing during which you can call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-104478#stopaudiodeviceplaytest) to stop playing.


<span id="stopaudiodeviceplaytest"></span>
### stopAudioDevicePlayTest  

Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiodevicerecordtest).

Before the test ends by itself, you can call this API to stop the recording or playing.


* **Type**

   ```ts
   () => void
   ```
   


<span id="setaudioprofile"></span>
### setAudioProfile  

Set the sound quality.


* **Type**

   ```ts
   (profile: AudioProfileType) => Promise<void>
   ```
   

* **Notes**

   You should call this API before starting audio capture and publishing streams.

* **Parameters**

   * **profile**

      Type: [AudioProfileType](https://docs.byteplus.com/en/docs/12/docs-104481#audioprofiletype)

      A sound quality option consists of a set of audio profiles and applying each brings a different listening experience. Choose the appropriate audio quality to meet the requirement of the scenario.

* **Return Value**

   Type: `Promise<void>`


<span id="getlocalstreamtrack"></span>
### getLocalStreamTrack  

Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the local audios or videos.


* **Type**

   ```ts
   (streamIndex: StreamIndex, type: 'video' | 'audio') => MediaStreamTrack | undefined
   ```
   

* **Notes**

   * Call this API after you start the local media capture or designate a customized MediaStreamTrack.

   * Callback of the MediaStreamTrack will inform you by the event of `ended` that the local media capture stops, probably caused either by an API call or the removal of devices.

   * You can get the following info from the MediaStreamTrack: video resolution, device ID, and volume. You can manage the track actions by the method of `stop` or `mute`. You can also change the properties of the stream, such as audio volume.

   * We recommend to call RTC APIs to enable your app with the following capabilities instead of using mediaStreamTrack.

&nbsp;

      * Get the video resolution or audio volume of the local streams: [onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalstreamstats)

      * Get device IDs: [enumerateDevices](https://docs.byteplus.com/en/docs/12/14190#enumeratedevices)

      * Stop capturing: [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14190#stopaudiocapture), [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14190#stopvideocapture)

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Mainstream or screen\-sharing stream.

   * **type**

      Type: `"video" | "audio"`

      Video or audio

      Audio: Track of the sounds collected from the microphone, customized audio track, audio files, and the sound card.

      Video: Track of the videos collected from the camera, customized video track and screen\-sharings.

* **Return Value**

   Type: `MediaStreamTrack | undefined`

   `undefined` for the MediaStreamTrack does not exist. For example, the local media capturing has not started.


<span id="getremotestreamtrack"></span>
### getRemoteStreamTrack  

Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the remote audios or videos.


* **Type**

   ```ts
   (userId: string, streamIndex: StreamIndex, type: 'video' | 'audio') => MediaStreamTrack | undefined
   ```
   

* **Notes**

   * Call this API after the local user subscribe to the remote media stream.

   * Callback of the MediaStreamTrack will inform you by the event of `ended` that the remote media stream stops, probably caused by the API call of [unsubscribeStream](https://docs.byteplus.com/en/docs/12/14190#unsubscribestream) or [unsubscribeScreen](https://docs.byteplus.com/en/docs/12/14190#unsubscribescreen).

   * You can get video resolution and audio volume from the MediaStreamTrack. You can manage the track actions by the method of `stop` or `mute`. You can also change the properties of the stream, such as audio volume.

   * We recommend to call RTC APIs to enable your app with the following capabilities instead of using mediaStreamTrack.

&nbsp;

      * Get the video resolution or audio volume of the remote streams: [onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#onremotestreamstats)

      * Unsubscribe: [unsubscribeStream](https://docs.byteplus.com/en/docs/12/14190#unsubscribestream), [unsubscribeScreen](https://docs.byteplus.com/en/docs/12/14190#unsubscribescreen)

* **Parameters**

   * **userId**

      Type: `string`

      ID of the remote user

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Mainstream or screen\-sharing stream.

   * **type**

      Type: `"video" | "audio"`

      Video or audio

* **Return Value**

   Type: `MediaStreamTrack | undefined`

   `undefined` for the MediaStreamTrack does not exist. For example, the local user has not subscribed to the remote stream.


<span id="getpublicstreamtrack"></span>
### getPublicStreamTrack  

Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the audios or videos from the subscribed WTN stream.


* **Type**

   ```ts
   (id: string, type: 'video' | 'audio') => MediaStreamTrack | undefined
   ```
   

* **Notes**

   * Call this API after you start playing the WTN stream by calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn).

   * Callback of the MediaStreamTrack will inform you of the event of `ended` that the WTN stream stops, probably caused by the API call of [stopPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stopplaywtn).

* **Parameters**

   * **id**

      Type: `string`

      ID of the WTN stream

   * **type**

      Type: `"video" | "audio"`

      Video or audio

* **Return Value**

   Type: `MediaStreamTrack | undefined`

   `undefined` for the MediaStreamTrack does not exist. For example, the WTN stream does not exist.


<span id="takelocalsnapshot"></span>
### takeLocalSnapshot  

Take a snapshot of the local video.


* **Type**

   ```ts
   (streamIndex: StreamIndex) => Promise<ImageData>
   ```
   

* **Notes**

   * Before using this method to capture a snapshot, make sure the local camera is actively streaming. You can check this via [getLocalStreamTrack](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getlocalstreamtrack). A non\-empty return value indicates that the local video stream is active and ready for snapshot capture.

   * The snapshot is taken with the beauty effect and virtual background.

   * You can take the snapshot either using SDK internal video capture or customized capture.

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      The specified video stream.

* **Return Value**

   Type: `Promise<ImageData>`

   `INVOKED_BEFORE_CAPTURE`: No such stream. Please make sure that the specified stream has been published.


<span id="takeremotesnapshot"></span>
### takeRemoteSnapshot  

Take a snapshot of the remote video.


* **Type**

   ```ts
   (id: string, streamIndex: StreamIndex) => Promise<ImageData>
   ```
   

* **Notes**

   Before using this method to capture a snapshot, make sure you have successfully received the remote stream on the local client. You can check this via [getRemoteStreamTrack](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getremotestreamtrack). A non\-empty return value indicates that the remote stream has been successfully subscribed to.

* **Parameters**

   * **id**

      Type: `string`

      The index of the user's stream or the index of the WTN stream.

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      The specified video stream.

* **Return Value**

   Type: `Promise<ImageData>`

   `STREAM_NOT_EXIST`: The target stream does not exist. Please enter the correct ID or make sure that the target stream is in the room.


<span id="registerextension"></span>
### registerExtension  

Registers an extension.

You can use the extension to implement features such as [Beauty Effects](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148646), [Virtual Background](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148647).


* **Type**

   ```ts
   (extension: RTCExtension) => Promise<void>
   ```
   

* **Parameters**

   * **extension**

      Type: `RTCExtension`

      The extension instance.

* **Return Value**

   Type: `Promise<void>`


<span id="setremotestreamrendersync"></span>
### setRemoteStreamRenderSync  

Set whether the remote audio and video streams are rendered synchronously.

You can achieve ultra low latency by turning off the audio and video synchronization.


* **Type**

   ```ts
   (sync: boolean) => boolean
   ```
   

* **Notes**

   You must call this API before joining the room. Calling it afterward is invalid.

* **Parameters**

   * **sync**

      Type: `boolean`

      `true`: (Default) Turn on sync.

      `false`: Turn off sync.

* **Return Value**

   Type: `boolean`

   * `true`: Success.

   * `false`: Failure.


<span id="setcapturevolume"></span>
### setCaptureVolume  

Adjust audio capture volume.


* **Type**

   ```ts
   (streamIndex: StreamIndex, volume: number) => void
   ```
   

* **Notes**

   * It is recommended to set the capture volume after the capture has started.

   * If capture has not yet started when you call this API, the setting will take effect after it starts.

   * The capture volume adjustment controls the audio stream before audio mixing.

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      The index of the target stream whose recording volume is to be adjusted.

   * **volume**

      Type: `number`

      The percentage of capturing volume to the original volume in the range of [0, 400]. The default value is 100%.

      For better call quality, it is recommended to set the value in the range of [0, 100].


<span id="setplaybackvolume"></span>
### setPlaybackVolume  

Adjust audio playback volume of a specified remote user.


* **Type**

   ```ts
   (userId: string, streamIndex: StreamIndex, volume: number) => void
   ```
   

* **Notes**

   * It is recommended to set the playback volume after the playing has started.

   * If the playing has not yet started when you call this API, the setting will take effect after it starts.

   * The playback volume cannot be adjusted in [Conference Mode](https://docs.byteplus.com/en/docs/12/docs-113547).

* **Parameters**

   * **userId**

      Type: `string`

      The Id of the specified remote user.

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      The index of the target stream whose playback volume is to be adjusted.

   * **volume**

      Type: `number`

      The percentage of playback volume to the original volume in the range of [0, 400]. The default value is 100%.

      For better call quality, it is recommended to set the value in the range of [0, 100].


<span id="setpublicstreamvolume"></span>
### setPublicStreamVolume  

Adjusts audio playback volume of a WTN stream.


* **Deprecated**

   since 4.65, use [setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-setwtnremoteaudioplaybackvolume) instead.

* **Type**

   ```ts
   (publicStreamId: string, volume: number) => void
   ```
   

* **Notes**

   * It is recommended to set the playback volume after the playing has started.

   * If the playing has not yet started when you call this API, the setting will take effect after it starts.

* **Parameters**

   * **publicStreamId**

      Type: `string`

      The Id of a specified WTN stream.

   * **volume**

      Type: `number`

      The percentage of playback volume to the original volume in the range of [0, 400]. The default value is 100%.

      For better call quality, it is recommended to set the value in the range of [0, 100].


<span id="startforwardstreamtorooms"></span>
### startForwardStreamToRooms  

Start forwarding media stream across rooms. See [Forward media stream across rooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104398) for details.

After calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-joinroom), you can call this API to publish the media stream to multiple rooms. This feature is suitable for scenarios such as co\-host PK and online karaoke.


* **Type**

   ```ts
   (forwardStreamInfos: ForwardStreamInfo[]) => Promise<ForwardStreamStateInfo[]>
   ```
   

* **Notes**

   * Once the forwarding begins, other users in the target room will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserjoined) and [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishstream)/[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishscreen).

   * Call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-updateforwardstreamtorooms) to add or remove the target room(s).

   * Call [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopforwardstreamtorooms) to stop forwarding media stream to all rooms.

   * Call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-pauseforwardstreamtoallrooms) to pause forwarding media stream to all rooms.

* **Parameters**

   * **forwardStreamInfos**

      Type: [ForwardStreamInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreaminfo)`[]`

      Information of the target rooms where the stream will be forwarded.

* **Return Value**

   Type: `Promise<`[ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreamstateinfo)`[]>`

   Status information for forwarding media stream across rooms.

   `UNEXPECTED_INVOKE_FORWARD_STREAM`: Unexpected operation. Triggered if the timing of API calls related to forwarding media streams across rooms is incorrect. Please refer to the documentation of each API to confirm the correct order of API calls.


<span id="updateforwardstreamtorooms"></span>
### updateForwardStreamToRooms  

Update information of the rooms where the stream will be forwarded after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startforwardstreamtorooms).


* **Type**

   ```ts
   (forwardStreamInfos: ForwardStreamInfo[]) => Promise<ForwardStreamStateInfo[]>
   ```
   

* **Notes**

   * Users in the added room will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserjoined) and [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishstream)/[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishscreen).

   * Users in the removed room will receive [onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishstream)/[onUserUnpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishscreen) and [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserleave).

* **Parameters**

   * **forwardStreamInfos**

      Type: [ForwardStreamInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreaminfo)`[]`

      Information of the target rooms where the stream will be forwarded.

* **Return Value**

   Type: `Promise<`[ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreamstateinfo)`[]>`

   Status information for forwarding media stream across rooms.

   `UNEXPECTED_INVOKE_FORWARD_STREAM`: Unexpected operation. Triggered if the timing of API calls related to forwarding media streams across rooms is incorrect. Please refer to the documentation of each API to confirm the correct order of API calls.


<span id="stopforwardstreamtorooms"></span>
### stopForwardStreamToRooms  

Stop forwarding media stream to all rooms.


* **Type**

   ```ts
   () => Promise<ForwardStreamStateInfo[]>
   ```
   

* **Notes**

   * Users in the former target rooms will receive [onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishstream)/[onUserUnpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishscreen) and [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserleave).

   * Call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-updateforwardstreamtorooms) to stop forwarding media stream to specific rooms.

   * Call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-pauseforwardstreamtoallrooms) and [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-resumeforwardstreamtoallrooms) to pause and resume forwarding media stream to all rooms.

* **Return Value**

   Type: `Promise<`[ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreamstateinfo)`[]>`

   Status information for forwarding media stream across rooms.

   `UNEXPECTED_INVOKE_FORWARD_STREAM`: Unexpected operation. Triggered if the timing of API calls related to forwarding media streams across rooms is incorrect. Please refer to the documentation of each API to confirm the correct order of API calls.


<span id="pauseforwardstreamtoallrooms"></span>
### pauseForwardStreamToAllRooms  

Pause forwarding media stream to all rooms.

After calling this API, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-resumeforwardstreamtoallrooms) to resume.


* **Type**

   ```ts
   () => Promise<ForwardStreamStateInfo[]>
   ```
   

* **Notes**

   Users in the target rooms will receive [onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishstream)/[onUserUnpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishscreen) and [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserleave).

* **Return Value**

   Type: `Promise<`[ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreamstateinfo)`[]>`

   Status information for forwarding media stream across rooms.

   `UNEXPECTED_INVOKE_FORWARD_STREAM`: Unexpected operation. Triggered if the timing of API calls related to forwarding media streams across rooms is incorrect. Please refer to the documentation of each API to confirm the correct order of API calls.


<span id="resumeforwardstreamtoallrooms"></span>
### resumeForwardStreamToAllRooms  

Resume forwarding media stream to all rooms.


* **Type**

   ```ts
   () => Promise<ForwardStreamStateInfo[]>
   ```
   

* **Notes**

   Users in the target room will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserjoined) and [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishstream)/[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishscreen).

* **Return Value**

   Type: `Promise<`[ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-104481#forwardstreamstateinfo)`[]>`

   Status information for forwarding media stream across rooms.

   `UNEXPECTED_INVOKE_FORWARD_STREAM`: Unexpected operation. Triggered if the timing of API calls related to forwarding media streams across rooms is incorrect. Please refer to the documentation of each API to confirm the correct order of API calls.


<span id="setaudioselectionconfig"></span>
### setAudioSelectionConfig  

Set the priority of the local audio stream to be published.


* **Type**

   ```ts
   (audioSelectionPriority: AudioSelectionPriority) => Promise<void>
   ```
   

* **Parameters**

   * **audioSelectionPriority**

      Type: [AudioSelectionPriority](https://docs.byteplus.com/en/docs/12/docs-104481#audioselectionpriority)

      The priority of the local audio stream which defaults to be subscribable only up to the result of the Audio Selection.

* **Return Value**

   Type: `Promise<void>`


<span id="getremotevideostats"></span>
### getRemoteVideoStats  

Gets the statistics of subscribed video streams and network states.


* **Type**

   ```ts
   () => Record<string, RemoteUserVideoStats[]>
   ```
   

* **Notes**

   The statistics obtained through this method within 1 second remain unchanged.

* **Return Value**

   Type: `Record<string, `[RemoteUserVideoStats](https://docs.byteplus.com/en/docs/12/docs-104481#remoteuservideostats)`[]>`

   Include the camera video and the screen recording.


<span id="getremoteaudiostats"></span>
### getRemoteAudioStats  

Gets the statistics of subscribed audio streams and network states.


* **Type**

   ```ts
   () => Record<string, RemoteUserAudioStats[]>
   ```
   

* **Notes**

   The statistics obtained through this method within 1 second remain unchanged.

* **Return Value**

   Type: `Record<string, `[RemoteUserAudioStats](https://docs.byteplus.com/en/docs/12/docs-104481#remoteuseraudiostats)`[]>`

   Include the microphone audio and the device audio.


<span id="getlocalvideostats"></span>
### getLocalVideoStats  

Gets the statistics of local video streams and network states.


* **Type**

   ```ts
   () => LocalUserVideoStats
   ```
   

* **Notes**

   The statistics obtained through this method within 1 second remain unchanged.

* **Return Value**

   Type: [LocalUserVideoStats](https://docs.byteplus.com/en/docs/12/docs-104481#localuservideostats)

   Include the camera video and the screen recording.


<span id="getlocalaudiostats"></span>
### getLocalAudioStats  

Gets the statistics of local audio streams and network states.


* **Type**

   ```ts
   () => LocalUserAudioStats
   ```
   

* **Notes**

   The statistics obtained through this method within 1 second remain unchanged.

* **Return Value**

   Type: [LocalUserAudioStats](https://docs.byteplus.com/en/docs/12/docs-104481#localuseraudiostats)

   Include the microphone audio and the device audio.


<span id="setearmonitormode"></span>
### setEarMonitorMode  

Enable/Disable in\-ear monitoring.


* **Type**

   ```ts
   (streamIndex: StreamIndex, position: EarMonitorPosition) => Promise<void>
   ```
   

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Mainstream or screen\-sharing stream.

   * **position**

      Type: [EarMonitorPosition](https://docs.byteplus.com/en/docs/12/docs-104481#earmonitorposition)

      Whether to enable in\-ear monitoring. Specify whether the in\-ear monitoring audio is processed.

* **Return Value**

   Type: `Promise<void>`

   If the in\-ear monitoring audio fails to play automatically, we recommend calling this method again after receiving [onAutoplayFailed](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onautoplayfailed) to recover.


<span id="setearmonitorvolume"></span>
### setEarMonitorVolume  

Set the monitoring volume.


* **Type**

   ```ts
   (streamIndex: StreamIndex, volume: number) => void
   ```
   

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Mainstream or screen\-sharing stream.

   * **volume**

      Type: `number`

      The monitoring volume with the adjustment range between 0 and 400. The initial value is `100`.


<span id="getlocalvideoplayervisibility"></span>
### getLocalVideoPlayerVisibility  

> Available since V4.67.


Get the visibility state of local video player and reasons for invisibility.


* **Type**

   ```ts
   (streamIndex: StreamIndex, playerId?: string) => PlayerVisibility | undefined
   ```
   

* **Parameters**

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Stream index

   * **playerId**

      Type: `string | undefined`

      Optional parameter, player ID.

* **Return Value**

   Type: [PlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104481#playervisibility)` | undefined`

   Player visibility state.

   If the corresponding player does not exist, return `undefined`.


<span id="getremoteplayervisibility"></span>
### getRemotePlayerVisibility  

> Available since V4.67.


Gets the visibility state of remote video player and reasons for invisibility.


* **Type**

   ```ts
   (userId: string, streamIndex: StreamIndex, playerId?: string) => PlayerVisibility | undefined
   ```
   

* **Parameters**

   * **userId**

      Type: `string`

      User ID.

   * **streamIndex**

      Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-104481#streamindex)

      Stream index.

   * **playerId**

      Type: `string | undefined`

      Optional parameter, player ID.

* **Return Value**

   Type: [PlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104481#playervisibility)` | undefined`

   Player visibility state.

   If the corresponding player does not exist, return `undefined`.


<span id="byteplusrtc"></span>
## BytePlusRTC  

Type: `interface`


* **API**



|Method |Description |
|---|---|
|[createEngine](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-createengine) |Call this API to create an IRTCEngine instance that provides RTC service.<br><br>Call this API before calling any other APIs within the RTC SDK.<br><br>Calling this API repeatedly will create multiple IRTCEngine instances. |
|[destroyEngine](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-destroyengine) |Call this API to destroy the IRTCEngine instance created by [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine). |
|[getSdkVersion](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-getsdkversion) |Get the current version of the SDK. |
|[enumerateDevices](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-enumeratedevices) |Call this API to enumerate media devices and their IDs, such as microphones, cameras, and headsets.<br><br>Call this API to get deviceId used to specify the device when calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice), [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture), and [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture). |
|[enableDevices](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-enabledevices) |Call this API to request access to video and audio devices. |
|[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-enumerateaudiocapturedevices) |Call this API to enumerate microphone devices.<br><br>Call this API to get Device IDs used to specify the device when calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture) and [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiocapturedevice). |
|[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-enumeratevideocapturedevices) |Call this API to enumerate audio and video devices and their IDs, such as microphones, cameras, and headsets.<br><br>Call this API to get Device IDs used to specify the device when calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture) and [setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setvideocapturedevice). |
|[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-enumerateaudioplaybackdevices) |Call this API to enumerate audio playback devices and their IDs, such as speakers and headsets.<br><br>Call this API to get Device IDs used to specify the device when calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice). |
|[isSupported](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-issupported) |Call this API to check whether the browser is supported. |
|[getSupportedCodecs](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-getsupportedcodecs) |Gets the codec type supported by current browser.<br><br>If you have enabled vp8 codec, you can call the API to check whether the current browser supports vp8 encoding type before entering the room. |
|[setLogConfig](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-setlogconfig) |Configures the logging level of local cache, and the maximum cache space that can be used. |
|[downloadLog](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-downloadlog) |Download the generated local cache file. |
|[getElectronScreenSources](https://docs.byteplus.com/en/docs/12/14190#byteplusrtc-getelectronscreensources) |Get the list of screen\-sharing objects. |


<span id="createengine"></span>
### createEngine  

Call this API to create an IRTCEngine instance that provides RTC service.

Call this API before calling any other APIs within the RTC SDK.

Calling this API repeatedly will create multiple IRTCEngine instances.


* **Type**

   ```ts
   (appId: string, config?: EngineConfig) => IRTCEngine
   ```
   

* **Notes**

   * Call [destroyEngine](https://docs.byteplus.com/en/docs/12/14190#destroyengine) respectively to destroy each IRTCEngine instance.

   * As each IRTCEngine instance is resource consuming, we recommend creating no more than 2 engine instances on each device at the same time.

* **Parameters**

   * **appId**

      Type: `string`

      A unique identifier for each application. You can apply appIDs on the RTC console.

      Instances generated by different AppIDs are independent in RTC service. Users served by one AppID cannot communicate with users served by another AppID.

   * **config**

      Type: [EngineConfig](https://docs.byteplus.com/en/docs/12/docs-104481#engineconfig)` | undefined`

      Configuration of the engine instance, such as Auto\-play policy

* **Return Value**

   Type: [IRTCEngine](https://docs.byteplus.com/en/docs/12/14190#rtcengine)

   Return an `IRTCEngine` instance if you call this API successfully.


<span id="destroyengine"></span>
### destroyEngine  

Call this API to destroy the IRTCEngine instance created by [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine).


* **Type**

   ```ts
   (engine: IRTCEngine) => void
   ```
   

* **Notes**

   * Before calling this API， ensure all business scenarios related to this `IRTCEngine` instance have ended.

   * Calling this API will block the main thread until it completes the exiting process. Therefore, do not include this API in a callback. Do not wait in a callback for the execution of this API in the main thread, thus causing a deadlock.

* **Parameters**

   * **engine**

      Type: [IRTCEngine](https://docs.byteplus.com/en/docs/12/14190#rtcengine)

      By calling this API, this `IRTCEngine` instance and related resources will be wiped from memory. And any interaction with the media server will end.


<span id="getsdkversion"></span>
### getSdkVersion  

Get the current version of the SDK.


* **Type**

   ```ts
   () => string
   ```
   

* **Return Value**

   Type: `string`

   The current SDK version.


<span id="enumeratedevices"></span>
### enumerateDevices  

Call this API to enumerate media devices and their IDs, such as microphones, cameras, and headsets.

Call this API to get deviceId used to specify the device when calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice), [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture), and [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture).


* **Type**

   ```ts
   () => Promise<MediaDeviceInfo[]>
   ```
   

* **Notes**

   Only when the browser has permission to the media devices can it enumerate the full device list. Make sure the media device access is turned on via [enableDevices](https://docs.byteplus.com/en/docs/12/14190#enabledevices) before calling this API.

* **Return Value**

   Type: `Promise<MediaDeviceInfo[]>`

   A list of all media devices. See [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo).


<span id="enabledevices"></span>
### enableDevices  

Call this API to request access to video and audio devices.


* **Type**

   ```ts
   (options?: { video: boolean; audio: boolean;}) => Promise<{ video: boolean; audio: boolean; videoExceptionError?: DOMException; audioExceptionError?: DOMException;}>
   ```
   

* **Parameters**

   * **options**

      Type: `{ video: boolean; audio: boolean; } | undefined`

      The device type you need.

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |video |`boolean` |Video devices |
         |audio |`boolean` |Audio devices |
         

* **Return Value**

   Type: `Promise<{ video: boolean; audio: boolean; videoExceptionError?: DOMException; audioExceptionError?: DOMException; }>`

   * `video: boolean` Whether the video device permission is obtained.

   * `audio: boolean` Whether the audio device permission is obtained.

   * `videoExceptionError?: DOMException` Error message for obtaining video device permission.

   * `audioExceptionError?: DOMException` Error message for obtaining audio device permission.


<span id="enumerateaudiocapturedevices"></span>
### enumerateAudioCaptureDevices  

Call this API to enumerate microphone devices.

Call this API to get Device IDs used to specify the device when calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture) and [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiocapturedevice).


* **Type**

   ```ts
   () => Promise<MediaDeviceInfo[]>
   ```
   

* **Notes**

   Only when the browser has permission to the media devices can it enumerate the full device list. Make sure the media device access is turned on [enableDevices](https://docs.byteplus.com/en/docs/12/14190#enabledevices) before calling this API.

* **Return Value**

   Type: `Promise<MediaDeviceInfo[]>`

   A list including all microphone devices. See [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo).


<span id="enumeratevideocapturedevices"></span>
### enumerateVideoCaptureDevices  

Call this API to enumerate audio and video devices and their IDs, such as microphones, cameras, and headsets.

Call this API to get Device IDs used to specify the device when calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture) and [setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setvideocapturedevice).


* **Type**

   ```ts
   () => Promise<MediaDeviceInfo[]>
   ```
   

* **Notes**

   Only when the browser has permission to the media devices can it enumerate the full device list. Make sure the media device access is turned on [enableDevices](https://docs.byteplus.com/en/docs/12/14190#enabledevices) before calling this API.

* **Return Value**

   Type: `Promise<MediaDeviceInfo[]>`

   A list including all camera devices. See [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo).


<span id="enumerateaudioplaybackdevices"></span>
### enumerateAudioPlaybackDevices  

Call this API to enumerate audio playback devices and their IDs, such as speakers and headsets.

Call this API to get Device IDs used to specify the device when calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice).


* **Type**

   ```ts
   () => Promise<MediaDeviceInfo[]>
   ```
   

* **Notes**

   Only when the browser has permission to the media devices can it enumerate the full device list. Make sure the media device access is turned on [enableDevices](https://docs.byteplus.com/en/docs/12/14190#enabledevices) before calling this API.

* **Return Value**

   Type: `Promise<MediaDeviceInfo[]>`

   A list including all audio playback devices. See [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo).


<span id="issupported"></span>
### isSupported  

Call this API to check whether the browser is supported.


* **Type**

   ```ts
   () => Promise<boolean>
   ```
   

* **Return Value**

   Type: `Promise<boolean>`

   * `True`: Supported

   * `False`: Not Supported


<span id="getsupportedcodecs"></span>
### getSupportedCodecs  

Gets the codec type supported by current browser.

If you have enabled vp8 codec, you can call the API to check whether the current browser supports vp8 encoding type before entering the room.


* **Type**

   ```ts
   () => Promise<string[]>
   ```
   

* **Return Value**

   Type: `Promise<string[]>`

   Codec types supported by the current browser


<span id="setlogconfig"></span>
### setLogConfig  

Configures the logging level of local cache, and the maximum cache space that can be used.


* **Type**

   ```ts
   ({ logLevel, LogfileSize, }: { logLevel?: 'none' | 'error' | 'warning' | 'info' | 'trace'; LogfileSize?: number;}) => void
   ```
   

* **Notes**

   This API must be called before [createEngine](https://docs.byteplus.com/en/docs/12/14190#createengine). If called after [createEngine](https://docs.byteplus.com/en/docs/12/14190#createengine), it will take effect after the next [createEngine](https://docs.byteplus.com/en/docs/12/14190#createengine) after [destroyEngine](https://docs.byteplus.com/en/docs/12/14190#destroyengine).

* **Parameters**

   *  **{** 

      **logLevel,** 

      **LogfileSize,** 

       **}** 

      Type: `{ logLevel?: "none" | "error" | "warning" | "info" | "trace" | undefined; LogfileSize?: number | undefined; }`

      * **Member**

         
         |Name |Type |Description |
         |---|---|---|
         |logLevel |`"none" \| "error" \| "warning" \| "info" \| "trace" \| undefined` |The logging level of local cache.<br><br>• `none`: (Default) Turn off logging.<br><br>• `error`: Error.<br><br>• `warning`: Warning.<br><br>• `info`: Information.<br><br>• `trace`: Trace. |
         |LogfileSize |`number \| undefined` |The maximum cache space available for logs in MB. The range is 1 to 100 MB, and the default value is 10 MB. |
         


<span id="downloadlog"></span>
### downloadLog  

Download the generated local cache file.


* **Type**

   ```ts
   (key?: string) => void
   ```
   

* **Parameters**

   * **key**

      Type: `string | undefined`

      The key of the local cache. If empty, download the logs from the current cache.


<span id="getelectronscreensources"></span>
### getElectronScreenSources  

Get the list of screen\-sharing objects.


* **Type**

   ```ts
   (type?: ScreenSourceType) => Promise<ElectronDesktopCapturerSource[]>
   ```
   

* **Notes**

   For more details, see [Implement screen sharing with Web SDK in Electron](https://docs.byteplus.com/byteplus-rtc/docs/1340581).

* **Parameters**

   * **type**

      Type: [ScreenSourceType](https://docs.byteplus.com/en/docs/12/docs-104481#screensourcetype)` | undefined`

      The type of screen\-sharing object, screen or application. If empty, get all the available screen\-sharing objects.

* **Return Value**

   Type: `Promise<`[ElectronDesktopCapturerSource](https://docs.byteplus.com/en/docs/12/docs-104481#electrondesktopcapturersource)`[]>`

   The list of screen\-sharing objects.

   Refer to [ERR_ELECTRON_IS_NULL](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode) and [ELECTRON_DESKTOP_CAPTURER_GET_SOURCES_ERROR](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode) for the details of the error code.


<span id="audiomixingmanager"></span>
## AudioMixingManager  

Type: `interface`


* **API**



|Method |Description |
|---|---|
|[startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-startaudiomixing) |Start playing audio files and mixes.<br><br>This method can be called many times by passing in different IDs and filepaths to realize simultaneous playback of multiple mixing files and mixing overlay. |
|[stopAudioMixing](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-stopaudiomixing) |Stop playing audio files and mixes |
|[pauseAudioMixing](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-pauseaudiomixing) |Pause playing audio files and mixes |
|[resumeAudioMixing](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-resumeaudiomixing) |Resume playing audio files and mixing |
|[preloadAudioMixing](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-preloadaudiomixing) |Preload the specified audio file into memory |
|[unloadAudioMixing](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-unloadaudiomixing) |Unload the specified audio file |
|[setAudioMixingVolume](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-setaudiomixingvolume) |Adjust the volume of the audio\-file mixing. |
|[getAudioMixingVolume](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-getaudiomixingvolume) |Get volume of the audio files. |
|[getAudioMixingDuration](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-getaudiomixingduration) |Get audio file duration |
|[getAudioMixingCurrentPosition](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-getaudiomixingcurrentposition) |Get audio file playback progress |
|[setAudioMixingPosition](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-setaudiomixingposition) |Set the starting playback position of the audio file |
|[setAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-setaudioframecallback) |Toggle the callbacks carrying the mixing audio frames. |
|[enableAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-enableaudiomixingbuffer) |Start PCM mixing.<br><br>To mix multiple PCM audio streams, call this API multiple times with different IDs. |
|[disableAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-disableaudiomixingbuffer) |Disable PCM mixing. |
|[pushAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/14190#audiomixingmanager-pushaudiomixingbuffer) |Push PCM audio frame data for mixing |


<span id="startaudiomixing"></span>
### startAudioMixing  

Start playing audio files and mixes.

This method can be called many times by passing in different IDs and filepaths to realize simultaneous playback of multiple mixing files and mixing overlay.


* **Type**

   ```ts
   (id: number, filePath: string, options: MixOption) => Promise<void>
   ```
   

* **Notes**

   * If you have already loaded the sound effect into memory through [preloadAudioMixing](https://docs.byteplus.com/en/docs/12/14190#preloadaudiomixing), make sure that the ID here is the same as the ID set by [preloadAudioMixing](https://docs.byteplus.com/en/docs/12/14190#preloadaudiomixing).

   * After you start playing the audio file and mixing, you can call the [stopAudioMixing](https://docs.byteplus.com/en/docs/12/14190#stopaudiomixing) method to stop playing the audio file.

   * The mixing data of this method comes from an external file, while the mixing data of [enableAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/14190#enableaudiomixingbuffer) comes from an external cache and the audio format is PCM. These two mixing methods can coexist.

* **Parameters**

   * **id**

      Type: `number`

      Mix ID. For identifying the mix, please ensure that the mix ID is unique.

      If this method is repeatedly called with the same ID, the previous mix stops and the next mix starts.

   * **filePath**

      Type: `string`

      Specify the file path either the absolute path of a local file or the url of online audio. Files with the extension of mp3 and aac are supported.

   * **options**

      Type: [MixOption](https://docs.byteplus.com/en/docs/12/docs-104481#mixoption)

      Mix Sound configuration.

      You can set the number of times the mix is played, whether the mix is played locally, and whether the mix is sent to the remote end. For details, see the documentation.

* **Return Value**

   Type: `Promise<void>`

   `LOAD_RESOURCES_FAILED`: Loading resource failed. Please pass in the correct resource path.


<span id="stopaudiomixing"></span>
### stopAudioMixing  

Stop playing audio files and mixes


* **Type**

   ```ts
   (id: number) => void
   ```
   

* **Notes**

   * After calling [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing) method to start playing audio files and mixes, you can call this method to stop playing audio files and mixes.

   * After calling this method to stop playing the audio file, the audio file will be automatically uninstalled.

* **Parameters**

   * **id**

      Type: `number`

      ID of the mixing


<span id="pauseaudiomixing"></span>
### pauseAudioMixing  

Pause playing audio files and mixes


* **Type**

   ```ts
   (id: number) => void
   ```
   

* **Notes**

   * After calling [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing) method to start playing audio files and mixes, you can call this method to pause playing audio files and mixes.

   * After calling this method to pause playing audio files and mixing, you can call the [resumeAudioMixing](https://docs.byteplus.com/en/docs/12/14190#resumeaudiomixing) method to resume playing and mixing.

* **Parameters**

   * **id**

      Type: `number`

      ID of the mixing


<span id="resumeaudiomixing"></span>
### resumeAudioMixing  

Resume playing audio files and mixing


* **Type**

   ```ts
   (id: number) => void
   ```
   

* **Notes**

   After calling the [pauseAudioMixing](https://docs.byteplus.com/en/docs/12/14190#pauseaudiomixing) method to pause playing audio files and mixing, you can resume playing and mixing by calling this method.

* **Parameters**

   * **id**

      Type: `number`

      Mixing ID


<span id="preloadaudiomixing"></span>
### preloadAudioMixing  

Preload the specified audio file into memory


* **Type**

   ```ts
   (id: number, filePath: string) => Promise<void>
   ```
   

* **Notes**

   * When you need to play an audio file frequently, call this method to preload the file. When playing, you can only load the file once to reduce CPU usage.

   * This method pre\-loads the specified audio file, and only calling [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing) API can you start playing the specified audio file.

   * The specified audio file preloaded by calling this method can be unloaded through [unloadAudioMixing](https://docs.byteplus.com/en/docs/12/14190#unloadaudiomixing).

* **Parameters**

   * **id**

      Type: `number`

      Mix ID. For identifying the mix, please ensure that the mix ID is unique.

      If this method is called repeatedly with the same ID, the latter overrides the previous.

      If you call [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing) and then call this method with the same ID, the previous mix stops, and then the next mix is loaded.

      After calling this method with an ID to preload A.mp3, if you need to call [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing) to play B.mp3 with the same ID, please call [unloadAudioMixing](https://docs.byteplus.com/en/docs/12/14190#unloadaudiomixing) to uninstall A.mp3 first, otherwise an error will be reported AUDIO_MIXING_ERROR_LOAD_CONFLICT.

   * **filePath**

      Type: `string`

      Used for mixing file paths. It can be the absolute path of the local file or the url of the online audio.

* **Return Value**

   Type: `Promise<void>`

   `LOAD_RESOURCES_FAILED`: Loading resource failed. Please pass in the correct resource path.


<span id="unloadaudiomixing"></span>
### unloadAudioMixing  

Unload the specified audio file


* **Type**

   ```ts
   (id: number) => void
   ```
   

* **Parameters**

   * **id**

      Type: `number`

      Mix ID


<span id="setaudiomixingvolume"></span>
### setAudioMixingVolume  

Adjust the volume of the audio\-file mixing.


* **Type**

   ```ts
   (id: number, volume: number) => void
   ```
   

* **Parameters**

   * **id**

      Type: `number`

      Mixing ID

   * **volume**

      Type: `number`

      The ratio of the mixing volume to the original volume. The range is `[0, 400]`. The recommended range is `[0, 100]`.

* 0: Mute

* 100: Original volume

* 400: Maximum volume (with overflow protection)


<span id="getaudiomixingvolume"></span>
### getAudioMixingVolume  

Get volume of the audio files.


* **Type**

   ```ts
   (id: number) => number
   ```
   

* **Parameters**

   * **id**

      Type: `number`

      Audio mix id

* **Return Value**

   Type: `number`

   * `0`: Failure

   * `>0`: Successful. Volume


<span id="getaudiomixingduration"></span>
### getAudioMixingDuration  

Get audio file duration


* **Type**

   ```ts
   (id: number) => number
   ```
   

* **Notes**

   Before calling this method to obtain the length of the audio file, you need to call [preloadAudioMixing](https://docs.byteplus.com/en/docs/12/14190#preloadaudiomixing) or [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing).

* **Parameters**

   * **id**

      Type: `number`

      Mix ID

* **Return Value**

   Type: `number`

   * `> 0`: Success, audio file duration, in milliseconds.

   * `< 0`: Failure


<span id="getaudiomixingcurrentposition"></span>
### getAudioMixingCurrentPosition  

Get audio file playback progress


* **Type**

   ```ts
   (id: number) => number
   ```
   

* **Notes**

   Before calling this method to get the audio file playback progress, you need to call [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing) to start playing the audio file.

* **Parameters**

   * **id**

      Type: `number`

      Mix ID

* **Return Value**

   Type: `number`

   * `> 0`: Success, audio file playback progress, in milliseconds.

   * `< 0`: Failed


<span id="setaudiomixingposition"></span>
### setAudioMixingPosition  

Set the starting playback position of the audio file


* **Type**

   ```ts
   (id: number, position: number) => void
   ```
   

* **Notes**

   * This method allows you to play an audio file from a specified position as appropriate, without having to play an audio file in its entirety from the beginning to finish.

   * Before calling this method to set the playback position of the audio file, you need to call [startAudioMixing](https://docs.byteplus.com/en/docs/12/14190#startaudiomixing) to start playing the audio file.

* **Parameters**

   * **id**

      Type: `number`

      Mixing ID

   * **position**

      Type: `number`

      The starting playback position of the audio file in milliseconds.

      Call [getAudioMixingDuration](https://docs.byteplus.com/en/docs/12/14190#getaudiomixingduration) to get the duration of the audio file. The value of `position` must not be greater than the duration of the audio file.


<span id="setaudioframecallback"></span>
### setAudioFrameCallback  

Toggle the callbacks carrying the mixing audio frames.


* **Type**

   ```ts
   (id: number, callback?: ((data: AudioFrameData) => void) | undefined, frameSize?: number) => void
   ```
   

* **Parameters**

   * **id**

      Type: `number`

      Audio from microphone or device audio.

      You will get the callback carrying the audio data as soon as the audio mixing starts.

   * **callback**

      Type: `((data: `[AudioFrameData](https://docs.byteplus.com/en/docs/12/docs-104481#audioframedata)`) => void) | undefined`

      The callback function to receive the audio frames. An empty value indicates disabling the callback.

      When the user disconnects, the audio data is empty.

   * **frameSize**

      Type: `number | undefined`

      The number of samples per frame. The interval between callbacks increases as the frameSize gets larger.

      It can be set to 256, 512, 1024, 2048, 4096, 8192, or 16384. It defaults to 4096. We recommend using the default value unless the application where the audio frames to be used requires a specific size.


<span id="enableaudiomixingbuffer"></span>
### enableAudioMixingBuffer  

Start PCM mixing.

To mix multiple PCM audio data, call this API multiple times with different ids.


* **Type**

   ```ts
   (type: AudioMixingType) => void
   ```
   

* **Notes**

   * After this API is called, you must call [pushAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/14190#pushaudiomixingbuffer) to start mixing.

   * To end PCM mixing, use [disableAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/14190#disableaudiomixingbuffer).

* **Parameters**

   * **type**

      Type: [AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-104481#audiomixingtype)

      Mixing type.

      Whether the PCM data is mixed locally and sent to the remotes.


<span id="disableaudiomixingbuffer"></span>
### disableAudioMixingBuffer  

Disable PCM mixing.


* **Type**

   ```ts
   () => void
   ```
   


<span id="pushaudiomixingbuffer"></span>
### pushAudioMixingBuffer  

Push PCM audio frame data for mixing


* **Type**

   ```ts
   (buffer: AudioBuffer) => void
   ```
   

* **Notes**

   Before calling this method, you must start the external audio stream mixing through [enableAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/14190#enableaudiomixingbuffer).

* **Parameters**

   * **buffer**

      Type: `AudioBuffer`

      Refer to [Browser documentation](https://developer.mozilla.org/en-US/docs/Web/API/AudioBuffer)
