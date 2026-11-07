---
title: "推流（以 OBS 為例）"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tui-liu-yi-obs-wei-li-zh-TW"
---

你可以將第三方直播工具的流推送到 BytePlus Live 的直播間。此處以 Open Broadcaster Software（OBS）為例。

<span id="380dceb6"></span>
## 背景

[OBS](https://obsproject.com/) 是一款適用於 Windows、macOS 和 Linux 的免費開源軟體，可用於錄製影片和直播。如需更多資訊，請參閱 [OBS 使用者指南](https://obsproject.com/help)。

<span id="d5511941"></span>
## 先決條件


* 點擊 [此處](https://obsproject.com/download)下載並安裝 OBS。

* 請確保你的電腦符合 OBS 的相應系統需求。如需更多資訊，請參閱 [系統需求](https://obsproject.com/kb/system-requirements)。


<span id="e3144fe9"></span>
## 操作流程

<span id="733e0d7a"></span>
### Step 1: 設定 OBS，將你的直播流推送到 BytePlus Live 的直播間


1. 登入 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播間列表中，點擊開啟一個直播間。

3. 在 **直播控制**頁面，於播放器下方的 **直播方式**分頁中點擊 **推流**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ca0e9561ea049e98ea5663b383078d0~tplv-goo7wpa0wc-image.image) </span>

4. 複製伺服器 URL 和串流金鑰。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">請妥善保管你的伺服器 URL 和串流金鑰。任何擁有伺服器 URL 和串流金鑰的人都能將直播內容推送到你的直播間。   </div>
   

5. 開啟你的 OBS，並在左上角點擊 **檔案** \> **設定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08fa3af089314917b7f3eb826da39c7b~tplv-goo7wpa0wc-image.image) </span>

6. 在 **設定**對話框中，於左側導覽窗格點擊 **串流**，並從 **服務**下拉清單中選擇 **自訂...** 從 **服務**下拉清單中選擇。

7. 將第 4 步複製的伺服器 URL 和串流金鑰分別輸入至 **伺服器** 和 **串流金鑰**欄位，然後點擊 **確定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a31253b2bba406a80eebfe44471e1a9~tplv-goo7wpa0wc-image.image) </span>

8. （可選）若啟用超低延遲功能，請完成以下設定，以確保觀眾能以超低延遲觀看直播，然後點擊 **確定**。如需瞭解如何啟用超低延遲功能，請參閱 [超低延遲直播](https://docs.byteplus.com/docs/byteplus-livesaas/chao-di-yan-chi-zhi-bo-zh-TW)。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bb73794258f45958dbcac83c27a8b89~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">較高的位元率需要更多的上行頻寬。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">你必須將 <strong>關鍵幀間隔</strong>設為 1 秒或 2 秒。   </div>
   


<span id="e444c779"></span>
### Step 2: 新增來源

新增你希望觀眾在直播期間觀看的來源。本範例將新增「顯示擷取」來源以串流你的螢幕畫面。


1. 在 OBS 底部的 **來源**區域點擊 +。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ead6c723b104c2094165a6c7c1dd8aa~tplv-goo7wpa0wc-image.image) </span>

2. 從下拉清單中選擇 **顯示擷取**。

3. 輸入名稱，並在出現的 **建立/選擇來源**對話框中點擊 **確定**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69b7048f31854fd3a42673b6167b63e4~tplv-goo7wpa0wc-image.image) </span>

4. （可選）在出現的對話框中，根據需求調整設定，例如是否擷取滑鼠游標。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd1789c442c5434d86fa70047dd20c08~tplv-goo7wpa0wc-image.image) </span>

5. 點擊 **確定**。


<span id="1fd2dcd6"></span>
### Step 3: 開始直播


1. 在 OBS 右下角點擊 **開始串流**以開始直播。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07085d4f62d94829a1996dd3239fad74~tplv-goo7wpa0wc-image.image) </span>

2. 觀眾即可在 BytePlus Live 的觀看頁面觀看你的直播內容。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">從 OBS 推流到 BytePlus Live 直播間可能會產生部分延遲。   </div>
