---
title: "在 Android 上实现互动直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-interactive-live-for-android-zh-CN"
---

要在 Android 平台构建互动直播应用，可以使用 BytePlus MediaLive 和 RTC SDK。本指南为主播和观众提供实现核心功能的分步说明及代码示例，包括开启直播、启用连麦以及播放直播流等。

<span id="51dca17e"></span>
## 系统要求


* 需使用运行 Android 5.0 或更高版本的实体移动设备。目前不支持在模拟器上运行该应用。

* CPU 架构：armv7a 或 arm64


<span id="91c450b9"></span>
## 前提条件


* 已激活 [BytePlus 账号](http://console.byteplus.com/)、[BytePlus MediaLive](https://console.byteplus.com/live) 和 [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC)。

* 已完成 [直播基础设置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 已获得 BytePlus MediaLive SDK 许可证。

   * 有关获取许可证的详细说明，请参见 [访问您的 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需了解如何选择适合需求的许可证类型，请参考 [SDK 介绍](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。

* 已获得 BytePlus MediaLive SDK 包。要访问互动直播功能，必须使用 SDK 的互动版。更多信息请参见 [访问您的 SDK 包](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-package)。


<span id="7cfc198d"></span>
## 集成 SDK

本节介绍如何将 BytePlus MediaLive 广播和播放器 SDK 集成到您的 Android 项目中。

<span id="57f5de7c"></span>
### 导入 SDK


1. 打开根目录下的 `build.gradle` 文件。

2. 定义 Maven 仓库并配置仓库 URL。

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
   

3. 打开应用模块项目中的 `build.gradle` 文件。

4. 在 `defaultConfig` 中配置 App 使用的 CPU 架构。支持 armv7a 和 arm64 两种架构。

5. 在 `dependencies` 部分添加 SDK 依赖项。

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
   

6. 点击 **Sync Project with Gradle Files** 按钮以同步 SDK。SDK 将自动下载并集成到项目中。如集成失败，请检查与远程仓库的网络连接。


<span id="402ffc70"></span>
### 配置权限


1. 在 `AndroidManifest.xml` 文件中声明应用所需权限：

   ```XML
   <uses-permission android:name="android.permission.CAMERA" />
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   

2. 添加动态请求权限的代码：

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
### 添加许可证

将已获得的许可证文件复制到项目目录。例如，将 `License2_test.lic` 文件复制到 `assets` 目录，如下截图所示。请记录许可证文件的目录路径，初始化 SDK 时将用到。

确保许可证文件关联的包名与项目包名一致。否则，许可证认证将失败。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0c295cb-file_path2.png) </span>

<span id="9a96c144"></span>
### 实现代码混淆


1. 在 `proguard-rules.pro` 文件中添加以下内容，以防止 SDK 相关类被混淆。

   ```XML
   -keep class com.pandora.**{*;}
   -keep class com.ss.**{*;} 
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.bytertc.**{*;} 
   ```
   

2. 由于集成了广播或播放器 SDK 的互动版，还需为 RTC SDK 配置混淆规则。详情请参考 [Android 应用代码混淆](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-78295)。


<span id="afb54d25"></span>
### 初始化 SDK

使用以下代码初始化 SDK：

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


下表描述了初始化所需的参数：


|**参数** |**必填** |**数据类型** |**说明** |**示例** |
|---|---|---|---|---|
|AppID |是 |String |App ID，即您的 SDK 应用的唯一标识。 |`123456` |
|AppName |是 |String |应用名称，即您的 SDK 应用的名称。 |`video_demo` |
|AppVersion |是 |String |您的 Android 应用的版本号。有效的版本号应包含两个或以上分隔符，例如 "1.3.2"。 |`1.3.2` |
|AppChannel |是 |String |应用的下载渠道。您也可以使用此参数区分不同环境（如生产、测试和调试）的应用构建。 |`google_play` |
|LicenseUri |是 |String |license 文件的本地路径。 |`assets:///license2/license2_test.lic` |


<span id="b5013c82"></span>
### 日志上传

默认情况下，SDK 自动启用日志上传功能用于调试和分析。为保护敏感数据，可在初始化 SDK 前调用 `Env.openAppLog(false)` 禁用日志上传。

<span id="79510838"></span>
## 实现主播功能

本节介绍如何为主播实现互动直播功能。

<span id="096f0b78"></span>
### 开启直播

主播使用 RTC 引擎开启直播流。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074454-1681924894309.png) </span>

**示例代码**


1. 创建 RTC 引擎，设置本地预览，并配置视频采集和编码参数。

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
   

2. 使用 RTC 引擎启动音视频采集。

   ```Java
    // Start video capture
    mRTCVideo.startVideoCapture();
   
    // Start audio capture
    mRTCVideo.startAudioCapture();
   ```
   

3. 创建 RTC 房间，设置用户信息并加入房间。请参考 [Token 鉴权](https://docs.byteplus.com/en/byteplus-rtc/docs/70121)，了解如何从应用服务器获取 Token 的详细信息。


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



4. 成功加入房间后，开始将 RTC 混流推送至 CDN。


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
### 开启美颜 AR（可选）

请参考[特效](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，了解如何通过 RTC 引擎实现美颜 AR 的详细操作说明。

<span id="be11235a"></span>
### 开启主播 PK

如需开启主播 PK，两位主播都需要使用 `startForwardStreamToRooms` 接口将各自的音视频流转发到对方的房间。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074558-869796448675.png) </span>

**示例代码**


1. 当主播 A 收到成功开启 PK 的通知后，调用 `startForwardStreamToRooms` 将主播 A 的流推送至主播 B 的房间。同样地，主播 B 需要调用 `startForwardStreamToRooms` 将主播 B 的流推送至主播 A 的房间。

   ```Java
   // Push one's flow to the opposite room
   ForwardStreamInfo forwardStreamInfo = new ForwardStreamInfo(room2ID, coHostRtcToken);
   mRTCRoom1.startForwardStreamToRooms(Collections.singletonList(forwardStreamInfo));
   ```
   

2. 调整 PK 的视频编码参数（分辨率降低一半），然后更新推送至 CDN 的布局。

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
### 结束主播 PK

如需结束主播 PK，请调用 `stopForwardStreamToRooms` 停止在房间之间推流，然后将推送至 CDN 的布局更新回单人布局。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074619-47905823354.png) </span>

**示例代码**


1. 当主播 A 收到成功结束 PK 的通知后，调用 `stopForwardStreamToRooms` 停止将主播 A 的流推送至主播 B 的房间。同样地，主播 B 需要调用 `stopForwardStreamToRooms` 停止将主播 B 的流推送至主播 A 的房间。

   ```Java
   // Stop pushing Host A's stream to Host B's room.
   mRTCRoom1.stopForwardStreamToRooms();
   
   // Stop pushing Host B's stream to Host A's room.
   mRTCRoom2.stopForwardStreamToRooms();
   ```
   

2. 将视频编码参数恢复为原始分辨率，然后将推送至 CDN 的布局更新回单人布局。

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
### 结束直播

如需结束直播，请停止将 RTC 混流推送至 CDN，停止音视频采集，移除本地预览，并销毁 RTC 房间和 RTC 引擎。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074634-1599975887259.png) </span>

**示例代码**


1. 停止将 RTC 混流推送至 CDN。

   ```Java
   // Stop pushing mixed RTC streams to CDN
   String taskId = "";
   mRTCVideo.stopPushMixedStream(taskId, MixedStreamPushTargetType.PUSH_TO_CDN);
   ```
   

2. 停止 RTC 引擎的音视频采集并移除本地预览。

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
   

3. 退出并销毁 RTC 房间，然后销毁 RTC 引擎。

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
## 观众端功能实现

本节提供观众端互动直播功能的实现说明。

<span id="8a21cfe7"></span>
### 播放直播流

使用直播播放器拉取并播放直播流。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074648-1351968520783.png) </span>

**示例代码**


1. 创建直播播放器并进行配置。

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
   

2. 为播放器设置视图，设置拉流地址并开始播放。

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
### 成为连麦者

如需成为连麦者，请停止直播播放器的播放，并使用 RTC 引擎开启连麦。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074702-940645475860.png) </span>

**示例代码**


1. 停止直播流播放并移除直播播放器的视图。

   ```Java
   // Stop playing the live stream
   mLivePlayer.stop();
   
   // Remove the view for the live player
   mLocalVideoContainer.removeView(mPlayerView);
   ```
   

2. 创建 RTC 引擎，设置本地预览和视频编码参数，以及视频采集参数。

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
   

3. 使用 RTC 引擎启动音视频采集。

   ```Java
   // Start video capture
   mRTCVideo.startVideoCapture();
   
   // Start audio capture
   mRTCVideo.startAudioCapture();
   ```
   

4. 创建 RTC 房间，设置用户信息并加入 RTC 房间。请参考 [Token 鉴权](https://docs.byteplus.com/en/byteplus-rtc/docs/70121)，了解如何从应用服务器获取 Token 的详细信息。

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
   

5. 收到其他连麦者发布流状态通知时，添加或移除其视图。

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
### 开启美颜 AR（可选）

请参阅[特效](https://docs.byteplus.com/en/byteplus-rtc/docs/114717)，获取如何通过 RTC 引擎实现美颜 AR 的详细说明。

<span id="0de0f01c"></span>
### 结束连麦

要恢复为普通观众身份，请通过 RTC 引擎停止连麦，并使用直播播放器继续播放直播流。

**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074719-393629603646.png) </span>

**示例代码**


1. 离开 RTC 房间，使用 RTC 引擎停止音视频采集，并移除本地和远端视图。

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
   

2. 为播放器设置视图并开始播放直播流。

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
### 离开直播间

要离开直播间，请执行以下操作：


1. 停止播放直播流并销毁直播播放器。

2. 离开 RTC 房间，停止音视频采集，并销毁 RTC 引擎。


**时序图**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074732-594839745970.png) </span>

**示例代码**


1. 停止播放直播流，移除播放器视图，并销毁直播播放器。

   ```Java
   // Stop playing the live stream
   mLivePlayer.stop();
   
   // Destroy the live player
   mLivePlayer.destroy();
   mLivePlayer = null;
   ```
   

2. 离开 RTC 房间，停止音视频采集，并销毁 RTC 引擎。

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
