---
title: "Resume Audio／Video Call"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-111590"
---

When the user uses the RTC service, the audio/video call may be interrupted by the phone call, third\-party app, and many others. When an interruption occurs, the RTC uses the system callback to resume the audio & video call. When an audio & video call is interrupted, RTC will respond as follows.


|Interruption |Android |iOS |Windows/macOS |
|---|---|---|---|
|The user received a phone call |Audio: Pauses capturing and reconnects after the phone call ends.<br><br>Video: on |Audio: pause capturing, reconnect after phone call ends<br><br>Video: pause capturing |Not applicable |
|Audio/video capturing modules are occupied by another app |Audio/video: Fails to reconnect and reports audio/video states via the callback. |Audio&video: pause capturing, reconnect after the interruption |Responds based on the system. For example, if capturing fails because the device is occupied, RTC reports audio/video state changes via the callback. |
|The screen is locked/ The laptop lid is closed<br><br>(but not in sleep mode) |Audio: on<br><br>Video: pause capturing, reconnect after the interruption |Audio: on<br><br>Video: pause capturing, reconnect after the interruption |Audio: on<br><br>Video: pause capturing, reconnect after the interruption |
|iOS app is running in Slide Over, Split View, or Picture in Picture mode<br><br>The performance of the device is reduced due to overheating<br><br>iOS app is sent to the background as the user starts the system camera app |Not applicable |Video: Pauses capturing and reconnects after the interruption.<br><br>The user is notified of the device state |Not applicable |


When RTC cannot automatically restore audio/video capture after an interruption, you must also monitor the remote audio/video playback status and configure the related subscription settings as described below. You can listen for state changes of the capturing device through the `onAudioDeviceStateChanged` and `onVideoDeviceStateChanged` callbacks.


* `InterruptionBegan`: Call is interrupted.

* `InterruptionEnded`: Call is resumed.

1. When an RTC call is interrupted, call `pauseAllSubscribedStream` to suspend receiving all remote users' streams. Follow the table above to specify the media stream type (audio or video) to suspend.

2. When the RTC call resumes from the interruption, call `resumeAllSubscribedStream` to resume subscribing to all remote users. Use the following callbacks to get the audio/video state changes.

   1. `onAudioDeviceStateChanged` and `onVideoDeviceStateChanged`

      * state: RuntimeError

      * error: DeviceNoCallback

   2. `onAudioDeviceWarning` and `onVideoDeviceWarning`

      * warning: CaptureSilence


When you detect a capture exception through the above callbacks, you can try to resume capturing by calling `startVideoCapture` or `startAudioCapture` again.

<span id="precautions"></span>
### Precautions


* By default, the SDK will listen for Android phone events and turn off the audio module during system calls. Make sure the app does not contain the logic to intercept system phone events ( `CALL_STATE_IDLE` and `CALL_STATE_OFFHOOK`), otherwise the RTC will not be able to detect the system phone call and will continue sending audio/video streams during the phone call.

* Due to the [system limitations](https://developer.android.com/about/versions/pie/android-9.0-changes-all) of Android 9 and above, if the screen is locked, the app will fail to capture audio/video during the call, but you can use the foreground service to keep capturing. If you want to capture audio or video after locking the screen, we recommend [starting a Service](https://developer.android.com/reference/android/app/Service) before the screen is locked or the app enters the background, and terminating the service before the screen is unlocked or the app returns to the foreground.


<span id="api-reference"></span>
### API Reference


* Android

   * [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onaudiodevicestatechanged)

   * [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onvideodevicestatechanged)

   * [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70081#onaudiodevicewarning)

   * [onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70081#onvideodevicewarning)

   * [pauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-70080#pauseallsubscribedstream)

   * [resumeAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-70080#resumeallsubscribedstream)

* iOS

   * [rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onaudiodevicestatechanged-device-type-device-state-device-error)

   * [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onvideodevicestatechanged-device-type-device-state-device-error)

   * [rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onaudiodevicewarning-devicetype-devicewarning)

   * [rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onvideodevicewarning-devicetype-devicewarning)

   * [pauseAllSubscribedStreamVideo:](https://docs.byteplus.com/en/docs/12/docs-70086#pauseallsubscribedstreamvideo)/[pauseAllSubscribedStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70086#pauseallsubscribedstreamaudio)

   * [resumeAllSubscribedStreamVideo:](https://docs.byteplus.com/en/docs/12/docs-70086#resumeallsubscribedstreamvideo)/[resumeAllSubscribedStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70086#resumeallsubscribedstreamaudio)

* Windows

   * [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onaudiodevicestatechanged)

   * [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onvideodevicestatechanged)

   * [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#onaudiodevicewarning)

   * [onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#onvideodevicewarning)

   * [pauseAllSubscribedStreamVideo:](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseallsubscribedstreamvideo)/[pauseAllSubscribedStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseallsubscribedstreamaudio)

   * [resumeAllSubscribedStreamVideo:](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeallsubscribedstreamvideo)/[resumeAllSubscribedStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeallsubscribedstreamaudio)
