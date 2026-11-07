---
title: "Android 与 iOS"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-release-notes-zh-CN"
---

本文档总结了 VideoOne 每个版本的新功能、改进及已修复的缺陷。请参考这些说明，及时了解最新产品更新。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">为确保集成顺畅并避免与其他 BytePlus SDK 产生依赖冲突，请参考每个版本的组件详细列表：<a href="https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN">客户端 SDK 组件</a>。</div>


<span id="a5f5b012"></span>
## 5.5.0

发布日期：2026/07/13（iOS），2026/07/16（Android）


|**主要更新** |**具体内容** |**说明** |
|---|---|---|
|新增场景并设有独立入口 |赛事直播 |新增基于 BytePlus MediaLive 构建的赛事直播解决方案，支持多机位视角切换、自适应码率（ABR）播放、低延迟直播协议以及互动观看（礼物、评论、点赞）。[了解更多](https://docs.byteplus.com/docs/byteplus-vos/docs-live-sport-streaming-solution-overview-zh-CN) |
|新功能 |投屏 |新增视频播放投屏功能。在 Android 上，演示通过 Chromecast（Google Cast）投屏；在 iOS 上，通过 AirPlay 投屏。 |
|优化 |SDK 版本升级 |基础媒体 SDK 版本已升级至最新，以提升性能与可靠性。请参考[客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN)页面，以获取各媒体 SDK 的最新版本。 |


<span id="f50c8ec1"></span>
## 5.4.0

发布日期：2026/03/05（iOS），2026/03/26（Android）


|**主要更新** |**具体内容** |**说明** |
|---|---|---|
|新功能 |客户端广告插入（CSAI） |为短剧解决方案新增客户端广告插入（CSAI）能力，实现客户端无缝广告集成与变现。详见[CSAI 集成概述](https://docs.byteplus.com/docs/byteplus-vos/csai-integration-overview-zh-CN)。 |
|（仅限 Android） |新增 ABR 能力 |VideoOne 现已支持视频播放的自适应码率流（ABR）。您可在所有 VoD 演示的新设置页面启用此功能，自动根据网络状况调整视频质量。 |
||SDK 版本升级 |基础媒体 SDK 版本已升级至最新，以提升性能与可靠性。 |
||移除 KTV 演示 |本版本已移除在线 KTV 场景。 |
||缺陷修复 |修复了若干已知问题，提升应用稳定性。 |


<span id="48e1756b"></span>
## 5.3.0

发布日期：2026/01/27

本次发布仅包含 **iOS** 演示应用的更新。您可在我们的 [GitHub repository](https://github.com/byteplus-sdk/VideoOneSolutions/commit/bf1667ab02df5bc041f9431919de364a560586a6) 获取最新代码。


|**主要更新** |**具体内容** |**说明** |
|---|---|---|
|新功能 |新增 ABR 能力 |VideoOne 现已支持视频播放的自适应码率流（ABR）。您可在所有 VoD 演示的新设置页面启用此功能，自动根据网络状况调整视频质量。 |
|优化 |SDK 版本升级 |基础媒体 SDK 版本已升级至最新，以提升性能与可靠性。 |
||移除 KTV 演示 |本版本已移除在线 KTV 场景。 |
||缺陷修复 |修复了若干已知问题，提升应用稳定性。 |


<span id="1fbd88ba"></span>
## 5.2.0

发布日期：2025/09/02


|**主要更新** |**具体内容** |**说明** |
|---|---|---|
|通用更新 |证书更新 |iOS 与 Android 的 Effect SDK 证书已更新。 |
|平台优化 |iOS \- 依赖变更 |TTSDK 的依赖方式已由静态库变更为动态库。此举有助于减小应用安装包体积，并可能提升性能。 |
||Android \- 合规性更新 |为符合最新标准，我们进行了如下调整：<br><br><br>* 已禁用对非必要传感器信息的收集。<br><br>* 移除了 MediaLive 的强制权限及不必要的读写权限，以更好地保护用户隐私。<br><br>* 修复了若干已知问题，提升了应用的整体稳定性和用户体验。 |


<span id="b60dd40e"></span>
## 5.0.0

发布日期：2025/01/17


|**关键更新** |**具体内容** |**描述** |
|---|---|---|
|新增场景并设有独立入口 |* 短剧 |VideoOne 发布了新版本，提供专为短剧定制的全套云端解决方案。 |


<span id="37ddf50f"></span>
## 4.0.1

发布日期：2024/12/26


|**关键更新** |**具体内容** |**描述** |
|---|---|---|
|新增场景并设有独立入口 |* 媒体上下滑动切换 |VideoOne 发布了新版本，支持视频与直播的组合播放。同时支持仅包含视频或仅包含直播的播放列表，并允许用户通过上下滑动切换媒体内容。 |
|TTSDK 版本升级 |* iOS: 1.41.300.203\-rtc —\> 1.43.300.2\-premium<br><br>* Android: 1.41.300.201\-rtc —\> 1.43.300.3 |您也可以参考[客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN)，以获取 VideoOne 所用各媒体 SDK 的**最新版本**。 |


<span id="e758678f"></span>
## 3.3.0

发布日期：2024/07/26


|**关键更新** |**具体内容** |**描述** |
|---|---|---|
|新增功能并设有独立入口 |* 首页用户界面优化<br><br>* RTC API 示例<br><br>* 合唱功能 |本次发布为在线 KTV 方案新增了合唱场景，提供了 RTC API 示例的接入指引，并优化了首页用户界面。 |
|TTSDK 版本升级 |* iOS: 1.40.200.5\-premium —\> 1.41.300.203\-rtc<br><br>* Android: 1.39.100.9.onekit —\> 1.41.300.201\-rtc |您也可以参考[客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN)，以获取 VideoOne 所用各媒体 SDK 的**最新版本**。 |


<span id="e9f89b4f"></span>
## 3.1.0

发布日期：2024/05/23


|**关键更新** |**具体内容** |**描述** |
|---|---|---|
|新增功能并设有独立入口 |* 直播推流<br><br>* 直播拉流 |本次发布新增了一个演示，展示如何通过不同来源发起直播，包括摄像头采集流、屏幕共享流、本地或在线视频文件及音频流。同时提供了推流和拉流的附加设置，帮助您快速实现项目中的直播推送与观看功能。<br><br>实现方式请参考[直播流](https://docs.byteplus.com/docs/byteplus-vos/docs-live-streaming-zh-CN)。 |


<span id="80846653"></span>
## 3.0.0

发布日期：2024/03/22

本次发布新增了 **在线 KTV** 场景的解决方案。您可以[安装应用](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-CN)进行试用，或参考[集成指南](https://docs.byteplus.com/docs/byteplus-vos/docs-online-ktv-solution-overview-zh-CN)在您的应用中实现该场景。

<span id="d4b47464"></span>
## 2.4.0

发布日期：2024/01/31


|**关键更新** |**具体内容** |**描述** |
|---|---|---|
|**TTSDK** 版本升级 |* iOS: 1.37.200.5\-premium —\> 1.40.200.5\-premium<br><br>* Android: 1.37.200.6.onekit —\> 1.39.100.9.onekit |本次升级对部分 API 进行了调整，尤其涉及互动直播方案相关内容。如果您已将 VideoOne 集成至项目中用于搭建互动直播场景，请务必根据新版本更新代码。请参考以下文档中提供的最新示例代码，完成必要修改，确保项目正常运行：<br><br><br>* iOS: [在 iOS 上实现互动直播](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-interactive-live-for-ios-zh-CN)<br><br>* Android: [在 Android 上实现互动直播](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-interactive-live-for-android-zh-CN)<br><br><br>您也可以参考[客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN)，以获取 VideoOne 所用各媒体 SDK 的**最新版本**。 |
|**新增功能**并设有独立入口 |新增功能：<br><br><br>* 常用播放器功能，包括手势控制、画中画等。<br><br>* 视频播放列表<br><br>* 智能多语种字幕<br><br>* 防录屏功能 |在本次发布中，我们精心整理并展示了在主流音视频场景中常用的关键功能演示。<br><br>您可以通过点击演示应用底部导航栏中新增加的“**功能**”标签体验这些功能，或在开源项目中探索其实现方式。 |


<span id="dd873133"></span>
## 2.3.0

发布日期：2023/12/07

本版本为演示应用的 **视频播放与编辑**场景新增以下功能。


1. 短视频沉浸式播放模式现已支持横屏视频播放，并可切换至全屏播放。

2. 在所有类型视频的全屏播放页面，支持观众互动，如点赞和评论。

3. 中长视频半屏播放页面现新增推荐视频列表。

4. 支持自定义媒体源的播放。详情请参阅[自定义媒体源播放](https://docs.byteplus.com/docs/byteplus-vos/docs-custom-media-source-playback-zh-CN)文档。


<span id="3ee7537d"></span>
## 2.0.0

发布日期：2023/11/10


|**功能** |**类型** |**描述** |**相关文档** |
|---|---|---|---|
|视频播放与编辑 |新增 |演示应用已更新，包含视频播放与编辑演示。演示中重点展示以下功能：<br><br><br>* 视频播放<br><br>* 视频拍摄与多轨编辑<br><br>* 媒体上传 |* [试用 Demo 应用](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-CN)<br><br>* [方案概述](https://docs.byteplus.com/docs/byteplus-vos/docs-video-playback-edit-solution-overview-zh-CN) |
|无 |文档更新 |新增了一篇文章。该文章全面列出了每个版本的 VideoOne 演示应用所集成的 SDK。按照本文中的版本组合进行集成，可有效避免不同 BytePlus SDK 之间的依赖冲突和兼容性问题。 |* [客户端 SDK 组件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-CN) |


<span id="00391e48"></span>
## 1.0.0

发布日期：2023/08/04

BytePlus Video One Solution（VideoOne）首次发布。


|**功能** |**类型** |**描述** |**相关文档** |
|---|---|---|---|
|BytePlus VideoOne 演示应用 |新增 |该开源演示应用集成了多种 BytePlus 媒体 SDK，并结合 BytePlus 视频云服务，针对行业场景提供演示。<br><br>演示应用重点展示以下功能：<br><br><br>* 直播推流与播放<br><br>* 联合直播，包括与观众或其他直播间主播（主播 PK 对战）<br><br>* 弹幕<br><br>* 礼物<br><br>* 直播间管理。 |* [试用 Demo 应用](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-CN)<br><br>* [方案概述](https://docs.byteplus.com/docs/byteplus-vos/docs-interactive-live-streaming-solution-overview-zh-CN) |
