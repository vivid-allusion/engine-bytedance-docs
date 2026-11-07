---
title: "Keytype"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104481"
---

## MixOption

Type: `interface`

Mixing configuration

playCount

Type: `number`

Mix playback times

* Play_count < = 0: Infinite loop

* Play_count == 1: Play once (default)

* Play_count \> 1: Play play_count times

type

Type: [AudioMixingType](https://docs.byteplus.com/en/docs/12/14193#audiomixingtype)` | undefined`

For mixing playback types.

## AudioMixingType

Type: `enum`

Mixing type

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |PLAYOUT |`0` |Played at the local device only |
   |PUBLISH |`1` |Sent to the remote devices only |
   |PLAYOUT_AND_PUBLISH |`2` |Played at the local device and sent to the remote devices. |

## AudioFrameData

Type: `interface`

Audio frames struct

channels

Type: `Float32Array[]`

Audio data in PCM format

channelCount

Type: `number`

The number of channels

sampleRate

Type: `number`

Sample rate in Hz.

## PlayerEvent

Type: `interface`

Event related to the player

type

Type: `"video" | "audio"`

Type of the player

eventName

Type: `string`

Event name

rawEvent

Type: `Event`

Play event. Refer to the [official documentation](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/play_event) for more details.

userId

Type: `string`

userId of the user who is joining the room

publicStreamId

Type: `string | undefined`

The WTN stream's ID.

readyState

Type: `number`

Ready state of the media. Refer to the [official documentation](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/readyState)

currentTime

Type: `number`

The current time

isScreen

Type: `boolean | undefined`

Whether it is a screen\-sharing stream

playerId

Type: `string | undefined`

Player ID. An empty value indicates the default player.

## onUserJoinedEvent

Type: `interface`

A user joins the room

userInfo

Type: [UserInfo](https://docs.byteplus.com/en/docs/12/14193#userinfo)

userId of the user who is joining the room

publishState

Type: [InitPublishState](https://docs.byteplus.com/en/docs/12/14193#initpublishstate)

The publish state of the media stream.

## UserInfo

Type: `interface`

User information.

userId

Type: `string`

User ID. A non\-empty string within 128 bytes.

extraInfo

Type: `string | undefined`

The additional information of the user, with a maximum length of 200 bytes. Remote users will receive the [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined).

* **Notes**

   The supported character types are as follows:

   * Uppercase letters: A~ Z

   * Lowercase letters: a~ z

   * Numbers: 0~ 9

   * Symbols: underscore "_"; at sign "@"; minus sign "\-"

## InitPublishState

Type: `interface`

Initial publish state

audio

Type: `boolean`

Microphone audio

video

Type: `boolean`

Video stream captured by cameras

screenAudio

Type: `boolean`

Device audio

screenVideo

Type: `boolean`

Screen recording

## onUserLeaveEvent

Type: `interface`

A user leaves the room

userInfo

Type: [UserInfo](https://docs.byteplus.com/en/docs/12/14193#userinfo)

User information

reason

Type: [UserOfflineReason](https://docs.byteplus.com/en/docs/12/14193#userofflinereason)

The reason why the remote user left the room

## UserOfflineReason

Type: `enum`

The reason why the remote user left the room

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |QUIT |`0` |The remote client calls leaveRoom to leave the room. |
   |DROPPED |`1` |The remote client is disconnected because of poor network connection or expired Token. |
   |SWITCH_TO_INVISIBLE |`2` |The remote client calls `setUserVisibility` to turn invisible. |
   |KICKED_BY_ADMIN |`3` |The remote user has been removed from the room by the administrator via an OpenAPI call. |

## ConnectionStateChangeEvent

Type: `interface`

The connection state changes.

state

Type: [ConnectionState](https://docs.byteplus.com/en/docs/12/14193#connectionstate)

The internal connection state

## ConnectionState

Type: `enum`

SDK Connection state with the signaling server.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |CONNECTION_START |`0` |Occupy related resources and get ready to start connecting. |
   |CONNECTION_STATE_DISCONNECTED |`1` |Disconnected. |
   |CONNECTION_STATE_CONNECTING |`2` |Connecting of the first connection |
   |CONNECTION_STATE_CONNECTED |`3` |Completion of the first connection |
   |CONNECTION_STATE_RECONNECTING |`4` |Reconnecting after a disconnection |
   |CONNECTION_STATE_RECONNECTED |`5` |Completion of the reconnecting |
   |CONNECTION_STATE_LOST |`6` |The `CONNECTION_STATE_DISCONNECTED` status lasted for more than 10 seconds, during which the SDK failed to reconnect. The SDK will continue to try to reconnect. |

## MediaType

Type: `enum`

Media stream type

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |AUDIO |`1` |Controls audio only |
   |VIDEO |`2` |Controls video only |
   |AUDIO_AND_VIDEO |`3` |Controls both audio and video |

## StreamRemoveReason

Type: `enum`

The reason for the removal of the remote stream in the room.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |STREAM_REMOVE_REASON_UNPUBLISH |`0` |The remote user stops publishing the stream. |
   |STREAM_REMOVE_REASON_PUBLISH_FAILED |`1` |The remote user failed to publish the stream. |
   |STREAM_REMOVE_REASON_KEEP_LIVE_FAILED |`2` |Keep alive failed. |
   |STREAM_REMOVE_REASON_CLIENT_DISCONNECTED |`3` |The remote user is disconnected. |
   |STREAM_REMOVE_REASON_REPUBLISH |`4` |The remote user republishes the stream. |
   |STREAM_REMOVE_REASON_OTHER |`5` |Other reasons. |
   |STREAM_REMOVE_REASON_TOKEN_PRIVILEGE_EXPIRED |`6` |The token loses the publish privilege. |

## onVideoFirstFrameRenderedEvent

Type: `interface`

The first video frame shown on the screen

userId

Type: `string`

User ID of the user who published the video stream.

height

Type: `number`

Height

width

Type: `number`

Width

isScreen

Type: `boolean`

If this event comes from a screen video stream

playerId

Type: `string | undefined`

Player ID. An empty value indicates the default player.

This property does not apply to the WTN stream.

## onAudioFirstFrameDecodedEvent

Type: `interface`

Event related to the decoder of the first audio frame

userId

Type: `string`

userId of the user who published the audio stream

isScreen

Type: `boolean`

Whether this event comes from screen sharing.

## DeviceInfo

Type: `interface`

Information and state of a media device.

mediaDeviceInfo

Type: `MediaDeviceInfo`

Information of a media device. See [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo).

deviceState

Type: `"active" | "inactive"`

Device state.

## UserMessageEvent

Type: `interface`

Point\-to\-point text message

userId

Type: `string`

The user who sent the message

message

Type: `string`

Point\-to\-point text message

## UserBinaryMessageEvent

Type: `interface`

Point\-to\-point binary message

userId

Type: `string`

The user who sent the message

message

Type: `ArrayBuffer`

Point\-to\-point binary message

## RemoteStreamStats

Type: `interface`

Information of the remote media stream

userId

Type: `string`

userId of the user who is joining the room

audioStats

Type: [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/14193#remoteaudiostats)

State of the remote audio stream

videoStats

Type: [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/14193#remotevideostats)

State of the remote video stream

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream

txQuality

Type: `number | undefined`

Quality of the transmitting stream

rxQuality

Type: `number | undefined`

Quality of the receiving stream

## RemoteAudioStats

Type: `interface`

State of the remote audio stream

audioLossRate

Type: `number`

Loss rate of the audio packets

receivedKBitrate

Type: `number`

Bitrate of receiving

stallCount

Type: `number | undefined`

Number of video stalls

stallDuration

Type: `number | undefined`

Duration of a video stall

totalRtt

Type: `number`

The round\-trip transmission time delay in ms.

* **Notes**

   For Firefox, the value is not accurate.

statsInterval

Type: `number`

Interval of each report of states

rtt

Type: `number`

Round trip time, unit: ms

jitterBufferDelay

Type: `number`

Jitter buffer delay, unit: ms

numChannels

Type: `number`

Number of channels

receivedSampleRate

Type: `number`

Sample rate of the received stream

concealedSamples

Type: `number`

Concealed samples

concealmentEvent

Type: `number`

Concealment events

## RemoteVideoStats

Type: `interface`

Information of the remote video stream

width

Type: `number`

Width

height

Type: `number`

Height

videoLossRate

Type: `number`

Loss rate of the video packages

receivedKBitrate

Type: `number`

Bitrate of the received video stream

decoderOutputFrameRate

Type: `number`

Frame rate of decoding

stallCount

Type: `number | undefined`

Number of video stalls

stallDuration

Type: `number | undefined`

Duration of a video stall

totalRtt

Type: `number`

The round\-trip transmission time delay in ms.

* **Notes**

   For Firefox, the value is not accurate.

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream

statsInterval

Type: `number`

Interval of each stat report.

rtt

Type: `number`

Round trip time, unit: ms

codecType

Type: `"H264" | "VP8"`

Video codec.

"H264": H.264 video codec.

"VP8": VP8 video codec.

## LocalStreamStats

Type: `interface`

State of the local media stream

audioStats

Type: [LocalAudioStats](https://docs.byteplus.com/en/docs/12/14193#localaudiostats)

State of the local audio stream

videoStats

Type: [LocalVideoStats](https://docs.byteplus.com/en/docs/12/14193#localvideostats)

State of the local video stream

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream

## LocalAudioStats

Type: `interface`

State of the local audio stream

audioLossRate

Type: `number`

Audio loss rate

sendKBitrate

Type: `number`

Bitrate of sending, unit: kbps

recordSampleRate

Type: `number`

Sample rate of audio capturing

statsInterval

Type: `number`

Interval of each stat report

rtt

Type: `number`

Round trip time, unit: ms

numChannels

Type: `number`

number of the signal channels

## LocalVideoStats

Type: `interface`

Local video states

sentKBitrate

Type: `number`

Bitrate of sending, unit: kbps

sentFrameRate

Type: `number`

Frame rate of sending

encoderOutputFrameRate

Type: `number`

Width of the encoded video frame

rendererOutputFrameRate

Type: `number | undefined`

Frame rate of rendering

statsInterval

Type: `number`

Interval of each stat report

videoLossRate

Type: `number`

Loss rate of video package

rtt

Type: `number`

Round trip time, unit: ms

encodedFrameWidth

Type: `number`

Width of the encoded video frame

encodedFrameHeight

Type: `number`

Height of the encoded video frame

encodedFrameCount

Type: `number`

Number of encoded frames

codecType

Type: `"H264" | "VP8"`

Video codec.

"H264": H.264 video codec.

"VP8": VP8 video codec.

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream

## PublicStreamStats

Subscribed WTN stream's statistics and network condition, reference period 2s.

* **Type**

   ```ts
   Omit<
     RemoteStreamStats,
     'userId' | 'isScreen'
   > & {
     publicStreamId: string;
   }
   ```

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |publicStreamId |`string` |The WTN stream's ID. |
   |RemoteStreamStats |[RemoteStreamStats](https://docs.byteplus.com/en/docs/12/14193#remotestreamstats) |Remote stream stats |

## LocalStatsException

Type: `interface`

Exception of local media stream information. Possible values, see the `Exception Message` column in [RTCExceptionCodeMap](https://docs.byteplus.com/en/docs/12/14193#rtcexceptioncodemap).

exception

Type: `string`

Exception of local media stream information.

code

Type: `number`

Exception code of local media stream. Possible values, see the `Exception code` column in [RTCExceptionCodeMap](https://docs.byteplus.com/en/docs/12/14193#rtcexceptioncodemap).

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream: true\-screen stream, false\-main stream

## RemoteStatsException

Type: `interface`

Exception of remote media stream information

userId

Type: `string`

The ID of the remote user who experienced an exception

exception

Type: `string`

Exception of remote media stream information. Possible values, see the `Exception Message` column in [RTCExceptionCodeMap](https://docs.byteplus.com/en/docs/12/14193#rtcexceptioncodemap).

code

Type: `number`

Exception code of remote media stream. Possible values, see the `Exception Code` column in [RTCExceptionCodeMap](https://docs.byteplus.com/en/docs/12/14193#rtcexceptioncodemap).

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream: true\-screen stream, false\-main stream

## LocalAudioPropertiesInfo

Type: `interface`

Information about local audio

streamIndex

Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/14193#streamindex)

Indicates whether the audio is captured by microphone or from screen sharing.

audioPropertiesInfo

Type: [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14193#audiopropertiesinfo)

Audio information

## StreamIndex

Type: `enum`

Stream specification

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |STREAM_INDEX_MAIN |`0` |A mainstream is a media stream either captured by the internal module or from the custom source. |
   |STREAM_INDEX_SCREEN |`1` |Screen\-sharing stream, including screen\-sharing video streams and/ or audio streams from sound cards |

## AudioPropertiesInfo

Type: `interface`

Audio information

linearVolume

Type: `number`

linear volume. The value is in linear relation to the original volume. The higher the value, the higher the volume. The range is [0,255].

* [0, 25]: Nearly silent

* [26, 75]: Low volume

* [76, 204]: Medium volume

* [205, 255]: High volume

nonlinearVolume

Type: `number`

non\-linear volume in dB. The value is in proportion to the log value of the original volume. You can use the value to recognize the Active Speaker in the room. The range is [\-127, 0].

* [\-127, \-60]: Nearly silent

* [\-59, \-40]: Low volume

* [\-39, \-20]: Medium volume

* [\-19, 0]: High volume

## RemoteAudioPropertiesInfo

Type: `interface`

Information about remote audio

streamKey

Type: [StreamKey](https://docs.byteplus.com/en/docs/12/14193#streamkey)

Information about remote stream

audioPropertiesInfo

Type: [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14193#audiopropertiesinfo)

Information about remote audio properties

## StreamKey

Type: `interface`

Information about the remote stream

roomId

Type: `string`

ID of the room from which the stream is published.

userId

Type: `string`

ID of the user who publishes the stream.

streamIndex

Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/14193#streamindex)

Indicates whether the audio is captured by microphone or from screen sharing.

## onSEIMessageEvent

Type: `interface`

Receiving video frames carrying SEI message

remoteStreamKey

Type: [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/14193#remotestreamkey)

Including userId of the user who sent the message, roomId of the current room, and the media stream carrying this SEI message.

sei

Type: `Uint8Array`

SEI message received

## RemoteStreamKey

Type: `interface`

Information of the remote stream

roomId

Type: `string`

Room ID

userId

Type: `string`

User ID

streamIndex

Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/14193#streamindex)

Mainstream or screen\-sharing stream.

## onSEIStreamUpdateEvent

Type: `interface`

Stream containing SEI information update event.

userId

Type: `string`

User ID.

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream.

type

Type: [SEIStreamEventType](https://docs.byteplus.com/en/docs/12/14193#seistreameventtype)

The stream type containing SEI information.

## SEIStreamEventType

Type: `enum`

The stream type containing SEI information.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |BLACK |`0` |A black frame video stream is published from the remote user.<br><br>In the voice call scenario, when a remote user sends SEI data by calling [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage), the SDK will publish a black frame video stream and trigger this callback. |
   |NORMAL |`1` |The black frame video stream is removed. The triggers for this callback include:<br><br><br> <br><br>* When the remote user starts camera capture, switching from voice call to video call, the black frame video stream stops publishing.<br><br>* When the remote user calls [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setvideosourcetype) to switch to custom video capture, black frame video stream stops publishing.<br><br>* If no SEI data is sent within 1 minute after the remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage), the black frame video stream stops publishing. |

## SubscribeState

Type: `enum`

Result of updating subscription

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |SUBSCRIBE_SUCC |`0` |Update subscription successfully. |
   |SUBSCRIBE_FAIL |`1` |Update subscription failed. |

## PublishState

Type: `enum`

Result of publishing

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |PUBLISH_SUCC |`0` |Publish successfully. |
   |PUBLISH_FAIL |`1` |Publish failed. |

## AutoPlayFailedEvent

Type: `interface`

Event of Auto\-play failure

userId

Type: `string`

ID of the user whose stream failed to playback automatically. Without this parameter, the notification is about the local stream.

kind

Type: `"video" | "audio"`

Type of the media which failed to play automatically

For example, when both audio and video streams from the same user failed to playback automatically, you would get notified by `onAutoPlayFailed` twice with the argument of `audio` and `video` respectively.

streamIndex

Type: [StreamIndex](https://docs.byteplus.com/en/docs/12/14193#streamindex)

The attributes of the screen\-sharing stream.

mediaType

Type: `MediaType.AUDIO | MediaType.VIDEO`

Remote stream type

playerId

Type: `string | undefined`

Player ID. An empty value indicates the default player.

position

Type: [EarMonitorPosition](https://docs.byteplus.com/en/docs/12/14193#earmonitorposition)` | undefined`

Whether the ear monitor is enabled. And whether the in\-ear monitoring audio is processed.

## EarMonitorPosition

Type: `enum`

The preference for the quality of the subscribed stream.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |NONE |`0` |Disables the ear monitor. |
   |AFTER_CAPTURE |`1` |Plays the local audio without any processing and audio mixing. |
   |AFTER_PROCESS |`2` |Plays the local audio after processing, without audio mixing. |

## AudioMixingStateChangedEvent

Type: `interface`

Event of the state change of audio mixing

mixId

Type: `number`

Audio mixing ID

state

Type: [AudioMixingState](https://docs.byteplus.com/en/docs/12/14193#audiomixingstate)

State of the audio mixing

error

Type: [AudioMixingError](https://docs.byteplus.com/en/docs/12/docs-104480#audiomixingerror)

Error of the audio mixing

## AudioMixingState

Type: `enum`

Audio mix file playback status.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |AUDIO_MIXING_STATE_PRELOADED |`0` |Mix loaded |
   |AUDIO_MIXING_STATE_PLAYING |`1` |Mix is playing |
   |AUDIO_MIXING_STATE_PAUSED |`2` |Mix paused |
   |AUDIO_MIXING_STATE_STOPPED |`3` |Mixing stopped |
   |AUDIO_MIXING_STATE_FAILED |`4` |Mix playback failed |
   |AUDIO_MIXING_STATE_FINISHED |`5` |End of mixing |
   |AUDIO_MIXING_STATE_PCM_ENABLED |`6` |Prepare PCM Mix |
   |AUDIO_MIXING_STATE_PCM_DISABLED |`7` |End of PCM mix playback |

## CloudProxyConnectedEvent

Type: `interface`

SDK successfully connected to the cloud proxy server event.

interval

Type: `number`

The time interval to join the channel after SDK turned on cloud proxy.

## PublicStreamResultEvent

Type: `interface`

The result of publishing the WTN stream.

code

Type: `number`

Event number of publishing the WTN stream.

message

Type: `string`

Event details of publishing the WTN stream.

* `200`: Published or subscribed successfully.

* `1191`: Invalid parameter(s). Please revise the parameter(s) and retry.

* `1192`: Error for the task at the server side. The server will retry automatically.

* `1193`: Unrecoverable error of publishing the WTN stream. Please start the task again.

* `1195`: Failed to publish the WTN stream. The SDK will retry automatically, so you do not need to handle it.

* `1196`: Time\-out error of publishing the WTN stream. The SDK will retry in 10 s. The SDK will stop trying again after three failed attempts.

## PublicStreamSEIMessageEvent

Type: `interface`

The SEI carried by the public video stream.

publicStreamId

Type: `string`

The WTN stream's ID.

sei

Type: `Uint8Array`

SEI message.

## PublicStreamVideoFirstFrameDecodedEvent

Event related to decoding the first video frame of the WTN stream.

* **Type**

   ```ts
   Omit<
     onVideoFirstFrameDecodedEvent,
     'userId'
   > & {
     publicStreamId: string;
   }
   ```

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |publicStreamId |`string` |The WTN stream's ID. |
   |onVideoFirstFrameDecodedEvent |[onVideoFirstFrameDecodedEvent](https://docs.byteplus.com/en/docs/12/14193#onvideofirstframedecodedevent) |Event related to the decoding of the first video frame. |

## onVideoFirstFrameDecodedEvent

Type: `interface`

Event related to the decoder of the first video frame

userId

Type: `string`

User ID of the user who published the video stream

height

Type: `number`

Height

width

Type: `number`

Width

## PublicStreamAudioFirstFrameDecodedEvent

Type: `interface`

Event related to decoding or rendering the first video frame of the WTN stream.

publicStreamId

Type: `string`

The WTN stream's ID.

## NetworkQuality

Type: `enum`

Network quality.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |UNKNOWN |`0` |Unknown. |
   |EXCELLENT |`1` |The network quality is excellent. |
   |GOOD |`2` |The quality is good, but the bitrate is lower than Excellent. |
   |POOR |`3` |Users experience slightly impaired communication. |
   |BAD |`4` |Users can communicate with each other, but not smoothly. It is recommended to lower sampling rate, frame rate, or remind the user through UI to switch to a voice call. |
   |VBAD |`5` |Network quality is very bad, users can barely communicate. It is recommended to notify users of poor network connection through UI. |
   |DOWN |`6` |The call was terminated due to a network disconnection. |

## RemoteStreamSwitch

Type: `interface`

Information of stream switching due to a subscribed media stream fallback.

userId

Type: `string`

User Id of the remote publisher

isScreen

Type: `boolean`

Whether it is a screen\-sharing stream

beforeVideoIndex

Type: `number`

The index of original video stream

afterVideoIndex

Type: `number`

The index of current video stream

beforeEnable

Type: `boolean`

Whether it is a video stream before stream switching.

afterEnable

Type: `boolean`

Whether it is a video stream after stream switching.

reason

Type: [FallbackOrRecoverReason](https://docs.byteplus.com/en/docs/12/14193#fallbackorrecoverreason)

Reason for media stream fallback or recovery

## FallbackOrRecoverReason

Type: `enum`

The reason for media stream fallback or recovery

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |Unknown |`-1` |Default value. Other reasons. |
   |SubscribeFallbackByBandwidth |`0` |Subscribed media stream falls back due to low bandwidth. |
   |SubscribeRecoverByBandwidth |`2` |Subscribed media stream recovers from the fallback due to bandwidth increase. |

## StreamMixingEvent

Type: `interface`

Pushing a mixed stream to CDN events

event

Type: [StreamMixingEventType](https://docs.byteplus.com/en/docs/12/14193#streammixingeventtype)

The types.

error

Type: [StreamMixingEventErrorCode](https://docs.byteplus.com/en/docs/12/docs-104480#streammixingeventerrorcode)

The error codes.

message

Type: `string`

The detailed error messages.

## StreamMixingEventType

Type: `enum`

The types of pushing a mixed stream to CDN events.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |START |`1` |Request a start to push the mixed stream to CDN. |
   |START_SUCCESS |`2` |Success. |
   |START_FAILED |`3` |Failure. |
   |UPDATE |`4` |Request a configuration update. |
   |UPDATE_SUCCESS |`5` |Push the mixed stream after the configuration update. |
   |UPDATE_FAILED |`6` |Failed to update the configuration. |
   |STOP |`7` |Request a stop to push the mixed stream to CDN. |
   |STOP_SUCCESS |`8` |Pushing the mixed stream to CDN is stopped. |
   |STOP_FAILED |`9` |Fail to stop pushing the mixed stream to CDN. |

## VideoStreamBannedEvent

Type: `interface`

Event of banning/unbanning video streaming

uid

Type: `string`

The ID of the user who is banned/unbanned from publishing video stream

banned

Type: `boolean`

Video Streaming Status

true: Video streaming is banned

false: Video streaming is unbanned

## AudioStreamBannedEvent

Type: `interface`

Event of banning/unbanning audio streaming

uid

Type: `string`

The ID of the user who is banned/unbanned from publishing audio stream

banned

Type: `boolean`

Audio Streaming Status

true: Audio streaming is banned

false: Audio streaming is unbanned

## ForwardStreamStateInfo

Type: `interface`

Status information for forwarding media stream across rooms.

roomId

Type: `string`

The target room ID for forwarding media streams.

state

Type: [ForwardStreamState](https://docs.byteplus.com/en/docs/12/14193#forwardstreamstate)

Status information for forwarding media stream across rooms.

error

Type: [ForwardStreamError](https://docs.byteplus.com/en/docs/12/docs-104480#forwardstreamerror)

Forward stream error code.

## ForwardStreamState

Type: `enum`

Status information for forwarding media stream across rooms.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |FORWARD_STREAM_STATE_SUCCESS |`0` |Success. |
   |FORWARD_STREAM_STATE_FAILURE |`1` |Failure. |

## PlayerVisibility

Type: `interface`

Player visibility status and related information (e.g., user ID, media type, stream index, etc.).

descriptor

Type: `{ userId?: string | undefined; mediaType: MediaType.VIDEO; streamIndex?: `[StreamIndex](https://docs.byteplus.com/en/docs/12/14193#streamindex)` | undefined; streamId?: string | undefined; playerId?: string | undefined; }`

Player descriptor information, which contains identification information like user ID, media type, stream index.

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |userId |`string \| undefined` |User ID that identifies the publisher of the stream. |
   |mediaType |`MediaType.VIDEO` |Media type, currently only supports video type. |
   |streamIndex |`StreamIndex \| undefined` |Stream index, used to distinguish between main stream and screen sharing stream. |
   |streamId |`string \| undefined` |Stream ID that uniquely identifies a media stream. |
   |playerId |`string \| undefined` |Player ID that uniquely identifies a player instance. |

status

Type: [VisibilityStatus](https://docs.byteplus.com/en/docs/12/14193#visibilitystatus)`[]`

Array of player visibility statuses, which contains all current visibility statuses of the player.

## VisibilityStatus

Type: `enum`

Player visibility status and reasons for invisibility.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |PLAYER_VISIBLE |`'visible'` |Player is visible. |
   |PLAYER_INVISIBLE_BY_UNMOUNT |`'unmount'` |Player is invisible due to unmounting from the DOM. |
   |PLAYER_INVISIBLE_BY_SIZE |`'size'` |Player is invisible due to size issues (for example, if the size is too small). |
   |PLAYER_INVISIBLE_BY_STYLE |`'style'` |Player is invisible due to style issues. For example: `display: none`, `opacity: 0`. |
   |PLAYER_INVISIBLE_BY_POSITION |`'position'` |Player is invisible due to position issues (for example, if the position is outside the visible area). |
   |PLAYER_INVISIBLE_BY_COVERED |`'covered'` |Player is invisible due to being covered. |

## RoomConfig

Type: `interface`

Room configurations.

isAutoPublish

Type: `boolean | undefined`

Enable/disable auto\-subscribe audio. Enabled by default.

This does not include the screen stream.

Call [publishStream](https://docs.byteplus.com/en/docs/12/docs-104478#publishstream) to publish media streams if you disable `isAutoPublish`.

isAutoSubscribeAudio

Type: `boolean | undefined`

Enable/disable auto\-subscribe audio. Enabled by default.

This does not include the screen stream.

You can call [subscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#subscribestream) and [unsubscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#unsubscribestream) to revise the subscription after entering the room.

isAutoSubscribeVideo

Type: `boolean | undefined`

Enable/disable auto\-subscribe video. Enabled by default.

This does not include the screen stream.

You can call [subscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#subscribestream) and [unsubscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#unsubscribestream) to revise the subscription after entering the room.

remoteVideoConfig

Type: [RemoteVideoConfig](https://docs.byteplus.com/en/docs/12/14193#remotevideoconfig)` | undefined`

Expected configuration of remote video stream.

roomMode

Type: [RoomMode](https://docs.byteplus.com/en/docs/12/14193#roommode)` | undefined`

Room creation mode. You can create a room that supports both RTC and RTS functions, or a room that only supports RTS functions.

## RemoteVideoConfig

Type: `interface`

Configuration of remote video stream

width

Type: `number`

Width of the video frame in px

height

Type: `number`

Height of the video frame in px

## RoomMode

Type: `enum`

Room mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |ROOM_MODE_RTC |`0` |Default setting. Both RTC and RTS features can be used in the room. |
   |ROOM_MODE_RTS_ONLY |`1` |Only RTS features can be used in the room. In this mode, RTC\-related interfaces cannot be called. |

## ScreenConfig

Type: `interface`

Configuration for screen\-sharing stream

enableAudio

Type: `boolean | undefined`

Whether to display the enable audio option when sharing screen.

• On Windows, you can share the system audio through sharing the entire screen, and share audio from a tab through sharing a Chrome tab.

• On macOS, you can only share audio from a tab through sharing a Chrome tab.

displaySurface

Type: `"monitor" | "browser" | "window" | undefined`

The type of display surface (window, browser, or monitor)

For Chrome 107, Edge 107, and later versions

See [displaySurface](https://developer.chrome.com/docs/web-platform/screen-sharing-controls/#displaySurface).

systemAudio

Type: `"include" | "exclude" | undefined`

Whether to include the system audio

`include`：(Default) Include.

`exclude`：Exclude.

For Chrome 107, Edge 107, and later versions on Windows.

For Electron app, only support sharing the system audio on Windows.

See [systemAudio](https://developer.chrome.com/docs/web-platform/screen-sharing-controls/#systemAudio).

surfaceSwitching

Type: `"include" | "exclude" | undefined`

Whether to allow the user to dynamically switch the shared tab during screen\-sharing.

`include`: (Default) Allow.

`exclude`: Disallow.

For Chrome 107, Edge 107, and later versions

See [surfaceSwitching](https://developer.chrome.com/docs/web-platform/screen-sharing-controls/#surfaceSwitching).

selfBrowserSurface

Type: `"include" | "exclude" | undefined`

Whether to allow the user to select the current tab for capture.

`include`: (Default) Allow.

`exclude`: Disallow.

For Chrome 107, Edge 107, and later versions

See [selfBrowserSurface](https://developer.chrome.com/docs/web-platform/screen-sharing-controls/#selfBrowserSurface).

sourceId

Type: `string | undefined`

The ID of the object to be shared during screen\-sharing in Electron.

You can get the ID from [getElectronScreenSources](https://docs.byteplus.com/en/docs/12/docs-104478#getelectronscreensources).

If you don't specify this parameter, the SDK will pop up a default selection box for the user to select the screen\-sharing source.

## VideoPlayerOption

Type: `interface`

Player information and rendering mode

renderDom

Type: `string | HTMLElement | undefined`

Render window, as the parent element for video rendering. Video's `htmlVideoElement` will be attached under this parent element for rendering, and the width and height of the rendered video will be based on `renderDom`, and it determines whether to completely fill the entire area of the parent element depending on the rendering mode.

renderMode

Type: [VideoRenderMode](https://docs.byteplus.com/en/docs/12/14193#videorendermode)` | undefined`

Rendering mode.

userId

Type: `string`

User ID, a non\-empty string within 128 bytes. Use the following character set ranges

* 26 uppercase letters A~ Z

* 26 lowercase letters a~ z

* 10 numbers 0~ 9

* underscore "_", at character "@", minus, number "\-"

   This property does not apply to the WTN stream.

rotation

Type: `number | undefined`

The clockwise rotation angle of the video frame, which can be set to 0, 90, 180, 270. The default value is 0, which means no rotation is applied.

This parameter only applies to remote video. Setting this parameter will not take effect when calling [setLocalVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setlocalvideoplayer).

playerId

Type: `string | undefined`

Player ID. An empty value indicates the default player.

This property does not apply to the WTN stream.

## VideoRenderMode

Type: `enum`

Rendering modes

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |RENDER_MODE_HIDDEN |`0` |(Default value for main stream) Fills the entire window with the video frame.<br><br>The video frame is scaled until the window is filled. If the video frame's aspect ratio is different from that of the window, the extra part of the video frame will be cropped. |
   |RENDER_MODE_FIT |`1` |(Default value for screen\-sharing stream) Makes the entire video frame fit within the window while maintaining the video frame's original aspect ratio.<br><br>There may be empty space at the margins of the window. |
   |RENDER_MODE_FILL |`2` |Stretch the video frame until the window is filled.<br><br>The video frame's aspect ratio can be changed as it is automatically stretched to fill the window. |

## MirrorType

Type: `enum`

Whether to enable the mirror effect when rendering the video.

You cannot use mirror effect during transmission and encoding due to the restrictions of web browsers.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |MIRROR_TYPE_NONE |`0` |No mirroring effect |
   |MIRROR_TYPE_RENDER |`1` |Enable mirror effect for the videos. |

## VideoEncoderConfig

Type: `interface`

The video encoding configuration.

width

Type: `ConstrainULong`

Video width in pixels. The default value is 640 px.

The input can be a number or a [ConstrainULong](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#constrainulong).

height

Type: `ConstrainULong`

Video height in pixels. The default value is 480 px.

The input can be a number or a [ConstrainULong](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#constrainulong).

frameRate

Type: `ConstrainDouble`

Video framerate in FPS. The default value is 15 FPS.

The input can be a number or a [ConstrainDouble](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#constraindouble).

maxKbps

Type: `number`

The maximum bitrate in Kbps (\>0). The default value is 600 Kbps.

contentHint

Type: `"text" | "motion" | "detail" | undefined`

The type of content the track contains.

`'text'`: The track should be treated as if video details are extra important, and that significant sharp edges and areas of consistent color can occur frequently. For example, presentations or web pages with text content.

`'motion'`: The track should be treated as if it contains video where motion is important. For example, webcam video, movies or video games.

`'detail'`: The track should be treated as if video details are extra important. For example, presentations or web pages with text content, painting or line art.

* **Notes**

   This property is not supported on Firefox. See [contentHint browser compatibility](https://caniuse.com/?search=contentHint).

preferCodecName

Type: [VideoCodecType](https://docs.byteplus.com/en/docs/12/14193#videocodectype)` | undefined`

The preferred codec for the video stream. The default value is `'auto'`, no preference. By default, the SDK will automatically match the best codec based on the current video resolution and device performance.

## VideoCodecType

Type: `enum`

Video codec type.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |AUTO |`'auto'` |Not specified. The SDK will automatically match the best codec based on the current video resolution and device performance. |
   |H264 |`'h264'` |H.264 |
   |VP8 |`'vp8'` |VP8 |
   |H265 |`'h265'` |H.265 |

## ScreenEncoderConfig

Type: `interface`

The encoding configuration of the screen\-sharing stream.

width

Type: `ConstrainULong`

Video width in pixels. The default value is 1920 px.

The input can be a number or a [ConstrainULong](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#constrainulong).

height

Type: `ConstrainULong`

Video height in pixels. The default value is 1080 px.

The input can be a number or a [ConstrainULong](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#constrainulong).

frameRate

Type: `ConstrainDouble`

Video framerate in FPS. The default value is 15 FPS.

The input can be a number or a [ConstrainDouble](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints#constraindouble).

maxKbps

Type: `number`

The maximum bitrate in Kbps (\>0). The default value is 3000 Kbps.

contentHint

Type: `"text" | "motion" | "detail" | undefined`

The type of content the track contains.

`'text'`: The track should be treated as if video details are extra important, and that significant sharp edges and areas of consistent color can occur frequently. For example, presentations or web pages with text content.

`'motion'`: The track should be treated as if it contains video where motion is important. For example, webcam video, movies or video games.

`'detail'`: The track should be treated as if video details are extra important. For example, presentations or web pages with text content, painting or line art.

* **Notes**

   This property is not supported on Firefox. See [contentHint browser compatibility](https://caniuse.com/?search=contentHint).

## SimulcastStreamType

Type: `enum`

The preference for the quality of the subscribed stream.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |VIDEO_STREAM_HIGH |`'high'` |High quality. |
   |VIDEO_STREAM_MID |`'mid'` |Medium quality. |
   |VIDEO_STREAM_LOW |`'low'` |Low quality. |

## VideoSimulcastMode

Type: `enum`

Multiple quality streams

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |VIDEO_ONLY_ONE |`0` |Single. The video stream is sent in only set of specification. |
   |VIDEO_ON_DEMAND |`1` |On\-demand. The publisher will publish streams according to the subscriber's demands. When no subscription preference is taking effect, 2 streams will be published. |
   |VIDEO_ALWAYS_SIMULCAST |`2` |Simulcast. The publisher will publish streams in the qualities of the settings. The default is to publish 2 streams. |

## AudioPropertiesConfig

Type: `interface`

Configuration related to audio information prompt.

interval

Type: `number | undefined`

Prompt interval in ms, the default value is 100.

* `≤0`: Turn off prompt.

* `(0,100)`: Invalid interval value, and will be automatically reset to 100ms.

* `≥100`: Enable prompt and set the prompt interval to the set value.

enableInBackground

Type: `boolean | undefined`

Whether to keep audio information prompt on when you are not on the video/audio call webpage. The default setting is `true`.

* true: Keep the prompt on

* false: Disable the prompt

localMainReportMode

Type: [LocalMainReportMode](https://docs.byteplus.com/en/docs/12/14193#localmainreportmode)` | undefined`

Audio callback mode of local main stream.

audioReportMode

Type: [AudioReportMode](https://docs.byteplus.com/en/docs/12/14193#audioreportmode)` | undefined`

The data range of the local main stream audio callback. It controls whether the callback includes mixed audio.

## LocalMainReportMode

Type: `enum`

Audio callback mode of local main stream.

This feature affects the callback [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-104479#onactivespeaker). For example, if [LocalMainReportMode](https://docs.byteplus.com/en/docs/12/14193#localmainreportmode) is set to `RESET` when the local main stream is unpublished, the callback will never include the local user's main stream audio.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |NORMAL |`0` |(Default) When the local main stream exists, the callback is always enabled. |
   |DISCONNECT |`1` |When the local main stream is unpublished, the callback is disabled. However, once it is published, the callback function will return the actual volume value. |
   |RESET |`2` |When the local main stream is unpublished, the callback function will return a fixed volume value of 0. However, once it is published, the callback function will return the actual volume value. |

## AudioReportMode

Type: `enum`

The data range of the local main stream audio callback. It controls whether the callback includes mixed audio.

This feature affects the callback [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-104479#onactivespeaker). For example, if [AudioReportMode](https://docs.byteplus.com/en/docs/12/14193#audioreportmode) is set to `AUDIOMIXING`, the callback may still include the local user's main stream audio even with zero microphone volume.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |MICROPHONE |`0` |(Default) The microphone audio or the audio before mixing. |
   |AUDIOMIXING |`1` |The audio after mixing. |

## LiveTranscodeConfig

Type: `interface`

Configurations to be set when pushing media streams to CDN.

url

Type: `string`

The URL for live transcoding. Only supports live transcoding via RTMP. The URL should match the regular expression `/^rtmps?:\/\//`.

This parameter cannot be updated while pushing stream to the CDN.

audio

Type: `Partial<`[LiveTranscodeAudioConfig](https://docs.byteplus.com/en/docs/12/14193#livetranscodeaudioconfig)`> | undefined`

Audio transcoding configurations.

These parameters cannot be updated while pushing stream to the CDN.

video

Type: `Partial<`[LiveTranscodeVideoConfig](https://docs.byteplus.com/en/docs/12/14193#livetranscodevideoconfig)`> | undefined`

Video transcoding configurations.

layout

Type: `Partial<`[LiveTranscodeLayoutConfig](https://docs.byteplus.com/en/docs/12/14193#livetranscodelayoutconfig)`> | undefined`

User layout information.

## LiveTranscodeAudioConfig

Type: `interface`

Audio transcoding configurations. With invalid or empty input, the configurations will be set as the default values.

codec

Type: `"AAC" | undefined`

Audio coding standard. Optional. The default value is `AAC`.

kBitRate

Type: `number`

The bitrate (Kbps) in the range of [32, 192]. Defaults to 64 Kbps.

sampleRate

Type: `number`

The sample rate (Hz). Supported sample rates: 32,000Hz, 44,100Hz, 48,000Hz. Defaults to 48,000Hz.

channels

Type: `number`

The number of channels. Supported channels: 1 (single channel), 2 (dual channel). Defaults to 2.

AACProfile

Type: [AAC_PROFILE](https://docs.byteplus.com/en/docs/12/14193#aac_profile)

AAC profile. Defaults to `LC`.

## AAC_PROFILE

Type: `enum`

Advanced Audio Coding (AAC) profile.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |LC |`'LC'` |(Default) AAC Low\-Complexity profile (AAC\-LC). |
   |HEv1 |`'HEv1'` |HE\-AAC v1 profile (AAC LC with SBR). |
   |HEv2 |`'HEv2'` |HE\-AAC v2 profile (AAC LC with SBR and Parametric Stereo). |

## LiveTranscodeVideoConfig

Type: `interface`

Video transcoding configurations. With invalid or empty input, the configurations will be set as the default values.

width

Type: `number`

The width (pixels) to be set. The range is [2, 1920], and the value must be an even number. The default value is 640 pixels.

If an odd number is set, the width will be adjusted to the next larger even number.

height

Type: `number`

The height (pixels) to be set. The range is [2, 1920], and the value must be an even number. The default value is 360 pixels.

If an odd number is set, the height will be adjusted to the next larger even number.

codec

Type: [TRANSCODING_VIDEO_CODEC](https://docs.byteplus.com/en/docs/12/14193#transcoding_video_codec)

The video codec. The default value is `H264`.

This parameter cannot be updated while pushing stream to the CDN.

fps

Type: `number`

The frame rate (FPS) in the range of [1, 60]. The default value is 15 FPS.

gop

Type: `number`

The time interval between I\-frames (second) in the range of [1, 5]. The default value is 2 seconds.

This parameter cannot be updated while pushing stream to the CDN.

kBitRate

Type: `number`

The bitrate (Kbps) in the range of [1, 10000]. The default value is self\-adaptive.

## TRANSCODING_VIDEO_CODEC

Type: `enum`

The video codec.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |H264 |`'H264'` |(Default) H.264 format. |
   |H265 |`'H265'` |H.265 format. |

## LiveTranscodeLayoutConfig

Type: `interface`

The overall video layout of the mixed stream.

regions

Type: [LiveTranscodeLayoutRegion](https://docs.byteplus.com/en/docs/12/14193#livetranscodelayoutregion)`[]`

List of user's video layout information. With invalid or empty input, the configurations will be set as the default values.

appData

Type: `string`

The data you need, up to 4KB in length.

backgroundColor

Type: `string`

Background\-color of the mixed stream in hexadecimal values such as #FFFFFF and #000000. The default value is #000000 (black).

With invalid or empty input, the configurations will be set as the default values.

## LiveTranscodeLayoutRegion

Type: `interface`

Layout information for one of the video streams to be mixed.

alpha

Type: `number | undefined`

The opacity in the range of (0.0, 1.0]. The lower the value, the more transparent. The default value is 1.0.

userId

Type: `string`

ID of the user who published the stream

x

Type: `number | undefined`

The normalized horizontal coordinate value of the top left end vertex of the user's view, ranging within [0.0, 1.0). The default value is 0.0.

y

Type: `number | undefined`

The normalized vertical coordinate value of the top left end vertex of the user's view, ranging within [0.0, 1.0). The default value is 0.0.

zorder

Type: `number | undefined`

The layer on which the video is rendered. The range is [0, 100]. 0 for the bottom layer, and 100 for the top layer. The default value is 0.

w

Type: `number | undefined`

The normalized width of the user's view, ranging within (0.0, 1.0]. The default value is 1.0.

h

Type: `number | undefined`

The normalized height of the user's view, ranging within (0.0, 1.0]. The default value is 1.0.

renderMode

Type: `number | undefined`

The render mode to be set. The default value is 1. See the following options:

• 1: Fill and Crop. The video is enlarged or shrunk with a fixed aspect ratio, and completely fills the window. The region of the video which exceeds the window will be cropped.

• 2: Fit. The video is enlarged or shrunk with a fixed aspect ratio, and is shown completely in the windows. The region of the window, which is not filled with video, is filled with a black background.

• 3: Stretch. The video's aspect ratio is changed as it is automatically stretched to completely fill the bounding box that it is contained in, but the whole image is visible.

contentControl

Type: `number | undefined`

The content to be set. The default value is 0. See the following options:

• 0: Push both audio and video stream.

• 1: Push audio stream only.

• 2: Push video stream only.

isScreenStream

Type: `boolean`

Whether the stream comes from screen sharing

## VideoSourceType

Type: `enum`

Video source type

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |VIDEO_SOURCE_TYPE_EXTERNAL |`0` |Custom video source |
   |VIDEO_SOURCE_TYPE_INTERNAL |`1` |Internal audio capture, referring to capturing video using the built\-in module (the default) |

## AudioSourceType

Type: `enum`

Audio source type

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |AUDIO_SOURCE_TYPE_EXTERNAL |`0` |Custom audio source |
   |AUDIO_SOURCE_TYPE_INTERNAL |`1` |Internal audio capture, referring to capture audio using the built\-in module (the default) |

## TrackCaptureConfig

Internal capture configuration for video & audio. Refer to [browser documentation](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints) for more details.

* **Type**

   ```ts
   Omit<MediaTrackConstraints, 'deviceId'>
   ```

## USER_ONLINE_STATUS

Type: `enum`

Login status

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |OFFLINE |`0` |Offline. And cannot send or receive any P2P message. |
   |ONLINE |`1` |Online |
   |UNREACHABLE |`2` |Unreachable. And cannot send or receive any P2P message. |

## CloudProxyInfo

Type: `interface`

Cloud proxy information.

logProxy

Type: `string`

The cloud proxy IP of log report

accessProxy

Type: `string | string[]`

The cloud proxy IP of the access

configProxy

Type: `string`

The cloud proxy IP of RTC admin control

## PublicStreamConfig

Type: `interface`

Configurations of the WTN stream.

video

Type: `{ width?: number | undefined; height?: number | undefined; fps?: number | undefined; kBitRate: number; } | undefined`

Video configurations.

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |width |`number \| undefined` |Width, unit: px.<br><br>Valid for even numbers only. Assigning an odd number will lead to a failure of publishing a WTN stream. |
   |height |`number \| undefined` |Height, unit: px.<br><br>Valid for even numbers only. Assigning an odd number will lead to a failure of publishing a WTN stream. |
   |fps |`number \| undefined` |Frame rate, unit: fps |
   |kBitRate |`number` |Bitrate, unit: kbps |

layout

Type: `{ interpolationMode?: `[PublicInterpolationMode](https://docs.byteplus.com/en/docs/12/14193#publicinterpolationmode)` | undefined; backgroundColor?: string | undefined; backgroundImage?: string | undefined; regions?: `[PublicStreamLayoutRegion](https://docs.byteplus.com/en/docs/12/14193#publicstreamlayoutregion)`[] | undefined; } | undefined`

The layout mode of the WTN stream.

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |interpolationMode |`PublicInterpolationMode \| undefined` |Interpolation mode. |
   |backgroundColor |`string \| undefined` |Background color in hexadecimal. |
   |backgroundImage |`string \| undefined` |Background image URL up to 1,024 bytes in length. The image format should be JPG, JPEG, or PNG. |
   |regions |`PublicStreamLayoutRegion[] \| undefined` |Layout configuration of the WTN stream |

## PublicInterpolationMode

Type: `enum`

Interpolation mode.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |PREV_FRAME |`0` |Interpolate with the last frame. |
   |OTHER_FRAME |`1` |Intermediate with the background image or blank frames. |

## PublicStreamLayoutRegion

Layout configuration of a media stream

This struct contains all parameters in [LiveTranscodeLayoutRegion](https://docs.byteplus.com/en/docs/12/14193#livetranscodelayoutregion) except for `isLocalUser` and `contentControl`, as well as the following parameters.

* **Type**

   ```ts
   Omit<LiveTranscodeLayoutRegion, 'isLocalUser' | 'contentControl'> & {
     roomId: string;
     mediaType?: PublicStreamType;
     sourceCrop?: {
       x: number;
       y: number;
       w: number;
       h: number;
     };
   }
   ```

* **Member**

   |Name |Type |Description |
   |---|---|---|
   |roomId |`string` |Room ID of the user that publishes the media stream. |
   |mediaType |[PublicStreamType](https://docs.byteplus.com/en/docs/12/14193#publicstreamtype)` \| undefined` |Media type of the WTN stream. |
   |sourceCrop |`{ x: number; y: number; w: number; h: number; } \| undefined` |Configurations on how to crop the WTN stream |
   |x |`number` |The normalized horizontal coordinate value of the top left vertex of the cropped image to width of the original image, ranging within [0.0, 1.0). |
   |y |`number` |The normalized vertical coordinate value of the top left vertex of the cropped image to height of the original image, ranging within [0.0, 1.0). |
   |w |`number` |The normalized ratio of the width of the cropped image to that of the original image, ranging within [0.0, 1.0). |
   |h |`number` |The normalized ratio of the height of the cropped image to that of the original image, ranging within [0.0, 1.0). |

## PublicStreamType

Type: `enum`

Whether to include audio or video in the WTN stream.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |AUDIO_AND_VIDEO |`0` |Includes both audio and video. |
   |AUDIO_ONLY |`1` |Audio only. |
   |VIDEO_ONLY |`2` |Video only. |

## SubscribeFallbackOption

Type: `enum`

Fallback options for subscribed media stream

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |DISABLE |`0` |Default setting. Media stream fallback is disabled. |
   |VIDEO_STREAM_LOW |`1` |When the downstream network quality is bad, the video stream falls back to stream of lower resolution and then to voice only.<br><br>This setting takes effect only when the publisher enables simulcast mode. See [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1359024) for fallback rules. |
   |AUDIO_ONLY |`2` |When the downstream network quality is bad, the video stream fallbacks to voice only.<br><br>If you enable simulcast mode on the publisher, this option is not recommended as it might impair user experience. |

## RemoteUserPriority

Type: `enum`

priority of the remote user

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |LOW |`0` |Low. Default value. |
   |MEDIUM |`100` |The remote user's priority is medium. |
   |HIGH |`200` |The remote user's priority is high. |

## AudioProfileType

Type: `enum`

Audio quality

Call [setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioprofile) to choose an audio quality option.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |default |`0` |Default sound quality<br><br>The sound quality set by the server |
   |fluent |`1` |Smooth<br><br>Sample rate: 16 KHz<br><br>Mono\-channel<br><br>Encoding birrate: 24 Kbps<br><br>Fluent priority, low power consumption, and low traffic consumption, suitable for most game scenarios, such as team\-wide voice chat, group\-wide voice chat, nation\-wide voice chat. |
   |standard |`2` |Mono\-channel standard<br><br>Sample rate: 48 KHz<br><br>Encoding bitrate: 48 Kbps<br><br>For scenarios requiring distinct voice, you can choose this mode, which achieves balanced latency, consumption, and network packets. It is suitable for educational Apps and the online Mafia Games. |
   |hd |`3` |Dual\-channel music<br><br>Sample rate: 48 KHz<br><br>Encoding birrate: 128 Kbps<br><br>This mode provides high\-resolution audio at a cost of high latency, consumption, and large network packets. It is suitable for entertainment Apps such as co\-hosting and online talent contests.<br><br>Not recommended for game Apps. |
   |standardStereo |`4` |Dual\-channel standard<br><br>Sample rate: 48 KHz<br><br>Encoding birrate: 80 Kbps |
   |hdMono |`5` |Mono\-channel music<br><br>Sample rate: 48 KHz<br><br>Encoding birrate: 128 Kbps |

## ForwardStreamInfo

Type: `interface`

Information of the target rooms where the stream will be forwarded.

roomId

Type: `string`

The target room ID for forwarding media streams.

token

Type: `string`

Tokens generated using the target room's roomId and userId.

You can use the temporary token generated on the [console](https://console.byteplus.com/rtc/workplaceRTC) for testing purposes only. The official launch requires token generated by your server.

## AudioSelectionPriority

Type: `enum`

User priority in the audio selection

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |DEFAULT |`0` |Normally, whether the stream can be subscribed is determined by the result of audio selection. |
   |HIGH |`1` |High priority with which the stream can skip the audio selection and always be subscribable. |

## RemoteUserVideoStats

Type: `interface`

Statistics of subscribed video streams and network states in the cycle of 1s.

mainVideoStats

Type: [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/14193#remotevideostats)

State of the camera video stream.

screenVideoStats

Type: [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/14193#remotevideostats)

State of the screen recording stream.

## RemoteUserAudioStats

Type: `interface`

Statistics of subscribed audio streams and network states in the cycle of 1s.

mainAudioStats

Type: [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/14193#remoteaudiostats)

State of the microphone audio stream

screenAudioStats

Type: [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/14193#remoteaudiostats)

State of the device audio stream

## LocalUserVideoStats

Type: `interface`

Statistics of local video streams and network states in the cycle of 1s.

mainVideoStats

Type: [LocalVideoStats](https://docs.byteplus.com/en/docs/12/14193#localvideostats)

State of the camera video stream.

screenVideoStats

Type: [LocalVideoStats](https://docs.byteplus.com/en/docs/12/14193#localvideostats)

State of the screen recording stream.

## LocalUserAudioStats

Type: `interface`

State of the local media stream

mainAudioStats

Type: [LocalAudioStats](https://docs.byteplus.com/en/docs/12/14193#localaudiostats)

State of the microphone audio stream

screenAudioStats

Type: [LocalAudioStats](https://docs.byteplus.com/en/docs/12/14193#localaudiostats)

State of the device audio stream

## EngineConfig

Type: `interface`

Configuration for the engine instance to be created

autoPlayPolicy

Type: [RTCAutoPlayPolicy](https://docs.byteplus.com/en/docs/12/14193#rtcautoplaypolicy)` | undefined`

Auto\-play policy

## RTCAutoPlayPolicy

Type: `enum`

Auto\-play policy

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |AUTO_PLAY |`0` |By default, play audios and videos automatically. |
   |VIDEO_ONLY |`1` |Play videos only automatically. |
   |PLAY_MANUALLY |`2` |Disable Auto\-play. Guide the user to interact with the app to play the media streams. |

## ScreenSourceType

The type of screen\-sharing object in Electron.

• `screen`: Screens.

• `window`: Windows and applications.

* **Type**

   ```ts
   'screen' | 'window'
   ```

## ElectronDesktopCapturerSource

Type: `interface`

The object to be shared during screen\-sharing in Electron.

id

Type: `string`

Identifier.

name

Type: `string`

Name.

thumbnail

Type: [IElectronNativeImage](https://docs.byteplus.com/en/docs/12/14193#ielectronnativeimage)

Thumbnail.

## IElectronNativeImage

Type: `interface`

The thumbnail of the screen\-sharing source in Electron.

toDataURL

A base 64 encoded Data URL string. Refer to [nativeImage](http://electron.atom.io/docs/api/native-image) for more details.

* **Type**

   ```ts
   () => string
   ```

* **Return Value**

   Type: `string`

## onWTNPushStateChangedEvent

Type: `interface`

The result of the WTN stream task.

streamId

Type: `string`

WTN stream ID.

oldState

Type: [WTNPushState](https://docs.byteplus.com/en/docs/12/14193#wtnpushstate)

The original state of the WTN stream publishing task.

newState

Type: [WTNPushState](https://docs.byteplus.com/en/docs/12/14193#wtnpushstate)

The new state of the WTN stream publishing task.

reason

Type: [WTNPushStateChangedReason](https://docs.byteplus.com/en/docs/12/14193#wtnpushstatechangedreason)

The reason why the WTN stream publishing task state changed.

elapse

Type: `number`

The time elapsed since the WTN stream publishing task state changed.

## WTNPushState

Type: `enum`

Status of the WTN streams task.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |INIT |`0` |Initial. Status changes from INIT to START after calling startPushWtn. |
   |START |`1` |Start. |
   |SUCCESS |`2` |Success. |
   |STOP |`3` |Stop. |
   |FAIL |`4` |Failed. |

## WTNPushStateChangedReason

Type: `enum`

The reason why the status of the WTN streams task changes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |PUSH_SUCCESS |`0` |Success. |
   |START_PUSH |`1` |By calling [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn). |
   |STOP_PUSH |`2` |By calling [stopPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stoppushwtn). |
   |IN_RETRY |`3` |Retry. |
   |RETRY_FAIL |`4` |Retry failed for three times. |
   |NO_PUSH_PERMISSION |`5` |Your token has no publishing permission. |
   |STREAM_PUSH_BY_OTHER |`6` |Your stream_id has been occupied by another stream. |
   |STREAM_BANNED |`7` |The stream has been forbidden. |

## onWTNPlayStateChangedEvent

Type: `interface`

The state of the WTN stream playing.

streamId

Type: `string`

WTN stream ID.

oldState

Type: [WTNPlayState](https://docs.byteplus.com/en/docs/12/14193#wtnplaystate)

The original state of the WTN stream playing.

newState

Type: [WTNPlayState](https://docs.byteplus.com/en/docs/12/14193#wtnplaystate)

The new state of the WTN stream playing.

reason

Type: [WTNPlayStateChangedReason](https://docs.byteplus.com/en/docs/12/14193#wtnplaystatechangedreason)

The reason why the playing state changed.

elapse

Type: `number`

The time elapsed since the WTN stream playing state changed.

## WTNPlayState

Type: `enum`

Events related to playing WTN streams.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |INIT |`0` |Initial. Status changes from INIT to START after calling startPlayWtn. |
   |START |`1` |Start. |
   |SUCCESS |`2` |Success. |
   |STOP |`3` |Stop. |
   |FAIL |`4` |Failed. |

## WTNPlayStateChangedReason

Type: `enum`

The reason why the play state of the WTN streams changes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |PLAY_SUCCESS |`0` |Success. |
   |START_PLAY |`1` |By calling startPlayWtn. |
   |STOP_PLAY |`2` |By calling stopPlayWtn. |
   |REMOTE_STOP |`3` |The publisher stops publishing the wtn stream. |
   |REMOTE_FAILURE |`4` |The publishing was stopped accidentally. |
   |STREAM_BANNED |`5` |The stream has been forbidden. |
   |NO_PLAY_PERMISSION |`6` |Your token has no subscribing permission. |
   |STREAM_NOT_EXIST |`7` |The stream does not exist. |
   |IN_RETRY |`8` |Retry. |
   |RETRY_FAIL |`9` |Retry failed for three times. |
   |INTERNAL |`10` |Internal error. |
   |OVER_CLIENT_SUBSCRIBE_STREAM_LIMIT |`1310` |A single engine instance can only subscribe to up to 5 streams. |
   |OVER_STREAM_SUBSCRIBE_USER_LIMIT |`1311` |The number of users who are subscribed to the same stream has exceeded the limit. |
   |OVER_STREAM_SUBSCRIBE_REQUES_TLIMIT |`1312` |The number of requests for subscribing to the same stream has exceeded the limit. |

## onWTNRemoteAudioStateChangedEvent

Type: `interface`

The state of the remote WTN stream audio changed.

streamId

Type: `string`

WTN stream ID.

state

Type: [WTNRemoteAudioState](https://docs.byteplus.com/en/docs/12/14193#wtnremoteaudiostate)

The state of the WTN stream audio changed.

reason

Type: [WTNRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14193#wtnremoteaudiostatechangereason)

The reason why the status of the remote WTN audio changes.

## WTNRemoteAudioState

Type: `enum`

Audio state of the remote WTN stream

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |STOPED |`0` |The init state of the remote WTN video. This state is reported in ReasonMute and ReasonRemotestop. |
   |STARTING |`1` |The local client has received the first audio packet of the WTN stream. |
   |DECODING |`2` |The WTN stream is playing. |
   |FROZEN |`3` |The WTN stream suffers from stutter. |
   |FAILED |`4` |The WTN stream failed to play. |

## WTNRemoteAudioStateChangeReason

Type: `enum`

The reason why the status of the remote WTN audio changes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |INTERNAL |`0` |Internal error. |
   |NETWORK_CONGESTION |`1` |Network congestion. |
   |NETWORK_RECOVERY |`2` |Network recovery. |
   |UNMUTE |`3` |The local client subscribed to the remote stream. |
   |MUTE |`4` |The local client unsubscribed from the remote stream. |
   |REMOTE_START |`5` |The remote stream started publishing. |
   |REMOTE_STOP |`6` |The remote stream stopped publishing. |

## onWTNRemoteVideoStateChangedEvent

Type: `interface`

The state of the WTN stream video changed.

streamId

Type: `string`

WTN stream ID.

state

Type: [WTNRemoteVideoState](https://docs.byteplus.com/en/docs/12/14193#wtnremotevideostate)

The state of the WTN stream video.

reason

Type: [WTNRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14193#wtnremotevideostatechangereason)

The reason why the WTN stream video state changed.

## WTNRemoteVideoState

Type: `enum`

Video state of the remote WTN stream.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |STOPED |`0` |The init state of the remote WTN video. This state is reported in ReasonMute and ReasonRemotestop. |
   |STARTING |`1` |The local client has received the first video frame of the wtn stream. |
   |DECODING |`2` |The WTN stream is playing. |
   |FROZEN |`3` |The WTN stream suffers from stutter. |
   |FAILED |`4` |The WTN stream failed to play. |

## WTNRemoteVideoStateChangeReason

Type: `enum`

The reason why the status of the remote WTN audio changes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |INTERNAL |`0` |Internal error. |
   |NETWORK_CONGESTION |`1` |Network congestion. |
   |NETWORK_RECOVERY |`2` |Network recovery. |
   |UNMUTE |`3` |The local client subscribed to the remote stream. |
   |MUTE |`4` |The local client unsubscribed from the remote stream. |
   |REMOTE_START |`5` |The remote stream started publishing. |
   |REMOTE_STOP |`6` |The remote stream stopped publishing. |

## onWTNRemoteVideoStatsEvent

Type: `interface`

The statistics of the video of the WTN stream.

streamId

Type: `string`

WTN stream ID.

videoStats

Type: [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/14193#remotevideostats)

The statistics of the video of the WTN stream.

## onWTNRemoteAudioStatsEvent

Type: `interface`

The statistics of the audio of the WTN stream.

streamId

Type: `string`

WTN stream ID.

audioStats

Type: [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/14193#remoteaudiostats)

The statistics of the audio of the WTN stream.

## onWTNFirstRemoteVideoFrameDecodedEvent

Type: `interface`

SEI messages carried by the WTN stream.

streamId

Type: `string`

WTN stream ID.

## onWTNSEIMessageReceivedEvent

Type: `interface`

SEI messages carried by the WTN stream.

streamId

Type: `string`

WTN stream ID.

sei

Type: `Uint8Array`

SEI.

## onWTNLocalStatsExceptionEvent

Type: `interface`

Exception event of local WTN media stream.

exception

Type: `string`

Exception of local WTN media stream information. Possible values, see the `Exception Message` column in [RTCExceptionCodeMap](https://docs.byteplus.com/en/docs/12/14193#rtcexceptioncodemap).

code

Type: `number`

Exception code of local WTN media stream. Possible values, see the `Exception Code` column in [RTCExceptionCodeMap](https://docs.byteplus.com/en/docs/12/14193#rtcexceptioncodemap).

streamId

Type: `string`

ID of the local WTN media stream.

## onWTNRemoteStatsExceptionEvent

Type: `interface`

Exception event of remote WTN media stream.

exception

Type: `string`

Exception of remote WTN media stream information. Possible values, see the `Exception Message` column in [RTCExceptionCodeMap](https://docs.byteplus.com/en/docs/12/14193#rtcexceptioncodemap).

code

Type: `number`

Exception code of remote WTN media stream.

streamId

Type: `string`

ID of the remote WTN media stream.

## RTCExceptionCodeMap

|Exception Message |Exception Code |Description |
|---|---|---|
|FRAMERATE_INPUT_TOO_LOW |1001 |Input video frame rate is too low |
|FRAMERATE_SENT_TOO_LOW |1002 |Sent video frame rate is too low |
|SEND_VIDEO_BITRATE_TOO_LOW |1003 |Sent video bitrate is too low |
|RECV_VIDEO_DECODE_FAILED |1005 |Remote video decoding failed |
|AUDIO_INPUT_LEVEL_TOO_LOW |2001 |Input audio volume is too low |
|AUDIO_OUTPUT_LEVEL_TOO_LOW |2002 |Output audio volume is too low |
|SEND_AUDIO_BITRATE_TOO_LOW |2003 |Send audio bitrate is too low |
|FRAMERATE_INPUT_TOO_LOW_RECOVER |3001 |Input video frame rate is too low recovery |
|FRAMERATE_SENT_TOO_LOW_RECOVER |3002 |Sent video frame rate is too low recovery |
|SEND_VIDEO_BITRATE_TOO_LOW_RECOVER |3003 |Send video bitrate is too low recovery |
|RECV_VIDEO_DECODE_FAILED_RECOVER |3005 |Remote video decoding recovered |
|AUDIO_INPUT_LEVEL_TOO_LOW_RECOVER |4001 |Input audio volume is too low recovery |
|AUDIO_OUTPUT_LEVEL_TOO_LOW_RECOVER |4002 |Output audio volume is too low recovery |
|SEND_AUDIO_BITRATE_TOO_LOW_RECOVER |4003 |Send audio bitrate is too low recovery |
