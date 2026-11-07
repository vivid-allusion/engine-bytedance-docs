---
title: "在 iOS 上實現互動直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-interactive-live-for-ios-zh-TW"
---

為在您的 iOS 應用中實現完整的互動直播功能，本指南提供了全面的操作說明和程式碼示例。您將學習如何使用 BytePlus MediaLive 和 RTC SDK 構建主播與觀眾的完整工作流程，涵蓋啟動直播、啟用連麥、播放直播影片以及管理會話生命週期等關鍵功能。

<span id="8d09389f"></span>
## 系統要求


* 執行 iOS 11 或更高版本的實體 iPhone 或 iPad

* Xcode 14.1 或更高版本


<span id="ce425396"></span>
## 前置條件


* 已啟用 [BytePlus 賬號](http://console.byteplus.com/)，並開通 [BytePlus MediaLive](https://console.byteplus.com/live) 和 [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC)。

* 您已完成 [直播基礎配置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 您已獲得 BytePlus MediaLive SDK 許可證。

   * 有關獲取許可證的詳細說明，請參見 [訪問您的 SDK 許可證](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需瞭解如何選擇適合您需求的許可證型別，請參考 [SDK 介紹](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。

* 您已獲得 BytePlus MediaLive SDK 包。要訪問互動直播功能，必須使用 SDK 的互動版。更多資訊請參見 [訪問您的 SDK 包](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-package)。


<span id="d7a50fa4"></span>
## 整合 SDK

本節介紹如何將 BytePlus MediaLive 推流和播放器 SDK 整合到您的 iOS 專案中。

<span id="eaa6433a"></span>
### 安裝 SDK


1. 在 Mac 上安裝 Ruby，並在終端執行以下命令以安裝 CocoaPods。

   ```Plain
   sudo gem install cocoapods
   ```
   

2. 在專案目錄中執行以下命令以建立 Podfile。

   ```Plain
   pod init
   ```
   

3. 在 Podfile 中新增以下 SDK 依賴項。

   ```Plain
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   source 'https://github.com/volcengine/volcengine-specs.git'
   pod 'TTSDK', '1.48.200.2-premium', :subspecs => ['LivePull-RTS', 'RTCSDK']
   ```
   

4. 在終端執行以下命令以更新本地庫並安裝 SDK。

   ```Plain
   pod install
   ```
   


<span id="788c713d"></span>
### 許可權申請

錄製音影片時，需申請攝像頭和麥克風許可權。為此，請在 `info.plist` 中包含以下鍵：


* NSCameraUsageDescription

* NSMicrophoneUsageDescription


您可以使用以下程式碼申請攝像頭和麥克風許可權：

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
### 新增許可證檔案

將許可證檔案複製到專案目錄，並記錄許可證檔案路徑。

確保許可證檔案關聯的 bundle ID 與您的專案一致。否則，許可證認證將失敗。

<span id="1ad87597"></span>
### SDK 初始化

使用以下程式碼初始化 SDK：

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


下表詳細說明了初始化所需的各引數：


|**引數** |**必填** |**資料型別** |**說明** |**示例** |
|---|---|---|---|---|
|AppID |是 |字串 |App ID，即 SDK 應用的唯一識別符號。 |`123456` |
|appName |是 |字串 |應用名稱，即 SDK 應用的名稱。 |`video_demo` |
|channel |否 |字串 |用於下載應用的渠道。您也可以使用該引數區分不同環境的應用構建，例如生產、測試和除錯。 |`appstore` |
|bundleID |是 |字串 |iOS 應用的包名（即專案主目標的 `bundleId` 值）。 |`com.byteplus.video.ios` |
|licenseFilePath |是 |字串 |許可證檔案的路徑。 |`live.lic` |


<span id="7bdd8f3b"></span>
### 日誌上傳

預設情況下，SDK 自動上傳日誌以便除錯和分析。為保護敏感資料，您可在 `TTSDKConfiguration` 中將 `shouldInitAppLog` 設定為 `NO`，以手動關閉日誌上傳。

```objectivec
- (void)configTTSDK {
    //....    
    configuration.shouldInitAppLog = NO;
    [TTSDKManager setShouldReportToAppLog:NO];
    //....
}
```


<span id="53373ec6"></span>
## 主播功能實現

本節介紹主播實現互動直播功能的操作說明。

<span id="8ccf9441"></span>
### 啟動直播

主播使用 RTC 引擎進行音視訊擷取，並透過 RTC 混流推送至 CDN 功能來啟動直播。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075156-1271852145783.png) </span>

**示例程式碼**


1. 建立 RTC 引擎並設定引擎參數。

   ```objectivec
   // Create the RTC engine configuration
   ByteRTCEngineConfig *config = [[ByteRTCEngineConfig alloc] init];
   config.appID = @"Your App ID";
   
   // Create the RTC engine instance
   self.rtcEngineKit = [ByteRTCEngine createRTCEngine:config delegate:self];
   ```
   

2. 設定視訊擷取和編碼參數。

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
   

3. 設定本機預覽視圖。

   ```objectivec
   // Set the local preview
   ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
   canvas.view = self.localView;
   canvas.renderMode = ByteRTCRenderModeHidden;
   [self.rtcEngineKit setLocalVideoCanvas:canvas];
   ```
   

4. 加入 RTC 房間並啟動音視訊擷取。

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
   

5. 成功加入房間後，開始將混合 RTC 流推送至 CDN。

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
### 開啟美顏 AR（可選）

請參閱[Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，瞭解如何透過 RTC 引擎實現美顏 AR 的詳細操作說明。

<span id="e4d5322c"></span>
### 開啟主播 PK

如需與其他主播進行主播 PK，您需要開啟跨房間轉推流，並更新混流佈局。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075211-1041707050688.png) </span>

**示例程式碼**


1. 當主播 A 收到開始主播 PK 成功的通知時，呼叫 `startForwardStreamToRooms` 將主播 A 的流推送至主播 B 的房間。同樣地，主播 B 需要呼叫 `startForwardStreamToRooms` 將主播 B 的流推送至主播 A 的房間。

   ```objectivec
       // Push one's flow to the opposite room
       ByteRTCForwardStreamConfiguration *forwardConfig = [[ByteRTCForwardStreamConfiguration alloc] init];
       forwardConfig.roomId = targetRoomId;
       forwardConfig.token = token;
       [self.rtcRoom startForwardStreamToRooms:@[forwardConfig]];
   
   ```
   

2. 調整用於 PK 的視訊編碼參數（降低至一半解析度），然後更新推送至 CDN 的佈局。

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
### 結束主播 PK

如需結束主播 PK，請停止跨房間轉推流，並將混流佈局恢復為單主播佈局。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075224-1778673591057.png) </span>

**示例程式碼**


1. 當主播 A 收到結束主播 PK 成功的通知時，呼叫 `stopForwardStreamToRooms` 停止將主播 A 的流推送至主播 B 的房間。同樣地，主播 B 需要呼叫 `stopForwardStreamToRooms` 停止將主播 B 的流推送至主播 A 的房間。

   ```objectivec
       // Stop pushing Host A's stream to Host B's room.
       [self.rtcRoom stopForwardStreamToRooms];
   
       // Stop pushing Host B's stream to Host A's room.
       [self.rtcRoom stopForwardStreamToRooms];
   
   ```
   

2. 將視訊編碼參數恢復至原始解析度，然後將推送至 CDN 的佈局恢復為單人佈局。

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
### 結束直播

如需結束直播，請停止推送混流、停止音視訊擷取、退出房間並銷毀引擎。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075235-1544626653002.png) </span>

**示例程式碼**


1. 停止將混流推送至 CDN。

   ```objectivec
   // Stop pushing the mixed stream to CDN
   [self.rtcEngineKit stopPushMixedStream:taskId
                       withPushTargetType:ByteRTCMixedStreamPushTargetTypeToCDN];
   ```
   

2. 停止音視訊擷取並移除本機預覽。

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
   

3. 退出 RTC 房間和 RTS 業務房間。

   ```objectivec
   // Leave the RTC room
   [self.rtcRoom leaveRoom];
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   ```
   

4. 銷毀 RTC 引擎。

   ```objectivec
   // Destroy the RTC engine
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngineKit = nil;
   ```
   


<span id="138c925a"></span>
## 觀眾端功能實現

<span id="0f8ca667"></span>
### 播放直播流

使用直播播放器從 CDN 拉取並播放直播流。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075247-965399141699.png) </span>

**示例程式碼**


1. 建立直播播放器並進行設定。

   ```objectivec
   // Create a live player
   BytedPlayerProtocol *player = [[BytedPlayerProtocol alloc] init];
   self.livePlayer = player;
   
   // Configure the player
   [self.livePlayer startWithConfiguration];
   ```
   

2. 設定播放地址、父視圖和 SEI 回呼。

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
   

3. 開始播放。

   ```objectivec
   // Start playing
   [self.livePlayer play];
   ```
   


<span id="a0212778"></span>
### 成為連麥者

如需成為連麥者，請停止播放 CDN 流、加入 RTC 房間並開啟音視訊擷取。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075258-613011345943.png) </span>

**示例程式碼**


1. 停止播放 CDN 流。

   ```objectivec
   // Stop playing
   [self.livePlayer stop];
   ```
   

2. 加入 RTC 房間並開啟音視訊擷取。

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
   

3. 收到遠端使用者的發布流通知後，設定遠端視訊視圖。

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
### 開啟美顏 AR（可選）

請參閱[Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，瞭解如何透過 RTC 引擎實現美顏 AR 的詳細操作說明。

<span id="600f249e"></span>
### 結束連麥

如需結束連麥並恢復為普通觀眾，請退出 RTC 房間、停止音視訊擷取並恢復 CDN 播放。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075310-1581069071585.png) </span>

**示例程式碼**


1. 退出 RTC 房間、停止音視訊擷取，並移除本機和遠端視圖。恢復 CDN 播放。

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
### 退出直播間

如需退出直播間，請停止 CDN 播放、退出 RTS 業務房間並銷毀 RTC 引擎。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707075327-75511538399.png) </span>

**示例程式碼**


1. 停止播放直播流，移除播放器的視圖，並銷毀直播播放器。

   ```objectivec
   // Stop playing
   [self.livePlayer stop];
   [self.livePlayer destroy];
   self.livePlayer = nil;
   ```
   

2. 退出 RTC 房間、停止音視訊擷取並銷毀 RTC 引擎。


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
