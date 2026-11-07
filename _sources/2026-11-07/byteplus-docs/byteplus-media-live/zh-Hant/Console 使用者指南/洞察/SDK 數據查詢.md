---
title: "SDK 數據查詢"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-clientdata-zh-TW"
---

要監控您的直播內容品質表現，可在 MediaLive 控制台使用 SDK 數據查詢功能。本主題說明如何查看及篩選推流與拉流的指標數據，並詳細介紹關鍵品質指標，包括播放成功率、首幀延遲及視頻卡頓。

<span id="cbfcf895"></span>
## 操作流程


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導航欄選擇 **洞察** ＞ **SDK 數據查詢**，預設進入 **全部推流**分頁的**SDK 數據查詢**頁面。

3. 可於指定時間範圍內，切換分頁查看**全部推流**、**單路推流**、**全部拉流**及**單路拉流**的數據。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在 SDK 數據查詢頁面，您可使用以下功能細化查詢結果。</div>



* <div data-tips="true" data-tips-type="tip">指定應用類型：目前僅可查看客戶端 SDK 數據。</div>


* <div data-tips="true" data-tips-type="tip">指定應用：查看指定應用或全部應用的 SDK 指標數據。預設顯示全部應用。</div>


* <div data-tips="true" data-tips-type="tip">指定時間：可快速選擇查詢時間或手動指定時間區間。</div>


* <div data-tips="true" data-tips-type="tip">數據拆分：將顯示的數據拆分為最多三個維度。預設不進行數據拆分。</div>


* <div data-tips="true" data-tips-type="tip">數據聚合：選擇數據聚合的時間粒度。</div>


* <div data-tips="true" data-tips-type="tip">指定指標：查看指定指標或全部指標的數據。</div>


* <div data-tips="true" data-tips-type="tip">條件篩選：根據特定值（如等於或不等於某值）篩選數據。</div>



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">當 SDK 版本非最新時，某些項目可能出現數據丟失問題，導致數據看板出現異常值。如遇此情況，可嘗試更新 SDK 版本。</div>


<span id="d37e31f2"></span>
## 指標說明

<span id="de270f9e"></span>
### SDK 日誌上報時機

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57854bdc6ecc499b8969dc6cf8f31983~tplv-goo7wpa0wc-image.image) </span>


* 首次設置 URL 並調用播放方法，視為一次播放事件。在此過程中，每次播放僅記錄並上報一條事件追蹤日誌。

* 用戶在啟動階段及播放階段停止播放（調用停止方法）時，會上報播放成功日誌。


<span id="bedcc3ec"></span>
### 關鍵品質指標


|流類型 |指標 |說明 |
|---|---|---|
|推流 |平均碼率 |顯示全部推流（或單路推流）在數據聚合時間粒度下的平均碼率趨勢圖，以及查詢時間內的平均碼率。 |
||平均幀率 |顯示全部推流（或單路推流）在數據聚合時間粒度下的平均幀率趨勢圖，以及查詢時間內的平均幀率。 |
|拉流 |播放成功率 |在觀眾設備上成功接收並播放的直播流比例。此指標衡量觀眾成功拉流的概率。<br><br>**計算方法**：播放成功率 =（成功播放次數 / 播放總次數）x 100%。 |
||平均首幀延遲 |用戶點擊播放按鈕至螢幕顯示首個視頻畫面的時間。此指標衡量觀眾等待影片開始播放的時間。<br><br>**計算方法**：首幀延遲 = 首幀播放時間戳 \- 使用者點擊播放按鈕時間戳。 |
||每100秒的影片卡頓時間 |直播期間，每100秒播放時影片渲染卡頓的總時長。此指標用於衡量播放過程中卡頓的嚴重程度。<br><br>**計算方法**：每100秒的影片卡頓時間＝播放過程中的影片卡頓時間／播放時長 x 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">影片卡頓的定義：若兩個連續渲染的影片幀之間的間隔大於200毫秒，則計為一次卡頓。該時間會累加至卡頓總時長。持續監控並優化此指標可提升播放流暢度與用戶體驗。</div><br> |
||平均位元率 |展示所有拉流（或單一拉流）在資料聚合時間粒度下的平均位元率趨勢圖，以及查詢時間範圍內的平均位元率。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">為減少啟動階段位元率波動的影響，拉流位元率的統計範圍排除播放開始後的前5秒。</div><br> |
||端到端延遲 |伺服器完成編碼後推流至觀眾螢幕上渲染首個影片幀的時間。此指標衡量觀眾開始觀看直播所需的等待時間。<br><br>**計算方法**：端到端延遲＝AVG（首幀完成渲染時間戳－編碼完成後實際推流時間戳） |
||平均播放時長 |展示所有拉流（或單一拉流）在資料聚合時間粒度下的平均播放時長趨勢圖，以及查詢時間範圍內的平均播放時長。 |
