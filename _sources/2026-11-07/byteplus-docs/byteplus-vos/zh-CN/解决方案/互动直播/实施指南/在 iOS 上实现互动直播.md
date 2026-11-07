---
title: "在 iOS 上实现互动直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-interactive-live-for-ios-zh-CN"
---

为在您的 iOS 应用中实现完整的互动直播功能，本指南提供了全面的操作说明和代码示例。您将学习如何使用 BytePlus MediaLive 和 RTC SDK 构建主播与观众的完整工作流程，涵盖启动直播、启用连麦、播放直播视频以及管理会话生命周期等关键功能。

<span id="8d09389f"></span>
## 系统要求


* 运行 iOS 11 或更高版本的实体 iPhone 或 iPad

* Xcode 14.1 或更高版本


<span id="ce425396"></span>
## 前置条件


* 已激活 [BytePlus 账号](http://console.byteplus.com/)，并开通 [BytePlus MediaLive](https://console.byteplus.com/live) 和 [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC)。

* 您已完成 [直播基础配置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 您已获得 BytePlus MediaLive SDK 许可证。

   * 有关获取许可证的详细说明，请参见 [访问您的 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需了解如何选择适合您需求的许可证类型，请参考 [SDK 介绍](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。

* 您已获得 BytePlus MediaLive SDK 包。要访问互动直播功能，必须使用 SDK 的互动版。更多信息请参见 [访问您的 SDK 包](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-package)。


<span id="d7a50fa4"></span>
## 集成 SDK

本节介绍如何将 BytePlus MediaLive 推流和播放器 SDK 集成到您的 iOS 项目中。

<span id="eaa6433a"></span>
### 安装 SDK


1. 在 Mac 上安装 Ruby，并在终端运行以下命令以安装 CocoaPods。

   ```Plain
   sudo gem install cocoapods
   ```
   

2. 在项目目录中运行以下命令以创建 Podfile。

   ```Plain
   pod init
   ```
   

3. 在 Podfile 中添加以下 SDK 依赖项。

   ```Plain
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   source 'https://github.com/volcengine/volcengine-specs.git'
   pod 'TTSDK', '1.48.200.2-premium', :subspecs => ['LivePull-RTS', 'RTCSDK']
   ```
   

4. 在终端执行以下命令以更新本地库并安装 SDK。

   ```Plain
   pod install
   ```
   


<span id="788c713d"></span>
### 权限申请

录制音视频时，需申请摄像头和麦克风权限。为此，请在 `info.plist` 中包含以下键：


* NSCameraUsageDescription

* NSMicrophoneUsageDescription


您可以使用以下代码申请摄像头和麦克风权限：

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


<span id="7539725a"></span>
### 添加许可证文件

将许可证文件复制到项目目录，并记录许可证文件路径。

确保许可证文件关联的 bundle ID 与您的项目一致。否则，许可证认证将失败。

<span id="1ad87597"></span>
### SDK 初始化

使用以下代码初始化 SDK：

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


下表详细说明了初始化所需的各参数：


|**参数** |**必填** |**数据类型** |**说明** |**示例** |
|---|---|---|---|---|
|AppID |是 |字符串 |App ID，即 SDK 应用的唯一标识符。 |`123456` |
|appName |是 |字符串 |应用名称，即 SDK 应用的名称。 |`video_demo` |
|channel |否 |字符串 |用于下载应用的渠道。您也可以使用该参数区分不同环境的应用构建，例如生产、测试和调试。 |`appstore` |
|bundleID |是 |字符串 |iOS 应用的包名（即项目主目标的 `bundleId` 值）。 |`com.byteplus.video.ios` |
|licenseFilePath |是 |字符串 |许可证文件的路径。 |`live.lic` |


<span id="7bdd8f3b"></span>
### 日志上传

默认情况下，SDK 自动上传日志以便调试和分析。为保护敏感数据，您可在 `TTSDKConfiguration` 中将 `shouldInitAppLog` 设置为 `NO`，以手动关闭日志上传。

```objectivec
- (void)configTTSDK {
    //....    
    configuration.shouldInitAppLog = NO;
    [TTSDKManager setShouldReportToAppLog:NO];
    //....
}
```


<span id="53373ec6"></span>
## 主播功能实现

本节介绍主播实现互动直播功能的操作说明。

<span id="8ccf9441"></span>
### 启动直播

主播使用 RTC 引擎进行音视频采集，并通过 RTC 混流推送至 CDN 功能来启动直播。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075156-1271852145783.png) </span>

**代码示例**


1. 创建 RTC 引擎并配置引擎参数。

   ```objectivec
   // Create the RTC engine configuration
   ByteRTCEngineConfig *config = [[ByteRTCEngineConfig alloc] init];
   config.appID = @"Your App ID";
   
   // Create the RTC engine instance
   self.rtcEngineKit = [ByteRTCEngine createRTCEngine:config delegate:self];
   ```
   

2. 配置视频采集和编码参数。

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
   

3. 设置本地预览视图。

   ```objectivec
   // Set the local preview
   ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
   canvas.view = self.localView;
   canvas.renderMode = ByteRTCRenderModeHidden;
   [self.rtcEngineKit setLocalVideoCanvas:canvas];
   ```
   

4. 加入 RTC 房间并启动音视频采集。

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
   

5. 成功加入房间后，开始将混合 RTC 流推送至 CDN。

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
   


<span id="40c58372"></span>
### 开启美颜 AR（可选）

请参阅[Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，了解如何通过 RTC 引擎实现美颜 AR 的详细操作说明。

<span id="e4d5322c"></span>
### 开启主播 PK

如需与其他主播进行主播 PK，您需要开启跨房间转推流，并更新混流布局。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075211-1041707050688.png) </span>

**示例代码**


1. 当主播 A 收到开始主播 PK 成功的通知时，调用 `startForwardStreamToRooms` 将主播 A 的流推送至主播 B 的房间。同样地，主播 B 需要调用 `startForwardStreamToRooms` 将主播 B 的流推送至主播 A 的房间。

   ```objectivec
       // Push one's flow to the opposite room
       ByteRTCForwardStreamConfiguration *forwardConfig = [[ByteRTCForwardStreamConfiguration alloc] init];
       forwardConfig.roomId = targetRoomId;
       forwardConfig.token = token;
       [self.rtcRoom startForwardStreamToRooms:@[forwardConfig]];
   
   ```
   

2. 调整用于 PK 的视频编码参数（降低至一半分辨率），然后更新推流至 CDN 的布局。

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
   


<span id="2ea653dd"></span>
### 结束主播 PK

如需结束主播 PK，请停止跨房间转推流，并将混流布局恢复为单主播布局。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075224-1778673591057.png) </span>

**示例代码**


1. 当主播 A 收到结束主播 PK 成功的通知时，调用 `stopForwardStreamToRooms` 停止将主播 A 的流推送至主播 B 的房间。同样地，主播 B 需要调用 `stopForwardStreamToRooms` 停止将主播 B 的流推送至主播 A 的房间。

   ```objectivec
       // Stop pushing Host A's stream to Host B's room.
       [self.rtcRoom stopForwardStreamToRooms];
   
       // Stop pushing Host B's stream to Host A's room.
       [self.rtcRoom stopForwardStreamToRooms];
   
   ```
   

2. 将视频编码参数恢复至原始分辨率，然后将推流至 CDN 的布局恢复为单人布局。

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
   


<span id="f65b2e7d"></span>
### 结束直播

如需结束直播，请停止推送混流、停止音视频采集、退出房间并销毁引擎。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075235-1544626653002.png) </span>

**示例代码**


1. 停止将混流推送至 CDN。

   ```objectivec
   // Stop pushing the mixed stream to CDN
   [self.rtcEngineKit stopPushMixedStream:taskId
                       withPushTargetType:ByteRTCMixedStreamPushTargetTypeToCDN];
   ```
   

2. 停止音视频采集并移除本地预览。

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
   

3. 退出 RTC 房间和 RTS 业务房间。

   ```objectivec
   // Leave the RTC room
   [self.rtcRoom leaveRoom];
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   ```
   

4. 销毁 RTC 引擎。

   ```objectivec
   // Destroy the RTC engine
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngineKit = nil;
   ```
   


<span id="138c925a"></span>
## 观众端功能实现

<span id="0f8ca667"></span>
### 播放直播流

使用直播播放器从 CDN 拉取并播放直播流。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075247-965399141699.png) </span>

**示例代码**


1. 创建直播播放器并进行配置。

   ```objectivec
   // Create a live player
   BytedPlayerProtocol *player = [[BytedPlayerProtocol alloc] init];
   self.livePlayer = player;
   
   // Configure the player
   [self.livePlayer startWithConfiguration];
   ```
   

2. 设置播放地址、父视图和 SEI 回调。

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
   

3. 开始播放。

   ```objectivec
   // Start playing
   [self.livePlayer play];
   ```
   


<span id="a0212778"></span>
### 成为连麦者

如需成为连麦者，请停止播放 CDN 流、加入 RTC 房间并开启音视频采集。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075258-613011345943.png) </span>

**示例代码**


1. 停止播放 CDN 流。

   ```objectivec
   // Stop playing
   [self.livePlayer stop];
   ```
   

2. 加入 RTC 房间并开启音视频采集。

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
   

3. 收到远端用户的发布流通知后，设置远端视频视图。

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
   


<span id="fa2fa84b"></span>
### 开启美颜 AR（可选）

请参阅[Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，了解如何通过 RTC 引擎实现美颜 AR 的详细操作说明。

<span id="600f249e"></span>
### 结束连麦

如需结束连麦并恢复为普通观众，请退出 RTC 房间、停止音视频采集并恢复 CDN 播放。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075310-1581069071585.png) </span>

**示例代码**


1. 退出 RTC 房间、停止音视频采集，并移除本地和远端视图。恢复 CDN 播放。

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
   


<span id="de712323"></span>
### 退出直播间

如需退出直播间，请停止 CDN 播放、退出 RTS 业务房间并销毁 RTC 引擎。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075327-75511538399.png) </span>

**示例代码**


1. 停止播放直播流，移除播放器的视图，并销毁直播播放器。

   ```objectivec
   // Stop playing
   [self.livePlayer stop];
   [self.livePlayer destroy];
   self.livePlayer = nil;
   ```
   

2. 退出 RTC 房间、停止音视频采集并销毁 RTC 引擎。


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
