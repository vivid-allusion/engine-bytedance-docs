---
title: "Quick Integration Guide - iOS - Magic Template"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-quick-integration-guide-ios-magic-template"
---

<span id="iOS project settings"></span>
## **iOS project settings**

<span id="System requirements"></span>
### **System requirements**

The SDK supports iOS 9.0 and later versions.

<span id="Development environment"></span>
### **Development environment**


* Xcode 9 or later

* OS X 10.10 or later


<span id="Add the SDK to a project"></span>
## **Add the SDK to a project**

You can add the Magic Template SDK to a project in the following two ways:


* Using the template editing APIs: This SDK provides only the operation objects and relevant APIs necessary for template editing, and does not include the user interfaces (UIs). You can develop the UIs based on your business requirements. You can also design the UI style as needed.

* Using the Magic Template UI SDK: The SDK provides default UIs to help you launch the app quickly.


For example, to integrate the Magic Template SDK with default UIs, see *Quick Integration of the Magic Template UI SDK*.

<span id="Integrate the Magic Template SDK"></span>
### **Integrate the Magic Template SDK**

<span id="Integrate CocoaPods"></span>
#### **Integrate CocoaPods**

1、If the project has been using CocoaPods, go to Step 3.

2、In the root directory of the project, run **pod init && pod install** to get the **Podfile** file.

3、Open the **Podfile** file and add the following dependencies:

```Ruby
# Comment off use_frameworks! 

 # use_frameworks!

 
 pod 'CutSameIF', '3.3.182.4', :source => 'https://github.com/volcengine/volcengine-specs.git'

 pod 'TTVideoEditor', '9.1.2.17', :source => 'https://github.com/volcengine/volcengine-specs.git'

 pod 'TTNetworkManager', '5.0.29.23', :source => 'https://github.com/volcengine/volcengine-specs.git'

 pod 'KVOController', '~> 1.2.0'
```


4、Run **pod install**. Upon completion, open the .xcworkspace project.

5、Develop the UIs as needed.

<span id="Quick integration of the Magic Template UI SDK"></span>
### **Quick integration of the Magic Template UI SDK**

<span id="Integrate CocoaPods"></span>
#### **Integrate CocoaPods**

1、If the project has been using CocoaPods, go to Step 3.

2、In the root directory of the project, run **pod init && pod install** to get the **Podfile** file.

3、Open the **Podfile** file and add the following dependencies:

```Ruby
 # Comment off use_frameworks! 

 # use_frameworks!

  
 pod 'CutSameIF', '3.3.182.4', :source => 'https://github.com/volcengine/volcengine-specs.git'

 pod 'CutSameUIIF', '3.3.182.2', :source  => 'https://github.com/volcengine/volcengine-specs.git'

 pod 'TTVideoEditor', '9.1.2.17', :source => 'https://github.com/volcengine/volcengine-specs.git'

 pod 'TTNetworkManager', '5.0.29.23', :source  => 'https://github.com/volcengine/volcengine-specs.git'

 pod 'KVOController', '~> 1.2.0'
```


4、Run **pod install**, and then open the  **.xcworkspace** project.

<span id="Configure app permissions"></span>
#### **Configure app permissions**

```XML
<key>NSPhotoLibraryAddUsageDescription</key>

<string>Allows you to set the avatar by selecting a photo, upload and publish videos, and save videos locally.</string>

<key>NSPhotoLibraryUsageDescription</key>

<string>The Magic Template component needs to access your album to edit videos.</string>
```


<span id="Note"></span>
## **Note**

The Magic Template SDK supports only on\-device debugging.
