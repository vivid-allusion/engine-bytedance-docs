---
title: "集成 iOS 观播 SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN"
---

要在你的 iOS 应用中集成直播功能，例如观看直播流、发送评论以及与主播互动，可以集成 iOS 观播 SDK。本指南提供了全面的分步说明，涵盖从初始设置、依赖管理到加入和离开直播间的所有内容，确保集成过程顺畅。

## 前提条件

* 运行 iOS 12.0 及以上版本的真机或模拟器。如果使用 Swift Package Manager 集成 SDK，则需要运行 iOS 13.0 及以上版本的真机或模拟器。

   > **说明**

   * > 如果你使用 Apple Silicon Mac，则需要 Rosetta 模拟器。

   * > 该模拟器仅用于界面调试，不保证音频、视频和画中画（PiP）等功能的正常运行。为避免出现屏幕花屏或黑边等问题，建议使用实体设备。

* Xcode。建议使用最新版本。

* 若通过 CocoaPods 集成，请使用 CocoaPods 1.11.0 或以上版本。更多信息，请参见 [CocoaPods 入门指南](https://guides.cocoapods.org/using/getting-started.html#getting-started)。若使用 Swift Package Manager 集成，请使用 swift\-tools\-version 5.9 或以上版本。

* CPU 架构：arm64 或 x86_64。

* 联系 BytePlus Live 技术支持，获取直播许可证文件和点播（VOD）许可证文件、用于申请许可证的应用名称，以及申请成功后返回的应用 ID。

## 集成步骤

### Step 1: 添加依赖

你可以通过 **CocoaPods（方式一）**  或 **Swift Package Manager（方式二）**  集成 SDK。

**方式一：通过 CocoaPods 添加依赖**

1. 打开项目的`Podfile` 文件以添加依赖。

   > **说明**

   > 如果你的项目尚未使用 CocoaPods，请在项目根目录运行 `pod init && pod install` 命令以生成 `Podfile` 文件。

   ```Ruby
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   
   # Your app target name
   target 'XXXX' do
     # 从 1.33.0 版本开始，你可以 使用 ViewerWithoutRTC 作为 podspec 来优化 SDK 包体积。这样可获得不包含超低延时直播功能的 SDK 包。
     pod 'BPLive', '1.66.1'
   end  
   ```

2. 打开终端窗口，运行 `cd` 命令进入项目目录。运行 `pod install` 命令安装依赖。

3. （可选）使用 TTSDK 的静态库版本：

   默认情况下，使用的是 TTSDK 的动态库版本。如需使用 TTSDK 的静态库版本，在添加依赖时于版本号后追加 `-static-ttsdk`。更多信息，请参见 `Podfile` 文件中的前述配置。

   ```Ruby
   pod 'BPLive', '1.66.1-static-ttsdk'
   ```

**方式二：通过 Swift Package Manager (SPM) 添加依赖**

你可以通过 `Package.swift` 或在 Xcode 页面两种方式集成 SDK。

**仓库地址**：

SDK：`https://github.com/byteplus-sdk/BPLive_SPM`

##### 方式 A：在 Package.swift 中集成

在 `Package.swift` 中添加 `BPLive_SPM` 依赖，并在需要的 target 中引入对应 Library。以下为观播 SDK 的集成示例：

```Swift
// swift-tools-version: 5.9
import PackageDescription

let package = Package(
    name: "MyApp",
    platforms: [.iOS(.v13)],
    products: [
        .library(name: "MyApp", targets: ["MyApp"]),
    ],
    dependencies: [
        // 请替换为目标版本号
        .package(url: "https://github.com/byteplus-sdk/BPLive_SPM.git", exact: "1.66.4")
    ],
    targets: [
        .target(
            name: "MyApp",
            dependencies: [
                // 基础库和通用组件库
                .product(name: "BPLiveBaseLibrary", package: "BPLive_SPM"),
                .product(name: "BPLiveCommonLibrary", package: "BPLive_SPM"),
                // 观播 SDK。你可以将 BPLiveViewerLibrary 替换为 BPLiveViewerWithoutRTCLibrary，以优化 SDK 包体积。BPLiveViewerWithoutRTCLibrary 不包含超低延时直播功能。
                .product(name: "BPLiveViewerLibrary", package: "BPLive_SPM")
            ]
        ),
    ]
)
```

##### 方式 B：在 Xcode 中集成

1. 打开 Xcode，选择菜单 **File** \> **Add Package Dependencies…** 。

2. 输入仓库地址 `https://github.com/byteplus-sdk/BPLive_SPM`。

3. 在版本规则中选择带标签的目标版本（如 **Exact Version: 1.66.4**）。

4. 在 Library 勾选列表中，勾选观播 SDK 相关的 Library 并关联到对应 target：

   * BPLiveBaseLibrary：基础库（必需）

   * BPLiveCommonLibrary：通用组件库（必需）

   * BPLiveViewerLibrary：观播库

   * BPLiveViewerWithoutRTCLibrary：不包含超低延时直播功能的观播库

### Step 2: 配置环境

在 Xcode 的应用 target 下，完成以下操作：

1. 打开 `info.plist` 文件，添加参数 `SSAppID`，并将该参数的值设置为许可证申请通过后获得的应用 ID。

2. 在 `info.plist` 文件中，通过以下任一方式添加权限：

   * 点击  **+** ，添加 **Privacy \- Photo Library Additions Usage Description** 和 **Privacy \- Calendars Usage Description** 键。对于每个键，将 **Type** 设置为 **String**，**Value** 设置为你希望在系统授权弹窗中显示的提示信息。

   * 以源码模式打开 `info.plist` 文件，添加以下键值对和字符串。你可以自定义字符串的值，用作系统授权弹窗中显示的提示信息。

      ```Plain
      <!-- Write access to photo library -->
      <key>NSPhotoLibraryAddUsageDescription</key> 
      <string>The app needs your permission to write to your photo library for saving images to the photo library</string>
      <!-- Write access to calendar -->
      <key>NSCalendarsUsageDescription</key>
      <string>Used to remind viewers before live stream starts</string>
      ```

3. （可选）如需应用在后台运行时继续播放音频，或需要使用画中画（PiP）功能，请完成以下操作：

   1. 在 **Signing & Capabilities** 标签下点击  **+ Capability**，并双击添加 **Background Modes**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/147f155c322d4f6cba5c2f26c813f33b~tplv-goo7wpa0wc-image.image)

   2. 在 **Background Modes** 部分，勾选 **Audio, AirPlay, and Picture in Picture** 复选框。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eefa3e63dd374db686c0b232547c944b~tplv-goo7wpa0wc-image.image)

4. （可选）如果你的项目使用了 Bitcode，则需要关闭 Bitcode。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/991f4357e3bb47579b6256340415e73d~tplv-goo7wpa0wc-image.image)

   1. 点击 **Build Settings** 标签。

   2. 在 **Build Options** 部分，将 **Enable Bitcode** 设置为 **No**。

5. 配置全屏播放直播、预告或回放时支持的屏幕方向。

   1. 点击 **General** 标签。

   2. 在 **Deployment Info** 部分，为 **iPhone Orientation** 和 **iPad Orientation** 勾选 **Portrait** 和 **Landscape Right** 复选框。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab42c8820c0f4eee99fe655eb65c2ff6~tplv-goo7wpa0wc-image.image)

   > **说明**

   * > 要让观众在全屏模式下根据设备方向自动左右旋转屏幕，需满足以下条件：

      * > 观众设备的竖屏方向锁已关闭。关于如何关闭竖屏方向锁的操作说明，请参见[官方 Apple 文档](https://support.apple.com/en-us/118226)。

      * > 在**Deployment Info**部分，需同时勾选**Landscape Left**和**Landscape Right**复选框。

   * > 为防止观众点击全屏按钮时全屏动画出现显示异常，请确保勾选**Landscape Right**复选框。

   * > 如需禁用全屏模式，可通过以下示例代码在播放器中隐藏全屏按钮。禁用全屏模式后，只能在**Deployment Info**部分选择**Portrait**复选框。

   > `[BDLLiveEngine sharedInstance].liveRoomConfiguration.playerConfig.common.enterFullScreenEnable = NO;`

### Step 3: 导入许可证

将直播许可证文件和点播许可证文件添加到 Xcode 的应用 target 中。选择 **Copy items if needed**，然后点击 **Finish**。

### Step 4: 初始化 BPLive

在 Xcode 的应用目标中，打开 `AppDelegate.m` 文件以初始化 BPLive：

```objectivec
#import <BPLive/BPLive.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self initBPLive];
    return YES;
}

- (void)initBPLive {
    BDLiveAuthInfo *authInfo = [[BDLiveAuthInfo alloc] init];
    authInfo.bizType = BDLiveBizTypeViewer; // If you integrate both the Live Streaming SDK and Viewer SDK, replace BDLiveBizTypeViewer with BDLiveBizTypeViewer | BDLiveBizTypeLiveStreaming.
    authInfo.appId = @"APP_ID"; // Replace APP_ID with the app ID returned after the successful license application.请联系 BytePlus Live 技术支持获取应用 ID。
    authInfo.appName = @"APP_NAME"; // Replace APP_NAME with the app name used to apply for the license.请联系 BytePlus Live 技术支持获取应用名称。
    authInfo.channel = @"CHANNEL_NAME"; // Replace CHANNEL_NAME with the name of the channel through which to download the app.默认值为 App Store。
    
    authInfo.vodLicensePath = [[NSBundle mainBundle] pathForResource:@"VOD_LICENSE_NAME" ofType:@"lic"]; // Replace VOD_LICENSE_NAME with the name of the VOD license file.
    authInfo.liveLicensePath = [[NSBundle mainBundle] pathForResource:@"LIVE_LICENSE_NAME" ofType:@"lic"];// Replace LIVE_LICENSE_NAME with the name of the live streaming license file.
    // Initialize the SDK.你必须在连接网络后调用此方法。你可以通过完成回调获取授权结果。
    [[BDLiveManager sharedInstance] startWithAuthInfo:authInfo complete:^(BOOL allSuccess, NSString * _Nullable warningInfo, NSArray<NSError *> * _Nullable errors) {
        NSLog(@"BDLive 【allSuccess】 %d \n 【warningInfo】: %@ 【errors】:\n\n%@", allSuccess, warningInfo, errors);
    }];
}
```

相关方法：[startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-startwithauthinfo-complete)

### Step 5: 创建加入直播间所需的Activity

在 Xcode 的应用目标中，打开定义如何加入和离开直播间的文件，并添加如下代码。

> **说明**

> 你可以通过调用[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN)或[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取直播间的活动 ID，通过调用[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)获取加入直播间所需的授权 token。

```objectivec
#import <BPLive/BPLive.h>

BDLActivity *activity = [[BDLActivity alloc] init];
activity.activityId = @(ACTIVITY_ID); // 将ACTIVITY_ID替换为直播间的活动 ID。
activity.token = @"TOKEN"; // 将TOKEN替换为加入直播间所需的授权 token。
activity.authMode = BDLActivityAuthModePublic; // 直播间的鉴权模式。此处以公开模式为例。观众无需登录直播间即可观看在线流、查看评论及进行其他操作。
activity.isPortrait = YES; // Whether the live room is in portrait mode.此处以竖屏模式为例。
```

### Step 6: 加入和离开直播间

在 Xcode 的应用目标中，打开定义如何加入和离开直播间的文件，然后添加相关方法。

以下示例代码展示了加入和离开完整直播间的方法。

```objectivec
...
// Join the live room.
[[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity success:^{
    // Join the live room successfully
} failure:^(NSError * _Nonnull error) {
    // Failed to join the live room.
}];
// Leave the live room.
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}
```

## 优化 SDK 包体积

从 1.33.0 版本开始，你可以通过如下方式在 `Podfile` 文件中添加依赖项来 优化 SDK 包体积。更多信息，请参见 [Step 1: 添加依赖](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b1a1a0ed)。

```Ruby
  # The optimized SDK package excludes the feature of ultra-low latency live streaming.
  pod 'BPLive', '1.66.1-static-ttsdk', :subspecs => [
    'ViewerWithoutRTC', 
  ]
```

## 包体积

此处的包体积指：

* 集成 SDK 后，压缩 IPA 文件体积的增加量。该数值通过新文件体积减去原文件体积计算得出。

* 集成 SDK 后，未压缩 IPA 文件体积的增加量。该数值通过新文件体积减去原文件体积计算得出。

压缩 IPA 文件体积代表应用的下载体积，未压缩 IPA 文件体积对应设备上安装应用的体积。

设备上的实际未压缩 IPA 文件体积比下表所列数值更小，因为安装时只保留适用于当前设备的资源。

以下数据基于应用仅支持 arm64 CPU 架构。

|版本 |类型 |TTSDK 库 |增量压缩 IPA 文件大小 |增量未压缩 IPA 文件大小 |依赖项 |
|---|---|---|---|---|---|
|1.58.0 \- 1.66.1（以 1.66.1 为依赖项示例） |观播 SDK |动态库 |约 47 MB |约 94.8 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1'```<br> |
|||静态库 |约 43.7 MB |约 79.1 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1-static-ttsdk'```<br> |
||优化包体大小的观播 SDK |动态库 |约 30.8 MB |约 64.7 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |
|||静态库 |约 27.5 MB |约 49 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1-static-ttsdk', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |

优化包体积的观播 SDK 不包含超低延时直播功能。关于添加依赖项的更多信息，请参见 [Step 1: 添加依赖](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN#b1a1a0ed)。

## FAQ

[iOS 观播 SDK 常见问题](https://docs.byteplus.com/docs/byteplus-livesaas/docs-faqs-about-ios-viewer-sdk-zh-CN)
