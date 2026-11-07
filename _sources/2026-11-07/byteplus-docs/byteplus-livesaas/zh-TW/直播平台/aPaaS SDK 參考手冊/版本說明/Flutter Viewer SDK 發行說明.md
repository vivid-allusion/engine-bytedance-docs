---
title: "Flutter Viewer SDK 發行說明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/flutter-viewer-sdk-fa-xing-shuo-ming-zh-TW"
---

Flutter Viewer SDK 持續推出新功能、改進及相容性調整。本發行說明提供所有更新的詳細時間順序記錄，協助您隨時掌握資訊並有效規劃開發與整合。

<span id="89cb2ead"></span>
## 2025 年 11 月


|發行日期 |版本 |說明 |
|---|---|---|
|2025\-11\-12 |1.65.0\-1 |**新功能**<br><br>新增在直播間顯示自訂 Flutter widget 的支援。如需更多資訊，請參閱 [Creating live room for displaying Flutter widgets](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#2cfaa0a8)。 |


<span id="47f10b1d"></span>
## 2025 年 6 月


|發行日期 |版本 |說明 |
|---|---|---|
|2025\-07\-15 |1.60.0 |* **相容性變更**<br><br>   iOS 依賴項目已不再需要。如需更多資訊，請參閱 [iOS](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-flutter#08ea213e)。<br><br>* **改進**<br><br>   優化直播抽獎功能的 UI，以提升使用者體驗。本次更新包含在抽獎對話框中顯示獎品圖片。 |
|2025\-06\-23 |1.58.0\-1 |* **相容性變更**<br><br>   新增 iOS 依賴項時，已刪除 `pod 'RangersAppLog', :podspec => ' https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/RangersAppLog/6.16.2/RangersAppLog.podspec.json'` 及 `pod 'TTNetworkManager', :podspec => ' https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/TTNetworkManager/4.1.127.42/TTNetworkManager.podspec'`。如需更多資訊，請參閱 [iOS](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-flutter#08ea213e)。<br><br>* **新功能**<br><br>   * 新增可啟用或停用自動播放功能的選項。如需更多資訊，請參閱 [Autoplay](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#2519a643)。<br><br>   * 新增支援畫中畫（PiP）功能。您現在可以啟用或停用 PiP。如需更多資訊，請參閱 [PiP](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#5d59daf1)。 |


<span id="6ed40f20"></span>
## 2024 年 11 月


|發行日期 |版本 |說明 |
|---|---|---|
|2024\-11\-29 |1.0.0 |這是 Flutter Viewer SDK 的首次發行。主要功能包括：如需更多資訊，請參閱 [Feature implementation](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation)。<br><br><br>* 加入直播間<br><br>* 離開直播間<br><br>* 在商品卡片及廣告中載入嵌入連結<br><br>* 設定直播間狀態回呼 |
