---
title: "Android"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70134"
---

To build a real\-time audio and video call app for Android from scratch, you can follow this guide. It provides step\-by\-step instructions for integrating the BytePlus RTC SDK, from project setup and SDK integration to implementing the core logic for a complete audio and video communication application.

<span id="prerequisites"></span>
## Prerequisites

Before you start integrating the RTC SDK, please make sure the following requirements are met:


* You are using Android Studio Arctic Fox | Ver. 2020.3.1 or higher versions (This document uses Android Studio Iguana | Ver. 2023.2.1)

* You are using an authentic Android device or emulator with Android 4.4 or higher versions.

* Your Android development device and computer are connected to the internet.

* To enable the real\-time audio and video call service, get an AppID and a temporary token from the [BytePlus Console](https://console.byteplus.com/rtc/listRTC).


<span id="project-creation-and-configuration"></span>
## Project creation and configuration

<span id="create-a-new-project"></span>
### Create a new project


1. Open Android Studio. In the Welcome to Android Studio window, click on **New Project**.

2. Choose **Empty Views Activity** in the Project Templates page, and click **Next**.

3. On the Project Configurations page, provide the project name, package name, and save location. Choose Java as the language, API level 19 or higher, and Groovy as the build configuration language, then click **Finish**. After the project is created, it is ready for you to start coding.


<span id="configure-permissions"></span>
### Configure permissions

The required permissions are declared within the SDK, so you don't need to add them manually. For sensitive permissions, you must request them at runtime in your Activity. Sample codes are provided in the [Dynamic permission application](https://docs.byteplus.com/docs/byteplus-rtc/docs-70134#dynamicpermission) section.


* If your app targets Android 11 (API level 30) or higher versions as target platform and you still need to capture the microphone while the app is in the background, you must declare the foreground service type in the `AndroidManifest.xml file`: `android:foregroundServiceType:microphone`. In addition, if your app targets Android 14 (API level 34) or higher versions as target platform, you must request the `FOREGROUND_SERVICE_MICROPHONE` permission for the types of tasks the foreground service will execute. The same permissions are required for camera access.

* If your app targets Android 12 (API level 31) or higher versions and requires Bluetooth, you should additionally declare the `BLUETOOTH_CONNECT`permission in the `AndroidManifest.xml` file, and submit a dynamic application in Activity.


<span id="integrate-sdk"></span>
## Integrate SDK

<span id="via-maven"></span>
### Via Maven


1. In the top\-left corner of the Android Studio window, switch to the **Project** view, and configure a Maven repository address in the `settings.gradle` file of the project root directory.

   ```groovy
   dependencyResolutionManagement {
       repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
       repositories {
           google()
           mavenCentral()
           maven {  url 'https://artifact.byteplus.com/repository/public/' }
       }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your Android Gradle Plugin version is below v7.1.0, then you should configure the Maven repository address in the <code>build.gradle</code> file of the project root directory.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```groovy
   allprojects {
       repositories {
           ...
           maven { url 'https://artifact.byteplus.com/repository/public/' }
       }
   }
   ```
      </div>
   

2. Add the RTC SDK dependency in the `build.gradle` file of the app.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to replace <code>3.x.y.z</code> with a specific version number. Please refer to the <a href="https://docs.byteplus.com/en/docs/12/docs-75707">Download SDK</a> section for the latest version numbers.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```groovy
   dependencies {
       ...
       implementation 'com.byteplus:BytePlusRTC:3.x.y.z' 
   }
   ```
      </div>
   

3. Add `android.enableJetifier=true` in the `gradle.properties` file of the project root directory to ensure compatibility.

4. Upon setup, click **Sync now** to synchronize the configurations.


<span id="integrate-manually"></span>
### **Integrate manually**


1. Download and decompress the [BytePlusRTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707) file.

2. In the top\-left corner of the Android Studio window, switch to the **Project** view.

   1. Put the decompressed `BytePlusRTC-Release.aar` under the `app/libs` directory, and place the four architecture folders (containing `.so` files) into the `app/jniLibs` directory.

   2. [Optional] If you need functions related to beautification, you must integrate `effectAAR-release_V4.4.3Lite.aar` at the same time.

3. Add the RTC SDK dependency and the `.so` file dependencies in your app's `build.gradle` file.

   ```groovy
   android {
       ...
       sourceSets {
           main {
               // Specify the directory containing the .so files
               jniLibs.srcDirs = ['jniLibs']
           }
       }
   }
   ...
   dependencies {
       ...
       // Integrate the main RTC library
       implementation files('libs/BytePlusRTC-Release.aar')
       // Integrate the effect library for beauty and visual effects
       implementation files('libs/effectAAR-release_V4.4.3Lite.aar')
   }
   ```
   

4. [Necessary] Since BytePlusRTC has not completely switched to `androidx`, you need to add `android.enableJetifier=true` in the `gradle.properties` file of the project root directory to ensure compatibility.

5. Upon setup, click **Sync now** to synchronize the configurations.


<span id="create-a-ui"></span>
## Create a UI

Create a UI for audio and video calls based on your project requirements. For basic audio and video calls, it's suggested to at least include a local video window, a remote video window, and buttons to enter and exit a room.

Replace corresponding codes in `src/main/res/layout/activity_main.xml` with the sample codes below for quick UI creation.

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    tools:padding="16dp">

    <FrameLayout
        android:id="@+id/local_container"
        android:layout_width="0dp"
        android:layout_height="300dp"
        android:layout_marginStart="16dp"
        android:layout_marginEnd="4dp"
        app:layout_constraintEnd_toStartOf="@id/remote_container"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <FrameLayout
        android:id="@+id/remote_container"
        android:layout_width="0dp"
        android:layout_height="300dp"
        android:layout_marginStart="4dp"
        android:layout_marginEnd="16dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@id/local_container"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/join_room"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginHorizontal="16dp"
        android:text="Join Room"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/local_container" />

    <Button
        android:id="@+id/leave_room"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginHorizontal="16dp"
        android:text="Leave Room"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/join_room" />

</androidx.constraintlayout.widget.ConstraintLayout>
```


<span id="implement-audio-and-video-calls"></span>
## Implement audio and video calls

This chapter provides an API call flow diagram and complete implementation code, followed by a detailed introduction to each step.

<span id="sample-codes"></span>
### Sample codes

Copy the following sample code and replace all contents after `package com.example.`in the `MainActivity.java` file with it. The `com.example.`here refers to the software package name designated when you created the project. Connect and select your Android device. Click the **Run 'app'**  button in the Android Studio toolbar to quickly run the audio and video call application.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the code, replace the placeholder values for <code>roomId</code>, <code>userId</code>, <code>APP_ID</code>, and <code>token</code> with the credentials you obtained from the Console.</div>


```java
package com.byteplus.rtc.quickstart;

import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Build;
import android.os.Bundle;
import android.view.TextureView;
import android.widget.FrameLayout;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.AppCompatButton;
import androidx.core.content.ContextCompat;
import com.ss.bytertc.engine.RTCRoom;
import com.ss.bytertc.engine.RTCRoomConfig;
import com.ss.bytertc.engine.RTCEngine;
import com.ss.bytertc.engine.UserInfo;
import com.ss.bytertc.engine.VideoCanvas;
import com.ss.bytertc.engine.data.EngineConfig;
import com.ss.bytertc.engine.data.RemoteStreamKey;
import com.ss.bytertc.engine.data.StreamIndex;
import com.ss.bytertc.engine.handler.IRTCRoomEventHandler;
import com.ss.bytertc.engine.handler.IRTCEngineEventHandler;
import com.ss.bytertc.engine.type.ChannelProfile;

public class MainActivity extends AppCompatActivity {

    private static final String APP_ID = ""; 
    private static final String roomId = ""; 
    private static final String userId = ""; 
    private static final String token = ""; 

    private FrameLayout localViewContainer;
    private FrameLayout remoteViewContainer;

    private RTCEngine rtcEngine;
    private RTCRoom rtcRoom;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        requestPermission();

        localViewContainer = findViewById(R.id.local_container);
        remoteViewContainer = findViewById(R.id.remote_container);

        ((AppCompatButton) findViewById(R.id.join_room)).setOnClickListener(v -> {
            joinRoom(roomId);
        });

        ((AppCompatButton) findViewById(R.id.leave_room)).setOnClickListener(v -> {
            leaveRoom();
        });

      EngineConfig engineConfig = new EngineConfig();
      engineConfig.context = this;
      engineConfig.appID = APP_ID;
      rtcEngine = RTCEngine.createRTCEngine(engineConfig, engineEventHandler);
        setLocalRenderView();
        rtcEngine.startVideoCapture();
        rtcEngine.startAudioCapture();
    }

    public void requestPermission() {
        String[] PERMISSIONS_STORAGE = {
                Manifest.permission.RECORD_AUDIO,
                Manifest.permission.CAMERA};

        if (Build.VERSION.SDK_INT  >= Build.VERSION_CODES.M) {
            if (ContextCompat.checkSelfPermission(this, "android.permission.CAMERA") != PackageManager.PERMISSION_GRANTED
                    || ContextCompat.checkSelfPermission(this, "android.permission.RECORD_AUDIO") != PackageManager.PERMISSION_GRANTED) {
                requestPermissions(PERMISSIONS_STORAGE, 22);
            }
        }
    }

    private void setLocalRenderView() {
        TextureView textureView = new TextureView(this);
        localViewContainer.removeAllViews();
        localViewContainer.addView(textureView);

        VideoCanvas videoCanvas = new VideoCanvas();
        videoCanvas.renderView = textureView;
        videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;

        rtcEngine.setLocalVideoCanvas(videoCanvas);
    }

    private void setRemoteRenderView(String streamId) {
        TextureView remoteTextureView = new TextureView(this);
        remoteViewContainer.removeAllViews();
        remoteViewContainer.addView(remoteTextureView);
        VideoCanvas videoCanvas = new VideoCanvas();
        videoCanvas.renderView = remoteTextureView;
        videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;

        rtcEngine.setRemoteVideoCanvas(streamId, videoCanvas);
    }

    private void removeRemoteView(String streamId) {
        rtcEngine.setRemoteVideoCanvas(streamId, null);
    }

   IRTCEngineEventHandler engineEventHandler = new IRTCEngineEventHandler() {
        @Override
        public void onFirstRemoteVideoFrameDecoded(RemoteStreamKey streamKey, int width, int height, int rotation) {
            runOnUiThread(() -> setRemoteRenderView(streamKey.getUserId()));
        }
   };

   IRTCRoomEventHandler rtcRoomEventHandler = new IRTCRoomEventHandler() {
        @Override
        public void onUserUnpublishStream(String userId, RemoteStreamKey streamKey, int reason) {
            runOnUiThread(() -> removeRemoteView(streamKey.getUserId()));
        }
   };

    private void joinRoom(String roomId) {
        rtcRoom = rtcEngine.createRTCRoom(roomId);
        rtcRoom.setRTCRoomEventHandler(rtcRoomEventHandler);
        // 用户信息
        UserInfo userInfo = new UserInfo(userId, "");
      boolean isAutoPublishAudio = true;
      boolean isAutoPublishVideo = true;
      boolean isAutoSubscribeAudio = true;
      boolean isAutoSubscribeVideo = true;
      
        RTCRoomConfig roomConfig = new RTCRoomConfig(
            ChannelProfile.CHANNEL_PROFILE_CHAT_ROOM,
            null,
            isAutoPublishAudio,
            isAutoPublishVideo,
            isAutoSubscribeAudio,
            isAutoSubscribeVideo
        );

      rtcRoom.joinRoom(token, userInfo, true, roomConfig);
    }

    private void leaveRoom() {
        if (rtcRoom != null) {
            rtcRoom.leaveRoom();
            rtcRoom.destroy();
            rtcRoom = null;
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (rtcEngine != null) {
            rtcEngine.stopVideoCapture();
            rtcEngine.stopAudioCapture();
        }
      RTCEngine.destroyRTCEngine();
    }
}
```


<span id="import-classes"></span>
### Import classes

Import classes that SDK needs.

```java
import com.ss.bytertc.engine.RTCRoom;
import com.ss.bytertc.engine.RTCRoomConfig;
import com.ss.bytertc.engine.RTCEngine;
import com.ss.bytertc.engine.UserInfo;
import com.ss.bytertc.engine.VideoCanvas;
import com.ss.bytertc.engine.data.RemoteStreamKey;
import com.ss.bytertc.engine.data.StreamIndex;
import com.ss.bytertc.engine.handler.IRTCRoomEventHandler;
import com.ss.bytertc.engine.handler.IRTCEngineEventHandler;
import com.ss.bytertc.engine.type.ChannelProfile;
import com.ss.bytertc.engine.data.EngineConfig;
```


<span id="dynamicpermission"></span>
### Dynamic permission application

When starting the app, make sure that the permissions needed are authorized. This step is essential for accessing camera and microphone functionality.

```java
if (ContextCompat.checkSelfPermission(this, Manifest.permission.CAMERA) != PackageManager.PERMISSION_GRANTED
        || ContextCompat.checkSelfPermission(this, Manifest.permission.RECORD_AUDIO) != PackageManager.PERMISSION_GRANTED) {
    requestPermissions(new String[]{
            Manifest.permission.CAMERA,
            Manifest.permission.RECORD_AUDIO
    }, 22);
}
```


<span id="initialize-the-engine"></span>
### Initialize the engine

Call `createRTCEngine` to initialize the `RTCEngine` instance. All RTC\-related API calls must be made after the engine is created. This step establishes the foundation for all subsequent RTC operations.

```java
EngineConfig engineConfig = new EngineConfig();
engineConfig.context = this;
engineConfig.appID = APP_ID;
rtcEngine = RTCEngine.createRTCEngine(engineConfig, engineEventHandler);
```


<span id="capture-audio-and-video"></span>
### Capture audio and video

After creating the engine, call `startVideoCapture` to enable video capture, and call `startAudioCapture` to enable audio capture. These methods activate the device's camera and microphone for real\-time communication.

```java
rtcEngine.startVideoCapture();
rtcEngine.startAudioCapture();
```


<span id="set-local-rendering-view"></span>
### Set local rendering view

Call `setLocalVideoCanvas` to set the local rendering window. Both `TextureView` and `SurfaceView` are supported. This allows users to see their own video feed during the call.

```java
private void setLocalRenderView() {
    localViewContainer.removeAllViews();

    TextureView textureView = new TextureView(this);
    localViewContainer.addView(textureView);

    VideoCanvas videoCanvas = new VideoCanvas();
    videoCanvas.renderView = textureView;
    videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
    rtcEngine.setLocalVideoCanvas(videoCanvas);
}
```


<span id="create-and-join-a-room"></span>
### Create and join a room

Follow the steps below to create and join a room. This process establishes the communication channel between participants:


1. Call `createRTCRoom` to create an RTC room. All APIs related to rooms are in the RTCRoom class.

2. Call `setRTCRoomEventHandler` to set up room callback monitoring.

3. Call `joinRoom` to join a room.


```java

private void joinRoom(String roomId) {
    rtcRoom = rtcEngine.createRTCRoom(roomId);
    rtcRoom.setRTCRoomEventHandler(rtcRoomEventHandler);
    UserInfo userInfo = new UserInfo(userId, "");
   boolean isAutoPublishAudio = true;
   boolean isAutoPublishVideo = true;
   boolean isAutoSubscribeAudio = true;
   boolean isAutoSubscribeVideo = true;
   RTCRoomConfig roomConfig = new RTCRoomConfig(
        ChannelProfile.CHANNEL_PROFILE_CHAT_ROOM,
        null,
        isAutoPublishAudio,
        isAutoPublishVideo,
        isAutoSubscribeAudio,
        isAutoSubscribeVideo
    );
   rtcRoom.joinRoom(token, userInfo, true, roomConfig);
}
```


<span id="set-remote-rendering-video"></span>
### Set remote rendering video

When a remote user joins a channel and publishes a video stream, the SDK will trigger callbacks to notify you. Use the `onFirstRemoteVideoFrameDecoded` callback to set up remote video rendering when the first frame is received, and use `onUserUnpublishStream` to clean up when the remote user stops publishing.

```java
IRTCEngineEventHandler rtcEngineEventHandler = new IRTCEngineEventHandler() {
    @Override
    public void onFirstRemoteVideoFrameDecoded(RemoteStreamKey streamKey, int width, int height, int rotation) {
        runOnUiThread(() -> setRemoteRenderView(streamKey.getUserId()));
    }
};

IRTCRoomEventHandler rtcRoomEventHandler = new IRTCRoomEventHandler() {
   @Override
   public void onUserUnpublishStream(String userId, RemoteStreamKey streamKey, int reason) {
        runOnUiThread(() -> removeRemoteView(streamKey.getUserId()));
   }

};

private void setRemoteRenderView(String streamId) {
    TextureView remoteTextureView = new TextureView(this);
    remoteViewContainer.removeAllViews();
    remoteViewContainer.addView(remoteTextureView);
    VideoCanvas videoCanvas = new VideoCanvas();
    videoCanvas.renderView = remoteTextureView;
    videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;

    rtcEngine.setRemoteVideoCanvas(streamId, videoCanvas);
}

private void removeRemoteView(String streamId) {
    rtcEngine.setRemoteVideoCanvas(streamId, null);
}
```


<span id="leave-a-room"></span>
### Leave a room

Call `leaveRoom` to exit a room, and call `destroy` to destroy the room instance. This properly cleans up resources and notifies other participants of your departure.

```java
private void leaveRoom() {
    if (rtcRoom != null) {
        rtcRoom.leaveRoom();
        rtcRoom.destroy();
        rtcRoom = null;
    }
}
```


<span id="destroy-the-engine"></span>
### **Destroy the engine**

When exiting the app, call `destroyRTCEngine` to destroy the `RTCEngine` instance. This ensures proper cleanup of all RTC resources and prevents memory leaks.

```java
RTCEngine.destroyRTCEngine();
```


<span id="compile-and-run"></span>
## **Compile and run**


1. Enable Developer Options on the Android device, turn on USB debugging, connect the Android device to your computer using a USB cable, and select your Android device among the Android Devices options.

2. Click the **Run 'app'**  button in the Android Studio toolbar to start compilation.

3. Your Android device will open the Demo app automatically. In the pop\-up window, grant the required camera and microphone permissions.

4. (Optional) By using the same AppID and RoomID on another device, changing the UserID and generating a new temporary token, you can join the same room to experience a two\-way call.
