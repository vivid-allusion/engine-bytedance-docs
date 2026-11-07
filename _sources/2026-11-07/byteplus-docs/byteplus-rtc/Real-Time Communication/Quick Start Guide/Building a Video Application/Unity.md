---
title: "Unity"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-108610"
---

This document introduces how to integrate the BytePlus RTC SDK and implement real\-time audio and video calls with it. Follow the steps below to build up your simple audio and video call app from scratch.

<span id="prerequisites"></span>
## Prerequisites


* Unity Editor 2017+

> The following examples are based on Unity 2017. The steps might differ slightly on other Unity versions. If you encounter problems on a different Unity version, contact technical support.


* Android Studio 3.5+

* XCode 14.1 +

* Follow instructions in [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) to obtain the AppID

* Obtain RTC [SDK Files](https://docs.byteplus.com/en/docs/12/docs-75707)


<span id="step-1-integrate-sdk"></span>
## Step 1: Integrate SDK

Download the SDK package offline and then import it into the Unity project as shown in the following figure:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7bbff5814a05c73016998089e2c4d47b.png) </span>

<span id="step-2-system-configuration"></span>
## Step 2: System Configuration

<span id="windows-platform"></span>
### Windows Platform

Go to **PlayerSetting** \-\> **Other Settings**.


1. Set Scripting Runtime Version to Experimental (.Net 4.6 Equivalent).

2. Select IL2CPP as the Scripting Backend.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bcd5d6640bad3442316f49dca73bf0b9.jpg) </span>

<span id="android-platform"></span>
### Android Platform

**Configure Gradle**

In **PlayerSetting** \-\> **Publishing Settings**, check **CustomGradleTemplate**. If there is no **CustomGradleTemplate**, then check **CustomLauncherGradle Template**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3f6cba05651ca403120fb6c11a5e7cfb.png) </span>

After that, a Template.gradle file will be generated in the **Assets** \-\> **Plugins** \-\> **Android** directory, and then add the following code inside:

```kotlin
dependencies
{
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:support-v4:28.0.0'
    implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.2.61'
}

android
{
    packagingOptions
    {
        pickFirst "lib/*/libc++_shared.so"

        pickFirst "lib/*/libbmf_hydra.so"
        pickFirst "lib/*/libbmf_mods.so"
        pickFirst "lib/*/libbytenn.so"
        pickFirst "lib/*/libbytertc_ffmpeg_audio_extension.so"
        pickFirst "lib/*/libbytertc_nico_extension.so"
        pickFirst "lib/*/libbytertc_videodenoise_extension.so"
        pickFirst "lib/*/libbytertc_videosharpen_extension.so"
        pickFirst "lib/*/libbytertc_videosr_extension.so"
        pickFirst "lib/*/libh265enc.so"

    }
}

```


<span id="ios-platform"></span>
### iOS Platform

**Configuring XCodePostProcess**

Create a new Editor directory under the Assets folder, and then create a new `XCodePostProcess.cs` file within the Editor directory.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f06967f84ede1294fcc75f04f8b66ca.png) </span>

Add the configuration code for generating the XCode project in XCodePostProcess.cs:

```C#
using UnityEditor;
using UnityEditor.Callbacks;
using UnityEditor.iOS.Xcode;
using UnityEditor.iOS.Xcode.Extensions;
using System.IO;

public static class XCodePostProcess
{
    private static void AddEmbedFramework(PBXProject project, string targetGuid, string frameworkName) 
    {
#if !UNITY_2019_3_OR_NEWER
        const string defaultLocationInProj = "Frameworks/RTCVideo/Plugins/iOS";
        string framework = Path.Combine(defaultLocationInProj, frameworkName);
        string fileGuid = project.AddFile(framework, "Frameworks/" + framework, PBXSourceTree.Sdk);
        PBXProjectExtensions.AddFileToEmbedFrameworks(project, targetGuid, fileGuid);
#endif
    }

    [PostProcessBuild(999)]
    public static void OnPostProcessBuild(BuildTarget buildTarget, string path)
    {
        if(buildTarget == BuildTarget.iOS)
        {
            string projectPath = path + "/Unity-iPhone.xcodeproj/project.pbxproj";

            PBXProject pbxProject = new PBXProject();
            pbxProject.ReadFromFile(projectPath);
#if !UNITY_2019_3_OR_NEWER
            string mainTarget = PBXProject.GetUnityTargetName();
#else
            string mainTarget = pbxProject.GetUnityMainTargetGuid();
#endif
            string targetGuid = pbxProject.TargetGuidByName(mainTarget);
            pbxProject.SetBuildProperty(targetGuid, "ENABLE_BITCODE", "NO");
            pbxProject.SetBuildProperty(targetGuid, "CODE_SIGN_STYLE", "Manual");
            pbxProject.SetBuildProperty(targetGuid, "PRODUCT_NAME", "VideoSDKDemo");
        
            AddEmbedFramework(pbxProject, targetGuid, "VolcEngineRTC.framework");
            AddEmbedFramework(pbxProject, targetGuid, "VolcEngineRTCScreenCapturer.framework");
            AddEmbedFramework(pbxProject, targetGuid, "ByteRTCCWrapper.framework");
            pbxProject.SetBuildProperty(targetGuid, "LD_RUNPATH_SEARCH_PATHS", "$(inherited) @executable_path/Frameworks");
            pbxProject.WriteToFile (projectPath);

            // 修改plist
            string plistPath = path + "/Info.plist";
            PlistDocument plist = new PlistDocument();
            plist.ReadFromString(File.ReadAllText(plistPath));
            PlistElementDict rootDict = plist.root;
            rootDict.SetString("NSMicrophoneUsageDescription", "App需要您的同意,才能访问麦克风");
            rootDict.SetString("NSCameraUsageDescription", "App需要您的同意,才能访问相机");
            rootDict.SetString("CFBundleIdentifier", "${PRODUCT_BUNDLE_IDENTIFIER}");
            PlistElementArray backgroundModesArray = rootDict.CreateArray("UIBackgroundModes");
            backgroundModesArray.AddString("audio");
            plist.WriteToFile(plistPath);
        }
    }
}
```


<span id="step-2-implement-audio-and-video-calls"></span>
## Step 3: **Implement audio and video calls**

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/1086610_plantuml_diagram0.png) </span>

<span id="_1-creatertcvideo"></span>
### 1. CreateRTCVideo

```c#
int bytertc.IRTCVideo.CreateRTCVideo(RTCVideoEngineParams initParams)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|initParams |RTCVideoEngineParams |Engine initialization parameters. See [RTCVideoEngineParams](https://docs.byteplus.com/en/docs/12/docs-191862#RTCVideoEngineParams). |


<span id="_2-setvideocaptureconfig"></span>
### 2. SetVideoCaptureConfig

```c#
int bytertc.IRTCVideo.SetVideoCaptureConfig(VideoCaptureConfig videoCaptureConfig)
```



|Name |Type |Instructions |
|---|---|---|
|videoCaptureConfig |VideoCaptureConfig |Video capture parameters. See: [VideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-191862#VideoCaptureConfig). |


<span id="_3-setlocalvideosink"></span>
### 3. SetLocalVideoSink

```c#
void bytertc.IRTCVideo.SetLocalVideoSink(
    StreamIndex index,
    VideoSinkPixelFormat requiredFormat
)
```



|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Video stream type. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |
|requiredFormat |VideoSinkPixelFormat |Video frame encoding format that applies to custom rendering. See [VideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/docs-191862#VideoSinkPixelFormat). |


<span id="_4-startvideocapture"></span>
### 4. StartVideoCapture

```c#
void bytertc.IRTCVideo.StartVideoCapture()
```


<span id="_5-startaudiocapture"></span>
### 5. StartAudioCapture

```c#
void bytertc.IRTCVideo.StartAudioCapture()
```


<span id="_6-creatertcroom"></span>
### 6. CreateRTCRoom

```c#
IRTCVideoRoom bytertc.IRTCVideo.CreateRTCRoom(string roomID)
```


<span id="_7-joinroom"></span>
### 7. JoinRoom

```c#
int bytertc.IRTCVideoRoom.JoinRoom(
    string token,
    UserInfo info,
    MultiRoomConfig roomConfig
)
```



|Name |Type |Instructions |
|---|---|---|
|token |string |Dynamic key for authentication and verification of users entering the room. You must provide a token to join a room. When testing, you can use the console to generate temporary tokens. The official launch requires the use of the key SDK to generate and issue tokens at your server level. Apps with different AppIDs are not interoperable. Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will cause the join room to fail. |
|info |UserInfo |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-191862#UserInfo). |
|roomConfig |MultiRoomConfig |Room parameter configuration, set the room mode and whether to automatically publish or subscribe to streams. See [MultiRoomConfig](https://docs.byteplus.com/en/docs/12/docs-191862#MultiRoomConfig) for the specific configuration mode. |


<span id="_8-onroomstatechangedeventhandler"></span>
### 8. OnRoomStateChangedEventHandler

```c#
delegate void bytertc.OnRoomStateChangedEventHandler(
    string roomID,
    string userID,
    int state,
    string ExtraInfo
)
```



|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |User ID. |
|state |int |Room state code.<br><br><br>* 0: Success.<br><br>* !0: Failure. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-191861#ErrorCode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-191861#WarningCode) for specific indications. The user has been removed from the room due to one of the following reasons. \-1004: The same user joined the room from another client \-1006: The administrator kicked the user out of the room by calling openAPI. |
|ExtraInfo |string |Extra information. `join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` means the user rejoins the room. `elapsed` indicates the time interval from calling [JoinRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-joinroom) to successfully joining the room, in ms. |


<span id="_9-onuserjoinedeventhandler"></span>
### 9. OnUserJoinedEventHandler

```c#
delegate void bytertc.OnUserJoinedEventHandler(
    string roomID,
    UserInfo userInfo,
    int elapsed
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userInfo |UserInfo |See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-191862#UserInfo). |
|elapsed |int |Reserved parameter. |


<span id="_10-onfirstremotevideoframedecodedeventhandler"></span>
### 10. OnFirstRemoteVideoFrameDecodedEventHandler

```c#
delegate void bytertc.OnFirstRemoteVideoFrameDecodedEventHandler(
    RemoteStreamKey key,
    VideoFrameInfo info
)
```



|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote stream information, see [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|info |VideoFrameInfo |Video Frame Information, see [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrameInfo) |


<span id="_11-setremotevideosink"></span>
### 11. SetRemoteVideoSink

```c#
void bytertc.IRTCVideo.SetRemoteVideoSink(
    RemoteStreamKey streamKey,
    VideoSinkPixelFormat requiredFormat
)
```



|Name |Type |Instructions |
|---|---|---|
|streamKey |RemoteStreamKey |Remote stream information which specifies the source and type of the video stream to be rendered. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|requiredFormat |VideoSinkPixelFormat |Encoding format that applies to the custom renderer. See [VideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/docs-191862#VideoSinkPixelFormat) |


<span id="_12-onuserleaveeventhandler"></span>
### 12. OnUserLeaveEventHandler

```c#
delegate void bytertc.OnUserLeaveEventHandler(
    string roomID,
    string userID,
    UserOfflineReason reason
)
```



|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |The ID of the user who leaves the room or becomes invisible. |
|reason |UserOfflineReason |The reason the user left the room. See [UserOfflineReason](https://docs.byteplus.com/en/docs/12/docs-191862#UserOfflineReason). |


<span id="_13-leaveroom"></span>
### 13. LeaveRoom

```c#
void bytertc.IRTCVideoRoom.LeaveRoom()
```


<span id="_14-release"></span>
### 14. Release

```c#
void bytertc.IRTCVideo.Release()
```
