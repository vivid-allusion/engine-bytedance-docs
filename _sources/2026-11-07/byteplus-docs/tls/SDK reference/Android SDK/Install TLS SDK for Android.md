---
title: "Install TLS SDK for Android"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_tls_sdk_for_android"
---

Before you use a Torch Log Service (TLS) SDK to perform operations, install the SDK. This topic describes how to install TLS SDK for Android.

<span id="前提条件"></span>
## **Before you begin**


* Create and get a BytePlus AccessKey pair.

* The AccessKey pair has the permissions to access all API actions, resulting in high risks. We recommend that you create and use an IAM user to call API actions or perform routine O&M. Before you perform operations as an IAM user, make sure that the IAM user is granted the permissions to operate TLS resources.


<span id="准备开发环境"></span>
## Preparing a development environment

TLS SDK for Android supports Android 4.0 and later. Before you install the SDK, make sure that an Android development environment is set up. For more information, visit the [Android official website](http://developer.android.com/sdk/index.html) and [Android Studio](https://developer.android.com/studio?spm=a2c4g.11186623.0.0.4eca60b1zlyFwL).

Run the following command to view your Android version:

```bash
adb shell getprop ro.build.version.release
```


<span id="集成-android-sdk"></span>
## Integrating TLS SDK for Android


1. Create an Android project. To create a project through Android Studio, refer to the [official documentation](https://developer.android.com/studio/projects/create-project).

2. Integrate TLS SDK for Android into your project through Maven Central.

   1. In the `build.gradle` file of your project root directory, add the following code to add the Maven Central dependency:

      ```Plain
      buildscript {
          repositories {
              ...
              mavenCentral()
          }
          ...
      }
      
       allprojects {
          repositories {
              ...
              mavenCentral()
          }
      }
      ```
      

   2. In the `build.gradle` file of the specified module directory, add the following code to integrate TLS SDK for Android into your Android project:

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the following code, 1.1.4 indicates the SDK version. Currently, version 1.1.4 and later are supported. We recommend that you use the latest version. To view the list of versions, visit <a href="https://search.maven.org/artifact/com.volcengine/volc-tls-android-sdk">Maven</a>.      </div>
      

      ```Plain
      ...
       dependencies {
           ...
          implementation 'com.squareup.okhttp3:okhttp:4.10.0'
          implementation 'com.volcengine:volc-tls-android-sdk:1.1.4'
        }
      ```
      

3. Add network permissions for the SDK.

   The SDK collects and sends application logs to TLS over the internet. In the `/app/Manifests/AndroidManifest.xml` file, add the following permissions after `</application>`:

   ```Plain
   <uses-permission android:name="android.permission.INTERNET" />
   ```
   

4. To prevent obfuscating the code in TLS SDK, add the following line.

   ```Plain
   -keep class net.jpountz.** { *; }
   ```
