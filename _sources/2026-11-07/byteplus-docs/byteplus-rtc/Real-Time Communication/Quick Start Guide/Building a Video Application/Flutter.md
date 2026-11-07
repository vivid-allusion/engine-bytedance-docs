---
title: "Flutter"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-132236"
---

With the BytePlus RTC SDK, you can build a basic app for real\-time video calls. For the complete sample code of the demo project, see [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793).

<span id="prerequisites"></span>
## Prerequisites


* Flutter 2.0.0+

* Dart 2.12.0+

* Get an AppID

* If the target system is Android:

   * Android Studio 3.5+

   * Android API Level 19 or later for real devices or emulators

   * Java as the programming language

* If the target system is iOS:

   * Xcode 12.5+

   * iOS 11.0+ of the real devices or emulators

   * Objective\-C as the programming language

   * Make sure your project has a valid developer signature


<span id="integrate-the-sdk"></span>
## Integrate the SDK

<span id="step-1-optional-create-a-project"></span>
### Step 1: (Optional) Create a project

> Note: Skip this step if you want to integrate BytePlus RTC into an existing project.


Please refer to [Create the App](https://docs.flutter.dev/get-started/test-drive#create-app) to create a Flutter project.

<span id="step-2-use-the-sdk-package-as-a-library"></span>
### Step 2: Use the SDK package as a library

<span id="option-1-depend-on-it-recommended"></span>
#### Option 1: Depend on it (recommended)

Go to the root directory of your project in the terminal, and run the following command to install the dependencies.

```dart
flutter pub add byteplus_rtc
```


This will automatically add the corresponding SDK version number field in your project's pubspec.yaml file, like this:

```dart
dependencies:
  byteplus_rtc: ^3.44.1
```


<span id="option-2-import-it"></span>
#### Option 2: Import it


1. Download the latest version of the [RTC SDK for Flutter](https://pub.dev/packages/byteplus_rtc/versions), and unzip the package to your project folder.

2. Add byteplus_rtc dependencies to the `pubspec.yaml file`.


```yaml
environment:
  sdk: ">=2.12.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
   
  # Replace <SDK_PATH> with the file path of the SDK under your project
  byteplus_rtc:
    path: <SDK_PATH>
```


<span id="update-dependencies"></span>
#### Update dependencies

If you need to update the version of integrated SDK, go to the root directory of your project in the terminal and run the following command to update dependencies.

```dart
flutter pub get
```


<span id="step-3-configure-project-properties"></span>
### Step 3: Configure project properties

<span id="permission-acquisition"></span>
#### Requesting permissions

Before using the audio & video function, you must request the required permissions in your code. This article uses the `permission_handler` component library as an example:

```dart
[Permission.camera, Permission.microphone].request();
```


<span id="other-configurations-for-app-development-in-different-systems"></span>
#### Other configurations for app development in different systems

For iOS system


1. Add the following permissions to the `ios/Runner/Info.plist` file:

   * `Privacy - Microphone Usage Description`, and fill in the description in the Value column.

   * `Privacy - Camera Usage Description`, and fill in the description in the Value column.

2. Add the following code to the `Podfile` file:


```ruby
# Uncomment this line to define a global platform for your project
# platform :ios, '11.0'

# CocoaPods analytics sends network stats synchronously affecting flutter build latency.
ENV['COCOAPODS_DISABLE_STATS'] = 'true'

source 'https://github.com/CocoaPods/Specs.git'
···
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
target '<YOUR_TARGET>' do
  pod 'BytePlusRTC'
end
```


If you run the app on an emulator, add the following code at the end of the `Podfile` file:

```dart
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)

    ## If you run the app on an emulator, add the following code.
    target.build_configurations.each do |config|
      if (config.name == 'Debug')
        config.build_settings['ONLY_ACTIVE_ARCH'] = 'YES'
      end
    end
    ##
  end
end
```


<span id="implement-a-client-for-video-call"></span>
## Implement a Client for Video Call

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/132236.jpeg) </span>

<span id="_1-optional-create-a-user-interface"></span>
#### 1. (Optional) Create a user interface

Create a user interface for your project according to your needs. You can refer to [Flutter User Interface](https://docs.flutter.dev/development/ui/widgets-intro) for more details. Skip this step if you have already built a user interface.

We recommend you add the following elements to your project:


* Room ID

* User ID

* Local Video Window

* Remote video window

* Microphone button

* Camera button

* End call button


<span id="_2-import-header-files"></span>
#### 2. Import header files

Include SDK API in files that use the header files.

```dart
import 'package:byteplus_rtc/byteplus_rtc.dart';
```


<span id="_3-rtcvideo-creatertcvideo"></span>
#### 3. RTCVideo.createRTCVideo

Call `RTCVideo.createRTCVideo` to create an engine instance.

This is the very first API that you must call if you want to use all the RTC capabilities.

```dart
static Future<RTCVideo?> createRTCVideo(RTCVideoContext context)
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|context |RTCVideoContext |Used to initialize the RTCVideo. |


<span id="_4-rtcvideo-setmaxvideoencoderconfig"></span>
#### 4. RTCVideo.setMaxVideoEncoderConfig

After creating the engine instance, call `RTCVideo.setMaxVideoEncoderConfig` to set the encoding parameters for the video stream you will publish, including resolution, frame rate, bitrate, etc.

```dart
Future<int?> setMaxVideoEncoderConfig(VideoEncoderConfig maxSolution)
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|maxSolution |VideoEncoderConfig |The maximum video encoding parameters. |


<span id="_5-rtcviewcontext-localcontext"></span>
#### 5. RTCViewContext.localContext

Before joining the room, you need to set up the local view to see the locally captured video.


* Create an `RTCViewContext` instance :


```dart
RTCViewContext.localContext(
    {required this.uid, this.streamType = StreamIndex.main})
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |ID of the local user. |
|streamType |StreamIndex |Stream type. Mainstream by default. |



* Build the `RTCSurfaceView` with the created `RTCViewContext` instance:


```dart
const RTCSurfaceView({
  Key? key,
  required this.context,
  this.renderMode = VideoRenderMode.hidden,
  this.backgroundColor = 0,
  this.zOrderOnTop = false,
  this.zOrderMediaOverlay = false,
  this.onPlatformViewCreated,
  this.gestureRecognizers,
})
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|context |RTCViewContext |Used to initialize the RTCSurfaceView |
|renderMode |VideoRenderMode |Video rendering mode. |
|backgroundColor |int |The background color used to fill the blank part of the canvas.<br><br><br>* The value range is [0x0000000, 0xFFFFFFFF].<br><br>* The default value is 0x00000000.<br><br>* Transparency settings are not supported. |
|zOrderOnTop |bool |Sets whether the Surface of the SurfaceView is placed at the top of the window it is in.<br><br><br>* See [setZOrderOnTop](https://developer.android.com/reference/android/view/SurfaceView#setZOrderOnTop(boolean)) for details.<br><br>* Applies to Android only. |
|zOrderMediaOverlay |bool |Sets whether the Surface of the SurfaceView is placed on top of another regular SurfaceView.<br><br><br>* See [setZOrderMediaOverlay](https://developer.android.com/reference/android/view/SurfaceView#setZOrderMediaOverlay(boolean)) for details.<br><br>* Applies to Android only. |
|onPlatformViewCreated |PlatformViewCreatedCallback |Triggered when the PlatformView is created. |
|gestureRecognizers |Set? |Which gestures should be passed to the PlatformView. |


<span id="_6-rtcvideo-startvideocapture"></span>
#### 6. RTCVideo.startVideoCapture

Call `RTCVideo.startVideoCapture` to start internal video capture.

```dart
Future<void> startVideoCapture()
```


<span id="_7-rtcvideo-startaudiocapture"></span>
#### 7. RTCVideo.startAudioCapture

Call `RTCVideo.startAudioCapture` to start audio internal capturing.

```dart
Future<void> startAudioCapture()
```


<span id="_8-rtcvideo-creatertcroom"></span>
#### 8. RTCVideo.createRTCRoom

After initialization, you can call `RTCVideo.createRTCRoom` to create a room instance in order to call room\-related APIs.

```dart
Future<RTCRoom?> createRTCRoom(String roomId)
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |Room ID |


<span id="_9-rtcroom-setrtcroomeventhandler"></span>
#### 9. RTCRoom.setRTCRoomEventHandler

After successfully creating the room, you can call `RTCRoom.setRTCRoomEventHandler` to set up the room event callback handler.

```dart
void setRTCRoomEventHandler(RTCRoomEventHandler eventHandler)
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|eventHandler |RTCRoomEventHandler |Room event callback handler. |


<span id="_10-rtcroom-joinroom"></span>
#### 10. RTCRoom.joinRoom

Call `RTCRoom.joinRoom` to join a room.

```dart
Future<int?> joinRoom(
    {required String token,
    required UserInfo userInfo,
    required RoomConfig roomConfig})
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |String |Dynamic key for authentication and verification of users entering the room.<br><br><br>* You can use the console to generate a temporary token for testing, but should use the key SDK to generate and issue a token on your server for official launch.<br><br>* Apps with different AppIDs cannot communicate with each other. Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise, the user will fail to join the room. |
|userInfo |UserInfo |User information. |
|roomConfig |RoomConfig |Room configuration, setting the room mode and whether to automatically publish or subscribe to streams. |


<span id="_11-rtcroomeventhandler-onroomstatechanged"></span>
#### 11. RTCRoomEventHandler.onRoomStateChanged

After joining a room, you need to handle the first join/rejoin event in `RTCRoomEventHandler.onRoomStateChanged`.

```dart
typedef OnRoomStateChangedType = void Function(
    String roomId, String uid, int state, String extraInfo);
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |The ID of the room where the state change occurred. |
|uid |String |The ID of the user whose state has changed. |
|state |int |Room status code:<br><br><br>* 0: Success<br><br>* !0: Failure, see ErrorCode and WarningCode for details. |
|extraInfo |String |Extra information.<br><br><br>* joinType: 0 represents joining the room for the first time, 1 represents a reconnection into the room.<br><br>* elapsed: The time interval (in ms) between the local user calling RTCRoom.joinRoom and successfully entering the room. |


<span id="_12-rtcroomeventhandler-onuserjoined"></span>
#### 12. RTCRoomEventHandler.onUserJoined

After joining the room, you need to handle the event of the remote user joining the room in `RTCRoomEventHandler.onUserJoined`.

```dart
typedef OnUserJoinedType = void Function(UserInfo userInfo, int elapsed);
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|userInfo |UserInfo |User information. |
|elapsed |int |This field is reserved and not currently used. |


<span id="_13-rtcvideoeventhandler-onfirstremotevideoframerendered"></span>
#### 13. RTCVideoEventHandler.onFirstRemoteVideoFrameRendered

After joining the room, you need to handle the event in the `RTCVideoEventHandler.onFirstRemoteVideoFrameRendered` after the first frame of the remote video stream is successfully rendered on the view.

```dart
typedef OnFirstRemoteVideoFrameRenderedType = void Function(RemoteStreamKey streamKey,VideoFrameInfo videoFrameInfo);
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamKey |RemoteStreamKey |Information about the remote stream. |
|videoFrameInfo |VideoFrameInfo |Information about the video frame. |


<span id="_14-rtcviewcontext-remotecontext"></span>
#### 14. RTCViewContext.remoteContext

After receiving the onFirstRemoteVideoFrameRendered callback, you need to set up the remote view to see the remote video during the call. Build the RTCSurfaceView with the created RTCViewContext instance.

```dart
RTCViewContext.remoteContext(
    {required this.roomId,
    required this.uid,
    this.streamType = StreamIndex.main})
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |String |Room ID |
|uid |String |ID of the remote user who published the video frame. |
|streamType |StreamIndex |Stream type. Mainstream by default. |


<span id="_15-rtcroomeventhandler-onuserleave"></span>
#### 15. RTCRoomEventHandler.onUserLeave

After joining the room, you need to handle the remote user leaving the room event in `RTCRoomEventHandler.onUserLeave`.

```dart
typedef OnUserLeaveType = void Function(String uid,int reason);
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |String |ID of the user who left the room. |
|reason |int |The reason why the user left the room. |


<span id="_16-rtcroom-leaveroom"></span>
#### 16. RTCRoom.leaveRoom

To end a call, call `RTCRoom.leaveRoom`. This action releases all resources related to the call.

```dart
Future<int?> leaveRoom()
```


<span id="_17-rtcroom-destroy"></span>
#### 17. RTCRoom.destroy

When you no longer need the RTC room instance, you can call `RTCRoom.destroy` to destroy the room instance and release all related resources.

```dart
Future<void> destroy()
```


<span id="_18-rtcvideo-destroy"></span>
#### 18. RTCVideo.destroy

After all business scenarios related to the RTC engine are over, you can call `RTCVideo.destroy` to destroy the engine instance and release all related resources.

```dart
Future<void> destroy()
```


Now you have completed a basic video call.
