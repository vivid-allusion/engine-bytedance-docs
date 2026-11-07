---
title: "iOS dynamic library upgrade guide"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ios-dynamic-library-upgrade-guide"
---

To upgrade to version 1.40.200 or later of the dynamic libraries for the Player SDK for iOS, you can follow these instructions. This topic covers both upgrading from an older dynamic library version and switching from static to dynamic libraries.

<span id="fd6edce5"></span>
## Benefits of the new version

Compared to 1.39.300 and earlier versions, the new version of the dynamic libraries has the following advantages:


* Smaller SDK package size.

* Dependencies are aligned with static libraries for easier switching between dynamic/static libraries.

* The header file import process is now consistent with that of standard system dynamic libraries.


<span id="a71d1f66"></span>
## Upgrading from older versions of dynamic libraries

If you have integrated the dynamic libraries version 1.39.300 or earlier, you can upgrade to version 1.40.200 and later by following these steps.


1. Keep the original CocoaPods integration method. If you need to reduce the SDK package size, you can change subspec names to those listed in [Integrating the SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios). For example, when integrating the pull streaming capability, you can change `subspecs => ["BasePull"]` to `subspecs => ["LivePull"]`.

2. To avoid header file import errors after the upgrade, you can modify the project code in one of the following two ways.

   * Method 1: Modify the way you import header files.

      * If you import by using `#import <xxx/xxx.h>`, replace all instances with `#import <TTSDKFramework/xxx.h>`.

      * If you import the header file of a submodule, such as `#import <TTSDKPUFramework/TTSDKPUFramework.h`, replace it with `#import <TTSDKFramework/TTSDKFramework.h>`.

   * Method 2: Add the environment variable `ENV['TTSDK_FRAMEWORK_MODULE_NAME'] = 'PREVIOUS_FRAMEWORK'` in your Podfile. Replace `PREVIOUS_FRAMEWORK` with the name of your existing framework.


<span id="4b65c91c"></span>
## Switching from static to dynamic libraries

If you have integrated the static libraries, you can switch to dynamic libraries version 1.40.200 and later by following these steps:


1. Modify the CocoaPods integration method by changing the pod name from `TTSDK` to `TTSDKFramework`. For example, change `pod 'TTSDK', :subspecs => ['LivePull-RTS']` to `pod 'TTSDKFramework', :subspecs => ['LivePull-RTS']`.

2. Modify the way you import header files.

   * If you import by using `#import "xxx.h"`, no code modification is needed.

   * If you import by using `#import <TTSDK/xxx.h>`, you can modify the project code in one of the following two ways:

      * Method 1 (recommended): Add the environment variable settings `ENV['TTSDK_FRAMEWORK_MODULE_NAME'] = 'TTSDK'` in the Podfile.

      * Method 2: Replace all instances of `#import <TTSDK/xxx.h>` with `#import <TTSDKFramework/xxx.h>`.
