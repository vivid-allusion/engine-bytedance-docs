---
title: "Configuring Xcode in React Native projects"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-configuring-xcode-in-react-native-projects"
---

Set up Xcode to manage and build the iOS part of your React Native project, including setting signing credentials and adjusting build settings.

<span id="d891ac51"></span>
# **Prerequisities**

Before you begin with creating RN projects, ensure that the following requirements have been met:


* Downloaded Xcode.

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to the [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/150-ios-package-deliverables-list).

* Set up your RN environment. For more information, refer to the [RN developers guide](https://reactnative.dev/docs/set-up-your-environment?platform=ios).

* Completed the steps in: [Creating React Native projects in iOS](https://docs.byteplus.com/docs/video-editor-sdk/150-creating-react-native-projects-in-ios).


<span id="15099da1"></span>
# Step 1: Adding specific files

In the sample file provided to you, add specific files into your project's iOS file.

**To add specific files:** 


1. Open the sample file provided to you.

2. Drag `EOExportUI`, `EOExportUI.podspec`, and `EOLocalResources.bundle` from the demo into the `ios` folder of your project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45841ab760b14444bfef05f95cc362cd~tplv-goo7wpa0wc-image.image) </span>

3. Drag `EffectOneModule.h`, `EffectOneModule.m`, `RNEffectModule.h`, and `RNEffectModule.m` from the sample file into the directory containing the `AppDelegate` file in your project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ea8f316dbe143af98930d097297c8e7~tplv-goo7wpa0wc-image.image) </span>


The files are added.

<span id="9ff41b94"></span>
# Step 2: Integrate `EOLocalResources.bundle` into your iOS project

You can integrate `EOLocalResources.bundle` into your iOS project.

**To integrate** **`EOLocalResources.bundle`** ** into your iOS project:** 


1. Double\-click the `xxx.xcworkspace` file in your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the file does not exist, you can refer to the <a href="https://docs.byteplus.com/docs/video-editor-sdk/140-ios-react-native-faq">iOS React Native FAQ</a>.   </div>
   

2. Right\-click **AppDelegate.** 

3. Click **Add Files to "EffectOneSample"**  \> **iOS** \> **EOLocalResources.bundle**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dad7e8643e4c4cde861f226ac415b9e8~tplv-goo7wpa0wc-image.image) </span>

4. Select **Copy items if needed**.

5. Select **Create groups**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>EOLocalResources.bundle</code>file contains resource assets.   </div>
   

6. Click **Add**.


The `EOLocalResources.bundle` file is integrated into your iOS project.

<span id="f517e63d"></span>
# Step 3: Integrate other files into your iOS project

You can integrate other files into your iOS project.

**To integrate other files into your iOS project:** 


1. Double\-click the `xxx.xcworkspace` file in your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the file does not exist, you can refer to the <a href="https://docs.byteplus.com/docs/video-editor-sdk/140-ios-react-native-faq">iOS React Native FAQ</a>.   </div>
   

2. Right\-click **AppDelegate.** 

3. Click **Add Files to "EffectOneSample".** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dad7e8643e4c4cde861f226ac415b9e8~tplv-goo7wpa0wc-image.image) </span>

4. Select **EffectOneSample**.

5. Select the files: `EffectOneModule.h`, `EffectOneModule.m`, `RNEffectModule.h`, and `RNEffectModule.m`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/920c6d5ccc834f06a0d317f370416679~tplv-goo7wpa0wc-image.image) </span>

6. Select **Copy items if needed**.

7. Select **Create groups**.

8. Click **Add**.


The files are integrated into your project.

<span id="a79fb4f9"></span>
# Step 4: Configuring BundleID

Configure the Bundle ID in your Xcode project.

**To configure the bundleid:** 


1. Click your Xcode project.

2. Under the TARGETS section, click your project.

3. Click **Signing & Capabilities**.

4. In Bundle Identifier, change the BundleID in Xcode to: `com.volcengine.effectone.inhouse`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d177a45318bb4499a0892d535f367c34~tplv-goo7wpa0wc-image.image) </span>


The BundleID has been configured.

<span id="be9ace35"></span>
# Step 5: Configure permissions for camera, microphone, and photo library

Video Editor SDK requires access to the camera, microphone, and photo library. You need to enable these permissions in your project configuration, as shown below:

```JavaScript
// Whether to allow the app to access your media library
NSAppleMusicUsageDescription 
<string>This app allows access to your media library for browsing music and other media.string>
// Whether to allow the app to use your camera
<key>NSCameraUsageDescriptionkey>
<string>This app uses the camera to take photos and record videos.string>
// Whether to allow the app to use your microphone
<key>NSMicrophoneUsageDescriptionkey>
<string>This app uses the microphone to record audio with your videos.string>
// Whether to allow the app to save images to your phone
<key>NSPhotoLibraryAddUsageDescriptionkey>
<string>This app saves images to your photo library for editing and storage.string>
// Whether to allow the app to access your photo library
<key>NSPhotoLibraryUsageDescriptionkey>
<string>This app allows you to view and edit photos and videos in your photo library.string>
```


**To configure permissions for the camera, microphone, and photo library:** 


1. Click your Xcode project.

2. Under the TARGETS section, click your project.

3. Click **Info**.

4. Configure the permissions for the media library, camera, microphone, and photo library.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/709568ad5dfd461cba70e0fbb952d608~tplv-goo7wpa0wc-image.image) </span>


The permissions are configured.

<span id="8c81fc70"></span>
# Step 6: Modify the Podfile

Add dependencies to your Podfile by using the following:

```JavaScript
pod 'EOExportUI', :path => './' 
pod 'EffectOneKit', '1.2.0', :source => 'https://github.com/volcengine/volcengine-specs'
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23f39bf1e2424407941a1c86c2323321~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the file does not exist, you can refer to the <a href="https://docs.byteplus.com/docs/video-editor-sdk/140-ios-react-native-faq">iOS React Native FAQ</a>.</div>


<span id="1157dac1"></span>
# Step 7: Install Third\-Party Components

Navigate to your project's `ios` directory in the terminal and run the following command:

```Plain
pod install
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d2ed871094c4576ae2c87a0b1d78682~tplv-goo7wpa0wc-image.image) </span>

Once run, the RN integration is completed.
