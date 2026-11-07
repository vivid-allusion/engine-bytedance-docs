---
title: "在 iOS 上实现赛事直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-ios-zh-CN"
---

本指南介绍如何使用 BytePlus MediaLive SDK 在 iOS 上实现赛事直播观看体验。您将学习如何初始化直播播放器、通过低延迟协议拉流、切换机位和画质，以及在播放之上叠加互动功能。

<span id="lsi-env"></span>
## 环境要求


* Xcode 16 或更高版本。我们建议使用最新版本的 Xcode 以获得最佳性能。

* 一台运行 iOS 13 或更高版本的真机设备。


<span id="lsi-prereq"></span>
## 前提条件


* 一个已激活 [BytePlus MediaLive](https://console.byteplus.com/live) 的有效 [BytePlus 账户](http://console.byteplus.com/)。

* 完成 [直播的基础设置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)：

   * 获取 BytePlus MediaLive SDK 许可证。

      * 有关如何获取许可证的详细说明，请参见 [访问您的 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

      * 要详细了解如何根据您的需求选择合适的许可证类型，请参考 [SDK 简介](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="lsi-version"></span>
## 版本要求


* 要使用 **直播拉流** 功能，您必须使用 BytePlus MediaLive SDK。请记得在 [客户端 SDK 组件](https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination) 页面选择正确的 SDK。


<span id="lsi-integrate"></span>
## 集成 SDK

将 `TTSDKFramework` 的 pull subspec 添加到您的 `Podfile` 中：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要获取最新的版本号，请参见 <a href="https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination">客户端 SDK 组件</a>。</div>


```Ruby
$TT_SDK_VERSION = '1.50.200.2-premium'
pod 'TTSDKFramework', $TT_SDK_VERSION, :subspecs => ['LivePull-RTS']
```


然后运行 `pod install`。

<span id="lsi-impl"></span>
## 实现

<span id="lsi-player"></span>
### 步骤 1: 创建播放器

使用 BytePlus MediaLive SDK 创建一个直播播放器实例，并设置其 delegate 以接收播放回调。

```Swift
let player = TVLManager(type: VeLivePlayerTypeOwn)
```


<span id="lsi-pull"></span>
### 步骤 2: 拉流

为选定的机位和画质配置拉流 URL，然后开始播放。要使用低延迟 FLV，请在播放前启用低延迟 FLV 选项。

<span id="lsi-switch"></span>
### 步骤 3: 切换机位和画质

当观众选择不同的机位或画质档位时，将播放器重新绑定到相应的拉流 URL。当同一源有多个协议或画质档位可用时，请选择与观众选择相匹配的 URL。

<span id="lsi-interact"></span>
### 步骤 4: 添加互动功能

在播放视图之上叠加互动 UI（礼物、评论和弹幕、点赞），并提供用于全屏观看的横屏模式。

<span id="lsi-code"></span>
## 示例代码

请参考 Demo 源代码，将此功能集成到您的应用中。


* iOS：[LiveSportStreaming](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/LiveSportStreaming)
