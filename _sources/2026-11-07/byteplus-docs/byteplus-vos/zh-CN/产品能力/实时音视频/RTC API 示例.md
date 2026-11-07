---
title: "RTC API 示例"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/doc-rtc-api-examples-zh-CN"
---

本文档简要介绍 VideoOne 如何利用 BytePlus RTC SDK 实现高级功能。旨在帮助用户高效配置 RTC 的高级功能。

<span id="a361cd61"></span>
# RTC 集成指南

<span id="586de8d7"></span>
## 前提条件

已开通 [BytePlus RTC ](https://console.byteplus.com/rtc/workplaceRTC)服务的有效 BytePlus 账号。请参阅 [使用 RTC 服务前 ](https://docs.byteplus.com/en/byteplus-rtc/docs/69865)获取详细操作说明。

<span id="11630b9b"></span>
## 功能实现

VideoOne 展示如何使用 BytePlus RTC SDK 实现高级功能。目前支持以下类别：核心功能、房间管理、音视频传输、音频管理、视频管理、消息管理及其他组件。有关这些功能实现的更多细节，请参考以下文档：


|**类别** |**功能** |**参考文档** |
|---|---|---|
|核心功能 |快速开始 |[BytePlus RTC：快速开始指南](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70123) |
|房间管理 |多房间 |[BytePlus RTC：加入多个 RTC 房间](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-196844) |
|音视频传输 |跨房间对战 |[BytePlus RTC：跨房间转发媒体流](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104398) |
|音频管理 |原始音频数据 |[BytePlus RTC：获取原始音频数据](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178324) |
||音效混音 |[BytePlus RTC：播放音效文件](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178326) |
||音乐混音 |[BytePlus RTC：播放音乐文件](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70141) |
||音效 |[BytePlus RTC：音效与降噪](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178327) |
|视频管理 |画中画 |[BytePlus RTC：支持移动端前台多任务](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178325) |
||视频配置 |[BytePlus RTC：设置视频编码配置](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70122) |
||视频旋转 |[BytePlus RTC：视频旋转](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-106458) |
|其他组件 |BytePlus Effects |[BytePlus RTC：视频特效（付费功能）](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717) |
||推流至 CDN |[BytePlus RTC：推流至 CDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69817) |
|消息管理 |SEI 消息 |[BytePlus RTC：补充增强信息（SEI）](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70140) |
||消息与帧同步 ||


参考开源代码，将这些功能集成到您的应用：


* [iOS：RTCAPIExample](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample)

* [Android：RTCAPIExample](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/rtc-api-example)
