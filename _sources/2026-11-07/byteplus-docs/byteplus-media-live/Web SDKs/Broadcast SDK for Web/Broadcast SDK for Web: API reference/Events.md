---
title: "Events"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-events"
---

<span id="observer"></span>
## Observer

Type：`class`

Used to receive various event callbacks during the audio and video capture and streaming process. Provides the ability to listen for information such as errors, warnings, status updates, and device switching, helping to monitor the status of the streamer in real\-time.

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|onError |(code: number, msg: string, extraInfo?: any) =\> void |Error notification callback. Used to capture fatal errors occurring during streaming or capture. Can be used in conjunction with error codes for troubleshooting and logging. |
|onWarning |(msg: string) =\> void |Warning notification callback used to alert about abnormal conditions that may affect streaming but are not fatal. |
|onCaptureFirstAudioFrame |() =\> void |The callback notification for the completion of the first frame audio capture. This is used to confirm if the audio source is working properly after starting the capture. |
|onCaptureFirstVideoFrame |() =\> void |The callback notification for the completion of the first frame video capture. This is used to confirm whether the video source is working properly after starting the capture. |
|onPushStatusUpdate |(status: number, msg: string) =\> void |The stream state update callback provides status codes and status descriptions. This can be used to monitor the status of the stream in real\-time (e.g., disconnection, retrying) and take appropriate actions. |
|onMicrophoneChanged |(changedDevice: MediaDeviceInfo) =\> void |The callback for switching the microphone device returns the information of the switched device. It is used to monitor the status changes of audio devices, such as hot swapping of devices. |
|onCameraChanged |(changedDevice: MediaDeviceInfo) =\> void |The callback for switching camera devices returns the information of the switched device. It is suitable for scenarios where the host switches video input devices, such as live streaming. |
|onCaptureInterrupted |(streamId: string) =\> void |Callback for stream interruption, returns the ID of the interrupted stream. This is used for handling situations where the stream stops due to device anomalies. |
|onPushStart |() =\> void |Callback notification for starting a live stream. |
|onPushStop |() =\> void |Callback notification for stopping the stream. |
|onStopCapture |(streamId: string) =\> void |The callback for stopping the capture returns the ID of the stopped stream. |
