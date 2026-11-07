---
title: "Keytype"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-191862"
---

<span id="ZoomConfigType"></span>
# ZoomConfigType

```c#
enum class bytertc.ZoomConfigType
```


Digital Zoom type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kZoomConfigTypeFocusOffset |0 |To set the offset for zooming in and zooming out. |
|kZoomConfigTypeMoveOffset |1 |To set the offset for panning and tiling. |


<span id="AudioFrameSource"></span>
# AudioFrameSource

```c#
enum class bytertc.AudioFrameSource
```


Audio file recording source type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioFrameSourceMic |0 |The audio captured by the local microphone. |
|kAudioFrameSourcePlayback |1 |The audio got by mixing all remote user's audio. |
|kAudioFrameSourceMixed |2 |The audio got by mixing the local captured audio and all remote user's audio. |


<span id="RangeAudioInfo"></span>
# RangeAudioInfo

```c#
struct bytertc::RangeAudioInfo
```


Range audio information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[user_id](https://docs.byteplus.com/en/docs/12/35817#RangeAudioInfo-user_id) |
|int |[factor](https://docs.byteplus.com/en/docs/12/35817#RangeAudioInfo-factor) |


<span id="instructions"></span>
## Instructions

<span id="RangeAudioInfo-user_id"></span>
### user_id

```c#
string bytertc.RangeAudioInfo.user_id
```


User ID.

<span id="RangeAudioInfo-factor"></span>
### factor

```c#
int bytertc.RangeAudioInfo.factor
```


Volume attenuation. The value range is '[0,100]', which attenuates linearly with distance. When the factor is 0, it means that the sound cannot be heard.

<span id="CameraID"></span>
# CameraID

```c#
enum class bytertc.CameraID
```


camera.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kCameraIDFront |0 |Front\-facing camera for mobile, build\-in camera for PC |
|kCameraIDBack |1 |Postconditioning camera for mobile, PC is undefined for camera 1 |
|kCameraIDExternal |2 |External camera |
|kCameraIDInvalid |3 |Invalid value |


<span id="AudioScenarioType"></span>
# AudioScenarioType

```c#
enum class bytertc.AudioScenarioType
```


Audio scenarios After selecting the audio scenario, SDK will automatically select the call/media volume, according to the client\-side audio device and status. You can set the audio scenario by calling [SetAudioScenario](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setaudioscenario). If the following audio scenarios cannot meet your business needs, please contact our technical support team for customization.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioScenarioTypeMusic |0 |Music scene. Default to this scenario. This scene is suitable for scenes that require musical expression. Such as live music, etc. Audio capture playback device and capture playback status, the mapping to the volume type is as follows: < Table \> |
|kAudioScenarioTypeHighQualityCommunication |1 |High\-quality call scenarios. This scene is suitable for scenes that require musical expression. However, I hope to be able to use the microphone on the Bluetooth headset for audio collection. This scene can take into account the audio experience when playing/using the Bluetooth headset; and avoid sudden changes in hearing caused by volume type switching when using the Bluetooth headset as much as possible. Audio capture playback device and capture playback status, the mapping to the volume type is as follows: < Table\> |
|kAudioScenarioTypeCommunication |2 |Pure call volume scene. In this scenario, regardless of the client side audio acquisition and playback device and the acquisition and playback status, the call volume is used throughout the process. Suitable for calls or meeting scenarios that require frequent access. This scene can maintain a unified audio mode without sudden volume changes; Eliminate echoes to the greatest extent, so that the call definition is optimal; When using Bluetooth headsets, you can use the microphone on the Bluetooth headset for audio collection. However, the volume of other audio played using media volume will be lowered and the sound quality will deteriorate. |
|kAudioScenarioTypeMedia |3 |Pure media scene. It is generally not recommended. In this scenario, regardless of the client side audio acquisition and playback device and the acquisition and playback status, the media volume is used throughout the process. |
|kAudioScenarioTypeGameStreaming |4 |Game media scene. Only suitable for game scenes. In this scenario, the Bluetooth headset uses the call volume, and other devices use the media volume. Echo and howling are easy to occur when talking outside and there is no game sound cancellation optimization. |


<span id="AVSyncState"></span>
# AVSyncState

```c#
enum class bytertc.AVSyncState
```


Snychronization state between audio and video

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAVSyncStateAVStreamSyncBegin |0 |Audio and video start to sync |
|kAVSyncStateAudioStreamRemove |1 |Audio is removed during the sync process, but does not affect the current sync relationship |
|kAVSyncStateVdieoStreamRemove |2 |Video is removed during the sync process, but does not affect the current sync relationship |


<span id="RoomProfileType"></span>
# RoomProfileType

```c#
enum class bytertc.RoomProfileType
```


Room profile

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRoomProfileTypeCommunication |0 |Normal call mode. Mono audio channel. The sampling rate is 48kHz. You should use this mode for 1V1 calls. This mode works fine even if the network quality is poor. |
|kRoomProfileTypeLiveBroadcasting |1 |Live broadcasting mode. Mono audio channel. The sampling rate is 48kHz. Use this mode for high quality of the media. In this mode, audio plays in media mode for Bluetooth earphones. |
|kRoomProfileTypeGame |2 |Game voice mode. Mono audio channel. The sampling rate is 16kHz. Additional performance optimizations have been made for low\-end devices: < br \><br><br><br>* Encodes frame length 40/60 for some low\-end models. < br \><br><br>* Disables software 3A audio processing for some low\-end models.< br \> Enhance iOS Compatibility with other screen recordings to avoid audio recordings being interrupted by RTC. |
|kRoomProfileTypeCloudGame |3 |Cloud game mode. Mono audio channel. The sampling rate is 48kHz. Use this mode for scenerios of low latency and high bitrate. This mode works poor when the network quality is poor. |
|kRoomProfileTypeLowLatency |4 |Low latency mode. Use this mode when the scenario is neither a game or cloud game but requires very low latency. In this mode, call delay will be significantly reduced. But the audio quality and the redundancy for weak network are poor. You must consult the technical support specialist before using this mode. |


<span id="AudioFrameCallbackMethod"></span>
# AudioFrameCallbackMethod

```c#
enum class bytertc.AudioFrameCallbackMethod
```


Audio data callback method

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioFrameCallbackRecord |0 |[OnRecordAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onrecordaudioframeeventhandler), the callback of the audio data recorded by local microphone. |
|kAudioFrameCallbackPlayback |1 |[OnPlaybackAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onplaybackaudioframeeventhandler), the callback of the mixed audio data of all remote users subscribed by the local user. |
|kAudioFrameCallbackMixed |2 |[OnMixedAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onmixedaudioframeeventhandler), the callback of the mixed audio data including the data recorded by local microphone and that of all remote users subscribed by the local user. |
|kAudioFrameCallbackRemoteUser |3 |[OnRemoteUserAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremoteuseraudioframeeventhandler), the callback of the audio data before mixing of each remote user subscribed by the local user. |
|kAudioFrameCallbackRecordScreen |4 |[OnRecordScreenAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onrecordscreenaudioframeeventhandler), the callback of screen audio data captured locally. |


<span id="VideoContentType"></span>
# VideoContentType

```c#
enum class bytertc.VideoContentType
```


Video content type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoContentTypeNormalFrame |0 |Normal video |
|kVideoContentTypeBlackFrame |1 |Black frame video |


<span id="ReceiveRange"></span>
# ReceiveRange

```c#
struct bytertc::ReceiveRange
```


When using the range speech function, the range of speech reception

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[min](https://docs.byteplus.com/en/docs/12/35817#ReceiveRange-min) |
|int |[max](https://docs.byteplus.com/en/docs/12/35817#ReceiveRange-max) |


<span id="instructions"></span>
## Instructions

<span id="ReceiveRange-min"></span>
### min

```c#
int bytertc.ReceiveRange.min
```


The minimum range value for listening to sound without attenuation. When the distance between the listener and the sound source is less than min, the received sound has no attenuation at all.

<span id="ReceiveRange-max"></span>
### max

```c#
int bytertc.ReceiveRange.max
```


The maximum range of sound that can be heard. When the distance between the listener and the sound source is greater than max, the sound cannot be heard. When the distance between the listener and the sound source is between [min, max), the volume heard is attenuated according to the distance.

<span id="RemoteAudioStreamState"></span>
# RemoteAudioStreamState

```c#
enum class bytertc.RemoteAudioStreamState
```


Local audio stream status. SDK callbacks local audio stream status via `OnLocalAudioStateChangedEventHandler`

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteAudioStateStopped |0 |The remote audio stream is not received. The callback `onRemoteAudioStateChanged` triggers:<br><br><br>* Local users stop receiving remote audio streams due to [kRemoteAudioStateChangeReasonLocalMuted](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* The remote user stops sending audio streams due to [kRemoteAudioStateChangeReasonRemoteMuted](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* The remote user left the room, the corresponding reason is: [kRemoteAudioStateChangeReasonRemoteOffline](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason) |
|kRemoteAudioStateStarting |1 |Start receiving the remote audio stream header. Just received the remote audio stream header will trigger a callback `onRemoteAudioStateChanged`, The corresponding reason is: [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason) in "kRemoteAudioStateChangeReasonLocalUnmuted" |
|kRemoteAudioStateDecoding |2 |The remote audio stream is decoding and playing normally. A callback is triggered in the following cases: `onRemoteAudioStateChanged`:<br><br><br>* The remote audio first frame was successfully decoded, and the corresponding reason is: 'kRemoteAudioStateChangeReasonLocalUnmuted' in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* The network returned to normal from blocking, and the corresponding reason is: "kRemoteAudioStateChangeReasonNetworkRecovery ' in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* Local users resume receiving remote audio streams, and the corresponding reason is 'kRemoteAudioStateChangeReasonLocalUnmuted ' [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* Remote users resume sending audio streams, and the corresponding reason is 'kRemoteAudioStateChangeReasonRemoteUnmuted' in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason) |
|kRemoteAudioStateFrozen |3 |Remote audio streaming card. A callback is triggered when the network is blocked and the packet loss rate is greater than 40%. `onRemoteAudioStateChanged`, The corresponding reason is: "kRemoteAudioStateChangeReasonNetworkCongestion" in [kRemoteAudioStateChangeReasonNetworkCongestion}](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason-kremoteaudiostatechangereasonnetworkcongestion) |


<span id="SyncInfoStreamType"></span>
# SyncInfoStreamType

```c#
enum class bytertc.SyncInfoStreamType
```


Stream type for media stream information synchronization

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSyncInfoStreamTypeAudio |0 |Audio stream |


<span id="LocalVideoStats"></span>
# LocalVideoStats

```c#
struct bytertc::LocalVideoStats
```


Local video stream statistics, reference period 2s. After a local user publishes a video stream successfully, the SDK will periodically notify the user through `OnLocalStreamStatsEventHandler`. The delivery status of the published video stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[sent_kbitrate](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-sent_kbitrate) |
|int |[input_frame_rate](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-input_frame_rate) |
|int |[sent_frame_rate](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-sent_frame_rate) |
|int |[encoder_output_frame_rate](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-encoder_output_frame_rate) |
|int |[renderer_output_frame_rate](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-renderer_output_frame_rate) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-stats_interval) |
|float |[video_loss_rate](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-video_loss_rate) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-rtt) |
|int |[encoded_bitrate](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-encoded_bitrate) |
|int |[encoded_frame_width](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-encoded_frame_width) |
|int |[encoded_frame_height](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-encoded_frame_height) |
|int |[encoded_frame_count](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-encoded_frame_count) |
|VideoCodecType |[codec_type](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-codec_type) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-is_screen) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats-jitter) |


<span id="instructions"></span>
## Instructions

<span id="LocalVideoStats-sent_kbitrate"></span>
### sent_kbitrate

```c#
int bytertc.LocalVideoStats.sent_kbitrate
```


TX bitrate in Kbps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-input_frame_rate"></span>
### input_frame_rate

```c#
int bytertc.LocalVideoStats.input_frame_rate
```


Sampling frame rate in fps of video capture during this reference period

<span id="LocalVideoStats-sent_frame_rate"></span>
### sent_frame_rate

```c#
int bytertc.LocalVideoStats.sent_frame_rate
```


TX frame rate in fps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encoder_output_frame_rate"></span>
### encoder_output_frame_rate

```c#
int bytertc.LocalVideoStats.encoder_output_frame_rate
```


Encoder\-output frame rate in fps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-renderer_output_frame_rate"></span>
### renderer_output_frame_rate

```c#
int bytertc.LocalVideoStats.renderer_output_frame_rate
```


Local\-rendering frame rate in fps during this reference period

<span id="LocalVideoStats-stats_interval"></span>
### stats_interval

```c#
int bytertc.LocalVideoStats.stats_interval
```


Reference period in ms. This field is used to set the reference period for the callback, which is 2 s by default.

<span id="LocalVideoStats-video_loss_rate"></span>
### video_loss_rate

```c#
float bytertc.LocalVideoStats.video_loss_rate
```


Video packet loss rate. The video uplink packet loss rate in this reference period ranges from [0,1].

<span id="LocalVideoStats-rtt"></span>
### rtt

```c#
int bytertc.LocalVideoStats.rtt
```


Round\-trip time in ms.

<span id="LocalVideoStats-encoded_bitrate"></span>
### encoded_bitrate

```c#
int bytertc.LocalVideoStats.encoded_bitrate
```


Video encoding bitrate in Kbps of the video stream with the highest resolution within the reference period.

<span id="LocalVideoStats-encoded_frame_width"></span>
### encoded_frame_width

```c#
int bytertc.LocalVideoStats.encoded_frame_width
```


Video encoding width in px of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encoded_frame_height"></span>
### encoded_frame_height

```c#
int bytertc.LocalVideoStats.encoded_frame_height
```


Video encoding height in px of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encoded_frame_count"></span>
### encoded_frame_count

```c#
int bytertc.LocalVideoStats.encoded_frame_count
```


The total number of the video stream with the highest resolution within the reference period sent in the reference period.

<span id="LocalVideoStats-codec_type"></span>
### codec_type

```c#
VideoCodecType bytertc.LocalVideoStats.codec_type
```


For the encoding type of the video, please refer to [VideoCodecType](https://docs.byteplus.com/en/docs/12/35817#VideoCodecType).

<span id="LocalVideoStats-is_screen"></span>
### is_screen

```c#
bool bytertc.LocalVideoStats.is_screen
```


Whether the media stream belongs to the user is a screen stream. You can know whether the current statistics come from mainstream or screen stream.

<span id="LocalVideoStats-jitter"></span>
### jitter

```c#
int bytertc.LocalVideoStats.jitter
```


Video uplink network jitter in ms.

<span id="ByteWatermark"></span>
# ByteWatermark

```c#
struct bytertc::ByteWatermark
```


Watermark's scaled coordinates and size, relative to the video stream.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/35817#ByteWatermark-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/35817#ByteWatermark-y) |
|float |[width](https://docs.byteplus.com/en/docs/12/35817#ByteWatermark-width) |
|float |[height](https://docs.byteplus.com/en/docs/12/35817#ByteWatermark-height) |


<span id="instructions"></span>
## Instructions

<span id="ByteWatermark-x"></span>
### x

```c#
float bytertc.ByteWatermark.x
```


The watermark's horizontal offset from the upper left corner of the video stream to the video stream's width in range of [0,1).

<span id="ByteWatermark-y"></span>
### y

```c#
float bytertc.ByteWatermark.y
```


The watermark's vertical offset from the upper left corner of the video stream to the video stream's height in range of [0,1).

<span id="ByteWatermark-width"></span>
### width

```c#
float bytertc.ByteWatermark.width
```


The watermark's width to the video stream's width in range of [0,1).

<span id="ByteWatermark-height"></span>
### height

```c#
float bytertc.ByteWatermark.height
```


The watermark height to the video stream's height in range of [0,1).

<span id="AudioPropertiesConfig"></span>
# AudioPropertiesConfig

```c#
struct bytertc::AudioPropertiesConfig
```


Configuration related to audio attribute information prompt.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[Interval](https://docs.byteplus.com/en/docs/12/35817#AudioPropertiesConfig-interval) |
|bool |[EnableSpectrum](https://docs.byteplus.com/en/docs/12/35817#AudioPropertiesConfig-enablespectrum) |
|bool |[EnableVad](https://docs.byteplus.com/en/docs/12/35817#AudioPropertiesConfig-enablevad) |


<span id="instructions"></span>
## Instructions

<span id="AudioPropertiesConfig-interval"></span>
### Interval

```c#
int bytertc.AudioPropertiesConfig.Interval
```


Prompt interval in ms

<span id="AudioPropertiesConfig-enablespectrum"></span>
### EnableSpectrum

```c#
bool bytertc.AudioPropertiesConfig.EnableSpectrum
```


Whether to enable audio spectrum detection

<span id="AudioPropertiesConfig-enablevad"></span>
### EnableVad

```c#
bool bytertc.AudioPropertiesConfig.EnableVad
```


Whether to enable Voice Activity Detection

<span id="MediaDeviceState"></span>
# MediaDeviceState

```c#
enum class bytertc.MediaDeviceState
```


Media device state. You will be informed of this state [byOnAudioDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiodevicestatechangedeventhandler) or [OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler).

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaDeviceStateStarted |1 |On |
|kMediaDeviceStateStopped |2 |Off |
|kMediaDeviceStateRuntimeError |3 |Runtime error For example, when the media device is expected to be working but no data is received. |
|kMediaDeviceStatePaused |4 |Device paused. Including:<br><br><br>* During screen capturing, the target application window is minimized in the taskbar.<br><br>* Before or during screen capturing, the target application window is hidden.<br><br>* During screen capturing, the target application window is being stretched.<br><br>* During screen capturing, the target application window is being dragged. |
|kMediaDeviceStateResumed |5 |Device resumed |
|kMediaDeviceStateAdded |10 |Added |
|kMediaDeviceStateRemoved |11 |Removed |
|kMediaDeviceInterruptionBegan |12 |Closing the laptop interrupted the RTC call. RTC call will resume once the laptop is opened. |
|kMediaDeviceInterruptionEnded |13 |RTC call resumed from the interruption caused by Closing the laptop. |


<span id="RoomStateCode"></span>
# RoomStateCode

```c#
enum class bytertc.RoomStateCode
```


Join room error code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|JOIN_ROOM_SUCCESS |0 |Join room success. |
|JOIN_ROOM_INVALID_TOKEN |\-1000 |Token is invalid. The token used when calling JoinRoom is invalid or expired. The user is required to retrieve the token and call RenewToken to update the token. |
|JOIN_ROOM_ERROR |\-1001 |Join room error. An unknown error occurred when calling JoinRoom, which caused the joining room to fail. Users are required to rejoin the room. |
|JOIN_ROOM_FAILED |\-2001 |Join room failed. When the user calls JoinRoom to join the room or due to poor network conditions, the user failed to join the room due to server errors, and the SDK will automatically retry joining the room. |
|JOIN_ROOM_DUPLICATE_LOGIN |\-1004 |A user with the same user ID as the user in the room where the local user is located has logged in, resulting in the local user being kicked out of the room |


<span id="RemoteVideoState"></span>
# RemoteVideoState

```c#
enum class bytertc.RemoteVideoState
```


Remote video stream status. You will receive `OnRemoteVideoStateChangedEventHandler` callback when the state changes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteVideoStateStopped |0 |The remote video stream defaults to the initial state, and the video has not yet started playing. |
|kRemoteVideoStateStarting |1 |Local user has received remote video stream header packet. |
|kRemoteVideoStateDecoding |2 |The remote video stream is decoding and playing normally. |
|kRemoteVideoStateFrozen |3 |Remote video streaming card, there may be network and other reasons. |
|kRemoteVideoStateFailed |4 |The remote video stream failed to play. |


<span id="Rectangle"></span>
# Rectangle

```c#
struct bytertc::Rectangle
```


Rectangle Area

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[X](https://docs.byteplus.com/en/docs/12/35817#Rectangle-x) |
|int |[Y](https://docs.byteplus.com/en/docs/12/35817#Rectangle-y) |
|int |[Width](https://docs.byteplus.com/en/docs/12/35817#Rectangle-width) |
|int |[Height](https://docs.byteplus.com/en/docs/12/35817#Rectangle-height) |


<span id="instructions"></span>
## Instructions

<span id="Rectangle-x"></span>
### X

```c#
int bytertc.Rectangle.X
```


The x coordinate of the upper left corner of the rectangular area

<span id="Rectangle-y"></span>
### Y

```c#
int bytertc.Rectangle.Y
```


The x coordinate of the upper left corner of the rectangular area

<span id="Rectangle-width"></span>
### Width

```c#
int bytertc.Rectangle.Width
```


Rectangle width in px

<span id="Rectangle-height"></span>
### Height

```c#
int bytertc.Rectangle.Height
```


Rectangular height in px

<span id="VoiceChangerType"></span>
# VoiceChangerType

```c#
enum class bytertc.VoiceChangerType
```


Change sound effect type. For more types, contact the technical supporters.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVoiceChangerTypeOriginal |0 |Acoustic, no special effects |
|kVoiceChangerTypeGiant |1 |Giant |
|kVoiceChangerTypeChipmunk |2 |Chipmunk |
|kVoiceChangerTypeMinionst |3 |Little yellow man |
|kVoiceChangerTypeVibrato |4 |Trill |
|kVoiceChangerTypeRobot |5 |Robot |


<span id="MediaDeviceError"></span>
# MediaDeviceError

```c#
enum class bytertc.MediaDeviceError
```


Media device error type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaDeviceErrorOK |0 |Media equipment is normal |
|kMediaDeviceErrorDeviceNoPermission |1 |No permission to start media device |
|kMediaDeviceErrorDeviceBusy |2 |Media devices are already in use |
|kMediaDeviceErrorDeviceFailure |3 |Media device error |
|kMediaDeviceErrorDeviceNotFound |4 |The specified media device was not found |
|kMediaDeviceErrorDeviceDisconnected |5 |Media device, window or monitor removed |
|kMediaDeviceErrorDeviceNoCallback |6 |Device has no data callback |
|kMediaDeviceErrorDeviceUNSupportFormat |7 |Device sample rate not supported |
|kMediaDeviceErrorDeviceNotFindGroupId |8 |iOS screen capture not find group Id parameter |


<span id="RTCAudioDeviceType"></span>
# RTCAudioDeviceType

```c#
enum class bytertc.RTCAudioDeviceType
```


Audio device type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRTCAudioDeviceTypeUnknown |\-1 |Unknown device type |
|kRTCAudioDeviceTypeRenderDevice |0 |Audio Rendering Device Type |
|kRTCAudioDeviceTypeCaptureDevice |1 |Audio Acquisition Device Type |
|kRTCAudioDeviceTypeScreenCaptureDevice |2 |Screen Streaming Audio Devices |


<span id="AudioRouteDevice"></span>
# AudioRouteDevice

```c#
enum class bytertc.AudioRouteDevice
```


Audio playback route

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioRouteDefault |\-1 |unknown devices |
|kAudioRouteDeviceHeadset |1 |Wired earphones |
|kAudioRouteDeviceEarpiece |2 |Earpiece. Built\-in device for calling. |
|kAudioRouteDeviceSpeakerphone |3 |Speaker. Built\-in device for hands\-free audio playing. |
|kAudioRouteDeviceHeadsetBluetooth |4 |Bluetooth earphones |
|kAudioRouteDeviceHeadsetUSB |5 |USB device |


<span id="FaceDetectResult"></span>
# FaceDetectResult

```c#
struct bytertc::FaceDetectResult
```


Face Detection Result

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const int |[max_face_num](https://docs.byteplus.com/en/docs/12/35817#FaceDetectResult-max_face_num) |
|int |[detect_result](https://docs.byteplus.com/en/docs/12/35817#FaceDetectResult-detect_result) |
|int |[face_count](https://docs.byteplus.com/en/docs/12/35817#FaceDetectResult-face_count) |
|Rectangle[] |[rect](https://docs.byteplus.com/en/docs/12/35817#FaceDetectResult-rect) |
|int |[image_width](https://docs.byteplus.com/en/docs/12/35817#FaceDetectResult-image_width) |
|int |[image_height](https://docs.byteplus.com/en/docs/12/35817#FaceDetectResult-image_height) |
|ulong |[frame_timestamp_us](https://docs.byteplus.com/en/docs/12/35817#FaceDetectResult-frame_timestamp_us) |


<span id="instructions"></span>
## Instructions

<span id="FaceDetectResult-max_face_num"></span>
### max_face_num

```c#
const int bytertc.FaceDetectResult.max_face_num = 10
```


Face information storage limit, up to 10 faces can be stored.

<span id="FaceDetectResult-detect_result"></span>
### detect_result

```c#
int bytertc.FaceDetectResult.detect_result
```


Face Detection Result


* 0: Success

* !0: Failure. See [Error Code Table](https://docs.byteplus.com/en/effects/docs/error-code-table).


<span id="FaceDetectResult-face_count"></span>
### face_count

```c#
int bytertc.FaceDetectResult.face_count
```


Number of the detected face

<span id="FaceDetectResult-rect"></span>
### rect

```c#
Rectangle [] bytertc.FaceDetectResult.rect
```


The face recognition rectangles. The length of the array is the same as the number of detected faces. See [Rectangle](https://docs.byteplus.com/en/docs/12/35817#Rectangle).

<span id="FaceDetectResult-image_width"></span>
### image_width

```c#
int bytertc.FaceDetectResult.image_width
```


Width of the original image (px)

<span id="FaceDetectResult-image_height"></span>
### image_height

```c#
int bytertc.FaceDetectResult.image_height
```


Height of the original image (px)

<span id="FaceDetectResult-frame_timestamp_us"></span>
### frame_timestamp_us

```c#
ulong bytertc.FaceDetectResult.frame_timestamp_us
```


The time stamp of the video frame using face detection.

<span id="AudioSourceType"></span>
# AudioSourceType

```c#
enum class bytertc.AudioSourceType
```


Audio input source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioSourceTypeExternal |0 |Custom Capture Audio Source |
|kAudioSourceTypeInternal |1 |RTC SDK internal acquisition audio source |


<span id="RemoteStreamKey"></span>
# RemoteStreamKey

```c#
struct bytertc::RemoteStreamKey
```


Information about the remote stream

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[RoomID](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamKey-roomid) |
|string |[UserID](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamKey-userid) |
|StreamIndex |[streamIndex](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamKey-streamindex) |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|bool |[operator==](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamKey-operator==) |
|bool |[operator!=](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamKey-operator!=) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamKey-roomid"></span>
### RoomID

```c#
string bytertc.RemoteStreamKey.RoomID
```


The room ID of the media stream.

<span id="RemoteStreamKey-userid"></span>
### UserID

```c#
string bytertc.RemoteStreamKey.UserID
```


The ID of the user who published the stream.

<span id="RemoteStreamKey-streamindex"></span>
### streamIndex

```c#
StreamIndex bytertc.RemoteStreamKey.streamIndex
```


Stream type. See [StreamIndex](https://docs.byteplus.com/en/docs/12/35817#StreamIndex)

<span id="instructions"></span>
## Instructions

<span id="RemoteStreamKey-operator=="></span>
### operator==

```c#
static bool bytertc.RemoteStreamKey.operator==(
    RemoteStreamKey l,
    RemoteStreamKey r
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|l |RemoteStreamKey |\- |
|r |RemoteStreamKey |\- |


<span id="RemoteStreamKey-operator!="></span>
### operator!=

```c#
static bool bytertc.RemoteStreamKey.operator!=(
    RemoteStreamKey l,
    RemoteStreamKey r
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|l |RemoteStreamKey |\- |
|r |RemoteStreamKey |\- |


<span id="VideoSinkPixelFormat"></span>
# VideoSinkPixelFormat

```c#
enum class bytertc.VideoSinkPixelFormat
```


Video frame encoding format

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kI420 |VideoPixelFormat.kVideoPixelFormatI420 |YUV I420 |
|kOriginal |VideoPixelFormat.kVideoPixelFormatUnknown |Original format |


<span id="MultiRoomConfig"></span>
# MultiRoomConfig

```c#
class bytertc::MultiRoomConfig
```


Multi\-room parameter configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|RoomProfileType |[roomProfileType](https://docs.byteplus.com/en/docs/12/35817#MultiRoomConfig-roomprofiletype) |
|bool |[is_auto_publish](https://docs.byteplus.com/en/docs/12/35817#MultiRoomConfig-is_auto_publish) |
|bool |[isAutoSubscribeAudio](https://docs.byteplus.com/en/docs/12/35817#MultiRoomConfig-isautosubscribeaudio) |
|bool |[isAutoSubscribeVideo](https://docs.byteplus.com/en/docs/12/35817#MultiRoomConfig-isautosubscribevideo) |
|RemoteVideoConfig |[remoteVideoConfig](https://docs.byteplus.com/en/docs/12/35817#MultiRoomConfig-remotevideoconfig) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MultiRoomConfig |[MultiRoomConfig](https://docs.byteplus.com/en/docs/12/35817#MultiRoomConfig-multiroomconfig) |


<span id="instructions"></span>
## Instructions

<span id="MultiRoomConfig-roomprofiletype"></span>
### roomProfileType

```c#
RoomProfileType bytertc.MultiRoomConfig.roomProfileType
```


Room mode. See [RoomProfileType](https://docs.byteplus.com/en/docs/12/35817#RoomProfileType), the default is normal audio & video call mode, which cannot be changed after entering the room.

<span id="MultiRoomConfig-is_auto_publish"></span>
### is_auto_publish

```c#
bool bytertc.MultiRoomConfig.is_auto_publish
```


Whether to publish media streams automatically. The default is automatic publishing. Only one of the rooms the user joined can be set to auto\-publish. If no settings are made in each room, the stream is automatically published in the first room joined by default. If you call [SetUserVisibility](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setuservisibility) to set your own visibility to false, you will not publish media streams regardless of the value of `is_auto_publish`.

<span id="MultiRoomConfig-isautosubscribeaudio"></span>
### isAutoSubscribeAudio

```c#
bool bytertc.MultiRoomConfig.isAutoSubscribeAudio
```


Whether to automatically subscribe to the audio stream, the default is automatic subscription

<span id="MultiRoomConfig-isautosubscribevideo"></span>
### isAutoSubscribeVideo

```c#
bool bytertc.MultiRoomConfig.isAutoSubscribeVideo
```


Whether to automatically subscribe to the video stream, the default is automatic subscription

<span id="MultiRoomConfig-remotevideoconfig"></span>
### remoteVideoConfig

```c#
RemoteVideoConfig bytertc.MultiRoomConfig.remoteVideoConfig
```


Expected configuration of remote video stream, see [RemoteVideoConfig](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoConfig).

<span id="instructions"></span>
## Instructions

<span id="MultiRoomConfig-multiroomconfig"></span>
### MultiRoomConfig

```c#
bytertc.MultiRoomConfig.MultiRoomConfig(
    RoomProfileType roomProfile=RoomProfileType.kRoomProfileTypeCommunication,
    bool Is_auto_publish=true,
    bool IsAutoSubscribeAudio=true,
    bool IsAutoSubscribeVideo=true
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomProfile |RoomProfileType |\- |
|Is_auto_publish |bool |\- |
|IsAutoSubscribeAudio |bool |\- |
|IsAutoSubscribeVideo |bool |\- |


<span id="VideoEncoderConfig"></span>
# VideoEncoderConfig

```c#
struct bytertc::VideoEncoderConfig
```


Video stream configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[Width](https://docs.byteplus.com/en/docs/12/35817#VideoEncoderConfig-width) |
|int |[Height](https://docs.byteplus.com/en/docs/12/35817#VideoEncoderConfig-height) |
|int |[FrameRate](https://docs.byteplus.com/en/docs/12/35817#VideoEncoderConfig-framerate) |
|int |[MaxBitrate](https://docs.byteplus.com/en/docs/12/35817#VideoEncoderConfig-maxbitrate) |
|int |[MinBitrate](https://docs.byteplus.com/en/docs/12/35817#VideoEncoderConfig-minbitrate) |
|VideoEncodePreference |[EncoderPreference](https://docs.byteplus.com/en/docs/12/35817#VideoEncoderConfig-encoderpreference) |


<span id="instructions"></span>
## Instructions

<span id="VideoEncoderConfig-width"></span>
### Width

```c#
int bytertc.VideoEncoderConfig.Width
```


Width of the video frame in px

<span id="VideoEncoderConfig-height"></span>
### Height

```c#
int bytertc.VideoEncoderConfig.Height
```


Height of the video frame in px

<span id="VideoEncoderConfig-framerate"></span>
### FrameRate

```c#
int bytertc.VideoEncoderConfig.FrameRate
```


Video frame rate in fps

<span id="VideoEncoderConfig-maxbitrate"></span>
### MaxBitrate

```c#
int bytertc.VideoEncoderConfig.MaxBitrate
```


Maximum bit rate in kbps. Optional for internal capturing while mandatory for custom capturing. The default value is \-1 in internal capturing mode, SDK will automatically calculate the applicable bit rate based on the input resolution and frame rate. No stream will be encoded and published if you set this parameter to 0.

<span id="VideoEncoderConfig-minbitrate"></span>
### MinBitrate

```c#
int bytertc.VideoEncoderConfig.MinBitrate
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `MinBitrate`. It defaults to `0`. It ranges within [0, MaxBitrate). When `MaxBitrate` < `MinBitrate`, the bitrate is self\-adpapted. In the following circumstance, the assignment to this variable has no effect:


* When `MaxBitrate` = `0`, the video encoding is disabled.

* When `MaxBitrate` < `0`, the bitrate is self\-adapted.


<span id="VideoEncoderConfig-encoderpreference"></span>
### EncoderPreference

```c#
VideoEncodePreference bytertc.VideoEncoderConfig.EncoderPreference
```


Encoding policy preference. See [VideoEncodePreference](https://docs.byteplus.com/en/docs/12/35817#VideoEncodePreference).

<span id="CapturePreference"></span>
# CapturePreference

```c#
enum class bytertc.CapturePreference
```


Video capture preference

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|KAuto |0 |(Default) Video capture preference: auto SDK determines the best video capture parameters referring to the camera output parameters and the encoder configuration. |
|KManual |1 |Video capture preference: manual Set the resolution and the frame rate manually. |
|KAutoPerformance |2 |Video capture preference: encoder configuration The capture parameters are the same with the parameters set in [SetVideoEncoderConfig1](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideoencoderconfig1). |


<span id="VirtualBackgroundSource"></span>
# VirtualBackgroundSource

```c#
struct bytertc::VirtualBackgroundSource
```


Virtual background object.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VirtualBackgroundSourceType |[source_type](https://docs.byteplus.com/en/docs/12/35817#VirtualBackgroundSource-source_type) |
|uint |[source_color](https://docs.byteplus.com/en/docs/12/35817#VirtualBackgroundSource-source_color) |
|string |[source_path](https://docs.byteplus.com/en/docs/12/35817#VirtualBackgroundSource-source_path) |


<span id="instructions"></span>
## Instructions

<span id="VirtualBackgroundSource-source_type"></span>
### source_type

```c#
VirtualBackgroundSourceType bytertc.VirtualBackgroundSource.source_type
```


See [VirtualBackgroundSourceType](https://docs.byteplus.com/en/docs/12/35817#VirtualBackgroundSourceType).

<span id="VirtualBackgroundSource-source_color"></span>
### source_color

```c#
uint bytertc.VirtualBackgroundSource.source_color
```


The solid color of the background. The format is 0xAARRGGBB.

<span id="VirtualBackgroundSource-source_path"></span>
### source_path

```c#
string bytertc.VirtualBackgroundSource.source_path
```


The absolute path of the specified image.


* You can upload a .JPG, .PNG, or .JPEG file.

* The image with a resolution higher than 1080p(Full HD) will be rescaled proportionally to fit in the video.

* If the image's aspect ratio matches the video's, the image will be rescaled proportionally to fit in the video.

* If the image’s aspect ratio doesn't match the video's, the shortest side (either height or width) of the image will be stretched proportionally to match the video. Then the image will be cropped to fill in the video.

* The transparent area in the image will be filled with black.


<span id="ScreenCaptureParameters"></span>
# ScreenCaptureParameters

```c#
struct bytertc::ScreenCaptureParameters
```


Screen internal capture parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ContentHint |[ContentHint](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureParameters-contenthint) |
|Rectangle |[RegionRect](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureParameters-regionrect) |
|MouseCursorCaptureState |[CaptureMouseCursor](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureParameters-capturemousecursor) |
|ScreenFilterConfig |[FilterConfig](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureParameters-filterconfig) |
|HighlightConfig |[HighlightConfig](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureParameters-highlightconfig) |


<span id="instructions"></span>
## Instructions

<span id="ScreenCaptureParameters-contenthint"></span>
### ContentHint

```c#
ContentHint bytertc.ScreenCaptureParameters.ContentHint
```


Content hint. See [ContentHint](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureParameters-contenthint).

<span id="ScreenCaptureParameters-regionrect"></span>
### RegionRect

```c#
Rectangle bytertc.ScreenCaptureParameters.RegionRect
```


Collection area. See [Rectangle](https://docs.byteplus.com/en/docs/12/35817#Rectangle).

<span id="ScreenCaptureParameters-capturemousecursor"></span>
### CaptureMouseCursor

```c#
MouseCursorCaptureState bytertc.ScreenCaptureParameters.CaptureMouseCursor
```


To collect mouse status. See [MouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/35817#MouseCursorCaptureState).

<span id="ScreenCaptureParameters-filterconfig"></span>
### FilterConfig

```c#
ScreenFilterConfig bytertc.ScreenCaptureParameters.FilterConfig
```


Screen filtering settings. See [ScreenFilterConfig](https://docs.byteplus.com/en/docs/12/35817#ScreenFilterConfig).

<span id="ScreenCaptureParameters-highlightconfig"></span>
### HighlightConfig

```c#
HighlightConfig bytertc.ScreenCaptureParameters.HighlightConfig
```


For the border highlighting settings of the acquisition area. See [HighlightConfig](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureParameters-highlightconfig).

<span id="VideoRotationMode"></span>
# VideoRotationMode

```c#
enum class bytertc.VideoRotationMode
```


Video rotation mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoRotationModeFollowApp |0 |Follow the rotation of app. |
|kVideoRotationModeFollowGSensor |1 |Follow the rotation of the G sensor. |


<span id="EarMonitorMode"></span>
# EarMonitorMode

```c#
enum class bytertc.EarMonitorMode
```


Whether or not in\-ear monitoring is enabled.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kEarMonitorModeOff |0 |Disabled (default) |
|kEarMonitorModeOn |1 |Enabled |


<span id="NetworkQuality"></span>
# NetworkQuality

```c#
enum class bytertc.NetworkQuality
```


Media streaming network quality.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kNetworkQualityUnknown |0 |Network quality unknown. |
|kNetworkQualityExcellent |1 |The network quality is excellent. |
|kNetworkQualityGood |2 |The subjective feeling is similar to kNetworkQualityExcellent, but the bit rate may be slightly lower. |
|kNetworkQualityPoor |3 |Subjective feelings are flawed but do not affect communication. |
|kNetworkQualityBad |4 |Can barely communicate but not smoothly. |
|kNetworkQualityVbad |5 |The quality of the network is very poor and communication is basically impossible. |


<span id="RemoteVideoStats"></span>
# RemoteVideoStats

```c#
struct bytertc::RemoteVideoStats
```


Remote video stream statistics, reference period 2s. After the local user subscribes to the remote video stream successfully, the SDK will periodically notify the local user of the reception status of the remote video stream subscribed by `OnRemoteStreamStatsEventHandler` During this reference period. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-height) |
|float |[video_loss_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-video_loss_rate) |
|int |[received_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-received_kbitrate) |
|int |[decoder_output_frame_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-decoder_output_frame_rate) |
|int |[renderer_output_frame_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-renderer_output_frame_rate) |
|int |[stall_count](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-stall_count) |
|int |[stall_duration](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-stall_duration) |
|long |[e2e_delay](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-e2e_delay) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-is_screen) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-stats_interval) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-rtt) |
|int |[frozen_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-frozen_rate) |
|int |[video_index](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-video_index) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats-jitter) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoStats-width"></span>
### width

```c#
int bytertc.RemoteVideoStats.width
```


Remote Video Stream Width

<span id="RemoteVideoStats-height"></span>
### height

```c#
int bytertc.RemoteVideoStats.height
```


Remote Video Stream Height

<span id="RemoteVideoStats-video_loss_rate"></span>
### video_loss_rate

```c#
float bytertc.RemoteVideoStats.video_loss_rate
```


Video packet loss rate. The video downlink packet loss rate in the reference period, in units of %, and the value range is [0,1].

<span id="RemoteVideoStats-received_kbitrate"></span>
### received_kbitrate

```c#
int bytertc.RemoteVideoStats.received_kbitrate
```


Receiving bit rate. Video reception rate within the reference period, in kbps.

<span id="RemoteVideoStats-decoder_output_frame_rate"></span>
### decoder_output_frame_rate

```c#
int bytertc.RemoteVideoStats.decoder_output_frame_rate
```


The decoder outputs the frame rate. Video decoder output frame rate within the reference period, in fps.

<span id="RemoteVideoStats-renderer_output_frame_rate"></span>
### renderer_output_frame_rate

```c#
int bytertc.RemoteVideoStats.renderer_output_frame_rate
```


Render frame rate. The video rendering frame rate in the reference period, in fps.

<span id="RemoteVideoStats-stall_count"></span>
### stall_count

```c#
int bytertc.RemoteVideoStats.stall_count
```


Number of cards. Number of cards in the reference period.

<span id="RemoteVideoStats-stall_duration"></span>
### stall_duration

```c#
int bytertc.RemoteVideoStats.stall_duration
```


Catton duration. The total duration of the video card in the reference period. Unit ms.

<span id="RemoteVideoStats-e2e_delay"></span>
### e2e_delay

```c#
long bytertc.RemoteVideoStats.e2e_delay
```


User experience\-level end\-to\-end delay, in milliseconds, from the time when the sender captures the encoding to the time when the receiver decodes the rendering

<span id="RemoteVideoStats-is_screen"></span>
### is_screen

```c#
bool bytertc.RemoteVideoStats.is_screen
```


Whether the media stream belongs to the user is a screen stream. You can know whether the current statistics come from mainstream or screen stream.

<span id="RemoteVideoStats-stats_interval"></span>
### stats_interval

```c#
int bytertc.RemoteVideoStats.stats_interval
```


Statistical interval, the interval of this reference period, in ms. This field is used to set the reference period for the callback, currently set to 2s.

<span id="RemoteVideoStats-rtt"></span>
### rtt

```c#
int bytertc.RemoteVideoStats.rtt
```


Round\-trip time in ms.

<span id="RemoteVideoStats-frozen_rate"></span>
### frozen_rate

```c#
int bytertc.RemoteVideoStats.frozen_rate
```


The cumulative duration of the video card of the remote user accounts for the percentage (%) of the total effective duration of the video after entering the room. The effective duration of the video refers to the duration of the video other than stopping sending the video stream and disabling the video module after the remote user enters the room to publish the video stream.

<span id="RemoteVideoStats-video_index"></span>
### video_index

```c#
int bytertc.RemoteVideoStats.video_index
```


For subscripts for streams with multiple resolutions.

<span id="RemoteVideoStats-jitter"></span>
### jitter

```c#
int bytertc.RemoteVideoStats.jitter
```


Video downlink network jitter in ms.

<span id="RemoteAudioState"></span>
# RemoteAudioState

```c#
enum class bytertc.RemoteAudioState
```


Remote audio stream state. Users can learn about this status through `OnRemoteAudioStateChangedEventHandler`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteAudioStateStopped |0 |The remote audio stream is not received. The callback `OnRemoteAudioStateChangedEventHandler` triggers:<br><br><br>* Local users stop receiving remote audio streams due to [kRemoteAudioStateChangeReasonLocalMuted](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* The remote user stops sending audio streams due to [kRemoteAudioStateChangeReasonRemoteMuted](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* The remote user left the room, the corresponding reason is: [kRemoteAudioStateChangeReasonRemoteOffline](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason) |
|kRemoteAudioStateStarting |1 |Start receiving the remote audio stream header. Just received the remote audio stream header will trigger a callback `OnRemoteAudioStateChangedEventHandler`, The corresponding reason is: [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason) in "kRemoteAudioStateChangeReasonLocalUnmuted" |
|kRemoteAudioStateDecoding |2 |The remote audio stream is decoding and playing normally. A callback is triggered in the following cases: `OnRemoteAudioStateChangedEventHandler`:<br><br><br>* The remote audio first frame was successfully decoded, and the corresponding reason is: 'kRemoteAudioStateChangeReasonLocalUnmuted' in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* The network returned to normal from blocking, and the corresponding reason is: "kRemoteAudioStateChangeReasonNetworkRecovery ' in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* Local users resume receiving remote audio streams, and the corresponding reason is 'kRemoteAudioStateChangeReasonLocalUnmuted ' [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason)<br><br>* Remote users resume sending audio streams, and the corresponding reason is 'kRemoteAudioStateChangeReasonRemoteUnmuted' in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason) |
|kRemoteAudioStateFrozen |3 |Remote audio streaming card. A callback is triggered when the network is blocked and the packet loss rate is greater than 40%. `OnRemoteAudioStateChangedEventHandler`, The corresponding reason is: "kRemoteAudioStateChangeReasonNetworkCongestion" in [kRemoteAudioStateChangeReasonNetworkCongestion}](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStateChangeReason-kremoteaudiostatechangereasonnetworkcongestion) |


<span id="ForwardStreamState"></span>
# ForwardStreamState

```c#
enum class bytertc.ForwardStreamState
```


Forwarding state of media streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kForwardStreamStateIdle |0 |Idle state<br><br><br>* After calling `stopForwardStreamToRooms`, all target rooms are in idle state.<br><br>* After calling `updateForwardStreamToRooms` to reduce target rooms, the target rooms you reduced are in idle state. |
|kForwardStreamStateSuccess |1 |Start forwarding<br><br><br>* After calling `startForwardStreamToRooms`, return this state after successfully forwarding the media stream to all rooms.<br><br>* After calling `updateForwardStreamToRooms`, return this state after successfully forwarding the media stream to the newly added target rooms. |
|kForwardStreamStateFailure |2 |Forwarding failure, failure details refer to [ForwardStreamError](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamError) After calling `startForwardStreamToRooms` or `updateForwardStreamToRooms`, if a failure occurs, return this state. |


<span id="RtcRoomStats"></span>
# RtcRoomStats

```c#
struct bytertc::RtcRoomStats
```


Call related statistics

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[txLostrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-txlostrate) |
|float |[rxLostrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-rxlostrate) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-rtt) |
|uint |[duration](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-duration) |
|uint |[tx_bytes](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-tx_bytes) |
|uint |[rx_bytes](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-rx_bytes) |
|ushort |[tx_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-tx_kbitrate) |
|ushort |[rx_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-rx_kbitrate) |
|ushort |[rx_audio_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-rx_audio_kbitrate) |
|ushort |[tx_audio_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-tx_audio_kbitrate) |
|ushort |[rx_video_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-rx_video_kbitrate) |
|ushort |[tx_video_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-tx_video_kbitrate) |
|uint |[user_count](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-user_count) |
|double |[cpu_app_usage](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-cpu_app_usage) |
|double |[cpu_total_usage](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-cpu_total_usage) |
|int |[tx_jitter](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-tx_jitter) |
|int |[rx_jitter](https://docs.byteplus.com/en/docs/12/35817#RtcRoomStats-rx_jitter) |


<span id="instructions"></span>
## Instructions

<span id="RtcRoomStats-txlostrate"></span>
### txLostrate

```c#
float bytertc.RtcRoomStats.txLostrate
```


The uplink packet loss rate currently applied, the value range is [0,1]

<span id="RtcRoomStats-rxlostrate"></span>
### rxLostrate

```c#
float bytertc.RtcRoomStats.rxLostrate
```


The downlink packet loss rate of the current application, the value range is [0,1]

<span id="RtcRoomStats-rtt"></span>
### rtt

```c#
int bytertc.RtcRoomStats.rtt
```


Round\-trip time (in ms) for client side to server level data transfers

<span id="RtcRoomStats-duration"></span>
### duration

```c#
uint bytertc.RtcRoomStats.duration
```


The duration, in seconds, that the local user has spent in the room.

<span id="RtcRoomStats-tx_bytes"></span>
### tx_bytes

```c#
uint bytertc.RtcRoomStats.tx_bytes
```


The total number of bytes sent by the local user (bytes), the cumulative value

<span id="RtcRoomStats-rx_bytes"></span>
### rx_bytes

```c#
uint bytertc.RtcRoomStats.rx_bytes
```


The total number of bytes received by the local user (bytes), the cumulative value

<span id="RtcRoomStats-tx_kbitrate"></span>
### tx_kbitrate

```c#
ushort bytertc.RtcRoomStats.tx_kbitrate
```


Send bit rate (kbps), get the instantaneous value of the data

<span id="RtcRoomStats-rx_kbitrate"></span>
### rx_kbitrate

```c#
ushort bytertc.RtcRoomStats.rx_kbitrate
```


Receive bit rate (kbps), get the instantaneous value of the data

<span id="RtcRoomStats-rx_audio_kbitrate"></span>
### rx_audio_kbitrate

```c#
ushort bytertc.RtcRoomStats.rx_audio_kbitrate
```


The transmission rate (kbps) of the audio packet, the instantaneous value when obtaining the data

<span id="RtcRoomStats-tx_audio_kbitrate"></span>
### tx_audio_kbitrate

```c#
ushort bytertc.RtcRoomStats.tx_audio_kbitrate
```


Audio receiving bit rate (kbps), obtaining the instantaneous value of the data

<span id="RtcRoomStats-rx_video_kbitrate"></span>
### rx_video_kbitrate

```c#
ushort bytertc.RtcRoomStats.rx_video_kbitrate
```


Video transmission rate (kbps), the instantaneous value when obtaining the data

<span id="RtcRoomStats-tx_video_kbitrate"></span>
### tx_video_kbitrate

```c#
ushort bytertc.RtcRoomStats.tx_video_kbitrate
```


Video receiving bit rate (kbps), the instantaneous value when obtaining the data

<span id="RtcRoomStats-user_count"></span>
### user_count

```c#
uint bytertc.RtcRoomStats.user_count
```


Number of visible users in the current room

<span id="RtcRoomStats-cpu_app_usage"></span>
### cpu_app_usage

```c#
double bytertc.RtcRoomStats.cpu_app_usage
```


Current application CPU usage (%)

<span id="RtcRoomStats-cpu_total_usage"></span>
### cpu_total_usage

```c#
double bytertc.RtcRoomStats.cpu_total_usage
```


Current system CPU usage (%)

<span id="RtcRoomStats-tx_jitter"></span>
### tx_jitter

```c#
int bytertc.RtcRoomStats.tx_jitter
```


Tx jitter(ms)

<span id="RtcRoomStats-rx_jitter"></span>
### rx_jitter

```c#
int bytertc.RtcRoomStats.rx_jitter
```


Rx jitter(ms)

<span id="ProblemFeedbackRoomInfo"></span>
# ProblemFeedbackRoomInfo

```c#
struct bytertc::ProblemFeedbackRoomInfo
```


Room information for audio & video quality feedback

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[room_id](https://docs.byteplus.com/en/docs/12/35817#ProblemFeedbackRoomInfo-room_id) |
|string |[user_id](https://docs.byteplus.com/en/docs/12/35817#ProblemFeedbackRoomInfo-user_id) |


<span id="instructions"></span>
## Instructions

<span id="ProblemFeedbackRoomInfo-room_id"></span>
### room_id

```c#
string bytertc.ProblemFeedbackRoomInfo.room_id
```


Room ID.

<span id="ProblemFeedbackRoomInfo-user_id"></span>
### user_id

```c#
string bytertc.ProblemFeedbackRoomInfo.user_id
```


The ID of the local user.

<span id="SubscribeState"></span>
# SubscribeState

```c#
enum class bytertc.SubscribeState
```


Subscription status of media streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSubscribeStateSuccess |0 |Successfully changed the subscription status |
|kSubscribeStateFailedNotInRoom |1 |Failed to change the subscription status, because you were not in the room. |
|kSubscribeStateFailedStreamNotFound |2 |Failed to change the subscription status, because the target audio/video stream was not found. |
|kSubscribeStateFailedOverLimit |3 |Failed to change the subscription status, because the number of streams you have subscribed to has exceeded the limit. |


<span id="VoiceEqualizationConfig"></span>
# VoiceEqualizationConfig

```c#
struct bytertc::VoiceEqualizationConfig
```


Voice equalization effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VoiceEqualizationBandFrequency |[frequency](https://docs.byteplus.com/en/docs/12/35817#VoiceEqualizationConfig-frequency) |
|int |[gain](https://docs.byteplus.com/en/docs/12/35817#VoiceEqualizationConfig-gain) |


<span id="instructions"></span>
## Instructions

<span id="VoiceEqualizationConfig-frequency"></span>
### frequency

```c#
VoiceEqualizationBandFrequency bytertc.VoiceEqualizationConfig.frequency
```


Frequency band. See [VoiceEqualizationBandFrequency](https://docs.byteplus.com/en/docs/12/35817#VoiceEqualizationBandFrequency).

<span id="VoiceEqualizationConfig-gain"></span>
### gain

```c#
int bytertc.VoiceEqualizationConfig.gain
```


Gain of the frequency band in dB. The range is `[-15, 15]`.

<span id="MirrorType"></span>
# MirrorType

```c#
enum class bytertc.MirrorType
```


Mirror type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMirrorTypeNone |0 |The preview and the published video stream are not mirrored. |
|kMirrorTypeRender |1 |The preview is mirrored. The published video stream is not mirrored. |
|kMirrorTypeRenderAndEncoder |3 |The preview and the published video stream are mirrored. |


<span id="VoiceEqualizationBandFrequency"></span>
# VoiceEqualizationBandFrequency

```c#
enum class bytertc.VoiceEqualizationBandFrequency
```


Audio Equalization effect.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVoiceEqualizationBandFrequency31 |0 |The frequency band with a center frequency of 31Hz. |
|kVoiceEqualizationBandFrequency62 |1 |The frequency band with a center frequency of 62Hz. |
|kVoiceEqualizationBandFrequency125 |2 |The frequency band with a center frequency of 125Hz. |
|kVoiceEqualizationBandFrequency250 |3 |The frequency band with a center frequency of 250Hz. |
|kVoiceEqualizationBandFrequency500 |4 |The frequency band with a center frequency of 500Hz. |
|kVoiceEqualizationBandFrequency1k |5 |The frequency band with a center frequency of 1kHz. |
|kVoiceEqualizationBandFrequency2k |6 |The frequency band with a center frequency of 2kHz. |
|kVoiceEqualizationBandFrequency4k |7 |The frequency band with a center frequency of 4kHz. |
|kVoiceEqualizationBandFrequency8k |8 |The frequency band with a center frequency of 8kHz. |
|kVoiceEqualizationBandFrequency16k |9 |The frequency band with a center frequency of 16kHz. |


<span id="PauseResumeControlMediaType"></span>
# PauseResumeControlMediaType

```c#
enum class bytertc.PauseResumeControlMediaType
```


Pause/resume receiving the remote media stream type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRTCPauseResumeControlMediaTypeAudio |0 |Only control audio, not affect video |
|kRTCPauseResumeControlMediaTypeVideo |1 |Only control video, not affect audio |
|kRTCPauseResumeControlMediaTypeVideoAndAudio |2 |Simultaneous control of audio and video |


<span id="VoiceReverbType"></span>
# VoiceReverbType

```c#
enum class bytertc.VoiceReverbType
```


Reverb effect type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVoiceReverbTypeOriginal |0 |Acoustic, no special effects |
|kVoiceReverbTypeEcho |1 |Echo |
|kVoiceReverbTypeConcert |2 |Concert |
|kVoiceReverbTypeEthereal |3 |Ethereal |
|kVoiceReverbTypeKTV |4 |Karaoke |
|kVoiceReverbTypeStudio |5 |Recording studio |
|kVoiceReverbTypeVirtualStereo |6 |Virtual Stereo |
|kVoiceReverbTypeSpacious |7 |Spacious |
|kVoiceReverbType3D |8 |3D vocal |


<span id="FirstFramePlayState"></span>
# FirstFramePlayState

```c#
enum class bytertc.FirstFramePlayState
```


First frame playback status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kFirstFramePlayStatePlaying |0 |Playing |
|kFirstFramePlayStatePlayed |1 |Play success |
|kFirstFramePlayStateEnd |2 |Play failed |


<span id="VideoRotation"></span>
# VideoRotation

```c#
enum class bytertc.VideoRotation
```


Video frame rotation angle

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoRotation0 |0 |Video does not rotate |
|kVideoRotation90 |90 |Video rotate 90 degrees clockwise |
|kVideoRotation180 |180 |Video rotate 180 degrees clockwise |
|kVideoRotation270 |270 |Video rotate 270 degrees clockwise |


<span id="ProblemFeedbackOption"></span>
# ProblemFeedbackOption

```c#
enum class bytertc.ProblemFeedbackOption
```


Audio & video quality feedback problem type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kProblemFeedbackOptionNone |0 |No problem |
|kProblemFeedbackOptionOtherMessage |1 << 0 |Other issues |
|kProblemFeedbackOptionAudioNotClear |1 << 1 |Unclear voice |
|kProblemFeedbackOptionVideoNotClear |1 << 2 |Video is not clear |
|kProblemFeedbackOptionNotSync |1 << 3 |Audio & video out of sync |
|kProblemFeedbackOptionAudioLagging |1 << 4 |Audio card |
|kProblemFeedbackOptionVideoLagging |1 << 5 |Video card |
|kProblemFeedbackOptionDisconnected |1 << 6 |Connection failed |
|kProblemFeedbackOptionNoAudio |1 << 7 |No sound |
|kProblemFeedbackOptionNoVideo |1 << 8 |No picture |
|kProblemFeedbackOptionAudioStrength |1 << 9 |Too little sound |
|kProblemFeedbackOptionEcho |1 << 10 |Echo noise |
|KFeedbackOptionEarBackDelay |1 << 11 |Large delay in earphone monitoring |


<span id="SysStats"></span>
# SysStats

```c#
struct bytertc::SysStats
```


System statistics.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|uint |[CpuCores](https://docs.byteplus.com/en/docs/12/35817#SysStats-cpucores) |
|double |[CpuAppUsage](https://docs.byteplus.com/en/docs/12/35817#SysStats-cpuappusage) |
|double |[CpuTotalUsage](https://docs.byteplus.com/en/docs/12/35817#SysStats-cputotalusage) |
|double |[MemoryUsage](https://docs.byteplus.com/en/docs/12/35817#SysStats-memoryusage) |
|ulong |[FullMemory](https://docs.byteplus.com/en/docs/12/35817#SysStats-fullmemory) |
|ulong |[TotalMemoryUsage](https://docs.byteplus.com/en/docs/12/35817#SysStats-totalmemoryusage) |
|ulong |[FreeMemory](https://docs.byteplus.com/en/docs/12/35817#SysStats-freememory) |
|double |[MemoryRatio](https://docs.byteplus.com/en/docs/12/35817#SysStats-memoryratio) |
|double |[TotalMemoryRatio](https://docs.byteplus.com/en/docs/12/35817#SysStats-totalmemoryratio) |


<span id="instructions"></span>
## Instructions

<span id="SysStats-cpucores"></span>
### CpuCores

```c#
uint bytertc.SysStats.CpuCores
```


Number of CPU cores.

<span id="SysStats-cpuappusage"></span>
### CpuAppUsage

```c#
double bytertc.SysStats.CpuAppUsage
```


Current application CPU usage (%)

<span id="SysStats-cputotalusage"></span>
### CpuTotalUsage

```c#
double bytertc.SysStats.CpuTotalUsage
```


Current system CPU usage (%)

<span id="SysStats-memoryusage"></span>
### MemoryUsage

```c#
double bytertc.SysStats.MemoryUsage
```


Memory usage of the current app (in MB)

<span id="SysStats-fullmemory"></span>
### FullMemory

```c#
ulong bytertc.SysStats.FullMemory
```


Full memory (in MB)

<span id="SysStats-totalmemoryusage"></span>
### TotalMemoryUsage

```c#
ulong bytertc.SysStats.TotalMemoryUsage
```


System used memory (in MB)

<span id="SysStats-freememory"></span>
### FreeMemory

```c#
ulong bytertc.SysStats.FreeMemory
```


Free allocable memory (in MB)

<span id="SysStats-memoryratio"></span>
### MemoryRatio

```c#
double bytertc.SysStats.MemoryRatio
```


Memory usage of the current application (in %)

<span id="SysStats-totalmemoryratio"></span>
### TotalMemoryRatio

```c#
double bytertc.SysStats.TotalMemoryRatio
```


System memory usage (in %)

<span id="LocalAudioStreamState"></span>
# LocalAudioStreamState

```c#
enum class bytertc.LocalAudioStreamState
```


Local audio stream status. SDK callbacks local audio stream status via `OnLocalAudioStateChangedEventHandler`

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalAudioStreamStateStopped |0 |The default initial state of the local audio. Callback to this state when the microphone stops working, corresponding to the error code kLocalAudioStreamErrorOk |
|kLocalAudioStreamStateRecording |1 |The local audio recording device started successfully. Callback to the state when the first frame of audio is collected, corresponding to the error code kLocalAudioStreamErrorOk |
|kLocalAudioStreamStateEncoding |2 |The first frame of the local audio was successfully encoded. Callback to the state when the audio first frame encoding is successful, corresponding to the error code kLocalAudioStreamErrorOk |
|kLocalAudioStreamStateFailed |3 |The local audio startup failed, and the status is called back at the following times:<br><br><br>* The local recording device failed to start, corresponding to the error code kLocalAudioStreamErrorRecordFailure<br><br>* No recording device permission was detected, corresponding to the error code kLocalAudioStreamErrorDeviceNoPermission<br><br>* The audio encoding failed, corresponding to the error code kLocalAudioStreamErrorEncodeFailure |
|kLocalAudioStreamMute |4 |Callback the state after the local audio is successfully muted. Callback after successful [SetAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudiocapturedevicemute) call, corresponding to kLocalAudioStreamErrorOk in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-191861#LocalAudioStreamError). |
|kLocalAudioStreamUnmute |5 |Callback the state after the local audio is successfully unmuted. Callback after successful [SetAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudiocapturedevicemute) call, corresponding to kLocalAudioStreamErrorOk in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-191861#LocalAudioStreamError). |


<span id="ConnectionState"></span>
# ConnectionState

```c#
enum class bytertc.ConnectionState
```


SDK Connection status with the signaling server.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kConnectionStateDisconnected |1 |Connection disconnected. |
|kConnectionStateConnecting |2 |First connection, connecting now. |
|kConnectionStateConnected |3 |The first connection was successful. |
|kConnectionStateReconnecting |4 |Reconnect after disconnection. |
|kConnectionStateReconnected |5 |Successful reconnection after disconnection. |
|kConnectionStateLost |6 |If the network connection is disconnected for more than 10 seconds, it will continue to reconnect. |


<span id="ContentHint"></span>
# ContentHint

```c#
enum class bytertc.ContentHint
```


Content hints of the internally captured screen video stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kContentHintDetails |0 |Detailed content. Recommended when you capture documents, images, etc. |
|kContentHintMotion |1 |Animation content. Recommended when you capture videos, games, etc. |


<span id="VideoPixelFormat"></span>
# VideoPixelFormat

```c#
enum class bytertc.VideoPixelFormat
```


Encoding format for video frame color

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoPixelFormatUnknown |0 |Unknown format |
|kVideoPixelFormatI420 |1 |YUV I420 |
|kVideoPixelFormatNV12 |2 |YUV NV12 |
|kVideoPixelFormatNV21 |3 |YUV NV21 |
|kVideoPixelFormatRGB24 |4 |RGB 24bit |
|kVideoPixelFormatRGBA |5 |RGBA |
|kVideoPixelFormatARGB |6 |ARGB |
|kVideoPixelFormatBGRA |7 |BGRA |
|kVideoPixelFormatTexture2D |0x0DE1 |Texture2D |
|kVideoPixelFormatTextureOES |0x8D65 |TextureOES |


<span id="ForwardStreamEventInfo"></span>
# ForwardStreamEventInfo

```c#
struct bytertc::ForwardStreamEventInfo
```


The event that occurs in the cross\-room forwarding of media streams to different target rooms

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[room_id](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamEventInfo-room_id) |
|ForwardStreamEvent |[stream_event](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamEventInfo-stream_event) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamEventInfo-room_id"></span>
### room_id

```c#
string bytertc.ForwardStreamEventInfo.room_id
```


The room ID of the target room during the cross\-room forwarding of media streams.

<span id="ForwardStreamEventInfo-stream_event"></span>
### stream_event

```c#
ForwardStreamEvent bytertc.ForwardStreamEventInfo.stream_event
```


The event that occurs in the cross\-room forwarding of media streams to the target room. See [ForwardStreamEvent](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamEvent)

<span id="VideoFrame"></span>
# VideoFrame

```c#
struct bytertc::VideoFrame
```


Video frame structure

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VideoFrameType |[FrameType](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-frametype) |
|VideoPixelFormat |[PixelFormat](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-pixelformat) |
|long |[TimestampUs](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-timestampus) |
|int |[Width](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-width) |
|int |[Height](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-height) |
|VideoRotation |[Rotation](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-rotation) |
|ColorSpace |[ColorSpace](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-colorspace) |
|int |[NumberOfPlanes](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-numberofplanes) |
|byte[][] |[PlaneData](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-planedata) |
|int[] |[PlaneLineSize](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-planelinesize) |
|byte[] |[ExtraDataInfo](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-extradatainfo) |
|int |[ExtraDataInfoSize](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-extradatainfosize) |
|byte[] |[SupplementaryInfo](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-supplementaryinfo) |
|int |[SupplementaryInfoSize](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-supplementaryinfosize) |
|IntPtr |[HwaccelBuffer](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-hwaccelbuffer) |
|IntPtr |[HwaccelContext](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-hwaccelcontext) |
|float[] |[Matrix](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-matrix) |
|int |[TextureId](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-textureid) |


<span id="instructions"></span>
## Instructions

<span id="VideoFrame-frametype"></span>
### FrameType

```c#
VideoFrameType bytertc.VideoFrame.FrameType
```


Video frame type. See [VideoFrameType](https://docs.byteplus.com/en/docs/12/35817#VideoFrameType).

<span id="VideoFrame-pixelformat"></span>
### PixelFormat

```c#
VideoPixelFormat bytertc.VideoFrame.PixelFormat
```


Video frame format. See [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/35817#VideoPixelFormat).

<span id="VideoFrame-timestampus"></span>
### TimestampUs

```c#
long bytertc.VideoFrame.TimestampUs
```


Video frame timestamp in microseconds

<span id="VideoFrame-width"></span>
### Width

```c#
int bytertc.VideoFrame.Width
```


Video frame width in px

<span id="VideoFrame-height"></span>
### Height

```c#
int bytertc.VideoFrame.Height
```


Video frame height in px

<span id="VideoFrame-rotation"></span>
### Rotation

```c#
VideoRotation bytertc.VideoFrame.Rotation
```


Video frame rotation angle

<span id="VideoFrame-colorspace"></span>
### ColorSpace

```c#
ColorSpace bytertc.VideoFrame.ColorSpace
```


The color space of video frame, see [ColorSpace](https://docs.byteplus.com/en/docs/12/35817#VideoFrame-colorspace)

<span id="VideoFrame-numberofplanes"></span>
### NumberOfPlanes

```c#
int bytertc.VideoFrame.NumberOfPlanes
```


Gets Video frame color plane number YUV formats are categorized into planar format and packed format. In a planar format, the Y, U, and V components are stored separately as three planes, while in a packed format, the Y, U, and V components are stored in a single array.

<span id="VideoFrame-planedata"></span>
### PlaneData

```c#
byte [][] bytertc.VideoFrame.PlaneData
```


Plane data pointer

<span id="VideoFrame-planelinesize"></span>
### PlaneLineSize

```c#
int [] bytertc.VideoFrame.PlaneLineSize
```


The length of the data line in the specified plane

<span id="VideoFrame-extradatainfo"></span>
### ExtraDataInfo

```c#
byte [] bytertc.VideoFrame.ExtraDataInfo
```


Extended data pointer

<span id="VideoFrame-extradatainfosize"></span>
### ExtraDataInfoSize

```c#
int bytertc.VideoFrame.ExtraDataInfoSize
```


Size of extended data in bytes

<span id="VideoFrame-supplementaryinfo"></span>
### SupplementaryInfo

```c#
byte [] bytertc.VideoFrame.SupplementaryInfo
```


Supplementary data

<span id="VideoFrame-supplementaryinfosize"></span>
### SupplementaryInfoSize

```c#
int bytertc.VideoFrame.SupplementaryInfoSize
```


Size of supplementary data in bytes

<span id="VideoFrame-hwaccelbuffer"></span>
### HwaccelBuffer

```c#
IntPtr bytertc.VideoFrame.HwaccelBuffer
```


Local buffer pointer

<span id="VideoFrame-hwaccelcontext"></span>
### HwaccelContext

```c#
IntPtr bytertc.VideoFrame.HwaccelContext
```


Hardware accelerate context(AKA Opengl Context, Vulkan Context)

<span id="VideoFrame-matrix"></span>
### Matrix

```c#
float [] bytertc.VideoFrame.Matrix
```


Get Texture matrix (only for texture type frame)

<span id="VideoFrame-textureid"></span>
### TextureId

```c#
int bytertc.VideoFrame.TextureId
```


Get Texture ID (only for texture type frame)

<span id="LocalAudioStats"></span>
# LocalAudioStats

```c#
struct bytertc::LocalAudioStats
```


Local audio stream statistics, reference period 2s. After the local user publishes the audio stream successfully, the SDK will periodically notify the user through `OnLocalStreamStatsEventHandler` the transmission status of the published audio stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[audio_loss_rate](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-audio_loss_rate) |
|int |[send_kbitrate](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-send_kbitrate) |
|int |[record_sample_rate](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-record_sample_rate) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-stats_interval) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-rtt) |
|int |[num_channels](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-num_channels) |
|int |[sent_sample_rate](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-sent_sample_rate) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats-jitter) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioStats-audio_loss_rate"></span>
### audio_loss_rate

```c#
float bytertc.LocalAudioStats.audio_loss_rate
```


Audio packet loss rate. The audio uplink packet loss rate in this reference period is % and the value range is [0,1].

<span id="LocalAudioStats-send_kbitrate"></span>
### send_kbitrate

```c#
int bytertc.LocalAudioStats.send_kbitrate
```


Send rate. The audio transmission rate in the reference period is kbps.

<span id="LocalAudioStats-record_sample_rate"></span>
### record_sample_rate

```c#
int bytertc.LocalAudioStats.record_sample_rate
```


Acquisition sampling rate. Audio sampling rate information collected in the reference period, in units of Hz.

<span id="LocalAudioStats-stats_interval"></span>
### stats_interval

```c#
int bytertc.LocalAudioStats.stats_interval
```


Statistical interval. The interval of this reference period is in ms. This field is used to set the reference period for the callback. The default setting is 2s.

<span id="LocalAudioStats-rtt"></span>
### rtt

```c#
int bytertc.LocalAudioStats.rtt
```


Round\-trip time. The unit is ms.

<span id="LocalAudioStats-num_channels"></span>
### num_channels

```c#
int bytertc.LocalAudioStats.num_channels
```


Number of audio channels.

<span id="LocalAudioStats-sent_sample_rate"></span>
### sent_sample_rate

```c#
int bytertc.LocalAudioStats.sent_sample_rate
```


Audio transmission sampling rate. Audio transmission sampling rate information in the reference period, in Hz.

<span id="LocalAudioStats-jitter"></span>
### jitter

```c#
int bytertc.LocalAudioStats.jitter
```


Audio uplink network jitter in ms.

<span id="RemoteVideoConfig"></span>
# RemoteVideoConfig

```c#
struct bytertc::RemoteVideoConfig
```


Information on remote video frame

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[framerate](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoConfig-framerate) |
|int |[resolutionWidth](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoConfig-resolutionwidth) |
|int |[resolutionHeight](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoConfig-resolutionheight) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoConfig-framerate"></span>
### framerate

```c#
int bytertc.RemoteVideoConfig.framerate
```


Expected maximum frame rate of the subscribed stream in px. The default value is 0, values greater than 10 are valid. If the frame rate of the stream published is lower than the value you set, or if your subscribed stream falls back under limited network conditions, the frame rate you set will drop accordingly. Only valid if the stream is coded with SVC technique.

<span id="RemoteVideoConfig-resolutionwidth"></span>
### resolutionWidth

```c#
int bytertc.RemoteVideoConfig.resolutionWidth
```


Width of the video frame in px

<span id="RemoteVideoConfig-resolutionheight"></span>
### resolutionHeight

```c#
int bytertc.RemoteVideoConfig.resolutionHeight
```


Height of the video frame in px

<span id="AudioRecordingConfig"></span>
# AudioRecordingConfig

```c#
struct bytertc::AudioRecordingConfig
```


Audio recording config

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[absolute_file_name](https://docs.byteplus.com/en/docs/12/35817#AudioRecordingConfig-absolute_file_name) |
|AudioFrameSource |[frame_source](https://docs.byteplus.com/en/docs/12/35817#AudioRecordingConfig-frame_source) |
|AudioSampleRate |[sample_rate](https://docs.byteplus.com/en/docs/12/35817#AudioRecordingConfig-sample_rate) |
|AudioChannel |[channel](https://docs.byteplus.com/en/docs/12/35817#AudioRecordingConfig-channel) |
|AudioQuality |[quality](https://docs.byteplus.com/en/docs/12/35817#AudioRecordingConfig-quality) |


<span id="instructions"></span>
## Instructions

<span id="AudioRecordingConfig-absolute_file_name"></span>
### absolute_file_name

```c#
string bytertc.AudioRecordingConfig.absolute_file_name
```


Absolute path of the recorded file, file name included. The App must have the write and read permission of the path.

**Notes**

The files format is restricted to .aac and .wav.

<span id="AudioRecordingConfig-frame_source"></span>
### frame_source

```c#
AudioFrameSource bytertc.AudioRecordingConfig.frame_source
```


The source of the recording. See [AudioFrameSource](https://docs.byteplus.com/en/docs/12/35817#AudioFrameSource).

<span id="AudioRecordingConfig-sample_rate"></span>
### sample_rate

```c#
AudioSampleRate bytertc.AudioRecordingConfig.sample_rate
```


See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/35817#AudioSampleRate).

<span id="AudioRecordingConfig-channel"></span>
### channel

```c#
AudioChannel bytertc.AudioRecordingConfig.channel
```


Number of audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/35817#AudioChannel).

**Notes**

If number of audio channels of recording is different than that of audio capture, the behavior is:


* If the number of capture is 1, and the number of recording is 2, the recorded audio is two\-channel data after copying mono\-channel data.

* If the number of capture is 2, and the number of recording is 1, the recorded audio is recorded by mixing the audio of the two channels.


<span id="AudioRecordingConfig-quality"></span>
### quality

```c#
AudioQuality bytertc.AudioRecordingConfig.quality
```


Recording quality. Only valid for .aac file. See [AudioQuality](https://docs.byteplus.com/en/docs/12/35817#AudioQuality).

**Notes**

When the sample rate is 32kHz, the file (10min) size for different qualities are:


* low: 1.2MB;

* medium: 2MB;

* high: 3.75MB;

* ultra high: 7.5MB.


<span id="ScreenVideoEncoderConfig"></span>
# ScreenVideoEncoderConfig

```c#
struct bytertc::ScreenVideoEncoderConfig
```


The encoding configuration for shared\-screen streams. Refer to [Screen sharing](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70144) for recommended settings.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[Width](https://docs.byteplus.com/en/docs/12/35817#ScreenVideoEncoderConfig-width) |
|int |[Height](https://docs.byteplus.com/en/docs/12/35817#ScreenVideoEncoderConfig-height) |
|int |[FrameRate](https://docs.byteplus.com/en/docs/12/35817#ScreenVideoEncoderConfig-framerate) |
|int |[MaxBitrate](https://docs.byteplus.com/en/docs/12/35817#ScreenVideoEncoderConfig-maxbitrate) |
|int |[MinBitrate](https://docs.byteplus.com/en/docs/12/35817#ScreenVideoEncoderConfig-minbitrate) |
|ScreenVideoEncodePreference |[EncoderPreference](https://docs.byteplus.com/en/docs/12/35817#ScreenVideoEncoderConfig-encoderpreference) |


<span id="instructions"></span>
## Instructions

<span id="ScreenVideoEncoderConfig-width"></span>
### Width

```c#
int bytertc.ScreenVideoEncoderConfig.Width
```


The maximum width of the captured screen, measured in pixel.

<span id="ScreenVideoEncoderConfig-height"></span>
### Height

```c#
int bytertc.ScreenVideoEncoderConfig.Height
```


The maximum height of the captured screen, measured in pixel.

<span id="ScreenVideoEncoderConfig-framerate"></span>
### FrameRate

```c#
int bytertc.ScreenVideoEncoderConfig.FrameRate
```


The frame rate of the screen capture, measured in fps. We recommend set this value to the same as the capture frame rate.

<span id="ScreenVideoEncoderConfig-maxbitrate"></span>
### MaxBitrate

```c#
int bytertc.ScreenVideoEncoderConfig.MaxBitrate
```


The maximum bitrate(in kbps). Optional for internal capture while mandatory for custom capture. The default value is –1. If you set this value to \-1, RTC will automatically recommend the bitrate based on the input resolution and frame rate. If you set this value to 0, streams will not be encoded and published. On Version 3.44 or later, the default value for internal capture is \-1. On versions earlier than 3.44, you must set the maximum bit rate because there is no default value.

<span id="ScreenVideoEncoderConfig-minbitrate"></span>
### MinBitrate

```c#
int bytertc.ScreenVideoEncoderConfig.MinBitrate
```


The minimum bitrate(in kbps).Optional for internal capture while mandatory for custom capture. The minimum bitrate must be set lower than the maximum bitrate. Otherwise, streams will not be encoded and published.

<span id="ScreenVideoEncoderConfig-encoderpreference"></span>
### EncoderPreference

```c#
ScreenVideoEncodePreference bytertc.ScreenVideoEncoderConfig.EncoderPreference
```


The encoding modes for shared\-screen streams.See [ScreenVideoEncoderPreference](https://docs.byteplus.com/en/docs/12/35817#ScreenVideoEncodePreference).

<span id="RemoteVideoStateChangeReason"></span>
# RemoteVideoStateChangeReason

```c#
enum class bytertc.RemoteVideoStateChangeReason
```


Cause of remote video stream state change

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteVideoStateChangeReasonInternal |0 |Internal reasons |
|kRemoteVideoStateChangeReasonNetworkCongestion |1 |Network blocking |
|kRemoteVideoStateChangeReasonNetworkRecovery |2 |Network back to normal |
|kRemoteVideoStateChangeReasonLocalMuted |3 |Local user stops receiving remote video stream or local user disables video module |
|kRemoteVideoStateChangeReasonLocalUnmuted |4 |Local user resumes receiving remote video streams or local user enables video modules |
|kRemoteVideoStateChangeReasonRemoteMuted |5 |The remote user stops sending the video stream or the remote user disables the video module |
|kRemoteVideoStateChangeReasonRemoteUnmuted |6 |Remote user resumes sending video stream or remote user enables video module |
|kRemoteVideoStateChangeReasonRemoteOffline |7 |The remote user leaves the channel. State transition see `OnUserUnPublishStream`. |


<span id="ScreenCaptureSourceInfo"></span>
# ScreenCaptureSourceInfo

```c#
struct bytertc::ScreenCaptureSourceInfo
```


Screen capture object specific information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ScreenCaptureSourceType |[type](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-type) |
|IntPtr |[SourceID](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-sourceid) |
|string |[SourceName](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-sourcename) |
|int |[length](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-length) |
|string |[application](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-application) |
|int |[AppLength](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-applength) |
|int |[pid](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-pid) |
|bool |[PrimaryMonitor](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-primarymonitor) |
|Rectangle |[RegionRect](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceInfo-regionrect) |


<span id="instructions"></span>
## Instructions

<span id="ScreenCaptureSourceInfo-type"></span>
### type

```c#
ScreenCaptureSourceType bytertc.ScreenCaptureSourceInfo.type
```


When sharing a screen. See [ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/35817#ScreenCaptureSourceType) for the type of shared object

<span id="ScreenCaptureSourceInfo-sourceid"></span>
### SourceID

```c#
IntPtr bytertc.ScreenCaptureSourceInfo.SourceID
```


ID of the screen\-shared object

<span id="ScreenCaptureSourceInfo-sourcename"></span>
### SourceName

```c#
string bytertc.ScreenCaptureSourceInfo.SourceName
```


Name of the screen\-shared object Save it as a `string` object before calling [Release](https://docs.byteplus.com/en/docs/12/docs-191859#IScreenCaptureSourceList-release) to release the dynamic memory.

<span id="ScreenCaptureSourceInfo-length"></span>
### length

```c#
int bytertc.ScreenCaptureSourceInfo.length
```


The length of `SourceName`.

<span id="ScreenCaptureSourceInfo-application"></span>
### application

```c#
string bytertc.ScreenCaptureSourceInfo.application
```


The title of the application to be shared. Only available if the sharing object is an application windows. Save it as a `string` object before calling [Release](https://docs.byteplus.com/en/docs/12/docs-191859#IScreenCaptureSourceList-release) to release the dynamic memory.

<span id="ScreenCaptureSourceInfo-applength"></span>
### AppLength

```c#
int bytertc.ScreenCaptureSourceInfo.AppLength
```


The length of `application`.

<span id="ScreenCaptureSourceInfo-pid"></span>
### pid

```c#
int bytertc.ScreenCaptureSourceInfo.pid
```


Process pid of the application to be shared. Only available if the sharing object is an application windows.

<span id="ScreenCaptureSourceInfo-primarymonitor"></span>
### PrimaryMonitor

```c#
bool bytertc.ScreenCaptureSourceInfo.PrimaryMonitor
```


Tag for the screen to be shared identifying whether it is the primary screen. Only available when the screen\-sharing object is a screen.

<span id="ScreenCaptureSourceInfo-regionrect"></span>
### RegionRect

```c#
Rectangle bytertc.ScreenCaptureSourceInfo.RegionRect
```


Coordinates of the screen\-sharing object. See [Rectangle](https://docs.byteplus.com/en/docs/12/35817#Rectangle).


* When there are several screens, the origin (0, 0) is different for different platforms:

   * For Windows, the origin (0, 0) is the top\-left corner of the main screen.

   * For Linux, the origin (0, 0) is the top\-left corner of the rectangle that merely covers all screens.

* The region of the window is different for different platforms:

   * For Windows and macOS, the region includes the system title bar of the window.

   * For Linux, the region does not includes the system title bar of the window.


<span id="AudioSampleRate"></span>
# AudioSampleRate

```c#
enum class bytertc.AudioSampleRate
```


Audio sample rate in Hz.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioSampleRateAuto |\-1 |Default value. |
|kAudioSampleRate8000 |8000 |8000 |
|kAudioSampleRate16000 |16000 |16000 |
|kAudioSampleRate32000 |32000 |32000 |
|kAudioSampleRate44100 |44100 |44100 |
|kAudioSampleRate48000 |48000 |48000 |


<span id="MediaStreamType"></span>
# MediaStreamType

```c#
enum class bytertc.MediaStreamType
```


Media stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaStreamTypeAudio |0 |Controls audio only |
|kMediaStreamTypeVideo |1 |Controls video only |
|kMediaStreamTypeBoth |2 |Controls both audio and video |


<span id="AudioFrameType"></span>
# AudioFrameType

```c#
enum class bytertc.AudioFrameType
```


Audio frame type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kFrameTypePCM16 |0 |PCM 16bit |


<span id="ForwardStreamEvent"></span>
# ForwardStreamEvent

```c#
enum class bytertc.ForwardStreamEvent
```


Forwarding events

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kForwardStreamEventDisconnected |0 |The network connection between the local endpoint and the server is disconnected, and the forwarding is paused. |
|kForwardStreamEventConnected |1 |The network connection between the local endpoint and the server is restored, and the forwarding service connection is successful. |
|kForwardStreamEventInterrupt |2 |Forwarding interruption. When the same user_id user enters the target room during the forwarding process, the forwarding is interrupted. |
|kForwardStreamEventDstRoomUpdated |3 |The target room has been updated. Triggered by `updateForwardStreamToRooms`. |
|kForwardStreamEventUnExpectAPICall |4 |API call sequence error. For example, call `updateForwardStreamToRooms` before calling `startForwardStreamToRooms`. |


<span id="VideoFrameType"></span>
# VideoFrameType

```c#
enum class bytertc.VideoFrameType
```


Video frame format

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoFrameTypeRawMemory |0 |Original format, stored as memory |
|kVideoFrameTypeCVPixelBuffer |1 |CVPixelBufferRef which applys to iOS and macOS |
|kVideoFrameTypeGLTexture |2 |Open gl texture |
|kVideoFrameTypeCuda |3 |Cuda |
|kVideoFrameTypeD3D11 |4 |Direct3d 11 |
|kVideoFrameTypeD3D9 |5 |Direct3d 9 |
|kVideoFrameTypeJavaFrame |6 |VideoFrame used in Java |
|kVideoFrameTypeVAAPI |7 |Vaapi |


<span id="SEIStreamEventType"></span>
# SEIStreamEventType

```c#
enum class bytertc.SEIStreamEventType
```


State of the black frame video stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSEIStreamEventTypeStreamAdd |0 |A black frame video stream is published from the remote user. In a voice call, when the remote user calls [SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendseimessage) to send SEI data, SDK will automatically publish a black frame video stream, and trigger this callback. |
|kSEIStreamEventTypeStreamRemove |1 |The black frame video stream is removed. The timing this callback will be triggered is as following:<br><br><br>* The remote user turns on their camera, switching from a voice call to a video call.<br><br>* No SEI data is sent within 1min after the remote user calls [SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendseimessage).<br><br>* The black frame video stream stops when the remote user calls [SetVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideosourcetype) to switch to custom video capture. |


<span id="RTCVideoDeviceType"></span>
# RTCVideoDeviceType

```c#
enum class bytertc.RTCVideoDeviceType
```


Video device type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRTCVideoDeviceTypeUnknown |\-1 |Unknown device type |
|kRTCVideoDeviceTypeRenderDevice |0 |Audio Rendering Device Type |
|kRTCVideoDeviceTypeCaptureDevice |1 |Audio Acquisition Device Type |
|kRTCVideoDeviceTypeScreenCaptureDevice |2 |Screen Streaming Audio Devices |


<span id="NetworkQualityStats"></span>
# NetworkQualityStats

```c#
struct bytertc::NetworkQualityStats
```


Tx/Rx network quality

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[uid](https://docs.byteplus.com/en/docs/12/35817#NetworkQualityStats-uid) |
|double |[fraction_lost](https://docs.byteplus.com/en/docs/12/35817#NetworkQualityStats-fraction_lost) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/35817#NetworkQualityStats-rtt) |
|int |[total_bandwidth](https://docs.byteplus.com/en/docs/12/35817#NetworkQualityStats-total_bandwidth) |
|NetworkQuality |[tx_quality](https://docs.byteplus.com/en/docs/12/35817#NetworkQualityStats-tx_quality) |
|NetworkQuality |[rx_quality](https://docs.byteplus.com/en/docs/12/35817#NetworkQualityStats-rx_quality) |


<span id="instructions"></span>
## Instructions

<span id="NetworkQualityStats-uid"></span>
### uid

```c#
string bytertc.NetworkQualityStats.uid
```


User ID

<span id="NetworkQualityStats-fraction_lost"></span>
### fraction_lost

```c#
double bytertc.NetworkQualityStats.fraction_lost
```


Packet loss ratio of the local client, ranging [0.0,1.0] For a local user, it is the sent\-packet loss ratio. For a remote user, it is the loss ratio of all the packets received.

<span id="NetworkQualityStats-rtt"></span>
### rtt

```c#
int bytertc.NetworkQualityStats.rtt
```


Round\-trip time (RTT) from client to server. Effective for the local user. Unit: ms

<span id="NetworkQualityStats-total_bandwidth"></span>
### total_bandwidth

```c#
int bytertc.NetworkQualityStats.total_bandwidth
```


Average transmission rate of the media RTP packages in 2s. unit: bps For a local user, it is the packet\-transmitting speed. For a more user, it is the speed of receiving all the subsribed media.

<span id="NetworkQualityStats-tx_quality"></span>
### tx_quality

```c#
NetworkQuality bytertc.NetworkQualityStats.tx_quality
```


Tx network quality grade. Refer to [NetworkQuality](https://docs.byteplus.com/en/docs/12/35817#NetworkQuality) for details.

<span id="NetworkQualityStats-rx_quality"></span>
### rx_quality

```c#
NetworkQuality bytertc.NetworkQualityStats.rx_quality
```


Rx network quality grade. Refer to [NetworkQuality](https://docs.byteplus.com/en/docs/12/35817#NetworkQuality) for details.

<span id="AudioRecordingState"></span>
# AudioRecordingState

```c#
enum class bytertc.AudioRecordingState
```


Audio recording config

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioRecordingStateError |0 |Recording exception |
|kAudioRecordingStateProcessing |1 |Recording in progress |
|kAudioRecordingStateSuccess |2 |The recording task ends, and the file is saved. |


<span id="StreamIndex"></span>
# StreamIndex

```c#
enum class bytertc.StreamIndex
```


Stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kStreamIndexMain |0 |Mainstream, including:<br><br><br>* Video/audio captured by the the camera/microphone using internal capturing;<br><br>* Video/audio captured by custom method. |
|kStreamIndexScreen |1 |Screen\-sharing stream. Video/Audio streams for screen sharing. |


<span id="MediaDeviceWarning"></span>
# MediaDeviceWarning

```c#
enum class bytertc.MediaDeviceWarning
```


Media device warning

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaDeviceWarningOK |0 |No warning |
|kMediaDeviceWarningOperationDenied |1 |Illegal device operation. Calls the API for internal device when using the external device. |
|kMediaDeviceWarningCaptureSilence |2 |No audio is captured. |
|kMediaDeviceWarningAndroidSysSilence |3 |Silence warning by Android system. |
|kMediaDeviceWarningAndroidSysSilenceDisappear |4 |Silence disappearing warning by Android system. |


<span id="VideoCodecType"></span>
# VideoCodecType

```c#
enum class bytertc.VideoCodecType
```


Video encoding type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoCodecTypeUnknown |0 |Unknown type |
|kVideoCodecTypeH264 |1 |H.264 format |
|kVideoCodecTypeByteVC1 |2 |ByteVC1 format |


<span id="RTCWatermarkConfig"></span>
# RTCWatermarkConfig

```c#
struct bytertc::RTCWatermarkConfig
```


Watermark configurations

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[visible_in_preview](https://docs.byteplus.com/en/docs/12/35817#RTCWatermarkConfig-visible_in_preview) |
|ByteWatermark |[position_in_landscape_mode](https://docs.byteplus.com/en/docs/12/35817#RTCWatermarkConfig-position_in_landscape_mode) |
|ByteWatermark |[position_in_portrait_mode](https://docs.byteplus.com/en/docs/12/35817#RTCWatermarkConfig-position_in_portrait_mode) |


<span id="instructions"></span>
## Instructions

<span id="RTCWatermarkConfig-visible_in_preview"></span>
### visible_in_preview

```c#
bool bytertc.RTCWatermarkConfig.visible_in_preview
```


Whether the watermark is visible in preview. Its default value is `true`.

<span id="RTCWatermarkConfig-position_in_landscape_mode"></span>
### position_in_landscape_mode

```c#
ByteWatermark bytertc.RTCWatermarkConfig.position_in_landscape_mode
```


Watermark's coordinates and size in landscape mode. See [ByteWatermark](https://docs.byteplus.com/en/docs/12/35817#ByteWatermark).

<span id="RTCWatermarkConfig-position_in_portrait_mode"></span>
### position_in_portrait_mode

```c#
ByteWatermark bytertc.RTCWatermarkConfig.position_in_portrait_mode
```


Watermark's coordinates and size in portrait mode. See [ByteWatermark](https://docs.byteplus.com/en/docs/12/35817#ByteWatermark).

<span id="EffectBeautyMode"></span>
# EffectBeautyMode

```c#
enum class bytertc.EffectBeautyMode
```


Basic beauty effect.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kEffectBeautyModeWhite |0 |Brightening. |
|kEffectBeautyModeSmooth |1 |Smoothing. |
|kEffectBeautyModeSharpen |2 |Sharpening. |
|kEffectBeautyModeClear |3 |Clarity. Integrating Effects SDK v4.4.2+ is required for this sub\-item. |


<span id="HumanOrientation"></span>
# HumanOrientation

```c#
struct bytertc::HumanOrientation
```


Three\-dimensional orientation information, each pair of vectors need to be perpendicular. See [Orientation](https://docs.byteplus.com/en/docs/12/35817#Orientation).

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|Orientation |[forward](https://docs.byteplus.com/en/docs/12/35817#HumanOrientation-forward) |
|Orientation |[right](https://docs.byteplus.com/en/docs/12/35817#HumanOrientation-right) |
|Orientation |[up](https://docs.byteplus.com/en/docs/12/35817#HumanOrientation-up) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|HumanOrientation |[HumanOrientation](https://docs.byteplus.com/en/docs/12/35817#HumanOrientation-humanorientation) |


<span id="instructions"></span>
## Instructions

<span id="HumanOrientation-forward"></span>
### forward

```c#
Orientation bytertc.HumanOrientation.forward
```


Forward orientation, the default value is {1,0,0}, i.e., the forward orientation is in the positive direction of x\-axis.

<span id="HumanOrientation-right"></span>
### right

```c#
Orientation bytertc.HumanOrientation.right
```


Rightward orientation, the default value is {0,1,0}, i.e., the rightward orientation is in the positive direction of y\-axis.

<span id="HumanOrientation-up"></span>
### up

```c#
Orientation bytertc.HumanOrientation.up
```


Upward orientation, the default value is {0,0,1}, i.e., the upward orientation is in the positive direction of z\-axis.

<span id="instructions"></span>
## Instructions

<span id="HumanOrientation-humanorientation"></span>
### HumanOrientation

```c#
bytertc.HumanOrientation.HumanOrientation(
    Orientation forward,
    Orientation right,
    Orientation up
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|forward |Orientation |\- |
|right |Orientation |\- |
|up |Orientation |\- |


<span id="AudioFrameCallback"></span>
# AudioFrameCallback

```c#
struct bytertc::AudioFrameCallback
```


Audio data

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|long |[TimestampUs](https://docs.byteplus.com/en/docs/12/35817#AudioFrameCallback-timestampus) |
|AudioSampleRate |[SampleRate](https://docs.byteplus.com/en/docs/12/35817#AudioFrameCallback-samplerate) |
|AudioChannel |[Channel](https://docs.byteplus.com/en/docs/12/35817#AudioFrameCallback-channel) |
|IntPtr |[Data](https://docs.byteplus.com/en/docs/12/35817#AudioFrameCallback-data) |
|int |[DataSize](https://docs.byteplus.com/en/docs/12/35817#AudioFrameCallback-datasize) |
|AudioFrameType |[FrameType](https://docs.byteplus.com/en/docs/12/35817#AudioFrameCallback-frametype) |
|bool |[IsMutedData](https://docs.byteplus.com/en/docs/12/35817#AudioFrameCallback-ismuteddata) |


<span id="instructions"></span>
## Instructions

<span id="AudioFrameCallback-timestampus"></span>
### TimestampUs

```c#
long bytertc.AudioFrameCallback.TimestampUs
```


Audio frame timestamp in microseconds.

<span id="AudioFrameCallback-samplerate"></span>
### SampleRate

```c#
AudioSampleRate bytertc.AudioFrameCallback.SampleRate
```


Audio sample rate. See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/35817#AudioSampleRate)

<span id="AudioFrameCallback-channel"></span>
### Channel

```c#
AudioChannel bytertc.AudioFrameCallback.Channel
```


The number of audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/35817#AudioChannel)

<span id="AudioFrameCallback-data"></span>
### Data

```c#
IntPtr bytertc.AudioFrameCallback.Data
```


Audio frame memory address

<span id="AudioFrameCallback-datasize"></span>
### DataSize

```c#
int bytertc.AudioFrameCallback.DataSize
```


Audio frame data size in bytes.

<span id="AudioFrameCallback-frametype"></span>
### FrameType

```c#
AudioFrameType bytertc.AudioFrameCallback.FrameType
```


Audio frame type, support PCM only. See [AudioFrameType](https://docs.byteplus.com/en/docs/12/35817#AudioFrameType).

<span id="AudioFrameCallback-ismuteddata"></span>
### IsMutedData

```c#
bool bytertc.AudioFrameCallback.IsMutedData
```


Gets audio mute state identifier

<span id="Position"></span>
# Position

```c#
struct bytertc::Position
```


The location of the user in the range speech, the coordinate system needs to be established by itself.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/35817#Position-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/35817#Position-y) |
|float |[z](https://docs.byteplus.com/en/docs/12/35817#Position-z) |


<span id="instructions"></span>
## Instructions

<span id="Position-x"></span>
### x

```c#
float bytertc.Position.x
```


X coordinate

<span id="Position-y"></span>
### y

```c#
float bytertc.Position.y
```


Y coordinate

<span id="Position-z"></span>
### z

```c#
float bytertc.Position.z
```


Z coordinate

<span id="VideoEncodePreference"></span>
# VideoEncodePreference

```c#
enum class bytertc.VideoEncodePreference
```


Encoder preference.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoEncodePreferenceDisabled |0 |No preference. The frame rate and the resolution will not be adjusted. |
|kVideoEncodePreferenceFramerate |1 |(Default) Frame rate first. |
|kVideoEncodePreferenceQuality |2 |Resolution first. |
|kVideoEncodePreferenceBalance |3 |Balancing resolution and frame rate. |


<span id="ScreenVideoEncodePreference"></span>
# ScreenVideoEncodePreference

```c#
enum class bytertc.ScreenVideoEncodePreference
```


The encoding modes for shared\-screen streams. The default mode is the high\-resolution mode. If you exclude specific windows by setting [ScreenFilterConfig](https://docs.byteplus.com/en/docs/12/35817#ScreenFilterConfig), the frame rate of the shared\-screen stream will be slower than 30fps。

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kScreenVideoEncodePreferenceAuto |0 |The automatic mode. The encoding mode is dynamically determined by RTC based on the content. |
|kScreenVideoEncodePreferenceFramerate |1 |The high frame rate mode. Ensure the highest framerate possible under challenging network conditions. This mode is designed to share audiovisual content, including games and videos. |
|kScreenVideoEncodePreferenceQuality |2 |The high\-resolution mode. Ensure the highest resolution possible under challenging network conditions. This mode is designed to share micro\-detailed content, including slides, documents, images, illustrations, or graphics. |


<span id="ForwardStreamConfiguration"></span>
# ForwardStreamConfiguration

```c#
struct bytertc::ForwardStreamConfiguration
```


Information of the rooms where you want to relay the media stream to

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|IntPtr |[forward_stream_dests](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamConfiguration-forward_stream_dests) |
|int |[dest_count](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamConfiguration-dest_count) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamConfiguration-forward_stream_dests"></span>
### forward_stream_dests

```c#
IntPtr bytertc.ForwardStreamConfiguration.forward_stream_dests
```


<span id="ForwardStreamConfiguration-dest_count"></span>
### dest_count

```c#
int bytertc.ForwardStreamConfiguration.dest_count
```


<span id="StreamRemoveReason"></span>
# StreamRemoveReason

```c#
enum class bytertc.StreamRemoveReason
```


The reason why the remote flow in the room was removed.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kStreamRemoveReasonUnpublish |0 |The remote user stops publishing the flow. |
|kStreamRemoveReasonPublishFailed |1 |The remote user failed to publish the flow. |
|kStreamRemoveReasonKeepLiveFailed |2 |Keep alive failed. |
|kStreamRemoveReasonClientDisconnected |3 |The remote user is disconnected. |
|kStreamRemoveReasonRepublish |4 |The remote user republishes the flow. |
|kStreamRemoveReasonOther |5 |Other reasons. |


<span id="RemoteAudioStats"></span>
# RemoteAudioStats

```c#
struct bytertc::RemoteAudioStats
```


Remote audio stream statistics, reference period 2s. After a local user subscribes to a remote audio stream successfully, the SDK periodically notifies the local user of the reception status of the subscribed audio stream during this reference period through `OnRemoteStreamStatsEventHandler`. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[audio_loss_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-audio_loss_rate) |
|int |[received_kbitrate](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-received_kbitrate) |
|int |[stall_count](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-stall_count) |
|int |[stall_duration](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-stall_duration) |
|long |[e2e_delay](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-e2e_delay) |
|int |[playout_sample_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-playout_sample_rate) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-stats_interval) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-rtt) |
|int |[total_rtt](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-total_rtt) |
|int |[quality](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-quality) |
|int |[jitter_buffer_delay](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-jitter_buffer_delay) |
|int |[num_channels](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-num_channels) |
|int |[received_sample_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-received_sample_rate) |
|int |[frozen_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-frozen_rate) |
|int |[concealed_samples](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-concealed_samples) |
|int |[concealment_event](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-concealment_event) |
|int |[dec_sample_rate](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-dec_sample_rate) |
|int |[dec_duration](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-dec_duration) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats-jitter) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioStats-audio_loss_rate"></span>
### audio_loss_rate

```c#
float bytertc.RemoteAudioStats.audio_loss_rate
```


Audio packet loss rate. The audio downlink packet loss rate in the reference period, the value range is [0,1].

<span id="RemoteAudioStats-received_kbitrate"></span>
### received_kbitrate

```c#
int bytertc.RemoteAudioStats.received_kbitrate
```


Receiving bit rate. The audio reception rate in the reference period in kbps.

<span id="RemoteAudioStats-stall_count"></span>
### stall_count

```c#
int bytertc.RemoteAudioStats.stall_count
```


Number of audio stalls.

<span id="RemoteAudioStats-stall_duration"></span>
### stall_duration

```c#
int bytertc.RemoteAudioStats.stall_duration
```


Audio stall duration. Stall duration in the reference period in ms.

<span id="RemoteAudioStats-e2e_delay"></span>
### e2e_delay

```c#
long bytertc.RemoteAudioStats.e2e_delay
```


End\-to\-end latency at the user experience level. The delay from the start of encoding at the sending end to the start of decoding at the receiving end, in units of ms.

<span id="RemoteAudioStats-playout_sample_rate"></span>
### playout_sample_rate

```c#
int bytertc.RemoteAudioStats.playout_sample_rate
```


Play sample rate. Audio playback sample rate information within the reference period in Hz.

<span id="RemoteAudioStats-stats_interval"></span>
### stats_interval

```c#
int bytertc.RemoteAudioStats.stats_interval
```


Statistical interval. The interval of this reference period is in ms.

<span id="RemoteAudioStats-rtt"></span>
### rtt

```c#
int bytertc.RemoteAudioStats.rtt
```


Round\-trip time for client side to server level data transfer in ms.

<span id="RemoteAudioStats-total_rtt"></span>
### total_rtt

```c#
int bytertc.RemoteAudioStats.total_rtt
```


The sender\-server level\-the receiver\-link data transmission round\-trip time. The unit is ms.

<span id="RemoteAudioStats-quality"></span>
### quality

```c#
int bytertc.RemoteAudioStats.quality
```


The quality of the audio stream sent by the remote user. Value meaning reference [NetworkQuality](https://docs.byteplus.com/en/docs/12/35817#NetworkQuality).

<span id="RemoteAudioStats-jitter_buffer_delay"></span>
### jitter_buffer_delay

```c#
int bytertc.RemoteAudioStats.jitter_buffer_delay
```


The delay caused by the introduction of the jitter buffer mechanism. The unit is ms.

<span id="RemoteAudioStats-num_channels"></span>
### num_channels

```c#
int bytertc.RemoteAudioStats.num_channels
```


Number of audio channels.

<span id="RemoteAudioStats-received_sample_rate"></span>
### received_sample_rate

```c#
int bytertc.RemoteAudioStats.received_sample_rate
```


Audio reception sampling rate. Remote audio sampling rate information received within the reference period, in Hz.

<span id="RemoteAudioStats-frozen_rate"></span>
### frozen_rate

```c#
int bytertc.RemoteAudioStats.frozen_rate
```


The accumulated length of the audio card occurs after the remote user joins the room as a percentage of the total effective length of the audio. The effective duration of audio refers to the duration of audio other than stopping sending audio streams and disabling audio modules after remote users enter the room to publish audio streams.

<span id="RemoteAudioStats-concealed_samples"></span>
### concealed_samples

```c#
int bytertc.RemoteAudioStats.concealed_samples
```


Audio packet loss compensation (PLC) total number of sample points.

<span id="RemoteAudioStats-concealment_event"></span>
### concealment_event

```c#
int bytertc.RemoteAudioStats.concealment_event
```


Audio packet loss compensation (PLC) cumulative times.

<span id="RemoteAudioStats-dec_sample_rate"></span>
### dec_sample_rate

```c#
int bytertc.RemoteAudioStats.dec_sample_rate
```


Audio decoding sample rate. Audio decoding sample rate information in the reference period in Hz.

<span id="RemoteAudioStats-dec_duration"></span>
### dec_duration

```c#
int bytertc.RemoteAudioStats.dec_duration
```


Cumulative decoding time in seconds of the remote audio stream in this subscription.

<span id="RemoteAudioStats-jitter"></span>
### jitter

```c#
int bytertc.RemoteAudioStats.jitter
```


Audio downlink network jitter in ms.

<span id="ForwardStreamInfo"></span>
# ForwardStreamInfo

```c#
struct bytertc::ForwardStreamInfo
```


Information of the rooms where you want to relay the media stream to

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[token](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamInfo-token) |
|string |[room_id](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamInfo-room_id) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamInfo-token"></span>
### token

```c#
string bytertc.ForwardStreamInfo.token
```


<span id="ForwardStreamInfo-room_id"></span>
### room_id

```c#
string bytertc.ForwardStreamInfo.room_id
```


<span id="ForwardStreamError"></span>
# ForwardStreamError

```c#
enum class bytertc.ForwardStreamError
```


Error codes thrown during the media stream cross\-room forwarding process.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kForwardStreamErrorOK |0 |Normal |
|kForwardStreamErrorInvalidArgument |1201 |Invalid parameter |
|kForwardStreamErrorInvalidToken |1202 |Invalid token |
|kForwardStreamErrorResponse |1203 |Server error |
|kForwardStreamErrorRemoteKicked |1204 |The user with the same user id joins the target room, and the forwarding is interrupted. |
|kForwardStreamErrorNotSupport |1205 |The server does not support forwarding function |


<span id="AudioQuality"></span>
# AudioQuality

```c#
enum class bytertc.AudioQuality
```


Audio quality.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioQualityLow |0 |low quality |
|kAudioQualityMedium |1 |medium quality |
|kAudioQualityHigh |2 |high quality |
|kAudioQualityUltraHigh |3 |ultra high quality |


<span id="RTCVideoEngineParams"></span>
# RTCVideoEngineParams

```c#
struct bytertc::RTCVideoEngineParams
```


Engine initialization parameters.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[AppID](https://docs.byteplus.com/en/docs/12/35817#RTCVideoEngineParams-appid) |
|Dictionary<string, object\> |[Params](https://docs.byteplus.com/en/docs/12/35817#RTCVideoEngineParams-params) |


<span id="instructions"></span>
## Instructions

<span id="RTCVideoEngineParams-appid"></span>
### AppID

```c#
string bytertc.RTCVideoEngineParams.AppID
```


App ID.

<span id="RTCVideoEngineParams-params"></span>
### Params

```c#
Dictionary<string, object> bytertc.RTCVideoEngineParams.Params
```


Initialization parameters.

<span id="AudioFormat"></span>
# AudioFormat

```c#
struct bytertc::AudioFormat
```


Audio parameters format

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|AudioSampleRate |[SampleRate](https://docs.byteplus.com/en/docs/12/35817#AudioFormat-samplerate) |
|AudioChannel |[Channel](https://docs.byteplus.com/en/docs/12/35817#AudioFormat-channel) |


<span id="instructions"></span>
## Instructions

<span id="AudioFormat-samplerate"></span>
### SampleRate

```c#
AudioSampleRate bytertc.AudioFormat.SampleRate
```


Audio sample rate. See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/35817#AudioSampleRate).

<span id="AudioFormat-channel"></span>
### Channel

```c#
AudioChannel bytertc.AudioFormat.Channel
```


Audio channel. See [AudioChannel](https://docs.byteplus.com/en/docs/12/35817#AudioChannel).

<span id="AudioFrame"></span>
# AudioFrame

```c#
struct bytertc::AudioFrame
```


Audio frame

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|long |[TimestampUs](https://docs.byteplus.com/en/docs/12/35817#AudioFrame-timestampus) |
|AudioSampleRate |[SampleRate](https://docs.byteplus.com/en/docs/12/35817#AudioFrame-samplerate) |
|AudioChannel |[Channel](https://docs.byteplus.com/en/docs/12/35817#AudioFrame-channel) |
|byte[] |[Data](https://docs.byteplus.com/en/docs/12/35817#AudioFrame-data) |
|int |[DataSize](https://docs.byteplus.com/en/docs/12/35817#AudioFrame-datasize) |
|AudioFrameType |[FrameType](https://docs.byteplus.com/en/docs/12/35817#AudioFrame-frametype) |
|bool |[IsMutedData](https://docs.byteplus.com/en/docs/12/35817#AudioFrame-ismuteddata) |


<span id="instructions"></span>
## Instructions

<span id="AudioFrame-timestampus"></span>
### TimestampUs

```c#
long bytertc.AudioFrame.TimestampUs
```


Audio frame timestamp in microseconds.

<span id="AudioFrame-samplerate"></span>
### SampleRate

```c#
AudioSampleRate bytertc.AudioFrame.SampleRate
```


Audio sample rate. See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/35817#AudioSampleRate)

<span id="AudioFrame-channel"></span>
### Channel

```c#
AudioChannel bytertc.AudioFrame.Channel
```


The number of audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/35817#AudioChannel)

<span id="AudioFrame-data"></span>
### Data

```c#
byte [] bytertc.AudioFrame.Data
```


Audio frame memory address

<span id="AudioFrame-datasize"></span>
### DataSize

```c#
int bytertc.AudioFrame.DataSize
```


Audio frame data size in bytes.

<span id="AudioFrame-frametype"></span>
### FrameType

```c#
AudioFrameType bytertc.AudioFrame.FrameType
```


Audio frame type, support PCM only. See [AudioFrameType](https://docs.byteplus.com/en/docs/12/35817#AudioFrameType).

<span id="AudioFrame-ismuteddata"></span>
### IsMutedData

```c#
bool bytertc.AudioFrame.IsMutedData
```


Gets audio mute state identifier

<span id="ScreenMediaType"></span>
# ScreenMediaType

```c#
enum class bytertc.ScreenMediaType
```


Screen media type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kScreenMediaTypeVideoOnly |0 |Capture video only |
|kScreenMediaTypeAudioOnly |1 |Capture audio only |
|kScreenMediaTypeVideoAndAudio |2 |Capture Audio and video simultaneously. |


<span id="RtcUser"></span>
# RtcUser

```c#
struct bytertc::RtcUser
```


User information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[UserID](https://docs.byteplus.com/en/docs/12/35817#RtcUser-userid) |
|string |[MetaData](https://docs.byteplus.com/en/docs/12/35817#RtcUser-metadata) |


<span id="instructions"></span>
## Instructions

<span id="RtcUser-userid"></span>
### UserID

```c#
string bytertc.RtcUser.UserID
```


User ID.

<span id="RtcUser-metadata"></span>
### MetaData

```c#
string bytertc.RtcUser.MetaData
```


Metadata

<span id="LocalAudioPropertiesInfo"></span>
# LocalAudioPropertiesInfo

```c#
struct bytertc::LocalAudioPropertiesInfo
```


Local audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|StreamIndex |[StreamIndex](https://docs.byteplus.com/en/docs/12/35817#LocalAudioPropertiesInfo-streamindex) |
|AudioPropertiesInfo |[AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/35817#LocalAudioPropertiesInfo-audiopropertiesinfo) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioPropertiesInfo-streamindex"></span>
### StreamIndex

```c#
StreamIndex bytertc.LocalAudioPropertiesInfo.StreamIndex
```


See [StreamIndex](https://docs.byteplus.com/en/docs/12/35817#LocalAudioPropertiesInfo-streamindex).

<span id="LocalAudioPropertiesInfo-audiopropertiesinfo"></span>
### AudioPropertiesInfo

```c#
AudioPropertiesInfo bytertc.LocalAudioPropertiesInfo.AudioPropertiesInfo
```


See [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/35817#LocalAudioPropertiesInfo-audiopropertiesinfo).

<span id="ColorSpace"></span>
# ColorSpace

```c#
enum class bytertc.ColorSpace
```


Video YUV format color space

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kColorSpaceUnknown |0 |\- |
|kColorSpaceYCbCrBT601LimitedRange |1 |BT.601 Digital Coding Standard, Color Space [16\-235] |
|kColorSpaceYCbCrBT601FullRange |2 |BT.601 Digital Coding Standard, Color Space [0\-255] |
|kColorSpaceYCbCrBT709LimitedRange |3 |BT.7091 Digital Coding Standard, Color Space [16\-235] |
|kColorSpaceYCbCrBT709FullRange |4 |BT.7091 Digital Coding Standard, Color Space [0\-255] |


<span id="ScreenCaptureSourceType"></span>
# ScreenCaptureSourceType

```c#
enum class bytertc.ScreenCaptureSourceType
```


Type of the screen capture object

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kScreenCaptureSourceTypeUnknown |0 |Type unknown |
|kScreenCaptureSourceTypeWindow |1 |Application window |
|kScreenCaptureSourceTypeScreen |2 |Desktop |


<span id="AudioProfileType"></span>
# AudioProfileType

```c#
enum class bytertc.AudioProfileType
```


Sound quality gear

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioProfileTypeDefault |0 |Default sound quality The sound quality configuration of [RoomProfileType](https://docs.byteplus.com/en/docs/12/35817#RoomProfileType) set by the server or client side |
|kAudioProfileTypeFluent |1 |Smooth sound quality. Mono, sampling rate of 16kHz, coding rate of 24 Kbps. Fluent priority, low latency, low power consumption, low traffic consumption, suitable for most game scenarios, such as MMORPG, MOBA, FPS and other game team voice, team voice, national war voice, etc. |
|kAudioProfileTypeStandard |2 |Standard sound quality. Mono, the sampling rate is 48kHz, the coding rate is 48 Kbps. Suitable for scenes with certain requirements for sound quality, while the delay, power consumption and traffic consumption are relatively moderate, suitable for educational scenes and Werewolf games such as Sirius. |
|kAudioProfileTypeHD |3 |High\-definition sound quality Dual channel, sampling rate is 48kHz, coding rate is 128 Kbps. Ultra\-high sound quality, while the delay, power consumption and flow consumption are relatively large, suitable for music scenes such as Lianmai PK. Game scenes are not recommended. |
|kAudioProfileTypeStandardStereo |4 |Dual\-channel standard. Sample rate: 48 KHz. Encoding bitrate: 80 Kbps. |
|kAudioProfileTypeHDMono |5 |Mono\-channel music. Sample rate: 48 KHz. Encoding bitrate: 64 Kbps. |


<span id="UserInfo"></span>
# UserInfo

```c#
struct bytertc::UserInfo
```


User information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[UserID](https://docs.byteplus.com/en/docs/12/35817#UserInfo-userid) |
|string |[ExtraInfo](https://docs.byteplus.com/en/docs/12/35817#UserInfo-extrainfo) |


<span id="instructions"></span>
## Instructions

<span id="UserInfo-userid"></span>
### UserID

```c#
string bytertc.UserInfo.UserID
```


User ID. The string matches the regular expression: `[a-zA-Z0-9_@\-]{1,128}`.

<span id="UserInfo-extrainfo"></span>
### ExtraInfo

```c#
string bytertc.UserInfo.ExtraInfo
```


Additional information of the user. The maximum length is 200 bytes. The remote user will receive the info in `OnUserJoined`.

<span id="RemoteAudioPropertiesInfo"></span>
# RemoteAudioPropertiesInfo

```c#
struct bytertc::RemoteAudioPropertiesInfo
```


Remote audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|RemoteStreamKey |[StreamKey](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioPropertiesInfo-streamkey) |
|AudioPropertiesInfo |[AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioPropertiesInfo-audiopropertiesinfo) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioPropertiesInfo-streamkey"></span>
### StreamKey

```c#
RemoteStreamKey bytertc.RemoteAudioPropertiesInfo.StreamKey
```


Remote stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamKey).

<span id="RemoteAudioPropertiesInfo-audiopropertiesinfo"></span>
### AudioPropertiesInfo

```c#
AudioPropertiesInfo bytertc.RemoteAudioPropertiesInfo.AudioPropertiesInfo
```


Information of audio properties. See [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioPropertiesInfo-audiopropertiesinfo).

<span id="VideoStreamScaleMode"></span>
# VideoStreamScaleMode

```c#
enum class bytertc.VideoStreamScaleMode
```


Video frame scale mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoStreamScaleModeAuto |0 |Auto mode, default to FitWithCropping. |
|kVideoStreamScaleModeStretch |1 |Stretch the video frame until the video frame and the window have the same resolution. The video frame's aspect ratio can be changed as it is automatically stretched to fill the window, but the whole image is visible. |
|kVideoStreamScaleModeFitWithCropping |2 |Fit the window with cropping Scale the video frame uniformly until the window is filled. If the video frame's aspect ratio is different from that of the window, the extra part of the video frame will be cropped. After the scaling process is completed, the width or height of the video frame will be consistent with that of the window, and the other dimension will be greater than or equal to that of the window. |
|kVideoStreamScaleModeFitWithFilling |3 |Fit the window with filling Scale the video frame uniformly until its width or height reaches the boundary of the window. If the video frame's aspect ratio is different from that of the window, the area that is not filled will be black. After the scaling process is completed, the width or height of the video frame will be consistent with that of the window, and the other dimension will be less than or equal to that of the window. |


<span id="ZoomDirectionType"></span>
# ZoomDirectionType

```c#
enum class bytertc.ZoomDirectionType
```


Action of the digital zoom control

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kZoomDirectionTypeMoveLeft |0 |Move to the left. |
|kZoomDirectionTypeMoveRight |1 |Move to the right. |
|kZoomDirectionTypeMoveUp |2 |Move upwards. |
|kZoomDirectionTypeMoveDown |3 |Move downwards. |
|kZoomDirectionTypeZoomOut |4 |Zoom out. |
|kZoomDirectionTypeZoomIn |5 |Zoom in. |
|kZoomDirectionTypeReset |6 |Reset digital zoom. |


<span id="VideoSourceType"></span>
# VideoSourceType

```c#
enum class bytertc.VideoSourceType
```


Video source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VideoSourceTypeExternal |0 |Custom video source |
|VideoSourceTypeInternal |1 |Internal video capture |
|VideoSourceTypeEncodedWithAutoSimulcast |2 |Custom encoded video source. Push the encoded video stream with the largest resolution, and the SDK will automatically transcode to generate multiple lower\-quality streams for Simulcast. |
|VideoSourceTypeEncodedWithoutAutoSimulcast |3 |Custom encoded video source. The SDK does not automatically generate multiple streams for Simulcast, you need to generate and push streams of different qualities. |


<span id="AudioProcessorMethod"></span>
# AudioProcessorMethod

```c#
enum class bytertc.AudioProcessorMethod
```


The type of the audio for the audio processor

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioFrameProcessorRecord |0 |Locally captured audio frame |
|kAudioFrameProcessorPlayback |1 |The mixed remote audio |
|kAudioFrameProcessorRemoteUser |2 |The audio streams from remote users |
|kAudioFrameProcessorEarMonitor |3 |The SDK\-level in\-ear monitoring. |
|kAudioFrameProcessorScreen |4 |The shared\-screen audio. |


<span id="AudioChannel"></span>
# AudioChannel

```c#
enum class bytertc.AudioChannel
```


Audio channel

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioChannelAuto |\-1 |Default value. |
|kAudioChannelMono |1 |Mono channel |
|kAudioChannelStereo |2 |Dual channels |


<span id="VideoCaptureConfig"></span>
# VideoCaptureConfig

```c#
struct bytertc::VideoCaptureConfig
```


Video Capture Configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CapturePreference |[CapturePreference](https://docs.byteplus.com/en/docs/12/35817#VideoCaptureConfig-capturepreference) |
|int |[Width](https://docs.byteplus.com/en/docs/12/35817#VideoCaptureConfig-width) |
|int |[Height](https://docs.byteplus.com/en/docs/12/35817#VideoCaptureConfig-height) |
|int |[FrameRate](https://docs.byteplus.com/en/docs/12/35817#VideoCaptureConfig-framerate) |


<span id="instructions"></span>
## Instructions

<span id="VideoCaptureConfig-capturepreference"></span>
### CapturePreference

```c#
CapturePreference bytertc.VideoCaptureConfig.CapturePreference
```


Video capture preference. See [CapturePreference](https://docs.byteplus.com/en/docs/12/35817#VideoCaptureConfig-capturepreference).

<span id="VideoCaptureConfig-width"></span>
### Width

```c#
int bytertc.VideoCaptureConfig.Width
```


The width of video capture resolution in px.

<span id="VideoCaptureConfig-height"></span>
### Height

```c#
int bytertc.VideoCaptureConfig.Height
```


The height of video capture resolution in px.

<span id="VideoCaptureConfig-framerate"></span>
### FrameRate

```c#
int bytertc.VideoCaptureConfig.FrameRate
```


Video capture frame rate in fps.

<span id="UserOfflineReason"></span>
# UserOfflineReason

```c#
enum class bytertc.UserOfflineReason
```


The reason why the user left the room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kUserOfflineReasonQuit |0 |The remote user invokes the [LeaveRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-leaveroom) method to actively exit the room. |
|kUserOfflineReasonDropped |1 |The remote user is offline. |
|kUserOfflineReasonSwitchToInvisible |2 |The remote user switches to invisible. |


<span id="LocalStreamStats"></span>
# LocalStreamStats

```c#
struct bytertc::LocalStreamStats
```


Local audio/video stream statistics and network status, the reference period is 2s. After the local user publishes the audio/video stream successfully, the SDK will periodically notify the local user through `OnLocalStreamStatsEventHandler` the transmission status of the published audio/video stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|LocalAudioStats |[audio_stats](https://docs.byteplus.com/en/docs/12/35817#LocalStreamStats-audio_stats) |
|LocalVideoStats |[video_stats](https://docs.byteplus.com/en/docs/12/35817#LocalStreamStats-video_stats) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/35817#LocalStreamStats-is_screen) |


<span id="instructions"></span>
## Instructions

<span id="LocalStreamStats-audio_stats"></span>
### audio_stats

```c#
LocalAudioStats bytertc.LocalStreamStats.audio_stats
```


For statistics on audio streams sent by local devices. See [LocalAudioStats](https://docs.byteplus.com/en/docs/12/35817#LocalAudioStats).

<span id="LocalStreamStats-video_stats"></span>
### video_stats

```c#
LocalVideoStats bytertc.LocalStreamStats.video_stats
```


For statistics on video streams sent by local devices. See [LocalVideoStats](https://docs.byteplus.com/en/docs/12/35817#LocalVideoStats).

<span id="LocalStreamStats-is_screen"></span>
### is_screen

```c#
bool bytertc.LocalStreamStats.is_screen
```


Whether the media stream belongs to the user is a screen stream. You can know whether the current statistics come from mainstream or screen stream.

<span id="VoiceReverbConfig"></span>
# VoiceReverbConfig

```c#
struct bytertc::VoiceReverbConfig
```


Voice reverb effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[room_size](https://docs.byteplus.com/en/docs/12/35817#VoiceReverbConfig-room_size) |
|float |[decay_time](https://docs.byteplus.com/en/docs/12/35817#VoiceReverbConfig-decay_time) |
|float |[damping](https://docs.byteplus.com/en/docs/12/35817#VoiceReverbConfig-damping) |
|float |[wet_gain](https://docs.byteplus.com/en/docs/12/35817#VoiceReverbConfig-wet_gain) |
|float |[dry_gain](https://docs.byteplus.com/en/docs/12/35817#VoiceReverbConfig-dry_gain) |
|float |[pre_delay](https://docs.byteplus.com/en/docs/12/35817#VoiceReverbConfig-pre_delay) |


<span id="instructions"></span>
## Instructions

<span id="VoiceReverbConfig-room_size"></span>
### room_size

```c#
float bytertc.VoiceReverbConfig.room_size
```


The room size for reverb simulation. The range is `[0.0, 100.0]`. The default value is `50.0f`. The larger the room, the stronger the reverberation.

<span id="VoiceReverbConfig-decay_time"></span>
### decay_time

```c#
float bytertc.VoiceReverbConfig.decay_time
```


The decay time of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="VoiceReverbConfig-damping"></span>
### damping

```c#
float bytertc.VoiceReverbConfig.damping
```


The damping index of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="VoiceReverbConfig-wet_gain"></span>
### wet_gain

```c#
float bytertc.VoiceReverbConfig.wet_gain
```


The Intensity of the wet signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="VoiceReverbConfig-dry_gain"></span>
### dry_gain

```c#
float bytertc.VoiceReverbConfig.dry_gain
```


The Intensity of the dry signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="VoiceReverbConfig-pre_delay"></span>
### pre_delay

```c#
float bytertc.VoiceReverbConfig.pre_delay
```


The delay of the wet signal in ms. The range is `[0.0, 200.0]`. The default value is `0.0f`.

<span id="AttenuationType"></span>
# AttenuationType

```c#
enum class bytertc.AttenuationType
```


Volume Roll\-off modes that a sound has in an audio source

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAttenuationTypeNone |0 |Disable Volume Attenuation |
|kAttenuationTypeLinear |1 |Linear roll\-off mode which lowers the volume of the sound over the distance |
|kAttenuationTypeExponential |2 |Exponential roll\-off mode which exponentially decreases the volume of the sound with the distance raising |


<span id="Orientation"></span>
# Orientation

```c#
struct bytertc::Orientation
```


Coordinate

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/35817#Orientation-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/35817#Orientation-y) |
|float |[z](https://docs.byteplus.com/en/docs/12/35817#Orientation-z) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|Orientation |[Orientation](https://docs.byteplus.com/en/docs/12/35817#Orientation-orientation) |


<span id="instructions"></span>
## Instructions

<span id="Orientation-x"></span>
### x

```c#
float bytertc.Orientation.x
```


X direction vector

<span id="Orientation-y"></span>
### y

```c#
float bytertc.Orientation.y
```


Y direction vector

<span id="Orientation-z"></span>
### z

```c#
float bytertc.Orientation.z
```


Z direction vector

<span id="instructions"></span>
## Instructions

<span id="Orientation-orientation"></span>
### Orientation

```c#
bytertc.Orientation.Orientation(
    float x,
    float y,
    float z
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|x |float |\- |
|y |float |\- |
|z |float |\- |


<span id="HighlightConfig"></span>
# HighlightConfig

```c#
struct bytertc::HighlightConfig
```


Border highlighting settings for screen sharing

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[EnableHighlight](https://docs.byteplus.com/en/docs/12/35817#HighlightConfig-enablehighlight) |
|uint |[BorderColor](https://docs.byteplus.com/en/docs/12/35817#HighlightConfig-bordercolor) |
|int |[BorderWidth](https://docs.byteplus.com/en/docs/12/35817#HighlightConfig-borderwidth) |


<span id="instructions"></span>
## Instructions

<span id="HighlightConfig-enablehighlight"></span>
### EnableHighlight

```c#
bool bytertc.HighlightConfig.EnableHighlight
```


Whether to display a highlighted border, the default display.

<span id="HighlightConfig-bordercolor"></span>
### BorderColor

```c#
uint bytertc.HighlightConfig.BorderColor
```


The color of the border, the color format is hexadecimal ARGB: 0xAARRGGBB

<span id="HighlightConfig-borderwidth"></span>
### BorderWidth

```c#
int bytertc.HighlightConfig.BorderWidth
```


The width of the border, in pixels

<span id="FirstFrameSendState"></span>
# FirstFrameSendState

```c#
enum class bytertc.FirstFrameSendState
```


First frame sending status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kFirstFrameSendStateSending |0 |Sending |
|kFirstFrameSendStateSent |1 |Sent successfully |
|kFirstFrameSendStateEnd |2 |Send failed |


<span id="SubscribeConfig"></span>
# SubscribeConfig

```c#
struct bytertc::SubscribeConfig
```


Configuration information for manual subscription flows.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-is_screen) |
|bool |[sub_video](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-sub_video) |
|bool |[sub_audio](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-sub_audio) |
|int |[video_index](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-video_index) |
|int |[priority](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-priority) |
|int |[svc_layer](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-svc_layer) |
|int |[framerate](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-framerate) |
|int |[sub_width](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-sub_width) |
|int |[sub_height](https://docs.byteplus.com/en/docs/12/35817#SubscribeConfig-sub_height) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeConfig-is_screen"></span>
### is_screen

```c#
bool bytertc.SubscribeConfig.is_screen
```


Whether it is a screen stream (default is no).

<span id="SubscribeConfig-sub_video"></span>
### sub_video

```c#
bool bytertc.SubscribeConfig.sub_video
```


Whether to subscribe to videos.

<span id="SubscribeConfig-sub_audio"></span>
### sub_audio

```c#
bool bytertc.SubscribeConfig.sub_audio
```


Whether to subscribe to audio.

<span id="SubscribeConfig-video_index"></span>
### video_index

```c#
int bytertc.SubscribeConfig.video_index
```


Subscribed video stream resolution subscript. The default value is 0.

<span id="SubscribeConfig-priority"></span>
### priority

```c#
int bytertc.SubscribeConfig.priority
```


For the remote user's requirement priority.


* 0: Low, the default.

* 100: Medium.

* 200: High.


<span id="SubscribeConfig-svc_layer"></span>
### svc_layer

```c#
int bytertc.SubscribeConfig.svc_layer
```


The time domain hierarchy of the remote user. This only works if the stream supports the SVC feature.


* 0: No hierarchy specified (default)

* 1: T0 layer

* 2: T0 + T1 layer

* 3: T0 + T1 + T2 layer


<span id="SubscribeConfig-framerate"></span>
### framerate

```c#
int bytertc.SubscribeConfig.framerate
```


Expected maximum frame rate of the subscribed stream in px. The default value is 0, values greater than 10 are valid. If the frame rate of the stream published is lower than the value you set, or if your subscribed stream falls back under limited network conditions, the frame rate you set will drop accordingly. Only valid if the stream is coded with SVC technique.

<span id="SubscribeConfig-sub_width"></span>
### sub_width

```c#
int bytertc.SubscribeConfig.sub_width
```


The user specifies the width(px) of the most appropriate stream corresponding to the UI by specifying

<span id="SubscribeConfig-sub_height"></span>
### sub_height

```c#
int bytertc.SubscribeConfig.sub_height
```


The user specifies the height(px) of the most appropriate stream corresponding to the UI by specifying

<span id="MouseCursorCaptureState"></span>
# MouseCursorCaptureState

```c#
enum class bytertc.MouseCursorCaptureState
```


Whether to collect mouse information when collecting screen video stream internally

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMouseCursorCaptureStateOn |0 |Collect mouse information |
|kMouseCursorCaptureStateOff |1 |Do not collect mouse information |


<span id="VirtualBackgroundSourceType"></span>
# VirtualBackgroundSourceType

```c#
enum class bytertc.VirtualBackgroundSourceType
```


Virtual background type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVirtualBackgroundSourceTypeColor |0 |Replace the original background with a solid color. |
|kVirtualBackgroundSourceTypeImage |1 |Replace the original background with the specified image. |


<span id="NetworkType"></span>
# NetworkType

```c#
enum class bytertc.NetworkType
```


SDK Network connection type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kNetworkTypeUnknown |\-1 |Network connection type unknown. |
|kNetworkTypeDisconnected |0 |The network connection has been disconnected. |
|kNetworkTypeLAN |1 |The network connection type is LAN. |
|kNetworkTypeWIFI |2 |The network connection type is Wi\-Fi (including hotspots). |
|kNetworkTypeMobile2G |3 |The network connection type is 2G mobile network. |
|kNetworkTypeMobile3G |4 |The network connection type is 3G mobile network. |
|kNetworkTypeMobile4G |5 |The network connection type is 4G mobile network. |
|kNetworkTypeMobile5G |6 |The network connection type is 5G mobile network. |


<span id="VideoFrameInfo"></span>
# VideoFrameInfo

```c#
struct bytertc::VideoFrameInfo
```


Video frame information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/en/docs/12/35817#VideoFrameInfo-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/35817#VideoFrameInfo-height) |
|VideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/35817#VideoFrameInfo-rotation) |


<span id="instructions"></span>
## Instructions

<span id="VideoFrameInfo-width"></span>
### width

```c#
int bytertc.VideoFrameInfo.width
```


Width (pixels)

<span id="VideoFrameInfo-height"></span>
### height

```c#
int bytertc.VideoFrameInfo.height
```


High (pixels)

<span id="VideoFrameInfo-rotation"></span>
### rotation

```c#
VideoRotation bytertc.VideoFrameInfo.rotation
```


Video frame clockwise rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/35817#VideoRotation).

<span id="LocalVideoStreamState"></span>
# LocalVideoStreamState

```c#
enum class bytertc.LocalVideoStreamState
```


Local video stream status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalVideoStreamStateStopped |0 |Local video capture stop state |
|kLocalVideoStreamStateRecording |1 |Local video capture device activated |
|kLocalVideoStreamStateEncoding |2 |After local video capture, the first frame is encoded successfully |
|kLocalVideoStreamStateFailed |3 |Local video capture device failed to start |


<span id="AudioPropertiesInfo"></span>
# AudioPropertiesInfo

```c#
struct bytertc::AudioPropertiesInfo
```


Audio properties.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[LinearVolume](https://docs.byteplus.com/en/docs/12/35817#AudioPropertiesInfo-linearvolume) |
|int |[NonlinearVolume](https://docs.byteplus.com/en/docs/12/35817#AudioPropertiesInfo-nonlinearvolume) |
|float[] |[Spectrum](https://docs.byteplus.com/en/docs/12/35817#AudioPropertiesInfo-spectrum) |
|int |[Vad](https://docs.byteplus.com/en/docs/12/35817#AudioPropertiesInfo-vad) |


<span id="instructions"></span>
## Instructions

<span id="AudioPropertiesInfo-linearvolume"></span>
### LinearVolume

```c#
int bytertc.AudioPropertiesInfo.LinearVolume
```


linear volume. The value is in linear relation to the original volume. The higher the value, the higher the volume. The range is [0,255].


* [0, 25]: Nearly silent

* [26, 75]: Low volume

* [76, 204]: Medium volume

* [205, 255]: High volume


<span id="AudioPropertiesInfo-nonlinearvolume"></span>
### NonlinearVolume

```c#
int bytertc.AudioPropertiesInfo.NonlinearVolume
```


non\-linear volume in dB. The value is in proportion to the log value of the original volume. You can use the value to recognize the Active Speaker in the room. The range is [\-127, 0].


* [\-127, \-60]: Nearly silent

* [\-59, \-40]: Low volume

* [\-39, \-20]: Medium volume

* [\-19, 0]: High volume


<span id="AudioPropertiesInfo-spectrum"></span>
### Spectrum

```c#
float [] bytertc.AudioPropertiesInfo.Spectrum
```


Spectrum array

<span id="AudioPropertiesInfo-vad"></span>
### Vad

```c#
int bytertc.AudioPropertiesInfo.Vad
```


Voice Activity Detection (VAD) result


* 1: Voice activity detected.

* 0: No voice activity detected.

* \-1: VAD not activated.


<span id="RemoteAudioStateChangeReason"></span>
# RemoteAudioStateChangeReason

```c#
enum class bytertc.RemoteAudioStateChangeReason
```


Receives the cause of the remote audio stream state change. Users can learn about this reason through `OnRemoteAudioStateChangedEventHandler`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteAudioStateChangeReasonInternal |0 |Internal reasons |
|kRemoteAudioStateChangeReasonNetworkCongestion |1 |Network blocking |
|kRemoteAudioStateChangeReasonNetworkRecovery |2 |Network back to normal |
|kRemoteAudioStateChangeReasonLocalMuted |3 |Local user stops receiving remote audio stream |
|kRemoteAudioStateChangeReasonLocalUnmuted |4 |Local users resume receiving remote audio streams |
|kRemoteAudioStateChangeReasonRemoteMuted |5 |Remote user stops sending audio stream |
|kRemoteAudioStateChangeReasonRemoteUnmuted |6 |Remote user resumes sending audio stream |
|kRemoteAudioStateChangeReasonRemoteOffline |7 |Remote user leaves room |


<span id="ProblemFeedbackInfo"></span>
# ProblemFeedbackInfo

```c#
struct bytertc::ProblemFeedbackInfo
```


Information for audio & video quality feedback

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[problem_desc](https://docs.byteplus.com/en/docs/12/35817#ProblemFeedbackInfo-problem_desc) |
|IntPtr |[room_info](https://docs.byteplus.com/en/docs/12/35817#ProblemFeedbackInfo-room_info) |
|int |[room_info_count](https://docs.byteplus.com/en/docs/12/35817#ProblemFeedbackInfo-room_info_count) |


<span id="instructions"></span>
## Instructions

<span id="ProblemFeedbackInfo-problem_desc"></span>
### problem_desc

```c#
string bytertc.ProblemFeedbackInfo.problem_desc
```


Specific description of problems other than the preset problem.

<span id="ProblemFeedbackInfo-room_info"></span>
### room_info

```c#
IntPtr bytertc.ProblemFeedbackInfo.room_info
```


Room information for audio & video quality feedback. See [ProblemFeedbackRoomInfo](https://docs.byteplus.com/en/docs/12/35817#ProblemFeedbackRoomInfo).

<span id="ProblemFeedbackInfo-room_info_count"></span>
### room_info_count

```c#
int bytertc.ProblemFeedbackInfo.room_info_count
```


The length of `FeedbackRoomInfo`.

<span id="JoinRoomType"></span>
# JoinRoomType

```c#
enum class bytertc.JoinRoomType
```


The type of joining the room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kJoinRoomTypeFirst |0 |Join the room for the first time. The user calls `JoinRoom` to join the room. |
|kJoinRoomTypeReconnected |1 |Rejoin the room. The user loses connection to the server due to poor network, and rejoins the room successfully. |


<span id="ForwardStreamStateInfo"></span>
# ForwardStreamStateInfo

```c#
struct bytertc::ForwardStreamStateInfo
```


The state and error information of the different target rooms in the cross\-room forwarding of media streams

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[room_id](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamStateInfo-room_id) |
|ForwardStreamState |[state](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamStateInfo-state) |
|ForwardStreamError |[error](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamStateInfo-error) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamStateInfo-room_id"></span>
### room_id

```c#
string bytertc.ForwardStreamStateInfo.room_id
```


The room ID of the target room during the cross\-room forwarding of media streams.

<span id="ForwardStreamStateInfo-state"></span>
### state

```c#
ForwardStreamState bytertc.ForwardStreamStateInfo.state
```


The state of the target room during the cross\-room forwarding of media streams. See [ForwardStreamState](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamState)

<span id="ForwardStreamStateInfo-error"></span>
### error

```c#
ForwardStreamError bytertc.ForwardStreamStateInfo.error
```


The error code of the target room during the cross\-room forwarding of media streams. See [ForwardStreamError](https://docs.byteplus.com/en/docs/12/35817#ForwardStreamError)

<span id="ScreenFilterConfig"></span>
# ScreenFilterConfig

```c#
struct bytertc::ScreenFilterConfig
```


Excludes the specified window when grabbing the screen, no form is excluded by default

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|IntPtr[] |[ExcludedWindowList](https://docs.byteplus.com/en/docs/12/35817#ScreenFilterConfig-excludedwindowlist) |
|int |[ExcludedWindowNum](https://docs.byteplus.com/en/docs/12/35817#ScreenFilterConfig-excludedwindownum) |


<span id="instructions"></span>
## Instructions

<span id="ScreenFilterConfig-excludedwindowlist"></span>
### ExcludedWindowList

```c#
IntPtr [] bytertc.ScreenFilterConfig.ExcludedWindowList
```


Exclude the list of windows when grabbing the screen. This parameter only takes effect when the screen is captured.

<span id="ScreenFilterConfig-excludedwindownum"></span>
### ExcludedWindowNum

```c#
int bytertc.ScreenFilterConfig.ExcludedWindowNum
```


Exclude the number of windows.

<span id="RemoteStreamStats"></span>
# RemoteStreamStats

```c#
struct bytertc::RemoteStreamStats
```


The remote audio/video stream statistics and network status subscribed by the user, with a reference period of 2s. After the remote user subscribed to successfully publish the audio/video stream, the SDK will periodically notify local users through `OnRemoteStreamStatsEventHandler` the reception status of the remote audio/video stream subscribed during this reference period. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|string |[uid](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamStats-uid) |
|RemoteAudioStats |[audio_stats](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamStats-audio_stats) |
|RemoteVideoStats |[video_stats](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamStats-video_stats) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/35817#RemoteStreamStats-is_screen) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamStats-uid"></span>
### uid

```c#
string bytertc.RemoteStreamStats.uid
```


User ID. The remote user ID of the audio/video source.

<span id="RemoteStreamStats-audio_stats"></span>
### audio_stats

```c#
RemoteAudioStats bytertc.RemoteStreamStats.audio_stats
```


For statistics on remote audio streams. See [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/35817#RemoteAudioStats)

<span id="RemoteStreamStats-video_stats"></span>
### video_stats

```c#
RemoteVideoStats bytertc.RemoteStreamStats.video_stats
```


For statistics on remote video streams. See [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/35817#RemoteVideoStats)

<span id="RemoteStreamStats-is_screen"></span>
### is_screen

```c#
bool bytertc.RemoteStreamStats.is_screen
```


Whether the media stream belongs to the user is a screen stream. You can know whether the current statistics come from mainstream or screen stream.
