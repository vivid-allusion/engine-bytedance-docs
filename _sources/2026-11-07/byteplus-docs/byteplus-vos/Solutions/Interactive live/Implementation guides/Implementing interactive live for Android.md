---
title: "Implementing interactive live for Android"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-interactive-live-for-android"
---

To build an interactive live streaming app on Android, you can use the BytePlus MediaLive and RTC SDKs. This guide provides step\-by\-step instructions and code examples for implementing core features for both hosts and audiences, such as starting a stream, enabling co\-hosting, and playing a live stream.

<span id="system-requirements"></span>
## System requirements


* A physical mobile device running Android 5.0 or above. Running the app on emulators is not currently supported.

* CPU architecture: armv7a or arm64


<span id="prerequisites"></span>
## Prerequisites


* A valid [BytePlus account](http://console.byteplus.com/) with [BytePlus MediaLive](https://console.byteplus.com/live) and [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC) activated.

* You have completed the [basic setup for live streaming](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started).

* You have obtained a BytePlus MediaLive SDK license.

   * For detailed instructions on how to acquire the license, see [Accessing your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license).

   * To learn more about choosing the right license type for your needs, please refer to [SDK introduction](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction).

* You have obtained the BytePlus MediaLive SDK package. To access the interactive live feature, you must use the Interactive edition of the SDK. See [Accessing your SDK package](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-package) for more information.


<span id="integrating-the-sdks"></span>
## Integrating the SDKs

This section introduces how to integrate BytePlus MediaLive Broadcast and Player SDKs into your Android project.

<span id="importing-the-sdks"></span>
### Importing the SDKs


1. Open the `build.gradle` file in the root directory.

2. Define the Maven repositories and configure the repository URLs.

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
   

3. Open the `build.gradle` file in the app module project.

4. Configure the CPU architecture used by the App in `defaultConfig`. Both armv7a and arm64 are supported.

5. Add the SDK dependencies in the `dependencies` section.

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
   

6. Click the **Sync Project with Gradle Files** button to synchronize the SDK. The SDK will be automatically downloaded and integrated into the project. If the integration fails, check your network connection to the remote repository.


<span id="configuring-permissions"></span>
### Configuring permissions


1. Declare the permissions required by the app in the `AndroidManifest.xml` file:

   ```XML
   <uses-permission android:name="android.permission.CAMERA" />
   <uses-permission android:name="android.permission.RECORD_AUDIO" />
   <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   

2. Add code for dynamically requesting permissions:

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
   


<span id="adding-a-license"></span>
### Adding a license

Copy the license file you have obtained to your project directory. For example, copy the `License2_test.lic` file to the `assets` directory, as shown in the following screenshot. Take note of the directory path to the license file as you will use it when initializing the SDK.

Make sure the package name associated with the license file is the same as that of your project. Otherwise, the license authentication will fail.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0c295cb-file_path2.png) </span>

<span id="implementing-code-obfuscation"></span>
### Implementing code obfuscation


1. Add the following lines to the `proguard-rules.pro` file to prevent SDK\-related classes from being obfuscated.

   ```XML
   -keep class com.pandora.**{*;}
   -keep class com.ss.**{*;} 
   -keep class com.bytedance.**{*;}
   -keep class com.pandora.ttlicense2.**{*;}
   -keep class com.bytertc.**{*;} 
   ```
   

2. As you are integrating the Interactive edition of the Broadcast or Player SDK, you also need to configure obfuscation rules for the RTC SDK. Please refer to [Obfuscating your code for Android Apps](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-78295) for details.


<span id="initializing-the-sdk"></span>
### Initializing the SDK

Use the following code to initialize the SDK:

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


The following table describes the parameters required for initialization:


|**Parameter** |**Required** |**Data Type** |**Description** |**Example** |
|---|---|---|---|---|
|AppID |Yes |String |App ID, which is the unique identifier of your SDK application. |`123456` |
|AppName |Yes |String |Application name, which is the name of your SDK application. |`video_demo` |
|AppVersion |Yes |String |The version number of your Android app. A valid version number should contain two or more separators, such as "1.3.2". |`1.3.2` |
|AppChannel |Yes |String |The app's download channel. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging. |`google_play` |
|LicenseUri |Yes |String |The local path to the license file. |`assets:///license2/license2_test.lic` |


<span id="uploading-logs"></span>
### Uploading logs

By default, automatic SDK log uploading is enabled for debugging and analysis. To protect confidential data, you can call `Env.openAppLog(false)` to disable log uploading before initializing the SDK.

<span id="implementing-the-feature-for-the-host"></span>
## Implementing the feature for the host

This section provides instructions on implementing the interactive live streaming feature for the host.

<span id="starting-the-live-stream"></span>
### Starting the live stream

The host uses the RTC engine to start a stream.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074454-1681924894309.png) </span>

**Sample code**


1. Create an RTC engine, set the local preview, and configure the video capture and encoding parameters.

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
   

2. Start audio and video capture with the RTC engine.

   ```Java
    // Start video capture
    mRTCVideo.startVideoCapture();
   
    // Start audio capture
    mRTCVideo.startAudioCapture();
   ```
   

3. Create an RTC room, set the user information, and join the room. Refer to [Authentication with Token](https://docs.byteplus.com/en/byteplus-rtc/docs/70121) for details about how to get the token from the app server.


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



4. Start pushing mixed RTC streams to CDN after successfully joining the room.


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


<span id="enabling-beauty-ar-optional"></span>
### Enabling beauty AR (Optional)

Refer to [Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717) for detailed instructions on how to implement beauty AR by using the RTC engine.

<span id="starting-a-host-pk-battle"></span>
### Starting a host PK battle

To start a host PK battle, both hosts need to forward their audio and video streams to each other's rooms using the `startForwardStreamToRooms` interface.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074558-869796448675.png) </span>

**Sample code**


1. When Host A receives the notification of starting the PK battle successfully, call `startForwardStreamToRooms` to push Host A's stream to Host B's room. Similarly, Host B needs to call `startForwardStreamToRooms` to push Host B's stream to Host A's room.

   ```Java
   // Push one's flow to the opposite room
   ForwardStreamInfo forwardStreamInfo = new ForwardStreamInfo(room2ID, coHostRtcToken);
   mRTCRoom1.startForwardStreamToRooms(Collections.singletonList(forwardStreamInfo));
   ```
   

2. Adjust the video encoding parameters for PK (reduce to half resolution), then update the push\-to\-CDN layout.

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
   


<span id="ending-the-host-pk-battle"></span>
### Ending the host PK battle

To end the host PK battle, call `stopForwardStreamToRooms` to stop pushing streams between rooms, then update the push\-to\-CDN layout back to a 1\-person layout.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074619-47905823354.png) </span>

**Sample code**


1. When Host A receives the notification of ending the PK battle successfully, call `stopForwardStreamToRooms` to stop pushing Host A's stream to Host B's room. Similarly, Host B needs to call `stopForwardStreamToRooms` to stop pushing Host B's stream to Host A's room.

   ```Java
   // Stop pushing Host A's stream to Host B's room.
   mRTCRoom1.stopForwardStreamToRooms();
   
   // Stop pushing Host B's stream to Host A's room.
   mRTCRoom2.stopForwardStreamToRooms();
   ```
   

2. Resume the video encoding parameters to the original resolution, then update the push\-to\-CDN layout back to a 1\-person layout.

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
   


<span id="ending-the-live-stream"></span>
### Ending the live stream

To end the live stream, stop pushing mixed RTC streams to CDN, stop audio and video capture, remove the local preview, and destroy the RTC room and engine.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074634-1599975887259.png) </span>

**Sample code**


1. Stop pushing mixed RTC streams to CDN.

   ```Java
   // Stop pushing mixed RTC streams to CDN
   String taskId = "";
   mRTCVideo.stopPushMixedStream(taskId, MixedStreamPushTargetType.PUSH_TO_CDN);
   ```
   

2. Stop audio and video capture with the RTC engine and remove the local preview.

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
   

3. Leave and destroy the RTC room, then destroy the RTC engine.

   ```Java
   // Leave and destroy the RTC room
   mRTCRoom.leaveRoom();
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine
   RTCEngine.destroyRTCEngine();
   mRTCVideo = null;
   ```
   


<span id="implementing-the-feature-for-the-audience"></span>
## Implementing the feature for the audience

This section provides instructions on implementing the interactive live streaming feature for the audience.

<span id="playing-the-live-stream"></span>
### Playing the live stream

Use the live player to pull and play the live stream.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074648-1351968520783.png) </span>

**Sample code**


1. Create a live player and configure it.

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
   

2. Set the view for the player, set the pull stream address, and start playing.

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
   


<span id="becoming-a-co-host"></span>
### Becoming a co\-host

To become a co\-host, stop playing the live stream with the live player, and start co\-hosting using the RTC engine.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074702-940645475860.png) </span>

**Sample code**


1. Stop playing the live stream and remove the view for the live player.

   ```Java
   // Stop playing the live stream
   mLivePlayer.stop();
   
   // Remove the view for the live player
   mLocalVideoContainer.removeView(mPlayerView);
   ```
   

2. Create an RTC engine and set the local preview and video encoding parameters, and video capture parameters.

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
   

3. Start audio and video capture with the RTC engine.

   ```Java
   // Start video capture
   mRTCVideo.startVideoCapture();
   
   // Start audio capture
   mRTCVideo.startAudioCapture();
   ```
   

4. Create an RTC room, set the user information, and join the RTC room. Refer to [Authentication with Token](https://docs.byteplus.com/en/byteplus-rtc/docs/70121) for details about how to get the token from the app server.

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
   

5. Add or remove the views for other co\-hosts when receiving notifications about their stream\-publishing status.

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
   


<span id="enabling-beauty-ar-optional"></span>
### Enabling beauty AR (Optional)

Refer to [Effects](https://docs.byteplus.com/en/byteplus-rtc/docs/114717) for detailed instructions on how to implement beauty AR by using the RTC engine.

<span id="ending-co-hosting"></span>
### Ending co\-hosting

To return to being a regular audience member, stop co\-hosting with the RTC engine and resume playing the live stream with the live player.

**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074719-393629603646.png) </span>

**Sample code**


1. Leave the RTC room, stop audio and video capture with the RTC engine, and remove the local and remote views.

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
   

2. Set the view for the player and start playing the live stream.

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
   


<span id="leaving-the-live-room"></span>
### Leaving the live room

To leave the live room, do the following:


1. Stop playing the live stream and destroy the live player.

2. Leave the RTC room, stop audio and video capture, and destroy the RTC engine.


**Sequence diagram**

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260707074732-594839745970.png) </span>

**Sample code**


1. Stop playing the live stream, remove the view for the player, and destroy the live player.

   ```Java
   // Stop playing the live stream
   mLivePlayer.stop();
   
   // Destroy the live player
   mLivePlayer.destroy();
   mLivePlayer = null;
   ```
   

2. Leave the RTC room, stop audio and video capture, and destroy the RTC engine.

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
