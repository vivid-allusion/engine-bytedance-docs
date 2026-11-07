---
title: "Video Rotation"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-106458"
---

<span id="use-cases"></span>
## Use cases

Horizontal and vertical screen switching may occur when making a video call on a mobile device. To provide a better viewing experience, you need to set the video rotation orientation based on the usage scenario to prevent the video image from being inverted.

<span id="prerequisite"></span>
## Prerequisite

You have already integrated RTC SDK v3.36 or newer versions and can implement basic audio and video calls.

<span id="glossary"></span>
## Glossary


* **App orientation**: The orientation of the app's user interface. This orientation depends on whether the developer has locked the UI and if the user has disabled automatic screen rotation.

* **Gravity orientation**: The orientation is determined by the device's built\-in gravity sensor, which detects the direction of the Earth's gravity.

* **Status Bar**: The system status bar on a mobile device is always at the top of the App interface. When the app orientation changes, the position of the system status bar also changes.

* **Automatic screen rotation switch**: When it is enabled, the app orientation and the system status bar adjust to the device's rotation, and the user can toggle it in the system control bar of the mobile device.

* **UI lock**: A setting configured by the developer. When the UI is locked, the screen cannot be rotated even if the user enables automatic screen rotation. When unlocked, the app will rotate with the device.


<span id="feature-description"></span>
## **Feature description**

The video frames captured and sent by the capturing side include information about the rotation angle of the video frame. When rendering the video, the receiving side rotates it in the same way as the capturing side.

We provide `setVideoRotationMode` to set the rotation mode and specify the orientation reference for internal video capture. The reference frame for the rotation orientation can be set to the app orientation (by default) or the gravity orientation.

The receiving side can call `setRemoteVideoCanvas` to adjust the rendering mode of the video frame, for example, in `fit` mode. In this mode, the SDK does not crop the captured image.

<span id="scope"></span>
### **Scope**


* Applicable to both the front\-facing camera and back\-facing cameras.

* Not applicable to shared screen and custom video capture.

* The video orientation on the receiving side is consistent with the orientation used for recording and in the merge\-and\-push stream.


<span id="when-the-ui-is-not-locked-and-automatic-screen-rotation-is-enabled"></span>
### **When the UI is not locked and automatic screen rotation is enabled**

The receiving side performs the same in both rotation modes.


|Capturing side |Receiving side |
|---|---|
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c23185383098f18e8d45664db6baaf91.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ec6ab3e32ba1ea34d6056d07842c3b00.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a74ce57d06809dccb156a780d607c575.png) </span> |
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_289ee854e2c64c56604d86a0ef2fd3e1.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d75a74d93ac042eb3caa79a95bbb37e.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_860fda21a0c1fef3614ac6922efb7ae6.png) </span> |


<span id="when-the-ui-is-locked-or-automatic-screen-rotation-is-disabled"></span>
### **When the UI is locked or automatic screen rotation is disabled**

different rotation modes perform as follows:

> The figures below assume the UI on the receiving side is not locked and the automatic screen rotation is enabled. When the UI on the receiving side is locked or the automatic screen rotation is disabled, the relative position of the video image and the status bar remains unchanged.



|Capturing side |Receiving side (the capturing side sets the rotation mode to the app orientation) |Receiving side (the capturing side sets the rotation mode to gravity orientation) |
|---|---|---|
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e4f07388f5d538c6a10f27450cff62ca.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1065b3a8382d070643838271713a7b0e.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_baf1da896bb4a973449e1315ff521d18.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_36adff94283bc6a1de31791134e7a6e2.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_54229b4e5e00e8247cf403dea93fae40.png) </span> |
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b046e21088290791cf5d7af9b0a99d7a.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7e55a95f27ce5476aaa9b6fee18a796b.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1c199a7688333eb92efb50fd07d6fe9a.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d081ffb604d300ab9b748f00878d85a.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_757b87412610c0a793bfcf6b55b59ed6.png) </span> |
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_37b2598e93b57647dfb720efc6ab448c.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_af56934b7855d4a7a00733c64cea79cf.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f53010f25e3fa824309c0e6b37d1bd37.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ec6fa6f31bd9240651a72c8a886359ef.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_86bf793cee91dfbb4d45ba00742cd879.png) </span> |
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_70c838812b98efd9cf9b80475c203377.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f68fa34ea8e64d4280b4873a3d9f1a93.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1cf849d3e543afefe41b4473d8823936.png) </span> |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a7ac49e86c07838f8c558c14bfb3873f.png) </span><br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f2ff43d550e5235ac09a0dbc619f2b88.png) </span> |


<span id="sample-codes"></span>
### Sample codes

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `
rtcEngine.startVideoCapture();
rtcEngine.setVideoRotationMode(VideoRotationMode.FOLLOW_APP);`,

    "selected": true,
  },
  {
    "lang": "swift",
    "text": `self.rtcEngine?.startVideoCapture()
self?.rtcEngine?.setVideoRotationMode(ByteRTCVideoRotationModeFollowApp)`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="notes"></span>
### **Notes**


* When the UI is locked or automatic rotation is disabled, the behavior of the mirror function depends on the rotation mode. In gravity orientation mode, the video is mirrored along the axis of the device's physical orientation. In app orientation mode, it is mirrored along the axis of the app's UI orientation. To enable and use the mirror function, see [Mirror](https://docs.byteplus.com/en/docs/12/docs-70143).

* If the [Video Frame Orientation](https://docs.byteplus.com/en/docs/12/docs-128787) is fixed to either `Portrait` or `Landscape` mode, the position of sticker video effects remains unchanged, even if the video frame rotates due to changes in app or gravity orientation.


<span id="sample-project"></span>
## Sample project


* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/video/VideoRotateConfigActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/VideoManager/VideoRotation/VideoRotationViewController.swift)


<span id="api-reference"></span>
## **API reference**


|Android |iOS |Flutter |Unity |
|---|---|---|---|
|[setVideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-70080#setvideorotationmode) |[setVideoRotationMode:](https://docs.byteplus.com/en/docs/12/docs-70086#setvideorotationmode) |setVideoRotationMode |[SetVideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-191859#setvideorotationmode) |
