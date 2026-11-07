---
title: "Native Client SDK"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-79882"
---

You can obtain the latest version of the SDK in [Download SDK](https://docs.byteplus.com/docs/byteplus-rtc/docs-75707#download-sdk).

## Upgrade Notes

If you need to upgrade the old version of the RTC SDK used in your application to the latest version, refer to the [SDK Upgrade Guides](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-changelogs) for each platform.

## 3.60.108

This version was released on November 02, 2026. This update includes the following client platforms: Android and iOS.

### Fixed

Fixed known issues.

## 3.60.1 (Electron)

Electron RTC SDK 3.60.1 was released on October 9, 2026.

This version introduces a redesigned engine and stream model and contains breaking API changes. Before upgrading from 3.56.1, refer to the [Electron SDK Upgrade Guide](https://docs.byteplus.com/docs/byteplus-rtc/docs-519257).

### Feature Changes

* **Engine and stream model**

   * Renamed the core class from `RTCVideo` to `RTCEngine`. Use `createRTCEngine` and `destroyRTCEngine` to create and destroy the engine.

   * Added `streamId` as the unique identifier for audio and video streams. APIs and callbacks that previously identified streams by user ID, room ID, `StreamIndex`, or `RemoteStreamKey` now use `streamId` and `StreamInfo`.

   * Split stream publishing and subscription operations by media type. For example, use `publishStreamAudio` and `publishStreamVideo` instead of `publishStream`. Camera and screen streams now use the same APIs and are distinguished by `streamId`.

* **WTN streams**

   * Added the `RTCWTNStream` module. You can subscribe to WTN audio and video, render WTN video, configure a WTN video sink, and adjust WTN playback volume.

   * Replaced the former public\-stream APIs and callbacks with the WTN stream module and unified mixed\-stream APIs.

* **Push to CDN and stream mixing**

   * Added unified server\-side mixed\-stream APIs: `startPushMixedStream`, `updatePushMixedStream`, and `stopPushMixedStream`. Use `MixedStreamPushTargetType` to push the mixed stream to CDN or WTN.

   * Replaced the single\-stream push APIs with `startPushSingleStream` and `stopPushSingleStream`. A single stream can be pushed to CDN or an RTC room.

* **Custom capture and rendering**

   * Added external audio and video capture through `setAudioSourceType`, `pushExternalAudioFrame`, `setVideoSourceType`, and `pushExternalVideoFrame`.

   * Added configurable local and remote video sinks through `setLocalVideoSink` and `setRemoteVideoSink`.

   * Added Alpha\-channel video encoding through `enableAlphaChannelVideoEncode` and `disableAlphaChannelVideoEncode`.

* **Live streaming and SEI**

   * Added `setLiveMode` and `RoomLiveMode` for switching between co\-host and solo\-host live modes.

   * Added `sendLivePushSEIMessage` for sending Key\-Value SEI data in solo\-host live mode.

* **Video and snapshot enhancements**

   * Added `key_frame_interval_ms` to `VideoEncoderConfig`.

   * Added local and remote snapshot\-to\-file APIs.

   * Added low\-light video enhancement through `setLowLightAdjusted`.

* **Other enhancements**

   * Added independent audio and video auto\-publish settings and a custom `stream_id` to `RTCRoomConfig`.

   * Added `setStreamExtraInfo` and the `onRoomStreamExtraInfoUpdate` callback.

   * Added custom\-source playback to `RTCMediaPlayer`.

   * Binary room and user messages are now returned as `Buffer` objects.

   * Updated mixed\-stream layout and server\-control configurations. Applications that build these objects must update renamed fields and newly required fields before upgrading.

   * Updated several callback signatures and enum member names, including local\-frame, recording, face\-detection, beauty\-mode, and capture\-preference definitions.

## 3.60.107

This version was released on September 18, 2026. This upgrade includes the following client systems: Android, iOS, macOS, Windows, and Linux.

### Enhanced

Added two error codes for single\-stream push tasks on Android, iOS, macOS, Windows, and Linux:

|Error |Android |iOS and macOS |Windows and Linux |Description |
|---|---|---|---|---|
|Push to CDN failed |`ERROR_PUSH_TO_CDN` (1098) |`ByteRTCSingleStreamTaskErrorCodePushToCDN` (1098) |`kSingleStreamTaskErrorCodePushToCDN` (1098) |The SDK reports this error when it fails to push the single stream to CDN. |
|Task count exceeded the limit |`ERROR_TASK_COUNT_OVER_LIMIT` (1099) |`ByteRTCSingleStreamTaskErrorCodeTaskCountOverLimit` (1099) |`kSingleStreamTaskErrorCodeCountOverLimit` (1099) |The SDK reports this error when a host has more than 20 concurrent single\-stream push tasks. |

## 3.60.106

This version was released on August 18, 2026. This upgrade includes the following client systems: Android, iOS, macOS, Windows, and Linux.

### Fixed

Fixed known issues.

## 3.60.105

This version was released on July 14, 2026. This upgrade includes the following client systems: Android, iOS, macOS, Windows, and Linux.

### New

1. **Live Mode Switching:**  Added `setLiveMode` API on `IRTCRoom` (C++ example), enabling dynamic switching between co\-hosted live streaming and single\-host live streaming modes after joining a room. The new `RoomLiveMode` enum provides two modes: `kRoomLiveModeCoHost` for multi\-person or co\-hosted live scenarios, and `kRoomLiveModeSoloHost` for single\-host live scenarios. The live mode can also be pre\-configured via the new `live_mode` field in `RTCRoomConfig` when joining a room.

   > **说明**

   > `setRoomProfile` has been replaced by `setLiveMode`. The old API and the related enum values `kRoomProfileTypeLinkMic` / `kRoomProfileTypeLivePush` have been removed. Use the new `RoomLiveMode` enum with `setLiveMode` instead.

2. **Key\-Value SEI Data Transmission:**  The `sendLivePushSEIMessage` API is now publicly available for sending SEI data in Key\-Value (JSON) format through video frames. This API supports setting SEI key\-value pairs that persist across video frames with configurable repeat count, keyframe\-only transmission, and overwrite policies. To use this feature, set the room live mode to `kRoomLiveModeSoloHost` via `setLiveMode`.

3. **Video Encoding Key Frame Interval:**  `VideoEncoderConfig` (C++ example) now supports a `key_frame_interval_ms` field, allowing developers to set the key frame interval in milliseconds. The default value is `0`, which means the encoder determines the interval automatically.

## 3.60.104

This version was released on May 26, 2026. This upgrade includes the following client systems: Android, iOS, macOS, Windows, and Linux.

### New

|Interface |Notes |
|---|---|
|`setRoomProfile` |Sets the room profile before or after joining a room. By selecting different profiles, the SDK automatically optimizes strategies (such as bitrate and latency) to match specific business scenarios.<br><br><br>* **Link mic mode:**  Focuses on a high\-quality experience, using the same bitrate configuration as live streaming.<br><br>* **Live push mode:**  Suitable for standard broadcasting or live streaming scenarios. |
|`sendLivePushSEIMessage` |Supports sending SEI (Supplemental Enhancement Information) data in Key\-Value format through video frames. This feature is ideal for embedding custom business metadata directly into the video stream. |

### Enhanced

1. **Video Encoding Configuration Enhancement**

   Added a new field in the video encoding configuration class to set the key\-frame interval. This allows developers to customize the I\-frame (Key Frame) interval in milliseconds. The default value is 0, which means the interval is automatically managed by the SDK.

2. **Custom Video Preprocessing Scope Control**

   Optimized the registration mechanism for custom video preprocessing. By setting the action domain field (`actionDomain` or `action_domain`) in the video preprocessing configuration class, developers can precisely control the effective scope of custom preprocessing plugins:

   * **Preview and Encode**: Effects are applied to both the local preview and the transmitted video stream.

   * **Preview Only**: Effects are only visible in the local preview and do not affect the stream seen by remote audience members.

   * **Encode Only**: Effects are only applied to the outgoing video stream, while the local preview remains as the original capture.

## 3.60.103

This version was released on November 3, 2025. This upgrade includes the following client systems: Android, iOS, macOS, Windows, and Linux.

### Feature Changes

The core changes in this version are as follows. For detailed changes, please refer to the [SDK Upgrade Guides](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-changelogs) for each platform.

* **Core Classes and Stream Identifiers**

   * **Core class and API renaming**: The SDK's core base class has been renamed from `RTCVideo` to `RTCEngine`, and related event callbacks have also been changed accordingly.

   * **Unified stream identifier**: Introduced `streamId` as the unique identifier for audio and video streams, replacing the old stream management method that relied on multiple methods such as user ID or stream index (`streamIndex`). Related APIs have been adapted to this change.

* **Interface Splitting and Unification**

   * **Audio and video stream interface splitting and unification**: Stream operation APIs such as publishing and subscribing have been split by audio and video. For example, `publishStream` is replaced by `publishStreamVideo` and `publishStreamAudio`. At the same time, the logic of "enable/disable" or "subscribe/unsubscribe" operations is unified through Boolean parameters, making the interface behavior more intuitive.

   * **Unified screen sharing and mainstream APIs**: Deprecated screen sharing\-specific interfaces such as `publishScreen` and `subscribeScreen`. Screen sharing and camera audio and video streams share the same set of interfaces, distinguished by `StreamId`.

   * **Unified push to CDN and WTN (formerly public stream) interfaces**: The separate interfaces for mixed stream push to CDN and public stream (WTN) push have been merged. For example, using the unified `startPushMixedStream` interface, you can configure different push destinations through parameters.

* **New Functional Modules**

   * **New RTS (Real\-time Messaging) module**: The RTS\-related capabilities are separated into an independent `RTSRoom` module. If you only need to use the real\-time messaging function, you can create an `RTSRoom` instance separately to achieve functional decoupling and lightweight integration.

* **API Usability Optimization**

   Optimized the parameters and callbacks of some APIs, for example, replacing integer status codes with more explicit enumeration types. At the same time, to maintain the simplicity of the interface, some long\-deprecated old interfaces have been formally removed.

## 3.58

RTC SDK for the following platform was released on May 24, 2024. Platforms: Android, iOS, macOS, Windows, Electron.

### New Platform

RTC SDK for Linux 3.58 is released.

### New Features

1. Supports internal capture signal mute control (without changing the status of the local hardware). You can choose to mute or unmute the microphone capture without affecting the SDK's audio stream publishing status. For details, see:

   |Feature Description |Android |iOS |macOS |Windows |
   |---|---|---|---|---|
   |Set whether to mute the recording signal (without changing status of the local hardware) |`muteAudioCapture` |`muteAudioCapture:mute:` |`muteAudioCapture:mute:` |`muteAudioCapture` |

2. Supports encoding the Alpha channel in externally captured RGBA video frames, allowing the client as a subscriber to internally render RGBA video frames with a transparent background effect. This feature is suitable for scenarios that require separation of the video subject from the background. For details, see:

   |Feature Description |Android |iOS |Windows |
   |---|---|---|---|
   |Enable encoding of the Alpha channel in externally captured video frames. |`enableAlphaChannelVideoEncode` |`enableAlphaChannelVideoEncode:withAlphaLayout:` |`enableAlphaChannelVideoEncode` |
   |Disable encoding of the Alpha channel in externally captured video frames. |`disableAlphaChannelVideoEncode` |`disableAlphaChannelVideoEncode:` |`disableAlphaChannelVideoEncode` |

3. On Android, the SDK now supports rendering to Surface objects in addition to View objects.

4. On the Android platform, dynamic loading of the main library `libbyteplusrtc.so` is supported. For integration guidelines, see Integrate Plugins on Demand.

5. Starting with this version, the RTC SDK supports dynamic loading of `.so` files other than the main library. The SDK provides a `nativeLoadPath` property in the `EngineConfig` class, which supports dynamically loading the required `.so` files from a specified private directory during the App's runtime, thereby reducing the App's installation package size. For information on dynamically loading `.so` files, see Integrate Plugins on Demand.

6. This version provides the SAMI audio technology dynamic library plugin. For details, see Integrate Plugins on Demand to Reduce App Size.

7. Android and iOS platforms support rotating the camera capture to a specified angle, suitable for video capture screen adaptation on devices without gravity sensors, such as face capture devices in the financial industry. For details, see:

|Feature Description |Android |iOS |
|---|---|---|
|Rotate the capture screen |`setVideoCaptureRotation` |`setVideoCaptureRotation:` |

> For devices with gravity sensors, such as mobile phones and tablets, use `setVideoRotationMode` to rotate the video capture screen. For more information, see Mobile Video Capture Rotation Direction.

8. The PC platform provides video enhancement capabilities. When video capture is in a low\-light environment, turning on this feature can improve the brightness of the image. For details, see:

|Feature Description |macOS |Windows |
|---|---|---|
|Set video low\-light enhancement processing |`setLowLightAdjusted` |`setLowLightAdjusted` |

9. All platforms support directional IoT card communication.

10. When internally rendering a remote stream, it supports mirror rendering of a specific remote stream.

|Feature Description |Android |iOS |macOS |Windows |Linux |
|---|---|---|---|---|---|
|Enable mirror rendering for a remote stream when using internal rendering |`setRemoteVideoMirrorType` |`setRemoteVideoMirrorType:withMirrorType:` |`setRemoteVideoMirrorType:withMirrorType:` |`setRemoteVideoMirrorType` |`setRemoteVideoMirrorType` |

11. The push live streaming feature has added the following capabilities:

|Feature Description |Android |iOS |macOS |windows |
|---|---|---|---|---|
|Support initiating a push live streaming task in scenarios where there are no users publishing streams in the room |`MixedStreamServerControlConfig.setPushStreamMode` |`ByteRTCMixedStreamServerControlConfig.pushStreamMode` |`ByteRTCMixedStreamServerControlConfig.pushStreamMode` |`MixedStreamServerControlConfig.push_stream_mode` |
|Support using a placeholder image instead of a video stream to initiate a push live streaming task, and set the fill mode for the placeholder image |* `MixedStreamLayoutRegionConfig.setAlternateImageURL`<br><br>* `MixedStreamLayoutRegionConfig.setAlternateImageFillMode` |* `ByteRTCMixedStreamLayoutRegionConfig.alternateImageUrl`<br><br>* `ByteRTCMixedStreamLayoutRegionConfig.alternateImageFillMode` |* `ByteRTCMixedStreamLayoutRegionConfig.alternateImageUrl`<br><br>* `ByteRTCMixedStreamLayoutRegionConfig.alternateImageFillMode` |* `MixedStreamLayoutRegionConfig.alternate_image_url`<br><br>* `MixedStreamLayoutRegionConfig.alternate_image_fill_mode` |
|Support pushing pure audio streams when mixing and pushing to a CDN |`MixedStreamServerControlConfig.setMediaType` |`ByteRTCMixedStreamServerControlConfig.mediaType` |`ByteRTCMixedStreamServerControlConfig.mediaType` |`MixedStreamServerControlConfig.media_type` |
|Support setting the background image of the overall canvas after mixing |`MixedStreamLayoutConfig.setBackgroundImageURL` |`ByteRTCMixedStreamLayoutConfig.backgroundImageUrl` |`ByteRTCMixedStreamLayoutConfig.backgroundImageUrl` |`IMixedStreamConfig.setBackgroundImageURL` |

12. New server\-side merging control parameters added to the live streaming configuration

13. Support for setting the PayLoadType when sending SEI in stream mixing to adapt to specific players receiving SEI information as the receiving end. See details below:

|Feature Description |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Set the payload type for SEI information in merged streaming |`setSeiPayloadType` |`seiPayloadType` |`seiPayloadType` |`sei_payload_type` |
|Set the Payload UUID for SEI information in merged streaming |`setSeiPayloadUuid` |`seiPayloadUUID` |`seiPayloadUUID` |`sei_payload_uuid` |

14. Support for controlling SEI transmission content. Previously, the server\-side merging defaulted to sending full SEI information. The new version supports sending volume indication SEI separately, which significantly reduces performance overhead in scenarios where high\-frequency transmission of volume information is required. See details below:

|Feature Description |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Set whether to enable the feature of sending volume indication SEI separately |`setEnableVolumeIndication` |`enableVolumeIndication` |`enableVolumeIndication` |`enable_volume_indication` |
|Set SEI Content |`setSeiContentMode` |`seiContentMode` |`seiContentMode` |`sei_content_mode` |
|Set whether the voice information SEI includes volume value |`setIsAddVolumeValue` |`isAddVolumeValue` |`isAddVolumeValue` |`is_add_volume_value` |
|Set the interval for voice information indication |`setVolumeIndicationInterval` |`volumeIndicationInterval` |`volumeIndicationInterval` |`volume_indication_interval` |
|Set the effective volume level |`setTalkVolume` |`talkVolume` |`talkVolume` |`talk_volume` |

15. On Android platform, support for multiple external cameras. Users can switch and select cameras as needed. For more details, refer to the following APIs:

* Create a video device manager instance: `getVideoDeviceManager`

* Get the list of video capture devices in the current system: `enumerateVideoCaptureDevices`

* Set the current video capture device: `setVideoCaptureDevice`

### Enhanced

1. On the Android system, when joining a room, the volume adjusted using the phone's volume buttons is the playback volume of the RTC room. Previously, on some Android phones, when joining a room without playing audio, the volume buttons adjusted the ringtone volume instead of the audio volume.

   * When the SDK sets the audio mode to call mode, adjust the call mode volume;

   * When the SDK sets the audio mode to media mode, adjust the media mode volume.

2. The hardware\-level in\-ear monitoring feature now supports multiple models from OPPO, VIVO, XIAOMI, and more.

3. A new callback `onActiveVideoLayer` has been added. When using custom video encoding and decoding features, the sender can use this callback to encode as needed, saving encoding performance resources.

   |Feature Description |Android |iOS |macOS |Windows |Linux |
   |---|---|---|---|---|---|
   |Callback when the video stream's active state changes |`onActiveVideoLayer` |`onActiveVideoLayer` |`onActiveVideoLayer` |`onActiveVideoLayer` |`onActiveVideoLayer` |

4. The custom video encoding and decoding feature has been optimized for use in custom audio subscription scenarios. To use this feature in a custom audio subscription scenario, you must call the `setVideoDecoderConfig` API on the decoding end to configure custom decoding for any remote main or screen streams.

5. An error scenario has been added when the client captures the video screen: an error code will be received if the video screen is not captured within more than 1 second.

   |Feature Description |Android |iOS |macOS |Windows |
   |---|---|---|---|---|
   |Callback when capturing the local video screen |`onTakeLocalSnapshotResult` |`onTakeLocalSnapshotResult:streamIndex:image:errorCode:` |`onTakeLocalSnapshotResult:streamIndex:image:errorCode:` |`onTakeLocalSnapshotResult` |
   |Callback when capturing the remote video screen |`onTakeRemoteSnapshotResult` |`onTakeRemoteSnapshotResult:streamKey:image:errorCode:` |`onTakeRemoteSnapshotResult:streamKey:image:errorCode:` |`onTakeRemoteSnapshotResult` |

6. When using the RTC SDK for internal video capture on the Android side, the video capture will automatically resume when the app returns to the foreground after being in the background for a long time (\>1 minute), without additional operations.

7. When obtaining local audio information through callbacks, support for obtaining the fundamental frequency of the human voice is added.

|Feature Description |Android |iOS |macOS |Windows |Linux |
|---|---|---|---|---|---|
|Enable audio information reporting |`enableAudioPropertiesReport` |`enableAudioPropertiesReport:` |`enableAudioPropertiesReport:` |`enableAudioPropertiesReport` |`enableAudioPropertiesReport` |
|Obtain local audio information |`onLocalAudioPropertiesReport` |`rtcEngine:onLocalAudioPropertiesReport:` |`rtcEngine:onLocalAudioPropertiesReport:` |`onLocalAudioPropertiesReport` |`onLocalAudioPropertiesReport` |

8. Support for customizing the local log file name prefix has been added. The final log file name will be in the format of `prefix + "_" +`file creation time`+ "_rtclog".log`.

|Feature Description |Android |iOS |macOS |Windows |Linux |
|---|---|---|---|---|---|
|Set the local log file name prefix |`RTCLogConfig.logFilenamePrefix` |`ByteRTCLogConfig.logFilenamePrefix` |`ByteRTCLogConfig.logFilenamePrefix` |`LogConfig.log_filename_prefix` |`LogConfig.log_filename_prefix` |

9. The basic beauty filter has added a clarity sub\-item and optimized the default values of beauty filter parameters. To use the clarity sub\-item, you need to integrate the effects SDK version 4.4.2 or higher. The default intensity for each basic beauty sub\-item has been adjusted to: Whitening 0.7, Smoothing 0.8, Sharpening 0.5, Clarity 0.7.

|Feature Description |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Enable/disable basic beauty filter |`enableEffectBeauty` |`enableEffectBeauty:` |`enableEffectBeauty:` |`enableEffectBeauty` |
|Adjust the intensity of the basic beauty filter |`setBeautyIntensity` |`setBeautyIntensity:withIntensity:` |`setBeautyIntensity:withIntensity:` |`setBeautyIntensity` |

## 3.56 (Flutter)

Release date: November 15, 2023

Refer to Changelog if you want to learn about new features, or update the RTC SDK used in the Flutter plugin to the latest version.

## 3.56

Release date: October 24, 2023

Platform: Android, iOS, macOS, Windows.

See Changelogs if you want to update the RTC SDK used in your app to the latest version.

### New

1. Adds support for connecting multiple external cameras on the Android platform, allowing users to switch between them as needed. Add getVideoDeviceManager interface for video device management, enumerateVideoCaptureDevices interface to get the list of video capture devices, and setVideoCaptureDevice interface for setting video capture devices.

2. Adds new parameters which you can set while mixing streams on the server side.

   a. Supports setting PayLoadType when sending SEI during stream mixing and pushing, and supports receiving SEI information when using specific players as the receiving end. See the APIs below:

   |API |Android |iOS |macOS |Windows |
   |---|---|---|---|---|
   |Set SEI payload type. |setSeiPayloadType |seiPayloadType |seiPayloadType |sei_payload_type |
   |Set SEI Payload UUID. |setSeiPayloadUuid |seiPayloadUUID |seiPayloadUUID |sei_payload_uuid |

   b. Supports SEI content control. In previous versions, the stream contains all the SEI information by default. While in the new version, you can choose whether to send volume indication SEI only, which significantly reduces performance consumption in scenarios where high\-frequency volume information needs to be sent. See the APIs below:

   |API |Android |iOS |macOS |Windows |
   |---|---|---|---|---|
   |Sets whether to enable the function of separately sending sound indication SEI. |setEnableVolumeIndication |enableVolumeIndication |enableVolumeIndication |enable_volume_indication |
   |Sets SEI content. |setSeiContentMode |seiContentMode |seiContentMode |sei_content_mode |
   |Sets whether volume value is contained in the sound indication SEI. |setIsAddVolumeValue |isAddVolumeValue |isAddVolumeValue |is_add_volume_value |
   |Sets the sound indication interval. |setVolumeIndicationInterval |volumeIndicationInterval |volumeIndicationInterval |volume_indication_interval |
   |Sets the effective volume. |setTalkVolume |talkVolume |talkVolume |talk_volume |

3. The in\-ear monitoring feature is now available for the PC SDK. See the following APIs:

   |API |Windows |macOS |Electron |
   |---|---|---|---|
   |Enable ear monitoring |setEarMonitorMode |setEarMonitorMode: |setEarMonitorMode |
   |Adjust the volume of ear monitoring |setEarMonitorVolume |setEarMonitorVolume: |setEarMonitorVolume |

4. When you get the audio raw data, you can set the number of samples in an audio frame. See:

   |Platform |Android |iOS |macOS |Windows |
   |---|---|---|---|---|
   |Parameter |samplesPerCall |samplesPerCall |samplesPerCall |samples_per_call |

5. When calling setLocalVideoSink/setRemoteVideoSink for custom video rendering, you can receive video frames encoded in RGBA format from the SDK. See:

   |Platform |Android |iOS |macOS |Windows |
   |---|---|---|---|---|
   |Parameter |PixelFormat |ByteRTCVideoSinkPixelFormat |ByteRTCVideoSinkPixelFormat |PixelFormat |

6. Added a callback for user visibility setting results.

   |Platform |Android |iOS |macOS |Windows |Electron |
   |---|---|---|---|---|---|
   |Callback |onUserVisibilityChanged |rtcRoom:onUserVisibilityChanged:errorCode: |rtcRoom:onUserVisibilityChanged:errorCode: |onUserVisibilityChanged |onUserVisibilityChanged |

7. This new feature allows users to enable or disable the function of blacklisting silent devices. It is only available for Windows. See the API below:

   |Platform |Windows |Electron |
   |---|---|---|
   |Enables/disables the silent device filter function. |enableFilterSilentDevice |enableFilterSilentDevice |

8. On Android, iOS and macOS platforms, you can get IRTCVideo in C++ layer. In some scenarios, getting and working with `IRTCVideo` in C++ layer has much higher execution efficiency than through the encapsulation layer. Typical scenarios include: custom processing of video/audio frames, encryption of audio and video calls, etc. See:

   |Platform |Android |iOS |macOS |
   |---|---|---|---|
   |API |getNativeHandle |getNativeHandle |getNativeHandle |

9. On Android and iOS platforms, when capturing video through the internal mechanism of the RTC SDK, you can disable the automatic face exposure feature and the dynamic capture frame rate feature. see:

   |API |Android |iOS |
   |---|---|---|
   |Enable / disable the automatic face exposure feature |enableCameraAutoExposureFaceMode |enableCameraAutoExposureFaceMode |
   |Set the lower limit of the dynamic capture frame rate |setCameraAdaptiveMinimumFrameRate |setCameraAdaptiveMinimumFrameRate |

10. Supports setting the local log parameters, including the directory, the total size limits, the logging level, and the name prefix for the log files.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setLogConfig |setLogConfig |setLogConfig |setLogConfig |setLogConfig |

### Enhanced

1. The `onActiveVideoLayer` callback has been added. When using custom video encoding and decoding, the sender can utilize this callback to encode video on\-demand, thereby saving performance resources consumed by encoding.

   |API |Android |iOS |macOS |Windows |
   |---|---|---|---|---|
   |`onActiveVideoLayer` |onActiveVideoLayer |onActiveVideoLayer |onActiveVideoLayer |onActiveVideoLayer |

2. The custom video encoding and transmission feature has been optimized to support usage in scenarios with custom audio subscription. If you want to use the custom video encoding and transmission feature in a scenario with custom audio subscription, you should call `setVideoDecoderConfig` to set the decoding parameters for any remote main stream or screen sharing stream to custom encoding/decoding.

3. The error message when capturing snapshots on the client side has been optimized. If it exceeds 1s, you will receive the corresponding error message. See:

   |API |Android |iOS |macOS |Windows |Electron |
   |---|---|---|---|---|---|
   |`onTakeLocalSnapshotResult` |onTakeLocalSnapshotResult |onTakeLocalSnapshotResult:streamIndex:image:errorCode: |onTakeLocalSnapshotResult:streamIndex:image:errorCode: |onTakeLocalSnapshotResult |onTakeLocalSnapshotResult |
   |`onTakeRemoteSnapshotResult` |onTakeRemoteSnapshotResult |onTakeRemoteSnapshotResult:streamKey:image:errorCode: |onTakeRemoteSnapshotResult:streamKey:image:errorCode: |onTakeRemoteSnapshotResult |onTakeRemoteSnapshotResult |

4. For an Android App using RTC SDK to capture video internally, if it goes to the background for a long time (\>1min) and then returns to the foreground, RTC will automatically resume video capture without any additional operations.

5. You can get the fundamental frequency of the local voice when you enable local audio property reporting. See:

   |API |Android |iOS |macOS |Windows |Electron |
   |---|---|---|---|---|---|
   |Enable audio property report |enableAudioPropertiesReport |enableAudioPropertiesReport: |enableAudioPropertiesReport: |enableAudioPropertiesReport |enableAudioPropertiesReport |
   |Get local audio property report |onLocalAudioPropertiesReport |rtcEngine:onLocalAudioPropertiesReport: |rtcEngine:onLocalAudioPropertiesReport: |onLocalAudioPropertiesReport |onLocalAudioPropertiesReport |

6. Added clarity to the basic beauty effects. This sub\-item requires integration with the Effects SDK v4.4.2+. The default values for each beauty mode's intensity are adjusted as follows: 0.7 for brightening, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity.

   |API |Android |iOS |macOS |Windows |Electron |
   |---|---|---|---|---|---|
   |Enable/Disable basic beauty effects |enableEffectBeauty |enableEffectBeauty: |enableEffectBeauty: |enableEffectBeauty |enableEffectBeauty |
   |Set the beauty effect intensity |setBeautyIntensity |setBeautyIntensity:withIntensity: |setBeautyIntensity:withIntensity: |enableEffectBeauty |setBeautyIntensity |

7. The audio mixing class has been split into an audio effect management class and a music management class:

   |Class |Android |iOS |macOS |Windows |Electron |
   |---|---|---|---|---|---|
   |Audio effect management class |IAudioEffectPlayer |ByteRTCAudioEffectPlayer |ByteRTCAudioEffectPlayer |IAudioEffectPlayer |RTCAudioEffectPlayer |
   |Music management class |IMediaPlayer |ByteRTCMediaPlayer |ByteRTCMediaPlayer |IMediaPlayer |RTCMediaPlayer |

## 3.52

Release date: July 3, 2023

Platform: Android, iOS, macOS, Windows, Electron.

See Changelogs if you want to update the RTC SDK used in your app to the latest version.

### Important Information

1. Per the request of App Store, starting from the SDK version, the RTC SDK for iOS no longer supports ARMv7. The lowest compatible iOS version is iOS 11.

2. We are providing iOS and macOS QuickStart Demo using Swift. See Build App with the demo project (iOS\-Swift) and Build App with the demo project (macOS\-Swift).

### New

1. Cellular enhanced communication is supported by RTC SDK for Android and iOS.

|Platform |Android |iOS |
|---|---|---|
|API |setCellularEnhancement |setCellularEnhancement: |

2. Supports setting local proxies and other extra information.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setLocalProxy |setLocalProxy: |setLocalProxy: |setLocalProxy |setLocalProxy |
|Callback |onLocalProxyStateChanged |rtcEngine:onLocalProxyStateChanged:withProxyState:withProxyError: |rtcEngine:onLocalProxyStateChanged:withProxyState:withProxyError: |onLocalProxyStateChanged |onLocalProxyStateChanged |

3. Supports setting room\-related attributes and other extra information.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setRoomExtraInfo |setRoomExtraInfo:value: |setRoomExtraInfo:value: |setRoomExtraInfo |setRoomExtraInfo |
|Callback |onSetRoomExtraInfoResult |rtcRoom:onSetRoomExtraInfoResult:error |rtcRoom:onSetRoomExtraInfoResult:error |onSetRoomExtraInfoResult |onSetRoomExtraInfoResult |
|Callback |onRoomExtraInfoUpdate |rtcRoom:onRoomExtraInfoUpdate:value:lastUpdateUserId:lastUpdateTimeMs: |rtcRoom:onRoomExtraInfoUpdate:value:lastUpdateUserId:lastUpdateTimeMs: |onRoomExtraInfoUpdate |onRoomExtraInfoUpdate |

4. Now you can examine the echo\-cancellation ability of local audio devices before or during an RTC call. This feature is available on all platforms.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |startHardwareEchoDetection |startHardwareEchoDetection: |startHardwareEchoDetection: |startHardwareEchoDetection |startHardwareEchoDetection |
|API |stopHardwareEchoDetection |stopHardwareEchoDetection |stopHardwareEchoDetection |stopHardwareEchoDetection |stopHardwareEchoDetection |
|Callback |onHardwareEchoDetectionResult |rtcEngine:onHardwareEchoDetectionResult: |rtcEngine:onHardwareEchoDetectionResult: |onHardwareEchoDetectionResult |onHardwareEchoDetectionResult |

5. This feature allows users to digitally zoom and pan the local video view. This is the recommended method for local video control, as it provides a consistent experience across the wide variety of cameras on different devices.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setVideoDigitalZoomConfig |setVideoDigitalZoomConfig:size: |setVideoDigitalZoomConfig:size: |setVideoDigitalZoomConfig |setVideoDigitalZoomConfig |
|API |setVideoDigitalZoomControl |setVideoDigitalZoomControl: |setVideoDigitalZoomControl: |setVideoDigitalZoomControl |setVideoDigitalZoomControl |
|API |startVideoDigitalZoomControl |startVideoDigitalZoomControl: |startVideoDigitalZoomControl: |startVideoDigitalZoomControl |startVideoDigitalZoomControl |
|API |stopVideoDigitalZoomControl |stopVideoDigitalZoomControl |stopVideoDigitalZoomControl |stopVideoDigitalZoomControl |stopVideoDigitalZoomControl |

6. In the case of PCs equipped with a rotated camera, call the following API to specify the rotation. It is available on Windows, macOS, and Electron.

|Platform |macOS |Windows |Electron |
|---|---|---|---|
|API |setVideoCaptureRotation: |setVideoCaptureRotation |setVideoCaptureRotation |

7. Automatically adapt the Ambient Noise Suppression(ANS) algorithm according to the business scenario selected when entering the room. You can also set the ANS mode manually during the call.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setAnsMode |setAnsMode: |setAnsMode: |setAnsMode |setAnsMode |

8. This feature allows users to enable or disable Automatic Gain Control (AGC). It is available on macOS, Windows, and Electron.

|Platform |macOS |Windows |Electron |
|---|---|---|---|
|API |enableAGC: |enableAGC |enableAGC |

9. Starting from this version, some features have been separated from the SDK and encapsulated into independent extensions. A new callback onExtensionAccessError is added, which allows you to locate the extension that you failed to access.

### Enhanced

1. Optimization for big conferences. After the Audio Selection is enabled, the publisher can choose to skip the Audio Selection. It is suitable for scenarios where the speeches of the specified users are expected to be heard all the time, such as the rooms with a host. For each appId, you should decide whether to enable Audio Selection instead of which room mode. See Audio Selection.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setAudioSelectionConfig |setAudioSelectionConfig: |setAudioSelectionConfig: |setAudioSelectionConfig |setAudioSelectionConfig |

2. Optimized the spatial audio feature. Supports updating the position and orientation of the local user and a certain remote user in the rectangular coordinate system in the current room, as well as removing one or all remote users from the spatial audio effect.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |updateSelfPosition |updateSelfPosition: |updateSelfPosition: |updateSelfPosition |updateSelfPosition |
|API |updateRemotePosition |updateRemotePosition:positionInfo: |updateRemotePosition:positionInfo: |updateRemotePosition |updateRemotePosition |
|API |removeRemotePosition |removeRemotePosition: |removeRemotePosition: |removeRemotePosition |removeRemotePosition |
|API |removeAllRemotePosition |removeAllRemotePosition |removeAllRemotePosition |removeAllRemotePosition |removeAllRemotePosition |

3. For video encoding, the strategy of adaptive encoding rate is optimized with the strategy of content adaptation. The video will be clearer for complex scenes and less bandwidth\-consuming in simple scenes. To use this feature, please contact technical support.

## 3.51

Release date: July 3, 2023

Platform: Flutter

See Changelogs if you want to update the RTC SDK used in your app to the latest version.

## 3.50

Release date: May 8, 2023

Platform: Android, iOS, macOS, Windows, Electron.

See Changelogs also if you want to update the RTC SDK already used in your app to the latest version.

### Notes

1. Starting with this release, we are providing macOS SDK that can natively support app development for Macs with Apple silicon (M1 Series). Download the SDK at Resources.

2. The naming and parameters of some APIs have been standardized. Please modify your project files as necessary according to the Changelogs.

### New

1. Adds new callbacks reporting sending and playing status of the first screen audio frame.

|Platform |Windows |Electron |
|---|---|---|
|Callback on the sending status |onScreenAudioFrameSendStateChanged |onScreenAudioFramePlayStateChanged |
|Callback on the playing status |onScreenAudioFrameSendStateChanged |onScreenAudioFramePlayStateChanged |

2. Adds callbacks triggered when the publishing/subscribing privilege of your Token is about to expire. After receiving this callback, you must re\-acquire and update the relevant privileges of the Token to ensure normal audio/video calls. Contact technical support if you need this feature.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|Callback for expiring Token with publishing privilege |onPublishPrivilegeTokenWillExpire |onPublishPrivilegeTokenWillExpire: |onPublishPrivilegeTokenWillExpire: |onPublishPrivilegeTokenWillExpire |onPublishPrivilegeTokenWillExpire |
|Callback for expiring Token with subscribing privilege |onSubscribePrivilegeTokenWillExpire |onSubscribePrivilegeTokenWillExpire: |onSubscribePrivilegeTokenWillExpire: |onSubscribePrivilegeTokenWillExpire |onSubscribePrivilegeTokenWillExpire |

3. Supports detecting background music during the call and protecting the sound quality of the music. Please contact technical support if you need this feature.

4. Supports some new voice reverb types.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|Supported voice reverb types |VoiceReverbType |ByteRTCVoiceReverbType |ByteRTCVoiceReverbType |VoiceReverbType |voice_reverb_type |

5. Supports recording the video/audio call and generating the local audio file.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |startAudioRecording |startAudioRecording |startAudioRecording |startAudioRecording |startAudioRecording |

6. Supports setting the equalization and reverb effect of the locally captured audio.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|Setting voice equalization |setLocalVoiceEqualization |setLocalVoiceEqualization |setLocalVoiceEqualization |setLocalVoiceEqualization |setLocalVoiceEqualization |
|Setting voice reverb effect |setLocalVoiceReverbParam |setLocalVoiceReverbParam |setLocalVoiceReverbParam |setLocalVoiceReverbParam |setLocalVoiceReverbParam |
|Enabling voice reverb effect |enableLocalVoiceReverb |enableLocalVoiceReverb |enableLocalVoiceReverb |enableLocalVoiceReverb |enableLocalVoiceReverb |

7. Supports stopping, pausing, and resuming playback of all audio files on all platforms.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|Stop all audio files |stopAllAudioMixing |stopAllAudioMixing |stopAllAudioMixing |stopAllAudioMixing |stopAllAudioMixing |
|Pause all audio files |pauseAllAudioMixing |pauseAllAudioMixing |pauseAllAudioMixing |pauseAllAudioMixing |pauseAllAudioMixing |
|Resume all audio files |resumeAllAudioMixing |resumeAllAudioMixing |resumeAllAudioMixing |resumeAllAudioMixing |resumeAllAudioMixing |

8. [Howling detection](docs\-

   70083#MediaDeviceWarning\-media_device_warning_capture_detect_howling) warning is added into MediaDeviceWarning, which will be triggered in the following circumstances:

   * Howling is detected in room modes that do not support howling suppression.

   * Unsuppressed howling is detected in room modes that support howling suppression.

9. From iPadOS 16 and macOS Ventura, you can use Stage Manager to organize Apps and Windows. If your App is not in the center, you can get informed by onVideoDeviceStateChanged. Refer to Resume Audio/Video Call.

|Platform |iOS |
|---|---|
|Enum |ByteRTCMediaDeviceErrorNotAvailableInBackground<br><br>ByteRTCMediaDeviceErrorVideoInUseByAnotherClient<br><br>ByteRTCMediaDeviceErrorNotAvailableWithMultipleForegroundApps<br><br>ByteRTCMediaDeviceErrorNotAvailableDueToSystemPressure |

10. When pushing streams to CDN, you can set the appearance of the window to a rounded rectangle. See setCornerRadius.

11. You can set the static picture as a replacement for the locally captured video stream.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setDummyCaptureImagePath |setDummyCaptureImagePath: |setDummyCaptureImagePath: |setDummyCaptureImagePath |setDummyCaptureImagePath |

12. You can share a dual\-channel audio stream during screen sharing with the new API on PC platforms.

|Platform |macOS |Windows |Electron |
|---|---|---|---|
|API |setScreenAudioChannel |setScreenAudioChannel |setScreenAudioChannel |

1. When you use the audio monitoring feature on an Android device, if the device supports hardware ear monitoring, RTC SDK enables hardware ear monitoring by default.

2. You can switch the Bluetooth communication mode between the iOS device and earphones when RTC works in media scenarios. See setBluetoothMode:.

3. In multi\-room scenarios, you can adjust the volume of all users in one room at once.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setRemoteRoomAudioPlaybackVolume |setRemoteRoomAudioPlaybackVolume: |setRemoteRoomAudioPlaybackVolume: |setRemoteRoomAudioPlaybackVolume |setRemoteRoomAudioPlaybackVolume |

16. This version adds support for VP8 encoding. Enabling the VP8 feature largely improves your users' access to web SDK. To enable the feature, contact technical support.

17. During custom video capture on macOS and Windows, you can set your maximum capture resolution with the new API setOriginalScreenVideoInfo. Then RTC will recommend you the best capture parameter through the onExternalScreenFrameUpdate callback.

18. Client\-side stream mixing supports setting the video frame callback format. It supports compressed textures on Android, which can help fix performance issues on some Android devices.

|Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Keytype |TranscoderClientMixVideoFormat |ByteRTCClientMixVideoFormat |ByteRTCClientMixVideoFormat |TranscoderClientMixVideoFormat |

19. You can now define teams whose members can talk to each other without audio attenuation, even when the range audio feature is enabled.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|API |setNoAttenuationFlags |setNoAttenuationFlags: |setNoAttenuationFlags: |setNoAttenuationFlags |setNoAttenuationFlags |

### Enhanced

1. When getting local and remote volume information by calling enableAudioPropertiesReport, you can make the volume curve smoother with `smooth` and get information about locally mixing audio with `audio_report_mode`.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|Parameter |smooth |smooth |smooth |smooth |smooth |

2. Optimizes real\-time signaling threads and components to reduce message arrival latency.

3. Upgrades 3D spatial audio stereo effect by supporting spherical stereo rendering. By simulating a stereo sound field in the spherical area of a human's head, the audio will be rendered differently with orientation, distance from the sound source, and height of the virtual image's head, making the user feel closer to the real\-world listening experience.

4. Improves the usability of pushing media streams to CDN. Unifies the configuration limits, restrictions, and default values of RTC SDK and OpenAPI, and the configurations will be verified by RTC SDK. Some illegal parameters will be automatically corrected to default values.

|Platform |Android |iOS |macOS |Windows |Electron |
|---|---|---|---|---|---|
|Keytype |LiveTranscoding |ByteRTCLiveTranscoding |ByteRTCLiveTranscoding |ITranscoderParam |TranscoderParam |

## 3.45.7

Release date: March 22, 2023

Platform: Android, iOS, macOS, Windows.

This release optimizes the RTC call experience when users' devices are under\-performing on mobile. Please contact the technical support team if you need this function.

## 3.45.6

Release date: March 1, 2023

See Changelogs also if you want to update the RTC SDK already used in your app to the latest version.

### New

1. When you call enableAudioPropertiesReport to get the local audio information, you can get the local mixing information with extra configuration.

2. The reverb effect is supported when using SDK\-level in\-ear monitoring on mobile phones. In addition, you can get and customize the SDK\-level in\-ear monitoring audio frames for custom processing from the new callback below:

|Platform |Android |iOS |
|---|---|---|
|Callback |`onProcessEarMonitorAudioFrame` |`onProcessEarMonitorAudioFrame:` |

3. Get the actual mixing length of the audio file, regardless of pausing, jumping, changing speed, and getting stuck. See:

|Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|API |`getAudioMixingPlaybackDuration` |`getAudioMixingPlaybackDuration:` |`getAudioMixingPlaybackDuration:` |`getAudioMixingPlaybackDuration` |

4. With the new pair of APIs you can subscribe or unsubscribe to all users by one call. We recommend using them in the scenario that requires a fixed number of publishers.

|Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|API |* `subscribeAllStreams`<br><br>* `unsubscribeAllStreams` |* `subscribeAllStreamsWithMeidaStreamType:`<br><br>* `unSubscribeAllStreamsWithMeidaStreamType:` |* `subscribeAllStreamsWithMeidaStreamType:`<br><br>* `unSubscribeAllStreamsWithMeidaStreamType:` |* `subscribeAllStreams`<br><br>* `unsubscribeAllStreams` |

5. Set the default volume during audio mixing on mobile with the API below:

|Platform |Android |iOS |
|---|---|---|
|API |`setAllAudioMixingVolume` |`setAllAudioMixingVolume:` |

6. You can get the screen\-sharing audio frames for custom processing. See:

|Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Callback |`onProcessScreenAudioFrame` |`onProcessScreenAudioFrame:` |`onProcessScreenAudioFrame:` |`onProcessScreenAudioFrame` |

7. When a user changes the system volume from the operating system settings on the PC, you can get the volume changes via the following callbacks instantly.

|Platform |macOS |Windows |
|---|---|---|
|Callback |`rtcEngine:onAudioDeviceVolumeChanged:volume:muted:` |`onAudioDeviceVolumeChanged` |

8. Get the snapshot of the local/remote screen on the client. See:

|Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|API |* `takeLocalSnapshot`<br><br>* `takeRemoteSnapshot` |* `takeLocalSnapshot:callback:`<br><br>* `takeRemoteSnapshot:callback:` |* `takeLocalSnapshot:callback:`<br><br>* `takeRemoteSnapshot:callback:` |* `takeLocalSnapshot`<br><br>* `takeRemoteSnapshot` |

### Enhanced

1. iTunes music files are supported for audio mixing on iOS.

2. Support adaptive hardware\-level ear monitoring on Android. See setEarMonitorMode.

3. The network quality callback now provides more detailed status information. You can now be notified when the network connection is down.

|Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Keytype |Add "NETWORK_QUALITY_DOWN = 6" to `NetworkQuality` |Add "ByteRTCNetworkQualityDown" to `ByteRTCNetworkQuality` |Add "ByteRTCNetworkQualityDown" to `ByteRTCNetworkQuality` |Add "kNetworkQualityDown" to `NetworkQuality` |

4. If the calling device successfully connects to the Bluetooth headset but the Synchronous Connection\-Oriented (SCO) link fails, the audio playback mode of the device will be switched from call mode to media mode, i.e., the sound will be played using the Bluetooth headset to optimize the listening experience.

5. If your app targets API 31, when the calling device connects to Bluetooth, there is no need to apply for Bluetooth permission from the system.

### Fixed

1. Fixed the VP8 related screen sharing failure on iOS.

2. Fixed an Acoustic Echo Cancellation (AEC) failure on some Android models.

## 3.45.1

Release date: September 1, 2022

We have released the first commercial version of BytePlus RTC SDK for Android, iOS, macOS, Windows, Flutter and Electron.

You can download our latest SDK and Demo.
