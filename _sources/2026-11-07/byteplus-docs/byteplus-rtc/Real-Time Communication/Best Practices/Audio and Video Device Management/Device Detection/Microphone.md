---
title: "Microphone"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-177016"
---

Detect the user's microphone device (usually on PC) to determine if it supports the required audio and video functionality. Relevant features include enumerating and selecting microphone devices, providing volume prompts, and adjusting volume.

<span id="sequence-diagram"></span>
## Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/5111eh7lbfnuhf/upload_0b077c5ec90cd4804f0f567771d3420b.png) </span>

<span id="api"></span>
## API


|**Feature** | |Windows |MacOS |
|---|---|---|---|
|Get audio device manager | |[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70095#getaudiodevicemanager) |[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70092#getaudiodevicemanager) |
|Enumerate microphones |Enumerate devices |[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-enumerateaudiocapturedevices) |[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-enumerateaudiocapturedevices) |
| |Get device count |[getCount](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-getcount) |[getCount](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCDeviceCollection-getcount) |
| |Get device information |[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-getdevice) |[getDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCDeviceCollection-getdevice-devicename-deviceid) |
| |Release devices |[release](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-release) | |
|Switch microphone |Get audio capture device |[getAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudiocapturedevice) |[getAudioCaptureDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-getaudiocapturedevice) |
| |Set a manual audio capture route |[followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-followsystemcapturedevice) |[followSystemCaptureDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-followsystemcapturedevice) |
| |Set audio capture device |[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudiocapturedevice) |[setAudioCaptureDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-setaudiocapturedevice) |
|Microphone volume callback | |[onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onaudiodevicevolumechanged) |[onAudioDeviceVolumeChanged:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onaudiodevicevolumechanged-volume-muted) |
|Adjust microphone volume (captured volume) | |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70095#setcapturevolume) |[setCaptureVolume:](https://docs.byteplus.com/en/docs/12/docs-70092#setcapturevolume) |
|Microphone test |Initialize audio capture device for testing |[initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-initaudiocapturedevicefortest) |[initAudioCaptureDeviceForTest:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-initaudiocapturedevicefortest) |
| |Enable audio information prompts |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#enableaudiopropertiesreport) |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70092#enableaudiopropertiesreport) |
| |Start device test (lasts for 30s) |[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-startaudiodevicerecordtest) |[startAudioDeviceRecordTest:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-startaudiodevicerecordtest) |
| |Stop the test recording and play it back |[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-stopaudiodevicerecordandplaytest) |[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-stopaudiodevicerecordandplaytest) |
| |Stop audio capture device test |[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-stopaudiodeviceplaytest) |[stopAudioRecordingDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-stopaudiorecordingdevicetest) |
|Volume callback during microphone test | |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#onlocalaudiopropertiesreport) |[onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onlocalaudiopropertiesreport) |


<span id="common-issues"></span>
## Common Issues

This section introduces common issues in the microphone detection process, with the following keywords:


* Whether the audio capture route follows the system

* Abnormality detection before device detection

* Volume callback

* Device permission configuration


<span id="whether-the-audio-capture-route-follows-the-system"></span>
### Whether the audio capture route follows the system


* If a user does not specify an audio capture or playback device, the system uses the default device. The system also switches automatically if the default device changes.

* You can use [followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-followsystemcapturedevice) to set whether the audio capture route follows the system. Setting the parameter of `followSystemCaptureDevice` to false disables system\-following, allowing users to manually switch microphone devices. If the audio capture route is set to follow the system, you cannot call [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudiocapturedevice) to select a specific audio capture device.


<span id="abnormality-detection-before-device-detection"></span>
### Abnormality detection before device detection

Before microphone detection, you can call [initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-initaudiocapturedevicefortest) to detect abnormalities such as device not found, permission denied/disabled, etc.

<span id="volume-callback"></span>
### Volume callback

When the microphone volume changes, [onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onaudiodevicevolumechanged) will be triggered. By listening to this callback, you can detect changes in the microphone volume. If the device volume is too low or muted, you can prompt the user accordingly.

<span id="device-permission-configuration"></span>
### Device permission configuration

On macOS, you need to set `NSMicrophoneUsageDescription` in the Info.plist file. On Windows, you can directly access the device without requesting permission by default.

Refer to [Device Permission](https://docs.byteplus.com/en/docs/12/docs-177013) for more information.
