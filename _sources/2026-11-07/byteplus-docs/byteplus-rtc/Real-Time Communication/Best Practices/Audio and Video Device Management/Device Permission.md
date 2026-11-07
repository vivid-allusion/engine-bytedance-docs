---
title: "Device Permission"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-177013"
---

In the process of using RTC, it is necessary to obtain device permissions to ensure a seamless real\-time communication experience. For example, audio communication requires microphone permission, video communication requires camera permission, and screen sharing on PC requires screen recording permission.

This guide provides step\-by\-step instructions and best practices for requesting microphone and camera permissions across multiple platforms, including Android, iOS, macOS, Windows, and Electron.

<span id="android"></span>
## Android


1. App permission configuration


Add the following permissions inside the `<manifest>` tag in the `/app/Manifests/AndroidManifest.xml` file.

```xml
 <uses-permission android:name="android.permission.INTERNET" />
 <uses-permission android:name="android.permission.CAMERA" />
 <uses-permission android:name="android.permission.RECORD_AUDIO" />
 <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
 <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
 <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
 <uses-permission android:name="android.permission.BLUETOOTH" />
 <!-- For Android 12.0 and above devices, the following permissions also need to be added. -->
 <uses-permission android:name="android.permission.BLUETOOTH_CONNECT"  />
```



2. Request microphone and camera permissions within the app


```java
//Constants used for callbacks
int MY_PERMISSION_APPLY = 1;
//Permission to use the camera. Camera: CAMERA; Microphone: RECORD_AUDIO
int permission = ContextCompat.checkSelfPermission(this, Manifest.permission.CAMERA);
//Check if camera permission is granted
if (permission == PackageManager.PERMISSION_GRANTED) {
    //Yes. Proceed with execution.           
} else { 
    //No. Prompt to obtain permission.
    String[] perms = {"android.permission.CAMERA"};
    ActivityCompat.requestPermissions(this, perms, MY_PERMISSION_APPLY);
}

public void onRequestPermissionsResult(int permsRequestCode, String[] permissions, int[] grantResults){
    switch(permsRequestCode){
        case MY_PERMISSION_APPLY:
            boolean accepted = grantResults[0]==PackageManager.PERMISSION_GRANTED;
            if(!accepted){
                //User denied permission
            }else{
                //User granted permission
            }
            break;
    }
}
```


> When permission is not obtained, the following callbacks will be received.


```java
//If microphone permission is not obtained, the error type will be MEDIA_DEVICE_ERROR_NOPERMISSION.
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onAudioDeviceStateChanged(
    String deviceID,
    AudioDeviceType deviceType,
    int deviceState,
    int deviceError)
//If camera permission is not obtained, the error type will be MEDIA_DEVICE_ERROR_NOPERMISSION.
public void com.ss.bytertc.engine.handler.IRTCEngineEventHandler.onVideoDeviceStateChanged(
    String deviceID,
    VideoDeviceType deviceType,
    int deviceState,
    int deviceError)
```


<span id="ios-macos"></span>
## iOS & macOS


1. App permission configuration


Add the following two items to the Info.plist file of the app, corresponding to the prompt messages for microphone and camera when the system displays the authorization dialog.


|**Key** |**Value** |
|---|---|
|Privacy \- Microphone Usage Description |Fill in the purpose of microphone usage, e.g., xx wants to access your microphone. Without permission, audio calls will not be possible. |
|Privacy \- Camera Usage Description |Fill in the purpose of camera usage, e.g., xx wants to access your camera. Without permission, video calls will not be possible. |


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/5111eh7lbfnuhf/5405a230-3b65-4917-9be5-95b3d27ae192.png) </span>


2. Request microphone and camera permissions within the app


```objectivec
//Check permission status. Camera: AVMediaTypeVideo; Microphone: AVMediaTypeAudio
AVAuthorizationStatus authStatus = [AVCaptureDevice authorizationStatusForMediaType:AVMediaTypeAudio];
//Permission definitions 
typedef NS_ENUM(NSInteger, AVAuthorizationStatus) {
    AVAuthorizationStatusNotDetermined = 0, /* The user has not yet been asked for permission. */
    AVAuthorizationStatusRestricted    = 1, /* Unauthorized. Parental control.*/
    AVAuthorizationStatusDenied        = 2, /* The user has denied permission. */
    AVAuthorizationStatusAuthorized    = 3, /* The user has granted permission. */
} API_AVAILABLE(macos(10.14), ios(7.0)) __WATCHOS_PROHIBITED __TVOS_PROHIBITED;
//Request permission
if (authStatus == AVAuthorizationStatusNotDetermined) {
    [AVCaptureDevice requestAccessForMediaType:AVMediaTypeAudio completionHandler:^(BOOL granted) {
        
        dispatch_async(dispatch_get_main_queue(), ^{
            if (granted) {
                [self doSomething];
            } else {
                [self showAlertWithTitle:@"Reminder" message:@"You have not enabled the Microphone permission. This is required to make calls. Please enable microphone access in your device settings."];
            }
        });
    }];
} else if (authStatus == AVAuthorizationStatusDenied || authStatus == AVAuthorizationStatusRestricted) {
     [self showAlertWithTitle:@"Reminder" message:@"You have not enabled the Microphone permission. This is required to make calls. Please enable microphone access in your device settings."];
} else if (authStatus == AVAuthorizationStatusAuthorized) {
     [self doSomething];
}
```


> When permission is not obtained, the following callbacks will be received.


```objectivec
//If microphone permission is not obtained, the error type will be ByteRTCMediaDeviceErrorDeviceNoPermission
- (void)rtcEngine:(ByteRTCEngine * _Nonnull)engine onAudioDeviceStateChanged:(NSString*_Nonnull)deviceID device_type:(ByteRTCAudioDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError;

//If camera permission is not obtained, the error type will be ByteRTCMediaDeviceErrorDeviceNoPermission
- (void)rtcEngine:(ByteRTCEngine * _Nonnull)engine onVideoDeviceStateChanged:(NSString*_Nonnull)deviceID device_type:(ByteRTCVideoDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError;
```


> Note: If Background Modes is not enabled on iOS, audio and video calls will be interrupted when the app is in the background. Once enabled, audio and video calls can be maintained in the background.


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/5111eh7lbfnuhf/c377c1f6-c684-4745-8c3e-2b023bb81c56.png) </span>

<span id="windows"></span>
## Windows

On Windows, apps can access microphone and camera permissions by default without requiring a specific permission request.

If microphone/camera permissions are disabled in the system settings, the following callbacks will be received.

```cpp
//If microphone permission is not obtained, the error type will be kMediaDeviceErrorDeviceNoPermission.
virtual void bytertc::IRTCEngineEventHandler::onAudioDeviceStateChanged(
    const char* device_id,
    bytertc::RTCAudioDeviceType device_type,
    bytertc::MediaDeviceState device_state,
    bytertc::MediaDeviceError device_error)
//If camera permission is not obtained, the error type will be kMediaDeviceErrorDeviceNoPermission.
virtual void bytertc::IRTCEngineEventHandler::onVideoDeviceStateChanged(
    const char* device_id,
    bytertc::RTCVideoDeviceType device_type,
    bytertc::MediaDeviceState device_state,
    bytertc::MediaDeviceError device_error)
```


> Note: If permissions are disabled in the system settings, you must re\-enable them in Settings \> Privacy \> Microphone/Camera.


<span id="electron"></span>
## Electron


1. Create the entitlements.mac.plist file and add the following configuration


```java
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>com.apple.security.cs.allow-jit</key>
    <true/>
    <key>com.apple.security.cs.allow-unsigned-executable-memory</key>
    <true/>
    <key>com.apple.security.cs.allow-dyld-environment-variables</key>
    <true/>
    <key>com.apple.security.device.audio-input</key>
    <true/>
    <key>com.apple.security.device.camera</key>
    <true/>
  </dict>
</plist>
```



2. Configure package.json


```java
"mac": {
      "entitlements": "build/entitlements.mac.plist",
      "extendInfo": {
        "NSMicrophoneUsageDescription": "Authorize access to the microphone",
        "NSCameraUsageDescription": "Authorize access to the camera"
      }
    }
```



3. Request microphone/camera permissions


```java
const { ipcMain,systemPreferences } = require('electron')
//Obtain microphone permission
ipcMain.on("getMediaAccessStatus",async ()=>{
    //Check if microphone permission is enabled
    let getMediaAccessStatus = systemPreferences.getMediaAccessStatus('microphone')
    if(getMediaAccessStatus !== 'granted'){
      //Request microphone permission
      if (process.platform === "darwin") {
      await systemPreferences.askForMediaAccess("microphone");
     }
    }
})

//Obtain camera permission
ipcMain.on("getMediaAccessStatus",async ()=>{
    //Check if camera permission is enabled
    let getMediaAccessStatus = systemPreferences.getMediaAccessStatus('camera')
    if(getMediaAccessStatus !== 'granted'){
      //Request camera permission
      if (process.platform === "darwin") {
      await systemPreferences.askForMediaAccess("camera");
     }
    }
})

//Use the following method to check the screen recording permission status
const screenPrivilege = systemPreferences.getMediaAccessStatus("screen");
```


> Note: On macOS 12.1 and later, an app might work during debugging but crash after installation. To fix this, request microphone and camera permissions from the main process. See the relevant content in the previous section on how to obtain permissions in Electron.
