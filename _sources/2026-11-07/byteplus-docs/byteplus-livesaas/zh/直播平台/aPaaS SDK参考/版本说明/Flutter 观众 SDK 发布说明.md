---
title: "Flutter 观众 SDK 发布说明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-building-viewer-sdk-for-flutter-zh-CN"
---

Flutter 观众 SDK 持续进行新功能、改进和兼容性调整的更新。本发布说明提供所有更新的详细、按时间顺序记录，帮助您及时了解信息并有效规划开发与集成。

<span id="89cb2ead"></span>
## 2025年11月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-11\-12 |1.65.0\-1 |**新功能**<br><br>新增在直播间显示自定义 Flutter 组件的支持。更多信息，请参见 [创建用于展示 Flutter 组件的直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-flutter-zh-CN#2cfaa0a8)。 |


<span id="47f10b1d"></span>
## 2025年6月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-07\-15 |1.60.0 |* **兼容性变更**<br><br>   iOS 依赖项已不再需要。更多信息，请参见 [iOS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-flutter-zh-CN#08ea213e)。<br><br>* **改进**<br><br>   优化了直播抽奖功能的 UI，提升用户体验。本次更新在抽奖对话框中新增奖品图片展示。 |
|2025\-06\-23 |1.58.0\-1 |* **兼容性变更**<br><br>   在添加 iOS 依赖项时，删除了 `pod 'RangersAppLog', :podspec => ' https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/RangersAppLog/6.16.2/RangersAppLog.podspec.json'` 和 `pod 'TTNetworkManager', :podspec => ' https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/TTNetworkManager/4.1.127.42/TTNetworkManager.podspec'`。更多信息，请参见 [iOS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-flutter-zh-CN#08ea213e)。<br><br>* **新功能**<br><br>   * 新增启用或禁用自动播放功能的选项。更多信息，请参见 [自动播放](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-flutter-zh-CN#2519a643)。<br><br>   * 新增画中画功能支持。现在可启用或禁用画中画。更多信息，请参见 [画中画](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-flutter-zh-CN#5d59daf1)。 |


<span id="6ed40f20"></span>
## 2024年11月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-11\-29 |1.0.0 |这是 Flutter 观众 SDK 的首次发布。主要功能包括：更多信息，请参见 [功能实现](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-flutter-zh-CN)。<br><br><br>* 加入直播间<br><br>* 离开直播间<br><br>* 在商品卡片和广告中加载内嵌链接<br><br>* 设置直播间状态回调 |
