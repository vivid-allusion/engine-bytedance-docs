---
title: "FAQ during Building Android Apps"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/faq-during-building-android-apps"
---

This document provides solutions to common issues that you may encounter when integrating the RTC SDK into an Android app.

<span id="failed-resolution-contextcompat"></span>
## The app crashes with `Failed resolution of: Landroid/support/v4/content/ContextCompat;`

BytePlusRTC has not completely switched to AndroidX. If your project enables AndroidX by setting `android.useAndroidX=true`, the app may fail to build or crash with this error.

Add the following setting to the `gradle.properties` file in the project root directory:

```properties
android.enableJetifier=true
```


For complete SDK integration instructions, see [Build a Video Call App for Android](https://docs.byteplus.com/docs/byteplus-rtc/docs-70134).

<span id="configure-code-obfuscation"></span>
## How do I configure code obfuscation?

The `ProGuard` configuration file is already included in the BytePlusRTC library, so you do not need to add additional rules for BytePlusRTC.

If you require detailed information regarding obfuscation configurations, please consult technical support.

<span id="keep-capturing-in-background"></span>
## How do I keep audio and video capture active while the app is in the background?

If your app targets Android 11 (API level 30) or later and must continue capturing audio or video after it enters the background, start a foreground service before the app enters the background. The foreground service keeps the app eligible to access the microphone or camera in the background. It does not start RTC capture. After creating the `RTCEngine` instance, call [startAudioCapture](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#startaudiocapture) or [startVideoCapture](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#startvideocapture) to start capture as described in [Build a Video Call App for Android](https://docs.byteplus.com/docs/byteplus-rtc/docs-70134#capture-audio-and-video).

The following example uses microphone capture. For camera capture, declare the corresponding [foreground service type](https://developer.android.com/develop/background-work/services/fg-service-types).

<span id="declare-foreground-service"></span>
### Declare the foreground service and permissions

Declare the foreground service permission under `<manifest>`, and declare the service under `<application>` in `AndroidManifest.xml`:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />

    <application>
        <service
            android:name=".RoomKeepAliveService"
            android:exported="false"
            android:foregroundServiceType="microphone" />
    </application>
</manifest>
```


If your app targets Android 13 (API level 33) or later, declare and request the following permission so that the foreground\-service notification can appear in the notification drawer:

```xml
<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
```


The foreground service must provide a notification even if the user denies this permission. In that case, Android displays the foreground\-service notice in Task Manager instead of the notification drawer.

If your app targets Android 14 (API level 34) or later, declare the permission that corresponds to the foreground service type. For microphone capture, add:

```xml
<uses-permission android:name="android.permission.FOREGROUND_SERVICE_MICROPHONE" />
```


For camera capture, use `camera` as the service type and declare `android.permission.FOREGROUND_SERVICE_CAMERA`. If the service captures both audio and video, use `android:foregroundServiceType="microphone|camera"` and declare both permissions. You must also request the `RECORD_AUDIO` and `CAMERA` runtime permissions as applicable. See [Dynamic permission request](https://docs.byteplus.com/capture-audio-and-vide#dynamicpermission) for the BytePlus RTC permission example.

<span id="implement-foreground-service"></span>
### Implement the foreground service

Create a service that displays an ongoing notification while capture continues:

```java
import android.app.Notification;
import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.app.Service;
import android.content.Intent;
import android.content.pm.ServiceInfo;
import android.os.Build;
import android.os.IBinder;

import androidx.annotation.Nullable;
import androidx.core.app.NotificationCompat;

public class RoomKeepAliveService extends Service {
    public static final String CHANNEL_ID = "RoomKeepAliveServiceChannel";
    private static final int NOTIFICATION_ID = 110;

    @Nullable
    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        createNotificationChannel();

        Intent notificationIntent = new Intent(this, MainActivity.class);
        PendingIntent pendingIntent = PendingIntent.getActivity(
                this,
                0,
                notificationIntent,
                PendingIntent.FLAG_IMMUTABLE
        );

        Notification notification = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setContentTitle("Call in progress")
                .setSmallIcon(R.drawable.ic_notification)
                .setContentIntent(pendingIntent)
                .setOngoing(true)
                .build();

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {
            startForeground(
                    NOTIFICATION_ID,
                    notification,
                    ServiceInfo.FOREGROUND_SERVICE_TYPE_MICROPHONE
            );
        } else {
            startForeground(NOTIFICATION_ID, notification);
        }
    }

    private void createNotificationChannel() {
        if (Build.VERSION.SDK_INT < Build.VERSION_CODES.O) {
            return;
        }
        NotificationChannel channel = new NotificationChannel(
                CHANNEL_ID,
                "RTC foreground service",
                NotificationManager.IMPORTANCE_DEFAULT
        );
        NotificationManager manager = getSystemService(NotificationManager.class);
        if (manager != null) {
            manager.createNotificationChannel(channel);
        }
    }
}
```


Replace `MainActivity` and `R.drawable.ic_notification` with resources from your app. If you capture video, pass `ServiceInfo.FOREGROUND_SERVICE_TYPE_CAMERA`; for both audio and video, combine the service types with the bitwise OR operator.

<span id="start-stop-foreground-service"></span>
### Start and stop the service

Start the service while the app is in the foreground, such as when the user joins an RTC room. Stop it when background capture is no longer needed, such as when the user leaves the room:

```java
import android.content.Context;
import android.content.Intent;

import androidx.core.content.ContextCompat;

private void startRoomKeepAliveService(Context context) {
    Intent intent = new Intent(context, RoomKeepAliveService.class);
    ContextCompat.startForegroundService(context, intent);
}

private void stopRoomKeepAliveService(Context context) {
    Intent intent = new Intent(context, RoomKeepAliveService.class);
    context.stopService(intent);
}
```


Starting the service does not change the RTC capture state. Continue to use [startAudioCapture](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#startaudiocapture), [stopAudioCapture](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#stopaudiocapture), [startVideoCapture](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#startvideocapture), and [stopVideoCapture](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#stopvideocapture) to manage capture.

Android restricts starting foreground services from the background. Start the service before the app enters the background, and follow the latest Android requirements for [foreground services that access while-in-use permissions](https://developer.android.com/develop/background-work/services/fgs/restrictions-bg-start#wiu-restrictions).

<span id="bluetooth-permission-target-sdk-31"></span>
## How do I configure Bluetooth permissions when `targetSdkVersion` is 31 or later?

Declare the Bluetooth connection permission in `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```


Request `BLUETOOTH_CONNECT` at runtime before using a Bluetooth headset. Camera and microphone permissions are covered in [Dynamic permission request](https://docs.byteplus.com/docs/byteplus-rtc/docs-70134#dynamicpermission). The following example requests the additional Bluetooth permission on Android 12 or later:

```java
import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Build;

import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

private static final int REQUEST_BLUETOOTH_CONNECT = 24;

private void requestBluetoothPermission() {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S
            && ContextCompat.checkSelfPermission(
                    this,
                    Manifest.permission.BLUETOOTH_CONNECT
            ) != PackageManager.PERMISSION_GRANTED) {
        ActivityCompat.requestPermissions(
                this,
                new String[]{Manifest.permission.BLUETOOTH_CONNECT},
                REQUEST_BLUETOOTH_CONNECT
        );
    }
}
```


<span id="enable-in-ear-monitoring"></span>
## How do I enable in\-ear monitoring on Android?

After creating the `RTCEngine` instance and starting audio capture, call [setEarMonitorMode](https://docs.byteplus.com/docs/byteplus-rtc/docs-70080#setearmonitormode) to enable in\-ear monitoring:

```java
import com.ss.bytertc.engine.data.EarMonitorMode;

rtcEngine.startAudioCapture();
rtcEngine.setEarMonitorMode(EarMonitorMode.EAR_MONITOR_MODE_ON);
```


In\-ear monitoring applies to audio captured by the RTC SDK. Wired earbuds or headphones are recommended for lower latency. The RTC SDK supports SDK\-level and hardware\-level in\-ear monitoring. When the app is on the device manufacturer's trusted list and the environment meets the required conditions, the SDK automatically uses hardware\-level in\-ear monitoring. Otherwise, it uses SDK\-level in\-ear monitoring.

<span id="distorted-video-emulator"></span>
## Why is the video distorted when I debug with an emulator?

Use a physical device for debugging whenever possible. Distorted video in an emulator can be caused by incorrect camera settings or missing camera permissions.

When developing on macOS and configuring the emulator to use the Mac camera, restart the computer after changing the setting. When the emulator starts, allow it to access the camera in the system prompt.

<span id="opencl-android-12"></span>
## How do I adapt OpenCL libraries for Android 12 or later?

On Android, some video processing features rely on OpenCL libraries supplied by the device manufacturer. If the app targets Android 12 (API level 31) or later, Android requires the app to declare the vendor libraries that it accesses. Without these declarations, affected video processing features may not work as expected.

Complete this adaptation if both of the following conditions apply:


* The app targets Android 12 (API level 31) or later.

* The app uses an RTC video processing feature that depends on OpenCL, or has strict video rendering frame\-rate requirements. Confirm with BytePlus RTC technical support whether the feature you use has this dependency.


Upgrade the Android Gradle Plugin to version 4.2.0 or later so that the build toolchain supports `<uses-native-library>`. Then add the following declarations inside the `<application>` element in `AndroidManifest.xml`:

```xml
<application>
    <uses-native-library
        android:name="libOpenCL.so"
        android:required="false" />
    <uses-native-library
        android:name="libGLES_mali.so"
        android:required="false" />
    <uses-native-library
        android:name="libmali.so"
        android:required="false" />
    <uses-native-library
        android:name="libPVROCL.so"
        android:required="false" />
    <uses-native-library
        android:name="libpocl.so"
        android:required="false" />
</application>
```


For more information, see [Changes to native shared libraries](https://developer.android.com/about/versions/12/behavior-changes-12#vendor-libraries) and [<uses-native-library>](https://developer.android.com/guide/topics/manifest/uses-native-library-element) in the Android documentation.
