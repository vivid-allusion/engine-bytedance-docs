---
title: "Camera"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-177015"
---

Detect the user's video device (usually on PC) to determine if it supports the required audio and video functionality. Relevant features include enumerating, selecting, previewing, and mirroring.

<span id="sequence-diagram"></span>
## Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/5111eh7lbfnuhf/upload_e967cbb9536f4bc3d79f7c75a39be419.png) </span>

<span id="api"></span>
## API


|Feature | |Windows |MacOS |
|---|---|---|---|
|Get video device manager | |[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70095#getvideodevicemanager) |[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70092#getvideodevicemanager) |
|Enumerate cameras |Enumerate devices |[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceManager-enumeratevideocapturedevices) |[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCVideoDeviceManager-enumeratevideocapturedevices) |
| |Get device count |[getCount](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection-getcount) |[getCount](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCDeviceCollection-getcount) |
| |Get device information |[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection-getdevice) |[getDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCDeviceCollection-getdevice-devicename-deviceid) |
| |Release device |[release](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection-release) | |
|Select camera |Get video capture device information |[getVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceManager-getvideocapturedevice) |[getVideoCaptureDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCVideoDeviceManager-getvideocapturedevice) |
| |Set the current video capture device |[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceManager-setvideocapturedevice) |[setVideoCaptureDevice:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCVideoDeviceManager-setvideocapturedevice) |
|Preview |Set local video canvas |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideocanvas) |[setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/12/docs-70092#setlocalvideocanvas) |
| |Set video capture parameters (optional) |[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setvideocaptureconfig) |[setVideoCaptureConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#setvideocaptureconfig) |
| |Start video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startvideocapture) |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70092#startvideocapture) |
| |Update local video canvas (optional) |[updateLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#updatelocalvideocanvas) |[updateLocalVideoCanvas:withBackgroundColor:](https://docs.byteplus.com/en/docs/12/docs-70092#updatelocalvideocanvas-withbackgroundcolor) |
|Set mirror mode | |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideomirrortype) |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70092#setlocalvideomirrortype) |
|Stop video capture | |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#stopvideocapture) |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70092#stopvideocapture) |
|Video device state callback | |[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onvideodevicestatechanged) |[rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onvideodevicestatechanged-device-type-device-state-device-error) |


<span id="common-issues"></span>
## Common Issues

This section introduces common issues in the camera detection process, with the following keywords:


* View binding and switching

* Cropped video frame

* Device error

* Device permission configuration

* Others


<span id="view-binding-and-switching"></span>
### View binding and switching

You can bind the video stream to the local view by calling [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideocanvas). If you need to switch views, call the method to bind the new view; if you need to unbind, call this method with an empty view.

<span id="cropped-video-frame"></span>
### Cropped video frame


* You can specify video capture parameters, including resolution and frame rate, by calling [setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setvideocaptureconfig). By default, the capture mode (capturePreference) is set to automatic (KAuto), which means the SDK will set the optimal capture parameters based on the server's capture configuration and encoding parameters.

* If the aspect ratio of the capture parameters and encoding parameters is different, the video frame will be cropped. For example, if the capture parameters are 960x540 (16:9) and the encoding parameters are 240x180 (4:3), part of the image will be cropped during encoding. This results in a smaller field of view and an enlarged effect on the image seen by the remote end. Therefore, it is recommended to set the capture and encoding resolutions with the same aspect ratio to avoid cropping and image distortion.


<span id="device-error"></span>
### Device error

Get the device status through listening to this callback [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onvideodevicestatechanged) and display corresponding error messages.

Refer to [Device Error](https://docs.byteplus.com/en/docs/12/docs-177014) for more information.

> Note: When plugging or unplugging the camera, [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onvideodevicestatechanged) will also be triggered. You can update the device list by enumerating the devices. If the device is removed, the SDK will not automatically switch to another device due to privacy concerns. Therefore, you need to call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startvideocapture) to initiate camera capture again.


<span id="device-permission"></span>
### Device permission

> If there is no camera permission, [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onvideodevicestatechanged) will trigger the error kMediaDeviceErrorDeviceNoPermission.


On macOS, you need to set `NSCameraUsageDescription` in the Info.plist file. On Windows, you can directly access the camera without requesting permission if the system settings are not changed.

Refer to [Device Permission](https://docs.byteplus.com/en/docs/12/docs-177013) for more information.

<span id="others"></span>
### Others


* The camera hardware on Windows does not support simultaneous usage by multiple apps.

* If [setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceManager-setvideocapturedevice) or [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startvideocapture) has not been called before, the returned device_id will be "auto". If it has been called, it will return the current device_id.
