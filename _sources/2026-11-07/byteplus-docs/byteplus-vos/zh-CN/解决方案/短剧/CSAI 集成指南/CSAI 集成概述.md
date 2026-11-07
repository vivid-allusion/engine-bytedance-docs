---
title: "CSAI 集成概述"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/csai-integration-overview-zh-CN"
---

本指南全面介绍了基于 VideoOne 的短剧应用的客户端广告插入（CSAI）解决方案。通过集成 BytePlus MediaAds SDK 和 Google IMA SDK，您可以通过片中广告实现内容变现，既可选择与付费墙/解锁模式互为替代，也可单独使用。

<span id="fb9bc419"></span>
## 主要特性


* **多样化广告格式**：支持片头、片中和片尾广告。

* **灵活排期**：可通过 VAST 标签 URL 和精确时间偏移配置广告。

* **播放器无关**：兼容 `TTVideoEngine` 及通过 `ContentPlayer` 接口的自定义播放器。

* **无缝体验**：自动管理内容的暂停/恢复及广告跳过逻辑。

* **防跳过**：当用户快进越过一个或多个广告点时，自动播放最近一次错过的广告，防止有意跳过广告。

* **频次控制**：确保每个片中广告位在每次会话中仅触发一次，优化用户体验。


<span id="aa76cfc7"></span>
## 变现规则


* **剧集级别**：单个剧集可选择 **付费墙/解锁**模式 **或**片中广告模式，但不可同时使用。

* **应用级别**：您可以在同一应用内为不同剧集配置不同的变现模式。


<span id="43918d44"></span>
## 体验演示

下载最新版 [VideoOne Demo](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-CN)（v5.4.0 及以上），亲身体验片中广告能力。

<span id="e2257056"></span>
## 集成指南

请选择您的平台以开始集成：


* [Android 平台 CSAI 集成](https://docs.byteplus.com/docs/byteplus-vos/csai-integration-for-android-zh-CN)

* [iOS 平台的 CSAI 集成](https://docs.byteplus.com/docs/byteplus-vos/csai-integration-for-ios-zh-CN)
