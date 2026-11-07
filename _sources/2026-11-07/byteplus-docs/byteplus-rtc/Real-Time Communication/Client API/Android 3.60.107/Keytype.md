---
title: "Keytype"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70083"
---

<span id="CapturePreference"></span>
# CapturePreference

```java
public enum com.ss.bytertc.engine.video.VideoCaptureConfig.CapturePreference
```


Video capture preference

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUTO |0 |(Default) Video capture preference: auto<br><br>&nbsp;<br><br>SDK determines the best video capture parameters referring to the camera output parameters and the encoder configuration. |
|MANUAL |1 |Video capture preference: manual<br><br>&nbsp;<br><br>Set the resolution and the frame rate manually. |
|AUTO_PERFORMANCE |2 |Video capture preference: encoder configuration<br><br>&nbsp;<br><br>The capture parameters are the same with the parameters set in [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideoencoderconfig). |


<span id="AudioProcessorMethod"></span>
# AudioProcessorMethod

```java
public enum com.ss.bytertc.engine.data.AudioProcessorMethod
```


The audio input for the audio processor.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_FRAME_PROCESSOR_RECORD |0 |Locally captured audio frame. |
|AUDIO_FRAME_PROCESSOR_PLAYBACK |1 |The mixed remote audio. |
|AUDIO_FRAME_PROCESSOR_REMOTE_USER |2 |The audio streams from remote users. |
|AUDIO_FRAME_PROCESSOR_EAR_MONITOR |3 |The SDK\-level in\-ear monitoring audio. |
|AUDIO_FRAME_PROCESSOR_SCREEN |4 |The shared\-screen audio. |


<span id="VideoSourceType"></span>
# VideoSourceType

```java
public enum com.ss.bytertc.engine.data.VideoSourceType
```


Video source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VIDEO_SOURCE_TYPE_EXTERNAL |0 |Custom video source |
|VIDEO_SOURCE_TYPE_INTERNAL |1 |Internal video capture |
|VIDEO_SOURCE_TYPE_ENCODED_WITH_SIMULCAST |2 |\- |
|VIDEO_SOURCE_TYPE_ENCODED_WITHOUT_SIMULCAST |3 |\- |


<span id="MessageConfig"></span>
# MessageConfig

```java
public enum com.ss.bytertc.engine.type.MessageConfig
```


Reliable orderliness of sent messages

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RELIABLE_ORDERED |0 |Low latency reliable and orderly message |
|UNRELIABLE_ORDERED |1 |Ultra\-low latency ordered message |
|UNRELIABLE_UNORDERED |2 |Ultra\-low latency unordered message |


<span id="ProblemFeedbackInfo"></span>
# ProblemFeedbackInfo

```java
public class com.ss.bytertc.engine.type.ProblemFeedbackInfo
```


Video call quality feedback preset information.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[problemDesc](https://docs.byteplus.com/en/docs/12/14169#ProblemFeedbackInfo-problemdesc) |
|List<ProblemFeedbackRoomInfo\> |\- |[roomInfo](https://docs.byteplus.com/en/docs/12/14169#ProblemFeedbackInfo-roominfo) |


<span id="instructions"></span>
## Instructions

<span id="ProblemFeedbackInfo-problemdesc"></span>
### problemDesc

```java
public String com.ss.bytertc.engine.type.ProblemFeedbackInfo.problemDesc
```


Text description

<span id="ProblemFeedbackInfo-roominfo"></span>
### roomInfo

```java
public List<ProblemFeedbackRoomInfo> com.ss.bytertc.engine.type.ProblemFeedbackInfo.roomInfo
```


Room info. See [ProblemFeedbackRoomInfo](https://docs.byteplus.com/en/docs/12/14169#ProblemFeedbackRoomInfo).

<span id="ExpressionDetectResult"></span>
# ExpressionDetectResult

```java
public class com.ss.bytertc.engine.video.ExpressionDetectResult
```


Expression Detection Result

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |10 |[MAX_COUNT](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectResult-max_count) |
|int |0 |[detectResult](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectResult-detectresult) |
|int |0 |[faceCount](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectResult-facecount) |
|ExpressionDetectInfo[] |\- |[detectInfo](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectResult-detectinfo) |


<span id="instructions"></span>
## Instructions

<span id="ExpressionDetectResult-max_count"></span>
### MAX_COUNT

```java
public static final int com.ss.bytertc.engine.video.ExpressionDetectResult.MAX_COUNT = 10
```


Face information storage limit, up to 10 faces can be stored.

<span id="ExpressionDetectResult-detectresult"></span>
### detectResult

```java
public int com.ss.bytertc.engine.video.ExpressionDetectResult.detectResult = 0
```


Expression detection result


* 0: Success

* !0: Failure

    &nbsp;


<span id="facecount"></span>
### faceCount

```java
public int com.ss.bytertc.engine.video.ExpressionDetectResult.faceCount = 0
```


The number of detected faces.

<span id="ExpressionDetectResult-detectinfo"></span>
### detectInfo

```java
public ExpressionDetectInfo [] com.ss.bytertc.engine.video.ExpressionDetectResult.detectInfo
```


Expression detection information. The length of the array is the same as the number of detected faces. See [ExpressionDetectInfo](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo).

<span id="UserInfo"></span>
# UserInfo

```java
public class com.ss.bytertc.engine.UserInfo
```


User information

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[uid](https://docs.byteplus.com/en/docs/12/14169#UserInfo-uid) |
|String |\- |[extraInfo](https://docs.byteplus.com/en/docs/12/14169#UserInfo-extrainfo) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|UserInfo |[UserInfo](https://docs.byteplus.com/en/docs/12/14169#UserInfo-userinfo) |


<span id="instructions"></span>
## Instructions

<span id="UserInfo-uid"></span>
### uid

```java
public String com.ss.bytertc.engine.UserInfo.uid
```


User ID. The string matches the regular expression: `[a-zA-Z0-9_\@\\-\\.]{1,128}`.

You must set or manage the uid yourself and ensure that each uid within the same room is unique.

<span id="UserInfo-extrainfo"></span>
### extraInfo

```java
public String com.ss.bytertc.engine.UserInfo.extraInfo
```


Additional information of the user. The maximum length is 200 bytes. The remote user will receive the info in `onUserJoined`.

<span id="instructions"></span>
## Instructions

<span id="UserInfo-userinfo"></span>
### UserInfo

```java
public com.ss.bytertc.engine.UserInfo.UserInfo(
    String uid,
    String extraInfo
)
```


User information

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID. The string matches the regular expression: `[a-zA-Z0-9_\@\\-\\.]{1,128}`. |
|extraInfo |String |Additional information of the user. The maximum length is 200 bytes. The remote user will receive the info in `onUserJoined`. |


<span id="ForwardStreamEvent"></span>
# ForwardStreamEvent

```java
public enum com.ss.bytertc.engine.data.ForwardStreamEventInfo.ForwardStreamEvent
```


Event from the room during relaying

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FORWARD_STREAM_EVENT_DISCONNECTED |0 |Relaying pauses for the reason of network disconnecting. |
|FORWARD_STREAM_EVENT_CONNECTED |1 |Relaying recovers from the disconnecting. |
|FORWARD_STREAM_EVENT_INTERRUPT |2 |Relaying aborts because a user with the same user ID as that of the publisher joins. |
|FORWARD_STREAM_EVENT_DST_ROOM_UPDATED |3 |Target room list updates after you call `updateForwardStreamToRooms`. |
|FORWARD_STREAM_EVENT_UN_EXPECT_API_CALL |4 |Wrong API\-calling order. For example, call `updateForwardStreamToRooms` before calling `startForwardStreamToRooms`. |


<span id="SubscribeMediaType"></span>
# SubscribeMediaType

```java
public enum com.ss.bytertc.engine.type.SubscribeMediaType
```


Type of the media stream subscribed to

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|NONE |0 |Neither audio nor video |
|AUDIO_ONLY |1 |Audio only |
|VIDEO_ONLY |2 |Video only |
|AUDIO_AND_VIDEO |3 |Both audio and video |


<span id="ConnectionState"></span>
# ConnectionState

```java
public enum com.ss.bytertc.engine.type.ConnectionState
```


The connection status between the client SDK and RTC server

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|CONNECTION_STATE_DISCONNECTED |1 |Disconnected for 12s, SDK will try to reconnect automatically. |
|CONNECTION_STATE_CONNECTING |2 |The first request to connect to the server. Connecting. |
|CONNECTION_STATE_CONNECTED |3 |The first connection was successful. |
|CONNECTION_STATE_RECONNECTING |4 |The code includes the following status:<br><br><br>&nbsp;<br><br>* The first connection is not successful for 10s.<br><br>* The connection has been lost for 10s. Auto reconnecting. |
|CONNECTION_STATE_RECONNECTED |5 |Successful reconnection after disconnection. |
|CONNECTION_STATE_LOST |6 |In status `CONNECTION_STATE_DISCONNECTED` for more than 10s without a successful reconnection. SDK will still continue to try to reconnect. |
|CONNECTION_STATE_FAILED |7 |Connection failure caused by abnormal state of the server. SDK will not automatically reconnect, please re\-enter the room or contact technical support. |


<span id="RecordingType"></span>
# RecordingType

```java
public enum com.ss.bytertc.engine.type.RecordingType
```


Locally recorded media type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RECORD_AUDIO_ONLY |0 |Audio only |
|RECORD_VIDEO_ONLY |1 |Video only |
|RECORD_VIDEO_AND_AUDIO |2 |Record audio and video simultaneously |


<span id="EarMonitorMode"></span>
# EarMonitorMode

```java
public enum com.ss.bytertc.engine.data.EarMonitorMode
```


Whether to enable in\-ear monitoring.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|EAR_MONITOR_MODE_OFF |0 |Off. |
|EAR_MONITOR_MODE_ON |1 |On |


<span id="FirstFrameSendState"></span>
# FirstFrameSendState

```java
public enum com.ss.bytertc.engine.type.FirstFrameSendState
```


First frame sending status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FIRST_FRAME_SEND_STATE_SENDING |0 |Sending |
|FIRST_FRAME_SEND_STATE_SENT |1 |Sent successfully |
|FIRST_FRAME_SEND_STAT_END |2 |Send failed |


<span id="VideoFrameData"></span>
# VideoFrameData

```java
public class com.ss.bytertc.engine.data.VideoFrameData
```


Video frame data

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|VideoBufferType |VideoBufferType.RAW_MEMORY |[bufferType](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-buffertype) |
|VideoPixelFormat |VideoPixelFormat.UNKNOWN |[pixelFormat](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-pixelformat) |
|VideoContentType |VideoContentType.NORMAL_FRAME |[contentType](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-contenttype) |
|long |\- |[timestampUs](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-timestampus) |
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-height) |
|VideoRotation |VideoRotation.VIDEO_ROTATION_0 |[rotation](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-rotation) |
|int |\- |[numberOfPlanes](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-numberofplanes) |
|ByteBuffer[] |\- |[planeData](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-planedata) |
|int[] |\- |[planeStride](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-planestride) |
|ByteBuffer |\- |[seiData](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-seidata) |
|ByteBuffer |\- |[roiData](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-roidata) |
|int |\- |[textureId](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-textureid) |
|float[] |\- |[textureMatrix](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-texturematrix) |
|EGLContext |\- |[eglContext](https://docs.byteplus.com/en/docs/12/14169#VideoFrameData-eglcontext) |


<span id="instructions"></span>
## Instructions

<span id="VideoFrameData-buffertype"></span>
### bufferType

```java
public VideoBufferType com.ss.bytertc.engine.data.VideoFrameData.bufferType = VideoBufferType.RAW_MEMORY
```


Video frame buffer type, see [VideoBufferType](https://docs.byteplus.com/en/docs/12/14169#VideoBufferType). Required.

<span id="VideoFrameData-pixelformat"></span>
### pixelFormat

```java
public VideoPixelFormat com.ss.bytertc.engine.data.VideoFrameData.pixelFormat = VideoPixelFormat.UNKNOWN
```


Video frame pixel format, see [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14169#VideoPixelFormat). Required, when `bufferType` is `RAW_MEMORY` or `GL_TEXTURE`.

<span id="VideoFrameData-contenttype"></span>
### contentType

```java
public VideoContentType com.ss.bytertc.engine.data.VideoFrameData.contentType = VideoContentType.NORMAL_FRAME
```


Video content type. See [VideoContentType](https://docs.byteplus.com/en/docs/12/14169#VideoContentType).

<span id="VideoFrameData-timestampus"></span>
### timestampUs

```java
public long com.ss.bytertc.engine.data.VideoFrameData.timestampUs
```


Video frame timestamp in microseconds. Required.

<span id="VideoFrameData-width"></span>
### width

```java
public int com.ss.bytertc.engine.data.VideoFrameData.width
```


Video frame width. Required.

<span id="VideoFrameData-height"></span>
### height

```java
public int com.ss.bytertc.engine.data.VideoFrameData.height
```


Video frame height. Required.

<span id="VideoFrameData-rotation"></span>
### rotation

```java
public VideoRotation com.ss.bytertc.engine.data.VideoFrameData.rotation = VideoRotation.VIDEO_ROTATION_0
```


Video frame rotation angle

<span id="VideoFrameData-numberofplanes"></span>
### numberOfPlanes

```java
public int com.ss.bytertc.engine.data.VideoFrameData.numberOfPlanes
```


The number of video frame planes. Required, when `bufferType` is `RAW_MEMORY`.

<span id="VideoFrameData-planedata"></span>
### planeData

```java
public ByteBuffer [] com.ss.bytertc.engine.data.VideoFrameData.planeData
```


Array of video frame planes. Required, when `bufferType` is `RAW_MEMORY`.

<span id="VideoFrameData-planestride"></span>
### planeStride

```java
public int [] com.ss.bytertc.engine.data.VideoFrameData.planeStride
```


Array of strides. Stride is the length of memory between two lines of image data in a video frame plane in bytes. Required, when `bufferType` is `RAW_MEMORY`.

<span id="VideoFrameData-seidata"></span>
### seiData

```java
public ByteBuffer com.ss.bytertc.engine.data.VideoFrameData.seiData
```


SEI data

<span id="VideoFrameData-roidata"></span>
### roiData

```java
public ByteBuffer com.ss.bytertc.engine.data.VideoFrameData.roiData
```


ROI(Region of Interest) Data in a video frame

<span id="VideoFrameData-textureid"></span>
### textureId

```java
public int com.ss.bytertc.engine.data.VideoFrameData.textureId
```


Texture ID. Required, when `bufferType` is `RAW_MEMORY` or `GL_TEXTURE`.

<span id="VideoFrameData-texturematrix"></span>
### textureMatrix

```java
public float [] com.ss.bytertc.engine.data.VideoFrameData.textureMatrix
```


Texture matrix

<span id="VideoFrameData-eglcontext"></span>
### eglContext

```java
public EGLContext com.ss.bytertc.engine.data.VideoFrameData.eglContext
```


EGLContext

<span id="SyncInfoStreamType"></span>
# SyncInfoStreamType

```java
public enum com.ss.bytertc.engine.data.StreamSyncInfoConfig.SyncInfoStreamType
```


Stream type for media stream information synchronization

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SYNC_INFO_STREAM_TYPE_AUDIO |0 |Audio stream |


<span id="SourceWantedData"></span>
# SourceWantedData

```java
public class com.ss.bytertc.engine.type.SourceWantedData
```


Performance fallback related data

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#SourceWantedData-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#SourceWantedData-height) |
|int |\- |[frameRate](https://docs.byteplus.com/en/docs/12/14169#SourceWantedData-framerate) |


<span id="instructions"></span>
## Instructions

<span id="SourceWantedData-width"></span>
### width

```java
public int com.ss.bytertc.engine.type.SourceWantedData.width
```


If send performance fallback is not turned on, this value represents the recommended video input width;

If send performance fallback is turned on, this value represents the maximum width of the current push stream.

<span id="SourceWantedData-height"></span>
### height

```java
public int com.ss.bytertc.engine.type.SourceWantedData.height
```


If send performance fallback is not turned on, this value represents the recommended video input height;

If send performance fallback is turned on, this value represents the maximum height of the current push stream.

<span id="SourceWantedData-framerate"></span>
### frameRate

```java
public int com.ss.bytertc.engine.type.SourceWantedData.frameRate
```


If send performance fallback is not turned on, this value represents the recommended video input frame rate in fps;

If send performance fallback is turned on, this value represents the maximum frame rate of the current push stream in fps.

<span id="VoiceChangerType"></span>
# VoiceChangerType

```java
public enum com.ss.bytertc.engine.type.VoiceChangerType
```


Change sound effect type. For more types, contact technical support.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VOICE_CHANGER_ORIGINAL |0 |Acoustic, no special effects |
|VOICE_CHANGER_GIANT |1 |Giant |
|VOICE_CHANGER_CHIPMUNK |2 |Chipmunk |
|VOICE_CHANGER_MINIONST |3 |Minion |
|VOICE_CHANGER_VIBRATO |4 |Vibrato |
|VOICE_CHANGER_ROBOT |5 |Robot |


<span id="VideoCodecType"></span>
# VideoCodecType

```java
public enum com.ss.bytertc.engine.VideoEncoderConfig.VideoCodecType
```


Encoding mode (H264, ByteVC1)

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|CODEC_TYPE_AUTO |0 |Other |
|CODEC_TYPE_H264 |1 |H264 |
|CODEC_TYPE_BYTEVC1 |2 |ByteVC1 |


<span id="EffectBeautyMode"></span>
# EffectBeautyMode

```java
public enum com.ss.bytertc.engine.data.EffectBeautyMode
```


Basic beauty effect.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|WHITE |0 |Brightening. |
|SMOOTH |1 |Smoothing. |
|SHARPEN |2 |Sharpening. |
|CLEAR |3 |Clarity. Integrating Effects SDK v4.4.2+ is required for this sub\-item. |


<span id="Orientation"></span>
# Orientation

```java
public class com.ss.bytertc.engine.data.Orientation
```


Direction Orientation Information

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |\- |[x](https://docs.byteplus.com/en/docs/12/14169#Orientation-x) |
|float |\- |[y](https://docs.byteplus.com/en/docs/12/14169#Orientation-y) |
|float |\- |[z](https://docs.byteplus.com/en/docs/12/14169#Orientation-z) |


<span id="instructions"></span>
## Instructions

<span id="Orientation-x"></span>
### x

```java
public float com.ss.bytertc.engine.data.Orientation.x
```


X\-coordinate

<span id="Orientation-y"></span>
### y

```java
public float com.ss.bytertc.engine.data.Orientation.y
```


Y\-coordinate

<span id="Orientation-z"></span>
### z

```java
public float com.ss.bytertc.engine.data.Orientation.z
```


Z\-coordinate

<span id="LiveMode"></span>
# LiveMode

```java
public enum com.ss.bytertc.engine.type.LiveMode
```


Live mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|LIVE_MODE_CO_HOST |1 |Co\-hosted live streaming. Focus on quality, the default video bitrate is higher. |
|LIVE_MODE_SOLO_HOST |2 |Single host live streaming. |


<span id="LocalLogLevel"></span>
# LocalLogLevel

```java
public enum com.ss.bytertc.engine.data.LocalLogLevel
```


Local log parameters.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|INFO |0 |Info level. |
|WARNING |1 |(Default) Warning level. |
|ERROR |2 |Error level. |
|NONE |3 |Turn off logging. |


<span id="ForwardStreamState"></span>
# ForwardStreamState

```java
public enum com.ss.bytertc.engine.data.ForwardStreamStateInfo.ForwardStreamState
```


The state of the relaying for each room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FORWARD_STREAM_STATE_IDLE |0 |Idle<br><br><br>&nbsp;<br><br>* The states of all rooms turn to idle after you call `stopForwardStreamToRooms`.<br><br>* The states of the rooms that you call `updateForwardStreamToRooms` to remove turn to idle. |
|FORWARD_STREAM_STATE_SUCCESS |1 |Start relaying.<br><br><br>&nbsp;<br><br>* The states of the rooms turn to this state after relaying starts successfully by calling `startForwardStreamToRooms`.<br><br>* The states of the rooms added by calling `updateForwardStreamToRooms` turn to this state after relaying starts successfully. |
|FORWARD_STREAM_STATE_FAILURE |2 |Relay fails. Refer to [ForwardStreamError](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamError) for more information.<br><br>&nbsp;<br><br>Once relaying fails, the state of the room turns to this state after calling `startForwardStreamToRooms` or `updateForwardStreamToRooms`. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamState-value) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamState-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.ForwardStreamStateInfo.ForwardStreamState.value()
```


Get the current value.

<span id="TorchState"></span>
# TorchState

```java
public enum com.ss.bytertc.engine.type.TorchState
```


Camera flash status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|TORCH_STATE_OFF |0 |Close |
|TORCH_STATE_ON |1 |Open |


<span id="ForwardStreamEventInfo"></span>
# ForwardStreamEventInfo

```java
public class com.ss.bytertc.engine.data.ForwardStreamEventInfo
```


Event from each room during relaying

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamEventInfo-roomid) |
|ForwardStreamEvent |\- |[event](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamEventInfo-event) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamEventInfo-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.data.ForwardStreamEventInfo.roomId
```


ID of the room where the media stream aims to relay to

An Empty string is for all rooms.

<span id="ForwardStreamEventInfo-event"></span>
### event

```java
public ForwardStreamEvent com.ss.bytertc.engine.data.ForwardStreamEventInfo.event
```


Event from the room during relaying.

<span id="RecordingConfig"></span>
# RecordingConfig

```java
public class com.ss.bytertc.engine.data.RecordingConfig
```


Local recording parameter configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[dirPath](https://docs.byteplus.com/en/docs/12/14169#RecordingConfig-dirpath) |
|RecordingFileType |RecordingFileType.MP4 |[recordingFileType](https://docs.byteplus.com/en/docs/12/14169#RecordingConfig-recordingfiletype) |


<span id="instructions"></span>
## Instructions

<span id="RecordingConfig-dirpath"></span>
### dirPath

```java
public String com.ss.bytertc.engine.data.RecordingConfig.dirPath
```


The absolute folder path to save the recording file. The filename will be generated by RTC. You need to ensure that you have read and write permissions to this path.

<span id="RecordingConfig-recordingfiletype"></span>
### recordingFileType

```java
public RecordingFileType com.ss.bytertc.engine.data.RecordingConfig.recordingFileType = RecordingFileType.MP4
```


Recording stored file format. See [RecordingFileType](https://docs.byteplus.com/en/docs/12/14169#RecordingFileType)

<span id="VideoCaptureConfig"></span>
# VideoCaptureConfig

```java
public class com.ss.bytertc.engine.video.VideoCaptureConfig
```


Video Capture Configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|CapturePreference |CapturePreference.AUTO |[capturePreference](https://docs.byteplus.com/en/docs/12/14169#VideoCaptureConfig-capturepreference) |
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#VideoCaptureConfig-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#VideoCaptureConfig-height) |
|int |\- |[frameRate](https://docs.byteplus.com/en/docs/12/14169#VideoCaptureConfig-framerate) |


<span id="instructions"></span>
## Instructions

<span id="VideoCaptureConfig-capturepreference"></span>
### capturePreference

```java
public CapturePreference com.ss.bytertc.engine.video.VideoCaptureConfig.capturePreference = CapturePreference.AUTO
```


Video capture preference. See [CapturePreference](https://docs.byteplus.com/en/docs/12/14169#VideoCaptureConfig-capturepreference).

<span id="VideoCaptureConfig-width"></span>
### width

```java
public int com.ss.bytertc.engine.video.VideoCaptureConfig.width
```


The width of video capture resolution in px.

<span id="VideoCaptureConfig-height"></span>
### height

```java
public int com.ss.bytertc.engine.video.VideoCaptureConfig.height
```


The height of video capture resolution in px.

<span id="VideoCaptureConfig-framerate"></span>
### frameRate

```java
public int com.ss.bytertc.engine.video.VideoCaptureConfig.frameRate
```


Video capture frame rate in fps.

<span id="HumanOrientation"></span>
# HumanOrientation

```java
public class com.ss.bytertc.engine.data.HumanOrientation
```


Three\-dimensional orientation information, each pair of vectors need to be perpendicular. See [Orientation](https://docs.byteplus.com/en/docs/12/14169#Orientation).

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|Orientation |\- |[forward](https://docs.byteplus.com/en/docs/12/14169#HumanOrientation-forward) |
|Orientation |\- |[right](https://docs.byteplus.com/en/docs/12/14169#HumanOrientation-right) |
|Orientation |\- |[up](https://docs.byteplus.com/en/docs/12/14169#HumanOrientation-up) |


<span id="instructions"></span>
## Instructions

<span id="HumanOrientation-forward"></span>
### forward

```java
public Orientation com.ss.bytertc.engine.data.HumanOrientation.forward
```


Forward orientation, the default value is `{1,0,0}`, i.e., the forward orientation is in the positive direction of x\-axis.

<span id="HumanOrientation-right"></span>
### right

```java
public Orientation com.ss.bytertc.engine.data.HumanOrientation.right
```


Rightward orientation, the default value is `{0,1,0}`, i.e., the rightward orientation is in the positive direction of y\-axis.

<span id="HumanOrientation-up"></span>
### up

```java
public Orientation com.ss.bytertc.engine.data.HumanOrientation.up
```


Upward orientation, the default value is `{0,0,1}`, i.e., the upward orientation is in the positive direction of z\-axis.

<span id="LocalAudioPropertiesInfo"></span>
# LocalAudioPropertiesInfo

```java
public class com.ss.bytertc.engine.data.LocalAudioPropertiesInfo
```


Local audio properties

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|IAudioSource |\- |[audioSource](https://docs.byteplus.com/en/docs/12/14169#LocalAudioPropertiesInfo-audiosource) |
|AudioPropertiesInfo |\- |[audioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14169#LocalAudioPropertiesInfo-audiopropertiesinfo) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioPropertiesInfo-audiosource"></span>
### audioSource

```java
public IAudioSource com.ss.bytertc.engine.data.LocalAudioPropertiesInfo.audioSource
```


Audio source, see IAudioSource.

<span id="LocalAudioPropertiesInfo-audiopropertiesinfo"></span>
### audioPropertiesInfo

```java
public AudioPropertiesInfo com.ss.bytertc.engine.data.LocalAudioPropertiesInfo.audioPropertiesInfo
```


Audio attribute information, see [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesInfo).

<span id="MixedStreamLayoutRegionConfig"></span>
# MixedStreamLayoutRegionConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig
```


Layout information for one of the video streams or image to be mixed.

After starting to push streams to CDN and mixing multiple video streams, you can set the layout information for each of them.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |"" |[userID](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-userid) |
|String |"" |[roomID](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-roomid) |
|int |0 |[locationX](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-locationx) |
|int |0 |[locationY](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-locationy) |
|int |360 |[width](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-width) |
|int |640 |[height](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-height) |
|int |0 |[zOrder](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-zorder) |
|double |1.0 |[alpha](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-alpha) |
|double |0.0 |[cornerRadius](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-cornerradius) |
|MixedStreamMediaType |MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO |[mediaType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-mediatype) |
|MixedStreamRenderMode |MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN |[renderMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-rendermode) |
|boolean |false |[isLocalUser](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-islocaluser) |
|MixedStreamVideoType |MixedStreamVideoType.MIXED_STREAM_VIDEO_TYPE_MAIN |[streamType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-streamtype) |
|MixedStreamLayoutRegionType |MixedStreamLayoutRegionType.MIXED_STREAM_LAYOUT_REGION_TYPE_VIDEO_STREAM |[regionContentType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-regioncontenttype) |
|byte[] |null |[imageWaterMark](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-imagewatermark) |
|MixedStreamLayoutRegionImageWaterMarkConfig |newMixedStreamLayoutRegionImageWaterMarkConfig(0, 0) |[imageWaterMarkConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-imagewatermarkconfig) |
|MixedStreamAlternateImageFillMode |MixedStreamAlternateImageFillMode.FIT |[alternateImageFillMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-alternateimagefillmode) |
|String |"" |[alternateImageURL](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-alternateimageurl) |
|Position |newPosition() |[spatialPosition](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-spatialposition) |
|boolean |true |[applySpatialAudio](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-appliespatialaudio) |
|SourceCrop |newSourceCrop() |[sourceCrop](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-sourcecrop) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamLayoutRegionConfig |[MixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-mixedstreamlayoutregionconfig) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamLayoutRegionConfig-userid"></span>
### userID

```java
public String com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.userID = ""
```


Sets the user ID of the user who publishes the video stream.

**Notes**

This parameter cannot be updated during the task.

<span id="MixedStreamLayoutRegionConfig-roomid"></span>
### roomID

```java
public String com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.roomID = ""
```


Sets the room ID of the user who publishes the video stream.

**Notes**

This parameter cannot be updated during the task.

<span id="MixedStreamLayoutRegionConfig-locationx"></span>
### locationX

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.locationX = 0
```


> Available since 3.57


Sets the X\-coordinate in pixels of the upper\-left corner of the user's frame in the entire canvas coordinate system, where the origin is at the upper\-left corner of the canvas. It represents the horizontal displacement of the upper\-left corner of the user's frame relative to the origin.

<span id="MixedStreamLayoutRegionConfig-locationy"></span>
### locationY

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.locationY = 0
```


> Available since 3.57


Sets the Y\-coordinate in pixels of the upper\-left corner of the user's frame in the entire canvas coordinate system, where the origin is at the upper\-left corner of the canvas. It represents the vertical displacement of the upper\-left corner of the user's frame relative to the origin.

<span id="MixedStreamLayoutRegionConfig-width"></span>
### width

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.width = 360
```


> Available since 3.57


Sets the width of the user's frame in pixels.

<span id="MixedStreamLayoutRegionConfig-height"></span>
### height

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.height = 640
```


> Available since 3.57


Sets the height of the user's frame in pixels.

<span id="MixedStreamLayoutRegionConfig-zorder"></span>
### zOrder

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.zOrder = 0
```


Sets the layer on which the video is rendered.

<span id="MixedStreamLayoutRegionConfig-alpha"></span>
### alpha

```java
public double com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.alpha = 1.0
```


Sets the transparency.

<span id="MixedStreamLayoutRegionConfig-cornerradius"></span>
### cornerRadius

```java
public double com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.cornerRadius = 0.0
```


Sets the corner radius.

**Notes**

After you set the value, `width_px`, `height_px`, and `radius_px` are calculated based on `width`, `height`, `radius`, and the width of the canvas. If `radius_px < min(width_px/2, height_px/2)` is met, the value of `radius` is set valid; if not, `radius_px` is set to `min(width_px/2, height_px/2)`, and `radius` is set to the proportion of `radius_px` to the width of the canvas.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-mediatype"></span>
### mediaType

```java
public MixedStreamMediaType com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.mediaType = MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO
```


(Only server\-side stream mixing can set this parameter.) Sets the stream mixing content type.

<span id="MixedStreamLayoutRegionConfig-rendermode"></span>
### renderMode

```java
public MixedStreamRenderMode com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.renderMode = MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN
```


Sets the render mode.

<span id="MixedStreamLayoutRegionConfig-islocaluser"></span>
### isLocalUser

```java
public boolean com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.isLocalUser = false
```


Sets whether the source user of the stream is a local user.

<span id="MixedStreamLayoutRegionConfig-streamtype"></span>
### streamType

```java
public MixedStreamVideoType com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.streamType = MixedStreamVideoType.MIXED_STREAM_VIDEO_TYPE_MAIN
```


Reserved field.

<span id="MixedStreamLayoutRegionConfig-regioncontenttype"></span>
### regionContentType

```java
public MixedStreamLayoutRegionType com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.regionContentType = MixedStreamLayoutRegionType.MIXED_STREAM_LAYOUT_REGION_TYPE_VIDEO_STREAM
```


Sets the stream mixing region type.

<span id="MixedStreamLayoutRegionConfig-imagewatermark"></span>
### imageWaterMark

```java
public byte [] com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.imageWaterMark = null
```


The RGBA data of the watermark.

<span id="MixedStreamLayoutRegionConfig-imagewatermarkconfig"></span>
### imageWaterMarkConfig

```java
public MixedStreamLayoutRegionImageWaterMarkConfig com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.imageWaterMarkConfig = newMixedStreamLayoutRegionImageWaterMarkConfig(0, 0)
```


Sets the resolution of the watermark.

<span id="MixedStreamLayoutRegionConfig-alternateimagefillmode"></span>
### alternateImageFillMode

```java
public MixedStreamAlternateImageFillMode com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.alternateImageFillMode = MixedStreamAlternateImageFillMode.FIT
```


> Available since 3.57


Sets the fill mode of the placeholder image.

This method is used to control the fill mode of the placeholder image after the user stops publishing video streams and the screen reverts to the placeholder image.

<span id="MixedStreamLayoutRegionConfig-alternateimageurl"></span>
### alternateImageURL

```java
public String com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.alternateImageURL = ""
```


> Available since 3.57


Sets the URL of the placeholder image

<span id="MixedStreamLayoutRegionConfig-spatialposition"></span>
### spatialPosition

```java
public Position com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.spatialPosition = newPosition()
```


Sets spatial audio position of the current region.

**Notes**

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-appliespatialaudio"></span>
### applySpatialAudio

```java
public boolean com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.applySpatialAudio = true
```


Sets whether a user applies spatial audio effects.

<span id="MixedStreamLayoutRegionConfig-sourcecrop"></span>
### sourceCrop

```java
public SourceCrop com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.sourceCrop = newSourceCrop()
```


Configurations on how to crop the WTN stream.

**Notes**

This parameter is not supported for mixing\-stream tasks.

<span id="instructions"></span>
## Instructions

<span id="MixedStreamLayoutRegionConfig-mixedstreamlayoutregionconfig"></span>
### MixedStreamLayoutRegionConfig

```java
public com.ss.bytertc.engine.live.MixedStreamLayoutRegionConfig.MixedStreamLayoutRegionConfig()
```


<span id="AudioAlignmentMode"></span>
# AudioAlignmentMode

```java
public enum com.ss.bytertc.engine.data.AudioAlignmentMode
```


The alignment mode of remote audio streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_ALIGNMENT_MODE_OFF |0 |Disabled |
|AUDIO_ALIGNMENT_MODE_AUDIOMIXING |1 |All subscribed audio streams are aligned based on the process of the background music. |


<span id="FallbackOrRecoverReason"></span>
# FallbackOrRecoverReason

```java
public enum com.ss.bytertc.engine.type.FallbackOrRecoverReason
```


Reason of the Fallback or reverting from a Fallback of the subscribed stream or the publishing stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FALLBACK_OR_RECOVER_REASON_UNKNOWN |\-1 |The default: Fallback due to an unknown reason that is neither insufficient bandwidth of the network nor poor\-performance of the device |
|FALLBACK_OR_RECOVER_REASON_SUBSCRIBE_FALLBACK_BY_BANDWIDTH |0 |Fallback of the subscribed stream due to insufficient bandwidth of the network |
|FALLBACK_OR_RECOVER_REASON_SUBSCRIBE_FALLBACK_BY_PERFORMANCE |1 |Fallback of the subscribed stream due to poor performance of the device |
|FALLBACK_OR_RECOVER_REASON_SUBSCRIBE_RECOVER_BY_BANDWIDTH |2 |Reverting from a Fallback of the subscribed stream due to the recovery of the network bandwidth |
|FALLBACK_OR_RECOVER_REASON_SUBSCRIBE_RECOVER_BY_PERFORMANCE |3 |Reverting from a Fallback of the subscribed stream due to the amelioration of the device performance |
|FALLBACK_OR_RECOVER_REASON_PUBLISH_FALLBACK_BY_BANDWIDTH |4 |Fallback of the publishing stream due to Insufficient bandwidth of the network |
|FALLBACK_OR_RECOVER_REASON_PUBLISH_FALLBACK_BY_PERFORMANCE |5 |Fallback of the publishing stream due to poor\-performance of the device |
|FALLBACK_OR_RECOVER_REASON_PUBLISH_RECOVER_BY_BANDWIDTH |6 |Reverting from a Fallback of the publishing stream due to the recovery of the network bandwidth |
|FALLBACK_OR_RECOVER_REASON_PUBLISH_RECOVER_BY_PERFORMANCE |7 |Reverting from a Fallback of the publishing stream due to the amelioration of the device performance |


<span id="SEIStreamUpdateEvent"></span>
# SEIStreamUpdateEvent

```java
public enum com.ss.bytertc.engine.type.SEIStreamUpdateEvent
```


State of the black frame video stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|STREAM_ADD |0 |A black frame video stream is published from the remote user.<br><br>&nbsp;<br><br>In a voice call, when the remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage) to send SEI data, SDK will automatically publish a black frame video stream, and trigger this callback. |
|STREAM_REMOVE |1 |The black frame video stream is removed. The timing this callback will be triggered is as following:<br><br><br>&nbsp;<br><br>* The remote user turns on their camera, switching from a voice call to a video call.<br><br>* No SEI data is sent within 1min after the remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage).<br><br>* The black frame video stream stops when the remote user calls [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideosourcetype) to switch to custom video capture. |


<span id="RemoteStreamStats"></span>
# RemoteStreamStats

```java
public class com.ss.bytertc.engine.type.RemoteStreamStats
```


The remote audio/video stream statistics and network status subscribed by the user, with a reference period of 2s.

After the remote user successfully publishes the audio/video stream, the SDK will periodically notify local users of the reception status of the subscribed remote audio/video stream during this reference period through `onRemoteStreamStats`. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[uid](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamStats-uid) |
|RemoteAudioStats |\- |[audioStats](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamStats-audiostats) |
|RemoteVideoStats |\- |[videoStats](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamStats-videostats) |
|boolean |\- |[isScreen](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamStats-isscreen) |
|int |\- |[deprecated] [txQuality](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamStats-txquality) |
|int |\- |[deprecated] [rxQuality](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamStats-rxquality) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamStats-uid"></span>
### uid

```java
public String com.ss.bytertc.engine.type.RemoteStreamStats.uid
```


User ID. The remote user ID of the audio/video source.

<span id="RemoteStreamStats-audiostats"></span>
### audioStats

```java
public RemoteAudioStats com.ss.bytertc.engine.type.RemoteStreamStats.audioStats
```


For statistics on remote audio streams. See [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats)

<span id="RemoteStreamStats-videostats"></span>
### videoStats

```java
public RemoteVideoStats com.ss.bytertc.engine.type.RemoteStreamStats.videoStats
```


For statistics on remote video streams. See [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats)

<span id="RemoteStreamStats-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.type.RemoteStreamStats.isScreen
```


Reserved field. Ignore the value returned in this field.

<span id="RemoteStreamStats-txquality"></span>
### txQuality

```java
public int com.ss.bytertc.engine.type.RemoteStreamStats.txQuality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onnetworkquality) instead.


For the uplink network quality of the media stream owned by the user. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality).

<span id="RemoteStreamStats-rxquality"></span>
### rxQuality

```java
public int com.ss.bytertc.engine.type.RemoteStreamStats.rxQuality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onnetworkquality) instead.


The downlink network quality of the media stream belongs to the user. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality).

<span id="MediaDeviceWarning"></span>
# MediaDeviceWarning

```java
public class com.ss.bytertc.engine.type.MediaDeviceWarning
```


Media device warning

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[MEDIA_DEVICE_WARNING_OK](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_ok) |
|int |1 |[MEDIA_DEVICE_WARNING_OPERATION_DENIED](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_operation_denied) |
|int |2 |[MEDIA_DEVICE_WARNING_CAPTURE_SILENCE](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_capture_silence) |
|int |3 |[MEDIA_DEVICE_WARNING_ANDROID_SYS_SILENCE](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_android_sys_silence) |
|int |4 |[MEDIA_DEVICE_WARNING_ANDROID_SYS_SILENCE_DISAPPEAR](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_android_sys_silence_disappear) |
|int |11 |[MEDIA_DEVICE_WARNING_DETECT_LEAK_ECHO](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_detect_leak_echo) |
|int |16 |[MEDIA_DEVICE_WARNING_CAPTURE_DETECT_HOWLING](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_capture_detect_howling) |
|int |20 |[MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_INVALID_SCENARIO](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_set_audio_route_invalid_scenario) |
|int |21 |[MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_NOT_EXISTS](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_set_audio_route_not_exists) |
|int |22 |[MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_FAILED_BY_PRIORITY](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_set_audio_route_failed_by_priority) |
|int |23 |[MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_NOT_VOIP_MODE](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_set_audio_route_not_voip_mode) |
|int |24 |[MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_DEVICE_NOT_START](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceWarning-media_device_warning_set_audio_route_device_not_start) |


<span id="instructions"></span>
## Instructions

<span id="MediaDeviceWarning-media_device_warning_ok"></span>
### MEDIA_DEVICE_WARNING_OK

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_OK = 0
```


No warning

<span id="MediaDeviceWarning-media_device_warning_operation_denied"></span>
### MEDIA_DEVICE_WARNING_OPERATION_DENIED

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_OPERATION_DENIED = 1
```


Illegal device operation. Calls the API for internal device when using the external device.

<span id="MediaDeviceWarning-media_device_warning_capture_silence"></span>
### MEDIA_DEVICE_WARNING_CAPTURE_SILENCE

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_CAPTURE_SILENCE = 2
```


The media device is capturing silent frames.

<span id="MediaDeviceWarning-media_device_warning_android_sys_silence"></span>
### MEDIA_DEVICE_WARNING_ANDROID_SYS_SILENCE

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_ANDROID_SYS_SILENCE = 3
```


Silence warning by Android system.

<span id="MediaDeviceWarning-media_device_warning_android_sys_silence_disappear"></span>
### MEDIA_DEVICE_WARNING_ANDROID_SYS_SILENCE_DISAPPEAR

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_ANDROID_SYS_SILENCE_DISAPPEAR = 4
```


Silence disappearing warning by Android system.

<span id="MediaDeviceWarning-media_device_warning_detect_leak_echo"></span>
### MEDIA_DEVICE_WARNING_DETECT_LEAK_ECHO

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_DETECT_LEAK_ECHO = 11
```


Echoes between mics and speakers are detected during a call.

`onAudioDeviceWarning` notifies you with this enum of echo issue. During a call, SDK will detect echo issue only when [ChannelProfile](https://docs.byteplus.com/en/docs/12/14169#ChannelProfile) is set to `CHANNEL_PROFIEL_MEETING` or `CHANNEL_PROFILE_MEETING_ROOM` and AEC is disabled.

<span id="MediaDeviceWarning-media_device_warning_capture_detect_howling"></span>
### MEDIA_DEVICE_WARNING_CAPTURE_DETECT_HOWLING

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_CAPTURE_DETECT_HOWLING = 16
```


Howling detected.

You will receive this callback in the following scenarios:


* Howling is detected under the room profiles that do not support howling suppression;

* Detect howling that is not suppressed under the room profiles that support howling suppression.

   You can only enable howling suppression when the room profile is CHANNEL_PROFILE_COMMUNICATION(0), CHANNEL_PROFIEL_MEETING(16), or CHANNEL_PROFILE_MEETING_ROOM(17).


We recommend that you remind your users to adjust the physical distance between two devices or disable all unused devices except the connecting one.

<span id="MediaDeviceWarning-media_device_warning_set_audio_route_invalid_scenario"></span>
### MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_INVALID_SCENARIO

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_INVALID_SCENARIO = 20
```


Setting audio route failed because the audio route can not be changed in the current Audio Scenario.

<span id="MediaDeviceWarning-media_device_warning_set_audio_route_not_exists"></span>
### MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_NOT_EXISTS

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_NOT_EXISTS = 21
```


Setting audio route failed because the routing device did not exist.

<span id="MediaDeviceWarning-media_device_warning_set_audio_route_failed_by_priority"></span>
### MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_FAILED_BY_PRIORITY

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_FAILED_BY_PRIORITY = 22
```


Setting audio route failed because the audio route was occupied by the system or the other Apps.

<span id="MediaDeviceWarning-media_device_warning_set_audio_route_not_voip_mode"></span>
### MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_NOT_VOIP_MODE

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_NOT_VOIP_MODE = 23
```


Setting audio route failed because the audio route can only be changed in AUDIO_SCENARIO_COMMUNICATION(2) mode.

<span id="MediaDeviceWarning-media_device_warning_set_audio_route_device_not_start"></span>
### MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_DEVICE_NOT_START

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceWarning.MEDIA_DEVICE_WARNING_SET_AUDIO_ROUTE_DEVICE_NOT_START = 24
```


Setting audio route failed because the audio route did not initiate.

<span id="RemoteVideoRenderConfig"></span>
# RemoteVideoRenderConfig

```java
public class com.ss.bytertc.engine.RemoteVideoRenderConfig
```


Remote video rendering configuration.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[renderMode](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoRenderConfig-rendermode) |
|int |\- |[backgroundColor](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoRenderConfig-backgroundcolor) |
|VideoRotation |\- |[renderRotation](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoRenderConfig-renderrotation) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoRenderConfig-rendermode"></span>
### renderMode

```java
public int com.ss.bytertc.engine.RemoteVideoRenderConfig.renderMode
```


Rendering mode.


* 1(`RENDER_MODE_HIDDEN`): Fill and Crop. Default setting. The video frame is scaled with a fixed aspect ratio and completely fills the canvas. The region of the video exceeding the canvas will be cropped.

* 2(`RENDER_MODE_FIT`): Fit. The video frame is scaled with a fixed aspect ratio and is shown completely on the canvas. The region of the canvas not filled with the video frame will be filled with `backgroundColor`.

* 3(`RENDER_MODE_FILL`): Fill the canvas. The video frame is scaled to fill the canvas. During the process, the aspect ratio may change.

    &nbsp;


<span id="backgroundcolor"></span>
### backgroundColor

```java
public int com.ss.bytertc.engine.RemoteVideoRenderConfig.backgroundColor
```


Set the background color of the canvas which is not filled with video frame. The range is `[0x00000000, 0xFFFFFFFF]`. The default is `0x00000000`. The Alpha index is ignored.

<span id="RemoteVideoRenderConfig-renderrotation"></span>
### renderRotation

```java
public VideoRotation com.ss.bytertc.engine.RemoteVideoRenderConfig.renderRotation
```


Video frame rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14169#VideoRotation). The default value is 0, which means no rotation is applied.

<span id="AudioProfileType"></span>
# AudioProfileType

```java
public enum com.ss.bytertc.engine.type.AudioProfileType
```


Sound quality

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_PROFILE_DEFAULT |0 |Default sound quality<br><br>&nbsp;<br><br>The sound quality configuration of [ChannelProfile](https://docs.byteplus.com/en/docs/12/14169#ChannelProfile) sent by the server or set by the client side |
|AUDIO_PROFILE_FLUENT |1 |Fluent<br><br>&nbsp;<br><br>Sample rate: 16 KHz<br><br>&nbsp;<br><br>Mono\-channel<br><br>&nbsp;<br><br>Encoding bitrate: 32 Kbps<br><br>&nbsp;<br><br>Low resource consumption, and small network packets guarantee a smooth call. It is suitable for most game scenarios, such as team\-wide voice chat, group\-wide voice chat, nation\-wide voice chat. |
|AUDIO_PROFILE_STANDARD |2 |Mono\-channel standard<br><br>&nbsp;<br><br>Sample rate: 24 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 48 Kbps<br><br>&nbsp;<br><br>For scenarios requiring distinct voice, you can choose this mode, which achieves balanced latency, consumption, and network packets. It is suitable for educational Apps and the online Mafia Games. |
|AUDIO_PROFILE_HD |3 |Dual\-channel music<br><br>&nbsp;<br><br>Sample rate: 48 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 128 Kbps<br><br>&nbsp;<br><br>This mode provides high\-resolution audio at a cost of high latency, consumption, and large network packets. It is suitable for music Apps such as co\-hosting and online talent contests.<br><br>&nbsp;<br><br>Not recommended for game Apps. |
|AUDIO_PROFILE_STANDARD_STEREO |4 |Dual\-channel standard<br><br>&nbsp;<br><br>Sample rate: 48 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 80 Kbps |
|AUDIO_PROFILE_HD_MONO |5 |Mono\-channel music<br><br>&nbsp;<br><br>Sample rate: 48 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 64 Kbps |


<span id="CameraId"></span>
# CameraId

```java
public enum com.ss.bytertc.engine.data.CameraId
```


Camera type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|CAMERA_ID_FRONT |0 |Front\-facing camera |
|CAMERA_ID_BACK |1 |Rear camera (default setting) |
|CAMERA_ID_INVALID |3 |Invalid value |


<span id="CodecMode"></span>
# CodecMode

```java
public enum com.ss.bytertc.engine.VideoEncoderConfig.CodecMode
```


Encoder Mode (softcoding or hardcoding)

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|CODEC_MODE_AUTO |0 |Automatic mode |
|CODEC_MODE_HARDWARE |1 |Hardware encoding mode |
|CODEC_MODE_SOFTWARE |2 |Software encoding mode |


<span id="AudioEffectPlayerConfig"></span>
# AudioEffectPlayerConfig

```java
public class com.ss.bytertc.engine.data.AudioEffectPlayerConfig
```


Mixing configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|AudioMixingType |AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH |[type](https://docs.byteplus.com/en/docs/12/14169#AudioEffectPlayerConfig-type) |
|int |1 |[playCount](https://docs.byteplus.com/en/docs/12/14169#AudioEffectPlayerConfig-playcount) |
|int |0 |[startPos](https://docs.byteplus.com/en/docs/12/14169#AudioEffectPlayerConfig-startpos) |
|int |0 |[pitch](https://docs.byteplus.com/en/docs/12/14169#AudioEffectPlayerConfig-pitch) |


<span id="instructions"></span>
## Instructions

<span id="AudioEffectPlayerConfig-type"></span>
### type

```java
public AudioMixingType com.ss.bytertc.engine.data.AudioEffectPlayerConfig.type = AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH
```


Mixing playback types. See [AudioMixingType](https://docs.byteplus.com/en/docs/12/14169#AudioMixingType)

<span id="AudioEffectPlayerConfig-playcount"></span>
### playCount

```java
public int com.ss.bytertc.engine.data.AudioEffectPlayerConfig.playCount = 1
```


Mix playback times


* Play_count < = 0: Infinite loop

* Play_count == 1: Play once (default)

* Play_count \> 1: Play play_count times

    &nbsp;


<span id="startpos"></span>
### startPos

```java
public int com.ss.bytertc.engine.data.AudioEffectPlayerConfig.startPos = 0
```


The starting position in ms. 0 by default.

<span id="AudioEffectPlayerConfig-pitch"></span>
### pitch

```java
public int com.ss.bytertc.engine.data.AudioEffectPlayerConfig.pitch = 0
```


The increase or decrease value compared with the original pitch of the music file. The range is `[-12, 12]`. The default value is 0. The pitch distance between two adjacent values is half a step. A positive value indicates a rising pitch, and a negative value indicates a falling pitch.

<span id="LocalVideoStreamError"></span>
# LocalVideoStreamError

```java
public enum com.ss.bytertc.engine.type.LocalVideoStreamError
```


Error code when the local video state changes

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|LOCAL_VIDEO_STREAM_ERROR_OK |0 |Normal status (default return value when local video status changes to normal) |
|LOCAL_VIDEO_STREAM_ERROR_FAILURE |1 |Local video stream publishing failed |
|LOCAL_VIDEO_STREAM_ERROR_DEVICE_NO_PERMISSION |2 |No access to the local video capture device |
|LOCAL_VIDEO_STREAM_ERROR_DEVICE_BUSY |3 |Local video capture equipment is occupied |
|LOCAL_VIDEO_STREAM_ERROR_DEVICE_NOT_FOUND |4 |The local video capture device does not exist or has been removed |
|LOCAL_VIDEO_STREAM_ERROR_CAPTURE_FAILURE |5 |Local video capture failed, it is recommended to check whether the acquisition device is working properly |
|LOCAL_VIDEO_STREAM_ERROR_ENCODE_FAILURE |6 |Local video encoding failed |
|LOCAL_VIDEO_STREAM_ERROR_DEVICE_DISCONNECTED |7 |The local video capture device is disconnected. It is occupied by other programs during the call. |


<span id="NetworkQualityStats"></span>
# NetworkQualityStats

```java
public class com.ss.bytertc.engine.type.NetworkQualityStats
```


Tx/Rx network quality

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[uid](https://docs.byteplus.com/en/docs/12/14169#NetworkQualityStats-uid) |
|double |\- |[fractionLost](https://docs.byteplus.com/en/docs/12/14169#NetworkQualityStats-fractionlost) |
|int |\- |[rtt](https://docs.byteplus.com/en/docs/12/14169#NetworkQualityStats-rtt) |
|int |\- |[totalBandwidth](https://docs.byteplus.com/en/docs/12/14169#NetworkQualityStats-totalbandwidth) |
|int |\- |[txQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQualityStats-txquality) |
|int |\- |[rxQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQualityStats-rxquality) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#NetworkQualityStats-tostring) |


<span id="instructions"></span>
## Instructions

<span id="NetworkQualityStats-uid"></span>
### uid

```java
public String com.ss.bytertc.engine.type.NetworkQualityStats.uid
```


User ID

<span id="NetworkQualityStats-fractionlost"></span>
### fractionLost

```java
public double com.ss.bytertc.engine.type.NetworkQualityStats.fractionLost
```


Packet loss ratio of the local client, ranging [0.0,1.0]

For a local user, it is the sent\-packet loss ratio.

For a remote user, it is the loss ratio of all the packets received.

<span id="NetworkQualityStats-rtt"></span>
### rtt

```java
public int com.ss.bytertc.engine.type.NetworkQualityStats.rtt
```


Round\-trip time (RTT) from client to server. Effective for the local user. Unit: ms

<span id="NetworkQualityStats-totalbandwidth"></span>
### totalBandwidth

```java
public int com.ss.bytertc.engine.type.NetworkQualityStats.totalBandwidth
```


Average transmission rate of the media RTP packets in 2s. unit: bps

For a local user, it is the packet\-transmitting speed.

For a remote user, it is the speed of receiving all the subscribed media streams.

<span id="NetworkQualityStats-txquality"></span>
### txQuality

```java
public int com.ss.bytertc.engine.type.NetworkQualityStats.txQuality
```


Tx network quality grade. The higher the grade, the worse the network quality. Refer to [NetworkQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality) for details.

<span id="NetworkQualityStats-rxquality"></span>
### rxQuality

```java
public int com.ss.bytertc.engine.type.NetworkQualityStats.rxQuality
```


Rx network quality grade. The higher the grade, the worse the network quality. Refer to [NetworkQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality) for details.

<span id="instructions"></span>
## Instructions

<span id="NetworkQualityStats-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.type.NetworkQualityStats.toString()
```


<span id="UserVisibilityChangeError"></span>
# UserVisibilityChangeError

```java
public enum com.ss.bytertc.engine.type.UserVisibilityChangeError
```


User visibility state change error.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|OK |0 |Success. |
|UNKNOWN |1 |Unknown error. |
|TOO_MANY_VISIBLE_USER |2 |The number of visible users in the room reaches the upper limit. |


<span id="PublishFallbackOption"></span>
# PublishFallbackOption

```java
public enum com.ss.bytertc.engine.type.PublishFallbackOption
```


Stream fallback options of publisher

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|DISABLE |0 |Default setting. No fallback is allowed under limited network conditions. |
|SIMULCAST_SMALL_VIDEO_ONLY |1 |Under limited network conditions, the video streams that you published will degrade sequentially from the highest\-quality stream to the lowest\-quality stream until they can match current network conditions. See [Stream Fallback](https://docs.byteplus.com/byteplus-rtc/docs/70137) for details. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static PublishFallbackOption |[fromId](https://docs.byteplus.com/en/docs/12/14169#PublishFallbackOption-fromid) |


<span id="instructions"></span>
## Instructions

<span id="PublishFallbackOption-fromid"></span>
### fromId

```java
public static PublishFallbackOption com.ss.bytertc.engine.type.PublishFallbackOption.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="LocalAudioStreamError"></span>
# LocalAudioStreamError

```java
public enum com.ss.bytertc.engine.data.LocalAudioStreamError
```


Error code when the state of the local audio stream changes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|LOCAL_AUDIO_STREAM_ERROR_OK |0 |Local audio status is normal |
|LOCAL_AUDIO_STREAM_ERROR_FAILURE |1 |Local audio error cause unknown |
|LOCAL_AUDIO_STREAM_ERROR_DEVICE_NO_PERMISSION |2 |No permission to start local audio recording device |
|LOCAL_AUDIO_STREAM_ERROR_RECORD_FAILURE |4 |Local audio recording failed, it is recommended that you check whether the recording device is working properly |
|LOCAL_AUDIO_STREAM_ERROR_ENCODE_FAILURE |5 |Local audio encoding failed |
|LOCAL_AUDIO_STREAM_ERROR_NO_RECORDING_DEVICE |6 |No audio recording equipment available |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamError-value) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioStreamError-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.LocalAudioStreamError.value()
```


Get current value

**Return Value**

Current value

<span id="RecordingInfo"></span>
# RecordingInfo

```java
public class com.ss.bytertc.engine.data.RecordingInfo
```


Details of local recording

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[filePath](https://docs.byteplus.com/en/docs/12/14169#RecordingInfo-filepath) |
|VideoCodecType |\- |[videoCodecType](https://docs.byteplus.com/en/docs/12/14169#RecordingInfo-videocodectype) |
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#RecordingInfo-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#RecordingInfo-height) |


<span id="instructions"></span>
## Instructions

<span id="RecordingInfo-filepath"></span>
### filePath

```java
public String com.ss.bytertc.engine.data.RecordingInfo.filePath
```


The absolute path of the recorded file, including the file name and file suffix

<span id="RecordingInfo-videocodectype"></span>
### videoCodecType

```java
public VideoCodecType com.ss.bytertc.engine.data.RecordingInfo.videoCodecType
```


The video encoding type of the recorded file. See see [VideoCodecType](https://docs.byteplus.com/en/docs/12/14169#RecordingInfo-videocodectype)

<span id="RecordingInfo-width"></span>
### width

```java
public int com.ss.bytertc.engine.data.RecordingInfo.width
```


The width of the recorded video, in pixels. Please ignore this field for audio\-only recording

<span id="RecordingInfo-height"></span>
### height

```java
public int com.ss.bytertc.engine.data.RecordingInfo.height
```


The height of the recorded video, the unit: pixels. Please ignore this field for audio\-only recording

<span id="RTCRoomStats"></span>
# RTCRoomStats

```java
public class com.ss.bytertc.engine.type.RTCRoomStats
```


Call related statistics

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[totalDuration](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-totalduration) |
|long |\- |[txBytes](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-txbytes) |
|long |\- |[rxBytes](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rxbytes) |
|int |\- |[txKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-txkbitrate) |
|int |\- |[rxKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rxkbitrate) |
|int |\- |[txAudioKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-txaudiokbitrate) |
|int |\- |[rxAudioKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rxaudiokbitrate) |
|int |\- |[txVideoKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-txvideokbitrate) |
|int |\- |[rxVideoKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rxvideokbitrate) |
|int |\- |[txScreenKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-txscreenkbitrate) |
|int |\- |[rxScreenKBitRate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rxscreenkbitrate) |
|int |\- |[users](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-users) |
|double |\- |[cpuTotalUsage](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-cputotalusage) |
|double |\- |[cpuAppUsage](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-cpuappusage) |
|double |\- |[txLostrate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-txlostrate) |
|double |\- |[rxLostrate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rxlostrate) |
|int |\- |[rtt](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rtt) |
|int |\- |[txCellularKBitrate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-txcellularkbitrate) |
|int |\- |[rxCellularKBitrate](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-rxcellularkbitrate) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[reset](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats-reset) |


<span id="instructions"></span>
## Instructions

<span id="RTCRoomStats-totalduration"></span>
### totalDuration

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.totalDuration
```


The duration, in seconds, that the local user has spent in the room.

<span id="RTCRoomStats-txbytes"></span>
### txBytes

```java
public long com.ss.bytertc.engine.type.RTCRoomStats.txBytes
```


Cumulative data sent by the user in bytes.

<span id="RTCRoomStats-rxbytes"></span>
### rxBytes

```java
public long com.ss.bytertc.engine.type.RTCRoomStats.rxBytes
```


Cumulative data received by the user in bytes.

<span id="RTCRoomStats-txkbitrate"></span>
### txKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.txKBitRate
```


The instantaneous value of Tx bitrate in Kbps

<span id="RTCRoomStats-rxkbitrate"></span>
### rxKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.rxKBitRate
```


The instantaneous value of Rx bitrate in kbps

<span id="RTCRoomStats-txaudiokbitrate"></span>
### txAudioKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.txAudioKBitRate
```


The instantaneous value of audio Tx bitrate in kbps

<span id="RTCRoomStats-rxaudiokbitrate"></span>
### rxAudioKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.rxAudioKBitRate
```


The instantaneous value of audio Rx bitrate in kbps

<span id="RTCRoomStats-txvideokbitrate"></span>
### txVideoKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.txVideoKBitRate
```


The instantaneous value of video Tx bitrate in kbps

<span id="RTCRoomStats-rxvideokbitrate"></span>
### rxVideoKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.rxVideoKBitRate
```


The instantaneous value of video Rx bitrate in kbps

<span id="RTCRoomStats-txscreenkbitrate"></span>
### txScreenKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.txScreenKBitRate
```


The instantaneous TX bitrate of screen\-sharing video in Kbps

<span id="RTCRoomStats-rxscreenkbitrate"></span>
### rxScreenKBitRate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.rxScreenKBitRate
```


The instantaneous RX bitrate of screen\-sharing video in Kbps

<span id="RTCRoomStats-users"></span>
### users

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.users
```


Number of visible users in the current room

<span id="RTCRoomStats-cputotalusage"></span>
### cpuTotalUsage

```java
public double com.ss.bytertc.engine.type.RTCRoomStats.cpuTotalUsage
```


Current CPU usage (%)

<span id="RTCRoomStats-cpuappusage"></span>
### cpuAppUsage

```java
public double com.ss.bytertc.engine.type.RTCRoomStats.cpuAppUsage
```


CPU usage (%) of the application

<span id="RTCRoomStats-txlostrate"></span>
### txLostrate

```java
public double com.ss.bytertc.engine.type.RTCRoomStats.txLostrate
```


Current Tx packet loss rate. The range is [0,1].

<span id="RTCRoomStats-rxlostrate"></span>
### rxLostrate

```java
public double com.ss.bytertc.engine.type.RTCRoomStats.rxLostrate
```


Current Rx packet loss rate. The range is [0,1].

<span id="RTCRoomStats-rtt"></span>
### rtt

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.rtt
```


Round\-trip time (in ms) from client side to server side

<span id="RTCRoomStats-txcellularkbitrate"></span>
### txCellularKBitrate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.txCellularKBitrate
```


Tx cellular bandwidth consumption

<span id="RTCRoomStats-rxcellularkbitrate"></span>
### rxCellularKBitrate

```java
public int com.ss.bytertc.engine.type.RTCRoomStats.rxCellularKBitrate
```


Rx cellular bandwidth consumption

<span id="instructions"></span>
## Instructions

<span id="RTCRoomStats-reset"></span>
### reset

```java
public void com.ss.bytertc.engine.type.RTCRoomStats.reset()
```


Reset [RTCRoomStats](https://docs.byteplus.com/en/docs/12/14169#RTCRoomStats)

<span id="LocalVideoSinkPosition"></span>
# LocalVideoSinkPosition

```java
public enum com.ss.bytertc.engine.video.LocalVideoSinkPosition
```


The position of the local video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AFTER_CAPTURE |0 |After capturing. |
|AFTER_PREPROCESS |1 |(Default) After preprocessing. |


<span id="MixedStreamVideoType"></span>
# MixedStreamVideoType

```java
public enum com.ss.bytertc.engine.live.MixedStreamVideoType
```


Reserved field.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamVideoType |[MixedStreamVideoType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamVideoType-mixedstreamvideotype) |
|int |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamVideoType-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamVideoType-mixedstreamvideotype"></span>
### MixedStreamVideoType

```java
public com.ss.bytertc.engine.live.MixedStreamVideoType.MixedStreamVideoType(int value)
```


Reserved field.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |It defaults to `kMixedStreamVideoTypeMain` indicating the main stream. |


<span id="MixedStreamVideoType-getvalue"></span>
### getValue

```java
public int com.ss.bytertc.engine.live.MixedStreamVideoType.getValue()
```


Reserved field.

<span id="ProblemFeedbackRoomInfo"></span>
# ProblemFeedbackRoomInfo

```java
public class com.ss.bytertc.engine.type.ProblemFeedbackRoomInfo
```


Room info of the video call quality feedback.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#ProblemFeedbackRoomInfo-roomid) |
|String |\- |[userId](https://docs.byteplus.com/en/docs/12/14169#ProblemFeedbackRoomInfo-userid) |


<span id="instructions"></span>
## Instructions

<span id="ProblemFeedbackRoomInfo-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.type.ProblemFeedbackRoomInfo.roomId
```


Room ID.

<span id="ProblemFeedbackRoomInfo-userid"></span>
### userId

```java
public String com.ss.bytertc.engine.type.ProblemFeedbackRoomInfo.userId
```


User ID.

<span id="AudioSourceType"></span>
# AudioSourceType

```java
public enum com.ss.bytertc.engine.data.AudioSourceType
```


Audio input source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_SOURCE_TYPE_EXTERNAL |0 |Custom Capture Audio Source |
|AUDIO_SOURCE_TYPE_INTERNAL |1 |RTC SDK internal acquisition audio source |


<span id="SingleStreamPushType"></span>
# SingleStreamPushType

```java
public enum com.ss.bytertc.engine.live.SingleStreamPushType
```


Single stream push type, specifying whether to push the media stream to CDN or RTC room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SINGLE_STREAM_PUSH_TYPE_TO_CDN |1 |Push to CDN |
|SINGLE_STREAM_PUSH_TYPE_TO_RTC |2 |Push to RTC room |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|SingleStreamPushType |[SingleStreamPushType](https://docs.byteplus.com/en/docs/12/14169#SingleStreamPushType-singlestreampushtype) |


<span id="instructions"></span>
## Instructions

<span id="SingleStreamPushType-singlestreampushtype"></span>
### SingleStreamPushType

```java
public com.ss.bytertc.engine.live.SingleStreamPushType.SingleStreamPushType(int value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |\- |


<span id="PerformanceAlarmMode"></span>
# PerformanceAlarmMode

```java
public enum com.ss.bytertc.engine.type.PerformanceAlarmMode
```


Mode of performance fallback

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|NORMAL |0 |Not enabled Publish performance fallback |
|SIMULCAST |1 |Enable publish performance fallback |


<span id="RoomStateChangeReason"></span>
# RoomStateChangeReason

```java
public enum com.ss.bytertc.engine.type.RoomStateChangeReason
```


Room state change reason.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|JOIN_ROOM |0 |Join room success for the first time. |
|RECONNECT |1 |Rejoin the room, such as the network is reconnected. |
|LEAVE_ROOM |2 |Leave room. |
|JOIN_ROOM_FAILED |\-2001 |Failed to enter the room.<br><br>&nbsp;<br><br>When you enter the room for the first time or disconnect and reconnect due to poor network condition, the room entry failed due to a server error. The SDK automatically retries to join the room. |
|INVALID_TOKEN |\-1000 |Token is invalid.<br><br>&nbsp;<br><br>The token used when entering the room is invalid or expired. The user is required to retrieve the token and call the `updateToken` method to update the token. |
|TOKEN_EXPIRED |\-1009 |Token expired. Call `joinRoom` to rejoin with a valid Token. |
|UPDATE_TOKEN_WITH_INVALID_TOKEN |\-1010 |The Token you provided when calling `updateToken` is invalid. |
|ROOM_FORBIDDEN |\-1025 |The room has been banned before the user calls `joinRoom`. |
|USER_FORBIDDEN |\-1026 |The user has been banned before calling `joinRoom`. |
|KICKED_OUT |\-1006 |The user has been removed from the room by the administrator via an OpenAPI call. |
|ROOM_DISMISS |\-1011 |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. |
|DUPLICATE_LOGIN |\-1004 |The user has been removed from the room because the same user joined the room on another client. |
|STATE_ABNORMAL_SERVER_STATUS |\-1084 |The user has been removed from the room due to the abnormal server status.<br><br>&nbsp;<br><br>SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support. |
|UNKNOWN |\-1001 |Join room error.<br><br>&nbsp;<br><br>An unknown error occurred while entering the room, which caused the joining room to fail. Users are required to rejoin the room. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static RoomStateChangeReason |[valueOf](https://docs.byteplus.com/en/docs/12/14169#RoomStateChangeReason-valueof) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|RoomStateChangeReason |[RoomStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RoomStateChangeReason-roomstatechangereason) |
|int |[value](https://docs.byteplus.com/en/docs/12/14169#RoomStateChangeReason-value) |


<span id="instructions"></span>
## Instructions

<span id="RoomStateChangeReason-valueof"></span>
### valueOf

```java
public static RoomStateChangeReason com.ss.bytertc.engine.type.RoomStateChangeReason.valueOf(int value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |\- |


<span id="RoomStateChangeReason-roomstatechangereason"></span>
### RoomStateChangeReason

```java
public com.ss.bytertc.engine.type.RoomStateChangeReason.RoomStateChangeReason(int value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |\- |


<span id="RoomStateChangeReason-value"></span>
### value

```java
public int com.ss.bytertc.engine.type.RoomStateChangeReason.value()
```


<span id="EarMonitorAudioFilter"></span>
# EarMonitorAudioFilter

```java
public enum com.ss.bytertc.engine.data.EarMonitorAudioFilter
```


Whether to include the local audio filters in the in\-ear monitoring.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|NONE |1 |No audio processing. |
|REUSE_AUDIO_PROCESSING |32768 |Audio processed by your processor or the SDK built\-in audio processor, such as 3A, voice changer, and reverb. |


<span id="VideoSinkMirrorType"></span>
# VideoSinkMirrorType

```java
public enum com.ss.bytertc.engine.video.VideoSinkMirrorType
```


Whether the video frame needs to be mirrored.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ON |1 |Enable mirroring effect. |
|OFF |2 |(Default) No mirroring effect. |


<span id="RecordingErrorCode"></span>
# RecordingErrorCode

```java
public enum com.ss.bytertc.engine.type.RecordingErrorCode
```


Error code for local recording

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RECORDING_ERROR_CODE_OK |0 |Recording normal |
|RECORDING_ERROR_CODE_NO_PERMISSION |\-1 |No file write permissions |
|RECORDING_ERROR_CODE_NOT_SUPPORT |\-2 |The current version SDK does not support local recording, please contact technical support |
|RECORDING_ERROR_CODE_NO_OTHER |\-3 |Other anomalies |


<span id="EchoTestResult"></span>
# EchoTestResult

```java
public enum com.ss.bytertc.engine.type.EchoTestResult
```


Call test result

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ECHO_TEST_SUCCESS |0 |The playback of captured audio/video is received, test succeeds. |
|ECHO_TEST_TIMEOUT |1 |Test is not completed after 60 seconds and has been stopped automatically. |
|ECHO_TEST_INTERVAL_SHORT |2 |Less than 5s between the end of the last test and the start of the next test. |
|ECHO_TEST_AUDIO_DEVICE_ERROR |3 |Audio capture error |
|ECHO_TEST_VIDEO_DEVICE_ERROR |4 |Video capture error |
|ECHO_TEST_AUDIO_RECEIVE_ERROR |5 |Audio reception error |
|ECHO_TEST_VIDEO_RECEIVE_ERROR |6 |Video reception error |
|ECHO_TEST_INTERNAL_ERROR |7 |Unrecoverable internal error |


<span id="NetworkTimeInfo"></span>
# NetworkTimeInfo

```java
public class com.ss.bytertc.engine.NetworkTimeInfo
```


network time info

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|long |\- |[timestamp](https://docs.byteplus.com/en/docs/12/14169#NetworkTimeInfo-timestamp) |


<span id="instructions"></span>
## Instructions

<span id="NetworkTimeInfo-timestamp"></span>
### timestamp

```java
public long com.ss.bytertc.engine.NetworkTimeInfo.timestamp
```


Network time. Unit: ms

<span id="RoomEventInfo"></span>
# RoomEventInfo

```java
public class com.ss.bytertc.engine.type.RoomEventInfo
```


Room event info.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|long |0 |[forbiddenTime](https://docs.byteplus.com/en/docs/12/14169#RoomEventInfo-forbiddentime) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|RoomEventInfo |[RoomEventInfo](https://docs.byteplus.com/en/docs/12/14169#RoomEventInfo-roomeventinfo) |


<span id="instructions"></span>
## Instructions

<span id="RoomEventInfo-forbiddentime"></span>
### forbiddenTime

```java
public long com.ss.bytertc.engine.type.RoomEventInfo.forbiddenTime = 0
```


When the room or user is forbidden, notice forbidden time via onRoomEvent.

<span id="instructions"></span>
## Instructions

<span id="RoomEventInfo-roomeventinfo"></span>
### RoomEventInfo

```java
public com.ss.bytertc.engine.type.RoomEventInfo.RoomEventInfo(InternalRoomEventInfo info)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|info |InternalRoomEventInfo |\- |


<span id="MixedStreamTaskInfo"></span>
# MixedStreamTaskInfo

```java
public class com.ss.bytertc.engine.live.MixedStreamTaskInfo
```


Detailed information of the stream mixing task.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamTaskInfo |[setTargetType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamTaskInfo-settargettype) |
|MixedStreamPushTargetType |[getTargetType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamTaskInfo-gettargettype) |
|MixedStreamTaskInfo |[setTaskId](https://docs.byteplus.com/en/docs/12/14169#MixedStreamTaskInfo-settaskid) |
|String |[getTaskId](https://docs.byteplus.com/en/docs/12/14169#MixedStreamTaskInfo-gettaskid) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamTaskInfo-settargettype"></span>
### setTargetType

```java
public MixedStreamTaskInfo com.ss.bytertc.engine.live.MixedStreamTaskInfo.setTargetType(MixedStreamPushTargetType targetType)
```


Task type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|targetType |MixedStreamPushTargetType |Pushing a mixing stream to CDN or starting a WTN stream. |


<span id="MixedStreamTaskInfo-gettargettype"></span>
### getTargetType

```java
public MixedStreamPushTargetType com.ss.bytertc.engine.live.MixedStreamTaskInfo.getTargetType()
```


Task type: Pushing a mixing stream to CDN or starting a WTN stream.

<span id="MixedStreamTaskInfo-settaskid"></span>
### setTaskId

```java
public MixedStreamTaskInfo com.ss.bytertc.engine.live.MixedStreamTaskInfo.setTaskId(String taskId)
```


Set task ID

For WTN stream task, this value represents the WTN stream ID. You can subscribe to a WTN stream by specifying the ID.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|taskId |String |Task ID |


<span id="MixedStreamTaskInfo-gettaskid"></span>
### getTaskId

```java
public String com.ss.bytertc.engine.live.MixedStreamTaskInfo.getTaskId()
```


Task ID

For WTN stream task, this value represents the WTN stream ID. You can subscribe to a WTN stream by specifying the ID.

<span id="RemoteMirrorType"></span>
# RemoteMirrorType

```java
public enum com.ss.bytertc.engine.data.RemoteMirrorType
```


Mirroring type for remote stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|NONE |0 |(Default) No mirroring effect. |
|RENDER |1 |Enable mirroring effect. |


<span id="VirtualBackgroundSource"></span>
# VirtualBackgroundSource

```java
public class com.ss.bytertc.engine.data.VirtualBackgroundSource
```


Virtual background source.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|VirtualBackgroundSourceType |\- |[sourceType](https://docs.byteplus.com/en/docs/12/14169#VirtualBackgroundSource-sourcetype) |
|int |\- |[sourceColor](https://docs.byteplus.com/en/docs/12/14169#VirtualBackgroundSource-sourcecolor) |
|String |\- |[sourcePath](https://docs.byteplus.com/en/docs/12/14169#VirtualBackgroundSource-sourcepath) |


<span id="instructions"></span>
## Instructions

<span id="VirtualBackgroundSource-sourcetype"></span>
### sourceType

```java
public VirtualBackgroundSourceType com.ss.bytertc.engine.data.VirtualBackgroundSource.sourceType
```


See [VirtualBackgroundSourceType](https://docs.byteplus.com/en/docs/12/14169#VirtualBackgroundSourceType).

<span id="VirtualBackgroundSource-sourcecolor"></span>
### sourceColor

```java
public int com.ss.bytertc.engine.data.VirtualBackgroundSource.sourceColor
```


The solid color of the background.

The format is 0xAARRGGBB.

<span id="VirtualBackgroundSource-sourcepath"></span>
### sourcePath

```java
public String com.ss.bytertc.engine.data.VirtualBackgroundSource.sourcePath
```


The absolute path of the specified image.


* You can use the absolute path of the local file (file://xxx) and the Asset path (asset://xxx).

* You can upload a .JPG, .PNG, or .JPEG file.

* The image with a resolution higher than 1080p(Full HD) will be rescaled proportionally to fit in the video.

* If the image's aspect ratio matches the video's, the image will be rescaled proportionally to fit in the video.

* If the image’s aspect ratio does not match the video's, the shortest side (either height or width) of the image will be stretched proportionally to match the video. Then the image will be cropped to fill in the video.

* The transparent area in the image will be filled with black.

    &nbsp;


<span id="streamindex"></span>
# StreamIndex

```java
public enum com.ss.bytertc.engine.data.StreamIndex
```


Reserved field.

<span id="RemoteAudioStateChangeReason"></span>
# RemoteAudioStateChangeReason

```java
public enum com.ss.bytertc.engine.data.RemoteAudioStateChangeReason
```


The cause of the remote audio stream state change.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|REMOTE_AUDIO_STATE_CHANGE_REASON_INTERNAL |0 |Internal reasons |
|REMOTE_AUDIO_STATE_CHANGE_REASON_NETWORK_CONGESTION |1 |Network blocking |
|REMOTE_AUDIO_STATE_CHANGE_REASON_NETWORK_RECOVERY |2 |Network back to normal |
|REMOTE_AUDIO_STATE_CHANGE_REASON_LOCAL_MUTED |3 |Local user stops receiving remote audio stream |
|REMOTE_AUDIO_STATE_CHANGE_REASON_LOCAL_UNMUTED |4 |Local users resume receiving remote audio streams |
|REMOTE_AUDIO_STATE_CHANGE_REASON_REMOTE_MUTED |5 |Remote user stops sending audio stream |
|REMOTE_AUDIO_STATE_CHANGE_REASON_REMOTE_UNMUTED |6 |Remote user resumes sending audio stream |
|REMOTE_AUDIO_STATE_CHANGE_REASON_REMOTE_OFFLINE |7 |Remote user leaves room |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason-value) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioStateChangeReason-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.RemoteAudioStateChangeReason.value()
```


Get current value

**Return Value**

Current value

<span id="PlayerError"></span>
# PlayerError

```java
public enum com.ss.bytertc.engine.data.PlayerError
```


Error code for audio playback.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|OK |0 |OK |
|FORMAT_NOT_SUPPORT |1 |Format not supported. |
|INVALID_PATH |2 |Invalid file path. |
|INVALID_STATE |3 |The prerequisite is not met. Check the specific API doc. |
|INVALID_POSITION |4 |Invalid position. |
|INVALID_VOLUME |5 |Invalid volume. |
|INVALID_PITCH |6 |Invalid pitch value. |
|INVALID_AUDIO_TRACK_INDEX |7 |Invalid audio track. |
|INVALID_PLAYBACK_SPEED |8 |Invalid playback speed. |
|INVALID_EFFECT_ID |9 |Invalid effect ID. Receive this error code when you call other APIs before the audio file is preloaded or opened. |
|ERROR_CURRENTLY_PLAYING |10 |The resource is currently playing. |


<span id="ReturnStatus"></span>
# ReturnStatus

```java
public enum com.ss.bytertc.engine.data.ReturnStatus
```


API call result.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RETURN_STATUS_SUCCESS |0 |Success. |
|RETURN_STATUS_FAILURE |\-1 |Failure. |
|RETURN_STATUS_PARAMETER_ERR |\-2 |Invalid parameter. |
|RETURN_STATUS_WRONG_STATE |\-3 |API status error. |
|RETURN_STATUS_HAS_IN_ROOM |\-4 |Failure. The user is already in the room. |
|RETURN_STATUS_HAS_IN_LOGIN |\-5 |Failure. The user has already logged in. |
|RETURN_STATUS_HAS_IN_ECHO_TEST |\-6 |Failure. The user is already in a pre\-call test. |
|RETURN_STATUS_NEITHER_VIDEO_NOR_AUDIO |\-7 |Failure. Neither video nor audio is captured. |
|RETURN_STATUS_ROOMID_IN_USE |\-8 |Failure. The roomId is already in use. |
|RETURN_STATUS_SCREEN_NOT_SUPPORT |\-9 |Failure. Screen stream is not supported. |
|RETURN_STATUS_NOT_SUPPORT |\-10 |Failure. Not supported. |
|RETURN_STATUS_RESOURCE_OVERFLOW |\-11 |Failure. Resource overflow. |
|RETURN_STATUS_VIDEO_NOT_SUPPORT |\-12 |Failure. Not supported. |
|RETURN_STATUS_AUDIO_NO_FRAME |\-101 |Failure. No audio frame. |
|RETURN_STATUS_AUDIO_NOT_IMPLEMENTED |\-102 |Failure. Not implemented. |
|RETURN_STATUS_AUDIO_NO_PERMISSION |\-103 |Failure. The audio capture device does not have microphone use permission, and the initialization of the device failed. |
|RETURN_STATUS_AUDIO_DEVICE_NOT_EXISTS |\-104 |Failure. The device does not exist. This value is returned if there is currently no device or if the device has been removed. |
|RETURN_STATUS_AUDIO_DEVICE_FORMAT_NOT_SUPPORT |\-105 |Failure. The device audio format is not supported. |
|RETURN_STATUS_AUDIO_DEVICE_NO_DEVICE |\-106 |Failure. No device in system. |
|RETURN_STATUS_AUDIO_DEVICE_CAN_NOT_USE |\-107 |Failure. The current device is not available and needs to be replaced. |
|RETURN_STATUS_AUDIO_DEVICE_INIT_FAILED |\-108 |Device initialization failed due to a system error. |
|RETURN_STATUS_AUDIO_DEVICE_START_FAILED |\-109 |Device start\-up failed due to a system error. |
|RETURN_STATUS_AUDIO_DEVICE_PROCESS_NOT_EXIST |\-110 |Sharing process audio failed because the process does not exist. |
|RETURN_STATUS_NATIVE_IN_VALID |\-201 |Failure. The native layer is not initialized and the engine is invalid. |
|RETURN_STATUS_VIDEO_TIMESTAMP_WARNING |\-202 |Warning. When pushing a video frame to the RTC SDK, the timing difference of subsequent video frames should be the same as the interval of the frame push operation. If not, you will receive this warning. |


<span id="MediaPlayerConfig"></span>
# MediaPlayerConfig

```java
public class com.ss.bytertc.engine.data.MediaPlayerConfig
```


Mixing configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|AudioMixingType |AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH |[type](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerConfig-type) |
|int |1 |[playCount](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerConfig-playcount) |
|int |0 |[startPos](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerConfig-startpos) |
|long |0 |[callbackOnProgressInterval](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerConfig-callbackonprogressinterval) |
|boolean |false |[syncProgressToRecordFrame](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerConfig-syncprogresstorecordframe) |
|boolean |true |[autoPlay](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerConfig-autoplay) |


<span id="instructions"></span>
## Instructions

<span id="MediaPlayerConfig-type"></span>
### type

```java
public AudioMixingType com.ss.bytertc.engine.data.MediaPlayerConfig.type = AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH
```


For mixing playback types. See [AudioMixingType](https://docs.byteplus.com/en/docs/12/14169#AudioMixingType)

<span id="MediaPlayerConfig-playcount"></span>
### playCount

```java
public int com.ss.bytertc.engine.data.MediaPlayerConfig.playCount = 1
```


Mix playback times


* Play_count < = 0: Infinite loop

* Play_count == 1: Play once (default)

* Play_count \> 1: Play play_count times

    &nbsp;


<span id="startpos"></span>
### startPos

```java
public int com.ss.bytertc.engine.data.MediaPlayerConfig.startPos = 0
```


The starting position in ms. 0 by default.

<span id="MediaPlayerConfig-callbackonprogressinterval"></span>
### callbackOnProgressInterval

```java
public long com.ss.bytertc.engine.data.MediaPlayerConfig.callbackOnProgressInterval = 0
```


Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing in ms.


* interval \> 0: The callback is enabled. The actual interval is `10*(mod(10)+1)`.

* interval <= 0: The callback is disabled.

    &nbsp;


<span id="syncprogresstorecordframe"></span>
### syncProgressToRecordFrame

```java
public boolean com.ss.bytertc.engine.data.MediaPlayerConfig.syncProgressToRecordFrame = false
```


Attach the process information of local audio file mixing to the captured audio data. Enable the function to enhance the synchronicity of the remote audio mixing.


* The function is effective when mixing a single audio file.

* Use `true` for enabling the function and `false` for disabling the function. The default is `false`.

    &nbsp;


<span id="autoplay"></span>
### autoPlay

```java
public boolean com.ss.bytertc.engine.data.MediaPlayerConfig.autoPlay = true
```


Play the audio automatically. If not, call [start](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-start) to play the audio.

<span id="VideoPictureType"></span>
# VideoPictureType

```java
public enum com.ss.bytertc.engine.data.VideoPictureType
```


Video compression picture type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VIDEO_PICTURE_TYPE_UNKNOWN |0 |Unknown type |
|VIDEO_PICTURE_TYPE_I |1 |I\-frames, key frames which are coded without reference to any other frame. |
|VIDEO_PICTURE_TYPE_P |2 |P\-frames, forward\-predicted frames which are coded by a forward predictive coding method. |
|VIDEO_PICTURE_TYPE_B |3 |B\-frames, bi\-directionally predicted frames which are coded by both forward and backward predictive coding method. |


<span id="ColorSpace"></span>
# ColorSpace

```java
public enum com.ss.bytertc.engine.data.ColorSpace
```


Color space of the video frame

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|UNKNOWN |0 |Unknown color space |
|BT601_LIMITED_RANGE |1 |BT.601 standard, color space values range from 16 to 235 |
|BT601_FULL_RANGE |2 |BT.601 standard, color space values range from 0 to 255 |
|BT709_LIMITED_RANGE |3 |BT.7091 standard, color space values range from 16 to 235 |
|BT709_FULL_RANGE |4 |BT.7091 standard, color space values range from 0 to 255 |


<span id="AudioPropertiesInfo"></span>
# AudioPropertiesInfo

```java
public class com.ss.bytertc.engine.data.AudioPropertiesInfo
```


Audio properties

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[linearVolume](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesInfo-linearvolume) |
|int |\- |[nonlinearVolume](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesInfo-nonlinearvolume) |
|float[] |new float[SPECTRUM_SIZE] |[spectrum](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesInfo-spectrum) |
|int |\- |[vad](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesInfo-vad) |
|double |0 |[voicePitch](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesInfo-voicepitch) |


<span id="instructions"></span>
## Instructions

<span id="AudioPropertiesInfo-linearvolume"></span>
### linearVolume

```java
public int com.ss.bytertc.engine.data.AudioPropertiesInfo.linearVolume
```


linear volume. The value is in linear relation to the original volume. The higher the value, the higher the volume. The range is [0,255].


* [0, 25]: Nearly silence

* [26, 75]: Low volume

* [76, 204]: Medium volume

* [205, 255]: High volume

    &nbsp;


<span id="nonlinearvolume"></span>
### nonlinearVolume

```java
public int com.ss.bytertc.engine.data.AudioPropertiesInfo.nonlinearVolume
```


non\-linear volume in dB. The value is in proportion to the log value of the original volume. You can use the value to recognize the Active Speaker in the room. The range is [\-127, 0].


* [\-127, \-60]: Nearly silence

* [\-59, \-40]: Low volume

* [\-39, \-20]: Medium volume

* [\-19, 0]: High volume

    &nbsp;


<span id="spectrum"></span>
### spectrum

```java
public float [] com.ss.bytertc.engine.data.AudioPropertiesInfo.spectrum = new float[SPECTRUM_SIZE]
```


Spectrum array

<span id="AudioPropertiesInfo-vad"></span>
### vad

```java
public int com.ss.bytertc.engine.data.AudioPropertiesInfo.vad
```


Voice Activity Detection (VAD) result


* 1: Voice activity detected.

* 0: No voice activity detected.

* \-1: VAD not activated.

    &nbsp;


<span id="voicepitch"></span>
### voicePitch

```java
public double com.ss.bytertc.engine.data.AudioPropertiesInfo.voicePitch = 0
```


The vocal pitch of the local user, in Hertz.

When the following two conditions are met at the same time, the vocal pitch of the local user will be returned:


* Calls [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport), and sets the value of enableVoicePitch to `true`.

* The local user's voice is included in the locally captured audio data.

   In other situations, `0` will be returned.

    &nbsp;


<span id="remotevideostate"></span>
# RemoteVideoState

```java
public enum com.ss.bytertc.engine.type.RemoteVideoState
```


Remote video stream status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|REMOTE_VIDEO_STATE_STOPPED |0 |The default initial state of the remote video stream<br><br>&nbsp;<br><br>The state is called back at the following times:<br><br><br>&nbsp;<br><br>* Local users stop receiving the remote video stream, corresponding to the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason) REMOTE_VIDEO_STATE_CHANGE_REASON_LOCAL_MUTED.<br><br>* The remote user stops sending the video stream, corresponding to the REMOTE_VIDEO_STATE_CHANGE_REASON_REMOTE_MUTED in the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason).<br><br>* The remote user leaves the room, corresponding to the REMOTE_VIDEO_STATE_CHANGE_REASON_REMOTE_OFFLINE in the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason). |
|REMOTE_VIDEO_STATE_STARTING |1 |Local users have received the remote video header packet<br><br>&nbsp;<br><br>Callback this state when the remote video header packet is received, corresponding to the REMOTE_VIDEO_STATE_CHANGE_REASON_LOCAL_UNMUTED in the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason). |
|REMOTE_VIDEO_STATE_DECODING |2 |The remote video stream is decoding, normal playback<br><br>&nbsp;<br><br>Callback this state at the following times:<br><br><br>&nbsp;<br><br>* Successfully decoded the remote video first frame, corresponding to the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason) REMOTE_VIDEO_STATE_CHANGE_REASON_LOCAL_UNMUTED.<br><br>* The network returned to normal from blocking, corresponding to the REMOTE_VIDEO_STATE_CHANGE_REASON_NETWORK_RECOVERY in the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason).<br><br>* Local users resume receiving remote video streams, corresponding to the REMOTE_VIDEO_STATE_CHANGE_REASON_LOCAL_UNMUTED in the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason).<br><br>* The remote user resumes sending the video stream, corresponding to the REMOTE_VIDEO_STATE_CHANGE_REASON_NETWORK_CONGESTION in the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason). |
|REMOTE_VIDEO_STATE_FROZEN |3 |The remote video stream stalls<br><br>&nbsp;<br><br>Callback this state when the network is blocked and the packet loss rate is greater than 40%, corresponding to the REMOTE_VIDEO_REASON_NETWORK_CONGESTION in the error code [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStateChangeReason). |


<span id="VideoEncoderConfiguration"></span>
# VideoEncoderConfiguration

```java
public class com.ss.bytertc.engine.video.VideoEncoderConfiguration
```


Video encoding configuration. Refer to [Setting Video Encoder Configuration](https://docs.byteplus.com/byteplus-rtc/docs/70122) to learn more.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|VideoDimensions |\- |[dimensions](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfiguration-dimensions) |
|FrameRate |\- |[frameRate](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfiguration-framerate) |
|int |\- |[kBitrate](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfiguration-kbitrate) |
|int |\- |[kMinBitrate](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfiguration-kminbitrate) |
|OrientationMode |\- |[orientationMode](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfiguration-orientationmode) |


<span id="instructions"></span>
## Instructions

<span id="VideoEncoderConfiguration-dimensions"></span>
### dimensions

```java
public VideoDimensions com.ss.bytertc.engine.video.VideoEncoderConfiguration.dimensions
```


Video coded pixel

<span id="VideoEncoderConfiguration-framerate"></span>
### frameRate

```java
public FrameRate com.ss.bytertc.engine.video.VideoEncoderConfiguration.frameRate
```


Video coding frame rate

<span id="VideoEncoderConfiguration-kbitrate"></span>
### kBitrate

```java
public int com.ss.bytertc.engine.video.VideoEncoderConfiguration.kBitrate
```


Video coding rate

<span id="VideoEncoderConfiguration-kminbitrate"></span>
### kMinBitrate

```java
public int com.ss.bytertc.engine.video.VideoEncoderConfiguration.kMinBitrate
```


<span id="VideoEncoderConfiguration-orientationmode"></span>
### orientationMode

```java
public OrientationMode com.ss.bytertc.engine.video.VideoEncoderConfiguration.orientationMode
```


Video coding direction mode

<span id="PixelFormat"></span>
# PixelFormat

```java
public interface com.ss.bytertc.engine.video.IVideoSink.PixelFormat
```


Video frame data format

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[Original](https://docs.byteplus.com/en/docs/12/14169#PixelFormat-original) |
|int |1 |[I420](https://docs.byteplus.com/en/docs/12/14169#PixelFormat-i420) |
|int |5 |[RGBA](https://docs.byteplus.com/en/docs/12/14169#PixelFormat-rgba) |


<span id="instructions"></span>
## Instructions

<span id="PixelFormat-original"></span>
### Original

```java
public int com.ss.bytertc.engine.video.IVideoSink.PixelFormat.Original = 0
```


Original video frame format

<span id="PixelFormat-i420"></span>
### I420

```java
public int com.ss.bytertc.engine.video.IVideoSink.PixelFormat.I420 = 1
```


I420

<span id="PixelFormat-rgba"></span>
### RGBA

```java
public int com.ss.bytertc.engine.video.IVideoSink.PixelFormat.RGBA = 5
```


RGBA format

<span id="HardwareEchoDetectionResult"></span>
# HardwareEchoDetectionResult

```java
public enum com.ss.bytertc.engine.type.HardwareEchoDetectionResult
```


Result of the detection inited before joining a room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|HARDWARE_ECHO_RESULT_CANCELED |0 |Detection is stopped by the call of `stopHardwareEchoDetection` before the SDK reports the detection result. |
|HARDWARE_ECHO_RESULT_UNKNOWN |1 |Unknown state<br><br>&nbsp;<br><br>Contact us if you retry several times but keep failing. |
|HARDWARE_ECHO_RESULT_NORMAL |2 |Excellent<br><br>&nbsp;<br><br>No echo issue is detected. |
|HARDWARE_ECHO_RESULT_POOR |3 |Echo<br><br>&nbsp;<br><br>Echo issue is detected. Recommend the user join the call with a headset through the interface. |


<span id="SubscribeVideoConfig"></span>
# SubscribeVideoConfig

```java
public class com.ss.bytertc.engine.SubscribeVideoConfig
```


Video subscription configuration information

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|SubscribeVideoConfig |[SubscribeVideoConfig](https://docs.byteplus.com/en/docs/12/14169#SubscribeVideoConfig-subscribevideoconfig) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeVideoConfig-subscribevideoconfig"></span>
### SubscribeVideoConfig

```java
public com.ss.bytertc.engine.SubscribeVideoConfig.SubscribeVideoConfig(
    int videoIndex,
    int priority
)
```


Subscription configuration of video streams

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoIndex |int |The label of subscribed video stream with different resolution.<br><br>&nbsp;<br><br>In Simulcast mode, use a number to specify the expected quality of the video stream to be subscribed to. In Simulcast mode, a video has multiple encoded qualities ranging from 0 to 3. Call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideoencoderconfig) to enable Simulcast mode on the publisher's clients.<br><br>&nbsp;<br><br>Ranging from \-1 to 3<br><br>&nbsp;<br><br>0 (Default): The best quality<br><br>&nbsp;<br><br>\-1: Use the previous settings. |
|priority |int |Remote user priority. The default value is 0. Refer to [RemoteUserPriority](https://docs.byteplus.com/en/docs/12/14169#RemoteUserPriority) for more details. |


<span id="RecordingState"></span>
# RecordingState

```java
public enum com.ss.bytertc.engine.type.RecordingState
```


Status of local recording

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RECORDING_STATE_ERROE |0 |Recording exception |
|RECORDING_STATE_PROCESSING |1 |Recording in progress |
|RECORDING_STATE_SUCCESS |2 |If the recording file is saved successfully. Normal call to stopFileRecording triggers this status code. If the encoding resolution changes during the recording, the SDK will automatically end the current file save and trigger this status code, followed by a new round of recording, until stopFileRecording is called. |


<span id="NetworkDetectionLinkType"></span>
# NetworkDetectionLinkType

```java
public enum com.ss.bytertc.engine.type.NetworkDetectionLinkType
```


Type of probe link before call.

`onNetworkDetectionResult` parameter type for callback

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|UP |0 |Uplink network sounding |
|DOWN |1 |Downlink network detection |


<span id="ByteWatermark"></span>
# ByteWatermark

```java
public class com.ss.bytertc.engine.video.ByteWatermark
```


Watermark's scaled coordinates and size, relative to the video stream.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |\- |[x](https://docs.byteplus.com/en/docs/12/14169#ByteWatermark-x) |
|float |\- |[y](https://docs.byteplus.com/en/docs/12/14169#ByteWatermark-y) |
|float |\- |[width](https://docs.byteplus.com/en/docs/12/14169#ByteWatermark-width) |
|float |\- |[height](https://docs.byteplus.com/en/docs/12/14169#ByteWatermark-height) |


<span id="instructions"></span>
## Instructions

<span id="ByteWatermark-x"></span>
### x

```java
public float com.ss.bytertc.engine.video.ByteWatermark.x
```


The watermark's horizontal offset from the upper left corner of the video stream to the video stream's width in the range of [0,1).

<span id="ByteWatermark-y"></span>
### y

```java
public float com.ss.bytertc.engine.video.ByteWatermark.y
```


The watermark's vertical offset from the upper left corner of the video stream to the video stream's height in the range of [0,1).

<span id="ByteWatermark-width"></span>
### width

```java
public float com.ss.bytertc.engine.video.ByteWatermark.width
```


The watermark's width to the video stream's width in the range of [0,1).

<span id="ByteWatermark-height"></span>
### height

```java
public float com.ss.bytertc.engine.video.ByteWatermark.height
```


The watermark height to the video stream's height in the range of [0,1).

<span id="AudioDeviceType"></span>
# AudioDeviceType

```java
public enum com.ss.bytertc.engine.type.AudioDeviceType
```


Type of audio device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_DEVICE_TYPE_UNKNOWN |\-1 |Unknown device |
|AUDIO_DEVICE_TYPE_RENDER_DEVICE |0 |Speaker or headphone |
|AUDIO_DEVICE_TYPE_CAPTURE_DEVICE |1 |Audio Capturing Device Type |
|AUDIO_DEVICE_TYPE_SCREEN_CAPTURE_DEVICE |2 |Screen capturing audio device |


<span id="SetRoomExtraInfoResult"></span>
# SetRoomExtraInfoResult

```java
public enum com.ss.bytertc.engine.type.SetRoomExtraInfoResult
```


Extra information setting result.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SUCCESS |0 |Success. |
|NOT_JOIN_ROOM |\-1 |Failure. You are not in the room. |
|KEY_IS_NULL |\-2 |Failure. The key pointer is null. |
|VALUE_IS_NULL |\-3 |Failure. The value pointer is null. |
|UNKNOW |\-99 |Failure. Unknown error. |
|KEY_IS_EMPTY |\-400 |Failure. The key length is 0. |
|TOO_OFTEN |\-406 |Failure. Excessively frequent setting. 10 times per second is preferable. |
|SILENT_USER |\-412 |Failure. Invisible users are not allowed to call `setRoomExtraInfo`. |
|KEY_TOO_LONG |\-413 |Failure. Key length exceeds 10 bytes. |
|VALUE_TOO_LONG |\-414 |Failure. Value length exceeds 128 bytes. |
|SERVER_ERROR |\-500 |Failure. Server error. |


<span id="LocalProxyState"></span>
# LocalProxyState

```java
public enum com.ss.bytertc.engine.type.LocalProxyState
```


The states of local proxy connection.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|INITED |0 |TCP proxy server is connected. |
|CONNECTED |1 |The local proxy is connected. |
|ERROR |2 |Errors occurred when connecting to the local proxy. |


<span id="AVSyncState"></span>
# AVSyncState

```java
public enum com.ss.bytertc.engine.data.AVSyncState
```


A/V synchronization states

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AV_SYNC_STATE_STREAM_SYNC_BEGIN |0 |A/V synchronization begins. |
|AV_SYNC_STATE_AUDIO_STREAM_REMOVE |1 |The publisher stops publishing the video stream during the synchronization, which does not affect the sync relationship. |
|AV_SYNC_STATE_VIDEO_STREAM_REMOVE |2 |The publisher stops publishing the video stream during the synchronization, which does not affect the sync relationship. |


<span id="RTCRoomConfig"></span>
# RTCRoomConfig

```java
public class com.ss.bytertc.engine.RTCRoomConfig
```


Room configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|ChannelProfile |\- |[profile](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-profile) |
|LiveMode |\- |[liveMode](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-livemode) |
|String |\- |[streamId](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-streamid) |
|boolean |\- |[isPublishAudio](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-ispublishaudio) |
|boolean |\- |[isPublishVideo](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-ispublishvideo) |
|boolean |\- |[isAutoSubscribeAudio](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-isautosubscribeaudio) |
|boolean |\- |[isAutoSubscribeVideo](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-isautosubscribevideo) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|RTCRoomConfig |[RTCRoomConfig](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-rtcroomconfig-2) |
|int |[getLiveMode](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-getlivemode) |
|boolean |[isPublishAudio](https://docs.byteplus.com/en/docs/12/14169#RTCRoomConfig-ispublishaudio-2) |


<span id="instructions"></span>
## Instructions

<span id="RTCRoomConfig-profile"></span>
### profile

```java
public ChannelProfile com.ss.bytertc.engine.RTCRoomConfig.profile
```


Room profile. See [ChannelProfile](https://docs.byteplus.com/en/docs/12/14169#ChannelProfile). The default is `CHANNEL_PROFILE_COMMUNICATION`. The setting cannot be changed after joining the room.

<span id="RTCRoomConfig-livemode"></span>
### liveMode

```java
public LiveMode com.ss.bytertc.engine.RTCRoomConfig.liveMode
```


Live mode. See [LiveMode](https://docs.byteplus.com/en/docs/12/14169#LiveMode). The default is `LIVE_MODE_CO_HOST`. The setting can be changed after joining the room.

<span id="RTCRoomConfig-streamid"></span>
### streamId

```java
public String com.ss.bytertc.engine.RTCRoomConfig.streamId
```


Stream ID. The setting cannot be changed after joining the room.

<span id="RTCRoomConfig-ispublishaudio"></span>
### isPublishAudio

```java
public boolean com.ss.bytertc.engine.RTCRoomConfig.isPublishAudio
```


Whether to publish media streams automatically. The default is automatic publishing.


* Changing the user role to audience via `setUserVisibility` will void this setting.

* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only.

    &nbsp;


<span id="ispublishvideo"></span>
### isPublishVideo

```java
public boolean com.ss.bytertc.engine.RTCRoomConfig.isPublishVideo
```


Whether to publish media streams automatically. The default is automatic publishing.


* Changing the user role to audience via `setUserVisibility` will void this setting.

* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only.

    &nbsp;


<span id="isautosubscribeaudio"></span>
### isAutoSubscribeAudio

```java
public boolean com.ss.bytertc.engine.RTCRoomConfig.isAutoSubscribeAudio
```


Whether to automatically subscribe to the audio stream. The default is automatic subscription.

This setting affects both the main stream and the screen\-sharing stream.

<span id="RTCRoomConfig-isautosubscribevideo"></span>
### isAutoSubscribeVideo

```java
public boolean com.ss.bytertc.engine.RTCRoomConfig.isAutoSubscribeVideo
```


Whether to automatically subscribe to the main video stream. The default is automatic subscription.

This setting affects both the main stream and the screen\-sharing stream.

<span id="instructions"></span>
## Instructions

<span id="RTCRoomConfig-rtcroomconfig-2"></span>
### RTCRoomConfig

```java
public com.ss.bytertc.engine.RTCRoomConfig.RTCRoomConfig(
    ChannelProfile channelProfile,
    String streamId,
    boolean isPublishAudio,
    boolean isPublishVideo,
    boolean isAutoSubscribeAudio,
    boolean isAutoSubscribeVideo
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|channelProfile |ChannelProfile |\- |
|streamId |String |\- |
|isPublishAudio |boolean |\- |
|isPublishVideo |boolean |\- |
|isAutoSubscribeAudio |boolean |\- |
|isAutoSubscribeVideo |boolean |\- |


<span id="RTCRoomConfig-getlivemode"></span>
### getLiveMode

```java
public int com.ss.bytertc.engine.RTCRoomConfig.getLiveMode()
```


<span id="RTCRoomConfig-ispublishaudio-2"></span>
### isPublishAudio

```java
public boolean com.ss.bytertc.engine.RTCRoomConfig.isPublishAudio()
```


<span id="SVCLayer"></span>
# SVCLayer

```java
public enum com.ss.bytertc.engine.SubscribeConfig.SVCLayer
```


Scalable Video Coding layer

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|DEFAULT |0 |Default value. No specified layer. |
|BASE |1 |Layer T0 |
|MAIN |2 |Layer T0 + T1 |
|HIGH |3 |Layer T0 + T1 + T2 |


<span id="Rectangle"></span>
# Rectangle

```java
public class com.ss.bytertc.engine.video.Rectangle
```


Rectangle Area

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[x](https://docs.byteplus.com/en/docs/12/14169#Rectangle-x) |
|int |0 |[y](https://docs.byteplus.com/en/docs/12/14169#Rectangle-y) |
|int |0 |[width](https://docs.byteplus.com/en/docs/12/14169#Rectangle-width) |
|int |0 |[height](https://docs.byteplus.com/en/docs/12/14169#Rectangle-height) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|Rectangle |[Rectangle](https://docs.byteplus.com/en/docs/12/14169#Rectangle-rectangle) |
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#Rectangle-tostring) |


<span id="instructions"></span>
## Instructions

<span id="Rectangle-x"></span>
### x

```java
public int com.ss.bytertc.engine.video.Rectangle.x = 0
```


The x coordinate of the upper left corner of the rectangular area

<span id="Rectangle-y"></span>
### y

```java
public int com.ss.bytertc.engine.video.Rectangle.y = 0
```


The y coordinate of the upper left corner of the rectangular area

<span id="Rectangle-width"></span>
### width

```java
public int com.ss.bytertc.engine.video.Rectangle.width = 0
```


Rectangle width in px

<span id="Rectangle-height"></span>
### height

```java
public int com.ss.bytertc.engine.video.Rectangle.height = 0
```


Rectangular height in px

<span id="instructions"></span>
## Instructions

<span id="Rectangle-rectangle"></span>
### Rectangle

```java
public com.ss.bytertc.engine.video.Rectangle.Rectangle(
    int x,
    int y,
    int w,
    int h
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|x |int |\- |
|y |int |\- |
|w |int |\- |
|h |int |\- |


<span id="Rectangle-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.video.Rectangle.toString()
```


<span id="VideoRotationMode"></span>
# VideoRotationMode

```java
public enum com.ss.bytertc.engine.data.VideoRotationMode
```


Video orientation

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FOLLOW_APP |0 |The orientation of the App |
|FOLLOW_GSENSOR |1 |Gravity |


<span id="PlayerState"></span>
# PlayerState

```java
public enum com.ss.bytertc.engine.data.PlayerState
```


Player state.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|IDLE |0 |Not started. |
|PRELOADED |1 |Preloaded. |
|OPENED |2 |Opened. |
|PLAYING |3 |Playing. |
|PAUSED |4 |Paused. |
|STOPPED |5 |Playback is stopped. |
|FAILED |6 |Failed. |
|FINISHED |7 |Playback ended. |
|LOOP_FINISHED |8 |Loop playback ended. |


<span id="AudioScenarioType"></span>
# AudioScenarioType

```java
public enum com.ss.bytertc.engine.type.AudioScenarioType
```


Audio scenarios.

After selecting the audio scenario, the SDK will automatically select the call/media volume, according to the OS and microphone status. For more information, see [What is the difference between in-call volume and media volume?](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-651068).

You can set the audio scenario by calling `setAudioScenario`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|DEFAULT |0 |Default scenario. |
|CHATROOM |1 |Chat room scenario. The call clarity is higher, suitable for meetings, chat rooms, etc. |
|GAMESTREAMING |2 |Audio streaming scenario, suitable for group voice chat in a game. |
|CHORUS |3 |Chorus scenario. Low latency. |
|EDUCATION |4 |Education scenario. Suitable for high\-fidelity audio scenarios dominated by human\-voice teaching content. |
|AICLIENT |5 |AI dialogue scenario: Applicable to scenarios where real humans interact with AI agents. |


<span id="AudioPropertiesMode"></span>
# AudioPropertiesMode

```java
public enum com.ss.bytertc.engine.data.AudioPropertiesMode
```


The audio info included in [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalaudiopropertiesreport).

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_PROPERTIES_MODE_MICROPHONE |0 |Only locally captured microphone audio info and locally captured screen audio info are included. |
|AUDIO_PROPERTIES_MODE_AUDIOMIXING |1 |The following information is included:<br><br><br>&nbsp;<br><br>* Locally captured microphone audio info and locally captured screen audio info;<br><br>* Locally audio mixing info. |


<span id="VoiceEqualizationBandFrequency"></span>
# VoiceEqualizationBandFrequency

```java
public enum com.ss.bytertc.engine.type.VoiceEqualizationBandFrequency
```


Audio Equalization effect.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VOICE_EQUALIZATION_BAND_FREQUENCY_31 |0 |The frequency band with a center frequency of 31Hz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_62 |1 |The frequency band with a center frequency of 62Hz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_125 |2 |The frequency band with a center frequency of 125Hz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_250 |3 |The frequency band with a center frequency of 250Hz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_500 |4 |The frequency band with a center frequency of 500Hz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_1K |5 |The frequency band with a center frequency of 1kHz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_2K |6 |The frequency band with a center frequency of 2kHz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_4K |7 |The frequency band with a center frequency of 4kHz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_8K |8 |The frequency band with a center frequency of 8kHz. |
|VOICE_EQUALIZATION_BAND_FREQUENCY_16K |9 |The frequency band with a center frequency of 16kHz. |


<span id="SysStats"></span>
# SysStats

```java
public class com.ss.bytertc.engine.SysStats
```


CPU and memory statistics

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[cpuCores](https://docs.byteplus.com/en/docs/12/14169#SysStats-cpucores) |
|double |\- |[cpuAppUsage](https://docs.byteplus.com/en/docs/12/14169#SysStats-cpuappusage) |
|double |\- |[cpuTotalUsage](https://docs.byteplus.com/en/docs/12/14169#SysStats-cputotalusage) |
|double |\- |[memoryUsage](https://docs.byteplus.com/en/docs/12/14169#SysStats-memoryusage) |
|long |\- |[fullMemory](https://docs.byteplus.com/en/docs/12/14169#SysStats-fullmemory) |
|long |\- |[totalMemoryUsage](https://docs.byteplus.com/en/docs/12/14169#SysStats-totalmemoryusage) |
|long |\- |[freeMemory](https://docs.byteplus.com/en/docs/12/14169#SysStats-freememory) |
|double |\- |[memoryRatio](https://docs.byteplus.com/en/docs/12/14169#SysStats-memoryratio) |
|double |\- |[totalMemoryRatio](https://docs.byteplus.com/en/docs/12/14169#SysStats-totalmemoryratio) |


<span id="instructions"></span>
## Instructions

<span id="SysStats-cpucores"></span>
### cpuCores

```java
public int com.ss.bytertc.engine.SysStats.cpuCores
```


Device CPU cores

<span id="SysStats-cpuappusage"></span>
### cpuAppUsage

```java
public double com.ss.bytertc.engine.SysStats.cpuAppUsage
```


The CPU usage of the application, the value range is [0,1].

<span id="SysStats-cputotalusage"></span>
### cpuTotalUsage

```java
public double com.ss.bytertc.engine.SysStats.cpuTotalUsage
```


The CPU usage of the system, the value range is [0,1].

<span id="SysStats-memoryusage"></span>
### memoryUsage

```java
public double com.ss.bytertc.engine.SysStats.memoryUsage
```


Application's memory occupancy in MB

<span id="SysStats-fullmemory"></span>
### fullMemory

```java
public long com.ss.bytertc.engine.SysStats.fullMemory
```


Device memory size unit: MB

<span id="SysStats-totalmemoryusage"></span>
### totalMemoryUsage

```java
public long com.ss.bytertc.engine.SysStats.totalMemoryUsage
```


System used memory (in MB)

<span id="SysStats-freememory"></span>
### freeMemory

```java
public long com.ss.bytertc.engine.SysStats.freeMemory
```


System current free memory (in MB)

<span id="SysStats-memoryratio"></span>
### memoryRatio

```java
public double com.ss.bytertc.engine.SysStats.memoryRatio
```


Memory usage of the current application (in %)

<span id="SysStats-totalmemoryratio"></span>
### totalMemoryRatio

```java
public double com.ss.bytertc.engine.SysStats.totalMemoryRatio
```


System memory usage (in %)

<span id="VideoContentType"></span>
# VideoContentType

```java
public enum com.ss.bytertc.engine.data.VideoContentType
```


Video content type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|NORMAL_FRAME |0 |Normal video |
|BLACK_FRAME |1 |Black frame video |


<span id="SubscribeConfig"></span>
# SubscribeConfig

```java
public class com.ss.bytertc.engine.SubscribeConfig
```


Select subscription configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|boolean |\- |[isScreen](https://docs.byteplus.com/en/docs/12/14169#SubscribeConfig-isscreen) |
|boolean |\- |[subVideo](https://docs.byteplus.com/en/docs/12/14169#SubscribeConfig-subvideo) |
|boolean |\- |[subAudio](https://docs.byteplus.com/en/docs/12/14169#SubscribeConfig-subaudio) |
|int |\- |[videoIndex](https://docs.byteplus.com/en/docs/12/14169#SubscribeConfig-videoindex) |
|int |0 |[subWidth](https://docs.byteplus.com/en/docs/12/14169#SubscribeConfig-subwidth) |
|int |0 |[subHeight](https://docs.byteplus.com/en/docs/12/14169#SubscribeConfig-subheight) |
|int |0 |[framerate](https://docs.byteplus.com/en/docs/12/14169#SubscribeConfig-framerate) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeConfig-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.SubscribeConfig.isScreen
```


Reserved field. Do not set this field in the single\-stream SDK.

<span id="SubscribeConfig-subvideo"></span>
### subVideo

```java
public boolean com.ss.bytertc.engine.SubscribeConfig.subVideo
```


Whether video stream is included

<span id="SubscribeConfig-subaudio"></span>
### subAudio

```java
public boolean com.ss.bytertc.engine.SubscribeConfig.subAudio
```


Whether audio stream is included

<span id="SubscribeConfig-videoindex"></span>
### videoIndex

```java
public int com.ss.bytertc.engine.SubscribeConfig.videoIndex
```


Subscribed video stream resolution subscript.

Users can publish multiple videos of different resolutions in a stream. Therefore, when subscribing to a stream, you need to specify the specific resolution of the subscription. This parameter is used to specify the subscript of the resolution to be subscribed to, and the default value is 0.

<span id="SubscribeConfig-subwidth"></span>
### subWidth

```java
public int com.ss.bytertc.engine.SubscribeConfig.subWidth = 0
```


Width of the video stream in px

<span id="SubscribeConfig-subheight"></span>
### subHeight

```java
public int com.ss.bytertc.engine.SubscribeConfig.subHeight = 0
```


Height of the video stream in px

<span id="SubscribeConfig-framerate"></span>
### framerate

```java
public int com.ss.bytertc.engine.SubscribeConfig.framerate = 0
```


Expected maximum frame rate of the subscribed stream in fps. The default value is 0, values greater than 10 are valid.

If the frame rate of the stream published is higher than the value set by the subscriber, the subscriber receives the video of the frame rate set by this API; if the frame rate of the stream published is lower than the value set by the subscriber, the subscriber receives the video of the same frame rate of the video published.

Only valid if the stream is coded with SVC technique.

<span id="EchoTestConfig"></span>
# EchoTestConfig

```java
public class com.ss.bytertc.engine.data.EchoTestConfig
```


Video/audio call test configurations

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|View |\- |[view](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-view) |
|String |\- |[uid](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-uid) |
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-roomid) |
|String |\- |[token](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-token) |
|boolean |\- |[enableAudio](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-enableaudio) |
|boolean |\- |[enableVideo](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-enablevideo) |
|int |\- |[audioReportInterval](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-audioreportinterval) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|View |[getEchoRenderView](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-getechorenderview) |
|String |[getEchoUid](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-getechouid) |
|String |[getEchoRoomId](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-getechoroomid) |
|String |[getEchoToken](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-getechotoken) |
|boolean |[getEchoEnabledAudio](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-getechoenabledaudio) |
|boolean |[getEchoEnabledVideo](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-getechoenabledvideo) |
|int |[getAudioReportInterval](https://docs.byteplus.com/en/docs/12/14169#EchoTestConfig-getaudioreportinterval) |


<span id="instructions"></span>
## Instructions

<span id="EchoTestConfig-view"></span>
### view

```java
public View com.ss.bytertc.engine.data.EchoTestConfig.view
```


View for rendering received video

<span id="EchoTestConfig-uid"></span>
### uid

```java
public String com.ss.bytertc.engine.data.EchoTestConfig.uid
```


User ID for testing

<span id="EchoTestConfig-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.data.EchoTestConfig.roomId
```


ID of the room that the tested user will join.

<span id="EchoTestConfig-token"></span>
### token

```java
public String com.ss.bytertc.engine.data.EchoTestConfig.token
```


Token used for authenticating users when they enter the room.

<span id="EchoTestConfig-enableaudio"></span>
### enableAudio

```java
public boolean com.ss.bytertc.engine.data.EchoTestConfig.enableAudio
```


Whether to test audio. The device to be tested is the default audio device.


* true: Yes

   * If you use internal capture, the device microphone will automatically turn on and `onLocalAudioPropertiesReport` will be triggered when the value of audioReportInterval is set to greater than 0, from which you can judge the working status of the microphone.

   * If you choose custom capture, you also need to call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushexternalaudioframe) to push the captured audio to the SDK.

* false: No

    &nbsp;


<span id="enablevideo"></span>
### enableVideo

```java
public boolean com.ss.bytertc.engine.data.EchoTestConfig.enableVideo
```


Whether to test video. If you are using a desktop PC, the device to be tested is by default the first video device in the list.


* true: Yes

   * If you use internal capture, the device camera will automatically turn on.

   * If you choose custom capture, you also need to call [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushexternalvideoframe) to push the captured video to the SDK.

* false: No


**Notes**

The video is published with fixed parameters: resolution 640px × 360px, frame rate 15fps.

<span id="EchoTestConfig-audioreportinterval"></span>
### audioReportInterval

```java
public int com.ss.bytertc.engine.data.EchoTestConfig.audioReportInterval
```


Volume prompt interval in ms, the default value is 100.


* `<= 0`: Turn off prompt

* `(0,100]` Invalid interval value, and will be automatically reset to 100ms.

* `> 100`: the actual value of interval


<span id="instructions"></span>
## Instructions

<span id="EchoTestConfig-getechorenderview"></span>
### getEchoRenderView

```java
public View com.ss.bytertc.engine.data.EchoTestConfig.getEchoRenderView()
```


<span id="EchoTestConfig-getechouid"></span>
### getEchoUid

```java
public String com.ss.bytertc.engine.data.EchoTestConfig.getEchoUid()
```


<span id="EchoTestConfig-getechoroomid"></span>
### getEchoRoomId

```java
public String com.ss.bytertc.engine.data.EchoTestConfig.getEchoRoomId()
```


<span id="EchoTestConfig-getechotoken"></span>
### getEchoToken

```java
public String com.ss.bytertc.engine.data.EchoTestConfig.getEchoToken()
```


<span id="EchoTestConfig-getechoenabledaudio"></span>
### getEchoEnabledAudio

```java
public boolean com.ss.bytertc.engine.data.EchoTestConfig.getEchoEnabledAudio()
```


<span id="EchoTestConfig-getechoenabledvideo"></span>
### getEchoEnabledVideo

```java
public boolean com.ss.bytertc.engine.data.EchoTestConfig.getEchoEnabledVideo()
```


<span id="EchoTestConfig-getaudioreportinterval"></span>
### getAudioReportInterval

```java
public int com.ss.bytertc.engine.data.EchoTestConfig.getAudioReportInterval()
```


<span id="AudioSampleRate"></span>
# AudioSampleRate

```java
public enum com.ss.bytertc.engine.data.AudioSampleRate
```


Audio sample rate in Hz.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_SAMPLE_RATE_AUTO |\-1 |Default value. 48000Hz. |
|AUDIO_SAMPLE_RATE_8000 |8000 |8000Hz |
|AUDIO_SAMPLE_RATE_11025 |11025 |11025Hz |
|AUDIO_SAMPLE_RATE_16000 |16000 |16000Hz |
|AUDIO_SAMPLE_RATE_22050 |22050 |22050Hz |
|AUDIO_SAMPLE_RATE_24000 |24000 |24000Hz |
|AUDIO_SAMPLE_RATE_32000 |32000 |32000Hz |
|AUDIO_SAMPLE_RATE_44100 |44100 |44100Hz |
|AUDIO_SAMPLE_RATE_48000 |48000 |48000Hz |


<span id="VideoSimulcastMode"></span>
# VideoSimulcastMode

```java
public enum com.ss.bytertc.engine.data.VideoSimulcastMode
```


Multiple quality streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VIDEO_SIMULCAST_MODE_ONLY_ONE |0 |Single. The video stream is sent in only set of specification. |
|VIDEO_SIMULCAST_MODE_ON_DEMAND |1 |On\-demand. The publisher will publish streams according to the subscriber's demands. When no subscription preference is taking effect, 2 streams will be published. |
|VIDEO_SIMULCAST_MODE_ALWAYS_SIMULCAST |2 |Manual. The publisher will publish streams in the qualities of the settings. The default is to publish 2 streams. |


<span id="MuteState"></span>
# MuteState

```java
public enum com.ss.bytertc.engine.data.MuteState
```


Transmission/Playback state of the media stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MUTE_STATE_OFF |0 |Enable |
|MUTE_STATE_ON |1 |Disable |


<span id="PublishState"></span>
# PublishState

```java
public enum com.ss.bytertc.engine.data.PublishState
```


Stream publishing state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|PUBLISHED |0 |Successfully published. |
|UNPUBLISHED |1 |Failed to publish. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static PublishState |[fromId](https://docs.byteplus.com/en/docs/12/14169#PublishState-fromid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#PublishState-value) |
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#PublishState-tostring) |


<span id="instructions"></span>
## Instructions

<span id="PublishState-fromid"></span>
### fromId

```java
public static PublishState com.ss.bytertc.engine.data.PublishState.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="PublishState-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.PublishState.value()
```


Get current value

**Return Value**

Current value

<span id="PublishState-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.data.PublishState.toString()
```


<span id="MediaDeviceError"></span>
# MediaDeviceError

```java
public class com.ss.bytertc.engine.type.MediaDeviceError
```


Media device error

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[MEDIA_DEVICE_ERROR_OK](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_ok) |
|int |1 |[MEDIA_DEVICE_ERROR_NOPERMISSION](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_nopermission) |
|int |2 |[MEDIA_DEVICE_ERROR_DEVICEBUSY](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_devicebusy) |
|int |3 |[MEDIA_DEVICE_ERROR_DEVICEFAILURE](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_devicefailure) |
|int |4 |[MEDIA_DEVICE_ERROR_DEVICENOTFOUND](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_devicenotfound) |
|int |5 |[MEDIA_DEVICE_ERROR_DEVICEDISCONNECTED](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_devicedisconnected) |
|int |6 |[MEDIA_DEVICE_ERROR_DEVICENOCALLBACK](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_devicenocallback) |
|int |7 |[MEDIA_DEVICE_ERROR_UNSUPPORTFORMAT](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceError-media_device_error_unsupportformat) |


<span id="instructions"></span>
## Instructions

<span id="MediaDeviceError-media_device_error_ok"></span>
### MEDIA_DEVICE_ERROR_OK

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_OK = 0
```


Normal

<span id="MediaDeviceError-media_device_error_nopermission"></span>
### MEDIA_DEVICE_ERROR_NOPERMISSION

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_NOPERMISSION = 1
```


No permission

<span id="MediaDeviceError-media_device_error_devicebusy"></span>
### MEDIA_DEVICE_ERROR_DEVICEBUSY

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_DEVICEBUSY = 2
```


Occupied by the other application

<span id="MediaDeviceError-media_device_error_devicefailure"></span>
### MEDIA_DEVICE_ERROR_DEVICEFAILURE

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_DEVICEFAILURE = 3
```


Error

<span id="MediaDeviceError-media_device_error_devicenotfound"></span>
### MEDIA_DEVICE_ERROR_DEVICENOTFOUND

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_DEVICENOTFOUND = 4
```


Not found

<span id="MediaDeviceError-media_device_error_devicedisconnected"></span>
### MEDIA_DEVICE_ERROR_DEVICEDISCONNECTED

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_DEVICEDISCONNECTED = 5
```


Disconnected

<span id="MediaDeviceError-media_device_error_devicenocallback"></span>
### MEDIA_DEVICE_ERROR_DEVICENOCALLBACK

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_DEVICENOCALLBACK = 6
```


No data callback from the capture devices.

RTC emits this error when the media device is expected to be working but no data is received.

<span id="MediaDeviceError-media_device_error_unsupportformat"></span>
### MEDIA_DEVICE_ERROR_UNSUPPORTFORMAT

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceError.MEDIA_DEVICE_ERROR_UNSUPPORTFORMAT = 7
```


Not supported sample rate

<span id="MixedStreamControlConfig"></span>
# MixedStreamControlConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamControlConfig
```


Configurations to be set while mixing streams on the server side.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|boolean |false |[enableVolumeIndication](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-enablevolumeindication) |
|float |2.0f |[volumeIndicationInterval](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-volumeindicationinterval) |
|int |0 |[talkVolume](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-talkvolume) |
|boolean |false |[isAddVolumeValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-isaddvolumevalue) |
|MixedStreamSEIContentMode |MixedStreamSEIContentMode.MIXED_STREAM_SEI_CONTENT_MODE_DEFAULT |[seiContentMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-seicontentmode) |
|int |100 |[seiPayloadType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-seipayloadtype) |
|String |"" |[seiPayloadUuid](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-seipayloaduuid) |
|MixedStreamMediaType |MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO |[mediaType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-mediatype) |
|MixedStreamPushMode |MixedStreamPushMode.ON_STREAM |[pushStreamMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-pushstreammode) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamControlConfig |[MixedStreamControlConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-mixedstreamcontrolconfig) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamControlConfig-enablevolumeindication"></span>
### enableVolumeIndication

```java
public boolean com.ss.bytertc.engine.live.MixedStreamControlConfig.enableVolumeIndication = false
```


> Available since 3.56


Sets whether to enable the function of separately sending sound indication SEI.

**Notes**

After setting this method to "true", you can choose whether to send sound indication SEI only through [seiContentMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-seicontentmode).

<span id="MixedStreamControlConfig-volumeindicationinterval"></span>
### volumeIndicationInterval

```java
public float com.ss.bytertc.engine.live.MixedStreamControlConfig.volumeIndicationInterval = 2.0f
```


> Available since 3.56


Sets the sound indication interval.

<span id="MixedStreamControlConfig-talkvolume"></span>
### talkVolume

```java
public int com.ss.bytertc.engine.live.MixedStreamControlConfig.talkVolume = 0
```


Sets the effective volume.

<span id="MixedStreamControlConfig-isaddvolumevalue"></span>
### isAddVolumeValue

```java
public boolean com.ss.bytertc.engine.live.MixedStreamControlConfig.isAddVolumeValue = false
```


> Available since 3.56


Sets whether volume value is contained in the sound indication SEI.

<span id="MixedStreamControlConfig-seicontentmode"></span>
### seiContentMode

```java
public MixedStreamSEIContentMode com.ss.bytertc.engine.live.MixedStreamControlConfig.seiContentMode = MixedStreamSEIContentMode.MIXED_STREAM_SEI_CONTENT_MODE_DEFAULT
```


> Available since 3.56


Sets SEI content.

<span id="MixedStreamControlConfig-seipayloadtype"></span>
### seiPayloadType

```java
public int com.ss.bytertc.engine.live.MixedStreamControlConfig.seiPayloadType = 100
```


> Available since 3.56


Set SEI payload type.

**Notes**

During the process of pushing streams to CDN, you cannot change the parameter.

<span id="MixedStreamControlConfig-seipayloaduuid"></span>
### seiPayloadUuid

```java
public String com.ss.bytertc.engine.live.MixedStreamControlConfig.seiPayloadUuid = ""
```


> Available since 3.56


Set SEI Payload UUID.

**Notes**

When PayloadType is `5`, you must set PayloadUUID, or you will receive a callback indicating parameter error. The error code is 1091.

When PayloadType is not `5`, it is not required to set PayloadUUID. If filled, it will be ignored by the backend.

During the process of pushing streams to CDN, you cannot change the parameter.

<span id="MixedStreamControlConfig-mediatype"></span>
### mediaType

```java
public MixedStreamMediaType com.ss.bytertc.engine.live.MixedStreamControlConfig.mediaType = MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO
```


> Available since 3.57


Sets the type of media stream pushed to CDN after being mixed.

<span id="MixedStreamControlConfig-pushstreammode"></span>
### pushStreamMode

```java
public MixedStreamPushMode com.ss.bytertc.engine.live.MixedStreamControlConfig.pushStreamMode = MixedStreamPushMode.ON_STREAM
```


> Available since 3.57


Sets whether to initiate a stream mixing task in the absence of any users publishing streams.

<span id="instructions"></span>
## Instructions

<span id="MixedStreamControlConfig-mixedstreamcontrolconfig"></span>
### MixedStreamControlConfig

```java
public com.ss.bytertc.engine.live.MixedStreamControlConfig.MixedStreamControlConfig()
```


<span id="AudioFrameSource"></span>
# AudioFrameSource

```java
public enum com.ss.bytertc.engine.data.AudioFrameSource
```


Audio file recording source type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_FRAME_SOURCE_MIC |0 |The audio captured by the local microphone. |
|AUDIO_FRAME_SOURCE_PLAYBACK |1 |The audio obtained by mixing all remote users' audio. |
|AUDIO_FRAME_SOURCE_MIXED |2 |The audio got by mixing the local captured audio and all remote user's audio. |


<span id="StreamRemoveReason"></span>
# StreamRemoveReason

```java
public enum com.ss.bytertc.engine.type.StreamRemoveReason
```


The reason for the removal of the remote stream in the room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|STREAM_REMOVE_REASON_UNPUBLISH |0 |The remote user stops publishing the stream. |
|STREAM_REMOVE_REASON_PUBLISH_FAILED |1 |The remote user failed to publish the stream. |
|STREAM_REMOVE_REASON_KEEP_LIVE_FAILED |2 |Media server failed to receive media data from the client for 10 seconds. |
|STREAM_REMOVE_REASON_CLIENT_DISCONNECTED |3 |The remote user is disconnected. |
|STREAM_REMOVE_REASON_REPUBLISH |4 |The remote user republishes the stream. |
|STREAM_REMOVE_REASON_OTHER |5 |Other reasons. |
|STREAM_REMOVE_REASON_PUBLISH_PRIVILEGE_TOKEN_EXPIRED |6 |The remote user's publishing privilege of the Token is expired. |


<span id="ForwardStreamError"></span>
# ForwardStreamError

```java
public enum com.ss.bytertc.engine.data.ForwardStreamStateInfo.ForwardStreamError
```


Error codes during the relaying

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FORWARD_STREAM_ERROR_OK |0 |Normal |
|FORWARD_STREAM_ERROR_INVALID_ARGUMENT |1201 |Invalid argument |
|FORWARD_STREAM_ERROR_INVALID_TOKEN |1202 |Invalid token |
|FORWARD_STREAM_ERROR_RESPONSE |1203 |Error returning from server |
|FORWARD_STREAM_ERROR_REMOTE_KICKED |1204 |Relaying aborts because a user with the same user ID as that of the publisher joins. |
|FORWARD_STREAM_ERROR_NOT_SUPPORT |1205 |Server denies. |


<span id="StreamInfo"></span>
# StreamInfo

```java
public class com.ss.bytertc.engine.data.StreamInfo
```


Information about the remote stream.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[streamId](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-streamid) |
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-roomid) |
|String |\- |[userId](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-userid) |
|int |\- |[streamIndex](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-streamindex) |
|boolean |\- |[isScreen](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-isscreen) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|String |[getStreamId](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-getstreamid) |
|String |[getRoomId](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-getroomid) |
|String |[getUserId](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-getuserid) |
|int |[getStreamIndex](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-getstreamindex) |
|boolean |[getIsScreen](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-getisscreen) |
|boolean |[hasNullProperty](https://docs.byteplus.com/en/docs/12/14169#StreamInfo-hasnullproperty) |


<span id="instructions"></span>
## Instructions

<span id="StreamInfo-streamid"></span>
### streamId

```java
public String com.ss.bytertc.engine.data.StreamInfo.streamId
```


Stream ID.

<span id="StreamInfo-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.data.StreamInfo.roomId
```


The ID of the room from which the stream was published.

<span id="StreamInfo-userid"></span>
### userId

```java
public String com.ss.bytertc.engine.data.StreamInfo.userId
```


The ID of the user who published the stream.

<span id="StreamInfo-streamindex"></span>
### streamIndex

```java
public int com.ss.bytertc.engine.data.StreamInfo.streamIndex
```


Reserved field.

<span id="StreamInfo-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.data.StreamInfo.isScreen
```


Reserved field. Ignore the value returned in this field.

<span id="instructions"></span>
## Instructions

<span id="StreamInfo-getstreamid"></span>
### getStreamId

```java
public String com.ss.bytertc.engine.data.StreamInfo.getStreamId()
```


Gets the stream ID

<span id="StreamInfo-getroomid"></span>
### getRoomId

```java
public String com.ss.bytertc.engine.data.StreamInfo.getRoomId()
```


Gets the room ID

<span id="StreamInfo-getuserid"></span>
### getUserId

```java
public String com.ss.bytertc.engine.data.StreamInfo.getUserId()
```


Gets the user ID

<span id="StreamInfo-getstreamindex"></span>
### getStreamIndex

```java
public int com.ss.bytertc.engine.data.StreamInfo.getStreamIndex()
```


Reserved field.

<span id="StreamInfo-getisscreen"></span>
### getIsScreen

```java
public boolean com.ss.bytertc.engine.data.StreamInfo.getIsScreen()
```


<span id="StreamInfo-hasnullproperty"></span>
### hasNullProperty

```java
public boolean com.ss.bytertc.engine.data.StreamInfo.hasNullProperty()
```


Check the class has null property

<span id="NetworkDetectionStopReason"></span>
# NetworkDetectionStopReason

```java
public enum com.ss.bytertc.engine.type.NetworkDetectionStopReason
```


The reason why the probe before the call is stopped.

The parameter type of the `onNetworkDetectionStopped`

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|USER |0 |User actively stops |
|TIMEOUT |1 |Detection over three minutes |
|CONNECTION_LOST |2 |Probe network connection disconnected.<br><br>&nbsp;<br><br>When no reply is received beyond 12s, the SDK will disconnect the network and will not try to reconnect. |
|STREAMING |3 |Local user starts publishing and subscribing to streams; stop detection |
|INNER_ERR |4 |Network probe failure, internal anomaly |


<span id="StreamSubscribeState"></span>
# StreamSubscribeState

```java
public enum com.ss.bytertc.engine.StreamSubscribeState
```


Subscription status of media streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SUCCESS |0 |Successfully changed the subscription status |
|FAILED_NOT_IN_ROOM |1 |Failed to change the subscription status, because you were not in the room. |
|FAILED_STREAM_NOT_FOUND |2 |Failed to change the subscription status, because the target audio/video stream was not found. |
|FAILED_AUTO_MODE |3 |\- |
|FAILED_SIGNAL |4 |Failed to change the subscription status because of a signaling error. Please try again. |


<span id="ReceiveRange"></span>
# ReceiveRange

```java
public class com.ss.bytertc.engine.data.ReceiveRange
```


The range where local user can hear audio with attenuation effect.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[min](https://docs.byteplus.com/en/docs/12/14169#ReceiveRange-min) |
|int |\- |[max](https://docs.byteplus.com/en/docs/12/14169#ReceiveRange-max) |


<span id="instructions"></span>
## Instructions

<span id="ReceiveRange-min"></span>
### min

```java
public int com.ss.bytertc.engine.data.ReceiveRange.min
```


The minimum distance at which the local user can hear the attenuated audio from remote users.

The value must be ≥ 0, but ≤ max.

No attenuation effect for audio from distances less than this value you set.

<span id="ReceiveRange-max"></span>
### max

```java
public int com.ss.bytertc.engine.data.ReceiveRange.max
```


The maximum distance at which the local user can hear audio from remote users.

The value must be ≥ min, and \> 0.

Audio from distances larger than the value you set cannot be heard.

<span id="NetworkQuality"></span>
# NetworkQuality

```java
public class com.ss.bytertc.engine.type.NetworkQuality
```


Quality of media streaming network for affiliated users.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[NETWORK_QUALITY_UNKNOWN](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality-network_quality_unknown) |
|int |1 |[NETWORK_QUALITY_EXCELLENT](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality-network_quality_excellent) |
|int |2 |[NETWORK_QUALITY_GOOD](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality-network_quality_good) |
|int |3 |[NETWORK_QUALITY_POOR](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality-network_quality_poor) |
|int |4 |[NETWORK_QUALITY_BAD](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality-network_quality_bad) |
|int |5 |[NETWORK_QUALITY_VERY_BAD](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality-network_quality_very_bad) |
|int |6 |[NETWORK_QUALITY_DOWN](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality-network_quality_down) |


<span id="instructions"></span>
## Instructions

<span id="NetworkQuality-network_quality_unknown"></span>
### NETWORK_QUALITY_UNKNOWN

```java
public static final int com.ss.bytertc.engine.type.NetworkQuality.NETWORK_QUALITY_UNKNOWN = 0
```


Media stream network quality unknown.

<span id="NetworkQuality-network_quality_excellent"></span>
### NETWORK_QUALITY_EXCELLENT

```java
public static final int com.ss.bytertc.engine.type.NetworkQuality.NETWORK_QUALITY_EXCELLENT = 1
```


Media Streaming Network quality is excellent.

<span id="NetworkQuality-network_quality_good"></span>
### NETWORK_QUALITY_GOOD

```java
public static final int com.ss.bytertc.engine.type.NetworkQuality.NETWORK_QUALITY_GOOD = 2
```


Media streaming network quality is good.

<span id="NetworkQuality-network_quality_poor"></span>
### NETWORK_QUALITY_POOR

```java
public static final int com.ss.bytertc.engine.type.NetworkQuality.NETWORK_QUALITY_POOR = 3
```


Media streaming The network quality is poor but does not affect communication.

<span id="NetworkQuality-network_quality_bad"></span>
### NETWORK_QUALITY_BAD

```java
public static final int com.ss.bytertc.engine.type.NetworkQuality.NETWORK_QUALITY_BAD = 4
```


Media streaming Poor network quality Poor communication.

<span id="NetworkQuality-network_quality_very_bad"></span>
### NETWORK_QUALITY_VERY_BAD

```java
public static final int com.ss.bytertc.engine.type.NetworkQuality.NETWORK_QUALITY_VERY_BAD = 5
```


Media streaming network quality is very poor.

<span id="NetworkQuality-network_quality_down"></span>
### NETWORK_QUALITY_DOWN

```java
public static final int com.ss.bytertc.engine.type.NetworkQuality.NETWORK_QUALITY_DOWN = 6
```


The network is down. It may be down due to no answer within 12s, airplane mode on, disconnected cable, etc.

Refer to [Get connection state](https://docs.byteplus.com/byteplus-rtc/docs/95376) for more details about getting connection state.

<span id="ZoomConfigType"></span>
# ZoomConfigType

```java
public enum com.ss.bytertc.engine.data.ZoomConfigType
```


Digital Zoom type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ZOOM_FOCUS_OFFSET |0 |To set the offset for zooming in and zooming out. |
|ZOOM_MOVE_OFFSET |1 |To set the offset for panning and tiling. |


<span id="LocalVideoStats"></span>
# LocalVideoStats

```java
public class com.ss.bytertc.engine.type.LocalVideoStats
```


Local video stream statistics, reference period 2s.

After a local user publishes a video stream successfully, the SDK will periodically notify the user through `onLocalStreamStats`

The delivery status of the published video stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |\- |[sentKBitrate](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-sentkbitrate) |
|int |\- |[inputFrameRate](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-inputframerate) |
|int |\- |[sentFrameRate](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-sentframerate) |
|int |\- |[encoderOutputFrameRate](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-encoderoutputframerate) |
|int |\- |[rendererOutputFrameRate](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-rendereroutputframerate) |
|int |\- |[statsInterval](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-statsinterval) |
|float |\- |[videoLossRate](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-videolossrate) |
|int |\- |[rtt](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-rtt) |
|int |\- |[encodedBitrate](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-encodedbitrate) |
|int |\- |[encodedFrameWidth](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-encodedframewidth) |
|int |\- |[encodedFrameHeight](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-encodedframeheight) |
|int |\- |[encodedFrameCount](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-encodedframecount) |
|int |\- |[codecType](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-codectype) |
|boolean |\- |[isScreen](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-isscreen) |
|int |\- |[jitter](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats-jitter) |


<span id="instructions"></span>
## Instructions

<span id="LocalVideoStats-sentkbitrate"></span>
### sentKBitrate

```java
public float com.ss.bytertc.engine.type.LocalVideoStats.sentKBitrate
```


TX bitrate in Kbps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-inputframerate"></span>
### inputFrameRate

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.inputFrameRate
```


Sampling frame rate in fps of video capture during this reference period

<span id="LocalVideoStats-sentframerate"></span>
### sentFrameRate

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.sentFrameRate
```


TX frame rate in fps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encoderoutputframerate"></span>
### encoderOutputFrameRate

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.encoderOutputFrameRate
```


Encoder\-output frame rate in fps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-rendereroutputframerate"></span>
### rendererOutputFrameRate

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.rendererOutputFrameRate
```


Local\-rendering frame rate in fps during this reference period

<span id="LocalVideoStats-statsinterval"></span>
### statsInterval

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.statsInterval
```


Reference period in ms.

This field is used to set the reference period for the callback, which is 2 s by default.

<span id="LocalVideoStats-videolossrate"></span>
### videoLossRate

```java
public float com.ss.bytertc.engine.type.LocalVideoStats.videoLossRate
```


Video packet loss rate. The video uplink packet loss rate in this reference period ranges from [0,1].

<span id="LocalVideoStats-rtt"></span>
### rtt

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.rtt
```


Round\-trip time in ms.

<span id="LocalVideoStats-encodedbitrate"></span>
### encodedBitrate

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.encodedBitrate
```


Video encoding bitrate in Kbps of the video stream with the highest resolution within the reference period.

<span id="LocalVideoStats-encodedframewidth"></span>
### encodedFrameWidth

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.encodedFrameWidth
```


Video encoding width in px of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encodedframeheight"></span>
### encodedFrameHeight

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.encodedFrameHeight
```


Video encoding height in px of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encodedframecount"></span>
### encodedFrameCount

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.encodedFrameCount
```


The total number of the video stream with the highest resolution within the reference period sent in the reference period.

<span id="LocalVideoStats-codectype"></span>
### codecType

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.codecType
```


For the encoding type of the video, please refer to [VideoCodecType](https://docs.byteplus.com/en/docs/12/14169#VideoCodecType).

<span id="LocalVideoStats-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.type.LocalVideoStats.isScreen
```


Reserved field. Ignore the value returned in this field.

<span id="LocalVideoStats-jitter"></span>
### jitter

```java
public int com.ss.bytertc.engine.type.LocalVideoStats.jitter
```


Video uplink network jitter in ms.

<span id="AudioRecordingState"></span>
# AudioRecordingState

```java
public enum com.ss.bytertc.engine.type.AudioRecordingState
```


Audio recording config

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_RECORDING_STATE_ERROR |0 |Recording exception |
|AUDIO_RECORDING_STATE_PROCESSING |1 |Recording in progress |
|AUDIO_RECORDING_STATE_SUCCESS |2 |The recording task ends, and the file is saved. |


<span id="SubscribeState"></span>
# SubscribeState

```java
public enum com.ss.bytertc.engine.data.SubscribeState
```


Stream subscription state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SUBSCRIBED |0 |Successfully subscribed. |
|UNSUBSCRIBED |1 |Failed to subscribe. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static SubscribeState |[fromId](https://docs.byteplus.com/en/docs/12/14169#SubscribeState-fromid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#SubscribeState-value) |
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#SubscribeState-tostring) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeState-fromid"></span>
### fromId

```java
public static SubscribeState com.ss.bytertc.engine.data.SubscribeState.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="SubscribeState-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.SubscribeState.value()
```


Get current value

**Return Value**

Current value

<span id="SubscribeState-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.data.SubscribeState.toString()
```


<span id="AudioPlaybackDevice"></span>
# AudioPlaybackDevice

```java
public enum com.ss.bytertc.engine.data.AudioPlaybackDevice
```


Audio playback device

When the audio playback device changes, you will receive the `onAudioPlaybackDeviceChanged` callback.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_PLAYBACK_DEVICE_HEADSET |1 |Wired earphones |
|AUDIO_PLAYBACK_DEVICE_EARPIECE |2 |Earpiece |
|AUDIO_PLAYBACK_DEVICE_SPEAKERPHONE |3 |Speaker |
|AUDIO_PLAYBACK_DEVICE_HEADSET_BLUETOOTH |4 |Bluetooth earphones |
|AUDIO_PLAYBACK_DEVICE_HEADSET_USB |5 |USB device |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#AudioPlaybackDevice-value) |


<span id="instructions"></span>
## Instructions

<span id="AudioPlaybackDevice-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.AudioPlaybackDevice.value()
```


Get current value

**Return Value**

Current value

<span id="ForwardStreamInfo"></span>
# ForwardStreamInfo

```java
public class com.ss.bytertc.engine.data.ForwardStreamInfo
```


Information of the rooms where you want to relay the media stream to

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamInfo-roomid) |
|String |\- |[token](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamInfo-token) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamInfo-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.data.ForwardStreamInfo.roomId
```


ID of the room where the media stream aims to forward to

<span id="ForwardStreamInfo-token"></span>
### token

```java
public String com.ss.bytertc.engine.data.ForwardStreamInfo.token
```


RoomId and UserId are required to generate the Token to forward media streams to the room.

During developing and testing, you can use temporary tokens generated on the console. At the production stage, Tokens are generated by the token generating application deployed on your server.

Forwarding will fail if the token is invalid.

<span id="VideoPreprocessorConfig"></span>
# VideoPreprocessorConfig

```java
public class com.ss.bytertc.engine.video.VideoPreprocessorConfig
```


Video processing configuration parameters.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|VideoPixelFormat |VideoPixelFormat.UNKNOWN |[requiredPixelFormat](https://docs.byteplus.com/en/docs/12/14169#VideoPreprocessorConfig-requiredpixelformat) |
|ProcessorActionDomain |ProcessorActionDomain.PREVIEWANDENCODE |[actionDomain](https://docs.byteplus.com/en/docs/12/14169#VideoPreprocessorConfig-actiondomain) |


<span id="instructions"></span>
## Instructions

<span id="VideoPreprocessorConfig-requiredpixelformat"></span>
### requiredPixelFormat

```java
public VideoPixelFormat com.ss.bytertc.engine.video.VideoPreprocessorConfig.requiredPixelFormat = VideoPixelFormat.UNKNOWN
```


To set the requested pixel format, see'VideoPixelFormat 'in [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14169#VideoPixelFormat).

Only `I420,`TEXTURE_2D`and`UNKNOWN` are supported.

<span id="VideoPreprocessorConfig-actiondomain"></span>
### actionDomain

```java
public ProcessorActionDomain com.ss.bytertc.engine.video.VideoPreprocessorConfig.actionDomain = ProcessorActionDomain.PREVIEWANDENCODE
```


The effective range of the custom video preprocessor. See [ProcessorActionDomain](https://docs.byteplus.com/en/docs/12/14169#ProcessorActionDomain).

<span id="LocalProxyConfiguration"></span>
# LocalProxyConfiguration

```java
public class com.ss.bytertc.engine.type.LocalProxyConfiguration
```


Detailed information of local proxy configurations.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|LocalProxyType |\- |[localProxyType](https://docs.byteplus.com/en/docs/12/14169#LocalProxyConfiguration-localproxytype) |
|String |\- |[localProxyIp](https://docs.byteplus.com/en/docs/12/14169#LocalProxyConfiguration-localproxyip) |
|int |\- |[localProxyPort](https://docs.byteplus.com/en/docs/12/14169#LocalProxyConfiguration-localproxyport) |
|String |\- |[localProxyUsername](https://docs.byteplus.com/en/docs/12/14169#LocalProxyConfiguration-localproxyusername) |
|String |\- |[localProxyPassword](https://docs.byteplus.com/en/docs/12/14169#LocalProxyConfiguration-localproxypassword) |


<span id="instructions"></span>
## Instructions

<span id="LocalProxyConfiguration-localproxytype"></span>
### localProxyType

```java
public LocalProxyType com.ss.bytertc.engine.type.LocalProxyConfiguration.localProxyType
```


Types of local proxies. Refer to [LocalProxyType](https://docs.byteplus.com/en/docs/12/14169#LocalProxyType) for details.

<span id="LocalProxyConfiguration-localproxyip"></span>
### localProxyIp

```java
public String com.ss.bytertc.engine.type.LocalProxyConfiguration.localProxyIp
```


Local proxy IP.

<span id="LocalProxyConfiguration-localproxyport"></span>
### localProxyPort

```java
public int com.ss.bytertc.engine.type.LocalProxyConfiguration.localProxyPort
```


Local proxy port.

<span id="LocalProxyConfiguration-localproxyusername"></span>
### localProxyUsername

```java
public String com.ss.bytertc.engine.type.LocalProxyConfiguration.localProxyUsername
```


The username of the local proxy.

<span id="LocalProxyConfiguration-localproxypassword"></span>
### localProxyPassword

```java
public String com.ss.bytertc.engine.type.LocalProxyConfiguration.localProxyPassword
```


The password of the local proxy.

<span id="AudioFrame"></span>
# AudioFrame

```java
public class com.ss.bytertc.engine.utils.AudioFrame
```


Audio frame in PCM

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|byte[] |\- |[buffer](https://docs.byteplus.com/en/docs/12/14169#AudioFrame-buffer) |
|int |\- |[samples](https://docs.byteplus.com/en/docs/12/14169#AudioFrame-samples) |
|AudioSampleRate |\- |[sampleRate](https://docs.byteplus.com/en/docs/12/14169#AudioFrame-samplerate) |
|AudioChannel |\- |[channel](https://docs.byteplus.com/en/docs/12/14169#AudioFrame-channel) |


<span id="instructions"></span>
## Instructions

<span id="AudioFrame-buffer"></span>
### buffer

```java
public byte [] com.ss.bytertc.engine.utils.AudioFrame.buffer
```


PCM data

<span id="AudioFrame-samples"></span>
### samples

```java
public int com.ss.bytertc.engine.utils.AudioFrame.samples
```


Total number of samples

<span id="AudioFrame-samplerate"></span>
### sampleRate

```java
public AudioSampleRate com.ss.bytertc.engine.utils.AudioFrame.sampleRate
```


Sample rate, see [AudioSampleRate](https://docs.byteplus.com/en/docs/12/14169#AudioSampleRate).

<span id="AudioFrame-channel"></span>
### channel

```java
public AudioChannel com.ss.bytertc.engine.utils.AudioFrame.channel
```


Audio channel, see [AudioChannel](https://docs.byteplus.com/en/docs/12/14169#AudioChannel).

<span id="StreamSyncInfoConfig"></span>
# StreamSyncInfoConfig

```java
public class com.ss.bytertc.engine.data.StreamSyncInfoConfig
```


Configuration related to media stream information synchronization

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[repeatCount](https://docs.byteplus.com/en/docs/12/14169#StreamSyncInfoConfig-repeatcount) |
|SyncInfoStreamType |\- |[streamType](https://docs.byteplus.com/en/docs/12/14169#StreamSyncInfoConfig-streamtype) |


<span id="instructions"></span>
## Instructions

<span id="StreamSyncInfoConfig-repeatcount"></span>
### repeatCount

```java
public int com.ss.bytertc.engine.data.StreamSyncInfoConfig.repeatCount
```


Repeated number of messages sent

<span id="StreamSyncInfoConfig-streamtype"></span>
### streamType

```java
public SyncInfoStreamType com.ss.bytertc.engine.data.StreamSyncInfoConfig.streamType
```


Stream types for media stream information synchronization. See [SyncInfoStreamType](https://docs.byteplus.com/en/docs/12/14169#SyncInfoStreamType)

<span id="AudioDumpStatus"></span>
# AudioDumpStatus

```java
public enum com.ss.bytertc.engine.type.AudioDumpStatus
```


Audio dump status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_DUMP_START_FAILURE |0 |audio dump start failure |
|AUDIO_DUMP_START_SUCCESS |1 |audio dump start success |
|AUDIO_DUMP_STOP_FAILURE |2 |audio dump stop failure |
|AUDIO_DUMP_STOP_SUCCESS |3 |audio dump stop success |
|AUDIO_DUMP_RUNNING_FAILURE |4 |audio dump running failure |
|AUDIO_DUMP_RUNNING_SUCCESS |5 |audio dump running success |


<span id="EncoderPreference"></span>
# EncoderPreference

```java
public enum com.ss.bytertc.engine.VideoEncoderConfig.EncoderPreference
```


Encoder preference.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|DISABLED |0 |No preference. The frame rate and the resolution will not be adjusted. |
|MAINTAIN_FRAMERATE |1 |The high frame rate mode. Ensure the highest framerate possible. This mode is designed for videos with high\-motion contents. |
|MAINTAIN_QUALITY |2 |The high\-resolution mode. Ensure the highest resolution possible. This mode is designed for videos with static content. |
|AUTO |3 |Balancing resolution and frame rate.<br><br>For the screen\-recordings, indicates No preference. The frame rate and the resolution will not be adjusted. |


<span id="ProblemFeedbackOption"></span>
# ProblemFeedbackOption

```java
public enum com.ss.bytertc.engine.type.ProblemFeedbackOption
```


Audio & video quality feedback problem type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|NONE |0 |No problem |
|OTHER_MESSAGE |1L |Other issues |
|DISCONNECTED |1L << 1 |Connection failed |
|EAR_BACK_DELAY |1L << 2 |High latency for the ear monitor |
|LOCAL_NOISE |1L << 10 |Noise on the local end |
|LOCAL_AUDIO_LAGGING |1L << 11 |Audio stall on the local end |
|LOCAL_NO_AUDIO |1L << 12 |No sound on the local end |
|LOCAL_AUDIO_STRENGTH |1L << 13 |Too little/loud sound on the local end |
|LOCAL_ECHO |1L << 14 |Echo noise on the local end |
|LOCAL_VIDEO_FUZZY |1L << 24 |Unclear video on the local end |
|LOCAL_NOT_SYNC |1L << 25 |Audio & video out of sync on the local end |
|LOCAL_VIDEO_LAGGING |1L << 26 |Video stall on the local end |
|LOCAL_NO_VIDEO |1L << 27 |No picture on the local end |
|REMOTE_NOISE |1L << 37 |Noise on the remote end |
|REMOTE_AUDIO_LAGGING |1L << 38 |Audio stall on the remote end |
|REMOTE_NO_AUDIO |1L << 39 |No sound on the remote end |
|REMOTE_AUDIO_STRENGTH |1L << 40 |Too little/loud sound on the remote end |
|REMOTE_ECHO |1L << 41 |Echo noise on the remote end |
|REMOTE_VIDEO_FUZZY |1L << 51 |Unclear video on the remote end |
|REMOTE_NOT_SYNC |1L << 52 |Audio & video out of sync on the remote end |
|REMOTE_VIDEO_LAGGING |1L << 53 |Video stall on the remote end |
|REMOTE_NO_VIDEO |1L << 54 |No picture on the remote end |


<span id="MixedStreamAudioProfile"></span>
# MixedStreamAudioProfile

```java
public enum com.ss.bytertc.engine.live.MixedStreamAudioProfile
```


Advanced Audio Coding (AAC) profile.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIXED_STREAM_AUDIO_PROFILE_LC |LC |(Default) AAC Low\-Complexity profile (AAC\-LC). |
|MIXED_STREAM_AUDIO_PROFILE_HEV1 |HEv1 |HE\-AAC v1 profile (AAC LC with SBR). |
|MIXED_STREAM_AUDIO_PROFILE_HEV2 |HEv2 |HE\-AAC v2 profile (AAC LC with SBR and Parametric Stereo). |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamAudioProfile |[MixedStreamAudioProfile](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioProfile-mixedstreamaudioprofile) |
|String |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioProfile-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamAudioProfile-mixedstreamaudioprofile"></span>
### MixedStreamAudioProfile

```java
public com.ss.bytertc.engine.live.MixedStreamAudioProfile.MixedStreamAudioProfile(String value)
```


AAC profile.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |String |See [MixedStreamAudioProfile](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioProfile). It defaults to `0`, indicating AAC\-LC. It's recommended to be set. |


<span id="MixedStreamAudioProfile-getvalue"></span>
### getValue

```java
public String com.ss.bytertc.engine.live.MixedStreamAudioProfile.getValue()
```


Gets the AAC profile.

**Return Value**

AAC Current AAC profile.

<span id="MixedStreamVideoCodecType"></span>
# MixedStreamVideoCodecType

```java
public enum com.ss.bytertc.engine.live.MixedStreamVideoCodecType
```


The video codec.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIXED_STREAM_VIDEO_CODEC_TYPE_H264 |H264 |(Default) H.264 format. |
|MIXED_STREAM_VIDEO_CODEC_TYPE_BYTEVC1 |ByteVC1 |ByteVC1 format. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamVideoCodecType |[MixedStreamVideoCodecType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamVideoCodecType-mixedstreamvideocodectype) |
|String |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamVideoCodecType-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamVideoCodecType-mixedstreamvideocodectype"></span>
### MixedStreamVideoCodecType

```java
public com.ss.bytertc.engine.live.MixedStreamVideoCodecType.MixedStreamVideoCodecType(String value)
```


Sets the video codec.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |String |The video codec. See [MixedStreamVideoCodecType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamVideoCodecType). The default value is `0`. It's recommended to be set.<br><br>The video codec of WTN stream can only be set as `0`, indicating H264.<br><br>This parameter cannot be updated during the task. |


<span id="MixedStreamVideoCodecType-getvalue"></span>
### getValue

```java
public String com.ss.bytertc.engine.live.MixedStreamVideoCodecType.getValue()
```


Get the video codec.

**Return Value**

Current video codec.

<span id="UserOnlineStatus"></span>
# UserOnlineStatus

```java
public class com.ss.bytertc.engine.type.UserOnlineStatus
```


User online status

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[USER_ONLINE_STATUS_OFFLINE](https://docs.byteplus.com/en/docs/12/14169#UserOnlineStatus-user_online_status_offline) |
|int |1 |[USER_ONLINE_STATUS_ONLINE](https://docs.byteplus.com/en/docs/12/14169#UserOnlineStatus-user_online_status_online) |
|int |2 |[USER_ONLINE_STATUS_UNREACHABLE](https://docs.byteplus.com/en/docs/12/14169#UserOnlineStatus-user_online_status_unreachable) |


<span id="instructions"></span>
## Instructions

<span id="UserOnlineStatus-user_online_status_offline"></span>
### USER_ONLINE_STATUS_OFFLINE

```java
public static final int com.ss.bytertc.engine.type.UserOnlineStatus.USER_ONLINE_STATUS_OFFLINE = 0
```


Counterpart user is offline

Counterpart user has called `logout`, or has not called `login` to sign in

<span id="UserOnlineStatus-user_online_status_online"></span>
### USER_ONLINE_STATUS_ONLINE

```java
public static final int com.ss.bytertc.engine.type.UserOnlineStatus.USER_ONLINE_STATUS_ONLINE = 1
```


The peer user is online

The peer user calls `login` to sign in, and the connection status is normal.

<span id="UserOnlineStatus-user_online_status_unreachable"></span>
### USER_ONLINE_STATUS_UNREACHABLE

```java
public static final int com.ss.bytertc.engine.type.UserOnlineStatus.USER_ONLINE_STATUS_UNREACHABLE = 2
```


Unable to get the online state of the peer user

Returned when a cascade error occurs and the online state of the peer user is abnormal

<span id="VideoDecoderConfig"></span>
# VideoDecoderConfig

```java
public enum com.ss.bytertc.engine.video.VideoDecoderConfig
```


Video decoding method

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VIDEO_DECODER_CONFIG_RAW |0 |Enable SDK internal decoding, only returns the decoded data via callback |
|VIDEO_DECODER_CONFIG_ENCODE |1 |Turn on custom decoding, only callback the data before decoding |
|VIDEO_DECODER_CONFIG_BOTH |2 |Enable SDK internal decoding, and call back the data before and after decoding at the same time |


<span id="PositionInfo"></span>
# PositionInfo

```java
public class com.ss.bytertc.engine.data.PositionInfo
```


Information on the user's position in the rectangular coordinate system for the spatial audio.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|Position |\- |[position](https://docs.byteplus.com/en/docs/12/14169#PositionInfo-position) |
|HumanOrientation |\- |[orientation](https://docs.byteplus.com/en/docs/12/14169#PositionInfo-orientation) |


<span id="instructions"></span>
## Instructions

<span id="PositionInfo-position"></span>
### position

```java
public Position com.ss.bytertc.engine.data.PositionInfo.position
```


3D coordinate values of the user's position in the rectangular coordinate system for the spatial audio. You need to build your own rectangular coordinate system. Refer to [Position](https://docs.byteplus.com/en/docs/12/14169#Position) for details.

<span id="PositionInfo-orientation"></span>
### orientation

```java
public HumanOrientation com.ss.bytertc.engine.data.PositionInfo.orientation
```


Information on the three\-dimensional orientation of the user in the rectangular coordinate system for the spatial audio. Any two of the 3D coordinate vectors of the user's position need to be perpendicular to each other. Refer to [HumanOrientation](https://docs.byteplus.com/en/docs/12/14169#HumanOrientation) for details.

<span id="LocalStreamStats"></span>
# LocalStreamStats

```java
public class com.ss.bytertc.engine.type.LocalStreamStats
```


Local audio/video stream statistics and network status, the reference period is 2s.

After the local user publishes the audio/video stream successfully, the SDK will periodically notify the local user through `onLocalStreamStats` the transmission status of the published audio/video stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|LocalAudioStats |\- |[audioStats](https://docs.byteplus.com/en/docs/12/14169#LocalStreamStats-audiostats) |
|LocalVideoStats |\- |[videoStats](https://docs.byteplus.com/en/docs/12/14169#LocalStreamStats-videostats) |
|boolean |\- |[isScreen](https://docs.byteplus.com/en/docs/12/14169#LocalStreamStats-isscreen) |
|int |\- |[deprecated] [txQuality](https://docs.byteplus.com/en/docs/12/14169#LocalStreamStats-txquality) |
|int |\- |[deprecated] [rxQuality](https://docs.byteplus.com/en/docs/12/14169#LocalStreamStats-rxquality) |


<span id="instructions"></span>
## Instructions

<span id="LocalStreamStats-audiostats"></span>
### audioStats

```java
public LocalAudioStats com.ss.bytertc.engine.type.LocalStreamStats.audioStats
```


For statistics on audio streams sent by local devices. See [LocalAudioStats](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats).

<span id="LocalStreamStats-videostats"></span>
### videoStats

```java
public LocalVideoStats com.ss.bytertc.engine.type.LocalStreamStats.videoStats
```


For statistics on video streams sent by local devices. See [LocalVideoStats](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStats).

<span id="LocalStreamStats-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.type.LocalStreamStats.isScreen
```


Reserved field. Ignore the value returned in this field.

<span id="LocalStreamStats-txquality"></span>
### txQuality

```java
public int com.ss.bytertc.engine.type.LocalStreamStats.txQuality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onnetworkquality) instead.


For local media uplink network quality. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality).

<span id="LocalStreamStats-rxquality"></span>
### rxQuality

```java
public int com.ss.bytertc.engine.type.LocalStreamStats.rxQuality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onnetworkquality) instead.


Local media downlink network quality. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality).

<span id="VoiceEqualizationConfig"></span>
# VoiceEqualizationConfig

```java
public class com.ss.bytertc.engine.type.VoiceEqualizationConfig
```


Voice equalization effect.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|VoiceEqualizationBandFrequency |\- |[frequency](https://docs.byteplus.com/en/docs/12/14169#VoiceEqualizationConfig-frequency) |
|int |\- |[gain](https://docs.byteplus.com/en/docs/12/14169#VoiceEqualizationConfig-gain) |


<span id="instructions"></span>
## Instructions

<span id="VoiceEqualizationConfig-frequency"></span>
### frequency

```java
public VoiceEqualizationBandFrequency com.ss.bytertc.engine.type.VoiceEqualizationConfig.frequency
```


Frequency band. See [VoiceEqualizationBandFrequency](https://docs.byteplus.com/en/docs/12/14169#VoiceEqualizationBandFrequency).

<span id="VoiceEqualizationConfig-gain"></span>
### gain

```java
public int com.ss.bytertc.engine.type.VoiceEqualizationConfig.gain
```


Gain of the frequency band in dB. The range is `[-15, 15]`.

<span id="MixedStreamPushTargetConfig"></span>
# MixedStreamPushTargetConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamPushTargetConfig
```


Configuration of the mixing stream task

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|MixedStreamPushTargetType |MixedStreamPushTargetType.PUSH_TO_CDN |[pushTargetType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-pushtargettype) |
|String |"" |[pushCDNURL](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-pushcdnurl) |
|String |"" |[pushWTNStreamID](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-pushwtnstreamid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamPushTargetConfig |[MixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-mixedstreampushtargetconfig) |
|MixedStreamPushTargetConfig |[MixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-mixedstreampushtargetconfig-2) |
|int |[getMixedStreamPushTargetTypePushTargetType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-getmixedstreampushtargettypepushtargettype) |
|String |[getMixedStreamPushTargetTypePushCDNURL](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-getmixedstreampushtargettypepushcdnurl) |
|String |[getMixedStreamPushTargetTypePushWTNStreamID](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushTargetConfig-getmixedstreampushtargettypepushwtnstreamid) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamPushTargetConfig-pushtargettype"></span>
### pushTargetType

```java
public MixedStreamPushTargetType com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.pushTargetType = MixedStreamPushTargetType.PUSH_TO_CDN
```


The push task type.

<span id="MixedStreamPushTargetConfig-pushcdnurl"></span>
### pushCDNURL

```java
public String com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.pushCDNURL = ""
```


Sets the URL for the mixed stream to be pushed to. Only supports live transcoding via RTMP. The URL should match the regular expression `/^rtmps?:\\/\\//`. It's recommended to be set.

This parameter cannot be updated while pushing stream to the CDN.

<span id="MixedStreamPushTargetConfig-pushwtnstreamid"></span>
### pushWTNStreamID

```java
public String com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.pushWTNStreamID = ""
```


The WTN stream ID. This parameter is not supported for mixing\-stream stream tasks.

<span id="instructions"></span>
## Instructions

<span id="MixedStreamPushTargetConfig-mixedstreampushtargetconfig"></span>
### MixedStreamPushTargetConfig

```java
public com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.MixedStreamPushTargetConfig(
    MixedStreamPushTargetType targetType,
    String pushUrl,
    String pushStreamId
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|targetType |MixedStreamPushTargetType |\- |
|pushUrl |String |\- |
|pushStreamId |String |\- |


<span id="MixedStreamPushTargetConfig-mixedstreampushtargetconfig-2"></span>
### MixedStreamPushTargetConfig

```java
public com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.MixedStreamPushTargetConfig()
```


<span id="MixedStreamPushTargetConfig-getmixedstreampushtargettypepushtargettype"></span>
### getMixedStreamPushTargetTypePushTargetType

```java
public int com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.getMixedStreamPushTargetTypePushTargetType()
```


<span id="MixedStreamPushTargetConfig-getmixedstreampushtargettypepushcdnurl"></span>
### getMixedStreamPushTargetTypePushCDNURL

```java
public String com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.getMixedStreamPushTargetTypePushCDNURL()
```


<span id="MixedStreamPushTargetConfig-getmixedstreampushtargettypepushwtnstreamid"></span>
### getMixedStreamPushTargetTypePushWTNStreamID

```java
public String com.ss.bytertc.engine.live.MixedStreamPushTargetConfig.getMixedStreamPushTargetTypePushWTNStreamID()
```


<span id="MixedStreamTaskEvent"></span>
# MixedStreamTaskEvent

```java
public enum com.ss.bytertc.engine.live.MixedStreamTaskEvent
```


Stream mixing and pushing status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|START_SUCCESS |1 |Request to start the task to push streams to CDN |
|START_FAILED |2 |Failed to start the task to push streams to CDN |
|UPDATE_SUCCESS |3 |Request to update the configuration for the task to push streams to CDN |
|UPDATE_FAILED |4 |Failed to update the configuration for the task to push streams to CDN |
|STOP_SUCCESS |5 |the task to push streams to CDN stopped |
|STOP_FAILED |6 |Failed to stop the task to push streams to CDN |
|WARNING |7 |Warnings. |


<span id="ChannelProfile"></span>
# ChannelProfile

```java
public enum com.ss.bytertc.engine.type.ChannelProfile
```


Room profile

Choose an appropriate room\-profile option to meet the requirement of the scenario for media encoding algorithm, video profiles, and network configurations.

Call `setAudioProfile` to apply another audio quality option.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|CHANNEL_PROFILE_COMMUNICATION |0 |General mode by default<br><br>&nbsp;<br><br>It is equivalent to `CHANNEL_PROFIEL_MEETING(16)`.<br><br>&nbsp;<br><br>Contact us to alter the default settings. |
|CHANNEL_PROFILE_GAME |2 |Game voice mode. Low consumption of computing resources and network data<br><br>&nbsp;<br><br>Additional performance optimizations have been made for low\-end devices:<br><br><br>&nbsp;<br><br>* Encodes frame length 40/60 for some low\-end models.<br><br>* Disables software 3A audio processing for some low\-end models.<br><br>   Enhance iOS Compatibility with other screen recordings to avoid audio recordings being interrupted by RTC. |
|CHANNEL_PROFILE_CLOUD_GAME |3 |Cloud game mode.<br><br>&nbsp;<br><br>Use this mode for game App requiring low latency.<br><br>&nbsp;<br><br>During poor network connection, communication experiences get worse with this mode. |
|CHANNEL_PROFILE_LOW_LATENCY |4 |Cloud render mode featuring extra\-low latency.<br><br>&nbsp;<br><br>Choose this mode if it is not a game App yet requires low latency.<br><br>&nbsp;<br><br>In this mode, latency will significantly decrease at the cost of lower audio quality as well as the bad performance with weak network signal. |
|CHANNEL_PROFILE_CHAT_ROOM |6 |For video and audio chat rooms of 3 or more people |
|CHANNEL_PROFILE_INTERACTIVE_PODCAST |10 |For interactive podcasts that the host can have video and audio interactions with the audience. The voice mode is set to communication mode to avoid volume spiking and dipping acutely. |
|CHANNEL_PROFILE_CHORUS |12 |The online\-chorusing scenario with high\-quality audio and low latency. Contact the technical specialists before using the value. |
|CHANNEL_PROFILE_GAME_STREAMING |14 |For scenarios of streaming live videos to only one client on the LAN. It can be applied to devices on the Internet or LAN. |
|CHANNEL_PROFIEL_MEETING |16 |For meeting Apps installed on personal devices |
|CHANNEL_PROFILE_MEETING_ROOM |17 |For meeting Apps installed on terminals of meeting rooms, such as Rooms. |
|CHANNEL_PROFILE_CLASSROOM |18 |For the online classrooms and lectures that over 10 participants in the room are allowed to join the video chat. |
|CHANNEL_PROFILE_CALL |19 |Focus on smoothness, the default video bitrate is lower. |
|CHANNEL_PROFILE_LIVE |20 |Focus on quality, the default video bitrate is higher. |


<span id="IAudioFrame"></span>
# IAudioFrame

```java
public interface com.ss.bytertc.engine.utils.IAudioFrame
```


Audio data

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|long |[timestamp_us](https://docs.byteplus.com/en/docs/12/14169#IAudioFrame-timestamp_us) |
|AudioSampleRate |[sample_rate](https://docs.byteplus.com/en/docs/12/14169#IAudioFrame-sample_rate) |
|AudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14169#IAudioFrame-channel) |
|ByteBuffer |[getDataBuffer](https://docs.byteplus.com/en/docs/12/14169#IAudioFrame-getdatabuffer) |
|int |[data_size](https://docs.byteplus.com/en/docs/12/14169#IAudioFrame-data_size) |
|AudioFrameType |[frame_type](https://docs.byteplus.com/en/docs/12/14169#IAudioFrame-frame_type) |
|void |[release](https://docs.byteplus.com/en/docs/12/14169#IAudioFrame-release) |


<span id="instructions"></span>
## Instructions

<span id="IAudioFrame-timestamp_us"></span>
### timestamp_us

```java
long com.ss.bytertc.engine.utils.IAudioFrame.timestamp_us()
```


Get the audio timestamp.

**Return Value**

Audio timestamp in microseconds.

<span id="IAudioFrame-sample_rate"></span>
### sample_rate

```java
AudioSampleRate com.ss.bytertc.engine.utils.IAudioFrame.sample_rate()
```


Get the audio sample rate. See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/14169#AudioSampleRate).

**Return Value**

AudioSampleRate

<span id="IAudioFrame-channel"></span>
### channel

```java
AudioChannel com.ss.bytertc.engine.utils.IAudioFrame.channel()
```


Get the audio channel. See [AudioChannel](https://docs.byteplus.com/en/docs/12/14169#AudioChannel).

**Return Value**

Audio channel

**Notes**

For dual channels, the audio frames are interleaved.

<span id="IAudioFrame-getdatabuffer"></span>
### getDataBuffer

```java
ByteBuffer com.ss.bytertc.engine.utils.IAudioFrame.getDataBuffer()
```


Get the audio frame's temporary storage address

**Return Value**

Audio frame's ByteBuffer

<span id="IAudioFrame-data_size"></span>
### data_size

```java
int com.ss.bytertc.engine.utils.IAudioFrame.data_size()
```


Get audio frame data size.

**Return Value**

Audio frame data size in bytes.

<span id="IAudioFrame-frame_type"></span>
### frame_type

```java
AudioFrameType com.ss.bytertc.engine.utils.IAudioFrame.frame_type()
```


Get audio frame type, only PCM is supported currently. See [AudioFrameType](https://docs.byteplus.com/en/docs/12/14169#AudioFrameType).

**Return Value**

Audio frame type.

<span id="IAudioFrame-release"></span>
### release

```java
void com.ss.bytertc.engine.utils.IAudioFrame.release()
```


Release audio frame.

<span id="ForwardStreamStateInfo"></span>
# ForwardStreamStateInfo

```java
public class com.ss.bytertc.engine.data.ForwardStreamStateInfo
```


State and error for each room during relaying

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamStateInfo-roomid) |
|ForwardStreamState |\- |[state](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamStateInfo-state) |
|ForwardStreamError |\- |[error](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamStateInfo-error) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamStateInfo-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.data.ForwardStreamStateInfo.roomId
```


ID of the room where the media stream aims to relay to

An Empty string is for all rooms.

<span id="ForwardStreamStateInfo-state"></span>
### state

```java
public ForwardStreamState com.ss.bytertc.engine.data.ForwardStreamStateInfo.state
```


State of the room during relaying. Refer to [ForwardStreamState](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamState) for more information.

<span id="ForwardStreamStateInfo-error"></span>
### error

```java
public ForwardStreamError com.ss.bytertc.engine.data.ForwardStreamStateInfo.error
```


Error code from the room during relaying. Refer to [ForwardStreamError](https://docs.byteplus.com/en/docs/12/14169#ForwardStreamError) for more information.

<span id="RemoteVideoConfig"></span>
# RemoteVideoConfig

```java
public class com.ss.bytertc.engine.data.RemoteVideoConfig
```


Information on remote video frame

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[width](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoConfig-width) |
|int |0 |[height](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoConfig-height) |
|int |0 |[framerate](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoConfig-framerate) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|RemoteVideoConfig |[RemoteVideoConfig](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoConfig-remotevideoconfig) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoConfig-width"></span>
### width

```java
public int com.ss.bytertc.engine.data.RemoteVideoConfig.width = 0
```


Width of the video frame in px

<span id="RemoteVideoConfig-height"></span>
### height

```java
public int com.ss.bytertc.engine.data.RemoteVideoConfig.height = 0
```


Height of the video frame in px

<span id="RemoteVideoConfig-framerate"></span>
### framerate

```java
public int com.ss.bytertc.engine.data.RemoteVideoConfig.framerate = 0
```


Expected maximum frame rate of the subscribed stream in fps. The default value is 0, which represents full\-frame\-rate, values greater than 0 are valid.

If the frame rate of the stream published is higher than the value set by the subscriber, the subscriber receives the video of the frame rate set by this API; if the frame rate of the stream published is lower than the value set by the subscriber, the subscriber receives the video of the same frame rate of the video published.

Only valid if the stream is coded with SVC technique.

<span id="instructions"></span>
## Instructions

<span id="RemoteVideoConfig-remotevideoconfig"></span>
### RemoteVideoConfig

```java
public com.ss.bytertc.engine.data.RemoteVideoConfig.RemoteVideoConfig(
    int width,
    int height,
    int framerate
)
```


Settings of remote video frame

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|width |int |Width of the video frame in px |
|height |int |Height of the video frame in px |
|framerate |int |Expected maximum frame rate of the subscribed stream in fps. The default value is 0, which represents full\-frame\-rate, values greater than 0 are valid.<br><br>&nbsp;<br><br>If the frame rate of the stream published is higher than the value set by the subscriber, the subscriber receives the video of the frame rate set by this API; if the frame rate of the stream published is lower than the value set by the subscriber, the subscriber receives the video of the same frame rate of the video published.<br><br>&nbsp;<br><br>Only valid if the stream is coded with SVC technique. |


<span id="PauseResumeControlMediaType"></span>
# PauseResumeControlMediaType

```java
public enum com.ss.bytertc.engine.type.PauseResumeControlMediaType
```


Type of the stream to be paused/resumed

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO |0 |Only control audio, not affect video |
|VIDEO |1 |Only control video, not affect audio |
|AUDIO_AND_VIDEO |2 |Simultaneous control of audio and video |


<span id="RTCEncodedVideoFrame"></span>
# RTCEncodedVideoFrame

```java
public class com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame
```


Information about video frames

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|ByteBuffer |\- |[buffer](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-buffer) |
|long |\- |[timestampUs](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-timestampus) |
|long |\- |[timestampDtsUs](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-timestampdtsus) |
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-height) |
|VideoCodecType |\- |[videoCodecType](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-videocodectype) |
|VideoPictureType |\- |[videoPictureType](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-videopicturetype) |
|VideoRotation |\- |[videoRotation](https://docs.byteplus.com/en/docs/12/14169#RTCEncodedVideoFrame-videorotation) |


<span id="instructions"></span>
## Instructions

<span id="RTCEncodedVideoFrame-buffer"></span>
### buffer

```java
public final ByteBuffer com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.buffer
```


The pointer to the video frame

The buffer must be Direct. And the buffer size is its capacity.

<span id="RTCEncodedVideoFrame-timestampus"></span>
### timestampUs

```java
public long com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.timestampUs
```


Video capture timestamp in microseconds

<span id="RTCEncodedVideoFrame-timestampdtsus"></span>
### timestampDtsUs

```java
public long com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.timestampDtsUs
```


Video encoding timestamp in microseconds

<span id="RTCEncodedVideoFrame-width"></span>
### width

```java
public int com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.width
```


Width of the video in px

<span id="RTCEncodedVideoFrame-height"></span>
### height

```java
public int com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.height
```


Height of the video in px

<span id="RTCEncodedVideoFrame-videocodectype"></span>
### videoCodecType

```java
public VideoCodecType com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.videoCodecType
```


Video encoding type. See [VideoCodecType](https://docs.byteplus.com/en/docs/12/14169#VideoCodecType)

<span id="RTCEncodedVideoFrame-videopicturetype"></span>
### videoPictureType

```java
public VideoPictureType com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.videoPictureType
```


Video compression picture type. See [VideoPictureType](https://docs.byteplus.com/en/docs/12/14169#VideoPictureType)

<span id="RTCEncodedVideoFrame-videorotation"></span>
### videoRotation

```java
public VideoRotation com.ss.bytertc.engine.mediaio.RTCEncodedVideoFrame.videoRotation
```


Video frame rotation angle, the default value is 0 degrees. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14169#VideoRotation)

<span id="AudioMixingState"></span>
# AudioMixingState

```java
public enum com.ss.bytertc.engine.data.AudioMixingState
```


Audio mix file playback status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_MIXING_STATE_PRELOADED |0 |Mix loaded |
|AUDIO_MIXING_STATE_PLAYING |1 |Mix is playing |
|AUDIO_MIXING_STATE_PAUSED |2 |Mix Pause |
|AUDIO_MIXING_STATE_STOPPED |3 |Mixing stopped |
|AUDIO_MIXING_STATE_FAILED |4 |Mix playback failed |
|AUDIO_MIXING_STATE_FINISHED |5 |End of mixing |
|AUDIO_MIXING_STATE_PCM_ENABLED |6 |Prepare PCM Mix |
|AUDIO_MIXING_STATE_PCM_DISABLED |7 |End of PCM mix playback |


<span id="RemoteAudioStats"></span>
# RemoteAudioStats

```java
public class com.ss.bytertc.engine.type.RemoteAudioStats
```


Remote audio stream statistics, reference period 2s.

After a local user subscribes to a remote audio stream successfully, the SDK periodically notifies the local user of the reception status of the subscribed audio stream during this reference period through `onRemoteStreamStats`. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |\- |[audioLossRate](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-audiolossrate) |
|float |\- |[receivedKBitrate](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-receivedkbitrate) |
|int |\- |[stallCount](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-stallcount) |
|int |\- |[stallDuration](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-stallduration) |
|long |\- |[e2eDelay](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-e2edelay) |
|int |\- |[playoutSampleRate](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-playoutsamplerate) |
|int |\- |[statsInterval](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-statsinterval) |
|int |\- |[rtt](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-rtt) |
|int |\- |[totalRtt](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-totalrtt) |
|int |\- |[quality](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-quality) |
|int |\- |[jitterBufferDelay](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-jitterbufferdelay) |
|int |\- |[numChannels](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-numchannels) |
|int |\- |[receivedSampleRate](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-receivedsamplerate) |
|int |\- |[frozenRate](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-frozenrate) |
|int |\- |[concealedSamples](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-concealedsamples) |
|int |\- |[concealmentEvent](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-concealmentevent) |
|int |\- |[decSampleRate](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-decsamplerate) |
|int |\- |[decDuration](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-decduration) |
|int |\- |[jitter](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-jitter) |
|double |\- |[decodeFrameRate](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStats-decodeframerate) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioStats-audiolossrate"></span>
### audioLossRate

```java
public float com.ss.bytertc.engine.type.RemoteAudioStats.audioLossRate
```


Audio packet loss rate. The audio downlink packet loss rate in the reference period. The value range is [0,1].

<span id="RemoteAudioStats-receivedkbitrate"></span>
### receivedKBitrate

```java
public float com.ss.bytertc.engine.type.RemoteAudioStats.receivedKBitrate
```


Receiving bit rate. The audio reception rate in the reference period in kbps.

<span id="RemoteAudioStats-stallcount"></span>
### stallCount

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.stallCount
```


Number of audio stalls.

<span id="RemoteAudioStats-stallduration"></span>
### stallDuration

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.stallDuration
```


Audio stall duration. Stall duration in the reference period in ms.

<span id="RemoteAudioStats-e2edelay"></span>
### e2eDelay

```java
public long com.ss.bytertc.engine.type.RemoteAudioStats.e2eDelay
```


End\-to\-end latency at the user experience level. The delay from the start of encoding at the sending end to the start of decoding at the receiving end, in units of ms.

<span id="RemoteAudioStats-playoutsamplerate"></span>
### playoutSampleRate

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.playoutSampleRate
```


Play sample rate. Audio playback sample rate information within the reference period in Hz.

<span id="RemoteAudioStats-statsinterval"></span>
### statsInterval

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.statsInterval
```


Statistical interval. The interval of this reference period is in ms.

<span id="RemoteAudioStats-rtt"></span>
### rtt

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.rtt
```


Round\-trip time for client side to server level data transfer in ms.

<span id="RemoteAudioStats-totalrtt"></span>
### totalRtt

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.totalRtt
```


The sender\-server level\-the receiver\-link data transmission round\-trip time. The unit is ms.

<span id="RemoteAudioStats-quality"></span>
### quality

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.quality
```


The quality of the audio stream sent by the remote user. Value meaning reference [NetworkQuality](https://docs.byteplus.com/en/docs/12/14169#NetworkQuality).

<span id="RemoteAudioStats-jitterbufferdelay"></span>
### jitterBufferDelay

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.jitterBufferDelay
```


The delay caused by the introduction of the jitter buffer mechanism. The unit is ms.

<span id="RemoteAudioStats-numchannels"></span>
### numChannels

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.numChannels
```


Number of audio channels.

<span id="RemoteAudioStats-receivedsamplerate"></span>
### receivedSampleRate

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.receivedSampleRate
```


Audio reception sampling rate. Remote audio sampling rate information received within the reference period, in Hz.

<span id="RemoteAudioStats-frozenrate"></span>
### frozenRate

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.frozenRate
```


The accumulated length of audio stuttering occurs after the remote user joins the room as a percentage of the total effective length of the audio. The effective duration of audio refers to the duration of audio other than stopping sending audio streams and disabling audio modules after remote users enter the room to publish audio streams.

<span id="RemoteAudioStats-concealedsamples"></span>
### concealedSamples

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.concealedSamples
```


Audio packet loss compensation (PLC) total number of sample points.

<span id="RemoteAudioStats-concealmentevent"></span>
### concealmentEvent

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.concealmentEvent
```


Audio packet loss compensation (PLC) cumulative times.

<span id="RemoteAudioStats-decsamplerate"></span>
### decSampleRate

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.decSampleRate
```


Audio decoding sample rate. Audio decoding sample rate information in the reference period in Hz.

<span id="RemoteAudioStats-decduration"></span>
### decDuration

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.decDuration
```


Cumulative decoding time in seconds of the remote audio stream in this subscription.

<span id="RemoteAudioStats-jitter"></span>
### jitter

```java
public int com.ss.bytertc.engine.type.RemoteAudioStats.jitter
```


Audio downlink network jitter in ms.

<span id="RemoteAudioStats-decodeframerate"></span>
### decodeFrameRate

```java
public double com.ss.bytertc.engine.type.RemoteAudioStats.decodeFrameRate
```


Audio decode frame rate.

<span id="ScreenSharingParameters"></span>
# ScreenSharingParameters

```java
public class com.ss.bytertc.engine.video.ScreenSharingParameters
```


Screen sharing encoding parameter configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[maxWidth](https://docs.byteplus.com/en/docs/12/14169#ScreenSharingParameters-maxwidth) |
|int |0 |[maxHeight](https://docs.byteplus.com/en/docs/12/14169#ScreenSharingParameters-maxheight) |
|int |15 |[frameRate](https://docs.byteplus.com/en/docs/12/14169#ScreenSharingParameters-framerate) |
|int |\-1 |[bitrate](https://docs.byteplus.com/en/docs/12/14169#ScreenSharingParameters-bitrate) |
|int |0 |[minBitrate](https://docs.byteplus.com/en/docs/12/14169#ScreenSharingParameters-minbitrate) |


<span id="instructions"></span>
## Instructions

<span id="ScreenSharingParameters-maxwidth"></span>
### maxWidth

```java
public int com.ss.bytertc.engine.video.ScreenSharingParameters.maxWidth = 0
```


Screen capture code maximum width,

<span id="ScreenSharingParameters-maxheight"></span>
### maxHeight

```java
public int com.ss.bytertc.engine.video.ScreenSharingParameters.maxHeight = 0
```


Screen capture coding maximum height

<span id="ScreenSharingParameters-framerate"></span>
### frameRate

```java
public int com.ss.bytertc.engine.video.ScreenSharingParameters.frameRate = 15
```


Screen capture coded frame rate, unit fps

<span id="ScreenSharingParameters-bitrate"></span>
### bitrate

```java
public int com.ss.bytertc.engine.video.ScreenSharingParameters.bitrate = -1
```


Encoding bitrate in kbps of the screen\-sharing stream. `-1` for self\-adapted that SDK will choose the appropriate encoding rate according to the width and height for the stream.

<span id="ScreenSharingParameters-minbitrate"></span>
### minBitrate

```java
public int com.ss.bytertc.engine.video.ScreenSharingParameters.minBitrate = 0
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `minBitrate`.

It defaults to `0`.

It ranges within [0, bitrate). When `bitrate` < `minBitrate`, the bitrate is self\-adapted.

In the following circumstance, the assignment to this variable has no effect:


* When `bitrate` = `0`, the video encoding is disabled.

* When `bitrate` < `0`, the bitrate is self\-adapted.

    &nbsp;


<span id="videoorientation"></span>
# VideoOrientation

```java
public enum com.ss.bytertc.engine.data.VideoOrientation
```


Orientation of the video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ADAPTIVE |0 |(Default) The original orientation of the captured video frame. |
|PORTRAIT |1 |Portrait mode. Adjust the captured video frame to vertical layout in RTC SDK. |
|LANDSCAPE |2 |Landscape mode. Adjust the captured video frame to horizontal layout in RTC SDK. |


<span id="AudioRecordingConfig"></span>
# AudioRecordingConfig

```java
public class com.ss.bytertc.engine.data.AudioRecordingConfig
```


Audio recording configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[absoluteFileName](https://docs.byteplus.com/en/docs/12/14169#AudioRecordingConfig-absolutefilename) |
|AudioSampleRate |\- |[sampleRate](https://docs.byteplus.com/en/docs/12/14169#AudioRecordingConfig-samplerate) |
|AudioChannel |\- |[channel](https://docs.byteplus.com/en/docs/12/14169#AudioRecordingConfig-channel) |
|AudioFrameSource |\- |[frameSource](https://docs.byteplus.com/en/docs/12/14169#AudioRecordingConfig-framesource) |
|AudioQuality |\- |[quality](https://docs.byteplus.com/en/docs/12/14169#AudioRecordingConfig-quality) |


<span id="instructions"></span>
## Instructions

<span id="AudioRecordingConfig-absolutefilename"></span>
### absoluteFileName

```java
public String com.ss.bytertc.engine.data.AudioRecordingConfig.absoluteFileName
```


Absolute path of the recorded file, file name included. The App must have the write and read permission of the path.

The file format is restricted to .aac and .wav.

<span id="AudioRecordingConfig-samplerate"></span>
### sampleRate

```java
public AudioSampleRate com.ss.bytertc.engine.data.AudioRecordingConfig.sampleRate
```


See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/14169#AudioSampleRate).

<span id="AudioRecordingConfig-channel"></span>
### channel

```java
public AudioChannel com.ss.bytertc.engine.data.AudioRecordingConfig.channel
```


Number of audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/14169#AudioChannel).

If number of audio channels of recording is different than that of audio capture, the behavior is:


* If the number of capture is 1, and the number of recording is 2, the recorded audio is two\-channel data after copying mono\-channel data.

* If the number of capture is 2, and the number of recording is 1, the recorded audio is recorded by mixing the audio of the two channels.

    &nbsp;


<span id="framesource"></span>
### frameSource

```java
public AudioFrameSource com.ss.bytertc.engine.data.AudioRecordingConfig.frameSource
```


The source of the recording. See [AudioFrameSource](https://docs.byteplus.com/en/docs/12/14169#AudioFrameSource).

It is AUDIO_FRAME_SOURCE_MIXED(2) by default.

<span id="AudioRecordingConfig-quality"></span>
### quality

```java
public AudioQuality com.ss.bytertc.engine.data.AudioRecordingConfig.quality
```


Recording quality. Only valid for .aac file. See [AudioQuality](https://docs.byteplus.com/en/docs/12/14169#AudioQuality).

When the sample rate is 32kHz, the file (10min) size for different qualities are:

```Plain Text
   - low: 1.2MB;
   - [By Default] medium: 2MB;
   - high: 3.75MB;
   - ultra high: 7.5MB.
```


<span id="AudioRoute"></span>
# AudioRoute

```java
public enum com.ss.bytertc.engine.data.AudioRoute
```


Audio playback route

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_ROUTE_DEFAULT |\-1 |Default devices. The audio route set by `setDefaultAudioRoute`. |
|AUDIO_ROUTE_HEADSET |1 |Wired earphones |
|AUDIO_ROUTE_EARPIECE |2 |Earpiece. Built\-in device for calling |
|AUDIO_ROUTE_SPEAKERPHONE |3 |Speaker. Built\-in device for hands\-free audio playing |
|AUDIO_ROUTE_HEADSET_BLUETOOTH |4 |Bluetooth earphones |
|AUDIO_ROUTE_HEADSET_USB |5 |USB device |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#AudioRoute-value) |


<span id="instructions"></span>
## Instructions

<span id="AudioRoute-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.AudioRoute.value()
```


Get current value

**Return Value**

Current value

<span id="Position"></span>
# Position

```java
public class com.ss.bytertc.engine.data.Position
```


Coordinate value of the local user's position in the rectangular coordinate system in the RTC room.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |\- |[x](https://docs.byteplus.com/en/docs/12/14169#Position-x) |
|float |\- |[y](https://docs.byteplus.com/en/docs/12/14169#Position-y) |
|float |\- |[z](https://docs.byteplus.com/en/docs/12/14169#Position-z) |


<span id="instructions"></span>
## Instructions

<span id="Position-x"></span>
### x

```java
public float com.ss.bytertc.engine.data.Position.x
```


X\-coordinate

<span id="Position-y"></span>
### y

```java
public float com.ss.bytertc.engine.data.Position.y
```


Y\-coordinate

<span id="Position-z"></span>
### z

```java
public float com.ss.bytertc.engine.data.Position.z
```


Z\-coordinate

<span id="MediaInputType"></span>
# MediaInputType

```java
public enum com.ss.bytertc.engine.data.MediaInputType
```


Video Input Type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MEDIA_INPUT_TYPE_EXTERNAL |0 |Custom collection.<br><br>&nbsp;<br><br>After setting, you can push video frames directly to the SDK. |
|MEDIA_INPUT_TYPE_INTERNAL |1 |Internal SDK acquisition.<br><br>&nbsp;<br><br>This setting only switches to internal collection. You need to continue to call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startvideocapture) to open internal collection. |


<span id="MixedStreamLayoutRegionType"></span>
# MixedStreamLayoutRegionType

```java
public enum com.ss.bytertc.engine.live.MixedStreamLayoutRegionType
```


Stream mixing region type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIXED_STREAM_LAYOUT_REGION_TYPE_VIDEO_STREAM |0 |Video. |
|MIXED_STREAM_LAYOUT_REGION_TYPE_IMAGE |1 |Watermark image. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamLayoutRegionType |[MixedStreamLayoutRegionType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionType-mixedstreamlayoutregiontype) |
|int |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionType-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamLayoutRegionType-mixedstreamlayoutregiontype"></span>
### MixedStreamLayoutRegionType

```java
public com.ss.bytertc.engine.live.MixedStreamLayoutRegionType.MixedStreamLayoutRegionType(int value)
```


The contents of the layout section in the mixing stream, including video section and water mark section.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |The default value is `0` indicating videos.<br><br>This parameter is not supported for WTN stream tasks. |


<span id="MixedStreamLayoutRegionType-getvalue"></span>
### getValue

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionType.getValue()
```


Gets the stream mixing region type.

**Return Value**

Stream mixing region type

<span id="MediaPlayerCustomSourceSeekWhence"></span>
# MediaPlayerCustomSourceSeekWhence

```java
public enum com.ss.bytertc.engine.data.MediaPlayerCustomSourceSeekWhence
```


The starting position where audio data seeking begins.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SET |0 |Seeks from the head of the audio data, and the actual data offset after seeking is offset. |
|CUR |1 |Seeks from a specific position of the audio data stream, and the actual data offset after seeking is the current position plus offset. |
|END |2 |Seeks from the end of the audio data, and the actual data offset after seeking is the whole data length plus offset. |
|SIZE |3 |Returns the size of audio data. |


<span id="MixedStreamSEIContentMode"></span>
# MixedStreamSEIContentMode

```java
public enum com.ss.bytertc.engine.live.MixedStreamSEIContentMode
```


Content of SEI sent while pushing mixed stream to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIXED_STREAM_SEI_CONTENT_MODE_DEFAULT |0 |The video stream contains all the SEI information. Default value. |
|MIXED_STREAM_SEI_CONTENT_MODE_ENABLE_VOLUME_INDICATION |1 |The SEI data transmitted with non\-key frames contains volume information only.<br><br>&nbsp;<br><br>This parameter only takes effect after you set [enableVolumeIndication](https://docs.byteplus.com/en/docs/12/14169#MixedStreamControlConfig-enablevolumeindication) to true. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamSEIContentMode |[MixedStreamSEIContentMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamSEIContentMode-mixedstreamseicontentmode) |
|int |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamSEIContentMode-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamSEIContentMode-mixedstreamseicontentmode"></span>
### MixedStreamSEIContentMode

```java
public com.ss.bytertc.engine.live.MixedStreamSEIContentMode.MixedStreamSEIContentMode(int value)
```


Sets SEI content. See [MixedStreamSEIContentMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamSEIContentMode).

The default value is `0`, indicating that the SEI in the video stream is included.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |SEI content mode. |


<span id="MixedStreamSEIContentMode-getvalue"></span>
### getValue

```java
public int com.ss.bytertc.engine.live.MixedStreamSEIContentMode.getValue()
```


Gets the stream mixing SEI content mode.

**Return Value**

Stream mixing SEI content mode

<span id="StreamLayoutMode"></span>
# StreamLayoutMode

```java
public enum com.ss.bytertc.engine.live.StreamLayoutMode
```


Layout mode of the WTN stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUTO |0 |Auto |
|CUSTOM |2 |Manual |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|StreamLayoutMode |[StreamLayoutMode](https://docs.byteplus.com/en/docs/12/14169#StreamLayoutMode-streamlayoutmode) |
|int |[value](https://docs.byteplus.com/en/docs/12/14169#StreamLayoutMode-value) |


<span id="instructions"></span>
## Instructions

<span id="StreamLayoutMode-streamlayoutmode"></span>
### StreamLayoutMode

```java
public com.ss.bytertc.engine.live.StreamLayoutMode.StreamLayoutMode(int value)
```


Sets the layout mode of the WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |The layout mode. |


<span id="StreamLayoutMode-value"></span>
### value

```java
public int com.ss.bytertc.engine.live.StreamLayoutMode.value()
```


Gets the layout mode of the WTN stream.

**Return Value**

The layout mode of the WTN stream.

<span id="AudioQuality"></span>
# AudioQuality

```java
public enum com.ss.bytertc.engine.data.AudioQuality
```


Audio quality.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_QUALITY_LOW |0 |low quality |
|AUDIO_QUALITY_MEDIUM |1 |medium quality |
|AUDIO_QUALITY_HIGH |2 |high quality |
|AUDIO_QUALITY_ULTRA_HIGH |3 |ultra high quality |


<span id="AudioFrameCallbackMethod"></span>
# AudioFrameCallbackMethod

```java
public enum com.ss.bytertc.engine.data.AudioFrameCallbackMethod
```


Audio data callback method

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_FRAME_CALLBACK_RECORD |0 |The callback of the audio data recorded by local microphone. |
|AUDIO_FRAME_CALLBACK_PLAYBACK |1 |The callback of the mixed audio data of all remote users subscribed to by the local user. |
|AUDIO_FRAME_CALLBACK_MIXED |2 |The callback of the mixed audio data including the data recorded by local microphone and that of all remote users subscribed to by the local user. |
|AUDIO_FRAME_CALLBACK_REMOTE_USER |3 |The callback of the audio data before mixing of each remote user subscribed to by the local user. |
|AUDIO_FRAME_CALLBACK_CAPTURE_MIXED |5 |The callback of the mixed audio data including the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`. |


<span id="PublishStateChangeReason"></span>
# PublishStateChangeReason

```java
public enum com.ss.bytertc.engine.data.PublishStateChangeReason
```


Reason to change the publishing state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|PUBLISH |0 |Requested to publish. |
|UNPUBLISH |1 |Requested to remove. |
|NO_PUBLISH_PERMISSION |2 |The token the user used was not permitted to publish. |
|OVER_STREAM_PUBLISH_LIMIT |3 |The number of streams the user has published has exceeded the limit. |
|MULTIROOM_UNPUBLISH_FAILED |4 |The stream failed to remove from a room when you are publishing the stream in two or more rooms. |
|PUBLISH_STREAM_FAILED |5 |Failed to publish due to the server error. |
|PUBLISH_STREAM_FORBIDEN |6 |The user who tried to publish a stream is not a host. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) to change the user role. |
|USER_IN_PUBLISH |7 |The user who tried to publish a stream has already published a stream in a room. |
|STREAM_PUBLISH_BY_OTHER |8 |The user who tried to publish a stream has already published a stream in a room. |
|STREAM_ID_INVALID |9 |Stream ID is invalid. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static PublishStateChangeReason |[fromId](https://docs.byteplus.com/en/docs/12/14169#PublishStateChangeReason-fromid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#PublishStateChangeReason-value) |
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#PublishStateChangeReason-tostring) |


<span id="instructions"></span>
## Instructions

<span id="PublishStateChangeReason-fromid"></span>
### fromId

```java
public static PublishStateChangeReason com.ss.bytertc.engine.data.PublishStateChangeReason.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="PublishStateChangeReason-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.PublishStateChangeReason.value()
```


Get current value

**Return Value**

Current value

<span id="PublishStateChangeReason-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.data.PublishStateChangeReason.toString()
```


<span id="RtcUser"></span>
# RtcUser

```java
public class com.ss.bytertc.engine.type.RtcUser
```


user information

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[userId](https://docs.byteplus.com/en/docs/12/14169#RtcUser-userid) |
|String |\- |[metaData](https://docs.byteplus.com/en/docs/12/14169#RtcUser-metadata) |


<span id="instructions"></span>
## Instructions

<span id="RtcUser-userid"></span>
### userId

```java
public String com.ss.bytertc.engine.type.RtcUser.userId
```


User id

<span id="RtcUser-metadata"></span>
### metaData

```java
public String com.ss.bytertc.engine.type.RtcUser.metaData
```


Metadata

<span id="LogoutReason"></span>
# LogoutReason

```java
public class com.ss.bytertc.engine.type.LogoutReason
```


The reason why users logout

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[LOGOUT_REASON_LOGOUT](https://docs.byteplus.com/en/docs/12/14169#LogoutReason-logout_reason_logout) |
|int |1 |[LOGOUT_REASON_DUPLICATE_LOGIN](https://docs.byteplus.com/en/docs/12/14169#LogoutReason-logout_reason_duplicate_login) |


<span id="instructions"></span>
## Instructions

<span id="LogoutReason-logout_reason_logout"></span>
### LOGOUT_REASON_LOGOUT

```java
public static final int com.ss.bytertc.engine.type.LogoutReason.LOGOUT_REASON_LOGOUT = 0
```


Users choose to sign out by calling `logout` or terminating the engine.

<span id="LogoutReason-logout_reason_duplicate_login"></span>
### LOGOUT_REASON_DUPLICATE_LOGIN

```java
public static final int com.ss.bytertc.engine.type.LogoutReason.LOGOUT_REASON_DUPLICATE_LOGIN = 1
```


The current user is kicked out as another user signs in with the same user ID.

<span id="SourceCrop"></span>
# SourceCrop

```java
public class com.ss.bytertc.engine.live.SourceCrop
```


Crop configuration of the WTN stream

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|double |0.0 |[locationX](https://docs.byteplus.com/en/docs/12/14169#SourceCrop-locationx) |
|double |0.0 |[locationY](https://docs.byteplus.com/en/docs/12/14169#SourceCrop-locationy) |
|double |1.0 |[widthProportion](https://docs.byteplus.com/en/docs/12/14169#SourceCrop-widthproportion) |
|double |1.0 |[heightProportion](https://docs.byteplus.com/en/docs/12/14169#SourceCrop-heightproportion) |


<span id="instructions"></span>
## Instructions

<span id="SourceCrop-locationx"></span>
### locationX

```java
public double com.ss.bytertc.engine.live.SourceCrop.locationX = 0.0
```


The normalized scale of the upper\-left corner of the cropped video frame relative to the overall frame before cropping, in the range [0.0, 1.0)

<span id="SourceCrop-locationy"></span>
### locationY

```java
public double com.ss.bytertc.engine.live.SourceCrop.locationY = 0.0
```


The normalized scale of the upper\-left corner of the cropped video frame relative to the overall frame before cropping, in the range [0.0, 1.0)

<span id="SourceCrop-widthproportion"></span>
### widthProportion

```java
public double com.ss.bytertc.engine.live.SourceCrop.widthProportion = 1.0
```


The normalized ratio of the width of the video frame obtained after cropping to the overall frame before cropping, in the range (0.0, 1.0]

<span id="SourceCrop-heightproportion"></span>
### heightProportion

```java
public double com.ss.bytertc.engine.live.SourceCrop.heightProportion = 1.0
```


The normalized ratio of the height of the obtained video frame after cropping to the overall frame before cropping, in the range (0.0, 1.0]

<span id="SubscribeStateChangeReason"></span>
# SubscribeStateChangeReason

```java
public enum com.ss.bytertc.engine.data.SubscribeStateChangeReason
```


Reason to change the subscription state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SUBSCRIBE |0 |Requested to subscribe. |
|UNSUBSCRIBE |1 |Requested to unsubscribe. |
|REMOTE_PUBLISH |2 |The remote user published a stream. |
|REMOTE_UNPUBLISH |3 |The remote user removed a stream. |
|STREAM_FAILED_5XX |4 |Failed to subscribe due to the server error. The SDK will automatically retry. |
|STREAM_FAILED_404 |5 |Failed to subscribe since the stream to be subscribed to was not found in the room. The SDK will automatically retry the subscription. If the subscription still fails, we recommend you exit and retry. |
|OVER_STREAM_SUBSCRIBE_LIMIT |6 |The number of streams the user has subscribedd to has exceeded the limit. |
|NO_SUBSCRIBE_PERMISSION |7 |The user was not permitted to subscribe to the stream. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static SubscribeStateChangeReason |[fromId](https://docs.byteplus.com/en/docs/12/14169#SubscribeStateChangeReason-fromid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#SubscribeStateChangeReason-value) |
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#SubscribeStateChangeReason-tostring) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeStateChangeReason-fromid"></span>
### fromId

```java
public static SubscribeStateChangeReason com.ss.bytertc.engine.data.SubscribeStateChangeReason.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="SubscribeStateChangeReason-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.SubscribeStateChangeReason.value()
```


Get current value

**Return Value**

Current value

<span id="SubscribeStateChangeReason-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.data.SubscribeStateChangeReason.toString()
```


<span id="SimulcastStreamType"></span>
# SimulcastStreamType

```java
public enum com.ss.bytertc.engine.data.SimulcastStreamType
```


The preference for the quality of the subscribed stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SIMULCAST_STREAM_TYPE_WEAK |0 |The stream with the lowest quality, which has the lowest resolution. |
|SIMULCAST_STREAM_TYPE_LOW |1 |The stream with a low quality. |
|SIMULCAST_STREAM_TYPE_MID |2 |The stream with a medium quality. |
|SIMULCAST_STREAM_TYPE_HIGH |3 |The stream with the best quality. |


<span id="VideoDimensions-2"></span>
# VideoDimensions

```java
public class com.ss.bytertc.engine.video.VideoDimensions
```


Video encoding pixel

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#VideoDimensions-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#VideoDimensions-height) |


<span id="instructions"></span>
## Instructions

<span id="VideoDimensions-width"></span>
### width

```java
public int com.ss.bytertc.engine.video.VideoDimensions.width
```


Width

<span id="VideoDimensions-height"></span>
### height

```java
public int com.ss.bytertc.engine.video.VideoDimensions.height
```


High

<span id="MixedStreamAudioCodecType"></span>
# MixedStreamAudioCodecType

```java
public enum com.ss.bytertc.engine.live.MixedStreamAudioCodecType
```


The audio codec. Currently, the only value `0` indicates AAC.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIXED_STREAM_AUDIO_CODEC_TYPE_AAC |AAC |AAC format. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamAudioCodecType |[MixedStreamAudioCodecType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioCodecType-mixedstreamaudiocodectype) |
|String |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioCodecType-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamAudioCodecType-mixedstreamaudiocodectype"></span>
### MixedStreamAudioCodecType

```java
public com.ss.bytertc.engine.live.MixedStreamAudioCodecType.MixedStreamAudioCodecType(String value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |String |AAC profile. See [MixedStreamAudioCodecType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioCodecType). Currently, the only value `0` indicates AAC. |


<span id="MixedStreamAudioCodecType-getvalue"></span>
### getValue

```java
public String com.ss.bytertc.engine.live.MixedStreamAudioCodecType.getValue()
```


Get the audio codec.

**Return Value**

The audio codec.

<span id="RoomEvent"></span>
# RoomEvent

```java
public enum com.ss.bytertc.engine.type.RoomEvent
```


Room event code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|USER_NOTIFY_STOP |\-2013 |When the number of people in the room exceeds 500, stop sending `onUserJoined` and `onUserLeave` callbacks to existing users in the room, and prompt all users in the room via broadcast. |
|FORBIDDEN |\-2012 |When the room or user is forbidden, notice forbidden time via onRoomEvent. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static RoomEvent |[valueOf](https://docs.byteplus.com/en/docs/12/14169#RoomEvent-valueof) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|RoomEvent |[RoomEvent](https://docs.byteplus.com/en/docs/12/14169#RoomEvent-roomevent) |
|int |[value](https://docs.byteplus.com/en/docs/12/14169#RoomEvent-value) |


<span id="instructions"></span>
## Instructions

<span id="RoomEvent-valueof"></span>
### valueOf

```java
public static RoomEvent com.ss.bytertc.engine.type.RoomEvent.valueOf(int value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |\- |


<span id="RoomEvent-roomevent"></span>
### RoomEvent

```java
public com.ss.bytertc.engine.type.RoomEvent.RoomEvent(int value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |\- |


<span id="RoomEvent-value"></span>
### value

```java
public int com.ss.bytertc.engine.type.RoomEvent.value()
```


<span id="AudioMixingError"></span>
# AudioMixingError

```java
public enum com.ss.bytertc.engine.data.AudioMixingError
```


Error code for audio mixing

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_MIXING_ERROR_OK |0 |OK |
|AUDIO_MIXING_ERROR_PRELOAD_FAILED |1 |Preload failed. Invalid path or the length exceeds 20s. |
|AUDIO_MIXING_ERROR_START_FAILED |2 |Mixing failed. Invalid path or fail to open the file. |
|AUDIO_MIXING_ERROR_ID_NOT_FOUND |3 |Invalid mixID |
|AUDIO_MIXING_ERROR_SET_POSITION_FAILED |4 |Invalid position |
|AUDIO_MIXING_ERROR_INVALID_VOLUME |5 |Invalid volume. The range is [0, 400]. |
|AUDIO_MIXING_ERROR_LOAD_CONFLICT |6 |Another file was preloaded for mixing. Call unloadAudioMixing first. |
|AUDIO_MIXING_ERROR_ID_TYPE_NOT_MATCH |7 |Do not support the mix type. |
|AUDIO_MIXING_ERROR_ID_TYPE_INVALID_PITCH |8 |Invalid pitch value. |
|AUDIO_MIXING_ERROR_INVALID_AUDIO_TRACK |9 |Invalid audio track. |
|AUDIO_MIXING_ERROR_IS_STARTING |10 |Mixing starting. |
|AUDIO_MIXING_ERROR_INVALID_PLAYBACK_SPEED |11 |Invalid playback speed |


<span id="SnapshotErrorCode"></span>
# SnapshotErrorCode

```java
public enum com.ss.bytertc.engine.type.SnapshotErrorCode
```


Snapshot error codes

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|OK |0 |Success. |
|CREATE_FAIL |\-1 |Failure. Fails to generate the image data or encode RGBA. |
|STREAM_INVALID |\-2 |Failure. The stream is invalid. |
|TIMEOUT |\-3 |Failure. Snapshot timeout, with a default timeout of 1 second. |
|FILE_SAVE_ERROR |\-4 |Failure. Fails to save the image. |


<span id="AudioSelectionPriority"></span>
# AudioSelectionPriority

```java
public enum com.ss.bytertc.engine.type.AudioSelectionPriority
```


User priority in the audio selection

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_SELECTION_PRIORITY_NORMAL |0 |Normally, whether the stream can be subscribed is determined by the result of audio selection. |
|AUDIO_SELECTION_PRIORITY_HIGIH |1 |High priority with which the stream can skip audio selection and always be subscribable. |


<span id="IVideoFrame"></span>
# IVideoFrame

```java
public interface com.ss.bytertc.engine.video.IVideoFrame
```


Video frame interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|VideoBufferType |[bufferType](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-buffertype) |
|VideoPixelFormat |[pixelFormat](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-pixelformat) |
|VideoContentType |[contentType](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-contenttype) |
|long |[timestampUs](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-timestampus) |
|int |[width](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-height) |
|VideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-rotation) |
|CameraId |[cameraId](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-cameraid) |
|int |[numberOfPlanes](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-numberofplanes) |
|ByteBuffer |[planeData](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-planedata) |
|int |[planeStride](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-planestride) |
|ByteBuffer |[seiData](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-seidata) |
|int |[textureId](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-textureid) |
|float[] |[textureMatrix](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-texturematrix) |
|EGLContext |[eglContext](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-eglcontext) |
|void |[addRef](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-addref) |
|long |[releaseRef](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame-releaseref) |


<span id="instructions"></span>
## Instructions

<span id="IVideoFrame-buffertype"></span>
### bufferType

```java
VideoBufferType com.ss.bytertc.engine.video.IVideoFrame.bufferType()
```


Gets video buffer type, see [VideoBufferType](https://docs.byteplus.com/en/docs/12/14169#VideoBufferType)

<span id="IVideoFrame-pixelformat"></span>
### pixelFormat

```java
VideoPixelFormat com.ss.bytertc.engine.video.IVideoFrame.pixelFormat()
```


Gets video frame's pixel format, see [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14169#VideoPixelFormat)

<span id="IVideoFrame-contenttype"></span>
### contentType

```java
VideoContentType com.ss.bytertc.engine.video.IVideoFrame.contentType()
```


Gets video content type.

**Return Value**

See [VideoContentType](https://docs.byteplus.com/en/docs/12/14169#VideoContentType).

<span id="IVideoFrame-timestampus"></span>
### timestampUs

```java
long com.ss.bytertc.engine.video.IVideoFrame.timestampUs()
```


Gets video frame timestamp in microseconds

<span id="IVideoFrame-width"></span>
### width

```java
int com.ss.bytertc.engine.video.IVideoFrame.width()
```


Gets video frame width

<span id="IVideoFrame-height"></span>
### height

```java
int com.ss.bytertc.engine.video.IVideoFrame.height()
```


Gets video frame height

<span id="IVideoFrame-rotation"></span>
### rotation

```java
VideoRotation com.ss.bytertc.engine.video.IVideoFrame.rotation()
```


Gets video frame rotation angle

<span id="IVideoFrame-cameraid"></span>
### cameraId

```java
CameraId com.ss.bytertc.engine.video.IVideoFrame.cameraId()
```


Get camera position info of the video frame, see [CameraId](https://docs.byteplus.com/en/docs/12/14169#CameraId)

<span id="IVideoFrame-numberofplanes"></span>
### numberOfPlanes

```java
int com.ss.bytertc.engine.video.IVideoFrame.numberOfPlanes()
```


Gets the number of video frame planes

<span id="IVideoFrame-planedata"></span>
### planeData

```java
ByteBuffer com.ss.bytertc.engine.video.IVideoFrame.planeData(int planeIndex)
```


Gets array of video frame planes

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|planeIndex |int |Plane index |


<span id="IVideoFrame-planestride"></span>
### planeStride

```java
int com.ss.bytertc.engine.video.IVideoFrame.planeStride(int planeIndex)
```


Gets the length of memory between two lines of image data in video frame plane in bytes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|planeIndex |int |Plane index |


<span id="IVideoFrame-seidata"></span>
### seiData

```java
ByteBuffer com.ss.bytertc.engine.video.IVideoFrame.seiData()
```


Gets SEI data

<span id="IVideoFrame-textureid"></span>
### textureId

```java
int com.ss.bytertc.engine.video.IVideoFrame.textureId()
```


Gets texture ID

<span id="IVideoFrame-texturematrix"></span>
### textureMatrix

```java
float[] com.ss.bytertc.engine.video.IVideoFrame.textureMatrix()
```


Gets texture matrix

<span id="IVideoFrame-eglcontext"></span>
### eglContext

```java
EGLContext com.ss.bytertc.engine.video.IVideoFrame.eglContext()
```


Gets the EGLContext

<span id="IVideoFrame-addref"></span>
### addRef

```java
void com.ss.bytertc.engine.video.IVideoFrame.addRef()
```


Increase the reference count of the video frame by 1.

**Notes**

If you want to asynchronously process the video frame (for example, switch the thread for rendering), you need to call this interface to increase the reference count. After the asynchronous processing is completed, you need to call `releaseRef` to reduce the reference count by 1.

<span id="IVideoFrame-releaseref"></span>
### releaseRef

```java
long com.ss.bytertc.engine.video.IVideoFrame.releaseRef()
```


Decrease the reference count of the video frame by 1.

**Notes**

When the reference count of a video frame is decreased to 0, the video frame object is released. After the video frame is released, it should not be used anymore.

<span id="MixedStreamRenderMode"></span>
# MixedStreamRenderMode

```java
public enum com.ss.bytertc.engine.live.MixedStreamRenderMode
```


The render mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIXED_STREAM_RENDER_MODE_HIDDEN |1 |(Default) Fill and Crop.<br><br>&nbsp;<br><br>The video frame is scaled with fixed aspect ratio, until it completely fills the canvas. The region of the video exceeding the canvas will be cropped. |
|MIXED_STREAM_RENDER_MODE_FIT |2 |Fit.<br><br>&nbsp;<br><br>The video frame is scaled with fixed aspect ratio, until it fits just within the canvas. Other part of the canvas is filled with the background color. |
|MIXED_STREAM_RENDER_MODE_ADAPTIVE |3 |Fill the canvas.<br><br>&nbsp;<br><br>The video frame is scaled to fill the canvas. During the process, the aspect ratio may change. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamRenderMode |[MixedStreamRenderMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamRenderMode-mixedstreamrendermode) |
|int |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamRenderMode-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamRenderMode-mixedstreamrendermode"></span>
### MixedStreamRenderMode

```java
public com.ss.bytertc.engine.live.MixedStreamRenderMode.MixedStreamRenderMode(int value)
```


Sets the render mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |See [MixedStreamRenderMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamRenderMode). The default value is `1` indicating the video frame is scaled with fixed aspect ratio. It's recommended to be set. |


<span id="MixedStreamRenderMode-getvalue"></span>
### getValue

```java
public int com.ss.bytertc.engine.live.MixedStreamRenderMode.getValue()
```


Gets the video rendering scale mode.

**Return Value**

Video rendering scale mode

<span id="ProcessorActionDomain"></span>
# ProcessorActionDomain

```java
public enum com.ss.bytertc.engine.data.ProcessorActionDomain
```


The effective range of the custom video preprocessor, including preview only, encode only, and both preview and encode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|PREVIEWANDENCODE |0 |The processed video frames are used for both local preview and pushing to the remote. |
|PREVIEW |1 |The processed video frames are used for local preview only. |
|ENCODE |2 |The processed video frames are used for pushing to the remote only. |


<span id="FaceDetectionResult"></span>
# FaceDetectionResult

```java
public class com.ss.bytertc.engine.video.FaceDetectionResult
```


Face Detection Result

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[detectResult](https://docs.byteplus.com/en/docs/12/14169#FaceDetectionResult-detectresult) |
|int |\- |[imageWidth](https://docs.byteplus.com/en/docs/12/14169#FaceDetectionResult-imagewidth) |
|int |\- |[imageHeight](https://docs.byteplus.com/en/docs/12/14169#FaceDetectionResult-imageheight) |
|Rectangle[] |\- |[faces](https://docs.byteplus.com/en/docs/12/14169#FaceDetectionResult-faces) |
|long |\- |[frameTimestampUs](https://docs.byteplus.com/en/docs/12/14169#FaceDetectionResult-frametimestampus) |


<span id="instructions"></span>
## Instructions

<span id="FaceDetectionResult-detectresult"></span>
### detectResult

```java
public int com.ss.bytertc.engine.video.FaceDetectionResult.detectResult
```


Face Detection Result


* 0: Success

* !0: Failure, see [Error Code Table](https://docs.byteplus.com/en/effects/docs/error-code-table)

    &nbsp;


<span id="imagewidth"></span>
### imageWidth

```java
public int com.ss.bytertc.engine.video.FaceDetectionResult.imageWidth
```


Width of the original image (px)

<span id="FaceDetectionResult-imageheight"></span>
### imageHeight

```java
public int com.ss.bytertc.engine.video.FaceDetectionResult.imageHeight
```


Height of the original image (px)

<span id="FaceDetectionResult-faces"></span>
### faces

```java
public Rectangle [] com.ss.bytertc.engine.video.FaceDetectionResult.faces
```


The face recognition rectangles. The length of the array is the same as the number of detected faces. See [Rectangle](https://docs.byteplus.com/en/docs/12/14169#Rectangle).

<span id="FaceDetectionResult-frametimestampus"></span>
### frameTimestampUs

```java
public long com.ss.bytertc.engine.video.FaceDetectionResult.frameTimestampUs
```


The time stamp of the video frame using face detection.

<span id="RemoteStreamKey"></span>
# RemoteStreamKey

```java
public class com.ss.bytertc.engine.data.RemoteStreamKey
```


Information about the remote stream.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamKey-roomid) |
|String |\- |[userId](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamKey-userid) |
|StreamIndex |\- |[streamIndex](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamKey-streamindex) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|String |[getRoomId](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamKey-getroomid) |
|String |[getUserId](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamKey-getuserid) |
|StreamIndex |[getStreamIndex](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamKey-getstreamindex) |
|boolean |[hasNullProperty](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamKey-hasnullproperty) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamKey-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.data.RemoteStreamKey.roomId
```


The ID of the room from which the stream was published.

<span id="RemoteStreamKey-userid"></span>
### userId

```java
public String com.ss.bytertc.engine.data.RemoteStreamKey.userId
```


The ID of the user who published the stream.

<span id="RemoteStreamKey-streamindex"></span>
### streamIndex

```java
public StreamIndex com.ss.bytertc.engine.data.RemoteStreamKey.streamIndex
```


Reserved field.

<span id="instructions"></span>
## Instructions

<span id="RemoteStreamKey-getroomid"></span>
### getRoomId

```java
public String com.ss.bytertc.engine.data.RemoteStreamKey.getRoomId()
```


Gets the room ID

<span id="RemoteStreamKey-getuserid"></span>
### getUserId

```java
public String com.ss.bytertc.engine.data.RemoteStreamKey.getUserId()
```


Gets the user ID

<span id="RemoteStreamKey-getstreamindex"></span>
### getStreamIndex

```java
public StreamIndex com.ss.bytertc.engine.data.RemoteStreamKey.getStreamIndex()
```


Reserved field.

<span id="RemoteStreamKey-hasnullproperty"></span>
### hasNullProperty

```java
public boolean com.ss.bytertc.engine.data.RemoteStreamKey.hasNullProperty()
```


Check the class has null property

<span id="VoiceReverbType"></span>
# VoiceReverbType

```java
public enum com.ss.bytertc.engine.type.VoiceReverbType
```


Reverb effect type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VOICE_REVERB_ORIGINAL |0 |Acoustic, no special effects |
|VOICE_REVERB_ECHO |1 |Echo |
|VOICE_REVERB_CONCERT |2 |Concert |
|VOICE_REVERB_ETHEREAL |3 |Ethereal |
|VOICE_REVERB_KTV |4 |Karaoke |
|VOICE_REVERB_STUDIO |5 |Recording studio |
|VOICE_REVERB_VIRTUAL_STEREO |6 |Virtual Stereo |
|VOICE_REVERB_SPACIOUS |7 |Spacious |
|VOICE_REVERB_3D |8 |3D vocal |


<span id="MixedStreamPushMode"></span>
# MixedStreamPushMode

```java
public enum com.ss.bytertc.engine.live.MixedStreamPushMode
```


The initiation mode for pushing the stream mixed on the server side to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ON_STREAM |0 |The initiation of a stream mixing task is dependent on a user actively publishing media streams. |
|ON_START_REQUEST |1 |Even if no user is actively publishing media streams, it is still possible to initiate a stream mixing task using a placeholder image.<br><br>&nbsp;<br><br>See [alternateImageURL](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-alternateimageurl) and [alternateImageFillMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig-alternateimagefillmode). |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamPushMode |[MixedStreamPushMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushMode-mixedstreampushmode) |
|int |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushMode-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamPushMode-mixedstreampushmode"></span>
### MixedStreamPushMode

```java
public com.ss.bytertc.engine.live.MixedStreamPushMode.MixedStreamPushMode(int value)
```


Sets whether to initiate a stream mixing task in the absence of any users publishing streams. It defaults to be dependent on a user actively publishing media streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |See [MixedStreamPushMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamPushMode).<br><br>&nbsp;<br><br>Once the stream mixing task is initiated, this parameter can not be updated any more. |


<span id="MixedStreamPushMode-getvalue"></span>
### getValue

```java
public int com.ss.bytertc.engine.live.MixedStreamPushMode.getValue()
```


Gets the initiation mode for pushing the stream mixed on the server side to CDN.

**Return Value**

The initiation mode for pushing the stream mixed on the server side to CDN.

<span id="MediaPlayerCustomSourceMode"></span>
# MediaPlayerCustomSourceMode

```java
public enum com.ss.bytertc.engine.data.MediaPlayerCustomSourceMode
```


Custom audio source mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|PUSH |0 |When you use the local PCM data, use this mode. |
|PULL |1 |When you use the audio data from local memory, use this mode. |


<span id="MixedStreamLayoutRegionImageWaterMarkConfig"></span>
# MixedStreamLayoutRegionImageWaterMarkConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamLayoutRegionImageWaterMarkConfig
```


Image parameters for stream mixing.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[imageWidth](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionImageWaterMarkConfig-imagewidth) |
|int |0 |[imageHeight](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionImageWaterMarkConfig-imageheight) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamLayoutRegionImageWaterMarkConfig-imagewidth"></span>
### imageWidth

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionImageWaterMarkConfig.imageWidth = 0
```


Sets the width of the original image.

<span id="MixedStreamLayoutRegionImageWaterMarkConfig-imageheight"></span>
### imageHeight

```java
public int com.ss.bytertc.engine.live.MixedStreamLayoutRegionImageWaterMarkConfig.imageHeight = 0
```


Sets the width of the original image.

<span id="AudioChannel"></span>
# AudioChannel

```java
public enum com.ss.bytertc.engine.data.AudioChannel
```


Audio channel

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_CHANNEL_AUTO |\-1 |Default value. Dual channels. |
|AUDIO_CHANNEL_MONO |1 |Mono channel. |
|AUDIO_CHANNEL_STEREO |2 |Dual channels. |


<span id="RemoteVideoStateChangeReason"></span>
# RemoteVideoStateChangeReason

```java
public enum com.ss.bytertc.engine.type.RemoteVideoStateChangeReason
```


Cause of remote video stream state change

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|REMOTE_VIDEO_STATE_CHANGE_REASON_INTERNAL |0 |Internal reasons |
|REMOTE_VIDEO_STATE_CHANGE_REASON_NETWORK_CONGESTION |1 |Network blocking |
|REMOTE_VIDEO_STATE_CHANGE_REASON_NETWORK_RECOVERY |2 |Network back to normal |
|REMOTE_VIDEO_STATE_CHANGE_REASON_LOCAL_MUTED |3 |Local user stops receiving remote video stream or local user disables video module |
|REMOTE_VIDEO_STATE_CHANGE_REASON_LOCAL_UNMUTED |4 |Local user resumes receiving remote video streams or local user enables video modules |
|REMOTE_VIDEO_STATE_CHANGE_REASON_REMOTE_MUTED |5 |The remote user stops sending the video stream or the remote user disables the video module |
|REMOTE_VIDEO_STATE_CHANGE_REASON_REMOTE_UNMUTED |6 |Remote user resumes sending video stream or remote user enables video module |
|REMOTE_VIDEO_STATE_CHANGE_REASON_REMOTE_OFFLINE |7 |Remote user leaves room. |


<span id="PerformanceAlarmReason"></span>
# PerformanceAlarmReason

```java
public enum com.ss.bytertc.engine.type.PerformanceAlarmReason
```


Reasons for performance\-related alarms

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BANDWIDTH_FALLBACKED |0 |The poor network causes the transmission performance to fall back. This reason is only received when sending performance fallback is turned on. |
|BANDWIDTH_RESUMED |1 |Network performance recovery, transmission performance rollback recovery. This reason is only received when sending performance fallback is turned on. |
|PERFORMANCE_FALLBACKED |2 |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance is insufficient;<br><br>&nbsp;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance is insufficient and the send performance fallback has occurred. |
|PERFORMANCE_RESUMED |3 |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance shortage has been restored;<br><br>&nbsp;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance shortage has been restored and the send performance fallback has occurred. Recovery. |


<span id="VideoDeviceType"></span>
# VideoDeviceType

```java
public enum com.ss.bytertc.engine.type.VideoDeviceType
```


Current audio device type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VIDEO_DEVICE_TYPE_UNKNOWN |\-1 |Unknown device type |
|VIDEO_DEVICE_TYPE_RENDER_DEVICE |0 |Audio Rendering Device Type |
|VIDEO_DEVICE_TYPE_CAPTURE_DEVICE |1 |Audio Acquisition Device Type |
|VIDEO_DEVICE_TYPE_SCREEN_CAPTURE_DEVICE |2 |Screen stream video devices |


<span id="DestInfo"></span>
# DestInfo

```java
public class com.ss.bytertc.engine.data.DestInfo
```


Target room information for stream pushing, specifying which room to push the media stream to and the user identity in that room.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#DestInfo-roomid) |
|String |\- |[userId](https://docs.byteplus.com/en/docs/12/14169#DestInfo-userid) |


<span id="instructions"></span>
## Instructions

<span id="DestInfo-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.data.DestInfo.roomId
```


Target room ID, specifying which room to push the media stream to.

<span id="DestInfo-userid"></span>
### userId

```java
public String com.ss.bytertc.engine.data.DestInfo.userId
```


User ID of the stream in the target room, users in the target room will see this ID as the stream publisher, and can use this ID to subscribe to the stream.

<span id="WTNSubscribeStateChangeReason"></span>
# WTNSubscribeStateChangeReason

```java
public enum com.ss.bytertc.engine.data.WTNSubscribeStateChangeReason
```


Reasons for change in WTN media stream's Subscription Status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SUBSCRIBE |0 |\- |
|UNSUBSCRIBE |1300 |\- |
|REMOTE_UNPUBLISH |1301 |\- |
|OVER_CLIENT_SUBSCRIBE_STREAM_LIMIT |1310 |\- |
|OVER_STREAM_SUBSCRIBE_USER_LIMIT |1311 |\- |
|OVER_STREAM_SUBSCRIBE_REQUEST_LIMIT |1312 |\- |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static WTNSubscribeStateChangeReason |[fromId](https://docs.byteplus.com/en/docs/12/14169#WTNSubscribeStateChangeReason-fromid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#WTNSubscribeStateChangeReason-value) |
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#WTNSubscribeStateChangeReason-tostring) |


<span id="instructions"></span>
## Instructions

<span id="WTNSubscribeStateChangeReason-fromid"></span>
### fromId

```java
public static WTNSubscribeStateChangeReason com.ss.bytertc.engine.data.WTNSubscribeStateChangeReason.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="WTNSubscribeStateChangeReason-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.WTNSubscribeStateChangeReason.value()
```


Get current value

**Return Value**

Current value

<span id="WTNSubscribeStateChangeReason-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.data.WTNSubscribeStateChangeReason.toString()
```


<span id="AudioMixingDualMonoMode"></span>
# AudioMixingDualMonoMode

```java
public enum com.ss.bytertc.engine.data.AudioMixingDualMonoMode
```


Mix playback channel type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_MIXING_DUAL_MONO_MODE_AUTO |0 |Consistent with audio files |
|AUDIO_MIXING_DUAL_MONO_MODE_L |1 |Only the left channel audio in the audio file can be heard |
|AUDIO_MIXING_DUAL_MONO_MODE_R |2 |Only the right channel audio in the audio file can be heard |
|AUDIO_MIXING_DUAL_MONO_MODE_MIX |3 |Can hear the left and right audio channels in the audio file at the same time |


<span id="WTNSubscribeState"></span>
# WTNSubscribeState

```java
public enum com.ss.bytertc.engine.data.WTNSubscribeState
```


State for WTN streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SUBSCRIBED |0 |Subscribe WTN media stream |
|UNSUBSCRIBED |1 |Unsubscribe WTN media stream |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#WTNSubscribeState-value) |


<span id="instructions"></span>
## Instructions

<span id="WTNSubscribeState-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.WTNSubscribeState.value()
```


Get current value

**Return Value**

Current value

<span id="LocalAudioStats"></span>
# LocalAudioStats

```java
public class com.ss.bytertc.engine.type.LocalAudioStats
```


Local audio stream statistics, reference period 2s.

After the local user publishes the audio stream successfully, the SDK will periodically notify the user through `onLocalStreamStats` the transmission status of the published audio stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |\- |[audioLossRate](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-audiolossrate) |
|float |\- |[sendKBitrate](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-sendkbitrate) |
|int |\- |[recordSampleRate](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-recordsamplerate) |
|int |\- |[statsInterval](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-statsinterval) |
|int |\- |[rtt](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-rtt) |
|int |\- |[numChannels](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-numchannels) |
|int |\- |[sentSampleRate](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-sentsamplerate) |
|int |\- |[jitter](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-jitter) |
|int |\- |[audioDeviceLoopDelay](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-audiodeviceloopdelay) |
|double |\- |[encodeFrameRate](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStats-encodeframerate) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioStats-audiolossrate"></span>
### audioLossRate

```java
public float com.ss.bytertc.engine.type.LocalAudioStats.audioLossRate
```


Audio packet loss rate. The audio uplink packet loss rate in this reference period. The value range is [0,1].

<span id="LocalAudioStats-sendkbitrate"></span>
### sendKBitrate

```java
public float com.ss.bytertc.engine.type.LocalAudioStats.sendKBitrate
```


Send rate. The audio transmission rate in the reference period is kbps.

<span id="LocalAudioStats-recordsamplerate"></span>
### recordSampleRate

```java
public int com.ss.bytertc.engine.type.LocalAudioStats.recordSampleRate
```


Acquisition sampling rate. Audio sampling rate information collected in the reference period, in units of Hz.

<span id="LocalAudioStats-statsinterval"></span>
### statsInterval

```java
public int com.ss.bytertc.engine.type.LocalAudioStats.statsInterval
```


Statistical interval. The interval of this reference period is in ms.

This field is used to set the reference period for the callback. The default setting is 2s.

<span id="LocalAudioStats-rtt"></span>
### rtt

```java
public int com.ss.bytertc.engine.type.LocalAudioStats.rtt
```


Round\-trip time. The unit is ms.

<span id="LocalAudioStats-numchannels"></span>
### numChannels

```java
public int com.ss.bytertc.engine.type.LocalAudioStats.numChannels
```


Number of audio channels.

<span id="LocalAudioStats-sentsamplerate"></span>
### sentSampleRate

```java
public int com.ss.bytertc.engine.type.LocalAudioStats.sentSampleRate
```


Audio transmission sampling rate. Audio transmission sampling rate information in the reference period, in Hz.

<span id="LocalAudioStats-jitter"></span>
### jitter

```java
public int com.ss.bytertc.engine.type.LocalAudioStats.jitter
```


Audio uplink network jitter in ms.

<span id="LocalAudioStats-audiodeviceloopdelay"></span>
### audioDeviceLoopDelay

```java
public int com.ss.bytertc.engine.type.LocalAudioStats.audioDeviceLoopDelay
```


Audio device record and playout delay in ms.

<span id="LocalAudioStats-encodeframerate"></span>
### encodeFrameRate

```java
public double com.ss.bytertc.engine.type.LocalAudioStats.encodeFrameRate
```


Audio encode frame rate.

<span id="MediaPlayerCustomSource"></span>
# MediaPlayerCustomSource

```java
public class com.ss.bytertc.engine.data.MediaPlayerCustomSource
```


The audio source for media player.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|MediaPlayerCustomSourceMode |MediaPlayerCustomSourceMode.PUSH |[mode](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerCustomSource-mode) |
|MediaPlayerCustomSourceStreamType |MediaPlayerCustomSourceStreamType.RAW |[type](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerCustomSource-type) |


<span id="instructions"></span>
## Instructions

<span id="MediaPlayerCustomSource-mode"></span>
### mode

```java
public MediaPlayerCustomSourceMode com.ss.bytertc.engine.data.MediaPlayerCustomSource.mode = MediaPlayerCustomSourceMode.PUSH
```


See [MediaPlayerCustomSourceMode](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerCustomSourceMode).

<span id="MediaPlayerCustomSource-type"></span>
### type

```java
public MediaPlayerCustomSourceStreamType com.ss.bytertc.engine.data.MediaPlayerCustomSource.type = MediaPlayerCustomSourceStreamType.RAW
```


See [MediaPlayerCustomSourceStreamType](https://docs.byteplus.com/en/docs/12/14169#MediaPlayerCustomSourceStreamType).

<span id="AVSyncEvent"></span>
# AVSyncEvent

```java
public enum com.ss.bytertc.engine.data.AVSyncEvent
```


AVSync events

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|INVALID_UID_REPEATED |0 |A/V synchronization failed.<br><br>&nbsp;<br><br>Current source audio ID has been set by other video publishers in the same room.<br><br>&nbsp;<br><br>One single audio source cannot be synchronized with multiple video sources at the same time. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static AVSyncEvent |[fromId](https://docs.byteplus.com/en/docs/12/14169#AVSyncEvent-fromid) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#AVSyncEvent-value) |
|String |[toString](https://docs.byteplus.com/en/docs/12/14169#AVSyncEvent-tostring) |


<span id="instructions"></span>
## Instructions

<span id="AVSyncEvent-fromid"></span>
### fromId

```java
public static AVSyncEvent com.ss.bytertc.engine.data.AVSyncEvent.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="AVSyncEvent-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.AVSyncEvent.value()
```


Get current value

**Return Value**

Current value

<span id="AVSyncEvent-tostring"></span>
### toString

```java
public String com.ss.bytertc.engine.data.AVSyncEvent.toString()
```


<span id="RemoteAudioPropertiesInfo"></span>
# RemoteAudioPropertiesInfo

```java
public class com.ss.bytertc.engine.data.RemoteAudioPropertiesInfo
```


Remote audio properties

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[streamId](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioPropertiesInfo-streamid) |
|StreamInfo |\- |[streamInfo](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioPropertiesInfo-streaminfo) |
|AudioPropertiesInfo |\- |[audioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioPropertiesInfo-audiopropertiesinfo) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioPropertiesInfo-streamid"></span>
### streamId

```java
public String com.ss.bytertc.engine.data.RemoteAudioPropertiesInfo.streamId
```


Remote stream ID.

<span id="RemoteAudioPropertiesInfo-streaminfo"></span>
### streamInfo

```java
public StreamInfo com.ss.bytertc.engine.data.RemoteAudioPropertiesInfo.streamInfo
```


Remote stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/14169#StreamInfo).

<span id="RemoteAudioPropertiesInfo-audiopropertiesinfo"></span>
### audioPropertiesInfo

```java
public AudioPropertiesInfo com.ss.bytertc.engine.data.RemoteAudioPropertiesInfo.audioPropertiesInfo
```


Information of audio properties. See [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesInfo).

<span id="RemoteVideoSinkPosition"></span>
# RemoteVideoSinkPosition

```java
public enum com.ss.bytertc.engine.video.RemoteVideoSinkPosition
```


The position of the remote video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AFTER_POST_PROCESS |1 |(Default) After post processing. |


<span id="RTCLogConfig"></span>
# RTCLogConfig

```java
public class com.ss.bytertc.engine.data.RTCLogConfig
```


Local log parameters.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[logPath](https://docs.byteplus.com/en/docs/12/14169#RTCLogConfig-logpath) |
|int |10 |[logFileSize](https://docs.byteplus.com/en/docs/12/14169#RTCLogConfig-logfilesize) |
|LocalLogLevel |LocalLogLevel.WARNING |[logLevel](https://docs.byteplus.com/en/docs/12/14169#RTCLogConfig-loglevel) |
|String |\- |[logFilenamePrefix](https://docs.byteplus.com/en/docs/12/14169#RTCLogConfig-logfilenameprefix) |


<span id="instructions"></span>
## Instructions

<span id="RTCLogConfig-logpath"></span>
### logPath

```java
public String com.ss.bytertc.engine.data.RTCLogConfig.logPath
```


(Required) Local log directory.

<span id="RTCLogConfig-logfilesize"></span>
### logFileSize

```java
public int com.ss.bytertc.engine.data.RTCLogConfig.logFileSize = 10
```


(Optional) The limits for total log file size in MB. The range is 1 to 100 MB, and the default value is 10 MB.

If `logFileSize` < 1, it will be set to 1 MB. If `logFileSize` \> 100, it will be set to 100 MB.

The maximum size for a single log file is 2 MB.

If 1 ≤ `logFileSize` ≤ 2, one log file will be generated. If `logFileSize` \> 2, the first `⌊logFileSize/2⌋` files will be filled with 2 MB each, the `⌊logFileSize/2⌋+1` fill will be filled with `logFileSize mod 2`.

If the size exceeds the remaining space, the oldest file will be deleted.

<span id="RTCLogConfig-loglevel"></span>
### logLevel

```java
public LocalLogLevel com.ss.bytertc.engine.data.RTCLogConfig.logLevel = LocalLogLevel.WARNING
```


(Optional) The logging level. See [LocalLogLevel](https://docs.byteplus.com/en/docs/12/14169#LocalLogLevel). The default is warning level.

<span id="RTCLogConfig-logfilenameprefix"></span>
### logFilenamePrefix

```java
public String com.ss.bytertc.engine.data.RTCLogConfig.logFilenamePrefix
```


(Optional) Local log file name prefix. It should follow the regular expression pattern of `[a-zA-Z0-9_\@-.]{1,128}`.

The final file name will be the prefix followed by "_" and the file creation time, and "_rtclog.log" at the end. For example, `logPrefix_2023-05-25_172324_rtclog.log`.

<span id="AudioReportMode"></span>
# AudioReportMode

```java
public enum com.ss.bytertc.engine.data.AudioReportMode
```


The volume callback modes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_REPORT_MODE_NORMAL |0 |Always\-on(Default). |
|AUDIO_REPORT_MODE_DISCONNECT |1 |After visibly joining a room and unpublishing your streams, disable the volume callback. |
|AUDIO_REPORT_MODE_RESET |2 |After visibly joining a room and unpublishing your streams, enable the volume callback. The volume is reset to 0. |


<span id="MixedStreamMediaType"></span>
# MixedStreamMediaType

```java
public enum com.ss.bytertc.engine.live.MixedStreamMediaType
```


The media type of the mixing stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO |0 |Audio and video |
|MIXED_STREAM_MEDIA_TYPE_AUDIO_ONLY |1 |Audio only |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamMediaType |[MixedStreamMediaType](https://docs.byteplus.com/en/docs/12/14169#MixedStreamMediaType-mixedstreammediatype) |
|int |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamMediaType-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamMediaType-mixedstreammediatype"></span>
### MixedStreamMediaType

```java
public com.ss.bytertc.engine.live.MixedStreamMediaType.MixedStreamMediaType(int value)
```


Sets the type of media stream pushed to CDN after being mixed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |The type of media stream pushed to CDN after being mixed. |


<span id="MixedStreamMediaType-getvalue"></span>
### getValue

```java
public int com.ss.bytertc.engine.live.MixedStreamMediaType.getValue()
```


Gets the media type of the mixing stream.

**Return Value**

The media type of the mixing stream.

<span id="AudioFormat"></span>
# AudioFormat

```java
public class com.ss.bytertc.engine.data.AudioFormat
```


Audio parameters format

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|AudioSampleRate |\- |[sampleRate](https://docs.byteplus.com/en/docs/12/14169#AudioFormat-samplerate) |
|AudioChannel |\- |[channel](https://docs.byteplus.com/en/docs/12/14169#AudioFormat-channel) |
|int |\- |[samplesPerCall](https://docs.byteplus.com/en/docs/12/14169#AudioFormat-samplespercall) |


<span id="instructions"></span>
## Instructions

<span id="AudioFormat-samplerate"></span>
### sampleRate

```java
public AudioSampleRate com.ss.bytertc.engine.data.AudioFormat.sampleRate
```


Audio sample rate. See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/14169#AudioSampleRate).

<span id="AudioFormat-channel"></span>
### channel

```java
public AudioChannel com.ss.bytertc.engine.data.AudioFormat.channel
```


Audio channel. See [AudioChannel](https://docs.byteplus.com/en/docs/12/14169#AudioChannel).

<span id="AudioFormat-samplespercall"></span>
### samplesPerCall

```java
public int com.ss.bytertc.engine.data.AudioFormat.samplesPerCall
```


Samples per audio frame returned by callback. `0` by default. The default samples per callback is the minimum value.

The minimum value is `sampleRate * channel * 0.01s`, the value when the callback interval is 0.01s.

The maximum value is `2048`. If the value is invalid, the samples per callback uses the default value.

This parameter only takes effect when setting the read\-write callback. It does not take effect when calling [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioframecallback) to enable read\-only callback.

<span id="MediaTypeEnhancementConfig"></span>
# MediaTypeEnhancementConfig

```java
public class com.ss.bytertc.engine.type.MediaTypeEnhancementConfig
```


Media type for cellular assisted Enhancement

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|boolean |false |[enhanceSignaling](https://docs.byteplus.com/en/docs/12/14169#MediaTypeEnhancementConfig-enhancesignaling) |
|boolean |false |[enhanceAudio](https://docs.byteplus.com/en/docs/12/14169#MediaTypeEnhancementConfig-enhanceaudio) |
|boolean |false |[enhanceVideo](https://docs.byteplus.com/en/docs/12/14169#MediaTypeEnhancementConfig-enhancevideo) |
|boolean |false |[enhanceScreenAudio](https://docs.byteplus.com/en/docs/12/14169#MediaTypeEnhancementConfig-enhancescreenaudio) |
|boolean |false |[enhanceScreenVideo](https://docs.byteplus.com/en/docs/12/14169#MediaTypeEnhancementConfig-enhancescreenvideo) |


<span id="instructions"></span>
## Instructions

<span id="MediaTypeEnhancementConfig-enhancesignaling"></span>
### enhanceSignaling

```java
public boolean com.ss.bytertc.engine.type.MediaTypeEnhancementConfig.enhanceSignaling = false
```


Apply to signaling or not. Not by default.

<span id="MediaTypeEnhancementConfig-enhanceaudio"></span>
### enhanceAudio

```java
public boolean com.ss.bytertc.engine.type.MediaTypeEnhancementConfig.enhanceAudio = false
```


Apply to audio stream (Screen\-sharing audio not included) or not. Not by default.

<span id="MediaTypeEnhancementConfig-enhancevideo"></span>
### enhanceVideo

```java
public boolean com.ss.bytertc.engine.type.MediaTypeEnhancementConfig.enhanceVideo = false
```


Apply to video (Screen\-sharing video not included) or not. Not by default.

<span id="MediaTypeEnhancementConfig-enhancescreenaudio"></span>
### enhanceScreenAudio

```java
public boolean com.ss.bytertc.engine.type.MediaTypeEnhancementConfig.enhanceScreenAudio = false
```


Apply to screen sharing audio or not. Not by default.

<span id="MediaTypeEnhancementConfig-enhancescreenvideo"></span>
### enhanceScreenVideo

```java
public boolean com.ss.bytertc.engine.type.MediaTypeEnhancementConfig.enhanceScreenVideo = false
```


Apply to screen sharing video or not. Not by default.

<span id="MirrorType"></span>
# MirrorType

```java
public enum com.ss.bytertc.engine.data.MirrorType
```


Mirror type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|MIRROR_TYPE_NONE |0 |The preview and the published video stream are not mirrored. |
|MIRROR_TYPE_RENDER |1 |The preview is mirrored. The published video stream is not mirrored. |
|MIRROR_TYPE_ENCODER |2 |The preview is not mirrored; only the published video stream is mirrored. |
|MIRROR_TYPE_RENDER_AND_ENCODER |3 |The preview and the published video stream are mirrored. |


<span id="CloudProxyInfo"></span>
# CloudProxyInfo

```java
public class com.ss.bytertc.engine.data.CloudProxyInfo
```


Cloud Proxy Information

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[cloudProxyIp](https://docs.byteplus.com/en/docs/12/14169#CloudProxyInfo-cloudproxyip) |
|int |\- |[cloudProxyPort](https://docs.byteplus.com/en/docs/12/14169#CloudProxyInfo-cloudproxyport) |


<span id="instructions"></span>
## Instructions

<span id="CloudProxyInfo-cloudproxyip"></span>
### cloudProxyIp

```java
public String com.ss.bytertc.engine.data.CloudProxyInfo.cloudProxyIp
```


Cloud proxy IP

<span id="CloudProxyInfo-cloudproxyport"></span>
### cloudProxyPort

```java
public int com.ss.bytertc.engine.data.CloudProxyInfo.cloudProxyPort
```


Cloud proxy Port

<span id="VideoEncoderConfig"></span>
# VideoEncoderConfig

```java
public class com.ss.bytertc.engine.VideoEncoderConfig
```


Video stream configuration

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfig-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfig-height) |
|int |\- |[frameRate](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfig-framerate) |
|int |\-1 |[maxBitrate](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfig-maxbitrate) |
|int |0 |[minBitrate](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfig-minbitrate) |
|int |0 |[keyFrameIntervalMs](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfig-keyframeintervalms) |
|EncoderPreference |EncoderPreference.MAINTAIN_FRAMERATE |[encodePreference](https://docs.byteplus.com/en/docs/12/14169#VideoEncoderConfig-encodepreference) |


<span id="instructions"></span>
## Instructions

<span id="VideoEncoderConfig-width"></span>
### width

```java
public int com.ss.bytertc.engine.VideoEncoderConfig.width
```


Width of the video frame in px

<span id="VideoEncoderConfig-height"></span>
### height

```java
public int com.ss.bytertc.engine.VideoEncoderConfig.height
```


Height of the video frame in px

<span id="VideoEncoderConfig-framerate"></span>
### frameRate

```java
public int com.ss.bytertc.engine.VideoEncoderConfig.frameRate
```


Video frame rate in fps

<span id="VideoEncoderConfig-maxbitrate"></span>
### maxBitrate

```java
public int com.ss.bytertc.engine.VideoEncoderConfig.maxBitrate = -1
```


Maximum bit rate in kbps. Optional for internal capturing while mandatory for custom capturing.

If you set this value to \-1, SDK will automatically calculate the applicable bit rate based on the input resolution and frame rate.

No stream will be encoded and published if you set this value to 0.

In 3.44.1 and later versions, the default value is `-1` for internal capturing, but no default value in versions earlier than 3.44.1.

<span id="VideoEncoderConfig-minbitrate"></span>
### minBitrate

```java
public int com.ss.bytertc.engine.VideoEncoderConfig.minBitrate = 0
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `minBitrate`.

It defaults to `0`.

It ranges within [0, maxBitrate). When `maxBitrate` < `minBitrate`, the bitrate is self\-adapted.

In the following circumstance, the assignment to this variable has no effect:


* When `maxBitrate` = `0`, the video encoding is disabled.

* When `maxBitrate` < `0`, the bitrate is self\-adapted.

    &nbsp;


<span id="keyframeintervalms"></span>
### keyFrameIntervalMs

```java
public int com.ss.bytertc.engine.VideoEncoderConfig.keyFrameIntervalMs = 0
```


Key frame interval in milliseconds

<span id="VideoEncoderConfig-encodepreference"></span>
### encodePreference

```java
public EncoderPreference com.ss.bytertc.engine.VideoEncoderConfig.encodePreference = EncoderPreference.MAINTAIN_FRAMERATE
```


Encoding preference. The default value is MaintainFramerate(1). See [EncoderPreference](https://docs.byteplus.com/en/docs/12/14169#EncoderPreference).

<span id="FirstFramePlayState"></span>
# FirstFramePlayState

```java
public enum com.ss.bytertc.engine.type.FirstFramePlayState
```


First frame playback status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FIRST_FRAME_PLAY_STATE_PLAYING |0 |Playing |
|FIRST_FRAME_PLAY_STATE_PLAYED |1 |Play success |
|FIRST_FRAME_PLAY_STATE_END |2 |Play failed |


<span id="RemoteVideoSinkConfig"></span>
# RemoteVideoSinkConfig

```java
public class com.ss.bytertc.engine.video.RemoteVideoSinkConfig
```


Remote video frame callback configurations.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|RemoteVideoSinkPosition |RemoteVideoSinkPosition.AFTER_POST_PROCESS |[position](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoSinkConfig-position) |
|VideoPixelFormat |VideoPixelFormat.UNKNOWN |[pixelFormat](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoSinkConfig-pixelformat) |
|VideoApplyRotation |VideoApplyRotation.DEFAULT |[applyRotation](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoSinkConfig-applyrotation) |
|VideoSinkMirrorType |VideoSinkMirrorType.OFF |[mirrorType](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoSinkConfig-mirrortype) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoSinkConfig-position"></span>
### position

```java
public RemoteVideoSinkPosition com.ss.bytertc.engine.video.RemoteVideoSinkConfig.position = RemoteVideoSinkPosition.AFTER_POST_PROCESS
```


The position of the remote video frame. See [RemoteVideoSinkPosition](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoSinkPosition). The default position is after processing.

<span id="RemoteVideoSinkConfig-pixelformat"></span>
### pixelFormat

```java
public VideoPixelFormat com.ss.bytertc.engine.video.RemoteVideoSinkConfig.pixelFormat = VideoPixelFormat.UNKNOWN
```


The pixel format of the remote video frame. See [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14169#VideoPixelFormat). The default value is 0.

<span id="RemoteVideoSinkConfig-applyrotation"></span>
### applyRotation

```java
public VideoApplyRotation com.ss.bytertc.engine.video.RemoteVideoSinkConfig.applyRotation = VideoApplyRotation.DEFAULT
```


Whether the video frame needs to be automatically rotated. See [VideoApplyRotation](https://docs.byteplus.com/en/docs/12/14169#VideoApplyRotation). The default value is no rotation.

<span id="RemoteVideoSinkConfig-mirrortype"></span>
### mirrorType

```java
public VideoSinkMirrorType com.ss.bytertc.engine.video.RemoteVideoSinkConfig.mirrorType = VideoSinkMirrorType.OFF
```


Whether the video frame needs to be mirrored. See [VideoSinkMirrorType](https://docs.byteplus.com/en/docs/12/14169#VideoSinkMirrorType). The default value is no mirroring effect.

<span id="AnsMode"></span>
# AnsMode

```java
public enum com.ss.bytertc.engine.type.AnsMode
```


ANC modes. The ANC algorithm is determined by the room profile you set when calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-joinroom).

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ANS_MODE_DISABLE |0 |Disable ANC. |
|ANS_MODE_LOW |1 |Cancel subtle background noise. |
|ANS_MODE_MEDIUM |2 |Cancel medium\-level, continuous noise, such as the sound of fans or air conditioners. |
|ANS_MODE_HIGH |3 |Cancel loud, impulsive, and intermittent noise, such as keyboard clicking noise, a crash/clash, a bark, and chair scraping noise. |
|ANS_MODE_AUTOMATIC |4 |Enable automatic ANC. The ANC algorithm is dynamically determined by RTC. |


<span id="LocalAudioStreamState"></span>
# LocalAudioStreamState

```java
public enum com.ss.bytertc.engine.data.LocalAudioStreamState
```


Local audio stream status. The

SDK calls back the state via onLocalAudioStateChanged.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|LOCAL_AUDIO_STREAM_STATE_STOPPED |0 |The default initial state of the local audio.<br><br>&nbsp;<br><br>Callbacks this state when the microphone stops working, corresponding to kLocalAudioStreamErrorOk in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamError). |
|LOCAL_AUDIO_STREAM_STATE_RECORDING |1 |The local audio recording device started successfully.<br><br>&nbsp;<br><br>Callback to this state when the first audio frame is collected, corresponding to kLocalAudioStreamErrorOk in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamError). |
|LOCAL_AUDIO_STREAM_STATE_ENCODING |2 |The first frame of the local audio was successfully encoded.<br><br>&nbsp;<br><br>Callback to this state when the first audio frame is successfully encoded, corresponding to kLocalAudioStreamErrorOk in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamError). |
|LOCAL_AUDIO_STREAM_STATE_FAILED |3 |The local audio startup failed, and the status is called back at the following times:<br><br><br>&nbsp;<br><br>* The local recording device failed to start, corresponding to the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamError) kLocalAudioStreamErrorRecordFailure.<br><br>* No recording device permissions detected, corresponding to kLocalAudioStreamError NoPermission in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamError).<br><br>* Audio encoding failed, corresponding to the error code kLocalAudioStreamError EncodeFailure in [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamError). |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#LocalAudioStreamState-value) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioStreamState-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.LocalAudioStreamState.value()
```


Get current value

**Return Value**

Current value

<span id="VideoFrameInfo"></span>
# VideoFrameInfo

```java
public class com.ss.bytertc.engine.data.VideoFrameInfo
```


Video frame information

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[width](https://docs.byteplus.com/en/docs/12/14169#VideoFrameInfo-width) |
|int |0 |[height](https://docs.byteplus.com/en/docs/12/14169#VideoFrameInfo-height) |
|VideoRotation |VideoRotation.VIDEO_ROTATION_0 |[rotation](https://docs.byteplus.com/en/docs/12/14169#VideoFrameInfo-rotation) |


<span id="instructions"></span>
## Instructions

<span id="VideoFrameInfo-width"></span>
### width

```java
public int com.ss.bytertc.engine.data.VideoFrameInfo.width = 0
```


Width (pixels)

<span id="VideoFrameInfo-height"></span>
### height

```java
public int com.ss.bytertc.engine.data.VideoFrameInfo.height = 0
```


Height (pixels)

<span id="VideoFrameInfo-rotation"></span>
### rotation

```java
public VideoRotation com.ss.bytertc.engine.data.VideoFrameInfo.rotation = VideoRotation.VIDEO_ROTATION_0
```


Video frame clockwise rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14169#VideoRotation).

<span id="EngineConfig"></span>
# EngineConfig

```java
public class com.ss.bytertc.engine.data.EngineConfig
```


Engine Config

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|Context |null |[context](https://docs.byteplus.com/en/docs/12/14169#EngineConfig-context) |
|String |\- |[appID](https://docs.byteplus.com/en/docs/12/14169#EngineConfig-appid) |
|Object |null |[eglContext](https://docs.byteplus.com/en/docs/12/14169#EngineConfig-eglcontext) |
|JSONObject |null |[parameters](https://docs.byteplus.com/en/docs/12/14169#EngineConfig-parameters) |


<span id="instructions"></span>
## Instructions

<span id="EngineConfig-context"></span>
### context

```java
public Context com.ss.bytertc.engine.data.EngineConfig.context = null
```


必填，Android Application Context

<span id="EngineConfig-appid"></span>
### appID

```java
public String com.ss.bytertc.engine.data.EngineConfig.appID
```


required. A unique identifier for each App, randomly generated by the RTC console. Engine instances created with different AppIds cannot communicate with each other.

<span id="EngineConfig-eglcontext"></span>
### eglContext

```java
public Object com.ss.bytertc.engine.data.EngineConfig.eglContext = null
```


Optional. If you need SDK to support custom texture hardcoding, you must import the eglContext in a JObject

<span id="EngineConfig-parameters"></span>
### parameters

```java
public JSONObject com.ss.bytertc.engine.data.EngineConfig.parameters = null
```


Optional. Reserved parameters. Please contact technical support fellow if needed.

<span id="RemoteStreamSwitch"></span>
# RemoteStreamSwitch

```java
public class com.ss.bytertc.engine.type.RemoteStreamSwitch
```


Information of stream switching due to a Fallback

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[uid](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamSwitch-uid) |
|boolean |\- |[isScreen](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamSwitch-isscreen) |
|int |\- |[beforeVideoIndex](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamSwitch-beforevideoindex) |
|int |\- |[afterVideoIndex](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamSwitch-aftervideoindex) |
|boolean |\- |[beforeEnable](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamSwitch-beforeenable) |
|boolean |\- |[afterEnable](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamSwitch-afterenable) |
|FallbackOrRecoverReason |\- |[reason](https://docs.byteplus.com/en/docs/12/14169#RemoteStreamSwitch-reason) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamSwitch-uid"></span>
### uid

```java
public String com.ss.bytertc.engine.type.RemoteStreamSwitch.uid
```


User ID of the publisher of the subscribed media stream

<span id="RemoteStreamSwitch-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.type.RemoteStreamSwitch.isScreen
```


Reserved field. Ignore the value returned in this field.

<span id="RemoteStreamSwitch-beforevideoindex"></span>
### beforeVideoIndex

```java
public int com.ss.bytertc.engine.type.RemoteStreamSwitch.beforeVideoIndex
```


The quality index of the subscribed stream before the stream switching

<span id="RemoteStreamSwitch-aftervideoindex"></span>
### afterVideoIndex

```java
public int com.ss.bytertc.engine.type.RemoteStreamSwitch.afterVideoIndex
```


The quality index of the subscribed stream after the stream switching

<span id="RemoteStreamSwitch-beforeenable"></span>
### beforeEnable

```java
public boolean com.ss.bytertc.engine.type.RemoteStreamSwitch.beforeEnable
```


Whether a video stream is enabled before stream switching

<span id="RemoteStreamSwitch-afterenable"></span>
### afterEnable

```java
public boolean com.ss.bytertc.engine.type.RemoteStreamSwitch.afterEnable
```


Whether a video stream after the stream switching

<span id="RemoteStreamSwitch-reason"></span>
#### reason

```java
public FallbackOrRecoverReason com.ss.bytertc.engine.type.RemoteStreamSwitch.reason
```


Refer to [FallbackOrRecoverReason](https://docs.byteplus.com/en/docs/12/14169#FallbackOrRecoverReason) for the reason of the Fallback or reverting from the Fallback of the subscribed stream.

<span id="VideoCanvas"></span>
# VideoCanvas

```java
public class com.ss.bytertc.engine.VideoCanvas
```


Video rendering configuration.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |1 |[RENDER_MODE_HIDDEN](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-render_mode_hidden) |
|int |2 |[RENDER_MODE_FIT](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-render_mode_fit) |
|int |3 |[RENDER_MODE_FILL](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-render_mode_fill) |
|View |\- |[renderView](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-renderview) |
|Surface |\- |[renderSurface](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-rendersurface) |
|int |\- |[renderMode](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-rendermode) |
|int |\- |[backgroundColor](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-backgroundcolor) |
|VideoRotation |\- |[renderRotation](https://docs.byteplus.com/en/docs/12/14169#VideoCanvas-renderrotation) |


<span id="instructions"></span>
## Instructions

<span id="VideoCanvas-render_mode_hidden"></span>
### RENDER_MODE_HIDDEN

```java
public static final int com.ss.bytertc.engine.VideoCanvas.RENDER_MODE_HIDDEN = 1
```


(Default) Fill and Crop.

The video frame is scaled with fixed aspect ratio, and completely fills the canvas. The region of the video exceeding the canvas will be cropped.

<span id="VideoCanvas-render_mode_fit"></span>
### RENDER_MODE_FIT

```java
public static final int com.ss.bytertc.engine.VideoCanvas.RENDER_MODE_FIT = 2
```


Fit.

The video frame is scaled with fixed aspect ratio, and is shown completely in the canvas. The region of the canvas not filled with video frame, is filled with `background`.

<span id="VideoCanvas-render_mode_fill"></span>
### RENDER_MODE_FILL

```java
public static final int com.ss.bytertc.engine.VideoCanvas.RENDER_MODE_FILL = 3
```


Fill the canvas.

The video frame is scaled to fill the canvas. During the process, the aspect ratio may change.

<span id="VideoCanvas-renderview"></span>
### renderView

```java
public View com.ss.bytertc.engine.VideoCanvas.renderView
```


Local view handler.

When you render the `View` object, use the field, and set `renderSurface` to `null`.

<span id="VideoCanvas-rendersurface"></span>
### renderSurface

```java
public Surface com.ss.bytertc.engine.VideoCanvas.renderSurface
```


Local surface handler.

When you render the Surface object, use the field, and set `renderView` to `null`.

<span id="VideoCanvas-rendermode"></span>
### renderMode

```java
public int com.ss.bytertc.engine.VideoCanvas.renderMode
```


Rendering mode, the value must be `RENDER_MODE_HIDDEN(1)`, `RENDER_MODE_FIT(2)`, or `RENDER_MODE_FILL(3)`. The default value is `RENDER_MODE_HIDDEN(1)`.

<span id="VideoCanvas-backgroundcolor"></span>
### backgroundColor

```java
public int com.ss.bytertc.engine.VideoCanvas.backgroundColor
```


Set the background color of the canvas which is not filled with video frame. The range is `[0x00000000, 0xFFFFFFFF]`. The default is `0x00000000`. The Alpha index is ignored.

<span id="VideoCanvas-renderrotation"></span>
### renderRotation

```java
public VideoRotation com.ss.bytertc.engine.VideoCanvas.renderRotation
```


Video frame rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14169#VideoRotation). The default value is 0, which means no rotation is applied.

This parameter only applies to remote video and does not affect local video settings.

<span id="RemoteVideoStats"></span>
# RemoteVideoStats

```java
public class com.ss.bytertc.engine.type.RemoteVideoStats
```


Remote video stream statistics, reference period 2s.

After the local user subscribes to the remote video stream successfully, the SDK will periodically notify the local user of the reception status of the subscribed remote video stream during this reference period through `onRemoteStreamStats`. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[width](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-width) |
|int |\- |[height](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-height) |
|float |\- |[videoLossRate](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-videolossrate) |
|float |\- |[receivedKBitrate](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-receivedkbitrate) |
|int |\- |[decoderOutputFrameRate](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-decoderoutputframerate) |
|int |\- |[rendererOutputFrameRate](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-rendereroutputframerate) |
|int |\- |[stallCount](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-stallcount) |
|int |\- |[stallDuration](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-stallduration) |
|long |\- |[e2eDelay](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-e2edelay) |
|boolean |\- |[isScreen](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-isscreen) |
|int |\- |[statsInterval](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-statsinterval) |
|int |\- |[rtt](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-rtt) |
|int |\- |[frozenRate](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-frozenrate) |
|int |\- |[codecType](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-codectype) |
|int |\- |[videoIndex](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-videoindex) |
|int |\- |[jitter](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-jitter) |
|int |\- |[capToRenderDelay](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-captorenderdelay) |
|int |\- |[avSyncDiffMs](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-avsyncdiffms) |
|int |\- |[codecElapsePerFrame](https://docs.byteplus.com/en/docs/12/14169#RemoteVideoStats-codecelapseperframe) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoStats-width"></span>
### width

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.width
```


Remote Video Stream Width

<span id="RemoteVideoStats-height"></span>
### height

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.height
```


Remote Video Stream Height

<span id="RemoteVideoStats-videolossrate"></span>
### videoLossRate

```java
public float com.ss.bytertc.engine.type.RemoteVideoStats.videoLossRate
```


Video packet loss rate. The video downlink packet loss rate in the reference period. The value range is [0,1].

<span id="RemoteVideoStats-receivedkbitrate"></span>
### receivedKBitrate

```java
public float com.ss.bytertc.engine.type.RemoteVideoStats.receivedKBitrate
```


Receiving bit rate. Video reception rate within the reference period, in kbps.

<span id="RemoteVideoStats-decoderoutputframerate"></span>
### decoderOutputFrameRate

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.decoderOutputFrameRate
```


The decoder outputs the frame rate. Video decoder output frame rate within the reference period, in fps.

<span id="RemoteVideoStats-rendereroutputframerate"></span>
### rendererOutputFrameRate

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.rendererOutputFrameRate
```


Render frame rate. The video rendering frame rate in the reference period, in fps.

<span id="RemoteVideoStats-stallcount"></span>
### stallCount

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.stallCount
```


Number of stalls. Number of stalls in the reference period.

<span id="RemoteVideoStats-stallduration"></span>
### stallDuration

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.stallDuration
```


Stall duration. The total duration of video stalling during the reference period. Unit ms.

<span id="RemoteVideoStats-e2edelay"></span>
### e2eDelay

```java
public long com.ss.bytertc.engine.type.RemoteVideoStats.e2eDelay
```


User experience\-level end\-to\-end delay, in milliseconds, from the time when the sender captures the encoding to the time when the receiver decodes the rendering

<span id="RemoteVideoStats-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.type.RemoteVideoStats.isScreen
```


Reserved field. Ignore the value returned in this field.

<span id="RemoteVideoStats-statsinterval"></span>
### statsInterval

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.statsInterval
```


Statistical interval, the interval of this reference period, in ms.

This field is used to set the reference period for the callback, currently set to 2s.

<span id="RemoteVideoStats-rtt"></span>
### rtt

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.rtt
```


Round\-trip time in ms.

<span id="RemoteVideoStats-frozenrate"></span>
### frozenRate

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.frozenRate
```


The cumulative duration of video freeze for the remote user accounts for the percentage (%) of the total effective duration of the video after entering the room. The effective duration of the video refers to the duration of the video other than stopping sending the video stream and disabling the video module after the remote user enters the room to publish the video stream.

<span id="RemoteVideoStats-codectype"></span>
### codecType

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.codecType
```


For the encoding type of the video, please refer to [VideoCodecType](https://docs.byteplus.com/en/docs/12/14169#VideoCodecType).

<span id="RemoteVideoStats-videoindex"></span>
### videoIndex

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.videoIndex
```


For subscripts for streams with multiple resolutions.

<span id="RemoteVideoStats-jitter"></span>
### jitter

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.jitter
```


Video downlink network jitter in ms.

<span id="RemoteVideoStats-captorenderdelay"></span>
### capToRenderDelay

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.capToRenderDelay
```


End\-to\-end latency at the user experience level. The delay from the start of capturing at the sending end to the completion of rendering at the receiving end, in units of ms.

<span id="RemoteVideoStats-avsyncdiffms"></span>
### avSyncDiffMs

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.avSyncDiffMs
```


Audio/video synchronization diff in ms.

<span id="RemoteVideoStats-codecelapseperframe"></span>
### codecElapsePerFrame

```java
public int com.ss.bytertc.engine.type.RemoteVideoStats.codecElapsePerFrame
```


Average time spent on video decoding in ms.

<span id="VideoApplyRotation"></span>
# VideoApplyRotation

```java
public enum com.ss.bytertc.engine.video.VideoApplyRotation
```


Whether the video frame needs to be automatically rotated.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|DEFAULT |\-1 |(Default) No rotation. |
|DEGREE_0 |0 |Automatic rotation, which rotates video frames to 0 degreess based on the rotation angle information. |


<span id="VideoDeviceInfo"></span>
# VideoDeviceInfo

```java
public class com.ss.bytertc.engine.video.VideoDeviceInfo
```


> Available since 3.56


Video device information

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[deviceId](https://docs.byteplus.com/en/docs/12/14169#VideoDeviceInfo-deviceid) |
|String |\- |[deviceName](https://docs.byteplus.com/en/docs/12/14169#VideoDeviceInfo-devicename) |
|VideoDeviceFacing |\- |[deviceFacing](https://docs.byteplus.com/en/docs/12/14169#VideoDeviceInfo-devicefacing) |


<span id="instructions"></span>
## Instructions

<span id="VideoDeviceInfo-deviceid"></span>
### deviceId

```java
public String com.ss.bytertc.engine.video.VideoDeviceInfo.deviceId
```


Device ID

<span id="VideoDeviceInfo-devicename"></span>
### deviceName

```java
public String com.ss.bytertc.engine.video.VideoDeviceInfo.deviceName
```


Device alias

<span id="VideoDeviceInfo-devicefacing"></span>
### deviceFacing

```java
public VideoDeviceFacing com.ss.bytertc.engine.video.VideoDeviceInfo.deviceFacing
```


camera facing info. See [VideoDeviceFacing](https://docs.byteplus.com/en/docs/12/14169#VideoDeviceFacing).

<span id="IVideoSink"></span>
# IVideoSink

```java
public interface com.ss.bytertc.engine.video.IVideoSink
```


Custom video renderer.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onFrame](https://docs.byteplus.com/en/docs/12/14169#IVideoSink-onframe) |
|int |[getRenderElapse](https://docs.byteplus.com/en/docs/12/14169#IVideoSink-getrenderelapse) |


<span id="instructions"></span>
## Instructions

<span id="IVideoSink-onframe"></span>
### onFrame

```java
void com.ss.bytertc.engine.video.IVideoSink.onFrame(IVideoFrame frame)
```


Video frame callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|frame |IVideoFrame |Video frame structure. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/14169#IVideoFrame) |


<span id="IVideoSink-getrenderelapse"></span>
### getRenderElapse

```java
int com.ss.bytertc.engine.video.IVideoSink.getRenderElapse()
```


Average external rendering time in milliseconds.

**Return Value**

Average external rendering time in milliseconds

<span id="PlayerEvent"></span>
# PlayerEvent

```java
public enum com.ss.bytertc.engine.data.PlayerEvent
```


Playback event.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SELECT_AUDIO_TRACK_BEGIN |0 |Beginning to switch audio tracks.<br><br>When you call [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-selectaudiotrack) to switch to a specific audio track, the player returns this state. |
|SELECT_AUDIO_TRACK_COMPLETED |1 |Audio track switch completed.<br><br>After you call [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-selectaudiotrack) to switch to a specific audio track, the player successfully switches to the track and returns this state. |
|SELECT_AUDIO_TRACK_FAILED |2 |Audio track switch failed.<br><br>After you call [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-selectaudiotrack) to switch to a specific audio track, the player fails to switch to the track and returns this state. |
|SEEK_BEGIN |3 |Beginning to move the playback position.<br><br>When you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition) to move the playback position, the player returns this state. |
|SEEK_COMPLETED |4 |Playback position move completed.<br><br>After you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition) to move the playback position, the player successfully moves to the new position and returns this state. |
|SEEK_FAILED |5 |Playback position move failed.<br><br>After you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition) to move the playback position, the player fails to move to the new position and returns this state. |


<span id="MixedStreamAudioConfig"></span>
# MixedStreamAudioConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamAudioConfig
```


Audio transcoding configurations. With invalid or empty input, the configurations will be set as the default values.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|MixedStreamAudioCodecType |MixedStreamAudioCodecType.MIXED_STREAM_AUDIO_CODEC_TYPE_AAC |[audioCodec](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioConfig-audiocodec) |
|int |64 |[bitrate](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioConfig-bitrate) |
|int |48000 |[sampleRate](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioConfig-samplerate) |
|int |2 |[channels](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioConfig-channels) |
|MixedStreamAudioProfile |MixedStreamAudioProfile.MIXED_STREAM_AUDIO_PROFILE_LC |[audioProfile](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioConfig-audioprofile) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamAudioConfig |[MixedStreamAudioConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAudioConfig-mixedstreamaudioconfig) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamAudioConfig-audiocodec"></span>
### audioCodec

```java
public MixedStreamAudioCodecType com.ss.bytertc.engine.live.MixedStreamAudioConfig.audioCodec = MixedStreamAudioCodecType.MIXED_STREAM_AUDIO_CODEC_TYPE_AAC
```


<span id="MixedStreamAudioConfig-bitrate"></span>
### bitrate

```java
public int com.ss.bytertc.engine.live.MixedStreamAudioConfig.bitrate = 64
```


Sets the bitrate.

<span id="MixedStreamAudioConfig-samplerate"></span>
### sampleRate

```java
public int com.ss.bytertc.engine.live.MixedStreamAudioConfig.sampleRate = 48000
```


Sets the sample rate.

<span id="MixedStreamAudioConfig-channels"></span>
### channels

```java
public int com.ss.bytertc.engine.live.MixedStreamAudioConfig.channels = 2
```


Sets the number of channels.

<span id="MixedStreamAudioConfig-audioprofile"></span>
### audioProfile

```java
public MixedStreamAudioProfile com.ss.bytertc.engine.live.MixedStreamAudioConfig.audioProfile = MixedStreamAudioProfile.MIXED_STREAM_AUDIO_PROFILE_LC
```


Sets the AAC profile.

**Notes**

This parameter is not supported for WTN stream tasks.

<span id="instructions"></span>
## Instructions

<span id="MixedStreamAudioConfig-mixedstreamaudioconfig"></span>
### MixedStreamAudioConfig

```java
public com.ss.bytertc.engine.live.MixedStreamAudioConfig.MixedStreamAudioConfig()
```


<span id="VideoRotation"></span>
# VideoRotation

```java
public enum com.ss.bytertc.engine.data.VideoRotation
```


Video frame rotation angle

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VIDEO_ROTATION_0 |0 |Video does not rotate |
|VIDEO_ROTATION_90 |90 |Video rotate 90 degrees clockwise |
|VIDEO_ROTATION_180 |180 |Video rotate 180 degrees clockwise |
|VIDEO_ROTATION_270 |270 |Video rotate 270 degrees clockwise |


<span id="OrientationMode"></span>
# OrientationMode

```java
public enum com.ss.bytertc.engine.video.VideoEncoderConfiguration.OrientationMode
```


Directional mode of video encoding

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ORIENTATION_MODE_ADAPTIVE |0 |The video output direction is consistent with the acquisition direction. |
|ORIENTATION_MODE_FIXED_LANDSCAPE |1 |Fixed horizontal screen output video. If the collected video is in vertical screen mode, the video encoder will crop it. |
|ORIENTATION_MODE_FIXED_PORTRAIT |2 |Fixed vertical screen output video. If the collected video is horizontal screen mode, the video encoder will crop it. |


<span id="MixedStreamAlternateImageFillMode"></span>
# MixedStreamAlternateImageFillMode

```java
public enum com.ss.bytertc.engine.live.MixedStreamAlternateImageFillMode
```


The fill mode of the placeholder image.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FIT |0 |The placeholder image is scaled with the same aspect ratio as the user's original video frame. Default setting. |
|FILL |1 |The placeholder image is not scaled with the same aspect ratio as the user's original video frame. It maintains the original aspect ratio. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamAlternateImageFillMode |[MixedStreamAlternateImageFillMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAlternateImageFillMode-mixedstreamalternateimagefillmode) |
|int |[getValue](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAlternateImageFillMode-getvalue) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamAlternateImageFillMode-mixedstreamalternateimagefillmode"></span>
### MixedStreamAlternateImageFillMode

```java
public com.ss.bytertc.engine.live.MixedStreamAlternateImageFillMode.MixedStreamAlternateImageFillMode(int value)
```


Sets the fill mode of the placeholder image.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |It is used to control the fill mode of the placeholder image after the user stops publishing video streams and the screen reverts to the placeholder image. It defaults to `kMixedStreamAlternateImageFillModeFit` indicating the image is scaled with the video's aspect ratio.<br><br>See [MixedStreamAlternateImageFillMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamAlternateImageFillMode).<br><br>This parameter is not supported for WTN stream tasks. |


<span id="MixedStreamAlternateImageFillMode-getvalue"></span>
### getValue

```java
public int com.ss.bytertc.engine.live.MixedStreamAlternateImageFillMode.getValue()
```


Gets the fill mode of the placeholder image.

**Return Value**

The fill mode of the placeholder image.

<span id="LocalVideoSinkConfig"></span>
# LocalVideoSinkConfig

```java
public class com.ss.bytertc.engine.video.LocalVideoSinkConfig
```


Local video frame callback config.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|LocalVideoSinkPosition |LocalVideoSinkPosition.AFTER_PREPROCESS |[position](https://docs.byteplus.com/en/docs/12/14169#LocalVideoSinkConfig-position) |
|VideoPixelFormat |VideoPixelFormat.UNKNOWN |[pixelFormat](https://docs.byteplus.com/en/docs/12/14169#LocalVideoSinkConfig-pixelformat) |


<span id="instructions"></span>
## Instructions

<span id="LocalVideoSinkConfig-position"></span>
### position

```java
public LocalVideoSinkPosition com.ss.bytertc.engine.video.LocalVideoSinkConfig.position = LocalVideoSinkPosition.AFTER_PREPROCESS
```


The position of the local video frame. See [LocalVideoSinkPosition](https://docs.byteplus.com/en/docs/12/14169#LocalVideoSinkPosition).

<span id="LocalVideoSinkConfig-pixelformat"></span>
### pixelFormat

```java
public VideoPixelFormat com.ss.bytertc.engine.video.LocalVideoSinkConfig.pixelFormat = VideoPixelFormat.UNKNOWN
```


The pixel format of the local video frame. See [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14169#VideoPixelFormat). The default value is 0.

<span id="RecordingProgress"></span>
# RecordingProgress

```java
public class com.ss.bytertc.engine.data.RecordingProgress
```


Local recording progress

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|long |\- |[duration](https://docs.byteplus.com/en/docs/12/14169#RecordingProgress-duration) |
|long |\- |[fileSize](https://docs.byteplus.com/en/docs/12/14169#RecordingProgress-filesize) |


<span id="instructions"></span>
## Instructions

<span id="RecordingProgress-duration"></span>
### duration

```java
public long com.ss.bytertc.engine.data.RecordingProgress.duration
```


The cumulative recording time of the current file, in milliseconds

<span id="RecordingProgress-filesize"></span>
### fileSize

```java
public long com.ss.bytertc.engine.data.RecordingProgress.fileSize
```


The size of the currently recorded file in bytes

<span id="RemoteUserPriority"></span>
# RemoteUserPriority

```java
public enum com.ss.bytertc.engine.type.RemoteUserPriority
```


Priority of the publisher. When a user encounters performance insufficiency of either the network or the device, the media stream will fall back in the ascending order of `RemoteUserPriority`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|REMOTE_USER_PRIORITY_LOW |0 |Low, the default |
|REMOTE_USER_PRIORITY_MEDIUM |100 |Medium |
|REMOTE_USER_PRIORITY_HIGH |200 |High |


<span id="MixedStreamSpatialAudioConfig"></span>
# MixedStreamSpatialAudioConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamSpatialAudioConfig
```


Spatial audio config when pushing to CDN.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|boolean |false |[enableSpatialRender](https://docs.byteplus.com/en/docs/12/14169#MixedStreamSpatialAudioConfig-enablespatialrender) |
|Position |\- |[audienceSpatialPosition](https://docs.byteplus.com/en/docs/12/14169#MixedStreamSpatialAudioConfig-audiencespatialposition) |
|HumanOrientation |\- |[audienceSpatialOrientation](https://docs.byteplus.com/en/docs/12/14169#MixedStreamSpatialAudioConfig-audiencespatialorientation) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamSpatialAudioConfig |[MixedStreamSpatialAudioConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamSpatialAudioConfig-mixedstreamspatialaudioconfig) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamSpatialAudioConfig-enablespatialrender"></span>
### enableSpatialRender

```java
public boolean com.ss.bytertc.engine.live.MixedStreamSpatialAudioConfig.enableSpatialRender = false
```


Whether to enable the spatial audio effect when pushing to CDN.

**Notes**

when you enable the feature, set the `spatial_position` of each [MixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamLayoutRegionConfig) for spatial audio effect.

<span id="MixedStreamSpatialAudioConfig-audiencespatialposition"></span>
### audienceSpatialPosition

```java
public Position com.ss.bytertc.engine.live.MixedStreamSpatialAudioConfig.audienceSpatialPosition
```


The spatial position of the audience. See [Position](https://docs.byteplus.com/en/docs/12/14169#Position).

The audience is the users who receive the audio stream from CDN.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamSpatialAudioConfig-audiencespatialorientation"></span>
### audienceSpatialOrientation

```java
public HumanOrientation com.ss.bytertc.engine.live.MixedStreamSpatialAudioConfig.audienceSpatialOrientation
```


The orientation of the audience. See [HumanOrientation](https://docs.byteplus.com/en/docs/12/14169#HumanOrientation).

The audience is the users who receive the audio stream from CDN.

<span id="instructions"></span>
## Instructions

<span id="MixedStreamSpatialAudioConfig-mixedstreamspatialaudioconfig"></span>
### MixedStreamSpatialAudioConfig

```java
public com.ss.bytertc.engine.live.MixedStreamSpatialAudioConfig.MixedStreamSpatialAudioConfig()
```


Sets spatial audio configurations.

<span id="LocalVideoStreamState"></span>
# LocalVideoStreamState

```java
public enum com.ss.bytertc.engine.type.LocalVideoStreamState
```


Local video stream status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|LOCAL_VIDEO_STREAM_STATE_STOPPED |0 |Local video capture stop state (default initial state)<br><br>&nbsp;<br><br>Callback this state when local video capture is closed, corresponding to the error code "LOCAL_VIDEO_STREAM_ERROR_OK" in [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStreamError) |
|LOCAL_VIDEO_STREAM_STATE_RECORDING |1 |Local video capture device starts successfully<br><br>&nbsp;<br><br>Callback this state when local video capture is started, corresponding to the error code 'LOCAL_VIDEO_STREAM_ERROR_OK 'in [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStreamError) |
|LOCAL_VIDEO_STREAM_STATE_ENCODING |2 |After local video capture, the first frame encoding is successful<br><br>&nbsp;<br><br>When the first frame encoding of the local video is successful, the state will be called back, corresponding to the error code "LOCAL_VIDEO_STREAM_ERROR_OK" in [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStreamError) |
|LOCAL_VIDEO_STREAM_STATE_FAILED |3 |Local video startup failed<br><br><br>&nbsp;<br><br>* Local video capture device failed to start, corresponding to the error code "LOCAL_VIDEO_STREAM_ERROR_FAILURE"<br><br>* No video capture device permission was detected in [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStreamError), corresponding to the error code "LOCAL_VIDEO_STREAM_ERROR_DEVICE_NO_PERMISSION"<br><br>* Video encoding failed, corresponding to the error code "LOCAL_VIDEO_STREAM_ERROR_ENCODE_FAILURE in [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14169#LocalVideoStreamError) ' |


<span id="ExpressionDetectInfo"></span>
# ExpressionDetectInfo

```java
public class com.ss.bytertc.engine.video.ExpressionDetectInfo
```


Expression detect information

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |\- |[age](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-age) |
|float |\- |[boyProb](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-boyprob) |
|float |\- |[attractive](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-attractive) |
|float |\- |[happyScore](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-happyscore) |
|float |\- |[sadScore](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-sadscore) |
|float |\- |[angryScore](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-angryscore) |
|float |\- |[surpriseScore](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-surprisescore) |
|float |\- |[arousal](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-arousal) |
|float |\- |[valence](https://docs.byteplus.com/en/docs/12/14169#ExpressionDetectInfo-valence) |


<span id="instructions"></span>
## Instructions

<span id="ExpressionDetectInfo-age"></span>
### age

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.age
```


The estimated age in the range of (0, 100).

<span id="ExpressionDetectInfo-boyprob"></span>
### boyProb

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.boyProb
```


The estimated probability of being a male in the range of (0.0, 1.0).

<span id="ExpressionDetectInfo-attractive"></span>
### attractive

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.attractive
```


The estimated attractiveness in the range of (0, 100).

<span id="ExpressionDetectInfo-happyscore"></span>
### happyScore

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.happyScore
```


The estimated happy score in the range of (0, 100).

<span id="ExpressionDetectInfo-sadscore"></span>
### sadScore

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.sadScore
```


The estimated sad score in the range of (0, 100).

<span id="ExpressionDetectInfo-angryscore"></span>
### angryScore

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.angryScore
```


The estimated angry score in the range of (0, 100).

<span id="ExpressionDetectInfo-surprisescore"></span>
### surpriseScore

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.surpriseScore
```


The estimated surprise score in the range of (0, 100).

<span id="ExpressionDetectInfo-arousal"></span>
### arousal

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.arousal
```


The estimated emotional arousal in the range of (0, 100).

<span id="ExpressionDetectInfo-valence"></span>
### valence

```java
public float com.ss.bytertc.engine.video.ExpressionDetectInfo.valence
```


The estimated emotional valence in the range of (\-100, 100).

<span id="RemoteAudioState"></span>
# RemoteAudioState

```java
public enum com.ss.bytertc.engine.data.RemoteAudioState
```


The remote audio stream state of the user subscription.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|REMOTE_AUDIO_STATE_STOPPED |0 |The default initial state of the remote audio stream is called back at the following times:<br><br><br>&nbsp;<br><br>* Local users stop receiving remote audio streams, the corresponding reason is `kRemoteAudioReasonLocalMuted` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason)<br><br>* The remote user stops sending audio streams, the corresponding reason is `kRemoteAudioReasonRemoteMuted` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason)<br><br>* The remote user leaves the room, the corresponding reason is `kRemoteAudioReasonRemoteOffline` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason) |
|REMOTE_AUDIO_STATE_STARTING |1 |Start receiving the remote audio stream header. |
|REMOTE_AUDIO_STATE_DECODING |2 |The remote audio stream is decoding and playing normally. The state is called back at the following times:<br><br><br>&nbsp;<br><br>* Successfully decoded the first frame of the remote audio, the corresponding reason is `kRemoteAudioReasonLocalUnmuted` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason)<br><br>* The network returned to normal from blocking, the corresponding reason is `kRemoteAudioReasonNetworkRecovery` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason)<br><br>* The local user resumes receiving the remote audio stream, the corresponding reason is `kRemoteAudioReasonLocalUnmuted` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason)<br><br>* The remote user resumes sending the audio stream, the corresponding reason is `kRemoteAudioReasonRemoteUnmuted` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason) |
|REMOTE_AUDIO_STATE_FROZEN |3 |Remote audio stream stalls.<br><br>&nbsp;<br><br>Callback to this state when the packet loss rate is greater than 40% due to network blocking, the corresponding reason is<br><br>&nbsp;<br><br>`kRemoteAudioReasonNetworkCongestion` in [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioStateChangeReason). |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#RemoteAudioState-value) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioState-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.RemoteAudioState.value()
```


Get current value

**Return Value**

Current value

<span id="FrameUpdateInfo"></span>
# FrameUpdateInfo

```java
public class com.ss.bytertc.engine.data.FrameUpdateInfo
```


The pixels and frame rate recommended by RTC.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[pixel](https://docs.byteplus.com/en/docs/12/14169#FrameUpdateInfo-pixel) |
|int |\- |[frameRate](https://docs.byteplus.com/en/docs/12/14169#FrameUpdateInfo-framerate) |


<span id="instructions"></span>
## Instructions

<span id="FrameUpdateInfo-pixel"></span>
### pixel

```java
public int com.ss.bytertc.engine.data.FrameUpdateInfo.pixel
```


Pixel (width \* height).

<span id="FrameUpdateInfo-framerate"></span>
### frameRate

```java
public int com.ss.bytertc.engine.data.FrameUpdateInfo.frameRate
```


The frame rate.

<span id="AudioPropertiesConfig"></span>
# AudioPropertiesConfig

```java
public class com.ss.bytertc.engine.data.AudioPropertiesConfig
```


Configuration related to audio attribute information prompt

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[interval](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesConfig-interval) |
|boolean |false |[enableSpectrum](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesConfig-enablespectrum) |
|boolean |false |[enableVad](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesConfig-enablevad) |
|AudioReportMode |AudioReportMode.AUDIO_REPORT_MODE_NORMAL |[localMainReportMode](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesConfig-localmainreportmode) |
|AudioPropertiesMode |AudioPropertiesMode.AUDIO_PROPERTIES_MODE_MICROPHONE |[audioReportMode](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesConfig-audioreportmode) |
|float |1.0f |[smooth](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesConfig-smooth) |
|boolean |false |[enableVoicePitch](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesConfig-enablevoicepitch) |


<span id="instructions"></span>
## Instructions

<span id="AudioPropertiesConfig-interval"></span>
### interval

```java
public int com.ss.bytertc.engine.data.AudioPropertiesConfig.interval
```


Prompt interval in ms


* `<= 0`: Turn off prompt

* `(0,100]`: Invalid interval value, and will be automatically reset to 100ms.

* `> 100`: the actual value of interval

    &nbsp;


<span id="enablespectrum"></span>
### enableSpectrum

```java
public boolean com.ss.bytertc.engine.data.AudioPropertiesConfig.enableSpectrum = false
```


Whether to enable audio spectrum detection

<span id="AudioPropertiesConfig-enablevad"></span>
### enableVad

```java
public boolean com.ss.bytertc.engine.data.AudioPropertiesConfig.enableVad = false
```


Whether to enable Voice Activity Detection

<span id="AudioPropertiesConfig-localmainreportmode"></span>
### localMainReportMode

```java
public AudioReportMode com.ss.bytertc.engine.data.AudioPropertiesConfig.localMainReportMode = AudioReportMode.AUDIO_REPORT_MODE_NORMAL
```


The volume callback modes. See [AudioReportMode](https://docs.byteplus.com/en/docs/12/14169#AudioReportMode).

<span id="AudioPropertiesConfig-audioreportmode"></span>
### audioReportMode

```java
public AudioPropertiesMode com.ss.bytertc.engine.data.AudioPropertiesConfig.audioReportMode = AudioPropertiesMode.AUDIO_PROPERTIES_MODE_MICROPHONE
```


The audio info included in [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalaudiopropertiesreport). See [AudioPropertiesMode](https://docs.byteplus.com/en/docs/12/14169#AudioPropertiesMode).

Locally captured microphone audio info and locally captured screen audio info are included by default.

<span id="AudioPropertiesConfig-smooth"></span>
### smooth

```java
public float com.ss.bytertc.engine.data.AudioPropertiesConfig.smooth = 1.0f
```


The smoothing coefficient for audio attribute information prompt. The range is `(0.0, 1.0]`.

The default value is `1.0`, which means the smoothing effect is off by default. The smaller the value, the smoother the audio volume prompt. If you want to enable the smooth effect, the recommended value is `0.3`.

<span id="AudioPropertiesConfig-enablevoicepitch"></span>
### enableVoicePitch

```java
public boolean com.ss.bytertc.engine.data.AudioPropertiesConfig.enableVoicePitch = false
```


Sets whether to return the vocal pitch of the local user.

<span id="VideoPixelFormat"></span>
# VideoPixelFormat

```java
public enum com.ss.bytertc.engine.data.VideoPixelFormat
```


Video frame pixel format

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|UNKNOWN |0 |Unknown format |
|I420 |1 |I420 |
|NV12 |2 |NV12 |
|NV21 |3 |NV21 |
|RGBA |5 |RGBA |
|TEXTURE_2D |GLES10.GL_TEXTURE_2D |Texture2D |
|TEXTURE_OES |GLES11Ext.GL_TEXTURE_EXTERNAL_OES |TextureOES |


<span id="LocalProxyError"></span>
# LocalProxyError

```java
public enum com.ss.bytertc.engine.type.LocalProxyError
```


The errors of local proxy connection.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|OK |0 |There are no errors in local proxies. |
|SOCKS5_VERSION_ERROR |1 |The connection to Socks5 proxy failed because the proxy server replies wrong version numbers which don't accord with the Socks5 document. Please check the proxy server. |
|SOCKS5_FORMAT_ERROR |2 |The connection to Socks5 proxy failed because the format of the proxy's replies does not accord with the Socks5 document. Please check the proxy server. |
|SOCKS5_INVALID_VALUE |3 |The connection to Socks5 proxy failed because the proxy replies wrong information which does not accord with the Socks5 document. Please check the proxy server. |
|SOCKS5_USER_PASS_NOT_GIVEN |4 |The connection to Socks5 proxy failed because the username and password of the local proxy are not provided. Please call `setLocalProxy` and enter your username and password. |
|SOCKS5_TCP_CLOSED |5 |The connection to Socks5 proxy failed because TCP is closed. Please check the proxy server and your network connection status. |
|HTTP_TUNNEL_FAILED |6 |Errors in Http tunnel proxy. Please check Http tunnel proxy and your network connection status. |


<span id="MediaStreamType"></span>
# MediaStreamType

```java
public enum com.ss.bytertc.engine.type.MediaStreamType
```


Media stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RTC_MEDIA_STREAM_TYPE_AUDIO |1 |Controls audio only |
|RTC_MEDIA_STREAM_TYPE_VIDEO |2 |Controls video only |
|RTC_MEDIA_STREAM_TYPE_BOTH |3 |Controls both audio and video |


<span id="RoomState"></span>
# RoomState

```java
public enum com.ss.bytertc.engine.type.RoomState
```


Room state code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|JOIN_SUCCESS |0 |Join room success. |
|JOIN_FAILED |1 |Join room failed. |
|LEFT |2 |Leave room. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static RoomState |[valueOf](https://docs.byteplus.com/en/docs/12/14169#RoomState-valueof) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|RoomState |[RoomState](https://docs.byteplus.com/en/docs/12/14169#RoomState-roomstate) |
|int |[value](https://docs.byteplus.com/en/docs/12/14169#RoomState-value) |


<span id="instructions"></span>
## Instructions

<span id="RoomState-valueof"></span>
### valueOf

```java
public static RoomState com.ss.bytertc.engine.type.RoomState.valueOf(int value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |\- |


<span id="RoomState-roomstate"></span>
### RoomState

```java
public com.ss.bytertc.engine.type.RoomState.RoomState(int value)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |\- |


<span id="RoomState-value"></span>
### value

```java
public int com.ss.bytertc.engine.type.RoomState.value()
```


<span id="MediaDeviceState"></span>
# MediaDeviceState

```java
public class com.ss.bytertc.engine.type.MediaDeviceState
```


Media device state

You will be informed of device state by `onAudioDeviceStateChanged`/`onVideoDeviceStateChanged`.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |1 |[MEDIA_DEVICE_STATE_STARTED](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceState-media_device_state_started) |
|int |2 |[MEDIA_DEVICE_STATE_STOPPED](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceState-media_device_state_stopped) |
|int |3 |[MEDIA_DEVICE_STATE_RUNTIMEERROR](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceState-media_device_state_runtimeerror) |
|int |10 |[MEDIA_DEVICE_STATE_ADDED](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceState-media_device_state_added) |
|int |11 |[MEDIA_DEVICE_STATE_REMOVED](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceState-media_device_state_removed) |
|int |12 |[MEDIA_DEVICE_STATE_INTERRUPTION_BEGAN](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceState-media_device_state_interruption_began) |
|int |13 |[MEDIA_DEVICE_STATE_INTERRUPTION_ENDED](https://docs.byteplus.com/en/docs/12/14169#MediaDeviceState-media_device_state_interruption_ended) |


<span id="instructions"></span>
## Instructions

<span id="MediaDeviceState-media_device_state_started"></span>
### MEDIA_DEVICE_STATE_STARTED

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceState.MEDIA_DEVICE_STATE_STARTED = 1
```


Device started capturing

<span id="MediaDeviceState-media_device_state_stopped"></span>
### MEDIA_DEVICE_STATE_STOPPED

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceState.MEDIA_DEVICE_STATE_STOPPED = 2
```


Device stopped capturing

<span id="MediaDeviceState-media_device_state_runtimeerror"></span>
### MEDIA_DEVICE_STATE_RUNTIMEERROR

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceState.MEDIA_DEVICE_STATE_RUNTIMEERROR = 3
```


Runtime error

For example, when the media device is expected to be working but no data is received.

<span id="MediaDeviceState-media_device_state_added"></span>
### MEDIA_DEVICE_STATE_ADDED

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceState.MEDIA_DEVICE_STATE_ADDED = 10
```


Device is added.

<span id="MediaDeviceState-media_device_state_removed"></span>
### MEDIA_DEVICE_STATE_REMOVED

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceState.MEDIA_DEVICE_STATE_REMOVED = 11
```


Device is removed.

<span id="MediaDeviceState-media_device_state_interruption_began"></span>
### MEDIA_DEVICE_STATE_INTERRUPTION_BEGAN

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceState.MEDIA_DEVICE_STATE_INTERRUPTION_BEGAN = 12
```


A Phone call interrupted the RTC call. RTC call will resume once the call ends.

<span id="MediaDeviceState-media_device_state_interruption_ended"></span>
### MEDIA_DEVICE_STATE_INTERRUPTION_ENDED

```java
public static final int com.ss.bytertc.engine.type.MediaDeviceState.MEDIA_DEVICE_STATE_INTERRUPTION_ENDED = 13
```


RTC call resumed from the interruption caused by a phone call.

<span id="LocalProxyType"></span>
# LocalProxyType

```java
public enum com.ss.bytertc.engine.type.LocalProxyType
```


Types of local proxies.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SOCKS5 |1 |Socks5 proxy. If you chose Socks5 as the local proxy, you need to make sure all requirements listed in the Socks5 document are satisfied. |
|HTTP_TUNNEL |2 |Http tunnel proxy. |


<span id="VoiceReverbConfig"></span>
# VoiceReverbConfig

```java
public class com.ss.bytertc.engine.type.VoiceReverbConfig
```


Voice reverb effect.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|float |50.0f |[roomSize](https://docs.byteplus.com/en/docs/12/14169#VoiceReverbConfig-roomsize) |
|float |50.0f |[decayTime](https://docs.byteplus.com/en/docs/12/14169#VoiceReverbConfig-decaytime) |
|float |50.0f |[damping](https://docs.byteplus.com/en/docs/12/14169#VoiceReverbConfig-damping) |
|float |0.0f |[wetGain](https://docs.byteplus.com/en/docs/12/14169#VoiceReverbConfig-wetgain) |
|float |0.0f |[dryGain](https://docs.byteplus.com/en/docs/12/14169#VoiceReverbConfig-drygain) |
|float |0.0f |[preDelay](https://docs.byteplus.com/en/docs/12/14169#VoiceReverbConfig-predelay) |


<span id="instructions"></span>
## Instructions

<span id="VoiceReverbConfig-roomsize"></span>
### roomSize

```java
public float com.ss.bytertc.engine.type.VoiceReverbConfig.roomSize = 50.0f
```


The room size for reverb simulation. The range is `[0.0, 100.0]`. The default value is `50.0f`. The larger the room, the stronger the reverberation.

<span id="VoiceReverbConfig-decaytime"></span>
### decayTime

```java
public float com.ss.bytertc.engine.type.VoiceReverbConfig.decayTime = 50.0f
```


The decay time of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="VoiceReverbConfig-damping"></span>
### damping

```java
public float com.ss.bytertc.engine.type.VoiceReverbConfig.damping = 50.0f
```


The damping index of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="VoiceReverbConfig-wetgain"></span>
### wetGain

```java
public float com.ss.bytertc.engine.type.VoiceReverbConfig.wetGain = 0.0f
```


The intensity of the wet signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="VoiceReverbConfig-drygain"></span>
### dryGain

```java
public float com.ss.bytertc.engine.type.VoiceReverbConfig.dryGain = 0.0f
```


The Intensity of the dry signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="VoiceReverbConfig-predelay"></span>
### preDelay

```java
public float com.ss.bytertc.engine.type.VoiceReverbConfig.preDelay = 0.0f
```


The delay of the wet signal in ms. The range is `[0.0, 200.0]`. The default value is `0.0f`.

<span id="AudioFrameType"></span>
# AudioFrameType

```java
public enum com.ss.bytertc.engine.data.AudioFrameType
```


Audio frame type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FRAME_TYPE_PCM16 |0 |PCM 16bit |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[value](https://docs.byteplus.com/en/docs/12/14169#AudioFrameType-value) |


<span id="instructions"></span>
## Instructions

<span id="AudioFrameType-value"></span>
### value

```java
public int com.ss.bytertc.engine.data.AudioFrameType.value()
```


Get current value

**Return Value**

Current value

<span id="PushSingleStreamParam"></span>
# PushSingleStreamParam

```java
public class com.ss.bytertc.engine.live.PushSingleStreamParam
```


Configurations for pushing a single media stream to CDN.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|String |\- |[roomId](https://docs.byteplus.com/en/docs/12/14169#PushSingleStreamParam-roomid) |
|String |\- |[userId](https://docs.byteplus.com/en/docs/12/14169#PushSingleStreamParam-userid) |
|String |\- |[url](https://docs.byteplus.com/en/docs/12/14169#PushSingleStreamParam-url) |
|boolean |false |[isScreen](https://docs.byteplus.com/en/docs/12/14169#PushSingleStreamParam-isscreen) |
|List<DestInfo\> |\- |[destInfos](https://docs.byteplus.com/en/docs/12/14169#PushSingleStreamParam-destinfos) |
|SingleStreamPushType |SingleStreamPushType.SINGLE_STREAM_PUSH_TYPE_TO_CDN |[pushType](https://docs.byteplus.com/en/docs/12/14169#PushSingleStreamParam-pushtype) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|PushSingleStreamParam |[PushSingleStreamParam](https://docs.byteplus.com/en/docs/12/14169#PushSingleStreamParam-pushsinglestreamparam-3) |


<span id="instructions"></span>
## Instructions

<span id="PushSingleStreamParam-roomid"></span>
### roomId

```java
public String com.ss.bytertc.engine.live.PushSingleStreamParam.roomId
```


The room ID of the media stream

<span id="PushSingleStreamParam-userid"></span>
### userId

```java
public String com.ss.bytertc.engine.live.PushSingleStreamParam.userId
```


The user ID of the media stream

<span id="PushSingleStreamParam-url"></span>
### url

```java
public String com.ss.bytertc.engine.live.PushSingleStreamParam.url
```


The URL for live transcoding. Only supports live transcoding via RTMP. The URL should match the regular expression `/^rtmps?:\\/\\//`.

This parameter cannot be updated while pushing stream to the CDN.

<span id="PushSingleStreamParam-isscreen"></span>
### isScreen

```java
public boolean com.ss.bytertc.engine.live.PushSingleStreamParam.isScreen = false
```


Reserved field. Do not set this field in the single\-stream SDK.

<span id="PushSingleStreamParam-destinfos"></span>
### destInfos

```java
public List<DestInfo> com.ss.bytertc.engine.live.PushSingleStreamParam.destInfos
```


Array of destination room info for cross\-room media stream forwarding, null by default.

When you need to forward media streams from current room to other rooms, you can specify multiple destination room info in this list.

Each DestInfo contains roomId and userId of the destination room. See details in [DestInfo](https://docs.byteplus.com/en/docs/12/14169#DestInfo).

<span id="PushSingleStreamParam-pushtype"></span>
### pushType

```java
public SingleStreamPushType com.ss.bytertc.engine.live.PushSingleStreamParam.pushType = SingleStreamPushType.SINGLE_STREAM_PUSH_TYPE_TO_CDN
```


Single stream push type, specifying whether to push the media stream to CDN or RTC room. Default value is push to CDN. See [SingleStreamPushType](https://docs.byteplus.com/en/docs/12/14169#SingleStreamPushType).

<span id="instructions"></span>
## Instructions

<span id="PushSingleStreamParam-pushsinglestreamparam-3"></span>
### PushSingleStreamParam

```java
public com.ss.bytertc.engine.live.PushSingleStreamParam.PushSingleStreamParam(
    String rid,
    String uid,
    String url,
    boolean isScreen
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rid |String |\- |
|uid |String |\- |
|url |String |\- |
|isScreen |boolean |Reserved. |


<span id="RecordingFileType"></span>
# RecordingFileType

```java
public enum com.ss.bytertc.engine.type.RecordingFileType
```


Storage format of locally recorded files

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AAC |0 |aac format file |
|MP4 |1 |mp4 format file |


<span id="RTCNativeLibraryLoader"></span>
# RTCNativeLibraryLoader

```java
public interface com.ss.bytertc.engine.loader.RTCNativeLibraryLoader
```


User\-defined dynamic library loader implementation

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|boolean |[load](https://docs.byteplus.com/en/docs/12/14169#RTCNativeLibraryLoader-load) |


<span id="instructions"></span>
## Instructions

<span id="RTCNativeLibraryLoader-load"></span>
### load

```java
boolean com.ss.bytertc.engine.loader.RTCNativeLibraryLoader.load(String libraryName)
```


SDK callbacks through this method when dynamic libraries need to be loaded

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|libraryName |String |The name of the dynamic library to be loaded |


<span id="ScreenMediaType"></span>
# ScreenMediaType

```java
public enum com.ss.bytertc.engine.data.ScreenMediaType
```


Screen media type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SCREEN_MEDIA_TYPE_VIDEO_ONLY |0 |Capture video. |
|SCREEN_MEDIA_TYPE_AUDIO_ONLY |1 |Capture audio. |
|SCREEN_MEDIA_TYPE_VIDEO_AND_AUDIO |2 |Capture audio and video. |


<span id="RTCWatermarkConfig"></span>
# RTCWatermarkConfig

```java
public class com.ss.bytertc.engine.video.RTCWatermarkConfig
```


Watermark configurations

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|boolean |true |[visibleInPreview](https://docs.byteplus.com/en/docs/12/14169#RTCWatermarkConfig-visibleinpreview) |
|ByteWatermark |\- |[positionInLandscapeMode](https://docs.byteplus.com/en/docs/12/14169#RTCWatermarkConfig-positioninlandscapemode) |
|ByteWatermark |\- |[positionInPortraitMode](https://docs.byteplus.com/en/docs/12/14169#RTCWatermarkConfig-positioninportraitmode) |


<span id="instructions"></span>
## Instructions

<span id="RTCWatermarkConfig-visibleinpreview"></span>
### visibleInPreview

```java
public boolean com.ss.bytertc.engine.video.RTCWatermarkConfig.visibleInPreview = true
```


Whether the watermark is visible in preview. Its default value is `true`.

<span id="RTCWatermarkConfig-positioninlandscapemode"></span>
### positionInLandscapeMode

```java
public ByteWatermark com.ss.bytertc.engine.video.RTCWatermarkConfig.positionInLandscapeMode
```


Watermark's coordinates and size in landscape mode. See [ByteWatermark](https://docs.byteplus.com/en/docs/12/14169#ByteWatermark).

<span id="RTCWatermarkConfig-positioninportraitmode"></span>
### positionInPortraitMode

```java
public ByteWatermark com.ss.bytertc.engine.video.RTCWatermarkConfig.positionInPortraitMode
```


Watermark's coordinates and size in portrait mode. See [ByteWatermark](https://docs.byteplus.com/en/docs/12/14169#ByteWatermark).

<span id="MixedStreamVideoConfig"></span>
# MixedStreamVideoConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamVideoConfig
```


Video transcoding configurations. With invalid or empty input, the configurations will be set as the default values.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|MixedStreamVideoConfig |[MixedStreamVideoConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamVideoConfig-mixedstreamvideoconfig) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamVideoConfig-mixedstreamvideoconfig"></span>
### MixedStreamVideoConfig

```java
public com.ss.bytertc.engine.live.MixedStreamVideoConfig.MixedStreamVideoConfig()
```


<span id="VirtualBackgroundSourceType"></span>
# VirtualBackgroundSourceType

```java
public enum com.ss.bytertc.engine.data.VirtualBackgroundSourceType
```


Virtual background types.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|COLOR |0 |Replace the background with a solid color. |
|IMAGE |1 |Replace the background with the specified image. |


<span id="AudioRenderType"></span>
# AudioRenderType

```java
public enum com.ss.bytertc.engine.data.AudioRenderType
```


Audio output source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_RENDER_TYPE_EXTERNAL |0 |Custom rendering |
|AUDIO_RENDER_TYPE_INTERNAL |1 |Internal rendering |


<span id="VideoDeviceFacing"></span>
# VideoDeviceFacing

```java
public enum com.ss.bytertc.engine.type.VideoDeviceFacing
```


> Available since 3.56


video device facing type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|FRONT |0 |Front\-facing video camera |
|BACK |1 |Back\-facing video camera |
|UNKNOWN |2 |video camera facing unknown |


<span id="SubscribeFallbackOptions"></span>
# SubscribeFallbackOptions

```java
public enum com.ss.bytertc.engine.type.SubscribeFallbackOptions
```


Stream fallback options of subscriber

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SUBSCRIBE_FALLBACK_OPTIONS_DISABLED |0 |Default setting. No fallback is allowed under limited network conditions. |
|SUBSCRIBE_FALLBACK_OPTIONS_STREAM_LOW |1 |The resolution of currently subscribed video stream will be reduced under limited network conditions, see [Stream Fallback](https://docs.byteplus.com/en/docs/12/docs-70137) for details.<br><br>&nbsp;<br><br>You can only select this setting after the stream publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalsimulcastmode-2) to enable the mode of publishing multiple streams, otherwise no fallback will occur. |
|SUBSCRIBE_FALLBACK_OPTIONS_AUDIO_ONLY |2 |The resolution of currently subscribed video stream will be reduced first under limited network conditions. When the network condition is not sufficient to receive the minimum resolution stream, the video is automatically cancelled and only the audio is received.<br><br>&nbsp;<br><br>You can only select this setting after the stream publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalsimulcastmode-2) to enable the mode of publishing multiple streams, otherwise no fallback will occur. |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static SubscribeFallbackOptions |[fromId](https://docs.byteplus.com/en/docs/12/14169#SubscribeFallbackOptions-fromid) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeFallbackOptions-fromid"></span>
### fromId

```java
public static SubscribeFallbackOptions com.ss.bytertc.engine.type.SubscribeFallbackOptions.fromId(int id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|id |int |\- |


<span id="MixedStreamPushTargetType"></span>
# MixedStreamPushTargetType

```java
public enum com.ss.bytertc.engine.live.MixedStreamPushTargetType
```


Task type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|PUSH_TO_CDN |0 |Push to CDN. |
|PUSH_TO_WTN |1 |WTN stream |


<span id="InterpolationMode"></span>
# InterpolationMode

```java
public enum com.ss.bytertc.engine.live.InterpolationMode
```


Interpolation mode of the WTN stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|LAST_FRAME_FILL |0 |Fill with the last frame. |
|BACKGROUND_IMAGE_FILL |1 |Fill with the background image. |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|InterpolationMode |[InterpolationMode](https://docs.byteplus.com/en/docs/12/14169#InterpolationMode-interpolationmode) |
|int |[value](https://docs.byteplus.com/en/docs/12/14169#InterpolationMode-value) |


<span id="instructions"></span>
## Instructions

<span id="InterpolationMode-interpolationmode"></span>
### InterpolationMode

```java
public com.ss.bytertc.engine.live.InterpolationMode.InterpolationMode(int value)
```


Sets the interpolationMode mode of the WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|value |int |The interpolationMode mode of the WTN stream. |


<span id="InterpolationMode-value"></span>
### value

```java
public int com.ss.bytertc.engine.live.InterpolationMode.value()
```


Get the interpolation mode of the WTN stream.

<span id="ZoomDirectionType"></span>
# ZoomDirectionType

```java
public enum com.ss.bytertc.engine.data.ZoomDirectionType
```


Action of the digital zoom control

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|CAMERA_MOVE_LEFT |0 |Move to the left. |
|CAMERA_MOVE_RIGHT |1 |Move to the right. |
|CAMERA_MOVE_UP |2 |Move upwards. |
|CAMERA_MOVE_DOWN |3 |Move downwards. |
|CAMERA_ZOOM_OUT |4 |Zoom out. |
|CAMERA_ZOOM_IN |5 |Zoom in. |
|CAMERA_RESET |6 |Reset digital zoom. |


<span id="VideoBufferType"></span>
# VideoBufferType

```java
public enum com.ss.bytertc.engine.data.VideoBufferType
```


video buffer type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RAW_MEMORY |0 |raw memory |
|GL_TEXTURE |2 |GL Texture |


<span id="StandardPitchInfo"></span>
# StandardPitchInfo

```java
public class com.ss.bytertc.engine.data.StandardPitchInfo
```


Standard Pitch Data.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\- |[startTime](https://docs.byteplus.com/en/docs/12/14169#StandardPitchInfo-starttime) |
|int |\- |[duration](https://docs.byteplus.com/en/docs/12/14169#StandardPitchInfo-duration) |
|int |\- |[pitch](https://docs.byteplus.com/en/docs/12/14169#StandardPitchInfo-pitch) |


<span id="instructions"></span>
## Instructions

<span id="StandardPitchInfo-starttime"></span>
### startTime

```java
public int com.ss.bytertc.engine.data.StandardPitchInfo.startTime
```


Starting time, unit: ms.

<span id="StandardPitchInfo-duration"></span>
### duration

```java
public int com.ss.bytertc.engine.data.StandardPitchInfo.duration
```


Duration, unit: ms.

<span id="StandardPitchInfo-pitch"></span>
### pitch

```java
public int com.ss.bytertc.engine.data.StandardPitchInfo.pitch
```


pitch.

<span id="AudioMixingType"></span>
# AudioMixingType

```java
public enum com.ss.bytertc.engine.data.AudioMixingType
```


Mixing type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_MIXING_TYPE_PLAYOUT |0 |Played at the local device only |
|AUDIO_MIXING_TYPE_PUBLISH |1 |Sent to the remote devices only |
|AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH |2 |Played at the local device and sent to the remote devices. |


<span id="AttenuationType"></span>
# AttenuationType

```java
public enum com.ss.bytertc.engine.type.AttenuationType
```


Volume Roll\-off modes that a sound has in an audio source

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ATTENUATION_TYPE_NONE |0 |Disable Volume Attenuation |
|ATTENUATION_TYPE_LINEAR |1 |Linear roll\-off mode which lowers the volume of the sound over the distance |
|ATTENUATION_TYPE_EXPONENTIAL |2 |Exponential roll\-off mode which exponentially decreases the volume of the sound with the distance raising |


<span id="MediaPlayerCustomSourceStreamType"></span>
# MediaPlayerCustomSourceStreamType

```java
public enum com.ss.bytertc.engine.data.MediaPlayerCustomSourceStreamType
```


Custom audio source stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|RAW |0 |When you use the local PCM data, use this type. |
|ENCODED |1 |When you use the audio data from local memory, use this type. |


<span id="AlphaLayout"></span>
# AlphaLayout

```java
public enum com.ss.bytertc.engine.data.AlphaLayout
```


The arrangement position of the Alpha channel data relative to the RGB channel data.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|TOP |0 |The Alpha channel data is on top of the RGB channel data. |


<span id="MixedStreamConfig"></span>
# MixedStreamConfig

```java
public class com.ss.bytertc.engine.live.MixedStreamConfig
```


Stream\-mixing task configurations.

If not specified, the parameter can be used for both WTN stream and mixing\-stream tasks.

If not specified, the parameter can be passed when starting a task or during a task.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|MixedStreamVideoConfig |\- |[videoConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-videoconfig) |
|MixedStreamAudioConfig |\- |[audioConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-audioconfig) |
|MixedStreamControlConfig |\- |[controlConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-controlconfig) |
|MixedStreamSpatialAudioConfig |\- |[spatialAudioConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-spatialaudioconfig) |
|MixedStreamLayoutRegionConfig |null |[regions](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-regions) |
|String |"" |[userConfigExtraInfo](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-userconfigextrainfo) |
|String |"#000000" |[backgroundColor](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-backgroundcolor) |
|String |"" |[backgroundImageURL](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-backgroundimageurl) |
|String |"" |[roomID](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-roomid) |
|String |"" |[userID](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-userid) |
|InterpolationMode |InterpolationMode.LAST_FRAME_FILL |[interpolationMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-interpolationmode) |
|StreamLayoutMode |StreamLayoutMode.AUTO |[layoutMode](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-layoutmode) |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static MixedStreamConfig |[defaultMixedStreamConfig](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-defaultmixedstreamconfig) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|boolean |[getMixedStreamVideoConfigBFrame](https://docs.byteplus.com/en/docs/12/14169#MixedStreamConfig-getmixedstreamvideoconfigbframe) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamConfig-videoconfig"></span>
### videoConfig

```java
public MixedStreamVideoConfig com.ss.bytertc.engine.live.MixedStreamConfig.videoConfig
```


Sets the video transcoding configurations. It's recommended to be set.

<span id="MixedStreamConfig-audioconfig"></span>
### audioConfig

```java
public MixedStreamAudioConfig com.ss.bytertc.engine.live.MixedStreamConfig.audioConfig
```


Sets audio transcoding configurations. It's recommended to be set.

<span id="MixedStreamConfig-controlconfig"></span>
### controlConfig

```java
public MixedStreamControlConfig com.ss.bytertc.engine.live.MixedStreamConfig.controlConfig
```


> Available since 3.56


Sets the configurations during mixing streams on the server side.

<span id="MixedStreamConfig-spatialaudioconfig"></span>
### spatialAudioConfig

```java
public MixedStreamSpatialAudioConfig com.ss.bytertc.engine.live.MixedStreamConfig.spatialAudioConfig
```


Sets the spatial audio configuration when pushing streams to CDN.

<span id="MixedStreamConfig-regions"></span>
### regions

```java
public MixedStreamLayoutRegionConfig com.ss.bytertc.engine.live.MixedStreamConfig.regions[] = null
```


Sets the user layout information list.

<span id="MixedStreamConfig-userconfigextrainfo"></span>
### userConfigExtraInfo

```java
public String com.ss.bytertc.engine.live.MixedStreamConfig.userConfigExtraInfo = ""
```


set user config extra information.

**Notes**

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamConfig-backgroundcolor"></span>
### backgroundColor

```java
public String com.ss.bytertc.engine.live.MixedStreamConfig.backgroundColor = "#000000"
```


Sets the background color of the canvas. With invalid or empty input, the configurations will be set as the default values.

<span id="MixedStreamConfig-backgroundimageurl"></span>
### backgroundImageURL

```java
public String com.ss.bytertc.engine.live.MixedStreamConfig.backgroundImageURL = ""
```


> Available since 3.57


Sets the URL of the background image for the canvas that renders the mixed stream

<span id="MixedStreamConfig-roomid"></span>
### roomID

```java
public String com.ss.bytertc.engine.live.MixedStreamConfig.roomID = ""
```


Set the room ID to specify where the streams to be mixed are sourced from.

**Notes**

This parameter cannot be updated during the task.

<span id="MixedStreamConfig-userid"></span>
### userID

```java
public String com.ss.bytertc.engine.live.MixedStreamConfig.userID = ""
```


Sets the user ID to specify who started the mixing\-stream task. The sum length of `roomID` and `userID` should not exceed 126 bytes. It's recommended to be set.

This parameter cannot be updated during the.

<span id="MixedStreamConfig-interpolationmode"></span>
### interpolationMode

```java
public InterpolationMode com.ss.bytertc.engine.live.MixedStreamConfig.interpolationMode = InterpolationMode.LAST_FRAME_FILL
```


Sets the interpolationMode mode of the WTN stream. See [InterpolationMode](https://docs.byteplus.com/en/docs/12/14169#InterpolationMode).

<span id="MixedStreamConfig-layoutmode"></span>
### layoutMode

```java
public StreamLayoutMode com.ss.bytertc.engine.live.MixedStreamConfig.layoutMode = StreamLayoutMode.AUTO
```


Sets the layout mode of the WTN stream. See [StreamLayoutMode](https://docs.byteplus.com/en/docs/12/14169#StreamLayoutMode).

<span id="instructions"></span>
## Instructions

<span id="MixedStreamConfig-defaultmixedstreamconfig"></span>
### defaultMixedStreamConfig

```java
public static MixedStreamConfig com.ss.bytertc.engine.live.MixedStreamConfig.defaultMixedStreamConfig()
```


<span id="MixedStreamConfig-getmixedstreamvideoconfigbframe"></span>
### getMixedStreamVideoConfigBFrame

```java
public boolean com.ss.bytertc.engine.live.MixedStreamConfig.getMixedStreamVideoConfigBFrame()
```


<span id="SEICountPerFrame"></span>
# SEICountPerFrame

```java
public enum com.ss.bytertc.engine.data.SEICountPerFrame
```


SEI sending mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|SEI_COUNT_PER_FRAME_SINGLE |0 |Single\-SEI mode. A single video frame carries at most one SEI message.<br><br>When you send multiple SEI messages in 1 frame, they will be sent in sequence following consecutive video frames.<br><br>For example, if you need to send 3 SEI data within a certain frame, then the 1st SEI will be sent in the current frame, the 2nd SEI will be sent in the next frame, and the 3rd SEI will be sent in the frame after that. |
|SEI_COUNT_PER_FRAME_MULTI |1 |Multi\-SEI mode.<br><br>When you send multiple SEI messages in 1 frame, all these SEI data will be sent together in the next frame, which can reduce sending delay, but a frame will carry multiple SEI messages.<br><br>For example, if there are 3 SEI data to be sent within a 1\-frame interval, these 3 SEIs will all be sent on the next video frame. |
