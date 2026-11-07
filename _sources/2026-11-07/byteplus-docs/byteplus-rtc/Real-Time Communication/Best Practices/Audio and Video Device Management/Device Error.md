---
title: "Device Error"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-177014"
---

To improve user experience during audio and video calls, you must handle device abnormalities such as a device being occupied or unauthorized.

This guide provides platform\-specific instructions for monitoring device status and handling common errors programmatically.

<span id="windows"></span>
## Windows

<span id="prerequisite"></span>
### Prerequisite

Monitor the user's local device status through the callbacks [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onaudiodevicestatechanged) and [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onvideodevicestatechanged).

<span id="approach"></span>
### Approach


1. Determine the device type through [RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-70098#rtcaudiodevicetype) and [RTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-70098#rtcvideodevicetype) in the callbacks mentioned above. For example, kRTCAudioDeviceTypeCaptureDevice indicates that the device type is audio capture device.

2. Determine the device status through MediaDeviceState and provide appropriate error messages.


When MediaDeviceState is kMediaDeviceStateRuntimeError, it means that an error occurs when the device is running. Then see the table below about [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70098#mediadeviceerror) for more instructions.


|Type |Description |Instruction |
|---|---|---|
|kMediaDeviceErrorDeviceNoPermission |No permission |Prompt the user to authorize and re\-enter the room |
|kMediaDeviceErrorDeviceBusy |Occupied by another application. |Prompt the user to close other applications and re\-enter the room |
|kMediaDeviceErrorDeviceNotFound |Not found |Prompt the user to check whether the device is connected correctly or to reconnect the device |
|kMediaDeviceErrorDeviceDisconnected |Disconnected |Prompt the user to reconnect the device |
|Other non\-zero return values |/ |Contact technical support |


<span id="ios"></span>
## iOS

<span id="prerequisite"></span>
### Prerequisite

Monitor the user's local device status through the callbacks [rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error) and [rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error).

<span id="approach"></span>
### Approach


1. Determine the device type through [ByteRTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcaudiodevicetype) and [ByteRTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcvideodevicetype) in the callbacks mentioned above. For example, ByteRTCAudioDeviceTypeCaptureDevice indicates that the device type is audio capture device.

2. Determine the device status through ByteRTCMediaDeviceState and provide appropriate error messages.



|Type |Description |Instruction |
|---|---|---|
|ByteRTCMediaDeviceStateInterruptionBegan |The RTC call was interrupted by a phone call, screen lock, or another app. |Prompt both local and remote users that the call is interrupted. |
|ByteRTCMediaDeviceStateInterruptionEnded |The RTC call resumed after being interrupted by a phone call or another app. |Prompt local and remote users respectively that they can continue the call |
|ByteRTCMediaDeviceStateRuntimeError |Runtime error |Handle the error based on [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcmediadeviceerror) |


> Refer to the following table for more information on `ByteRTCMediaDeviceError`.



|Type |Description |Instruction |
|---|---|---|
|ByteRTCMediaDeviceErrorDeviceNoPermission |No permission |Prompt the user to authorize and re\-enter the room. |
|ByteRTCMediaDeviceErrorDeviceBusy |Occupied by another application. |Prompt the user to close other applications and re\-enter the room |
|ByteRTCMediaDeviceErrorDeviceDisconnected |Disconnected |Prompt the user to reconnect the device |
|ByteRTCMediaDeviceErrorNotAvailableInBackground |An interruption occurs when the app enters the background because the user starts the system camera app. |Prompt the user to re\-enter the room or restart video capture after stopping the video capture at the application layer (For services with signaling, we also recommend notifying remote users why the local user's video is unavailable). |
|ByteRTCMediaDeviceErrorVideoInUseByAnotherClient |An interruption caused by the video device temporarily being unavailable (for example, when used by another app). |Prompt the user to close other applications that may use the camera and then re\-enter the room (For services with signaling, we also recommend notifying remote users why the local user's video is unavailable). |
|ByteRTCMediaDeviceErrorNotAvailableWithMultipleForegroundApps |An interruption caused by your app running in Slide Over, Split View, or Picture in Picture mode on iPad. |Prompt the user to stop such operations (For services with signaling, we also recommend notifying remote users why the local user's video is unavailable). |
|Other non\-zero return values |/ |Contact technical support |


<span id="android-macos"></span>
## Android & macOS

Refer to the handling methods for Windows and iOS.

If you have any questions, please contact technical support.
