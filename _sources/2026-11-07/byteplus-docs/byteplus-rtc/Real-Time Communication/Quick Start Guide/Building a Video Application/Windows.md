---
title: "Windows"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70130"
---

With the BytePlus RTC SDK, you can build a basic app for real\-time video calls. For the complete sample code of the demo project, see [Demo Project](https://docs.byteplus.com/en/docs/12/docs-1163793).

<span id="prerequisites"></span>
## Prerequisites


* Microsoft Visual Studio 2017 or above

* Windows 7 or later (Windows 10 is recommended)

* C++ as the programming language

* Get an [AppID](https://docs.byteplus.com/en/docs/12/docs-69865)

* Download [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707#download-sdk)


<span id="integrate-the-sdk"></span>
## Integrate the SDK

<span id="step-1-optional-create-the-project"></span>
### Step 1: (Optional) Create the project

> Note: This step helps you create a new project. Skip this step if you want to integrate BytePlus RTC into an existing project.


1. Open Visual Studio and create a new project

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70130_1.png) </span>

2. In the New Project window, select the project type as **MFC Application** or **Windows Desktop Application**, enter the project name, select the project storage path, and click **OK**.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70130_2.jpeg) </span>


<span id="step-2-unzip-the-sdk-and-copy-it-to-the-project-directory"></span>
### Step 2: Unzip the SDK and copy it to the project directory

Download the SDK for your target platform (Win32 or x64). After downloading, copy the "BytePlusRTC" folder into your project directory.

<span id="step-3-configure-project-properties"></span>
### Step 3: Configure Project Properties

In the **Solution Explorer** window, right\-click the project name and select **Properties** to configure the following settings. Click **OK** when the configuration is complete.


1. Add the header file directory to the "**include**" search path.

   Select **Configuration Properties \> VC++ Directories \> General \> Include Directory**, click Edit, and add the header file search path to the "include" directory .

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70130_3.jpeg) </span>

2. Add the "**lib**" directory to the Additional Library Directories path.

   Select **Configuration Properties \> Linker \> General** and add the "BytePlusRTC/lib/Win32" or "BytePlusRTC/lib/x64" directory to the "**Additional Libraries Directories**".

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70130_4.jpeg) </span>

3. Specify the link library

   Select **Configuration Properties \> Linker \> Input** and add "BytePlusRTC.lib" to "**Additional Dependencies**".

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70130_5.jpeg) </span>


<span id="implement-a-client-for-video-call"></span>
## Implement a client for Video Call


1. (Optional) Create a user interface

   Create a user interface for your project according to your needs. We recommend you add the following elements to your project:

* Room ID

* User ID

* Local video window

* Remote video window

* Microphone button

* Camera button

* End call button

2. Import header files

   Include SDK API in files that use the header files.


```Plain
#include "bytertc_engine.h"
```



3. Call [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#creatertcengine) to initialize the RTC engine.


```cpp
static BYTERTC_STATIC_API IRTCEngine* createRTCEngine(
    const EngineConfig& config,
    IRTCEngineEventHandler* event_handler
);
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|config |const EngineConfig& |Engine configuration. You must pass your AppID in this struct. See [EngineConfig](https://docs.byteplus.com/en/docs/12/docs-70098#EngineConfig). |
|event_handler |IRTCEngineEventHandler\* |Handler sent from SDK to App. See [IRTCEngineEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler). |



4. Call [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideocanvas) to set up the view for local video rendering.


```cpp
virtual int setLocalVideoCanvas(const VideoCanvas& canvas) = 0;
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|canvas |const VideoCanvas& |View information and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70098#VideoCanvas). |



5. Call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startvideocapture) to start local video capture.


```cpp
virtual void startVideoCapture() = 0;
```



6. Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startaudiocapture) to start local audio capture.


```cpp
virtual void startAudioCapture() = 0;
```



7. Call [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70095#creatertcroom) to create an RTC room.


```cpp
virtual IRTCRoom* createRTCRoom(const char* room_id) = 0;
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|room_id |**const char**\* |A non\-empty string within 128 bytes. Each room created by calling this API requires a unique roomid. So that the room can be distinguished from each other.<br><br>The following character sets are supported:<br><br>• 26 uppercase letters: A ~ Z,<br><br>• 26 lowercase letters: a ~ z,<br><br>• 10 numbers: 0 ~ 9,<br><br>• Underscore "_", at sign "@", and minus sign "\-". |



8. Call [setRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setrtcroomeventhandler) to receive room\-specific events.


```cpp
virtual int setRTCRoomEventHandler(IRTCRoomEventHandler* room_event_handler) = 0;
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|room_event_handler |IRTCRoomEventHandler\* |See [IRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#irtcroomeventhandler). |



9. Call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) to join the RTC room.


```cpp
virtual int joinRoom(const char* token, const UserInfo& user_info, bool user_visibility, const RTCRoomConfig& config) = 0;
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|token |**const char**\* |Dynamic key for authenticating the logged\-in user.<br><br>You must provide a token to join the room. When testing, you can use the console to generate temporary tokens. For production environments, you must generate tokens on your server using the server\-side SDK. See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br>• Apps with different App IDs cannot communicate with each other.<br><br>• Make sure that the App ID used to generate the Token is the same as the App ID used to create the engine, otherwise it will cause the join room to fail. The reason for the failure will be communicated via the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onroomstatechanged) callback. |
|user_info |**const UserInfo&**  |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70098#userinfo). |
|user_visibility |**bool** |User visibility in the room. If true, the user can publish streams and other users will be notified of their presence. |
|config |**const RTCRoomConfig&**  |Configures room parameters, such as the room profile and whether to automatically publish or subscribe to streams. See [RTCRoomConfig](https://docs.byteplus.com/en/docs/12/docs-70098#rtcroomconfig) for the specific configuration mode. |



10. Listen for room state changes via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onroomstatechanged).


```cpp
virtual void onRoomStateChanged(
   const char* room_id, const char* uid, int state, const char* extra_info);
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|room_id |**const char**\* |Room ID. |
|uid |**const char**\* |User ID. |
|state |**int** |Room state code.<br><br>• 0: Success.<br><br>• !0: Failure. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70097#errorcode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-70097#warningcode) for specific indications. The user has been removed from the room due to one of the following reasons.<br><br><br>* \-1004: The same user joined the room in another client<br><br>* \-1006: The administrator removed the user from the room by calling a server\-side API. |
|extra_info |**const char**\* |Extra information.<br><br>`join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` indicates that the user rejoined the room.<br><br>`elapsed` indicates the time interval from calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) to successfully joining room, in ms. |



11. Listen for remote users joining the room via [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserjoined).


```cpp
virtual void onUserJoined(const UserInfo& user_info)
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|user_info |const UserInfo& |See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70098#userinfo). |



12. Listen for the first remote video frame decoded via [onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70096#onfirstremotevideoframedecoded).


```cpp
virtual void onFirstRemoteVideoFrameDecoded(const char* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info)
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote video stream ID. |
|stream_info |const StreamInfo& |Remote video stream information. See [StreamInfo](https://docs.byteplus.com/en/docs/12/docs-70098#streaminfo). |
|info |const VideoFrameInfo& |Video frame information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70098#videoframeinfo). |



13. Call [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#setremotevideocanvas) to render the remote video stream.


```cpp
virtual int setRemoteVideoCanvas(const char* stream_id, const VideoCanvas& canvas) = 0;
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |Remote video stream ID. |
|canvas |const VideoCanvas& |canvas and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70098#videocanvas). |



14. Listen for remote users leaving the room via [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70096#onuserleave).


```cpp
virtual void onUserLeave(const char* uid, UserOfflineReason reason)
```


Parameters


|Name |Type |Instructions |
|---|---|---|
|uid |**const char**\* |The ID of the user who left the room or became invisible. |
|reason |**UserOfflineReason** |Reason to leave the room. Refer to [UserOfflineReason](https://docs.byteplus.com/en/docs/12/docs-70098#userofflinereason).<br><br>• 0: The remote client calls [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70095#leaveroom) to leave the room.<br><br>• 1: The remote client was disconnected due to a poor network connection or an expired token.<br><br>• 2: The remote client calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setuservisibility) to turn invisible.<br><br>• 3: The remote user has been removed from the room by the administrator via a OpenAPI call. |



15. Call [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70095#leaveroom) to leave the room.


```cpp
virtual void leaveRoom() = 0;
```



16. Call [destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#destroyrtcengine) to release all SDK resources.


```cpp
static BYTERTC_STATIC_API void destroyRTCEngine(IRTCEngine* engine);
```


You have now implemented a basic video call application.
