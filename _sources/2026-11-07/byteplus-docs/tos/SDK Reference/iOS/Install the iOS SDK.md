---
title: "Install the iOS SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-ios-sdk"
---

This article presents the installation procedure for the TOS iOS SDK.

<span id=".546v5aKD6KaB5rGC"></span>
## Environmental Requirements

iOS system version: iOS 8.0 or later.

<span id=".c2RrLeS4i-i9veWcsOWdgA=="></span>
## SDK Download Link

The source code address for the iOS SDK can be found at [ iOS SDK](https://github.com/volcengine/ve-tos-ios-sdk).

<span id=".5a6J6KOF"></span>
## Installation

You may choose any of the following methods to install the iOS SDK.

<span id=".55u05o6l5byV5YWlLWZyYW1ld29yaw=="></span>
### Direct Import of the Framework

You need to compile VeTOSiOSSDK.framework according to the platform type, and then add VeTOSiOSSDK.framework to your Xcode project.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Drag the framework package directly into the Xcode project, make sure to select <strong>Copy items if needed</strong>, and then import the header file to begin using it.</div>


```objectivec
#import <VeTOSiOSSDK/VeTOSiOSSDK.h>
```


<span id=".5L2_55SoLXRvcy1pb3Mtc2RrLea6kOeggQ=="></span>
### Using the TOS iOS SDK source code

Directly incorporate the source code of the TOS iOS SDK into the project.
