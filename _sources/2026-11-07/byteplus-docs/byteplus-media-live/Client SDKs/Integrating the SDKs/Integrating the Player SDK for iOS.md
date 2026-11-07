---
title: "Integrating the Player SDK for iOS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios"
---

This topic introduces how to integrate the Player SDK for iOS.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This guide covers SDK versions 1.40.200 and later. If you have already integrated an older version of the SDK, you can refer to <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-ios-dynamic-library-upgrade-guide">iOS dynamic library upgrade guide</a> for instructions on upgrading or switching from static to dynamic libraries.</div>


<span id="2178b17a"></span>
## System requirements


* Physical devices running iOS 11.0 or later

* Xcode 14.1 or later


<span id="43e22af2"></span>
## Prerequisites

You have created an SDK application and obtained the SDK license. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).

<span id="d2f677b3"></span>
## Integrating the SDK

You can integrate the SDK through one of the following methods:


* Automatic integration (recommended): Use CocoaPods or Swift Package Manager (SPM) to download the SDK package automatically. For CocoaPods, you can choose to integrate dynamic or static libraries, while for SPM, you can only integrate dynamic libraries.

* Manual integration: [Contact your technical support](https://console.byteplus.com/workorder/create) for assistance if you want to integrate the SDK manually.


This section describes how to automatically integrate the SDK.


<Tabs>
<Tab zoneid="KsNKPADFuu" title="Use CocoaPod">
<TabTitle>Use CocoaPod</TabTitle>

<span id="e266c047"></span>
### Integrating dynamic libraries (recommended)

<span id="64362f11"></span>
#### Step 1: Installing CocoaPods

Install Ruby on your Mac and run the following command in Terminal to install CocoaPods.

```Ruby
sudo gem install cocoapods
```


<span id="5fb664bc"></span>
#### Step 2: Creating Podfile

Run the following command in your project directory to create a Podfile.

```Ruby
pod init
```


<span id="22dee6b4"></span>
#### Step 3: Adding dependencies

Add the following code to your Podfile.

```Ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull']
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>x.x.x.x-premium</code> with the specific SDK version. We recommend that you use the latest version. For more information about the version number, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes">Player SDK for iOS release notes</a>.</div>


* <div data-tips="true" data-tips-type="tip">To pull streams with the RTM protocol, use <code>'LivePull-RTS'</code> instead of <code>'LivePull'</code>: <code>pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull-RTS']</code>.</div>


* <div data-tips="true" data-tips-type="tip">Starting from version 1.51.300.2\-premium, to use the super\-resolution (SR) and video sharpening features, add <code>'LivePull-BMF'</code> in addition to <code>'LivePull'</code>: <code>pod 'TTSDKFramework', 'x.x.x.x-premium', :subspecs => ['LivePull', 'LivePull-BMF']</code>.</div>



<span id="627e080c"></span>
#### Step 4: Installing the SDK

Run the following command in Terminal to install the SDK dependencies specified in your Podfile.

```Plain
pod install
```


<span id="cd337301"></span>
### Integrating static libraries

To integrate static libraries, follow the same steps as for dynamic libraries, but use the pod name TTSDK instead of TTSDKFramework.

```Ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull']
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>x.x.x.x-premium</code> with the specific SDK version. We recommend that you use the latest version. For more information about the version number, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes">Player SDK for iOS release notes</a>.</div>


* <div data-tips="true" data-tips-type="tip">To pull streams with the RTM protocol, use <code>'LivePull-RTS'</code> instead of <code>'LivePull'</code>: <code>pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull-RTS']</code>.</div>


* <div data-tips="true" data-tips-type="tip">Starting from version 1.51.300.2\-premium, to use the super\-resolution (SR) and video sharpening features, add <code>'LivePull-BMF'</code> in addition to <code>'LivePull'</code>: <code>pod 'TTSDK', 'x.x.x.x-premium', :subspecs => ['LivePull', 'LivePull-BMF']</code>.</div>



</Tab>
<Tab zoneid="ren0l4v55S" title="Use SPM">
<TabTitle>Use SPM</TabTitle>

1. In your Xcode project, click the  **+**  button under the **Package Dependencies** tab.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b6519c733fb4d17a41f535fab1039da~tplv-goo7wpa0wc-image.image" width="2516px" />   </div>
   

2. In the dialog box that appears, enter `git@github.com:byteplus-sdk/TTSDK_BytePlus_SPM.git` in the upper\-right corner. Then, enter the version of the SDK you want to integrate and click **Add Package** to add the TTSDK dependency.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f2260bdeb5c41fea0aa4a023aaa4ccf~tplv-goo7wpa0wc-image.image" width="1872px" />   </div>
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you select <strong>Exact Version</strong> as the <strong>Dependency Rule</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only specify an SDK version that supports integration using SPM. For more information about the specific version, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/sdk-for-ios-release-notes">Player SDK for iOS release notes</a>.   </div>
   

3. Select the components you need and click **Add Package** to add them to your targets.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f922aa76e474e02b625c653262b3c3d~tplv-goo7wpa0wc-image.image" width="1312px" />   </div>
   

   You can select the following components for the BytePlus MediaLive SDK:

   * `TTSDK_LivePull`: Pull live streams using the FLV, HLS, or RTMP protocols.

   * `TTSDK_LivePull-RTS`: Pull live streams using the FLV, HLS, RTMP, or RTM protocols.


</Tab>
</Tabs>


<span id="bee4f6c1"></span>
## Adding the license file

Copy the license file to your project directory. You will need this file path for SDK initialization.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure the bundle ID and app ID associated with the license file are the same as those of your project. Otherwise, the license authentication will fail.</div>
