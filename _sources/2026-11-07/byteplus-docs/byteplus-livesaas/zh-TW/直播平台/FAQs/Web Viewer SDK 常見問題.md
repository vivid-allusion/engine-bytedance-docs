---
title: "Web Viewer SDK 常見問題"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/web-viewer-sdk-chang-jian-wen-ti-zh-TW"
---

<span id="aa2a89d8"></span>
## 我可以直接覆蓋 `modules` 中的元素樣式嗎？

可以。Web Viewer SDK 的 DOM 層級及 `class` 屬性值不可更改。你可以在 `modules` 中按需覆蓋元素樣式。

<span id="0cf5bcc4"></span>
## Web Viewer SDK 是否支援預載相關功能，例如要求觀眾輸入正確邀請碼或在進入直播間前提交問卷？

不支援，Web Viewer SDK 的權限僅由使用者 token 決定。

<span id="74f082f5"></span>
## 如何取得使用者 token？


* 若 `mode` 的值為 `1`，可透過呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) 或前往 **Producer** \> **Page embedding** \> **Web SDK embedding**，在 [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) 的直播間頁面取得使用者 token。

* 若 `mode` 的值為 `2`，可透過呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) 取得使用者 token。


<span id="e9f203f8"></span>
## 使用者 token 有效期限多久？

使用者 token 不會過期。

<span id="6a025b97"></span>
## 為什麼我無法在本地播放預覽或回放？

只有將你的網域名稱加入 BytePlus Live 的 allowlist 後，才能播放預覽和回放。若使用本地除錯的網域名稱 `localhost`，將無法播放預覽或回放。

<span id="05511e4b"></span>
## 部署 Web 應用後，若 SDK 初始化失敗且 `apiservice/sdkinit` 介面報錯，該怎麼處理？

Web Viewer SDK 的 API 不支援跨網域呼叫。請聯繫 BytePlus Live 技術支援，將你的網域名稱加入 BytePlus Live 的 allowlist。

<span id="45c57a46"></span>
## 進入直播間或切換菜單時，若行動裝置上的菜單長寬比例異常，該怎麼處理？

菜單的高度與寬度會繼承其父元素。這表示你提供的容器存在問題。請勿將容器的高度與寬度設為動態值，例如 `auto` 或 `unset`。

<span id="c0c412bb"></span>
## 若 iPad 上的播放器出現黑屏，該怎麼處理？

播放器在 iPad 拉流時可能存在相容性問題。請在業務程式碼中使用 `const isMobile = /(ipad|iphone|ipod|windows phone|android)/i.test(navigator.userAgent)`，檢查載入的 SDK 腳本是否與瀏覽器的使用者代理（UA）相符。針對 iPad，必須匯入行動裝置資源，而非 PC 資源。
