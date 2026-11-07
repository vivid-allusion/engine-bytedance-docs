---
title: "macOS with Objective-C"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70131"
---

With the BytePlus RTC SDK, you can build a basic app for real\-time video calls. For the complete sample code of the demo project, see [Demo Project](https://docs.byteplus.com/en/docs/12/docs-1163793).

<span id="prerequisites"></span>
## Prerequisites


* Xcode 12.5+. This document uses Xcode 14.0.1 as an example.

* macOS 10.10+

* Get an [AppID](https://docs.byteplus.com/en/docs/12/docs-69865)

* Download [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707#download-sdk)


<span id="integrate-the-sdk"></span>
## Integrate the SDK

<span id="step-1-optional-create-a-project"></span>
### Step 1: (Optional) Create a project

> Note: This step helps you create a new project. Skip this step if you want to integrate BytePlus RTC into an existing project.


1. Create a new macOS App with Xcode.

2. Set the project name, the team name, and select the development language (Objective\-C).

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70131_1.png) </span>

3. Select the project storage location and create the project.

4. Signature Settings: Go to **TARGETS \> Project Name \> Signing & Capabilities** , make sure that `Automatically manage signing` is checked, and select your team to enable it.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70131_2.png) </span>


<span id="step-2-include-rtc-sdk"></span>
### Step 2: Include RTC SDK

Include the following files into the project:


* `BytePlusRTC.framework`

* `libbytenn.dylib`

* `RTCFFmpeg.framework`


<span id="step-3-configure-project-properties"></span>
### Step 3: Configure Project Properties


1. Configure audio & video permissions

   a. Find the `info.plist` file in the project.

   Click the Add button (+) to add permissions for audio and video devices:

   * `Privacy - Microphone Usage Description` and enter a reason for using the microphone in the Value column

   * `Privacy - Camera Usage Description` and fill in the reason for using the camera (Value)

      <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70131_3.png) </span>


 &nbsp;

2. SDK configuration

In **TARGETS \> Project Name \> General**, select **Frameworks, Libraries, and Embedded Content**, and set the following libraries to `Embed & Sign`:


* `BytePlusRTC.framework`

* `libbytenn.dylib`

* `RTCFFmpeg.framework`


<span id="implement-a-client-for-video-call"></span>
## Implement a Client for Video Call

See the following diagram of the API calling sequence.


1. (Optional) Create a user interface.

   Create a user interface for your App. We recommend you add the following elements to your project:

* Room ID

* User ID

* Local video window

* Remote video window

* Microphone button

* Camera button

* End call button

2. Import header files.


```objective-c
/// import header file
#import <BytePlusRTC.framework/Headers/BytePlusRTC.h>
```



3. Create the RTCEngine instance.


Call [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-creatertcengine-delegate) to create an RTCEngine instance for video\-related functions.


4. Set local video canvas.


Call [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70092#setlocalvideocanvas) to configure the view for the local video stream.


5. Start local video capture.


Call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-startvideocapture) to enable local video capture.


6. Start local audio capture.


Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-startaudiocapture) to enable local audio capture.


7. Create the RTCRoom instance.


Call [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70092#creatertcroom) to create an RTCRoom instance for room\-related functions. A room is a virtual space where users can have real\-time audio and video communications.


8. Set RTCRoom\-related callbacks.


Call `ByteRTCRoom.delegate` to set the RTCRoom\-related callbacks.


9. Join a room.


Call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#joinroom-userinfo-uservisibility-roomconfig) to enter the room. After joining, the user can have real\-time audio and video communications with anyone else in the same room.


10. Handle the callbacks of joining the room.


You'll receive [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70093#onroomstatechanged-withuid-state-extrainfo) after joining the room. Implement logic to handle events for when a user joins the room for the first time or rejoins after a disconnection.


11. Handle the callbacks of the remote user joining the room.


You'll receive the [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70093#onuserjoined) callback when a remote user joins the same room. Add logics for events of the remote user joining the room for the first time or rejoining the room based on the callbacks.


12. Handle the callbacks of the first remote video frame decoded.


You will receive the [onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70093#onfirstremotevideoframedecoded-info-withframeinfo) callback after the first video frame from a remote user has been decoded. You may render the remote video on the video canvas of your app.


13. Set the canvas for the remote video.


Call [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setremotevideocanvas-withcanvas) to set the canvas for the remote video.


14. Handle the callbacks of the remote user leaving the room.


You'll receive the [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70093#onuserleave-reason) callback after the remote user leaves the room. You can add logic to handle this event, such as removing the remote user's video canvas.


15. Leave the room.


After the call is finished, call [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70092#leaveroom) to leave the room.


16. Destroy the RTCEngine instance.


Call [destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-destroyrtcengine) to destroy the RTCEngine instance and release all related resources.

This completes the implementation of a basic video call app.

<span id="error-handling"></span>
## Error Handling

When you compile the project, you may encounter the following error message: `dnssd_clientstub ConnectToServer: connect() failed path:/var/run/mDNSResponder Socket:20 Err:-1 Errno:1 Operation not permitted`, try one of the following solutions:


* If you are not using `App Sandbox`, disable this feature;

* If you use `App Sandbox`, enable the following options:

   * `Incoming Connections`;

   * `Outgoing Connections`;

   * `Camera`

   * `Audio Input`.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e655fc6085f9ddcca34f0abf9eeef89.png) </span>
