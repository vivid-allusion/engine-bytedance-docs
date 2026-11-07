---
title: "在 Android 上實現互動直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-interactive-live-for-android-zh-TW"
---

要在 Android 平臺構建互動直播應用，可以使用 BytePlus MediaLive 和 RTC SDK。本指南為主播和觀眾提供實現核心功能的分步說明及程式碼示例，包括開啟直播、啟用連麥以及播放直播流等。

<span id="51dca17e"></span>
## 系統要求


* 需使用執行 Android 5.0 或更高版本的實體移動裝置。目前不支援在模擬器上執行該應用。

* CPU 架構：armv7a 或 arm64


<span id="91c450b9"></span>
## 前提條件


* 已啟用 [BytePlus 賬號](http://console.byteplus.com/)、[BytePlus MediaLive](https://console.byteplus.com/live) 和 [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC)。

* 已完成 [直播基礎設定](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 已獲得 BytePlus MediaLive SDK 許可證。

   * 有關獲取許可證的詳細說明，請參見 [訪問您的 SDK 許可證](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需瞭解如何選擇適合需求的許可證型別，請參考 [SDK 介紹](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。

* 已獲得 BytePlus MediaLive SDK 包。要訪問互動直播功能，必須使用 SDK 的互動版。更多資訊請參見 [訪問您的 SDK 包](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-package)。


<span id="7cfc198d"></span>
## 整合 SDK

本節介紹如何將 BytePlus MediaLive 廣播和播放器 SDK 整合到您的 Android 專案中。

<span id="57f5de7c"></span>
### 匯入 SDK


1. 開啟根目錄下的 `build.gradle` 檔案。

2. 定義 Maven 倉庫並配置倉庫 URL。

   ```Groovy
   allprojects {
       repositories {
           google()
           mavenCentral()
           maven {
               url 'https://artifact.bytedance.com/repository/Volcengine/'
           }
           maven {
               url 'https://artifact.byteplus.com/repository/public/'
           }
       }
   }
   
   apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
   ```
   

3. 開啟應用模組專案中的 `build.gradle` 檔案。

4. 在 `defaultConfig` 中配置 App 使用的 CPU 架構。支援 armv7a 和 arm64 兩種架構。

5. 在 `dependencies` 部分新增 SDK 依賴項。

   ```Groovy
   android {
      defaultConfig {
          ndk {
   // Set the native library architectures to support armv7a or arm64.
              abiFilters 'armeabi-v7a', 'arm64-v8a'
           }
      }
   }
   
   dependencies {
       ......
       // Add the online integration address of the SDK.
      ttsdkVersion = '1.48.200.2'
      implementation "com.bytedanceapi:ttsdk-ttlivepull_rtc:$ttsdkVersion"
      implementation "com.bytedanceapi:ttsdk-ttcommon:$ttsdkVersion"
      implementation "com.bytedanceapi:ttsdk-ttlicense2:$ttsdkVersion"
       // Add third-party dependencies.
      implementation 'commons-net:commons-net:3.9.0'
      // Enable HTTPDNS resolution.
       implementation 'com.squareup.okhttp3:okhttp:4.12.0'
   }
   ```
   

6. 點選 **Sync Project with Gradle Files** 按鈕以同步 SDK。SDK 將自動下載並整合到專案中。如整合失敗，請檢查與遠端倉庫的網路連線。


<span id="402ffc70"></span>
### 配置許可權


1. 在 `AndroidManifest.xml` 檔案中宣告應用所需許可權：

   ```XML
   <uses-permission android:name="android.permission.CAMERA" />
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   

2. 新增動態請求許可權的程式碼：

   ```XML
   private boolean checkPermission(int request) {
           String permissions[] = new String[]{
                   Manifest.permission.CAMERA,
                   Manifest.permission.RECORD_AUDIO,
                   Manifest.permission.MODIFY_AUDIO_SETTINGS,
                   Manifest.permission.ACCESS_NETWORK_STATE
           };
           List<String> permissionList = new ArrayList<>();
           for (String permission : permissions) {
               boolean granted = ContextCompat.checkSelfPermission(this, permission) == PackageManager.PERMISSION_GRANTED;
               if (granted) continue;
               permissionList.add(permission);
           }
           if (permissionList.isEmpty()) return true;
   
           String permissionsToGrant[] = new String[permissionList.size()];
           permissionList.toArray(permissionsToGrant);
           ActivityCompat.requestPermissions(this, permissionsToGrant, request);
           return false;
   }
   ```
   


<span id="5a2ea2e5"></span>
### 新增許可證

將已獲得的許可證檔案複製到專案目錄。例如，將 `License2_test.lic` 檔案複製到 `assets` 目錄，如下截圖所示。請記錄許可證檔案的目錄路徑，初始化 SDK 時將用到。

確保許可證檔案關聯的包名與專案包名一致。否則，許可證認證將失敗。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0c295cb-file_path2.png) </span>

<span id="9a96c144"></span>
### 實現程式碼混淆


1. 在 `proguard-rules.pro` 檔案中新增以下內容，以防止 SDK 相關類被混淆。

   ```XML
   -keep class com.pandora.**{*;}
   -keep class com.ss.**{*;} 
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.bytertc.**{*;} 
   ```
   

2. 由於整合了廣播或播放器 SDK 的互動版，還需為 RTC SDK 配置混淆規則。詳情請參考 [Android 應用程式碼混淆](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-78295)。


<span id="afb54d25"></span>
### 初始化 SDK

使用以下程式碼初始化 SDK：

```Java
// Initialize the environment.
Env.start(new Config.Builder()
        .setApplicationContext(sApplicationContext)
        .setAppID("Your App ID")
        .setAppName("Your application name")
        .setAppVersion(BuildConfig.VERSION_NAME) // A valid version number should contain two or more separators, such as "1.3.2".
        .setAppChannel("Your app channel")
        .setLicenseUri("Your license URI")
        .setLicenseCallback(mLicenseCallback) // Set the license callbacks.
        .build());

// Enable logcat. It is recommended to enable logcat during development and disable logcat when compiling the release APK.
LicenseManager.turnOnLogcat(true);

// License callbacks.
LicenseManager.Callback mLicenseCallback = new LicenseManager.Callback() {
        @Override
        public void onLicenseLoadSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
            licenseID = licenseId; // License ID, through which you can get the license information.
        }

        @Override
        public void onLicenseLoadError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseLoadRetry(@NonNull String licenseUri) {
           
        }

        @Override
        public void onLicenseUpdateSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
          licenseID = licenseId;
        }

        @Override
        public void onLicenseUpdateError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseUpdateRetry(@NonNull String licenseUri) {
          
        }
    };
    
// Get the license information.
License license = LicenseManager.getInstance().getLicense(licenseID); // You can get the license ID through mLicenseCallback.
if (license != null) {
    StringBuilder builder = new StringBuilder();
    builder.append("License id:" + license.getId()).append("\n")
           .append("License package:" + license.getPackageName()).append("\n")
           .append("License test:" + license.getType()).append("\n")
           .append("License version:" + license.getVersion()).append("\n");

    if (license.getModules() != null) {
        String names = "";
        for (License.Module module : license.getModules()) {
            names = "module name:" + module.getName() + ", start time:" +
            TimeUtil.format(module.getStartTime(), Times.YYYY_MM_DD_KK_MM_SS)
                    + ", expire time:" + TimeUtil.format(module.getExpireTime(), Times.YYYY_MM_DD_KK_MM_SS) + "\n";
            builder.append("License modules:" + names);
        }
    }
 }
```


下表描述了初始化所需的引數：


|**引數** |**必填** |**資料型別** |**說明** |**示例** |
|---|---|---|---|---|
|AppID |是 |String |App ID，即您的 SDK 應用的唯一標識。 |`123456` |
|AppName |是 |String |應用名稱，即您的 SDK 應用的名稱。 |`video_demo` |
|AppVersion |是 |String |您的 Android 應用的版本號。有效的版本號應包含兩個或以上分隔符，例如 "1.3.2"。 |`1.3.2` |
|AppChannel |是 |String |應用的下載渠道。您也可以使用此引數區分不同環境（如生產、測試和除錯）的應用構建。 |`google_play` |
|LicenseUri |是 |String |license 檔案的本地路徑。 |`assets:///license2/license2_test.lic` |


<span id="b5013c82"></span>
### 日誌上傳

預設情況下，SDK 自動啟用日誌上傳功能用於除錯和分析。為保護敏感資料，可在初始化 SDK 前呼叫 `Env.openAppLog(false)` 禁用日誌上傳。

<span id="79510838"></span>
## 實現主播功能

本節介紹如何為主播實現互動直播功能。

<span id="096f0b78"></span>
### 開啟直播

主播使用 RTC 引擎開啟直播流。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074454-1681924894309.png) </span>

**示例程式碼**


1. 建立 RTC 引擎，設定本地預覽，並配置影片採集和編碼引數。

   ```Java
    // Create the EngineConfig object
    EngineConfig engineConfig = new EngineConfig();
    engineConfig.context = Env.getApplicationContext();
    engineConfig.appID = appId;
   
    // Create the RTC engine
    mRTCVideo = RTCEngine.createRTCEngine(engineConfig, mRTCVideoEventHandler);
   
    // Set the video capture parameters
    VideoCaptureConfig captureConfig = new VideoCaptureConfig( 
            mConfig.mVideoCaptureWidth, 
            mConfig.mVideoCaptureHeight, 
            mConfig.mVideoCaptureFps);
    mRTCVideo.setVideoCaptureConfig(captureConfig);
    
    // Set the video encoding parameters
    VideoEncoderConfig config = new VideoEncoderConfig(
            mConfig.mVideoEncoderWidth, 
            mConfig.mVideoEncoderHeight, 
            mConfig.mVideoEncoderFps, 
            mConfig.mVideoEncoderKBitrate * 1000);
    mRTCVideo.setVideoEncoderConfig(config);  
   
    // Set the local preview
    VideoCanvas videoCanvas = new VideoCanvas();
    videoCanvas.renderView = renderView;
    videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
    mRTCVideo.setLocalVideoCanvas(videoCanvas);
   ```
   

2. 使用 RTC 引擎啟動音影片採集。

   ```Java
    // Start video capture
    mRTCVideo.startVideoCapture();
   
    // Start audio capture
    mRTCVideo.startAudioCapture();
   ```
   

3. 建立 RTC 房間，設定使用者資訊並加入房間。請參考 [Token 鑑權](https://docs.byteplus.com/en/byteplus-rtc/docs/70121)，瞭解如何從應用服務器獲取 Token 的詳細資訊。


```Java
    // Create an RTC room
    mRTCRoom = mRTCVideo.createRTCRoom(roomId);
    mRTCRoom.setRTCRoomEventHandler(mIRtcRoomEventHandler);
    
    // Set the user information
    mUserId = userId;
    mRoomId = roomId;
    UserInfo userInfo = new UserInfo(userId, null);
    RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_INTERACTIVE_PODCAST,
            true, //isPublishAudio       
            true, //isPublishVideo       
            true, //isSubscribeAudio       
            true); //isSubscribeVideo       
            
    // Join the room. Get the token from the app server.
    mRTCRoom.joinRoom(token, userInfo, true, roomConfig);
```



4. 成功加入房間後，開始將 RTC 混流推送至 CDN。


```Java
    // Notification of a successful join room
    private RtcRoomEventHandlerAdapter mIRtcRoomEventHandler = new RtcRoomEventHandlerAdapter() {
        @Override
        public void onRoomStateChanged(String roomId, String uid, int state, String extraInfo) {
            // Not first time entering or reconnecting to the room
            if (state != 0 || !extraInfo.contains("\"join_type\":0")) {
                return;
            }
            // Create a stream mixing configuration instance
            final MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
            streamConfig.roomID = roomId;
            streamConfig.userID = uid;
            
            // Set the video encoding parameters for the mixed stream. The settings must be consistent with the encoding settings for stream pushing.
            if (streamConfig.videoConfig != null) {
                streamConfig.videoConfig.width = myConfig.width;
                streamConfig.videoConfig.height = myConfig.height;
                streamConfig.videoConfig.fps = myConfig.frameRate;
                streamConfig.videoConfig.bitrate = myConfig.bitRate;
            }
            
            // Set the audio encoding parameters for the mixed stream. The settings must be consistent with the encoding settings for stream pushing.
            if (streamConfig.audioConfig != null) {
                streamConfig.audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
                streamConfig.audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
                streamConfig.audioConfig.bitrate = 128;
                streamConfig.audioConfig.channels = 2;
                streamConfig.audioConfig.sampleRate = 48000;
            }
            
            // Set the layout information for the host
            final MixedStreamLayoutRegionConfig region = new MixedStreamLayoutRegionConfig();
            region.userID = uid;
            region.roomID = roomId;
            region.isLocalUser = true;
            region.locationX = 0;
            region.locationY = 0;
            region.width = myConfig.width;
            region.height = myConfig.height;
            region.alpha = 1;
            region.zOrder = 0;
            region.mediaType = MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO;
            region.renderMode = MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN;
    
            streamConfig.regions = new MixedStreamLayoutRegionConfig[]{region};

            // Set the ID for the push to CDN task
            String taskId = "";

            MixedStreamPushTargetConfig target = new MixedStreamPushTargetConfig();
            target.pushTargetType = MixedStreamPushTargetType.PUSH_TO_CDN;
            target.pushCDNURL = mPushCDNUrl;
        
            // Start pushing the mixed RTC stream to CDN
            mRTCVideo.startPushMixedStream(taskId, target, streamConfig); 
        }
    }
```


<span id="71c1b4f6"></span>
### 開啟美顏 AR（可選）

請參考[特效](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，瞭解如何透過 RTC 引擎實現美顏 AR 的詳細操作說明。

<span id="be11235a"></span>
### 開啟主播 PK

如需開啟主播 PK，兩位主播都需要使用 `startForwardStreamToRooms` 介面將各自的音影片流轉發到對方的房間。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074558-869796448675.png) </span>

**示例程式碼**


1. 當主播 A 收到成功開啟 PK 的通知後，調用 `startForwardStreamToRooms` 將主播 A 的流推送至主播 B 的房間。同樣地，主播 B 需要調用 `startForwardStreamToRooms` 將主播 B 的流推送至主播 A 的房間。

   ```Java
   // Push one's flow to the opposite room
   ForwardStreamInfo forwardStreamInfo = new ForwardStreamInfo(room2ID, coHostRtcToken);
   mRTCRoom1.startForwardStreamToRooms(Collections.singletonList(forwardStreamInfo));
   ```
   

2. 調整 PK 的影片編碼引數（解析度降低一半），然後更新推送至 CDN 的佈局。

   ```Java
   // For Host A
   private RtcRoomEventHandlerAdapter mIRtcRoomEventHandler = new RtcRoomEventHandlerAdapter() {
       @Override
       public void onUserJoined(String uid, int elapsed) {
        
           // Set the stream push configuration, including the URL for the mixed stream to be pushed to
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = MixedStreamPushTargetType.PUSH_TO_CDN;
           
           // Set video encoding parameters for transcoding
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = myConfig.frameRate;
           videoconfig.height = myConfig.height;
           videoconfig.width = myConfig.width;
           videoconfig.bitrate = myConfig.bitRate;
           
           // Set audio encoding parameters for transcoding
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // Update the push-to-CDN layout from a 1-person layout to a 2-person layout
           final MixedStreamLayoutRegionConfig localRegion = new MixedStreamLayoutRegionConfig();
           localRegion.userID = userId;
           localRegion.roomID = roomId;
           localRegion.isLocalUser = true;
           localRegion.locationX = 0;
           localRegion.locationY = 0;
           localRegion.width = (int) (myConfig.width * 0.5);
           localRegion.height = (int) (myConfig.height * 0.5);
           localRegion.alpha = 1;
           localRegion.zOrder = 0;
           localRegion.mediaType = MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO;
           localRegion.renderMode = MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN;
          
           final MixedStreamLayoutRegionConfig remoteRegion = new MixedStreamLayoutRegionConfig();
           remoteRegion.userID = coHostUserId;
           remoteRegion.roomID = roomId;
           remoteRegion.isLocalUser = false;
           remoteRegion.locationX = (int) (myConfig.width * 0.5);
           remoteRegion.locationY = 0;
           remoteRegion.width = (int) (myConfig.width * 0.5);
           remoteRegion.height = (int) (myConfig.height * 0.5);
           remoteRegion.alpha = 1;
           remoteRegion.zOrder = 0;
           remoteRegion.mediaType = MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO;
           remoteRegion.renderMode = MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN;
   
           streamConfig.regions = new MixedStreamLayoutRegionConfig[]{localRegion, remoteRegion};
           // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream
           String taskId = "";
           
           // Update the stream push parameters
           mRTCVideo.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       
       @Override
       public void onUserPublishStreamVideo (String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // Add the remote user view
               TextureView renderView = new TextureView(Env.getApplicationContext());
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = renderView;
               canvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
               mRTCVideo.setRemoteVideoCanvas(streamId, canvas);
           }
       }
   };
   ```
   


<span id="8ae39c06"></span>
### 結束主播 PK

如需結束主播 PK，請調用 `stopForwardStreamToRooms` 停止在房間之間推流，然後將推送至 CDN 的佈局更新回單人佈局。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074619-47905823354.png) </span>

**示例程式碼**


1. 當主播 A 收到成功結束 PK 的通知後，調用 `stopForwardStreamToRooms` 停止將主播 A 的流推送至主播 B 的房間。同樣地，主播 B 需要調用 `stopForwardStreamToRooms` 停止將主播 B 的流推送至主播 A 的房間。

   ```Java
   // Stop pushing Host A's stream to Host B's room.
   mRTCRoom1.stopForwardStreamToRooms();
   
   // Stop pushing Host B's stream to Host A's room.
   mRTCRoom2.stopForwardStreamToRooms();
   ```
   

2. 將影片編碼引數恢復為原始解析度，然後將推送至 CDN 的佈局更新回單人佈局。

   ```Java
   // For Host A
   private RtcRoomEventHandlerAdapter mIRtcRoomEventHandler = new RtcRoomEventHandlerAdapter() {
       @Override
       public void onUserLeave(String uid, int reason) {
           
           // Set the stream push configuration
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = MixedStreamPushTargetType.PUSH_TO_CDN;
           
           // Set video encoding parameters for transcoding
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = myConfig.frameRate;
           videoconfig.height = myConfig.height;
           videoconfig.width = myConfig.width;
           videoconfig.bitrate = myConfig.bitRate;
           
           // Set audio encoding parameters for transcoding
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // Update the push-to-CDN layout from a 2-person layout to a 1-person layout
           MixedStreamLayoutRegionConfig[] regions = new MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamLayoutRegionConfig();
           region.userID = mUserId;// Host A's user ID
           region.roomID = mRoomId;
           region.isLocalUser = true;
           region.locationX = 0;
           region.locationY = 0;
           region.width = myConfig.width;
           region.height = myConfig.height;
           region.alpha = 1;
           region.zOrder = 0;
           region.mediaType = MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO;
           region.renderMode = MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN;
           regions[0] = region;
           
           // Pass the configured audio and video parameters into the final structure
           MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
           streamConfig.audioConfig = audioConfig;
           streamConfig.videoConfig = videoconfig;
           streamConfig.roomID = mRoomId;
           streamConfig.userID = mUserId;
           streamConfig.regions = regions;
           
           // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream
           String taskId = "";
           
           // Update the stream push parameters
           mRTCVideo.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       
       @Override
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               // Remove the remote user view
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = null;
               canvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
               mRTCVideo.setRemoteVideoCanvas(streamId, canvas);
           }
       }
   };
   ```
   


<span id="dd89bf38"></span>
### 結束直播

如需結束直播，請停止將 RTC 混流推送至 CDN，停止音影片採集，移除本地預覽，並銷燬 RTC 房間和 RTC 引擎。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074634-1599975887259.png) </span>

**示例程式碼**


1. 停止將 RTC 混流推送至 CDN。

   ```Java
   // Stop pushing mixed RTC streams to CDN
   String taskId = "";
   mRTCVideo.stopPushMixedStream(taskId, MixedStreamPushTargetType.PUSH_TO_CDN);
   ```
   

2. 停止 RTC 引擎的音影片採集並移除本地預覽。

   ```Java
   // Stop video capture
   mRTCVideo.stopVideoCapture();
   
   // Stop audio capture
   mRTCVideo.stopAudioCapture();
   
   // Remove the local preview
   VideoCanvas videoCanvas = new VideoCanvas();
   videoCanvas.renderView = null;
   videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   mRTCVideo.setLocalVideoCanvas(videoCanvas);
   ```
   

3. 退出並銷燬 RTC 房間，然後銷燬 RTC 引擎。

   ```Java
   // Leave and destroy the RTC room
   mRTCRoom.leaveRoom();
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine
   RTCEngine.destroyRTCEngine();
   mRTCVideo = null;
   ```
   


<span id="88d76076"></span>
## 觀眾端功能實現

本節提供觀眾端互動直播功能的實現說明。

<span id="8a21cfe7"></span>
### 播放直播流

使用直播播放器拉取並播放直播流。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074648-1351968520783.png) </span>

**示例程式碼**


1. 建立直播播放器並進行配置。

   ```Java
   // Create a live player
   VeLivePlayer mLivePlayer = new VideoLiveManager(context);
   
   // Configure the player
   VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
   config.enableSei = true;
   config.statisticsCallbackInterval = 5;
   config.enableStatisticsCallback = true;
   mLivePlayer.setConfig(config);
   ```
   

2. 為播放器設定檢視，設定拉流地址並開始播放。

   ```Java
    // Create TextureView and set Surface for the player
    TextureView textureView = new TextureView(context);
    textureView.setSurfaceTextureListener(new TextureView.SurfaceTextureListener() {
        @Override
        public void onSurfaceTextureAvailable(SurfaceTexture surface, int width, int height) {
            Surface playerSurface = new Surface(surface);
            mLivePlayer.setSurface(playerSurface);
            
            // Set the pull stream address
            VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
            flvStream.url = mPullUrl;
            
            VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
            streamData.mainStreamList = Collections.singletonList(flvStream);
            mLivePlayer.setPlayStreamData(streamData);
            
            // Start playing
            mLivePlayer.play();
        }
        // ... other callback methods
    });
    
    // Attach TextureView to container
    container.addView(textureView);
   ```
   


<span id="577e7ebe"></span>
### 成為連麥者

如需成為連麥者，請停止直播播放器的播放，並使用 RTC 引擎開啟連麥。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074702-940645475860.png) </span>

**示例程式碼**


1. 停止直播流播放並移除直播播放器的檢視。

   ```Java
   // Stop playing the live stream
   mLivePlayer.stop();
   
   // Remove the view for the live player
   mLocalVideoContainer.removeView(mPlayerView);
   ```
   

2. 建立 RTC 引擎，設定本地預覽和影片編碼引數，以及影片採集引數。

   ```Java
   // Create the EngineConfig object
   EngineConfig engineConfig = new EngineConfig();
   engineConfig.context = Env.getApplicationContext();
   engineConfig.appID = appId;
   
   // Create the RTC engine
   mRTCVideo = RTCEngine.createRTCEngine(engineConfig, mRTCVideoEventHandler);
   
   // Set the video capture parameters
    VideoCaptureConfig captureConfig = new VideoCaptureConfig( 
            mConfig.mVideoCaptureWidth, 
            mConfig.mVideoCaptureHeight, 
            mConfig.mVideoCaptureFps);
    mRTCVideo.setVideoCaptureConfig(captureConfig);
    
    // Set the video encoding parameters
    VideoEncoderConfig config = new VideoEncoderConfig(
            mConfig.mVideoEncoderWidth, 
            mConfig.mVideoEncoderHeight, 
            mConfig.mVideoEncoderFps, 
            mConfig.mVideoEncoderKBitrate * 1000);
    mRTCVideo.setVideoEncoderConfig(config);  
   
   // Set the local preview
   VideoCanvas videoCanvas = new VideoCanvas();
   videoCanvas.renderView = renderView;
   videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   mRTCVideo.setLocalVideoCanvas(videoCanvas);
   
   ```
   

3. 使用 RTC 引擎啟動音影片採集。

   ```Java
   // Start video capture
   mRTCVideo.startVideoCapture();
   
   // Start audio capture
   mRTCVideo.startAudioCapture();
   ```
   

4. 建立 RTC 房間，設定使用者資訊並加入 RTC 房間。請參考 [Token 鑑權](https://docs.byteplus.com/en/byteplus-rtc/docs/70121)，瞭解如何從應用服務器獲取 Token 的詳細資訊。

   ```Java
   // Create an RTC room
   mRTCRoom = mRTCVideo.createRTCRoom(roomId);
   mRTCRoom.setRTCRoomEventHandler(mIRtcRoomEventHandler);
   
    // Set the user information
   UserInfo userInfo = new UserInfo(userId, null);
   RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_INTERACTIVE_PODCAST,
           true,//isPublishAudio
           true,//isPublishVideo    
           true,//isSubscribeAudio
           true);//isSubscribeVideo
       
   // Join the room. Get the token from the app server.
   mRTCRoom.joinRoom(token, userInfo, true/**userVisibility*/, roomConfig);
   ```
   

5. 收到其他連麥者釋出流狀態通知時，新增或移除其檢視。

   ```Java
   private RtcRoomEventHandlerAdapter mIRtcRoomEventHandler = new RtcRoomEventHandlerAdapter() {
       @Override
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // Cache the streamId for the userId
               mUserStreamIdMap.put(streamInfo.userId, streamInfo.streamId);
               
               // Add the view to render the co-host's video
               TextureView renderView = new TextureView(Env.getApplicationContext());
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = view;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               mRTCVideo.setRemoteVideoCanvas(streamId, canvas);
           } else {
               // Remove the view for the co-host
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = null;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               mRTCVideo.setRemoteVideoCanvas(streamId, canvas);
           }        
       }
   };
   ```
   


<span id="190918b2"></span>
### 開啟美顏 AR（可選）

請參閱[特效](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，獲取如何透過 RTC 引擎實現美顏 AR 的詳細說明。

<span id="0de0f01c"></span>
### 結束連麥

要恢復為普通觀眾身份，請透過 RTC 引擎停止連麥，並使用直播播放器繼續播放直播流。

**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074719-393629603646.png) </span>

**示例程式碼**


1. 離開 RTC 房間，使用 RTC 引擎停止音影片採集，並移除本地和遠端檢視。

   ```Java
   // Leave the RTC room
   mRTCRoom.leaveRoom();
   
   // Stop video capture
   mRTCVideo.stopVideoCapture();
   
   // Stop audio capture
   mRTCVideo.stopAudioCapture();
   
   // Remove the local preview
   VideoCanvas localCanvas = new VideoCanvas();
   localCanvas.renderView = null;
   localCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   mRTCVideo.setLocalVideoCanvas(localCanvas);
   
   // Remove the remote views
   VideoCanvasCanvas remoteCanvas = new VideoCanvas();
   remoteCanvas.renderView = null;
   remoteCanvas.renderMode = RENDER_MODE_HIDDEN;
   mRTCVideo.setRemoteVideoCanvas(streamId, remoteCanvas);
   ```
   

2. 為播放器設定檢視並開始播放直播流。

   ```Java
    // Create TextureView and set Surface for the player
    TextureView textureView = new TextureView(context);
    textureView.setSurfaceTextureListener(new TextureView.SurfaceTextureListener() {
        @Override
        public void onSurfaceTextureAvailable(SurfaceTexture surface, int width, int height) {
            Surface playerSurface = new Surface(surface);
            mLivePlayer.setSurface(playerSurface);
            
            // Set the pull stream address
            VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
            flvStream.url = mPullUrl;
            
            VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
            streamData.mainStreamList = Collections.singletonList(flvStream);
            mLivePlayer.setPlayStreamData(streamData);
            
            // Start playing
            mLivePlayer.play();
        }
        // ... other callback methods
    });
    
    // Attach TextureView to container
    container.addView(textureView);
   ```
   


<span id="6fe2868e"></span>
### 離開直播間

要離開直播間，請執行以下操作：


1. 停止播放直播流並銷燬直播播放器。

2. 離開 RTC 房間，停止音影片採集，並銷燬 RTC 引擎。


**時序圖**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074732-594839745970.png) </span>

**示例程式碼**


1. 停止播放直播流，移除播放器檢視，並銷燬直播播放器。

   ```Java
   // Stop playing the live stream
   mLivePlayer.stop();
   
   // Destroy the live player
   mLivePlayer.destroy();
   mLivePlayer = null;
   ```
   

2. 離開 RTC 房間，停止音影片採集，並銷燬 RTC 引擎。

   ```Java
   // Destroy the RTC room
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Stop all audio and video capture
   mRTCVideo.stopVideoCapture();
   mRTCVideo.stopAudioCapture();
   
   // Destroy the RTC engine
   RTCEngine.destroyRTCEngine();
   mRTCVideo = null;
   ```
