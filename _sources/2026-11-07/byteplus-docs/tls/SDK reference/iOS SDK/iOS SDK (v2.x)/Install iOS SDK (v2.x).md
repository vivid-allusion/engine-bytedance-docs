---
title: "Install iOS SDK (v2.x)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Install-iOS-SDK-v2-x"
---

Before using the BytePlus iOS SDK to call TLS API endpoints and implement related features, you must first install the iOS SDK. This article describes the steps for installing the iOS SDK.

## Prepare the development environment

|Environment |Notice |
|---|---|
|Xcode |Version 14.3.1 and later. |
|Swift |Version 5.8 and later. |
|Operating system |* iOS: Version 13.0 and later.<br><br>* Intel: macOS 10.15 and later.<br><br>* Apple Silicon: macOS 11.0 and later.<br><br><br>For the complete platform declaration and verification scope, see [Compatibility](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/reference/compatibility.md). |

## Install the SDK

The ve\-tls\-ios\-sdk can be installed using the following methods:

**Swift Package Manager**

* Xcode configuration:

   1. Select **File \> Add Package Dependencies**.

   2. Enter `https://github.com/volcengine/ve-tls-ios-sdk.git`.

   3. Select `2.0.1` or a higher compatible version.

   4. Add the `VolcengineTLSProducer` product to the target where logging is required.

* Package.swift configuration:

   ```Swift
   dependencies: [
       .package(
           url: "https://github.com/volcengine/ve-tls-ios-sdk.git",
           from: "2.0.1"
       )
   ],
   targets: [
       .target(
           name: "YourTarget",
           dependencies: [
               .product(
                   name: "VolcengineTLSProducer",
                   package: "ve-tls-ios-sdk"
               )
           ]
       )
   ]
   ```

**CocoaPods**

1. Configure dependencies in `Podfile`.

   * Install from CocoaPods source

      * iOS

         ```Ruby
         # iOS
         platform :ios, '13.0'
         pod 'VolcengineTLSProducer', '~> 2.0.1'
         ```

      * macOS

         ```Ruby
         # macOS
         platform :osx, '10.15'
         pod 'VolcengineTLSProducer', '~> 2.0.1'
         ```

   * Install from Git tag (if a specific version is required)

      * iOS

         ```Ruby
         platform :ios, '13.0'
         pod 'VolcengineTLSProducer',
             :git => 'https://github.com/volcengine/ve-tls-ios-sdk.git',
             :tag => 'v2.0.1'
         ```

      * macOS

         ```Ruby
         platform :osx, '10.15'
         pod 'VolcengineTLSProducer',
             :git => 'https://github.com/volcengine/ve-tls-ios-sdk.git',
             :tag => 'v2.0.1'
         ```

2. Run `pod install`.

3. Open the project using the generated `.xcworkspace`.

## Installation verification

Add the following content to the target source code to compile the target:

```Swift
import VolcengineTLSProducer

let metadata = ProducerMetadata()
```

If `No such module 'VolcengineTLSProducer'` appears:

1. Verify that the product or Pod has been added to the current Target, not just to the project.

2. Open the CocoaPods project using `.xcworkspace`. Opening `.xcodeproj` alone will not load Pod dependencies.

3. Check whether the Deployment target meets the minimum version requirement.

4. Clear DerivedData and re\-resolve dependencies.

> **tip**

* > The public import entry for the business Target is `VolcengineTLSProducer`; other modules in the package are not part of the public API.

* > For the import method and complete usage steps for Objective\-C projects, see [Objective\-C integration](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/getting-started/objective-c.md).
