---
title: "iOS Upload SDK: Quickstart"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-upload-sdk"
---

To add powerful video upload capabilities to your iOS application, you must first integrate the SDK. This guide provides step\-by\-step instructions for integrating the iOS Upload SDK into your project using CocoaPods as either a dynamic or static library.

<span id="8cd249ac"></span>
## Prerequisites


* Xcode 14.0 or higher. We recommend using the latest version.

* A device running iOS 11.0 or higher.


<span id="f1e6264e"></span>
## Integrate the SDK

Integrate the SDK into your project using [CocoaPods](https://guides.cocoapods.org/using/getting-started.html#getting-started) as either a static or dynamic library. You need to add the required library to your project's `Podfile` and run `pod install`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get the latest version number, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-ios-upload-sdk-changelog">iOS Upload SDK: Release notes</a>.</div>


<span id="3a9bf234"></span>
#### Add the dynamic library (Recommended)

The code to add the dynamic library is as follows:

```Ruby
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'

platform :ios, '11.0'

target 'YourTarget'
    # Add the dynamic library TTSDKFramework and specify subspecs as Uploader
    # Replace x.x.x.x with the version number
    pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['Uploader']
end
```


<span id="e12b94d2"></span>
#### Add the static library

The code to add the static library is as follows:

```Ruby
source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'

platform :ios, '11.0'

target 'YourTarget' do
  # Add the static library TTSDK and specify subspecs as Uploader
  # Replace x.x.x.x with the version number
  pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['Uploader']
 
end
```


<span id="b4f02e0b"></span>
## Import the header file

Import the header file based on how you have integrated the SDK:


* If you have added the dynamic library, use the following code:

   ```objectivec
   #import <TTSDKFramework/TTSDKFramework.h>
   ```
   

* If you have added the static library, use the following code:

   ```objectivec
   #import <TTSDK/TTSDKManager.h>
   #import <TTSDK/BDFileUploaderHeader.h>
   ```
