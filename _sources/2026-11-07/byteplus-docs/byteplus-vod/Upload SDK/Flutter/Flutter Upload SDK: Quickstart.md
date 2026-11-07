---
title: "Flutter Upload SDK: Quickstart"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-upload-sdk-quickstart"
---

To enable media upload functionality in your Flutter application, you first need to integrate the Upload SDK. This guide provides step\-by\-step instructions for configuring your development environment, setting up your Android and iOS projects, and adding the necessary dependencies.

<span id="88b662f4"></span>
## Development environment


* Flutter stable channel 3.0.0 or above

* Dart Version: 3.7.0 ≤ Version < 4.0.0

* System version:

   * iOS 11.0 or above

   * Android 4.1 or above (`minSdkVersion: 16`). Requires armv7 or arm64 architecture.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is highly recommended to test on a physical device. Emulators may have missing functionalities or performance issues.   </div>
   

* Development Tools: Use the latest version of Visual Studio Code or Android Studio.


<span id="96688c34"></span>
## Integration

<span id="04174955"></span>
### **Step 1: Project configuration**

<span id="416193f2"></span>
#### Android

You need to add Maven repositories, permission declarations, and obfuscation rules.


1. In your project's build.gradle file, specify the [Maven central repository](https://search.maven.org/) and BytePlus's Maven repository as repository locations, as shown below:

   ```Groovy
   allprojects {
       repositories {
           google()
           jcenter()
           // Maven central repository
           mavenCentral()
           maven {
               // BytePlus's Maven repository
               url "https://artifact.byteplus.com/repository/public/"
           }
           maven {
               // some additional dependencies
                url "https://artifact.bytedance.com/repository/Volcengine/"
           }
       }
   }
   ```
   

2. Declare the permissions required by the SDK in `AndroidManifest.xml`.

   ```XML
   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
   <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
   ```
   

3. To prevent SDK\-related classes from being obfuscated, add the following rules to `proguard-rules.pro`.

   ```Plain
   # For the upload module
   -keep class com.pandora.common.applog.**{*;}
   -keep class com.pandora.ttuploader2.** {*;}
   -keep class com.ss.bduploader.** {*;}
   ```
   


<span id="8de8cf06"></span>
#### iOS


1. [Disable bitcode](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk#step-3-disable-bitcode).

2. Configure Pod sources. Add the following sources to the Podfile in your Xcode project:

   ```Ruby
   source 'https://github.com/volcengine/volcengine-specs.git'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   


<span id="f61a573d"></span>
### **Step 2: Add dependencies**

In your Flutter project's root directory, run the following command to install the dependencies for the corresponding version.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Replace <code>x.x.x</code> with the version number. To get the latest version number, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-upload-sdk-release-notes">Flutter Upload SDK: Release notes</a>.</div>


```Shell
flutter pub add byteplus_bd_file_upload:^x.x.x
```


<span id="3a78be5b"></span>
## Next steps

You have now completed the integration of the Flutter Upload SDK. To upload videos or media to BytePlus VOD service using the SDK, please refer to the following documents:


* [Flutter Upload SDK: Uploading audios and videos](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-upload-sdk-uploading-audios-and-videos)

* [Flutter Upload SDK: Uploading materials](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-upload-sdk-uploading-materials)
