---
title: "Keytype"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70098"
---

<span id="PositionInfo"></span>
# PositionInfo

```cpp
struct bytertc::PositionInfo
```


Information on the user's position in the rectangular coordinate system for the spatial audio.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|Position |[position](https://docs.byteplus.com/en/docs/12/14187#PositionInfo-position) |
|HumanOrientation |[orientation](https://docs.byteplus.com/en/docs/12/14187#PositionInfo-orientation) |


<span id="instructions"></span>
## Instructions

<span id="PositionInfo-position"></span>
### position

```cpp
Position bytertc::PositionInfo::position
```


3D coordinate values of the user's position in the rectangular coordinate system for the spatial audio. You need to build your own rectangular coordinate system. Refer to [Position](https://docs.byteplus.com/en/docs/12/14187#Position) for details.

<span id="PositionInfo-orientation"></span>
### orientation

```cpp
HumanOrientation bytertc::PositionInfo::orientation
```


Information on the three\-dimensional orientation of the user in the rectangular coordinate system for the spatial audio. Any two of the 3D coordinate vectors of the user's position need to be perpendicular to each other. Refer to [HumanOrientation](https://docs.byteplus.com/en/docs/12/14187#HumanOrientation) for details.

<span id="LocalAudioStreamError"></span>
# LocalAudioStreamError

```cpp
enum bytertc::LocalAudioStreamError
```


Error code when the state of the local audio stream changes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalAudioStreamErrorOk |0 |Local audio status is normal |
|kLocalAudioStreamErrorFailure |1 |Local audio error cause unknown |
|kLocalAudioStreamErrorDeviceNoPermission |2 |No permission to start local audio recording device |
|kLocalAudioStreamErrorRecordFailure |4 |Local audio recording failed, it is recommended that you check whether the recording device is working properly |
|kLocalAudioStreamErrorEncodeFailure |5 |Local audio encoding failed |
|kLocalAudioStreamErrorNoRecordingDevice |6 |No audio recording equipment available |


<span id="ZoomConfigType"></span>
# ZoomConfigType

```cpp
enum bytertc::ZoomConfigType
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

```cpp
enum bytertc::AudioFrameSource
```


Audio file recording source type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioFrameSourceMic |0 |The audio captured by the local microphone. |
|kAudioFrameSourcePlayback |1 |The audio obtained by mixing all remote users' audio. |
|kAudioFrameSourceMixed |2 |The audio got by mixing the local captured audio and all remote user's audio. |


<span id="CameraID"></span>
# CameraID

```cpp
enum bytertc::CameraID
```


camera.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kCameraIDFront |0 |Front\-facing camera for mobile, build\-in camera for PC |
|kCameraIDBack |1 |Rear camera for mobile, PC is undefined for camera 1 |
|kCameraIDInvalid |3 |Invalid value |


<span id="AudioDeviceInfo"></span>
# AudioDeviceInfo

```cpp
struct bytertc::AudioDeviceInfo
```


Audio device information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|char[MAX_DEVICE_ID_LENGTH] |[device_id](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-device_id) |
|char[MAX_DEVICE_ID_LENGTH] |[device_name](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-device_name) |
|char[MAX_DEVICE_ID_LENGTH] |[device_short_name](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-device_short_name) |
|char[MAX_DEVICE_ID_LENGTH] |[device_container_id](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-device_container_id) |
|int64_t |[device_vid](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-device_vid) |
|int64_t |[device_pid](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-device_pid) |
|DeviceTransportType |[transport_type](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-transport_type) |
|AudioAbilityType |[volume_settable](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-volume_settable) |
|bool |[is_system_default](https://docs.byteplus.com/en/docs/12/14187#AudioDeviceInfo-is_system_default) |


<span id="instructions"></span>
## Instructions

<span id="AudioDeviceInfo-device_id"></span>
### device_id

```cpp
char bytertc::AudioDeviceInfo::device_id[MAX_DEVICE_ID_LENGTH]
```


Device ID

<span id="AudioDeviceInfo-device_name"></span>
### device_name

```cpp
char bytertc::AudioDeviceInfo::device_name[MAX_DEVICE_ID_LENGTH]
```


Friendly name of the audio adapter to which the endpoint device is attached. For example, "Speakers (XYZ Audio Adapter)"

<span id="AudioDeviceInfo-device_short_name"></span>
### device_short_name

```cpp
char bytertc::AudioDeviceInfo::device_short_name[MAX_DEVICE_ID_LENGTH]
```


Friendly name of the endpoint device. For example, "XYZ Audio Adapter"

<span id="AudioDeviceInfo-device_container_id"></span>
### device_container_id

```cpp
char bytertc::AudioDeviceInfo::device_container_id[MAX_DEVICE_ID_LENGTH]
```


ID of the sound card connected to the audio device. With this variable, you can choose the speaker and microphone connected to the same sound card with ease.

<span id="AudioDeviceInfo-device_vid"></span>
### device_vid

```cpp
int64_t bytertc::AudioDeviceInfo::device_vid
```


ID of the device vendor

<span id="AudioDeviceInfo-device_pid"></span>
### device_pid

```cpp
int64_t bytertc::AudioDeviceInfo::device_pid
```


Product number of the device

<span id="AudioDeviceInfo-transport_type"></span>
### transport_type

```cpp
DeviceTransportType bytertc::AudioDeviceInfo::transport_type
```


Connection type of the device

<span id="AudioDeviceInfo-volume_settable"></span>
### volume_settable

```cpp
AudioAbilityType bytertc::AudioDeviceInfo::volume_settable
```


Accessibility to the volume setting

<span id="AudioDeviceInfo-is_system_default"></span>
### is_system_default

```cpp
bool bytertc::AudioDeviceInfo::is_system_default
```


Whether the device is the default device

<span id="RoomEvent"></span>
# RoomEvent

```cpp
enum bytertc::RoomEvent
```


Room event code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRoomEventUserNotifyStop |\-2013 |When the number of people in the room exceeds 500, stop sending `onUserJoined` and `onUserLeave` callbacks to existing users in the room, and prompt all users in the room via broadcast. |
|kRoomEventForbidden |\-2012 |When the room or user is forbidden, notice forbidden time. |
|kRoomEventRetryOnServerError |\-2014 |When the room or user is forbidden, notice forbidden time. |


<span id="DesktopCaptureParameters"></span>
# DesktopCaptureParameters

```cpp
struct bytertc::DesktopCaptureParameters
```


The encoding configuration for screen sharing.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[max_width](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-max_width) |
|int |[max_height](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-max_height) |
|int |[frame_rate](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-frame_rate) |
|int |[bitrate](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-bitrate) |
|int |[min_bitrate](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-min_bitrate) |
|bool |[capture_mouse_cursor](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-capture_mouse_cursor) |
|view_t\* |[excluded_window_list](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-excluded_window_list) |
|int |[excluded_window_num](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-excluded_window_num) |
|HighlightConfig |[highlight_config](https://docs.byteplus.com/en/docs/12/14187#DesktopCaptureParameters-highlight_config) |


<span id="instructions"></span>
## Instructions

<span id="DesktopCaptureParameters-max_width"></span>
### max_width

```cpp
int bytertc::DesktopCaptureParameters::max_width = 1920
```


The maximum width(in px).

<span id="DesktopCaptureParameters-max_height"></span>
### max_height

```cpp
int bytertc::DesktopCaptureParameters::max_height = 1080
```


The maximum height(in px).

<span id="DesktopCaptureParameters-frame_rate"></span>
### frame_rate

```cpp
int bytertc::DesktopCaptureParameters::frame_rate = 15
```


The frame rate(in fps).

<span id="DesktopCaptureParameters-bitrate"></span>
### bitrate

```cpp
int bytertc::DesktopCaptureParameters::bitrate = -1
```


The bitrate. If you set this value to \-1, RTC will automatically recommend the bitrate(in kbps) based on the input resolution.

<span id="DesktopCaptureParameters-min_bitrate"></span>
### min_bitrate

```cpp
int bytertc::DesktopCaptureParameters::min_bitrate = 0
```


The minimum bitrate (in Kbps). Optional for internal capture while mandatory for custom capture.

The minimum bitrate must be set lower than the maximum bitrate. Otherwise, the streams will not be encoded and published.

<span id="DesktopCaptureParameters-capture_mouse_cursor"></span>
### capture_mouse_cursor

```cpp
bool bytertc::DesktopCaptureParameters::capture_mouse_cursor = true
```


Whether to capture the mouse cursor.

<span id="DesktopCaptureParameters-excluded_window_list"></span>
### excluded_window_list

```cpp
view_t* bytertc::DesktopCaptureParameters::excluded_window_list = nullptr
```


The list of windows excluded from screen capture. This parameter only takes effect when you capture your screen.

<span id="DesktopCaptureParameters-excluded_window_num"></span>
### excluded_window_num

```cpp
int bytertc::DesktopCaptureParameters::excluded_window_num = 0
```


The number of windows excluded from screen capture.

<span id="DesktopCaptureParameters-highlight_config"></span>
### highlight_config

```cpp
HighlightConfig bytertc::DesktopCaptureParameters::highlight_config
```


Configure how a border is highlighted.

<span id="AudioScenarioType"></span>
# AudioScenarioType

```cpp
enum bytertc::AudioScenarioType
```


Audio scenarios.

After selecting the audio scenario, the SDK will automatically select the call/media volume, according to the OS and microphone status. For more information, see [What is the difference between in-call volume and media volume?](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-651068).

You can set the audio scenario by calling `setAudioScenario`.

If the following audio scenarios cannot meet your business needs, please contact our technical support team.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioScenarioTypeDefault |0 |Default scenario. |
|kAudioScenarioTypeChatRoom |1 |Chat room scenario. The call clarity is higher, suitable for meetings, chat rooms, etc. |
|kAudioScenarioTypeGameStreaming |2 |High\-quality scenario. Suitable for scenarios with music, such as Karaoke. |
|kAudioScenarioTypeChorus |3 |Chorus scenario. Low latency. |
|kAudioScenarioTypeEducation |4 |Education scenario. Suitable for high\-fidelity audio scenarios dominated by human\-voice teaching content. |
|kAudioScenarioTypeAiClient |5 |AI dialogue scenario: Applicable to scenarios where real humans interact with AI agents. |


<span id="AVSyncState"></span>
# AVSyncState

```cpp
enum bytertc::AVSyncState
```


A/V synchronization states

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAVSyncStateAVStreamSyncBegin |0 |A/V synchronization begins. |
|kAVSyncStateAudioStreamRemove |1 |The publisher stops publishing the video stream during the synchronization, which does not affect the sync relationship. |
|kAVSyncStateVdieoStreamRemove |2 |The publisher stops publishing the video stream during the synchronization, which does not affect the sync relationship. |


<span id="VideoFrameData"></span>
# VideoFrameData

```cpp
struct bytertc::VideoFrameData
```


Video frame data

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VideoBufferType |[buffer_type](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-buffer_type) |
|VideoPixelFormat |[pixel_format](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-pixel_format) |
|VideoContentType |[content_type](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-content_type) |
|int |[number_of_planes](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-number_of_planes) |
|uint8_t\*[4] |[plane_data](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-plane_data) |
|int[4] |[plane_stride](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-plane_stride) |
|uint8_t\* |[sei_data](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-sei_data) |
|int |[sei_data_size](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-sei_data_size) |
|uint8_t\* |[roi_data](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-roi_data) |
|int |[roi_data_size](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-roi_data_size) |
|int |[width](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-height) |
|VideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-rotation) |
|int64_t |[timestamp_us](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-timestamp_us) |
|void\* |[hw_buffer](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-hw_buffer) |
|void\* |[hw_context](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-hw_context) |
|float[16] |[texture_matrix](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-texture_matrix) |
|uint32_t |[texture_id](https://docs.byteplus.com/en/docs/12/14187#VideoFrameData-texture_id) |


<span id="instructions"></span>
## Instructions

<span id="VideoFrameData-buffer_type"></span>
### buffer_type

```cpp
VideoBufferType bytertc::VideoFrameData::buffer_type = kVideoBufferTypeRawMemory
```


Video frame buffer type, the default value is raw memory. See [VideoBufferType](https://docs.byteplus.com/en/docs/12/14187#VideoBufferType). Required.

<span id="VideoFrameData-pixel_format"></span>
### pixel_format

```cpp
VideoPixelFormat bytertc::VideoFrameData::pixel_format = kVideoPixelFormatUnknown
```


Video frame pixel format. See [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14187#VideoPixelFormat). Required, when `buffer_type` is `kVideoBufferTypeRawMemory` or `kVideoFrameTypeGLTexture`.

<span id="VideoFrameData-content_type"></span>
### content_type

```cpp
VideoContentType bytertc::VideoFrameData::content_type = kVideoContentTypeNormalFrame
```


Video frame content type. See [VideoContentType](https://docs.byteplus.com/en/docs/12/14187#VideoContentType)

<span id="VideoFrameData-number_of_planes"></span>
### number_of_planes

```cpp
int bytertc::VideoFrameData::number_of_planes = 0
```


Number of video frame planes. Required, `buffer_type` is `kVideoBufferTypeRawMemory`.

<span id="VideoFrameData-plane_data"></span>
### plane_data

```cpp
uint8_t* bytertc::VideoFrameData::plane_data[4] = { nullptr }
```


Array of video frame plane. Required, when `buffer_type` is `kVideoBufferTypeRawMemory`.

<span id="VideoFrameData-plane_stride"></span>
### plane_stride

```cpp
int bytertc::VideoFrameData::plane_stride[4] = { 0 }
```


Array of stride. Stride is the length of memory between two lines of image data in video frame plane in bytes. Required, when `buffer_type` is `kVideoBufferTypeRawMemory`.

<span id="VideoFrameData-sei_data"></span>
### sei_data

```cpp
uint8_t* bytertc::VideoFrameData::sei_data = nullptr
```


SEI data

<span id="VideoFrameData-sei_data_size"></span>
### sei_data_size

```cpp
int bytertc::VideoFrameData::sei_data_size = 0
```


SEI data size

<span id="VideoFrameData-roi_data"></span>
### roi_data

```cpp
uint8_t* bytertc::VideoFrameData::roi_data = nullptr
```


ROI(Region of Interest) Data in a video frame

<span id="VideoFrameData-roi_data_size"></span>
### roi_data_size

```cpp
int bytertc::VideoFrameData::roi_data_size = 0
```


Data length of ROI (Region of Interest) data in a video frame

<span id="VideoFrameData-width"></span>
### width

```cpp
int bytertc::VideoFrameData::width = 0
```


Video frame width. Required.

<span id="VideoFrameData-height"></span>
### height

```cpp
int bytertc::VideoFrameData::height = 0
```


Video frame height. Required.

<span id="VideoFrameData-rotation"></span>
### rotation

```cpp
VideoRotation bytertc::VideoFrameData::rotation = kVideoRotation0
```


Video rotation angle, see [VideoRotation](https://docs.byteplus.com/en/docs/12/14187#VideoRotation).

<span id="VideoFrameData-timestamp_us"></span>
### timestamp_us

```cpp
int64_t bytertc::VideoFrameData::timestamp_us = 0
```


Video frame timestamp in ms. Required.

<span id="VideoFrameData-hw_buffer"></span>
### hw_buffer

```cpp
void* bytertc::VideoFrameData::hw_buffer = nullptr
```


Hardware acceleration buffer pointer

<span id="VideoFrameData-hw_context"></span>
### hw_context

```cpp
void* bytertc::VideoFrameData::hw_context = nullptr
```


Hardware acceleration context object handle

<span id="VideoFrameData-texture_matrix"></span>
### texture_matrix

```cpp
float bytertc::VideoFrameData::texture_matrix[16] = { 0 }
```


Texture matrix (only for texture type frame)

<span id="VideoFrameData-texture_id"></span>
### texture_id

```cpp
uint32_t bytertc::VideoFrameData::texture_id = 0
```


Texture ID (only for texture type frame). Required, when `buffer_type` is `kVideoBufferTypeRawMemory` or `kVideoFrameTypeGLTexture`.

<span id="VideoBufferType"></span>
# VideoBufferType

```cpp
enum bytertc::VideoBufferType
```


Video buffer type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoBufferTypeRawMemory |0 |raw memory |
|kVideoBufferTypeGLTexture |2 |OpenGL texture |
|kVideoBufferTypeCuda |3 |Cuda data format |
|kVideoBufferTypeD3D11 |4 |Direct3D11 texture |
|kVideoBufferTypeVAAPI |5 |Vaapi data format |


<span id="AudioFrameCallbackMethod"></span>
# AudioFrameCallbackMethod

```cpp
enum class bytertc::AudioFrameCallbackMethod
```


Audio data callback method

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRecord |0 |The callback of the audio data recorded by local microphone. |
|kPlayback |1 |The callback of the mixed audio data of all remote users subscribed to by the local user. |
|kMixed |2 |The callback of the mixed audio data including the data recorded by local microphone and that of all remote users subscribed to by the local user. |
|kRemoteUser |3 |The callback of the audio data before mixing of each remote user subscribed to by the local user. |
|kRecordScreen |4 |The callback of screen audio data captured locally. |
|kCaptureMixed |5 |The callback of the mixed audio data including the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`. |


<span id="MixedStreamPushTargetConfig"></span>
# MixedStreamPushTargetConfig

```cpp
struct bytertc::MixedStreamPushTargetConfig
```


Configurations for the mixing streams.

If not specified, the parameter can be used for both WTN stream and mixing\-stream tasks.

If not specified, the parameter can be passed when starting a task or during a task.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[push_wtn_stream_id](https://docs.byteplus.com/en/docs/12/14187#MixedStreamPushTargetConfig-push_wtn_stream_id) |
|const char\* |[push_cdn_url](https://docs.byteplus.com/en/docs/12/14187#MixedStreamPushTargetConfig-push_cdn_url) |
|MixedStreamPushTargetType |[push_target_type](https://docs.byteplus.com/en/docs/12/14187#MixedStreamPushTargetConfig-push_target_type) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamPushTargetConfig-push_wtn_stream_id"></span>
### push_wtn_stream_id

```cpp
const char* bytertc::MixedStreamPushTargetConfig::push_wtn_stream_id = nullptr
```


The WTN stream ID. This parameter is not supported for mixing\-stream stream tasks.

<span id="MixedStreamPushTargetConfig-push_cdn_url"></span>
### push_cdn_url

```cpp
const char* bytertc::MixedStreamPushTargetConfig::push_cdn_url = nullptr
```


The URL for the mixed stream to be pushed to. Only supports live transcoding via RTMP. The URL should match the regular expression `/^rtmps?:\\/\\//`. It's recommended to be set.

This parameter cannot be updated while pushing stream to the CDN.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamPushTargetConfig-push_target_type"></span>
### push_target_type

```cpp
MixedStreamPushTargetType bytertc::MixedStreamPushTargetConfig::push_target_type = kMixedStreamPushTargetTypeToCDN
```


The task type.

<span id="SnapshotErrorCode"></span>
# SnapshotErrorCode

```cpp
enum bytertc::SnapshotErrorCode
```


Snapshot error codes

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSnapshotErrorCodeOk |0 |Success. |
|kSnapshotErrorCodeCreateFail |\-1 |Failure. Fails to generate the image data or encode RGBA. |
|kSnapshotErrorCodeStreamInvalid |\-2 |Failure. The stream is invalid. |
|kSnapshotErrorCodeTimeout |\-3 |Failure. Snapshot timeout, with a default timeout of 1 second. |
|kSnapshotErrorCodeFileSaveError |\-4 |Failure. Failed to save the image. |


<span id="VideoContentType"></span>
# VideoContentType

```cpp
enum bytertc::VideoContentType
```


Video frame content type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoContentTypeNormalFrame |0 |Normal video |
|kVideoContentTypeBlackFrame |1 |Black frame |


<span id="ReceiveRange"></span>
# ReceiveRange

```cpp
struct bytertc::ReceiveRange
```


The range where local user can hear audio with attenuation effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[min](https://docs.byteplus.com/en/docs/12/14187#ReceiveRange-min) |
|int |[max](https://docs.byteplus.com/en/docs/12/14187#ReceiveRange-max) |


<span id="instructions"></span>
## Instructions

<span id="ReceiveRange-min"></span>
### min

```cpp
int bytertc::ReceiveRange::min
```


The minimum distance at which the local user can hear the attenuated audio from remote users.

The value must be ≥ 0, but ≤ max.

No attenuation effect for audio from distances less than this value you set.

<span id="ReceiveRange-max"></span>
### max

```cpp
int bytertc::ReceiveRange::max
```


The maximum distance at which the local user can hear audio from remote users.

The value must be ≥ min, and \> 0.

Audio from distances larger than the value you set cannot be heard.

<span id="AudioReportMode"></span>
# AudioReportMode

```cpp
enum bytertc::AudioReportMode
```


The volume callback modes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioReportModeNormal |0 |Always\-on(Default). |
|kAudioReportModeDisconnect |1 |After visibly joining a room and unpublishing your streams, disable the volume callback. |
|kAudioReportModeReset |2 |After visibly joining a room and unpublishing your streams, enable the volume callback. The volume is reset to 0. |


<span id="SyncInfoStreamType"></span>
# SyncInfoStreamType

```cpp
enum bytertc::SyncInfoStreamType
```


Stream type for media stream information synchronization

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSyncInfoStreamTypeAudio |0 |Audio stream |


<span id="LocalVideoStats"></span>
# LocalVideoStats

```cpp
struct bytertc::LocalVideoStats
```


Local video stream statistics, reference period 2s.

After a local user publishes a video stream successfully, the SDK will periodically notify the user through `onLocalStreamStats`

The delivery status of the published video stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[sent_kbitrate](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-sent_kbitrate) |
|int |[input_frame_rate](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-input_frame_rate) |
|int |[sent_frame_rate](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-sent_frame_rate) |
|int |[encoder_output_frame_rate](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-encoder_output_frame_rate) |
|int |[renderer_output_frame_rate](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-renderer_output_frame_rate) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-stats_interval) |
|float |[video_loss_rate](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-video_loss_rate) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-rtt) |
|int |[encoded_bitrate](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-encoded_bitrate) |
|int |[encoded_frame_width](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-encoded_frame_width) |
|int |[encoded_frame_height](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-encoded_frame_height) |
|int |[encoded_frame_count](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-encoded_frame_count) |
|VideoCodecType |[codec_type](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-codec_type) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-is_screen) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-jitter) |
|int |[codec_elapse_per_frame](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats-codec_elapse_per_frame) |


<span id="instructions"></span>
## Instructions

<span id="LocalVideoStats-sent_kbitrate"></span>
### sent_kbitrate

```cpp
int bytertc::LocalVideoStats::sent_kbitrate
```


TX bitrate in Kbps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-input_frame_rate"></span>
### input_frame_rate

```cpp
int bytertc::LocalVideoStats::input_frame_rate
```


Sampling frame rate in fps of video capture during this reference period

<span id="LocalVideoStats-sent_frame_rate"></span>
### sent_frame_rate

```cpp
int bytertc::LocalVideoStats::sent_frame_rate
```


TX frame rate in fps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encoder_output_frame_rate"></span>
### encoder_output_frame_rate

```cpp
int bytertc::LocalVideoStats::encoder_output_frame_rate
```


Encoder\-output frame rate in fps of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-renderer_output_frame_rate"></span>
### renderer_output_frame_rate

```cpp
int bytertc::LocalVideoStats::renderer_output_frame_rate
```


Local\-rendering frame rate in fps during this reference period

<span id="LocalVideoStats-stats_interval"></span>
### stats_interval

```cpp
int bytertc::LocalVideoStats::stats_interval
```


Reference period in ms.

This field is used to set the reference period for the callback, which is 2 s by default.

<span id="LocalVideoStats-video_loss_rate"></span>
### video_loss_rate

```cpp
float bytertc::LocalVideoStats::video_loss_rate
```


Video packet loss rate. The video uplink packet loss rate in this reference period ranges from [0,1].

<span id="LocalVideoStats-rtt"></span>
### rtt

```cpp
int bytertc::LocalVideoStats::rtt
```


Round\-trip time in ms.

<span id="LocalVideoStats-encoded_bitrate"></span>
### encoded_bitrate

```cpp
int bytertc::LocalVideoStats::encoded_bitrate
```


Video encoding bitrate in Kbps of the video stream with the highest resolution within the reference period.

<span id="LocalVideoStats-encoded_frame_width"></span>
### encoded_frame_width

```cpp
int bytertc::LocalVideoStats::encoded_frame_width
```


Video encoding width in px of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encoded_frame_height"></span>
### encoded_frame_height

```cpp
int bytertc::LocalVideoStats::encoded_frame_height
```


Video encoding height in px of the video stream with the highest resolution within the reference period

<span id="LocalVideoStats-encoded_frame_count"></span>
### encoded_frame_count

```cpp
int bytertc::LocalVideoStats::encoded_frame_count
```


The total number of the video stream with the highest resolution within the reference period sent in the reference period.

<span id="LocalVideoStats-codec_type"></span>
### codec_type

```cpp
VideoCodecType bytertc::LocalVideoStats::codec_type
```


For the encoding type of the video, please refer to [VideoCodecType](https://docs.byteplus.com/en/docs/12/14187#VideoCodecType).

<span id="LocalVideoStats-is_screen"></span>
### is_screen

```cpp
bool bytertc::LocalVideoStats::is_screen
```


Reserved field. Ignore the value returned in this field.

<span id="LocalVideoStats-jitter"></span>
### jitter

```cpp
int bytertc::LocalVideoStats::jitter
```


Video uplink network jitter in ms.

<span id="LocalVideoStats-codec_elapse_per_frame"></span>
### codec_elapse_per_frame

```cpp
int bytertc::LocalVideoStats::codec_elapse_per_frame
```


Average time spent on video encoding in ms.

<span id="Public-API"></span>
# Public API

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|struct bytertc::MixedStreamPushTargetConfig |[MixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/14187#mixedstreampushtargetconfig) |
|const unsigned int |[MAX_DEVICE_ID_LENGTH](https://docs.byteplus.com/en/docs/12/14187#max_device_id_length) |
|RtcRoomStats |[ConnectionStats](https://docs.byteplus.com/en/docs/12/14187#connectionstats) |
|VideoSolutionDescription |[deprecated] [VideoProfile](https://docs.byteplus.com/en/docs/12/14187#videoprofile) |


<span id="instructions"></span>
## Instructions

<span id="mixedstreampushtargetconfig"></span>
### MixedStreamPushTargetConfig

```cpp
typedef struct bytertc::MixedStreamPushTargetConfig bytertc::MixedStreamPushTargetConfig
```


The task type.

<span id="max_device_id_length"></span>
### MAX_DEVICE_ID_LENGTH

```cpp
const unsigned int bytertc::MAX_DEVICE_ID_LENGTH = 512
```


The maximum length of an ID.

<span id="connectionstats"></span>
### ConnectionStats

```cpp
typedef RtcRoomStats bytertc::streamingrtc::ConnectionStats
```


See [RtcRoomStats](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats).

<span id="videoprofile"></span>
### VideoProfile

```cpp
typedef VideoSolutionDescription bytertc::VideoProfile
```


> Deprecated since 3.45 and will be deleted in 3.51.


<span id="ReturnStatus"></span>
# ReturnStatus

```cpp
enum bytertc::ReturnStatus
```


API call result.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kReturnStatusSuccess |0 |Success. |
|kReturnStatusFailure |\-1 |Failure. |
|kReturnStatusParameterErr |\-2 |Invalid parameter. |
|kReturnStatusWrongState |\-3 |API status error. |
|kReturnStatusHasInRoom |\-4 |Failure. The user is already in the room. |
|kReturnStatusHasInLogin |\-5 |Failure. The user has already logged in. |
|kReturnStatusHasInEchoTest |\-6 |Failure. The user is already in a pre\-call test. |
|kReturnStatusNeitherVideoNorAudio |\-7 |Failure. Neither video nor audio is captured. |
|kReturnStatusRoomIdInUse |\-8 |Failure. The roomId is already in use. |
|kReturnStatusScreenNotSupport |\-9 |Failure. Screen stream is not supported. |
|kReturnStatusNotSupport |\-10 |Failure. Not supported. |
|kReturnStatusResourceOverflow |\-11 |Failure. Resource overflow. |
|kReturnStatusVideoNotSupport |\-12 |Failure. Not supported. |
|kReturnStatusAudioNoFrame |\-101 |Failure. No audio frame. |
|kReturnStatusAudioNotImplemented |\-102 |Failure. Not implemented. |
|kReturnStatusAudioNoPermission |\-103 |Failure. The audio capture device does not have microphone use permission, and the initialization of the device failed. |
|kReturnStatusAudioDeviceNotExists |\-104 |Failure. The device does not exist. This value is returned if there is currently no device or if the device has been removed. |
|kReturnStatusAudioDeviceFormatNotSupport |\-105 |Failure. The device audio format is not supported. |
|kReturnStatusAudioDeviceNoDevice |\-106 |Failure. No device in system. |
|kReturnStatusAudioDeviceCannotUse |\-107 |Failure. The current device is not available and needs to be replaced. |
|kReturnStatusAudioDeviceInitFailed |\-108 |Device initialization failed due to a system error. |
|kReturnStatusAudioDeviceStartFailed |\-109 |Device start\-up failed due to a system error. |
|kReturnStatusAudioDeviceProcessNotExist |\-110 |Sharing process audio failed because the process does not exist. |
|kReturnStatusAudioDeviceSpecifyingProcessUnsupport |\-111 |Unsupported for capturing audio from a specified process. |
|kReturnStatusNativeInvalid |\-201 |Failure. invalid object. |
|kReturnStatusVideoTimeStampWarning |\-202 |Warning. When pushing a video frame to the RTC SDK, the timing difference of subsequent video frames should be the same as the interval of the frame push operation. If not, you will receive this warning. |
|kReturnStatusAecSceneWarning |\-302 |Warning. The configuration delivers an invalid aec scene. |
|kReturnStatusAecTypeWarning |\-303 |Warning. The configuration delivers an invalid aec type. |


<span id="EchoTestResult"></span>
# EchoTestResult

```cpp
enum class bytertc::EchoTestResult
```


Call test result

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kTestSuccess |0 |The playback of captured audio/video is received, test succeeds. |
|kTestTimeout |1 |Test is not completed after 60 seconds and has been stopped automatically. |
|kTestIntervalShort |2 |Less than 5s between the end of the last test and the start of the next test. |
|kAudioDeviceError |3 |Audio capture error |
|kVideoDeviceError |4 |Video capture error |
|kAudioReceiveError |5 |Audio reception error |
|kVideoReceiveError |6 |Video reception error |
|kInternalError |7 |Unrecoverable internal error |


<span id="MixedStreamVideoCodecType"></span>
# MixedStreamVideoCodecType

```cpp
enum bytertc::MixedStreamVideoCodecType
```


The video codec.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamVideoCodecTypeH264 |0 |(Default) H.264 format. |
|kMixedStreamVideoCodecTypeByteVC1 |1 |ByteVC1 format. |


<span id="ByteWatermark"></span>
# ByteWatermark

```cpp
struct bytertc::ByteWatermark
```


Watermark's scaled coordinates and size, relative to the video stream.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/14187#ByteWatermark-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/14187#ByteWatermark-y) |
|float |[width](https://docs.byteplus.com/en/docs/12/14187#ByteWatermark-width) |
|float |[height](https://docs.byteplus.com/en/docs/12/14187#ByteWatermark-height) |


<span id="instructions"></span>
## Instructions

<span id="ByteWatermark-x"></span>
### x

```cpp
float bytertc::ByteWatermark::x
```


The watermark's horizontal offset from the upper left corner of the video stream to the video stream's width in the range of [0,1).

<span id="ByteWatermark-y"></span>
### y

```cpp
float bytertc::ByteWatermark::y
```


The watermark's vertical offset from the upper left corner of the video stream to the video stream's height in the range of [0,1).

<span id="ByteWatermark-width"></span>
### width

```cpp
float bytertc::ByteWatermark::width
```


The watermark's width to the video stream's width in the range of [0,1).

<span id="ByteWatermark-height"></span>
### height

```cpp
float bytertc::ByteWatermark::height
```


The watermark height to the video stream's height in the range of [0,1).

<span id="RoomMessageSendResult"></span>
# RoomMessageSendResult

```cpp
enum bytertc::RoomMessageSendResult
```


Result of broadcasting messages in the room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRoomMessageSendResultSuccess |200 |Message sent successfully. |
|kRoomMessageSendResultTimeout |1 |Failure. Sending timeout. |
|kRoomMessageSendResultNetworkDisconnected |2 |Failure. Channel disconnected. |
|kRoomMessageSendResultExceedQPS |5 |Failure. Exceeds QPS limit. |
|kRoomMessageSendResultNotJoin |100 |Failure. The sender has not joined a room. |
|kRoomMessageSendResultNoConnection |102 |Failure. No data transmission channel connection available |
|kRoomMessageSendResultExceedMaxLength |103 |Failure. The default maximum length of a message is 1 KB. If you [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode), the maximum length is 64 KB. |
|kRoomMessageSendResultUnknown |1000 |Failure. Unknown error |


<span id="MixedStreamPushTargetType"></span>
# MixedStreamPushTargetType

```cpp
enum bytertc::MixedStreamPushTargetType
```


Mixed stream push target type, specifying whether to push the mixed media stream to CDN or WTN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamPushTargetTypeToCDN |0 |Push to CDN |
|kMixedStreamPushTargetTypeToWTN |1 |Push to WTN |


<span id="SubscribeMediaType"></span>
# SubscribeMediaType

```cpp
enum bytertc::SubscribeMediaType
```


Type of the media stream subscribed to

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRTCSubscribeMediaTypeNone |0 |Neither audio nor video |
|kRTCSubscribeMediaTypeAudioOnly |1 |Audio only |
|kRTCSubscribeMediaTypeVideoOnly |2 |Video only |
|kRTCSubscribeMediaTypeVideoAndAudio |3 |Video only |


<span id="AudioPropertiesConfig"></span>
# AudioPropertiesConfig

```cpp
struct bytertc::AudioPropertiesConfig
```


Configuration for audio property prompt.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[interval](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesConfig-interval) |
|bool |[enable_spectrum](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesConfig-enable_spectrum) |
|bool |[enable_vad](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesConfig-enable_vad) |
|AudioReportMode |[local_main_report_mode](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesConfig-local_main_report_mode) |
|float |[smooth](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesConfig-smooth) |
|AudioPropertiesMode |[audio_report_mode](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesConfig-audio_report_mode) |
|bool |[enable_voice_pitch](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesConfig-enable_voice_pitch) |


<span id="instructions"></span>
## Instructions

<span id="AudioPropertiesConfig-interval"></span>
### interval

```cpp
int bytertc::AudioPropertiesConfig::interval = 0
```


Prompt interval in ms


* `<= 0`: Turn off prompt

* `(0,100]`: Invalid interval value, and will be automatically reset to 100ms.

* `> 100`: the actual value of interval

    &nbsp;


<span id="enable-spectrum"></span>
### enable_spectrum

```cpp
bool bytertc::AudioPropertiesConfig::enable_spectrum = false
```


Whether to enable audio spectrum detection.

<span id="AudioPropertiesConfig-enable_vad"></span>
### enable_vad

```cpp
bool bytertc::AudioPropertiesConfig::enable_vad = false
```


Whether to enable Voice Activity Detection.

<span id="AudioPropertiesConfig-local_main_report_mode"></span>
### local_main_report_mode

```cpp
AudioReportMode bytertc::AudioPropertiesConfig::local_main_report_mode = kAudioReportModeNormal
```


The volume callback modes. See [AudioReportMode](https://docs.byteplus.com/en/docs/12/14187#AudioReportMode).

<span id="AudioPropertiesConfig-smooth"></span>
### smooth

```cpp
float bytertc::AudioPropertiesConfig::smooth = 1.0f
```


The smoothing coefficient for audio attribute information prompt. The range is `(0.0, 1.0]`.

The default value is `1.0`, which means the smoothing effect is off by default. The smaller the value, the smoother the audio volume prompt. If you want to enable the smooth effect, the recommended value is `0.3`.

<span id="AudioPropertiesConfig-audio_report_mode"></span>
### audio_report_mode

```cpp
AudioPropertiesMode bytertc::AudioPropertiesConfig::audio_report_mode = kAudioPropertiesModeMicrophone
```


The audio info included in [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalaudiopropertiesreport). See [AudioPropertiesMode](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesMode).

Locally captured microphone audio info and locally captured screen audio info are included by default.

<span id="AudioPropertiesConfig-enable_voice_pitch"></span>
### enable_voice_pitch

```cpp
bool bytertc::AudioPropertiesConfig::enable_voice_pitch = false
```


Sets whether to return the vocal pitch of the local user.

<span id="AudioRoute"></span>
# AudioRoute

```cpp
enum bytertc::AudioRoute
```


Audio playback device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioRouteDefault |\-1 |Default devices |
|kAudioRouteHeadset |1 |Wired earphones |
|kAudioRouteEarpiece |2 |Earpiece |
|kAudioRouteSpeakerphone |3 |Speaker |
|kAudioRouteHeadsetBluetooth |4 |Bluetooth earphones |
|kAudioRouteHeadsetUSB |5 |USB Device |


<span id="VideoMetadataBuffer"></span>
# VideoMetadataBuffer

```cpp
struct bytertc::VideoMetadataBuffer
```


The metadata information contained in the video frame

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|char\* |[data](https://docs.byteplus.com/en/docs/12/14187#VideoMetadataBuffer-data) |
|int |[size](https://docs.byteplus.com/en/docs/12/14187#VideoMetadataBuffer-size) |
|int64_t |[timestamp_us](https://docs.byteplus.com/en/docs/12/14187#VideoMetadataBuffer-timestamp_us) |


<span id="instructions"></span>
## Instructions

<span id="VideoMetadataBuffer-data"></span>
### data

```cpp
char* bytertc::VideoMetadataBuffer::data
```


Received or sent metadata

<span id="VideoMetadataBuffer-size"></span>
### size

```cpp
int bytertc::VideoMetadataBuffer::size
```


The size of metadata data received or sent cannot exceed 1024

<span id="VideoMetadataBuffer-timestamp_us"></span>
### timestamp_us

```cpp
int64_t bytertc::VideoMetadataBuffer::timestamp_us
```


A timestamp containing metadata video frames in microseconds

<span id="MediaDeviceState"></span>
# MediaDeviceState

```cpp
enum bytertc::MediaDeviceState
```


Media device state.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaDeviceStateStarted |1 |On |
|kMediaDeviceStateStopped |2 |Off |
|kMediaDeviceStateRuntimeError |3 |Runtime error<br><br>For example, when the media device is expected to be working but no data is received. |
|kMediaDeviceStatePaused |4 |Device paused. Including:<br><br><br>&nbsp;<br><br>* During screen capturing, the target application window is minimized in the taskbar.<br><br>* Before or during screen capturing, the target application window is hidden.<br><br>* During screen capturing, the target application window is being stretched.<br><br>* During screen capturing, the target application window is being dragged. |
|kMediaDeviceStateResumed |5 |Device resumed |
|kMediaDeviceStateAdded |10 |Added<br><br>Call enumerate\-device api to update the device list when you get this notification. |
|kMediaDeviceStateRemoved |11 |Removed<br><br>Call enumerate\-device api to update the device list when you get this notification. |
|kMediaDeviceStateInterruptionBegan |12 |Closing the laptop interrupted the RTC call. RTC call will resume once the laptop is opened. |
|kMediaDeviceStateInterruptionEnded |13 |RTC call resumed from the interruption caused by closing the laptop. |
|kMediaDeviceStateBecomeSystemDefault |14 |The device just became the default device. |
|kMediaDeviceStateResignSystemDefault |15 |The device is no longer the default device. |
|kMediaDeviceStateListUpdated |16 |Notification of receiving the device list after time\-out.<br><br>Call enumerate\-device api to update the device list when you get this notification. |


<span id="RemoteVideoState"></span>
# RemoteVideoState

```cpp
enum bytertc::RemoteVideoState
```


Remote video stream status. You will receive `onRemoteVideoStateChanged` callback when the state changes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteVideoStateStopped |0 |The remote video stream defaults to the initial state, and the video has not yet started playing. |
|kRemoteVideoStateStarting |1 |Local user has received remote video stream header packet. |
|kRemoteVideoStateDecoding |2 |The remote video stream is decoding and playing normally. |
|kRemoteVideoStateFrozen |3 |The remote video stream is freezing due to network or other reasons. |
|kRemoteVideoStateFailed |4 |The remote video stream failed to play. |


<span id="Rectangle"></span>
# Rectangle

```cpp
struct bytertc::Rectangle
```


A rectangle that you can move around and re\-size to share just the portion of the screen defined by that rectangle.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[x](https://docs.byteplus.com/en/docs/12/14187#Rectangle-x) |
|int |[y](https://docs.byteplus.com/en/docs/12/14187#Rectangle-y) |
|int |[width](https://docs.byteplus.com/en/docs/12/14187#Rectangle-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#Rectangle-height) |


<span id="instructions"></span>
## Instructions

<span id="Rectangle-x"></span>
### x

```cpp
int bytertc::Rectangle::x = 0
```


The upper\-left X coordinate of the rectangle.

<span id="Rectangle-y"></span>
### y

```cpp
int bytertc::Rectangle::y = 0
```


The upper\-left Y coordinates of the rectangular.

<span id="Rectangle-width"></span>
### width

```cpp
int bytertc::Rectangle::width = 0
```


Width.

<span id="Rectangle-height"></span>
### height

```cpp
int bytertc::Rectangle::height = 0
```


Height.

<span id="VoiceChangerType"></span>
# VoiceChangerType

```cpp
enum bytertc::VoiceChangerType
```


Change sound effect type. For more types, contact the technical support.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVoiceChangerTypeOriginal |0 |Acoustic, no special effects |
|kVoiceChangerTypeGiant |1 |Giant |
|kVoiceChangerTypeChipmunk |2 |Chipmunk |
|kVoiceChangerTypeMinionst |3 |Minion |
|kVoiceChangerTypeVibrato |4 |Vibrato |
|kVoiceChangerTypeRobot |5 |Robot |


<span id="LocalProxyState"></span>
# LocalProxyState

```cpp
enum bytertc::LocalProxyState
```


The states of local proxy connection.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalProxyStateInited |0 |TCP proxy server is connected. |
|kLocalProxyStateConnected |1 |The local proxy is connected. |
|kLocalProxyStateError |2 |Errors occurred when connecting to the local proxy. |


<span id="MediaDeviceError"></span>
# MediaDeviceError

```cpp
enum bytertc::MediaDeviceError
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
|kMediaDeviceErrorDeviceNotFound |4 |The specified media device was not found. |
|kMediaDeviceErrorDeviceDisconnected |5 |Media device, window or monitor removed. |
|kMediaDeviceErrorDeviceNoCallback |6 |Device has no data callback. |
|kMediaDeviceErrorDeviceUNSupportFormat |7 |Device sample rate not supported. |
|kMediaDeviceErrorAudioServerNeedRestart |13 |System service error or long response time. We suggest restarting the audio service process or restarting the device. |


<span id="RTCAudioDeviceType"></span>
# RTCAudioDeviceType

```cpp
enum bytertc::RTCAudioDeviceType
```


Type of audio device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRTCAudioDeviceTypeUnknown |\-1 |Unknown device |
|kRTCAudioDeviceTypeRenderDevice |0 |Speaker or headphone |
|kRTCAudioDeviceTypeCaptureDevice |1 |Microphone |
|kRTCAudioDeviceTypeScreenCaptureDevice |2 |Screen capturing audio device |


<span id="MixedStreamTaskEvent"></span>
# MixedStreamTaskEvent

```cpp
enum bytertc::MixedStreamTaskEvent
```


Events related to mixed stream task

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamTaskEventStartSuccess |1 |The task initiated successfully. |
|kMixedStreamTaskEventStartFailed |2 |Failed to initiate the task. |
|kMixedStreamTaskEventUpdateSuccess |3 |The task updated successfully. |
|kMixedStreamTaskEventUpdateFailed |4 |Failed to update the task. |
|kMixedStreamTaskEventStopSuccess |5 |The task stopped. |
|kMixedStreamTaskEventStopFailed |6 |Failed to stop the task. |
|kMixedStreamTaskEventWarning |7 |Warnings |


<span id="MixedStreamSEIContentMode"></span>
# MixedStreamSEIContentMode

```cpp
enum bytertc::MixedStreamSEIContentMode
```


Content of SEI sent while pushing mixed stream to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamSEIContentModeDefault |0 |The video stream contains all the SEI information. Default value. |
|kMixedStreamSEIContentModeEnableVolumeIndication |1 |The SEI data transmitted with non\-key frames contains volume information only.<br><br>This parameter only takes effect after you set `MixedStreamControlConfig.enable_volume_indication` to "True". |


<span id="MixedStreamAudioProfile"></span>
# MixedStreamAudioProfile

```cpp
enum bytertc::MixedStreamAudioProfile
```


Advanced Audio Coding (AAC) profile.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamAudioProfileLC |0 |(Default) AAC Low\-Complexity profile (AAC\-LC). |
|kMixedStreamAudioProfileHEv1 |1 |HE\-AAC v1 profile (AAC LC with SBR). |
|kMixedStreamAudioProfileHEv2 |2 |HE\-AAC v2 profile (AAC LC with SBR and Parametric Stereo). |


<span id="FaceDetectResult"></span>
# FaceDetectResult

```cpp
struct bytertc::FaceDetectResult
```


Face Detection Result

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const int |[max_face_num](https://docs.byteplus.com/en/docs/12/14187#FaceDetectResult-max_face_num) |
|int |[detect_result](https://docs.byteplus.com/en/docs/12/14187#FaceDetectResult-detect_result) |
|int |[face_count](https://docs.byteplus.com/en/docs/12/14187#FaceDetectResult-face_count) |
|Rectangle[max_face_num] |[rect](https://docs.byteplus.com/en/docs/12/14187#FaceDetectResult-rect) |
|int |[image_width](https://docs.byteplus.com/en/docs/12/14187#FaceDetectResult-image_width) |
|int |[image_height](https://docs.byteplus.com/en/docs/12/14187#FaceDetectResult-image_height) |
|int64_t |[frame_timestamp_us](https://docs.byteplus.com/en/docs/12/14187#FaceDetectResult-frame_timestamp_us) |


<span id="instructions"></span>
## Instructions

<span id="FaceDetectResult-max_face_num"></span>
### max_face_num

```cpp
const int bytertc::FaceDetectResult::max_face_num = 10
```


Face information storage limit, up to 10 faces can be stored.

<span id="FaceDetectResult-detect_result"></span>
### detect_result

```cpp
int bytertc::FaceDetectResult::detect_result = 0
```


Face Detection Result


* 0: Success

* !0: Failure. See [Error Code Table](https://docs.byteplus.com/en/effects/docs/error-code-table).

    &nbsp;


<span id="face-count"></span>
### face_count

```cpp
int bytertc::FaceDetectResult::face_count = 0
```


Number of the detected faces

<span id="FaceDetectResult-rect"></span>
### rect

```cpp
Rectangle bytertc::FaceDetectResult::rect[max_face_num]
```


The face recognition rectangles. The length of the array is the same as the number of detected faces. See [Rectangle](https://docs.byteplus.com/en/docs/12/14187#Rectangle).

<span id="FaceDetectResult-image_width"></span>
### image_width

```cpp
int bytertc::FaceDetectResult::image_width = 0
```


Width of the original image (px)

<span id="FaceDetectResult-image_height"></span>
### image_height

```cpp
int bytertc::FaceDetectResult::image_height = 0
```


Height of the original image (px)

<span id="FaceDetectResult-frame_timestamp_us"></span>
### frame_timestamp_us

```cpp
int64_t bytertc::FaceDetectResult::frame_timestamp_us = 0
```


The time stamp of the video frame using face detection.

<span id="WTNSubscribeState"></span>
# WTNSubscribeState

```cpp
enum bytertc::WTNSubscribeState
```


State for WTN streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kWTNSubscribeStateSubscribed |0 |Subscribe WTN media stream |
|kWTNSubscribeStateUnsubscribed |1 |Unsubscribe WTN media stream |


<span id="RecordingInfo"></span>
# RecordingInfo

```cpp
struct bytertc::RecordingInfo
```


Details of local recording

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[file_path](https://docs.byteplus.com/en/docs/12/14187#RecordingInfo-file_path) |
|VideoCodecType |[video_codec_type](https://docs.byteplus.com/en/docs/12/14187#RecordingInfo-video_codec_type) |
|int |[width](https://docs.byteplus.com/en/docs/12/14187#RecordingInfo-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#RecordingInfo-height) |


<span id="instructions"></span>
## Instructions

<span id="RecordingInfo-file_path"></span>
### file_path

```cpp
const char* bytertc::RecordingInfo::file_path
```


The absolute path of the recorded file, including the file name and file suffix

<span id="RecordingInfo-video_codec_type"></span>
### video_codec_type

```cpp
VideoCodecType bytertc::RecordingInfo::video_codec_type
```


For the video encoding type of the recorded file. See [VideoCodecType](https://docs.byteplus.com/en/docs/12/14187#VideoCodecType)

<span id="RecordingInfo-width"></span>
### width

```cpp
int bytertc::RecordingInfo::width
```


The width of the recorded video, in pixels. Please ignore this field for audio\-only recording

<span id="RecordingInfo-height"></span>
### height

```cpp
int bytertc::RecordingInfo::height
```


The height of the recorded video, the unit: pixels. Please ignore this field for audio\-only recording

<span id="P2PRole"></span>
# P2PRole

```cpp
enum bytertc::streamingrtc::P2PRole
```


Role of the streaming Engine

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kP2PRoleClient |0 |client |
|kP2PRoleServer |1 |Server |


<span id="HWDeviceType"></span>
# HWDeviceType

```cpp
enum bytertc::HWDeviceType
```


Hardware acceleration device type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kHWDeviceTypeNone |0 |Unknown device type |
|kHWDeviceTypeD3D11 |1 |Direct3d 11 Video acceleration device |
|kHWDeviceTypeCuda |2 |Cuda hardware acceleration device |
|kHWDeviceTypeQsv |3 |Qsv acceleration device under intel platform |
|kHWDeviceTypeDxva2 |4 |Windows platform dx hardware acceleration device |
|kHWDeviceTypeMediaCodec |5 |Hardware acceleration device mediacodec under Android platform |
|kHWDeviceTypeVideoToolbox |6 |IOS, MACOS platform hardware acceleration device VideoToolbox |
|kHWDeviceTypeEglContext |7 |Android, linux platform hardware acceleration device egl context |
|kHWDeviceTypeVaapi |8 |Linux, windows platform hardware acceleration device va context |


<span id="AudioSourceType"></span>
# AudioSourceType

```cpp
enum bytertc::AudioSourceType
```


Audio input source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioSourceTypeExternal |0 |Custom Capture Audio Source |
|kAudioSourceTypeInternal |1 |RTC SDK internal acquisition audio source |


<span id="VideoSinkMirrorType"></span>
# VideoSinkMirrorType

```cpp
enum bytertc::VideoSinkMirrorType
```


Whether the video frame needs to be mirrored.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoSinkMirrorTypeON |1 |Enable mirroring effect. |
|kVideoSinkMirrorTypeOFF |2 |(Default) Disable mirroring effect. |


<span id="RemoteStreamKey"></span>
# RemoteStreamKey

```cpp
struct bytertc::RemoteStreamKey
```


Information about the remote stream

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamKey-room_id) |
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamKey-user_id) |
|StreamIndex |[stream_index](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamKey-stream_index) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamKey-room_id"></span>
### room_id

```cpp
const char* bytertc::RemoteStreamKey::room_id
```


The room ID of the media stream.

If the media stream is the stream forwarded by `startForwardStreamToRooms`, you must set the roomID to the room ID of the target room.

<span id="RemoteStreamKey-user_id"></span>
### user_id

```cpp
const char* bytertc::RemoteStreamKey::user_id
```


The ID of the user who published the stream.

<span id="RemoteStreamKey-stream_index"></span>
### stream_index

```cpp
StreamIndex bytertc::RemoteStreamKey::stream_index
```


Reserved field.

<span id="PerformanceAlarmMode"></span>
# PerformanceAlarmMode

```cpp
enum bytertc::PerformanceAlarmMode
```


Whether to turn on release performance fallback

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPerformanceAlarmModeNormal |0 |Not enabled Publish performance fallback |
|kPerformanceAlarmModeSimulcast |1 |Enable publish performance fallback |


<span id="MuteState"></span>
# MuteState

```cpp
enum bytertc::MuteState
```


Transmission/Playback state of the media stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMuteStateOff |0 |Enable |
|kMuteStateOn |1 |Disable |


<span id="IVideoFrame"></span>
# IVideoFrame

```cpp
class bytertc::IVideoFrame
```


video frame interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual VideoBufferType |[bufferType](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-buffertype) |
|virtual VideoPixelFormat |[pixelFormat](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-pixelformat) |
|virtual VideoContentType |[contentType](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-contenttype) |
|virtual int64_t |[timestampUs](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-timestampus) |
|virtual int |[width](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-width) |
|virtual int |[height](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-height) |
|virtual VideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-rotation) |
|virtual int |[numberOfPlanes](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-numberofplanes) |
|virtual uint8_t\* |[planeData](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-planedata) |
|virtual int |[planeStride](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-planestride) |
|virtual uint8_t\* |[seiData](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-seidata) |
|virtual void\* |[hwBuffer](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-hwbuffer) |
|virtual void\* |[hwContext](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-hwcontext) |
|virtual void |[textureMatrix](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-texturematrix) |
|virtual uint32_t |[textureId](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-textureid) |
|virtual void |[addRef](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-addref) |
|virtual long |[releaseRef](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-releaseref) |
|virtual CameraID |[cameraId](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame-cameraid) |


<span id="instructions"></span>
## Instructions

<span id="IVideoFrame-buffertype"></span>
### bufferType

```cpp
virtual VideoBufferType bufferType() = 0;
```


Gets video frame buffer type, see [VideoBufferType](https://docs.byteplus.com/en/docs/12/14187#VideoBufferType).

<span id="IVideoFrame-pixelformat"></span>
### pixelFormat

```cpp
virtual VideoPixelFormat pixelFormat() = 0;
```


Gets video frame's pixel format, see [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14187#VideoPixelFormat).

<span id="IVideoFrame-contenttype"></span>
### contentType

```cpp
virtual VideoContentType contentType() = 0;
```


Gets video frame content type, see [VideoContentType](https://docs.byteplus.com/en/docs/12/14187#VideoContentType).

<span id="IVideoFrame-timestampus"></span>
### timestampUs

```cpp
virtual int64_t timestampUs() = 0;
```


Gets video frame timestamp in microseconds

<span id="IVideoFrame-width"></span>
### width

```cpp
virtual int width() = 0;
```


Gets video frame width

<span id="IVideoFrame-height"></span>
### height

```cpp
virtual int height() = 0;
```


Gets video frame height

<span id="IVideoFrame-rotation"></span>
### rotation

```cpp
virtual VideoRotation rotation() = 0;
```


Gets the video frame rotation angle, see [VideoRotation](https://docs.byteplus.com/en/docs/12/14187#VideoRotation)

<span id="IVideoFrame-numberofplanes"></span>
### numberOfPlanes

```cpp
virtual int numberOfPlanes() = 0;
```


Gets the number of video frame plane

<span id="IVideoFrame-planedata"></span>
### planeData

```cpp
virtual uint8_t* planeData(int plane_index) = 0;
```


Gets video frame plane

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|plane_index |int |plane index |


<span id="IVideoFrame-planestride"></span>
### planeStride

```cpp
virtual int planeStride(int plane_index) = 0;
```


Get the length of memory between two lines of image data in video frame plane in bytes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|plane_index |int |Plane index |


<span id="IVideoFrame-seidata"></span>
### seiData

```cpp
virtual uint8_t* seiData(int& size)  = 0;
```


Gets SEI data pointer

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|size |int& |Byte count of SEI data |


<span id="IVideoFrame-hwbuffer"></span>
### hwBuffer

```cpp
virtual void* hwBuffer() = 0;
```


Gets hardware buffer pointer

<span id="IVideoFrame-hwcontext"></span>
### hwContext

```cpp
virtual void* hwContext() = 0;
```


Gets hardware acceleration context object handle

<span id="IVideoFrame-texturematrix"></span>
### textureMatrix

```cpp
virtual void textureMatrix(float matrix[16]) = 0;
```


Get Texture matrix (only for texture type frame)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|matrix |float[16] |Texture matrix |


<span id="IVideoFrame-textureid"></span>
### textureId

```cpp
virtual uint32_t textureId() = 0;
```


Get Texture ID (only for texture type frame)

<span id="IVideoFrame-addref"></span>
### addRef

```cpp
virtual void addRef() = 0;
```


Increase the reference count of the video frame by 1.

**Notes**

If you want to asynchronously process the video frame (for example, switch the thread for rendering), you need to call this interface to increase the reference count. After the asynchronous processing is completed, you need to call `releaseRef` to reduce the reference count by 1.

<span id="IVideoFrame-releaseref"></span>
### releaseRef

```cpp
virtual long releaseRef() = 0;
```


Decrease the reference count of the video frame by 1.

**Notes**

When the reference count of a video frame is decreased to 0, the video frame object is released. After the video frame is released, it should not be used anymore.

<span id="IVideoFrame-cameraid"></span>
### cameraId

```cpp
virtual CameraID cameraId()  = 0;
```


Gets camera position info of the video frame, see [CameraID](https://docs.byteplus.com/en/docs/12/14187#CameraID)

<span id="VideoEncoderConfig"></span>
# VideoEncoderConfig

```cpp
struct bytertc::VideoEncoderConfig
```


Video encoding configuration. Refer to [Setting Video Encoder Configuration](https://docs.byteplus.com/byteplus-rtc/docs/70122) to learn more.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/en/docs/12/14187#VideoEncoderConfig-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#VideoEncoderConfig-height) |
|int |[frame_rate](https://docs.byteplus.com/en/docs/12/14187#VideoEncoderConfig-frame_rate) |
|int |[max_bitrate](https://docs.byteplus.com/en/docs/12/14187#VideoEncoderConfig-max_bitrate) |
|int |[min_bitrate](https://docs.byteplus.com/en/docs/12/14187#VideoEncoderConfig-min_bitrate) |
|int32_t |[key_frame_interval_ms](https://docs.byteplus.com/en/docs/12/14187#VideoEncoderConfig-key_frame_interval_ms) |
|VideoEncodePreference |[encoder_preference](https://docs.byteplus.com/en/docs/12/14187#VideoEncoderConfig-encoder_preference) |


<span id="instructions"></span>
## Instructions

<span id="VideoEncoderConfig-width"></span>
### width

```cpp
int bytertc::VideoEncoderConfig::width
```


Width of the video frame in px

<span id="VideoEncoderConfig-height"></span>
### height

```cpp
int bytertc::VideoEncoderConfig::height
```


Height of the video frame in px

<span id="VideoEncoderConfig-frame_rate"></span>
### frame_rate

```cpp
int bytertc::VideoEncoderConfig::frame_rate
```


Video frame rate in fps

<span id="VideoEncoderConfig-max_bitrate"></span>
### max_bitrate

```cpp
int bytertc::VideoEncoderConfig::max_bitrate = SEND_KBPS_AUTO_CALCULATE
```


Maximum bit rate in kbps. Optional for internal capturing while mandatory for custom capturing.

The default value is \-1 in internal capturing mode; the SDK will automatically calculate the applicable bit rate based on the input resolution and frame rate.

No stream will be encoded and published if you set this parameter to 0.

<span id="VideoEncoderConfig-min_bitrate"></span>
### min_bitrate

```cpp
int bytertc::VideoEncoderConfig::min_bitrate = 0
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `minBitrate`.

It defaults to `0`.

It ranges within [0, maxBitrate). When `maxBitrate` < `minBitrate`, the bitrate is self\-adapted.

In the following circumstances, the assignment to this variable has no effect:


* When `maxBitrate` = `0`, the video encoding is disabled.

* When `maxBitrate` < `0`, the bitrate is self\-adapted.

    &nbsp;


<span id="key-frame-interval-ms"></span>
### key_frame_interval_ms

```cpp
int32_t bytertc::VideoEncoderConfig::key_frame_interval_ms = 0
```


Key frame interval in milliseconds. The default value is `0`.

<span id="VideoEncoderConfig-encoder_preference"></span>
### encoder_preference

```cpp
VideoEncodePreference bytertc::VideoEncoderConfig::encoder_preference = VideoEncodePreference::kVideoEncodePreferenceFramerate
```


Encoding preference. The default value is kVideoEncodePreferenceFramerate. See [VideoEncodePreference](https://docs.byteplus.com/en/docs/12/14187#VideoEncodePreference).

<span id="AudioMixingState"></span>
# AudioMixingState

```cpp
enum bytertc::AudioMixingState
```


Audio mix file playback status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioMixingStatePreloaded |0 |Mix loaded |
|kAudioMixingStatePlaying |1 |Mix is playing |
|kAudioMixingStatePaused |2 |Mix paused |
|kAudioMixingStateStopped |3 |Mixing stopped |
|kAudioMixingStateFailed |4 |Mix playback failed |
|kAudioMixingStateFinished |5 |End of mixing |
|kAudioMixingStatePCMEnabled |6 |Prepare PCM Mix |
|kAudioMixingStatePCMDisabled |7 |End of PCM mix playback |


<span id="AudioSelectionPriority"></span>
# AudioSelectionPriority

```cpp
enum bytertc::AudioSelectionPriority
```


User priority in the audio selection

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioSelectionPriorityNormal |0 |Normally, whether the stream can be subscribed is determined by the result of audio selection. |
|kAudioSelectionPriorityHigh |1 |High priority with which the stream can skip audio selection and always be subscribable. |


<span id="MixedStreamAudioCodecType"></span>
# MixedStreamAudioCodecType

```cpp
enum bytertc::MixedStreamAudioCodecType
```


The audio codec.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamAudioCodecTypeAAC |0 |AAC format. |


<span id="ScreenParameters"></span>
# ScreenParameters

```cpp
struct bytertc::ScreenParameters
```


Screen sharing parameter

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[frame_rate](https://docs.byteplus.com/en/docs/12/14187#ScreenParameters-frame_rate) |
|int |[kbitrate](https://docs.byteplus.com/en/docs/12/14187#ScreenParameters-kbitrate) |
|int |[min_kbitrate](https://docs.byteplus.com/en/docs/12/14187#ScreenParameters-min_kbitrate) |


<span id="instructions"></span>
## Instructions

<span id="ScreenParameters-frame_rate"></span>
### frame_rate

```cpp
int bytertc::ScreenParameters::frame_rate = 15
```


Encoded frame rate in fps

<span id="ScreenParameters-kbitrate"></span>
### kbitrate

```cpp
int bytertc::ScreenParameters::kbitrate = -1
```


Encoding bitrate in kbps of the screen\-sharing stream. `-1` for self\-adapted, meaning the SDK will choose the appropriate encoding rate according to the width and height for the stream.

<span id="ScreenParameters-min_kbitrate"></span>
### min_kbitrate

```cpp
int bytertc::ScreenParameters::min_kbitrate = 0
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `min_kbitrate`.

It defaults to `0`.

It ranges within [0, kbitrate). When `bitrate` < `min_kbitrate`, the bitrate is self\-adapted.

In the following circumstances, the assignment to this variable has no effect:


* When `min_kbitrate` = `0`, the video encoding is disabled.

* When `min_kbitrate` < `0`, the bitrate is self\-adapted.

    &nbsp;


<span id="mixedstreamvideoconfig"></span>
# MixedStreamVideoConfig

```cpp
struct bytertc::MixedStreamVideoConfig
```


Video mix stream configurations.

With invalid or empty input, the configurations will be set as the default values.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int32_t |[width](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig-width) |
|int32_t |[height](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig-height) |
|int32_t |[fps](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig-fps) |
|int32_t |[gop](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig-gop) |
|int32_t |[bitrate](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig-bitrate) |
|MixedStreamVideoCodecType |[video_codec](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig-video_codec) |
|bool |[enable_bframe](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig-enable_bframe) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamVideoConfig-width"></span>
### width

```cpp
int32_t bytertc::MixedStreamVideoConfig::width = MIXED_STREAM_VIDEO_DEFAULT_WIDTH
```


The width (pixels) to be set. The range is [2, 1920], and must be an even number. The default value is 360 pixels. It's recommended to be set.

If an odd number is set, the width will be adjusted to the next larger even number.

<span id="MixedStreamVideoConfig-height"></span>
### height

```cpp
int32_t bytertc::MixedStreamVideoConfig::height = MIXED_STREAM_DEFAULT_VIDEO_HEIGHT
```


The height (pixels) to be set. The range is [2, 1920], and must be an even number. The default value is 640 pixels. It's recommended to be set.

If an odd number is set, the height will be adjusted to the next larger even number.

<span id="MixedStreamVideoConfig-fps"></span>
### fps

```cpp
int32_t bytertc::MixedStreamVideoConfig::fps = 15
```


The frame rate (FPS) in the range of [1, 60]. The default value is 15 FPS. It's recommended to be set.

<span id="MixedStreamVideoConfig-gop"></span>
### gop

```cpp
int32_t bytertc::MixedStreamVideoConfig::gop = 2
```


The time interval between I\-frames (second) in the range of [1, 5]. The default value is 2 seconds. It's recommended to be set.

This parameter is not supported for WTN stream tasks.

This parameter cannot be updated during the task.

<span id="MixedStreamVideoConfig-bitrate"></span>
### bitrate

```cpp
int32_t bytertc::MixedStreamVideoConfig::bitrate = 500
```


The bitrate (Kbps) in the range of [1, 10000]. The default value is `500`. It's recommended to be set.

<span id="MixedStreamVideoConfig-video_codec"></span>
### video_codec

```cpp
MixedStreamVideoCodecType bytertc::MixedStreamVideoConfig::video_codec = MixedStreamVideoCodecType::kMixedStreamVideoCodecTypeH264
```


The video codec. See [MixedStreamVideoCodecType](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoCodecType). The default value is `0`. It's recommended to be set.

The video codec of WTN stream can only be set as `0`, indicating H264.

This parameter cannot be updated during the task.

<span id="MixedStreamVideoConfig-enable_bframe"></span>
### enable_bframe

```cpp
bool bytertc::MixedStreamVideoConfig::enable_bframe = false
```


Whether to use B frames when pushing the mixing streams to CDN.


* True: Yes

* False: No

    &nbsp;


<span id="networkdetectionstopreason"></span>
# NetworkDetectionStopReason

```cpp
enum bytertc::NetworkDetectionStopReason
```


The reason why the probe stopped before the call

`onNetworkDetectionStopped` The parameter type of the callback

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kNetworkDetectionStopReasonUser |0 |User actively stops |
|kNetworkDetectionStopReasonTimeout |1 |Detection over three minutes |
|kNetworkDetectionStopReasonConnectionLost |2 |Probe network connection disconnected.<br><br>When no reply is received beyond 12s, the SDK will disconnect the network and will not try to reconnect. |
|kNetworkDetectionStopReasonStreaming |3 |Local user starts publishing and subscribing to streams; stop detection |
|kNetworkDetectionStopReasonInnerErr |4 |Network probe failure, internal anomaly |


<span id="MixedStreamControlConfig"></span>
# MixedStreamControlConfig

```cpp
struct bytertc::MixedStreamControlConfig
```


Configurations to be set while mixing streams on the server side.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[enable_volume_indication](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-enable_volume_indication) |
|float |[volume_indication_interval](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-volume_indication_interval) |
|int |[talk_volume](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-talk_volume) |
|bool |[is_add_volume_value](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-is_add_volume_value) |
|MixedStreamSEIContentMode |[sei_content_mode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-sei_content_mode) |
|int |[sei_payload_type](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-sei_payload_type) |
|const char\* |[sei_payload_uuid](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-sei_payload_uuid) |
|MixedStreamMediaType |[media_type](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-media_type) |
|MixedStreamPushMode |[push_stream_mode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig-push_stream_mode) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamControlConfig-enable_volume_indication"></span>
### enable_volume_indication

```cpp
bool bytertc::MixedStreamControlConfig::enable_volume_indication = false
```


> Available since 3.56


Sets whether to enable the function of separately sending sound indication SEI:


* true: Enable.

* false: (Default) Disable.

   After setting this parameter to "true", you can choose whether to send sound indication SEI only through `MixedStreamControlConfig.sei_content_mode`.

    &nbsp;


<span id="volume-indication-interval"></span>
### volume_indication_interval

```cpp
float bytertc::MixedStreamControlConfig::volume_indication_interval = 2.0f
```


> Available since 3.56


Sound indication interval in s. The range is [0.3,+∞). The default value is 2.

If a decimal with two or more decimal places is passed in, it will be rounded to the value of the first decimal place. For example, if you pass in 0.36, it will be automatically adjusted to 0.4.

<span id="MixedStreamControlConfig-talk_volume"></span>
### talk_volume

```cpp
int bytertc::MixedStreamControlConfig::talk_volume = 0
```


> Available since 3.56


Effective volume within the range of [0, 255]. The default value is 0.

If the value is set beyond the range, it will be automatically adjusted to the default value 0.

<span id="MixedStreamControlConfig-is_add_volume_value"></span>
### is_add_volume_value

```cpp
bool bytertc::MixedStreamControlConfig::is_add_volume_value = false
```


> Available since 3.56


Sets whether the volume value is contained in the sound indication SEI:


* true: Yes.

* false: (Default) No.

    &nbsp;


<span id="sei-content-mode"></span>
### sei_content_mode

```cpp
MixedStreamSEIContentMode bytertc::MixedStreamControlConfig::sei_content_mode = kMixedStreamSEIContentModeDefault
```


> Available since 3.56


Sets SEI content. See [MixedStreamSEIContentMode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamSEIContentMode).

The default value is `0`, indicating that the SEI in the video stream is included.

<span id="MixedStreamControlConfig-sei_payload_type"></span>
### sei_payload_type

```cpp
int bytertc::MixedStreamControlConfig::sei_payload_type = 100
```


> Available since 3.56


SEI payload type.

The default value is `100`, and the supported values are `5` and `100`.

During the process of pushing streams to CDN, you cannot change the parameter.

<span id="MixedStreamControlConfig-sei_payload_uuid"></span>
### sei_payload_uuid

```cpp
const char* bytertc::MixedStreamControlConfig::sei_payload_uuid = nullptr
```


> Available since 3.56


SEI payload UUID.

**Notes**

When PayloadType is `5`, you must set PayloadUUID, or you will receive a callback indicating parameter error. The error code is 1091.

When PayloadType is not `5`, it is not required to set PayloadUUID. If filled, it will be ignored by the backend.

The length of PayloadUUID should be 32 bits, or you will receive an error code of 1091.

Each character of the parameter should be within the range of [0, 9] [a, f] [A, F].

The PayloadUUID should not contain `-`. If the automatically generated UUID contains `-`, you should delete it.

During the process of pushing streams to CDN, you cannot change the parameter.

<span id="MixedStreamControlConfig-media_type"></span>
### media_type

```cpp
MixedStreamMediaType bytertc::MixedStreamControlConfig::media_type = MixedStreamMediaType::kMixedStreamMediaTypeAudioAndVideo
```


Sets the type of media stream pushed to CDN after being mixed. [MixedStreamMediaType](https://docs.byteplus.com/en/docs/12/14187#MixedStreamMediaType).

The default value is 0, which means pushing both audio and video.

<span id="MixedStreamControlConfig-push_stream_mode"></span>
### push_stream_mode

```cpp
MixedStreamPushMode bytertc::MixedStreamControlConfig::push_stream_mode = MixedStreamPushMode::kMixedStreamPushModeOnStream
```


Sets whether to initiate a stream mixing task in the absence of any users publishing streams. It defaults to be dependent on a user actively publishing media streams. See [MixedStreamPushMode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamPushMode).

Once the stream mixing task is initiated, this parameter can not be updated any more.

<span id="VirtualBackgroundSource"></span>
# VirtualBackgroundSource

```cpp
struct bytertc::VirtualBackgroundSource
```


Virtual background object.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VirtualBackgroundSourceType |[source_type](https://docs.byteplus.com/en/docs/12/14187#VirtualBackgroundSource-source_type) |
|uint32_t |[source_color](https://docs.byteplus.com/en/docs/12/14187#VirtualBackgroundSource-source_color) |
|const char\* |[source_path](https://docs.byteplus.com/en/docs/12/14187#VirtualBackgroundSource-source_path) |


<span id="instructions"></span>
## Instructions

<span id="VirtualBackgroundSource-source_type"></span>
### source_type

```cpp
VirtualBackgroundSourceType bytertc::VirtualBackgroundSource::source_type = kVirtualBackgroundSourceTypeColor
```


See [VirtualBackgroundSourceType](https://docs.byteplus.com/en/docs/12/14187#VirtualBackgroundSourceType).

<span id="VirtualBackgroundSource-source_color"></span>
### source_color

```cpp
uint32_t bytertc::VirtualBackgroundSource::source_color = 0xFFFFFFFF
```


The solid color of the background.

The format is 0xAARRGGBB.

<span id="VirtualBackgroundSource-source_path"></span>
### source_path

```cpp
const char* bytertc::VirtualBackgroundSource::source_path = nullptr
```


The absolute path of the specified image.


* You can upload a .JPG, .PNG, or .JPEG file.

* The image with a resolution higher than 1080p(Full HD) will be rescaled proportionally to fit in the video.

* If the image's aspect ratio matches the video's, the image will be rescaled proportionally to fit in the video.

* If the image’s aspect ratio does not match the video's, the shortest side (either height or width) of the image will be stretched proportionally to match the video. Then the image will be cropped to fill in the video.

* The transparent area in the image will be filled with black.

    &nbsp;


<span id="rendertargettype"></span>
# RenderTargetType

```cpp
enum bytertc::RenderTargetType
```


Render target type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRenderTargetTypeView |0 |Use this value when the target is in the range of SurfaceView/TextureView for Android, UIView for iOS, NSView for macOS, or HWND for Windows |
|kRenderTargetTypeSurface |1 |Use this value when the target is in the range of Surface for Android |


<span id="SVCLayer"></span>
# SVCLayer

```cpp
enum bytertc::SVCLayer
```


Time domain hierarchical definition

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSVCLayerDefault |0 |No hierarchy specified (default) |
|kSVCLayerBase |1 |T0 layer |
|kSVCLayerMain |2 |T0 + T1 layer |
|kSVCLayerHigh |3 |T0 + T1 + T2 layer |


<span id="HttpProxyState"></span>
# HttpProxyState

```cpp
enum bytertc::HttpProxyState
```


HTTP/HTTPS proxy status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kHttpProxyStateInit |0 |HTTP/HTTPS initialization state |
|kHttpProxyStateConnected |1 |HTTP/HTTPS Connection successful |
|kHttpProxyStateError |2 |HTTP/HTTPS connection failed |


<span id="RecordingConfig"></span>
# RecordingConfig

```cpp
struct bytertc::RecordingConfig
```


Local recording parameter configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[dir_path](https://docs.byteplus.com/en/docs/12/14187#RecordingConfig-dir_path) |
|RecordingFileType |[file_type](https://docs.byteplus.com/en/docs/12/14187#RecordingConfig-file_type) |


<span id="instructions"></span>
## Instructions

<span id="RecordingConfig-dir_path"></span>
### dir_path

```cpp
const char* bytertc::RecordingConfig::dir_path
```


The absolute folder path to save the recording file. The filename will be generated by RTC. You need to ensure that you have read and write permissions to this path.

<span id="RecordingConfig-file_type"></span>
### file_type

```cpp
RecordingFileType bytertc::RecordingConfig::file_type
```


Recording stored file format. See [RecordingFileType](https://docs.byteplus.com/en/docs/12/14187#RecordingFileType)

<span id="LoginType"></span>
# LoginType

```cpp
enum bytertc::LoginType
```


The type of user login

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLoginTypeFirst |0 |login for the first time. The user manually called `login` and received a successful login. |
|kLoginTypeReconnected |1 |Reconnect. The user network is poor and the connection with the server is lost, and the SDK automatically reconnects and logs in successfully. |


<span id="ScreenCaptureParameters"></span>
# ScreenCaptureParameters

```cpp
struct bytertc::ScreenCaptureParameters
```


Screen internal capture parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|Rectangle |[region_rect](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureParameters-region_rect) |
|MouseCursorCaptureState |[capture_mouse_cursor](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureParameters-capture_mouse_cursor) |
|ScreenFilterConfig |[filter_config](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureParameters-filter_config) |
|HighlightConfig |[highlight_config](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureParameters-highlight_config) |


<span id="instructions"></span>
## Instructions

<span id="ScreenCaptureParameters-region_rect"></span>
### region_rect

```cpp
Rectangle bytertc::ScreenCaptureParameters::region_rect
```


Collection area. See [Rectangle](https://docs.byteplus.com/en/docs/12/14187#Rectangle).

<span id="ScreenCaptureParameters-capture_mouse_cursor"></span>
### capture_mouse_cursor

```cpp
MouseCursorCaptureState bytertc::ScreenCaptureParameters::capture_mouse_cursor = MouseCursorCaptureState::kMouseCursorCaptureStateOn
```


To collect mouse status. See [MouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/14187#MouseCursorCaptureState).

<span id="ScreenCaptureParameters-filter_config"></span>
### filter_config

```cpp
ScreenFilterConfig bytertc::ScreenCaptureParameters::filter_config
```


Screen filtering settings. Provide ID of the windows to be excluded. See [ScreenFilterConfig](https://docs.byteplus.com/en/docs/12/14187#ScreenFilterConfig).

<span id="ScreenCaptureParameters-highlight_config"></span>
### highlight_config

```cpp
HighlightConfig bytertc::ScreenCaptureParameters::highlight_config
```


Settings for highlighting borders of the sharing region. See [HighlightConfig](https://docs.byteplus.com/en/docs/12/14187#HighlightConfig).

<span id="VideoRotationMode"></span>
# VideoRotationMode

```cpp
enum bytertc::VideoRotationMode
```


Video orientation

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoRotationModeFollowApp |0 |The orientation of the App |
|kVideoRotationModeFollowGSensor |1 |Gravity |


<span id="EarMonitorMode"></span>
# EarMonitorMode

```cpp
enum bytertc::EarMonitorMode
```


Whether to enable in\-ear monitoring.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kEarMonitorModeOff |0 |Off |
|kEarMonitorModeOn |1 |On |


<span id="ManagedMemory"></span>
# ManagedMemory

```cpp
struct bytertc::ManagedMemory
```


Custom Memory Release

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|uint8_t\* |[data](https://docs.byteplus.com/en/docs/12/14187#ManagedMemory-data) |
|int |[size](https://docs.byteplus.com/en/docs/12/14187#ManagedMemory-size) |
|void\* |[user_opaque](https://docs.byteplus.com/en/docs/12/14187#ManagedMemory-user_opaque) |
|int( *)(uint8_t*data, int size, void\*user_opaque) |[memory_deleter](https://docs.byteplus.com/en/docs/12/14187#ManagedMemory-memory_deleter) |


<span id="instructions"></span>
## Instructions

<span id="ManagedMemory-data"></span>
### data

```cpp
uint8_t* bytertc::ManagedMemory::data = nullptr
```


Memory data address

<span id="ManagedMemory-size"></span>
### size

```cpp
int bytertc::ManagedMemory::size = 0
```


Size of memory space

<span id="ManagedMemory-user_opaque"></span>
### user_opaque

```cpp
void* bytertc::ManagedMemory::user_opaque = nullptr
```


User\-defined data

<span id="ManagedMemory-memory_deleter"></span>
### memory_deleter

```cpp
int(* bytertc::ManagedMemory::memory_deleter) (uint8_t *data, int size, void *user_opaque) = nullptr
```


Custom memory free method pointer. If the pointer is not empty, the method will be called to free memory space. The parameters passed into the function are the data, size, and user_opaque fields in this structure.

<span id="NetworkQuality"></span>
# NetworkQuality

```cpp
enum bytertc::NetworkQuality
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
|kNetworkQualityDown |6 |The network is down. It may be down due to no answer within 12s, airplane mode on, disconnected cable, etc.<br><br>Refer to [Get connection state](https://docs.byteplus.com/byteplus-rtc/docs/95376) for more details about getting connection state. |


<span id="RemoteVideoStats"></span>
# RemoteVideoStats

```cpp
struct bytertc::RemoteVideoStats
```


Remote video stream statistics, reference period 2s.

After the local user subscribes to the remote video stream successfully, the SDK will periodically notify the local user of the reception status of the remote video stream subscribed to during this reference period through `onRemoteStreamStats`. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-height) |
|float |[video_loss_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-video_loss_rate) |
|int |[received_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-received_kbitrate) |
|int |[decoder_output_frame_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-decoder_output_frame_rate) |
|int |[renderer_output_frame_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-renderer_output_frame_rate) |
|int |[stall_count](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-stall_count) |
|int |[stall_duration](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-stall_duration) |
|long |[e2e_delay](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-e2e_delay) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-is_screen) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-stats_interval) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-rtt) |
|int |[frozen_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-frozen_rate) |
|VideoCodecType |[codec_type](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-codec_type) |
|int |[video_index](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-video_index) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-jitter) |
|int |[codec_elapse_per_frame](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-codec_elapse_per_frame) |
|int |[cap_to_render_delay](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-cap_to_render_delay) |
|int |[av_sync_diff_ms](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats-av_sync_diff_ms) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoStats-width"></span>
### width

```cpp
int bytertc::RemoteVideoStats::width
```


Video Width

<span id="RemoteVideoStats-height"></span>
### height

```cpp
int bytertc::RemoteVideoStats::height
```


Video height

<span id="RemoteVideoStats-video_loss_rate"></span>
### video_loss_rate

```cpp
float bytertc::RemoteVideoStats::video_loss_rate
```


Video packet loss rate, e.g., the video downlink packet loss rate in the reference period, which is in the range of [0,1].

<span id="RemoteVideoStats-received_kbitrate"></span>
### received_kbitrate

```cpp
int bytertc::RemoteVideoStats::received_kbitrate
```


Receiving bit rate. Video reception rate within the reference period, in kbps.

<span id="RemoteVideoStats-decoder_output_frame_rate"></span>
### decoder_output_frame_rate

```cpp
int bytertc::RemoteVideoStats::decoder_output_frame_rate
```


The decoder outputs the frame rate. Video decoder output frame rate within the reference period, in fps.

<span id="RemoteVideoStats-renderer_output_frame_rate"></span>
### renderer_output_frame_rate

```cpp
int bytertc::RemoteVideoStats::renderer_output_frame_rate
```


Render frame rate. The video rendering frame rate in the reference period, in fps.

<span id="RemoteVideoStats-stall_count"></span>
### stall_count

```cpp
int bytertc::RemoteVideoStats::stall_count
```


Number of stalls. Number of stalls in the reference period.

<span id="RemoteVideoStats-stall_duration"></span>
### stall_duration

```cpp
int bytertc::RemoteVideoStats::stall_duration
```


Stall duration. The total duration of the video stall in the reference period. Unit ms.

<span id="RemoteVideoStats-e2e_delay"></span>
### e2e_delay

```cpp
long bytertc::RemoteVideoStats::e2e_delay
```


End\-to\-end latency at the user experience level. The delay from the start of encoding at the sending end to the start of decoding at the receiving end, in units of ms.

<span id="RemoteVideoStats-is_screen"></span>
### is_screen

```cpp
bool bytertc::RemoteVideoStats::is_screen
```


Reserved field. Ignore the value returned in this field.

<span id="RemoteVideoStats-stats_interval"></span>
### stats_interval

```cpp
int bytertc::RemoteVideoStats::stats_interval
```


Statistical interval, the interval of this reference period, in ms.

This field is used to set the reference period for the callback, currently set to 2s.

<span id="RemoteVideoStats-rtt"></span>
### rtt

```cpp
int bytertc::RemoteVideoStats::rtt
```


Round\-trip time in ms.

<span id="RemoteVideoStats-frozen_rate"></span>
### frozen_rate

```cpp
int bytertc::RemoteVideoStats::frozen_rate
```


The cumulative duration of video freeze for the remote user as a percentage of the total effective duration of the video after entering the room. The effective duration of the video refers to the duration of the video other than stopping sending the video stream and disabling the video module after the remote user enters the room to publish the video stream.

<span id="RemoteVideoStats-codec_type"></span>
### codec_type

```cpp
VideoCodecType bytertc::RemoteVideoStats::codec_type
```


For the encoding type of the video, please refer to [VideoCodecType](https://docs.byteplus.com/en/docs/12/14187#VideoCodecType).

<span id="RemoteVideoStats-video_index"></span>
### video_index

```cpp
int bytertc::RemoteVideoStats::video_index
```


For subscripts of streams with multiple resolutions.

<span id="RemoteVideoStats-jitter"></span>
### jitter

```cpp
int bytertc::RemoteVideoStats::jitter
```


Video downlink network jitter in ms.

<span id="RemoteVideoStats-codec_elapse_per_frame"></span>
### codec_elapse_per_frame

```cpp
int bytertc::RemoteVideoStats::codec_elapse_per_frame
```


Average time spent on video decoding in ms.

<span id="RemoteVideoStats-cap_to_render_delay"></span>
### cap_to_render_delay

```cpp
int bytertc::RemoteVideoStats::cap_to_render_delay
```


End\-to\-end latency at the user experience level. The delay from the start of capturing at the sending end to the completion of rendering at the receiving end, in units of ms.

<span id="RemoteVideoStats-av_sync_diff_ms"></span>
### av_sync_diff_ms

```cpp
int bytertc::RemoteVideoStats::av_sync_diff_ms
```


Audio/video synchronization diff in ms.

<span id="RemoteAudioState"></span>
# RemoteAudioState

```cpp
enum bytertc::RemoteAudioState
```


Remote audio stream state.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteAudioStateStopped |0 |The remote audio stream is not received. |
|kRemoteAudioStateStarting |1 |Start receiving the remote audio stream header. |
|kRemoteAudioStateDecoding |2 |The remote audio stream is decoding and playing normally. |
|kRemoteAudioStateFrozen |3 |Remote audio stream stalls. |


<span id="AggregationOption"></span>
# AggregationOption

```cpp
enum bytertc::AggregationOption
```


> Available since 3.56


Stream aggregation strategy

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAggregationOptionMin |0 |Stream aggregation with the lowest resolution.(Default Strategy) |
|kAggregationOptionMax |1 |Stream aggregation with the highest resolution. |
|kAggregationOptionMajority |2 |Stream aggregation according to the proportions, and when the proportions are the same, it takes the lowest resolution. |


<span id="DestInfo"></span>
# DestInfo

```cpp
struct bytertc::DestInfo
```


Configurations for pushing a single media stream destination room info

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#DestInfo-room_id) |
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#DestInfo-user_id) |


<span id="instructions"></span>
## Instructions

<span id="DestInfo-room_id"></span>
### room_id

```cpp
const char* bytertc::DestInfo::room_id
```


ID of the room where the media stream aims to forward to.

<span id="DestInfo-user_id"></span>
### user_id

```cpp
const char* bytertc::DestInfo::user_id
```


ID of the user where the media stream aims to forward to in aim room.

<span id="UserWorkerType"></span>
# UserWorkerType

```cpp
enum bytertc::UserWorkerType
```


Define user functions for linux users

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kUserWorkerTypeNormal |0 |Normal user, no special attributes |
|kUserWorkerTypeSupportSip |1 << 0 |User supports SIP flow, signaling only sends SIP flow |
|kUserWorkerTypeByteVc1Transcoder |1 << 1 |User supports bytevc1 to H264 transcoding of screen streams |
|kUserWorkerTypeNeedUserListAndCb |1 << 2 |The user needs the signaling server to send a full number of user lists and callback functions |
|kUserWorkerTypeNeedStreamCallBack |1 << 3 |The user needs to get relevant callbacks for all streams in the room when the room enters multiplayer mode |
|kUserWorkerTypeAudioSelectionExemption |1 << 4 |User disables audio selection |


<span id="RemoteStreamSwitch"></span>
# RemoteStreamSwitch

```cpp
struct bytertc::RemoteStreamSwitch
```


Information of stream switching due to a Fallback

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[uid](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamSwitch-uid) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamSwitch-is_screen) |
|int |[before_video_index](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamSwitch-before_video_index) |
|int |[after_video_index](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamSwitch-after_video_index) |
|bool |[before_enable](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamSwitch-before_enable) |
|bool |[after_enable](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamSwitch-after_enable) |
|FallbackOrRecoverReason |[reason](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamSwitch-reason) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamSwitch-uid"></span>
### uid

```cpp
const char* bytertc::RemoteStreamSwitch::uid
```


User ID of the publisher of the subscribed media stream

<span id="RemoteStreamSwitch-is_screen"></span>
### is_screen

```cpp
bool bytertc::RemoteStreamSwitch::is_screen
```


Reserved field. Ignore the value returned in this field.

<span id="RemoteStreamSwitch-before_video_index"></span>
### before_video_index

```cpp
int bytertc::RemoteStreamSwitch::before_video_index
```


Index corresponding to the resolution of the subscribed video stream before the stream switch.

<span id="RemoteStreamSwitch-after_video_index"></span>
### after_video_index

```cpp
int bytertc::RemoteStreamSwitch::after_video_index
```


Index corresponding to the resolution of the subscribed video stream after the stream switch.

<span id="RemoteStreamSwitch-before_enable"></span>
### before_enable

```cpp
bool bytertc::RemoteStreamSwitch::before_enable
```


Is there a video stream before switching.

<span id="RemoteStreamSwitch-after_enable"></span>
### after_enable

```cpp
bool bytertc::RemoteStreamSwitch::after_enable
```


Is there a video stream after switching.

<span id="RemoteStreamSwitch-reason"></span>
#### reason

```cpp
FallbackOrRecoverReason bytertc::RemoteStreamSwitch::reason
```


Refer to [FallbackOrRecoverReason](https://docs.byteplus.com/en/docs/12/14187#FallbackOrRecoverReason) for the reason of the Fallback or reverting from the Fallback of the subscribed stream.

<span id="VideoDeviceFacing"></span>
# VideoDeviceFacing

```cpp
enum bytertc::VideoDeviceFacing
```


video device facing type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoDeviceFacingFront |0 |Front\-facing video camera |
|kVideoDeviceFacingBack |1 |Back\-facing video camera |
|kVideoDeviceFacingUnknown |2 |video camera facing unknown |


<span id="ForwardStreamState"></span>
# ForwardStreamState

```cpp
enum bytertc::ForwardStreamState
```


The state of the relaying for each room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kForwardStreamStateIdle |0 |Idle<br><br><br>&nbsp;<br><br>* States of all the rooms turn to idle after you call `stopForwardStreamToRooms`.<br><br>* States of the rooms turns to idle that you call `updateForwardStreamToRooms` to remove. |
|kForwardStreamStateSuccess |1 |Start relaying.<br><br><br>&nbsp;<br><br>* State of the rooms turn to this state after the relaying starts successfully by calling `startForwardStreamToRooms`.<br><br>* State of the rooms added by calling `updateForwardStreamToRooms` turn to this state after the relaying start successfully. |
|kForwardStreamStateFailure |2 |Relay fails. Refer to [ForwardStreamError](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamError) for more information.<br><br>Once the relaying fails, state of the room turns to this state after calling `startForwardStreamToRooms` or `updateForwardStreamToRooms`. |


<span id="SEICountPerFrame"></span>
# SEICountPerFrame

```cpp
enum bytertc::SEICountPerFrame
```


SEI sending mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSEICountPerFrameSingle |0 |Single\-SEI mode. A single video frame carries at most one SEI message.<br><br>When you send multiple SEI messages in 1 frame, they will be sent in sequence following consecutive video frames.<br><br>For example, if you need to send 3 SEI data within a certain frame, then the 1st SEI will be sent in the current frame, the 2nd SEI will be sent in the next frame, and the 3rd SEI will be sent in the frame after that. |
|kSEICountPerFrameMulti |1 |Multi\-SEI mode.<br><br>When you send multiple SEI messages in 1 frame, all these SEI data will be sent together in the next frame, which can reduce sending delay, but a frame will carry multiple SEI messages.<br><br>For example, if there are 3 SEI data to be sent within a 1\-frame interval, these 3 SEIs will all be sent on the next video frame. |


<span id="RemoteVideoSinkPosition"></span>
# RemoteVideoSinkPosition

```cpp
enum bytertc::RemoteVideoSinkPosition
```


The position of the remote video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteVideoSinkPositionAfterPostProcess |1 |(Default) After processing. |


<span id="VideoSolution"></span>
# VideoSolution

```cpp
struct bytertc::VideoSolution
```


> Deprecated since 3.45 along with setVideoEncoderConfig(StreamIndex index, const VideoSolution\* solutions, int solution_num) = 0;


Video stream parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/en/docs/12/14187#VideoSolution-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#VideoSolution-height) |
|int |[fps](https://docs.byteplus.com/en/docs/12/14187#VideoSolution-fps) |
|int |[max_send_kbps](https://docs.byteplus.com/en/docs/12/14187#VideoSolution-max_send_kbps) |
|int |[min_send_kbps](https://docs.byteplus.com/en/docs/12/14187#VideoSolution-min_send_kbps) |
|VideoEncodePreference |[encode_preference](https://docs.byteplus.com/en/docs/12/14187#VideoSolution-encode_preference) |


<span id="instructions"></span>
## Instructions

<span id="VideoSolution-width"></span>
### width

```cpp
int bytertc::VideoSolution::width
```


Width (pixels)

<span id="VideoSolution-height"></span>
### height

```cpp
int bytertc::VideoSolution::height
```


Height (pixels)

<span id="VideoSolution-fps"></span>
### fps

```cpp
int bytertc::VideoSolution::fps
```


Video frame rate

<span id="VideoSolution-max_send_kbps"></span>
### max_send_kbps

```cpp
int bytertc::VideoSolution::max_send_kbps = SEND_KBPS_AUTO_CALCULATE
```


Set maximum bitrate in kbps

We recommend the default setting: `SEND_KBPS_AUTO_CALCULATE(-1)`

`SEND_KBPS_DISABLE_VIDEO_SEND(0)` for no limitation for the sending bitrate

<span id="VideoSolution-min_send_kbps"></span>
### min_send_kbps

```cpp
int bytertc::VideoSolution::min_send_kbps = 0
```


<span id="VideoSolution-encode_preference"></span>
### encode_preference

```cpp
VideoEncodePreference bytertc::VideoSolution::encode_preference = VideoEncodePreference::kVideoEncodePreferenceFramerate
```


ncoder preference. See [VideoEncodePreference](https://docs.byteplus.com/en/docs/12/14187#VideoEncodePreference).

<span id="EarMonitorAudioFilter"></span>
# EarMonitorAudioFilter

```cpp
enum bytertc::EarMonitorAudioFilter
```


Whether to include the local audio filters in the in\-ear monitoring.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kEarMonitorAudioFilterNone |0x1 |No audio processing. |
|kEarMonitorAudioFilterReuseAudioProcessing |0x8000 |Audio processed by your processor or the SDK built\-in audio processor, such as 3A, voice changer, and reverb. |


<span id="DataFrameType"></span>
# DataFrameType

```cpp
enum bytertc::DataFrameType
```


Data frame type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kDataFrameTypeSei |0 |SEI video frame |


<span id="SubscribeStateChangeReason"></span>
# SubscribeStateChangeReason

```cpp
enum bytertc::SubscribeStateChangeReason
```


Reason to change the subscription state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSubscribeStateChangeReasonSubscribe |0 |Requested to subscribe. |
|kSubscribeStateChangeReasonUnsubscribe |1 |Requested to unsubscribe. |
|kSubscribeStateChangeReasonRemotePublish |2 |The remote user published a stream. |
|kSubscribeStateChangeReasonRemoteUnpublish |3 |The remote user removed a stream. |
|kSubscribeStateChangeReasonStreamFailed5xx |4 |Failed to subscribe due to the server error. The SDK will automatically retry. |
|kSubscribeStateChangeReasonStreamFailed404 |5 |Failed to subscribe since the stream to be subscribed to was not found in the room. The SDK will automatically retry the subscription. If the subscription still fails, we recommend you exit and retry. |
|kSubscribeStateChangeReasonOverStreamSubscribeLimit |6 |The number of streams the user has subscribedd to has exceeded the limit. |
|kSubscribeStateChangeReasonNoSubscribePermission |7 |The user was not permitted to subscribe to the stream. |


<span id="RtcRoomStats"></span>
# RtcRoomStats

```cpp
struct bytertc::RtcRoomStats
```


Call related statistics

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[tx_lostrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-tx_lostrate) |
|float |[rx_lostrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rx_lostrate) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rtt) |
|unsigned int |[duration](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-duration) |
|unsigned int |[tx_bytes](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-tx_bytes) |
|unsigned int |[rx_bytes](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rx_bytes) |
|unsigned short |[tx_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-tx_kbitrate) |
|unsigned short |[rx_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rx_kbitrate) |
|unsigned short |[rx_audio_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rx_audio_kbitrate) |
|unsigned short |[tx_audio_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-tx_audio_kbitrate) |
|unsigned short |[rx_video_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rx_video_kbitrate) |
|unsigned short |[tx_video_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-tx_video_kbitrate) |
|unsigned short |[rx_screen_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rx_screen_kbitrate) |
|unsigned short |[tx_screen_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-tx_screen_kbitrate) |
|unsigned int |[user_count](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-user_count) |
|double |[cpu_app_usage](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-cpu_app_usage) |
|unsigned short |[tx_cellular_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-tx_cellular_kbitrate) |
|unsigned short |[rx_cellular_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RtcRoomStats-rx_cellular_kbitrate) |


<span id="instructions"></span>
## Instructions

<span id="RtcRoomStats-tx_lostrate"></span>
### tx_lostrate

```cpp
float bytertc::RtcRoomStats::tx_lostrate
```


Current Tx packet loss rate. The range is [0,1].

<span id="RtcRoomStats-rx_lostrate"></span>
### rx_lostrate

```cpp
float bytertc::RtcRoomStats::rx_lostrate
```


Current Rx packet loss rate. The range is [0,1].

<span id="RtcRoomStats-rtt"></span>
### rtt

```cpp
int bytertc::RtcRoomStats::rtt
```


Round\-trip time (in ms) from client side to server side

<span id="RtcRoomStats-duration"></span>
### duration

```cpp
unsigned int bytertc::RtcRoomStats::duration
```


The duration, in seconds, that the local user has spent in the room.

<span id="RtcRoomStats-tx_bytes"></span>
### tx_bytes

```cpp
unsigned int bytertc::RtcRoomStats::tx_bytes
```


Cumulative data sent by the user in bytes.

<span id="RtcRoomStats-rx_bytes"></span>
### rx_bytes

```cpp
unsigned int bytertc::RtcRoomStats::rx_bytes
```


Cumulative data received by the user in bytes.

<span id="RtcRoomStats-tx_kbitrate"></span>
### tx_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::tx_kbitrate
```


The instantaneous value of Tx bitrate in Kbps

<span id="RtcRoomStats-rx_kbitrate"></span>
### rx_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::rx_kbitrate
```


The instantaneous value of Rx bitrate in kbps

<span id="RtcRoomStats-rx_audio_kbitrate"></span>
### rx_audio_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::rx_audio_kbitrate
```


The instantaneous value of audio Rx bitrate in kbps

<span id="RtcRoomStats-tx_audio_kbitrate"></span>
### tx_audio_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::tx_audio_kbitrate
```


The instantaneous value of audio Tx bitrate in kbps

<span id="RtcRoomStats-rx_video_kbitrate"></span>
### rx_video_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::rx_video_kbitrate
```


The instantaneous value of video Rx bitrate in kbps

<span id="RtcRoomStats-tx_video_kbitrate"></span>
### tx_video_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::tx_video_kbitrate
```


The instantaneous value of video Tx bitrate in kbps

<span id="RtcRoomStats-rx_screen_kbitrate"></span>
### rx_screen_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::rx_screen_kbitrate
```


The instantaneous RX bitrate of screen\-sharing video in Kbps

<span id="RtcRoomStats-tx_screen_kbitrate"></span>
### tx_screen_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::tx_screen_kbitrate
```


The instantaneous TX bitrate of screen\-sharing video in Kbps

<span id="RtcRoomStats-user_count"></span>
### user_count

```cpp
unsigned int bytertc::RtcRoomStats::user_count
```


Number of visible users in the current room

<span id="RtcRoomStats-cpu_app_usage"></span>
### cpu_app_usage

```cpp
double bytertc::RtcRoomStats::cpu_app_usage
```


CPU usage (%) of the application

<span id="RtcRoomStats-tx_cellular_kbitrate"></span>
### tx_cellular_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::tx_cellular_kbitrate
```


Cellular Link Send bit rate (kbps), get the instantaneous value of the data

<span id="RtcRoomStats-rx_cellular_kbitrate"></span>
### rx_cellular_kbitrate

```cpp
unsigned short bytertc::RtcRoomStats::rx_cellular_kbitrate
```


Cellular Link Receive bit rate (kbps), get the instantaneous value of the data

<span id="VideoCodecMode"></span>
# VideoCodecMode

```cpp
enum bytertc::VideoCodecMode
```


Video encoding mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoCodecModeAuto |0 |Automatic selection |
|kVideoCodecModeHardware |1 |Hardware encoding |
|kVideoCodecModeSoftware |2 |Software encoding |


<span id="ProblemFeedbackRoomInfo"></span>
# ProblemFeedbackRoomInfo

```cpp
struct bytertc::ProblemFeedbackRoomInfo
```


Room information for audio & video quality feedback

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#ProblemFeedbackRoomInfo-room_id) |
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#ProblemFeedbackRoomInfo-user_id) |


<span id="instructions"></span>
## Instructions

<span id="ProblemFeedbackRoomInfo-room_id"></span>
### room_id

```cpp
const char* bytertc::ProblemFeedbackRoomInfo::room_id = nullptr
```


Room ID.

<span id="ProblemFeedbackRoomInfo-user_id"></span>
### user_id

```cpp
const char* bytertc::ProblemFeedbackRoomInfo::user_id = nullptr
```


The ID of the local user.

<span id="IEncodedVideoFrame"></span>
# IEncodedVideoFrame

```cpp
class bytertc::IEncodedVideoFrame
```


Information about video frames

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual VideoCodecType |[codecType](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-codectype) |
|virtual int64_t |[timestampUs](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-timestampus) |
|virtual int64_t |[timestampDtsUs](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-timestampdtsus) |
|virtual int |[width](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-width) |
|virtual int |[height](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-height) |
|virtual VideoPictureType |[pictureType](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-picturetype) |
|virtual VideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-rotation) |
|virtual uint8_t\* |[data](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-data) |
|virtual int |[dataSize](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-datasize) |
|virtual IEncodedVideoFrame\* |[shallowCopy](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-shallowcopy) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14187#IEncodedVideoFrame-release) |


<span id="instructions"></span>
## Instructions

<span id="IEncodedVideoFrame-codectype"></span>
### codecType

```cpp
virtual VideoCodecType codecType() const = 0;
```


Gets the video encoding type

**Return Value**

Video encoding type. See [VideoCodecType](https://docs.byteplus.com/en/docs/12/14187#VideoCodecType)

<span id="IEncodedVideoFrame-timestampus"></span>
### timestampUs

```cpp
virtual int64_t timestampUs() const = 0;
```


Gets video capture timestamp

**Return Value**

Video capture timestamp in microseconds

<span id="IEncodedVideoFrame-timestampdtsus"></span>
### timestampDtsUs

```cpp
virtual int64_t timestampDtsUs() const = 0;
```


Gets video encoding timestamp

**Return Value**

Video encoding timestamp in microseconds

<span id="IEncodedVideoFrame-width"></span>
### width

```cpp
virtual int width() const = 0;
```


Get video frame width

**Return Value**

Video frame width in px

<span id="IEncodedVideoFrame-height"></span>
### height

```cpp
virtual int height() const = 0;
```


Gets video frame height

**Return Value**

Video frame height in px

<span id="IEncodedVideoFrame-picturetype"></span>
### pictureType

```cpp
virtual VideoPictureType pictureType() const = 0;
```


Gets video compression picture type.

**Return Value**

Video compression picture type.See [VideoPictureType](https://docs.byteplus.com/en/docs/12/14187#VideoPictureType)

<span id="IEncodedVideoFrame-rotation"></span>
### rotation

```cpp
virtual VideoRotation rotation() const = 0;
```


Gets video frame rotation angle

**Return Value**

Video frame rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14187#VideoRotation)

<span id="IEncodedVideoFrame-data"></span>
### data

```cpp
virtual uint8_t* data() const = 0;
```


Get the pointer to the video frame

**Return Value**

The pointer to the video frame

<span id="IEncodedVideoFrame-datasize"></span>
### dataSize

```cpp
virtual int dataSize() const = 0;
```


Gets video frame data size

**Return Value**

Video frame data size

<span id="IEncodedVideoFrame-shallowcopy"></span>
### shallowCopy

```cpp
virtual IEncodedVideoFrame* shallowCopy() const = 0;
```


Makes shallow copies of video frame and return pointer

<span id="IEncodedVideoFrame-release"></span>
### release

```cpp
virtual void release() = 0;
protected:
```


Releases video frame

<span id="RecordingProgress"></span>
# RecordingProgress

```cpp
struct bytertc::RecordingProgress
```


Local recording progress

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|unsigned long long |[duration](https://docs.byteplus.com/en/docs/12/14187#RecordingProgress-duration) |
|unsigned long long |[file_size](https://docs.byteplus.com/en/docs/12/14187#RecordingProgress-file_size) |


<span id="instructions"></span>
## Instructions

<span id="RecordingProgress-duration"></span>
### duration

```cpp
unsigned long long bytertc::RecordingProgress::duration
```


The cumulative recording time of the current file, in milliseconds

<span id="RecordingProgress-file_size"></span>
### file_size

```cpp
unsigned long long bytertc::RecordingProgress::file_size
```


The size of the currently recorded file in bytes

<span id="FallbackOrRecoverReason"></span>
# FallbackOrRecoverReason

```cpp
enum bytertc::FallbackOrRecoverReason
```


Reason of the Fallback or reverting from a Fallback of the subscribed stream or the publishing stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kFallbackOrRecoverReasonUnknown |\-1 |The default: Fallback due to an unknown reason that is neither insufficient bandwidth of the network nor poor\-performance of the device |
|kFallbackOrRecoverReasonSubscribeFallbackByBandwidth |0 |Fallback of the subscribed stream due to insufficient bandwidth of the network |
|kFallbackOrRecoverReasonSubscribeFallbackByPerformance |1 |Fallback of the subscribed stream due to poor performance of the device |
|kFallbackOrRecoverReasonSubscribeRecoverByBandwidth |2 |Reverting from a Fallback of the subscribed stream due to the recovery of the network bandwidth |
|kFallbackOrRecoverReasonSubscribeRecoverByPerformance |3 |Reverting from a Fallback of the subscribed stream due to the amelioration of the device performance |
|kFallbackOrRecoverReasonPublishFallbackByBandwidth |4 |Fallback of the publishing stream due to Insufficient bandwidth of the network |
|kFallbackOrRecoverReasonPublishFallbackByPerformance |5 |Fallback of the publishing stream due to poor\-performance of the device |
|kFallbackOrRecoverReasonPublishRecoverByBandwidth |6 |Reverting from a Fallback of the publishing stream due to the recovery of the network bandwidth |
|kFallbackOrRecoverReasonPublishRecoverByPerformance |7 |Reverting from a Fallback of the publishing stream due to the amelioration of the device performance |


<span id="SubscribeState"></span>
# SubscribeState

```cpp
enum bytertc::SubscribeState
```


Stream subscription state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSubscribeStateSubscribed |0 |Successfully subscribed. |
|kSubscribeStateUnsubscribed |1 |Failed to subscribe. |


<span id="EncodedVideoFrameBuilder"></span>
# EncodedVideoFrameBuilder

```cpp
struct bytertc::EncodedVideoFrameBuilder
```


Video frame parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VideoCodecType |[codec_type](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-codec_type) |
|VideoPictureType |[picture_type](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-picture_type) |
|VideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-rotation) |
|uint8_t\* |[data](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-data) |
|int |[size](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-size) |
|int |[width](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-height) |
|int64_t |[timestamp_us](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-timestamp_us) |
|int64_t |[timestamp_dts_us](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-timestamp_dts_us) |
|int( *)(uint8_t*data, int size, void\*user_opaque) |[memory_deleter](https://docs.byteplus.com/en/docs/12/14187#EncodedVideoFrameBuilder-memory_deleter) |


<span id="instructions"></span>
## Instructions

<span id="EncodedVideoFrameBuilder-codec_type"></span>
### codec_type

```cpp
VideoCodecType bytertc::EncodedVideoFrameBuilder::codec_type = kVideoCodecTypeUnknown
```


Video frame encoding format. See [VideoCodecType](https://docs.byteplus.com/en/docs/12/14187#VideoCodecType)

<span id="EncodedVideoFrameBuilder-picture_type"></span>
### picture_type

```cpp
VideoPictureType bytertc::EncodedVideoFrameBuilder::picture_type = kVideoPictureTypeUnknown
```


Video frame encoding type. See [VideoPictureType](https://docs.byteplus.com/en/docs/12/14187#VideoPictureType)

<span id="EncodedVideoFrameBuilder-rotation"></span>
### rotation

```cpp
VideoRotation bytertc::EncodedVideoFrameBuilder::rotation = kVideoRotation0
```


Video frame rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14187#VideoRotation)

<span id="EncodedVideoFrameBuilder-data"></span>
### data

```cpp
uint8_t* bytertc::EncodedVideoFrameBuilder::data = nullptr
```


Video frame data pointer

**Notes**

IEncodedVideoFrame takes ownership of the data

<span id="EncodedVideoFrameBuilder-size"></span>
### size

```cpp
int bytertc::EncodedVideoFrameBuilder::size = 0
```


Video frame data size

<span id="EncodedVideoFrameBuilder-width"></span>
### width

```cpp
int bytertc::EncodedVideoFrameBuilder::width = 0
```


Video frame width in px

<span id="EncodedVideoFrameBuilder-height"></span>
### height

```cpp
int bytertc::EncodedVideoFrameBuilder::height = 0
```


Video frame height in px

<span id="EncodedVideoFrameBuilder-timestamp_us"></span>
### timestamp_us

```cpp
int64_t bytertc::EncodedVideoFrameBuilder::timestamp_us = 0
```


Video capture timestamp in microseconds

<span id="EncodedVideoFrameBuilder-timestamp_dts_us"></span>
### timestamp_dts_us

```cpp
int64_t bytertc::EncodedVideoFrameBuilder::timestamp_dts_us = 0
```


Video encoding timestamp in microseconds

<span id="EncodedVideoFrameBuilder-memory_deleter"></span>
### memory_deleter

```cpp
int(* bytertc::EncodedVideoFrameBuilder::memory_deleter) (uint8_t *data, int size, void *user_opaque) = nullptr
```


The user\-defined video frame releases the callback function pointer. If the pointer is not empty, the method will be called to free memory space

<span id="PushSingleStreamParam"></span>
# PushSingleStreamParam

```cpp
struct bytertc::PushSingleStreamParam
```


Configurations for pushing a single media stream to CDN.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#PushSingleStreamParam-room_id) |
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#PushSingleStreamParam-user_id) |
|const char\* |[uri](https://docs.byteplus.com/en/docs/12/14187#PushSingleStreamParam-uri) |
|bool |[is_screen_stream](https://docs.byteplus.com/en/docs/12/14187#PushSingleStreamParam-is_screen_stream) |
|DestInfo\* |[dest_info](https://docs.byteplus.com/en/docs/12/14187#PushSingleStreamParam-dest_info) |
|int32_t |[dest_info_size](https://docs.byteplus.com/en/docs/12/14187#PushSingleStreamParam-dest_info_size) |
|SingleStreamPushType |[push_type](https://docs.byteplus.com/en/docs/12/14187#PushSingleStreamParam-push_type) |


<span id="instructions"></span>
## Instructions

<span id="PushSingleStreamParam-room_id"></span>
### room_id

```cpp
const char* bytertc::PushSingleStreamParam::room_id
```


The room ID of the media stream

<span id="PushSingleStreamParam-user_id"></span>
### user_id

```cpp
const char* bytertc::PushSingleStreamParam::user_id
```


The user ID of the media stream

<span id="PushSingleStreamParam-uri"></span>
### uri

```cpp
const char* bytertc::PushSingleStreamParam::uri
```


The URL for live transcoding. Only supports live transcoding via RTMP. The URL should match the regular expression `/^rtmps?:\\/\\//`.

This parameter cannot be updated during the task.

<span id="PushSingleStreamParam-is_screen_stream"></span>
### is_screen_stream

```cpp
bool bytertc::PushSingleStreamParam::is_screen_stream
```


Reserved field. Do not set this field in the single\-stream SDK.

<span id="PushSingleStreamParam-dest_info"></span>
### dest_info

```cpp
DestInfo* bytertc::PushSingleStreamParam::dest_info = nullptr
```


forward destination room info，nullptr by default

<span id="PushSingleStreamParam-dest_info_size"></span>
### dest_info_size

```cpp
int32_t bytertc::PushSingleStreamParam::dest_info_size = 0
```


forward dest room counts, The length of `dest_info`.

0 by default, The range is `[0, 8]`

<span id="PushSingleStreamParam-push_type"></span>
### push_type

```cpp
SingleStreamPushType bytertc::PushSingleStreamParam::push_type = kPushToCDN
```


Single stream push type, specifying whether to push the media stream to CDN or RTC room. Default value is push to CDN.

<span id="VoiceEqualizationConfig"></span>
# VoiceEqualizationConfig

```cpp
struct bytertc::VoiceEqualizationConfig
```


Voice equalization effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VoiceEqualizationBandFrequency |[frequency](https://docs.byteplus.com/en/docs/12/14187#VoiceEqualizationConfig-frequency) |
|int |[gain](https://docs.byteplus.com/en/docs/12/14187#VoiceEqualizationConfig-gain) |


<span id="instructions"></span>
## Instructions

<span id="VoiceEqualizationConfig-frequency"></span>
### frequency

```cpp
VoiceEqualizationBandFrequency bytertc::VoiceEqualizationConfig::frequency
```


Frequency band. See [VoiceEqualizationBandFrequency](https://docs.byteplus.com/en/docs/12/14187#VoiceEqualizationBandFrequency).

<span id="VoiceEqualizationConfig-gain"></span>
### gain

```cpp
int bytertc::VoiceEqualizationConfig::gain
```


Gain of the frequency band in dB. The range is `[-15, 15]`.

<span id="SourceWantedData"></span>
# SourceWantedData

```cpp
struct bytertc::SourceWantedData
```


Performance fallback related data

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/en/docs/12/14187#SourceWantedData-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#SourceWantedData-height) |
|int |[frame_rate](https://docs.byteplus.com/en/docs/12/14187#SourceWantedData-frame_rate) |


<span id="instructions"></span>
## Instructions

<span id="SourceWantedData-width"></span>
### width

```cpp
int bytertc::SourceWantedData::width
```


If the send performance rollback is not turned on, this value represents the recommended Video input width;

If the send performance rollback is turned on, this value represents the maximum width of the current push stream.

<span id="SourceWantedData-height"></span>
### height

```cpp
int bytertc::SourceWantedData::height
```


If send performance fallback is not turned on, this value represents the recommended video input height;

If send performance fallback is turned on, this value represents the maximum height of the current push stream.

<span id="SourceWantedData-frame_rate"></span>
### frame_rate

```cpp
int bytertc::SourceWantedData::frame_rate
```


If send performance fallback is not turned on, this value represents the recommended video input frame rate in fps;

If send performance fallback is turned on, this value represents the maximum frame rate of the current push stream in fps.

<span id="VoiceEqualizationBandFrequency"></span>
# VoiceEqualizationBandFrequency

```cpp
enum bytertc::VoiceEqualizationBandFrequency
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


<span id="MixedStreamLayoutRegionType"></span>
# MixedStreamLayoutRegionType

```cpp
enum bytertc::MixedStreamLayoutRegionType
```


The contents of the layout section in the mixing stream, including video section and water mark section.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamLayoutRegionTypeVideoStream |0 |Video. |
|kMixedStreamLayoutRegionTypeImage |1 |Watermark image. |


<span id="AudioPlaybackDevice"></span>
# AudioPlaybackDevice

```cpp
enum bytertc::AudioPlaybackDevice
```


Audio playback device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioPlaybackDeviceHeadset |1 |Wired earphones |
|kAudioPlaybackDeviceEarpiece |2 |Earpiece |
|kAudioPlaybackDeviceSpeakerphone |3 |Speaker |
|kAudioPlaybackDeviceHeadsetBluetooth |4 |Bluetooth earphones |
|kAudioPlaybackDeviceHeadsetUSB |5 |USB Device |


<span id="PauseResumeControlMediaType"></span>
# PauseResumeControlMediaType

```cpp
enum bytertc::PauseResumeControlMediaType
```


Type of the stream to be paused/resumed.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRTCPauseResumeControlMediaTypeAudio |0 |Audio only |
|kRTCPauseResumeControlMediaTypeVideo |1 |Video only |
|kRTCPauseResumeControlMediaTypeVideoAndAudio |2 |Both video and audio |


<span id="BackgroundMode"></span>
# BackgroundMode

```cpp
enum bytertc::BackgroundMode
```


Background mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kBackgroundModeNone |0 |No |
|kBackgroundModeBlur |1 |Virtualization |
|kBackgroundModeA |2 |Background 1 |
|kBackgroundModeB |3 |Background 2 |


<span id="PlayerError"></span>
# PlayerError

```cpp
enum bytertc::PlayerError
```


Error code for audio playout.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPlayerErrorOK |0 |OK |
|kPlayerErrorFormatNotSupport |1 |Format not supported. |
|kPlayerErrorInvalidPath |2 |Invalid file path. |
|kPlayerErrorInvalidState |3 |The prerequisite is not met. Check the specific API doc. |
|kPlayerErrorInvalidPosition |4 |Invalid position. |
|kPlayerErrorInvalidVolume |5 |Invalid volume. |
|kPlayerErrorInvalidPitch |6 |Invalid pitch value. |
|kPlayerErrorInvalidAudioTrackIndex |7 |Invalid audio track. |
|kPlayerErrorInvalidPlaybackSpeed |8 |Invalid playback speed. |
|kPlayerErrorInvalidEffectId |9 |Invalid effect ID. Receive this error code when you call other APIs before the audio file is preloaded or opened. |
|kPlayerErrorCurrentlyPlaying |10 |The resource is currently playing. |


<span id="VoiceReverbType"></span>
# VoiceReverbType

```cpp
enum bytertc::VoiceReverbType
```


Reverb effect type

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


<span id="MediaPlayerCustomSource"></span>
# MediaPlayerCustomSource

```cpp
struct bytertc::MediaPlayerCustomSource
```


The audio source for media player.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|MediaPlayerCustomSourceMode |[mode](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerCustomSource-mode) |
|MediaPlayerCustomSourceStreamType |[type](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerCustomSource-type) |


<span id="instructions"></span>
## Instructions

<span id="MediaPlayerCustomSource-mode"></span>
### mode

```cpp
MediaPlayerCustomSourceMode bytertc::MediaPlayerCustomSource::mode = kMediaPlayerCustomSourceModePush
```


See [MediaPlayerCustomSourceMode](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerCustomSourceMode).

<span id="MediaPlayerCustomSource-type"></span>
### type

```cpp
MediaPlayerCustomSourceStreamType bytertc::MediaPlayerCustomSource::type = kMediaPlayerCustomSourceStreamTypeRaw
```


See [MediaPlayerCustomSourceStreamType](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerCustomSourceStreamType).

<span id="AudioAlignmentMode"></span>
# AudioAlignmentMode

```cpp
enum bytertc::AudioAlignmentMode
```


The alignment mode of remote audio streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioAlignmentModeOff |0 |Disabled |
|kAudioAlignmentModeAudioMixing |1 |All subscribed audio streams are aligned based on the process of the background music. |


<span id="BluetoothMode"></span>
# BluetoothMode

```cpp
enum bytertc::BluetoothMode
```


bluetooth mode, it works only in media mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kBluetoothModeAuto |0 |select bluetooth mode automatically. |
|kBluetoothModeA2DP |1 |use A2DP mode |
|kBluetoothModeHFP |2 |use HFP mode |


<span id="ProblemFeedbackOption"></span>
# ProblemFeedbackOption

```cpp
enum bytertc::ProblemFeedbackOption
```


Audio & video quality feedback problem

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kProblemFeedbackOptionNone |0 |Everything is OK. |
|kProblemFeedbackOptionOtherMessage |1ULL << 0 |Issues not included in the list |
|kProblemFeedbackOptionDisconnected |1ULL << 1 |Connection failed |
|kProblemFeedbackOptionEarBackDelay |1ULL << 2 |High latency for the ear monitor |
|kProblemFeedbackOptionLocalNoise |1ULL << 10 |Noise on the local end |
|kProblemFeedbackOptionLocalAudioLagging |1ULL << 11 |Audio stall on the local end |
|kProblemFeedbackOptionLocalNoAudio |1ULL << 12 |No sound on the local end |
|kProblemFeedbackOptionLocalAudioStrength |1ULL << 13 |Too little/loud sound on the local end |
|kProblemFeedbackOptionLocalEcho |1ULL << 14 |Echo noise on the local end |
|kProblemFeedbackOptionLocalVideoFuzzy |1ULL << 24 |Unclear video on the local end |
|kProblemFeedbackOptionLocalNotSync |1ULL << 25 |Audio & video out of sync on the local end |
|kProblemFeedbackOptionLocalVideoLagging |1ULL << 26 |Video stall on the local end |
|kProblemFeedbackOptionLocalNoVideo |1ULL << 27 |No picture on the local end |
|kProblemFeedbackOptionRemoteNoise |1ULL << 37 |Noise on the remote end |
|kProblemFeedbackOptionRemoteAudioLagging |1ULL << 38 |Audio stall on the remote end |
|kProblemFeedbackOptionRemoteNoAudio |1ULL << 39 |No sound on the remote end |
|kProblemFeedbackOptionRemoteAudioStrength |1ULL << 40 |Too little/loud sound on the remote end |
|kProblemFeedbackOptionRemoteEcho |1ULL << 41 |Echo noise on the remote end |
|kProblemFeedbackOptionRemoteVideoFuzzy |1ULL << 51 |Unclear video on the remote end |
|kProblemFeedbackOptionRemoteNotSync |1ULL << 52 |Audio & video out of sync on the remote end |
|kProblemFeedbackOptionRemoteVideoLagging |1ULL << 53 |Video stall on the remote end |
|kProblemFeedbackOptionRemoteNoVideo |1ULL << 54 |No picture on the remote end |


<span id="MessageConfig"></span>
# MessageConfig

```cpp
enum bytertc::MessageConfig
```


Message type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMessageConfigReliableOrdered |0 |Low latency reliable and orderly message |
|kMessageConfigUnreliableOrdered |1 |Ultra\-low latency ordered message |
|kMessageConfigUnreliableUnordered |2 |Ultra\-low latency unordered message |


<span id="ServerACKMsg"></span>
# ServerACKMsg

```cpp
struct bytertc::ServerACKMsg
```


Server message send result content

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[length](https://docs.byteplus.com/en/docs/12/14187#ServerACKMsg-length) |
|char\* |[ack_msg](https://docs.byteplus.com/en/docs/12/14187#ServerACKMsg-ack_msg) |


<span id="instructions"></span>
## Instructions

<span id="ServerACKMsg-length"></span>
### length

```cpp
int bytertc::ServerACKMsg::length
```


length

<span id="ServerACKMsg-ack_msg"></span>
### ack_msg

```cpp
char* bytertc::ServerACKMsg::ack_msg
```


content of the message

<span id="FirstFramePlayState"></span>
# FirstFramePlayState

```cpp
enum bytertc::FirstFramePlayState
```


First frame playback status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kFirstFramePlayStatePlaying |0 |Playing |
|kFirstFramePlayStatePlayed |1 |Play success |
|kFirstFramePlayStateEnd |2 |Play failed |


<span id="VideoOrientation"></span>
# VideoOrientation

```cpp
enum bytertc::VideoOrientation
```


Orientation of the video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoOrientationAdaptive |0 |(Default) The original orientation of the captured video frame. |
|kVideoOrientationPortrait |1 |Portrait mode. Adjust the captured video frame to vertical layout in RTC SDK. |
|kVideoOrientationLandscape |2 |Landscape mode. Adjust the captured video frame to horizontal layout in RTC SDK. |


<span id="HardwareEchoDetectionResult"></span>
# HardwareEchoDetectionResult

```cpp
enum bytertc::HardwareEchoDetectionResult
```


Result of the detection inited before joining a room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kHardwareEchoDetectionResultCanceled |0 |Detection is stopped by the call of `stopHardwareEchoDetection` before the SDK reports the detection result. |
|kHardwareEchoDetectionResultUnknown |1 |Unknown state<br><br>Contact us if you retry several times but keep failing. |
|kHardwareEchoDetectionResultNormal |2 |Excellent<br><br>No echo issue is detected. |
|kHardwareEchoDetectionResultPoor |3 |Echo<br><br>Echo issue is detected. Recommend the user join the call with a headset through the interface. |


<span id="ProcessorActionDomain"></span>
# ProcessorActionDomain

```cpp
enum bytertc::ProcessorActionDomain
```


The effective range of the custom video preprocessor, including preview only, encode only, and both preview and encode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kProcessorActionDomainPreviewAndEncode |0 |The processed video frames are used for both local preview and pushing to the remote. |
|kProcessorActionDomainPreview |1 |The processed video frames are used for local preview only. |
|kProcessorActionDomainEncode |2 |The processed video frames are used for pushing to the remote only. |


<span id="PlayerState"></span>
# PlayerState

```cpp
enum bytertc::PlayerState
```


Player state.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPlayerStateIdle |0 |Not started. |
|kPlayerStatePreloaded |1 |Preloaded. |
|kPlayerStateOpened |2 |Opened. |
|kPlayerStatePlaying |3 |Playing. |
|kPlayerStatePaused |4 |Paused. |
|kPlayerStateStopped |5 |Playback is stopped. |
|kPlayerStateFailed |6 |Failed. |
|kPlayerStateFinished |7 |Playback ended. |
|kPlayerStateLoopFinished |8 |Loop playback ended. |


<span id="PublishState"></span>
# PublishState

```cpp
enum bytertc::PublishState
```


Stream publishing state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPublishStatePublished |0 |Successfully published. |
|kPublishStateUnpublished |1 |Failed to publish. |


<span id="VideoRotation"></span>
# VideoRotation

```cpp
enum bytertc::VideoRotation
```


Video frame rotation

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoRotation0 |0 |Not to rotate. |
|kVideoRotation90 |90 |Rotate 90 degrees clockwise. |
|kVideoRotation180 |180 |Rotate 180 degrees clockwise. |
|kVideoRotation270 |270 |Rotate 270 degrees clockwise. |


<span id="SysStats"></span>
# SysStats

```cpp
struct bytertc::SysStats
```


The CPU and memory information used by App.

You will periodically (2s) receive `onSysStats` of the information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|unsigned int |[cpu_cores](https://docs.byteplus.com/en/docs/12/14187#SysStats-cpu_cores) |
|double |[cpu_app_usage](https://docs.byteplus.com/en/docs/12/14187#SysStats-cpu_app_usage) |
|double |[memory_usage](https://docs.byteplus.com/en/docs/12/14187#SysStats-memory_usage) |
|unsigned long long |[full_memory](https://docs.byteplus.com/en/docs/12/14187#SysStats-full_memory) |
|unsigned long long |[total_memory_usage](https://docs.byteplus.com/en/docs/12/14187#SysStats-total_memory_usage) |
|unsigned long long |[free_memory](https://docs.byteplus.com/en/docs/12/14187#SysStats-free_memory) |
|double |[memory_ratio](https://docs.byteplus.com/en/docs/12/14187#SysStats-memory_ratio) |
|double |[total_memory_ratio](https://docs.byteplus.com/en/docs/12/14187#SysStats-total_memory_ratio) |


<span id="instructions"></span>
## Instructions

<span id="SysStats-cpu_cores"></span>
### cpu_cores

```cpp
unsigned int bytertc::SysStats::cpu_cores
```


The CPU cores of your system.

<span id="SysStats-cpu_app_usage"></span>
### cpu_app_usage

```cpp
double bytertc::SysStats::cpu_app_usage
```


The CPU usage rate of the current application. The value range is [0,1].

<span id="SysStats-memory_usage"></span>
### memory_usage

```cpp
double bytertc::SysStats::memory_usage
```


The memory usage of the current application(/MB).

<span id="SysStats-full_memory"></span>
### full_memory

```cpp
unsigned long long bytertc::SysStats::full_memory
```


Total memory(/MB).

<span id="SysStats-total_memory_usage"></span>
### total_memory_usage

```cpp
unsigned long long bytertc::SysStats::total_memory_usage
```


Used system memory(/MB).

<span id="SysStats-free_memory"></span>
### free_memory

```cpp
unsigned long long bytertc::SysStats::free_memory
```


Free system memory(/MB).

<span id="SysStats-memory_ratio"></span>
### memory_ratio

```cpp
double bytertc::SysStats::memory_ratio
```


The memory usage rate of the current application(/%).

<span id="SysStats-total_memory_ratio"></span>
### total_memory_ratio

```cpp
double bytertc::SysStats::total_memory_ratio
```


The system memory usage rate(/%).

<span id="LocalAudioStreamState"></span>
# LocalAudioStreamState

```cpp
enum bytertc::LocalAudioStreamState
```


Local audio stream status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalAudioStreamStateStopped |0 |The default initial state of the local audio.<br><br>Callback to this state when the microphone stops working, corresponding to the error code kLocalAudioStreamErrorOk |
|kLocalAudioStreamStateRecording |1 |The local audio recording device started successfully.<br><br>Callback to the state when the first frame of audio is collected, corresponding to the error code kLocalAudioStreamErrorOk |
|kLocalAudioStreamStateEncoding |2 |The first frame of the local audio was successfully encoded.<br><br>Callback to the state when the audio first frame encoding is successful, corresponding to the error code kLocalAudioStreamErrorOk |
|kLocalAudioStreamStateFailed |3 |The local audio startup failed, and the status is called back at the following times:<br><br><br>&nbsp;<br><br>* The local recording device failed to start, corresponding to the error code kLocalAudioStreamErrorRecordFailure<br><br>* No recording device permission was detected, corresponding to the error code kLocalAudioStreamErrorDeviceNoPermission<br><br>* The audio encoding failed, corresponding to the error code kLocalAudioStreamErrorEncodeFailure |
|kLocalAudioStreamStateMute |4 |Callback the state after the local audio is successfully muted.<br><br>Callback after successful [setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudiocapturedevicemute) call, corresponding to kLocalAudioStreamErrorOk in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStreamError). |
|kLocalAudioStreamStateUnmute |5 |Callback the state after the local audio is successfully unmuted.<br><br>Callback after successful [setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudiocapturedevicemute) call, corresponding to kLocalAudioStreamErrorOk in the error code [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStreamError). |


<span id="ConnectionState"></span>
# ConnectionState

```cpp
enum bytertc::ConnectionState
```


SDK Connection status with the signaling server.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kConnectionStateDisconnected |1 |Disconnected for 12s, SDK will try to reconnect automatically. |
|kConnectionStateConnecting |2 |The first request to connect to the server. Connecting. |
|kConnectionStateConnected |3 |The first connection was successful. |
|kConnectionStateReconnecting |4 |The code includes the following status:<br><br><br>&nbsp;<br><br>* The first connection is not successful for 10s.<br><br>* The connection has been lost for 10s. Auto reconnecting. |
|kConnectionStateReconnected |5 |Successful reconnection after disconnection. |
|kConnectionStateLost |6 |In status `kConnectionStateDisconnected` for more than 10s without a successful reconnection. SDK will still continue to try to reconnect. |
|kConnectionStateFailed |7 |Connection failure caused by abnormal state of the server. SDK will not automatically reconnect, please re\-enter the room or contact technical support. |


<span id="VideoRateInfo"></span>
# VideoRateInfo

```cpp
struct bytertc::VideoRateInfo
```


Custom coded stream information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[fps](https://docs.byteplus.com/en/docs/12/14187#VideoRateInfo-fps) |
|int |[bitrate_kbps](https://docs.byteplus.com/en/docs/12/14187#VideoRateInfo-bitrate_kbps) |
|int |[min_bitrate_kbps](https://docs.byteplus.com/en/docs/12/14187#VideoRateInfo-min_bitrate_kbps) |


<span id="instructions"></span>
## Instructions

<span id="VideoRateInfo-fps"></span>
### fps

```cpp
int bytertc::VideoRateInfo::fps = 0
```


Frame rate, units fps

<span id="VideoRateInfo-bitrate_kbps"></span>
### bitrate_kbps

```cpp
int bytertc::VideoRateInfo::bitrate_kbps = 0
```


Bit rate, unit kbps

<span id="VideoRateInfo-min_bitrate_kbps"></span>
### min_bitrate_kbps

```cpp
int bytertc::VideoRateInfo::min_bitrate_kbps = 0
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `min_bitrate_kbps`.

It defaults to `0`.

It ranges within [0, bitrate_kbps). When `bitrate_kbps` < `min_bitrate_kbps`, the bitrate is self\-adapted.

In the following circumstances, the assignment to this variable has no effect:


* When `bitrate_kbps` = `0`, the video encoding is disabled.

* When `bitrate_kbps` < `0`, the bitrate is self\-adapted.

    &nbsp;


<span id="contenthint"></span>
# ContentHint

```cpp
enum bytertc::ContentHint
```


Content hints of the internally captured screen video stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kContentHintDetails |0 |Detailed content. Recommended when you capture documents, images, etc. Default value. |
|kContentHintMotion |1 |Animation content. Recommended when you capture videos, games, etc. |


<span id="UserVisibilityChangeError"></span>
# UserVisibilityChangeError

```cpp
enum bytertc::UserVisibilityChangeError
```


User visibility state change error.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kUserVisibilityChangeErrorOk |0 |Success. |
|kUserVisibilityChangeErrorUnknown |1 |Unknown error. |
|kUserVisibilityChangeErrorTooManyVisibleUser |2 |Visible users in the room have reached the upper limit. |


<span id="VideoStreamType"></span>
# VideoStreamType

```cpp
enum bytertc::VideoStreamType
```


Remote video type

Currently C++ sdk only supports kVideoStreamTypeHigh type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoStreamTypeHigh |0 |High Resolution Video Streaming |
|kVideoStreamTypeLow |1 |Low Resolution Video |


<span id="AudioEffectPlayerConfig"></span>
# AudioEffectPlayerConfig

```cpp
struct bytertc::AudioEffectPlayerConfig
```


Mixing configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|AudioMixingType |[type](https://docs.byteplus.com/en/docs/12/14187#AudioEffectPlayerConfig-type) |
|int |[play_count](https://docs.byteplus.com/en/docs/12/14187#AudioEffectPlayerConfig-play_count) |
|int |[pitch](https://docs.byteplus.com/en/docs/12/14187#AudioEffectPlayerConfig-pitch) |
|int |[start_pos](https://docs.byteplus.com/en/docs/12/14187#AudioEffectPlayerConfig-start_pos) |


<span id="instructions"></span>
## Instructions

<span id="AudioEffectPlayerConfig-type"></span>
### type

```cpp
AudioMixingType bytertc::AudioEffectPlayerConfig::type = kAudioMixingTypePlayoutAndPublish
```


Mixing playback types. See [AudioMixingType](https://docs.byteplus.com/en/docs/12/14187#AudioMixingType)

<span id="AudioEffectPlayerConfig-play_count"></span>
### play_count

```cpp
int bytertc::AudioEffectPlayerConfig::play_count = 1
```


Mix playback times


* Play_count < = 0: Infinite loop

* Play_count == 1: Play once (default)

* Play_count \> 1: Play play_count times

    &nbsp;


<span id="pitch"></span>
### pitch

```cpp
int bytertc::AudioEffectPlayerConfig::pitch = 0
```


The increase or decrease value compared with the original pitch of the music file. The range is `[-12, 12]`. The default value is 0. The pitch distance between two adjacent values is half a step. A positive value indicates a rising pitch, and a negative value indicates a falling pitch.

<span id="AudioEffectPlayerConfig-start_pos"></span>
### start_pos

```cpp
int bytertc::AudioEffectPlayerConfig::start_pos = 0
```


The starting position in ms. 0 by default.

<span id="MediaPlayerConfig"></span>
# MediaPlayerConfig

```cpp
struct bytertc::MediaPlayerConfig
```


Mixing configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[play_count](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerConfig-play_count) |
|int |[start_pos](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerConfig-start_pos) |
|int64_t |[callback_on_progress_interval](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerConfig-callback_on_progress_interval) |
|bool |[sync_progress_to_record_frame](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerConfig-sync_progress_to_record_frame) |
|bool |[auto_play](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerConfig-auto_play) |
|AudioMixingType |[type](https://docs.byteplus.com/en/docs/12/14187#MediaPlayerConfig-type) |


<span id="instructions"></span>
## Instructions

<span id="MediaPlayerConfig-play_count"></span>
### play_count

```cpp
int bytertc::MediaPlayerConfig::play_count = 1
```


Mix playback times


* Play_count < = 0: Infinite loop

* Play_count == 1: Play once (default)

* Play_count \> 1: Play play_count times

    &nbsp;


<span id="start-pos"></span>
### start_pos

```cpp
int bytertc::MediaPlayerConfig::start_pos = 0
```


The starting position in ms. 0 by default.

<span id="MediaPlayerConfig-callback_on_progress_interval"></span>
### callback_on_progress_interval

```cpp
int64_t bytertc::MediaPlayerConfig::callback_on_progress_interval = 0
```


Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing in ms.


* interval \> 0: The callback is enabled. The actual interval is a multiple of 10. If the input value is not divisible by 10, it will be automatically rounded up. For example, if 52 is entered, the actual interval is 60 ms.

* interval <= 0: The callback is disabled.

    &nbsp;


<span id="sync-progress-to-record-frame"></span>
### sync_progress_to_record_frame

```cpp
bool bytertc::MediaPlayerConfig::sync_progress_to_record_frame = false
```


Attach the process information of local audio file mixing to the captured audio data. Enable the function to enhance the synchronicity of the remote audio mixing.


* The function is effective when mixing a single audio file.

* Use `true` for enabling the function and `false` for disabling the function. The default is `false`.

    &nbsp;


<span id="auto-play"></span>
### auto_play

```cpp
bool bytertc::MediaPlayerConfig::auto_play = true
```


Play the audio automatically. If not, call [start](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-start) to play the audio.

<span id="MediaPlayerConfig-type"></span>
### type

```cpp
AudioMixingType bytertc::MediaPlayerConfig::type = kAudioMixingTypePlayoutAndPublish
```


For mixing playback types. See [AudioMixingType](https://docs.byteplus.com/en/docs/12/14187#AudioMixingType)

<span id="RoomProfileType"></span>
# RoomProfileType

```cpp
enum bytertc::RoomProfileType
```


Room profile

Choose an appropriate room\-profile option to meet the requirement of the scenario for media encoding algorithm, video profiles, and network configurations.

Call `setAudioProfile` to apply another audio quality option.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRoomProfileTypeCommunication |0 |General mode by default<br><br>It is equivalent to `kRoomProfileTypeMeeting = 16`.<br><br>Contact us to alter the default settings. |
|kRoomProfileTypeGame |2 |Game voice mode. Low consumption of computing resources and network data<br><br>Additional performance optimizations have been made for low\-end devices:<br><br><br>&nbsp;<br><br>* Encodes frame length 40/60 for some low\-end models.<br><br>* Disables software 3A audio processing for some low\-end models.<br><br>   Enhance iOS Compatibility with other screen recordings to avoid audio recordings being interrupted by RTC. |
|kRoomProfileTypeCloudGame |3 |Cloud game mode.<br><br>Use this mode for game App requiring low latency.<br><br>During poor network connection, communication experiences get worse with this mode. |
|kRoomProfileTypeLowLatency |4 |Cloud render mode featuring extra\-low latency.<br><br>Choose this mode if it is not a game App yet requires low latency.<br><br>In this mode, latency will significantly decrease at the cost of lower audio quality as well as the bad performance with weak network signal. |
|kRoomProfileTypeChatRoom |6 |For video and audio chat rooms of 3 or more people |
|kRoomProfileTypeInteractivePodcast |10 |For interactive podcasts that the host can have video and audio interactions with the audience. The voice mode is set to communication mode to avoid volume spiking and dipping acutely. |
|kRoomProfileTypeChorus |12 |For the online\-chorusing scenarios requiring high\-quality audio and low latency. Contact our technical specialists before you apply it to your App. |
|kRoomProfileTypeGameStreaming |14 |For scenarios of streaming live videos to only one client on the LAN. It can be applied to devices on the Internet or LAN. |
|kRoomProfileTypeMeeting |16 |For meeting Apps installed on personal devices |
|kRoomProfileTypeMeetingRoom |17 |For meeting Apps installed on terminals of meeting rooms, such as Rooms. |
|kRoomProfileTypeClassroom |18 |For the online classrooms and lectures that over 10 participants in the room are allowed to join the video chat. |
|kRoomProfileTypeCall |19 |Focus on smoothness, the default video bitrate is lower. |
|kRoomProfileTypeLive |20 |Focus on quality, the default video bitrate is higher. |


<span id="IVideoSink"></span>
# IVideoSink

```cpp
class bytertc::IVideoSink
```


Custom video renderer

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual bool |[onFrame](https://docs.byteplus.com/en/docs/12/14187#IVideoSink-onframe) |
|virtual int |[getRenderElapse](https://docs.byteplus.com/en/docs/12/14187#IVideoSink-getrenderelapse) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14187#IVideoSink-release) |


<span id="instructions"></span>
## Instructions

<span id="IVideoSink-onframe"></span>
### onFrame

```cpp
virtual bool onFrame(IVideoFrame* video_frame) = 0;
```


Video frame callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_frame |IVideoFrame\* |Video frame structure. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/14187#IVideoFrame). |


**Return Value**

Temporarily unavailable

<span id="IVideoSink-getrenderelapse"></span>
### getRenderElapse

```cpp
virtual int getRenderElapse() = 0;
```


Gets the time taken in custom rendering.

**Notes**

Gets the time taken in custom rendering and report. You need to calculate the average rendering time by yourself.

<span id="IVideoSink-release"></span>
### release

```cpp
virtual void release() {
    }
```


Releases the renderer.

**Notes**

Used to notify the user that the renderer is about to be deprecated. Resources can be released upon receipt of this notification.

<span id="VideoPixelFormat"></span>
# VideoPixelFormat

```cpp
enum bytertc::VideoPixelFormat
```


video frame pixel format

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


<span id="VideoDecoderConfig"></span>
# VideoDecoderConfig

```cpp
enum bytertc::VideoDecoderConfig
```


Video decoding method

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoDecoderConfigRaw |0 |Enable SDK internal decoding, only returns the decoded data via callback |
|kVideoDecoderConfigEncode |1 |Turn on custom decoding, only callback the data before decoding |
|kVideoDecoderConfigBoth |2 |Enable SDK internal decoding, and call back the data before and after decoding at the same time |


<span id="MediaPlayerCustomSourceSeekWhence"></span>
# MediaPlayerCustomSourceSeekWhence

```cpp
enum bytertc::MediaPlayerCustomSourceSeekWhence
```


The starting position where audio data seeking begins.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaPlayerCustomSourceSeekWhenceSet |0 |Seeks from the head of the audio data, and the actual data offset after seeking is offset. |
|kMediaPlayerCustomSourceSeekWhenceCur |1 |Seeks from a specific position of the audio data stream, and the actual data offset after seeking is the current position plus offset. |
|kMediaPlayerCustomSourceSeekWhenceEnd |2 |Seeks from the end of the audio data, and the actual data offset after seeking is the whole data length plus offset. |
|kMediaPlayerCustomSourceSeekWhenceSize |3 |Returns the size of audio data. |


<span id="ForwardStreamEventInfo"></span>
# ForwardStreamEventInfo

```cpp
struct bytertc::ForwardStreamEventInfo
```


Event from each room during relaying

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamEventInfo-room_id) |
|ForwardStreamEvent |[event](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamEventInfo-event) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamEventInfo-room_id"></span>
### room_id

```cpp
const char* bytertc::ForwardStreamEventInfo::room_id
```


ID of the room where the media stream aims to relay to

An Empty string is for all rooms.

<span id="ForwardStreamEventInfo-event"></span>
### event

```cpp
ForwardStreamEvent bytertc::ForwardStreamEventInfo::event
```


Event from the room during relaying. Refer to [ForwardStreamEvent](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamEvent) for more information.

<span id="SubscribeFallbackOption"></span>
# SubscribeFallbackOption

```cpp
enum bytertc::SubscribeFallbackOption
```


Stream fallback options of subscriber

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSubscribeFallbackOptionDisable |0 |Default setting. No fallback is allowed under limited network conditions. |
|kSubscribeFallbackOptionVideoStreamLow |1 |The resolution of currently subscribed video stream will be reduced under limited network conditions, see [Stream Fallback](https://docs.byteplus.com/en/docs/12/docs-70137) for details.<br><br>You can only select this setting after the stream publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalsimulcastmode-2) to enable the mode of publishing multiple streams, otherwise no fallback will occur. |
|kSubscribeFallbackOptionAudioOnly |2 |The resolution of currently subscribed video stream will be reduced first under limited network conditions. When the network condition is not sufficient to receive the minimum resolution stream, the video is automatically cancelled and only the audio is received.<br><br>You can only select this setting after the stream publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalsimulcastmode-2) to enable the mode of publishing multiple streams, otherwise no fallback will occur. |


<span id="LocalAudioStats"></span>
# LocalAudioStats

```cpp
struct bytertc::LocalAudioStats
```


Local audio stream statistics, reference period 2s.

After the local user publishes the audio stream successfully, the SDK will periodically notify the user through `onLocalStreamStats`

The transmission status of the published audio stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[audio_loss_rate](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-audio_loss_rate) |
|int |[send_kbitrate](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-send_kbitrate) |
|int |[record_sample_rate](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-record_sample_rate) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-stats_interval) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-rtt) |
|int |[num_channels](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-num_channels) |
|int |[sent_sample_rate](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-sent_sample_rate) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-jitter) |
|int |[audio_device_loop_delay](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-audio_device_loop_delay) |
|double |[encode_frame_rate](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats-encode_frame_rate) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioStats-audio_loss_rate"></span>
### audio_loss_rate

```cpp
float bytertc::LocalAudioStats::audio_loss_rate
```


Audio packet loss rate, i.e., the audio uplink packet loss rate in this reference period. The value range is [0,1].

<span id="LocalAudioStats-send_kbitrate"></span>
### send_kbitrate

```cpp
int bytertc::LocalAudioStats::send_kbitrate
```


Send rate, i.e., the audio transmission rate in the reference period is kbps.

<span id="LocalAudioStats-record_sample_rate"></span>
### record_sample_rate

```cpp
int bytertc::LocalAudioStats::record_sample_rate
```


Acquisition sampling rate. Audio sampling rate information collected in the reference period, in units of Hz.

<span id="LocalAudioStats-stats_interval"></span>
### stats_interval

```cpp
int bytertc::LocalAudioStats::stats_interval
```


Statistical interval. The interval of this reference period is in ms.

This field is used to set the reference period for the callback. The default setting is 2s.

<span id="LocalAudioStats-rtt"></span>
### rtt

```cpp
int bytertc::LocalAudioStats::rtt
```


Round\-trip time. The unit is ms.

<span id="LocalAudioStats-num_channels"></span>
### num_channels

```cpp
int bytertc::LocalAudioStats::num_channels
```


Number of audio channels.

<span id="LocalAudioStats-sent_sample_rate"></span>
### sent_sample_rate

```cpp
int bytertc::LocalAudioStats::sent_sample_rate
```


Audio transmission sampling rate. Audio transmission sampling rate information in the reference period, in Hz.

<span id="LocalAudioStats-jitter"></span>
### jitter

```cpp
int bytertc::LocalAudioStats::jitter
```


Audio uplink network jitter in ms.

<span id="LocalAudioStats-audio_device_loop_delay"></span>
### audio_device_loop_delay

```cpp
int bytertc::LocalAudioStats::audio_device_loop_delay
```


Audio device record and playout delay in ms.

<span id="LocalAudioStats-encode_frame_rate"></span>
### encode_frame_rate

```cpp
double bytertc::LocalAudioStats::encode_frame_rate
```


Audio encode frame rate.

<span id="IAudioFrame"></span>
# IAudioFrame

```cpp
class bytertc::IAudioFrame
```


Audio frame

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int64_t |[timestampUs](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-timestampus) |
|virtual AudioSampleRate |[sampleRate](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-samplerate) |
|virtual AudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-channel) |
|virtual uint8_t\* |[data](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-data) |
|virtual int |[dataSize](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-datasize) |
|virtual AudioFrameType |[frameType](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-frametype) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-release) |
|virtual bool |[isMutedData](https://docs.byteplus.com/en/docs/12/14187#IAudioFrame-ismuteddata) |


<span id="instructions"></span>
## Instructions

<span id="IAudioFrame-timestampus"></span>
### timestampUs

```cpp
virtual int64_t timestampUs() const = 0;
```


Gets audio frame timestamp.

**Return Value**

Audio frame timestamp in microseconds

<span id="IAudioFrame-samplerate"></span>
### sampleRate

```cpp
virtual AudioSampleRate sampleRate() const = 0;
```


Gets audio sample rate. See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/14187#AudioSampleRate)

**Return Value**

Audio sample rate in Hz

<span id="IAudioFrame-channel"></span>
### channel

```cpp
virtual AudioChannel channel() const = 0;
```


Gets the number of audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/14187#AudioChannel)

**Return Value**

Number of audio channels

**Notes**

For dual channels, the audio frames are interleaved.

<span id="IAudioFrame-data"></span>
### data

```cpp
virtual uint8_t* data() const = 0;
```


Gets audio frame memory address

**Return Value**

Audio frame memory address

<span id="IAudioFrame-datasize"></span>
### dataSize

```cpp
virtual int dataSize() const = 0;
```


Getd audio frame data size

**Return Value**

Audio frame data size in bytes.

<span id="IAudioFrame-frametype"></span>
### frameType

```cpp
virtual AudioFrameType frameType() const = 0;
```


Gets audio frame type

**Return Value**

Audio frame type, support PCM only. See [AudioFrameType](https://docs.byteplus.com/en/docs/12/14187#AudioFrameType)

<span id="IAudioFrame-release"></span>
### release

```cpp
virtual void release() = 0;
```


Release audio frames

<span id="IAudioFrame-ismuteddata"></span>
### isMutedData

```cpp
virtual bool isMutedData() const = 0;
protected:
```


Gets audio mute state identifier

**Return Value**

Is the data muted:


* true: Yes

* false: No

    &nbsp;


<span id="remotevideoconfig"></span>
# RemoteVideoConfig

```cpp
struct bytertc::RemoteVideoConfig
```


Information on remote video frame

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[framerate](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoConfig-framerate) |
|int |[resolution_width](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoConfig-resolution_width) |
|int |[resolution_height](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoConfig-resolution_height) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoConfig-framerate"></span>
### framerate

```cpp
int bytertc::RemoteVideoConfig::framerate = 0
```


Expected maximum frame rate of the subscribed stream in fps. The default value is 0, which represents full\-frame\-rate, values greater than 0 are valid.

If the frame rate of the stream published is higher than the value set by the subscriber, the subscriber receives the video of the frame rate set by this API; if the frame rate of the stream published is lower than the value set by the subscriber, the subscriber receives the video of the same frame rate of the video published.

Only valid if the stream is coded with SVC technique.

<span id="RemoteVideoConfig-resolution_width"></span>
### resolution_width

```cpp
int bytertc::RemoteVideoConfig::resolution_width = 0
```


Width of the video frame in px

<span id="RemoteVideoConfig-resolution_height"></span>
### resolution_height

```cpp
int bytertc::RemoteVideoConfig::resolution_height = 0
```


Height of the video frame in px

<span id="AudioRecordingConfig"></span>
# AudioRecordingConfig

```cpp
struct bytertc::AudioRecordingConfig
```


Audio recording config

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[absolute_file_name](https://docs.byteplus.com/en/docs/12/14187#AudioRecordingConfig-absolute_file_name) |
|AudioFrameSource |[frame_source](https://docs.byteplus.com/en/docs/12/14187#AudioRecordingConfig-frame_source) |
|AudioSampleRate |[sample_rate](https://docs.byteplus.com/en/docs/12/14187#AudioRecordingConfig-sample_rate) |
|AudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14187#AudioRecordingConfig-channel) |
|AudioQuality |[quality](https://docs.byteplus.com/en/docs/12/14187#AudioRecordingConfig-quality) |


<span id="instructions"></span>
## Instructions

<span id="AudioRecordingConfig-absolute_file_name"></span>
### absolute_file_name

```cpp
const char* bytertc::AudioRecordingConfig::absolute_file_name
```


Absolute path of the recorded file, file name included. The App must have the write and read permission of the path.

The files format is restricted to .aac and .wav.

<span id="AudioRecordingConfig-frame_source"></span>
### frame_source

```cpp
AudioFrameSource bytertc::AudioRecordingConfig::frame_source
```


The source of the recording. See [AudioFrameSource](https://docs.byteplus.com/en/docs/12/14187#AudioFrameSource).

It is kAudioFrameSourceMixed = 2, by default.

<span id="AudioRecordingConfig-sample_rate"></span>
### sample_rate

```cpp
AudioSampleRate bytertc::AudioRecordingConfig::sample_rate
```


See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/14187#AudioSampleRate).

<span id="AudioRecordingConfig-channel"></span>
### channel

```cpp
AudioChannel bytertc::AudioRecordingConfig::channel
```


Number of audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/14187#AudioChannel).

If number of audio channels of recording is different than that of audio capture, the behavior is:


* If the number of capture is 1, and the number of recording is 2, the recorded audio is two\-channel data after copying mono\-channel data.

* If the number of capture is 2, and the number of recording is 1, the recorded audio is recorded by mixing the audio of the two channels.

    &nbsp;


<span id="quality"></span>
### quality

```cpp
AudioQuality bytertc::AudioRecordingConfig::quality
```


Recording quality. Only valid for .aac file. See [AudioQuality](https://docs.byteplus.com/en/docs/12/14187#AudioQuality).

When the sample rate is 32kHz, the file (10min) size for different qualities are:

```Plain Text
   - low: 1.2MB;
   - [By Default] medium: 2MB;
   - high: 3.75MB;
   - ultra high: 7.5MB.
```


<span id="HWDeviceContextKey"></span>
# HWDeviceContextKey

```cpp
enum bytertc::HWDeviceContextKey
```


Hardware encoding device context

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kHWDeviceContextKeyCudaContext |0 |cuda context |
|kHWDeviceContextKeyD3D11Device |1 |Direct3D11 device |
|kHWDeviceContextKeyD3D11DeviceContext |2 |Direct3D11 device context |
|kHWDeviceContextKeyEglContext |3 |Egl device context |
|kHWDeviceContextKeyVADisplay |4 |Vadisplay device context |


<span id="CloudProxyInfo"></span>
# CloudProxyInfo

```cpp
struct bytertc::CloudProxyInfo
```


Cloud Proxy Information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[cloud_proxy_ip](https://docs.byteplus.com/en/docs/12/14187#CloudProxyInfo-cloud_proxy_ip) |
|int |[cloud_proxy_port](https://docs.byteplus.com/en/docs/12/14187#CloudProxyInfo-cloud_proxy_port) |


<span id="instructions"></span>
## Instructions

<span id="CloudProxyInfo-cloud_proxy_ip"></span>
### cloud_proxy_ip

```cpp
const char* bytertc::CloudProxyInfo::cloud_proxy_ip
```


Cloud proxy IP

<span id="CloudProxyInfo-cloud_proxy_port"></span>
### cloud_proxy_port

```cpp
int bytertc::CloudProxyInfo::cloud_proxy_port
```


Cloud Proxy Port

<span id="LocalProxyConfiguration"></span>
# LocalProxyConfiguration

```cpp
struct bytertc::LocalProxyConfiguration
```


Detailed information of local proxy configurations.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|LocalProxyType |[local_proxy_type](https://docs.byteplus.com/en/docs/12/14187#LocalProxyConfiguration-local_proxy_type) |
|const char\* |[local_proxy_ip](https://docs.byteplus.com/en/docs/12/14187#LocalProxyConfiguration-local_proxy_ip) |
|int |[local_proxy_port](https://docs.byteplus.com/en/docs/12/14187#LocalProxyConfiguration-local_proxy_port) |
|const char\* |[local_proxy_username](https://docs.byteplus.com/en/docs/12/14187#LocalProxyConfiguration-local_proxy_username) |
|const char\* |[local_proxy_password](https://docs.byteplus.com/en/docs/12/14187#LocalProxyConfiguration-local_proxy_password) |


<span id="instructions"></span>
## Instructions

<span id="LocalProxyConfiguration-local_proxy_type"></span>
### local_proxy_type

```cpp
LocalProxyType bytertc::LocalProxyConfiguration::local_proxy_type
```


Types of local proxies. Refer to [LocalProxyType](https://docs.byteplus.com/en/docs/12/14187#LocalProxyType) for details.

<span id="LocalProxyConfiguration-local_proxy_ip"></span>
### local_proxy_ip

```cpp
const char* bytertc::LocalProxyConfiguration::local_proxy_ip
```


Local proxy IP.

<span id="LocalProxyConfiguration-local_proxy_port"></span>
### local_proxy_port

```cpp
int bytertc::LocalProxyConfiguration::local_proxy_port
```


Local proxy port.

<span id="LocalProxyConfiguration-local_proxy_username"></span>
### local_proxy_username

```cpp
const char* bytertc::LocalProxyConfiguration::local_proxy_username
```


The username of the local proxy.

<span id="LocalProxyConfiguration-local_proxy_password"></span>
### local_proxy_password

```cpp
const char* bytertc::LocalProxyConfiguration::local_proxy_password
```


The password of the local proxy.

<span id="RemoteVideoStateChangeReason"></span>
# RemoteVideoStateChangeReason

```cpp
enum bytertc::RemoteVideoStateChangeReason
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
|kRemoteVideoStateChangeReasonRemoteOffline |7 |The remote user leaves the room. |


<span id="ScreenCaptureSourceInfo"></span>
# ScreenCaptureSourceInfo

```cpp
struct bytertc::ScreenCaptureSourceInfo
```


Detailed information of the screen sharing object

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ScreenCaptureSourceType |[type](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceInfo-type) |
|view_t |[source_id](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceInfo-source_id) |
|const char\* |[source_name](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceInfo-source_name) |
|const char\* |[application](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceInfo-application) |
|int |[pid](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceInfo-pid) |
|bool |[primary_monitor](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceInfo-primary_monitor) |
|Rectangle |[region_rect](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceInfo-region_rect) |


<span id="instructions"></span>
## Instructions

<span id="ScreenCaptureSourceInfo-type"></span>
### type

```cpp
ScreenCaptureSourceType bytertc::ScreenCaptureSourceInfo::type = kScreenCaptureSourceTypeUnknown
```


Type of the screen\-sharing object. Refer to [ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/14187#ScreenCaptureSourceType) for the type of shared object.

<span id="ScreenCaptureSourceInfo-source_id"></span>
### source_id

```cpp
view_t bytertc::ScreenCaptureSourceInfo::source_id = nullptr
```


ID of the screen\-sharing object

<span id="ScreenCaptureSourceInfo-source_name"></span>
### source_name

```cpp
const char* bytertc::ScreenCaptureSourceInfo::source_name = nullptr
```


Name of the screen\-sharing object

Make sure you have saved them as `string` objects before calling [release](https://docs.byteplus.com/en/docs/12/docs-70095#IScreenCaptureSourceList-release) to release the dynamic memory.

<span id="ScreenCaptureSourceInfo-application"></span>
### application

```cpp
const char* bytertc::ScreenCaptureSourceInfo::application = nullptr
```


The title of the application to be shared.

Only available if the sharing object is an application window.

Make sure you have saved them as `string` objects before calling [release](https://docs.byteplus.com/en/docs/12/docs-70095#IScreenCaptureSourceList-release) to release the dynamic memory.

<span id="ScreenCaptureSourceInfo-pid"></span>
### pid

```cpp
int bytertc::ScreenCaptureSourceInfo::pid = 0
```


Process pid of the application to be shared.

Only available if the sharing object is an application window.

<span id="ScreenCaptureSourceInfo-primary_monitor"></span>
### primary_monitor

```cpp
bool bytertc::ScreenCaptureSourceInfo::primary_monitor = false
```


Tag for the screen to be shared identifying whether it is the primary screen

Only available when the screen\-sharing object is a screen.

<span id="ScreenCaptureSourceInfo-region_rect"></span>
### region_rect

```cpp
Rectangle bytertc::ScreenCaptureSourceInfo::region_rect
```


Coordinates of the screen\-sharing object. See [Rectangle](https://docs.byteplus.com/en/docs/12/14187#Rectangle).

Valid only when the capture source is the monitor screen.


* When there are several screens, the origin (0, 0) is different for different platforms:

   * For Windows, the origin (0, 0) is the top\-left corner of the main screen.

   * For Linux, the origin (0, 0) is the top\-left corner of the rectangle that merely covers all screens.

* The region of the window is different for different platforms:

   * For Windows and macOS, the region includes the system title bar of the window.

   * For Linux, the region does not include the system title bar of the window.

       &nbsp;


<span id="recordingstate"></span>
# RecordingState

```cpp
enum bytertc::RecordingState
```


Status of local recording

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRecordingStateError |0 |Recording exception |
|kRecordingStateProcessing |1 |Recording in progress |
|kRecordingStateSuccess |2 |If the recording file is saved successfully. Normal call to stopFileRecording triggers this status code. If the encoding resolution changes during the recording, the SDK will automatically end the current file save and trigger this status code, followed by a new round of recording, until stopFileRecording is called. |


<span id="AudioSampleRate"></span>
# AudioSampleRate

```cpp
enum bytertc::AudioSampleRate
```


Audio sample rate in Hz.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioSampleRateAuto |\-1 |Default value. 48000Hz. |
|kAudioSampleRate8000 |8000 |8000Hz |
|kAudioSampleRate11025 |11025 |11025Hz |
|kAudioSampleRate16000 |16000 |16000Hz |
|kAudioSampleRate22050 |22050 |22050Hz |
|kAudioSampleRate24000 |24000 |24000Hz |
|kAudioSampleRate32000 |32000 |32000Hz |
|kAudioSampleRate44100 |44100 |44100Hz |
|kAudioSampleRate48000 |48000 |48000Hz |


<span id="SourceCrop"></span>
# SourceCrop

```cpp
struct bytertc::SourceCrop
```


Configurations on how to crop the WTN stream

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[location_x](https://docs.byteplus.com/en/docs/12/14187#SourceCrop-location_x) |
|float |[location_y](https://docs.byteplus.com/en/docs/12/14187#SourceCrop-location_y) |
|float |[width_proportion](https://docs.byteplus.com/en/docs/12/14187#SourceCrop-width_proportion) |
|float |[height_proportion](https://docs.byteplus.com/en/docs/12/14187#SourceCrop-height_proportion) |


<span id="instructions"></span>
## Instructions

<span id="SourceCrop-location_x"></span>
### location_x

```cpp
float bytertc::SourceCrop::location_x = 0.0
```


The normalized horizontal coordinate value of the top left vertex of the cropped image to width of the original image, ranging within [0.0, 1.0).

Default value is 0.0.

<span id="SourceCrop-location_y"></span>
### location_y

```cpp
float bytertc::SourceCrop::location_y = 0.0
```


The normalized vertical coordinate value of the top left vertex of the cropped image to height of the original image, ranging within [0.0, 1.0).

Default value is 0.0.

<span id="SourceCrop-width_proportion"></span>
### width_proportion

```cpp
float bytertc::SourceCrop::width_proportion = 1.0
```


The normalized ratio of the width of the cropped image to that of the original image, ranging within [0.0, 1.0).

Default value is 1.0.

<span id="SourceCrop-height_proportion"></span>
### height_proportion

```cpp
float bytertc::SourceCrop::height_proportion = 1.0
```


The normalized ratio of the height of the cropped image to that of the original image, ranging within [0.0, 1.0).

Default value is 1.0.

<span id="EchoTestConfig"></span>
# EchoTestConfig

```cpp
struct bytertc::EchoTestConfig
```


Video/audio call test configurations

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|void\* |[view](https://docs.byteplus.com/en/docs/12/14187#EchoTestConfig-view) |
|bool |[enable_audio](https://docs.byteplus.com/en/docs/12/14187#EchoTestConfig-enable_audio) |
|bool |[enable_video](https://docs.byteplus.com/en/docs/12/14187#EchoTestConfig-enable_video) |
|int |[audio_properties_report_interval](https://docs.byteplus.com/en/docs/12/14187#EchoTestConfig-audio_properties_report_interval) |
|const char\* |[uid](https://docs.byteplus.com/en/docs/12/14187#EchoTestConfig-uid) |
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#EchoTestConfig-room_id) |
|const char\* |[token](https://docs.byteplus.com/en/docs/12/14187#EchoTestConfig-token) |


<span id="instructions"></span>
## Instructions

<span id="EchoTestConfig-view"></span>
### view

```cpp
void* bytertc::EchoTestConfig::view
```


View for rendering received video

<span id="EchoTestConfig-enable_audio"></span>
### enable_audio

```cpp
bool bytertc::EchoTestConfig::enable_audio
```


Whether to test audio. The device to be tested is the default audio device.


* true: Yes

   * If you use internal capture, the device microphone will automatically turn on and `onLocalAudioPropertiesReport` will be triggered when the value of audioPropertiesReportInterval is set to greater than 0, from which you can judge the working status of the microphone.

   * If you choose custom capture, you also need to call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushexternalaudioframe) to push the captured audio to the SDK.

* false: No

    &nbsp;


<span id="enable-video"></span>
### enable_video

```cpp
bool bytertc::EchoTestConfig::enable_video
```


Whether to test video. If you are using a desktop PC, the device to be tested is by default the first video device in the list.


* true: Yes

   * If you use internal capture, the device camera will automatically turn on.

   * If you choose custom capture, you also need to call [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushexternalvideoframe) to push the captured video to the SDK.

* false: No


**Notes**

The video is published with fixed parameters: resolution 640px × 360px, frame rate 15fps.

<span id="EchoTestConfig-audio_properties_report_interval"></span>
### audio_properties_report_interval

```cpp
int bytertc::EchoTestConfig::audio_properties_report_interval
```


Volume prompt interval in ms, the default value is 100.


* `<= 0`: Turn off prompt

* `(0,100]` Invalid interval value, and will be automatically reset to 100ms.

* `> 100`: the actual value of interval

    &nbsp;


<span id="uid"></span>
### uid

```cpp
const char* bytertc::EchoTestConfig::uid
```


User ID for testing

<span id="EchoTestConfig-room_id"></span>
### room_id

```cpp
const char* bytertc::EchoTestConfig::room_id
```


ID of the room that the tested user will join.

<span id="EchoTestConfig-token"></span>
### token

```cpp
const char* bytertc::EchoTestConfig::token
```


Token used for authenticating users when they enter the room.

<span id="NetworkDetectionLinkType"></span>
# NetworkDetectionLinkType

```cpp
enum bytertc::NetworkDetectionLinkType
```


The type of probe link before the call.

`onNetworkDetectionResult` The parameter type for the callback

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kNetworkDetectionLinkTypeUp |0 |Uplink network sounding |
|kNetworkDetectionLinkTypeDown |1 |Downlink network detection |


<span id="MediaStreamType"></span>
# MediaStreamType

```cpp
enum bytertc::MediaStreamType
```


Media stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaStreamTypeAudio |1 << 0 |Controls audio only |
|kMediaStreamTypeVideo |1 << 1 |Controls video only |
|kMediaStreamTypeBoth |kMediaStreamTypeAudio \| kMediaStreamTypeVideo |Controls both audio and video |


<span id="LocalProxyError"></span>
# LocalProxyError

```cpp
enum bytertc::LocalProxyError
```


The errors of local proxy connection.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalProxyErrorOK |0 |There are no errors in local proxies. |
|kLocalProxyErrorSocks5VersionError |1 |The connection to Socks5 proxy failed because the proxy server replies wrong version numbers which don't accord with the Socks5 document. Please check the proxy server. |
|kLocalProxyErrorSocks5FormatError |2 |The connection to Socks5 proxy failed because the format of the proxy's replies does not accord with the Socks5 document. Please check the proxy server. |
|kLocalProxyErrorSocks5InvalidValue |3 |The connection to Socks5 proxy failed because the proxy replies wrong information which does not accord with the Socks5 document. Please check the proxy server. |
|kLocalProxyErrorSocks5UserPassNotGiven |4 |The connection to Socks5 proxy failed because the username and password of the local proxy are not provided. Please call `setLocalProxy` and enter your username and password. |
|kLocalProxyErrorSocks5TcpClosed |5 |The connection to Socks5 proxy failed because TCP is closed. Please check the proxy server and your network connection status. |
|kLocalProxyErrorHttpTunnelFailed |6 |Errors in Http tunnel proxy. Please check Http tunnel proxy and your network connection status. |


<span id="AudioFrameType"></span>
# AudioFrameType

```cpp
enum bytertc::AudioFrameType
```


Audio frame type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioFrameTypePCM16 |0 |PCM 16bit |


<span id="ForwardStreamEvent"></span>
# ForwardStreamEvent

```cpp
enum bytertc::ForwardStreamEvent
```


Events during the relaying

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kForwardStreamEventDisconnected |0 |Relaying pauses for the reason of network disconnecting. |
|kForwardStreamEventConnected |1 |Relaying recovers from the disconnecting. |
|kForwardStreamEventInterrupt |2 |Relaying aborts because a user with the same user ID as that of the publisher joins. |
|kForwardStreamEventDstRoomUpdated |3 |Target room list updates after you call `updateForwardStreamToRooms`. |
|kForwardStreamEventUnExpectAPICall |4 |Wrong API\-calling order. For example, call `updateForwardStreamToRooms` before calling `startForwardStreamToRooms`. |


<span id="AudioAbilityType"></span>
# AudioAbilityType

```cpp
enum bytertc::AudioAbilityType
```


Accessibility to volume setting

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioAbilityTypeUnknown |\-1 |Unknown |
|kAudioAbilityTypeAble |0 |The volume setting is accessible. |
|kAudioAbilityTypeUnable |1 |The volume setting is inaccessible. |


<span id="MixedStreamAudioConfig"></span>
# MixedStreamAudioConfig

```cpp
struct bytertc::MixedStreamAudioConfig
```


Audio mix stream configurations.

With invalid or empty input, the configurations will be set as the default values.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int32_t |[sample_rate](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioConfig-sample_rate) |
|int32_t |[channels](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioConfig-channels) |
|int32_t |[bitrate](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioConfig-bitrate) |
|MixedStreamAudioProfile |[audio_profile](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioConfig-audio_profile) |
|MixedStreamAudioCodecType |[audio_codec](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioConfig-audio_codec) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamAudioConfig-sample_rate"></span>
### sample_rate

```cpp
int32_t bytertc::MixedStreamAudioConfig::sample_rate = 48000
```


The sample rate (Hz). Supported sample rates: 32,000 Hz, 44,100 Hz, 48,000 Hz. Defaults to 48,000 Hz. It's recommended to be set.

<span id="MixedStreamAudioConfig-channels"></span>
### channels

```cpp
int32_t bytertc::MixedStreamAudioConfig::channels = 2
```


The number of channels. Supported channels: 1 (single channel), 2 (dual channel). Defaults to 2. It's recommended to be set.

<span id="MixedStreamAudioConfig-bitrate"></span>
### bitrate

```cpp
int32_t bytertc::MixedStreamAudioConfig::bitrate = 64
```


The bitrate (Kbps) in the range of [32, 192]. Defaults to 64 Kbps. It's recommended to be set.

<span id="MixedStreamAudioConfig-audio_profile"></span>
### audio_profile

```cpp
MixedStreamAudioProfile bytertc::MixedStreamAudioConfig::audio_profile = MixedStreamAudioProfile::kMixedStreamAudioProfileLC
```


AAC profile. See [MixedStreamAudioProfile](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioProfile). It defaults to `0`, indicating AAC\-LC.

<span id="MixedStreamAudioConfig-audio_codec"></span>
### audio_codec

```cpp
MixedStreamAudioCodecType bytertc::MixedStreamAudioConfig::audio_codec = MixedStreamAudioCodecType::kMixedStreamAudioCodecTypeAAC
```


AAC profile. See [MixedStreamAudioCodecType](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioCodecType). Currently, the only value `0` indicates AAC.

This parameter is not supported for WTN stream tasks.

<span id="SetRoomExtraInfoResult"></span>
# SetRoomExtraInfoResult

```cpp
enum bytertc::SetRoomExtraInfoResult
```


Extra information setting result.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSetRoomExtraInfoResultSuccess |0 |Success. |
|kSetRoomExtraInfoResultErrorNotJoinRoom |\-1 |Failure. You are not in the room. |
|kSetRoomExtraInfoResultErrorKeyIsNull |\-2 |Failure. The key pointer is null. |
|kSetRoomExtraInfoResultErrorValueIsNull |\-3 |Failure. The value pointer is null. |
|kSetRoomExtraInfoResultResultUnknow |\-99 |Failure. Unknown error. |
|kSetRoomExtraInfoResultErrorKeyIsEmpty |\-400 |Failure. The key length is 0. |
|kSetRoomExtraInfoResultErrorTooOften |\-406 |Failure. Excessively frequent setting. 10 times per second is preferable. |
|kSetRoomExtraInfoResultErrorSilentUser |\-412 |Failure. Invisible users are not allowed to call `setRoomExtraInfo`. |
|kSetRoomExtraInfoResultErrorKeyTooLong |\-413 |Failure. Key length exceeds 10 bytes. |
|kSetRoomExtraInfoResultErrorValueTooLong |\-414 |Failure. Value length exceeds 128 bytes. |
|kSetRoomExtraInfoResultErrorServer |\-500 |Failure. Server error. |


<span id="VideoCanvas"></span>
# VideoCanvas

```cpp
struct bytertc::VideoCanvas
```


Video rendering configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|void\* |[view](https://docs.byteplus.com/en/docs/12/14187#VideoCanvas-view) |
|int |[render_mode](https://docs.byteplus.com/en/docs/12/14187#VideoCanvas-render_mode) |
|uint32_t |[background_color](https://docs.byteplus.com/en/docs/12/14187#VideoCanvas-background_color) |
|RenderTargetType |[render_target_type](https://docs.byteplus.com/en/docs/12/14187#VideoCanvas-render_target_type) |
|VideoRotation |[render_rotation](https://docs.byteplus.com/en/docs/12/14187#VideoCanvas-render_rotation) |


<span id="instructions"></span>
## Instructions

<span id="VideoCanvas-view"></span>
### view

```cpp
void* bytertc::VideoCanvas::view = NULL
```


Local view handle

<span id="VideoCanvas-render_mode"></span>
### render_mode

```cpp
int bytertc::VideoCanvas::render_mode = kRenderModeHidden
```


Video rendering mode. See [RenderMode](https://docs.byteplus.com/en/docs/12/14187#RenderMode)

<span id="VideoCanvas-background_color"></span>
### background_color

```cpp
uint32_t bytertc::VideoCanvas::background_color = 0
```


Set the background color of the canvas which is not filled with video frame. The range is `[0x00000000, 0xFFFFFFFF]`. The default is `0x00000000`. The Alpha index is ignored.

<span id="VideoCanvas-render_target_type"></span>
### render_target_type

```cpp
RenderTargetType bytertc::VideoCanvas::render_target_type = kRenderTargetTypeView
```


See [RenderTargetType](https://docs.byteplus.com/en/docs/12/14187#RenderTargetType).

<span id="VideoCanvas-render_rotation"></span>
### render_rotation

```cpp
VideoRotation bytertc::VideoCanvas::render_rotation = kVideoRotation0
```


Video frame rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14187#VideoRotation). The default value is 0, which means no rotation is applied.

This parameter only applies to remote video and does not affect local video settings.

<span id="LogConfig"></span>
# LogConfig

```cpp
struct bytertc::LogConfig
```


Local log parameters.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[log_path](https://docs.byteplus.com/en/docs/12/14187#LogConfig-log_path) |
|LocalLogLevel |[log_level](https://docs.byteplus.com/en/docs/12/14187#LogConfig-log_level) |
|uint32_t |[log_file_size](https://docs.byteplus.com/en/docs/12/14187#LogConfig-log_file_size) |
|const char\* |[log_filename_prefix](https://docs.byteplus.com/en/docs/12/14187#LogConfig-log_filename_prefix) |


<span id="instructions"></span>
## Instructions

<span id="LogConfig-log_path"></span>
### log_path

```cpp
const char* bytertc::LogConfig::log_path = nullptr
```


(Required) Local log directory.

<span id="LogConfig-log_level"></span>
### log_level

```cpp
LocalLogLevel bytertc::LogConfig::log_level = LocalLogLevel::kWarning
```


(Optional) The logging level. See [LocalLogLevel](https://docs.byteplus.com/en/docs/12/14187#LocalLogLevel). The default is warning level.

<span id="LogConfig-log_file_size"></span>
### log_file_size

```cpp
uint32_t bytertc::LogConfig::log_file_size = 10
```


(Optional) The limits for total log file size in MB. The range is 1 to 100 MB, and the default value is 10 MB.

If `log_file_size` < 1, it will be set to 1 MB. If `log_file_size` \> 100, it will be set to 100 MB.

The maximum size for a single log file is 2 MB.

If 1 ≤ `log_file_size` ≤ 2, one log file will be generated. If `log_file_size` \> 2, the first `⌊log_file_size/2⌋` files will be filled with 2 MB each, the `⌊log_file_size/2⌋+1` file will be filled with `log_file_size mod 2`.

If the size exceeds the remaining space, the oldest file will be deleted.

<span id="LogConfig-log_filename_prefix"></span>
### log_filename_prefix

```cpp
const char* bytertc::LogConfig::log_filename_prefix = nullptr
```


(Optional) Local log file name prefix. It should follow the regular expression pattern of `[a-zA-Z0-9_\@-.]{1,128}`.

The final file name will be the prefix followed by "_" and the file creation time, and "_rtclog.log" at the end. For example, `logPrefix_2023-05-25_172324_rtclog.log`.

<span id="RemoteMirrorType"></span>
# RemoteMirrorType

```cpp
enum bytertc::RemoteMirrorType
```


Mirroring type for remote stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteMirrorTypeNone |0 |(Default) Disable mirroring effect for remote streams. |
|kRemoteMirrorTypeRender |1 |Enable mirroring effect for remote streams. |


<span id="SEIStreamEventType"></span>
# SEIStreamEventType

```cpp
enum bytertc::SEIStreamEventType
```


State of the black frame video stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSEIStreamEventTypeStreamAdd |0 |A black frame video stream is published from the remote user.<br><br>In a voice call, when the remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendseimessage) to send SEI data, SDK will automatically publish a black frame video stream, and trigger this callback. |
|kSEIStreamEventTypeStreamRemove |1 |The black frame video stream is removed. The timing this callback will be triggered is as following:<br><br><br>&nbsp;<br><br>* The black frame video stream stops when the remote user turns on their camera, switching from a voice call to a video call.<br><br>* No SEI data is sent within 1min after the remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendseimessage).<br><br>* The remote user calls [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideosourcetype) to switch to custom video capture. |


<span id="VideoApplyRotation"></span>
# VideoApplyRotation

```cpp
enum bytertc::VideoApplyRotation
```


Whether the video frame needs to be automatically rotated.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoApplyRotationDefault |\-1 |(Default) No rotation. |
|kVideoApplyRotation0 |0 |Automatic rotation, which rotates video frames to 0 degreess based on the rotation angle information. |


<span id="VideoPreprocessorConfig"></span>
# VideoPreprocessorConfig

```cpp
struct bytertc::VideoPreprocessorConfig
```


Video preprocessing configuration parameters.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VideoPixelFormat |[required_pixel_format](https://docs.byteplus.com/en/docs/12/14187#VideoPreprocessorConfig-required_pixel_format) |
|ProcessorActionDomain |[action_domain](https://docs.byteplus.com/en/docs/12/14187#VideoPreprocessorConfig-action_domain) |


<span id="instructions"></span>
## Instructions

<span id="VideoPreprocessorConfig-required_pixel_format"></span>
### required_pixel_format

```cpp
VideoPixelFormat bytertc::VideoPreprocessorConfig::required_pixel_format = kVideoPixelFormatUnknown
```


Video frame pixel format. See [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14187#VideoPixelFormat)

Only `kVideoPixelFormatI420` and `kVideoPixelFormatUnknown` are supported.

<span id="VideoPreprocessorConfig-action_domain"></span>
### action_domain

```cpp
ProcessorActionDomain bytertc::VideoPreprocessorConfig::action_domain = kProcessorActionDomainPreviewAndEncode
```


The effective range of the custom video preprocessor. See [ProcessorActionDomain](https://docs.byteplus.com/en/docs/12/14187#ProcessorActionDomain).

<span id="PlayerEvent"></span>
# PlayerEvent

```cpp
enum bytertc::PlayerEvent
```


Player event.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPlayerEventSelectAudioTrackBegin |0 |Beginning to switch audio tracks.<br><br>When calling [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-selectaudiotrack), this state is returned. |
|kPlayerEventSelectAudioTrackCompleted |1 |Switching audio tracks completed.<br><br>After calling [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-selectaudiotrack), this state is returned. |
|kPlayerEventSelectAudioTrackFailed |2 |Switching audio tracks failed.<br><br>After calling [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-selectaudiotrack), this state is returned. |
|kPlayerEventSeekBegin |3 |Beginning to seek.<br><br>When calling [setPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setposition), this state is returned. |
|kPlayerEventSeekCompleted |4 |Seeking completed.<br><br>After calling [setPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setposition), this state is returned. |
|kPlayerEventSeekFailed |5 |Seeking failed.<br><br>After calling [setPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setposition), this state is returned. |


<span id="RTCVideoDeviceType"></span>
# RTCVideoDeviceType

```cpp
enum bytertc::RTCVideoDeviceType
```


Current audio device type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRTCVideoDeviceTypeUnknown |\-1 |Unknown device |
|kRTCVideoDeviceTypeRenderDevice |0 |Video rendering device |
|kRTCVideoDeviceTypeCaptureDevice |1 |Video capture device |
|kRTCVideoDeviceTypeScreenCaptureDevice |2 |Screen recorder |


<span id="NetworkQualityStats"></span>
# NetworkQualityStats

```cpp
struct bytertc::NetworkQualityStats
```


Tx/Rx network quality

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[uid](https://docs.byteplus.com/en/docs/12/14187#NetworkQualityStats-uid) |
|double |[fraction_lost](https://docs.byteplus.com/en/docs/12/14187#NetworkQualityStats-fraction_lost) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/14187#NetworkQualityStats-rtt) |
|int |[total_bandwidth](https://docs.byteplus.com/en/docs/12/14187#NetworkQualityStats-total_bandwidth) |
|NetworkQuality |[tx_quality](https://docs.byteplus.com/en/docs/12/14187#NetworkQualityStats-tx_quality) |
|NetworkQuality |[rx_quality](https://docs.byteplus.com/en/docs/12/14187#NetworkQualityStats-rx_quality) |


<span id="instructions"></span>
## Instructions

<span id="NetworkQualityStats-uid"></span>
### uid

```cpp
const char* bytertc::NetworkQualityStats::uid
```


User ID

<span id="NetworkQualityStats-fraction_lost"></span>
### fraction_lost

```cpp
double bytertc::NetworkQualityStats::fraction_lost
```


Packet loss ratio of the local client, ranging [0.0,1.0]

For a local user, it is the sent\-packet loss ratio.

For a remote user, it is the loss ratio of all the packets received.

<span id="NetworkQualityStats-rtt"></span>
### rtt

```cpp
int bytertc::NetworkQualityStats::rtt
```


Round\-trip time (RTT) from client to server. Effective for the local user. Unit: ms

<span id="NetworkQualityStats-total_bandwidth"></span>
### total_bandwidth

```cpp
int bytertc::NetworkQualityStats::total_bandwidth
```


Average transmission rate of the media RTP packets in 2s. unit: bps

For a local user, it is the packet\-transmitting speed.

For a remote user, it is the speed of receiving all the subscribed media.

<span id="NetworkQualityStats-tx_quality"></span>
### tx_quality

```cpp
NetworkQuality bytertc::NetworkQualityStats::tx_quality
```


Tx network quality grade. Refer to [NetworkQuality](https://docs.byteplus.com/en/docs/12/14187#NetworkQuality) for details.

<span id="NetworkQualityStats-rx_quality"></span>
### rx_quality

```cpp
NetworkQuality bytertc::NetworkQualityStats::rx_quality
```


Rx network quality grade. Refer to [NetworkQuality](https://docs.byteplus.com/en/docs/12/14187#NetworkQuality) for details.

<span id="RemoteVideoRenderConfig"></span>
# RemoteVideoRenderConfig

```cpp
struct bytertc::RemoteVideoRenderConfig
```


Remote video rendering configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|RenderMode |[render_mode](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoRenderConfig-render_mode) |
|uint32_t |[background_color](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoRenderConfig-background_color) |
|VideoRotation |[render_rotation](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoRenderConfig-render_rotation) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoRenderConfig-render_mode"></span>
### render_mode

```cpp
RenderMode bytertc::RemoteVideoRenderConfig::render_mode = kRenderModeHidden
```


Rendering mode.


* 1（`RENDER_MODE_HIDDEN`）Fill and Crop. Default setting. The video frame is scaled with a fixed aspect ratio and completely fills the canvas. The region of the video exceeding the canvas will be cropped.

* 2（`RENDER_MODE_FIT`）Fit. The video frame is scaled with a fixed aspect ratio and is shown completely on the canvas. The region of the canvas not filled with the video frame will be filled with `backgroundColor`.

* 3（`RENDER_MODE_FILL`）Fill the canvas. The video frame is scaled to fill the canvas. During the process, the aspect ratio may change.

    &nbsp;


<span id="background-color"></span>
### background_color

```cpp
uint32_t bytertc::RemoteVideoRenderConfig::background_color = 0
```


Set the background color of the canvas which is not filled with video frame. The range is `[0x00000000, 0xFFFFFFFF]`. The default is `0x00000000`. The Alpha index is ignored.

<span id="RemoteVideoRenderConfig-render_rotation"></span>
### render_rotation

```cpp
VideoRotation bytertc::RemoteVideoRenderConfig::render_rotation = kVideoRotation0
```


User\-defined render rotation. The value must be 0, 90, 180, or 270. 0 means keeping the original canvas orientation, and 90, 180, and 270 represent clockwise rotation angles of the original canvas.

<span id="MixedStreamLayoutRegionConfig"></span>
# MixedStreamLayoutRegionConfig

```cpp
struct bytertc::MixedStreamLayoutRegionConfig
```


Layout information for one of the video streams to be mixed.

After starting to push streams to CDN and mixing multiple video streams, you can set the layout information for each of them.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-user_id) |
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-room_id) |
|int |[location_x](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-location_x) |
|int |[location_y](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-location_y) |
|int |[width](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-height) |
|float |[alpha](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-alpha) |
|float |[corner_radius](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-corner_radius) |
|int32_t |[z_order](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-z_order) |
|bool |[is_local_user](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-is_local_user) |
|MixedStreamVideoType |[stream_type](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-stream_type) |
|MixedStreamMediaType |[media_type](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-media_type) |
|MixedStreamRenderMode |[render_mode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-render_mode) |
|MixedStreamLayoutRegionType |[region_content_type](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-region_content_type) |
|uint8_t\* |[image_water_mark](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-image_water_mark) |
|MixedStreamLayoutRegionImageWaterMarkConfig |[image_water_mark_param](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-image_water_mark_param) |
|MixedStreamAlternateImageFillMode |[alternate_image_fill_mode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-alternate_image_fill_mode) |
|const char\* |[alternate_image_url](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-alternate_image_url) |
|Position |[spatial_position](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-spatial_position) |
|bool |[apply_spatial_audio](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-apply_spatial_audio) |
|SourceCrop |[source_crop](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-source_crop) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamLayoutRegionConfig-user_id"></span>
### user_id

```cpp
const char* bytertc::MixedStreamLayoutRegionConfig::user_id = nullptr
```


The ID of the user who publishes the video stream. It's recommended to be set.

<span id="MixedStreamLayoutRegionConfig-room_id"></span>
### room_id

```cpp
const char* bytertc::MixedStreamLayoutRegionConfig::room_id = nullptr
```


The room ID of the media stream. It's recommended to be set.

If the media stream is the stream forwarded by [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-startforwardstreamtorooms), you must set the roomID to the room ID of the target room.

<span id="MixedStreamLayoutRegionConfig-location_x"></span>
### location_x

```cpp
int bytertc::MixedStreamLayoutRegionConfig::location_x = 0
```


The X\-coordinate in pixels of the upper\-left corner of the user's frame in the entire canvas coordinate system, where the origin is at the upper\-left corner of the canvas. It represents the horizontal displacement of the upper\-left corner of the user's frame relative to the origin.

The value range is [0, the width of the canvas). The default value is 0.

<span id="MixedStreamLayoutRegionConfig-location_y"></span>
### location_y

```cpp
int bytertc::MixedStreamLayoutRegionConfig::location_y = 0
```


The Y\-coordinate in pixels of the upper\-left corner of the user's frame in the entire canvas coordinate system, where the origin is at the upper\-left corner of the canvas. It represents the vertical displacement of the upper\-left corner of the user's frame relative to the origin.

The value range is [0, the height of the canvas). The default value is 0.

<span id="MixedStreamLayoutRegionConfig-width"></span>
### width

```cpp
int bytertc::MixedStreamLayoutRegionConfig::width = MIXED_STREAM_VIDEO_DEFAULT_WIDTH
```


The width of the user's frame in pixels. The value range is [0, the width of the canvas]. The default value is 360.

<span id="MixedStreamLayoutRegionConfig-height"></span>
### height

```cpp
int bytertc::MixedStreamLayoutRegionConfig::height = MIXED_STREAM_DEFAULT_VIDEO_HEIGHT
```


The height of the user's frame in pixels. The value range is [0, the height of the canvas]. The default value is 640.

<span id="MixedStreamLayoutRegionConfig-alpha"></span>
### alpha

```cpp
float bytertc::MixedStreamLayoutRegionConfig::alpha = 1.0f
```


The opacity in the range of (0.0, 1.0]. The lower the value, the more transparent. The default value is 1.0.

<span id="MixedStreamLayoutRegionConfig-corner_radius"></span>
### corner_radius

```cpp
float bytertc::MixedStreamLayoutRegionConfig::corner_radius = 0
```


The proportion of the radius to the width of the canvas. `0.0` by default.

After you set the value, `width_px`, `height_px`, and `corner_radius_px` are calculated based on `width`, `height`, `corner_radius`, and the width of the canvas. If `corner_radius_px < min(width_px/2, height_px/2)` is met, the value of `corner_radius` is set valid; if not, `corner_radius_px` is set to `min(width_px/2, height_px/2)`, and `corner_radius` is set to the proportion of `corner_radius_px` to the width of the canvas.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-z_order"></span>
### z_order

```cpp
int32_t bytertc::MixedStreamLayoutRegionConfig::z_order = 0
```


The layer on which the video is rendered. The range is [0, 100]. 0 for the bottom layer, and 100 for the top layer. The default value is 0.

<span id="MixedStreamLayoutRegionConfig-is_local_user"></span>
### is_local_user

```cpp
bool bytertc::MixedStreamLayoutRegionConfig::is_local_user = false
```


Whether the source user of the stream is a local user:


* true: Yes

* false: (Default) No

   This parameter is not supported for WTN stream tasks.

    &nbsp;


<span id="stream-type"></span>
### stream_type

```cpp
MixedStreamVideoType bytertc::MixedStreamLayoutRegionConfig::stream_type = MixedStreamVideoType::kMixedStreamVideoTypeMain
```


Reserved field.

<span id="MixedStreamLayoutRegionConfig-media_type"></span>
### media_type

```cpp
MixedStreamMediaType bytertc::MixedStreamLayoutRegionConfig::media_type = MixedStreamMediaType::kMixedStreamMediaTypeAudioAndVideo
```


The stream mixing content type. The default value is `kMediaTypeAudioAndVideo`. See [MixedStreamMediaType](https://docs.byteplus.com/en/docs/12/14187#MixedStreamMediaType).

<span id="MixedStreamLayoutRegionConfig-render_mode"></span>
### render_mode

```cpp
MixedStreamRenderMode bytertc::MixedStreamLayoutRegionConfig::render_mode = MixedStreamRenderMode::kMixedStreamRenderModeHidden
```


The render mode. See [MixedStreamRenderMode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamRenderMode). The default value is `1` indicating the video frame is scaled with fixed aspect ratio. It's recommended to be set.

<span id="MixedStreamLayoutRegionConfig-region_content_type"></span>
### region_content_type

```cpp
MixedStreamLayoutRegionType bytertc::MixedStreamLayoutRegionConfig::region_content_type = MixedStreamLayoutRegionType::kMixedStreamLayoutRegionTypeVideoStream
```


Section type, including video section and water mark section. See [MixedStreamLayoutRegionType](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionType). The default value is `0` indicating videos.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-image_water_mark"></span>
### image_water_mark

```cpp
uint8_t* bytertc::MixedStreamLayoutRegionConfig::image_water_mark = nullptr
```


The RGBA data of the watermark. It is required when the region_content_type is set to `kMixedStreamLayoutRegionTypeImage`.

Put in null when you choose `kMixedStreamLayoutRegionTypeVideoStream` as `region_content_type`.

```Plain Text
   This parameter is not supported for WTN stream tasks.
```


<span id="MixedStreamLayoutRegionConfig-image_water_mark_param"></span>
### image_water_mark_param

```cpp
MixedStreamLayoutRegionImageWaterMarkConfig bytertc::MixedStreamLayoutRegionConfig::image_water_mark_param
```


The resolution of the watermark. It is required when the region_content_type is set to `kMixedStreamLayoutRegionTypeImage`. See [MixedStreamLayoutRegionImageWaterMarkConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionImageWaterMarkConfig).

Put in null when you choose `kMixedStreamLayoutRegionTypeVideoStream` as `region_content_type`.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-alternate_image_fill_mode"></span>
### alternate_image_fill_mode

```cpp
MixedStreamAlternateImageFillMode bytertc::MixedStreamLayoutRegionConfig::alternate_image_fill_mode = kMixedStreamAlternateImageFillModeFit
```


Sets the fill mode of the placeholder image.

This parameter is used to control the fill mode of the placeholder image after the user stops publishing video streams and the screen reverts to the placeholder image. It defaults to `kMixedStreamAlternateImageFillModeFit` indicating the image is scaled with the video's aspect ratio.

See [MixedStreamAlternateImageFillMode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAlternateImageFillMode).

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-alternate_image_url"></span>
### alternate_image_url

```cpp
const char* bytertc::MixedStreamLayoutRegionConfig::alternate_image_url = nullptr
```


Sets the URL of the placeholder image, limited to a maximum of 1024 characters.

<span id="MixedStreamLayoutRegionConfig-spatial_position"></span>
### spatial_position

```cpp
Position bytertc::MixedStreamLayoutRegionConfig::spatial_position
```


spatial position. See [Position](https://docs.byteplus.com/en/docs/12/14187#Position).

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-apply_spatial_audio"></span>
### apply_spatial_audio

```cpp
bool bytertc::MixedStreamLayoutRegionConfig::apply_spatial_audio = true
```


Whether to apply spatial audio effect. The default value is true.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamLayoutRegionConfig-source_crop"></span>
### source_crop

```cpp
SourceCrop bytertc::MixedStreamLayoutRegionConfig::source_crop
```


Configurations on how to crop the WTN stream. Refer to [SourceCrop](https://docs.byteplus.com/en/docs/12/14187#SourceCrop) for more details.

This parameter is not supported for mixing\-stream tasks.

<span id="FrameUpdateInfo"></span>
# FrameUpdateInfo

```cpp
struct bytertc::FrameUpdateInfo
```


The pixels and frame rate recommended by RTC.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[pixel](https://docs.byteplus.com/en/docs/12/14187#FrameUpdateInfo-pixel) |
|int |[framerate](https://docs.byteplus.com/en/docs/12/14187#FrameUpdateInfo-framerate) |


<span id="instructions"></span>
## Instructions

<span id="FrameUpdateInfo-pixel"></span>
### pixel

```cpp
int bytertc::FrameUpdateInfo::pixel
```


Pixel (width \* height).

<span id="FrameUpdateInfo-framerate"></span>
### framerate

```cpp
int bytertc::FrameUpdateInfo::framerate
```


The frame rate.

<span id="StreamSubscribeState"></span>
# StreamSubscribeState

```cpp
enum bytertc::StreamSubscribeState
```


Subscription status of media streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kStreamSubscribeStateSuccess |0 |Successfully changed the subscription status |
|kStreamSubscribeStateFailedNotInRoom |1 |Failed to change the subscription status, because you were not in the room. |
|kStreamSubscribeStateFailedStreamNotFound |2 |Failed to change the subscription status, because the target audio/video stream was not found. |
|kStreamSubscribeStateFailedOverLimit |3 |Failed to change the subscription status, because the number of streams you have subscribed to has exceeded the limit. |


<span id="RenderMode"></span>
# RenderMode

```cpp
enum bytertc::RenderMode
```


Rendering mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRenderModeHidden |1 |(Default) Fill and Crop.<br><br>The video frame is scaled with fixed aspect ratio, and completely fills the canvas. The region of the video exceeding the canvas will be cropped. |
|kRenderModeFit |2 |Fit.<br><br>The video frame is scaled with fixed aspect ratio, and is shown completely in the canvas. The region of the canvas not filled with video frame, is filled with `background`. |
|kRenderModeFill |3 |\- |


<span id="AudioRecordingState"></span>
# AudioRecordingState

```cpp
enum bytertc::AudioRecordingState
```


Audio recording config

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioRecordingStateError |0 |Recording exception |
|kAudioRecordingStateProcessing |1 |Recording in progress |
|kAudioRecordingStateSuccess |2 |The recording task ends, and the file is saved. |


<span id="UserOnlineStatus"></span>
# UserOnlineStatus

```cpp
enum bytertc::UserOnlineStatus
```


User online status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kUserOnlineStatusOffline |0 |The peer user is offline<br><br>The peer user has called `logout`, or has not called `login` to sign in. |
|kUserOnlineStatusOnline |1 |The peer user is online<br><br>The peer user calls `login` to sign in, and the connection status is normal. |
|kUserOnlineStatusUnreachable |2 |Unable to get the online state of the peer user<br><br>Returned when a cascade error occurs and the online state of the peer user is abnormal. |


<span id="MixedStreamMediaType"></span>
# MixedStreamMediaType

```cpp
enum bytertc::MixedStreamMediaType
```


The media type of the mixing stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamMediaTypeAudioAndVideo |0 |Audio and video |
|kMixedStreamMediaTypeAudioOnly |1 |Audio only |


<span id="NetworkTimeInfo"></span>
# NetworkTimeInfo

```cpp
struct bytertc::NetworkTimeInfo
```


network time info

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int64_t |[timestamp](https://docs.byteplus.com/en/docs/12/14187#NetworkTimeInfo-timestamp) |


<span id="instructions"></span>
## Instructions

<span id="NetworkTimeInfo-timestamp"></span>
### timestamp

```cpp
int64_t bytertc::NetworkTimeInfo::timestamp
```


Network time. Unit: ms

<span id="MediaDeviceType"></span>
# MediaDeviceType

```cpp
enum bytertc::MediaDeviceType
```


Type of media device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaDeviceTypeAudioUnknown |\-1 |Unknown device |
|kMediaDeviceTypeAudioRenderDevice |0 |Speaker or headphone |
|kMediaDeviceTypeAudioCaptureDevice |1 |Microphone |
|kMediaDeviceTypeVideoCaptureDevice |3 |Video capture device |
|kMediaDeviceTypeScreenVideoCaptureDevice |4 |Screen capture device |
|kMediaDeviceTypeScreenAudioCaptureDevice |5 |Screen audio capture device |


<span id="StreamIndex"></span>
# StreamIndex

```cpp
enum bytertc::StreamIndex
```


Reserved field.

<span id="PublishStateChangeReason"></span>
# PublishStateChangeReason

```cpp
enum bytertc::PublishStateChangeReason
```


Reason to change the publishing state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPublishStateChangeReasonPublish |0 |Requested to publish. |
|kPublishStateChangeReasonUnpublish |1 |Requested to remove. |
|kPublishStateChangeReasonNoPublishPermission |2 |The token the user used was not permitted to publish. |
|kPublishStateChangeReasonOverStreamPublishLimit |3 |The number of streams the user has published has exceeded the limit. |
|kPublishStateChangeReasonMultiRoomUnpublishFailed |4 |The stream failed to remove from a room when you are publishing the stream in two or more rooms. |
|kPublishStateChangeReasonPublishStreamFailed |5 |Failed to publish due to the server error. |
|kPublishStateChangeReasonPublishStreamForbidden |6 |The user who tried to publish a stream is not a host. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setuservisibility) to change the user role. |
|kPublishStateChangeReasonUserInPublish |7 |The user who tried to publish a stream has already published a stream in a room. |
|kPublishStateChangeReasonStreamPublishByOther |8 |Another user publishes a stream with the same streamid, which causes the stream you are publishing to be removed. |
|kPublishStateChangeReasonStreamIdInvalid |9 |Stream ID validation failed. |


<span id="RemoteVideoSinkConfig"></span>
# RemoteVideoSinkConfig

```cpp
struct bytertc::RemoteVideoSinkConfig
```


Remote video frame callback configurations.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|RemoteVideoSinkPosition |[position](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoSinkConfig-position) |
|VideoPixelFormat |[pixel_format](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoSinkConfig-pixel_format) |
|VideoApplyRotation |[apply_rotation](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoSinkConfig-apply_rotation) |
|VideoSinkMirrorType |[mirror_type](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoSinkConfig-mirror_type) |


<span id="instructions"></span>
## Instructions

<span id="RemoteVideoSinkConfig-position"></span>
### position

```cpp
RemoteVideoSinkPosition bytertc::RemoteVideoSinkConfig::position = kRemoteVideoSinkPositionAfterPostProcess
```


The position of the remote video frame. See [RemoteVideoSinkPosition](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoSinkPosition). The default position is after processing.

<span id="RemoteVideoSinkConfig-pixel_format"></span>
### pixel_format

```cpp
VideoPixelFormat bytertc::RemoteVideoSinkConfig::pixel_format = kVideoPixelFormatUnknown
```


The pixel format of the remote video frame. See [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14187#VideoPixelFormat). The default value is 0.

<span id="RemoteVideoSinkConfig-apply_rotation"></span>
### apply_rotation

```cpp
VideoApplyRotation bytertc::RemoteVideoSinkConfig::apply_rotation = kVideoApplyRotationDefault
```


Whether the video frame needs to be automatically rotated. See [VideoApplyRotation](https://docs.byteplus.com/en/docs/12/14187#VideoApplyRotation). The default value is no rotation.

<span id="RemoteVideoSinkConfig-mirror_type"></span>
### mirror_type

```cpp
VideoSinkMirrorType bytertc::RemoteVideoSinkConfig::mirror_type = kVideoSinkMirrorTypeOFF
```


Whether the video frame needs to be mirrored. See [VideoSinkMirrorType](https://docs.byteplus.com/en/docs/12/14187#VideoSinkMirrorType). The default value is no mirroring effect.

This setting is independent of [setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setremotevideomirrortype) (which is applicable for internal rendering).

<span id="MediaDeviceWarning"></span>
# MediaDeviceWarning

```cpp
enum bytertc::MediaDeviceWarning
```


Media device warning

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaDeviceWarningOK |0 |No warning |
|kMediaDeviceWarningOperationDenied |1 |Illegal device operation. Calls the API for internal device when using the external device. |
|kMediaDeviceWarningCaptureSilence |2 |No audio is captured. |
|kMediaDeviceWarningDetectLeakEcho |11 |Echoes between mics and speakers are detected during a call.<br><br>`onAudioDeviceWarning` notifies you with this enum of echo issue. During a call, SDK will detect echo<br><br>issue only when [RoomProfileType](https://docs.byteplus.com/en/docs/12/14187#RoomProfileType) is set to `kRoomProfileTypeMeeting` or<br><br>`kRoomProfileTypeMeetingRoom` and AEC is disabled. |
|kMediaDeviceWarningCaptureDetectHowling |16 |Howling detected.<br><br>You will receive this callback in the following scenarios: 1) Howling is detected under the room profiles that do not support howling suppression; 2) Detect howling that is not suppressed under the room profiles that support howling suppression. You can only enable howling suppression by calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom)to set your room profile as kRoomProfileTypeCommunication, kRoomProfileTypeMeeting, and kRoomProfileTypeMeetingRoom. We recommend that you remind your users to adjust the physical distance between two devices or disable all unused devices except the connecting one. |
|kMediaDeviceWarningPlayoutUseSilentDevice |28 |use silent playout device |
|kMediaDeviceWarningRecordingAllProcess |29 |Unsupport exclude current process capture, all process audio is being captured currently. |
|kMediaDeviceWarningRecordingAllProcessFailed |30 |recording all process failed |


<span id="MixedStreamPushMode"></span>
# MixedStreamPushMode

```cpp
enum bytertc::MixedStreamPushMode
```


The initiation mode for pushing the stream mixed on the server side to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamPushModeOnStream |0 |When no user publishes a media stream, a mixing\-stream task can't be initiated. Default setting.<br><br>When a user publishes at least one media stream, a mixing\-stream task can be initiated. |
|kMixedStreamPushModeOnStartRequest |1 |Even if no user is actively publishing media streams, it is still possible to initiate a stream mixing task using a placeholder image.<br><br>See [alternate_image_url](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-alternate_image_url) and [alternate_image_fill_mode](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig-alternate_image_fill_mode) for setting a placeholder image. |


<span id="VideoCodecType"></span>
# VideoCodecType

```cpp
enum bytertc::VideoCodecType
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

```cpp
struct bytertc::RTCWatermarkConfig
```


Watermark configurations

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[visible_in_preview](https://docs.byteplus.com/en/docs/12/14187#RTCWatermarkConfig-visible_in_preview) |
|ByteWatermark |[position_in_landscape_mode](https://docs.byteplus.com/en/docs/12/14187#RTCWatermarkConfig-position_in_landscape_mode) |
|ByteWatermark |[position_in_portrait_mode](https://docs.byteplus.com/en/docs/12/14187#RTCWatermarkConfig-position_in_portrait_mode) |


<span id="instructions"></span>
## Instructions

<span id="RTCWatermarkConfig-visible_in_preview"></span>
### visible_in_preview

```cpp
bool bytertc::RTCWatermarkConfig::visible_in_preview = true
```


Whether the watermark is visible in preview. Its default value is `true`.

<span id="RTCWatermarkConfig-position_in_landscape_mode"></span>
### position_in_landscape_mode

```cpp
ByteWatermark bytertc::RTCWatermarkConfig::position_in_landscape_mode
```


Watermark's coordinates and size in landscape mode. See [ByteWatermark](https://docs.byteplus.com/en/docs/12/14187#ByteWatermark).

<span id="RTCWatermarkConfig-position_in_portrait_mode"></span>
### position_in_portrait_mode

```cpp
ByteWatermark bytertc::RTCWatermarkConfig::position_in_portrait_mode
```


Watermark's coordinates and size in portrait mode. See [ByteWatermark](https://docs.byteplus.com/en/docs/12/14187#ByteWatermark).

<span id="EffectBeautyMode"></span>
# EffectBeautyMode

```cpp
enum bytertc::EffectBeautyMode
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


<span id="PixelFormat"></span>
# PixelFormat

```cpp
enum bytertc::IVideoSink::PixelFormat
```


Video frame encoding format

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kI420 |VideoPixelFormat::kVideoPixelFormatI420 |YUV I420 format |
|kRGBA |VideoPixelFormat::kVideoPixelFormatRGBA |RGBA format |
|kOriginal |VideoPixelFormat::kVideoPixelFormatUnknown |Original format |


<span id="HumanOrientation"></span>
# HumanOrientation

```cpp
struct bytertc::HumanOrientation
```


Three\-dimensional orientation information, each pair of vectors need to be perpendicular. See [Orientation](https://docs.byteplus.com/en/docs/12/14187#Orientation).

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|Orientation |[forward](https://docs.byteplus.com/en/docs/12/14187#HumanOrientation-forward) |
|Orientation |[right](https://docs.byteplus.com/en/docs/12/14187#HumanOrientation-right) |
|Orientation |[up](https://docs.byteplus.com/en/docs/12/14187#HumanOrientation-up) |


<span id="instructions"></span>
## Instructions

<span id="HumanOrientation-forward"></span>
### forward

```cpp
Orientation bytertc::HumanOrientation::forward = { 1, 0, 0 }
```


Forward orientation, the default value is {1,0,0}, i.e., the forward orientation is in the positive direction of x\-axis.

<span id="HumanOrientation-right"></span>
### right

```cpp
Orientation bytertc::HumanOrientation::right = { 0, 1, 0 }
```


Rightward orientation, the default value is {0,1,0}, i.e., the rightward orientation is in the positive direction of y\-axis.

<span id="HumanOrientation-up"></span>
### up

```cpp
Orientation bytertc::HumanOrientation::up = { 0, 0, 1 }
```


Upward orientation, the default value is {0,0,1}, i.e., the upward orientation is in the positive direction of z\-axis.

<span id="VideoEnhancementMode"></span>
# VideoEnhancementMode

```cpp
enum bytertc::VideoEnhancementMode
```


Low light adjusted type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoEnhancementModeDisabled |0 |Turn off low light adaptation |
|kVideoEnhancementModeAuto |1 |Turn on low light adaptation |


<span id="AnsMode"></span>
# AnsMode

```cpp
enum bytertc::AnsMode
```


ANC modes.The ANC algorithm is determined by the room profile you set when calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom).

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAnsModeDisable |0 |Disable ANC. |
|kAnsModeLow |1 |Cancel subtle background noise. |
|kAnsModeMedium |2 |Cancel medium\-level, continuous noise, such as the sound of fans or air conditioners. |
|kAnsModeHigh |3 |Cancel loud, impulsive, and intermittent noise, such as keyboard clicking noise, a crash/clash, a bark, and chair scraping noise. |
|kAnsModeAutomatic |4 |Enable automatic ANC. The ANC algorithm is dynamically determined by RTC. |


<span id="MixedStreamAlternateImageFillMode"></span>
# MixedStreamAlternateImageFillMode

```cpp
enum bytertc::MixedStreamAlternateImageFillMode
```


The fill mode of the placeholder image.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamAlternateImageFillModeFit |0 |The placeholder image is scaled with the same aspect ratio as the user's original video frame. Default setting. |
|kMixedStreamAlternateImageFillModeFill |1 |The placeholder image is not scaled with the same aspect ratio as the user's original video frame. It maintains the original aspect ratio. |


<span id="LocalVideoSinkPosition"></span>
# LocalVideoSinkPosition

```cpp
enum bytertc::LocalVideoSinkPosition
```


The position of the local video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalVideoSinkPositionAfterCapture |0 |After capturing. |
|kLocalVideoSinkPositionAfterPreProcess |1 |(Default) After preprocessing. |


<span id="AudioRenderType"></span>
# AudioRenderType

```cpp
enum bytertc::AudioRenderType
```


Audio output type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioRenderTypeExternal |0 |Custom Render |
|kAudioRenderTypeInternal |1 |RTC SDK internal render |


<span id="AudioVolumeInfo"></span>
# AudioVolumeInfo

```cpp
struct bytertc::AudioVolumeInfo
```


User ID of the source of the audio stream and the corresponding volume.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[linear_volume](https://docs.byteplus.com/en/docs/12/14187#AudioVolumeInfo-linear_volume) |
|int |[nonlinear_volume](https://docs.byteplus.com/en/docs/12/14187#AudioVolumeInfo-nonlinear_volume) |
|const char\* |[uid](https://docs.byteplus.com/en/docs/12/14187#AudioVolumeInfo-uid) |


<span id="instructions"></span>
## Instructions

<span id="AudioVolumeInfo-linear_volume"></span>
### linear_volume

```cpp
int bytertc::AudioVolumeInfo::linear_volume
```


Linear volume, the value range is: [0,255], which has a linear relationship with the original volume.

The larger the value, the greater the volume. Silence is below 25 (absolutely silent is 0, below 25 there is basically no sound, which can be regarded as silent),

low volume is 25~76, medium volume is 76~204, and high volume is above 204

<span id="AudioVolumeInfo-nonlinear_volume"></span>
### nonlinear_volume

```cpp
int bytertc::AudioVolumeInfo::nonlinear_volume
```


Non\-linear volume, the value range is: [\-127, 0], the unit is dB. This volume range is a logarithmic conversion of the original volume,

and the resolution is more sensitive at medium and low volume, which is suitable for identification as an Active Speaker (the most active user in the room).

The high volume is 0~\-20dB, the medium volume is \-20~\-40dB, and the low volume is \-40~\-60dB. If it is lower than \-60dB, it is silent.

<span id="AudioVolumeInfo-uid"></span>
### uid

```cpp
const char* bytertc::AudioVolumeInfo::uid
```


User ID of the audio stream source

<span id="LocalVideoSinkConfig"></span>
# LocalVideoSinkConfig

```cpp
struct bytertc::LocalVideoSinkConfig
```


Local video frame callback config.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|LocalVideoSinkPosition |[position](https://docs.byteplus.com/en/docs/12/14187#LocalVideoSinkConfig-position) |
|VideoPixelFormat |[pixel_format](https://docs.byteplus.com/en/docs/12/14187#LocalVideoSinkConfig-pixel_format) |


<span id="instructions"></span>
## Instructions

<span id="LocalVideoSinkConfig-position"></span>
### position

```cpp
LocalVideoSinkPosition bytertc::LocalVideoSinkConfig::position = kLocalVideoSinkPositionAfterPreProcess
```


The position of the local video frame. See [LocalVideoSinkPosition](https://docs.byteplus.com/en/docs/12/14187#LocalVideoSinkPosition).

<span id="LocalVideoSinkConfig-pixel_format"></span>
### pixel_format

```cpp
VideoPixelFormat bytertc::LocalVideoSinkConfig::pixel_format = kVideoPixelFormatUnknown
```


The pixel format of the local video frame. See [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/14187#VideoPixelFormat). The default value is 0.

<span id="CloudProxyConfiguration"></span>
# CloudProxyConfiguration

```cpp
struct bytertc::CloudProxyConfiguration
```


Configuration of Cloud Proxy

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CloudProxyInfo\* |[cloud_proxies](https://docs.byteplus.com/en/docs/12/14187#CloudProxyConfiguration-cloud_proxies) |
|int |[cloud_proxy_count](https://docs.byteplus.com/en/docs/12/14187#CloudProxyConfiguration-cloud_proxy_count) |


<span id="instructions"></span>
## Instructions

<span id="CloudProxyConfiguration-cloud_proxies"></span>
### cloud_proxies

```cpp
CloudProxyInfo* bytertc::CloudProxyConfiguration::cloud_proxies = nullptr
```


Information of cloud proxy.

<span id="CloudProxyConfiguration-cloud_proxy_count"></span>
### cloud_proxy_count

```cpp
int bytertc::CloudProxyConfiguration::cloud_proxy_count = 0
```


Number of cloud proxy.

<span id="Position"></span>
# Position

```cpp
struct bytertc::Position
```


Coordinate value of the local user's position in the rectangular coordinate system in the RTC room.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/14187#Position-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/14187#Position-y) |
|float |[z](https://docs.byteplus.com/en/docs/12/14187#Position-z) |


<span id="instructions"></span>
## Instructions

<span id="Position-x"></span>
### x

```cpp
float bytertc::Position::x
```


X\-coordinate

<span id="Position-y"></span>
### y

```cpp
float bytertc::Position::y
```


Y\-coordinate

<span id="Position-z"></span>
### z

```cpp
float bytertc::Position::z
```


Z\-coordinate

<span id="VideoEncodePreference"></span>
# VideoEncodePreference

```cpp
enum bytertc::VideoEncodePreference
```


Encoder preference.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoEncodePreferenceDisabled |0 |No preference. The frame rate and the resolution will not be adjusted. |
|kVideoEncodePreferenceFramerate |1 |The high frame rate mode. Ensure the highest framerate possible. This mode is designed for videos with high\-motion contents. |
|kVideoEncodePreferenceQuality |2 |The high\-resolution mode. Ensure the highest resolution possible. This mode is designed for videos with static contents. |
|kVideoEncodePreferenceAuto |3 |Balancing resolution and frame rate.<br><br>For the screen\-recordings, the mode is dynamically determined by RTC based on the content. |


<span id="LocalProxyType"></span>
# LocalProxyType

```cpp
enum bytertc::LocalProxyType
```


Types of local proxies.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalProxyTypeSocks5 |1 |Socks5 proxy. If you chose Socks5 as the local proxy, you need to make sure all requirements listed in the Socks5 document are satisfied. |
|kLocalProxyTypeHttpTunnel |2 |Http tunnel proxy. |


<span id="AudioMixingType"></span>
# AudioMixingType

```cpp
enum bytertc::AudioMixingType
```


Mixing type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioMixingTypePlayout |0 |Played at the local device only |
|kAudioMixingTypePublish |1 |Sent to the remote devices only |
|kAudioMixingTypePlayoutAndPublish |2 |Played at the local device and sent to the remote devices. |


<span id="RoomLiveMode"></span>
# RoomLiveMode

```cpp
enum bytertc::RoomLiveMode
```


Live streaming mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRoomLiveModeCoHost |1 |Co\-hosted live streaming. Focus on quality, the default video bitrate is higher. |
|kRoomLiveModeSoloHost |2 |Single host live streaming. |


<span id="AudioFrameBuilder"></span>
# AudioFrameBuilder

```cpp
struct bytertc::AudioFrameBuilder
```


Audio frame construction class

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|AudioSampleRate |[sample_rate](https://docs.byteplus.com/en/docs/12/14187#AudioFrameBuilder-sample_rate) |
|AudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14187#AudioFrameBuilder-channel) |
|int64_t |[timestamp_us](https://docs.byteplus.com/en/docs/12/14187#AudioFrameBuilder-timestamp_us) |
|uint8_t\* |[data](https://docs.byteplus.com/en/docs/12/14187#AudioFrameBuilder-data) |
|int64_t |[data_size](https://docs.byteplus.com/en/docs/12/14187#AudioFrameBuilder-data_size) |
|bool |[deep_copy](https://docs.byteplus.com/en/docs/12/14187#AudioFrameBuilder-deep_copy) |


<span id="instructions"></span>
## Instructions

<span id="AudioFrameBuilder-sample_rate"></span>
### sample_rate

```cpp
AudioSampleRate bytertc::AudioFrameBuilder::sample_rate
```


Audio Sampling Rate

<span id="AudioFrameBuilder-channel"></span>
### channel

```cpp
AudioChannel bytertc::AudioFrameBuilder::channel
```


Number of audio channels

<span id="AudioFrameBuilder-timestamp_us"></span>
### timestamp_us

```cpp
int64_t bytertc::AudioFrameBuilder::timestamp_us = 0
```


Audio frame timestamp in microseconds

**Notes**

This timestamp is not a Linux timestamp; it is an internal timestamp of the SDK, which only ensures the relative relationship between the timestamps of frames.

<span id="AudioFrameBuilder-data"></span>
### data

```cpp
uint8_t* bytertc::AudioFrameBuilder::data
```


Audio frame data

<span id="AudioFrameBuilder-data_size"></span>
### data_size

```cpp
int64_t bytertc::AudioFrameBuilder::data_size = 0
```


Audio frame data size

<span id="AudioFrameBuilder-deep_copy"></span>
### deep_copy

```cpp
bool bytertc::AudioFrameBuilder::deep_copy = true
```


Is deep\-copy or not

<span id="ForwardStreamConfiguration"></span>
# ForwardStreamConfiguration

```cpp
struct bytertc::ForwardStreamConfiguration
```


Information of the rooms where you want to relay the media stream to

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ForwardStreamInfo\* |[forward_stream_dests](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamConfiguration-forward_stream_dests) |
|int |[dest_count](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamConfiguration-dest_count) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamConfiguration-forward_stream_dests"></span>
### forward_stream_dests

```cpp
ForwardStreamInfo* bytertc::ForwardStreamConfiguration::forward_stream_dests = nullptr
```


Information of the rooms where you want to relay the media stream to

<span id="ForwardStreamConfiguration-dest_count"></span>
### dest_count

```cpp
int bytertc::ForwardStreamConfiguration::dest_count = 0
```


Number of the rooms where you want to relay the media stream

We recommend that the number is not higher than 4.

<span id="RoomStateChangeReason"></span>
# RoomStateChangeReason

```cpp
enum bytertc::RoomStateChangeReason
```


Room state change reason.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRoomStateChangeReasonJoinRoom |0 |Join room success for the first time. |
|kRoomStateChangeReasonReconnect |1 |Rejoin the room, such as the network is reconnected. |
|kRoomStateChangeReasonLeaveRoom |2 |Leave room. |
|kRoomStateChangeReasonJoinRoomFailed |\-2001 |Failed to enter the room.<br><br>When you call the first time to join the room or disconnect and reconnect due to poor network conditions, the room entry fails due to a server error. The SDK automatically retries joining the room. |
|kRoomStateChangeReasonInvalidToken |\-1000 |Token is invalid. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>The Token used when calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) is invalid or expired. The user is required to retrieve the token and call the [updateToken](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-updatetoken) to update the token. |
|kRoomStateChangeReasonTokenExpired |\-1009 |Token expired. This error code is returned when the user's token expires in the room.<br><br>Call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) to rejoin the room with a new required Token. |
|kRoomStateChangeReasonUpdateTokenWithInvalidToken |\-1010 |The Token you provided when calling `updateToken` is invalid. |
|kRoomStateChangeReasonRoomForbidden |\-1025 |The room has been banned before the user calls `joinRoom`. |
|kRoomStateChangeReasonUserForbidden |\-1026 |The user has been banned before calling `joinRoom`. |
|kRoomStateChangeReasonKickedOut |\-1006 |The user has been removed from the room by the administrator via an OpenAPI call. |
|kRoomStateChangeReasonRoomDismiss |\-1011 |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. |
|kRoomStateChangeReasonDuplicateLogin |\-1004 |The user has been removed from the room because the same user joined the room on another client. |
|kRoomStateChangeReasonStateAbnormalServerStatus |\-1084 |The user has been removed from the room due to the abnormal server status. This code will be received via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged).<br><br>SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support. |
|kRoomStateChangeReasonUnknown |\-1001 |Join room error. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>An unknown error occurred while joining the room, which caused the joining room to fail. Users are required to rejoin the room. |


<span id="DivideMode"></span>
# DivideMode

```cpp
enum bytertc::DivideMode
```


To split the model

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kDivideModeNone |0 |In\-house |
|kDivideModeEffect |1 |effect |


<span id="MediaStreamInfo"></span>
# MediaStreamInfo

```cpp
struct bytertc::MediaStreamInfo
```


Stream property.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#MediaStreamInfo-user_id) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#MediaStreamInfo-is_screen) |
|bool |[has_video](https://docs.byteplus.com/en/docs/12/14187#MediaStreamInfo-has_video) |
|bool |[has_audio](https://docs.byteplus.com/en/docs/12/14187#MediaStreamInfo-has_audio) |
|VideoSolutionDescription\* |[profiles](https://docs.byteplus.com/en/docs/12/14187#MediaStreamInfo-profiles) |
|int |[profile_count](https://docs.byteplus.com/en/docs/12/14187#MediaStreamInfo-profile_count) |
|VideoSolutionDescription |[max_profile](https://docs.byteplus.com/en/docs/12/14187#MediaStreamInfo-max_profile) |


<span id="instructions"></span>
## Instructions

<span id="MediaStreamInfo-user_id"></span>
### user_id

```cpp
const char* bytertc::MediaStreamInfo::user_id
```


The user ID that published this stream.

<span id="MediaStreamInfo-is_screen"></span>
### is_screen

```cpp
bool bytertc::MediaStreamInfo::is_screen
```


Reserved field. Ignore the value returned in this field.

<span id="MediaStreamInfo-has_video"></span>
### has_video

```cpp
bool bytertc::MediaStreamInfo::has_video
```


Whether this stream includes a video stream.

<span id="MediaStreamInfo-has_audio"></span>
### has_audio

```cpp
bool bytertc::MediaStreamInfo::has_audio
```


Whether the stream includes an audio stream.

<span id="MediaStreamInfo-profiles"></span>
### profiles

```cpp
VideoSolutionDescription* bytertc::MediaStreamInfo::profiles
```


Properties of the video stream.

When a remote user calls the [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideoencoderconfig) method to publish multiple configured video streams, this will contain attribute information for all video streams published by the user.

<span id="MediaStreamInfo-profile_count"></span>
### profile_count

```cpp
int bytertc::MediaStreamInfo::profile_count
```


Number of different configuration streams.

When a remote user calls the [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideoencoderconfig) method to publish multiple configured video streams, this contains the number of video streams published by the user.

<span id="MediaStreamInfo-max_profile"></span>
### max_profile

```cpp
VideoSolutionDescription bytertc::MediaStreamInfo::max_profile
```


Properties of the maximum video stream.

When a remote user publishes multiple configured video streams, this will contain the maximum attribute information . user with new subscribe call can require any stream does not exceed this resolution.

The final stream received, influenced by the others in room, the server will deliver the resolution closest to what the user requested。

<span id="SimulcastStreamType"></span>
# SimulcastStreamType

```cpp
enum bytertc::SimulcastStreamType
```


The preference for the quality of the subscribed stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSimulcastStreamTypeWeak |0 |The stream with the lowest quality, which has the lowest resolution. |
|kSimulcastStreamTypeLow |1 |The stream with a low quality. |
|kSimulcastStreamTypeMid |2 |The stream with a medium quality. |
|kSimulcastStreamTypeHigh |3 |The stream with the best quality. |


<span id="StreamRemoveReason"></span>
# StreamRemoveReason

```cpp
enum bytertc::StreamRemoveReason
```


The reason why the remote stream in the room was removed.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kStreamRemoveReasonUnpublish |0 |The remote user stops publishing the stream. |
|kStreamRemoveReasonPublishFailed |1 |The remote user failed to publish the stream. |
|kStreamRemoveReasonKeepLiveFailed |2 |Media server failed to receive media data from the client for 10 seconds. |
|kStreamRemoveReasonClientDisconnected |3 |The remote user is disconnected. |
|kStreamRemoveReasonRepublish |4 |The remote user republishes the stream. |
|kStreamRemoveReasonOther |5 |Other reasons. |
|kStreamRemoveReasonPrivilegeTokenExpired |6 |The remote user's publishing privilege of the Token is expired. |
|kStreamRemoveReasonStreamKickedByOther |7 |The stream is kicked. |


<span id="RemoteAudioStats"></span>
# RemoteAudioStats

```cpp
struct bytertc::RemoteAudioStats
```


Remote audio stream statistics, reference period 2s.

After a local user subscribes to a remote audio stream successfully, the SDK periodically notifies the local user of the reception status of the subscribed audio stream during this reference period through `onRemoteStreamStats`. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[audio_loss_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-audio_loss_rate) |
|int |[received_kbitrate](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-received_kbitrate) |
|int |[stall_count](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-stall_count) |
|int |[stall_duration](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-stall_duration) |
|long |[e2e_delay](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-e2e_delay) |
|int |[playout_sample_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-playout_sample_rate) |
|int |[stats_interval](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-stats_interval) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-rtt) |
|int |[total_rtt](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-total_rtt) |
|int |[quality](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-quality) |
|int |[jitter_buffer_delay](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-jitter_buffer_delay) |
|int |[num_channels](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-num_channels) |
|int |[received_sample_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-received_sample_rate) |
|int |[frozen_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-frozen_rate) |
|int |[concealed_samples](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-concealed_samples) |
|int |[concealment_event](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-concealment_event) |
|int |[dec_sample_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-dec_sample_rate) |
|int |[dec_duration](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-dec_duration) |
|int |[jitter](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-jitter) |
|double |[decode_frame_rate](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats-decode_frame_rate) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioStats-audio_loss_rate"></span>
### audio_loss_rate

```cpp
float bytertc::RemoteAudioStats::audio_loss_rate
```


Audio packet loss rate. The audio downlink packet loss rate in the reference period, the value range is [0,1].

<span id="RemoteAudioStats-received_kbitrate"></span>
### received_kbitrate

```cpp
int bytertc::RemoteAudioStats::received_kbitrate
```


Receiving bit rate. The audio reception rate in the reference period in kbps.

<span id="RemoteAudioStats-stall_count"></span>
### stall_count

```cpp
int bytertc::RemoteAudioStats::stall_count
```


Number of audio stalls. Number of stalls in the reference period.

<span id="RemoteAudioStats-stall_duration"></span>
### stall_duration

```cpp
int bytertc::RemoteAudioStats::stall_duration
```


Audio stall Duration. Stall duration in the reference period in ms.

<span id="RemoteAudioStats-e2e_delay"></span>
### e2e_delay

```cpp
long bytertc::RemoteAudioStats::e2e_delay
```


End\-to\-end latency at the user experience level. The delay from the start of encoding at the sending end to the start of decoding at the receiving end, in units of ms.

<span id="RemoteAudioStats-playout_sample_rate"></span>
### playout_sample_rate

```cpp
int bytertc::RemoteAudioStats::playout_sample_rate
```


Play sample rate. Audio playback sample rate information within the reference period in Hz.

<span id="RemoteAudioStats-stats_interval"></span>
### stats_interval

```cpp
int bytertc::RemoteAudioStats::stats_interval
```


Statistical interval. The interval of this reference period is in ms.

<span id="RemoteAudioStats-rtt"></span>
### rtt

```cpp
int bytertc::RemoteAudioStats::rtt
```


Round\-trip time for client side to server level data transfer in ms.

<span id="RemoteAudioStats-total_rtt"></span>
### total_rtt

```cpp
int bytertc::RemoteAudioStats::total_rtt
```


The sender\-server level\-the receiver\-link data transmission round\-trip time. The unit is ms.

<span id="RemoteAudioStats-quality"></span>
### quality

```cpp
int bytertc::RemoteAudioStats::quality
```


The quality of the audio stream sent by the remote user. Value meaning reference [NetworkQuality](https://docs.byteplus.com/en/docs/12/14187#NetworkQuality).

<span id="RemoteAudioStats-jitter_buffer_delay"></span>
### jitter_buffer_delay

```cpp
int bytertc::RemoteAudioStats::jitter_buffer_delay
```


The delay caused by the introduction of the jitter buffer mechanism. The unit is ms.

<span id="RemoteAudioStats-num_channels"></span>
### num_channels

```cpp
int bytertc::RemoteAudioStats::num_channels
```


Number of audio channels.

<span id="RemoteAudioStats-received_sample_rate"></span>
### received_sample_rate

```cpp
int bytertc::RemoteAudioStats::received_sample_rate
```


Audio reception sampling rate. Remote audio sampling rate information received within the reference period, in Hz.

<span id="RemoteAudioStats-frozen_rate"></span>
### frozen_rate

```cpp
int bytertc::RemoteAudioStats::frozen_rate
```


The accumulated length of audio stuttering occurs after the remote user joins the room as a percentage of the total effective length of the audio. The effective duration of audio refers to the duration of audio other than stopping sending audio streams and disabling audio modules after remote users enter the room to publish audio streams.

<span id="RemoteAudioStats-concealed_samples"></span>
### concealed_samples

```cpp
int bytertc::RemoteAudioStats::concealed_samples
```


Audio packet loss compensation (PLC) total number of sample points.

<span id="RemoteAudioStats-concealment_event"></span>
### concealment_event

```cpp
int bytertc::RemoteAudioStats::concealment_event
```


Audio packet loss compensation (PLC) cumulative times.

<span id="RemoteAudioStats-dec_sample_rate"></span>
### dec_sample_rate

```cpp
int bytertc::RemoteAudioStats::dec_sample_rate
```


Audio decoding sample rate. Audio decoding sample rate information in the reference period in Hz.

<span id="RemoteAudioStats-dec_duration"></span>
### dec_duration

```cpp
int bytertc::RemoteAudioStats::dec_duration
```


Cumulative decoding time in seconds of the remote audio stream in this subscription.

<span id="RemoteAudioStats-jitter"></span>
### jitter

```cpp
int bytertc::RemoteAudioStats::jitter
```


Audio downlink network jitter in ms.

<span id="RemoteAudioStats-decode_frame_rate"></span>
### decode_frame_rate

```cpp
double bytertc::RemoteAudioStats::decode_frame_rate
```


Audio decode frame rate.

<span id="TorchState"></span>
# TorchState

```cpp
enum bytertc::TorchState
```


Camera fill light status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kTorchStateOff |0 |Camera fill light off |
|kTorchStateOn |1 |Camera fill light on |


<span id="IMixedStreamConfig"></span>
# IMixedStreamConfig

```cpp
class bytertc::IMixedStreamConfig
```


Stream\-mixing task configurations.

If not specified, the parameter can be used for both WTN stream and mixing\-stream tasks.

If not specified, the parameter can be passed when starting a task or during a task.

<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|BYTERTC_STATIC_API IMixedStreamConfig\* |[createMixedStreamConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-createmixedstreamconfig) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual const char\* |[getRoomID](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getroomid) |
|virtual void |[setRoomID](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setroomid) |
|virtual const char\* |[getUserID](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getuserid) |
|virtual void |[setUserID](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setuserid) |
|virtual MixedStreamAudioConfig |[getAudioConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getaudioconfig) |
|virtual void |[setAudioConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setaudioconfig) |
|virtual MixedStreamVideoConfig |[getVideoConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getvideoconfig) |
|virtual void |[setVideoConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setvideoconfig) |
|virtual MixedStreamControlConfig |[getControlConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getcontrolconfig) |
|virtual void |[setControlConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setcontrolconfig) |
|virtual const char\* |[getUserConfigExtraInfo](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getuserconfigextrainfo) |
|virtual void |[setUserConfigExtraInfo](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setuserconfigextrainfo) |
|virtual StreamLayoutMode |[getStreamLayoutMode](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getstreamlayoutmode) |
|virtual void |[setStreamLayoutMode](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setstreamlayoutmode) |
|virtual InterpolationMode |[getInterpolationMode](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getinterpolationmode) |
|virtual void |[setInterpolationMode](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setinterpolationmode) |
|virtual const char\* |[getPushWTNStreamID](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getpushwtnstreamid) |
|virtual void |[setPushWTNStreamID](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setpushwtnstreamid) |
|virtual MixedStreamPushTargetType |[getPushTargetType](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getpushtargettype) |
|virtual void |[setPushTargetType](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setpushtargettype) |
|virtual const char\* |[getBackgroundColor](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getbackgroundcolor) |
|virtual void |[setBackgroundColor](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setbackgroundcolor) |
|virtual const char\* |[getBackgroundImageURL](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getbackgroundimageurl) |
|virtual void |[setBackgroundImageURL](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setbackgroundimageurl) |
|virtual MixedStreamLayoutRegionConfig |[getLayoutByIndex](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getlayoutbyindex) |
|virtual int32_t |[getLayoutRegionsSize](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-getlayoutregionssize) |
|virtual void |[setLayoutConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-setlayoutconfig) |
|virtual |[~IMixedStreamConfig](https://docs.byteplus.com/en/docs/12/14187#IMixedStreamConfig-~imixedstreamconfig) |


<span id="instructions"></span>
## Instructions

<span id="IMixedStreamConfig-createmixedstreamconfig"></span>
### createMixedStreamConfig

```cpp
static BYTERTC_STATIC_API IMixedStreamConfig* createMixedStreamConfig();
```


Create a mixed stream task configuration.

**Return Value**

A mixed stream task configuration.

<span id="IMixedStreamConfig-getroomid"></span>
### getRoomID

```cpp
virtual const char* getRoomID() = 0;
```


Get the ID of the room where the streams to be mixed sources from.

**Return Value**

The room ID

<span id="IMixedStreamConfig-setroomid"></span>
### setRoomID

```cpp
virtual void setRoomID(const char* room_id) = 0;
```


Set the room ID to specify where the streams to be mixed sources from.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |The room ID |


**Notes**

This parameters cannot be updated during.

<span id="IMixedStreamConfig-getuserid"></span>
### getUserID

```cpp
virtual const char* getUserID() = 0;
```


Gets the ID of the user who started the mixing\-stream task.

**Return Value**

The user ID

<span id="IMixedStreamConfig-setuserid"></span>
### setUserID

```cpp
virtual void setUserID(const char* user_id) = 0;
```


Sets the user ID to specify who started the mixing\-stream task. The sum length of `room_id` and `user_id` should not exceed 126 bytes. It's recommended to be set.

This parameter cannot be updated during the task.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|user_id |const char\* |The user ID. |


<span id="IMixedStreamConfig-getaudioconfig"></span>
### getAudioConfig

```cpp
virtual MixedStreamAudioConfig getAudioConfig() = 0;
```


Gets the audio configurations.

**Return Value**

Audio configurations. See [MixedStreamAudioConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamAudioConfig).

<span id="IMixedStreamConfig-setaudioconfig"></span>
### setAudioConfig

```cpp
virtual void setAudioConfig(const MixedStreamAudioConfig&) = 0;
```


Sets audio configurations. It's recommended to be set.

**Notes**


* This parameters cannot be updated during the task.

* This parameter is not supported for WTN stream tasks.

    &nbsp;


<span id="getvideoconfig"></span>
### getVideoConfig

```cpp
virtual MixedStreamVideoConfig getVideoConfig() = 0;
```


Gets the video configurations.

**Return Value**

Video configurations. See [MixedStreamVideoConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamVideoConfig).

<span id="IMixedStreamConfig-setvideoconfig"></span>
### setVideoConfig

```cpp
virtual void setVideoConfig(const MixedStreamVideoConfig&) = 0;
```


Sets video configurations. It's recommended to be set.

<span id="IMixedStreamConfig-getcontrolconfig"></span>
### getControlConfig

```cpp
virtual MixedStreamControlConfig getControlConfig() = 0;
```


Gets the configurations while mixing streams on the server side. See [MixedStreamControlConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig).

<span id="IMixedStreamConfig-setcontrolconfig"></span>
### setControlConfig

```cpp
virtual void setControlConfig(MixedStreamControlConfig& config) = 0;
```


Sets the configurations while mixing streams on the server side. See [MixedStreamControlConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |MixedStreamControlConfig& |see [MixedStreamControlConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamControlConfig). |


<span id="IMixedStreamConfig-getuserconfigextrainfo"></span>
### getUserConfigExtraInfo

```cpp
virtual const char* getUserConfigExtraInfo() = 0;
```


Get user config extra information.

**Return Value**

Extra Information.

<span id="IMixedStreamConfig-setuserconfigextrainfo"></span>
### setUserConfigExtraInfo

```cpp
virtual void setUserConfigExtraInfo(const char* user_ext_info) = 0;
```


set user config extra information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|user_ext_info |const char\* |Extra information. |


**Notes**

This parameter is not supported for WTN stream tasks.

<span id="IMixedStreamConfig-getstreamlayoutmode"></span>
### getStreamLayoutMode

```cpp
virtual StreamLayoutMode getStreamLayoutMode() = 0;
```


Get the layout mode of the WTN stream.

**Return Value**

[StreamLayoutMode](https://docs.byteplus.com/en/docs/12/14187#StreamLayoutMode) Information.

<span id="IMixedStreamConfig-setstreamlayoutmode"></span>
### setStreamLayoutMode

```cpp
virtual void setStreamLayoutMode(StreamLayoutMode mode) = 0;
```


Sets the layout mode of the WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mode |StreamLayoutMode |Layout mode. See [StreamLayoutMode](https://docs.byteplus.com/en/docs/12/14187#StreamLayoutMode). |


<span id="IMixedStreamConfig-getinterpolationmode"></span>
### getInterpolationMode

```cpp
virtual InterpolationMode getInterpolationMode() = 0;
```


Get the interpolation mode of the WTN stream.

**Return Value**

[InterpolationMode](https://docs.byteplus.com/en/docs/12/14187#InterpolationMode) Information.

<span id="IMixedStreamConfig-setinterpolationmode"></span>
### setInterpolationMode

```cpp
virtual void setInterpolationMode(InterpolationMode mode) = 0;
```


Sets the interpolationMode mode of the WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mode |InterpolationMode |Interpolation mode. See [InterpolationMode](https://docs.byteplus.com/en/docs/12/14187#InterpolationMode). |


<span id="IMixedStreamConfig-getpushwtnstreamid"></span>
### getPushWTNStreamID

```cpp
virtual const char* getPushWTNStreamID() = 0;
```


Gets the WTN stream ID.

**Return Value**

The WTN stream ID.

<span id="IMixedStreamConfig-setpushwtnstreamid"></span>
### setPushWTNStreamID

```cpp
virtual void setPushWTNStreamID(const char* stream_id) = 0;
```


Specify the WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The WTN stream ID. |


<span id="IMixedStreamConfig-getpushtargettype"></span>
### getPushTargetType

```cpp
virtual MixedStreamPushTargetType getPushTargetType() = 0;
```


Gets the task type.

**Return Value**

[MixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/14187#MixedStreamPushTargetType)

<span id="IMixedStreamConfig-setpushtargettype"></span>
### setPushTargetType

```cpp
virtual void setPushTargetType(MixedStreamPushTargetType type) = 0;
```


Sets push task type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |MixedStreamPushTargetType |See [MixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/14187#MixedStreamPushTargetType). |


<span id="IMixedStreamConfig-getbackgroundcolor"></span>
### getBackgroundColor

```cpp
virtual const char* getBackgroundColor() = 0;
```


Gets the background color.

**Return Value**

Background color. Use HEX color code to represent. For example, #FFFFFF for white, and #000000 for black.

<span id="IMixedStreamConfig-setbackgroundcolor"></span>
### setBackgroundColor

```cpp
virtual void setBackgroundColor(const char* background_color) = 0;
```


set user config extra information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|background_color |const char\* |Background color. Use HEX color code to represent. For example, #FFFFFF for white, and #000000 for black. The default value is #000000. It's recommended to be set. |


<span id="IMixedStreamConfig-getbackgroundimageurl"></span>
### getBackgroundImageURL

```cpp
virtual const char* getBackgroundImageURL() = 0;
```


Gets the background image URL.

**Return Value**

Background image URL.

<span id="IMixedStreamConfig-setbackgroundimageurl"></span>
### setBackgroundImageURL

```cpp
virtual void setBackgroundImageURL(const char* background_image_url) = 0;
```


Sets the background image for the canvas that renders the mixed stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|background_image_url |const char\* |The URL of the image, with a maximum length of 1023 bytes.<br><br>&nbsp;<br><br>The URL must start with http. Supported image formats include: JPG, JPEG, PNG. If the width and height of the background image do not match the width and height of the overall screen, the background image will be scaled to fill the screen. |


<span id="IMixedStreamConfig-getlayoutbyindex"></span>
### getLayoutByIndex

```cpp
virtual MixedStreamLayoutRegionConfig getLayoutByIndex(int32_t index) = 0;
```


> Available since 3.57


Gets the video layout information of the mixed stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int32_t |The number of the view of which you want to get information. |


**Return Value**

Layout information. See [MixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig).

<span id="IMixedStreamConfig-getlayoutregionssize"></span>
### getLayoutRegionsSize

```cpp
virtual int32_t getLayoutRegionsSize() = 0;
```


Get the number of windows in the stream mixing parameter

**Return Value**

The number of windows in the confluence parameter

<span id="IMixedStreamConfig-setlayoutconfig"></span>
### setLayoutConfig

```cpp
virtual void setLayoutConfig(
    MixedStreamLayoutRegionConfig regions[],
    int32_t regions_size
) = 0;
```


Sets the layout configurations.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|regions |MixedStreamLayoutRegionConfig[] |User layout information list. It's a list of [MixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig) that you construct for each stream.<br><br>&nbsp;<br><br>With invalid or empty input, the configurations will be set as the default values. It's recommended to be set. |
|regions_size |int32_t |Amount of views. It's recommended to be set. |


<span id="IMixedStreamConfig-~imixedstreamconfig"></span>
### ~IMixedStreamConfig

```cpp
virtual ~IMixedStreamConfig() = default;
```


<span id="ForwardStreamInfo"></span>
# ForwardStreamInfo

```cpp
struct bytertc::ForwardStreamInfo
```


Information of the rooms where you want to relay the media stream to

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[token](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamInfo-token) |
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamInfo-room_id) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamInfo-token"></span>
### token

```cpp
const char* bytertc::ForwardStreamInfo::token
```


RoomId and UserId are required to generate the Token to forward media streams to the room.

During developing and testing, you can use temporary tokens generated on the console. At the production stage, Tokens are generated by the token generating application deployed on your server.

Forwarding will fail if the token is invalid.

<span id="ForwardStreamInfo-room_id"></span>
### room_id

```cpp
const char* bytertc::ForwardStreamInfo::room_id
```


ID of the room where the media stream aims to relay to

<span id="RecordingFileType"></span>
# RecordingFileType

```cpp
enum bytertc::RecordingFileType
```


Storage format of locally recorded files

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRecordingFileTypeAAC |0 |AAC format file |
|kRecordingFileTypeMP4 |1 |MP4 format file |


<span id="ForwardStreamError"></span>
# ForwardStreamError

```cpp
enum bytertc::ForwardStreamError
```


Error codes during the relaying

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kForwardStreamErrorOK |0 |Normal |
|kForwardStreamErrorInvalidArgument |1201 |Invalid argument |
|kForwardStreamErrorInvalidToken |1202 |Invalid token |
|kForwardStreamErrorResponse |1203 |Error returning from server |
|kForwardStreamErrorRemoteKicked |1204 |Relaying aborts because a user with the same user ID as that of the publisher joins. |
|kForwardStreamErrorNotSupport |1205 |Server denies. |


<span id="MixedStreamRenderMode"></span>
# MixedStreamRenderMode

```cpp
enum bytertc::MixedStreamRenderMode
```


The render mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamRenderModeHidden |1 |(Default) Fill and Crop.<br><br>The video frame is scaled with fixed aspect ratio, until it completely fills the canvas. The region of the video exceeding the canvas will be cropped. |
|kMixedStreamRenderModeFit |2 |Fit.<br><br>The video frame is scaled with fixed aspect ratio, until it fits just within the canvas. Other part of the canvas is filled with the background color. |
|kMixedStreamRenderModeAdaptive |3 |Fill the canvas.<br><br>The video frame is scaled to fill the canvas. During the process, the aspect ratio may change. |


<span id="AudioQuality"></span>
# AudioQuality

```cpp
enum bytertc::AudioQuality
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


<span id="DeviceTransportType"></span>
# DeviceTransportType

```cpp
enum bytertc::DeviceTransportType
```


Connection type of the audio device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kDeviceTransportTypeUnknown |0 |Unknown |
|kDeviceTransportTypeBuiltIn |1 |Built\-in device |
|kDeviceTransportTypeBlueToothUnknownMode |2 |Unknown profile via a Bluetooth connection |
|kDeviceTransportTypeBlueToothHandsFreeMode |3 |Handsfree Profile(HFP) via a Bluetooth connection |
|kDeviceTransportTypeBlueToothStereoMode |4 |Advanced Audio Distribution Profile(A2DP) via a Bluetooth connection |
|kDeviceTransportTypeDisplayAudio |5 |Speaker of the display or television |
|kDeviceTransportTypeVirtual |6 |Virtual sound card |
|kDeviceTransportTypeUSB |7 |USB device |
|kDeviceTransportTypePCI |8 |PCI device |
|kDeviceTransportTypeAirPlay |9 |AirPlay device |
|kDeviceTransportTypeContinuityCamera |100 |Continuity Camera (external iPhone camera) |


<span id="RecordingType"></span>
# RecordingType

```cpp
enum bytertc::RecordingType
```


Locally recorded media type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRecordingTypeAudioOnly |0 |Audio only |
|kRecordingTypeVideoOnly |1 |Video only |
|kRecordingTypeVideoAndAudio |2 |Record audio and video simultaneously |


<span id="RemoteUserPriority"></span>
# RemoteUserPriority

```cpp
enum bytertc::RemoteUserPriority
```


Priority of the publisher. When a user encounters performance insufficiency of either the network or the device, the media stream will fall back in the ascending order of `RemoteUserPriority`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRemoteUserPriorityLow |0 |Low, the default |
|kRemoteUserPriorityMedium |100 |Medium |
|kRemoteUserPriorityHigh |200 |High |


<span id="AudioFormat"></span>
# AudioFormat

```cpp
struct bytertc::AudioFormat
```


Audio format

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|AudioSampleRate |[sample_rate](https://docs.byteplus.com/en/docs/12/14187#AudioFormat-sample_rate) |
|AudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14187#AudioFormat-channel) |
|int |[samples_per_call](https://docs.byteplus.com/en/docs/12/14187#AudioFormat-samples_per_call) |


<span id="instructions"></span>
## Instructions

<span id="AudioFormat-sample_rate"></span>
### sample_rate

```cpp
AudioSampleRate bytertc::AudioFormat::sample_rate = kAudioSampleRateAuto
```


Audio sample rate. See [AudioSampleRate](https://docs.byteplus.com/en/docs/12/14187#AudioSampleRate)

<span id="AudioFormat-channel"></span>
### channel

```cpp
AudioChannel bytertc::AudioFormat::channel = kAudioChannelAuto
```


Audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/14187#AudioChannel)

<span id="AudioFormat-samples_per_call"></span>
### samples_per_call

```cpp
int bytertc::AudioFormat::samples_per_call = 0
```


Samples per audio frame returned by callback. `0` by default. The default samples per callback is the minimum value.

The minimum value is `sampleRate * channel * 0.01s`, the value when the callback interval is 0.01s.

The maximum value is `2048`. If the value is invalid, the samples per callback uses the default value.

This parameter only takes effect when setting the read\-write callback. It does not take effect when calling [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudioframecallback) to enable read\-only callback.

<span id="RoomState"></span>
# RoomState

```cpp
enum bytertc::RoomState
```


Room state code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRoomStateJoinSuccess |0 |Join room success. |
|kRoomStateJoinFailed |1 |Join room failed. |
|kRoomStateLeft |2 |Leave room. |


<span id="InterpolationMode"></span>
# InterpolationMode

```cpp
enum bytertc::InterpolationMode
```


Interpolation mode of the WTN stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kInterpolationModeLastFrameFill |0 |Fill with the last frame. |
|kInterpolationModeBackgroundImageFill |1 |Fill with the background image. |


<span id="ScreenMediaType"></span>
# ScreenMediaType

```cpp
enum bytertc::ScreenMediaType
```


The media type for screen capture

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kScreenMediaTypeVideoOnly |0 |Capture video only |
|kScreenMediaTypeAudioOnly |1 |Capture audio only |
|kScreenMediaTypeVideoAndAudio |2 |Capture Audio and video simultaneously. |


<span id="FrameRateRatio"></span>
# FrameRateRatio

```cpp
enum bytertc::FrameRateRatio
```


Ratio to the original video frame rate of the publisher

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kFrameRateRatioOriginal |0 |100% |
|kFrameRateRatioHalf |1 |50% |
|kFrameRateRatioQuarter |2 |25% |


<span id="StreamInfo"></span>
# StreamInfo

```cpp
struct bytertc::StreamInfo
```


Stream property.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[stream_id](https://docs.byteplus.com/en/docs/12/14187#StreamInfo-stream_id) |
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#StreamInfo-room_id) |
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#StreamInfo-user_id) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#StreamInfo-is_screen) |


<span id="instructions"></span>
## Instructions

<span id="StreamInfo-stream_id"></span>
### stream_id

```cpp
const char* bytertc::StreamInfo::stream_id
```


Stream ID.

<span id="StreamInfo-room_id"></span>
### room_id

```cpp
const char* bytertc::StreamInfo::room_id
```


Room ID.

<span id="StreamInfo-user_id"></span>
### user_id

```cpp
const char* bytertc::StreamInfo::user_id
```


The user ID that published this stream.

<span id="StreamInfo-is_screen"></span>
### is_screen

```cpp
bool bytertc::StreamInfo::is_screen
```


Reserved field. Ignore the value returned in this field.

<span id="CapturePreference"></span>
# CapturePreference

```cpp
enum bytertc::VideoCaptureConfig::CapturePreference
```


Video capture preference

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAuto |0 |(Default) Video capture preference: auto<br><br>SDK determines the best video capture parameters referring to the camera output parameters and the encoder configuration. |
|kManual |1 |Video capture preference: manual<br><br>Set the resolution and the frame rate manually. |
|kAutoPerformance |2 |Video capture preference: encoder configuration<br><br>The capture parameters are the same with the parameters set in [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideoencoderconfig). |


<span id="RtcUser"></span>
# RtcUser

```cpp
struct bytertc::RtcUser
```


User information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[user_id](https://docs.byteplus.com/en/docs/12/14187#RtcUser-user_id) |
|const char\* |[meta_data](https://docs.byteplus.com/en/docs/12/14187#RtcUser-meta_data) |


<span id="instructions"></span>
## Instructions

<span id="RtcUser-user_id"></span>
### user_id

```cpp
const char* bytertc::RtcUser::user_id
```


User id

<span id="RtcUser-meta_data"></span>
### meta_data

```cpp
const char* bytertc::RtcUser::meta_data
```


Metadata

<span id="LocalAudioPropertiesInfo"></span>
# LocalAudioPropertiesInfo

```cpp
struct bytertc::LocalAudioPropertiesInfo
```


Local audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|IAudioSource\* |[audio_source](https://docs.byteplus.com/en/docs/12/14187#LocalAudioPropertiesInfo-audio_source) |
|AudioPropertiesInfo |[audio_properties_info](https://docs.byteplus.com/en/docs/12/14187#LocalAudioPropertiesInfo-audio_properties_info) |


<span id="instructions"></span>
## Instructions

<span id="LocalAudioPropertiesInfo-audio_source"></span>
### audio_source

```cpp
IAudioSource* bytertc::LocalAudioPropertiesInfo::audio_source
```


Audio source

<span id="LocalAudioPropertiesInfo-audio_properties_info"></span>
### audio_properties_info

```cpp
AudioPropertiesInfo bytertc::LocalAudioPropertiesInfo::audio_properties_info
```


See [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesInfo).

<span id="AVSyncEvent"></span>
# AVSyncEvent

```cpp
enum bytertc::AVSyncEvent
```


AVSync events

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAVSyncEventInvalidUidRepeated |0 |A/V synchronization failed.<br><br>Current source audio ID has been set by other video publishers in the same room.<br><br>One single audio source cannot be synchronized with multiple video sources at the same time. |


<span id="ScreenCaptureSourceType"></span>
# ScreenCaptureSourceType

```cpp
enum bytertc::ScreenCaptureSourceType
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

```cpp
enum bytertc::AudioProfileType
```


Sound quality

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioProfileTypeDefault |0 |Default sound quality<br><br>The sound quality configuration of [RoomProfileType](https://docs.byteplus.com/en/docs/12/14187#RoomProfileType) set by the server or client. |
|kAudioProfileTypeFluent |1 |Smooth<br><br>Sample rate: 16 KHz<br><br>Mono\-channel<br><br>Encoding bitrate: 32 Kbps<br><br>Low resource consumption, and small network packets guarantee a smooth call. It is suitable for most game scenarios, such as team\-wide voice chat, group\-wide voice chat, nation\-wide voice chat. |
|kAudioProfileTypeStandard |2 |Mono\-channel standard<br><br>Sample rate: 24 KHz<br><br>Encoding bitrate: 48 Kbps<br><br>For scenarios requiring distinct voice, you can choose this mode, which achieves balanced latency, consumption, and network packets. It is suitable for educational Apps and the online Mafia Games. |
|kAudioProfileTypeHD |3 |Dual\-channel music<br><br>Sample rate: 48 KHz<br><br>Encoding bitrate: 128 Kbps<br><br>This mode provides high\-resolution audio at a cost of high latency, consumption, and large network packets. It is suitable for music Apps such as co\-hosting and online talent contests.<br><br>Not recommended for game Apps. |
|kAudioProfileTypeStandardStereo |4 |Dual\-channel standard<br><br>Sample rate: 48 KHz<br><br>Encoding bitrate: 80 Kbps |
|kAudioProfileTypeHDMono |5 |Mono\-channel music<br><br>Sample rate: 48 KHz<br><br>Encoding bitrate: 64 Kbps |


<span id="UserInfo"></span>
# UserInfo

```cpp
struct bytertc::UserInfo
```


User information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[uid](https://docs.byteplus.com/en/docs/12/14187#UserInfo-uid) |
|const char\* |[extra_info](https://docs.byteplus.com/en/docs/12/14187#UserInfo-extra_info) |


<span id="instructions"></span>
## Instructions

<span id="UserInfo-uid"></span>
### uid

```cpp
const char* bytertc::UserInfo::uid = nullptr
```


User ID. The string matches the regular expression: `[a-zA-Z0-9_\@\\-\\.]{1,128}`.

<span id="UserInfo-extra_info"></span>
### extra_info

```cpp
const char* bytertc::UserInfo::extra_info = nullptr
```


Additional information of the user. The maximum length is 200 bytes. The remote user will receive the info in `onUserJoined`.

<span id="EncryptType"></span>
# EncryptType

```cpp
enum bytertc::EncryptType
```


Custom encryption type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kEncryptTypeNone |0 |No encryption is used. Default value. |
|kEncryptTypeAES128CBC |1 |AES\-128\-CBC encryption algorithm |
|kEncryptTypeAES256CBC |2 |AES\-256\-CBC encryption algorithm |
|kEncryptTypeAES128ECB |3 |AES\-128\-ECB encryption algorithm |
|kEncryptTypeAES256ECB |4 |AES\-256\-ECB encryption algorithm |


<span id="VideoDeviceInfo"></span>
# VideoDeviceInfo

```cpp
struct bytertc::VideoDeviceInfo
```


Video device information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|char[MAX_DEVICE_ID_LENGTH] |[device_id](https://docs.byteplus.com/en/docs/12/14187#VideoDeviceInfo-device_id) |
|char[MAX_DEVICE_ID_LENGTH] |[device_name](https://docs.byteplus.com/en/docs/12/14187#VideoDeviceInfo-device_name) |
|int64_t |[device_vid](https://docs.byteplus.com/en/docs/12/14187#VideoDeviceInfo-device_vid) |
|int64_t |[device_pid](https://docs.byteplus.com/en/docs/12/14187#VideoDeviceInfo-device_pid) |
|DeviceTransportType |[transport_type](https://docs.byteplus.com/en/docs/12/14187#VideoDeviceInfo-transport_type) |
|VideoDeviceFacing |[device_facing](https://docs.byteplus.com/en/docs/12/14187#VideoDeviceInfo-device_facing) |


<span id="instructions"></span>
## Instructions

<span id="VideoDeviceInfo-device_id"></span>
### device_id

```cpp
char bytertc::VideoDeviceInfo::device_id[MAX_DEVICE_ID_LENGTH]
```


Device ID

<span id="VideoDeviceInfo-device_name"></span>
### device_name

```cpp
char bytertc::VideoDeviceInfo::device_name[MAX_DEVICE_ID_LENGTH]
```


Device alias

<span id="VideoDeviceInfo-device_vid"></span>
### device_vid

```cpp
int64_t bytertc::VideoDeviceInfo::device_vid
```


ID of the device vendor

<span id="VideoDeviceInfo-device_pid"></span>
### device_pid

```cpp
int64_t bytertc::VideoDeviceInfo::device_pid
```


Product number of the device

<span id="VideoDeviceInfo-transport_type"></span>
### transport_type

```cpp
DeviceTransportType bytertc::VideoDeviceInfo::transport_type
```


Connection type of the device

<span id="VideoDeviceInfo-device_facing"></span>
### device_facing

```cpp
VideoDeviceFacing bytertc::VideoDeviceInfo::device_facing
```


video device facing type

<span id="RemoteAudioPropertiesInfo"></span>
# RemoteAudioPropertiesInfo

```cpp
struct bytertc::RemoteAudioPropertiesInfo
```


Remote audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[stream_id](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioPropertiesInfo-stream_id) |
|StreamInfo |[stream_info](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioPropertiesInfo-stream_info) |
|AudioPropertiesInfo |[audio_properties_info](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioPropertiesInfo-audio_properties_info) |


<span id="instructions"></span>
## Instructions

<span id="RemoteAudioPropertiesInfo-stream_id"></span>
### stream_id

```cpp
const char* bytertc::RemoteAudioPropertiesInfo::stream_id
```


Stream ID

<span id="RemoteAudioPropertiesInfo-stream_info"></span>
### stream_info

```cpp
StreamInfo bytertc::RemoteAudioPropertiesInfo::stream_info
```


See [StreamInfo](https://docs.byteplus.com/en/docs/12/14187#StreamInfo).

<span id="RemoteAudioPropertiesInfo-audio_properties_info"></span>
### audio_properties_info

```cpp
AudioPropertiesInfo bytertc::RemoteAudioPropertiesInfo::audio_properties_info
```


See [AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesInfo).

<span id="RecordingErrorCode"></span>
# RecordingErrorCode

```cpp
enum bytertc::RecordingErrorCode
```


Error code for local recording

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRecordingErrorCodeOk |0 |Recording normal |
|kRecordingErrorCodeNoPermission |\-1 |No file write permissions |
|kRecordingErrorCodeNotSupport |\-2 |The current version SDK does not support local recording, please contact technical support |
|kRecordingErrorCodeOther |\-3 |Other anomalies |


<span id="AudioMixingDualMonoMode"></span>
# AudioMixingDualMonoMode

```cpp
enum bytertc::AudioMixingDualMonoMode
```


Mix playback channel type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioMixingDualMonoModeAuto |0 |Consistent with audio files |
|kAudioMixingDualMonoModeL |1 |Only the left channel audio in the audio file can be heard |
|kAudioMixingDualMonoModeR |2 |Only the right channel audio in the audio file can be heard |
|kAudioMixingDualMonoModeMix |3 |Can hear the left and right audio channels in the audio file at the same time |


<span id="VideoStreamScaleMode"></span>
# VideoStreamScaleMode

```cpp
enum bytertc::VideoStreamScaleMode
```


Video frame scale mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoStreamScaleModeAuto |0 |Auto mode, default to FitWithCropping. |
|kVideoStreamScaleModeStretch |1 |Stretch the video frame until the video frame and the window have the same resolution. The video frame's aspect ratio can be changed as it is automatically stretched to fill the window, but the whole image is visible. |
|kVideoStreamScaleModeFitWithCropping |2 |Fit the window with cropping<br><br>Scale the video frame uniformly until the window is filled. If the video frame's aspect ratio is different from that of the window, the extra part of the video frame will be cropped.<br><br>After the scaling process is completed, the width or height of the video frame will be consistent with that of the window, and the other dimension will be greater than or equal to that of the window. |
|kVideoStreamScaleModeFitWithFilling |3 |Fit the window with filling<br><br>Scale the video frame uniformly until its width or height reaches the boundary of the window. If the video frame's aspect ratio is different from that of the window, the area that is not filled will be black.<br><br>After the scaling process is completed, the width or height of the video frame will be consistent with that of the window, and the other dimension will be less than or equal to that of the window. |


<span id="AudioPropertiesMode"></span>
# AudioPropertiesMode

```cpp
enum bytertc::AudioPropertiesMode
```


The audio info included in [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalaudiopropertiesreport).

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioPropertiesModeMicrophone |0 |Only locally captured microphone audio info and locally captured screen audio info are included. |
|kAudioPropertiesModeAudioMixing |1 |The following information is included:<br><br><br>&nbsp;<br><br>* Locally captured microphone audio info and locally captured screen audio info;<br><br>* Locally audio mixing info. |


<span id="VideoPictureType"></span>
# VideoPictureType

```cpp
enum bytertc::VideoPictureType
```


Video compression picture type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoPictureTypeUnknown |0 |Unknown type |
|kVideoPictureTypeI |1 |I\-frames, key frames which are coded without reference to any other frame. |
|kVideoPictureTypeP |2 |P\-frames, forward\-predicted frames which are coded by a forward predictive coding method. |
|kVideoPictureTypeB |3 |B\-frames, bi\-directionally predicted frames which are coded by both forward and backward predictive coding method. |


<span id="AudioMixingError"></span>
# AudioMixingError

```cpp
enum bytertc::AudioMixingError
```


Error code for audio mixing

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioMixingErrorOk |0 |OK |
|kAudioMixingErrorPreloadFailed |1 |Preload failed. Invalid path or the length exceeds 20s. |
|kAudioMixingErrorStartFailed |2 |Mixing failed. Invalid path or fail to open the file. |
|kAudioMixingErrorIdNotFound |3 |Invalid mixID |
|kAudioMixingErrorSetPositionFailed |4 |Invalid position |
|kAudioMixingErrorInValidVolume |5 |Invalid volume. The range is [0, 400]. |
|kAudioMixingErrorLoadConflict |6 |Another file was preloaded for mixing. Call unloadAudioMixing first. |
|kAudioMixingErrorIdTypeNotMatch |7 |Do not support the mix type. |
|kAudioMixingErrorInValidPitch |8 |Invalid pitch value. |
|kAudioMixingErrorInValidAudioTrack |9 |Invalid audio track. |
|kAudioMixingErrorIsStarting |10 |Mixing starting |
|kAudioMixingErrorInValidPlaybackSpeed |11 |Invalid playback speed |
|[deprecated] kAudioMixingErrorCanNotOpen |701 |`Deprecated since 3.45 and will be deleted in 3.51`<br><br>Audio mixing error code. Deprecated. |


<span id="ZoomDirectionType"></span>
# ZoomDirectionType

```cpp
enum bytertc::ZoomDirectionType
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


<span id="WTNSubscribeStateChangeReason"></span>
# WTNSubscribeStateChangeReason

```cpp
enum bytertc::WTNSubscribeStateChangeReason
```


Reasons for change in WTN media stream's Subscription Status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kWTNSubscribeStateChangeReasonSubscribe |0 |Subscribe WTN media stream successfully |
|kWTNSubscribeStateChangeReasonUnsubscribe |1300 |Failed to subscribe WTN media stream for other reasons. |
|kWTNSubscribeStateChangeReasonRemoteUnpublish |1301 |Failed to subscribe because the remote end did not publish. |
|kWTNSubscribeStateChangeReasonOverClientSubscribeStreamLimit |1310 |Failed to subscribe because the single\-end subscription limit has been exceeded. An engine instance can pull a maximum of 5 streams. |
|kWTNSubscribeStateChangeReasonOverStreamSubscribeUserLimit |1311 |Failed to subscribe because the single\-stream subscription limit has been exceeded. The limit is set by RTC server. |
|kWTNSubscribeStateChangeReasonOverStreamSubscribeRequestLimit |1312 |Failed to subscribe because the limit of the single\-stream subscription request has been exceeded. The limit is set by RTC server. |


<span id="SingleStreamPushType"></span>
# SingleStreamPushType

```cpp
enum bytertc::SingleStreamPushType
```


Single stream push type, specifying whether to push the media stream to CDN or RTC room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPushToCDN |1 |Push to CDN |
|kPushToRTC |2 |Push to RTC room |


<span id="MediaPlayerCustomSourceMode"></span>
# MediaPlayerCustomSourceMode

```cpp
enum bytertc::MediaPlayerCustomSourceMode
```


Custom audio source mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaPlayerCustomSourceModePush |0 |When you use the local PCM data, use this mode. |
|kMediaPlayerCustomSourceModePull |1 |When you use the audio data from local memory, use this mode. |


<span id="VideoSourceType"></span>
# VideoSourceType

```cpp
enum bytertc::VideoSourceType
```


Video source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoSourceTypeExternal |0 |Custom video source |
|kVideoSourceTypeInternal |1 |Internal video capture |
|kVideoSourceTypeEncodedWithAutoSimulcast |2 |Custom encoded video source.<br><br>Push the encoded video stream with the largest resolution, and the SDK will automatically transcode to generate multiple lower\-quality streams for Simulcast. |
|kVideoSourceTypeEncodedWithoutAutoSimulcast |3 |Custom encoded video source.<br><br>The SDK does not automatically generate multiple streams for Simulcast, you need to generate and push streams of different qualities. |


<span id="StreamIndex-2"></span>
# StreamIndex

```cpp
enum bytertc::streamingrtc::StreamIndex
```


Stream index, which is used to identify different streams affiliated with the same user， such as the left\-eye/right\-eye stream in a 3D video. Another example is the video stream captured by the camera or the screen recorder.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kStreamIndexIndex0 |0 |Stream index 0 |
|kStreamIndexIndex1 |1 |Steam index 1 |


<span id="AudioProcessorMethod"></span>
# AudioProcessorMethod

```cpp
enum bytertc::AudioProcessorMethod
```


The audio input for the audio processor.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioProcessorMethodRecord |0 |Locally captured audio frame. |
|kAudioProcessorMethodPlayback |1 |The mixed remote audio. |
|kAudioProcessorMethodRemoteUser |2 |The audio streams from remote users. |
|kAudioProcessorMethodScreen |4 |The shared\-screen audio. |


<span id="VideoSimulcastMode"></span>
# VideoSimulcastMode

```cpp
enum bytertc::VideoSimulcastMode
```


Multiple quality streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kVideoSimulcastModeOnlyOne |0 |Single. The video stream is sent in only set of specification. |
|kVideoSimulcastModeOnDemand |1 |On\-demand. The publisher will publish streams according to the subscriber's demands. When no subscription preference is taking effect, 2 streams will be published. |
|kVideoSimulcastModeAlwaysSimulcast |2 |Manual. The publisher will publish streams in the qualities of the settings. The default is to publish 2 streams. |


<span id="AudioChannel"></span>
# AudioChannel

```cpp
enum bytertc::AudioChannel
```


Audio channel

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioChannelAuto |\-1 |Default value. |
|kAudioChannelMono |1 |Mono channel. |
|kAudioChannelStereo |2 |Dual channels. |


<span id="AudioFormatType"></span>
# AudioFormatType

```cpp
enum class bytertc::AudioFormatType
```


Audio input format type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRawPCMs16 |0 |PCM_S16 |
|kRawPCMs32 |1 |PCM_S32 |


<span id="MirrorType"></span>
# MirrorType

```cpp
enum bytertc::MirrorType
```


Mirror type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMirrorTypeNone |0 |The preview and the published video stream are not mirrored. |
|kMirrorTypeRender |1 |The preview is mirrored. The published video stream is not mirrored. |
|kMirrorTypeEncoder |2 |The preview is not mirrored; only the published video stream is mirrored. |
|kMirrorTypeRenderAndEncoder |3 |The preview and the published video stream are mirrored. |


<span id="StreamLayoutMode"></span>
# StreamLayoutMode

```cpp
enum bytertc::StreamLayoutMode
```


Layout mode of the WTN stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kStreamLayoutModeAuto |0 |Auto |
|kStreamLayoutModeCustom |2 |Manual |


<span id="VideoCaptureConfig"></span>
# VideoCaptureConfig

```cpp
struct bytertc::VideoCaptureConfig
```


Video capture configuration parameters.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CapturePreference |[capture_preference](https://docs.byteplus.com/en/docs/12/14187#VideoCaptureConfig-capture_preference) |
|int |[width](https://docs.byteplus.com/en/docs/12/14187#VideoCaptureConfig-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#VideoCaptureConfig-height) |
|int |[frame_rate](https://docs.byteplus.com/en/docs/12/14187#VideoCaptureConfig-frame_rate) |


<span id="instructions"></span>
## Instructions

<span id="VideoCaptureConfig-capture_preference"></span>
### capture_preference

```cpp
CapturePreference bytertc::VideoCaptureConfig::capture_preference = CapturePreference::kAuto
```


Video capture preference. See [CapturePreference](https://docs.byteplus.com/en/docs/12/14187#capturepreference).

<span id="VideoCaptureConfig-width"></span>
### width

```cpp
int bytertc::VideoCaptureConfig::width = 0
```


The width of video capture resolution in px.

<span id="VideoCaptureConfig-height"></span>
### height

```cpp
int bytertc::VideoCaptureConfig::height = 0
```


The height of video capture resolution in px.

<span id="VideoCaptureConfig-frame_rate"></span>
### frame_rate

```cpp
int bytertc::VideoCaptureConfig::frame_rate = 0
```


Video capture frame rate in fps.

<span id="LogoutReason"></span>
# LogoutReason

```cpp
enum bytertc::LogoutReason
```


The reason why users log out

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLogoutReasonLogout |0 |Users choose to sign out by calling `logout` or terminating the engine. |
|kLogoutReasonDuplicateLogin |1 |The current user is kicked out as another user signs in with the same user ID. |


<span id="UserOfflineReason"></span>
# UserOfflineReason

```cpp
enum bytertc::UserOfflineReason
```


The reason why the user left the room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kUserOfflineReasonQuit |0 |The remote user calls `leaveRoom` to exit the room. |
|kUserOfflineReasonDropped |1 |The remote user is offline. |
|kUserOfflineReasonSwitchToInvisible |2 |The remote user switches to invisible. |
|kUserOfflineReasonKickedByAdmin |3 |The remote user is kicked out of the room.<br><br>Is kicked out of the room due to calling the OpenAPI to kick out the user. |


<span id="SubscribeVideoConfig"></span>
# SubscribeVideoConfig

```cpp
struct bytertc::SubscribeVideoConfig
```


Video subscription configuration information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[video_index](https://docs.byteplus.com/en/docs/12/14187#SubscribeVideoConfig-video_index) |
|int |[priority](https://docs.byteplus.com/en/docs/12/14187#SubscribeVideoConfig-priority) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeVideoConfig-video_index"></span>
### video_index

```cpp
int bytertc::SubscribeVideoConfig::video_index = 0
```


Subscribed video stream resolution subscript.

In Simulcast mode, use a number to specify the expected quality of the video stream to be subscribed to. In Simulcast mode, a video has multiple encoded qualities ranging from 0 to 3. Call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideoencoderconfig) to enable Simulcast mode on the publisher's clients.

Ranging from \-1 to 3

0 (Default): The best quality

\-1: Use the previous settings.

<span id="SubscribeVideoConfig-priority"></span>
### priority

```cpp
int bytertc::SubscribeVideoConfig::priority = 0
```


Remote user priority. The default value is 0. Refer to [RemoteUserPriority](https://docs.byteplus.com/en/docs/12/14187#RemoteUserPriority) for more details.

<span id="PublishFallbackOption"></span>
# PublishFallbackOption

```cpp
enum bytertc::PublishFallbackOption
```


Stream fallback options of publisher

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPublishFallbackOptionDisabled |0 |Default setting. No fallback is allowed under limited network conditions. |
|kPublishFallbackOptionSimulcast |1 |Under limited network conditions, the video streams that you published will degrade sequentially from the highest\-quality stream to the lowest\-quality stream until it can match current network conditions. |


<span id="MixedStreamSpatialAudioConfig"></span>
# MixedStreamSpatialAudioConfig

```cpp
struct bytertc::MixedStreamSpatialAudioConfig
```


Spatial audio config when pushing to CDN.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[enable_spatial_render](https://docs.byteplus.com/en/docs/12/14187#MixedStreamSpatialAudioConfig-enable_spatial_render) |
|Position |[audience_spatial_position](https://docs.byteplus.com/en/docs/12/14187#MixedStreamSpatialAudioConfig-audience_spatial_position) |
|HumanOrientation |[audience_spatial_orientation](https://docs.byteplus.com/en/docs/12/14187#MixedStreamSpatialAudioConfig-audience_spatial_orientation) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamSpatialAudioConfig-enable_spatial_render"></span>
### enable_spatial_render

```cpp
bool bytertc::MixedStreamSpatialAudioConfig::enable_spatial_render
```


Whether to enable the spatial audio effect when pushing to CDN.

**Notes**

when you enable the feature, set the `spatial_position` of each [MixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionConfig) for spatial audio effect.

<span id="MixedStreamSpatialAudioConfig-audience_spatial_position"></span>
### audience_spatial_position

```cpp
Position bytertc::MixedStreamSpatialAudioConfig::audience_spatial_position
```


The spatial position of the audience. See [Position](https://docs.byteplus.com/en/docs/12/14187#Position).

The audience is the users who receive the audio stream from CDN.

This parameter is not supported for WTN stream tasks.

<span id="MixedStreamSpatialAudioConfig-audience_spatial_orientation"></span>
### audience_spatial_orientation

```cpp
HumanOrientation bytertc::MixedStreamSpatialAudioConfig::audience_spatial_orientation
```


The orientation of the audience. See [HumanOrientation](https://docs.byteplus.com/en/docs/12/14187#HumanOrientation).

The audience is the users who receive the audio stream from CDN.

<span id="LocalStreamStats"></span>
# LocalStreamStats

```cpp
struct bytertc::LocalStreamStats
```


Local audio/video stream statistics and network status, the reference period is 2s.

After the local user publishes the audio/video stream successfully, the SDK will periodically notify the local user through `onLocalStreamStats`

The transmission status of the published audio/video stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|LocalAudioStats |[audio_stats](https://docs.byteplus.com/en/docs/12/14187#LocalStreamStats-audio_stats) |
|LocalVideoStats |[video_stats](https://docs.byteplus.com/en/docs/12/14187#LocalStreamStats-video_stats) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#LocalStreamStats-is_screen) |
|NetworkQuality |[deprecated] [local_tx_quality](https://docs.byteplus.com/en/docs/12/14187#LocalStreamStats-local_tx_quality) |
|NetworkQuality |[deprecated] [local_rx_quality](https://docs.byteplus.com/en/docs/12/14187#LocalStreamStats-local_rx_quality) |


<span id="instructions"></span>
## Instructions

<span id="LocalStreamStats-audio_stats"></span>
### audio_stats

```cpp
LocalAudioStats bytertc::LocalStreamStats::audio_stats
```


For statistics on audio streams sent by local devices. See [LocalAudioStats](https://docs.byteplus.com/en/docs/12/14187#LocalAudioStats)

<span id="LocalStreamStats-video_stats"></span>
### video_stats

```cpp
LocalVideoStats bytertc::LocalStreamStats::video_stats
```


For statistics on video streams sent by local devices. See [LocalVideoStats](https://docs.byteplus.com/en/docs/12/14187#LocalVideoStats)

<span id="LocalStreamStats-is_screen"></span>
### is_screen

```cpp
bool bytertc::LocalStreamStats::is_screen
```


Reserved field. Ignore the value returned in this field.

<span id="LocalStreamStats-local_tx_quality"></span>
### local_tx_quality

```cpp
NetworkQuality bytertc::LocalStreamStats::local_tx_quality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onnetworkquality) instead.


For the media stream uplink network quality of the user you belong to. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14187#NetworkQuality)

<span id="LocalStreamStats-local_rx_quality"></span>
### local_rx_quality

```cpp
NetworkQuality bytertc::LocalStreamStats::local_rx_quality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onnetworkquality) instead.


The downlink network quality of the media stream belongs to the user. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14187#NetworkQuality)

<span id="EngineConfig-2"></span>
# EngineConfig

```cpp
struct bytertc::streamingrtc::EngineConfig
```


Configuration of the Streaming Engine

The client and server use the port range in the following ways.

kP2PRoleServer: The engine waits for connection establishment by listening to the first available port from `server_port_min` to `server_port_max`.

kP2PRoleClient: The engine tries to connect to a server by connecting to `server_ip` with the port number from `server_port_min` to `server_port_max` until the connection establishment.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[app_id](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-app_id) |
|P2PRole |[role](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-role) |
|const char\* |[server_ip](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-server_ip) |
|int |[server_port_min](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-server_port_min) |
|int |[server_port_max](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-server_port_max) |


<span id="instructions"></span>
## Instructions

<span id="EngineConfig-app_id-2"></span>
### app_id

```cpp
const char* bytertc::streamingrtc::EngineConfig::app_id = nullptr
```


A unique identifier for each App. Instances generated with different RTC AppIDs are isolated from each other in audio/video calls. That is, users cannot communicate with the ones using the App created with a different AppID.

<span id="EngineConfig-role"></span>
### role

```cpp
P2PRole bytertc::streamingrtc::EngineConfig::role = kP2PRoleClient
```


Role of the streaming Engine. Refer to [P2PRole](https://docs.byteplus.com/en/docs/12/14187#P2PRole) for more details.

<span id="EngineConfig-server_ip"></span>
### server_ip

```cpp
const char* bytertc::streamingrtc::EngineConfig::server_ip = nullptr
```


IP address of the server, required when the role is set to `kP2PRoleClient`.

<span id="EngineConfig-server_port_min"></span>
### server_port_min

```cpp
int bytertc::streamingrtc::EngineConfig::server_port_min = 50000
```


The lower limit of range of the port numbers

<span id="EngineConfig-server_port_max"></span>
### server_port_max

```cpp
int bytertc::streamingrtc::EngineConfig::server_port_max = 50004
```


The upper limit of range of the port numbers

<span id="MixedStreamLayoutRegionImageWaterMarkConfig"></span>
# MixedStreamLayoutRegionImageWaterMarkConfig

```cpp
struct bytertc::MixedStreamLayoutRegionImageWaterMarkConfig
```


Resolution of the watermark image.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[image_width](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionImageWaterMarkConfig-image_width) |
|int |[image_height](https://docs.byteplus.com/en/docs/12/14187#MixedStreamLayoutRegionImageWaterMarkConfig-image_height) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamLayoutRegionImageWaterMarkConfig-image_width"></span>
### image_width

```cpp
int bytertc::MixedStreamLayoutRegionImageWaterMarkConfig::image_width = 0
```


Width of the original image in px.

<span id="MixedStreamLayoutRegionImageWaterMarkConfig-image_height"></span>
### image_height

```cpp
int bytertc::MixedStreamLayoutRegionImageWaterMarkConfig::image_height = 0
```


Height of the original image in px.

<span id="VoiceReverbConfig"></span>
# VoiceReverbConfig

```cpp
struct bytertc::VoiceReverbConfig
```


Voice reverb effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[room_size](https://docs.byteplus.com/en/docs/12/14187#VoiceReverbConfig-room_size) |
|float |[decay_time](https://docs.byteplus.com/en/docs/12/14187#VoiceReverbConfig-decay_time) |
|float |[damping](https://docs.byteplus.com/en/docs/12/14187#VoiceReverbConfig-damping) |
|float |[wet_gain](https://docs.byteplus.com/en/docs/12/14187#VoiceReverbConfig-wet_gain) |
|float |[dry_gain](https://docs.byteplus.com/en/docs/12/14187#VoiceReverbConfig-dry_gain) |
|float |[pre_delay](https://docs.byteplus.com/en/docs/12/14187#VoiceReverbConfig-pre_delay) |


<span id="instructions"></span>
## Instructions

<span id="VoiceReverbConfig-room_size"></span>
### room_size

```cpp
float bytertc::VoiceReverbConfig::room_size = 50.0f
```


The room size for reverb simulation. The range is `[0.0, 100.0]`. The default value is `50.0f`. The larger the room, the stronger the reverberation.

<span id="VoiceReverbConfig-decay_time"></span>
### decay_time

```cpp
float bytertc::VoiceReverbConfig::decay_time = 50.0f
```


The decay time of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="VoiceReverbConfig-damping"></span>
### damping

```cpp
float bytertc::VoiceReverbConfig::damping = 50.0f
```


The damping index of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="VoiceReverbConfig-wet_gain"></span>
### wet_gain

```cpp
float bytertc::VoiceReverbConfig::wet_gain = 0.0f
```


The intensity of the wet signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="VoiceReverbConfig-dry_gain"></span>
### dry_gain

```cpp
float bytertc::VoiceReverbConfig::dry_gain = 0.0f
```


The Intensity of the dry signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="VoiceReverbConfig-pre_delay"></span>
### pre_delay

```cpp
float bytertc::VoiceReverbConfig::pre_delay = 0.0f
```


The delay of the wet signal in ms. The range is `[0.0, 200.0]`. The default value is `0.0f`.

<span id="AttenuationType"></span>
# AttenuationType

```cpp
enum bytertc::AttenuationType
```


Volume Roll\-off modes that a sound has in an audio source

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAttenuationTypeNone |0 |Disable Volume Attenuation |
|kAttenuationTypeLinear |1 |Linear roll\-off mode which lowers the volume of the sound over the distance |
|kAttenuationTypeExponential |2 |Exponential roll\-off mode which exponentially decreases the volume of the sound with the distance raising |


<span id="StreamSyncInfoConfig"></span>
# StreamSyncInfoConfig

```cpp
struct bytertc::StreamSyncInfoConfig
```


Configuration related to media stream information synchronization

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[repeat_count](https://docs.byteplus.com/en/docs/12/14187#StreamSyncInfoConfig-repeat_count) |
|SyncInfoStreamType |[stream_type](https://docs.byteplus.com/en/docs/12/14187#StreamSyncInfoConfig-stream_type) |


<span id="instructions"></span>
## Instructions

<span id="StreamSyncInfoConfig-repeat_count"></span>
### repeat_count

```cpp
int bytertc::StreamSyncInfoConfig::repeat_count
```


The number of duplicates sent by the message, the value range is [0,25], it is recommended to set it to [3,5].

<span id="StreamSyncInfoConfig-stream_type"></span>
### stream_type

```cpp
SyncInfoStreamType bytertc::StreamSyncInfoConfig::stream_type
```


Stream types for media stream information synchronization. See [SyncInfoStreamType](https://docs.byteplus.com/en/docs/12/14187#SyncInfoStreamType)

<span id="MixedStreamVideoType"></span>
# MixedStreamVideoType

```cpp
enum bytertc::MixedStreamVideoType
```


Reserved field.

<span id="AlphaLayout"></span>
# AlphaLayout

```cpp
enum bytertc::AlphaLayout
```


The arrangement position of the Alpha channel relative to the RGB channel data.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAlphaLayoutTop |0 |Alpha data is placed above the RGB data. |


<span id="Orientation"></span>
# Orientation

```cpp
struct bytertc::Orientation
```


Direction Orientation Information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/14187#Orientation-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/14187#Orientation-y) |
|float |[z](https://docs.byteplus.com/en/docs/12/14187#Orientation-z) |


<span id="instructions"></span>
## Instructions

<span id="Orientation-x"></span>
### x

```cpp
float bytertc::Orientation::x
```


X\-coordinate

<span id="Orientation-y"></span>
### y

```cpp
float bytertc::Orientation::y
```


Y\-coordinate

<span id="Orientation-z"></span>
### z

```cpp
float bytertc::Orientation::z
```


Z\-coordinate

<span id="HighlightConfig"></span>
# HighlightConfig

```cpp
struct bytertc::HighlightConfig
```


Configure how a border is highlighted when you share your screen.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[enable_highlight](https://docs.byteplus.com/en/docs/12/14187#HighlightConfig-enable_highlight) |
|uint32_t |[border_color](https://docs.byteplus.com/en/docs/12/14187#HighlightConfig-border_color) |
|int |[border_width](https://docs.byteplus.com/en/docs/12/14187#HighlightConfig-border_width) |


<span id="instructions"></span>
## Instructions

<span id="HighlightConfig-enable_highlight"></span>
### enable_highlight

```cpp
bool bytertc::HighlightConfig::enable_highlight = true
```


Whether to display a highlighted border. A border is highlighted by default.

<span id="HighlightConfig-border_color"></span>
### border_color

```cpp
uint32_t bytertc::HighlightConfig::border_color = 0xFF29CCA3
```


Color(ARGB format: 0xAARRGGBB).

<span id="HighlightConfig-border_width"></span>
### border_width

```cpp
int bytertc::HighlightConfig::border_width = 4
```


Width(in pixel).

<span id="RoomEventInfo"></span>
# RoomEventInfo

```cpp
struct bytertc::RoomEventInfo
```


Room event info.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int64_t |[forbidden_time](https://docs.byteplus.com/en/docs/12/14187#RoomEventInfo-forbidden_time) |


<span id="instructions"></span>
## Instructions

<span id="RoomEventInfo-forbidden_time"></span>
### forbidden_time

```cpp
int64_t bytertc::RoomEventInfo::forbidden_time = 0
```


When the room or user is forbidden, notice forbidden time.

<span id="LocalLogLevel"></span>
# LocalLogLevel

```cpp
enum class bytertc::LocalLogLevel
```


Local log parameters.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kInfo |0 |Info level. |
|kWarning |1 |(Default) Warning level. |
|kError |2 |Error level. |
|kNone |3 |Turn off logging. |


<span id="FirstFrameSendState"></span>
# FirstFrameSendState

```cpp
enum bytertc::FirstFrameSendState
```


First frame sending status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kFirstFrameSendStateSending |0 |Sending |
|kFirstFrameSendStateSent |1 |Sent successfully |
|kFirstFrameSendStateEnd |2 |Send failed |


<span id="AudioDumpStatus"></span>
# AudioDumpStatus

```cpp
enum bytertc::AudioDumpStatus
```


Audio dump status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioDumpStatusStartFailure |0 |audio dump start failure |
|kAudioDumpStatusStartSuccess |1 |audio dump start success |
|kAudioDumpStatusStopFailure |2 |audio dump stop failure |
|kAudioDumpStatusStopSuccess |3 |audio dump stop success |
|kAudioDumpStatusRunningFailure |4 |audio dump running failure |
|kAudioDumpStatusRunningSuccess |5 |audio dump running success |


<span id="MixedStreamTaskInfo"></span>
# MixedStreamTaskInfo

```cpp
struct bytertc::MixedStreamTaskInfo
```


Detailed information of the stream mixing task.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[task_id](https://docs.byteplus.com/en/docs/12/14187#MixedStreamTaskInfo-task_id) |
|MixedStreamPushTargetType |[push_target_type](https://docs.byteplus.com/en/docs/12/14187#MixedStreamTaskInfo-push_target_type) |


<span id="instructions"></span>
## Instructions

<span id="MixedStreamTaskInfo-task_id"></span>
### task_id

```cpp
const char* bytertc::MixedStreamTaskInfo::task_id
```


Task ID

For WTN stream task, this value represents the WTN stream ID. You can subscribe to a WTN stream by specifying the ID.

<span id="MixedStreamTaskInfo-push_target_type"></span>
### push_target_type

```cpp
MixedStreamPushTargetType bytertc::MixedStreamTaskInfo::push_target_type
```


Task type: Pushing a mixing stream to CDN or starting a WTN stream.

<span id="SubscribeConfig"></span>
# SubscribeConfig

```cpp
struct bytertc::SubscribeConfig
```


Configuration information for manual subscription flows.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-is_screen) |
|bool |[sub_video](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-sub_video) |
|bool |[sub_audio](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-sub_audio) |
|int |[video_index](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-video_index) |
|int |[priority](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-priority) |
|int |[svc_layer](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-svc_layer) |
|int |[framerate](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-framerate) |
|int |[sub_width](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-sub_width) |
|int |[sub_height](https://docs.byteplus.com/en/docs/12/14187#SubscribeConfig-sub_height) |


<span id="instructions"></span>
## Instructions

<span id="SubscribeConfig-is_screen"></span>
### is_screen

```cpp
bool bytertc::SubscribeConfig::is_screen = false
```


Reserved field. Do not set this field in the single\-stream SDK.

<span id="SubscribeConfig-sub_video"></span>
### sub_video

```cpp
bool bytertc::SubscribeConfig::sub_video
```


Whether to subscribe to videos.

<span id="SubscribeConfig-sub_audio"></span>
### sub_audio

```cpp
bool bytertc::SubscribeConfig::sub_audio
```


Whether to subscribe to audio.

<span id="SubscribeConfig-video_index"></span>
### video_index

```cpp
int bytertc::SubscribeConfig::video_index
```


Subscribed video stream resolution subscript.

Users can publish multiple videos of different resolutions in a stream by calling the [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideoencoderconfig) method. Therefore, when subscribing to a stream, you need to specify the specific resolution of the subscription. This parameter is used to specify the subscript of the resolution to be subscribed to, and the default value is 0.

<span id="SubscribeConfig-priority"></span>
### priority

```cpp
int bytertc::SubscribeConfig::priority = 0
```


For the remote user's requirement priority. See [RemoteUserPriority](https://docs.byteplus.com/en/docs/12/14187#RemoteUserPriority), the default value is 0.

When the subscription flow fallback option function is turned on (see [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setsubscribefallbackoption) method for details), weak connections or insufficient performance will give priority to ensuring the quality of the received high\-priority user's flow.

<span id="SubscribeConfig-svc_layer"></span>
### svc_layer

```cpp
int bytertc::SubscribeConfig::svc_layer = 0
```


The time domain hierarchy of the remote user. See [SVCLayer](https://docs.byteplus.com/en/docs/12/14187#SVCLayer), the default value is 0.

This only works if the stream supports the SVC feature.

<span id="SubscribeConfig-framerate"></span>
### framerate

```cpp
int bytertc::SubscribeConfig::framerate = 0
```


Expected maximum frame rate of the subscribed stream in fps. The default value is 0, values greater than 10 are valid.

If the frame rate of the stream published is higher than the value set by the subscriber, the subscriber receives the video of the frame rate set by this API; if the frame rate of the stream published is lower than the value set by the subscriber, the subscriber receives the video of the same frame rate of the video published.

Only valid if the stream is coded with SVC technique.

<span id="SubscribeConfig-sub_width"></span>
### sub_width

```cpp
int bytertc::SubscribeConfig::sub_width = 0
```


The user specifies the width (px) of the most appropriate stream corresponding to the UI

<span id="SubscribeConfig-sub_height"></span>
### sub_height

```cpp
int bytertc::SubscribeConfig::sub_height = 0
```


The user specifies the height(px) of the most appropriate stream corresponding to the UI by specifying

<span id="EngineConfig"></span>
# EngineConfig

```cpp
struct bytertc::EngineConfig
```


Create engine parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[app_id](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-app_id) |
|const char\* |[parameters](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-parameters) |
|const char\* |[native_load_path](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-native_load_path) |
|void\* |[j_application_context](https://docs.byteplus.com/en/docs/12/14187#EngineConfig-j_application_context) |


<span id="instructions"></span>
## Instructions

<span id="EngineConfig-app_id"></span>
### app_id

```cpp
const char* bytertc::EngineConfig::app_id = nullptr
```


The unique identifier of each app. Only instances generated with the same app_id can communicate.

<span id="EngineConfig-parameters"></span>
### parameters

```cpp
const char* bytertc::EngineConfig::parameters = nullptr
```


Please contact the technical support personnel.

<span id="EngineConfig-native_load_path"></span>
### native_load_path

```cpp
const char* bytertc::EngineConfig::native_load_path = nullptr
```


Custom plugin dynamic library loading directory. Only supported on Android platform.

<span id="EngineConfig-j_application_context"></span>
### j_application_context

```cpp
void* bytertc::EngineConfig::j_application_context = nullptr
```


The context of the Android application (Application Context), only supported on Android platform.

<span id="MouseCursorCaptureState"></span>
# MouseCursorCaptureState

```cpp
enum bytertc::MouseCursorCaptureState
```


Whether to capture the mouse cursor when capturing screen streams by RTC.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMouseCursorCaptureStateOn |0 |Yes. |
|kMouseCursorCaptureStateOff |1 |No. |


<span id="VirtualBackgroundSourceType"></span>
# VirtualBackgroundSourceType

```cpp
enum bytertc::VirtualBackgroundSourceType
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

```cpp
enum bytertc::NetworkType
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


<span id="StandardPitchInfo"></span>
# StandardPitchInfo

```cpp
struct bytertc::StandardPitchInfo
```


Standard pitch data

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[start_time](https://docs.byteplus.com/en/docs/12/14187#StandardPitchInfo-start_time) |
|int |[duration](https://docs.byteplus.com/en/docs/12/14187#StandardPitchInfo-duration) |
|int |[pitch](https://docs.byteplus.com/en/docs/12/14187#StandardPitchInfo-pitch) |


<span id="instructions"></span>
## Instructions

<span id="StandardPitchInfo-start_time"></span>
### start_time

```cpp
int bytertc::StandardPitchInfo::start_time
```


Starting time, unit: ms.

<span id="StandardPitchInfo-duration"></span>
### duration

```cpp
int bytertc::StandardPitchInfo::duration
```


Duration, unit: ms.

<span id="StandardPitchInfo-pitch"></span>
### pitch

```cpp
int bytertc::StandardPitchInfo::pitch
```


pitch.

<span id="MediaPlayerCustomSourceStreamType"></span>
# MediaPlayerCustomSourceStreamType

```cpp
enum bytertc::MediaPlayerCustomSourceStreamType
```


Custom audio source stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMediaPlayerCustomSourceStreamTypeRaw |0 |When you use the local PCM data, use this type. |
|kMediaPlayerCustomSourceStreamTypeEncoded |1 |When you use the audio data from local memory, use this type. |


<span id="AudioRoomConfig"></span>
# AudioRoomConfig

```cpp
struct bytertc::AudioRoomConfig
```


Multi\-room parameter configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|RoomProfileType |[room_profile_type](https://docs.byteplus.com/en/docs/12/14187#AudioRoomConfig-room_profile_type) |
|bool |[is_auto_subscribe_audio](https://docs.byteplus.com/en/docs/12/14187#AudioRoomConfig-is_auto_subscribe_audio) |
|bool |[is_auto_publish_audio](https://docs.byteplus.com/en/docs/12/14187#AudioRoomConfig-is_auto_publish_audio) |


<span id="instructions"></span>
## Instructions

<span id="AudioRoomConfig-room_profile_type"></span>
### room_profile_type

```cpp
RoomProfileType bytertc::AudioRoomConfig::room_profile_type = kRoomProfileTypeCommunication
```


Room profile. See [RoomProfileType](https://docs.byteplus.com/en/docs/12/14187#RoomProfileType). The default is `kRoomProfileTypeCommunication`. The setting cannot be changed after joining the room.

<span id="AudioRoomConfig-is_auto_subscribe_audio"></span>
### is_auto_subscribe_audio

```cpp
bool bytertc::AudioRoomConfig::is_auto_subscribe_audio = true
```


Whether to automatically subscribe to the audio stream. The default is automatic subscription.

<span id="AudioRoomConfig-is_auto_publish_audio"></span>
### is_auto_publish_audio

```cpp
bool bytertc::AudioRoomConfig::is_auto_publish_audio = true
```


Whether to publish media streams automatically. The default is automatic publishing.


* Changing the user role to audience via `setUserVisibility` will void this setting.

* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only.

    &nbsp;


<span id="rtcroomconfig"></span>
# RTCRoomConfig

```cpp
struct bytertc::RTCRoomConfig
```


Room configuration. A room is an abstract concept for an RTC call. Users can interact with each other in the same room.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|RoomProfileType |[room_profile_type](https://docs.byteplus.com/en/docs/12/14187#RTCRoomConfig-room_profile_type) |
|RoomLiveMode |[live_mode](https://docs.byteplus.com/en/docs/12/14187#RTCRoomConfig-live_mode) |
|const char\* |[stream_id](https://docs.byteplus.com/en/docs/12/14187#RTCRoomConfig-stream_id) |
|bool |[is_auto_publish_audio](https://docs.byteplus.com/en/docs/12/14187#RTCRoomConfig-is_auto_publish_audio) |
|bool |[is_auto_publish_video](https://docs.byteplus.com/en/docs/12/14187#RTCRoomConfig-is_auto_publish_video) |
|bool |[is_auto_subscribe_audio](https://docs.byteplus.com/en/docs/12/14187#RTCRoomConfig-is_auto_subscribe_audio) |
|bool |[is_auto_subscribe_video](https://docs.byteplus.com/en/docs/12/14187#RTCRoomConfig-is_auto_subscribe_video) |


<span id="instructions"></span>
## Instructions

<span id="RTCRoomConfig-room_profile_type"></span>
### room_profile_type

```cpp
RoomProfileType bytertc::RTCRoomConfig::room_profile_type = kRoomProfileTypeCommunication
```


Room profile. See [RoomProfileType](https://docs.byteplus.com/en/docs/12/14187#RoomProfileType). The default is `kRoomProfileTypeCommunication`. The setting cannot be changed after joining the room.

<span id="RTCRoomConfig-live_mode"></span>
### live_mode

```cpp
RoomLiveMode bytertc::RTCRoomConfig::live_mode = kRoomLiveModeCoHost
```


live streaming mode. See [RoomLiveMode](https://docs.byteplus.com/en/docs/12/14187#RoomLiveMode). The default is `kRoomLiveModeCoHost`. The setting can be changed after joining the room.

**Notes**

If `room_profile_type` is not `kRoomProfileTypeLive`, `live_mode` is invalid.

<span id="RTCRoomConfig-stream_id"></span>
### stream_id

```cpp
const char* bytertc::RTCRoomConfig::stream_id = nullptr
```


Stream ID. Set the stream ID for the stream to be published. If it is empty, the SDK automatically generates the stream ID.

<span id="RTCRoomConfig-is_auto_publish_audio"></span>
### is_auto_publish_audio

```cpp
bool bytertc::RTCRoomConfig::is_auto_publish_audio = true
```


Whether to publish media streams automatically. The default is automatic publishing.


* Changing the user role to audience via `setUserVisibility` will void this setting.

* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only.

    &nbsp;


<span id="is-auto-publish-video"></span>
### is_auto_publish_video

```cpp
bool bytertc::RTCRoomConfig::is_auto_publish_video = true
```


Whether to publish media streams automatically. The default is automatic publishing.


* Changing the user role to audience via `setUserVisibility` will void this setting.

* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only.

    &nbsp;


<span id="is-auto-subscribe-audio"></span>
### is_auto_subscribe_audio

```cpp
bool bytertc::RTCRoomConfig::is_auto_subscribe_audio = true
```


Whether to automatically subscribe to the audio stream. The default is automatic subscription.

This setting affects both the main stream and the screen\-sharing stream.

<span id="RTCRoomConfig-is_auto_subscribe_video"></span>
### is_auto_subscribe_video

```cpp
bool bytertc::RTCRoomConfig::is_auto_subscribe_video = true
```


Whether to automatically subscribe to the video stream. The default is automatic subscription.

This setting affects both the main stream and the screen\-sharing stream.

<span id="VideoFrameInfo"></span>
# VideoFrameInfo

```cpp
struct bytertc::VideoFrameInfo
```


Video frame information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/en/docs/12/14187#VideoFrameInfo-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14187#VideoFrameInfo-height) |
|VideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14187#VideoFrameInfo-rotation) |


<span id="instructions"></span>
## Instructions

<span id="VideoFrameInfo-width"></span>
### width

```cpp
int bytertc::VideoFrameInfo::width = 0
```


Width (pixels)

<span id="VideoFrameInfo-height"></span>
### height

```cpp
int bytertc::VideoFrameInfo::height = 0
```


Height (pixels)

<span id="VideoFrameInfo-rotation"></span>
### rotation

```cpp
VideoRotation bytertc::VideoFrameInfo::rotation = VideoRotation::kVideoRotation0
```


Video frame clockwise rotation angle. See [VideoRotation](https://docs.byteplus.com/en/docs/12/14187#VideoRotation).

<span id="Socks5ProxyState"></span>
# Socks5ProxyState

```cpp
enum bytertc::Socks5ProxyState
```


SOCKS5 proxy connection status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSocks5Init |0 |SOCKS5 connection initialization |
|kSocks5Connected |1 |SOCKS5 Connection successful |
|kSocks5Error |2 |SOCKS5 connection error |
|kSocks5TcpConnectFail |3 |TCP connection failed |
|kSocks5TcpClose |4 |TCP connection closed |
|kSocks5ProtocolTcpFail |5 |SOCKS protocol TCP negotiation phase failed |
|kSocks5ProtocolUdpFail |6 |UDP connection failed |
|kSocks5AuthFail |7 |Authorization failed |
|kSocks5Unknown |8 |Unknown state |


<span id="LocalVideoStreamState"></span>
# LocalVideoStreamState

```cpp
enum bytertc::LocalVideoStreamState
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

```cpp
struct bytertc::AudioPropertiesInfo
```


Audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[linear_volume](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesInfo-linear_volume) |
|int |[nonlinear_volume](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesInfo-nonlinear_volume) |
|float[SPECTRUM_SIZE] |[spectrum](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesInfo-spectrum) |
|int |[vad](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesInfo-vad) |
|double |[voice_pitch](https://docs.byteplus.com/en/docs/12/14187#AudioPropertiesInfo-voice_pitch) |


<span id="instructions"></span>
## Instructions

<span id="AudioPropertiesInfo-linear_volume"></span>
### linear_volume

```cpp
int bytertc::AudioPropertiesInfo::linear_volume = 0
```


linear volume. The value is in linear relation to the original volume. The higher the value, the higher the volume. The range is [0,255].


* [0, 25]: Nearly silence

* [26, 75]: Low volume

* [76, 204]: Medium volume

* [205, 255]: High volume

    &nbsp;


<span id="nonlinear-volume"></span>
### nonlinear_volume

```cpp
int bytertc::AudioPropertiesInfo::nonlinear_volume = 0
```


non\-linear volume in dB. The value is in proportion to the log value of the original volume. You can use the value to recognize the Active Speaker in the room. The range is [\-127, 0].


* [\-127, \-60]: Nearly silence

* [\-59, \-40]: Low volume

* [\-39, \-20]: Medium volume

* [\-19, 0]: High volume

    &nbsp;


<span id="spectrum"></span>
### spectrum

```cpp
float bytertc::AudioPropertiesInfo::spectrum[SPECTRUM_SIZE] = {0}
```


Spectrum array. The default length is 257.

<span id="AudioPropertiesInfo-vad"></span>
### vad

```cpp
int bytertc::AudioPropertiesInfo::vad = -1
```


Voice Activity Detection (VAD) result


* 1: Voice activity detected.

* 0: No voice activity detected.

* \-1: VAD not activated.

    &nbsp;


<span id="voice-pitch"></span>
### voice_pitch

```cpp
double bytertc::AudioPropertiesInfo::voice_pitch = 0
```


The vocal pitch of the local user, in Hertz. The range is [50, 1600].

When the following two conditions are met at the same time, the vocal pitch of the local user will be returned:


* Calls [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudiopropertiesreport), and sets the value of enable_voice_pitch to `true`.

* The local user's voice is included in the locally captured audio data.

   In other situations, `0` will be returned.

    &nbsp;


<span id="remoteaudiostatechangereason"></span>
# RemoteAudioStateChangeReason

```cpp
enum bytertc::RemoteAudioStateChangeReason
```


Receives the cause of the remote audio stream state change.

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

```cpp
struct bytertc::ProblemFeedbackInfo
```


Information for audio & video quality feedback

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[problem_desc](https://docs.byteplus.com/en/docs/12/14187#ProblemFeedbackInfo-problem_desc) |
|ProblemFeedbackRoomInfo\* |[room_info](https://docs.byteplus.com/en/docs/12/14187#ProblemFeedbackInfo-room_info) |
|int |[room_info_count](https://docs.byteplus.com/en/docs/12/14187#ProblemFeedbackInfo-room_info_count) |


<span id="instructions"></span>
## Instructions

<span id="ProblemFeedbackInfo-problem_desc"></span>
### problem_desc

```cpp
const char* bytertc::ProblemFeedbackInfo::problem_desc = nullptr
```


Specific description of problems other than the preset problem.

<span id="ProblemFeedbackInfo-room_info"></span>
### room_info

```cpp
ProblemFeedbackRoomInfo* bytertc::ProblemFeedbackInfo::room_info = nullptr
```


Room information for audio & video quality feedback. See [ProblemFeedbackRoomInfo](https://docs.byteplus.com/en/docs/12/14187#ProblemFeedbackRoomInfo).

<span id="ProblemFeedbackInfo-room_info_count"></span>
### room_info_count

```cpp
int bytertc::ProblemFeedbackInfo::room_info_count = 0
```


The length of `FeedbackRoomInfo`.

<span id="IHWDeviceContext"></span>
# IHWDeviceContext

```cpp
class bytertc::IHWDeviceContext
```


Hardware acceleration device context

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual |[~IHWDeviceContext](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-~ihwdevicecontext) |
|virtual HWDeviceType |[deviceType](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-devicetype) |
|virtual void |[setProperty](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-setproperty) |
|virtual void\* |[getProperty](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-getproperty) |
|virtual bool |[ownContext](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-owncontext) |
|virtual void |[setOwnContext](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-setowncontext) |
|virtual IHWDeviceContext\* |[moveContext](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-movecontext) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14187#IHWDeviceContext-release) |


<span id="instructions"></span>
## Instructions

<span id="IHWDeviceContext-~ihwdevicecontext"></span>
### ~IHWDeviceContext

```cpp
virtual ~IHWDeviceContext() = default;
```


<span id="IHWDeviceContext-devicetype"></span>
### deviceType

```cpp
virtual HWDeviceType deviceType() const = 0;
```


Get the hardware acceleration device context type

**Return Value**

Hardware acceleration device type. See [HWDeviceType](https://docs.byteplus.com/en/docs/12/14187#HWDeviceType)

<span id="IHWDeviceContext-setproperty"></span>
### setProperty

```cpp
virtual void setProperty(
    HWDeviceContextKey key,
    void* value
) = 0;
```


Set property

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |HWDeviceContextKey |Hardware acceleration device context type. See [HWDeviceContextKey](https://docs.byteplus.com/en/docs/12/14187#HWDeviceContextKey) |
|value |void\* |Pointer to the hardware acceleration device context address |


<span id="IHWDeviceContext-getproperty"></span>
### getProperty

```cpp
virtual void* getProperty(HWDeviceContextKey key) = 0;
```


Get the property

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |HWDeviceContextKey |Hardware acceleration device context type. See [HWDeviceContextKey](https://docs.byteplus.com/en/docs/12/14187#HWDeviceContextKey) |


**Return Value**

Return a pointer to the hardware acceleration device context address

<span id="IHWDeviceContext-owncontext"></span>
### ownContext

```cpp
virtual bool ownContext() const = 0;
```


Internal context is owned by the instance

**Return Value**


* True: hardware device context is owned by the instance object

* False: hardware device context is not owned by the instance object

    &nbsp;


<span id="setowncontext"></span>
### setOwnContext

```cpp
virtual void setOwnContext(bool own_context) = 0;
```


Sets whether context is owned by the instance object

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|own_context |bool |* True: context is owned by the instance object<br><br>* False: context is not owned by the instance object |


<span id="IHWDeviceContext-movecontext"></span>
### moveContext

```cpp
virtual IHWDeviceContext* moveContext() = 0;
```


Transfer hardware device context,

**Return Value**

Pointer to hardware device context

<span id="IHWDeviceContext-release"></span>
### release

```cpp
virtual void release() = 0;
```


Release instance object

<span id="PerformanceAlarmReason"></span>
# PerformanceAlarmReason

```cpp
enum bytertc::PerformanceAlarmReason
```


Reasons of performance\-related alarms

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kPerformanceAlarmReasonBandwidthFallbacked |0 |The poor network causes the transmission performance to fall back. This reason is only received when sending performance fallback is turned on. |
|kPerformanceAlarmReasonBandwidthResumed |1 |Network performance recovery, transmission performance rollback recovery. This reason is only received when sending performance fallback is turned on. |
|kPerformanceAlarmReasonPerformanceFallbacked |2 |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance is insufficient;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance is insufficient and the send performance fallback has occurred. |
|kPerformanceAlarmReasonPerformanceResumed |3 |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance shortage has been restored;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance shortage has been restored and the send performance fallback has occurred. Recovery. |


<span id="JoinRoomType"></span>
# JoinRoomType

```cpp
enum bytertc::JoinRoomType
```


The type of joining the room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kJoinRoomTypeFirst |0 |Join the room for the first time. The user calls `joinRoom` to join the room. |
|kJoinRoomTypeReconnected |1 |Rejoin the room. The user loses connection to the server due to poor network, and rejoins the room successfully. |


<span id="ForwardStreamStateInfo"></span>
# ForwardStreamStateInfo

```cpp
struct bytertc::ForwardStreamStateInfo
```


State and error for each room during relaying

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[room_id](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamStateInfo-room_id) |
|ForwardStreamState |[state](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamStateInfo-state) |
|ForwardStreamError |[error](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamStateInfo-error) |


<span id="instructions"></span>
## Instructions

<span id="ForwardStreamStateInfo-room_id"></span>
### room_id

```cpp
const char* bytertc::ForwardStreamStateInfo::room_id
```


ID of the room where the media stream aims to relay to

<span id="ForwardStreamStateInfo-state"></span>
### state

```cpp
ForwardStreamState bytertc::ForwardStreamStateInfo::state
```


State of the room during relaying. Refer to [ForwardStreamState](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamState) for more information.

<span id="ForwardStreamStateInfo-error"></span>
### error

```cpp
ForwardStreamError bytertc::ForwardStreamStateInfo::error
```


Error code from the room during relaying. Refer to [ForwardStreamError](https://docs.byteplus.com/en/docs/12/14187#ForwardStreamError) for more information.

<span id="ScreenFilterConfig"></span>
# ScreenFilterConfig

```cpp
struct bytertc::ScreenFilterConfig
```


Exclude a specific window when sharing your screen. No window is excluded by default.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|view_t\* |[excluded_window_list](https://docs.byteplus.com/en/docs/12/14187#ScreenFilterConfig-excluded_window_list) |
|int |[excluded_window_num](https://docs.byteplus.com/en/docs/12/14187#ScreenFilterConfig-excluded_window_num) |


<span id="instructions"></span>
## Instructions

<span id="ScreenFilterConfig-excluded_window_list"></span>
### excluded_window_list

```cpp
view_t* bytertc::ScreenFilterConfig::excluded_window_list = nullptr
```


The list of windows excluded from screen capture. This parameter only takes effect when sharing your screen.

<span id="ScreenFilterConfig-excluded_window_num"></span>
### excluded_window_num

```cpp
int bytertc::ScreenFilterConfig::excluded_window_num = 0
```


The number of windows excluded from screen capture.

<span id="RemoteStreamStats"></span>
# RemoteStreamStats

```cpp
struct bytertc::RemoteStreamStats
```


The remote audio/video stream statistics and network status subscribed by the user, with a reference period of 2s.

After the remote user successfully publishes the audio/video stream, the SDK will periodically notify local users of the reception status of the subscribed remote audio/video stream during this reference period through `onRemoteStreamStats`. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|const char\* |[uid](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamStats-uid) |
|RemoteAudioStats |[audio_stats](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamStats-audio_stats) |
|RemoteVideoStats |[video_stats](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamStats-video_stats) |
|bool |[is_screen](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamStats-is_screen) |
|NetworkQuality |[deprecated] [remote_tx_quality](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamStats-remote_tx_quality) |
|NetworkQuality |[deprecated] [remote_rx_quality](https://docs.byteplus.com/en/docs/12/14187#RemoteStreamStats-remote_rx_quality) |


<span id="instructions"></span>
## Instructions

<span id="RemoteStreamStats-uid"></span>
### uid

```cpp
const char* bytertc::RemoteStreamStats::uid
```


User ID. The remote user ID of the audio source.

<span id="RemoteStreamStats-audio_stats"></span>
### audio_stats

```cpp
RemoteAudioStats bytertc::RemoteStreamStats::audio_stats
```


For statistics on remote audio streams. See [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/14187#RemoteAudioStats)

<span id="RemoteStreamStats-video_stats"></span>
### video_stats

```cpp
RemoteVideoStats bytertc::RemoteStreamStats::video_stats
```


For statistics on remote video streams. See [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/14187#RemoteVideoStats)

<span id="RemoteStreamStats-is_screen"></span>
### is_screen

```cpp
bool bytertc::RemoteStreamStats::is_screen
```


Reserved field. Ignore the value returned in this field.

<span id="RemoteStreamStats-remote_tx_quality"></span>
### remote_tx_quality

```cpp
NetworkQuality bytertc::RemoteStreamStats::remote_tx_quality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onnetworkquality) instead.


For the media stream uplink network quality of the user you belong to. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14187#NetworkQuality)

<span id="RemoteStreamStats-remote_rx_quality"></span>
### remote_rx_quality

```cpp
NetworkQuality bytertc::RemoteStreamStats::remote_rx_quality
```


> Deprecated since 3.45 and will be deleted in 3.51, use [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onnetworkquality) instead.


The downlink network quality of the media stream belongs to the user. See [NetworkQuality](https://docs.byteplus.com/en/docs/12/14187#NetworkQuality)
