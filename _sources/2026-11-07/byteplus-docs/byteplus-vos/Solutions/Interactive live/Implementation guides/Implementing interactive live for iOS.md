---
title: "Implementing interactive live for iOS"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-interactive-live-for-ios"
---

To implement a complete interactive live streaming feature in your iOS app, this guide provides comprehensive instructions and code samples. You will learn how to use the BytePlus MediaLive and RTC SDKs to build the entire workflow for both hosts and audiences, covering key functionalities such as starting a stream, enabling co\-hosting, playing live video, and managing the session lifecycle.

<span id="system-requirements"></span>
## System requirements


* A physical iPhone or iPad running iOS 11 or higher

* Xcode 14.1 or higher


<span id="prerequisites"></span>
## Prerequisites


* A valid [BytePlus account](http://console.byteplus.com/) with [BytePlus MediaLive](https://console.byteplus.com/live) and [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC) activated.

* You have completed the [basic setup for live streaming](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started).

* You have obtained a BytePlus MediaLive SDK license.

   * For detailed instructions on how to acquire the license, see [Accessing your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license).

   * To learn more about choosing the right license type for your needs, please refer to [SDK introduction](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction).

* You have obtained the BytePlus MediaLive SDK package. To access the interactive live streaming feature, you must use the Interactive edition of the SDK. See [Accessing your SDK package](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-package) for more information.


<span id="integrating-the-sdks"></span>
## Integrating the SDKs

This section introduces how to integrate BytePlus MediaLive Broadcast and Player SDKs into your iOS project.

<span id="importing-the-sdks"></span>
### Importing the SDKs


1. Install Ruby on your Mac and run the following command in Terminal to install CocoaPods.

   ```Plain
   sudo gem install cocoapods
   ```
   

2. Run the following command in your project directory to create a Podfile.

   ```Plain
   pod init
   ```
   

3. Add the following dependencies for the SDKs to your Podfile.

   ```Plain
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   source 'https://github.com/volcengine/volcengine-specs.git'
   pod 'TTSDK', '1.48.200.2-premium', :subspecs => ['LivePull-RTS', 'RTCSDK']
   ```
   

4. Execute the following command in Terminal to update the local libraries and install the SDK.

   ```Plain
   pod install
   ```
   


<span id="configuring-permissions"></span>
### Configuring permissions

To record video and audio, you need to request camera and microphone permissions. To do so, include the following keys in `info.plist`:


* NSCameraUsageDescription

* NSMicrophoneUsageDescription


You can use the following code to request permissions for the camera and microphone:

```objectivec
- (void)requestCameraAuthorization:(void (^)(BOOL granted))handler {
    AVAuthorizationStatus authStatus = [AVCaptureDevice authorizationStatusForMediaType:AVMediaTypeVideo];
    if (authStatus == AVAuthorizationStatusNotDetermined) {
        [AVCaptureDevice requestAccessForMediaType:AVMediaTypeVideo completionHandler:^(BOOL granted) {
            handler(granted);
        }];
    } else if (authStatus == AVAuthorizationStatusAuthorized) {
        handler(YES);
    } else {
        handler(NO);
    }
}

- (void)requestMicrophoneAuthorization:(void (^)(BOOL granted))handler {
    AVAuthorizationStatus authStatus = [AVCaptureDevice authorizationStatusForMediaType:AVMediaTypeAudio];
    if (authStatus == AVAuthorizationStatusNotDetermined) {
        [AVCaptureDevice requestAccessForMediaType:AVMediaTypeAudio completionHandler:^(BOOL granted) {
            handler(granted);
        }];
    } else if (authStatus == AVAuthorizationStatusAuthorized) {
        handler(YES);
    } else {
        handler(NO);
    }
}

- (void)requestAuthorization {
    [self requestCameraAuthorization:^(BOOL granted) {
        if (granted) {
            NSLog(@"camera Authorization succeeds!");
        } else {
            NSLog(@"camera Authorization fails!");
        }
    }];
    [self requestMicrophoneAuthorization:^(BOOL granted) {
        if (granted) {
            NSLog(@"microphone Authorization succeeds!");
        } else {
            NSLog(@"microphone Authorization fails!");
        }
    }];
}
```


<span id="adding-a-license"></span>
### Adding a license

Copy the license file to your project directory and note the path to the license file.

Make sure the bundle ID associated with the license file is the same as that of your project. Otherwise, the license authentication will fail.

<span id="implementing-code-obfuscation"></span>
### Implementing code obfuscation

iOS apps do not require code obfuscation by default. However, if you need to obfuscate your code to protect intellectual property, you can use third\-party tools such as [ProGuard for iOS](https://github.com/facebook/FBRetainCycleDetector) or [llvm-obfuscator](https://github.com/obfuscator-llvm/obfuscator).

<span id="initializing-the-sdk"></span>
### Initializing the SDK

Initialize the SDK with the following code:

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Your code.
    [self configTTSDK];
    // Your code.
    return YES;
}

- (void)configTTSDK {
    // Create TTSDKConfiguration with your App ID.
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"Your App ID" licenseName:@"Your License Name"];
    // Configure your application information.
    configuration.appName = @"Your application name";
    configuration.channel = @"Your app channel";
    configuration.bundleID = @"Your bundle ID";

    // Pass TTSDKConfiguration to TTSDKManager.
    [TTSDKManager startWithConfiguration:configuration];
}
```


The following table contains a detailed description for each parameter required for initialization:


|**Parameter** |**Required** |**Data Type** |**Description** |**Example** |
|---|---|---|---|---|
|AppID |Yes |String |App ID, which is the unique identifier of your SDK application. |`123456` |
|appName |Yes |String |Application name, which is the name of your SDK application. |`video_demo` |
|channel |No |String |The channel through which to download the app. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging. |`appstore` |
|bundleID |Yes |String |The package name of your iOS app (i.e., the `bundleId` value of your project's main target). |`com.byteplus.video.ios` |
|licenseFilePath |Yes |String |The path to the license file. |`live.lic` |


<span id="uploading-logs"></span>
### Uploading logs

By default, automatic SDK log uploading is enabled for debugging and analytics. To protect confidential data, you can manually disable it by setting `shouldInitAppLog` to `NO` in `TTSDKConfiguration`.

```objectivec
- (void)configTTSDK {
    //....
    configuration.shouldInitAppLog = NO;
    [TTSDKManager setShouldReportToAppLog:NO];
    //....
}
```


<span id="implementing-the-feature-for-the-host"></span>
## Implementing the feature for the host

This section provides instructions on implementing the interactive live streaming feature for the host.

<span id="starting-the-live-stream"></span>
### Starting the live stream

The host uses the RTC engine for audio and video capture and the RTC mixed\-stream CDN pushing feature to start a stream.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075156-1271852145783.png) </span>

**Sample code**


1. Create an RTC engine and configure the engine parameters.

   ```objectivec
   // Create the RTC engine configuration
   ByteRTCEngineConfig *config = [[ByteRTCEngineConfig alloc] init];
   config.appID = @"Your App ID";
   
   // Create the RTC engine instance
   self.rtcEngineKit = [ByteRTCEngine createRTCEngine:config delegate:self];
   ```
   

2. Configure the video capture and encoding parameters.

   ```objectivec
   // Set the video capture configuration
   ByteRTCVideoCaptureConfig *captureConfig = [[ByteRTCVideoCaptureConfig alloc] init];
   captureConfig.videoSize = CGSizeMake(720, 1280);
   captureConfig.frameRate = 15;
   captureConfig.preference = ByteRTCVideoCapturePreferenceAutoPerformance;
   [self.rtcEngineKit setVideoCaptureConfig:captureConfig];
   
   // Set the video encoding configuration
   ByteRTCVideoEncoderConfig *encoderConfig = [[ByteRTCVideoEncoderConfig alloc] init];
   encoderConfig.width = 720;
   encoderConfig.height = 1280;
   encoderConfig.frameRate = 15;
   encoderConfig.maxBitrate = 1600;
   [self.rtcEngineKit setVideoEncoderConfig:encoderConfig];
   ```
   

3. Set the local preview view.

   ```objectivec
   // Set the local preview
   ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
   canvas.view = self.localView;
   canvas.renderMode = ByteRTCRenderModeHidden;
   [self.rtcEngineKit setLocalVideoCanvas:canvas];
   ```
   

4. Join the RTC room and start audio and video capture.

   ```objectivec
   // Start video capture
   [self.rtcEngineKit startVideoCapture];
   
   // Start audio capture
   [self.rtcEngineKit startAudioCapture];
   
   // Create the RTC room
   self.rtcRoom = [self.rtcEngineKit createRTCRoom:rtcRoomId];
   [self.rtcRoom setRTCRoomDelegate:self];
   
   // Set user information
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = userId;
   
   // Configure the RTC room
   ByteRTCRoomConfig *rtcRoomConfig = [[ByteRTCRoomConfig alloc] init];
   rtcRoomConfig.profile = ByteRTCRoomProfileInteractivePodcast;
   rtcRoomConfig.isPublishAudio = YES;
   rtcRoomConfig.isPublishVideo = YES;
   rtcRoomConfig.isAutoSubscribeAudio = YES;
   rtcRoomConfig.isAutoSubscribeVideo = YES;
   
   // Join the RTC room
   [self.rtcRoom joinRoom:rtcToken
                  userInfo:userInfo
            userVisibility:YES
                roomConfig:rtcRoomConfig];
   ```
   

5. After successfully joining the room, start pushing the mixed RTC stream to CDN.

   ```objectivec
   // Callback for successful room entry
   - (void)rtcRoom:(ByteRTCRoom *)rtcRoom
      onRoomStateChanged:(NSString *)roomId
                   withUid:(NSString *)uid
                     state:(NSInteger)state
                 extraInfo:(NSString *)extraInfo {
       if (state == 0) {
           // Start pushing the mixed stream to CDN
           [self startPushMixedStream];
       }
   }
   
   - (void)startPushMixedStream {
       // Create the mixed stream configuration
       ByteRTCMixedStreamConfig *mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.roomID = rtcRoomId;
       mixedStreamConfig.userID = userId;
       mixedStreamConfig.backgroundColor = @"#0D0B53";
   
       // Configure video encoding parameters
       ByteRTCMixedStreamVideoConfig *videoConfig = [ByteRTCMixedStreamVideoConfig new];
       videoConfig.videoCodec = kCMVideoCodecType_H264;
       videoConfig.width = 720;
       videoConfig.height = 1280;
       videoConfig.fps = 15;
       mixedStreamConfig.videoConfig = videoConfig;
   
       // Configure audio encoding parameters
       ByteRTCMixedStreamAudioConfig *audioConfig = [ByteRTCMixedStreamAudioConfig new];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 44100;
       audioConfig.channels = 2;
       audioConfig.bitrate = 64;
       mixedStreamConfig.audioConfig = audioConfig;
   
       // Configure the layout for the host
       ByteRTCMixedStreamLayoutRegionConfig *region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.userID = userId;
       region.roomID = rtcRoomId;
       region.isLocalUser = YES;
       region.renderMode = ByteRTCMixedStreamRenderModeHidden;
       region.locationX = 0.0;
       region.locationY = 0.0;
       region.width = 720;
       region.height = 1280;
       region.zOrder = 1;
       region.alpha = 1.0;
   
       // Set the layout configuration
       mixedStreamConfig.layoutMode = ByteRTCStreamLayoutModeCustom;
       mixedStreamConfig.regions = @[region];
   
       // Configure the push target
       ByteRTCMixedStreamPushTargetConfig *pushTargetConfig = [ByteRTCMixedStreamPushTargetConfig new];
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       pushTargetConfig.pushCDNURL = pushUrl;
   
       // Task ID for the mixed stream push
       NSString *taskId = @"pushCDNtaskId_001";
   
       // Start pushing the mixed stream to CDN
       [self.rtcEngineKit startPushMixedStream:taskId
                          withPushTargetConfig:pushTargetConfig
                              withMixedConfig:mixedStreamConfig];
   }
   ```
   


<span id="enabling-beauty-ar-optional"></span>
### Enabling beauty AR (Optional)

Refer to [Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717) for detailed instructions on how to implement beauty AR by using the RTC engine.

<span id="starting-a-host-pk-battle"></span>
### Starting a host PK battle

To start a host PK battle with another host, you need to start cross\-room stream forwarding and update the mixed stream layout.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075211-1041707050688.png) </span>

**Sample code**


1. When Host A receives the notification of starting the PK battle successfully, call `startForwardStreamToRooms` to push Host A's stream to Host B's room. Similarly, Host B needs to call `startForwardStreamToRooms` to push Host B's stream to Host A's room.

   ```objectivec
       // Push one's flow to the opposite room
       ByteRTCForwardStreamConfiguration *forwardConfig = [[ByteRTCForwardStreamConfiguration alloc] init];
       forwardConfig.roomId = targetRoomId;
       forwardConfig.token = token;
       [self.rtcRoom startForwardStreamToRooms:@[forwardConfig]];
   
   ```
   

2. Adjust the video encoding parameters for PK (reduce to half resolution), then update the push\-to\-CDN layout.

   ```objectivec
   
       // Set the stream push configuration, including the URL for the mixed stream to be pushed to
       ByteRTCMixedStreamPushTargetConfig *pushTargetConfig = [ByteRTCMixedStreamPushTargetConfig new];
       pushTargetConfig.pushCDNURL = mTargetUrl;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
   
       // Set video encoding parameters for transcoding
       ByteRTCMixedStreamVideoConfig *videoConfig = [ByteRTCMixedStreamVideoConfig new];
       videoConfig.fps = myConfig.frameRate;
       videoConfig.height = myConfig.height;
       videoConfig.width = myConfig.width;
       videoConfig.bitrate = myConfig.bitRate;
       self.mixedStreamConfig.videoConfig = videoConfig;
   
       // Set audio encoding parameters for transcoding
       ByteRTCMixedStreamAudioConfig *audioConfig = [ByteRTCMixedStreamAudioConfig new];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.bitrate = 128;
       audioConfig.channels = 2;
       audioConfig.sampleRate = 48000;
       self.mixedStreamConfig.audioConfig = audioConfig;
   
       // Update the push-to-CDN layout from a 1-person layout to a 2-person layout
       NSMutableArray *regions = [[NSMutableArray alloc] init];
       ByteRTCMixedStreamLayoutRegionConfig *localRegion = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       localRegion.userID = userId;
       localRegion.roomID = rtcRoomId;
       localRegion.isLocalUser = YES;
       localRegion.locationX = 0;
       localRegion.locationY = 0;
       localRegion.width = (int) (myConfig.width * 0.5);
       localRegion.height = (int) (myConfig.height * 0.5);
       localRegion.alpha = 1;
       localRegion.zOrder = 0;
       localRegion.mediaType = ByteRTCMixedStreamMediaTypeAudioAndVideo;
       localRegion.renderMode = ByteRTCMixedStreamRenderModeHidden;
       [regions addObject:localRegion];
   
       ByteRTCMixedStreamLayoutRegionConfig *remoteRegion = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       remoteRegion.userID = userId;
       remoteRegion.roomID = rtcRoomId;
       remoteRegion.isLocalUser = NO;
       remoteRegion.locationX = (int) (myConfig.width * 0.5);
       remoteRegion.locationY = 0;
       remoteRegion.width = (int) (myConfig.width * 0.5);
       remoteRegion.height = (int) (myConfig.height * 0.5);
       remoteRegion.alpha = 1;
       remoteRegion.zOrder = 0;
       remoteRegion.mediaType = ByteRTCMixedStreamMediaTypeAudioAndVideo;
       remoteRegion.renderMode = ByteRTCMixedStreamRenderModeHidden;
       [regions addObject:remoteRegion];
   
       // Update the layout
       self.mixedStreamConfig.regions = regions;
   
       // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream
       NSString *taskId = @"";
   
       // Update the stream push parameters
       [self.rtcEngineKit updatePushMixedStream:taskId
                            withPushTargetConfig:pushTargetConfig
                                withMixedConfig:self.mixedStreamConfig];
   ```
   


<span id="ending-the-host-pk-battle"></span>
### Ending the host PK battle

To end the host PK battle, stop cross\-room stream forwarding and restore the single\-host mixed stream layout.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075224-1778673591057.png) </span>

**Sample code**


1. When Host A receives the notification of ending the PK battle successfully, call `stopForwardStreamToRooms` to stop pushing Host A's stream to Host B's room. Similarly, Host B needs to call `stopForwardStreamToRooms` to stop pushing Host B's stream to Host A's room.

   ```objectivec
       // Stop pushing Host A's stream to Host B's room.
       [self.rtcRoom stopForwardStreamToRooms];
   
       // Stop pushing Host B's stream to Host A's room.
       [self.rtcRoom stopForwardStreamToRooms];
   
   ```
   

2. Resume the video encoding parameters to the original resolution, then update the push\-to\-CDN layout back to a 1\-person layout.

   ```objectivec
   
       ByteRTCMixedStreamLayoutRegionConfig *localRegion = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       localRegion.userID = localUserId;
       localRegion.roomID = rtcRoomId;
       localRegion.isLocalUser = YES;
       localRegion.renderMode = ByteRTCMixedStreamRenderModeHidden;
       localRegion.locationX = 0.0;
       localRegion.locationY = 0.0;
       localRegion.width = videoWidth;
       localRegion.height = videoHeight;
       localRegion.zOrder = 1;
       localRegion.alpha = 1.0;
   
       // Update the layout
       self.mixedStreamConfig.regions = @[localRegion];
   
       // Update the mixed stream push configuration
       [self.rtcEngineKit updatePushMixedStream:taskId
                            withPushTargetConfig:self.mixedStreamPushConfig
                                withMixedConfig:self.mixedStreamConfig];
   ```
   


<span id="ending-the-live-stream"></span>
### Ending the live stream

To end the live stream, stop pushing the mixed stream, stop audio and video capture, leave the room, and destroy the engine.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075235-1544626653002.png) </span>

**Sample code**


1. Stop pushing the mixed stream to CDN.

   ```objectivec
   // Stop pushing the mixed stream to CDN
   [self.rtcEngineKit stopPushMixedStream:taskId
                       withPushTargetType:ByteRTCMixedStreamPushTargetTypeToCDN];
   ```
   

2. Stop audio and video capture and remove the local preview.

   ```objectivec
   // Stop video capture
   [self.rtcEngineKit stopVideoCapture];
   
   // Stop audio capture
   [self.rtcEngineKit stopAudioCapture];
   
   // Remove the local preview
   ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
   canvas.view = nil;
   canvas.renderMode = ByteRTCRenderModeHidden;
   [self.rtcEngineKit setLocalVideoCanvas:canvas];
   ```
   

3. Leave the RTC room and the RTS business room.

   ```objectivec
   // Leave the RTC room
   [self.rtcRoom leaveRoom];
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   ```
   

4. Destroy the RTC engine.

   ```objectivec
   // Destroy the RTC engine
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngineKit = nil;
   ```
   


<span id="implementing-the-feature-for-the-audience"></span>
## Implementing the feature for the audience

<span id="playing-the-live-stream"></span>
### Playing the live stream

Use the live player to pull and play the live stream from CDN.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075247-965399141699.png) </span>

**Sample code**


1. Create a live player and configure it.

   ```objectivec
   // Create a live player
   BytedPlayerProtocol *player = [[BytedPlayerProtocol alloc] init];
   self.livePlayer = player;
   
   // Configure the player
   [self.livePlayer startWithConfiguration];
   ```
   

2. Set the playback address, parent view, and SEI callback.

   ```objectivec
   // Set the pull stream address, default resolution, parent view, and SEI callback
   NSDictionary *urlMap = @{
       @"720p": pullUrl720p,
       @"540p": pullUrl540p
   };
   
   [self.livePlayer setPlayerWithUrlMap:urlMap
                      defaultResolution:@"720p"
                              superView:self.view
                               SEIBlcok:^(NSDictionary *SEIDic) {
       // Process SEI data
       NSLog(@"SEI data: %@", SEIDic);
   }];
   ```
   

3. Start playing.

   ```objectivec
   // Start playing
   [self.livePlayer play];
   ```
   


<span id="becoming-a-co-host"></span>
### Becoming a co\-host

To become a co\-host, stop playing the CDN stream, join the RTC room, and enable audio and video capture.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075258-613011345943.png) </span>

**Sample code**


1. Stop playing the CDN stream.

   ```objectivec
   // Stop playing
   [self.livePlayer stop];
   ```
   

2. Join the RTC room and start audio and video capture.

   ```objectivec
   
       // Configure the video encoding parameters for the guest
       ByteRTCVideoEncoderConfig *encoderConfig = [[ByteRTCVideoEncoderConfig alloc] init];
       encoderConfig.width = 256;
       encoderConfig.height = 256;
       encoderConfig.frameRate = 15;
       encoderConfig.maxBitrate = 124;
       [self.rtcEngineKit setVideoEncoderConfig:encoderConfig];
   
       // Start video capture
       [self.rtcEngineKit startVideoCapture];
   
       // Start audio capture
       [self.rtcEngineKit startAudioCapture];
   
       // Set the local preview
       ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
       canvas.view = self.localView;
       canvas.renderMode = ByteRTCRenderModeHidden;
       [self.rtcEngineKit setLocalVideoCanvas:canvas];
   
       // Create the RTC room
       self.rtcRoom = [self.rtcEngineKit createRTCRoom:rtcRoomId];
       [self.rtcRoom setRTCRoomDelegate:self];
   
       // Set user information
       ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
       userInfo.userId = userId;
   
       // Configure the RTC room
       ByteRTCRoomConfig *rtcRoomConfig = [[ByteRTCRoomConfig alloc] init];
       rtcRoomConfig.profile = ByteRTCRoomProfileInteractivePodcast;
       rtcRoomConfig.isPublishAudio = YES;
       rtcRoomConfig.isPublishVideo = YES;
       rtcRoomConfig.isAutoSubscribeAudio = YES;
       rtcRoomConfig.isAutoSubscribeVideo = YES;
   
       // Join the RTC room
       [self.rtcRoom joinRoom:rtcToken
                      userInfo:userInfo
                userVisibility:YES
                    roomConfig:rtcRoomConfig];
   ```
   

3. After receiving the remote user's stream publishing notification, set the remote video view.

   ```objectivec
   - (void)rtcRoom:(ByteRTCRoom *)rtcRoom
   onUserPublishStreamVideo:(NSString *)streamId
                      info:(ByteRTCStreamInfo *)info
                 isPublish:(BOOL)isPublish {
       if (isPublish) {
           // Set the remote video view
           ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
           canvas.view = remoteView;
           canvas.renderMode = ByteRTCRenderModeHidden;
   
           ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
           streamKey.userId = info.userId;
           streamKey.roomId = rtcRoom.getRoomId;
           streamKey.streamIndex = ByteRTCStreamIndexMain;
   
           [self.rtcEngineKit setRemoteVideoCanvas:info.streamId withCanvas:canvas];
       }
   }
   ```
   


<span id="enabling-beauty-ar-optional"></span>
### Enabling beauty AR (Optional)

Refer to [Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717) for detailed instructions on how to implement beauty AR by using the RTC engine.

<span id="ending-co-hosting"></span>
### Ending co\-hosting

To end co\-hosting and return to being a regular audience member, leave the RTC room, stop audio and video capture, and resume CDN playback.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075310-1581069071585.png) </span>

**Sample code**


1. Leave the RTC room, stop audio and video capture, and remove the local and remote views. Resume CDN playback.

   ```objectivec
       // Leave the RTC room
       [self.rtcRoom leaveRoom];
       [self.rtcRoom destroy];
       self.rtcRoom = nil;
   
       // Remove the local preview
       ByteRTCVideoCanvas *localCanvas = [[ByteRTCVideoCanvas alloc] init];
       localCanvas.view = nil;
       localCanvas.renderMode = ByteRTCRenderModeHidden;
       [self.rtcEngineKit setLocalVideoCanvas:localCanvas];
   
       // Remove the remote view
       ByteRTCVideoCanvas *remoteCanvas = [[ByteRTCVideoCanvas alloc] init];
       remoteCanvas.view = nil;
       remoteCanvas.renderMode = ByteRTCRenderModeHidden;
       [self.rtcEngineKit setRemoteVideoCanvas:streamId withCanvas:remoteCanvas];
   
       // Stop video capture
       [self.rtcEngineKit stopVideoCapture];
   
       // Stop audio capture
       [self.rtcEngineKit stopAudioCapture];
   
       // Resume CDN playback
       [self.livePlayer play];
   
   ```
   


<span id="leaving-the-live-room"></span>
### Leaving the live room

To leave the live room, stop CDN playback, leave the RTS business room, and destroy the RTC engine.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075327-75511538399.png) </span>

**Sample code**


1. Stop playing the live stream, remove the view for the player, and destroy the live player.

   ```objectivec
   // Stop playing
   [self.livePlayer stop];
   [self.livePlayer destroy];
   self.livePlayer = nil;
   ```
   

2. Leave the RTC room, stop audio and video capture, and destroy the RTC engine.


```objectivec
 // If co-hosting, leave the RTC room first
 [self.rtcRoom leaveRoom];
 [self.rtcRoom destroy];
 self.rtcRoom = nil;

 [self.rtcEngineKit stopVideoCapture];
 [self.rtcEngineKit stopAudioCapture];

 // Destroy the RTC engine
 [ByteRTCEngine destroyRTCEngine];
 self.rtcEngineKit = nil;

```
