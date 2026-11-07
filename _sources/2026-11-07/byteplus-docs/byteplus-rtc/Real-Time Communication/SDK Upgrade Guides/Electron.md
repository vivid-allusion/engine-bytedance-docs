---
title: "Electron"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-519257"
---

Before upgrading the RTC SDK for Electron, refer to this changelog to understand the breaking changes introduced in each version.

This document details API modifications, replacements, and data type updates, ensuring you can smoothly transition between versions by making the necessary adjustments to your existing code.

<span id="_3-60-1"></span>
## 3.60.1

Electron RTC SDK 3.60.1 introduces a redesigned engine and stream model and contains breaking changes. Complete the changes in this section when upgrading from 3.56.1.

<span id="electron-3-60-1-sdk-integration"></span>
### SDK Integration

The exported engine class has changed.


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`import { RTCVideo } from '@byteplus/byteplus-electron-sdk'` |`import { RTCEngine } from '@byteplus/byteplus-electron-sdk'` |**Export rename**: Replace the imported `RTCVideo` class with `RTCEngine`. |
|`RTCVideo` |`RTCEngine` |**Class rename**: Update the engine type, constructor calls, variables, and type annotations that reference `RTCVideo`. |


<span id="electron-3-60-1-api-changes"></span>
### API Changes

<span id="engine-management"></span>
#### Engine Management


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`createRTCVideo(app_id, parameters)` |`createRTCEngine(engine_config)` |**Interface rename and parameter merge**: Rename the method to `createRTCEngine`. Replace the separate `app_id` and `parameters` arguments with one `EngineConfig` object containing both fields. |
|`destroyRTCVideo()` |`destroyRTCEngine()` |**Interface rename**: Rename the engine\-destruction method to match the new `RTCEngine` class. The method has no parameter changes. |
|`RTCVideo.getErrorDescription(code)` |Removed |**Interface removal**: The static error\-description lookup is no longer exposed. Update error handling to use the error\-code and return\-code enums delivered by the relevant interface or callback. |


Example:

```ts
import { RTCEngine } from '@byteplus/byteplus-electron-sdk';

const engine = new RTCEngine();
engine.createRTCEngine({
  app_id: '<YOUR_APP_ID>',
  parameters: '',
});

// Destroy the engine when it is no longer needed.
engine.destroyRTCEngine();
```


<span id="room-management"></span>
#### Room Management


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`joinRoom(token, user_info, config?)` |`joinRoom(token, user_info, user_visibility, config?)` |**Parameter addition**: Add the required Boolean `user_visibility` before `config`. Set it to `false` when joining, then call `setUserVisibility(true)` before publishing media streams. |
|`RTCRoomConfig.is_auto_publish` |`is_auto_publish_audio` and `is_auto_publish_video` |**Field split**: Replace the single auto\-publish switch with separate audio and video switches. Set both fields when you need the same behavior as the former `is_auto_publish` field. |
|`RTCRoomConfig.remote_video_config` |Removed |**Field removal and configuration timing change**: Remote video configuration is no longer supplied when joining. After receiving the remote stream's `streamId`, call `setRemoteVideoConfig(stream_id, config)`. |


<span id="stream-identification"></span>
#### Stream Identification

3.60.1 uses `streamId` as the unique identifier for an audio and video stream. Replace combinations such as `roomId + userId`, `StreamIndex`, and `RemoteStreamKey` with `streamId` where required. Obtain the stream ID and related metadata from callbacks that provide `StreamInfo`.

`StreamInfo` contains the following fields:


|Field |Description |
|---|---|
|`stream_id` |Unique stream ID. |
|`room_id` |Room that contains the stream. |
|`user_id` |User that publishes the stream. |
|`is_screen` |Whether the stream is a screen\-sharing stream. |


The following commonly used APIs are affected:


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`setRemoteAudioPlaybackVolume(room_id, user_id, volume)` |`setRemoteAudioPlaybackVolume(stream_id, volume)` |**Stream identifier change**: Remove `room_id` and `user_id`; pass the target stream's `stream_id` instead. |
|`setRemoteVideoConfig(user_id, config)` |`setRemoteVideoConfig(stream_id, config)` |**Stream identifier change**: Replace `user_id` with `stream_id`, allowing configuration to target a specific stream published by the user. |
|`setRemoteVideoSuperResolution(stream_key, mode)` |Removed |**Interface removal**: Remote video super resolution is no longer exposed. Remove the call and any handling that depends on its result callback. |
|`setAudioAlignmentProperty(stream_key, mode)` |`setAudioAlignmentProperty(stream_id, mode)` |**Parameter type change**: Replace the `RemoteStreamKey` object with its `stream_id`. |
|`takeRemoteSnapshot(stream_key)` |`takeRemoteSnapshot(stream_id)` |**Parameter type change**: Replace the `RemoteStreamKey` object with its `stream_id`. |


<span id="publish-and-subscribe-to-streams"></span>
#### Publish and Subscribe to Streams

Publishing and subscription operations are split by media type. Camera and screen streams use the same APIs and are distinguished by `streamId`.


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`publishStream(type)` / `unpublishStream(type)` |`publishStreamAudio(publish)` and `publishStreamVideo(publish)` |**Interface split and operation merge**: Split control by audio and video. Merge publish and unpublish into the Boolean `publish` argument: `true` publishes and `false` unpublishes. The former `MediaStreamType` argument is removed. |
|`publishScreen(type)` / `unpublishScreen(type)` |`publishStreamAudio(publish)` and `publishStreamVideo(publish)` |**Interface merge**: Remove the screen\-specific methods. Camera and screen sources use the same audio/video publishing methods; publish after starting the corresponding capture source. |
|`subscribeStream(user_id, type)` / `unsubscribeStream(user_id, type)` |`subscribeStreamAudio(stream_id, subscribe)` and `subscribeStreamVideo(stream_id, subscribe)` |**Interface split and operation merge**: Split subscription by audio and video, and merge subscribe/unsubscribe through the Boolean `subscribe` argument. Replace `user_id` with `stream_id`; remove `MediaStreamType`. |
|`subscribeScreen(user_id, type)` / `unsubscribeScreen(user_id, type)` |`subscribeStreamAudio(stream_id, subscribe)` and `subscribeStreamVideo(stream_id, subscribe)` |**Interface merge**: Remove screen\-specific subscription methods. Pass the screen stream's `stream_id` to the unified audio/video subscription methods. |
|`subscribeAllStreams(type)` / `unsubscribeAllStreams(type)` |`subscribeAllStreamsAudio`, `unsubscribeAllStreamsAudio`, `subscribeAllStreamsVideo`, and `unsubscribeAllStreamsVideo` |**Interface split**: Replace the `MediaStreamType` argument with separate audio and video methods. Subscribe and unsubscribe remain separate operations. |
|`pauseAllSubscribedStream(type)` / `resumeAllSubscribedStream(type)` |`pauseAllSubscribedStreamAudio`, `resumeAllSubscribedStreamAudio`, `pauseAllSubscribedStreamVideo`, and `resumeAllSubscribedStreamVideo` |**Interface split**: Replace `PauseResumeControlMediaType` with separate audio and video pause/resume methods that take no arguments. |


<span id="video-rendering-and-frame-sinks"></span>
#### Video Rendering and Frame Sinks


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`setupRemoteVideo(user_id, room_id, view, options?)` |`setupRemoteVideo(stream_id, view, options?, sink_config?)` |**Parameter replacement and addition**: Replace `user_id` and `room_id` with `stream_id`. Add the optional `sink_config` parameter to configure rotation, mirroring, and pixel format. |
|`removeRemoteVideo(user_id, room_id)` |`removeRemoteVideo(stream_id)` |**Parameter replacement**: Replace `user_id` and `room_id` with `stream_id`. |
|`setupLocalScreen` / `removeLocalScreen` |`setupLocalVideo` / `removeLocalVideo` |**Interface merge**: Local camera and screen rendering now use the same methods. When binding a local frame sink, use `LocalVideoSinkPosition` to select the frame position. |
|`setupRemoteScreen` / `removeRemoteScreen` |`setupRemoteVideo` / `removeRemoteVideo` |**Interface merge**: Remote camera and screen rendering now use the same methods. Pass the screen stream's `stream_id`. |


<span id="video-encoding-and-capture"></span>
#### Video Encoding and Capture


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`setVideoEncoderConfig(configs: VideoEncoderConfig[])` |`setVideoEncoderConfig(config: VideoEncoderConfig)` |**Parameter type and scope change**: Replace the configuration array with one `VideoEncoderConfig` object for the primary stream. Configure simulcast streams through `setLocalSimulcastMode`. |
|`setMaxVideoEncoderConfig(config)` |`setVideoEncoderConfig(config)` |**Interface merge**: The former maximum\-stream configuration is handled by `setVideoEncoderConfig`; the old method is removed. |
|`enableSimulcastMode(enabled)` |`setLocalSimulcastMode(mode, stream_config?)` |**Interface replacement and parameter extension**: Replace the Boolean switch with `VideoSimulcastMode`. Use the optional `stream_config` array to configure simulcast encoding parameters. |
|`setScreenVideoEncoderConfig(config)` |`setVideoEncoderConfig(config)` |**Interface merge**: Screen and camera streams use the unified encoder configuration method; the screen\-specific method is removed. |


<span id="audio-capture-and-processing"></span>
#### Audio Capture and Processing


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`setCaptureVolume(index, volume)` |`setCaptureVolume(volume)` |**Parameter removal**: Remove `index`; capture volume is no longer selected by `StreamIndex`. |
|`setScreenAudioStreamIndex(index)` |Removed |**Interface removal**: Screen and microphone audio use the unified stream model, so selecting a screen\-audio stream index is no longer supported. Remove the call. |
|`setVoiceChangerType(change_type: number)` |`setVoiceChangerType(change_type: VoiceChangerType)` |**Parameter type change**: Replace numeric literals with members of the new `VoiceChangerType` enum. |
|`setVoiceReverbType(voice_reverb_type: number)` |`setVoiceReverbType(voice_reverb_type: VoiceReverbType)` |**Parameter type change**: Replace numeric literals with members of the new `VoiceReverbType` enum. |


The legacy engine\-level audio\-mixing methods, including `startAudioMixing`, `stopAudioMixing`, `pauseAudioMixing`, `resumeAudioMixing`, and the related preload, position, volume, pitch, speed, track, and progress APIs, are removed. Use `RTCAudioEffectPlayer` for short sound effects and `RTCMediaPlayer` for longer media files. `enableFilterSilentDevice` is also removed without a replacement.

<span id="snapshots-and-local-recording"></span>
#### Snapshots and Local Recording


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`takeLocalSnapshot(stream_index)` |`takeLocalSnapshot()` |**Parameter removal**: Remove `stream_index`; the local snapshot method no longer selects the source by `StreamIndex`. |
|`takeRemoteSnapshot(stream_key)` |`takeRemoteSnapshot(stream_id)` |**Parameter type change**: Replace `RemoteStreamKey` with `stream_id`. |
|`startFileRecording(stream_index, config, type)` |`startFileRecording(config, type)` |**Parameter removal**: Remove `stream_index`; keep the recording configuration and recording type. |
|`stopFileRecording(stream_index)` |`stopFileRecording()` |**Parameter removal**: Remove `stream_index`. |
|`setVideoWatermark(stream_index, path, config)` |`setVideoWatermark(path, config)` |**Parameter removal**: Remove `stream_index`; keep the image path and watermark configuration. |
|`clearVideoWatermark(stream_index)` |`clearVideoWatermark()` |**Parameter removal**: Remove `stream_index`. |


<span id="wtn-streams-formerly-public-streams"></span>
#### WTN Streams (Formerly Public Streams)

The former public\-stream APIs on the engine are removed. Obtain an `RTCWTNStream` instance by calling `getWTNStream()`, and migrate as follows:


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`startPlayPublicStream(public_stream_id)` |`getWTNStream().subscribeWTNAudioStream(stream_id, true)` and/or `subscribeWTNVideoStream(stream_id, true)` |**Object ownership change and interface split**: Obtain `RTCWTNStream` from the engine, then subscribe to WTN audio and video separately. Replace `public_stream_id` with `stream_id`; pass `true` to subscribe. |
|`stopPlayPublicStream(public_stream_id)` |`subscribeWTNAudioStream(stream_id, false)` and/or `subscribeWTNVideoStream(stream_id, false)` |**Operation merge**: Stop\-play is merged into the subscription methods. Pass `false` to unsubscribe from the required media types. |
|`setupPublicStreamVideo(public_stream_id, view, options?)` |`setupWTNRemoteVideo(stream_id, view, options?)` |**Object ownership and identifier changes**: Move the call from the engine to `RTCWTNStream`, and replace `public_stream_id` with `stream_id`. |
|`removePublicStreamVideo(public_stream_id)` |`removeWTNRemoteVideo(stream_id)` |**Object ownership and identifier changes**: Move the call to `RTCWTNStream`, and replace `public_stream_id` with `stream_id`. |
|`setPublicStreamVideoSink` / `unsetPublicStreamVideoSink` |`setWTNRemoteVideoSink` / `unsetWTNRemoteVideoSink` |**Interface rename and object ownership change**: Configure the custom WTN video sink on `RTCWTNStream` instead of the engine. |
|`setPublicStreamAudioPlaybackVolume` |`setWTNRemoteAudioPlaybackVolume` |**Interface rename and object ownership change**: Configure WTN playback volume on `RTCWTNStream`. |
|`startPushPublicStream` / `updatePublicStreamParam` / `stopPushPublicStream` |`startPushMixedStream` / `updatePushMixedStream` / `stopPushMixedStream` |**Interface merge and configuration replacement**: Public\-stream push is merged into mixed\-stream tasks. Replace `IPublicStreamParam` with `IMixedStreamConfig` and set `push_target_type` to `kMixedStreamPushTargetTypeToWTN`. |


WTN callbacks have moved to `RTCWTNStream`, including subscription state changes, first\-frame callbacks, SEI messages, data messages, and raw video frames.

<span id="push-to-cdn-and-stream-mixing"></span>
#### Push to CDN and Stream Mixing


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`startLiveTranscoding` / `updateLiveTranscoding` / `stopLiveTranscoding` |`startPushMixedStream` / `updatePushMixedStream` / `stopPushMixedStream` |**Interface replacement**: Replace the legacy transcoding task APIs and `ITranscoderParam` with the unified mixed\-stream APIs and `IMixedStreamConfig`. |
|`startPushMixedStreamToCDN` |`startPushMixedStream` |**Interface rename and target extension**: The method is no longer CDN\-specific. Set `IMixedStreamConfig.push_target_type` to select CDN or WTN. |
|`updatePushMixedStreamToCDN` |`updatePushMixedStream` |**Interface rename**: Update a task started by `startPushMixedStream` using the same task ID and the new `IMixedStreamConfig`. |
|`stopPushStreamToCDN` |`stopPushMixedStream` |**Interface replacement**: Use the mixed\-stream stop method. The optional `target_type` identifies the push destination when required. |
|`setupMixingVideo` / `removeMixingVideo` |Removed |**Interface removal**: Local rendering for client\-side mixed streams is no longer exposed. Remove these calls. |


`IMixedStreamConfig` has also changed:


* Added `push_target_type`, `push_wtn_stream_id`, `layout_mode`, `interpolation_mode`, and `background_image_url`.

* Removed `is_support_client_push_stream`, `expected_mix_type`, and `client_mix_config`.

* `user_config_extra_info` and `server_control_config` are now optional.


<span id="single-stream-push"></span>
#### Single\-Stream Push


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`startPushSingleStreamToCDN(task_id, param)` |`startPushSingleStream(task_id, param)` |**Interface rename and target extension**: Single\-stream push is no longer limited to CDN. Add `push_type`, `dest_info`, and `dest_info_size` to `PushSingleStreamParam` to select CDN or an RTC room. |
|`stopPushStreamToCDN(task_id)` |`stopPushSingleStream(task_id)` |**Interface rename**: Stop the destination\-independent single\-stream task using the same task ID. |


`PushSingleStreamParam` adds `push_type`, `dest_info`, and `dest_info_size`. Use `SingleStreamPushType` to select CDN or RTC as the destination.

<span id="sei-and-stream-synchronization"></span>
#### SEI and Stream Synchronization


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`sendSEIMessage(stream_index, message, repeat_count, mode)` |`sendSEIMessage(message, repeat_count, mode)` |**Parameter removal**: Remove `stream_index`; keep the SEI payload, repeat count, and per\-frame mode. |
|`StreamSycnInfoConfig` |`StreamSyncInfoConfig` |**Type rename**: Correct the misspelled type name. A compatibility alias remains in 3.60.1, but new code should use `StreamSyncInfoConfig`. |


<span id="other-api-changes"></span>
#### Other API Changes


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`getHotMusic(hot_types: number, filters)` |`getHotMusic(custom_hotlist_id: string[], filters)` |**Parameter replacement and type change**: Replace the numeric hot\-list type with an array of custom hot\-list IDs. The `filters` argument is unchanged. |
|`RTCRoom.updateSpatialPosition`, `updateSelfOrientation`, `updateListenerPosition`, and `updateListenerOrientation` |Removed |**Interface removal**: The room\-level spatial position and orientation update methods are no longer exposed. Remove these calls when upgrading. |


<span id="electron-3-60-1-callback-changes"></span>
### Callback Changes

<span id="room-and-stream-state"></span>
#### Room and Stream State


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`onRoomStateChanged(room_id, uid, state, extra_info)` |Removed |**Callback removal**: This room\-state callback is no longer exposed. Remove the listener and use the return values and other public room callbacks that apply to your workflow. |
|`onStreamStateChanged(room_id, uid, state, extra_info)` |`onVideoPublishStateChanged`, `onAudioPublishStateChanged`, `onVideoSubscribeStateChanged`, and `onAudioSubscribeStateChanged` |**Interface split and parameter replacement**: Split the general stream\-state callback by media type and publish/subscribe operation. Replace `room_id`, `uid`, and `extra_info` with `stream_id` and `StreamInfo`; handle the operation result through `state` and `reason`. |
|`onUserPublishStream(uid, type)` / `onUserUnpublishStream(uid, type, reason)` |`onUserPublishStreamVideo(stream_id, stream_info, is_publish)` and `onUserPublishStreamAudio(stream_id, stream_info, is_publish)` |**Interface split and operation merge**: Split the callback by audio and video, and merge publish/unpublish into `is_publish`. Replace `uid` with `stream_id` and `StreamInfo`; remove `MediaStreamType` and `StreamRemoveReason`. |
|`onUserPublishScreen(uid, type)` / `onUserUnpublishScreen(uid, type, reason)` |`onUserPublishStreamVideo(stream_id, stream_info, is_publish)` and `onUserPublishStreamAudio(stream_id, stream_info, is_publish)` |**Interface merge**: Remove the screen\-specific callbacks. Handle camera and screen streams through the same audio/video callbacks, use `StreamInfo.is_screen` to identify a screen stream, and use `is_publish` to distinguish publishing from removal. |
|`onStreamSubscribed(state_code, user_id, info)` |`onVideoSubscribeStateChanged(stream_id, stream_info, state, reason)` and `onAudioSubscribeStateChanged(stream_id, stream_info, state, reason)` |**Interface split and parameter replacement**: Split subscription results by audio and video. Replace `user_id` and `SubscribeConfig` with `stream_id` and `StreamInfo`; use `state` for the subscription state and `reason` for the failure or transition reason. |
|`onUserJoined(user_info, elapsed)` |`onUserJoined(user_info)` |**Parameter removal**: Remove `elapsed` from the callback handler. |
|`onRoomBinaryMessageReceived`, `onUserBinaryMessageReceived`, and `onUserBinaryMessageReceivedOutsideRoom` with `message: string` |The same callbacks with `message: Buffer` |**Parameter type change**: Change the binary\-message parameter from `string` to `Buffer`. Text\-message callbacks continue to use `string`; decode a binary buffer explicitly only when the application payload is text. |


Other callback signatures require the following changes:


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`onFirstLocalAudioFrame(index)` |`onFirstLocalAudioFrame()` |**Parameter removal**: Remove `StreamIndex`. |
|`onFirstLocalVideoFrameCaptured(index, info)` |`onFirstLocalVideoFrameCaptured(info)` |**Parameter removal**: Remove `StreamIndex`; `VideoFrameInfo` remains unchanged. |
|`onLocalVideoSizeChanged(index, info)` |`onLocalVideoSizeChanged(info)` |**Parameter removal**: Remove `StreamIndex`; `VideoFrameInfo` remains unchanged. |
|`onLocalVideoStateChanged(index, state, error)` |`onLocalVideoStateChanged(state, error)` |**Parameter removal**: Remove `StreamIndex`; keep the state and error parameters. |
|`onRecordingStateUpdate(type, state, error_code, info)` |`onRecordingStateUpdate(state, error_code, info)` |**Parameter removal**: Remove the `StreamIndex` parameter `type`. |
|`onRecordingProgressUpdate(type, process, info)` |`onRecordingProgressUpdate(process, info)` |**Parameter removal**: Remove the `StreamIndex` parameter `type`. |
|`onFaceDetectResult(result)` |`onFaceDetectResult(detect_result, face_count, rect, image_width, image_height, frame_timestamp_us)` |**Object flattening**: Replace the single `FaceDetectResult` object with its six fields as separate callback parameters. |
|`onMusicDetailResult(music_info, error_code)` where `music_info` is `MusicInfo` |The same callback where `music_info` is `MusicInfo \\| null` |**Parameter type change**: Handle `music_info` as nullable, especially when `error_code` indicates that music details could not be returned. |


The following callbacks are removed:


* Remove `onCreateRoomStateChanged`; no direct replacement is exposed.

* Replace `onScreenVideoFrameSendStateChanged`, `onScreenVideoFramePlayStateChanged`, `onScreenAudioFrameSendStateChanged`, and `onScreenAudioFramePlayStateChanged` with the unified audio/video frame send/play callbacks and inspect `StreamInfo.is_screen`.

* Remove `onHttpProxyState`, `onHttpsProxyState`, and `onSocks5ProxyState`; use `onLocalProxyStateChanged` for local proxy connection state.


<span id="stream-based-callback-parameters"></span>
#### Stream\-Based Callback Parameters

Callbacks that identify a remote stream now use `stream_id` and `StreamInfo`. Apply the following parameter changes to callback handlers and use `stream_id` as the application\-side lookup key.


|Affected callbacks |3.56.1 parameters |3.60.1 parameters |Change description |
|---|---|---|---|
|`onFirstRemoteAudioFrame`, `onFirstRemoteVideoFrameDecoded`, `onRemoteVideoSizeChanged`, `onRemoteAudioStateChanged`, and `onRemoteVideoStateChanged` |`RemoteStreamKey` |`stream_id`, `stream_info` |**Parameter replacement**: Replace `RemoteStreamKey` with the stream ID and the complete `StreamInfo` object. Existing state, reason, and frame\-information parameters remain after the two new parameters. |
|`onSEIMessageReceived`, `onSEIStreamUpdate`, and `onStreamSyncInfoReceived` |`RemoteStreamKey` |`stream_id`, `stream_info` |**Parameter replacement**: Replace `RemoteStreamKey` with `stream_id` and `StreamInfo`. Keep the message, event, stream type, or data parameter. |
|`onTakeRemoteSnapshotResult` |`task_id`, `RemoteStreamKey`, `image`, `error_code` |`task_id`, `stream_id`, `stream_info`, `image`, `error_code` |**Parameter replacement**: Replace `RemoteStreamKey` with `stream_id` and `StreamInfo`; the task, image, and error parameters are unchanged. |
|`onRemoteUserAudioFrame` |`RemoteStreamKey`, `audio_frame` |`stream_id`, `stream_info`, `audio_frame` |**Parameter replacement**: Replace `RemoteStreamKey` with `stream_id` and `StreamInfo`; keep the audio frame parameter. |
|`onAudioFrameSendStateChanged`, `onVideoFrameSendStateChanged`, `onAudioFramePlayStateChanged`, and `onVideoFramePlayStateChanged` |`room_id`, `user`, `state` |`stream_id`, `stream_info`, `user`, `state` |**Parameter replacement and addition**: Replace `room_id` with `stream_id` and add `StreamInfo`. The user and state parameters remain unchanged. The former screen\-specific versions of these callbacks are merged into these four callbacks. |


<span id="mixed-and-single-stream-tasks"></span>
#### Mixed and Single\-Stream Tasks


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`onStreamMixingEvent(event, task_id, error, mix_type)` / `onMixingEvent(event, task_id, error, mix_type)` |`onMixedStreamEvent(info, event, error_code)` |**Callback merge and parameter replacement**: Merge the two mixed\-stream result callbacks. Replace the separate `task_id` and `mix_type` parameters with `MixedStreamTaskInfo`; replace `StreamMixingEvent` and the old error value with `MixedStreamTaskEvent` and `MixedStreamTaskErrorCode`. |
|`onStreamPushEvent(event, task_id, error)` |`onSingleStreamEvent(task_id, event, error_code)` |**Interface rename and parameter type change**: Rename the callback, keep `task_id`, replace `SingleStreamPushEvent` with `SingleStreamTaskEvent`, and replace the numeric error with `SingleStreamTaskErrorCode`. The parameter order also changes to place `task_id` first. |
|`onMixingVideoFrame`, `onMixingAudioFrame`, and `onMixingDataFrame` |Removed |**Callback removal**: Client\-side mixed\-stream frame callbacks are no longer exposed. Remove these listeners. |


<span id="wtn-callbacks"></span>
#### WTN Callbacks

Register WTN playback callbacks on the `RTCWTNStream` instance returned by `getWTNStream()`, rather than on the engine.


|3.56.1 |3.60.1 |Change description |
|---|---|---|
|`onPlayPublicStreamResult(public_stream_id, error_code)` |`onWTNVideoSubscribeStateChanged(stream_id, state_code, reason)` and `onWTNAudioSubscribeStateChanged(stream_id, state_code, reason)` |**Interface split and state\-model replacement**: Split the playback result by audio and video. Replace `public_stream_id` with `stream_id`, and replace `PublicStreamErrorCode` with a subscription state plus a state\-change reason. |
|`onFirstPublicStreamAudioFrame(public_stream_id)` |`onWTNFirstRemoteAudioFrame(stream_id)` |**Interface rename and parameter rename**: Rename the callback and replace `public_stream_id` with `stream_id`. |
|`onFirstPublicStreamVideoFrameDecoded(public_stream_id, info)` |`onWTNFirstRemoteVideoFrameDecoded(stream_id, info)` |**Interface rename and parameter rename**: Rename the callback and replace `public_stream_id` with `stream_id`. `VideoFrameInfo` is unchanged. |
|`onPublicStreamSEIMessageReceived(public_stream_id, message, source_type)` |`onWTNSEIMessageReceived(stream_id, channel_id, message, message_length)` |**Interface rename and parameter replacement**: Replace `public_stream_id` with `stream_id`; replace the string message and `source_type` with `channel_id`, a `Uint8Array` payload, and `message_length`. |
|`onPublicStreamDataMessageReceived(public_stream_id, message, source_type)` |`onWTNDataMessageReceived(stream_id, message, source_type)` |**Interface rename and parameter rename**: Replace `public_stream_id` with `stream_id`. The `Uint8Array` message and source parameter remain unchanged. |
|`onPublicStreamVideoFrame(frame)` |`onWTNVideoFrame(frame)` |**Interface rename and object ownership change**: Register the renamed raw\-frame callback on `RTCWTNStream`. The `IVideoFrame` parameter is unchanged. |
|`onPushPublicStreamResult(room_id, public_stream_id, error_code)` |`onMixedStreamEvent(info, event, error_code)` |**Callback replacement**: WTN push is handled as a mixed\-stream push task. Replace the public\-stream push result callback with the unified mixed\-stream task callback and read the task identity and target information from `MixedStreamTaskInfo`. |


<span id="electron-3-60-1-type-changes"></span>
### Type Changes


|Type |Change description |
|---|---|
|`EngineConfig` |**Parameter object addition**: Create an `EngineConfig` containing `app_id` and `parameters`, and pass it to `createRTCEngine` instead of passing the two values separately. |
|`StreamInfo` |**Stream metadata replacement**: Use `StreamInfo` with `stream_id`, `room_id`, `user_id`, and `is_screen` wherever callbacks previously returned `RemoteStreamKey` or separate room and user IDs. |
|`RTCRoomConfig` |**Field additions and removals**: Add `live_mode`, `is_auto_publish_audio`, `is_auto_publish_video`, and `stream_id`. Replace `is_auto_publish` with the two media\-specific fields, and remove `remote_video_config`. |
|`RoomLiveMode` |**Enum addition**: Use this enum for the new `RTCRoomConfig.live_mode` field and `setLiveMode`; select co\-host or solo\-host mode explicitly where required. |
|`VideoEncoderConfig` |**Field addition**: Add `key_frame_interval_ms` when a custom key\-frame interval is required. Use `0` to let the encoder determine the interval. |
|`IVideoFrame` |**Field additions and removal**: Add `is_screen` and optional `stream_id` handling. Replace any reads of `public_stream_id` with `stream_id` for WTN frames. |
|`LocalVideoSinkConfig` / `RemoteVideoSinkConfig` |**Configuration addition**: Supply these new objects to local and remote video\-sink APIs to configure frame position, rotation, mirroring, or pixel format. |
|`ExternalVideoFrame` / `ExternalAudioFrame` |**Frame type addition**: Build these structures when passing application\-captured frames to `pushExternalVideoFrame` or `pushExternalAudioFrame`. |
|`MixedStreamTaskEvent` / `MixedStreamTaskErrorCode` |**Type replacement**: Replace `StreamMixingEvent` and `StreamMixingErrorCode` in mixed\-stream callback handlers with the new task event and error enums. |
|`SingleStreamTaskEvent` / `SingleStreamTaskErrorCode` |**Type replacement**: Replace `SingleStreamPushEvent` and numeric error handling in single\-stream callback handlers with the new task event and error enums. |
|`VoiceChangerType` / `VoiceReverbType` |**Parameter type replacement**: Replace numeric literals passed to the voice changer and reverb methods with members of these enums. |
|`StreamSyncInfoConfig` |**Type rename**: Replace `StreamSycnInfoConfig` with the corrected name. A compatibility alias remains in 3.60.1, but new code should use `StreamSyncInfoConfig`. |
|`EffectBeautyMode` |**Enum member rename**: Replace `kEffectBeautyModeWhite`, `kEffectBeautyModeSmooth`, and `kEffectBeautyModeSharpen` with `kEffectBeautyWhite`, `kEffectBeautySmooth`, and `kEffectBeautySharpen`. |
|`CapturePreference` |**Enum member rename**: Replace `KAuto`, `KManual`, and `KAutoPerformance` with `kAuto`, `kManual`, and `kAutoPerformance`. |
|`LogConfig` |**Required\-field change**: Always provide `log_level` and `log_file_size`; both fields are required in 3.60.1. |
|`LocalAudioPropertiesInfo` |**Field removal**: Remove application reads of `stream_index`. |
|`RemoteAudioPropertiesInfo` |**Field replacement**: Replace `stream_key` reads with `stream_id` and `stream_info`. |
|`SubtitleMessage` |**Field additions**: Handle `language` and `mode` in subtitle results. |
|`SubscribeState` |**Enum simplification**: Replace the four success and failure states with `kSubscribeStateSubscribed` and `kSubscribeStateUnsubscribed`. Read the callback's `reason` parameter to distinguish failure causes. |
|Device information types |**Type removal and return\-shape change**: Remove dependencies on `VideoDeviceInfo`, `AudioDeviceInfo`, `MediaDeviceState`, and their supporting enums. Device enumeration now returns objects containing only `device_name` and `device_id`; device\-state callbacks use a numeric state. |


The following types are removed because their corresponding features have moved or been redesigned: `RemoteStreamKey`, `PauseResumeControlMediaType`, `ScreenVideoEncoderConfig`, `ITranscoderParam`, legacy transcoder types, public\-stream types, `AudioMixingConfig`, `StreamMixingEvent`, `StreamMixingErrorCode`, and `SingleStreamPushEvent`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>RemoteAudioState</code> values changed: <code>kRemoteAudioStateFrozen</code> changed from <code>1</code> to <code>3</code>, and <code>kRemoteAudioStateFailed</code> changed from <code>2</code> to <code>4</code>. Do not persist or compare the old numeric values.</div>


<span id="mixed-stream-configuration-changes"></span>
#### Mixed\-Stream Configuration Changes

`MixedStreamLayoutRegionConfig` has breaking field changes: **Field replacement**: Replace `region_id`, `width_proportion`, and `height_proportion` with `user_id`, `width`, and `height`. **Field additions**: Set `source_crop`, `alternate_image_fill_mode`, and `alternate_image_url` when source cropping or fallback images are required.

`MixedStreamServerControlConfig` has **field additions and required\-field changes**: Add `media_type` and `push_stream_mode`. Its existing volume\-indication and SEI fields are required in the 3.60.1 TypeScript declaration, so add explicit values to configuration objects that previously omitted them.

<span id="electron-3-60-1-error-code-changes"></span>
### Error Code Changes


* `WarningCode.kWarningCodePublishStreamForbiden` was corrected to `kWarningCodePublishStreamForbidden`.

* Added `kWarningCodeSubscribeStreamForbidden`.

* Mixed\-stream and single\-stream tasks now use `MixedStreamTaskErrorCode` and `SingleStreamTaskErrorCode`. Update task\-result handling together with the corresponding callbacks.

* Added `SnapshotErrorCode` for snapshot\-to\-file operations.


<span id="electron-3-60-1-new-interfaces"></span>
### New Interfaces

The following capabilities are new in 3.60.1 and do not replace interfaces in 3.56.1:


|Capability |New interfaces or fields |Description |
|---|---|---|
|Room and stream metadata |`RTCRoomConfig.stream_id`, `getCallId`, and `setStreamExtraInfo` |Assigns a custom local stream ID, obtains the call ID, and updates extra information for a published stream. |
|Room events |`onRoomWarning`, `onRoomEvent`, `onAVSyncEvent`, and `onRoomStreamExtraInfoUpdate` |Reports room warnings, room events, audio\-video synchronization events, and stream\-extra\-information updates. |
|Live mode |`RTCRoomConfig.live_mode` and `setLiveMode` |Selects or changes co\-host or solo\-host live mode. |
|Video frame sinks |`setLocalVideoSink`, `setRemoteVideoSink`, and the corresponding unset methods |Delivers local or remote video frames to a custom renderer. |
|Remote key\-frame request |`requestRemoteVideoKeyFrame` |Requests a new key frame for a subscribed remote video stream. |
|External capture |`setVideoSourceType`, `pushExternalVideoFrame`, `setAudioSourceType`, and `pushExternalAudioFrame` |Supplies application\-captured audio and video frames to the SDK. |
|Capture control |`setScreenCaptureVolume`, `muteAudioCapture`, and `muteScreenAudioCapture` |Controls screen\-capture volume and mutes captured audio without stopping capture. |
|Alpha\-channel video |`enableAlphaChannelVideoEncode` and `disableAlphaChannelVideoEncode` |Encodes the Alpha channel of externally supplied RGBA video. |
|Video encoding |`VideoEncoderConfig.key_frame_interval_ms` |Configures the key\-frame interval. A value of `0` lets the encoder choose the interval. |
|Low\-light enhancement |`setLowLightAdjusted` |Enables or disables low\-light video enhancement. |
|Snapshot files |`takeLocalSnapshotToFile` and `takeRemoteSnapshotToFile` |Saves a local or remote video snapshot directly to a file. |
|Live\-push SEI |`sendLivePushSEIMessage` |Sends Key\-Value SEI data in solo\-host live mode. |
|Custom\-source media playback |`RTCMediaPlayer.openWithCustomSource` and `pushExternalAudioFrame` |Plays PCM audio supplied by the application through a media player. |


<span id="electron-3-60-1-deleted-interfaces"></span>
### Deleted or Deprecated Interfaces

Before removing 3.56.1 from your project, verify that your application no longer uses:


* `RTCVideo`, `createRTCVideo`, or `destroyRTCVideo`.

* Screen\-specific publish, subscribe, and rendering APIs.

* Public\-stream APIs and callbacks.

* `startLiveTranscoding`, `updateLiveTranscoding`, and `stopLiveTranscoding`.

* Engine\-level legacy audio\-mixing APIs.

* `setupLocalScreen`, `setupRemoteScreen`, and their removal methods.

* Proxy\-state callbacks for HTTP, HTTPS, and SOCKS5 proxies.

* Legacy engine callback names such as `onStreamMixingEvent`, `onStreamPushEvent`, and `onMixingVideoFrame`.


<span id="electron-3-60-1-important-notes"></span>
### Important Notes


* Treat `streamId` as the primary key for stream\-related application state. Do not continue keying remote views only by user ID because one user can publish different streams.

* Update all `joinRoom` calls. Omitting `user_visibility` causes a TypeScript signature error and can lead to incorrect publishing behavior if bypassed at runtime.

* Update binary\-message handlers to accept `Buffer`. Convert the buffer explicitly only when your business payload is text.

* Do not migrate public\-stream playback by renaming methods only. The callbacks and object lifecycle have moved to `RTCWTNStream`.

* Re\-test publishing, subscription, screen sharing, rendering, mixed\-stream push, and reconnect scenarios after migration because they are affected by the new stream model.


<span id="_3-56"></span>
## 3.56

<span id="api"></span>
### API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Audio management<br><br><br>* [enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-85532#enumerateaudiocapturedevices)<br><br>* [enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-85532#enumerateaudioplaybackdevices) |Wait until getting the result list. |The method now times out after 10 seconds and returns an empty list. |None |
|Modified |Video management<br><br>[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-85532#enumeratevideocapturedevices) |Wait until getting the result list. |The method now times out after 10 seconds and returns an empty list. |None |
|Modified |Engine Management |`createRTCVideo(app_id: string, document_path: string, parameters: string) => number` |`createRTCVideo(app_id: string, parameters: string): number`<br><br>`setLogConfig` |Instead of passing `document_path` when calling `createRTCVideo` you can configure the logs by calling `setLogConfig`. |
|Replaced |Audio mixing |`RTCVideo` |* `RTCMediaPlayer`<br><br>* `RTCAudioEffectPlayer` |The audio mixing methods have been moved to `RTCMediaPlayer` and `RTCAudioEffectPlayer` from `RTCVideo`. Please refer to the table below for details. Typically, for audio clips less than 20 seconds, you should use `RTCAudioEffectPlayer`. For clips longer than that, use `RTCMediaPlayer`. |


The table below lists the deprecated audio mixing methods along with their replacement methods.


|Brief |Deprecated methods |`RTCAudioEffectPlayer` |`RTCMediaPlayer` | |
|---|---|---|---|---|
|Load |`preloadAudioMixing`, `unloadAudioMixing` |[preload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-preload), [unload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-unload) |[open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open), [unloadAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-unloadall) | |
|Control |`startAudioMixing`, `stopAudioMixing`, `stopAllAudioMixing`, `pauseAudioMixing`, `pauseAllAudioMixing`, `resumeAudioMixing`, `resumeAllAudioMixing` |[start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start), [stop](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-stop), [stopAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-stopall), [pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-pause), [pauseAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-pauseall), [resume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-resume), [resumeAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-resumeall) |[start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start), [stop](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-stop), [pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-pause),[resume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-resume) | |
|Duration and position |`setAudioMixingPosition`, `getAudioMixingCurrentPosition`, `getAudioMixingDuration` |[setPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setposition), [getPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-getposition), [getDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-getduration) |[setPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setposition), [getPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getposition), [getTotalDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-gettotalduration), [getPlaybackDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getplaybackduration) | |
|Volume |`setAudioMixingVolume` |[setVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setvolume), [setVolumeAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setvolumeall), [getVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-getvolume) |[setVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setvolume), [getVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getvolume) | |
|Pitch |`setAudioMixingPitch` |Not applicable |[setAudioPitch](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setaudiopitch) | |
|Audio channel |`setAudioMixingDualMonoMode` |Not applicable |[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setaudiodualmonomode) | |
|Audio track |`getAudioTrackCount`, `selectAudioTrack` |Not applicable |[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getaudiotrackcount), [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-selectaudiotrack)<br><br>`Index` begins from `0`. | |
|Speed |`setAudioMixingPlaybackSpeed` |Not applicable |[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setplaybackspeed) | |
|Callback interval |`setAudioMixingProgressInterval` |Not applicable |[setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setprogressinterval) | |
|Loudness |`setAudioMixingLoudness` |Not applicable |[setLoudness](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setloudness) | |
|Callback |`onAudioMixingStateChanged` |[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-seteventhandler), [onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcaudioeffectplayercallback-onaudioeffectplayerstatechanged) |[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-seteventhandler), [onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerstatechanged), [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress) | |


<span id="callback"></span>
### Callback


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Parameter change |Message |`virtual void onLogout()` |virtual void onLogout(int reason) |New parameter `reason` for `onLogout` to indicate the reason for the user logout. Refer to [LogoutReason](https://docs.byteplus.com/en/docs/12/docs-85535#logoutreason) for details. |


<span id="data-type"></span>
### Data type


|Change |Data type |Note |
|---|---|---|
|Member change |[AudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-85535#audiopropertiesinfo) |New member `voicePitch` for the vocal pitch of the local user |
|Renaming |[IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#iaudioframe) |The member `type` changed to `frame_type`. |
|Modified |[format](https://docs.byteplus.com/en/docs/12/docs-85535#ivideoframe-format) |The type was changed to an enumeration class named [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/docs-85535#videopixelformat). |
|Member change |[IDataFrame](https://docs.byteplus.com/en/docs/12/docs-85535#idataframe) |The `u32_data_size` member has been removed. |


<span id="uniform-code-style"></span>
#### Uniform Code Style

This version standardizes all enumeration values and member variable names to align with the native SDKs, improving code consistency and usability.


1. Enumeration



|Enumeration class |3.52 and previous |3.56 |
|---|---|---|
|`SEICountPerFrame` |* `kSingleSEIPerFrame`<br><br>* `kMultiSEIPerFrame` |* `kSEICountPerFrameSingle`<br><br>* `kSEICountPerFrameMulti` |
|`RecordingType` |* `kRecordAudioOnly`<br><br>* `kRecordVideoOnly`<br><br>* `kRecordVideoAndAudio` |* `kRecordingTypeAudioOnly`<br><br>* `kRecordingTypeVideoOnly`<br><br>* `kRecordingTypeVideoAndAudio` |
|`VirtualBackgroundSourceType` |* `kVirtualBackgroundSourceColor`<br><br>* `kVirtualBackgroundSourceImage` |* `kVirtualBackgroundSourceTypeColor`<br><br>* `kVirtualBackgroundSourceTypeImage` |
|`ZoomConfigType` |* `kZoomFocusOffset`<br><br>* `kZoomMoveOffset` |* `kZoomConfigTypeFocusOffset`<br><br>* `kZoomConfigTypeMoveOffset` |
|`ZoomDirectionType` |* `kCameraMoveLeft`<br><br>* `kCameraMoveRight`<br><br>* `kCameraMoveUp`<br><br>* `kCameraMoveDown`<br><br>* `kCameraZoomOut`<br><br>* `kCameraZoomIn`<br><br>* `kCameraReset` |* `kZoomDirectionTypeMoveLeft`<br><br>* `kZoomDirectionTypeMoveRight`<br><br>* `kZoomDirectionTypeMoveUp`<br><br>* `kZoomDirectionTypeMoveDown`<br><br>* `kZoomDirectionTypeZoomOut`<br><br>* `kZoomDirectionTypeZoomIn`<br><br>* `kZoomDirectionTypeReset` |
|`AudioFrameCallbackMethod` |* `kAudioFrameCallbackRecord`<br><br>* `kAudioFrameCallbackPlayback`<br><br>* `kAudioFrameCallbackMixed`<br><br>* `kAudioFrameCallbackRemoteUser`<br><br>* `kAudioFrameCallbackRecordScreen` |* `kRecord`<br><br>* `kPlayback`<br><br>* `kMixed`<br><br>* `kRemoteUser`<br><br>* `kRecordScreen` |
|`AudioAlignmentMode` |* `kAudioAlighmentModeOff`<br><br>* `kAudioAlighmentModeAudioMixing` |* `kAudioAlignmentModeOff`<br><br>* `kAudioAlignmentModeAudioMixing` |
|`SetRoomExtraInfoResult` |* `kSetRoomExtraInfoErrorNotJoinRoom`<br><br>* `kSetRoomExtraInfoErrorKeyIsNull`<br><br>* `kSetRoomExtraInfoErrorValueIsNull`<br><br>* `kSetRoomExtraInfoResultUnknow`<br><br>* `kSetRoomExtraInfoErrorKeyIsEmpty`<br><br>* `kSetRoomExtraInfoErrorTooOften`<br><br>* `kSetRoomExtraInfoErrorSilentUser`<br><br>* `kSetRoomExtraInfoErrorKeyTooLong`<br><br>* `kSetRoomExtraInfoErrorValueTooLong`<br><br>* `kSetRoomExtraInfoErrorServer`<br><br>* `kSetRoomExtraInfoResultSuccess` |* `kSetRoomExtraInfoResultErrorNotJoinRoom`<br><br>* `kSetRoomExtraInfoResultErrorKeyIsNull`<br><br>* `kSetRoomExtraInfoResultErrorValueIsNull`<br><br>* `kSetRoomExtraInfoResultResultUnknow`<br><br>* `kSetRoomExtraInfoResultErrorKeyIsEmpty`<br><br>* `kSetRoomExtraInfoResultErrorTooOften`<br><br>* `kSetRoomExtraInfoResultErrorSilentUser`<br><br>* `kSetRoomExtraInfoResultErrorKeyTooLong`<br><br>* `kSetRoomExtraInfoResultErrorValueTooLong`<br><br>* `kSetRoomExtraInfoResultErrorServer`<br><br>* `kSetRoomExtraInfoSuccess` |
|`HardwareEchoDetectionResult` |* `kHardwareEchoDetectionCanceled`<br><br>* `kHardwareEchoDetectionUnknown`<br><br>* `kHardwareEchoDetectionNormal`<br><br>* `kHardwareEchoDetectionPoor` |* `kHardwareEchoDetectionResultCanceled`<br><br>* `kHardwareEchoDetectionResultUnknown`<br><br>* `kHardwareEchoDetectionResultNormal`<br><br>* `kHardwareEchoDetectionResultPoor` |
|`StreamMixingEvent` |* `kStreamMixingStart`<br><br>* `kStreamMixingStartSuccess`<br><br>* `kStreamMixingStartFailed`<br><br>* `kStreamMixingUpdate`<br><br>* `kStreamMixingUpdateSuccess`<br><br>* `kStreamMixingUpdateFailed`<br><br>* `kStreamMixingStop`<br><br>* `kStreamMixingStopSuccess`<br><br>* `kStreamMixingStopFailed`<br><br>* `kStreamMixingChangeMixType`<br><br>* `kStreamMixingFirstAudioFrameByClientMix`<br><br>* `kStreamMixingFirstVideoFrameByClientMix`<br><br>* `kStreamMixingUpdateTimeout`<br><br>* `kStreamMixingStartTimeout`<br><br>* `kStreamMixingRequestParamError`<br><br>* `kStreamMixingMixImageEvent` |* `kStreamMixingEventStart`<br><br>* `kStreamMixingEventStartSuccess`<br><br>* `kStreamMixingEventStartFailed`<br><br>* `kStreamMixingEventUpdate`<br><br>* `kStreamMixingEventUpdateSuccess`<br><br>* `kStreamMixingEventUpdateFailed`<br><br>* `kStreamMixingEventStop`<br><br>* `kStreamMixingEventStopSuccess`<br><br>* `kStreamMixingEventStopFailed`<br><br>* `kStreamMixingEventChangeMixType`<br><br>* `kStreamMixingEventFirstAudioFrameByClientMix`<br><br>* `kStreamMixingEventFirstVideoFrameByClientMix`<br><br>* `kStreamMixingEventUpdateTimeout`<br><br>* `kStreamMixingEventStartTimeout`<br><br>* `kStreamMixingEventRequestParamError`<br><br>* `kStreamMixingEventMixImageEvent` |
|`SingleStreamPushEvent` |* `kSingleStreamPushStart`<br><br>* `kSingleStreamPushSuccess`<br><br>* `kSingleStreamPushFailed`<br><br>* `kSingleStreamPushStop`<br><br>* `kSingleStreamPushTimeout`<br><br>* `kSingleStreamPushParamError` |* `kSingleStreamPushEventStart`<br><br>* `kSingleStreamPushEventSuccess`<br><br>* `kSingleStreamPushEventFailed`<br><br>* `kSingleStreamPushEventStop`<br><br>* `kSingleStreamPushEventTimeout`<br><br>* `kSingleStreamPushEventParamError` |



2. Member variable



|Member variable |3.52 and previous |3.56 |
|---|---|---|
|`SourceCrop` |* `LocationX`<br><br>* `LocationY`<br><br>* `WidthProportion`<br><br>* `HeightProportion` |* `location_x`<br><br>* `location_y`<br><br>* `width_proportion`<br><br>* `height_proportion` |
|`EchoTestConfig` |* `audioPropertiesReportInterval`<br><br>* `roomId` |* `audio_properties_report_interval`<br><br>* `room_id` |
|`VideoEncoderConfig` |* `frameRate`<br><br>* `maxBitrate`<br><br>* `minBitrate`<br><br>* `encoderPreference` |* `frame_rate`<br><br>* `max_bitrate`<br><br>* `min_bitrate`<br><br>* `encoder_preference` |
|`ScreenCaptureSourceInfo` |* `primaryMonitor` |* `primary_monitor` |
|`ScreenVideoEncoderConfig` |* `frameRate`<br><br>* `maxBitrate`<br><br>* `minBitrate`<br><br>* `encoderPreference` |* `frame_rate`<br><br>* `max_bitrate`<br><br>* `min_bitrate`<br><br>* `encoder_preference` |
|`VideoCaptureConfig` |* `capturePreference`<br><br>* `frameRate` |* `capture_preference`<br><br>* `frame_rate` |
|`RTCWatermarkConfig` |* `visibleInPreview`<br><br>* `positionInLandscapeMode`<br><br>* `positionInPortraitMode` |* `visible_in_preview`<br><br>* `position_in_landscape_mode`<br><br>* `position_in_portrait_mode` |
|`MixedStreamVideoConfig` |`enable_Bframe` |`enable_bframe` |
|`RtcRoomStats` |* `txLostrate`<br><br>* `rxLostrate` |* `tx_lostrate`<br><br>* `rx_lostrate` |


<span id="error-code"></span>
### Error Code


|Type |Error code |Note |
|---|---|---|
|Enumeration removal |`ErrorCode` |Removed `kErrorCodeOverScreenPublishLimit = -1081` and `kErrorCodeOverVideoPublishLimit = -1082` |
|Renaming |[AudioRecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#audiorecordingerrorcode)<br><br><br>* `kAudioRecordingErrorNotInRoom`<br><br>* `kAudioRecordingAlreadyStarted`<br><br>* `kAudioRecordingNotStarted` |Changed to:<br><br><br>* `kAudioRecordingErrorCodeNotInRoom`<br><br>* `kAudioRecordingErrorCodeAlreadyStarted`<br><br>* `kAudioRecordingErrorCodeNotStarted` |
|Renaming |[StreamMixingErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#streammixingerrorcode)<br><br><br>* `kStreamMixingErrorOK`<br><br>* `kStreamMixingErrorBase`<br><br>* `kStreamMixingErrorInvalidParam`<br><br>* `kStreamMixingErrorInvalidState`<br><br>* `kStreamMixingErrorInvalidOperator`<br><br>* `kStreamMixingErrorTimeout`<br><br>* `kStreamMixingErrorInvalidParamByServer`<br><br>* `kStreamMixingErrorSubTimeoutByServer`<br><br>* `kStreamMixingErrorInvalidStateByServer`<br><br>* `kStreamMixingErrorAuthenticationByCDN`<br><br>* `kStreamMixingErrorTimeoutBySignaling`<br><br>* `kStreamMixingErrorMixImageFail`<br><br>* `kStreamMixingErrorUnKnownByServer` |Changed to:<br><br><br>* `kStreamMixingErrorCodeOK`<br><br>* `kStreamMixingErrorCodeBase`<br><br>* `kStreamMixingErrorCodeInvalidParam`<br><br>* `kStreamMixingErrorCodeInvalidState`<br><br>* `kStreamMixingErrorCodeInvalidOperator`<br><br>* `kStreamMixingErrorCodeTimeout`<br><br>* `kStreamMixingErrorCodeInvalidParamByServer`<br><br>* `kStreamMixingErrorCodeSubTimeoutByServer`<br><br>* `kStreamMixingErrorCodeInvalidStateByServer`<br><br>* `kStreamMixingErrorCodeAuthenticationByCDN`<br><br>* `kStreamMixingErrorCodeTimeoutBySignaling`<br><br>* `kStreamMixingErrorCodeMixImageFail`<br><br>* `kStreamMixingErrorCodeUnKnownByServer` |


<span id="_3-52"></span>
## 3.52

<span id="api"></span>
### API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Engine Management |`feedback` |[feedback](https://docs.byteplus.com/en/docs/12/docs-85532#feedback) |The data types of the parameters are changed. |
|Replaced |Push to CDN |`startLiveTranscoding` |[startPushMixedStreamToCDN](https://docs.byteplus.com/en/docs/12/docs-85532#startpushmixedstreamtocdn) |None |
|Replaced |Push to CDN |`stopLiveTranscoding` |[stopPushStreamToCDN](https://docs.byteplus.com/en/docs/12/docs-85532#stoppushstreamtocdn) |None |
|Replaced |Push to CDN |`updateLiveTranscoding` |[updatePushMixedStreamToCDN](https://docs.byteplus.com/en/docs/12/docs-85532#updatepushmixedstreamtocdn) |None |


<span id="error-code"></span>
### Error Code


1. Added new error codes: `kErrorCodeJoinRoomRoomForbidden=-1025` and `kErrorCodeJoinRoomUserForbidden =-1026`. The client SDK receives the error code when the user is banned in a specific room by the RTC server and fails to join the room or is removed from the room.

2. `kErrorCodeOverScreenPublishLimit=-1081` is deprecated and replaced by `kErrorCodeOverStreamPublishLimit=-1080`.


<span id="others"></span>
### Others

If you are using license\-related features, when you update the RTC SDK to this version or above, you need to include the corresponding extension. If not, you'll receive [onExtensionAccessError](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onextensionaccesserror).

<span id="_3-50-3"></span>
## 3.50.3

Class names changed.


* From `veRTCVideo` to `RTCVideo`

* From `veRTCRoom` to `RTCRoom`.


<span id="api"></span>
### API


|Change |Module |Previous |Current |Note |
|---|---|---|---|---|
|Return value change |Room management |`joinRoom` returns:<br><br><br>* `-1`: Invalid parameters.<br><br>* `-2`: Already in a room. |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#joinroom) returns:<br><br><br>* `-1`: Failure.<br><br>* `-2`: Invalid parameters.<br><br>* `-4`: Already in a room. |`0` continues to represent success. |
| |Network management |`stopEchoTest` returns `-1` denoting failure because no echo test is in progress. |[stopEchoTest](https://docs.byteplus.com/en/docs/12/docs-85532#stopechotest) returns `-3` denoting failure because no echo test is in progress. | |
| |Engine management |`setBusinessId` returns:<br><br><br>* `< 0`: Failure. Refer to `BusinessCheckCode`.<br><br>* `-6001`: Already in a room.<br><br>* `-6002`: Invalid parameters. |[setBusinessId](https://docs.byteplus.com/en/docs/12/docs-85532#setbusinessid) returns:<br><br><br>* `< 0`: Failure. Refer to `ReturnStatus`<br><br>* `-2`: Invalid parameters. | |
|Replaced |Video management |`registerFaceDetectionObserver` |* enableFaceDetection<br><br>* disableFaceDetection |Decoupled face detection and video effects to improve usability. |
|Deprecated |Range audio |`registerRangeAudioObserver`<br><br>`onRangeAudioInfor` |None |Previously, in the manual subscription scenario, you had to register the range audio callback to obtain the attenuation coefficient and set the volume.<br><br>From this version onwards, the RTC SDK automatically adjusts attenuation for both manual and automatic subscriptions. |
|Replaced |Audio management |`muteAudioPlayback` |`setPlaybackVolume` |To mute the audio playback, set the playback volume to 0. |
|Modified |Screen Sharing |public setVideoEncoderConfig(solutions: VideoEncoderConfig[]): number |setScreenVideoEncoderConfig(screenSolution: VideoEncoderConfig): any; |The data type of the parameter changed to ScreenVideoEncoderConfig. |
|Replaced |Video Processing |* checkLicense<br><br>* setAlgoModelPath |initCVResource |None |
| | |enableEffect |* enableVideoEffect<br><br>* disableVideoEffect |None |
| | |updateNode |`updateEffectNode` |None |
| | |setBackgroundSticker |* enableVirtualBackground<br><br>* disableVirtualBackground |None |
|Modified |Message |(stream_index: number, message: Uint8Array, repeat_count: number) =\> number |public sendSEIMessage(stream_index: number, message: Uint8Array, repeat_count: number, mode: SEICountPerFrame): number |Added Multi\-SEI mode. When you send multiple SEI messages in 1 frame, they will be sent together in the next frame. |


<span id="callback"></span>
### Callback


|Change |Module |Previous |Current |Note |
|---|---|---|---|---|
|Parameter change |Message |onPublicStreamSEIMessageReceived(public_stream_id: string, message: string) =\> void |onPublicStreamSEIMessageReceived(public_stream_id: string, source_type: SEIMessageSourceType) =\> void |Added new parameter: source_type |
|Deprecated |Audio management |* onRemoteAudioStateChanged<br><br>* onRemoteVideoStateChanged |None |None |
|Replaced |Push to CDN |onStreamMixingVideoFrame<br><br>onStreamMixingAudioFrame<br><br>onStreamMixingDataFrame |onMixingVideoFrame<br><br>onMixingAudioFrame<br><br>onMixingDataFrame |None |


<span id="data-type"></span>
### Data type


|Change |Data type |Note |
|---|---|---|
|Member change |FaceDetectResult |Added new member: frame_timestamp_us |
|Member change |TranscoderAudioParam |Added new member: audio_codec_type |
|Member change |TranscoderVideoParam |Added new member: bFrame<br><br>The `lowLatency` member has been removed.<br><br>The `video_codec_profile` member is replaced with `video_codec_type`, and its data type is changed from `TranscoderVideoCodecProfile` to `TranscoderVideoCodecType`. |
|Member change |TranscoderLayoutRegion |Added new member:<br><br>corner_radius<br><br>type<br><br>data<br><br>data_param<br><br>spatial_position |
|Member change, renaming |ITranscoderParam |Rename TranscoderParam.<br><br>Added member expected_mix_type: StreamMixingType |
|Enum change |TranscoderAudioCodecProfile |Remove kByteAACProfileMain<br><br>kByteAACProfileHEv1 changed from 2 to 1<br><br>kByteAACProfileHEv2 changed from 3 to 2 |
|Default value changed. |RoomProfileType |The default value of kRoomProfileTypeCommunication is changed from kRoomProfileTypeChatRoom = 6 to kRoomProfileTypeMeeting = 16. |
|The `AudioPropertiesConfig` struct has been changed. |AudioPropertiesConfig |Add the parameter to the data type: smooth |
|The valid range for the `width` and `height` parameters in `TranscoderLayoutRegion` has been extended. |width and height in TranscoderLayoutRegion |(0.0, 1.0] \-\> [0.0, 1.0] |
