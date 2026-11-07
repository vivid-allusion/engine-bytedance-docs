---
title: "iOS 动态库升级指南"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ios-dynamic-library-upgrade-guide-zh-CN"
---

要将 iOS 拉流 SDK 的动态库升级到 1.40.200 或更高版本，可按照以下说明操作。本主题涵盖从旧版动态库升级以及从静态库切换到动态库的操作。

<span id="fd6edce5"></span>
## 新版本的优势

与 1.39.300 及更早版本相比，新版本动态库具有以下优势：


* SDK 包体积更小。

* 依赖项与静态库保持一致，便于动态库与静态库之间切换。

* 头文件的导入方式与标准系统动态库保持一致。


<span id="a71d1f66"></span>
## 从旧版动态库升级

如果已集成 1.39.300 或更早版本的动态库，可按照以下步骤升级到 1.40.200 及更高版本。


1. 保持原有的 CocoaPods 集成方式。如需减小 SDK 包体积，可将 subspec 名称更改为 [Integrating the SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) 中列出的名称。例如，集成拉流能力时，可将 `subspecs => ["BasePull"]` 更改为 `subspecs => ["LivePull"]`。

2. 为避免升级后头文件导入报错，可通过以下两种方式之一修改项目代码。

   * 方式一：修改头文件的导入方式。

      * 如果通过 `#import <xxx/xxx.h>` 导入头文件，请全部替换为 `#import <TTSDKFramework/xxx.h>`。

      * 如果导入子模块头文件，如 `#import <TTSDKPUFramework/TTSDKPUFramework.h`，请替换为 `#import <TTSDKFramework/TTSDKFramework.h>`。

   * 方式二：在 Podfile 中添加环境变量 `ENV['TTSDK_FRAMEWORK_MODULE_NAME'] = 'PREVIOUS_FRAMEWORK'`。将 `PREVIOUS_FRAMEWORK` 替换为现有框架的名称。


<span id="4b65c91c"></span>
## 从静态库切换到动态库

如果已集成静态库，可按照以下步骤切换到 1.40.200 及更高版本的动态库：


1. 修改 CocoaPods 集成方式，将 pod 名称从 `TTSDK` 更改为 `TTSDKFramework`。例如，将 `pod 'TTSDK', :subspecs => ['LivePull-RTS']` 更改为 `pod 'TTSDKFramework', :subspecs => ['LivePull-RTS']`。

2. 修改头文件的导入方式。

   * 如果通过 `#import "xxx.h"` 导入头文件，无需修改代码。

   * 如果通过 `#import <TTSDK/xxx.h>` 导入头文件，可通过以下两种方式之一修改项目代码：

      * 方式一（推荐）：在 Podfile 中添加环境变量设置 `ENV['TTSDK_FRAMEWORK_MODULE_NAME'] = 'TTSDK'`。

      * 方式二：将所有 `#import <TTSDK/xxx.h>` 替换为 `#import <TTSDKFramework/xxx.h>`。
