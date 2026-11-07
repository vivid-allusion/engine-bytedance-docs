---
title: "Install an earlier version of the iOS SDK"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_tls_sdk_for_ios"
---

Before performing various TLS operations using the SDK, you need to install the SDK. This article describes how to install the iOS SDK.

## Development environment requirements

Ensure that your current development environment meets the following requirements.

|Software |Notice |
|---|---|
|Xcode |Version 12.0 or later. |
|Other environments |iOS development environment installed. For more information, see [Apple Developer](https://developer.apple.com/). |

## Integrate the iOS SDK

You can choose any of the following methods to install the TLS iOS SDK.

### Directly import the framework

1. Generate the TLS iOS SDK framework.

   On macOS, directly use the source code project obtained from [GitHub](https://github.com/volcengine/ve-tls-ios-sdk), select the scheme VeTLSiOSSDK, and then generate `VeTLSiOSSDK.framework`.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_54bc74d1183388145b855876f0a47ed7.png)

2. In Xcode, drag the framework into the corresponding target.

   For detailed instructions on importing the framework, refer to the [Apple official documentation](https://help.apple.com/xcode/mac/current/#/dev51a648b07).

3. In the pop\-up dialog box, select **Copy items if needed**.

4. In the project's **Build Setting**, add "\-ObjC" to Other Linker Flags.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8101ac5e821233dfb7e5a173b50e6265.png)

5. Import the header files into your project.

   Refer to the following command to import the header files into your local project.

   ```objectivec
   #import <VeTLSiOSSDK/VeTLSiOSSDK.h>
   ```

### Manually integrate the SDK

You can also manually integrate the SDK by copying the TLS iOS SDK source code.

1. Obtain the latest version of the TLS iOS SDK source code project from Github.

2. Extract the SDK package.

3. Copy the files under the `VeTLSiOSSDK` path to your local project directory.

## Use the TLS iOS SDK in Swift

The TLS iOS SDK is written in Objective\-C and does not currently provide a native Swift version of the SDK.

If you are a Swift user, you can use the Objective\-C version of the SDK in Swift projects through mixed\-language coding; that is, use the TLS iOS SDK in the same way as other Objective\-C source code in Swift. For example, refer to the [Directly import the framework](https://docs.byteplus.com/en/docs/tls/install_tls_sdk_for_ios#.55u05o6l5byV5YWlLWZyYW1ld29yaw==) section to import the TLS iOS SDK into your Swift project.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c52f1442585c7c06b4f20dd5de2f73ff.png)
