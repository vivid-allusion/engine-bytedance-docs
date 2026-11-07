---
title: "Speaker"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-177017"
---

Detect the user's speaker device (usually on PC) to determine if it supports the required audio playback functionality. Relevant features include enumerating and selecting speaker devices and adjusting and detecting volume.

<span id="sequence-diagram"></span>
## Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/5111eh7lbfnuhf/upload_2e043df6d10d7812ff8d7cc5b46b717e.png) </span>

<span id="api"></span>
## API


|**Feature** | |Windows |MacOS |
|---|---|---|---|
|Get audio device manager | |[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70095#getaudiodevicemanager) |[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70092#getaudiodevicemanager) |
|Enumerate speakers |Enumerate devices |[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-enumerateaudioplaybackdevices) |[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-enumerateaudioplaybackdevices) |
| |Get device count |[getCount](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-getcount) |[getCount](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCDeviceCollection-getcount) |
| |Get device information |[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-getdevice) |[getDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCDeviceCollection-getdevice-devicename-deviceid) |
| |Release devices |[release](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-release) | |
|Switch speaker |Get audio playback device |[getAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudioplaybackdevice) |[getAudioPlaybackDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-getaudioplaybackdevice) |
| |Set whether the audio playback route follows the system |[followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-followsystemplaybackdevice) |[followSystemPlaybackDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-followsystemplaybackdevice) |
| |Set audio playback device |[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudioplaybackdevice) |[setAudioPlaybackDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-setaudioplaybackdevice) |
|Speaker volume callback | |[onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onaudiodevicevolumechanged) |[onAudioDeviceVolumeChanged:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onaudiodevicevolumechanged-volume-muted) |
|Adjust speaker volume (playback volume) | |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70095#setplaybackvolume) |[setPlaybackVolume:](https://docs.byteplus.com/en/docs/12/docs-70092#setplaybackvolume) |
|Speaker test |Initialize audio playback device |[initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-initaudioplaybackdevicefortest) |[initAudioPlaybackDeviceForTest:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCAudioDeviceManager-initaudioplaybackdevicefortest) |
|Volume callback during speaker test | |[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-70096#onaudioplaybackdevicetestvolume) |[onAudioPlaybackDeviceTestVolume:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onaudioplaybackdevicetestvolume) |


<span id="common-issues"></span>
## Common Issues

This section introduces common issues that can occur during speaker detection:


* Following the system's audio playback route

* Pre\-detection error checks

* Audio playback test

* Volume callback

* Device permission configuration


<span id="following-the-system-s-audio-playback-route"></span>
### Following the system's audio playback route


* If the user does not specify an audio capture or playback device, the system automatically selects the default device. When the default device changes, the system switches to the new one automatically.

* You can use [followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-followsystemplaybackdevice) to set whether the audio playback route follows the system. Setting this method's parameter to false prevents the audio playback route from following the system, which allows users to switch speaker devices manually. If the audio playback route follows the system, you cannot call [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudioplaybackdevice) to set the audio playback device.


<span id="pre-detection-error-checks"></span>
### Pre\-detection error checks

Before speaker detection, you can call [initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-initaudioplaybackdevicefortest) to check for issues such as a missing device or denied/disabled permissions.

<span id="audio-playback-test"></span>
### Audio playback test

You can call [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-startaudioplaybackdevicetest) to perform speaker detection. After the test is started, it plays the specified audio file in a loop.

To stop the audio playback test, call [stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-stopaudioplaybackdevicetest).

<span id="volume-callback"></span>
### Volume callback

When the speaker system volume changes, the SDK triggers the [onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onaudiodevicevolumechanged) callback. By listening for this callback, you can detect changes in the speaker volume. If the device volume is too low or muted, you can prompt the user accordingly.

<span id="device-permission-configuration"></span>
### Device permission configuration

On macOS, you need to set `NSMicrophoneUsageDescription` in the Info.plist file. On Windows, you can directly access the device without requesting permission by default.

Refer to [Device Permission](https://docs.byteplus.com/en/docs/12/docs-177013) for more information.
