---
title: "Keytype"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70089"
---

<span id="ByteRTCAudioEffectPlayerConfig"></span>
# ByteRTCAudioEffectPlayerConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioEffectPlayerConfig : NSObject
```


Mixing configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCAudioMixingType |[type](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioEffectPlayerConfig-type) |
|NSInteger |[pitch](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioEffectPlayerConfig-pitch) |
|NSInteger |[playCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioEffectPlayerConfig-playcount) |
|NSInteger |[startPos](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioEffectPlayerConfig-startpos) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioEffectPlayerConfig-type"></span>
### type

```objectivec
@property(assign, nonatomic) ByteRTCAudioMixingType type;
```


Mixing playback types. See [ByteRTCAudioMixingType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioMixingType)

<span id="ByteRTCAudioEffectPlayerConfig-pitch"></span>
### pitch

```objectivec
@property(assign, nonatomic) NSInteger pitch;
```


The increase or decrease value compared with the original pitch of the music file. The range is `[-12, 12]`. The default value is 0. The pitch distance between two adjacent values is half a step. A positive value indicates a rising pitch, and a negative value indicates a falling pitch.

<span id="ByteRTCAudioEffectPlayerConfig-playcount"></span>
### playCount

```objectivec
@property(assign, nonatomic) NSInteger playCount;
```


Mix playback times


* Play_count < = 0: Infinite loop

* Play_count == 1: Play once (default)

* Play_count \> 1: Play play_count times

    &nbsp;


<span id="startpos"></span>
### startPos

```objectivec
@property(assign, nonatomic) NSInteger startPos;
```


The starting position in ms. 0 by default.

<span id="ByteRTCRecordingInfo"></span>
# ByteRTCRecordingInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRecordingInfo : NSObject
```


Details of local recording

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[filePath](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingInfo-filepath) |
|ByteRTCVideoCodecType |[codecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingInfo-codectype) |
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingInfo-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingInfo-height) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRecordingInfo-filepath"></span>
### filePath

```objectivec
@property(strong, nonatomic) NSString* _Nullable filePath;
```


The absolute path of the recorded file, including the file name and file suffix

<span id="ByteRTCRecordingInfo-codectype"></span>
### codecType

```objectivec
@property(assign, nonatomic) ByteRTCVideoCodecType codecType;
```


For the video encoding type of the recorded file. See [ByteRTCVideoCodecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCodecType)

<span id="ByteRTCRecordingInfo-width"></span>
### width

```objectivec
@property(nonatomic, assign) NSInteger width;
```


The width of the recorded video, in pixels. Please ignore this field for audio\-only recording

<span id="ByteRTCRecordingInfo-height"></span>
### height

```objectivec
@property(nonatomic, assign) NSInteger height;
```


The height of the recorded video, the unit: pixels. Please ignore this field for audio\-only recording

<span id="ByteRTCSubscribeConfig"></span>
# ByteRTCSubscribeConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCSubscribeConfig: NSObject
```


The parameter configuration of the subscribed stream. The subscription configuration parameters used when the user manually subscribes to all audio & video streams.

When the user turns off the automatic subscription function, when using the manual subscription mode, he subscribes to the audio & video stream by calling the `subscribeStream`, and the incoming parameters are for this data type.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-isscreen) |
|BOOL |[subscribeVideo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-subscribevideo) |
|BOOL |[subscribeAudio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-subscribeaudio) |
|NSInteger |[videoIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-videoindex) |
|NSInteger |[svcLayer](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-svclayer) |
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-height) |
|NSInteger |[framerate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeConfig-framerate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCSubscribeConfig-isscreen"></span>
### isScreen

```objectivec
@property(nonatomic, assign) BOOL isScreen;
```


Reserved field. Do not set this field in the single\-stream SDK.

<span id="ByteRTCSubscribeConfig-subscribevideo"></span>
### subscribeVideo

```objectivec
@property(nonatomic, assign) BOOL subscribeVideo;
```


Whether to subscribe to videos.

The user selects whether to subscribe to videos in the remote stream by setting this parameter. YES means subscribing to video, NO means not subscribing to video, and the default value is YES.

<span id="ByteRTCSubscribeConfig-subscribeaudio"></span>
### subscribeAudio

```objectivec
@property(nonatomic, assign) BOOL subscribeAudio;
```


Whether to subscribe to audio.

The user selects whether to subscribe to audio in the remote stream by setting this parameter. YES is subscribed audio, NO is not subscribed audio, the default value is YES.

<span id="ByteRTCSubscribeConfig-videoindex"></span>
### videoIndex

```objectivec
@property(nonatomic, assign) NSInteger videoIndex;
```


Subscribed video stream resolution index.

Users can publish multiple video streams of different resolutions by calling the [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setvideoencoderconfig) method. Therefore, when subscribing to a stream, you need to specify the specific resolution of the subscription. This parameter is used to specify the subscript of the resolution to be subscribed to, and the default value is 0.

<span id="ByteRTCSubscribeConfig-svclayer"></span>
### svcLayer

```objectivec
@property(nonatomic, assign) NSInteger svcLayer;
```


Temporal layer of the subscribed video stream, default value is 0.

<span id="ByteRTCSubscribeConfig-width"></span>
### width

```objectivec
@property(nonatomic, assign) NSInteger width;
```


The width in px of the subscription, the default value is 0.

<span id="ByteRTCSubscribeConfig-height"></span>
### height

```objectivec
@property(nonatomic, assign) NSInteger height;
```


The height in px of the subscription, the default value is 0.

<span id="ByteRTCSubscribeConfig-framerate"></span>
### framerate

```objectivec
@property (nonatomic, assign) NSInteger framerate;
```


Expected maximum frame rate of the subscribed stream in fps. The default value is 0, values greater than 10 are valid.

If the frame rate of the stream published is higher than the value set by the subscriber, the subscriber receives the video of the frame rate set by this API; if the frame rate of the stream published is lower than the value set by the subscriber, the subscriber receives the video of the same frame rate of the video published.

Only valid if the stream is coded with SVC technique.

<span id="ByteRTCUserInfo"></span>
# ByteRTCUserInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCUserInfo : NSObject
```


User information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCUserInfo-userid) |
|NSString\* |[extraInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCUserInfo-extrainfo) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCUserInfo-userid"></span>
### userId

```objectivec
@property(copy, nonatomic) NSString *_Nonnull userId;
```


User ID. The string matches the regular expression: `[a-zA-Z0-9_\@\\-\\.]{1,128}`.

<span id="ByteRTCUserInfo-extrainfo"></span>
### extraInfo

```objectivec
@property(copy, nonatomic) NSString *_Nonnull extraInfo;
```


Additional information of the user. The string is no more than 200 bytes.

The remote users will receive the info with `rtcRoom:onUserJoined:`.

<span id="ByteRTCAudioPlaybackDevice"></span>
# ByteRTCAudioPlaybackDevice

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioPlaybackDevice
)
```


Audio playback device

When the audio playback device changes, you will receive the `rtcEngine:onAudioPlaybackDeviceChanged:` callback.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioPlaybackDeviceHeadset |1 |Wired earphones |
|ByteRTCAudioPlaybackDeviceEarpiece |2 |Earpiece |
|ByteRTCAudioPlaybackDeviceSpeakerphone |3 |Speaker |
|ByteRTCAudioPlaybackDeviceHeadsetBluetooth |4 |Bluetooth earphones |
|ByteRTCAudioPlaybackDeviceHeadsetUSB |5 |USB Device |


<span id="ByteRTCStreamSyncInfoConfig"></span>
# ByteRTCStreamSyncInfoConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCStreamSyncInfoConfig : NSObject
```


Configuration related to media stream information synchronization

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[repeatCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamSyncInfoConfig-repeatcount) |
|ByteRTCSyncInfoStreamType |[streamType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamSyncInfoConfig-streamtype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCStreamSyncInfoConfig-repeatcount"></span>
### repeatCount

```objectivec
@property(assign, nonatomic) int repeatCount;
```


The number of duplicates sent by the message, the value range is [0,25], it is recommended to set it to [3,5].

<span id="ByteRTCStreamSyncInfoConfig-streamtype"></span>
### streamType

```objectivec
@property(assign, nonatomic) ByteRTCSyncInfoStreamType streamType;
```


For the stream type for media stream information synchronization. See [ByteRTCSyncInfoStreamType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSyncInfoStreamType).

<span id="ByteRTCMessageConfig"></span>
# ByteRTCMessageConfig

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMessageConfig
)
```


Reliable orderliness of sent messages

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMessageConfigReliableOrdered |0 |Low latency reliable and orderly message |
|ByteRTCMessageConfigUnreliableOrdered |1 |Ultra\-low latency ordered message |
|ByteRTCMessageConfigUnreliableUnordered |2 |Ultra\-low latency unordered message |


<span id="ByteRTCVideoSinkDelegate"></span>
# ByteRTCVideoSinkDelegate

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCVideoSinkDelegate <NSObject>
```


Custom video renderer

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onFrame:](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSinkDelegate-onframe) |
|void |[deprecated] [renderPixelBuffer:rotation:contentType:extendedData:](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSinkDelegate-renderpixelbuffer-rotation-contenttype-extendeddata) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoSinkDelegate-onframe"></span>
### onFrame:

```objectivec
- (void)onFrame:(id<ByteRTCVideoFrame > _Nonnull)videoFrame;
```


Outputs video PixelBuffer

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoFrame |id<ByteRTCVideoFrame\> |video frame |


<span id="ByteRTCVideoSinkDelegate-renderpixelbuffer-rotation-contenttype-extendeddata"></span>
### renderPixelBuffer:rotation:contentType:extendedData:

```objectivec
- (void)renderPixelBuffer:(CVPixelBufferRef _Nonnull)pixelBuffer
                 rotation:(ByteRTCVideoRotation)rotation
                 contentType:(ByteRTCVideoContentType)contentType
                extendedData:(NSData* _Nullable)extendedData;
```


> Deprecated since 3.54, use onFrame: instead


Outputs video PixelBuffer

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pixelBuffer |CVPixelBufferRef |Video PixelBuffer |
|rotation |ByteRTCVideoRotation |Video rotation angle. See [ByteRTCVideoRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoRotation) |
|contentType |ByteRTCVideoContentType |Video content type. See [ByteRTCVideoContentType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoContentType) |
|extendedData |NSData\* |Additional data obtained after video is decoded. |


<span id="ByteRTCMixedStreamConfig"></span>
# ByteRTCMixedStreamConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamConfig : NSObject
```


Configurations for the mixing streams.

If not specified, the parameter can be used for both WTN stream and mixing\-stream tasks.

If not specified, the parameter can be passed when starting a task or during a task.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[backgroundColor](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-backgroundcolor) |
|NSArray<ByteRTCMixedStreamLayoutRegionConfig\*\>\* |[regions](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-regions) |
|ByteRTCMixedStreamVideoConfig\* |[videoConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-videoconfig) |
|ByteRTCMixedStreamAudioConfig\* |[audioConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-audioconfig) |
|ByteRTCMixedStreamControlConfig\* |[controlConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-controlconfig) |
|NSString\* |[roomID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-roomid) |
|NSString\* |[userID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-userid) |
|NSString\* |[userConfigExtraInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-userconfigextrainfo) |
|NSString\* |[backgroundImageURL](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-backgroundimageurl) |
|ByteRTCStreamLayoutMode |[layoutMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-layoutmode) |
|ByteRTCInterpolationMode |[interpolationMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-interpolationmode) |
|ByteRTCMixedStreamPushTargetType |[pushTargetType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-pushtargettype) |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|instancetype |[defaultMixedStreamConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig-defaultmixedstreamconfig) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamConfig-backgroundcolor"></span>
### backgroundColor

```objectivec
@property(copy, nonatomic) NSString *_Nonnull backgroundColor;
```


Background\-color of the mixed stream in hexadecimal values such as #FFFFFF and #000000. The default value is #000000 (black). It's recommended to be set.

With invalid or empty input, the configurations will be set as the default values.

<span id="ByteRTCMixedStreamConfig-regions"></span>
### regions

```objectivec
@property(copy, nonatomic) NSArray<ByteRTCMixedStreamLayoutRegionConfig *> * _Nonnull regions;
```


List of user's video layout information. The specific layout of each stream is detailed in [ByteRTCMixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig). It's recommended to be set.

With invalid or empty input, the configurations will be set as the default values.

<span id="ByteRTCMixedStreamConfig-videoconfig"></span>
### videoConfig

```objectivec
@property(strong, nonatomic) ByteRTCMixedStreamVideoConfig * _Nonnull videoConfig;
```


Video transcoding related configurations. See [ByteRTCMixedStreamVideoConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig). It's recommended to be set.

<span id="ByteRTCMixedStreamConfig-audioconfig"></span>
### audioConfig

```objectivec
@property(strong, nonatomic) ByteRTCMixedStreamAudioConfig * _Nonnull audioConfig;
```


Audio mixed related configurations. See [ByteRTCMixedStreamAudioConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioConfig) for data types. It's recommended to be set.


* This parameter cannot be updated during the task.

* This parameter is not supported for WTN stream tasks.

    &nbsp;


<span id="controlconfig"></span>
### controlConfig

```objectivec
@property(strong, nonatomic) ByteRTCMixedStreamControlConfig * _Nonnull controlConfig;
```


Server mix Control config. See [ByteRTCMixedStreamControlConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig) for detail.

<span id="ByteRTCMixedStreamConfig-roomid"></span>
### roomID

```objectivec
@property(copy, nonatomic) NSString * _Nonnull roomID;
```


The room ID for live transcoding. The sum length of `roomID` and `userID` should not exceed 126 bytes. It's recommended to be set.

This parameter cannot be updated during the task.

<span id="ByteRTCMixedStreamConfig-userid"></span>
### userID

```objectivec
@property(copy, nonatomic) NSString * _Nonnull userID;
```


The user ID for live transcoding. The sum length of `roomID` and `userID` should not exceed 126 bytes. It's recommended to be set.

This parameter cannot be updated during the task.

<span id="ByteRTCMixedStreamConfig-userconfigextrainfo"></span>
### userConfigExtraInfo

```objectivec
@property(copy, nonatomic) NSString *_Nonnull userConfigExtraInfo;
```


Info passed through from the user.

This parameter is not supported for WTN stream tasks.

<span id="ByteRTCMixedStreamConfig-backgroundimageurl"></span>
### backgroundImageURL

```objectivec
@property(copy, nonatomic) NSString *_Nonnull backgroundImageURL;
```


> Available since 3.57


Sets the URL of the background image for the canvas that renders the mixed stream, with a maximum length of 1024 bytes.

The URL must start with http, and you can input images in the following supported formats: JPG, JPEG, PNG.

If the width and height of the background image are different from the screen dimensions, the background image will be scaled to fill the screen.

<span id="ByteRTCMixedStreamConfig-layoutmode"></span>
### layoutMode

```objectivec
@property(assign, nonatomic)ByteRTCStreamLayoutMode layoutMode;
```


Layout mode. See [ByteRTCStreamLayoutMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamLayoutMode). The optional values:


* `auto`: Auto layout. The default value.

* `custom`: Custom mode.

    &nbsp;


<span id="interpolationmode"></span>
### interpolationMode

```objectivec
@property(assign, nonatomic) ByteRTCInterpolationMode interpolationMode;
```


Layout mode. See [ByteRTCInterpolationMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCInterpolationMode). The optional values:

<span id="ByteRTCMixedStreamConfig-pushtargettype"></span>
### pushTargetType

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamPushTargetType pushTargetType;
```


Layout mode. See [ByteRTCMixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamPushTargetType). The optional values:

<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamConfig-defaultmixedstreamconfig"></span>
### defaultMixedStreamConfig

```objectivec
+ (instancetype _Nonnull)defaultMixedStreamConfig;
```


Gets the default configurations for pushing streams to CDN.

**Return Value**

Configurations for pushing streams to CDN. See [ByteRTCMixedStreamConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamConfig).

<span id="ByteRTCNetworkDetectionLinkType"></span>
# ByteRTCNetworkDetectionLinkType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCNetworkDetectionLinkType
)
```


The type of probe link before the call.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCNetworkDetectionLinkTypeUp |0 |Uplink network probing. |
|ByteRTCNetworkDetectionLinkTypeDown |1 |Downlink network probing. |


<span id="ByteRTCVirtualBackgroundSource"></span>
# ByteRTCVirtualBackgroundSource

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVirtualBackgroundSource: NSObject
```


Virtual background object

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCVirtualBackgroundSourceType |[sourceType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVirtualBackgroundSource-sourcetype) |
|int |[sourceColor](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVirtualBackgroundSource-sourcecolor) |
|NSString\* |[sourcePath](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVirtualBackgroundSource-sourcepath) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVirtualBackgroundSource-sourcetype"></span>
### sourceType

```objectivec
@property(nonatomic, assign) ByteRTCVirtualBackgroundSourceType sourceType;
```


See [ByteRTCVirtualBackgroundSourceType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVirtualBackgroundSourceType).

<span id="ByteRTCVirtualBackgroundSource-sourcecolor"></span>
### sourceColor

```objectivec
@property int sourceColor;
```


The solid color of the background.

The format is 0xAARRGGBB.

<span id="ByteRTCVirtualBackgroundSource-sourcepath"></span>
### sourcePath

```objectivec
@property(nonatomic) NSString* _Nullable sourcePath;
```


The absolute path of the specified image.


* You can upload a .JPG, .PNG, or .JPEG file.

* The image with a resolution higher than 1080p(Full HD) will be rescaled proportionally to fit in the video.

* If the image's aspect ratio matches the video's, the image will be rescaled proportionally to fit in the video.

* If the image’s aspect ratio does not match the video's, the shortest side (either height or width) of the image will be stretched proportionally to match the video. Then the image will be cropped to fill in the video.

* The transparent area in the image will be filled with black.

    &nbsp;


<span id="bytertclocalvideosinkconfig"></span>
# ByteRTCLocalVideoSinkConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCLocalVideoSinkConfig : NSObject
```


Local video frame callback config.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCLocalVideoSinkPosition |[position](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoSinkConfig-position) |
|ByteRTCVideoSinkPixelFormat |[requiredPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoSinkConfig-requiredpixelformat) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLocalVideoSinkConfig-position"></span>
### position

```objectivec
@property(nonatomic, assign) ByteRTCLocalVideoSinkPosition position;
```


The position of the local video frame. See [ByteRTCLocalVideoSinkPosition](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoSinkPosition).

<span id="ByteRTCLocalVideoSinkConfig-requiredpixelformat"></span>
### requiredPixelFormat

```objectivec
@property(nonatomic, assign) ByteRTCVideoSinkPixelFormat requiredPixelFormat;
```


The pixel format of the local video frame. See [ByteRTCVideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSinkPixelFormat). The default value is 0.

<span id="ByteRTCVideoCapturePreference"></span>
# ByteRTCVideoCapturePreference

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoCapturePreference
)
```


Video capture preference

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoCapturePreferenceAuto |0 |(Default) Video capture preference: auto<br><br>&nbsp;<br><br>SDK determines the best video capture parameters referring to the camera output parameters and the encoder configuration. |
|ByteRTCVideoCapturePreferenceMannal |1 |Video capture preference: manual<br><br>&nbsp;<br><br>Set the resolution and the frame rate manually. |
|ByteRTCVideoCapturePreferenceAutoPerformance |2 |Video capture preference: encoder configuration |


<span id="ByteRTCProblemFeedbackOption"></span>
# ByteRTCProblemFeedbackOption

```objectivec
typedef NS_OPTIONS(
    uint64_t,
    ByteRTCProblemFeedbackOption
)
```


Audio & video quality feedback problem type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCProblemFeedbackOptionNone |0 |No problem |
|ByteRTCProblemFeedbackOptionOtherMessage |1ULL << 0 |Other issues |
|ByteRTCProblemFeedbackOptionDisconnected |1ULL << 1 |Connection failed |
|ByteRTCProblemFeedbackOptionEarBackDelay |1ULL << 2 |High latency for the ear monitor |
|ByteRTCProblemFeedbackOptionLocalNoise |1ULL << 10 |Noise on the local end |
|ByteRTCProblemFeedbackOptionLocalAudioLagging |1ULL << 11 |Audio stall on the local end |
|ByteRTCProblemFeedbackOptionLocalNoAudio |1ULL << 12 |No sound on the local end |
|ByteRTCProblemFeedbackOptionLocalAudioStrength |1ULL << 13 |Too little/loud sound on the local end |
|ByteRTCProblemFeedbackOptionLocalEcho |1ULL << 14 |Echo noise on the local end |
|ByteRTCProblemFeedbackOptionLocalVideoFuzzy |1ULL << 24 |Unclear video on the local end |
|ByteRTCProblemFeedbackOptionLocalNotSync |1ULL << 25 |Audio & video out of sync on the local end |
|ByteRTCProblemFeedbackOptionLocalVideoLagging |1ULL << 26 |Video stall on the local end |
|ByteRTCProblemFeedbackOptionLocalNoVideo |1ULL << 27 |No picture on the local end |
|ByteRTCProblemFeedbackOptionRemoteNoise |1ULL << 37 |Noise on the remote end |
|ByteRTCProblemFeedbackOptionRemoteAudioLagging |1ULL << 38 |Audio stall on the remote end |
|ByteRTCProblemFeedbackOptionRemoteNoAudio |1ULL << 39 |No sound on the remote end |
|ByteRTCProblemFeedbackOptionRemoteAudioStrength |1ULL << 40 |Too little/loud sound on the remote end |
|ByteRTCProblemFeedbackOptionRemoteEcho |1ULL << 41 |Echo noise on the remote end |
|ByteRTCProblemFeedbackOptionRemoteVideoFuzzy |1ULL << 51 |Unclear video on the remote end |
|ByteRTCProblemFeedbackOptionRemoteNotSync |1ULL << 52 |Audio & video out of sync on the remote end |
|ByteRTCProblemFeedbackOptionRemoteVideoLagging |1ULL << 53 |Video stall on the remote end |
|ByteRTCProblemFeedbackOptionRemoteNoVideo |1ULL << 54 |No picture on the remote end |


<span id="ByteRTCAudioFormat"></span>
# ByteRTCAudioFormat

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioFormat : NSObject
```


Audio parameters format

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCAudioSampleRate |[sampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFormat-samplerate) |
|ByteRTCAudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFormat-channel) |
|int |[samplesPerCall](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFormat-samplespercall) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioFormat-samplerate"></span>
### sampleRate

```objectivec
@property(nonatomic, assign) ByteRTCAudioSampleRate sampleRate;
```


Audio sampling rate. See [ByteRTCAudioSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioSampleRate)

<span id="ByteRTCAudioFormat-channel"></span>
### channel

```objectivec
@property(nonatomic, assign) ByteRTCAudioChannel channel;
```


For audio channels. See [ByteRTCAudioChannel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioChannel)

<span id="ByteRTCAudioFormat-samplespercall"></span>
### samplesPerCall

```objectivec
@property(nonatomic, assign) int samplesPerCall;
```


Samples per audio frame returned by callback. `0` by default. The default samples per callback is the minimum value.

The minimum value is `sampleRate * channel * 0.01s`, the value when the callback interval is 0.01s.

The maximum value is `2048`. If the value is invalid, the samples per callback uses the default value.

This parameter only takes effect when setting the read\-write callback. It does not take effect when calling [enableAudioFrameCallback:format:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-enableaudioframecallback-format) to enable read\-only callback.

<span id="ByteRTCNetworkType"></span>
# ByteRTCNetworkType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCNetworkType
)
```


SDK Network connection type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCNetworkTypeUnknown |\-1 |Network connection type unknown. |
|ByteRTCNetworkTypeDisconnected |0 |The network connection has been disconnected. |
|ByteRTCNetworkTypeLAN |1 |The network connection type is LAN. |
|ByteRTCNetworkTypeWIFI |2 |The network connection type is Wi\-Fi (including hotspots). |
|ByteRTCNetworkTypeMobile2G |3 |The network connection type is 2G mobile network. |
|ByteRTCNetworkTypeMobile3G |4 |The network connection type is 3G mobile network. |
|ByteRTCNetworkTypeMobile4G |5 |The network connection type is 4G mobile network. |
|ByteRTCNetworkTypeMobile5G |6 |The network connection type is 5G mobile network. |


<span id="ByteRTCPlayerError"></span>
# ByteRTCPlayerError

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPlayerError
)
```


Error code for audio playout.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPlayerErrorOK |0 |OK |
|ByteRTCPlayerErrorFormatNotSupport |1 |Format not supported. |
|ByteRTCPlayerErrorInvalidPath |2 |Invalid file path. |
|ByteRTCPlayerErrorInvalidState |3 |The prerequisite is not met. Check the specific API doc. |
|ByteRTCPlayerErrorInvalidPosition |4 |Invalid position. |
|ByteRTCPlayerErrorInvalidVolume |5 |Invalid volume. |
|ByteRTCPlayerErrorInvalidPitch |6 |Invalid pitch value. |
|ByteRTCPlayerErrorInvalidAudioTrackIndex |7 |Invalid audio track. |
|ByteRTCPlayerErrorInvalidPlaybackSpeed |8 |Invalid playback speed. |
|ByteRTCPlayerErrorInvalidEffectId |9 |Invalid effect ID. Receive this error code when you call other APIs before the audio file is preloaded or opened. |
|ByteRTCPlayerErrorCurrentlyPlaying |10 |The resource is currently playing. |


<span id="ByteRTCPlayerEvent"></span>
# ByteRTCPlayerEvent

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPlayerEvent
)
```


Player events.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPlayerEventSelectAudioTrackBegin |0 |Beginning to switch audio tracks.<br><br>When you call [selectAudioTrack:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCMediaPlayer-selectaudiotrack) to switch audio tracks, the player returns this state. |
|ByteRTCPlayerEventSelectAudioTrackCompleted |1 |Audio track switch completed.<br><br>After you call [selectAudioTrack:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCMediaPlayer-selectaudiotrack) to switch audio tracks, the player switches to the specified audio track and returns this state. |
|ByteRTCPlayerEventSelectAudioTrackFailed |2 |Audio track switch failed.<br><br>After you call [selectAudioTrack:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCMediaPlayer-selectaudiotrack) to switch audio tracks, the player fails to switch to the specified audio track and continues playing the previous audio track. This event returns this state. |
|ByteRTCPlayerEventSeekBegin |3 |Beginning to seek.<br><br>When you call [setPosition:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCMediaPlayer-setposition) to seek to a specific position, the player returns this state. |
|ByteRTCPlayerEventSeekCompleted |4 |Seeking completed.<br><br>After you call [setPosition:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCMediaPlayer-setposition) to seek to a specific position, the player returns this state. |
|ByteRTCPlayerEventSeekFailed |5 |Seeking failed.<br><br>After you call [setPosition:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCMediaPlayer-setposition) to seek to a specific position, the player fails to seek and returns this state. |


<span id="ByteRTCAudioEnhancementConfig"></span>
# ByteRTCAudioEnhancementConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioEnhancementConfig: NSObject
```


Media type for cellular assisted Enhancement

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enhanceSignaling](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioEnhancementConfig-enhancesignaling) |
|BOOL |[enhanceAudio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioEnhancementConfig-enhanceaudio) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioEnhancementConfig-enhancesignaling"></span>
### enhanceSignaling

```objectivec
@property (assign, nonatomic) BOOL enhanceSignaling;
```


Apply to signaling or not. Not by default.

<span id="ByteRTCAudioEnhancementConfig-enhanceaudio"></span>
### enhanceAudio

```objectivec
@property (assign, nonatomic) BOOL enhanceAudio;
```


Apply to audio stream or not. Not by default.

<span id="ByteRTCLocalAudioStreamState"></span>
# ByteRTCLocalAudioStreamState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCLocalAudioStreamState
)
```


Local audio stream status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalAudioStreamStateStopped |0 |The default initial state of the local audio.<br><br>&nbsp;<br><br>Callback to this state when the microphone stops working, corresponding to the error code [ByteRTCLocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStreamError) in ByteRTCLocalAudioStreamErrorOk |
|ByteRTCLocalAudioStreamStateRecording |1 |The local audio recording device started successfully.<br><br>&nbsp;<br><br>Callback to this state when the first audio frame is collected, corresponding to the error code [ByteRTCLocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStreamError) in ByteRTCLocalAudioStreamErrorOk |
|ByteRTCLocalAudioStreamStateEncoding |2 |The first frame of the local audio was successfully encoded.<br><br>&nbsp;<br><br>Callback to this state when the audio first frame encoding is successful, corresponding to the error code [ByteRTCLocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStreamError) in ByteRTCLocalAudioStreamErrorOk |
|ByteRTCLocalAudioStreamStateFailed |3 |The local audio startup failed, and the status is called back at the following times:<br><br><br>&nbsp;<br><br>* The local recording device failed to start, corresponding to the error code [ByteRTCLocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStreamError) ByteRTCLocalAudioStreamErrorRecordFailure<br><br>* No recording device permission was detected, corresponding to the error code [ByteRTCLocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStreamError) ByteRTCLocalAudioStreamErrorDeviceNoPermission<br><br>* The audio encoding failed, corresponding to the error code [ByteRTCLocalAudioStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStreamError) in ByteRTCLocalAudioStreamError |


<span id="ByteRTCMixedStreamVideoType"></span>
# ByteRTCMixedStreamVideoType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMixedStreamVideoType
)
```


Reserved field.

<span id="ByteRTCVoiceReverbType"></span>
# ByteRTCVoiceReverbType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVoiceReverbType
)
```


Reverb effect type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVoiceReverbOriginal |0 |Acoustic, no special effects |
|ByteRTCVoiceReverbEcho |1 |Echo |
|ByteRTCVoiceReverbConcert |2 |Concert |
|ByteRTCVoiceReverbEthereal |3 |Ethereal |
|ByteRTCVoiceReverbKTV |4 |Karaoke |
|ByteRTCVoiceReverbStudio |5 |Recording studio |
|ByteRTCVoiceReverbVirtualStereo |6 |Virtual Stereo |
|ByteRTCVoiceReverbSpacious |7 |Spacious |
|ByteRTCVoiceReverb3D |8 |3D vocal |


<span id="ByteRTCAudioFrameSource"></span>
# ByteRTCAudioFrameSource

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioFrameSource
)
```


Audio file recording source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioFrameSourceTypeMic |0 |The audio captured by the local microphone. |
|ByteRTCAudioFrameSourceTypePlayback |1 |The audio obtained by mixing all remote users' audio. |
|ByteRTCAudioFrameSourceTypeMixed |2 |The audio obtained by mixing the locally captured audio and all remote users' audio. |


<span id="ByteRTCLocalAudioStreamError"></span>
# ByteRTCLocalAudioStreamError

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCLocalAudioStreamError
)
```


Error code when the state of the local audio stream changes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalAudioStreamErrorOk |0 |Local audio status is normal |
|ByteRTCLocalAudioStreamErrorFailure |1 |Local audio error cause unknown |
|ByteRTCLocalAudioStreamErrorDeviceNoPermission |2 |No permission to start local audio recording device |
|ByteRTCLocalAudioStreamErrorRecordFailure |4 |Local audio recording failed, it is recommended that you check whether the recording device is working properly |
|ByteRTCLocalAudioStreamErrorEncodeFailure |5 |Local audio encoding failed |
|ByteRTCLocalAudioStreamErrorNoRecordingDevice |6 |No audio recording equipment available |


<span id="ByteRTCUserOfflineReason"></span>
# ByteRTCUserOfflineReason

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCUserOfflineReason
)
```


The reason why the user leaves the room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCUserOfflineReasonQuit |0 |The remote user calls `leaveRoom` and leaves the room. |
|ByteRTCUserOfflineReasonDropped |1 |The remote user is offline. |
|ByteRTCUserOfflineReasonSwitchToInvisible |2 |The remote user switches to invisible. |
|ByteRTCUserOfflineReasonKickedByAdmin |3 |The remote user is kicked out of the room.<br><br>&nbsp;<br><br>Is kicked out of the room due to calling the OpenAPI to kick out the user. |


<span id="ByteRTCExpressionDetectInfo"></span>
# ByteRTCExpressionDetectInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCExpressionDetectInfo : NSObject
```


Expression detect information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[age](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-age) |
|float |[boyProb](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-boyprob) |
|float |[attractive](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-attractive) |
|float |[happyScore](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-happyscore) |
|float |[sadScore](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-sadscore) |
|float |[angryScore](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-angryscore) |
|float |[surpriseScore](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-surprisescore) |
|float |[arousal](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-arousal) |
|float |[valence](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo-valence) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCExpressionDetectInfo-age"></span>
### age

```objectivec
@property (assign, nonatomic) float age;
```


The estimated age in the range of (0, 100).

<span id="ByteRTCExpressionDetectInfo-boyprob"></span>
### boyProb

```objectivec
@property (assign, nonatomic) float boyProb;
```


The estimated probability of being a male in the range of (0.0, 1.0).

<span id="ByteRTCExpressionDetectInfo-attractive"></span>
### attractive

```objectivec
@property (assign, nonatomic) float attractive;
```


The estimated attractiveness in the range of (0, 100).

<span id="ByteRTCExpressionDetectInfo-happyscore"></span>
### happyScore

```objectivec
@property (assign, nonatomic) float happyScore;
```


The estimated happy score in the range of (0, 100).

<span id="ByteRTCExpressionDetectInfo-sadscore"></span>
### sadScore

```objectivec
@property (assign, nonatomic) float sadScore;
```


The estimated sad score in the range of (0, 100).

<span id="ByteRTCExpressionDetectInfo-angryscore"></span>
### angryScore

```objectivec
@property (assign, nonatomic) float angryScore;
```


The estimated angry score in the range of (0, 100).

<span id="ByteRTCExpressionDetectInfo-surprisescore"></span>
### surpriseScore

```objectivec
@property (assign, nonatomic) float surpriseScore;
```


The estimated surprise score in the range of (0, 100).

<span id="ByteRTCExpressionDetectInfo-arousal"></span>
### arousal

```objectivec
@property (assign, nonatomic) float arousal;
```


The estimated emotional arousal in the range of (0, 100).

<span id="ByteRTCExpressionDetectInfo-valence"></span>
### valence

```objectivec
@property (assign, nonatomic) float valence;
```


The estimated emotional valence in the range of (\-100, 100).

<span id="ByteRTCEngineConfig"></span>
# ByteRTCEngineConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCEngineConfig: NSObject
```


Create engine parameters.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[appID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEngineConfig-appid) |
|NSDictionary\* |[parameters](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEngineConfig-parameters) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCEngineConfig-appid"></span>
### appID

```objectivec
@property(copy, nonatomic) NSString* _Nonnull appID;
```


The unique identifier of the application. Only instances generated with the same app_id can communicate.

<span id="ByteRTCEngineConfig-parameters"></span>
### parameters

```objectivec
@property(copy, nonatomic) NSDictionary* _Nullable parameters;
```


Private parameters. Please contact the technical support personnel if you need to use them.

<span id="ByteRTCForwardStreamConfiguration"></span>
# ByteRTCForwardStreamConfiguration

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCForwardStreamConfiguration: NSObject
```


Information of the rooms where you want to relay the media stream to

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamConfiguration-roomid) |
|NSString\* |[token](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamConfiguration-token) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCForwardStreamConfiguration-roomid"></span>
### roomId

```objectivec
@property(strong, nonatomic) NSString* _Nullable roomId;
```


ID of the room to which the media stream is relayed

<span id="ByteRTCForwardStreamConfiguration-token"></span>
### token

```objectivec
@property(strong, nonatomic) NSString* _Nullable token;
```


RoomId and UserId are required to generate the Token to forward media streams to the room.

During developing and testing, you can use temporary tokens generated on the console. At the production stage, Tokens are generated by the token generating application deployed on your server.

Forwarding will fail if the token is invalid.

<span id="ByteRTCVideoEncoderConfig"></span>
# ByteRTCVideoEncoderConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoEncoderConfig: NSObject
```


Video encoding configuration. Refer to [Setting Video Encoder Configuration](https://docs.byteplus.com/byteplus-rtc/docs/70122) to learn more.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderConfig-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderConfig-height) |
|NSInteger |[frameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderConfig-framerate) |
|NSInteger |[maxBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderConfig-maxbitrate) |
|NSInteger |[minBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderConfig-minbitrate) |
|NSInteger |[keyFrameIntervalMS](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderConfig-keyframeintervalms) |
|ByteRTCVideoEncoderPreference |[encoderPreference](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderConfig-encoderpreference) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoEncoderConfig-width"></span>
### width

```objectivec
@property(nonatomic, assign) NSInteger width;
```


Width of the video frame in px

<span id="ByteRTCVideoEncoderConfig-height"></span>
### height

```objectivec
@property(nonatomic, assign) NSInteger height;
```


Height of the video frame in px

<span id="ByteRTCVideoEncoderConfig-framerate"></span>
### frameRate

```objectivec
@property(nonatomic, assign) NSInteger frameRate;
```


Video frame rate in fps

<span id="ByteRTCVideoEncoderConfig-maxbitrate"></span>
### maxBitrate

```objectivec
@property(nonatomic, assign) NSInteger maxBitrate;
```


Maximum bit rate in kbps. Optional for internal capturing while mandatory for custom capturing.

If you set this value to \-1, SDK will automatically calculate the applicable bit rate based on the input resolution and frame rate.

No stream will be encoded and published if you set this value to 0.

In 344 and later versions, the default value is \-1 for internal capturing, but no default value in versions earlier than 344.

<span id="ByteRTCVideoEncoderConfig-minbitrate"></span>
### minBitrate

```objectivec
@property(nonatomic, assign) NSInteger minBitrate;
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `minBitrate`.

It defaults to `0`.

It ranges within [0, maxBitrate). When `maxBitrate` < `minBitrate`, the bitrate is self\-adapted.

In the following circumstance, the assignment to this variable has no effect:


* When `maxBitrate` = `0`, the video encoding is disabled.

* When `maxBitrate` < `0`, the bitrate is self\-adapted.

    &nbsp;


<span id="keyframeintervalms"></span>
### keyFrameIntervalMS

```objectivec
@property(nonatomic, assign) NSInteger keyFrameIntervalMS;
```


Key frame interval in milliseconds. The default value is `0`.

<span id="ByteRTCVideoEncoderConfig-encoderpreference"></span>
### encoderPreference

```objectivec
@property(nonatomic, assign) ByteRTCVideoEncoderPreference encoderPreference;
```


Encoding preference. The default value is ByteRTCVideoEncoderPreferenceMaintainFramerate(1). See [ByteRTCVideoEncoderPreference](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderPreference).

<span id="ByteRTCVideoSimulcastStreamType"></span>
# ByteRTCVideoSimulcastStreamType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoSimulcastStreamType
)
```


The preference for the quality of the subscribed stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoSimulcastStreamTypeWeak |0 |The stream with the lowest quality, which has the lowest resolution. |
|ByteRTCVideoSimulcastStreamTypeLow |1 |The stream with a low quality. |
|ByteRTCVideoSimulcastStreamTypeMid |2 |The stream with a medium quality. |
|ByteRTCVideoSimulcastStreamTypeHigh |3 |The stream with the best quality. |


<span id="ByteRTCUserVisibilityChangeError"></span>
# ByteRTCUserVisibilityChangeError

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCUserVisibilityChangeError
)
```


User visibility state change error.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCUserVisibilityChangeErrorOk |0 |Success. |
|ByteRTCUserVisibilityChangeErrorUnknown |1 |Unknown error. |
|ByteRTCUserVisibilityChangeErrorTooManyVisibleUser |2 |Visible users in the room have reached the upper limit. |


<span id="ByteRTCLocalProxyType"></span>
# ByteRTCLocalProxyType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCLocalProxyType
)
```


Types of local proxies.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalProxyTypeSocks5 |1 |Socks5 proxy. If you chose Socks5 as the local proxy, you need to make sure all requirements listed in the Socks5 document are satisfied. |
|ByteRTCLocalProxyTypeHttpTunnel |2 |Http tunnel proxy. |


<span id="ByteRTCForwardStreamEventInfo"></span>
# ByteRTCForwardStreamEventInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCForwardStreamEventInfo: NSObject
```


Event from each room during relaying

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamEventInfo-roomid) |
|ByteRTCForwardStreamEvent |[event](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamEventInfo-event) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCForwardStreamEventInfo-roomid"></span>
### roomId

```objectivec
@property(strong, nonatomic) NSString* _Nullable roomId;
```


ID of the room to which the media stream is relayed

An empty string is for all rooms.

<span id="ByteRTCForwardStreamEventInfo-event"></span>
### event

```objectivec
@property(assign, nonatomic) ByteRTCForwardStreamEvent event;
```


Event from the room during relaying. Refer to [ByteRTCForwardStreamEvent](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamEvent) for more information.

<span id="ByteRTCLocalLogLevel"></span>
# ByteRTCLocalLogLevel

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCLocalLogLevel
)
```


Local log parameters.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalLogLevelInfo |0 |Info level. |
|ByteRTCLocalLogLevelWarning |1 |(Default) Warning level. |
|ByteRTCLocalLogLevelError |2 |Error level. |
|ByteRTCLocalLogLevelNone |3 |Turn off logging. |


<span id="ByteRTCLocalProxyState"></span>
# ByteRTCLocalProxyState

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCLocalProxyState
)
```


The states of local proxy connection.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalProxyStateInited |0 |TCP proxy server is connected. |
|ByteRTCLocalProxyStateConnected |1 |The local proxy is connected. |
|ByteRTCLocalProxyStateError |2 |Errors occurred when connecting to the local proxy. |


<span id="ByteRTCStreamIndex"></span>
# ByteRTCStreamIndex

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCStreamIndex
)
```


Reserved field.

<span id="ByteRTCSysStats"></span>
# ByteRTCSysStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCSysStats : NSObject
```


The cpu and memory information used by App

Information is periodically (2s) notified to the user by the SDK via the `reportSysStats` callback event.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|unsignedint |[cpuCores](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-cpucores) |
|double |[cpuAppUsage](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-cpuappusage) |
|double |[memoryUsage](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-memoryusage) |
|unsignedlonglong |[fullMemory](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-fullmemory) |
|unsignedlonglong |[totalMemoryUsage](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-totalmemoryusage) |
|unsignedlonglong |[freeMemory](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-freememory) |
|double |[memoryRatio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-memoryratio) |
|double |[totalMemoryRatio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSysStats-totalmemoryratio) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCSysStats-cpucores"></span>
### cpuCores

```objectivec
@property(assign, nonatomic) unsigned int cpuCores;
```


Current system cpu number

<span id="ByteRTCSysStats-cpuappusage"></span>
### cpuAppUsage

```objectivec
@property(assign, nonatomic) double cpuAppUsage;
```


The CPU usage of the current application, the value range is [0,1].

<span id="ByteRTCSysStats-memoryusage"></span>
### memoryUsage

```objectivec
@property(assign, nonatomic) double memoryUsage;
```


Memory usage of the current app (in MB)

<span id="ByteRTCSysStats-fullmemory"></span>
### fullMemory

```objectivec
@property(assign, nonatomic) unsigned long long fullMemory;
```


Full memory (in MB)

<span id="ByteRTCSysStats-totalmemoryusage"></span>
### totalMemoryUsage

```objectivec
@property(assign, nonatomic) unsigned long long totalMemoryUsage;
```


System used memory (in MB)

<span id="ByteRTCSysStats-freememory"></span>
### freeMemory

```objectivec
@property(assign, nonatomic) unsigned long long freeMemory;
```


Free allocable memory (in MB)

<span id="ByteRTCSysStats-memoryratio"></span>
### memoryRatio

```objectivec
@property(assign, nonatomic) double memoryRatio;
```


Memory usage of the current application (in %)

<span id="ByteRTCSysStats-totalmemoryratio"></span>
### totalMemoryRatio

```objectivec
@property(assign, nonatomic) double totalMemoryRatio;
```


System memory usage (in %)

<span id="ByteRTCVideoStreamState"></span>
# ByteRTCVideoStreamState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoStreamState
)
```


Sets the return state of the local video property.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoStreamStateSuccess |0 |Set local video properties successfully |
|ByteRTCVideoStreamStateInvalid |\-2 |Local video attribute parameter is invalid |


<span id="ByteRTCMixedStreamVideoConfig"></span>
# ByteRTCMixedStreamVideoConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamVideoConfig : NSObject
```


Video transcoding configurations.

With invalid or empty input, the configurations will be set as the default values.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCMixedStreamVideoCodecType |[videoCodec](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig-videocodec) |
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig-height) |
|NSInteger |[fps](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig-fps) |
|NSInteger |[gop](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig-gop) |
|NSInteger |[bitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig-bitrate) |
|BOOL |[enableBFrame](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoConfig-enablebframe) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamVideoConfig-videocodec"></span>
### videoCodec

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamVideoCodecType videoCodec;
```


The video codec. See [ByteRTCMixedStreamVideoCodecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamVideoCodecType). The default value is `0`. It's recommended to be set.

These parameters cannot be updated during the task.

<span id="ByteRTCMixedStreamVideoConfig-width"></span>
### width

```objectivec
@property(assign, nonatomic) NSInteger width;
```


The width (pixels) to be set. The range is [2, 1920], and must be an even number. The default value is 640 pixels. It's recommended to be set.

If an odd number is set, the width will be adjusted to the next larger even number.

<span id="ByteRTCMixedStreamVideoConfig-height"></span>
### height

```objectivec
@property(assign, nonatomic) NSInteger height;
```


The height (pixels) to be set. The range is [2, 1920], and must be an even number. The default value is 360 pixels. It's recommended to be set.

If an odd number is set, the height will be adjusted to the next larger even number.

<span id="ByteRTCMixedStreamVideoConfig-fps"></span>
### fps

```objectivec
@property(assign, nonatomic) NSInteger fps;
```


The frame rate (FPS) in the range of [1, 60]. The default value is 15 FPS. It's recommended to be set.

<span id="ByteRTCMixedStreamVideoConfig-gop"></span>
### gop

```objectivec
@property(assign, nonatomic) NSInteger gop;
```


The time interval between I\-frames (second) in the range of [1, 5]. The default value is 2 seconds. It's recommended to be set.

These parameters cannot be updated during the task.

<span id="ByteRTCMixedStreamVideoConfig-bitrate"></span>
### bitrate

```objectivec
@property(assign, nonatomic) NSInteger bitrate;
```


The bitrate (Kbps) in the range of [1, 10000]. The default value is self\-adaptive. It's recommended to be set.

<span id="ByteRTCMixedStreamVideoConfig-enablebframe"></span>
### enableBFrame

```objectivec
@property(assign, nonatomic) BOOL enableBFrame;
```


Whether to push streams with B frames. This is supported only by server\-side stream mixing.

<span id="ByteRTCVideoSourceType"></span>
# ByteRTCVideoSourceType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoSourceType
)
```


Video source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoSourceTypeExternal |0 |Custom video source |
|ByteRTCVideoSourceTypeInternal |1 |Internal video capture |
|ByteRTCVideoSourceTypeEncodedAutoSimulcast |2 |Custom encoded video source.<br><br>&nbsp;<br><br>Push the encoded video stream with the largest resolution, and the SDK will automatically transcode to generate multiple lower\-quality streams for Simulcast. |
|ByteRTCVideoSourceTypeEncodedManualSimulcast |3 |Custom encoded video source.<br><br>&nbsp;<br><br>The SDK does not automatically generate multiple streams for Simulcast, you need to generate and push streams of different qualities. |


<span id="ByteRTCUserOnlineStatus"></span>
# ByteRTCUserOnlineStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCUserOnlineStatus
)
```


User online status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCUserOnlineStatusOffline |0 |The peer user is offline<br><br>&nbsp;<br><br>The peer user has called `logout`, or has not called [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) to sign in |
|ByteRTCUserOnlineStatusOnline |1 |The peer user is online<br><br>&nbsp;<br><br>The peer user calls [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) to sign in and the connection status is normal |
|ByteRTCUserOnlineStatusUnreachable |2 |Unable to get the online state of the peer user<br><br>&nbsp;<br><br>Returned when a cascade error occurs and the online state of the peer user is abnormal |


<span id="ByteRTCVideoSimulcastMode"></span>
# ByteRTCVideoSimulcastMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoSimulcastMode
)
```


Multiple quality streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoSimulcastModeOnlyOne |0 |Single. The video stream is sent in only one set of specifications. |
|ByteRTCVideoSimulcastModeOnDemand |1 |On\-demand. The publisher will publish streams according to the subscriber's demands. When no subscription preference is taking effect, 2 streams will be published. |
|ByteRTCVideoSimulcastModeAlwaysSimulcast |2 |Manual. The publisher will publish streams in the qualities of the settings. The default is to publish 2 streams. |


<span id="ByteRTCMixedStreamLayoutRegionConfig"></span>
# ByteRTCMixedStreamLayoutRegionConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamLayoutRegionConfig : NSObject
```


Layout information for one of the video streams to be mixed.

After starting to push streams to CDN and mixing multiple video streams, you can set the layout information for each of them.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[userID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-userid) |
|NSString\* |[roomID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-roomid) |
|NSInteger |[locationX](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-locationx) |
|NSInteger |[locationY](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-locationy) |
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-height) |
|NSInteger |[zOrder](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-zorder) |
|BOOL |[isLocalUser](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-islocaluser) |
|ByteRTCMixedStreamVideoType |[streamType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-streamtype) |
|CGFloat |[alpha](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-alpha) |
|CGFloat |[cornerRadius](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-cornerradius) |
|ByteRTCMixedStreamMediaType |[mediaType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-mediatype) |
|ByteRTCMixedStreamRenderMode |[renderMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-rendermode) |
|ByteRTCMixedStreamLayoutRegionType |[regionContentType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-regioncontenttype) |
|NSData\* |[imageWaterMark](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-imagewatermark) |
|ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig\* |[imageWaterMarkConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-imagewatermarkconfig) |
|ByteRTCPosition\* |[spatialPosition](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-spatialposition) |
|BOOL |[applySpatialAudio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-appliespatialaudio) |
|ByteRTCMixedStreamAlternateImageFillMode |[alternateImageFillMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-alternateimagefillmode) |
|NSString\* |[alternateImageUrl](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-alternateimageurl) |
|ByteRTCSourceCropInfo\* |[sourceCrop](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-sourcecrop) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamLayoutRegionConfig-userid"></span>
### userID

```objectivec
@property(copy, nonatomic) NSString * _Nonnull userID;
```


The user ID of the user who publishes the video stream. It's recommended to be set.

<span id="ByteRTCMixedStreamLayoutRegionConfig-roomid"></span>
### roomID

```objectivec
@property(copy, nonatomic) NSString * _Nonnull roomID;
```


The room ID of the media stream. It's recommended to be set.

If the media stream is the stream forwarded by [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-startforwardstreamtorooms), you must set the roomID to the room ID of the target room.

<span id="ByteRTCMixedStreamLayoutRegionConfig-locationx"></span>
### locationX

```objectivec
@property(assign, nonatomic) NSInteger locationX;
```


The X\-coordinate in pixels of the upper\-left corner of the user's frame in the entire canvas coordinate system, where the origin is at the upper\-left corner of the canvas. It represents the horizontal displacement of the upper\-left corner of the user's frame relative to the origin.

The value range is [0, the width of the canvas). The default value is 0.

<span id="ByteRTCMixedStreamLayoutRegionConfig-locationy"></span>
### locationY

```objectivec
@property(assign, nonatomic) NSInteger locationY;
```


The Y\-coordinate in pixels of the upper\-left corner of the user's frame in the entire canvas coordinate system, where the origin is at the upper\-left corner of the canvas. It represents the vertical displacement of the upper\-left corner of the user's frame relative to the origin.

The value range is [0, the height of the canvas). The default value is 0.

<span id="ByteRTCMixedStreamLayoutRegionConfig-width"></span>
### width

```objectivec
@property(assign, nonatomic) NSInteger width;
```


The width of the user's frame in pixels. The value range is [0, the width of the canvas]. The default value is 360.

<span id="ByteRTCMixedStreamLayoutRegionConfig-height"></span>
### height

```objectivec
@property(assign, nonatomic) NSInteger height;
```


The height of the user's frame in pixels. The value range is [0, the height of the canvas]. The default value is 640.

<span id="ByteRTCMixedStreamLayoutRegionConfig-zorder"></span>
### zOrder

```objectivec
@property(assign, nonatomic) NSInteger zOrder;
```


The layer on which the video is rendered. The range is [0, 100]. 0 for the bottom layer, and 100 for the top layer. The default value is 0. It's recommended to be set.

<span id="ByteRTCMixedStreamLayoutRegionConfig-islocaluser"></span>
### isLocalUser

```objectivec
@property(assign, nonatomic) BOOL isLocalUser;
```


<span id="ByteRTCMixedStreamLayoutRegionConfig-streamtype"></span>
### streamType

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamVideoType streamType;
```


<span id="ByteRTCMixedStreamLayoutRegionConfig-alpha"></span>
### alpha

```objectivec
@property(assign, nonatomic) CGFloat alpha;
```


The opacity in the range of (0.0, 1.0]. The lower the value, the more transparent. The default value is 1.0.

<span id="ByteRTCMixedStreamLayoutRegionConfig-cornerradius"></span>
### cornerRadius

```objectivec
@property(assign, nonatomic) CGFloat cornerRadius;
```


The proportion of the radius to the width of the canvas. `0.0` by default.

After you set the value, `width_px`, `height_px`, and `cornerRadius_px` are calculated based on `width`, `height`, `cornerRadius`, and the width of the canvas. If `cornerRadius_px < min(width_px/2, height_px/2)` is met, the value of `cornerRadius` is set valid; if not, `cornerRadius_px` is set to `min(width_px/2, height_px/2)`, and `cornerRadius` is set to the proportion of `cornerRadius_px` to the width of the canvas.

This parameter is not supported for WTN stream tasks.

<span id="ByteRTCMixedStreamLayoutRegionConfig-mediatype"></span>
### mediaType

```objectivec
@property (assign, nonatomic) ByteRTCMixedStreamMediaType mediaType;
```


The stream mixing content type. The default value is `ByteRTCTranscoderContentControlTypeHasAudioAndVideo`. See [ByteRTCMixedStreamMediaType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamMediaType).

<span id="ByteRTCMixedStreamLayoutRegionConfig-rendermode"></span>
### renderMode

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamRenderMode renderMode;
```


The render mode. See [ByteRTCMixedStreamRenderMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamRenderMode). The default value is 1.

<span id="ByteRTCMixedStreamLayoutRegionConfig-regioncontenttype"></span>
### regionContentType

```objectivec
@property (assign, nonatomic) ByteRTCMixedStreamLayoutRegionType regionContentType;
```


Stream mixing region type. See [ByteRTCMixedStreamLayoutRegionType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionType). It's recommended to be set.

<span id="ByteRTCMixedStreamLayoutRegionConfig-imagewatermark"></span>
### imageWaterMark

```objectivec
@property (strong, nonatomic) NSData * _Nullable imageWaterMark;
```


The RGBA data of the watermark. It is required when the `regionContentType` is set to `ByteRTCMixedStreamLayoutRegionTypeImage`.

Put in null when you choose `ByteRTCMixedStreamLayoutRegionTypeVideoStream` as `regionContentType`.

This parameter is not supported for WTN stream tasks.

<span id="ByteRTCMixedStreamLayoutRegionConfig-imagewatermarkconfig"></span>
### imageWaterMarkConfig

```objectivec
@property (strong, nonatomic) ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig * _Nullable imageWaterMarkConfig;
```


The resolution of the watermark. It is required when the `regionContentType` is set to `ByteRTCMixedStreamLayoutRegionTypeImage`. See [ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig).

Put in null when you choose `ByteRTCMixedStreamLayoutRegionTypeVideoStream` as `regionContentType`.

This parameter is not supported for WTN stream tasks.

<span id="ByteRTCMixedStreamLayoutRegionConfig-spatialposition"></span>
### spatialPosition

```objectivec
@property (strong, nonatomic) ByteRTCPosition * _Nullable spatialPosition;
```


spatial position. See [ByteRTCPosition](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPosition).

<span id="ByteRTCMixedStreamLayoutRegionConfig-appliespatialaudio"></span>
### applySpatialAudio

```objectivec
@property(assign, nonatomic) BOOL applySpatialAudio;
```


Sets whether a user applies spatial audio effects:


* Yes: Yes (default setting)

* No: No

    &nbsp;


<span id="alternateimagefillmode"></span>
### alternateImageFillMode

```objectivec
@property (assign, nonatomic)ByteRTCMixedStreamAlternateImageFillMode alternateImageFillMode;
```


> Available since 3.57


Sets the fill mode of the placeholder image.

This parameter is used to control the fill mode of the placeholder image after the user stops publishing video streams and the screen reverts to the placeholder image. See [ByteRTCMixedStreamAlternateImageFillMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAlternateImageFillMode).

<span id="ByteRTCMixedStreamLayoutRegionConfig-alternateimageurl"></span>
### alternateImageUrl

```objectivec
@property(copy, nonatomic)NSString * alternateImageUrl;
```


> Available since 3.57


Sets the URL of the placeholder image, limited to a maximum of 1024 characters.

<span id="ByteRTCMixedStreamLayoutRegionConfig-sourcecrop"></span>
### sourceCrop

```objectivec
@property(strong, nonatomic) ByteRTCSourceCropInfo * _Nonnull sourceCrop;
```


Crop the stream before merging it into the WTN stream. See [ByteRTCSourceCropInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceCropInfo).

<span id="ByteRTCRoomStats"></span>
# ByteRTCRoomStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRoomStats : NSObject
```


Room call statistics, reference period is 2s.

After the user enters the room successfully, the SDK will periodically notify the user through `onRoomStats` callback statistics in the current room. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[duration](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-duration) |
|NSInteger |[txBytes](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-txbytes) |
|NSInteger |[rxBytes](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rxbytes) |
|NSInteger |[txKbitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-txkbitrate) |
|NSInteger |[rxKbitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rxkbitrate) |
|NSInteger |[txAudioKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-txaudiokbitrate) |
|NSInteger |[rxAudioKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rxaudiokbitrate) |
|NSInteger |[txVideoKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-txvideokbitrate) |
|NSInteger |[rxVideoKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rxvideokbitrate) |
|NSInteger |[txScreenKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-txscreenkbitrate) |
|NSInteger |[rxScreenKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rxscreenkbitrate) |
|NSInteger |[userCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-usercount) |
|float |[rxLostrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rxlostrate) |
|float |[txLostrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-txlostrate) |
|NSInteger |[rtt](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rtt) |
|NSInteger |[txCellularKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-txcellularkbitrate) |
|NSInteger |[rxCellularKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomStats-rxcellularkbitrate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRoomStats-duration"></span>
### duration

```objectivec
@property(assign, nonatomic) NSInteger duration;
```


The duration, in seconds, that the local user has spent in the room.

<span id="ByteRTCRoomStats-txbytes"></span>
### txBytes

```objectivec
@property(assign, nonatomic) NSInteger txBytes;
```


The total number of bytes sent by the local user (bytes), the cumulative value

<span id="ByteRTCRoomStats-rxbytes"></span>
### rxBytes

```objectivec
@property(assign, nonatomic) NSInteger rxBytes;
```


The total number of bytes received by the local user (bytes), the cumulative value

<span id="ByteRTCRoomStats-txkbitrate"></span>
### txKbitrate

```objectivec
@property(assign, nonatomic) NSInteger txKbitrate;
```


The instantaneous value of Tx bitrate in Kbps

<span id="ByteRTCRoomStats-rxkbitrate"></span>
### rxKbitrate

```objectivec
@property(assign, nonatomic) NSInteger rxKbitrate;
```


The instantaneous value of Rx bitrate in kbps

<span id="ByteRTCRoomStats-txaudiokbitrate"></span>
### txAudioKBitrate

```objectivec
@property(assign, nonatomic) NSInteger txAudioKBitrate;
```


Local user's audio transmission bit rate (kbps), instantaneous value

<span id="ByteRTCRoomStats-rxaudiokbitrate"></span>
### rxAudioKBitrate

```objectivec
@property(assign, nonatomic) NSInteger rxAudioKBitrate;
```


Local user's audio receiving bit rate (kbps), instantaneous value

<span id="ByteRTCRoomStats-txvideokbitrate"></span>
### txVideoKBitrate

```objectivec
@property(assign, nonatomic) NSInteger txVideoKBitrate;
```


Local user's video transmission bit rate (kbps), instantaneous value

<span id="ByteRTCRoomStats-rxvideokbitrate"></span>
### rxVideoKBitrate

```objectivec
@property(assign, nonatomic) NSInteger rxVideoKBitrate;
```


Local user's video receiving bit rate (kbps), instantaneous value

<span id="ByteRTCRoomStats-txscreenkbitrate"></span>
### txScreenKBitrate

```objectivec
@property(assign, nonatomic) NSInteger txScreenKBitrate;
```


The instantaneous TX bitrate of screen\-sharing video in Kbps

<span id="ByteRTCRoomStats-rxscreenkbitrate"></span>
### rxScreenKBitrate

```objectivec
@property(assign, nonatomic) NSInteger rxScreenKBitrate;
```


The instantaneous RX bitrate of screen\-sharing video in Kbps

<span id="ByteRTCRoomStats-usercount"></span>
### userCount

```objectivec
@property(assign, nonatomic) NSInteger userCount;
```


Number of visible users in the current room, including local users themselves

<span id="ByteRTCRoomStats-rxlostrate"></span>
### rxLostrate

```objectivec
@property(assign, nonatomic) float rxLostrate;
```


App Current downlink packet loss rate

<span id="ByteRTCRoomStats-txlostrate"></span>
### txLostrate

```objectivec
@property(assign, nonatomic) float txLostrate;
```


App current uplink packet loss rate

<span id="ByteRTCRoomStats-rtt"></span>
### rtt

```objectivec
@property(assign, nonatomic) NSInteger rtt;
```


Client side round\-trip time

<span id="ByteRTCRoomStats-txcellularkbitrate"></span>
### txCellularKBitrate

```objectivec
@property(assign, nonatomic) NSInteger txCellularKBitrate;
```


Cellular Link Send bit rate (kbps), get the instantaneous value of the data

<span id="ByteRTCRoomStats-rxcellularkbitrate"></span>
### rxCellularKBitrate

```objectivec
@property(assign, nonatomic) NSInteger rxCellularKBitrate;
```


Cellular Link Receive bit rate (kbps), get the instantaneous value of the data

<span id="ByteRTCAudioRecordingState"></span>
# ByteRTCAudioRecordingState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioRecordingState
)
```


Audio recording config

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioRecordingStateError |0 |Recording exception |
|ByteRTCAudioRecordingStateProcessing |1 |Recording in progress |
|ByteRTCAudioRecordingStateSuccess |2 |The recording task ends, and the file is saved. |


<span id="ByteRTCMediaDeviceState"></span>
# ByteRTCMediaDeviceState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMediaDeviceState
)
```


Media device state

You will be informed of device state by `rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:` or `rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaDeviceStateStarted |1 |On |
|ByteRTCMediaDeviceStateStopped |2 |Off |
|ByteRTCMediaDeviceStateRuntimeError |3 |Runtime error<br><br>&nbsp;<br><br>For example, when the media device is expected to be working but no data is received. |
|ByteRTCMediaDeviceStateAdded |10 |Added<br><br>&nbsp;<br><br>Call enumerate\-device api to update the device list when you get this notification. |
|ByteRTCMediaDeviceStateRemoved |11 |Removed<br><br>&nbsp;<br><br>Call enumerate\-device api to update the device list when you get this notification. |
|ByteRTCMediaDeviceStateInterruptionBegan |12 |Phone calls, locking screen or the other Apps interrupted the RTC call. RTC call will resume once the call ends or the other Apps release the media devices. |
|ByteRTCMediaDeviceStateInterruptionEnded |13 |RTC call resumed from the interruption caused by the phone calls or the other Apps. |
|ByteRTCMediaDeviceListUpdated |16 |Notification of receiving the device list after time\-out.<br><br>&nbsp;<br><br>Call enumerate\-device api to update the device list when you get this notification. |


<span id="ByteRTCAudioRoute"></span>
# ByteRTCAudioRoute

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioRoute
)
```


Audio playback device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioRouteDefault |\-1 |The audio route set by `setDefaultAudioRoute:`, or the AirPlay device. |
|ByteRTCAudioRouteHeadset |1 |Wired earphones |
|ByteRTCAudioRouteEarpiece |2 |Earpiece. Built\-in device for calling |
|ByteRTCAudioRouteSpeakerphone |3 |Speaker. Built\-in device for hands\-free audio playing |
|ByteRTCAudioRouteHeadsetBluetooth |4 |Bluetooth earphones |
|ByteRTCAudioRouteHeadsetUSB |5 |\- |


<span id="ByteRtcScreenCapturerExt"></span>
# ByteRtcScreenCapturerExt

```objectivec
BYTE_RTC_EXPORT @interface ByteRtcScreenCapturerExt : NSObject
```


Screen capture related extension examples, for SDK internal capture only.

The SampleHandler generated by the user after creating the extension needs to implement screen sharing related capabilities through this instance.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRtcScreenCapturerExt\* |[shared](https://docs.byteplus.com/en/docs/12/14181#ByteRtcScreenCapturerExt-shared) |
|NSObject<ByteRtcScreenCapturerExtDelegate\>\* |[delegate](https://docs.byteplus.com/en/docs/12/14181#ByteRtcScreenCapturerExt-delegate) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[startWithDelegate:groupId:](https://docs.byteplus.com/en/docs/12/14181#ByteRtcScreenCapturerExt-startwithdelegate-groupid) |
|void |[stop](https://docs.byteplus.com/en/docs/12/14181#ByteRtcScreenCapturerExt-stop) |
|void |[processSampleBuffer:withType:](https://docs.byteplus.com/en/docs/12/14181#ByteRtcScreenCapturerExt-processsamplebuffer-withtype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRtcScreenCapturerExt-shared"></span>
### shared

```objectivec
@property (readonly, class) ByteRtcScreenCapturerExt *shared;
```


Read\-only variable to get the ByteRtcScreenCapturerExt instance.

<span id="ByteRtcScreenCapturerExt-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak, nullable) NSObject<ByteRtcScreenCapturerExtDelegate> *delegate;
```


Callback agent for ByteRtcScreenCapturerExt instance.

<span id="instructions"></span>
## Instructions

<span id="ByteRtcScreenCapturerExt-startwithdelegate-groupid"></span>
### startWithDelegate:groupId:

```objectivec
- (void)startWithDelegate:(NSObject<ByteRtcScreenCapturerExtDelegate>*)delegate groupId:(NSString*)groupId;
```


Start screen capture

After the Extension is started, the system will automatically call this method to enable screen capture.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|delegate |NSObject<ByteRtcScreenCapturerExtDelegate\>\* |Callback agent, see [ByteRtcScreenCapturerExtDelegate](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRtcScreenCapturerExtDelegate) |
|groupId |NSString\* |The group ID set in App groups |


<span id="ByteRtcScreenCapturerExt-stop"></span>
### stop

```objectivec
- (void)stop;
```


Stop screen capture

After the Extension is closed, the system will automatically call this method to stop screen capture.

<span id="ByteRtcScreenCapturerExt-processsamplebuffer-withtype"></span>
### processSampleBuffer:withType:

```objectivec
- (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType API_AVAILABLE(ios(10));
```


Push data captured by Extension

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|sampleBuffer |CMSampleBufferRef |Captured data |
|sampleBufferType |RPSampleBufferType |Data type |


<span id="ByteRTCVideoDecoderConfig"></span>
# ByteRTCVideoDecoderConfig

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoDecoderConfig
)
```


Video decoding method

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoDecoderConfigRaw |0 |Enable SDK internal decoding, only returns the decoded data via callback |
|ByteRTCVideoDecoderConfigEncode |1 |Turn on custom decoding, only callback the data before decoding |
|ByteRTCVideoDecoderConfigBoth |2 |Enable SDK internal decoding, and call back the data before and after decoding at the same time |


<span id="ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig"></span>
# ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig : NSObject
```


Resolution of the watermark image.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[imageWidth](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig-imagewidth) |
|NSInteger |[imageHeight](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig-imageheight) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig-imagewidth"></span>
### imageWidth

```objectivec
@property (assign, nonatomic) NSInteger imageWidth;
```


Width of the original image in px.

<span id="ByteRTCMixedStreamLayoutRegionImageWaterMarkConfig-imageheight"></span>
### imageHeight

```objectivec
@property (assign, nonatomic) NSInteger imageHeight;
```


Height of the original image in px.

<span id="ByteRTCVideoPixelFormat"></span>
# ByteRTCVideoPixelFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoPixelFormat
)
```


video frame pixel format

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoPixelFormatUnknown |0 |Unknown format |
|ByteRTCVideoPixelFormatI420 |1 |YUV I420 |
|ByteRTCVideoPixelFormatNV12 |2 |YUV NV12 |
|ByteRTCVideoPixelFormatNV21 |3 |YUV NV21 |
|ByteRTCVideoPixelFormatRGB24 |4 |RGB 24bit |
|ByteRTCVideoPixelFormatRGBA |5 |RGBA |
|ByteRTCVideoPixelFormatARGB |6 |ARGB |
|ByteRTCVideoPixelFormatBGRA |7 |BGRA |
|ByteRTCVideoPixelFormatEndMark |0xFF |End mark. Newly added pixel formats should have values less than ByteRTCVideoPixelFormatEndMark. |
|ByteRTCVideoPixelFormatTexture2D |0x0DE1 |Texture2D |
|ByteRTCVideoPixelFormatTextureOES |0x8D65 |TextureOES |


<span id="ByteRTCEncryptType"></span>
# ByteRTCEncryptType

```objectivec
typedef NS_OPTIONS(
    NSUInteger,
    ByteRTCEncryptType
)
```


Custom encryption type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCEncryptTypeCustomize |0 |Built\-in encryption is not used. Default value. |
|ByteRTCEncryptTypeAES128CBC |1 |AES\-128\-CBC encryption algorithm |
|ByteRTCEncryptTypeAES256CBC |2 |AES\-256\-CBC encryption algorithm |
|ByteRTCEncryptTypeAES128ECB |3 |AES\-128\-ECB encryption algorithm |
|ByteRTCEncryptTypeAES256ECB |4 |AES\-256\-ECB encryption algorithm |


<span id="ByteRTCMixedStreamTaskEvent"></span>
# ByteRTCMixedStreamTaskEvent

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMixedStreamTaskEvent
)
```


Events related to mixed stream task

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamTaskEventStartSuccess |1 |The task initiated successfully. |
|ByteRTCMixedStreamTaskEventStartFailed |2 |Failed to initiate the task. |
|ByteRTCMixedStreamTaskEventUpdateSuccess |3 |The task updated successfully. |
|ByteRTCMixedStreamTaskEventUpdateFailed |4 |Failed to update the task. |
|ByteRTCMixedStreamTaskEventStopSuccess |5 |The task stopped. |
|ByteRTCMixedStreamTaskEventStopFailed |6 |Failed to stop the task. |
|ByteRTCMixedStreamTaskEventWarning |7 |Warnings |


<span id="ByteRTCLocalProxyError"></span>
# ByteRTCLocalProxyError

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCLocalProxyError
)
```


The errors of local proxy connection.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalProxyErrorOK |0 |There are no errors in local proxies. |
|ByteRTCLocalProxyErrorSocks5VersionError |1 |The connection to Socks5 proxy failed because the proxy server replies wrong version numbers which don't accord with the Socks5 document. Please check the proxy server. |
|ByteRTCLocalProxyErrorSocks5FormatError |2 |The connection to Socks5 proxy failed because the format of the proxy's replies does not accord with the Socks5 document. Please check the proxy server. |
|ByteRTCLocalProxyErrorSocks5InvalidValue |3 |The connection to Socks5 proxy failed because the proxy replies wrong information which does not accord with the Socks5 document. Please check the proxy server. |
|ByteRTCLocalProxyErrorSocks5UserPassNotGiven |4 |The connection to Socks5 proxy failed because the username and password of the local proxy are not provided. Please call `setLocalProxy` and enter your username and password. |
|ByteRTCLocalProxyErrorSocks5TcpClosed |5 |The connection to Socks5 proxy failed because TCP is closed. Please check the proxy server and your network connection status. |
|ByteRTCLocalProxyErrorHttpTunnelFailed |6 |Errors in Http tunnel proxy. Please check Http tunnel proxy and your network connection status. |


<span id="ByteRTCWTNSubscribeState"></span>
# ByteRTCWTNSubscribeState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCWTNSubscribeState
)
```


State for WTN streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCWTNSubscribeStateSubscribe |0 |Subscribe WTN media stream |
|ByteRTCWTNSubscribeStateUnsubscribe |1 |Unsubscribe WTN media stream |


<span id="ByteRTCBluetoothMode"></span>
# ByteRTCBluetoothMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCBluetoothMode
)
```


The Bluetooth profiles.

<span id="enumerated-value"></span>
## Enumerated Value


|The default mode:<br><br>&nbsp;<br><br>&nbsp;<br><br> | | |
|---|---|---|
|ByteRTCBluetoothModeA2DP |1 |Advanced Audio Distribution Profile(A2DP). This profile defines how high\-quality audio (stereo or mono) can be streamed from one device to another over a Bluetooth connection. Audio is captured by your iOS device and played by your Bluetooth device. |
|ByteRTCBluetoothModeHFP |2 |Hands\-Free Profile(HFP). This profile defines how voice\-quality, mono audio can be streamed from one device to another. Audio is captured and played by your Bluetooth device. |


<span id="ByteRTCVideoContentType"></span>
# ByteRTCVideoContentType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoContentType
)
```


Video content type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoContentTypeNormalFrame |0 |Normal video |
|ByteRTCVideoContentTypeBlackFrame |1 |Black frame video |


<span id="ByteRTCRemoteVideoStats"></span>
# ByteRTCRemoteVideoStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteVideoStats : NSObject
```


Remote video stream statistics, reference period 2s.

After the remote user subscribes to the remote video stream successfully, the SDK will periodically notify the remote user of the reception status of the subscribed remote video stream during this reference period through `onRemoteStreamStats`

. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-height) |
|float |[videoLossRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-videolossrate) |
|float |[receivedKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-receivedkbitrate) |
|NSInteger |[receivedFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-receivedframerate) |
|NSInteger |[decoderOutputFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-decoderoutputframerate) |
|NSInteger |[renderOutputFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-renderoutputframerate) |
|NSInteger |[stallCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-stallcount) |
|NSInteger |[stallDuration](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-stallduration) |
|NSInteger |[e2eDelay](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-e2edelay) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-isscreen) |
|NSInteger |[statsInterval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-statsinterval) |
|NSInteger |[rtt](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-rtt) |
|NSInteger |[frozenRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-frozenrate) |
|ByteRTCVideoCodecType |[codecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-codectype) |
|NSInteger |[videoIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-videoindex) |
|NSInteger |[jitter](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-jitter) |
|NSInteger |[capToRenderDelay](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-captorenderdelay) |
|NSInteger |[avSyncDiffMs](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-avsyncdiffms) |
|NSInteger |[codecElapsePerFrame](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats-codecelapseperframe) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteVideoStats-width"></span>
### width

```objectivec
@property(assign, nonatomic) NSInteger width;
```


Remote video width.

<span id="ByteRTCRemoteVideoStats-height"></span>
### height

```objectivec
@property(assign, nonatomic) NSInteger height;
```


Remote video height.

<span id="ByteRTCRemoteVideoStats-videolossrate"></span>
### videoLossRate

```objectivec
@property(assign, nonatomic) float videoLossRate;
```


Remote video packet loss rate. The video downlink packet loss rate in the reference period, the value range is [0,1].

<span id="ByteRTCRemoteVideoStats-receivedkbitrate"></span>
### receivedKBitrate

```objectivec
@property(assign, nonatomic) float receivedKBitrate;
```


Receiving bit rate. Video reception rate within the reference period, in kbps.

<span id="ByteRTCRemoteVideoStats-receivedframerate"></span>
### receivedFrameRate

```objectivec
@property(assign, nonatomic) NSInteger receivedFrameRate;
```


Remote video receiving frame rate.

<span id="ByteRTCRemoteVideoStats-decoderoutputframerate"></span>
### decoderOutputFrameRate

```objectivec
@property(assign, nonatomic) NSInteger decoderOutputFrameRate;
```


Remote video decoding output frame rate.

<span id="ByteRTCRemoteVideoStats-renderoutputframerate"></span>
### renderOutputFrameRate

```objectivec
@property(assign, nonatomic) NSInteger renderOutputFrameRate;
```


Remote video rendering output frame rate.

<span id="ByteRTCRemoteVideoStats-stallcount"></span>
### stallCount

```objectivec
@property(assign, nonatomic) NSInteger stallCount;
```


The number of remote video freezes.

<span id="ByteRTCRemoteVideoStats-stallduration"></span>
### stallDuration

```objectivec
@property(assign, nonatomic) NSInteger stallDuration;
```


Remote video lag duration, in ms.

<span id="ByteRTCRemoteVideoStats-e2edelay"></span>
### e2eDelay

```objectivec
@property(assign, nonatomic) NSInteger e2eDelay;
```


End\-to\-end latency at the user experience level. The delay from the completion of encoding at the transmitting end to the completion of decoding at the receiving end, in units of ms.

<span id="ByteRTCRemoteVideoStats-isscreen"></span>
### isScreen

```objectivec
@property(assign, nonatomic) BOOL isScreen;
```


Reserved field. Ignore the value returned in this field.

<span id="ByteRTCRemoteVideoStats-statsinterval"></span>
### statsInterval

```objectivec
@property(assign, nonatomic) NSInteger statsInterval;
```


Statistical interval, the interval of this reference period, in ms.

This field is used to set the reference period for the callback, currently set to 2s.

<span id="ByteRTCRemoteVideoStats-rtt"></span>
### rtt

```objectivec
@property(assign, nonatomic) NSInteger rtt;
```


Round\-trip time. The unit is ms.

<span id="ByteRTCRemoteVideoStats-frozenrate"></span>
### frozenRate

```objectivec
@property(assign, nonatomic) NSInteger frozenRate;
```


The cumulative duration of video freeze for the remote user accounts for the percentage (%) of the total effective duration of the video after entering the room. The effective duration of the video refers to the duration of the video other than stopping sending the video stream and disabling the video module after the remote user enters the room to publish the video stream.

<span id="ByteRTCRemoteVideoStats-codectype"></span>
### codecType

```objectivec
@property(nonatomic) ByteRTCVideoCodecType codecType;
```


For the encoding type of the video, please refer to [ByteRTCVideoCodecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCodecType).

<span id="ByteRTCRemoteVideoStats-videoindex"></span>
### videoIndex

```objectivec
@property(assign, nonatomic) NSInteger videoIndex;
```


The resolution subscript of the SDK subscribed remote video stream.

<span id="ByteRTCRemoteVideoStats-jitter"></span>
### jitter

```objectivec
@property(assign, nonatomic) NSInteger jitter;
```


Video downlink network jitter in ms.

<span id="ByteRTCRemoteVideoStats-captorenderdelay"></span>
### capToRenderDelay

```objectivec
@property(assign, nonatomic) NSInteger capToRenderDelay;
```


End\-to\-end latency at the user experience level. The delay from the start of capturing at the sending end to the completion of rendering at the receiving end, in units of ms.

<span id="ByteRTCRemoteVideoStats-avsyncdiffms"></span>
### avSyncDiffMs

```objectivec
@property(assign, nonatomic) NSInteger avSyncDiffMs;
```


Audio/video synchronization diff in ms.

<span id="ByteRTCRemoteVideoStats-codecelapseperframe"></span>
### codecElapsePerFrame

```objectivec
@property(assign, nonatomic) NSInteger codecElapsePerFrame;
```


Average time spent on video decoding in ms.

<span id="ByteRTCFrameExtendedData"></span>
# ByteRTCFrameExtendedData

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCFrameExtendedData : NSObject
```


Attached data obtained after video decoding

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCDataFrameType |[frameType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFrameExtendedData-frametype) |
|NSData\* |[extendedData](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFrameExtendedData-extendeddata) |
|NSInteger |[extendedDataLen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFrameExtendedData-extendeddatalen) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCFrameExtendedData-frametype"></span>
### frameType

```objectivec
@property(assign, nonatomic) ByteRTCDataFrameType frameType;
```


Data type. See [ByteRTCDataFrameType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCDataFrameType).

<span id="ByteRTCFrameExtendedData-extendeddata"></span>
### extendedData

```objectivec
@property(strong, nonatomic) NSData * _Nullable extendedData;
```


Attached data

<span id="ByteRTCFrameExtendedData-extendeddatalen"></span>
### extendedDataLen

```objectivec
@property(assign, nonatomic) NSInteger extendedDataLen;
```


Data length

<span id="ByteRTCRoomConfig"></span>
# ByteRTCRoomConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRoomConfig : NSObject
```


Room configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCRoomProfile |[profile](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomConfig-profile) |
|ByteRTCRoomLiveMode |[liveMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomConfig-livemode) |
|NSString\* |[streamId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomConfig-streamid) |
|BOOL |[isPublishAudio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomConfig-ispublishaudio) |
|BOOL |[isPublishVideo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomConfig-ispublishvideo) |
|BOOL |[isAutoSubscribeAudio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomConfig-isautosubscribeaudio) |
|BOOL |[isAutoSubscribeVideo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomConfig-isautosubscribevideo) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRoomConfig-profile"></span>
### profile

```objectivec
@property(nonatomic) ByteRTCRoomProfile profile;
```


Room profile. See [ByteRTCRoomProfile](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomProfile). The default is `ByteRTCRoomProfileCommunication`. The setting cannot be changed after joining the room.

<span id="ByteRTCRoomConfig-livemode"></span>
### liveMode

```objectivec
@property(nonatomic) ByteRTCRoomLiveMode liveMode;
```


live streaming mode. See [ByteRTCRoomLiveMode](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoomLiveMode). The default is `ByteRTCRoomLiveModeCoHost`. The setting can be changed after joining the room.

**Notes**

If `room_profile_type` is not `ByteRTCRoomProfileTypeLive`, `live_mode` is invalid.

<span id="ByteRTCRoomConfig-streamid"></span>
### streamId

```objectivec
@property(nonatomic) NSString * streamId;
```


Stream ID. The default is an empty string.

<span id="ByteRTCRoomConfig-ispublishaudio"></span>
### isPublishAudio

```objectivec
@property(assign, nonatomic) BOOL isPublishAudio;
```


Whether to automatically subscribe to the audio stream. The default is automatic subscription.


* Changing the user role to audience via `setUserVisibility` will void this setting.

* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only.

    &nbsp;


<span id="ispublishvideo"></span>
### isPublishVideo

```objectivec
@property(assign, nonatomic) BOOL isPublishVideo;
```


Whether to publish media streams automatically. The default is automatic publishing.


* Changing the user role to audience via [setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-setuservisibility) will void this setting.

* You can publish streams in only one of the rooms you have participated. If you have joined multiple rooms with the automatically publishing setting, the stream will be added into the first room you have joined only.

    &nbsp;


<span id="isautosubscribeaudio"></span>
### isAutoSubscribeAudio

```objectivec
@property(assign, nonatomic) BOOL isAutoSubscribeAudio;
```


Whether to automatically subscribe to the audio stream. The default is automatic subscription.

This setting affects both the main stream and the screen\-sharing stream.

<span id="ByteRTCRoomConfig-isautosubscribevideo"></span>
### isAutoSubscribeVideo

```objectivec
@property(assign, nonatomic) BOOL isAutoSubscribeVideo;
```


Whether to automatically subscribe to the video stream. The default is automatic subscription.

This setting affects both the main stream and the screen\-sharing stream.

<span id="ByteRTCScreenCaptureSourceInfo"></span>
# ByteRTCScreenCaptureSourceInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCScreenCaptureSourceInfo : NSObject
```


Screen capture object information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCScreenCaptureSourceType |[sourceType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceInfo-sourcetype) |
|intptr_t |[sourceId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceInfo-sourceid) |
|NSString\* |[sourceName](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceInfo-sourcename) |
|NSString\* |[application](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceInfo-application) |
|int |[pid](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceInfo-pid) |
|BOOL |[primaryMonitor](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceInfo-primarymonitor) |
|CGRect |[regionRect](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceInfo-regionrect) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCScreenCaptureSourceInfo-sourcetype"></span>
### sourceType

```objectivec
@property (assign, nonatomic) ByteRTCScreenCaptureSourceType sourceType;
```


The type of the sharing screen. See [ByteRTCScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureSourceType).

<span id="ByteRTCScreenCaptureSourceInfo-sourceid"></span>
### sourceId

```objectivec
@property (assign, nonatomic) intptr_t sourceId;
```


ID of the sharing object

<span id="ByteRTCScreenCaptureSourceInfo-sourcename"></span>
### sourceName

```objectivec
@property (copy, nonatomic) NSString * _Nullable sourceName;
```


Name of the sharing screen

<span id="ByteRTCScreenCaptureSourceInfo-application"></span>
### application

```objectivec
@property (copy, nonatomic) NSString * _Nullable application;
```


The title of the application to be shared.

Only available if the sharing object is an application window.

<span id="ByteRTCScreenCaptureSourceInfo-pid"></span>
### pid

```objectivec
@property (assign, nonatomic) int pid;
```


Process pid of the application to be shared.

Only available if the sharing object is an application window.

<span id="ByteRTCScreenCaptureSourceInfo-primarymonitor"></span>
### primaryMonitor

```objectivec
@property (assign, nonatomic) BOOL primaryMonitor;
```


Tag for the screen to be shared identifying whether it is the primary screen

Only available when the screen\-sharing object is a screen.

<span id="ByteRTCScreenCaptureSourceInfo-regionrect"></span>
### regionRect

```objectivec
@property (assign, nonatomic) CGRect regionRect;
```


Coordinate of the screen\-sharing object. (0, 0), the origin is the top left on the main screen for clients with multiple screens.

<span id="ByteRTCLocalVideoSinkPosition"></span>
# ByteRTCLocalVideoSinkPosition

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCLocalVideoSinkPosition
)
```


The position of the local video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalVideoSinkPositionAfterCapture |0 |After capturing. |
|ByteRTCLocalVideoSinkPositionAfterPreprocess |1 |(Default) After preprocessing. |


<span id="ByteRTCBandFrequency"></span>
# ByteRTCBandFrequency

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCBandFrequency
)
```


Audio Equalization effect.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCBandFrequency31 |0 |The frequency band with a center frequency of 31Hz. |
|ByteRTCBandFrequency62 |1 |The frequency band with a center frequency of 62Hz. |
|ByteRTCBandFrequency125 |2 |The frequency band with a center frequency of 125Hz. |
|ByteRTCBandFrequency250 |3 |The frequency band with a center frequency of 250Hz. |
|ByteRTCBandFrequency500 |4 |The frequency band with a center frequency of 500Hz. |
|ByteRTCBandFrequency1k |5 |The frequency band with a center frequency of 1kHz. |
|ByteRTCBandFrequency2k |6 |The frequency band with a center frequency of 2kHz. |
|ByteRTCBandFrequency4k |7 |The frequency band with a center frequency of 4kHz. |
|ByteRTCBandFrequency8k |8 |The frequency band with a center frequency of 8kHz. |
|ByteRTCBandFrequency16k |9 |The frequency band with a center frequency of 16kHz. |


<span id="ByteRTCInterpolationMode"></span>
# ByteRTCInterpolationMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCInterpolationMode
)
```


Interpolation mode of the WTN stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCInterpolationModeLastFrameFill |0 |Fill with the last frame. |
|ByteRTCInterpolationModeBackgroundImageFill |1 |Fill with the background image. |


<span id="ByteRTCAudioDumpStatus"></span>
# ByteRTCAudioDumpStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioDumpStatus
)
```


audio dump status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioDumpStartFailure |0 |audio dump start failure |
|ByteRTCAudioDumpStartSuccess |1 |audio dump start success |
|ByteRTCAudioDumpStopFailure |2 |audio dump stop failure |
|ByteRTCAudioDumpStopSuccess |3 |audio dump stop success |
|ByteRTCAudioDumpRunningFailure |4 |audio dump running failure |
|ByteRTCAudioDumpRunningSuccess |5 |audio dump running success |


<span id="ByteRTCAudioProfileType"></span>
# ByteRTCAudioProfileType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioProfileType
)
```


Sound quality

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioProfileDefault |0 |Default sound quality<br><br>&nbsp;<br><br>The sound quality configuration of [ByteRTCRoomProfile](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomProfile) set by the server or client. |
|ByteRTCAudioProfileFluent |1 |Fluent<br><br>&nbsp;<br><br>Sample rate: 16 KHz<br><br>&nbsp;<br><br>Mono\-channel<br><br>&nbsp;<br><br>Encoding bitrate: 32 Kbps<br><br>&nbsp;<br><br>Low resource consumption, and small network packets guarantee a smooth call. It is suitable for most game scenarios, such as team\-wide voice chat, group\-wide voice chat, nation\-wide voice chat. |
|ByteRTCAudioProfileStandard |2 |Mono\-channel standard<br><br>&nbsp;<br><br>Sample rate: 24 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 48 Kbps<br><br>&nbsp;<br><br>For scenarios requiring distinct voice, you can choose this mode, which achieves balanced latency, consumption, and network packets. It is suitable for educational Apps and the online Mafia Games. |
|ByteRTCAudioProfileHD |3 |Dual\-channel music<br><br>&nbsp;<br><br>Sample rate: 48 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 128 Kbps<br><br>&nbsp;<br><br>This mode provides high\-resolution audio at a cost of high latency, consumption, and large network packets. It is suitable for music Apps such as co\-hosting and online talent contests.<br><br>&nbsp;<br><br>Not recommended for game Apps. |
|ByteRTCAudioProfileStandardStereo |4 |Dual\-channel standard<br><br>&nbsp;<br><br>Sample rate: 48 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 80 Kbps |
|ByteRTCAudioProfileHDMono |5 |Mono\-channel music<br><br>&nbsp;<br><br>Sample rate: 48 KHz<br><br>&nbsp;<br><br>Encoding bitrate: 64 Kbps |


<span id="ByteRTCAggregationOption"></span>
# ByteRTCAggregationOption

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAggregationOption
)
```


> Available since 3.56


stream aggregation strategy

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAggregationOptionMin |0 |Stream Aggregation with the lowest resolution.(Default Strategy) |
|ByteRTCAggregationOptionMax |1 |Stream Aggregation with the highest resolution. |
|ByteRTCAggregationOptionMajority |2 |Stream Aggregation according to the proportions, and when the proportions are the same, it takes the lowest resolution. |


<span id="ByteRTCMediaStreamType"></span>
# ByteRTCMediaStreamType

```objectivec
typedef NS_OPTIONS(
    NSUInteger,
    ByteRTCMediaStreamType
)
```


Media stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaStreamTypeAudio |1 << 0 |Controls audio only |
|ByteRTCMediaStreamTypeVideo |1 << 1 |Controls video only |
|ByteRTCMediaStreamTypeBoth |ByteRTCMediaStreamTypeAudio \| ByteRTCMediaStreamTypeVideo |Controls both audio and video |


<span id="ByteRTCEchoTestResult"></span>
# ByteRTCEchoTestResult

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCEchoTestResult
)
```


Call test result

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCEchoTestResultSuccess |0 |The playback of captured audio/video is received, test succeeds. |
|ByteRTCEchoTestResultTimeout |1 |Test is not completed after 60 seconds and has been stopped automatically. |
|ByteRTCEchoTestResultIntervalShort |2 |Less than 5s between the end of the last test and the start of the next test. |
|ByteRTCEchoTestResultAudioDeviceError |3 |Audio capture error |
|ByteRTCEchoTestResultVideoDeviceError |4 |Video capture error |
|ByteRTCEchoTestResultAudioReceiveError |5 |Audio reception error |
|ByteRTCEchoTestResultVideoReceiveError |6 |Video reception error |
|ByteRTCEchoTestResultInternalError |7 |Unrecoverable internal error |


<span id="ByteRTCRoomProfile"></span>
# ByteRTCRoomProfile

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRoomProfile
)
```


Room profile

Choose an appropriate room\-profile option to meet the requirement of the scenario for media encoding algorithm, video profiles, and network configurations.

Call `setAudioProfile` to apply another audio quality option.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRoomProfileCommunication |0 |General mode by default<br><br>&nbsp;<br><br>It is equivalent to `ByteRTCRoomProfileMeeting = 16`.<br><br>&nbsp;<br><br>Contact us to alter the default settings. |
|ByteRTCRoomProfileGame |2 |Game voice mode. Low consumption of computing resources and network data<br><br>&nbsp;<br><br>Additional performance optimizations have been made for low\-end devices:<br><br><br>&nbsp;<br><br>* Encodes frame length 40/60 for some low\-end models.<br><br>* Disables software 3A audio processing for some low\-end models.<br><br>   Enhance iOS Compatibility with other screen recordings to avoid audio recordings being interrupted by RTC. |
|ByteRTCRoomProfileCloudGame |3 |Cloud game mode.<br><br>&nbsp;<br><br>Use this mode for game App requiring low latency.<br><br>&nbsp;<br><br>During poor network connection, communication experiences get worse with this mode. |
|ByteRTCRoomProfileLowLatency |4 |Cloud render mode featuring extra\-low latency.<br><br>&nbsp;<br><br>Choose this mode if it is not a game App yet requires low latency.<br><br>&nbsp;<br><br>In this mode, latency will significantly decrease at the cost of lower audio quality as well as the bad performance with weak network signal. |
|ByteRTCRoomProfileChatRoom |6 |For video and audio chat rooms of 3 or more people |
|ByteRTCRoomProfileInteractivePodcast |10 |For interactive podcasts that the host can have video and audio interactions with the audience. The voice mode is set to communication mode to avoid volume spiking and dipping acutely. |
|ByteRTCRoomProfileChorus |12 |For the online\-chorusing scenarios requiring high\-quality audio and low latency. Contact our technical specialists before you apply it to your App. |
|ByteRTCRoomProfileGameStreaming |14 |For scenarios of streaming live videos to only one client on the LAN. It can be applied to devices on the Internet or LAN. |
|ByteRTCRoomProfileMeeting |16 |For meeting Apps installed on personal devices |
|ByteRTCRoomProfileMeetingRoom |17 |For meeting Apps installed on terminals of meeting rooms, such as Rooms. |
|ByteRTCRoomProfileClassroom |18 |For the online classrooms and lectures that over 10 participants in the room are allowed to join the video chat. |
|ByteRTCRoomProfileCall |19 |Focus on smoothness, the default video bitrate is lower. |
|ByteRTCRoomProfileLive |20 |Focus on quality, the default video bitrate is higher. |


<span id="ByteRTCPositionInfo"></span>
# ByteRTCPositionInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCPositionInfo : NSObject
```


Information on the user's position in the rectangular coordinate system for the spatial audio.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCPosition\* |[position](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPositionInfo-position) |
|ByteRTCHumanOrientation\* |[orientation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPositionInfo-orientation) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCPositionInfo-position"></span>
### position

```objectivec
@property(strong, nonatomic) ByteRTCPosition *_Nonnull position;
```


3D coordinate values of the user's position in the rectangular coordinate system for the spatial audio. You need to build your own rectangular coordinate system. Refer to [ByteRTCPosition](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPosition) for details.

<span id="ByteRTCPositionInfo-orientation"></span>
### orientation

```objectivec
@property(strong, nonatomic) ByteRTCHumanOrientation *_Nonnull orientation;
```


Information on the three\-dimensional orientation of the user in the rectangular coordinate system for the spatial audio. Any two of the 3D coordinate vectors of the user's position need to be perpendicular to each other. Refer to [ByteRTCHumanOrientation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHumanOrientation) for details.

<span id="ByteRTCScreenParam"></span>
# ByteRTCScreenParam

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCScreenParam : NSObject
```


Screen capture setting parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[frameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenParam-framerate) |
|NSInteger |[bitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenParam-bitrate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCScreenParam-framerate"></span>
### frameRate

```objectivec
@property(nonatomic, assign) NSInteger frameRate;
```


Encoded frame rate in fps

<span id="ByteRTCScreenParam-bitrate"></span>
### bitrate

```objectivec
@property(nonatomic, assign) NSInteger bitrate;
```


Encoding bitrate. When the value is less than 0, the SDK adaptively sets the bitrate based on the height and width, in Kbps

<span id="ByteRTCScreenCaptureSourceType"></span>
# ByteRTCScreenCaptureSourceType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCScreenCaptureSourceType
)
```


Type of the screen capture object

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCScreenCaptureSourceTypeUnknown |0 |Type unknown |
|ByteRTCScreenCaptureSourceTypeWindow |1 |Application window |
|ByteRTCScreenCaptureSourceTypeScreen |2 |Desktop |


<span id="ByteRTCForwardStreamState"></span>
# ByteRTCForwardStreamState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCForwardStreamState
)
```


The state of the relaying for each room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCForwardStreamStateIdle |0 |Idle<br><br><br>&nbsp;<br><br>* States of all the rooms turn to idle after you call `stopForwardStreamToRooms`.<br><br>* The states of the rooms that you removed by calling `updateForwardStreamToRooms` turn to idle. |
|ByteRTCForwardStreamStateSuccess |1 |Start relaying.<br><br><br>&nbsp;<br><br>* The states of the rooms turn to this state after the relaying starts successfully by calling `startForwardStreamToRooms`.<br><br>* The states of the rooms added by calling `updateForwardStreamToRooms` turn to this state after the relaying starts successfully. |
|ByteRTCForwardStreamStateFailure |2 |Relay fails. Refer to [ByteRTCForwardStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamError) for more information.<br><br>&nbsp;<br><br>Once the relaying fails, state of the room turns to this state after calling `startForwardStreamToRooms` or `updateForwardStreamToRooms`. |


<span id="ByteRTCMediaPlayerCustomSourceSeekWhence"></span>
# ByteRTCMediaPlayerCustomSourceSeekWhence

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMediaPlayerCustomSourceSeekWhence
)
```


The starting position where audio data seeking begins.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaPlayerCustomSourceSeekWhenceSet |0 |Seeks from the head of the audio data and the position of actual data offset after seeking is offset. |
|ByteRTCMediaPlayerCustomSourceSeekWhenceCur |1 |Seeks from a specific position of the audio data stream, and the actual data offset after seeking is the current position plus offset. |
|ByteRTCMediaPlayerCustomSourceSeekWhenceEnd |2 |Seeks from the end of the audio data, and the actual data offset after seeking is the whole data length plus offset. |
|ByteRTCMediaPlayerCustomSourceSeekWhenceSize |3 |Returns the size of audio data. |


<span id="ByteRTCAudioMixingDualMonoMode"></span>
# ByteRTCAudioMixingDualMonoMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioMixingDualMonoMode
)
```


Mix playback channel type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioMixingDualMonoModeAuto |0 |Consistent with audio files |
|ByteRTCAudioMixingDualMonoModeL |1 |Only the left channel audio in the audio file can be heard |
|ByteRTCAudioMixingDualMonoModeR |2 |Only the right channel audio in the audio file can be heard |
|ByteRTCAudioMixingDualMonoModeMix |3 |Both the left and right channel audio in the file can be heard at the same time |


<span id="ByteRTCRecordingType"></span>
# ByteRTCRecordingType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRecordingType
)
```


Locally recorded media type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRecordingTypeAudioOnly |0 |Audio only |
|ByteRTCRecordingTypeVideoOnly |1 |Video only |
|ByteRTCRecordingTypeVideoAndAudio |2 |Record audio and video simultaneously |


<span id="ByteRTCZoomDirectionType"></span>
# ByteRTCZoomDirectionType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCZoomDirectionType
)
```


Action of the digital zoom control

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCZoomDirectionTypeMoveLeft |0 |Move to the left. |
|ByteRTCZoomDirectionTypeMoveRight |1 |Move to the right. |
|ByteRTCZoomDirectionTypeMoveUp |2 |Move upwards. |
|ByteRTCZoomDirectionTypeMoveDown |3 |Move downwards. |
|ByteRTCZoomDirectionTypeZoomOut |4 |Zoom out. |
|ByteRTCZoomDirectionTypeZoomIn |5 |Zoom in. |
|ByteRTCZoomDirectionTypeReset |6 |Reset digital zoom. |


<span id="ByteRTCNetworkDetectionStopReason"></span>
# ByteRTCNetworkDetectionStopReason

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCNetworkDetectionStopReason
)
```


Reason for stopping pre\-call detection

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCNetworkDetectionStopReasonUser |0 |The user actively stops. |
|ByteRTCNetworkDetectionStopReasonTimeout |1 |Detection takes more than three minutes. |
|ByteRTCNetworkDetectionStopReasonConnectionLost |2 |Probe network connection disconnected. |
|ByteRTCNetworkDetectionStopReasonStreaming |3 |Begin publishing and subscribing to streams and stop probing. |
|ByteRTCNetworkDetectionStopReasonInnerErr |4 |Network probe failure, internal anomaly |


<span id="ByteRTCAudioQuality"></span>
# ByteRTCAudioQuality

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioQuality
)
```


Audio quality

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioQualityLow |0 |low quality |
|ByteRTCAudioQualityMedium |1 |medium quality |
|ByteRTCAudioQualityHigh |2 |high quality |
|ByteRTCAudioQualityUltraHigh |3 |ultra high quality |


<span id="ByteRTCMediaPlayerCustomSourceMode"></span>
# ByteRTCMediaPlayerCustomSourceMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMediaPlayerCustomSourceMode
)
```


Custom audio source mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaPlayerCustomSourceModePush |0 |When you use the local PCM data, use this mode. |
|ByteRTCMediaPlayerCustomSourceModePull |1 |When you use the audio data from local memory, use this mode. |


<span id="ByteRTCRenderMode"></span>
# ByteRTCRenderMode

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCRenderMode
)
```


The render mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRenderModeHidden |1 |(Default) Fill and Crop.<br><br>&nbsp;<br><br>The video frame is scaled with fixed aspect ratio, until it completely fills the canvas. The region of the video exceeding the canvas will be cropped. |
|ByteRTCRenderModeFit |2 |Fit.<br><br>&nbsp;<br><br>The video frame is scaled with fixed aspect ratio, until it fits just within the canvas. Other part of the canvas is filled with the background color. |
|ByteRTCRenderModeFill |3 |Fill the canvas.<br><br>&nbsp;<br><br>The video frame is scaled to fill the canvas. During the process, the aspect ratio may change. |


<span id="ByteRTCSEIStreamEventType"></span>
# ByteRTCSEIStreamEventType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSEIStreamEventType
)
```


State of the black frame video stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSEIStreamEventTypeStreamAdd |0 |A black frame video stream is published from the remote user.<br><br>&nbsp;<br><br>In a voice call, when the remote user calls [sendSEIMessage:andRepeatCount:andCountPerFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-sendseimessage-andrepeatcount-andcountperframe) to send SEI data, SDK will automatically publish a black frame video stream, and trigger this callback. |
|ByteRTCSEIStreamEventTypeStreamRemove |1 |The black frame video stream is removed. The timing this callback will be triggered is as following:<br><br><br>&nbsp;<br><br>* The remote user turns on their camera, switching from a voice call to a video call.<br><br>* No SEI data is sent within 1min after the remote user calls [sendSEIMessage:andRepeatCount:andCountPerFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-sendseimessage-andrepeatcount-andcountperframe).<br><br>* The black frame video stream stops when the remote user calls [setVideoSourceType:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setvideosourcetype) to switch to custom video capture. |


<span id="ByteRTCRecordingConfig"></span>
# ByteRTCRecordingConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRecordingConfig : NSObject
```


Local recording parameter configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[dirPath](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingConfig-dirpath) |
|ByteRTCRecordingFileType |[recordingFileType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingConfig-recordingfiletype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRecordingConfig-dirpath"></span>
### dirPath

```objectivec
@property(strong, nonatomic) NSString* _Nullable dirPath;
```


The absolute folder path to save the recording file. The filename will be generated by RTC. You need to ensure that you have read and write permissions to this path.

<span id="ByteRTCRecordingConfig-recordingfiletype"></span>
### recordingFileType

```objectivec
@property(assign, nonatomic) ByteRTCRecordingFileType recordingFileType;
```


Record the stored file format. See [ByteRTCRecordingFileType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingFileType)

<span id="ByteRTCRemoteVideoSinkConfig"></span>
# ByteRTCRemoteVideoSinkConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteVideoSinkConfig : NSObject
```


Remote video frame callback configurations.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCRemoteVideoSinkPosition |[position](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoSinkConfig-position) |
|ByteRTCVideoSinkPixelFormat |[requiredPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoSinkConfig-requiredpixelformat) |
|ByteRTCVideoApplyRotation |[applyRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoSinkConfig-applyrotation) |
|ByteRTCVideoSinkMirrorType |[mirrorType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoSinkConfig-mirrortype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteVideoSinkConfig-position"></span>
### position

```objectivec
@property(nonatomic, assign) ByteRTCRemoteVideoSinkPosition position;
```


The position of the remote video frame. See [ByteRTCLocalVideoSinkPosition](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoSinkPosition). The default position is after processing.

<span id="ByteRTCRemoteVideoSinkConfig-requiredpixelformat"></span>
### requiredPixelFormat

```objectivec
@property(nonatomic, assign) ByteRTCVideoSinkPixelFormat requiredPixelFormat;
```


The pixel format of the remote video frame. See [ByteRTCVideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSinkPixelFormat). The default value is 0.

<span id="ByteRTCRemoteVideoSinkConfig-applyrotation"></span>
### applyRotation

```objectivec
@property(nonatomic, assign) ByteRTCVideoApplyRotation applyRotation;
```


Whether the video frame needs to be automatically rotated. See [ByteRTCVideoApplyRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoApplyRotation). The default value is no rotation.

<span id="ByteRTCRemoteVideoSinkConfig-mirrortype"></span>
### mirrorType

```objectivec
@property(nonatomic, assign) ByteRTCVideoSinkMirrorType mirrorType;
```


Whether the video frame needs to be mirrored. See [ByteRTCVideoSinkMirrorType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSinkMirrorType). The default value is no mirroring effect.

This setting is independent of [setRemoteVideoMirrorType:withMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setremotevideomirrortype-withmirrortype) (which is applicable for internal rendering).

<span id="ByteRTCVideoOutputOrientationMode"></span>
# ByteRTCVideoOutputOrientationMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoOutputOrientationMode
)
```


Video output direction mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoOutputOrientationModeAdaptative |0 |Self\-adaptation layout |
|ByteRTCVideoOutputOrientationModeFixedLandscape |1 |Landscape layout |
|ByteRTCVideoOutputOrientationModeFixedPortrait |2 |Vertical screen layout |


<span id="ByteRTCSubscribeStateChangeReason"></span>
# ByteRTCSubscribeStateChangeReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSubscribeStateChangeReason
)
```


Reason to change the subscription state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSubscribeStateChangeReasonSubscribe |0 |Requested to subscribe. |
|ByteRTCSubscribeStateChangeReasonUnsubscribe |1 |Requested to unsubscribe. |
|ByteRTCSubscribeStateChangeReasonRemotePublish |2 |The remote user published a stream. |
|ByteRTCSubscribeStateChangeReasonRemoteUnpublish |3 |The remote user removed a stream. |
|ByteRTCSubscribeStateChangeReasonStreamFailed5xx |4 |Failed to subscribe due to the server error. The SDK will automatically retry. |
|ByteRTCSubscribeStateChangeReasonStreamFailed404 |5 |Failed to subscribe since the stream to be subscribed to was not found in the room. The SDK will automatically retry the subscription. If the subscription still fails, we recommend you exit and retry. |
|ByteRTCSubscribeStateChangeReasonOverStreamSubscribeLimit |6 |The number of streams the user has subscribed to has exceeded the limit. |
|ByteRTCSubscribeStateChangeReasonNoSubscribePermission |7 |The user was not permitted to subscribe to the stream. |


<span id="ByteRTCRemoteVideoStateChangeReason"></span>
# ByteRTCRemoteVideoStateChangeReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRemoteVideoStateChangeReason
)
```


Cause of remote video stream state change

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRemoteVideoStateChangeReasonInternal |0 |Internal reasons |
|ByteRTCRemoteVideoStateChangeReasonNetworkCongestion |1 |Network blocking |
|ByteRTCRemoteVideoStateChangeReasonNetworkRecovery |2 |Network back to normal |
|ByteRTCRemoteVideoStateChangeReasonLocalMuted |3 |Local user stops receiving remote video stream or local user disables video module |
|ByteRTCRemoteVideoStateChangeReasonLocalUnmuted |4 |Local user resumes receiving remote video streams or local user enables video modules |
|ByteRTCRemoteVideoStateChangeReasonRemoteMuted |5 |The remote user stops sending the video stream or the remote user disables the video module |
|ByteRTCRemoteVideoStateChangeReasonRemoteUnmuted |6 |Remote user resumes sending video stream or remote user enables video module |
|ByteRTCRemoteVideoStateChangeReasonRemoteOffline |7 |Remote user leaves room |


<span id="ByteRTCVideoStreamType"></span>
# ByteRTCVideoStreamType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoStreamType
)
```


Video Stream Type

Currently C++ SDK only supports ByteRTCVideoStreamTypeHigh type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoStreamTypeHigh |0 |High Resolution Video Streaming |
|ByteRTCVideoStreamTypeLow |1 |Low Resolution Video |


<span id="ByteRTCRemoteVideoSinkPosition"></span>
# ByteRTCRemoteVideoSinkPosition

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRemoteVideoSinkPosition
)
```


The position of the remote video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRemoteVideoSinkPositionAfterPostprocess |1 |(Default) After processing. |


<span id="ByteRTCMixedStreamVideoCodecType"></span>
# ByteRTCMixedStreamVideoCodecType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMixedStreamVideoCodecType
)
```


The video codec.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamVideoCodecTypeH264 |0 |(Default) H.264 format. |
|ByteRTCMixedStreamVideoCodecTypeByteVC1 |1 |ByteVC1 format. |


<span id="ByteRTCFirstFramePlayState"></span>
# ByteRTCFirstFramePlayState

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCFirstFramePlayState
)
```


First frame playback status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCFirstFramePlayStatePlaying |0 |Playing |
|ByteRTCFirstFramePlayStatePlay |1 |Play success |
|ByteRTCFirstFramePlayStateEnd |2 |Play failed |


<span id="ByteRTCAVSyncState"></span>
# ByteRTCAVSyncState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAVSyncState
)
```


A/V synchronization states

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAVSyncStateAVStreamSyncBegin |0 |A/V synchronization begins. |
|ByteRTCAVSyncStateAudioStreamRemove |1 |The publisher stops publishing the video stream during the synchronization, which does not affect the sync relationship. |
|ByteRTCAVSyncStateVideoStreamRemove |2 |The publisher stops publishing the video stream during the synchronization, which does not affect the sync relationship. |


<span id="ByteRTCPauseResumControlMediaType"></span>
# ByteRTCPauseResumControlMediaType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPauseResumControlMediaType
)
```


Type of the stream to be paused/resumed

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCControlMediaTypeAudio |0 |Only control audio, not affect video |
|ByteRtcControlMediaTypeVideo |1 |Only control video, not affect audio |
|ByteRtcControlMediaTypeAudioAndVideo |2 |Simultaneous control of audio and video |


<span id="ByteRTCVideoCaptureConfig"></span>
# ByteRTCVideoCaptureConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoCaptureConfig: NSObject
```


Video acquisition parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCVideoCapturePreference |[preference](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCaptureConfig-preference) |
|CGSize |[videoSize](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCaptureConfig-videosize) |
|NSInteger |[frameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCaptureConfig-framerate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoCaptureConfig-preference"></span>
### preference

```objectivec
@property(nonatomic, assign) ByteRTCVideoCapturePreference preference;
```


Video capture preference. See [ByteRTCVideoCapturePreference](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCapturePreference)

<span id="ByteRTCVideoCaptureConfig-videosize"></span>
### videoSize

```objectivec
@property(nonatomic, assign) CGSize videoSize;
```


Video capture resolution

<span id="ByteRTCVideoCaptureConfig-framerate"></span>
### frameRate

```objectivec
@property(nonatomic, assign) NSInteger frameRate;
```


Video capture frame rate in fps.

<span id="ByteRTCPublishState"></span>
# ByteRTCPublishState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPublishState
)
```


Stream publishing state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPublishStatePublish |0 |Successfully published. |
|ByteRTCPublishStateUnpublish |1 |Failed to publish. |


<span id="ByteRTCUser"></span>
# ByteRTCUser

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCUser : NSObject
```


User information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCUser-userid) |
|NSString\* |[metaData](https://docs.byteplus.com/en/docs/12/14181#ByteRTCUser-metadata) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCUser-userid"></span>
### userId

```objectivec
@property(nonatomic, copy, nullable) NSString *userId;
```


User ID

<span id="ByteRTCUser-metadata"></span>
### metaData

```objectivec
@property(nonatomic, copy, nullable) NSString *metaData;
```


Meta information

<span id="ByteRTCPublishStateChangeReason"></span>
# ByteRTCPublishStateChangeReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPublishStateChangeReason
)
```


Reason to change the publishing state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPublishStateChangeReasonPublish |0 |Requested to publish. |
|ByteRTCPublishStateChangeReasonUnpublish |1 |Requested to remove. |
|ByteRTCPublishStateChangeReasonNoPublishPermission |2 |The token the user used was not permitted to publish. |
|ByteRTCPublishStateChangeReasonOverStreamPublishLimit |3 |The number of streams the user has published has exceeded the limit. |
|ByteRTCPublishStateChangeReasonMultiRoomUnpublishFailed |4 |The stream failed to remove from a room when you are publishing the stream in two or more rooms. |
|ByteRTCPublishStateChangeReasonPublishStreamFailed |5 |Failed to publish due to the server error. |
|ByteRTCPublishStateChangeReasonPublishStreamForbidden |6 |The user who tried to publish a stream is not a host. Call [setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-setuservisibility) to change the user role. |
|ByteRTCPublishStateChangeReasonUserInPublish |7 |The user who tried to publish a stream has already published a stream in a room. |
|ByteRTCPublishStateChangeReasonStreamPublishByOther |8 |Another user publishes a stream with the same streamid, which causes the stream you are publishing to be removed. |
|ByteRTCPublishStateChangeReasonStreamIdInvalid |9 |Stream ID is invalid. |


<span id="ByteRTCPerformanceAlarmMode"></span>
# ByteRTCPerformanceAlarmMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPerformanceAlarmMode
)
```


Mode of performance fallback

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPerformanceAlarmModeNormal |0 |Not enabled Publish performance fallback |
|ByteRTCPerformanceAlarmModeSimulcast |1 |Enable publish performance fallback |


<span id="ByteRTCRemoteStreamSwitchEvent"></span>
# ByteRTCRemoteStreamSwitchEvent

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteStreamSwitchEvent : NSObject
```


Information of stream switching due to a Fallback

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[uid](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamSwitchEvent-uid) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamSwitchEvent-isscreen) |
|NSInteger |[beforeVideoIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamSwitchEvent-beforevideoindex) |
|NSInteger |[afterVideoIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamSwitchEvent-aftervideoindex) |
|BOOL |[beforeVideoEnabled](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamSwitchEvent-beforevideoenabled) |
|BOOL |[afterVideoEnabled](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamSwitchEvent-aftervideoenabled) |
|ByteRTCFallbackOrRecoverReason |[reason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamSwitchEvent-reason) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteStreamSwitchEvent-uid"></span>
### uid

```objectivec
@property(nonatomic, copy) NSString * _Nonnull uid;
```


User ID of the publisher of the subscribed media stream

<span id="ByteRTCRemoteStreamSwitchEvent-isscreen"></span>
### isScreen

```objectivec
@property(nonatomic, assign) BOOL isScreen;
```


Reserved field. Ignore the value returned in this field.

<span id="ByteRTCRemoteStreamSwitchEvent-beforevideoindex"></span>
### beforeVideoIndex

```objectivec
@property(nonatomic, assign) NSInteger beforeVideoIndex;
```


The quality index of the subscribed stream before the stream switching

<span id="ByteRTCRemoteStreamSwitchEvent-aftervideoindex"></span>
### afterVideoIndex

```objectivec
@property(nonatomic, assign) NSInteger afterVideoIndex;
```


The quality index of the subscribed stream after the stream switching

<span id="ByteRTCRemoteStreamSwitchEvent-beforevideoenabled"></span>
### beforeVideoEnabled

```objectivec
@property(nonatomic, assign) BOOL beforeVideoEnabled;
```


Whether a video stream is enabled before stream switching

<span id="ByteRTCRemoteStreamSwitchEvent-aftervideoenabled"></span>
### afterVideoEnabled

```objectivec
@property(nonatomic, assign) BOOL afterVideoEnabled;
```


Whether a video stream after the stream switching

<span id="ByteRTCRemoteStreamSwitchEvent-reason"></span>
#### reason

```objectivec
@property(nonatomic, assign) ByteRTCFallbackOrRecoverReason reason;
```


Refer to [ByteRTCFallbackOrRecoverReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFallbackOrRecoverReason) for the reason of the Fallback or reverting from the Fallback of the subscribed stream.

<span id="ByteRTCMixedStreamPushTargetType"></span>
# ByteRTCMixedStreamPushTargetType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMixedStreamPushTargetType
)
```


Task type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamPushTargetTypeToCDN |0 |Push to CDN. |
|ByteRTCMixedStreamPushTargetTypeToWTN |1 |WTN stream |


<span id="ByteRTCLocalAudioStats"></span>
# ByteRTCLocalAudioStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCLocalAudioStats : NSObject
```


Local audio stream statistics, reference period 2s.

After the local user publishes the audio stream successfully, the SDK will periodically notify the local user through `onLocalStreamStats`

The sending status of the published audio stream during this reference period. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[audioLossRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-audiolossrate) |
|float |[sentKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-sentkbitrate) |
|NSInteger |[recordSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-recordsamplerate) |
|NSInteger |[statsInterval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-statsinterval) |
|NSInteger |[rtt](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-rtt) |
|NSInteger |[numChannels](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-numchannels) |
|NSInteger |[sentSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-sentsamplerate) |
|NSInteger |[jitter](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-jitter) |
|NSInteger |[audioDeviceLoopDelay](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-audiodeviceloopdelay) |
|double |[encodeFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats-encodeframerate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLocalAudioStats-audiolossrate"></span>
### audioLossRate

```objectivec
@property(assign, nonatomic) float audioLossRate;
```


Audio packet loss rate. The audio uplink packet loss rate in this reference period is in the range of [0,1].

<span id="ByteRTCLocalAudioStats-sentkbitrate"></span>
### sentKBitrate

```objectivec
@property(assign, nonatomic) float sentKBitrate;
```


The bit rate of transmission. The audio transmission rate in the reference period is kbps.

<span id="ByteRTCLocalAudioStats-recordsamplerate"></span>
### recordSampleRate

```objectivec
@property(assign, nonatomic) NSInteger recordSampleRate;
```


Acquisition sampling rate. Audio sampling rate information collected in the reference period, in units of Hz.

<span id="ByteRTCLocalAudioStats-statsinterval"></span>
### statsInterval

```objectivec
@property(assign, nonatomic) NSInteger statsInterval;
```


Statistical interval. The interval of this reference period is in ms.

This field is used to set the reference period for the callback. The default setting is 2s.

<span id="ByteRTCLocalAudioStats-rtt"></span>
### rtt

```objectivec
@property(assign, nonatomic) NSInteger rtt;
```


Round\-trip time. The unit is ms.

<span id="ByteRTCLocalAudioStats-numchannels"></span>
### numChannels

```objectivec
@property(assign, nonatomic) NSInteger numChannels;
```


Number of audio channels.

<span id="ByteRTCLocalAudioStats-sentsamplerate"></span>
### sentSampleRate

```objectivec
@property(assign, nonatomic) NSInteger sentSampleRate;
```


Audio transmission sampling rate. Audio transmission sampling rate information in the reference period, in Hz.

<span id="ByteRTCLocalAudioStats-jitter"></span>
### jitter

```objectivec
@property(assign, nonatomic) NSInteger jitter;
```


Audio uplink network jitter in ms.

<span id="ByteRTCLocalAudioStats-audiodeviceloopdelay"></span>
### audioDeviceLoopDelay

```objectivec
@property(assign, nonatomic) NSInteger audioDeviceLoopDelay;
```


Audio device record and playout delay in ms.

<span id="ByteRTCLocalAudioStats-encodeframerate"></span>
### encodeFrameRate

```objectivec
@property(assign, nonatomic) double encodeFrameRate;
```


Audio encode frame rate.

<span id="ByteRTCAudioAlignmentMode"></span>
# ByteRTCAudioAlignmentMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioAlignmentMode
)
```


The alignment mode of remote audio streams

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioAlignmentModeOff |0 |Disabled |
|ByteRTCAudioAlignmentModeAudioMixing |1 |All subscribed audio streams are aligned based on the process of the background music. |


<span id="ByteRTCReceiveRange"></span>
# ByteRTCReceiveRange

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCReceiveRange : NSObject
```


The range where local user can hear audio with attenuation effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[min](https://docs.byteplus.com/en/docs/12/14181#ByteRTCReceiveRange-min) |
|int |[max](https://docs.byteplus.com/en/docs/12/14181#ByteRTCReceiveRange-max) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCReceiveRange-min"></span>
### min

```objectivec
@property(nonatomic, assign) int min;
```


The minimum distance at which the local user can hear the attenuated audio from remote users.

The value must be ≥ 0, but ≤ max.

No attenuation effect for audio from distances less than this value you set.

<span id="ByteRTCReceiveRange-max"></span>
### max

```objectivec
@property(nonatomic, assign) int max;
```


The maximum distance at which the local user can hear audio from remote users.

The value must be ≥ min, and \> 0.

Audio from distances larger than the value you set cannot be heard.

<span id="ByteRTCRecordingState"></span>
# ByteRTCRecordingState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRecordingState
)
```


Status of local recording

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRecordingStateError |0 |Recording exception |
|ByteRTCRecordingStateProcessing |1 |Recording in progress |
|ByteRTCRecordingStateSuccess |2 |If the recording file is saved successfully. Normal call to stopFileRecording triggers this status code. If the encoding resolution changes during the recording, the SDK will automatically end the current file save and trigger this status code, followed by a new round of recording, until stopFileRecording is called. |


<span id="ByteRTCFaceDetectionResult"></span>
# ByteRTCFaceDetectionResult

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCFaceDetectionResult : NSObject
```


Face Detection Result

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[detectResult](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFaceDetectionResult-detectresult) |
|int |[imageWidth](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFaceDetectionResult-imagewidth) |
|int |[imageHeight](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFaceDetectionResult-imageheight) |
|NSArray<ByteRTCRectangle\*\>\* |[faces](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFaceDetectionResult-faces) |
|CMTime |[frameTimestamp](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFaceDetectionResult-frametimestamp) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCFaceDetectionResult-detectresult"></span>
### detectResult

```objectivec
@property(assign, nonatomic) int detectResult;
```


Face Detection Result


* 0: Success

* !0: Failure. See [Error Code Table](https://docs.byteplus.com/en/effects/docs/error-code-table).

    &nbsp;


<span id="imagewidth"></span>
### imageWidth

```objectivec
@property(assign, nonatomic) int imageWidth;
```


Width of the original image (px)

<span id="ByteRTCFaceDetectionResult-imageheight"></span>
### imageHeight

```objectivec
@property(assign, nonatomic) int imageHeight;
```


Height of the original image (px)

<span id="ByteRTCFaceDetectionResult-faces"></span>
### faces

```objectivec
@property(nonatomic, copy) NSArray<ByteRTCRectangle *> * _Nullable faces;
```


The face recognition rectangles. The length of the array is the same as the number of detected faces. See [ByteRTCRectangle](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRectangle).

<span id="ByteRTCFaceDetectionResult-frametimestamp"></span>
### frameTimestamp

```objectivec
@property(assign, nonatomic) CMTime frameTimestamp;
```


The time stamp of the video frame using face detection.

<span id="ByteRTCVideoByteWatermark"></span>
# ByteRTCVideoByteWatermark

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoByteWatermark: NSObject
```


Watermark's scaled coordinates and size, relative to the video stream.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoByteWatermark-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoByteWatermark-y) |
|float |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoByteWatermark-width) |
|float |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoByteWatermark-height) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoByteWatermark-x"></span>
### x

```objectivec
@property(assign, nonatomic) float x;
```


The watermark's horizontal offset from the upper left corner of the video stream to the video stream's width in the range of [0,1).

<span id="ByteRTCVideoByteWatermark-y"></span>
### y

```objectivec
@property(assign, nonatomic) float y;
```


The watermark's vertical offset from the upper left corner of the video stream to the video stream's height in the range of [0,1).

<span id="ByteRTCVideoByteWatermark-width"></span>
### width

```objectivec
@property(assign, nonatomic) float width;
```


The watermark's width to the video stream's width in the range of [0,1).

<span id="ByteRTCVideoByteWatermark-height"></span>
### height

```objectivec
@property(assign, nonatomic) float height;
```


The watermark height to the video stream's height in the range of [0,1).

<span id="ByteRTCMixedStreamControlConfig"></span>
# ByteRTCMixedStreamControlConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamControlConfig : NSObject
```


Configurations to be set while mixing streams on the server side.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enableVolumeIndication](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-enablevolumeindication) |
|CGFloat |[volumeIndicationInterval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-volumeindicationinterval) |
|NSInteger |[talkVolume](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-talkvolume) |
|BOOL |[isAddVolumeValue](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-isaddvolumevalue) |
|ByteRTCMixedStreamSEIContentMode |[seiContentMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-seicontentmode) |
|NSInteger |[seiPayloadType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-seipayloadtype) |
|NSString\* |[seiPayloadUUID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-seipayloaduuid) |
|ByteRTCMixedStreamMediaType |[mediaType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-mediatype) |
|ByteRTCMixedStreamPushMode |[pushStreamMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamControlConfig-pushstreammode) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamControlConfig-enablevolumeindication"></span>
### enableVolumeIndication

```objectivec
@property(assign, nonatomic) BOOL enableVolumeIndication;
```


> Available since 3.56


Sets whether to enable the function of separately sending sound indication SEI:


* True: Enable.

* False: Disable. Default setting.

   After setting this parameter to "true", you can choose whether to send sound indication SEI only through `ByteRTCMixedStreamControlConfig.seiContentMode`.

    &nbsp;


<span id="volumeindicationinterval"></span>
### volumeIndicationInterval

```objectivec
@property(assign, nonatomic) CGFloat volumeIndicationInterval;
```


> Available since 3.56


Sound indication interval in s. The range is [0.3,+∞). The default value is 2.

If a decimal with two or more decimal places is passed in, it will be rounded to the value of the first decimal place. For example, if you pass in 0.36, it will be automatically adjusted to 0.4.

<span id="ByteRTCMixedStreamControlConfig-talkvolume"></span>
### talkVolume

```objectivec
@property(assign, nonatomic) NSInteger talkVolume;
```


> Available since 3.56


Effective volume within the range of [0, 255]. The default value is 0.

If the value is set beyond the range, it will be automatically adjusted to the default value 0.

<span id="ByteRTCMixedStreamControlConfig-isaddvolumevalue"></span>
### isAddVolumeValue

```objectivec
@property(assign, nonatomic) BOOL isAddVolumeValue;
```


> Available since 3.56


Sets whether volume value is contained in the sound indication SEI:


* True: Yes.

* False: No. Default setting.

    &nbsp;


<span id="seicontentmode"></span>
### seiContentMode

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamSEIContentMode seiContentMode;
```


> Available since 3.56


Sets SEI content. See [ByteRTCMixedStreamSEIContentMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamSEIContentMode).

<span id="ByteRTCMixedStreamControlConfig-seipayloadtype"></span>
### seiPayloadType

```objectivec
@property(assign, nonatomic) NSInteger seiPayloadType;
```


> Available since 3.56


SEI payload type.

The default value is `100`, and the value supported is `5` and `100`.

During the process of pushing streams to CDN, you cannot change the parameter.

<span id="ByteRTCMixedStreamControlConfig-seipayloaduuid"></span>
### seiPayloadUUID

```objectivec
@property(copy, nonatomic) NSString *seiPayloadUUID;
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

<span id="ByteRTCMixedStreamControlConfig-mediatype"></span>
### mediaType

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamMediaType mediaType;
```


> Available since 3.57


Sets the type of media stream pushed to CDN after being mixed. [ByteRTCMixedStreamMediaType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamMediaType).

The default value is 0, which means pushing both audio and video.

<span id="ByteRTCMixedStreamControlConfig-pushstreammode"></span>
### pushStreamMode

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamPushMode pushStreamMode;
```


> Available since 3.57


Sets whether to initiate a stream mixing task in the absence of any users publishing streams. See [ByteRTCMixedStreamPushMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamPushMode).

Once the stream mixing task is initiated, this parameter can not be updated any more.

<span id="ByteRTCEchoTestConfig"></span>
# ByteRTCEchoTestConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCEchoTestConfig : NSObject
```


Video/audio call test configurations

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCView\* |[view](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEchoTestConfig-view) |
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEchoTestConfig-roomid) |
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEchoTestConfig-userid) |
|NSString\* |[token](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEchoTestConfig-token) |
|BOOL |[enableAudio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEchoTestConfig-enableaudio) |
|BOOL |[enableVideo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEchoTestConfig-enablevideo) |
|NSInteger |[audioReportInterval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEchoTestConfig-audioreportinterval) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCEchoTestConfig-view"></span>
### view

```objectivec
@property(strong, nonatomic) ByteRTCView* _Nullable view;
```


View for rendering received video

<span id="ByteRTCEchoTestConfig-roomid"></span>
### roomId

```objectivec
@property(copy, nonatomic) NSString *_Nonnull roomId;
```


ID of the room that the tested user will join.

<span id="ByteRTCEchoTestConfig-userid"></span>
### userId

```objectivec
@property(copy, nonatomic) NSString *_Nonnull userId;
```


User ID for testing

<span id="ByteRTCEchoTestConfig-token"></span>
### token

```objectivec
@property(copy, nonatomic) NSString *_Nonnull token;
```


Token used for authenticating users when they enter the room.

<span id="ByteRTCEchoTestConfig-enableaudio"></span>
### enableAudio

```objectivec
@property(assign, nonatomic) BOOL enableAudio;
```


Whether to test audio. The device to be tested is the default audio device.


* true: Yes

   * If you use internal capture, the device microphone will automatically turn on and `onLocalAudioPropertiesReport` will be triggered when the value of audioReportInterval is set to greater than 0, from which you can judge the working status of the microphone.

   * If you choose custom capture, you also need to call [pushExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-pushexternalaudioframe) to push the captured audio to the SDK.

* false: No

    &nbsp;


<span id="enablevideo"></span>
### enableVideo

```objectivec
@property(assign, nonatomic) BOOL enableVideo;
```


Whether to test video. If you are using a desktop PC, the device to be tested is by default the first video device in the list.


* true: Yes

   * If you use internal capture, the device camera will automatically turn on.

   * If you choose custom capture, you also need to call [pushExternalVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-pushexternalvideoframe) to push the captured video to the SDK.

* false: No

   The video is published with fixed parameters: resolution 640px × 360px, frame rate 15fps.

    &nbsp;


<span id="audioreportinterval"></span>
### audioReportInterval

```objectivec
@property(assign, nonatomic) NSInteger audioReportInterval;
```


Volume prompt interval in ms, the default value is 100.


* `<= 0`: Turn off prompt

* `(0,100]` Invalid interval value, and will be automatically reset to 100ms.

* `> 100`: the actual value of interval

    &nbsp;


<span id="bytertcsnapshoterrorcode"></span>
# ByteRTCSnapshotErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSnapshotErrorCode
)
```


Snapshot error codes

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSnapshotErrorCodeOk |0 |Success. |
|ByteRTCSnapshotErrorCodeCreateFail |\-1 |Failure. Fails to generate the image data or encode RGBA. |
|ByteRTCSnapshotErrorCodeStreamInvalid |\-2 |Failure. The stream is invalid. |
|ByteRTCSnapshotErrorCodeTimeout |\-3 |Failure. Snapshot timeout, with a default timeout of 1 second. |
|ByteRTCSnapshotErrorCodeFileSaveError |\-4 |Failure. Fails to save the image. |


<span id="ByteRTCFrameRateRatio"></span>
# ByteRTCFrameRateRatio

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCFrameRateRatio
)
```


Ratio to the original video frame rate of the publisher

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCFrameRateRatioOrigin |0 |100% |
|ByteRTCFrameRateRatioHalf |1 |50% |
|ByteRTCFrameRateRatioQuater |2 |25% |


<span id="ByteRTCMixedStreamRenderMode"></span>
# ByteRTCMixedStreamRenderMode

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMixedStreamRenderMode
)
```


The render mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamRenderModeHidden |1 |(Default) Fill and Crop.<br><br>&nbsp;<br><br>The video frame is scaled with fixed aspect ratio, until it completely fills the canvas. The region of the video exceeding the canvas will be cropped. |
|ByteRTCMixedStreamRenderModeFit |2 |Fit.<br><br>&nbsp;<br><br>The video frame is scaled with fixed aspect ratio, until it fits just within the canvas. Other part of the canvas is filled with the background color. |
|ByteRTCMixedStreamRenderModeAdaptive |3 |Fill the canvas.<br><br>&nbsp;<br><br>The video frame is scaled to fill the canvas. During the process, the aspect ratio may change. |


<span id="ByteRTCMirrorType"></span>
# ByteRTCMirrorType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMirrorType
)
```


Mirror type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMirrorTypeNone |0 |The preview and the published video stream are not mirrored. |
|ByteRTCMirrorTypeRender |1 |The preview is mirrored. The published video stream is not mirrored. |
|ByteRTCMirrorTypeEncoder |2 |The preview is not mirrored; only the published video stream is mirrored. |
|ByteRTCMirrorTypeRenderAndEncoder |3 |The preview and the published video stream are mirrored. |


<span id="ByteRTCAVSyncEvent"></span>
# ByteRTCAVSyncEvent

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAVSyncEvent
)
```


AVSync events

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAVSyncEventInvalidUidRepeated |0 |A/V synchronization failed.<br><br>&nbsp;<br><br>Current source audio ID has been set by other video publishers in the same room.<br><br>&nbsp;<br><br>One single audio source cannot be synchronized with multiple video sources at the same time. |


<span id="ByteRTCForwardStreamError"></span>
# ByteRTCForwardStreamError

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCForwardStreamError
)
```


Error codes during the relaying

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCForwardStreamErrorOK |0 |Normal |
|ByteRTCForwardStreamErrorInvalidArgument |1201 |Invalid argument |
|ByteRTCForwardStreamErrorInvalidToken |1202 |Invalid token |
|ByteRTCForwardStreamErrorResponse |1203 |Error returning from server |
|ByteRTCForwardStreamErrorRemoteKicked |1204 |Relaying aborts because a user with the same user ID as that of the publisher joins. |
|ByteRTCForwardStreamErrorNotSupport |1205 |Server denies. |


<span id="ByteRTCStreamInfo"></span>
# ByteRTCStreamInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCStreamInfo : NSObject
```


Stream information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[streamId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamInfo-streamid) |
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamInfo-userid) |
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamInfo-roomid) |
|NSInteger |[streamIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamInfo-streamindex) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamInfo-isscreen) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCStreamInfo-streamid"></span>
### streamId

```objectivec
@property(nonatomic) NSString * _Nonnull streamId;
```


Stream ID.

<span id="ByteRTCStreamInfo-userid"></span>
### userId

```objectivec
@property(nonatomic) NSString * _Nonnull userId;
```


User ID.

<span id="ByteRTCStreamInfo-roomid"></span>
### roomId

```objectivec
@property(nonatomic) NSString * _Nonnull roomId;
```


Room ID.

<span id="ByteRTCStreamInfo-streamindex"></span>
### streamIndex

```objectivec
@property(nonatomic, assign) NSInteger streamIndex;
```


Stream index.

<span id="ByteRTCStreamInfo-isscreen"></span>
### isScreen

```objectivec
@property(assign, nonatomic) BOOL isScreen;
```


Reserved field. Ignore the value returned in this field.

<span id="ByteRTCReturnStatus"></span>
# ByteRTCReturnStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCReturnStatus
)
```


API call result.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCReturnStatusSuccess |0 |Success. |
|ByteRTCReturnStatusFailure |\-1 |Failure. |
|ByteRTCReturnStatusParameterErr |\-2 |Invalid parameter. |
|ByteRTCReturnStatusWrongState |\-3 |API status error. |
|ByteRTCReturnStatusHasInRoom |\-4 |Failure. The user is already in the room. |
|ByteRTCReturnStatusHasInLogin |\-5 |Failure. The user has already logged in. |
|ByteRTCReturnStatusHasInEchoTest |\-6 |Failure. The user is already in a pre\-call test. |
|ByteRTCReturnStatusNeitherVideoNorAudio |\-7 |Failure. Neither video nor audio is captured. |
|ByteRTCReturnStatusRoomIdInUse |\-8 |Failure. The roomId is already in use. |
|ByteRTCReturnStatusScreenNotSupport |\-9 |Failure. Screen stream is not supported. |
|ByteRTCReturnStatusNotSupport |\-10 |Failure. Not supported. |
|ByteRTCReturnStatusResourceOverflow |\-11 |Failure. Resource overflow. |
|ByteRTCReturnStatusAudioNoFrame |\-101 |Failure. No audio frame. |
|ByteRTCReturnStatusAudioNotImplemented |\-102 |Failure. Not implemented. |
|ByteRTCReturnStatusAudioNoPermission |\-103 |Failure. The audio capture device does not have microphone use permission, and the initialization of the device failed. |
|ByteRTCReturnStatusAudioDeviceNotExists |\-104 |Failure. The device does not exist. This value is returned if there is currently no device or if the device has been removed. |
|ByteRTCReturnStatusAudioDeviceFormatNotSupport |\-105 |Failure. The device audio format is not supported. |
|ByteRTCReturnStatusAudioDeviceNoDevice |\-106 |Failure. No device in system. |
|ByteRTCReturnStatusAudioDeviceCannotUse |\-107 |Failure. The current device is not available and needs to be replaced. |
|ByteRTCReturnStatusAudioDeviceInitFailed |\-108 |Device initialization failed due to a system error. |
|ByteRTCReturnStatusAudioDeviceStartFailed |\-109 |Device start\-up failed due to a system error. |
|ByteRTCReturnStatusAudioDeviceProcessNotExist |\-110 |Sharing process audio failed because the process does not exist. |
|ByteRTCReturnStatusNativeInValid |\-201 |Failure. The native layer is not initialized and the engine is invalid. |


<span id="ByteRTCAudioMixingType"></span>
# ByteRTCAudioMixingType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioMixingType
)
```


Mixing type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioMixingTypePlayout |0 |Played at the local device only |
|ByteRTCAudioMixingTypePublish |1 |Sent to the remote devices only |
|ByteRTCAudioMixingTypePlayoutAndPublish |2 |Played at the local device and sent to the remote devices. |


<span id="ByteRTCVideoEnhancementMode"></span>
# ByteRTCVideoEnhancementMode

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCVideoEnhancementMode
)
```


Low light adjusted type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoEnhancementModeDisabled |0 |Turn off low light adaptation |
|ByteRTCVideoEnhancementModeAuto |1 |Turn on low light adaptation auto |


<span id="ByteRTCSubscribeMediaType"></span>
# ByteRTCSubscribeMediaType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSubscribeMediaType
)
```


Type of the media stream subscribed to

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSubscribeMediaTypeNone |0 |Neither audio nor video |
|ByteRTCSubscribeMediaTypeAudioOnly |1 |Audio only |
|ByteRTCSubscribeMediaTypeVideoOnly |2 |Video only |
|ByteRTCSubscribeMediaTypeAudioAndVideo |3 |Both audio and video |


<span id="ByteRTCPushSingleStreamParam"></span>
# ByteRTCPushSingleStreamParam

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCPushSingleStreamParam : NSObject
```


Configurations for pushing a single media stream to CDN.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[url](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPushSingleStreamParam-url) |
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPushSingleStreamParam-roomid) |
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPushSingleStreamParam-userid) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPushSingleStreamParam-isscreen) |
|NSArray<DestInfo\*\>\* |[destInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPushSingleStreamParam-destinfo) |
|ByteRTCSingleStreamPushType |[pushType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPushSingleStreamParam-pushtype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCPushSingleStreamParam-url"></span>
### url

```objectivec
@property(copy, nonatomic) NSString * _Nullable url;
```


The URL for live transcoding. Only supports live transcoding via RTMP. The URL should match the regular expression `/^rtmps?:\\/\\//`.

<span id="ByteRTCPushSingleStreamParam-roomid"></span>
### roomId

```objectivec
@property(copy, nonatomic) NSString * _Nonnull roomId;
```


The room ID of the media stream

<span id="ByteRTCPushSingleStreamParam-userid"></span>
### userId

```objectivec
@property(copy, nonatomic) NSString * _Nullable userId;
```


The user ID of the media stream

<span id="ByteRTCPushSingleStreamParam-isscreen"></span>
### isScreen

```objectivec
@property(nonatomic, assign) BOOL isScreen;
```


Reserved field. Do not set this field in the single\-stream SDK.

<span id="ByteRTCPushSingleStreamParam-destinfo"></span>
### destInfo

```objectivec
@property(nonatomic, strong) NSArray<DestInfo *> * _Nullable destInfo;
```


Array of destination room info for cross\-room media stream forwarding, nil by default.

When you need to forward media streams from current room to other rooms, you can specify multiple destination room info in this array.

<span id="ByteRTCPushSingleStreamParam-pushtype"></span>
### pushType

```objectivec
@property(assign, nonatomic) ByteRTCSingleStreamPushType pushType;
```


Single stream push type, specifying whether to push the media stream to CDN or RTC room. Default value is push to CDN.

<span id="ByteRTCMediaDeviceWarning"></span>
# ByteRTCMediaDeviceWarning

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMediaDeviceWarning
)
```


Media device warning

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaDeviceWarningOK |0 |No warning |
|ByteRTCMediaDeviceWarningOperationDenied |1 |Illegal device operation. Calls the API for internal device when using the external device. |
|ByteRTCMediaDeviceWarningCaptureSilence |2 |The media device is capturing silent frames. |
|ByteRTCMediaDeviceWarningDetectLeakEcho |11 |Echoes between mics and speakers are detected during a call.<br><br>&nbsp;<br><br>`rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:` notifies you with this enum of echo issue. During a call, SDK will detect echo issue only when [ByteRTCRoomProfile](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomProfile) is set to `ByteRTCRoomProfileMeeting` or `ByteRTCRoomProfileMeetingRoom` and AEC is disabled. |
|ByteRTCMediaDeviceWarningCaptureDetectHowling |16 |Howling detected.<br><br>&nbsp;<br><br>You will receive this callback in the following scenarios: 1) Howling is detected under the room profiles that do not support howling suppression; 2) Detect howling that is not suppressed under the room profiles that support howling suppression.<br><br>&nbsp;<br><br>You can only enable howling suppression by calling calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) to set your room profile as ByteRTCRoomProfileCommunication, ByteRTCRoomProfileMeeting, and ByteRTCRoomProfileMeetingRoom.<br><br>&nbsp;<br><br>We recommend that you remind your users to adjust the physical distance between two devices or disable all unused devices except the connecting one. |


<span id="ByteRTCExpressionDetectConfig"></span>
# ByteRTCExpressionDetectConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCExpressionDetectConfig : NSObject
```


Expression detection configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enableAgeDetect](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectConfig-enableagedetect) |
|BOOL |[enableGenderDetect](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectConfig-enablegenderdetect) |
|BOOL |[enableEmotionDetect](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectConfig-enableemotiondetect) |
|BOOL |[enableAttractivenessDetect](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectConfig-enableattractivenessdetect) |
|BOOL |[enableHappinessDetect](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectConfig-enablehappinessdetect) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCExpressionDetectConfig-enableagedetect"></span>
### enableAgeDetect

```objectivec
@property (assign, nonatomic) BOOL enableAgeDetect;
```


Whether to enable age detection.

<span id="ByteRTCExpressionDetectConfig-enablegenderdetect"></span>
### enableGenderDetect

```objectivec
@property (assign, nonatomic) BOOL enableGenderDetect;
```


Whether to enable gender detection.

<span id="ByteRTCExpressionDetectConfig-enableemotiondetect"></span>
### enableEmotionDetect

```objectivec
@property (assign, nonatomic) BOOL enableEmotionDetect;
```


Whether to enable emotion detection.

<span id="ByteRTCExpressionDetectConfig-enableattractivenessdetect"></span>
### enableAttractivenessDetect

```objectivec
@property (assign, nonatomic) BOOL enableAttractivenessDetect;
```


Whether to enable attractiveness detection.

<span id="ByteRTCExpressionDetectConfig-enablehappinessdetect"></span>
### enableHappinessDetect

```objectivec
@property (assign, nonatomic) BOOL enableHappinessDetect;
```


Whether to enable happiness detection.

<span id="ByteRTCAudioReportMode"></span>
# ByteRTCAudioReportMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioReportMode
)
```


The volume callback modes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioReportModeNormal |0 |Always\-on(Default). |
|ByteRTCAudioReportModeDisconnect |1 |After visibly joining a room and unpublishing your streams, disable the volume callback. |
|ByteRTCAudioReportModeReset |2 |After visibly joining a room and unpublishing your streams, enable the volume callback. The volume is reset to 0. |


<span id="ByteRTCSourceWantedData"></span>
# ByteRTCSourceWantedData

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCSourceWantedData : NSObject
```


Performance fallback related data

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceWantedData-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceWantedData-height) |
|NSInteger |[frameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceWantedData-framerate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCSourceWantedData-width"></span>
### width

```objectivec
@property(nonatomic, assign) NSInteger width;
```


Recommended video input width

<span id="ByteRTCSourceWantedData-height"></span>
### height

```objectivec
@property(nonatomic, assign) NSInteger height;
```


Recommended video input height

<span id="ByteRTCSourceWantedData-framerate"></span>
### frameRate

```objectivec
@property(nonatomic, assign) NSInteger frameRate;
```


Recommended video input frame rate

<span id="ByteRTCLogConfig"></span>
# ByteRTCLogConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCLogConfig : NSObject
```


Local log parameters.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[logPath](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLogConfig-logpath) |
|ByteRTCLocalLogLevel |[logLevel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLogConfig-loglevel) |
|int |[logFileSize](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLogConfig-logfilesize) |
|NSString\* |[logFilenamePrefix](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLogConfig-logfilenameprefix) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLogConfig-logpath"></span>
### logPath

```objectivec
@property(copy, nonatomic) NSString *_Nonnull logPath;
```


(Required) Local log directory.

<span id="ByteRTCLogConfig-loglevel"></span>
### logLevel

```objectivec
@property(assign, nonatomic) ByteRTCLocalLogLevel logLevel;
```


(Optional) The logging level. See [ByteRTCLocalLogLevel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalLogLevel). The default is warning level.

<span id="ByteRTCLogConfig-logfilesize"></span>
### logFileSize

```objectivec
@property(assign, nonatomic) int logFileSize;
```


(Optional) The limits for total log file size in MB. The range is 1 to 100 MB, and the default value is 10 MB.

If `logFileSize` < 1, it will be set to 1 MB. If `logFileSize` \> 100, it will be set to 100 MB.

The maximum size for a single log file is 2 MB.

If 1 ≤ `logFileSize` ≤ 2, one log file will be generated. If `logFileSize` \> 2, the first `⌊logFileSize/2⌋` files will be filled with 2 MB each, and the `⌊logFileSize/2⌋+1` file will be filled with `logFileSize mod 2`.

If the size exceeds the remaining space, the oldest file will be deleted.

<span id="ByteRTCLogConfig-logfilenameprefix"></span>
### logFilenamePrefix

```objectivec
@property(copy, nonatomic) NSString *_Nonnull logFilenamePrefix;
```


(Optional) Local log file name prefix. It should follow the regular expression pattern of `[a-zA-Z0-9_\@-.]{1,128}`.

The final file name will be the prefix followed by "_" and the file creation time, and "_rtclog.log" at the end. For example, `logPrefix_2023-05-25_172324_rtclog.log`.

<span id="ByteRTCSubscribeVideoConfig"></span>
# ByteRTCSubscribeVideoConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCSubscribeVideoConfig : NSObject
```


Video subscription configuration information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[videoIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeVideoConfig-videoindex) |
|NSInteger |[priority](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSubscribeVideoConfig-priority) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCSubscribeVideoConfig-videoindex"></span>
### videoIndex

```objectivec
@property(assign, nonatomic) NSInteger videoIndex;
```


Subscribed video stream resolution index.

Quality level of the video stream subscribed to.

In Simulcast mode, use a number to specify the expected quality of the video stream to be subscribed to. In Simulcast mode, a video has multiple encoded qualities ranging from 0 to 3. Call [setLocalSimulcastMode:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setlocalsimulcastmode) to enable Simulcast mode on the publisher's clients.

Ranging from \-1 to 3

0 (Default): The best quality

\-1: Use the previous settings.

<span id="ByteRTCSubscribeVideoConfig-priority"></span>
### priority

```objectivec
@property(assign, nonatomic) NSInteger priority;
```


Remote user priority. See [ByteRTCRemoteUserPriority](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteUserPriority), the default value is 0.

<span id="ByteRTCNetworkTimeInfo"></span>
# ByteRTCNetworkTimeInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCNetworkTimeInfo: NSObject
```


network time info

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int64_t |[timestamp](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkTimeInfo-timestamp) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCNetworkTimeInfo-timestamp"></span>
### timestamp

```objectivec
@property(assign, nonatomic) int64_t timestamp;
```


Network time. Unit: ms

<span id="ByteRTCRemoteAudioPropertiesInfo"></span>
# ByteRTCRemoteAudioPropertiesInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteAudioPropertiesInfo : NSObject
```


Remote audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[streamId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioPropertiesInfo-streamid) |
|ByteRTCStreamInfo\* |[streamInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioPropertiesInfo-streaminfo) |
|ByteRTCAudioPropertiesInfo\* |[audioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioPropertiesInfo-audiopropertiesinfo) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteAudioPropertiesInfo-streamid"></span>
### streamId

```objectivec
@property(nonatomic) NSString *_Nonnull streamId;
```


The unique identifier of the remote stream.

<span id="ByteRTCRemoteAudioPropertiesInfo-streaminfo"></span>
### streamInfo

```objectivec
@property(strong, nonatomic) ByteRTCStreamInfo *_Nonnull streamInfo;
```


See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStreamInfo)

<span id="ByteRTCRemoteAudioPropertiesInfo-audiopropertiesinfo"></span>
### audioPropertiesInfo

```objectivec
@property(strong, nonatomic) ByteRTCAudioPropertiesInfo *_Nonnull audioPropertiesInfo;
```


See [ByteRTCAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesInfo)

<span id="ByteRTCTranscodingAudioCodec"></span>
# ByteRTCTranscodingAudioCodec

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCTranscodingAudioCodec
)
```


> Deprecated since 3.52, use [ByteRTCMixedStreamAudioCodecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioCodecType) instead.


The audio codec.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCTranscodingAudioCodecAAC |0 |AAC format. |


<span id="ByteRTCVirtualBackgroundSourceType"></span>
# ByteRTCVirtualBackgroundSourceType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVirtualBackgroundSourceType
)
```


Virtual background type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVirtualBackgroundSourceTypeColor |0 |Replace the original background with a solid color. |
|ByteRTCVirtualBackgroundSourceTypeImage |1 |Replace the original background with the specified image. |


<span id="ByteRTCAudioPropertiesInfo"></span>
# ByteRTCAudioPropertiesInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioPropertiesInfo : NSObject
```


Audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[linearVolume](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesInfo-linearvolume) |
|NSInteger |[nonlinearVolume](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesInfo-nonlinearvolume) |
|NSInteger |[vad](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesInfo-vad) |
|NSArray<NSNumber\*\>\* |[spectrum](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesInfo-spectrum) |
|NSInteger |[voicePitch](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesInfo-voicepitch) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioPropertiesInfo-linearvolume"></span>
### linearVolume

```objectivec
@property(assign, nonatomic) NSInteger linearVolume;
```


linear volume. The value is in linear relation to the original volume. The higher the value, the higher the volume. The range is [0,255].


* [0, 25]: Nearly silence

* [26, 75]: Low volume

* [76, 204]: Medium volume

* [205, 255]: High volume

    &nbsp;


<span id="nonlinearvolume"></span>
### nonlinearVolume

```objectivec
@property(assign, nonatomic) NSInteger nonlinearVolume;
```


non\-linear volume in dB. The value is in proportion to the log value of the original volume. You can use the value to recognize the Active Speaker in the room. The range is [\-127, 0].


* [\-127, \-60]: Nearly silence

* [\-59, \-40]: Low volume

* [\-39, \-20]: Medium volume

* [\-19, 0]: High volume

    &nbsp;


<span id="vad"></span>
### vad

```objectivec
@property(assign, nonatomic) NSInteger vad;
```


Voice Activity Detection (VAD) result


* 1: Voice activity detected.

* 0: No voice activity detected.

* \-1: VAD not activated.

    &nbsp;


<span id="spectrum"></span>
### spectrum

```objectivec
@property(copy, nonatomic) NSArray<NSNumber*> * _Nonnull spectrum;
```


Spectrum array. The default length is 257.

<span id="ByteRTCAudioPropertiesInfo-voicepitch"></span>
### voicePitch

```objectivec
@property(assign, nonatomic) NSInteger voicePitch;
```


The vocal pitch of the local user, in Hertz.

When the following two conditions are met at the same time, the vocal pitch of the local user will be returned:


* Calls [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-enableaudiopropertiesreport), and sets the value of enableVoicePitch to `true`.

* The local user's voice is included in the locally captured audio data.

   In other situations, `0` will be returned.

    &nbsp;


<span id="bytertcsinglestreampushtype"></span>
# ByteRTCSingleStreamPushType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCSingleStreamPushType
)
```


forward stream push type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSingleStreamPushToCDN |1 |single\-stream pushing to CDN. |
|ByteRTCSingleStreamPushToRTC |2 |Single stream forwarding to RTC room. |


<span id="ByteRTCLogoutReason"></span>
# ByteRTCLogoutReason

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCLogoutReason
)
```


The reason why users log out

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLogoutReasonLogout |0 |Users choose to sign out by calling `logout` or terminating the engine. |
|ByteRTCLogoutReasonDuplicateLogin |1 |The current user is kicked out as another user signs in with the same user ID. |


<span id="ByteRTCRoomEvent"></span>
# ByteRTCRoomEvent

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRoomEvent
)
```


Room event code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRoomEventUserNotifyStop |\-2013 |When the number of people in the room exceeds 500, stop sending `rtcRoom:onUserJoined:` and `rtcEngine:onUserLeave:reason:` callbacks to existing users in the room, and prompt all users in the room via broadcast. |
|ByteRTCRoomEventForbidden |\-2012 |When the room or user is forbidden, send 'rtcEngine:onRoomEvent:withUid:state:info:' to notify the forbidden time. |


<span id="ByteRTCStreamLayoutMode"></span>
# ByteRTCStreamLayoutMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCStreamLayoutMode
)
```


Layout mode of the WTN stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCStreamLayoutModeAuto |0 |Auto |
|ByteRTCStreamLayoutModeCustom |2 |Manual |


<span id="ByteRTCVideoWatermarkConfig"></span>
# ByteRTCVideoWatermarkConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoWatermarkConfig: NSObject
```


Watermark configurations

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[visibleInPreview](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoWatermarkConfig-visibleinpreview) |
|ByteRTCVideoByteWatermark\* |[positionInLandscapeMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoWatermarkConfig-positioninlandscapemode) |
|ByteRTCVideoByteWatermark\* |[positionInPortraitMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoWatermarkConfig-positioninportraitmode) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoWatermarkConfig-visibleinpreview"></span>
### visibleInPreview

```objectivec
@property(nonatomic, assign) BOOL visibleInPreview;
```


Whether the watermark is visible in preview. Its default value is `true`.

<span id="ByteRTCVideoWatermarkConfig-positioninlandscapemode"></span>
### positionInLandscapeMode

```objectivec
@property(strong, nonatomic) ByteRTCVideoByteWatermark * _Nonnull positionInLandscapeMode;
```


Watermark's coordinates and size in landscape mode. See [ByteRTCVideoByteWatermark](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoByteWatermark).

<span id="ByteRTCVideoWatermarkConfig-positioninportraitmode"></span>
### positionInPortraitMode

```objectivec
@property(strong, nonatomic) ByteRTCVideoByteWatermark * _Nonnull positionInPortraitMode;
```


Watermark's coordinates and size in portrait mode. See [ByteRTCVideoByteWatermark](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoByteWatermark).

<span id="ByteRTCMixedStreamPushMode"></span>
# ByteRTCMixedStreamPushMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMixedStreamPushMode
)
```


The initiation mode for pushing the stream mixed on the server side to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamPushModeOnStream |0 |When no user publishes a media stream, a mixing\-stream task can't be initiated. Default setting.<br><br>When a user publishes at least one media stream, a mixing\-stream task can be initiated. |
|ByteRTCMixedStreamPushModeOnStartRequest |1 |Even if no user is actively publishing media streams, it is still possible to initiate a stream mixing task using a placeholder image.<br><br>&nbsp;<br><br>See [alternateImageUrl](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-alternateimageurl) and [alternateImageFillMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig-alternateimagefillmode) for setting a placeholder image. |


<span id="ByteRTCLocalVideoStats"></span>
# ByteRTCLocalVideoStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCLocalVideoStats : NSObject
```


Local video stream statistics, reference period 2s.

After the local user publishes the video stream successfully, the SDK will periodically notify the local user through `onLocalStreamStats`

The delivery status of the published video stream during this reference period. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[sentKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-sentkbitrate) |
|NSInteger |[inputFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-inputframerate) |
|NSInteger |[sentFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-sentframerate) |
|NSInteger |[encoderOutputFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-encoderoutputframerate) |
|NSInteger |[rendererOutputFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-rendereroutputframerate) |
|NSInteger |[statsInterval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-statsinterval) |
|float |[videoLossRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-videolossrate) |
|NSInteger |[rtt](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-rtt) |
|NSInteger |[encodedBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-encodedbitrate) |
|NSInteger |[encodedFrameWidth](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-encodedframewidth) |
|NSInteger |[encodedFrameHeight](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-encodedframeheight) |
|NSInteger |[encodedFrameCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-encodedframecount) |
|ByteRTCVideoCodecType |[codecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-codectype) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-isscreen) |
|NSInteger |[jitter](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats-jitter) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLocalVideoStats-sentkbitrate"></span>
### sentKBitrate

```objectivec
@property(assign, nonatomic) float sentKBitrate;
```


TX bitrate in Kbps of the video stream with the highest resolution within the reference period

<span id="ByteRTCLocalVideoStats-inputframerate"></span>
### inputFrameRate

```objectivec
@property(assign, nonatomic) NSInteger inputFrameRate;
```


Sampling frame rate in fps of video capture during this reference period

<span id="ByteRTCLocalVideoStats-sentframerate"></span>
### sentFrameRate

```objectivec
@property(assign, nonatomic) NSInteger sentFrameRate;
```


TX frame rate in fps of the video stream with the highest resolution within the reference period

<span id="ByteRTCLocalVideoStats-encoderoutputframerate"></span>
### encoderOutputFrameRate

```objectivec
@property(assign, nonatomic) NSInteger encoderOutputFrameRate;
```


Encoder\-output frame rate in fps of the video stream with the highest resolution within the reference period

<span id="ByteRTCLocalVideoStats-rendereroutputframerate"></span>
### rendererOutputFrameRate

```objectivec
@property(assign, nonatomic) NSInteger rendererOutputFrameRate;
```


Local\-rendering frame rate in fps during this reference period

<span id="ByteRTCLocalVideoStats-statsinterval"></span>
### statsInterval

```objectivec
@property(assign, nonatomic) NSInteger statsInterval;
```


Reference period in ms.

This field is used to set the reference period for the callback, which is 2 s by default.

<span id="ByteRTCLocalVideoStats-videolossrate"></span>
### videoLossRate

```objectivec
@property(assign, nonatomic) float videoLossRate;
```


Video packet loss rate. The video uplink packet loss rate in the reference period, the value range is [0,1].

<span id="ByteRTCLocalVideoStats-rtt"></span>
### rtt

```objectivec
@property(assign, nonatomic) NSInteger rtt;
```


Round\-trip time. The unit is ms.

<span id="ByteRTCLocalVideoStats-encodedbitrate"></span>
### encodedBitrate

```objectivec
@property(assign, nonatomic) NSInteger encodedBitrate;
```


Video encoding bitrate in Kbps of the video stream with the highest resolution within the reference period.

<span id="ByteRTCLocalVideoStats-encodedframewidth"></span>
### encodedFrameWidth

```objectivec
@property(assign, nonatomic) NSInteger encodedFrameWidth;
```


Video encoding width in px of the video stream with the highest resolution within the reference period

<span id="ByteRTCLocalVideoStats-encodedframeheight"></span>
### encodedFrameHeight

```objectivec
@property(assign, nonatomic) NSInteger encodedFrameHeight;
```


Video encoding height in px of the video stream with the highest resolution within the reference period

<span id="ByteRTCLocalVideoStats-encodedframecount"></span>
### encodedFrameCount

```objectivec
@property(assign, nonatomic) NSInteger encodedFrameCount;
```


The total number of the video stream with the highest resolution within the reference period sent in the reference period.

<span id="ByteRTCLocalVideoStats-codectype"></span>
### codecType

```objectivec
@property(nonatomic) ByteRTCVideoCodecType codecType;
```


Encoding type. See [ByteRTCVideoCodecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCodecType) type.

<span id="ByteRTCLocalVideoStats-isscreen"></span>
### isScreen

```objectivec
@property(assign, nonatomic) BOOL isScreen;
```


Reserved field. Ignore the value returned in this field.

<span id="ByteRTCLocalVideoStats-jitter"></span>
### jitter

```objectivec
@property(assign, nonatomic) NSInteger jitter;
```


Video uplink network jitter in ms.

<span id="ByteRTCStream"></span>
# ByteRTCStream

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCStream <NSObject>
```


Stream property.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStream-userid) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStream-isscreen) |
|BOOL |[hasVideo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStream-hasvideo) |
|BOOL |[hasAudio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStream-hasaudio) |
|NSArray<ByteRTCVideoSolution\*\>\* |[videoStreamDescriptions](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStream-videostreamdescriptions) |
|ByteRTCVideoSolution\* |[maxVideoStreamDescription](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStream-maxvideostreamdescription) |
|ByteRTCStreamIndex |[streamIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStream-streamindex) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCStream-userid"></span>
### userId

```objectivec
@property(nonatomic, copy, readonly) NSString * userId;
```


The user ID that published this stream.

<span id="ByteRTCStream-isscreen"></span>
### isScreen

```objectivec
@property(nonatomic, assign, readonly) BOOL isScreen;
```


Reserved field. Ignore the value returned in this field.

<span id="ByteRTCStream-hasvideo"></span>
### hasVideo

```objectivec
@property(nonatomic, assign, readonly) BOOL hasVideo;
```


Whether this stream includes a video stream.

<span id="ByteRTCStream-hasaudio"></span>
### hasAudio

```objectivec
@property(nonatomic, assign, readonly) BOOL hasAudio;
```


Whether the stream includes an audio stream.

<span id="ByteRTCStream-videostreamdescriptions"></span>
### videoStreamDescriptions

```objectivec
@property(nonatomic, copy, readonly) NSArray<ByteRTCVideoSolution *> * videoStreamDescriptions;
```


Resolution information of the video stream.

When a remote user calls [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setvideoencoderconfig) method to publish multiple configured video streams, this will contain attribute information for all video streams published by the user.

See [ByteRTCVideoSolution](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSolution).

<span id="ByteRTCStream-maxvideostreamdescription"></span>
### maxVideoStreamDescription

```objectivec
@property(nonatomic, retain, readonly) ByteRTCVideoSolution *maxVideoStreamDescription;
```


The maximum resolution of the video stream, the maximum publish resolution that can be supported by the callback publisher when multi\-resolution publish subscription is enabled.

<span id="ByteRTCStream-streamindex"></span>
### streamIndex

```objectivec
@property(nonatomic, assign) ByteRTCStreamIndex streamIndex;
```


Reserved field.

<span id="ByteRTCScreenMediaType"></span>
# ByteRTCScreenMediaType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCScreenMediaType
)
```


Screen media type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCScreenMediaTypeVideoOnly |0 |only capture video data |
|ByteRTCScreenMediaTypeAudioOnly |1 |only capture audio data |
|ByteRTCScreenMediaTypeVideoAndAudio |2 |capture video && audio data |


<span id="ByteRTCAudioRecordingConfig"></span>
# ByteRTCAudioRecordingConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioRecordingConfig : NSObject
```


Audio recording configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[absoluteFileName](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioRecordingConfig-absolutefilename) |
|ByteRTCAudioFrameSource |[frameSource](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioRecordingConfig-framesource) |
|ByteRTCAudioSampleRate |[sampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioRecordingConfig-samplerate) |
|ByteRTCAudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioRecordingConfig-channel) |
|ByteRTCAudioQuality |[quality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioRecordingConfig-quality) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioRecordingConfig-absolutefilename"></span>
### absoluteFileName

```objectivec
@property(nonatomic, copy) NSString* _Nonnull absoluteFileName;
```


Absolute path of the recorded file, file name included. The App must have the write and read permission of the path.

**Notes**

The files format is restricted to .aac and .wav.

<span id="ByteRTCAudioRecordingConfig-framesource"></span>
### frameSource

```objectivec
@property(nonatomic, assign) ByteRTCAudioFrameSource frameSource;
```


The source of the recording. See [ByteRTCAudioFrameSource](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFrameSource).

It is ByteRTCAudioFrameSourceTypeMixed = 2 by default.

<span id="ByteRTCAudioRecordingConfig-samplerate"></span>
### sampleRate

```objectivec
@property(nonatomic, assign) ByteRTCAudioSampleRate sampleRate;
```


See [ByteRTCAudioSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioSampleRate).

<span id="ByteRTCAudioRecordingConfig-channel"></span>
### channel

```objectivec
@property(nonatomic, assign) ByteRTCAudioChannel channel;
```


Number of audio channels. See [ByteRTCAudioChannel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioChannel).

If number of audio channels of recording is different than that of audio capture, the behavior is:


* If the number of capture is 1, and the number of recording is 2, the recorded audio is two\-channel data after copying mono\-channel data.

* If the number of capture is 2, and the number of recording is 1, the recorded audio is recorded by mixing the audio of the two channels.

    &nbsp;


<span id="quality"></span>
### quality

```objectivec
@property(nonatomic, assign) ByteRTCAudioQuality quality;
```


Recording quality. Only valid for .aac file. See [ByteRTCAudioQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioQuality).

When the sample rate is 32kHz, the file (10min) size for different qualities are:

```Plain Text
   - low: 1.2MB;
   - [By Default] medium: 2MB;
   - high: 3.75MB;
   - ultra high: 7.5MB.
```


<span id="ByteRTCAudioFrameCallbackMethod"></span>
# ByteRTCAudioFrameCallbackMethod

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioFrameCallbackMethod
)
```


Audio data callback method

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioFrameCallbackRecord |0 |The callback of the audio data recorded by local microphone. |
|ByteRTCAudioFrameCallbackPlayback |1 |The callback of the mixed audio data of all remote users subscribed to by the local user. |
|ByteRTCAudioFrameCallbackMixed |2 |The callback of the mixed audio data including the data recorded by local microphone and that of all remote users subscribed to by the local user. |
|ByteRTCAudioFrameCallbackRemoteUser |3 |The callback of the audio data before mixing of each remote user subscribed to by the local user. |
|ByteRTCAudioFrameCallbackCaptureMixed |5 |The callback of the mixed audio data including the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`. |


<span id="ByteRTCMixedStreamAlternateImageFillMode"></span>
# ByteRTCMixedStreamAlternateImageFillMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMixedStreamAlternateImageFillMode
)
```


The fill mode of the placeholder image.

This parameter is used to control the fill mode of the placeholder image after the user stops publishing video streams and the screen reverts to the placeholder image. It defaults to `kMixedStreamAlternateImageFillModeFit` indicating the image is scaled with the video's aspect ratio.

See [ByteRTCMixedStreamAlternateImageFillMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAlternateImageFillMode).

This parameter is not supported for WTN stream tasks.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamAlternateImageFillModeFit |0 |The placeholder image is scaled with the same aspect ratio as the user's original video frame. Default setting. |
|ByteRTCMixedStreamAlternateImageFillModeFill |1 |The placeholder image is not scaled with the same aspect ratio as the user's original video frame. It maintains the original aspect ratio. |


<span id="ByteRTCNetworkQuality"></span>
# ByteRTCNetworkQuality

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCNetworkQuality
)
```


Media streaming network quality.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCNetworkQualityUnknown |0 |Network quality unknown. |
|ByteRTCNetworkQualityExcellent |1 |The network quality is excellent. |
|ByteRTCNetworkQualityGood |2 |The subjective feeling is similar to kNetworkQualityExcellent, but the bit rate may be slightly lower. |
|ByteRTCNetworkQualityPoor |3 |Subjective feelings are flawed but do not affect communication. |
|ByteRTCNetworkQualityBad |4 |Can barely communicate but not smoothly. |
|ByteRTCNetworkQualityVeryBad |5 |The quality of the network is very poor and communication is basically impossible. |
|ByteRTCNetworkQualityDown |6 |The network is down. It may be down due to no answer within 12s, airplane mode on, disconnected cable, etc.<br><br>&nbsp;<br><br>Refer to [Get connection state](https://docs.byteplus.com/byteplus-rtc/docs/95376) for more details. |


<span id="ByteRTCStreamRemoveReason"></span>
# ByteRTCStreamRemoveReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCStreamRemoveReason
)
```


The reason for the removal of the remote stream in the room.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCStreamRemoveReasonUnpublish |0 |The remote user stops publishing the stream. |
|ByteRTCStreamRemoveReasonPublishFailed |1 |The remote user failed to publish the stream. |
|ByteRTCStreamRemoveReasonKeepLiveFailed |2 |Media server failed to receive media data from the client for 10 seconds. |
|ByteRTCStreamRemoveReasonClientDisconnected |3 |The remote user is disconnected. |
|ByteRTCStreamRemoveReasonRepublish |4 |The remote user republishes the stream. |
|ByteRTCStreamRemoveReasonOther |5 |Other reasons. |
|ByteRTCStreamRemoveReasonPublishPrivilegeExpired |6 |The remote user's publishing privilege of the Token is expired. |


<span id="ByteRTCForwardStreamStateInfo"></span>
# ByteRTCForwardStreamStateInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCForwardStreamStateInfo: NSObject
```


State and error for each room during relaying

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamStateInfo-roomid) |
|ByteRTCForwardStreamState |[state](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamStateInfo-state) |
|ByteRTCForwardStreamError |[error](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamStateInfo-error) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCForwardStreamStateInfo-roomid"></span>
### roomId

```objectivec
@property(strong, nonatomic) NSString* _Nullable roomId;
```


ID of the room to which the media stream is relayed.

An empty string is for all rooms.

<span id="ByteRTCForwardStreamStateInfo-state"></span>
### state

```objectivec
@property(assign, nonatomic) ByteRTCForwardStreamState state;
```


State of the room during relaying. Refer to [ByteRTCForwardStreamState](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamState) for more information.

<span id="ByteRTCForwardStreamStateInfo-error"></span>
### error

```objectivec
@property(assign, nonatomic) ByteRTCForwardStreamError error;
```


Error code from the room during relaying. Refer to [ByteRTCForwardStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCForwardStreamError) for more information.

<span id="ByteRTCSourceCropInfo"></span>
# ByteRTCSourceCropInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCSourceCropInfo : NSObject
```


Crop configuration of the WTN stream

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CGFloat |[locationX](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceCropInfo-locationx) |
|CGFloat |[locationY](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceCropInfo-locationy) |
|CGFloat |[widthProportion](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceCropInfo-widthproportion) |
|CGFloat |[heightProportion](https://docs.byteplus.com/en/docs/12/14181#ByteRTCSourceCropInfo-heightproportion) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCSourceCropInfo-locationx"></span>
### locationX

```objectivec
@property(assign, nonatomic) CGFloat locationX;
```


The normalized scale of the upper\-left corner of the cropped video frame relative to the overall frame before cropping, in the range [0.0, 1.0)

<span id="ByteRTCSourceCropInfo-locationy"></span>
### locationY

```objectivec
@property(assign, nonatomic) CGFloat locationY;
```


The normalized scale of the upper\-left corner of the cropped video frame relative to the overall frame before cropping, in the range [0.0, 1.0)

<span id="ByteRTCSourceCropInfo-widthproportion"></span>
### widthProportion

```objectivec
@property(assign, nonatomic) CGFloat widthProportion;
```


The normalized ratio of the width of the video frame obtained after cropping to the overall frame before cropping, in the range (0.0, 1.0]

<span id="ByteRTCSourceCropInfo-heightproportion"></span>
### heightProportion

```objectivec
@property(assign, nonatomic) CGFloat heightProportion;
```


The normalized ratio of the height of the obtained video frame after cropping to the overall frame before cropping, in the range (0.0, 1.0]

<span id="ByteRTCMulDimSingScoringMode"></span>
# ByteRTCMulDimSingScoringMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMulDimSingScoringMode
)
```


Karaoke scoring mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMulDimSingScoringModeNote |0 |The score is provided based on the pitch. |


<span id="ByteRTCAttenuationType"></span>
# ByteRTCAttenuationType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAttenuationType
)
```


Volume Roll\-off modes that a sound has in an audio source

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAttenuationTypeNone |0 |Disable Volume Attenuation |
|ByteRTCAttenuationTypeLinear |1 |Linear roll\-off mode which lowers the volume of the sound over the distance |
|ByteRTCAttenuationTypeExponential |2 |Exponential roll\-off mode which exponentially decreases the volume of the sound as the distance increases |


<span id="ByteRTCRoomStateChangeReason"></span>
# ByteRTCRoomStateChangeReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRoomStateChangeReason
)
```


Room state change reason.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRoomStateChangeReasonJoinRoom |0 |Join room success for the first time. |
|ByteRTCRoomStateChangeReasonReconnect |1 |Rejoin the room, such as the network is reconnected. |
|ByteRTCRoomStateChangeReasonLeaveRoom |2 |Leave room. |
|ByteRTCRoomStateChangeReasonJoinRoomFailed |\-2001 |Failed to enter the room.<br><br>&nbsp;<br><br>When entering the room for the first time or when the network is disconnected and reconnected due to poor network conditions, entering the room failed due to a server error. The SDK automatically retries joining the room. |
|ByteRTCRoomStateChangeReasonInvalidToken |\-1000 |Token is invalid.<br><br>&nbsp;<br><br>The Token used when calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) is invalid or expired. The user is required to retrieve the token and call the [updateToken:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRTSRoom-updatetoken) to update the token. |
|ByteRTCRoomStateChangeReasonTokenExpired |\-1009 |Token expired. This error code is returned when the user's token expires in the room.<br><br>&nbsp;<br><br>Call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) to rejoin the room with a new required Token. |
|ByteRTCRoomStateChangeReasonUpdateTokenWithInvalidToken |\-1010 |The Token you provided when calling `updateToken:` is invalid. |
|ByteRTCRoomStateChangeReasonRoomForbidden |\-1025 |The room has been banned before the user calls `joinRoom`. |
|ByteRTCRoomStateChangeReasonUserForbidden |\-1026 |The user has been banned before calling `joinRoom`. |
|ByteRTCRoomStateChangeReasonKickedOut |\-1006 |The user has been removed from the room by the administrator via an OpenAPI call. |
|ByteRTCRoomStateChangeReasonRoomDismiss |\-1011 |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. |
|ByteRTCRoomStateChangeReasonDuplicateLogin |\-1004 |The current user is removed from the room because another user with the same user ID joins the room. |
|ByteRTCRoomStateChangeReasonStateAbnormalServerStatus |\-1084 |The user has been removed from the room due to the abnormal server status. This code will be received via [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo).<br><br>&nbsp;<br><br>SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support. |
|ByteRTCRoomStateChangeReasonUnknown |\-1001 |Join room error.<br><br>&nbsp;<br><br>An unknown error occurred when joining the room, which caused the user to fail to join the room. Users are required to rejoin the room. |


<span id="ByteRTCLogLevel"></span>
# ByteRTCLogLevel

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCLogLevel
)
```


Log level.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLogLevelTrace |0 |Print trace level and above information. |
|ByteRTCLogLevelDebug |1 |Print debug level and above information. |
|ByteRTCLogLevelInfo |2 |Print info level and above information. |
|ByteRTCLogLevelWarning |3 |Print warning level and above information. |
|ByteRTCLogLevelError |4 |Print error level information. |


<span id="ByteRTCRemoteVideoRenderConfig"></span>
# ByteRTCRemoteVideoRenderConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteVideoRenderConfig : NSObject
```


Remote video rendering configuration.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCRenderMode |[renderMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoRenderConfig-rendermode) |
|NSInteger |[backgroundColor](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoRenderConfig-backgroundcolor) |
|ByteRTCVideoRotation |[renderRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoRenderConfig-renderrotation) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteVideoRenderConfig-rendermode"></span>
### renderMode

```objectivec
@property(assign, nonatomic) ByteRTCRenderMode renderMode;
```


See [ByteRTCRenderMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRenderMode)

<span id="ByteRTCRemoteVideoRenderConfig-backgroundcolor"></span>
### backgroundColor

```objectivec
@property(assign, nonatomic) NSInteger backgroundColor;
```


Set the background color of the canvas which is not filled with video frame. The range is `[0x00000000, 0xFFFFFFFF]`. The default is `0x00000000`. The Alpha index is ignored.

<span id="ByteRTCRemoteVideoRenderConfig-renderrotation"></span>
### renderRotation

```objectivec
@property(assign, nonatomic) ByteRTCVideoRotation renderRotation;
```


Video frame rotation angle. See [ByteRTCVideoRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoRotation). The default value is 0, which means no rotation is applied.

<span id="ByteRTCAudioRenderType"></span>
# ByteRTCAudioRenderType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioRenderType
)
```


Audio output type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioRenderTypeExternal |0 |Custom render Audio |
|ByteRTCAudioRenderTypeInternal |1 |RTC SDK internal render audio |


<span id="ByteRTCVideoDeviceType"></span>
# ByteRTCVideoDeviceType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoDeviceType
)
```


Current audio device type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoDeviceTypeUnknown |\-1 |Unknown video device |
|ByteRTCVideoDeviceTypeRenderDevice |0 |Video Rendering Device Type |
|ByteRTCVideoDeviceTypeCaptureDevice |1 |Video Acquisition Device Type |
|ByteRTCVideoDeviceTypeScreenCaptureDevice |2 |Screen Capture Device Type |


<span id="ByteRTCVideoOrientation"></span>
# ByteRTCVideoOrientation

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCVideoOrientation
)
```


Orientation of the video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoOrientationAdaptive |0 |(Default) The original orientation of the captured video frame. |
|ByteRTCVideoOrientationPortrait |1 |Portrait mode. Adjust the captured video frame to vertical layout in RTC SDK. |
|ByteRTCVideoOrientationLandscape |2 |Landscape mode. Adjust the captured video frame to horizontal layout in RTC SDK. |


<span id="ByteRTCAlphaLayout"></span>
# ByteRTCAlphaLayout

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAlphaLayout
)
```


The arrangement position of the Alpha channel relative to the RGB channel data.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAlphaLayoutTop |0 |Alpha data is placed above the RGB data. |


<span id="ByteRTCVideoFrameInfo"></span>
# ByteRTCVideoFrameInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoFrameInfo : NSObject
```


Video frame basic information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameInfo-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameInfo-height) |
|ByteRTCVideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameInfo-rotation) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoFrameInfo-width"></span>
### width

```objectivec
@property(nonatomic, assign) NSInteger width;
```


Width of video frame (pixels)

<span id="ByteRTCVideoFrameInfo-height"></span>
### height

```objectivec
@property(nonatomic, assign) NSInteger height;
```


Height of video frame (pixels)

<span id="ByteRTCVideoFrameInfo-rotation"></span>
### rotation

```objectivec
@property(nonatomic, assign) ByteRTCVideoRotation rotation;
```


Video frame clockwise rotation angle. See [ByteRTCVideoRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoRotation).

<span id="ByteRTCScreenCaptureParam"></span>
# ByteRTCScreenCaptureParam

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCScreenCaptureParam : NSObject
```


Screen capture settings

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-width) |
|NSInteger |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-height) |
|NSInteger |[frameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-framerate) |
|NSInteger |[bitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-bitrate) |
|NSInteger |[minBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-minbitrate) |
|CGRect |[regionRect](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-regionrect) |
|ByteRTCMouseCursorCaptureState |[mouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-mousecursorcapturestate) |
|NSArray<NSNumber\*\>\* |[excludedWindowList](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-excludedwindowlist) |
|ByteRTCHighlightConfig\* |[highlightConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCScreenCaptureParam-highlightconfig) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCScreenCaptureParam-width"></span>
### width

```objectivec
@property(nonatomic, assign) NSInteger width;
```


The maximum width of the captured screen, measured in pixel.

<span id="ByteRTCScreenCaptureParam-height"></span>
### height

```objectivec
@property(nonatomic, assign) NSInteger height;
```


The maximum height of the captured screen, measured in pixel.

<span id="ByteRTCScreenCaptureParam-framerate"></span>
### frameRate

```objectivec
@property(nonatomic, assign) NSInteger frameRate;
```


Screen capture frame rate in fps

<span id="ByteRTCScreenCaptureParam-bitrate"></span>
### bitrate

```objectivec
@property(nonatomic, assign) NSInteger bitrate;
```


Screen capture bitrate rate in kbps

<span id="ByteRTCScreenCaptureParam-minbitrate"></span>
### minBitrate

```objectivec
@property(nonatomic, assign) NSInteger minBitrate;
```


Minimum video encoding bitrate in kbps. The encoding bitrate will not be lower than the `minBitrate`.

It defaults to `0`.

It ranges within [0, bitrate). When `bitrate` < `minBitrate`, the bitrate is self\-adapted.

In the following circumstance, the assignment to this variable has no effect:


* When `bitrate` = `0`, the video encoding is disabled.

* When `bitrate` < `0`, the bitrate is self\-adapted.

    &nbsp;


<span id="regionrect"></span>
### regionRect

```objectivec
@property(nonatomic, assign) CGRect regionRect;
```


Screen capture area.

<span id="ByteRTCScreenCaptureParam-mousecursorcapturestate"></span>
### mouseCursorCaptureState

```objectivec
@property(nonatomic, assign) ByteRTCMouseCursorCaptureState mouseCursorCaptureState;
```


Whether to capture the mouse

<span id="ByteRTCScreenCaptureParam-excludedwindowlist"></span>
### excludedWindowList

```objectivec
@property (strong, nonatomic) NSArray<NSNumber *> * _Nullable excludedWindowList;
```


The list of excluded windows.

<span id="ByteRTCScreenCaptureParam-highlightconfig"></span>
### highlightConfig

```objectivec
@property (strong, nonatomic) ByteRTCHighlightConfig * _Nonnull highlightConfig;
```


Settings for highlighting borders of the sharing region. See [ByteRTCHighlightConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHighlightConfig).

<span id="ByteRTCProblemFeedbackRoomInfo"></span>
# ByteRTCProblemFeedbackRoomInfo

```objectivec
BYTERTC_APPLE_EXPORT  @interface ByteRTCProblemFeedbackRoomInfo: NSObject
```


Video call quality feedback preset information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCProblemFeedbackRoomInfo-roomid) |
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCProblemFeedbackRoomInfo-userid) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCProblemFeedbackRoomInfo-roomid"></span>
### roomId

```objectivec
@property(nonatomic, copy) NSString * _Nonnull roomId;
```


Room ID.

<span id="ByteRTCProblemFeedbackRoomInfo-userid"></span>
### userId

```objectivec
@property(nonatomic, copy) NSString * _Nonnull userId;
```


User ID.

<span id="ByteRTCSetRoomExtraInfoResult"></span>
# ByteRTCSetRoomExtraInfoResult

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSetRoomExtraInfoResult
)
```


Extra information setting result.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSetRoomExtraInfoResultSuccess |0 |Success. |
|ByteRTCSetRoomExtraInfoResultNotJoinRoom |\-1 |Failure. You are not in the room. |
|ByteRTCSetRoomExtraInfoResultKeyIsNull |\-2 |Failure. The key pointer is null. |
|ByteRTCSetRoomExtraInfoResultValueIsNull |\-3 |Failure. The value pointer is null. |
|ByteRTCSetRoomExtraInfoResultUnknow |\-99 |Failure. Unknown error. |
|ByteRTCSetRoomExtraInfoResultKeyIsEmpty |\-400 |Failure. The key length is 0. |
|ByteRTCSetRoomExtraInfoResultTooOften |\-406 |Failure. Excessively frequent setting. 10 times per second is preferable. |
|ByteRTCSetRoomExtraInfoResultSilentUser |\-412 |Failure. Invisible users are not allowed to call `setRoomExtraInfo`. |
|ByteRTCSetRoomExtraInfoResultKeyTooLong |\-413 |Failure. Key length exceeds 10 bytes. |
|ByteRTCSetRoomExtraInfoResultValueTooLong |\-414 |Failure. Value length exceeds 128 bytes. |
|ByteRTCSetRoomExtraInfoResultServerError |\-500 |Failure. Server error. |


<span id="ByteRTCEarMonitorAudioFilter"></span>
# ByteRTCEarMonitorAudioFilter

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCEarMonitorAudioFilter
)
```


Whether to include the local audio filters in the in\-ear monitoring.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCEarMonitorAudioFilterNone |0x0001 |No audio processing. |
|ByteRTCEarMonitorAudioFilterReuseAudioProcessing |0x8000 |Audio processed by your processor or the SDK built\-in audio processor, such as 3A, voice changer, and reverb. |


<span id="ByteRTCVideoFrameData"></span>
# ByteRTCVideoFrameData

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoFrameData : NSObject
```


Video frame data

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCVideoBufferType |[bufferType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-buffertype) |
|ByteRTCVideoPixelFormat |[pixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-pixelformat) |
|ByteRTCVideoContentType |[contentType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-contenttype) |
|CMTime |[timestamp](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-timestamp) |
|int |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-height) |
|CVPixelBufferRef |[cvpixelbuffer](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-cvpixelbuffer) |
|ByteRTCVideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-rotation) |
|ByteRTCCameraID |[cameraId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-cameraid) |
|NSData\* |[seiData](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-seidata) |
|NSData\* |[roiData](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-roidata) |
|int |[numberOfPlanes](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-numberofplanes) |
|void\*\* |[planeDataArray](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-planedataarray) |
|int\* |[planeStrideArray](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrameData-planestridearray) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoFrameData-buffertype"></span>
### bufferType

```objectivec
@property ByteRTCVideoBufferType bufferType;
```


Video frame buffer type, see [ByteRTCVideoBufferType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoBufferType). Required.

<span id="ByteRTCVideoFrameData-pixelformat"></span>
### pixelFormat

```objectivec
@property ByteRTCVideoPixelFormat pixelFormat;
```


Video frame pixel format, see [ByteRTCVideoPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoPixelFormat). Required, when `bufferType` is `ByteRTCVideoBufferTypeRawMemory` and `ByteRTCVideoBufferTypeGLTexture`.

<span id="ByteRTCVideoFrameData-contenttype"></span>
### contentType

```objectivec
@property ByteRTCVideoContentType contentType;
```


Video content type, see [ByteRTCVideoContentType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoContentType).

<span id="ByteRTCVideoFrameData-timestamp"></span>
### timestamp

```objectivec
@property CMTime timestamp;
```


The timestamp of the current video frame. Required.

<span id="ByteRTCVideoFrameData-width"></span>
### width

```objectivec
@property int width;
```


Video frame width. Required.

<span id="ByteRTCVideoFrameData-height"></span>
### height

```objectivec
@property int height;
```


Video frame height. Required.

<span id="ByteRTCVideoFrameData-cvpixelbuffer"></span>
### cvpixelbuffer

```objectivec
@property CVPixelBufferRef _Nullable cvpixelbuffer;
```


Data of `CVPixelBufferRef` type. Required, when format is `kPixelFormatCVPixelBuffer`

<span id="ByteRTCVideoFrameData-rotation"></span>
### rotation

```objectivec
@property ByteRTCVideoRotation rotation;
```


Video frame rotation angle, see [ByteRTCVideoRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoRotation).

<span id="ByteRTCVideoFrameData-cameraid"></span>
### cameraId

```objectivec
@property ByteRTCCameraID cameraId;
```


Camera position info of the video frame, see [ByteRTCCameraID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCCameraID)

<span id="ByteRTCVideoFrameData-seidata"></span>
### seiData

```objectivec
@property NSData * _Nullable seiData;
```


SEI data

<span id="ByteRTCVideoFrameData-roidata"></span>
### roiData

```objectivec
@property NSData * _Nullable roiData;
```


ROI(Region of Interest) Data in a video frame

<span id="ByteRTCVideoFrameData-numberofplanes"></span>
### numberOfPlanes

```objectivec
@property int numberOfPlanes;
```


The number of video frame planes. Required, when `bufferType` is `ByteRTCVideoBufferTypeRawMemory` and `ByteRTCVideoBufferTypeGLTexture`.

<span id="ByteRTCVideoFrameData-planedataarray"></span>
### planeDataArray

```objectivec
@property void ** _Nullable planeDataArray;
```


Array of video frame planes. Required, when `bufferType` is `ByteRTCVideoBufferTypeRawMemory` and `ByteRTCVideoBufferTypeGLTexture`.

<span id="ByteRTCVideoFrameData-planestridearray"></span>
### planeStrideArray

```objectivec
@property int * _Nullable planeStrideArray;
```


Array of stride. Stride is the length of memory between two lines of image data in video frame plane in bytes. Required, when `bufferType` is `ByteRTCVideoBufferTypeRawMemory` and `ByteRTCVideoBufferTypeGLTexture`.

<span id="ByteRTCAudioVolumeInfo"></span>
# ByteRTCAudioVolumeInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioVolumeInfo : NSObject
```


User ID of the source of the audio stream, and the corresponding volume.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[uid](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioVolumeInfo-uid) |
|NSUInteger |[linearVolume](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioVolumeInfo-linearvolume) |
|NSUInteger |[nonlinearVolume](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioVolumeInfo-nonlinearvolume) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioVolumeInfo-uid"></span>
### uid

```objectivec
@property(copy, nonatomic) NSString * _Nonnull uid;
```


User ID of the audio stream source

<span id="ByteRTCAudioVolumeInfo-linearvolume"></span>
### linearVolume

```objectivec
@property(assign, nonatomic) NSUInteger linearVolume;
```


LinearVolume, range: [0,255]

<span id="ByteRTCAudioVolumeInfo-nonlinearvolume"></span>
### nonlinearVolume

```objectivec
@property(assign, nonatomic) NSUInteger nonlinearVolume;
```


NonlinearVolume, range: [\-127,0]

<span id="ByteRTCLocalProxyInfo"></span>
# ByteRTCLocalProxyInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCLocalProxyInfo : NSObject
```


Detailed information of local proxy configurations.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCLocalProxyType |[localProxyType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalProxyInfo-localproxytype) |
|NSString\* |[localProxyIp](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalProxyInfo-localproxyip) |
|int |[localProxyPort](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalProxyInfo-localproxyport) |
|NSString\* |[localProxyUsername](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalProxyInfo-localproxyusername) |
|NSString\* |[localProxyPassword](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalProxyInfo-localproxypassword) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLocalProxyInfo-localproxytype"></span>
### localProxyType

```objectivec
@property(assign, nonatomic) ByteRTCLocalProxyType localProxyType;
```


Types of the local proxies. Refer to [ByteRTCLocalProxyType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalProxyType) for details.

<span id="ByteRTCLocalProxyInfo-localproxyip"></span>
### localProxyIp

```objectivec
@property(copy, nonatomic) NSString * _Nullable localProxyIp;
```


Local proxy IP.

<span id="ByteRTCLocalProxyInfo-localproxyport"></span>
### localProxyPort

```objectivec
@property(assign, nonatomic) int localProxyPort;
```


Local proxy port.

<span id="ByteRTCLocalProxyInfo-localproxyusername"></span>
### localProxyUsername

```objectivec
@property(copy, nonatomic) NSString * _Nullable localProxyUsername;
```


The username of the local proxy.

<span id="ByteRTCLocalProxyInfo-localproxypassword"></span>
### localProxyPassword

```objectivec
@property(copy, nonatomic) NSString * _Nullable localProxyPassword;
```


The password of the local proxy.

<span id="ByteRTCMixedStreamMediaType"></span>
# ByteRTCMixedStreamMediaType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMixedStreamMediaType
)
```


The media type of mixing stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamMediaTypeAudioAndVideo |0 |Audio and video |
|ByteRTCMixedStreamMediaTypeAudioOnly |1 |Audio only |


<span id="ByteRTCRecordingProgress"></span>
# ByteRTCRecordingProgress

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRecordingProgress : NSObject
```


Local recording progress

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|unsignedlonglong |[duration](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingProgress-duration) |
|unsignedlonglong |[fileSize](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRecordingProgress-filesize) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRecordingProgress-duration"></span>
### duration

```objectivec
@property(assign, nonatomic) unsigned long long duration;
```


The cumulative recording time of the current file, in milliseconds

<span id="ByteRTCRecordingProgress-filesize"></span>
### fileSize

```objectivec
@property(assign, nonatomic) unsigned long long fileSize;
```


The size of the currently recorded file in bytes

<span id="ByteRTCAudioSelectionPriority"></span>
# ByteRTCAudioSelectionPriority

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCAudioSelectionPriority
)
```


User priority in the audio selection

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioSelectionPriorityNormal |0 |Normally, whether the stream can be subscribed is determined by the result of audio selection. |
|ByteRTCAudioSelectionPriorityHigh |1 |High priority with which the stream can skip audio selection and always be subscribable. |


<span id="ByteRTCAudioSampleRate"></span>
# ByteRTCAudioSampleRate

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioSampleRate
)
```


Audio sample rate in Hz.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioSampleRateAuto |\-1 |Default value. 48000Hz. |
|ByteRTCAudioSampleRate8000 |8000 |8000Hz |
|ByteRTCAudioSampleRate11025 |11025 |11025Hz |
|ByteRTCAudioSampleRate16000 |16000 |16000Hz |
|ByteRTCAudioSampleRate22050 |22050 |22050Hz |
|ByteRTCAudioSampleRate24000 |24000 |24000Hz |
|ByteRTCAudioSampleRate32000 |32000 |32000Hz |
|ByteRTCAudioSampleRate44100 |44100 |44100Hz |
|ByteRTCAudioSampleRate48000 |48000 |48000Hz |


<span id="ByteRTCAudioChannel"></span>
# ByteRTCAudioChannel

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioChannel
)
```


Audio channel

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioChannelAuto |\-1 |Default value. `2` by default. |
|ByteRTCAudioChannelMono |1 |Mono channel. |
|ByteRTCAudioChannelStereo |2 |Dual channels. |


<span id="ByteRTCHardwareEchoDetectionResult"></span>
# ByteRTCHardwareEchoDetectionResult

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCHardwareEchoDetectionResult
)
```


Result of the detection inited before joining a room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCHardwareEchoDetectionCanceled |0 |Detection is stopped by the call of `stopHardwareEchoDetection` before the SDK reports the detection result. |
|ByteRTCHardwareEchoDetectionUnknown |1 |Unknown state<br><br>&nbsp;<br><br>Contact us if you retry several times but keep failing. |
|ByteRTCHardwareEchoDetectionNormal |2 |Excellent<br><br>&nbsp;<br><br>No echo issue is detected. |
|ByteRTCHardwareEchoDetectionPoor |3 |Echo<br><br>&nbsp;<br><br>Echo issue is detected. Recommend the user join the call with a headset through the interface. |


<span id="ByteRTCEffectBeautyMode"></span>
# ByteRTCEffectBeautyMode

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCEffectBeautyMode
)
```


Basic beauty effect.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCEffectBeautyModeWhite |0 |Brightening. |
|ByteRTCEffectBeautyModeSmooth |1 |Smoothing. |
|ByteRTCEffectBeautyModeSharpen |2 |Sharpening. |
|ByteRTCEffectBeautyModeClear |3 |Clarity. Integrating Effects SDK v4.4.2+ is required for this sub\-item. |


<span id="ByteRTCVideoCanvas"></span>
# ByteRTCVideoCanvas

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoCanvas : NSObject
```


Video rendering mode

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCView\* |[view](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCanvas-view) |
|ByteRTCRenderMode |[renderMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCanvas-rendermode) |
|NSInteger |[backgroundColor](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCanvas-backgroundcolor) |
|ByteRTCVideoRotation |[renderRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCanvas-renderrotation) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoCanvas-view"></span>
### view

```objectivec
@property(strong, nonatomic) ByteRTCView* _Nullable view;
```


Local view handle

<span id="ByteRTCVideoCanvas-rendermode"></span>
### renderMode

```objectivec
@property(assign, nonatomic) ByteRTCRenderMode renderMode;
```


See [ByteRTCRenderMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRenderMode)

<span id="ByteRTCVideoCanvas-backgroundcolor"></span>
### backgroundColor

```objectivec
@property(assign, nonatomic) NSInteger backgroundColor;
```


Set the background color of the canvas which is not filled with video frame. The range is `[0x00000000, 0xFFFFFFFF]`. The default is `0x00000000`. The Alpha index is ignored.

<span id="ByteRTCVideoCanvas-renderrotation"></span>
### renderRotation

```objectivec
@property(assign, nonatomic) ByteRTCVideoRotation renderRotation;
```


Video frame rotation angle. See [ByteRTCVideoRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoRotation). The default value is 0, which means no rotation is applied.

This parameter only applies to remote video and does not affect local video settings.

<span id="ByteRTCRemoteAudioState"></span>
# ByteRTCRemoteAudioState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRemoteAudioState
)
```


The remote audio stream state of the user subscription.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRemoteAudioStateStopped |0 |The default initial state of the remote audio stream is called back at the following times:<br><br><br>&nbsp;<br><br>* Local users stop receiving the remote audio stream, the corresponding reason is `ByteRTCRemoteAudioStateChangeReasonLocalMuted` in [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStateChangeReason)<br><br>* The remote user stopped sending the audio stream, the corresponding reason is `ByteRTCRemoteAudioStateChangeReasonRemoteMuted` in [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStateChangeReason)<br><br>* The remote user left the room, the corresponding reason is `ByteRTCRemoteAudioStateChangeReasonRemoteOffline` in [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStateChangeReason) |
|ByteRTCRemoteAudioStateStarting |1 |Start receiving the remote audio stream header. |
|ByteRTCRemoteAudioStateDecoding |2 |The remote audio stream is decoding and playing normally. The state will be called back at the following times:<br><br><br>&nbsp;<br><br>* The first frame of the remote audio is successfully decoded, and the corresponding reason is ByteRTCRemoteAudioStateChangeReason in [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStateChangeReason)<br><br>* The network returned to normal from blocking, and the corresponding reason is ByteRTCRemoteAudioStateChangeReason in [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStateChangeReason)<br><br>* Local users recover receiving remote audio streams due to ByteRTCRemoteAudioStateChangeReason in [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStateChangeReason)<br><br>* The remote user resumes sending audio streams, the corresponding reason is ByteRTCRemoteAudioStateChangeReason in [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStateChangeReason) |
|ByteRTCRemoteAudioStateFrozen |3 |Remote audio stream stalls. |


<span id="ByteRTCMuteState"></span>
# ByteRTCMuteState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMuteState
)
```


Transmission/Playback state of the media stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMuteStateOff |0 |Enable |
|ByteRTCMuteStateOn |1 |Disable |


<span id="ByteRTCVideoPreprocessorConfig"></span>
# ByteRTCVideoPreprocessorConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoPreprocessorConfig : NSObject
```


Video processing configuration parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCVideoPixelFormat |[requiredPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoPreprocessorConfig-requiredpixelformat) |
|ByteRTCProcessorActionDomain |[actionDomain](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoPreprocessorConfig-actiondomain) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoPreprocessorConfig-requiredpixelformat"></span>
### requiredPixelFormat

```objectivec
@property(nonatomic, assign) ByteRTCVideoPixelFormat requiredPixelFormat;
```


For the pixel format of the video frame. See [ByteRTCVideoPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoPixelFormat).

Only `ByteRTCVideoPixelFormatI420` and `ByteRTCVideoPixelFormatUnknown` are supported.

<span id="ByteRTCVideoPreprocessorConfig-actiondomain"></span>
### actionDomain

```objectivec
@property(nonatomic, assign) ByteRTCProcessorActionDomain actionDomain;
```


The effective range of the custom video preprocessor. See [ByteRTCProcessorActionDomain](https://docs.byteplus.com/en/docs/12/14181#ByteRTCProcessorActionDomain).

<span id="ByteRTCRemoteAudioStateChangeReason"></span>
# ByteRTCRemoteAudioStateChangeReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRemoteAudioStateChangeReason
)
```


Receives the cause of the remote audio stream state change.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRemoteAudioStateChangeReasonInternal |0 |Internal reasons |
|ByteRTCRemoteAudioStateChangeReasonNetworkCongestion |1 |Network blocking |
|ByteRTCRemoteAudioStateChangeReasonNetworkRecovery |2 |Network back to normal |
|ByteRTCRemoteAudioStateChangeReasonLocalMuted |3 |Local user stops receiving remote audio stream |
|ByteRTCRemoteAudioStateChangeReasonLocalUnmuted |4 |Local users resume receiving remote audio streams |
|ByteRTCRemoteAudioStateChangeReasonRemoteMuted |5 |Remote user stops sending audio stream |
|ByteRTCRemoteAudioStateChangeReasonRemoteUnmuted |6 |Remote user resumes sending audio stream |
|ByteRTCRemoteAudioStateChangeReasonRemoteOffline |7 |Remote user leaves room |


<span id="ByteRTCLocalVideoStreamState"></span>
# ByteRTCLocalVideoStreamState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCLocalVideoStreamState
)
```


Local video stream status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalVideoStreamStateStopped |0 |Local video default initial state<br><br>&nbsp;<br><br>Callback the state when the camera stops working, corresponding to the error code [ByteRTCLocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStreamError) ByteRTCLocalVideoStreamErrorOk |
|ByteRTCLocalVideoStreamStateRecording |1 |The local video recording device starts successfully<br><br>&nbsp;<br><br>Callback the state when the first frame of the video is collected, corresponding to the error code [ByteRTCLocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStreamError) ByteRTCLocalVideoStreamErrorOk |
|ByteRTCLocalVideoStreamStateEncoding |2 |Local video first frame encoding success<br><br>&nbsp;<br><br>Local video first frame encoding success callback to the state, corresponding to the error code [ByteRTCLocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStreamError) in ByteRTCLocalVideoStreamErrorOk |
|ByteRTCLocalVideoStreamStateFailed |3 |Local video startup failed, the status is called back at the following times:<br><br><br>&nbsp;<br><br>* The local acquisition device failed to start, corresponding to the error code [ByteRTCLocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStreamError) ByteRTCLocalVideoStreamErrorCaptureFailure<br><br>* No camera permission was detected, corresponding to the error code [ByteRTCLocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStreamError) ByteRTCLocalVideoStreamErrorDeviceNoPermission<br><br>* The video encoding failed, corresponding to the error code [ByteRTCLocalVideoStreamError](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStreamError) in ByteRTCLocalVideoStreamErrorEncodeFailure |


<span id="ByteRTCFirstFrameSendState"></span>
# ByteRTCFirstFrameSendState

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCFirstFrameSendState
)
```


First frame sending status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCFirstFrameSendStateSending |0 |Sending |
|ByteRTCFirstFrameSendStateSent |1 |Sent successfully |
|ByteRTCFirstFrameSendStateEnd |2 |Send failed |


<span id="ByteRTCRemoteMirrorType"></span>
# ByteRTCRemoteMirrorType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCRemoteMirrorType
)
```


Mirroring type for remote stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRemoteMirrorTypeNone |0 |(Default) Disable mirroring effect for remote streams. |
|ByteRTCRemoteMirrorTypeRender |1 |Enable mirroring effect for remote streams. |


<span id="ByteRTCVoiceEqualizationConfig"></span>
# ByteRTCVoiceEqualizationConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVoiceEqualizationConfig : NSObject
```


Voice equalization effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCBandFrequency |[frequency](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceEqualizationConfig-frequency) |
|int |[gain](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceEqualizationConfig-gain) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVoiceEqualizationConfig-frequency"></span>
### frequency

```objectivec
@property(assign, nonatomic) ByteRTCBandFrequency frequency;
```


Frequency band. See [ByteRTCBandFrequency](https://docs.byteplus.com/en/docs/12/14181#ByteRTCBandFrequency).

<span id="ByteRTCVoiceEqualizationConfig-gain"></span>
### gain

```objectivec
@property(assign, nonatomic) int gain;
```


Gain of the frequency band in dB. The range is `[-15, 15]`.

<span id="ByteRTCConnectionState"></span>
# ByteRTCConnectionState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCConnectionState
)
```


SDK Connection status with the signaling server.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCConnectionStateDisconnected |1 |Disconnected for 12s, SDK will try to reconnect automatically. |
|ByteRTCConnectionStateConnecting |2 |The first request to connect to the server. Connecting. |
|ByteRTCConnectionStateConnected |3 |The first connection was successful. |
|ByteRTCConnectionStateReconnecting |4 |The code includes the following status:<br><br><br>&nbsp;<br><br>* The first connection is not successful for 10s.<br><br>* The connection has been lost for 10s. Auto reconnecting. |
|ByteRTCConnectionStateReconnected |5 |Successful reconnection after disconnection. |
|ByteRTCConnectionStateLost |6 |In status `ByteRTCConnectionStateDisconnected` for more than 10s without a successful reconnection. SDK will still continue to try to reconnect. |
|ByteRTCConnectionStateFailed |7 |Connection failure caused by abnormal state of the server. SDK will not automatically reconnect, please re\-enter the room or contact technical support. |


<span id="ByteRTCFallbackOrRecoverReason"></span>
# ByteRTCFallbackOrRecoverReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCFallbackOrRecoverReason
)
```


Reason of the Fallback or reverting from a Fallback of the subscribed stream or the publishing stream

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCFallbackOrRecoverReasonUnknown |\-1 |The default: Fallback due to an unknown reason that is neither insufficient bandwidth of the network nor poor\-performance of the device |
|ByteRTCFallbackOrRecoverReasonSubscribeFallbackByBandwidth |0 |Fallback of the subscribed stream due to insufficient bandwidth of the network |
|ByteRTCFallbackOrRecoverReasonSubscribeFallbackByPerformance |1 |Fallback of the subscribed stream due to poor performance of the device |
|ByteRTCFallbackOrRecoverReasonSubscribeRecoverByBandwidth |2 |Reverting from a Fallback of the subscribed stream due to the recovery of the network bandwidth |
|ByteRTCFallbackOrRecoverReasonSubscribeRecoverByPerformance |3 |Reverting from a Fallback of the subscribed stream due to the amelioration of the device performance |
|ByteRTCFallbackOrRecoverReasonPublishFallbackByBandwidth |4 |Fallback of the publishing stream due to Insufficient bandwidth of the network |
|ByteRTCFallbackOrRecoverReasonPublishFallbackByPerformance |5 |Fallback of the publishing stream due to poor\-performance of the device |
|ByteRTCFallbackOrRecoverReasonPublishRecoverByBandwidth |6 |Reverting from a Fallback of the publishing stream due to the recovery of the network bandwidth |
|ByteRTCFallbackOrRecoverReasonPublishRecoverByPerformance |7 |Reverting from a Fallback of the publishing stream due to the amelioration of the device performance |


<span id="ByteRTCRecordingFileType"></span>
# ByteRTCRecordingFileType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRecordingFileType
)
```


Storage format of locally recorded files

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRecordingFileTypeAAC |0 |AAC format file |
|ByteRTCRecordingFileTypeMP4 |1 |MP4 format file |


<span id="ByteRTCVideoPictureType"></span>
# ByteRTCVideoPictureType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoPictureType
)
```


Video compression picture type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoPictureTypeUnknown |0 |Unknown type |
|ByteRTCVideoPictureTypeI |1 |I\-frames, key frames which are coded without reference to any other frame. |
|ByteRTCVideoPictureTypeP |2 |P\-frames, forward\-predicted frames which are coded by a forward predictive coding method. |
|ByteRTCVideoPictureTypeB |3 |B\-frames, bi\-directionally predicted frames which are coded by both forward and backward predictive coding method. |


<span id="ByteRTCVideoStreamScaleMode"></span>
# ByteRTCVideoStreamScaleMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoStreamScaleMode
)
```


Video frame scale mode

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoStreamScaleModeAuto |0 |Auto mode, default to ByteRTCVideoStreamScaleModeFitWithCropping. |
|ByteRTCVideoStreamScaleModeStretch |1 |Stretch the video frame until the video frame and the window have the same resolution. The video frame's aspect ratio can be changed as it is automatically stretched to fill the window, but the whole image is visible. |
|ByteRTCVideoStreamScaleModeFitWithCropping |2 |Fit the window with cropping<br><br>&nbsp;<br><br>Scale the video frame uniformly until the window is filled. If the video frame's aspect ratio is different from that of the window, the extra part of the video frame will be cropped.<br><br>&nbsp;<br><br>After the scaling process is completed, the width or height of the video frame will be consistent with that of the window, and the other dimension will be greater than or equal to that of the window. |
|ByteRTCVideoStreamScaleModeFitWithFilling |3 |Fit the window with filling<br><br>&nbsp;<br><br>Scale the video frame uniformly until its width or height reaches the boundary of the window. If the video frame's aspect ratio is different from that of the window, the area that is not filled will be black.<br><br>&nbsp;<br><br>After the scaling process is completed, the width or height of the video frame will be consistent with that of the window, and the other dimension will be less than or equal to that of the window. |


<span id="DestInfo"></span>
# DestInfo

```objectivec
BYTERTC_APPLE_EXPORT  @interface DestInfo: NSObject
```


Configurations for pushing a single media stream destination room info

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#DestInfo-roomid) |
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#DestInfo-userid) |


<span id="instructions"></span>
## Instructions

<span id="DestInfo-roomid"></span>
### roomId

```objectivec
@property(nonatomic, copy) NSString * _Nonnull roomId;
```


Room ID.

<span id="DestInfo-userid"></span>
### userId

```objectivec
@property(nonatomic, copy) NSString * _Nonnull userId;
```


User ID.

<span id="ByteRTCVideoSinkPixelFormat"></span>
# ByteRTCVideoSinkPixelFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoSinkPixelFormat
)
```


Video frame encoding format

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoSinkPixelFormatOriginal |0 |Original format |
|ByteRTCVideoSinkPixelFormatI420 |1 |YUV I420 |
|ByteRTCVideoSinkPixelFormatNV12 |2 |YUV NV12 |
|ByteRTCVideoSinkPixelFormatRGBA |5 |RGBA format |
|ByteRTCVideoSinkPixelFormatBGRA |7 |BGRA |


<span id="ByteRTCAudioMixingError"></span>
# ByteRTCAudioMixingError

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioMixingError
)
```


Error code for audio mixing

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioMixingErrorOk |0 |OK |
|ByteRTCAudioMixingErrorPreloadFailed |1 |Preload failed. Invalid path or the length exceeds 20s. |
|ByteRTCAudioMixingErrorStartFailed |2 |Mixing failed. Invalid path or fail to open the file. |
|ByteRTCAudioMixingErrorIdNotFound |3 |Invalid mixID |
|ByteRTCAudioMixingErrorSetPositionFailed |4 |Invalid position |
|ByteRTCAudioMixingErrorInValidVolume |5 |Invalid volume. The range is [0, 400]. |
|ByteRTCAudioMixingErrorLoadConflict |6 |Another file was preloaded for mixing. Call unloadAudioMixing: first. |
|ByteRTCAudioMixingErrorIdTypeNotMatch |7 |Invalid mix type. |
|ByteRTCAudioMixingErrorInValidPitch |8 |Invalid pitch value. |
|ByteRTCAudioMixingErrorInValidAudioTrack |9 |Invalid audio track. |
|ByteRTCAudioMixingErrorIsStarting |10 |Mixing starting. |
|ByteRTCAudioMixingErrorInValidPlaybackSpeed |11 |Invalid playback speed |


<span id="ByteRTCMixedStreamSpatialAudioConfig"></span>
# ByteRTCMixedStreamSpatialAudioConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamSpatialAudioConfig : NSObject
```


Spatial audio config when pushing to CDN.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enableSpatialRender](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamSpatialAudioConfig-enablespatialrender) |
|ByteRTCPosition\* |[audienceSpatialPosition](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamSpatialAudioConfig-audiencespatialposition) |
|ByteRTCHumanOrientation\* |[audienceSpatialOrientation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamSpatialAudioConfig-audiencespatialorientation) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamSpatialAudioConfig-enablespatialrender"></span>
### enableSpatialRender

```objectivec
@property(assign, nonatomic) BOOL enableSpatialRender;
```


Whether to enable the spatial audio effect when pushing to CDN.

when you enable the feature, set the `spatialPosition` of each [ByteRTCMixedStreamLayoutRegionConfig](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamLayoutRegionConfig) for spatial audio effect.

<span id="ByteRTCMixedStreamSpatialAudioConfig-audiencespatialposition"></span>
### audienceSpatialPosition

```objectivec
@property (strong, nonatomic) ByteRTCPosition * _Nullable audienceSpatialPosition;
```


The spatial position of the audience. See [ByteRTCPosition](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPosition).

The audience is the users who receive the audio stream from CDN.

This parameter is not supported for WTN stream tasks.

<span id="ByteRTCMixedStreamSpatialAudioConfig-audiencespatialorientation"></span>
### audienceSpatialOrientation

```objectivec
@property(strong, nonatomic) ByteRTCHumanOrientation * _Nullable audienceSpatialOrientation;
```


The orientation of the audience. See [ByteRTCHumanOrientation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHumanOrientation).

The audience is the users who receive the audio stream from CDN.

<span id="ByteRTCRoomState"></span>
# ByteRTCRoomState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRoomState
)
```


Room state code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRoomStateJoinSuccess |0 |Join room success. |
|ByteRTCRoomStateJoinFailed |1 |Join room failed. |
|ByteRTCRoomStateLeft |2 |Leave room. |


<span id="ByteRTCProblemFeedbackInfo"></span>
# ByteRTCProblemFeedbackInfo

```objectivec
BYTERTC_APPLE_EXPORT  @interface ByteRTCProblemFeedbackInfo: NSObject
```


Video call quality feedback preset information.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[problemDesc](https://docs.byteplus.com/en/docs/12/14181#ByteRTCProblemFeedbackInfo-problemdesc) |
|NSArray<ByteRTCProblemFeedbackRoomInfo\*\>\* |[roomInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCProblemFeedbackInfo-roominfo) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCProblemFeedbackInfo-problemdesc"></span>
### problemDesc

```objectivec
@property(nonatomic, copy) NSString * _Nonnull problemDesc;
```


Text description corresponding to the feedback.

<span id="ByteRTCProblemFeedbackInfo-roominfo"></span>
### roomInfo

```objectivec
@property(nonatomic, strong) NSArray<ByteRTCProblemFeedbackRoomInfo *> * _Nullable roomInfo;
```


Text description corresponding to the feedback room information. See [ByteRTCProblemFeedbackRoomInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCProblemFeedbackRoomInfo).

<span id="ByteRTCRectangle"></span>
# ByteRTCRectangle

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRectangle : NSObject
```


A rectangle that you can move around and re\-size to share just the portion of the screen defined by that rectangle.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[x](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRectangle-x) |
|int |[y](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRectangle-y) |
|int |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRectangle-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRectangle-height) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRectangle-x"></span>
### x

```objectivec
@property(assign, nonatomic) int x;
```


The upper\-left X coordinate of the rectangle.

<span id="ByteRTCRectangle-y"></span>
### y

```objectivec
@property(assign, nonatomic) int y;
```


The upper\-left Y coordinate of the rectangle.

<span id="ByteRTCRectangle-width"></span>
### width

```objectivec
@property(assign, nonatomic) int width;
```


Width(in px).

<span id="ByteRTCRectangle-height"></span>
### height

```objectivec
@property(assign, nonatomic) int height;
```


Height(in px).

<span id="ByteRTCColorSpace"></span>
# ByteRTCColorSpace

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCColorSpace
)
```


ColorSpace

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCColorSpaceUnknown |0 |Unknown color space, default kColorSpaceYCbCrBT601LimitedRange color space |
|ByteRTCColorSpaceYCbCrBT601LimitedRange |1 |BT.601 Digital Coding Standard, Color Space [16\-235] |
|ByteRTCColorSpaceYCbCrBT601FullRange |2 |\- |
|ByteRTCColorSpaceYCbCrBT709LimitedRange |3 |BT.7091 Digital Coding Standard, Color Space [16\-235] |
|ByteRTCColorSpaceYCbCrBT709FullRange |4 |BT.7091 Digital Coding Standard, Color Space [0\-255] |


<span id="ByteRTCExpressionDetectResult"></span>
# ByteRTCExpressionDetectResult

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCExpressionDetectResult : NSObject
```


Expression Detection Result

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[detectResult](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectResult-detectresult) |
|int |[faceCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectResult-facecount) |
|NSArray<ByteRTCExpressionDetectInfo\*\>\* |[detectInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectResult-detectinfo) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCExpressionDetectResult-detectresult"></span>
### detectResult

```objectivec
@property (assign, nonatomic) int detectResult;
```


Expression detection result


* 0: Success

* !0: Failure

    &nbsp;


<span id="facecount"></span>
### faceCount

```objectivec
@property (assign, nonatomic) int faceCount;
```


The number of detected faces.

<span id="ByteRTCExpressionDetectResult-detectinfo"></span>
### detectInfo

```objectivec
@property (nonatomic, copy) NSArray<ByteRTCExpressionDetectInfo *> * _Nonnull detectInfo;
```


Expression detection information. The length of the array is the same as the number of detected faces. See [ByteRTCExpressionDetectInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCExpressionDetectInfo).

<span id="ByteRTCEncodedVideoFrame"></span>
# ByteRTCEncodedVideoFrame

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCEncodedVideoFrame : NSObject
```


Information about video frames

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCVideoCodecType |[codecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-codectype) |
|ByteRTCVideoPictureType |[pictureType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-picturetype) |
|SInt64 |[timestampUs](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-timestampus) |
|SInt64 |[timestampDtsUs](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-timestampdtsus) |
|int |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-height) |
|ByteRTCVideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-rotation) |
|NSData\* |[data](https://docs.byteplus.com/en/docs/12/14181#ByteRTCEncodedVideoFrame-data) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCEncodedVideoFrame-codectype"></span>
### codecType

```objectivec
@property(assign, nonatomic) ByteRTCVideoCodecType codecType;
```


Video encoding type. See [ByteRTCVideoCodecType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoCodecType)

<span id="ByteRTCEncodedVideoFrame-picturetype"></span>
### pictureType

```objectivec
@property(assign, nonatomic) ByteRTCVideoPictureType pictureType;
```


Encoded type of video frame. See [ByteRTCVideoPictureType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoPictureType)

<span id="ByteRTCEncodedVideoFrame-timestampus"></span>
### timestampUs

```objectivec
@property(assign, nonatomic) SInt64 timestampUs;
```


Video capture timestamp in microseconds

<span id="ByteRTCEncodedVideoFrame-timestampdtsus"></span>
### timestampDtsUs

```objectivec
@property(assign, nonatomic) SInt64 timestampDtsUs;
```


Video encoding timestamp in microseconds

<span id="ByteRTCEncodedVideoFrame-width"></span>
### width

```objectivec
@property(assign, nonatomic) int width;
```


Video frame width in px

<span id="ByteRTCEncodedVideoFrame-height"></span>
### height

```objectivec
@property(assign, nonatomic) int height;
```


Video frame height in px

<span id="ByteRTCEncodedVideoFrame-rotation"></span>
### rotation

```objectivec
@property(nonatomic, assign) ByteRTCVideoRotation rotation;
```


Video frame rotation angle. See [ByteRTCVideoRotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoRotation)

<span id="ByteRTCEncodedVideoFrame-data"></span>
### data

```objectivec
@property(strong, nonatomic) NSData * _Nonnull data;
```


The pointer to the video frame

<span id="ByteRTCMediaDeviceType"></span>
# ByteRTCMediaDeviceType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMediaDeviceType
)
```


Type of media device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaDeviceTypeAudioUnknown |\-1 |Unknown device |
|ByteRTCMediaDeviceTypeAudioRenderDevice |0 |Screen audio recorder |
|ByteRTCMediaDeviceTypeAudioCaptureDevice |1 |Microphone |
|ByteRTCMediaDeviceTypeVideoRenderDevice |2 |\- |
|ByteRTCMediaDeviceTypeVideoCaptureDevice |3 |Video capture device |
|ByteRTCMediaDeviceTypeScreenVideoCaptureDevice |4 |Screen video capture device |
|ByteRTCMediaDeviceTypeScreenAudioCaptureDevice |5 |Screen audio recorder |


<span id="ByteRTCFrameUpdateInfo"></span>
# ByteRTCFrameUpdateInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCFrameUpdateInfo : NSObject
```


The pixels and frame rate recommended by RTC.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[pixel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFrameUpdateInfo-pixel) |
|int |[framerate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCFrameUpdateInfo-framerate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCFrameUpdateInfo-pixel"></span>
### pixel

```objectivec
@property(assign, nonatomic) int pixel;
```


Pixel (width \* height).

<span id="ByteRTCFrameUpdateInfo-framerate"></span>
### framerate

```objectivec
@property(assign, nonatomic) int framerate;
```


The frame rate.

<span id="ByteRTCAnsMode"></span>
# ByteRTCAnsMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAnsMode
)
```


ANC modes. The ANC algorithm is determined by the room profile you set when calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig).

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAnsModeDisable |0 |Disable ANC. |
|ByteRTCAnsModeLow |1 |Cancel subtle background noise. |
|ByteRTCAnsModeMedium |2 |Cancel medium\-level, continuous noise, such as the sound of fans or air conditioners. |
|ByteRTCAnsModeHigh |3 |Cancel loud, impulsive, and intermittent noise, such as keyboard clicking noise, a crash/clash, a bark, and chair scraping noise. |
|ByteRTCAnsModeAutomatic |4 |Enable automatic ANC. The ANC algorithm is dynamically determined by RTC. |


<span id="ByteRTCRemoteUserPriority"></span>
# ByteRTCRemoteUserPriority

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCRemoteUserPriority
)
```


Priority of the publisher. When a user encounters performance insufficiency of either the network or the device, the media stream will fall back in the ascending order of `RemoteUserPriority`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRemoteUserPriorityLow |0 |Low, the default |
|ByteRTCRemoteUserPriorityMedium |100 |Medium |
|ByteRTCRemoteUserPriorityHigh |200 |High |


<span id="ByteRTCHumanOrientation"></span>
# ByteRTCHumanOrientation

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCHumanOrientation : NSObject
```


Three\-dimensional orientation information, each pair of vectors need to be perpendicular. See [ByteRTCOrientation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCOrientation).

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCOrientation\* |[forward](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHumanOrientation-forward) |
|ByteRTCOrientation\* |[right](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHumanOrientation-right) |
|ByteRTCOrientation\* |[up](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHumanOrientation-up) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCHumanOrientation-forward"></span>
### forward

```objectivec
@property(nonatomic, strong) ByteRTCOrientation* _Nonnull forward;
```


Forward orientation, the default value is {1,0,0}, i.e., the forward orientation is in the positive direction of x\-axis.

<span id="ByteRTCHumanOrientation-right"></span>
### right

```objectivec
@property(nonatomic, strong) ByteRTCOrientation* _Nonnull right;
```


Rightward orientation, the default value is {0,1,0}, i.e., the rightward orientation is in the positive direction of y\-axis.

<span id="ByteRTCHumanOrientation-up"></span>
### up

```objectivec
@property(nonatomic, strong) ByteRTCOrientation* _Nonnull up;
```


Upward orientation, the default value is {0,0,1}, i.e., the upward orientation is in the positive direction of z\-axis.

<span id="ByteRTCRecordingErrorCode"></span>
# ByteRTCRecordingErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRecordingErrorCode
)
```


Local recording error code

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRecordingErrorCodeOk |0 |Recording normal |
|ByteRTCRecordingErrorCodeNoPermission |\-1 |No file write permissions |
|ByteRTCRecordingErrorCodeNotSupport |\-2 |The current version SDK does not support local recording, please contact technical support |
|ByteRTCRecordingErrorCodeOther |\-3 |Other anomalies |


<span id="ByteRTCTorchState"></span>
# ByteRTCTorchState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCTorchState
)
```


Torch status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCTorchStateOff |0 |Torch off |
|ByteRTCTorchStateOn |1 |Torch on |


<span id="ByteRTCAudioFrame"></span>
# ByteRTCAudioFrame

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioFrame : NSObject
```


Audio frame in PCM

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSData\* |[buffer](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFrame-buffer) |
|int |[samples](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFrame-samples) |
|ByteRTCAudioChannel |[channel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFrame-channel) |
|ByteRTCAudioSampleRate |[sampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioFrame-samplerate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioFrame-buffer"></span>
### buffer

```objectivec
@property(strong, nonatomic) NSData * _Nonnull buffer;
```


PCM data

<span id="ByteRTCAudioFrame-samples"></span>
### samples

```objectivec
@property(assign, nonatomic) int samples;
```


Total number of samples

<span id="ByteRTCAudioFrame-channel"></span>
### channel

```objectivec
@property(assign, nonatomic) ByteRTCAudioChannel channel;
```


Audio channel. See [ByteRTCAudioChannel](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioChannel).

For dual channels, the audio frames are interleaved.

<span id="ByteRTCAudioFrame-samplerate"></span>
### sampleRate

```objectivec
@property(assign, nonatomic) ByteRTCAudioSampleRate sampleRate;
```


Sample rate. See [ByteRTCAudioSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioSampleRate).

<span id="ByteRTCRemoteAudioStats"></span>
# ByteRTCRemoteAudioStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteAudioStats : NSObject
```


Remote audio stream statistics, reference period 2s.

After the remote audio stream subscription is successful, the SDK will periodically notify the local user of the reception status of the subscribed audio stream during this reference period through `onRemoteStreamStats`

. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[audioLossRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-audiolossrate) |
|float |[receivedKBitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-receivedkbitrate) |
|NSInteger |[stallCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-stallcount) |
|NSInteger |[stallDuration](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-stallduration) |
|NSInteger |[playoutSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-playoutsamplerate) |
|NSInteger |[e2eDelay](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-e2edelay) |
|NSInteger |[statsInterval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-statsinterval) |
|NSInteger |[rtt](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-rtt) |
|NSInteger |[totalRtt](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-totalrtt) |
|NSInteger |[quality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-quality) |
|NSInteger |[jitterBufferDelay](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-jitterbufferdelay) |
|NSInteger |[numChannels](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-numchannels) |
|NSInteger |[receivedSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-receivedsamplerate) |
|NSInteger |[frozenRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-frozenrate) |
|NSInteger |[concealedSamples](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-concealedsamples) |
|NSInteger |[concealmentEvent](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-concealmentevent) |
|NSInteger |[decSampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-decsamplerate) |
|NSInteger |[decDuration](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-decduration) |
|NSInteger |[jitter](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-jitter) |
|double |[decodeFrameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats-decodeframerate) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteAudioStats-audiolossrate"></span>
### audioLossRate

```objectivec
@property(assign, nonatomic) float audioLossRate;
```


Audio packet loss rate. The audio downlink packet loss rate in the reference period, the value range is [0,1].

<span id="ByteRTCRemoteAudioStats-receivedkbitrate"></span>
### receivedKBitrate

```objectivec
@property(assign, nonatomic) float receivedKBitrate;
```


Receiving bit rate. The audio reception rate in the reference period in kbps.

<span id="ByteRTCRemoteAudioStats-stallcount"></span>
### stallCount

```objectivec
@property(assign, nonatomic) NSInteger stallCount;
```


Number of audio stutters. Number of stutters in the reference period.

<span id="ByteRTCRemoteAudioStats-stallduration"></span>
### stallDuration

```objectivec
@property(assign, nonatomic) NSInteger stallDuration;
```


Audio stuttering duration. Stuttering duration in the reference period in ms.

<span id="ByteRTCRemoteAudioStats-playoutsamplerate"></span>
### playoutSampleRate

```objectivec
@property(assign, nonatomic) NSInteger playoutSampleRate;
```


Play sample rate. Audio playback sample rate information within the reference period in Hz.

<span id="ByteRTCRemoteAudioStats-e2edelay"></span>
### e2eDelay

```objectivec
@property(assign, nonatomic) NSInteger e2eDelay;
```


End\-to\-end latency at the user experience level. The delay from the completion of encoding at the transmitting end to the completion of decoding at the receiving end, in units of ms.

<span id="ByteRTCRemoteAudioStats-statsinterval"></span>
### statsInterval

```objectivec
@property(assign, nonatomic) NSInteger statsInterval;
```


Statistical interval. The interval of this reference period is in ms.

<span id="ByteRTCRemoteAudioStats-rtt"></span>
### rtt

```objectivec
@property(assign, nonatomic) NSInteger rtt;
```


Round\-trip time for client side to server level data transfer in ms.

<span id="ByteRTCRemoteAudioStats-totalrtt"></span>
### totalRtt

```objectivec
@property(assign, nonatomic) NSInteger totalRtt;
```


The sender\-server level\-the receiver\-link data transmission round\-trip time. The unit is ms.

<span id="ByteRTCRemoteAudioStats-quality"></span>
### quality

```objectivec
@property(assign, nonatomic) NSInteger quality;
```


The quality of the audio stream sent by the remote user. Value meaning reference [ByteRTCNetworkQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQuality).

<span id="ByteRTCRemoteAudioStats-jitterbufferdelay"></span>
### jitterBufferDelay

```objectivec
@property(assign, nonatomic) NSInteger jitterBufferDelay;
```


The delay caused by the introduction of the jitter buffer mechanism. The unit is ms.

<span id="ByteRTCRemoteAudioStats-numchannels"></span>
### numChannels

```objectivec
@property(assign, nonatomic) NSInteger numChannels;
```


Number of audio channels.

<span id="ByteRTCRemoteAudioStats-receivedsamplerate"></span>
### receivedSampleRate

```objectivec
@property(assign, nonatomic) NSInteger receivedSampleRate;
```


Audio reception sampling rate. Remote audio sample rate information received within the reference period, in Hz.

<span id="ByteRTCRemoteAudioStats-frozenrate"></span>
### frozenRate

```objectivec
@property(assign, nonatomic) NSInteger frozenRate;
```


The accumulated length of audio stuttering that occurs after the remote user joins the room, as a percentage of the total effective length of the audio. The effective duration of audio refers to the duration of audio other than stopping sending audio streams and disabling audio modules after remote users enter the room to publish audio streams.

<span id="ByteRTCRemoteAudioStats-concealedsamples"></span>
### concealedSamples

```objectivec
@property(assign, nonatomic) NSInteger concealedSamples;
```


Audio PLC Total number of sample points.

<span id="ByteRTCRemoteAudioStats-concealmentevent"></span>
### concealmentEvent

```objectivec
@property(assign, nonatomic) NSInteger concealmentEvent;
```


PLC cumulative times.

<span id="ByteRTCRemoteAudioStats-decsamplerate"></span>
### decSampleRate

```objectivec
@property(assign, nonatomic) NSInteger decSampleRate;
```


Audio decoding sample rate. Audio decoding sample rate information in the reference period in Hz.

<span id="ByteRTCRemoteAudioStats-decduration"></span>
### decDuration

```objectivec
@property(assign, nonatomic) NSInteger decDuration;
```


Cumulative decoding time in seconds of the remote audio stream in this subscription.

<span id="ByteRTCRemoteAudioStats-jitter"></span>
### jitter

```objectivec
@property(assign, nonatomic) NSInteger jitter;
```


Video downlink network jitter in ms.

<span id="ByteRTCRemoteAudioStats-decodeframerate"></span>
### decodeFrameRate

```objectivec
@property(assign, nonatomic) double decodeFrameRate;
```


Audio decode frame rate.

<span id="ByteRTCOrientation"></span>
# ByteRTCOrientation

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCOrientation : NSObject
```


Direction Orientation Information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/14181#ByteRTCOrientation-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/14181#ByteRTCOrientation-y) |
|float |[z](https://docs.byteplus.com/en/docs/12/14181#ByteRTCOrientation-z) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCOrientation-x"></span>
### x

```objectivec
@property(nonatomic, assign) float x;
```


X\-coordinate

<span id="ByteRTCOrientation-y"></span>
### y

```objectivec
@property(nonatomic, assign) float y;
```


Y\-coordinate

<span id="ByteRTCOrientation-z"></span>
### z

```objectivec
@property(nonatomic, assign) float z;
```


Z\-coordinate

<span id="ByteRTCPerformanceAlarmReason"></span>
# ByteRTCPerformanceAlarmReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPerformanceAlarmReason
)
```


Reasons for performance\-related alarms

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPerformanceAlarmReasonBandwidthFallback |0 |The poor network causes the transmission performance to fall back. This reason is only received when sending performance fallback is turned on. |
|ByteRTCPerformanceAlarmReasonBandwidthResumed |1 |Network performance recovery, transmission performance rollback recovery. This reason is only received when sending performance fallback is turned on. |
|ByteRTCPerformanceAlarmReasonFallback |2 |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance is insufficient;<br><br>&nbsp;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance is insufficient and the send performance fallback has occurred. |
|ByteRTCPerformanceAlarmReasonResumed |3 |If the send performance fallback is not turned on, when receiving this alarm, it means that the performance shortage has been restored;<br><br>&nbsp;<br><br>If the send performance fallback is turned on, when receiving this alarm, it means that the performance shortage has been restored and the send performance fallback has occurred. Recovery. |


<span id="ByteRTCVideoApplyRotation"></span>
# ByteRTCVideoApplyRotation

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoApplyRotation
)
```


Whether the video frame needs to be automatically rotated.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoApplyRotationDefault |\-1 |(Default) No rotation. |
|ByteRTCVideoApplyRotation0 |0 |Automatic rotation, which rotates video frames to 0 degrees based on the rotation angle information. |


<span id="ByteRTCAACProfile"></span>
# ByteRTCAACProfile

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAACProfile
)
```


> Deprecated since 3.52, use [ByteRTCMixedStreamAudioProfile](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioProfile) instead.


Advanced Audio Coding (AAC) profile.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAACProfileLC |0 |(Default) AAC Low\-Complexity profile (AAC\-LC). |
|ByteRTCAACProfileHEv1 |1 |HE\-AAC v1 profile (AAC LC with SBR). |
|ByteRTCAACProfileHEv2 |2 |HE\-AAC v2 profile (AAC LC with SBR and Parametric Stereo). |


<span id="ByteRTCRoomEventInfo"></span>
# ByteRTCRoomEventInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRoomEventInfo : NSObject
```


Room event info.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[forbiddenTime](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRoomEventInfo-forbiddentime) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRoomEventInfo-forbiddentime"></span>
### forbiddenTime

```objectivec
@property(assign, nonatomic) NSInteger forbiddenTime;
```


When the room or user is forbidden, send 'rtcEngine:onRoomEvent:withUid:state:info:' to notify the forbidden time.

<span id="ByteRTCSyncInfoStreamType"></span>
# ByteRTCSyncInfoStreamType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSyncInfoStreamType
)
```


Stream type for media stream information synchronization

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSyncInfoStreamTypeAudio |0 |Audio stream |


<span id="ByteRTCVoiceChangerType"></span>
# ByteRTCVoiceChangerType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVoiceChangerType
)
```


Change sound effect type. For more types, contact the technical support.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVoiceChangerOriginal |0 |Acoustic, no special effects |
|ByteRTCVoiceChangerGiant |1 |Giant |
|ByteRTCVoiceChangerChipmunk |2 |Chipmunk |
|ByteRTCVoiceChangerMinionst |3 |Minion |
|ByteRTCVoiceChangerVibrato |4 |Vibrato |
|ByteRTCVoiceChangerRobot |5 |Robot |


<span id="ByteRTCStandardPitchInfo"></span>
# ByteRTCStandardPitchInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCStandardPitchInfo : NSObject
```


Standard Pitch Data.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[startTime](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStandardPitchInfo-starttime) |
|int |[duration](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStandardPitchInfo-duration) |
|int |[pitch](https://docs.byteplus.com/en/docs/12/14181#ByteRTCStandardPitchInfo-pitch) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCStandardPitchInfo-starttime"></span>
### startTime

```objectivec
@property(nonatomic, assign) int startTime;
```


Starting time, unit: ms.

<span id="ByteRTCStandardPitchInfo-duration"></span>
### duration

```objectivec
@property(nonatomic, assign) int duration;
```


Duration, unit: ms.

<span id="ByteRTCStandardPitchInfo-pitch"></span>
### pitch

```objectivec
@property(nonatomic, assign) int pitch;
```


pitch.

<span id="ByteRTCMixedStreamAudioProfile"></span>
# ByteRTCMixedStreamAudioProfile

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMixedStreamAudioProfile
)
```


Advanced Audio Coding (AAC) profile.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamAudioProfileLC |0 |(Default) AAC Low\-Complexity profile (AAC\-LC). |
|ByteRTCMixedStreamAudioProfileHEv1 |1 |HE\-AAC v1 profile (AAC LC with SBR). |
|ByteRTCMixedStreamAudioProfileHEv2 |2 |HE\-AAC v2 profile (AAC LC with SBR and Parametric Stereo). |


<span id="ByteRTCVoiceReverbConfig"></span>
# ByteRTCVoiceReverbConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVoiceReverbConfig : NSObject
```


Voice reverb effect.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[roomSize](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceReverbConfig-roomsize) |
|float |[decayTime](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceReverbConfig-decaytime) |
|float |[damping](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceReverbConfig-damping) |
|float |[wetGain](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceReverbConfig-wetgain) |
|float |[dryGain](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceReverbConfig-drygain) |
|float |[preDelay](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVoiceReverbConfig-predelay) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVoiceReverbConfig-roomsize"></span>
### roomSize

```objectivec
@property(assign, nonatomic) float roomSize;
```


The room size for reverb simulation. The range is `[0.0, 100.0]`. The default value is `50.0f`. The larger the room, the stronger the reverberation.

<span id="ByteRTCVoiceReverbConfig-decaytime"></span>
### decayTime

```objectivec
@property(assign, nonatomic) float decayTime;
```


The decay time of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="ByteRTCVoiceReverbConfig-damping"></span>
### damping

```objectivec
@property(assign, nonatomic) float damping;
```


The damping index of the reverb effect. The range is `[0.0, 100.0]`. The default value is `50.0f`.

<span id="ByteRTCVoiceReverbConfig-wetgain"></span>
### wetGain

```objectivec
@property(assign, nonatomic) float wetGain;
```


The intensity of the wet signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="ByteRTCVoiceReverbConfig-drygain"></span>
### dryGain

```objectivec
@property(assign, nonatomic) float dryGain;
```


The Intensity of the dry signal in dB. The range is `[-20.0, 10.0]`. The default value is `0.0f`.

<span id="ByteRTCVoiceReverbConfig-predelay"></span>
### preDelay

```objectivec
@property(assign, nonatomic) float preDelay;
```


The delay of the wet signal in ms. The range is `[0.0, 200.0]`. The default value is `0.0f`.

<span id="ByteRTCSEICountPerFrame"></span>
# ByteRTCSEICountPerFrame

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSEICountPerFrame
)
```


SEI sending mode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSEICountPerFrameSingle |0 |Single\-SEI mode. A single video frame carries at most one SEI message.<br><br>When you send multiple SEI messages in 1 frame, they will be sent in sequence following consecutive video frames.<br><br>For example, if you need to send 3 SEI data within a certain frame, then the 1st SEI will be sent in the current frame, the 2nd SEI will be sent in the next frame, and the 3rd SEI will be sent in the frame after that. |
|ByteRTCSEICountPerFrameMulti |1 |Multi\-SEI mode.<br><br>When you send multiple SEI messages in 1 frame, all these SEI data will be sent together in the next frame, which can reduce sending delay, but a frame will carry multiple SEI messages.<br><br>For example, if there are 3 SEI data to be sent within a 1\-frame interval, these 3 SEIs will all be sent on the next video frame. |


<span id="ByteRTCPublishFallbackOption"></span>
# ByteRTCPublishFallbackOption

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCPublishFallbackOption
)
```


Stream fallback options of publisher

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPublishFallbackOptionDisabled |0 |Default setting. No fallback is allowed under limited network conditions. |
|ByteRTCPublishFallbackOptionSimulcast |1 |Under limited network conditions, the video streams that you published will degrade sequentially from the highest\-quality stream to the lowest\-quality stream until it can match current network conditions. |


<span id="ByteRTCPosition"></span>
# ByteRTCPosition

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCPosition : NSObject
```


Coordinate value of the local user's position in the rectangular coordinate system in the RTC room.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|float |[x](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPosition-x) |
|float |[y](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPosition-y) |
|float |[z](https://docs.byteplus.com/en/docs/12/14181#ByteRTCPosition-z) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCPosition-x"></span>
### x

```objectivec
@property(nonatomic, assign) float x;
```


X\-coordinate

<span id="ByteRTCPosition-y"></span>
### y

```objectivec
@property(nonatomic, assign) float y;
```


Y\-coordinate

<span id="ByteRTCPosition-z"></span>
### z

```objectivec
@property(nonatomic, assign) float z;
```


Z\-coordinate

<span id="ByteRTCVideoSolution"></span>
# ByteRTCVideoSolution

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCVideoSolution: NSObject
```


Video stream parameters

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|CGSize |[videoSize](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSolution-videosize) |
|NSInteger |[frameRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSolution-framerate) |
|NSInteger |[maxKbps](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSolution-maxkbps) |
|NSInteger |[minKbps](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSolution-minkbps) |
|ByteRTCVideoEncoderPreference |[encoderPreference](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoSolution-encoderpreference) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoSolution-videosize"></span>
### videoSize

```objectivec
@property(nonatomic, assign) CGSize videoSize;
```


Video resolution

<span id="ByteRTCVideoSolution-framerate"></span>
### frameRate

```objectivec
@property(nonatomic, assign) NSInteger frameRate;
```


Video frame rate

<span id="ByteRTCVideoSolution-maxkbps"></span>
### maxKbps

```objectivec
@property(nonatomic, assign) NSInteger maxKbps;
```


Maximum bitrate (kbps). You can use `-1` to use the self\-adaptive bitrate based on the resolution and framerate.

<span id="ByteRTCVideoSolution-minkbps"></span>
### minKbps

```objectivec
@property(nonatomic, assign) NSInteger minKbps;
```


Minimum bitrate (kbps).

<span id="ByteRTCVideoSolution-encoderpreference"></span>
### encoderPreference

```objectivec
@property(nonatomic, assign) ByteRTCVideoEncoderPreference encoderPreference;
```


Encoder preference. See [ByteRTCVideoEncoderPreference](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoEncoderPreference)

<span id="ByteRTCRemoteVideoConfig"></span>
# ByteRTCRemoteVideoConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteVideoConfig : NSObject
```


Information on remote video frame

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[framerate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoConfig-framerate) |
|int |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoConfig-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoConfig-height) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteVideoConfig-framerate"></span>
### framerate

```objectivec
@property (nonatomic, assign) int framerate;
```


Expected maximum frame rate of the subscribed stream in fps. The default value is 0, which represents full\-frame\-rate, values greater than 0 are valid.

If the frame rate of the stream published is higher than the value set by the subscriber, the subscriber receives the video of the frame rate set by this API; if the frame rate of the stream published is lower than the value set by the subscriber, the subscriber receives the video of the same frame rate of the video published.

Only valid if the stream is coded with SVC technique.

<span id="ByteRTCRemoteVideoConfig-width"></span>
### width

```objectivec
@property(nonatomic, assign) int  width;
```


Width of the video frame in px

<span id="ByteRTCRemoteVideoConfig-height"></span>
### height

```objectivec
@property(nonatomic, assign) int   height;
```


Height of the video frame in px

<span id="ByteRTCProcessorActionDomain"></span>
# ByteRTCProcessorActionDomain

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCProcessorActionDomain
)
```


The effective range of the custom video preprocessor, including preview only, encode only, and both preview and encode.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCProcessorActionDomainPreviewAndEncode |0 |The processed video frames are used for both local preview and pushing to the remote. |
|ByteRTCProcessorActionDomainPreview |1 |The processed video frames are used for local preview only. |
|ByteRTCProcessorActionDomainEncode |2 |The processed video frames are used for pushing to the remote only. |


<span id="ByteRTCLocalVideoStreamError"></span>
# ByteRTCLocalVideoStreamError

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCLocalVideoStreamError
)
```


Error code when the local video state changes

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLocalVideoStreamErrorOk |0 |Local video status is normal (the default return value when the local video status changes to normal) |
|ByteRTCLocalVideoStreamErrorFailure |1 |Local video stream publishing failed |
|ByteRTCLocalVideoStreamErrorDeviceNoPermission |2 |No access to the local video capture device |
|ByteRTCLocalVideoStreamErrorDeviceBusy |3 |Local video capture equipment is occupied |
|ByteRTCLocalVideoStreamErrorDeviceNotFound |4 |The local video capture device does not exist or has been removed |
|ByteRTCLocalVideoStreamErrorCaptureFailure |5 |Local video capture failed, it is recommended to check whether the acquisition device is working properly |
|ByteRTCLocalVideoStreamErrorEncodeFailure |6 |Local video encoding failed |
|ByteRTCLocalVideoStreamErrorDeviceDisconnected |7 |The local video capture device is disconnected. It is occupied by other programs during the call. |


<span id="ByteRTCZoomConfigType"></span>
# ByteRTCZoomConfigType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCZoomConfigType
)
```


Digital Zoom type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCZoomConfigTypeFocusOffset |0 |set ZoomIn/ZoomOut config |
|ByteRTCZoomConfigTypeMoveOffset |1 |set move config |


<span id="ByteRTCMediaPlayerCustomSource"></span>
# ByteRTCMediaPlayerCustomSource

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMediaPlayerCustomSource : NSObject
```


The audio source for media player.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id<ByteRTCMediaPlayerCustomSourceProvider\> |[provider](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerCustomSource-provider) |
|ByteRTCMediaPlayerCustomSourceMode |[mode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerCustomSource-mode) |
|ByteRTCMediaPlayerCustomSourceStreamType |[type](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerCustomSource-type) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMediaPlayerCustomSource-provider"></span>
### provider

```objectivec
@property(weak, nonatomic) id<ByteRTCMediaPlayerCustomSourceProvider> _Nullable provider;
```


Specify the [ByteRTCMediaPlayerCustomSourceProvider](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCMediaPlayerCustomSourceProvider) instance when you want to play the audio data in memory.

<span id="ByteRTCMediaPlayerCustomSource-mode"></span>
### mode

```objectivec
@property(assign, nonatomic) ByteRTCMediaPlayerCustomSourceMode mode;
```


See [ByteRTCMediaPlayerCustomSourceMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerCustomSourceMode). `push` by default.

<span id="ByteRTCMediaPlayerCustomSource-type"></span>
### type

```objectivec
@property(assign, nonatomic) ByteRTCMediaPlayerCustomSourceStreamType type;
```


See [ByteRTCMediaPlayerCustomSourceStreamType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerCustomSourceStreamType). `raw` by default.

<span id="ByteRTCNetworkQualityStats"></span>
# ByteRTCNetworkQualityStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCNetworkQualityStats: NSObject
```


Tx/Rx network quality

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[uid](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQualityStats-uid) |
|double |[lossRatio](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQualityStats-lossratio) |
|int |[rtt](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQualityStats-rtt) |
|int |[totalBandwidth](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQualityStats-totalbandwidth) |
|ByteRTCNetworkQuality |[txQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQualityStats-txquality) |
|ByteRTCNetworkQuality |[rxQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQualityStats-rxquality) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCNetworkQualityStats-uid"></span>
### uid

```objectivec
@property(strong, nonatomic) NSString* _Nonnull uid;
```


User ID

<span id="ByteRTCNetworkQualityStats-lossratio"></span>
### lossRatio

```objectivec
@property(assign, nonatomic) double lossRatio;
```


Packet loss ratio of the local client, ranging [0.0,1.0]

For a local user, it is the sent\-packet loss ratio.

For a remote user, it is the loss ratio of all the packets received.

<span id="ByteRTCNetworkQualityStats-rtt"></span>
### rtt

```objectivec
@property(assign, nonatomic) int rtt;
```


Round\-trip time (RTT) from client to server. Effective for the local user. Unit: ms

<span id="ByteRTCNetworkQualityStats-totalbandwidth"></span>
### totalBandwidth

```objectivec
@property(assign, nonatomic) int totalBandwidth;
```


Average transmission rate of the media RTP packets in 2s. unit: bps

For a local user, it is the packet\-sending speed.

For a remote user, it is the speed of receiving all the subscribed media streams.

<span id="ByteRTCNetworkQualityStats-txquality"></span>
### txQuality

```objectivec
@property(assign, nonatomic) ByteRTCNetworkQuality txQuality;
```


Tx network quality grade. Refer to [ByteRTCNetworkQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQuality) for details.

<span id="ByteRTCNetworkQualityStats-rxquality"></span>
### rxQuality

```objectivec
@property(assign, nonatomic) ByteRTCNetworkQuality rxQuality;
```


Rx network quality grade. Refer to [ByteRTCNetworkQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQuality) for details.

<span id="ByteRTCMixedStreamLayoutRegionType"></span>
# ByteRTCMixedStreamLayoutRegionType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMixedStreamLayoutRegionType
)
```


The contents of the layout section in the mixing stream, including video section and water mark section.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamLayoutRegionTypeVideoStream |0 |Video. |
|ByteRTCMixedStreamLayoutRegionTypeImage |1 |Watermark image. |


<span id="ByteRTCAudioFrameMethod"></span>
# ByteRTCAudioFrameMethod

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioFrameMethod
)
```


The audio input for the audio processor.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioFrameProcessorRecord |0 |Locally captured audio frame. |
|ByteRTCAudioFrameProcessorPlayback |1 |The mixed remote audio. |
|ByteRTCAudioFrameProcessorRemoteUser |2 |The audio streams from remote users. |
|ByteRTCAudioFrameProcessorScreen |4 |The shared\-screen audio. |


<span id="ByteRTCEarMonitorMode"></span>
# ByteRTCEarMonitorMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCEarMonitorMode
)
```


Whether to enable in\-ear monitoring.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCEarMonitorModeOff |0 |Off. |
|ByteRTCEarMonitorModeOn |1 |On. |


<span id="ByteRTCVideoCodecType"></span>
# ByteRTCVideoCodecType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoCodecType
)
```


Video encoding type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoCodecTypeUnknown |0 |Unknown type |
|ByteRTCVideoCodecTypeH264 |1 |H.264 format |
|ByteRTCVideoCodecTypeByteVC1 |2 |ByteVC1 format |


<span id="ByteRTCLocalStreamStats"></span>
# ByteRTCLocalStreamStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCLocalStreamStats : NSObject
```


Local audio/video stream statistics and network status, the reference period is 2s.

After the local user publishes the audio/video stream successfully, the SDK will periodically notify the local user through `onLocalStreamStats`

The transmission status of the published audio/video stream during this reference period. This data structure is the type of parameter that is called back to the user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCLocalAudioStats\* |[audioStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalStreamStats-audiostats) |
|ByteRTCLocalVideoStats\* |[videoStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalStreamStats-videostats) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalStreamStats-isscreen) |
|ByteRTCNetworkQuality |[deprecated] [txQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalStreamStats-txquality) |
|ByteRTCNetworkQuality |[deprecated] [rxQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalStreamStats-rxquality) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLocalStreamStats-audiostats"></span>
### audioStats

```objectivec
@property(strong, nonatomic) ByteRTCLocalAudioStats *_Nonnull audioStats;
```


For statistics on audio streams sent by local devices. See [ByteRTCLocalAudioStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioStats)

<span id="ByteRTCLocalStreamStats-videostats"></span>
### videoStats

```objectivec
@property(strong, nonatomic) ByteRTCLocalVideoStats *_Nonnull videoStats;
```


For statistics on video streams sent by local devices. See [ByteRTCLocalVideoStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalVideoStats)

<span id="ByteRTCLocalStreamStats-isscreen"></span>
### isScreen

```objectivec
@property(nonatomic, assign) BOOL isScreen;
```


Reserved field. Ignore the value returned in this field.

<span id="ByteRTCLocalStreamStats-txquality"></span>
### txQuality

```objectivec
@property(assign, nonatomic) ByteRTCNetworkQuality txQuality;
```


> Deprecated since 3.45 and will be deleted in 3.51, use [rtcRoom:onNetworkQuality:remoteQualities:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onnetworkquality-remotequalities) instead


For the uplink network quality of the media stream of the user you belong to. See [ByteRTCNetworkQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQuality)

<span id="ByteRTCLocalStreamStats-rxquality"></span>
### rxQuality

```objectivec
@property(assign, nonatomic) ByteRTCNetworkQuality rxQuality;
```


> Deprecated since 3.45 and will be deleted in 3.51, use [rtcRoom:onNetworkQuality:remoteQualities:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onnetworkquality-remotequalities) instead


The downlink network quality of the media stream belongs to the user. See [ByteRTCNetworkQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQuality)

<span id="ByteRTCVideoRotation"></span>
# ByteRTCVideoRotation

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoRotation
)
```


Video frame rotation

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoRotation0 |0 |Not to rotate. |
|ByteRTCVideoRotation90 |90 |Rotate 90 degrees clockwise. |
|ByteRTCVideoRotation180 |180 |Rotate 180 degrees clockwise. |
|ByteRTCVideoRotation270 |270 |Rotate 270 degrees clockwise. |


<span id="ByteRTCDataFrameType"></span>
# ByteRTCDataFrameType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCDataFrameType
)
```


Data type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCDataFrameTypeSei |0 |SEI data |
|ByteRTCDataFrameTypeRoi |1 |Facial recognition data |
|ByteRTCDataFrameTypeOther |2 |Other data frame type |


<span id="ByteRTCMouseCursorCaptureState"></span>
# ByteRTCMouseCursorCaptureState

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCMouseCursorCaptureState
)
```


Whether to capture the mouse cursor when capturing screen streams by RTC.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMouseCursorCaptureStateOn |0 |Yes. |
|ByteRTCMouseCursorCaptureStateOff |1 |No. |


<span id="ByteRTCSubscribeFallbackOption"></span>
# ByteRTCSubscribeFallbackOption

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCSubscribeFallbackOption
)
```


Stream fallback options of subscriber

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSubscribeFallbackOptionDisabled |0 |Default setting. No fallback is allowed under limited network conditions. |
|ByteRTCSubscribeFallbackOptionVideoStreamLow |1 |The resolution of currently subscribed video stream will be reduced under limited network conditions, see [Stream Fallback](https://docs.byteplus.com/en/docs/12/docs-70137) for details.<br><br>&nbsp;<br><br>You can only select this setting after the stream publisher calls `enableSimulcastMode:` to enable the mode of publishing multiple streams, otherwise no fallback will occur. |
|ByteRTCSubscribeFallbackOptionAudioOnly |2 |The resolution of currently subscribed video stream will be reduced first under limited network conditions. When the network condition is not sufficient to receive the minimum resolution stream, the video is automatically cancelled and only the audio is received.<br><br>&nbsp;<br><br>You can only select this setting after the stream publisher calls `enableSimulcastMode:` to enable the mode of publishing multiple streams, otherwise no fallback will occur. |


<span id="ByteRTCAudioSourceType"></span>
# ByteRTCAudioSourceType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioSourceType
)
```


Audio input source type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioSourceTypeExternal |0 |Custom Capture Audio Source |
|ByteRTCAudioSourceTypeInternal |1 |RTC SDK internal acquisition audio source |


<span id="ByteRTCRemoteStreamKey"></span>
# ByteRTCRemoteStreamKey

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteStreamKey : NSObject
```


Information about the remote stream

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[userId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamKey-userid) |
|NSString\* |[roomId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamKey-roomid) |
|ByteRTCStreamIndex |[streamIndex](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamKey-streamindex) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteStreamKey-userid"></span>
### userId

```objectivec
@property(nonatomic, copy, nullable) NSString *userId;
```


The ID of the user who published the stream.

<span id="ByteRTCRemoteStreamKey-roomid"></span>
### roomId

```objectivec
@property(nonatomic, copy, nullable) NSString *roomId;
```


The ID of the room from which the stream was published.

<span id="ByteRTCRemoteStreamKey-streamindex"></span>
### streamIndex

```objectivec
@property(nonatomic, assign) ByteRTCStreamIndex streamIndex;
```


Reserved field.

<span id="ByteRTCPlayerState"></span>
# ByteRTCPlayerState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCPlayerState
)
```


Player state.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCPlayerStateIdle |0 |Not started. |
|ByteRTCPlayerStatePreloaded |1 |Preloaded. |
|ByteRTCPlayerStateOpened |2 |Opened. |
|ByteRTCPlayerStatePlaying |3 |Playing. |
|ByteRTCPlayerStatePaused |4 |Paused. |
|ByteRTCPlayerStateStopped |5 |Playback is stopped. |
|ByteRTCPlayerStateFailed |6 |Failed. |
|ByteRTCPlayerStateFinished |7 |Playback ended. |
|ByteRTCPlayerStateLoopFinished |8 |Loop playback has finished. |


<span id="ByteRTCMediaPlayerConfig"></span>
# ByteRTCMediaPlayerConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMediaPlayerConfig : NSObject
```


Mixing configuration

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCAudioMixingType |[type](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerConfig-type) |
|NSInteger |[playCount](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerConfig-playcount) |
|NSInteger |[startPos](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerConfig-startpos) |
|NSInteger |[callbackOnProgressInterval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerConfig-callbackonprogressinterval) |
|BOOL |[syncProgressToRecordFrame](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerConfig-syncprogresstorecordframe) |
|BOOL |[autoPlay](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMediaPlayerConfig-autoplay) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMediaPlayerConfig-type"></span>
### type

```objectivec
@property(assign, nonatomic) ByteRTCAudioMixingType type;
```


For mixing playback types. See [ByteRTCAudioMixingType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioMixingType)

<span id="ByteRTCMediaPlayerConfig-playcount"></span>
### playCount

```objectivec
@property(assign, nonatomic) NSInteger playCount;
```


Mix playback times


* Play_count < = 0: Infinite loop

* Play_count == 1: Play once (default)

* Play_count \> 1: Play play_count times

    &nbsp;


<span id="startpos"></span>
### startPos

```objectivec
@property(assign, nonatomic) NSInteger startPos;
```


The starting position in ms. 0 by default.

<span id="ByteRTCMediaPlayerConfig-callbackonprogressinterval"></span>
### callbackOnProgressInterval

```objectivec
@property(assign, nonatomic) NSInteger callbackOnProgressInterval;
```


Set the interval of the periodic callback [onMediaPlayerPlayingProgress:progress:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCMediaPlayerEventHandler-onmediaplayerplayingprogress-progress) during audio mixing in ms.


* interval \> 0: The callback is enabled. The actual interval is a multiple of 10. If the input value is not divisible by 10, it will be automatically rounded up. For example, if 52 is entered, the actual interval is 60 ms.

* interval <= 0: The callback is disabled.

    &nbsp;


<span id="syncprogresstorecordframe"></span>
### syncProgressToRecordFrame

```objectivec
@property(assign, nonatomic) BOOL syncProgressToRecordFrame;
```


Attach the process information of local audio file mixing to the captured audio data. Enable the function to enhance the synchronicity of the remote audio mixing.


* The function is effective when mixing a single audio file.

* Use `true` for enabling the function and `false` for disabling the function. The default is `false`.

    &nbsp;


<span id="autoplay"></span>
### autoPlay

```objectivec
@property(assign, nonatomic) BOOL autoPlay;
```


Play the audio automatically. If not, call [start](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCMediaPlayer-start) to play the audio. True by default.

<span id="ByteRTCVideoRotationMode"></span>
# ByteRTCVideoRotationMode

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCVideoRotationMode
)
```


Video orientation

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoRotationModeFollowApp |0 |The orientation of the App |
|ByteRTCVideoRotationModeFollowGSensor |1 |Gravity |


<span id="ByteRTCForwardStreamEvent"></span>
# ByteRTCForwardStreamEvent

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCForwardStreamEvent
)
```


Events during the relaying

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCForwardStreamEventDisconnected |0 |Relaying pauses for the reason of network disconnecting. |
|ByteRTCForwardStreamEventConnected |1 |Relaying recovers from the disconnecting. |
|ByteRTCForwardStreamEventInterrupt |2 |Relaying aborts because a user with the same user ID as that of the publisher joins. |
|ByteRTCForwardStreamEventDstRoomUpdated |3 |Designated room list updates after you call `updateForwardStreamToRooms`. |
|ByteRTCForwardStreamEventUnExpectAPICall |4 |Wrong API\-calling order. For example, call `updateForwardStreamToRooms` before calling `startForwardStreamToRooms`. |


<span id="ByteRTCVideoFrameType"></span>
# ByteRTCVideoFrameType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoFrameType
)
```


Video frame type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoFrameTypeRawMemory |0 |Video frame type: memory data |
|ByteRTCVideoFrameTypePixelBuffer |1 |Video frame type: CVPixelBuffer |


<span id="ByteRTCVideoFrame"></span>
# ByteRTCVideoFrame

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCVideoFrame <NSObject>
```


video frame interface

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCVideoBufferType |[bufferType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-buffertype) |
|ByteRTCVideoPixelFormat |[pixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-pixelformat) |
|ByteRTCVideoContentType |[contentType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-contenttype) |
|CMTime |[timestamp](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-timestamp) |
|int |[width](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-width) |
|int |[height](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-height) |
|CVPixelBufferRef |[cvpixelbuffer](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-cvpixelbuffer) |
|ByteRTCVideoRotation |[rotation](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-rotation) |
|ByteRTCCameraID |[cameraId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-cameraid) |
|NSData\* |[seiData](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-seidata) |
|int |[numberOfPlanes](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-numberofplanes) |
|void\*\* |[planeDataArray](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-planedataarray) |
|int\* |[planeStrideArray](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-planestridearray) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[addRef](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-addref) |
|long |[releaseRef](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoFrame-releaseref) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoFrame-buffertype"></span>
### bufferType

```objectivec
@property(readonly) ByteRTCVideoBufferType bufferType;
```


Gets video frame buffer type, see [ByteRTCVideoBufferType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoBufferType).

<span id="ByteRTCVideoFrame-pixelformat"></span>
### pixelFormat

```objectivec
@property(readonly) ByteRTCVideoPixelFormat pixelFormat;
```


Gets video frame format, see [ByteRTCVideoPixelFormat](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoPixelFormat)

<span id="ByteRTCVideoFrame-contenttype"></span>
### contentType

```objectivec
@property(readonly) ByteRTCVideoContentType contentType;
```


Gets video content type, see [ByteRTCVideoContentType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCVideoContentType).

<span id="ByteRTCVideoFrame-timestamp"></span>
### timestamp

```objectivec
@property(readonly) CMTime timestamp;
```


Gets video frame timestamp

<span id="ByteRTCVideoFrame-width"></span>
### width

```objectivec
@property(readonly) int width;
```


Gets video frame width

<span id="ByteRTCVideoFrame-height"></span>
### height

```objectivec
@property(readonly) int height;
```


Gets video frame height

<span id="ByteRTCVideoFrame-cvpixelbuffer"></span>
### cvpixelbuffer

```objectivec
@property(readonly) CVPixelBufferRef _Nullable cvpixelbuffer;
```


Gets data of `CVPixelBufferRef` type, valid when format is `kPixelFormatCVPixelBuffer`

<span id="ByteRTCVideoFrame-rotation"></span>
### rotation

```objectivec
@property(readonly) ByteRTCVideoRotation rotation;
```


Gets video frame rotation angle

<span id="ByteRTCVideoFrame-cameraid"></span>
### cameraId

```objectivec
@property(readonly) ByteRTCCameraID cameraId;
```


Gets camera position info of the video frame, see [ByteRTCCameraID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCCameraID)

<span id="ByteRTCVideoFrame-seidata"></span>
### seiData

```objectivec
@property(readonly) NSData * _Nullable seiData;
```


Gets SEI data

<span id="ByteRTCVideoFrame-numberofplanes"></span>
### numberOfPlanes

```objectivec
@property (readonly) int numberOfPlanes;
```


Gets the number of video frame planes

<span id="ByteRTCVideoFrame-planedataarray"></span>
### planeDataArray

```objectivec
@property (readonly) void ** _Nullable planeDataArray;
```


Gets array of video frame planes

<span id="ByteRTCVideoFrame-planestridearray"></span>
### planeStrideArray

```objectivec
@property (readonly) int * _Nullable planeStrideArray;
```


Gets an array of strides. Stride is the length of memory between two lines of image data in a video frame plane in bytes.

<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoFrame-addref"></span>
### addRef

```objectivec
- (void)addRef;
```


Increase the reference count of the video frame by 1.

**Notes**

If you want to asynchronously process the video frame (for example, switch the thread for rendering), you need to call this interface to increase the reference count. After the asynchronous processing is completed, you need to call `releaseRef` to reduce the reference count by 1.

<span id="ByteRTCVideoFrame-releaseref"></span>
### releaseRef

```objectivec
- (long)releaseRef;
```


Decrease the reference count of the video frame by 1.

**Notes**

When the reference count of a video frame is decreased to 0, the video frame object is released. After the video frame is released, it should not be used anymore.

<span id="ByteRTCWTNSubscribeStateChangeReason"></span>
# ByteRTCWTNSubscribeStateChangeReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCWTNSubscribeStateChangeReason
)
```


Reasons for change in WTN media stream's Subscription Status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCWTNSubscribeStateChangeReasonSubscribe |0 |Subscribe WTN media stream successfully |
|ByteRTCWTNSubscribeStateChangeReasonUnsubscribe |1300 |Failed to subscribe WTN media stream for other reasons. |
|ByteRTCWTNSubscribeStateChangeReasonRemotePublish |1301 |Failed to subscribe because the remote end did not publish. |
|ByteRTCWTNSubscribeStateChangeReasonOverClientSubscribeStreamLimit |1310 |Failed to subscribe because the single\-end subscription limit has been exceeded. An engine instance can pull a maximum of 5 streams. |
|ByteRTCWTNSubscribeStateChangeReasonOverStreamSubscribeUserLimit |1311 |Failed to subscribe because the single\-stream subscription limit has been exceeded. The limit is set by RTC server. |
|ByteRTCWTNSubscribeStateChangeReasonOverStreamSubscribeRequestLimit |1312 |Failed to subscribe because the limit of the single\-stream subscription request has been exceeded. The limit is set by RTC server. |


<span id="ByteRTCLocalAudioPropertiesInfo"></span>
# ByteRTCLocalAudioPropertiesInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCLocalAudioPropertiesInfo : NSObject
```


Local audio properties

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCAudioPropertiesInfo\* |[audioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCLocalAudioPropertiesInfo-audiopropertiesinfo) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLocalAudioPropertiesInfo-audiopropertiesinfo"></span>
### audioPropertiesInfo

```objectivec
@property(strong, nonatomic) ByteRTCAudioPropertiesInfo *_Nonnull audioPropertiesInfo;
```


See [ByteRTCAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesInfo)

<span id="ByteRTCVideoSinkMirrorType"></span>
# ByteRTCVideoSinkMirrorType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoSinkMirrorType
)
```


Whether the video frame needs to be mirrored.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoSinkMirrorTypeOn |1 |Enable mirroring effect. |
|ByteRTCVideoSinkMirrorTypeOff |2 |(Default) Disable mirroring effect. |


<span id="ByteRTCCameraID"></span>
# ByteRTCCameraID

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCCameraID
)
```


Camera type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCCameraIDFront |0 |Front\-facing camera |
|ByteRTCCameraIDBack |1 |Back\-facing camera |
|ByteRTCCameraIDInvalid |3 |Invalid value |


<span id="ByteRTCCloudProxyInfo"></span>
# ByteRTCCloudProxyInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCCloudProxyInfo: NSObject
```


Cloud Proxy Information

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[cloudProxyIp](https://docs.byteplus.com/en/docs/12/14181#ByteRTCCloudProxyInfo-cloudproxyip) |
|int |[cloudProxyPort](https://docs.byteplus.com/en/docs/12/14181#ByteRTCCloudProxyInfo-cloudproxyport) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCCloudProxyInfo-cloudproxyip"></span>
### cloudProxyIp

```objectivec
@property(strong, nonatomic) NSString* _Nonnull cloudProxyIp;
```


Cloud proxy IP

<span id="ByteRTCCloudProxyInfo-cloudproxyport"></span>
### cloudProxyPort

```objectivec
@property(assign, nonatomic) int cloudProxyPort;
```


Cloud proxy Port

<span id="ByteRTCMixedStreamAudioConfig"></span>
# ByteRTCMixedStreamAudioConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamAudioConfig : NSObject
```


Audio transcoding configurations.

With invalid or empty input, the configurations will be set as the default values.

These parameters cannot be updated during the task.

This parameter is not supported for WTN stream tasks.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|ByteRTCMixedStreamAudioCodecType |[audioCodec](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioConfig-audiocodec) |
|NSInteger |[sampleRate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioConfig-samplerate) |
|NSInteger |[channels](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioConfig-channels) |
|NSInteger |[bitrate](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioConfig-bitrate) |
|ByteRTCMixedStreamAudioProfile |[audioProfile](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioConfig-audioprofile) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamAudioConfig-audiocodec"></span>
### audioCodec

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamAudioCodecType audioCodec;
```


The audio codec.

<span id="ByteRTCMixedStreamAudioConfig-samplerate"></span>
### sampleRate

```objectivec
@property(assign, nonatomic) NSInteger sampleRate;
```


The sample rate (Hz). Supported sample rates: 32,000 Hz, 44,100 Hz, 48,000 Hz. Defaults to 48,000 Hz. It's recommended to be set.

<span id="ByteRTCMixedStreamAudioConfig-channels"></span>
### channels

```objectivec
@property(assign, nonatomic) NSInteger channels;
```


The number of channels. Supported channels: 1 (single channel), 2 (dual channel). Defaults to 2. It's recommended to be set.

<span id="ByteRTCMixedStreamAudioConfig-bitrate"></span>
### bitrate

```objectivec
@property(assign, nonatomic) NSInteger bitrate;
```


The bitrate (Kbps) in the range of [32, 192]. Defaults to 64 Kbps. It's recommended to be set.

<span id="ByteRTCMixedStreamAudioConfig-audioprofile"></span>
### audioProfile

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamAudioProfile audioProfile;
```


AAC profile. See [ByteRTCMixedStreamAudioProfile](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamAudioProfile). Defaults to `0`. It's recommended to be set.

<span id="ByteRTCVideoBufferType"></span>
# ByteRTCVideoBufferType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoBufferType
)
```


Video buffer type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoBufferTypeRawMemory |0 |raw memory |
|ByteRTCVideoBufferTypeCVPixelBuffer |1 |CVPixelBufferRef |
|ByteRTCVideoBufferTypeGLTexture |2 |OpenGL texture |
|ByteRTCVideoBufferTypeCuda |3 |Cuda data format |
|ByteRTCVideoBufferTypeD3D11 |4 |Direct3D11 texture |
|ByteRTCVideoBufferTypeVAAPI |5 |Vaapi data format |
|ByteRTCVideoBufferTypeNvidiaJetsonDma |6 |nvidia jetson dma |


<span id="ByteRTCSubscribeState"></span>
# ByteRTCSubscribeState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSubscribeState
)
```


Stream subscription state

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSubscribeStateSubscribe |0 |Successfully subscribed. |
|ByteRTCSubscribeStateUnsubscribe |1 |Failed to subscribe. |


<span id="ByteRTCMixedStreamTaskInfo"></span>
# ByteRTCMixedStreamTaskInfo

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamTaskInfo : NSObject
```


Detailed information of the stream mixing task.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[taskId](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamTaskInfo-taskid) |
|ByteRTCMixedStreamPushTargetType |[pushTargetType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamTaskInfo-pushtargettype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamTaskInfo-taskid"></span>
### taskId

```objectivec
@property(nonatomic, copy) NSString * _Nonnull taskId;
```


Task ID

For WTN stream task, this value represents the WTN stream ID. You can subscribe to a WTN stream by specifying the ID.

<span id="ByteRTCMixedStreamTaskInfo-pushtargettype"></span>
### pushTargetType

```objectivec
@property(nonatomic, assign) ByteRTCMixedStreamPushTargetType pushTargetType;
```


Task type: Pushing a mixing stream to CDN or starting a WTN stream.

<span id="ByteRTCVideoEncoderPreference"></span>
# ByteRTCVideoEncoderPreference

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCVideoEncoderPreference
)
```


Encoder preference.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCVideoEncoderPreferenceDisabled |0 |No preference. The frame rate and the resolution will not be adjusted. |
|ByteRTCVideoEncoderPreferenceMaintainFramerate |1 |The high frame rate mode. Ensure the highest framerate possible. This mode is designed for videos with high\-motion contents. |
|ByteRTCVideoEncoderPreferenceMaintainQuality |2 |The high\-resolution mode. Ensure the highest resolution possible. This mode is designed for videos with static contents. |
|ByteRTCVideoEncoderPreferenceAuto |3 |Balancing resolution and frame rate.<br><br>For the screen\-recordings, indicates No preference. The frame rate and the resolution will not be adjusted. |


<span id="ByteRTCAudioMixingState"></span>
# ByteRTCAudioMixingState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioMixingState
)
```


Audio mix file playback status.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioMixingStatePreloaded |0 |Mix loaded |
|ByteRTCAudioMixingStatePlaying |1 |Mix is playing |
|ByteRTCAudioMixingStatePaused |2 |Mix Pause |
|ByteRTCAudioMixingStateStopped |3 |Mixing stopped |
|ByteRTCAudioMixingStateFailed |4 |Mix playback failed |
|ByteRTCAudioMixingStateFinished |5 |End of mixing |
|ByteRTCAudioMixingStatePCMEnabled |6 |PCM mixing enabled |
|ByteRTCAudioMixingStatePCMDisabled |7 |PCM mixing disabled |


<span id="ByteRTCMixedStreamAudioCodecType"></span>
# ByteRTCMixedStreamAudioCodecType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMixedStreamAudioCodecType
)
```


The audio codec.(New)

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamAudioCodecTypeAAC |0 |AAC format. |


<span id="ByteRTCRemoteStreamStats"></span>
# ByteRTCRemoteStreamStats

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCRemoteStreamStats : NSObject
```


The remote audio/video stream statistics and network status subscribed by the user, with a reference period of 2s.

After the remote user subscribed to successfully publish the audio/video stream, the SDK will periodically notify the remote user of the reception status of the subscribed audio/video stream during this reference period through `onRemoteStreamStats`

. This data structure is the type of parameter that is called back to the local user.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[uid](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamStats-uid) |
|ByteRTCRemoteAudioStats\* |[audioStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamStats-audiostats) |
|ByteRTCRemoteVideoStats\* |[videoStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamStats-videostats) |
|BOOL |[isScreen](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamStats-isscreen) |
|ByteRTCNetworkQuality |[deprecated] [rxQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteStreamStats-rxquality) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteStreamStats-uid"></span>
### uid

```objectivec
@property(copy, nonatomic) NSString *_Nonnull uid;
```


User ID. The user ID of the audio source.

<span id="ByteRTCRemoteStreamStats-audiostats"></span>
### audioStats

```objectivec
@property(strong, nonatomic) ByteRTCRemoteAudioStats *_Nonnull audioStats;
```


For statistics on remote audio streams. See [ByteRTCRemoteAudioStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteAudioStats)

<span id="ByteRTCRemoteStreamStats-videostats"></span>
### videoStats

```objectivec
@property(strong, nonatomic) ByteRTCRemoteVideoStats *_Nonnull videoStats;
```


For statistics on remote video streams. See [ByteRTCRemoteVideoStats](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStats)

<span id="ByteRTCRemoteStreamStats-isscreen"></span>
### isScreen

```objectivec
@property(nonatomic, assign) BOOL isScreen;
```


Reserved field. Ignore the value returned in this field.

<span id="ByteRTCRemoteStreamStats-rxquality"></span>
### rxQuality

```objectivec
@property(assign, nonatomic) ByteRTCNetworkQuality rxQuality;
```


> Deprecated since 3.45 and will be deleted in 3.51, use [rtcRoom:onNetworkQuality:remoteQualities:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onnetworkquality-remotequalities) instead


The downlink network quality of the media stream belongs to the user. See [ByteRTCNetworkQuality](https://docs.byteplus.com/en/docs/12/14181#ByteRTCNetworkQuality)

<span id="ByteRTCHighlightConfig"></span>
# ByteRTCHighlightConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCHighlightConfig: NSObject
```


Configure how a border is highlighted when you share your screen.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enableHighlight](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHighlightConfig-enablehighlight) |
|uint32_t |[borderColor](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHighlightConfig-bordercolor) |
|int |[borderWidth](https://docs.byteplus.com/en/docs/12/14181#ByteRTCHighlightConfig-borderwidth) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCHighlightConfig-enablehighlight"></span>
### enableHighlight

```objectivec
@property (assign, nonatomic) BOOL enableHighlight;
```


Whether to display a highlighted border. A border is highlighted by default.

<span id="ByteRTCHighlightConfig-bordercolor"></span>
### borderColor

```objectivec
@property (assign, nonatomic) uint32_t borderColor;
```


Color(ARGB format: 0xAARRGGBB).

<span id="ByteRTCHighlightConfig-borderwidth"></span>
### borderWidth

```objectivec
@property (assign, nonatomic) int borderWidth;
```


Width(in pixel).

<span id="ByteRTCAudioCodecType"></span>
# ByteRTCAudioCodecType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioCodecType
)
```


Audio codec type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioCodecTypeNone |0 |Unknown encoding type |
|ByteRTCAudioCodecTypeOpus |1 |Opus encoding type |


<span id="ByteRTCRemoteVideoState"></span>
# ByteRTCRemoteVideoState

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRemoteVideoState
)
```


Remote video stream status

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRemoteVideoStateStopped |0 |The default initial state of the remote video stream, callback the state at the following times:<br><br><br>&nbsp;<br><br>* The local user stops receiving the remote video stream, corresponding to the error code [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) ByteRTCRemoteVideoStateChangeReasonLocalMuted<br><br>* The remote user stops sending the video stream, corresponding to the error code ByteRTCRemoteVideoStateChangeReasonRemoteMuted<br><br>* The remote user leaves the room, corresponding to Error code [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) in ByteRTCRemoteVideoStateChangeReasonRemoteOffline |
|ByteRTCRemoteVideoStateStarting |1 |Local users have received the remote video header package<br><br>&nbsp;<br><br>Callback this state when the remote video header package is received, corresponding to the error code [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) ByteRTCRemoteVideoStateChangeReasonLocalUnmuted |
|ByteRTCRemoteVideoStateDecoding |2 |The remote video stream is decoding and playing normally, callback the status at the following times:<br><br><br>&nbsp;<br><br>* [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) ByteRTCRemoteVideoStateChangeReasonLocalUnmuted<br><br>* The network returned to normal from blocking, corresponding to the error code ByteRTCRemoteVideoStateChangeReasonNetworkRecovery<br><br>* The local user recovers the received remote video Stream, corresponding to the error code [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) ByteRTCRemoteVideoStateChangeReasonLocalUnmuted<br><br>* The remote user resumes sending the video stream, corresponding to the error code in [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) |
|ByteRTCRemoteVideoStateFrozen |3 |Remote video stream freezing<br><br>&nbsp;<br><br>Network blocking, packet loss rate and other reasons will report the status of the video card stream, corresponding to the error code [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) ByteRTCRemoteVideoStateChangeReasonNetworkCongestion |
|ByteRTCRemoteVideoStateFailed |4 |The remote video stream failed to play<br><br>&nbsp;<br><br>If the internal processing of the remote video stream fails, the method will be called back, corresponding to the error code [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/14181#ByteRTCRemoteVideoStateChangeReason) ByteRTCRemoteVideoStateChangeReasonInternal |


<span id="ByteRTCMediaDeviceError"></span>
# ByteRTCMediaDeviceError

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMediaDeviceError
)
```


Media device error

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaDeviceErrorOK |0 |Normal |
|ByteRTCMediaDeviceErrorDeviceNoPermission |1 |No permission |
|ByteRTCMediaDeviceErrorDeviceBusy |2 |Occupied by the other application |
|ByteRTCMediaDeviceErrorDeviceFailure |3 |Error |
|ByteRTCMediaDeviceErrorDeviceNotFound |4 |Not found |
|ByteRTCMediaDeviceErrorDeviceDisconnected |5 |Disconnected |
|ByteRTCMediaDeviceErrorDeviceNoCallback |6 |No data callback from the capture devices.<br><br>&nbsp;<br><br>RTC emits this error when the media device is expected to be working but no data is received. |
|ByteRTCMediaDeviceErrorUNSupportFormat |7 |Not supported sample rate |
|ByteRTCMediaDeviceErrorAudioServerNeedRestart |13 |The system service has an error or does not respond for a long time. It is recommended to restart the audio service process or restart the device. |


<span id="ByteRTCMixedStreamSEIContentMode"></span>
# ByteRTCMixedStreamSEIContentMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMixedStreamSEIContentMode
)
```


Content of SEI sent while pushing mixed stream to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamSEIContentModeDefault |0 |The video stream contains all the SEI information. Default value. |
|ByteRTCMixedStreamSEIContentModeEnableVolumeIndication |1 |The SEI data transmitted with non\-key frames contains volume information only.<br><br>&nbsp;<br><br>This parameter only takes effect after you set `ByteRTCMixedStreamControlConfig.enableVolumeIndication` to "True". |


<span id="ByteRTCAudioPropertiesMode"></span>
# ByteRTCAudioPropertiesMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioPropertiesMode
)
```


The audio info included in [rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCEngineDelegate-rtcengine-onlocalaudiopropertiesreport).

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioPropertiesModeMicrohone |0 |Only locally captured microphone audio info and locally captured screen audio info are included. |
|ByteRTCAudioPropertiesModeAudioMixing |1 |The following information is included:<br><br><br>&nbsp;<br><br>* Locally captured microphone audio info and locally captured screen audio info;<br><br>* Locally audio mixing info. |


<span id="ByteRTCAudioDeviceType"></span>
# ByteRTCAudioDeviceType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioDeviceType
)
```


Type of audio device

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioDeviceTypeUnknown |\-1 |Unknown device |
|ByteRTCAudioDeviceTypeRenderDevice |0 |Screen audio recorder |
|ByteRTCAudioDeviceTypeCaptureDevice |1 |Microphone |
|ByteRTCAudioDeviceTypeScreenCaptureDevice |2 |Screen audio recorder |


<span id="ByteRTCMediaPlayerCustomSourceStreamType"></span>
# ByteRTCMediaPlayerCustomSourceStreamType

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMediaPlayerCustomSourceStreamType
)
```


Custom audio source stream type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMediaPlayerCustomSourceStreamTypeRaw |0 |When you use the local PCM data, use this type. |
|ByteRTCMediaPlayerCustomSourceStreamTypeEncoded |1 |When you use the audio data from local memory, use this type. |


<span id="ByteRTCAudioPropertiesConfig"></span>
# ByteRTCAudioPropertiesConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCAudioPropertiesConfig : NSObject
```


Configuration related to audio attribute information prompt.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[interval](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesConfig-interval) |
|BOOL |[enableSpectrum](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesConfig-enablespectrum) |
|BOOL |[enableVad](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesConfig-enablevad) |
|ByteRTCAudioReportMode |[localMainReportMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesConfig-localmainreportmode) |
|float |[smooth](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesConfig-smooth) |
|ByteRTCAudioPropertiesMode |[audioReportMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesConfig-audioreportmode) |
|BOOL |[enableVoicePitch](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesConfig-enablevoicepitch) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioPropertiesConfig-interval"></span>
### interval

```objectivec
@property(assign, nonatomic) NSInteger interval;
```


Prompt interval in ms


* `<= 0`: Turn off prompt

* `(0,100]`: Invalid interval value, and will be automatically reset to 100ms.

* `> 100`: the actual value of interval

    &nbsp;


<span id="enablespectrum"></span>
### enableSpectrum

```objectivec
@property(assign, nonatomic) BOOL enableSpectrum;
```


Whether to enable audio spectrum detection.

<span id="ByteRTCAudioPropertiesConfig-enablevad"></span>
### enableVad

```objectivec
@property(assign, nonatomic) BOOL enableVad;
```


Whether to enable Voice Activity Detection.

<span id="ByteRTCAudioPropertiesConfig-localmainreportmode"></span>
### localMainReportMode

```objectivec
@property(assign, nonatomic) ByteRTCAudioReportMode localMainReportMode;
```


The volume callback modes. See [ByteRTCAudioReportMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioReportMode).

<span id="ByteRTCAudioPropertiesConfig-smooth"></span>
### smooth

```objectivec
@property(nonatomic, assign) float smooth;
```


The smoothing coefficient for audio attribute information prompt. The range is `(0.0, 1.0]`.

The default value is `1.0`, which means the smoothing effect is off by default. The smaller the value, the smoother the audio volume prompt. If you want to enable the smooth effect, the recommended value is `0.3`.

<span id="ByteRTCAudioPropertiesConfig-audioreportmode"></span>
### audioReportMode

```objectivec
@property(assign, nonatomic) ByteRTCAudioPropertiesMode audioReportMode;
```


The audio info included in [rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCEngineDelegate-rtcengine-onlocalaudiopropertiesreport). See [ByteRTCAudioPropertiesMode](https://docs.byteplus.com/en/docs/12/14181#ByteRTCAudioPropertiesMode).

Locally captured microphone audio info and locally captured screen audio info are included by default.

<span id="ByteRTCAudioPropertiesConfig-enablevoicepitch"></span>
### enableVoicePitch

```objectivec
@property(assign, nonatomic) BOOL enableVoicePitch;
```


Sets whether to return the vocal pitch of the local user.

<span id="ByteRTCMixedStreamPushTargetConfig"></span>
# ByteRTCMixedStreamPushTargetConfig

```objectivec
BYTERTC_APPLE_EXPORT @interface ByteRTCMixedStreamPushTargetConfig : NSObject
```


Configurations for the mixing streams.

If not specified, the parameter can be used for both WTN stream and mixing\-stream tasks.

If not specified, the parameter can be passed when starting a task or during a task.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[pushCDNURL](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamPushTargetConfig-pushcdnurl) |
|NSString\* |[pushWTNStreamID](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamPushTargetConfig-pushwtnstreamid) |
|ByteRTCMixedStreamPushTargetType |[pushTargetType](https://docs.byteplus.com/en/docs/12/14181#ByteRTCMixedStreamPushTargetConfig-pushtargettype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMixedStreamPushTargetConfig-pushcdnurl"></span>
### pushCDNURL

```objectivec
@property(copy, nonatomic) NSString * _Nullable pushCDNURL;
```


The URL for the mixed stream to be pushed to. Only supports live transcoding via RTMP. The URL should match the regular expression `/^rtmps?:\\/\\//`. It's recommended to be set.

This parameter cannot be updated while pushing stream to the CDN.

This parameter is not supported for WTN stream tasks.

<span id="ByteRTCMixedStreamPushTargetConfig-pushwtnstreamid"></span>
### pushWTNStreamID

```objectivec
@property(copy, nonatomic) NSString * _Nullable pushWTNStreamID;
```


The WTN stream ID.

This parameter is not supported for mixing\-stream stream tasks.

<span id="ByteRTCMixedStreamPushTargetConfig-pushtargettype"></span>
### pushTargetType

```objectivec
@property(assign, nonatomic) ByteRTCMixedStreamPushTargetType pushTargetType;
```


The task type.
