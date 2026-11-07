---
title: "iOS with Objective-C"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70133"
---

With the BytePlus RTC SDK, you can build a basic app for real\-time video calls. For the complete sample code of the demo project, see [Demo Project](https://docs.byteplus.com/en/docs/12/docs-1163793).

<span id="prerequisites"></span>
## Prerequisites


* Xcode 12.5 or above

* iOS 11.0 or above

* Objective\-C as the programming language

* Make sure your project has a valid developer signature set up

* Get an [Appid](https://docs.byteplus.com/en/docs/12/docs-69865)

* Download [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707#download-sdk)


<span id="integrate-the-sdk"></span>
## Integrate the SDK

<span id="step-1-optional-create-a-project"></span>
### Step 1: (Optional) Create a project

> Note: This step helps you create a new project. Skip this step if you want to integrate BytePlus RTC into an existing project.


1. Open **Xcode** and click **File \> New \> Project**.

2. Select **iOS \> Apps** and click **Next**.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70133_1.jpeg) </span>

3. Enter the project name and team name, select **Objective\-C** as the development language, and then click Next.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70133_2.png) </span>

4. Select the project storage location and click **Create**.

5. For Signature Settings, go to **TARGETS \> Project Name \> Signing & Capabilities** and select the "Automatically manage signing" checkbox. If prompted, click **Enable Automatic**.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70133_3.png) </span>

<span id="step-2-unzip-the-sdk-and-copy-it-to-the-project-directory"></span>
### Step 2: Unzip the SDK and copy it to the project directory

Drag the following downloaded files into the project:


* `ByteplusRTC.xcframework`

* `RTCFFmpeg.xcframework` (for RTC SDK 3.50+)

* `RealXBase.xcframework` (for RTC SDK 3.57+)


<span id="step-3-configure-project-properties"></span>
### Step 3: Configure Project Properties


1. Configure audio & video permissions.

   a. Find the "info" file in the project.

   b. Click the plus icon (+) to add permissions for audio and video devices:

   * Privacy \- Microphone Usage Description and provide a reason for using the microphone in the Value field.

   * Privacy \- Camera Usage Description and provide a reason for using the camera in the Value field.

      <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70133_4.png) </span>

2. Close Bitcode.

   a. Choose **TARGETS \> Project Name \> Build Setting**.

   b. Select **All** and search for **bitcode**.

   c. Set Enable Bitcode to **NO**.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70133_5.png) </span>


 &nbsp;

3. SDK configuration.

a. Choose **TARGETS \> Project Name \> General**.

b. Select **Frameworks,Libraries,and Embedded Content**.

c. Set the following files to `Embed & Sign`:


* `ByteplusRTC.xcframework`

* `RTCFFmpeg.xcframework` (for RTC SDK 3.50+)

* `RealXBase.xcframework` (for RTC SDK 3.57+)

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3a3cf1c233131fd09b46c74e143dc12e.png) </span>


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

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/quickstart/70133_8.jpeg) </span>

   You can use the following snippet to build the user interface.


```objectivec
- (void)buildUI{
    self.view.backgroundColor = [UIColor whiteColor];
    
    UIEdgeInsets edgeInsets = UIEdgeInsetsZero;
    if (@available(iOS 11.0, *)) {
        edgeInsets = [UIApplication sharedApplication].keyWindow.safeAreaInsets;
    }
    
    [self.view addSubview:self.headerView];
    [self.headerView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.mas_equalTo(edgeInsets.top);
        make.left.right.equalTo(self.view);
        make.height.mas_equalTo(49);
    }];
    
     self.switchCameraBtn.frame = CGRectMake(22, 14, 26, 26);
    [self.headerView addSubview:self.switchCameraBtn];
    [self.switchCameraBtn mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.mas_equalTo(22);
        make.size.mas_equalTo(26);
        make.centerY.equalTo(self.headerView);
    }];
    
    [self.headerView addSubview:self.roomIdLabel];
    [self.roomIdLabel mas_makeConstraints:^(MASConstraintMaker *make) {
        make.center.equalTo(self.headerView);
        make.left.greaterThanOrEqualTo(self.switchCameraBtn.mas_right).mas_offset(22);
    }];
    self.roomIdLabel.text = [NSString stringWithFormat:@"RoomID: %@",self.roomID];
    
    [self.headerView addSubview:self.switchAudioRouteBtn];
    [self.switchAudioRouteBtn mas_makeConstraints:^(MASConstraintMaker *make) {
        make.right.mas_equalTo(-20);
        make.centerY.equalTo(self.headerView);
    }];
    
    [self.view addSubview: self.foooterView];
    [self.foooterView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.right.equalTo(self.view);
        make.bottom.equalTo(self.view).offset(-edgeInsets.bottom);
        make.height.mas_equalTo(49);
    }];
    
    [self.foooterView addSubview:self.localAudioBtn];
    [self.localAudioBtn mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.mas_equalTo(42);
        make.centerY.equalTo(self.foooterView);
    }];
    
    [self.foooterView addSubview:self.localVideoBtn];
    [self.localVideoBtn mas_makeConstraints:^(MASConstraintMaker *make) {
        make.right.mas_equalTo(-42);
        make.centerY.equalTo(self.foooterView);
    }];
    
    [self.foooterView addSubview:self.hangUpBtn];
    [self.hangUpBtn mas_makeConstraints:^(MASConstraintMaker *make) {
        make.center.equalTo(self.foooterView);
    }];
    
    [self.view addSubview:self.containerView];
    [self.containerView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.right.equalTo(self.view);
        make.top.equalTo(self.headerView.mas_bottom);
        make.bottom.equalTo(self.foooterView.mas_top);
    }];
    
    [self.containerView addSubview:self.localView];
    [self.localView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.left.equalTo(self.containerView);
        make.width.height.equalTo(self.containerView).multipliedBy(0.5);
    }];
    
    [self.containerView addSubview:self.firstRemoteView];
    [self.firstRemoteView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.right.equalTo(self.containerView);
        make.width.height.equalTo(self.containerView).multipliedBy(0.5);
    }];
    
    [self.containerView addSubview:self.secondRemoteView];
    [self.secondRemoteView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.bottom.left.equalTo(self.containerView);
        make.width.height.equalTo(self.containerView).multipliedBy(0.5);
    }];
    
    [self.containerView addSubview:self.thirdRemoteView];
    [self.thirdRemoteView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.bottom.right.equalTo(self.containerView);
        make.width.height.equalTo(self.containerView).multipliedBy(0.5);
    }];
}
```



2. Import header files

   Include SDK API in files that use the header files.


```Plain
#import <BytePlusRTC.framework/Headers/BytePlusRTC.h>
```



3. Call [createRTCEngine:delegate:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-creatertcengine-delegate) to create an engine instance to use the various audio and video capabilities provided by RTC.


```objectivec
+ (ByteRTCEngine * _Nullable) createRTCEngine:(ByteRTCEngineConfig * _Nonnull) config
                                      delegate:(id<ByteRTCEngineDelegate> _Nullable)delegate;
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|`config` |`ByteRTCEngineConfig*` |Create engine parameter configuration, where AppID is the unique identifier of each application, randomly generated by the RTC console.<br><br>Instances generated with different AppIds are completely independent for audio and video calls in RTC and cannot interoperate. |
|`delegate` |`id<ByteRTCEngineDelegate>` |The delegate that receives callbacks from the SDK. See [ByteRTCEngineDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#bytertcenginedelegate) |



4. Call [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setlocalvideocanvas) to set the local view.


```objectivec
- (int)setLocalVideoCanvas:(ByteRTCVideoCanvas * _Nullable)canvas;
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|`canvas` |`ByteRTCVideoCanvas*` |View information and rendering mode, see [ByteRTCVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcvideocanvas) |



5. Call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startvideocapture) to start video capture.


```objectivec
- (void)startVideoCapture;
```



6. Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startaudiocapture) to start audio capture.


```objectivec
- (void)startAudioCapture;
```



7. Call [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-creatertcroom) to create an RTC room.


```objectivec
- ( ByteRTCRoom * _Nullable)createRTCRoom:(NSString * _Nonnull)roomId;
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomId |NSString\* |roomId is a non\-empty string within 128 bytes. Each room created by calling this API requires a unique roomId. This ensures that each room is uniquely identifiable. The following character sets are supported:<br><br>• 26 uppercase letters A~Z<br><br>• 26 lowercase letters a~z<br><br>• 10 numbers: 0~9<br><br>• Underscore "_", at sign "@" , and minus sign "\-" |



8. Call [setRTCRoomDelegate](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-setrtcroomdelegaterts) to set the room delegate.


```objectivec
- (int)setRTCRoomDelegate:(id<ByteRTCRoomDelegate> _Nullable)roomDelegate;
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|`roomDelegate` |`id<ByteRTCRoomDelegate>` |参看 [ByteRTCRoomDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#bytertcroomdelegate)。 |



9. Call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#joinroom-userinfo-uservisibility-roomconfig) to join an RTC room.


```objectivec
- (int)joinRoom:(NSString *_Nullable)token userInfo:(ByteRTCUserInfo *_Nonnull)userInfo userVisibility:(BOOL)userVisibility roomConfig:(ByteRTCRoomConfig *_Nonnull)roomConfig;
```


**Parameters**


|Parameter name |Type |Description |
|---|---|---|
|`token` |`NSString*` |Dynamic key for authenticating users who join the room.<br><br>A token is required to enter a room. For testing, you can use the console to generate a temporary token. For production, you need to use the key SDK to generate and issue tokens on your server.<br><br>Apps with different AppIDs cannot communicate with each other.<br><br>Make sure that the AppID used to generate the token is the same as the AppID used when creating the engine, otherwise joining the room will fail. |
|`userInfo` |`ByteRTCUserInfo*` |User ID. See [ByteRTCUserInfo](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcuserinfo). |
|`userVisibility` |`BOOL` |Indicates whether the user is visible. It is recommended to set the user visibility to `false` when entering the room, and then set it to `true` via `setUserVisibility` when the user needs to send audio and video streams. This operation will fail when the number of users in the RTC room reaches the upper limit. An RTC room can accommodate up to 50 visible users and can publish 30 media streams at the same time. For more information, see[Room Capacity](https://docs.byteplus.com/6uofwzl3/14302). |
|`roomConfig` |`ByteRTCRoomConfig*` |Room parameter configuration, set the room mode and whether to automatically publish or subscribe to streams. For specific configuration modes, see [ByteRTCRoomConfig](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcroomconfig). |



10. Listen for room status changes via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70087#onroomstatechanged-withuid-state-extrainfo).


```objectivec
- (void)rtcRoom:(ByteRTCRoom *_Nonnull)rtcRoom
    onRoomStateChanged:(NSString *_Nonnull)roomId
             withUid:(nonnull NSString *)uid
           state:(NSInteger)state
           extraInfo:(NSString *_Nonnull)extraInfo;
```


**Parameters**


|Parameter name |Type |Description |
|---|---|---|
|`rtcRoom` |`ByteRTCRoom*` |`ByteRTCRoom` object. |
|`roomId` |`NSString*` |Room ID |
|`uid` |`NSString*` |User ID |
|`state` |`NSInteger` |Room status code.<br><br>• `0`: Success.<br><br>• `!0`: Failure, for specific reasons, see [ByteRTCErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#bytertcerrorcode) and [ByteRTCWarningCode](https://docs.byteplus.com/en/docs/12/docs-70085#bytertcwarningcode). |
|`extraInfo` |`NSString*` |Extra information, such as `{"elapsed":1187,"join_type":0}`. In this object,<br><br>`joinType` indicates how the user joined the room: `0` for the first time and `1` for a reconnection.<br><br>`elapsed` is the time in milliseconds (ms) from calling `joinRoom:userInfo:roomConfig:` until the user successfully joins the room. |



11. Handle the callback for remote users joining the room via [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70087#onuserjoined)


```objectivec
- (void)rtcRoom:( ByteRTCRoom *_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo *_Nonnull)userInfo;
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|userInfo |ByteRTCUserInfo\* |Contains user information. See [ByteRTCUserInfo](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcuserinfo). |



12. Handle the callback for the first frame of remote video decoding via [onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70087#onfirstremotevideoframedecoded-info-withframeinfo).


```objectivec
- (void)rtcEngine:(ByteRTCEngine * _Nonnull)engine onFirstRemoteVideoFrameDecoded:(NSString * _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info withFrameInfo:(ByteRTCVideoFrameInfo * _Nonnull)frameInfo;
```


**Parameters**


|Parameter name |Type |Description |
|---|---|---|
|`engine` |`ByteRTCEngine*` |ByteRTCEngine object |
|`streamId` |`NSString*` |Remote stream ID |
|`info` |`ByteRTCStreamInfo*` |Remote stream information, see [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcstreaminfo) |
|`frameInfo` |`ByteRTCVideoFrameInfo*` |Video frame information, see [ByteRTCVideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcvideoframeinfo) |



13. Set the remote view via [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas).


```objectivec
- (int)setRemoteVideoCanvas:(NSString* _Nonnull)streamId
             withCanvas:(ByteRTCVideoCanvas * _Nullable)canvas;

```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|`streamId` |`NSString*` |Remote stream ID |
|`canvas` |`ByteRTCVideoCanvas*` |View information and rendering mode, see [ByteRTCVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcvideocanvas) |



14. Handle the callback for remote users leaving the room via [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70087#onuserleave-reason)


```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserLeave:(NSString*_Nonnull)uid reason:(ByteRTCUserOfflineReason)reason;
```


**Parameters**


|Name |Type |Instructions |
|---|---|---|
|`uid` |`NSString*` |The ID of the remote user who left the room. |
|`reason` |`ByteRTCUserOfflineReason` |The reason why the user left the room, see [ByteRTCUserOfflineReason](https://docs.byteplus.com/en/docs/12/docs-70088#bytertcuserofflinereason). |



15. Call [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#leaveroom) to leave the room.


```objectivec
- (int)leaveRoom;
```



16. Call [destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-destroyrtcengine) to destroy the engine instance.


```objectivec
+ (void)destroyRTCEngine;
```


When you have finished using the RTC engine instance, call `destroyRTCEngine` to destroy the instance and release all related resources.

Now you have completed a basic video call.
